---
# required metadata

title: Considerazioni sulle app
description:
keywords:
author: YuriDio
manager: swadhwa
ms.date: 04/28/2016
ms.topic: article
ms.prod:
ms.service:
ms.technology:
ms.assetid: 4b871c74-fec8-45e2-8b45-6ef0e62f7cc6

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: 
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---


# Considerazioni sulle app

Le considerazioni sulle app per il BYOD possono variare in base agli obiettivi aziendali, ai vincoli e alle risorse. Le aziende devono valutare le app esistenti, le tecnologie usate per lo sviluppo delle app, i requisiti per l'esecuzione delle app in qualsiasi dispositivo e quali app sono essenziali per consentire agli utenti l'accesso da qualsiasi posizione. Anche se il provisioning e la distribuzione delle app moderne non richiedono un elevato utilizzo di risorse rispetto alle app basate su Windows, per lo sviluppo e la gestione di queste app è comunque previsto un costo.

Per le app sviluppate in modo specifico per gli scenari BYOD esistono dei criteri ed è necessario valutare se le app esistenti hanno tali criteri e quindi decidere se adattare le app a uno scenario BYOD o se fornire un'esperienza datata per consentire agli utenti di accedere alle app dai propri dispositivi. Per identificare questi criteri, è possibile usare l'elenco seguente:

- Capire l'utente: quale problema si sta cercando di risolvere con l'app? Il problema riguarda l'utente? L'esperienza utente con l'app e lo scopo per cui l'app viene usata dagli utenti sono aspetti importanti da considerare.
- Semplicità: gli utenti devono poter imparare a usare le app autonomamente e con il minimo aiuto, nonché navigare tra le opzioni senza sentirsi persi.
- Flessibilità di aggiornamento: la strategia delle app per dispositivi mobili consiste nel dare agli utenti la possibilità di usare immediatamente le app e di inviare commenti e suggerimenti per migliorarle. Distribuire un'app perfetta già al primo rilascio non è possibile per le app per dispositivi mobili. È necessario rendere il ciclo di rilascio più flessibile e rispondere rapidamente ai commenti e suggerimenti. In pratica, tali app vanno distribuite subito continuando ad apportare modifiche per tutto il ciclo di vita dell'app.
- Prestazioni: anche se le tradizionali app basate su Windows possono essere più affidabili perché vengono eseguite su PC, gli utenti tendono a credere che usano più risorse. Le app per dispositivi mobili devono essere progettate per risparmiare risorse. Occorre concentrarsi su cosa si vuole realmente offrire all'utente per fornire la migliore esperienza utente possibile.

Per altre informazioni sugli aspetti generali da considerare durante la creazione di app per dispositivi mobili, vedere le [10 considerazioni per la creazione di app per dispositivi mobili per le aziende](https://www.microsoft.com/en-gb/developers/articles/week01jan14/10-considerations-when-creating-mobile-apps-for-business).

## Esperienza

Per ottimizzare l'esperienza utente basata sulla piattaforma su cui verranno eseguite le app e sulla strategia di distribuzione, l'azienda deve identificare quali app pubblicare e come. Se l'ambiente è eterogeneo e alcuni dispositivi verranno supportati dall'azienda, una strategia consiste nel pubblicare le app tramite il portale aziendale. Fondamentalmente, le decisioni aziendali determineranno le considerazioni per l'esperienza utente. L'azienda intende sviluppare app che forniranno la stessa esperienza indipendentemente dalla piattaforma o intende offrire agli utenti la formazione per usare le app in piattaforme diverse senza avere la stessa esperienza?
Considerare il costo e il ritorno sugli investimenti per ogni caso menzionato nel paragrafo precedente. Si potrebbe provare a consolidare tutte le app in una pagina principale del portale Web per fornire la stessa esperienza ma il comportamento delle app risulterebbe comunque diverso a seconda della piattaforma.

Considerando che le app per gli utenti remoti devono essere eseguite su più di una piattaforma, essere quanto più semplici possibile e richiedere il minimo accesso ai dispositivi degli utenti, è consigliabile ridurre le opzioni per le app basate sul Web e le app moderne. La sezione seguente consente di determinare quale esperienza app risulta più appropriata per la soluzione da progettare.

### Opzioni di esperienze app: vantaggi e svantaggi

Usare l'elenco che segue per comprendere i vantaggi e gli svantaggi di ogni opzione di esperienza app:

- Basato su Web
    - Vantaggi
        - Ampiamente disponibile in molte piattaforme
        - Crittografia disponibile con il protocollo HTTPS
        - Tecnologia avanzata
        - Facilità d'uso
        - Non richiede l'installazione sui dispositivi degli utenti
    - Svantaggi
        - Non ha l'aspetto tipico di un'app per dispositivi mobili
        - Potrebbe richiedere l'installazione di componenti di terze parti, ad esempio Flash, sui dispositivi degli utenti
        - Soggetta alle vulnerabilità del browser
- Moderna
    - Vantaggi
        - Aspetto moderno
            - Esperienza più completa per gli utenti finali
            - I controlli di sicurezza vengono stabiliti dallo sviluppatore
            - Sfrutta le API del sistema operativo locale
            - Può essere eseguita su piattaforme diverse
            - Non si basa sul Web browser per l'esecuzione
    - Svantaggi
        - Richiede l'installazione sui dispositivi degli utenti.
        - Richiede un'infrastruttura di back-end per la distribuzione ai dispositivi degli utenti.
        - Potrebbe richiedere agli sviluppatori di ampliare le proprie conoscenze sullo sviluppo delle app con questo nuovo formato.


### Requisiti delle app e considerazioni

Considerare le app che verranno adattate per poter essere usate sui dispositivi degli utenti remoti e assicurarsi che questi requisiti vengano comunicati agli utenti. Di seguito sono elencati i requisiti delle app con le relative considerazioni:

- **Accesso a Internet e/o ai servizi cloud** se le app per funzionare richiedono l'accesso a Internet. Considerare gli aspetti seguenti:
    - Le app devono poter trasferire dati crittografati.
    - Le app devono utilizzare una larghezza di banda minima.
    - Considerare la possibilità di usare i Servizi notifica Push Windows per gli aggiornamenti.
    - Le app devono poter interagire con un server proxy nel caso in cui l'organizzazione usa questo tipo di tecnologia per consentire l'accesso a Internet.
    - Le app devono poter essere usare la connessione Wi-Fi dei dispositivi mobili.
- **Raccogliere i dati degli utenti** se sono necessari per il funzionamento delle app. Considerare gli aspetti seguenti:
    - Le app devono indicare in dettaglio i dati degli utenti che verranno raccolti e gli utenti devono acconsentire alla raccolta.
    - Se verranno trasferiti dati privati, assicurarsi che siano crittografati.
    - Se nei dispositivi degli utenti verranno archiviati dati privati, assicurarsi che siano crittografati.
- **Integrazione con i social network** se le app la richiedono per essere eseguite. Considerare gli aspetti seguenti:
    - Considerare il metodo di autenticazione che verrà usato per consentire l'autenticazione delle app con i social network.
    - Verificare il livello di integrazione con i social network per evitare la fuga di dati in un contesto più ampio.
    - Assicurarsi che le app indichino in dettaglio i dati che verranno condivisi dall'utente nel social network in questione.
    - Assicurarsi che i dati inviati al provider del social network siano crittografati.

Per migliorare l'esperienza utente, è consigliabile categorizzare tutte le app in base agli standard del team di sviluppo per evitare che gli utenti debbano scorrere centinaia di app.

## Piattaforma

Quando ci si occupa dell'esperienza utente, è normale valutare diverse piattaforme per determinare quella che l'azienda è disposta a supportare. Molte volte, consentendo agli utenti di usare i propri dispositivi, significa creare un ecosistema eterogeneo e il reparto IT potrebbe non essere pronto per supportare tale ecosistema.

Ogni piattaforma prevede requisiti diversi per la firma e la pubblicazione delle app, che influiscono direttamente sulle risorse IT in quanto il reparto IT deve valutare l'intero ciclo di vita delle app in esecuzione su una piattaforma specifica. È anche necessario accedere ai requisiti della piattaforma delle app per una soluzione di infrastruttura BYOD. La sezione seguente include considerazioni importanti sui requisiti della piattaforma dell'app.

### Requisiti della piattaforma dell'app: considerazioni

Di seguito sono elencati i requisiti della piattaforma dell'app con le relative considerazioni:

- Infrastruttura di back-end
    - Valutare se consentire l'uso delle app agli utenti remoti influirà sulle prestazioni complessive del server app.
    - In base a questa valutazione, verificare la necessità di aggiornare i server, aumentare il numero di server o virtualizzare i server.
- Supporto
    - Definire quali piattaforme, ad esempio Windows, iOS e Android, verranno supportate dall'azienda.
        - Se l'azienda decide di adottare tutte le piattaforme, definire i limiti di supportabilità per ogni piattaforma.
    - Stabilire gli scenari supportati e non supportati dall'azienda. Ad esempio, l'azienda potrebbe decidere di non supportare i dispositivi che sono stati sottoposti a jailbreak.
- Piattaforma del sistema operativo
    - Definire i vincoli di ogni sistema operativo per eseguire le app dell'azienda.
    - Definire i requisiti minimi per le app in ogni sistema operativo che l'azienda decide di supportare.
    - Testare le app in ogni sistema operativo per verificare se in ognuno hanno un comportamento simile. Documentare le differenze.

Come parte della strategia per il supporto di più piattaforme, è necessario definire il modo in cui le app verranno utilizzate da tali piattaforme. Con Microsoft Intune è possibile consentire agli utenti l'uso delle app dal [portale aziendale](http://apps.microsoft.com/windows/app/company-portal/4b1dff1a-e76f-4fdd-a993-9c59048c3768). Questa funzionalità non è disponibile solo per Windows, ma anche per altre [piattaforme](http://blogs.technet.com/b/windowsintune/archive/2013/11/25/windows-intune-company-portals-for-ios-and-android-now-available.aspx). Quando si valutano le app a cui gli utenti possono accedere tramite il portale aziendale, prendere in considerazione i due tipi di app disponibili tramite il portale aziendale:

- App con sideload: app LOB moderne sviluppate e pubblicate nel portale aziendale in cui è ospitato il contenuto.
- App con collegamento diretto: collegamenti alle app in Microsoft Store (o Apple Marketplace per le app iOS) archiviate in Configuration Manager, a cui gli utenti accedono tramite il portale aziendale.

Le app con collegamento diretto possono ridurre il sovraccarico amministrativo, reindirizzando gli utenti a Windows Store per la versione più recente, anziché dover gestire e pubblicare gli aggiornamenti nel portale aziendale. L'uso di Microsoft Store per la distribuzione delle app può anche sollevare alcune domande, ad esempio:

- È possibile usare l'infrastruttura esistente per distribuire queste app tramite Windows Store?
- Qual è il ruolo di Windows Store nel processo di distribuzione delle app?
- Le app devono provenire tutte da Windows Store?

Le risposte variano in base allo stato attuale della strategia di distribuzione dell'azienda e a come deve evolversi se si sceglie di usare Windows Store. Tenere presente che Windows Store è un sistema di distribuzione digitale ed è la piattaforma di distribuzione principale per le app moderne in Windows 10, Windows 8.1, Windows 8 e Windows RT. Tuttavia, è possibile usare Windows Store per visualizzare l'elenco di app desktop certificate per l'esecuzione in dispositivi basati su Windows 8. Per altre informazioni sulle app di cui è stato eseguito il sideload, vedere [Prova pratica: sideload delle applicazioni Windows Store](https://technet.microsoft.com/windows/jj874388.aspx).

## Distribuzione

Per valutare le considerazioni sulle app che verranno distribuite agli utenti, è necessario comprendere i requisiti relativi all'accesso aziendale. Gli scenari di distribuzione includono le app che devono essere sempre connesse alle risorse aziendali, anche se gli utenti non necessitano dell'accesso alle altre risorse aziendali o dell'accesso completo a tutte le risorse aziendali all'interno della rete aziendale. Verificare le opzioni di distribuzione per ogni app e valutare il metodo preferibile per l'azienda. La sezione che segue include le opzioni di distribuzione più comuni che è possibile usare come punto di riferimento decisionale.

### Opzioni di distribuzione: vantaggi e svantaggi

Usare l'elenco che segue per comprendere i vantaggi e gli svantaggi di ogni opzione di distribuzione:

- In locale
    - Vantaggi
        - Tutti i controlli di sicurezza risiedono fisicamente in locale e il reparto IT ne ha il pieno controllo
        - Il reparto IT può applicare una protezione avanzata al server che svolge il ruolo di distribuzione
        - Offre funzionalità più granulari per il controllo, la registrazione e la creazione di report
    - Svantaggi
        - Costi di gestione maggiori rispetto a una soluzione cloud
        - Mancanza di integrazione con i servizi cloud
        - Difficoltà di distribuzione delle app per i dispositivi non gestiti
        - Difficoltà di controllo delle opzioni di distribuzione per i dispositivi che non risiedono in locale
- Basata su cloud
    - Vantaggi
        - Le app possono essere installate da qualsiasi posizione
        - Funzionalità di distribuzione multipiattaforma
        - Maggiore semplicità di distribuzione delle app ai dispositivi non gestiti rispetto a una soluzione locale
    - Svantaggi
        - Funzionalità di creazione di report limitate per i dispositivi locali che usano le app
        - Mancanza di gestione centralizzata e di controllo della distribuzione
- Ibrida (parte in locale e parte nel cloud)
    - Vantaggi
        - Maggiore semplicità di distribuzione delle app ai dispositivi non gestiti rispetto a una soluzione locale.
        - Il reparto IT continua ad avere il controllo totale della parte in locale del ruolo di distribuzione.
        - Integrazione tra dispositivi in locale e dispositivi gestiti su cloud in un'unica posizione.
        - Semplicità di controllo delle opzioni di distribuzione in più piattaforme rispetto a una soluzione locale.
    - Svantaggi
        - È richiesta in genere una sottoscrizione al servizio cloud.
        - L'integrazione con la soluzione di distribuzione locale può variare in base al servizio cloud.

### Requisiti di distribuzione delle app: considerazioni

È necessario anche accedere ai requisiti di distribuzione delle app per una soluzione di infrastruttura BYOD. L'elenco che segue include alcune considerazioni importanti sulla distribuzione delle app:

- Autorizzazioni
    - Verificare che il livello di autorizzazioni che gli utenti devono avere per installare le app non sia intrusivo. Ad esempio, non è necessario che un utente sia l'amministratore di un dispositivo per installare le app.
    - Se un'app usa file o cartelle temporanei, assicurarsi che non richieda autorizzazioni a livello di amministratore per gestire tali oggetti.
- Certificato
    - Se la distribuzione dell'app richiede un certificato nei dispositivi degli utenti, assicurarsi che i dispositivi possano accedere all'elenco di revoche di certificati (CRL) per convalidare l'autenticità del certificato.
    - Se un certificato viene installato durante il processo di installazione dell'app, assicurarsi che gli utenti ne siano informati e che ne venga richiesto il consenso.
    - Definire il certificato da usare. Se il certificato è stato rilasciato da un'autorità di certificazione (CA) interna, assicurarsi innanzitutto che nei dispositivi degli utenti sia installato il certificato della CA e quindi installare i certificati delle app. Se il certificato è stato rilasciato da una CA pubblica di terze parti, verificare che il dispositivo sia in grado di convalidare il certificato tramite Internet. Se la convalida non riesce, assicurarsi che gli utenti vengano informati del motivo per cui non sia riuscita ed evitare l'installazione per motivi di sicurezza.
- Agente di gestione dei dispositivi mobili (MDM)
    - Se le app richiedono l'installazione di un agente MDM nei dispositivi degli utenti prima dell'installazione delle app, assicurarsi che gli utenti ne siano informati e che ne venga richiesto il consenso.
    - Se è necessario installare l'agente MDM, assicurarsi che il processo di installazione sia facile da eseguire e che richieda l'uso minimo di risorse di sistema.

Con System Center 2012 R2 Configuration Manager, il reparto IT può identificare e concedere licenze a utenti specifici usando la funzionalità di individuazione utente in Configuration Manager e quindi aggiungere gli utenti a una raccolta personalizzata che sincronizzerà gli account utente con Microsoft Intune. In questo modo viene agevolata anche la distribuzione delle app.
Nelle considerazioni sulla distribuzione delle app occorre tenere presente anche l'aggiornamento di queste ultime. Dopo l'installazione delle app, i relativi aggiornamenti dovrebbero essere rilevati automaticamente e gli utenti dovrebbero ricevere una notifica nell'app di Windows Store. System Center 2012 R2 offre alle aziende la possibilità di avere un app store aziendale e di consentire agli utenti di installare le app LOB da questo store. Per altre informazioni sull'app store aziendale, vedere Case study sulla progettazione: app di Windows Store line-of-business aziendali.

La funzionalità di [VPN ad attivazione automatica in Windows 10](http://blogs.technet.com/b/canitpro/archive/2016/01/26/step-by-step-enabling-apps-to-auto-trigger-vpns-in-windows-10.aspx) può essere usata per consentire alle app di accedere alle risorse aziendali. Questa funzionalità consente al reparto IT di impostare un elenco di app predefinite da connettere automaticamente alle reti aziendali aprendo una connessione VPN all'avvio dell'app. È possibile specificare le app da rendere disponibili per l'attivazione automatica e limitare l'accesso remoto in base all'identità dell'utente e all'identità del computer da cui l'utente accede alla risorsa. Per altre informazioni sulla funzionalità di VPN ad attivazione automatica, vedere [Novità di Accesso remoto in Windows Server 2012 R2](https://technet.microsoft.com/library/dn383589.aspx).

Se l'azienda sta adottando Windows Phone e vuole consentire agli utenti di usare le app LOB per questa piattaforma, è consigliabile iniziare a comprendere il processo di registrazione delle app. Le aziende devono eseguire alcuni passaggi per creare un account aziendale, registrare i dispositivi e distribuire le app ai dispositivi registrati. Per altre informazioni sulla distribuzione di app di Windows Phone, vedere [Distribuzione di app aziendali per Windows Phone](https://msdn.microsoft.com/library/windowsphone/develop/jj206943(v=vs.105).aspx).

## Archiviazione e rete

Le considerazioni sulle app in merito ad archiviazione e rete possono influire sia sui server app che sui dispositivi. Quando si iniziano a considerare questi due componenti essenziali per le app, sorgono le domande seguenti:

- Le app archivieranno qualcosa nell'archivio degli utenti?
    - In tal caso, quali sono i requisiti di archiviazione per le app quando si archiviano informazioni sui dispositivi degli utenti? I dati vengono crittografati dalle app o dal sistema operativo?
- Le app gestiscono le informazioni riservate durante la trasmissione attraverso la rete cablata o wireless?
    - In tal caso, i dati vengono crittografati?

La sezione che segue include considerazioni importanti sui requisiti di archiviazione e rete per le app.

### Requisiti di archiviazione e rete per le app: considerazioni

L'elenco che segue agevola la comprensione dei vantaggi e degli svantaggi di ogni requisito di archiviazione e rete per le app e delle relative considerazioni:

- Spazio su disco
    - Se il processo di distribuzione delle app deve usare più spazio rispetto a quanto richiesto dall'app (a causa dei file temporanei), assicurarsi che tale aspetto sia ben documentato, che gli utenti ne siano informati e che ne venga richiesto il consenso.
    - Assicurarsi che tutti i file e le cartelle temporanei archiviati nei dispositivi di archiviazione degli utenti durante il processo di distribuzione vengano rimossi dopo l'installazione di un'app.
- Privacy dei dati
    - Se un'app archivia informazioni private dell'azienda o dell'utente nella memoria del dispositivo degli utenti, assicurarsi che gli utenti ne siano informati e ne venga richiesto il consenso.
        - Se l'app archivia informazioni private, assicurarsi che i file vengano crittografati nei dispositivi degli utenti.
    - Se le app trasferiscono informazioni private dell'azienda o degli utenti tramite la rete, assicurarsi che il processo di trasferimento venga crittografato.
- Backup
    - Se le app archiviano i file temporanei nella memoria del dispositivo degli utenti durante il normale funzionamento per eseguirne successivamente il commit nel database del server, assicurarsi che esista un meccanismo di backup per salvare i file in caso di arresto anomalo delle app, di interruzione dell'alimentazione del dispositivo e per qualsiasi altra circostanza ignota che potrebbe causare la perdita di dati.
    - Assicurarsi che anche i dati di backup siano protetti da utenti o processi non autorizzati.
    - Se la rete dell'utente perde la connettività con il server app, assicurarsi che le app abbiano un processo di backup per evitare la perdita di dati.
- Infrastruttura di back-end
    - Considerare le esigenze di aggiornamento, espansione o virtualizzazione dei server di archiviazione back-end.
    - Assicurarsi che l'infrastruttura di back-end contenga più percorsi di rete per accedere ai dispositivi degli utenti.
    - Assicurarsi che la soluzione perimetrale locale sia in grado di gestire più ISP per evitare che gli utenti provenienti dal cloud perdano la connettività con i server app locali.

Quando si considerano le app da usare nell'infrastruttura BYOD, è anche possibile sfruttare Virtual Desktop Infrastructure (VDI) di Windows Server 2012 R2. Gli utenti possono eseguire in remoto le app di Windows 8 come se fossero in esecuzione sul proprio dispositivo locale, inclusi videoclip, filmati, video in streaming e app dall'elevato utilizzo di risorse grafiche. È possibile migliorare l'esperienza utente in Windows Server 2012 R2 con Microsoft RemoteFX. Windows Server 2012 R2 include miglioramenti al codec e ai flussi multimediali e offre un'esperienza utente ottimizzata in condizioni di rete variabili, raggiungendo un compromesso tra risoluzione dell'esperienza e larghezza di banda disponibile quando richiesta. Inoltre, con l'app Desktop remoto di Microsoft, gli utenti possono connettersi alle app e ai dati aziendali da diverse piattaforme, tra cui Windows, Windows RT, iOS, Mac OS X e Android.

Se si prevede di usare VDI per consentire agli utenti BYOD di accedere alle app aziendali, è necessario conoscere prima di tutto i tipi di distribuzione disponibili per VDI:

- Basata su macchine virtuali: macchine virtuali di Windows 8 in esecuzione in un'infrastruttura Hyper-V. In tal caso, usare Servizi Desktop remoto per fornire agli utenti la connettività remota alle macchine virtuali. È possibile usare lo scenario di distribuzione basata su macchine virtuali con le raccolte di macchine virtuali in pool o personali.
- Basata su sessioni: gli utenti si connettono a Servizi Desktop remoto in Windows Server 2012 R2 ed eseguono le app in sessioni di Windows Server 2012 R2. Per questo tipo di distribuzione è richiesto solo Servizi Desktop remoto.
L'esperienza di archiviazione per l'infrastruttura VDI in Windows Server 2012 R2 è stata migliorata con l'archiviazione suddivisa in livelli e la deduplicazione dei dati online. Questa funzionalità consente al reparto IT di creare volumi di archiviazione che ottimizzano automaticamente i percorsi dei dati nei dischi e individuano i blocchi di dati a cui si accede più frequentemente nei dischi a elevate prestazioni. È anche possibile sfruttare le seguenti funzionalità di archiviazione in Windows Server 2012 R2 per l'infrastruttura VDI:
- Più opzioni di archiviazione: supporta l'archiviazione diretta, basata sulla rete, in cluster o SAN di macchine virtuali; utilizza la deduplicazione dei dischi online per ridurre notevolmente i requisiti di archiviazione.
- Condivisione equa: distribuisce in modo dinamico larghezza di banda, CPU e spazio su disco in altre macchine virtuali e sessioni garantendo che nessuna macchina virtuale o sessione monopolizzi le risorse o comprometta l'esperienza degli altri utenti del sistema.


Per altre informazioni su VDI in Windows Server 2012 R2, vedere [Novità di Servizi Desktop remoto in Windows Server 2012 R2](https://technet.microsoft.com/library/dn283323.aspx).

La decisione di quale esperienza e distribuzione delle app verrà usata per il progetto di infrastruttura BYOD deve essere bilanciata con il costo totale di proprietà. Per comprendere meglio il costo totale di proprietà per l'adozione di VDI, è consigliabile leggere [VDI TCO Analysis for Office Worker Environments](http://download.microsoft.com/download/7/9/A/79AAA903-25B4-4D76-8580-BC47D5700433/Microsoft VDI TCO whitepaper customer ready v1 2.pdf).

## Sicurezza

Valutare di usare un ciclo di vita dello sviluppo della sicurezza per tutte le app che verranno utilizzate dagli utenti sui propri dispositivi. La sicurezza deve essere incorporata in tutte le fasi del processo di sviluppo e devono essere prese in considerazione tutte le minacce potenziali. [STRIDE](https://msdn.microsoft.com/magazine/cc163519.aspx) e altre strategie di sicurezza possono essere incorporate nel ciclo di vita dello sviluppo con [Microsoft Security Development Lifecycle (SDL)](https://www.microsoft.com/security/sdl/process/requirements.aspx). È importante considerare il modo in cui l'infrastruttura esistente verrà integrata con la strategia di sicurezza globale per il BYOD. L'ambiente esistente è in grado di fornire una base sicura per le app? L'azienda deve acquistare soluzioni sicure di terze parti per ridurre qualsiasi vulnerabilità potenziale che questa nuova scelta può creare?

Le considerazioni sulla sicurezza sono importanti per le app che verranno utilizzate dagli utenti sui propri dispositivi. È consigliabile usare raccolte personalizzate in base ai gruppi di sicurezza di Active Directory per restringere l'accesso degli utenti ad alcune app con requisiti di accesso specifici, limitando in tal modo gli utenti che possono installarle. La sicurezza può anche essere sfruttata per migliorare l'esperienza utente consentendo l'uso dello stesso nome utente e della stessa password per accedere alle risorse aziendali, che possono essere eseguite con AD FS. La sicurezza è importante anche per la progettazione della distribuzione delle app. È consigliabile acquisire e distribuire i certificati e le chiavi di sideload prima di abilitare la registrazione degli utenti. Lavorare insieme ad altri team per semplificare il processo di certificazione delle app.


<!--HONumber=Apr16_HO2-->


