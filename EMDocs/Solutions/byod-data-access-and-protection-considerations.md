---
# required metadata

title: Considerazioni su protezione e accesso ai dati
description:
keywords:
author: YuriDio
manager: swadhwa
ms.date: 04/28/2016
ms.topic: article
ms.prod:
ms.service:
ms.technology:
ms.assetid: 181eb917-119d-4e56-8ead-1182b1dc5cab

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: 
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Considerazioni su protezione e accesso ai dati

La perdita di dati sensibili è un rischio per qualsiasi azienda e con l'introduzione del modello BYOD le informazioni si trovano in un numero sempre maggiore di posizioni. Questo si traduce in una più ampia varietà di minacce e rischi che devono essere affrontati in modo corretto. A causa delle diverse normative di legge, aziendali e di settore che regolano la protezione dei dati sensibili, proteggere i dati può risultare complesso. È importante tenere conto di questi requisiti legali, dei criteri aziendali interni e dei regolamenti del settore.
Come parte della strategia di implementazione dell'infrastruttura BYOD è fondamentale che, dopo aver definito i criteri e le classificazioni dei dati, i dati vengano collocati fisicamente, inseriti in livelli di classificazione adeguati e sottoposti alle impostazioni di sicurezza appropriate. I reparti IT necessitano di un metodo per convalidare l'identità degli utenti e possono applicare ulteriori condizioni sui tipi di dispositivi in grado di accedere alle informazioni e alle app fornite.

## Archiviazione

Il modo in cui i dati vengono archiviati nei dispositivi degli utenti può influire direttamente sul metodo scelto per l'accesso e la protezione dei dati in ambienti BYOD. È necessario considerare la crittografia dei dati, inoltre il reparto IT deve poter controllare nei dispositivi quando la crittografia dei dati è abilitata e per quali tipi di dati. Le aziende devono analizzare i propri criteri e normative per comprendere quali tipi di dati possono lasciare il data center ed essere inattivi nei dispositivi remoti. La crittografia dei dati inattivi presenti nell'archivio del data center è fondamentale. Se l'azienda non ha ancora implementato la crittografia in questo ambito, l'adozione della stessa deve essere considerata come parte della strategia per il passaggio a un'infrastruttura BYOD. In teoria, i dati devono essere crittografati lungo tutto il percorso.

Con Windows Server 2012 R2 è possibile crittografare i dati inattivi nei dispositivi degli utenti usando Cartelle di lavoro. Gli amministratori IT possono usare Cartelle di lavoro per ottenere un maggiore controllo sui dati aziendali e i dispositivi degli utenti e per centralizzare i dati di lavoro in modo da poter applicare i processi e gli strumenti appropriati per garantire la conformità della propria azienda. Si tratta di misure che vanno dall'avere semplicemente una copia dei dati nel caso in cui l'utente lasci l'azienda a una vasta gamma di funzionalità di backup, conservazione, classificazione e crittografia automatizzata. Se si decide di usare [Cartelle di lavoro](https://technet.microsoft.com/library/dn265974.aspx), verificare che i server che ospiteranno le condivisioni di sincronizzazione siano pianificati correttamente dal punto di vista delle prestazioni. Per altre informazioni, vedere il blog sulle [considerazioni relative alle prestazioni per le distribuzioni di Cartelle di lavoro](http://blogs.technet.com/b/filecab/archive/2013/11/01/performance-considerations-for-large-scale-work-folders-deployments.aspx).

Se si pensa a un archivio come a un contenitore per un determinato contenuto, è importante capire che occorre proteggere l'uso del contenuto. È possibile evitare la perdita di dati applicando criteri che definiscono come verrà usato dall'utente finale il contenuto che si trova nell'archivio. È possibile usare [Active Directory Rights Management Services (AD RMS)](https://technet.microsoft.com/library/hh831554.aspx) per potenziare la strategia di sicurezza dell'organizzazione proteggendo i documenti che usano Information Rights Management (IRM). AD RMS consente agli utenti e agli amministratori di usare i criteri IRM per specificare le autorizzazioni di accesso a documenti, cartelle di lavoro e presentazioni, contribuendo quindi a impedire la stampa, l'inoltro o la copia di informazioni sensibili da parte di persone non autorizzate. Quando l'autorizzazione per un file viene limitata tramite IRM, le restrizioni di accesso e uso vengono applicate indipendentemente dalla posizione in cui si trovano le informazioni, perché l'autorizzazione è archiviata nel file stesso.

Se la società decide di usare una soluzione basata su cloud per la protezione dei file, può anche usare [Azure Rights Management](https://technet.microsoft.com/en-us/library/jj585026.aspx). Azure Rights Management è in grado di proteggere le informazioni riservate dell'azienda usando crittografia, identità e criteri di autorizzazione per proteggere i file e i messaggi di posta elettronica in più dispositivi, tra cui telefoni, tablet e PC. È possibile proteggere le informazioni sia all'interno che all'esterno dell'organizzazione perché la protezione rimane associata ai dati, anche quando supera i limiti dell'organizzazione. 

È anche possibile usare altre tecnologie di archiviazione disponibili nel sistema operativo Windows per migliorare la protezione generale dei dati, ad esempio BitLocker per la crittografia delle unità ed [Encrypting File System (EFS)](https://technet.microsoft.com/library/cc700811.aspx) per la crittografia dei file. La tabella seguente presenta i vantaggi e gli svantaggi della protezione dell'archiviazione. Si tenga presente che queste opzioni non si escludono a vicenda. In altre parole, si potrebbe concludere che in una soluzione di infrastruttura BYOD da progettare sono necessarie tutte queste opzioni per garantire la protezione dei dati archiviati.

### Opzioni di protezione dell'archiviazione: vantaggi e svantaggi

Usare l'elenco che segue per comprendere i vantaggi e gli svantaggi di ogni opzione di protezione dell'archiviazione:

- Encrypting File System (EFS)
    - Vantaggi
        - Disponibilità della crittografia a livello di file
        - Il processo di crittografia è trasparente all'utente perché la crittografia non viene applicata a livello di app, ma a livello di file system
        - Offre funzionalità di backup con Key Recovery Agent
        - Disponibile in tutte le versioni supportate del sistema operativo Windows
        - Può essere abilitato usando Criteri di gruppo
        - Conformità con i requisiti di crittografia Suite B definiti dalla National Security Agency per soddisfare le esigenze delle agenzie governative degli Stati Uniti per la protezione delle informazioni riservate
    - Svantaggi
        - Se il proprietario dei dati non è disponibile e l'utente non ha Key Recovery Agent, non è possibile decrittografare un file EFS
        - La gestione del certificato deve essere impostata per gestire le chiavi private associate a certificati di ripristino
        - Non disponibile su altre piattaforme non Windows
- BitLocker
    - Vantaggi
        - Offre funzionalità di crittografia per le unità
        - Garantisce l'integrità e la verifica del sistema usando Trusted Platform Module (TPM)
        - Migliora la protezione per limitare gli attacchi basati su software offline
        - Offre un metodo per verificare che venga mantenuta l'integrità dei file di avvio
    - Svantaggi
        - Non disponibile in tutte le versioni di Windows
        - Richiede TPM versione 1.2
        - Richiede che il BIOS di sistema (per i computer con TPM e senza TPM) supporti la classe di dispositivi di archiviazione di massa USB
        - Non disponibile per i cluster precedenti a Windows Server 2012
- Cartelle di lavoro
    - Vantaggi
        - Si basa su EFS per la crittografia dei file.
        - Consente al reparto IT di crittografare i dati inattivi nei dispositivi degli utenti
        - Può essere abilitato usando Criteri di gruppo in base all'utente o al dispositivo
        - Integrazione con Microsoft Intune, che consente la cancellazione selettiva dei dati che si trovano in Cartelle di lavoro nei dispositivi degli utenti
        - Possibilità di chiedere agli utenti di ripetere l'autenticazione per poter accedere ai dati che si trovano in Cartelle di lavoro
        - Consente l'integrazione con Microsoft Rights Management Services per la classificazione dei dati
    - Svantaggi
        - Disponibile solo per Windows 8.1, Windows RT 8.1 e Windows 10
        - Richiede Windows Server 2012 R2 per ospitare le condivisioni di sincronizzazione
- Active Directory Rights Management Services (AD RMS)
    - Vantaggi
        - Impossibilità per un destinatario autorizzato di contenuto con restrizioni di inoltrare, copiare, modificare, stampare, inviare tramite fax o incollare tale contenuto per un utilizzo non autorizzato.
        - Supporto della scadenza dei file in modo che il contenuto dei documenti non possa essere più visualizzato dopo un periodo di tempo specificato.
        - Impossibilità di copiare contenuto con restrizioni utilizzando la funzione STAMP di Microsoft Windows.
    - Svantaggi
        - Richiede la distribuzione di un nuovo ruolo del server (AD RMS)
        - Non limita la copia dei contenuti quando si usano programmi per l'acquisizione delle schermate di terze parti
        - Non impedisce la perdita o il danneggiamento dei contenuti dovuti all'azione di virus informatici

## Rete

È essenziale considerare i fattori impliciti quando si consente agli utenti di usare i propri dispositivi e si desidera che i dati siano sicuri nell'intero percorso tra il data center (locale) o il cloud e i dispositivi degli utenti. Questi fattori sono evidenziati nella figura seguente:

![Diagramma di rete](./media/BYOD_Figure6.png)

Il diagramma evidenzia le aree critiche in cui è necessario considerare la protezione dei dati per un'infrastruttura BYOD. Queste aree sono descritte più in dettaglio nella sezione seguente.

### Protezione dei dati: posizioni e considerazioni
    
Usare l'elenco riportato di seguito per comprendere le considerazioni sulla protezione dei dati in base alla posizione. I numeri nell'elenco corrispondono al diagramma precedente:

- (1) Dati inattivi nel centro dati
    - Crittografia di archiviazione: considerare una soluzione di archiviazione che supporta la crittografia
    - Gestione delle chiavi: eseguire il backup della chiave usata per crittografare l'archiviazione e garantire la disponibilità di un Key Recovery Agent, in caso di necessità
- (2) Dati in fase di trasferimento dal centro dati al perimetro della rete aziendale
    - Crittografia di rete: considerare l'uso di un protocollo Web standard per la crittografia, ad esempio SSL
    - Infrastruttura a chiave pubblica (PKI): se l'azienda usa un'infrastruttura a chiave pubblica, è possibile usarla per crittografare il canale di comunicazione
- (3) Dati in fase di trasferimento dal perimetro della rete aziendale ai dispositivi degli utenti
    - Crittografia di rete: considerare l'uso di un protocollo Web standard per la crittografia, ad esempio SSL
    - PKI: gli utenti eseguiranno l'accesso a questo canale usando i dispositivi personali, quindi è consigliabile usare un certificato pubblico, che probabilmente sarà già considerato attendibile dai dispositivi degli utenti
- (3.1) Dati in fase di trasferimento dal perimetro della rete aziendale al provider di servizi cloud (facoltativo: si applica solo se l'azienda usa servizi cloud per BYOD)
    - Crittografia di rete: considerare l'uso di un protocollo Web standard per la crittografia, ad esempio SSL.
    - PKI: poiché gli utenti eseguiranno l'accesso a questo canale usando i dispositivi personali, è consigliabile usare un certificato pubblico, che probabilmente sarà già considerato attendibile dai dispositivi degli utenti
    - VPN da sito a sito: nel caso di un'[infrastruttura cloud ibrida](http://blogs.technet.com/b/cloudsolutions/archive/2013/08/22/hybrid-it-infrastructure-solution-for-enterprise-it-overview.aspx) connessa a Servizi cloud, è consigliabile usare una rete VPN da sito a sito per assicurare la disponibilità del canale sicuro per l'uso da parte delle app presenti nei dispositivi degli utenti
- (3.2) Dati inattivi nel centro dati del provider di servizi cloud (facoltativo: si applica solo se l'azienda usa servizi cloud per BYOD)
    - Provider di servizi cloud: considerare le opzioni che il provider di servizi cloud può offrire per crittografare i dati inattivi
    - Gestione delle chiavi: verificare come il provider di servizi cloud gestisce le chiavi ed esegue il processo di backup. Considerare anche l'integrazione tra i servizi cloud e un sistema di gestione delle chiavi locale
(4) Dati inattivi nei dispositivi degli utenti
    - Crittografia di archiviazione: considerare una soluzione di archiviazione che supporta la crittografia
    - Gestione delle chiavi: eseguire il backup della chiave usata per crittografare l'archiviazione e garantire la disponibilità di un Key Recovery Agent, in caso di necessità
    - Cancellazione remota: i dati che si trovano nei dispositivi degli utenti possono essere eliminati in remoto, se necessario

Windows Server 2012 R2 consente l'uso del protocollo [HTTPS](https://msdn.microsoft.com/library/aa767735.aspx) per pubblicare le risorse tramite [Proxy applicazione Web](https://technet.microsoft.com/library/dn280944.aspx) allo scopo di proteggere i dati in transito sulla rete. Le comunicazioni tra i server back-end possono anche essere crittografate con [IPsec](https://technet.microsoft.com/library/cc757613.aspx) o la [crittografia SMB](http://support.microsoft.com/kb/2709568), se il traffico di rete si basa solo sul [protocollo SMB](https://technet.microsoft.com/library/hh831795.aspx). Usare la tabella seguente per valutare l'opzione di protezione di rete più adatta alla proprie esigenze di progettazione per la comunicazione tra server back-end.

La sezione seguente consente di valutare l'opzione di protezione di rete più adatta ai propri requisiti di progettazione per la comunicazione tra server back-end.

### Opzioni di protezione della rete: vantaggi e svantaggi

Usare l'elenco che segue per comprendere i vantaggi e gli svantaggi di ogni opzione di protezione della rete:

- SSL
    - Vantaggi
        - Varie possibilità di supporto da molti dispositivi
        - Autenticazione avanzata, riservatezza dei messaggi e integrità.
        - Interoperabilità
    - Svantaggi
        - Richiede un'infrastruttura di certificati, a meno che non si usino certificati SSL pubblici
- IPSec
    - Vantaggi
        - Crittografia dell'intero datagramma IP
        - Autenticazione a livello di computer
        - Ampiamente supportato su più piattaforme e disponibile in tutte le versioni supportate da Windows
        - Autenticazione Internet Key Exchange (IKE) per limitare l'accesso alla rete ai computer attendibili
    - Svantaggi
        - Richiede un'infrastruttura di certificati, a meno che non si usi una chiave già condivisa
        - IPsec agisce a livello di host, quindi non può essere controllato a livello di app
        - Risoluzione dei problemi complessa
- Crittografia SMB
    - Vantaggi
        - Consente di crittografare i dati in transito con il protocollo SMB
        - Facile da implementare nell'interfaccia utente e usando Windows PowerShell
        - Flessibile perché può essere implementata in base al server o alla condivisione
    - Svantaggi
        - Funziona solo con Windows 8 e versioni successive per i computer client e con Windows Server 2012 e versioni successive per i computer server

## Directory

Gli attributi utente devono essere archiviati nella directory, per consentire ai responsabili IT di trovare facilmente informazioni sull'utente quali i ruoli e i gruppi. È inoltre necessario considerare come verrà registrata la relazione tra utenti e dispositivi. Ogni dispositivo sconosciuto che diventa noto o gestibile dal reparto IT deve anche avere un record nel database di gestione o nella directory per poter essere controllato dal reparto IT.

In ambienti ibridi in cui sono presenti archivi di autenticazione diversi, è necessario considerare come consentire agli utenti di eseguire l'autenticazione usando le stesse credenziali indipendentemente da dove si trovano gli utenti e le app. È consigliabile usare Active Directory Federation Services (AD FS) per centralizzare l'autenticazione in locale anziché replicare la directory con il provider di servizi cloud. La sezione che segue consente di valutare le opzioni di directory per un'infrastruttura BYOD.

### Opzioni di directory: vantaggi e svantaggi

Usare l'elenco che segue per comprendere i vantaggi e gli svantaggi di ogni opzione di protezione della directory:

- Centralizzata locale
    - Vantaggi
        - Tutti i controlli di sicurezza risiedono fisicamente in locale e il reparto IT ne ha il pieno controllo
        - Possibilità di applicare la protezione avanzata del server con il ruolo di directory
        - Controllo più completo e funzionalità di registrazione
    - Svantaggi
        - Costo di manutenzione superiore rispetto ai servizi cloud
        - Mancanza di integrazione con i servizi cloud
- Centralizzata nel cloud
    - Vantaggi
        - Costo di manutenzione inferiore rispetto a una soluzione locale
        - Più facile da gestire rispetto a una soluzione locale
    - Svantaggi
        - Mancanza di personalizzazione
        - Dipende dal provider di servizi cloud per ottenere il controllo e la registrazione dei dati
- Sincronizzazione di directory tra l'ambiente locale e il cloud
    - Vantaggi
        - Directory integrata locale e nel cloud
        - Abilitazione di Single Sign-On per gli utenti
        - Il reparto IT può applicare comunque la protezione avanzata del server con il ruolo di directory in locale
        - Esperienza di accesso trasparente per gli utenti
    - Svantaggi
        - Richiede la sincronizzazione dell'hash password
        - Richiede un servizio di firma
- Federata tra l'ambiente locale e il cloud
    - Vantaggi
        - Directory integrata locale e nel cloud.
        - Abilita Single Sign-On per gli utenti.
        - Il reparto IT può applicare comunque la protezione avanzata del server con il ruolo di directory in locale.
        - Esperienza di accesso trasparente per gli utenti.
        - Più affidabile per le soluzioni che richiedono l'integrazione con altri servizi directory.
        Richiede la sincronizzazione, ma non sincronizza le password.
    - Svantaggi
        - Richiede un servizio di firma.
        - Richiede un'infrastruttura server per la federazione.
        - Richiede un certificato per proteggere la comunicazione tra il server federativo e il servizio cloud.

Gli ambienti ibridi che richiedono la connettività con i servizi cloud dai dispositivi degli utenti possono sfruttare l'integrazione tra [Azure Active Directory](https://azure.microsoft.com/en-us/documentation/articles/active-directory-whatis/) e Servizi di dominio Active Directory. In uno [scenario di identità per gli ambienti ibridi](https://technet.microsoft.com/library/dn550987.aspx) le aziende che vogliono mantenere l'autenticazione utente trasparente possono scegliere tra le opzioni seguenti:

- Sincronizzazione della directory con Sincronizzazione password: viene usato DirSync con la [sincronizzazione dell'hash password](https://technet.microsoft.com/library/dn246918.aspx) tra Servizi di dominio Active Directory e Azure AD.
- Autenticazione federata con Single Sign-On: gli attributi utente vengono sincronizzati mediante DirSync. L'autenticazione viene passata attraverso la federazione (AD FS) e completata da Servizi di dominio Active Directory (AD DS).

Quando si usa il servizio Registrazione dispositivo in Windows 8.1, viene installato un certificato in un dispositivo dell'utente e viene creato un record di dispositivo in AD DS con il numero di identificazione personale del certificato. Questo il collegamento tra il dispositivo e l'utente consente al reparto IT di tenere traccia di quali dispositivi vengono registrati da ogni utente. Questa funzionalità non richiede un'infrastruttura a chiave pubblica dell'organizzazione. Il servizio Registrazione dispositivo è disponibile anche in Azure AD per Windows 10. Per altre informazioni su Registrazione dispositivo con Azure AD e Windows 10, leggere [Introduzione a Registrazione dispositivo Azure Active Directory](https://azure.microsoft.com/en-us/documentation/articles/active-directory-conditional-access-device-registration-overview/).

## Autenticazione e autorizzazione

La decisione di consentire agli utenti di accedere alle app e ai dati dai propri dispositivi deve garantire che gli utenti vengano identificati in un processo di autenticazione attendibile e che siano autorizzati a usare le risorse richieste. È necessario rivedere i criteri di autenticazione e autorizzazione correnti e considerare le domande seguenti:

- Quali sono i requisiti di autenticazione per gli utenti perché possano accedere in remoto alle app aziendali dai propri dispositivi?
- La piattaforma corrente è in grado di applicare l'autorizzazione in base all'utente e all'app senza che sia necessario riscrivere le app?
- È possibile applicare Multi-Factor Authentication in base alla posizione di un utente?

L'autenticazione e l'autorizzazione sono gestite da AD FS con AD DS. I dati in fase di trasferimento nel data center useranno anche il protocollo HTTPS durante la connessione al ruolo File server e ai servizi di autenticazione.

Per applicare Multi-Factor Authentication, le società possono usare le funzionalità incorporate in AD FS o [Azure Multi-Factor Authentication (MFA)](https://azure.microsoft.com/en-us/documentation/articles/multi-factor-authentication/). Usando questa funzionalità di Azure, il reparto IT può applicare l'autenticazione a più fattori per gli utenti che accedono alle risorse aziendali tramite Internet. Per altre informazioni sull'autenticazione a più fattori, vedere [Gestire i rischi con l'autenticazione a più fattori aggiuntiva per le applicazioni con esigenze particolari](https://technet.microsoft.com/library/dn280949.aspx).

Per imporre l'autorizzazione per le app per gli utenti che vi accedono da una rete esterna o interna, il reparto IT può sfruttare Proxy applicazione Web, che consente di creare regole specifiche per applicare l'autenticazione e l'autorizzazione in combinazione con AD FS. La pubblicazione di Proxy applicazione Web funziona per qualsiasi dispositivo dell'utente: computer portatili personali, tablet o smartphone. Inoltre, gli utenti non devono installare software aggiuntivo nei loro dispositivi per accedere alle app pubblicate. Proxy applicazione Web funge da proxy inverso per qualsiasi app da esso pubblicata e, di conseguenza, l'esperienza utente è la stessa che si avrebbe se i dispositivi degli utenti fossero collegati direttamente alle app. Per informazioni sul Proxy applicazione Web, vedere [Guida alla distribuzione di Proxy applicazione Web](https://technet.microsoft.com/library/dn280944.aspx).

>[!NOTE] Nota: in caso di scenario ibrido, se è necessaria un'esperienza utente ottimale in termini di autenticazione e autorizzazione, leggere [Considerazioni di progettazione dell'identità ibrida di Azure Active Directory](http://aka.ms/azhidcg).

## Criteri e conformità

Le considerazioni sui criteri e la conformità devono avere la priorità in una strategia basata sul modello BYOD. Alcune aziende potrebbero avere requisiti rigidi che non rientrano in questo modello a causa delle regole aziendali. Una società che sta passando a una strategia incentrata sulle persone deve comprendere i criteri correnti e quali effetti avrà il modello BYOD su questi criteri. È necessario considerare i requisiti di classificazione dei dati e come il reparto IT può avere il controllo della classificazione dei dati, anche quando sono inattivi nello spazio di archiviazione del dispositivo. Quando si pensa alla classificazione dei dati, è importante essere in grado di classificare i dati durante l'esecuzione di alcune operazioni, ad esempio la modifica di un file.

È consigliabile applicare i criteri da una posizione centralizzata per consentire al reparto IT di rispondere rapidamente in caso di modifiche ad hoc che avranno effetto su tutti gli utenti. Considerare inoltre l'uso di funzionalità di controllo affidabili per dispositivi mobili. Se si verifica una violazione, è essenziale che il reparto IT possa tenere traccia dei criteri che sono stati violati, di chi ha eseguito l'operazione e quando.
    
### Criteri e conformità: funzionalità e considerazioni

L'elenco riportato di seguito consente di comprendere le considerazioni sulle funzionalità relative a criteri e conformità:

- Classificazione dei dati
    - Applicare la classificazione dei dati quando il contenuto viene salvato e modificato
    - Il reparto IT deve essere in grado di classificare i dati inattivi nel centro dati e nel dispositivo dell'utente
- Gestione centralizzata
    - Il reparto IT deve essere in grado di gestire la classificazione dei dati da un'unica posizione, anche se i dati si trovano in più dispositivi
    - Gli ambienti IT ibridi devono essere in grado di gestire le risorse locali e nel cloud
- Integrazione con servizi directory
    - Il reparto IT deve essere in grado di usare il servizio directory corrente come repository di identità
- Controllo e registrazione
    - Il reparto IT deve essere in grado di controllare l'accesso alle risorse e aumentare la capacità di registrazione, se necessario.


L'applicazione della governance dei dati nei vari file server per controllare quali utenti possono accedere alle informazioni e controllare chi ha avuto accesso alle informazioni è un elemento chiave per un ambiente BYOD. In Windows Server 2012 R2 questa operazione può essere eseguita usando [Controllo dinamico degli accessi](https://technet.microsoft.com/library/dn408191.aspx), basato sugli investimenti nell'infrastruttura che possono essere usati dai partner e dalle applicazioni line-of-business. Le funzionalità di Controllo dinamico degli accessi possono offrire un grande valore per le organizzazioni che usano Servizi di dominio Active Directory.

Quando si sfruttando le funzionalità di Controllo dinamico degli accessi, è possibile identificare i dati mediante la classificazione automatica e manuale dei file. È ad esempio possibile contrassegnare i dati nei file server nell'organizzazione. Si può anche controllare l'accesso ai file applicando criteri di sicurezza di rete che usano criteri di accesso centrale. Controllo dinamico degli accessi si avvale anche della protezione di Rights Management Services (RMS) tramite la crittografia RMS automatica per i documenti riservati. È ad esempio possibile configurare RMS per crittografare tutti i documenti contenenti informazioni sulla legge HIPPA (Health Insurance Portability and Accountability Act). Per indagini forensi e controlli, i criteri di controllo centrale possono essere usati per i rapporti di conformità e le analisi forensi. È possibile identificare chi ha accesso a informazioni riservate.

Controllo dinamico degli accessi, una funzione del ruolo File server, garantisce ai reparti IT le funzionalità elencate nella tabella precedente. Per altre informazioni su Controllo dinamico degli accessi, vedere [Controllo dinamico degli accessi: panoramica dello scenario](https://technet.microsoft.com/library/hh831717.aspx).


<!--HONumber=Apr16_HO4-->


