---
# required metadata

title: Considerazioni su utenti e dispositivi
description:
keywords:
author: YuriDio
manager: swadhwa
ms.date: 04/28/2016
ms.topic: article
ms.prod:
ms.service:
ms.technology:
ms.assetid: d1653116-3922-40d3-bc4f-3d845b6aaecb

# optional metadataco

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: 
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Considerazioni su utenti e dispositivi

Il primo problema relativo a utenti e dispositivi da affrontare è come le tecnologie esistenti influiranno sull'esperienza utente per l'accesso sicuro alle risorse aziendali. Indirizzare l'esperienza utente in diversi dispositivi può essere difficile, non solo da un punto di vista della sicurezza, ma anche dal punto di vista dello sviluppo delle app. Il canale di comunicazione tra il dispositivo e le risorse aziendali deve essere valutato in base al livello di sicurezza di rete appropriato necessario per evitare la perdita di dati durane il trasferimento.

Le sezioni seguenti sono basate sui componenti per il sottodominio Utenti e dispositivi illustrato nella sezione [Problem Definition](byod-design-considerations-guide.md#problem-definition) (Definizione del problema) di questa guida, contenente il diagramma concettuale per il dominio del problema BYOD.

## Profiles

Per la progettazione di una soluzione di infrastruttura BYOD è fondamentale comprendere i requisiti e le esigenze degli utenti per svolgere il lavoro dai dispositivi scelti. Non tutti gli utenti avranno gli stessi requisiti; alcuni utenti accederanno ai dati sempre in locale e l'applicazione dei criteri per questi utenti può essere diversa. Gli utenti remoti accederanno ai dati aziendali da varie posizioni e in circostanze diverse. Valutare le opzioni disponibili per soddisfare queste esigenze. Stabilire un profilo utente a seconda delle esigenze:

- Devono accedere solo alle app?
- Devono accedere alle cartelle che si trovano in un file server?

Anche se nella tabella seguente è indicato un set di requisiti per ogni profilo utente, è possibile personalizzare la tabella aggiungendo o rimuovendo i requisiti in base alle esigenze dell'azienda. La base logica di ogni categoria di profilo rispetto a ciò che deve contenere si fonda sulle risorse che utilizza. Ad esempio, il profilo leggero indica un utilizzo limitato delle risorse nel dispositivo e requisiti di rete minimi. Assicurarsi di comprendere l'impatto di ogni profilo utente. In questo modo, sarà possibile effettuare scelte più appropriate nel resto del processo di progettazione.

I profili utente proposti in questa guida sono:

- **Chiaro**
    - Accesso alle app basate su Web in locale o nel cloud
    - Accesso alle app aziendali per dispositivi mobili
- **Moderato**
    - Accesso alle app basate su Web in locale o nel cloud
    - Accesso alle app aziendali per dispositivi mobili
    - Accesso alle app aziendali virtualizzate
    - Accesso ai file che si trovano nei file server locali
    - Accesso ai file che si trovano nel cloud
- **Pesante**
    - Accesso alle app basate su Web in locale o nel cloud
    - Accesso alle app aziendali per dispositivi mobili
    - Accesso ai file che si trovano nei file server locali
    - Accesso ai file che si trovano nel cloud
    - Accesso ai computer con Desktop remoto
    - Accesso ad altri computer locali

Sarà necessario stabilire quale profilo utente è più adatto per la soluzione di infrastruttura BYOD. Si potrebbe valutare la possibilità di creare più profili utente a seconda delle relative esigenze lavorative. Idealmente, la tecnologia usata per implementare la soluzione di infrastruttura BYOD deve poter soddisfare tutti i profili utente, poiché le esigenze possono variare a seconda dell'utente. 

## Dispositivi

Il reparto IT deve determinare se è necessaria la conoscenza dei dispositivi. Ad esempio, uno scenario BYOD prevede che i dipendenti a ore controllino il foglio presenze o consultino le comunicazioni aziendali quando sono fuori ufficio. In molte organizzazioni, questi requisiti erano tradizionalmente servizi solo per LAN, mentre ora possono essere estesi ai dispositivi personali. A un utente che verifica la pianificazione è necessaria la gestione dei dispositivi? Comprendere il footprint dei dispositivi consente al reparto IT di:

- Tenere traccia dell'utente che registra i dispositivi: un utente che registra diversi dispositivi ogni settimana potrebbe indicare un'attività sospetta.
- Comprendere i footprint dei dispositivi: conoscere i tipi di dispositivi usati nella rete consente al reparto IT di fornire il supporto necessario.

Valutare la possibilità di creare un collegamento tra il dispositivo e l'utente, archiviato in una posizione centrale che in seguito possa essere usato dal reparto IT per il controllo o la creazione di rapporti. Per abilitare il BYOD il reparto IT deve passare da uno stato di dispositivi sconosciuti a uno stato di dispositivi noti. In questo modo il reparto IT avrà un maggiore controllo dei dispositivi appartenenti all'azienda. In genere, le aziende affrontano questa esigenza in tre modi diversi:

- Approccio 1: Installazione di un agente di gestione in ogni dispositivo dell'utente.
- Approccio 2: Registrazione di ogni dispositivo in un repository centrale senza installare un agente di gestione.
- Approccio 3 (1+2): Registrazione e installazione di un agente di gestione in ogni dispositivo dell'utente.


### Opzioni per il passaggio dello stato dei dispositivi da sconosciuti a noti: vantaggi e svantaggi

Usare l'elenco che segue per comprendere i vantaggi e gli svantaggi delle opzioni per il passaggio dello stato dei dispositivi da sconosciuti a noti:

- Installazione di un agente di gestione in ogni dispositivo dell'utente
    - Vantaggi
        - Maggiore controllo dei dispositivi degli utenti
        - Funzionalità di cancellazione remota
        - Funzionalità di distribuzione delle app
        - Più controlli di sicurezza a disposizione del reparto IT per controllare il dispositivo
    - Svantaggi
        - Gli utenti devono installare un agente di gestione
        - L'agente di gestione deve poter essere installato su piattaforme dei dispositivi diverse
        - Maggiore sovraccarico amministrativo
- Registrazione di ogni dispositivo in un repository centrale senza installare un agente di gestione
    - Vantaggi
        - Non è necessario un agente di gestione
        - Minore sovraccarico amministrativo
        - Autenticazione dei dispositivi a due fattori
        - Convalida del collegamento tra utenti e dispositivi
    - Svantaggi
        - Minore controllo dei dispositivi degli utenti
        - Meno controlli di sicurezza disponibili
        - Non sono disponibili le funzionalità di distribuzione delle app e cancellazione remota
- Registrazione e installazione di un agente di gestione in ogni dispositivo dell'utente
    - Vantaggi
        - Maggiore controllo dei dispositivi degli utenti
        - Funzionalità di cancellazione remota
        - Funzionalità di distribuzione delle app
        - Più controlli di sicurezza
        - Autenticazione dei dispositivi a due fattori
        - Convalida del collegamento tra utenti e dispositivi
    - Svantaggi
        - Gli utenti devono installare un agente di gestione
        - L'agente di gestione deve poter essere installato su piattaforme dei dispositivi diverse
        - Maggiore sovraccarico amministrativo

In Windows Server 2012 R2 il nuovo concetto di [aggiunta all'area di lavoro](https://technet.microsoft.com/library/dn280945.aspx) consente al reparto IT di cambiare lo stato del dispositivo da sconosciuto a noto. Il dispositivo può anche essere usato come autenticazione a due fattori e Single Sign-On per le risorse e le app dell'area di lavoro. L'aggiunta all'area di lavoro è disponibile in modo nativo in Windows 10, ma è supportata anche in altre piattaforme come iOS e Android. L'aggiunta all'area di lavoro sfrutta il servizio DRS (Device Registration). Per altre informazioni su DRS, vedere [Configurare un server federativo con Device Registration Service](https://technet.microsoft.com/library/dn486831.aspx). L'aggiunta all'area di lavoro è una nuova tecnologia e funziona con specifici casi di utilizzo. Per altre informazioni su una soluzione che sfrutti l'aggiunta all'area di lavoro con Single Sign-On, vedere [Accesso protetto alle risorse aziendali ovunque e con qualsiasi dispositivo](https://technet.microsoft.com/library/dn550982.aspx).

Se si prevede di usare DRS, tenere presente che questa funzione non fornisce funzionalità di gestione. Se l'azienda necessita di più controlli di sicurezza per avere a disposizione più opzioni per controllare i dispositivi degli utenti, è consigliabile usare DRS insieme alla [registrazione dei dispositivi mobili](https://technet.microsoft.com/library/jj733620.aspx) come soluzione di agente di gestione. Se si sceglie questa opzione, tuttavia è necessario avere una sottoscrizione a Windows Intune. Per altre informazioni su Microsoft Intune, vedere [Introduction to Intune](/intune/understand-explore/introduction-to-microsoft-intune) (Introduzione a Intune).

## Rete

Prendere in esame l'accesso alla rete aziendale dal punto di vista dell'utente e da quello del dispositivo. Come possono gli utenti accedere dati aziendali dai propri dispositivi? La maggior parte delle soluzioni di infrastruttura BYOD è concentrata solo minimamente sull'accesso remoto dai dispositivi degli utenti. Tuttavia, da un approccio incentrato sugli utenti, è necessario considerare dove si trovano fisicamente gli utenti. È consigliabile concentrarsi non solo sull'accesso remoto, ma anche sul modo in cui gli utenti potranno accedere ai dati in locale. Inoltre, sarà necessario prendere in considerazione i problemi normativi specifici dell'allineamento geopolitico dell'organizzazione. Ad esempio, come si può consentire agli utenti che si trovano fisicamente in un altro paese o in un'altra area l'accesso personalizzato alla rete?

Se l'azienda ha delle risorse nel cloud pubblico accessibile tramite Internet dai dispositivi degli utenti, è necessario considerare il modo in cui viene gestito il traffico. Valutare la possibilità di usare la crittografia durante il trasferimento dei dati dai dispositivi degli utenti al provider dei servizi cloud. È consigliabile usare la crittografia dei dati anche quando gli utenti accedono alle risorse interne.

### Opzioni di connettività di rete: vantaggi e svantaggi

Usare l'elenco che segue per comprendere i vantaggi e gli svantaggi delle opzioni di connettività:

- VPN tradizionale
    - Vantaggi
        - Tecnologia avanzata
        - Facile da configurare
        - Ampiamente disponibile in molte piattaforme
    - Svantaggi
        - Overhead del protocollo dai protocolli VPN e di crittografia
        - Deve essere avviata prima di avviare le app
        - Richiede l'interazione dell'utente per stabilire la connessione
- Accesso diretto Microsoft
    - Vantaggi
        - Accesso facilitato per gli utenti (sempre attivo)
        - Supporta l'accesso al server selezionato e l'autenticazione IPsec con un server di rete Internet
        - Supporta la crittografia e l'autenticazione end-to-end
    - Svantaggi
        - Richiede un'infrastruttura locale per supportare questa funzionalità
        - La risoluzione dei problemi può risultare complessa
        - Maggiore sovraccarico amministrativo
        - Non disponibile in tutte le piattaforme
- VPN ad attivazione automatica
    - Vantaggi
        - Facile da configurare
        - La connessione al server locale viene avviata quando un'app richiede l'accesso alle risorse aziendali
    - Svantaggi
        - Overhead del protocollo dai protocolli VPN e di crittografia
        - Non disponibile in tutte le piattaforme
- Desktop remoto con VDI
    - Vantaggi
        - Esperienza utente trasparente
        - Maggiore controllo del desktop (protezione avanzata)
        - Ampiamente disponibile in molte piattaforme
    - Svantaggi
        - Richiede un'infrastruttura locale per supportare questa funzionalità
        - La pianificazione della capacità di rete, archiviazione e calcolo deve essere eseguita attentamente per evitare di penalizzare le prestazioni
        - Ogni dispositivo richiede un'app client di accesso remoto
- Accesso Web
    - Vantaggi
        - Ampiamente disponibile in molte piattaforme
        - Crittografia disponibile usando HTTPS
        - Tecnologia avanzata
        - Facile da configurare
    - Svantaggi
        - Richiede certificati
        - Se l'infrastruttura di certificati è interna, è necessaria un'infrastruttura PKI
        - Richiede un'infrastruttura perimetrale per pubblicare le app in modo sicuro

Dopo aver definito la progettazione per l'accesso alla rete remota, valutare il modo in cui i dispositivi di proprietà dell'utente si connetteranno alla rete quando vengono connessi fisicamente alla rete. Gli utenti che portano i propri dispositivi nel posto di lavoro probabilmente useranno la funzionalità Wi-Fi per connettersi alle risorse aziendali. È consigliabile valutare la possibilità di usare la segmentazione della rete (fisica o logica) per i dispositivi degli utenti al fine di isolarli.

È anche possibile segmentare i dispositivi che si connetteranno alla rete Wi-Fi a seconda della piattaforma di esecuzione. Valutare inoltre come proteggere le comunicazioni e l'autorizzazione durante l'accesso in locale alle risorse aziendali.

È possibile scegliere una segmentazione fisica sul punto di accesso wireless e sui componenti di rete (commutatori e router) per isolare gli utenti che si connettono con i propri dispositivi. È anche possibile implementare questo tipo di segmentazione usando i [profili Wi-Fi in Configuration Manager](https://technet.microsoft.com/library/dn261221.aspx). È disponibile una vasta gamma di impostazioni di sicurezza, ad esempio certificati per la convalida del server e per l'autenticazione client di cui è stato eseguito il provisioning con i [profili certificati in Configuration Manager](https://technet.microsoft.com/library/dn270540.aspx)..


### Opzioni di segmentazione della rete Wi-Fi: vantaggi e svantaggi

Usare l'elenco che segue per comprendere i vantaggi e gli svantaggi delle opzioni di segmentazione della rete Wi-Fi:

- Segmentazione fisica
    - Vantaggi
        - Segmentazione della sicurezza di livello inferiore
        - Relativamente facile da configurare
        - Astrazione dalla piattaforma (sistema operativo)
    - Svantaggi
        - La gestibilità può variare in base al fornitore
        - L'integrazione tra diversi fornitori di hardware può essere complessa
        - Costi elevati di implementazione e gestione
- Segmentazione logica (profili Wi-Fi)
    - Vantaggi
        - Esperienza trasparente per gli utenti.
        - Più facile da gestire, rispetto alla segmentazione fisica
        - Costi di implementazione più bassi, rispetto alla segmentazione fisica
        - Astrazione dall'hardware usato per la connessione dei dispositivi
        - Supporta più piattaforme (sistemi operativi)
    - Svantaggi
        - Non offre la segmentazione della sicurezza di livello inferiore come la soluzione hardware
- Segmentazione dinamica
    - Vantaggi
        - I punti di accesso wireless usano un'infrastruttura e un SSID comuni
        - Gli attributi degli utenti finali e dei dispositivi eseguono il provisioning dell'accesso alla rete in modo dinamico
    - Svantaggi
        - Richiede IPsec per l'implementazione con la funzionalità [Protezione accesso alla rete Microsoft](https://technet.microsoft.com/library/cc731276(v=ws.10).aspx), che può rappresentare un problema in uno scenario BYOD che richiede il supporto per "qualsiasi dispositivo"

> [!NOTE] Per altre informazioni sui profili Wi-Fi in Configuration Manager, vedere [Introduzione ai profili Wi-Fi in Configuration Manager](https://technet.microsoft.com/library/dn261224.aspx)..

Il percorso di rete svolge un ruolo importante per le considerazioni sugli utenti e i dispositivi. È possibile sfruttare il controllo degli accessi a più fattori in ADFS per abilitare i criteri di autorizzazione per applicazione, con i quali è possibile consentire o negare l'accesso in base a utente, dispositivo e percorso di rete. Per altre informazioni su come configurare un ambiente per convalidare questa funzionalità, vedere [Gestire i rischi con il controllo degli accessi a più fattori](https://technet.microsoft.com/library/dn280936.aspx).



<!--HONumber=Apr16_HO4-->


