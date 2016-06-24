---
# required metadata

title: Determinare i requisiti di rete
description:
keywords:
author: andredm7
manager: swadhwa
ms.date: 05/31/2016
ms.topic: article
ms.prod:
ms.service:
ms.technology:
ms.assetid: 77e7cab9-2fae-4857-be5d-2b6f57e981be

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: 
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Determinare i requisiti di rete

>[!NOTE]
>Questo argomento fa parte di una guida più ampia dedicata alle considerazioni di progettazione. Per leggere la guida dall'inizio, vedere l'[argomento principale](mdm-design-considerations-guide.md). Per scaricare una copia della versione integrale della guida, visitare la raccolta [TechNet](https://gallery.technet.microsoft.com/Mobile-Device-Management-7d401582).

Garantire l'accesso sicuro e gestito a un'ampia gamma di risorse aziendali dai dispositivi mobili è un'importante funzione di una soluzione di gestione dei dispositivi mobili. Sebbene queste risorse si trovino solitamente su reti locali, è ora comune ospitare le risorse anche su servizi Web basati sul cloud e reti esterne.</para><para>La modalità di connessione dei dispositivi mobili alle piattaforme di posta elettronica aziendali, alle reti private virtuali (VPN) e alle reti wireless (Wi-Fi) aziendali svolge un ruolo importante nella prevenzione dell'accesso non autorizzato ai dati e ad altre risorse aziendali. È ugualmente importante fare in modo che l'accesso a queste risorse sia semplice e pratico per gli utenti di dispositivi mobili, per evitare che gli utenti cerchino un metodo più pratico ma non sicuro per l'archiviazione o l'accesso alle risorse.</para></content>


## Gestione della posta elettronica
La posta elettronica aziendale è in genere la risorsa dati primaria a cui la maggior parte degli utenti deve accedere su una rete aziendale, da un dispositivo mobile personale o di proprietà della società. L'accesso alla posta elettronica in genere rappresenta anche la connessione che avvia la registrazione iniziale del dispositivo mobile. Essere in grado di gestire l'accesso alla posta elettronica per i dispositivi mobili sia da parte della soluzione di gestione dei dispositivi non mobili esistente sia da parte della soluzione di gestione dei dispositivi mobili aiuta a evitare interruzioni nella copertura dei dispositivi e aumenta la protezione per i dati archiviati nei server di posta elettronica.

La maggior parte delle soluzioni di gestione dei dispositivi mobili offrono protezione per l'accesso alla posta elettronica tramite una o entrambe le funzionalità seguenti:

- **Profili di posta elettronica:** configurando e distribuendo i profili di posta elettronica, gli amministratori possono configurare automaticamente i dispositivi mobili con le informazioni sul server di posta elettronica appropriate, in modo che gli utenti possano collegarsi alle proprie cassette postali. Questo aiuta gli utenti a connettersi al server di posta elettronica corretto senza dover ricordare i nomi degli endpoint del server di posta elettronica o gli indirizzi di rete corretti. Inoltre, quando si rimuove un profilo di posta elettronica, gli amministratori possono rimuovere la posta elettronica dai dispositivi come parte del ripristino del dispositivo o del processo di cancellazione selettiva. La gestione dei profili di posta elettronica può essere una funzionalità della soluzione di gestione dei dispositivi non mobili o può essere integrata con una soluzione di gestione dei dispositivi mobili.
- **Accesso condizionale alla posta elettronica:** l'accesso condizionale, o "gestito", alla posta elettronica di solito è incentrato sulla sicurezza e sulla conformità per l'accesso alla posta elettronica su un dispositivo mobile anziché sull'endpoint a cui il dispositivo si connette. Con l'accesso alla posta elettronica condizionale, vengono definiti e assegnati criteri di conformità a singoli utenti o dispositivi o a gruppi di utenti e/o dispositivi. l criteri descrivono i prerequisiti che devono essere presenti prima che un dispositivo mobile possa connettersi a una risorsa di posta elettronica. Ad esempio, può essere necessario un PIN sul dispositivo. I criteri vengono solitamente applicati alla registrazione iniziale del dispositivo, ma rimangono attivi per tutta la durata della registrazione del dispositivo mobile nel sistema di gestione dei dispositivi mobili.

###Domande sulla pianificazione della gestione della posta elettronica

 Rispondere alle domande seguenti relative alla pianificazione della gestione della posta elettronica:

- In che modo i dispositivi mobili si connetteranno al sistema di posta elettronica locale o ospitato nel cloud esistente?
- Gli amministratori o gli utenti (o una combinazione di entrambi) saranno responsabili del collegamento dei dispositivi mobili al sistema di posta elettronica? Se gli utenti connettono i dispositivi mobili al sistema di posta elettronica, in che modo:
 - Sceglieranno il punto di connessione appropriato per accedere alla propria cassetta di posta elettronica?
 - Sceglieranno il metodo di connessione o il protocollo di connessione corretto?
- I dispositivi mobili dovranno soddisfare determinati standard di sicurezza e conformità prima e durante la connessione al sistema di posta elettronica?
- È necessario avere la possibilità di creare criteri di connessione per la sicurezza e la conformità della posta elettronica personalizzati? In tal caso, quali sono i requisiti specifici?
- È necessario avere la possibilità di importare o esportare i criteri di connessione per la sicurezza e la conformità della posta elettronica?
- In che modo è necessario gestire le connessioni al sistema di posta elettronica?
 - In base all'utente del dispositivo?
 - In base al tipo di dispositivo?
 - In base al sistema operativo del dispositivo?
 - In base al gruppo o al ruolo dell'utente?
- Quando un dispositivo mobile deve essere disconnesso dal sistema di posta elettronica, come verranno eliminati dal dispositivo mobile i dati della posta elettronica?
- Gli amministratori e gli utenti devono poter entrambi eliminare i dati della posta elettronica o la connessione al sistema di posta elettronica?
- Come verrà verificata o confermata l'eliminazione dei dati della posta elettronica?
- Se si usa sia un sistema di posta elettronica locale che un sistema basato sul cloud, come si integrano tali sistemi con la soluzione di gestione dei dispositivi mobili? 
- I profili di posta elettronica o i criteri di accesso gestito sono gestiti allo stesso modo o in modo diverso dal punto di vista dell'IT? L'esperienza di connessione alla posta elettronica dell'utente è la stessa o è diversa a seconda di dove è ospitata la cassetta postale?

## Gestione della connettività di rete

I dispositivi mobili solitamente si collegano alle reti e alle risorse aziendali usando le tecnologie di accesso seguenti:

- **Wi-Fi:** l'accesso wireless alle risorse aziendali è solitamente offerto come servizio di estensione della rete locale per i dispositivi con prossimità fisica alla rete locale. Questo solitamente comporta l'autorizzazione della connessione dei dispositivi mobili alle risorse di rete mentre gli utenti si spostano da una posizione all'altra nell'ufficio locale, ad esempio tra la sala conferenze e le sale riunioni, tra uffici diversi o altre aree locali. Può anche includere l'accesso wireless da posizioni remote tramite punti di accesso alla rete wireless gestiti non aziendali, ad esempio la rete domestica dell'utente o un punto di accesso wireless pubblico. Per semplificare le connessioni alle reti wireless, gli amministratori solitamente gestiscono queste connessioni usando i profili wireless che delineano le impostazioni specifiche di cui devono disporre i dispositivi mobili prima di potersi connettere alla rete wireless. Queste possono comprendere la configurazione automatica di un nome di rete personalizzato, di un identificatore del set di servizi di rete (SSID), di impostazioni di sicurezza e proxy di rete. È anche possibile stabilire se il dispositivo debba connettersi automaticamente alla rete wireless o meno quando si trova nel campo.
- **Rete privata virtuale (VPN):** l'accesso remoto sicuro alle risorse aziendali spesso include l'uso di un tipo di connessione VPN definito dal dispositivo mobile. Questo è spesso specifico del fornitore e include l'installazione di un'applicazione VPN sul dispositivo mobile. Inoltre, queste applicazioni VPN usano spesso certificati digitali o credenziali dell'account utente gestite separatamente per autenticare la connessione VPN. Per semplificare le connessioni alle reti VPN, gli amministratori possono solitamente gestire queste connessioni usando profili VPN o gli strumenti di gestione VPN inclusi nella soluzione VPN. A seconda del supporto dell'integrazione, la gestione delle connessioni VPN con la soluzione di gestione dei dispositivi mobili può essere possibile o meno in determinate piattaforme VPN.

>[!NOTE]
>Si potrebbe disporre di altre risorse basate sul Web, ad esempio SharePoint, che sfruttano l'accesso sicuro tramite Secure Socket Layer (SSL) o Transport Layer Security (TLS). Assicurarsi di comprendere il modo in cui i dispositivi mobili accederanno a queste risorse o a risorse con metodi di accesso sicuri o VPN separati.

### Domande sulla pianificazione della gestione della connettività di rete

Rispondere alle domande seguenti relative alla pianificazione della gestione della connettività di rete:
 
- Quale tipo di piattaforma VPN è distribuito nella rete locale?
- La piattaforma VPN è supportata o può essere integrata con la soluzione di gestione dei dispositivi mobili?
- Se la piattaforma VPN è già integrata o supportata da una soluzione di gestione dei dispositivi non mobili esistente, la soluzione di gestione dei dispositivi mobili si integra con entrambi i sistemi?
- L'infrastruttura Wi-Fi richiede un aggiornamento per sostenere il maggior numero di connessioni dei dispositivi e le maggiori esigenze di larghezza di banda?
- In che modo i dispositivi mobili si connetteranno alla piattaforma VPN o wireless locale esistente?
- Se i dispositivi mobili sono già connessi alla piattaforma VPN o wireless esistente, che tipo di connessione o protocollo useranno i dispositivi per la connessione?
- Quali modifiche è necessario apportare a queste connessioni se i dispositivi vengono registrati in una soluzione di gestione dei dispositivi mobili?
- Gli amministratori o gli utenti (o una combinazione di entrambi) saranno responsabili del collegamento dei dispositivi mobili alla piattaforma VPN o wireless? Se gli utenti connettono i dispositivi mobili alla piattaforma VPN o wireless, in che modo:
 - Sceglieranno il punto di connessione appropriato per accedere alla rete aziendale?
 - Sceglieranno il metodo di connessione o il protocollo di connessione corretto?
 - Sceglieranno il certificato digitale appropriato per il metodo di connessione?
- Si desidera configurare automaticamente le proprietà e le impostazioni della connessione VPN e wireless sui dispositivi mobili dell'utente?
 - È necessario mettere a disposizione impostazioni di configurazione o sicurezza della rete wireless diverse per diversi tipi di utenti, dispositivi, sistemi operativi dei dispositivi o gruppi e ruoli degli utenti?
 - È necessario poter importare o esportare i criteri di connessione relativi alla configurazione o alla sicurezza della rete wireless e/o VPN?

## Gestione dei certificati

È possibile usare i certificati digitali, autofirmati o emessi da un'autorità di certificazione (CA) di terze parti, per autenticare i dispositivi mobili per le connessioni di rete o per risorse di rete specifiche. Per semplificare la gestione dei certificati digitali, gli amministratori solitamente gestiscono tali certificati usando i profili dei certificati. Questo consente un metodo uniforme e centralizzato per la gestione dei certificati, tra cui il metodo di creazione, rilascio e rinnovo. Ciò consente anche agli utenti di connettersi alla risorsa aziendale senza dover richiedere e installare i certificati manualmente o tramite un processo di sicurezza non approvato.</para><para>Tuttavia, l'uso di certificati per questo tipo di autenticazione richiede spesso requisiti dell'infrastruttura aziendali aggiuntivi. che potrebbero comprendere tutti o alcuni dei componenti di rete seguenti, a seconda del livello di integrazione supportato dalla soluzione di gestione dei dispositivi mobili:

- **Servizi directory:** i servizi come, ad esempio, Microsoft Active Directory in genere sono necessari per connettere e gestire in modo sicuro tutti gli altri componenti della rete.
- **Server dell'autorità di certificazione (CA):** se si rilasciano certificati autofirmati per l'organizzazione, è necessaria un'autorità di certificazione per creare, rilasciare, gestire e rinnovare i certificati digitali.
- **Server del servizio Registrazione dispositivi di rete (NDES):** consente al software e ai dispositivi mobili di ottenere certificati basati sul protocollo SCEP (Simple Certificate Enrollment Protocol).
- **Server proxy:** a seconda della configurazione della rete locale, può essere necessario un server proxy che consente ai dispositivi mobili di ricevere certificati usando una connessione Internet e senza connessione diretta alla rete aziendale interna.

### Domande sulla pianificazione della gestione dei certificati

Rispondere alle domande seguenti relative alla pianificazione della gestione dei certificati:

- L'organizzazione richiede o usa già i certificati digitali per autenticare l'accesso alle risorse di rete?
- Si dispone di un'infrastruttura a chiave pubblica (PKI) aziendale?
- È necessario rilasciare automaticamente i certificati digitali per i dispositivi mobili?
- Come vengono creati, rilasciati, rinnovati o revocati i certificati digitali dai dispositivi mobili?
- I certificati digitali sono gestiti centralmente da un'autorità di certificazione (CA) locale o di terze parti?
- È necessario assegnare certificati diversi per l'accesso a servizi di rete diversi, a seconda del tipo di dispositivo mobile che accede alla rete?

>[!TIP]
>Assicurarsi di prendere appunti per ogni risposta e di comprendere la logica alla base della risposta. Le attività successive esamineranno le opzioni disponibili e i vantaggi e svantaggi di ogni opzione.  Rispondere a queste domande consentirà di selezionare l'opzione più adatta alle esigenze aziendali.

<!--HONumber=Jun16_HO1-->


