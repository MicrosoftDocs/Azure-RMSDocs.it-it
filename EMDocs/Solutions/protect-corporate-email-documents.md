---
# required metadata

title: Proteggere messaggi di posta elettronica e documenti aziendali
description:
keywords:
author: karthikaraman
manager: swadhwa
ms.date: 04/28/2016
ms.topic: article
ms.prod:
ms.service:
ms.technology:
ms.assetid: 78d8368e-1bfe-4ac4-991d-467321a76ed7

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer:
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Protezione dei messaggi di posta elettronica e dei documenti aziendali
La protezione dei messaggi di posta elettronica aziendali prevede due obiettivi principali:

-   Consentire solo a dispositivi compatibili di accedere alla posta elettronica dell'azienda

-   Proteggere il contenuto nei messaggi di posta elettronica e negli allegati

## Consentire solo a dispositivi compatibili di accedere alla posta elettronica dell'azienda
Un passaggio importante per la protezione dei dati aziendali è limitare l'accesso a dispositivi che non usano una password complessa, non sono jailbroken né crittografati. Microsoft Intune offre la possibilità di impostare le condizioni che gli utenti devono soddisfare per accedere alle risorse aziendali. Questa caratteristica è nota come accesso condizionale.

L'accesso condizionale è determinato da due tipi di criteri che è possibile impostare in Intune:

I**criteri di conformità** stabiliscono la conformità di un dispositivo. Esaminano impostazioni e condizioni quali:

-   **PIN e password**: il reparto IT può creare regole per richiedere la password prima di sbloccare un dispositivo, per la complessità e la scadenza delle password nonché per altre impostazioni relative alle password.

-   **Crittografia**: il reparto IT può limitare l'accesso ai dispositivi che vengono crittografati.

-   **Dispositivo non jailbroken o rooted**: Intune può rilevare se un dispositivo registrato è jailbroken e il reparto IT può impostare i criteri per bloccare l'accesso a tale dispositivo.

I**criteri di accesso condizionale** sono configurati per un determinato servizio, ad esempio Exchange Online o SharePoint Online. Per ogni servizio, è possibile definire i gruppi di utenti a cui devono essere applicati questi criteri. È possibile ad esempio assicurarsi che tutti i dipendenti del reparto contabilità possano accedere alla posta elettronica aziendale solo da dispositivi registrati e conformi.

## Esperienza generale dell'utente finale:
Dopo aver implementato la soluzione, gli utenti finali potranno accedere alla posta elettronica aziendale solo sui dispositivi gestiti e conformi. Quando accedono alla posta elettronica sui dispositivi, i dati dell'azienda sono protetti e contenuti all'interno dell'ecosistema di app e sono disponibili unicamente agli utenti previsti. L'accesso potrà essere revocato in qualsiasi momento se il dispositivo risulta non conforme.

In particolare, i criteri di accesso condizionale configurati in Intune fanno sì che i dispositivi possano accedere alla posta elettronica solo se sono conformi ai criteri di conformità impostati. Alcune azioni, ad esempio le operazioni Copia e Incolla oppure il salvataggio nei servizi di archiviazione cloud personale, possono essere limitate usando i criteri di gestione delle applicazioni mobili. Il servizio di Azure Rights Management può essere usato per fare in modo che i dati sensibili di posta elettronica e gli allegati inoltrati possano essere letti solo dai destinatari. L'esperienza dell'utente finale è descritta in dettaglio in [Esperienza utente finale di accesso condizionale](end-user-experience-conditional-access.md).


Guardare [questo](https://www.youtube.com/watch?feature=player_embedded&v=lYx3YIezccg) video di quattro minuti per vedere come l'accesso condizionale influisce sugli utenti finali.

## Importanza dell'architettura
I diversi componenti di EMS e Office 365 sono compilati e progettati per l'esecuzione nel cloud portando tutti i vantaggi offerti dal cloud: scalabilità, flessibilità e facilità di gestione.

Poiché aziende diverse hanno requisiti diversi, EMS è progettato per integrarsi con l'infrastruttura locale esistente, ad esempio Active Directory, Exchange Server o System Center Configuration Manager. In questo modo è possibile usare le credenziali già definite nella rete sia per le risorse locali che per quelle cloud.

Le sezioni seguenti descrivono l'architettura progettata per l'esecuzione nel cloud e illustrano brevemente l'opzione locale.

### Flusso di accessi alla posta elettronica
A seconda del tipo di applicazione di posta elettronica usato per accedere a Exchange Online, il percorso per stabilire l'accesso protetto alla posta elettronica può essere variare leggermente. Tuttavia, i componenti chiave, Azure Active Directory (Azure AD), Office 365/Exchange Online e Microsoft Intune, sono gli stessi. Anche l'esperienza del reparto IT e quella dell'utente finale sono simili. EMS supporta attualmente app di posta elettronica native e l'app Microsoft Outlook per iOS e Android.

### Flusso di controllo degli accessi per le applicazioni di posta elettronica native
I client di Exchange ActiveSync (EAS) che provano ad accedere alla posta elettronica in Exchange Online verranno esaminati in base alle proprietà seguenti:

-   Il dispositivo è gestito da Intune?

-   Il dispositivo è registrato con Azure Active Directory?

-   Il dispositivo è compatibile?

-   L'ID EAS del client è mappato a un dispositivo registrato?

Per ottenere uno stato conforme, il dispositivo in cui è in esecuzione il client EAS deve:

-   Essere registrato con Intune

-   Registrarsi con [Azure Active Directory](https://msdn.microsoft.com/en-us/6a14cb1f-a058-4453-8ede-d9f4a66a7073.aspx)

-   Essere conforme ai criteri del dispositivo impostati dall'amministratore IT.

Nella maggior parte delle piattaforme, la registrazione del dispositivo con Azure Active Directory viene eseguita automaticamente durante il processo di registrazione. Gli stati del dispositivo vengono scritti da Intune in Azure Active Directory e quindi letti da Exchange Online la volta successiva che il client EAS prova a ricevere la posta elettronica. Se il dispositivo non è registrato, l'utente riceverà un messaggio nella posta in arrivo con le istruzioni su come eseguire la registrazione. Se il dispositivo non è conforme, l'utente riceverà un messaggio di posta elettronica diverso che lo reindirizza al portale Web Intune dove può ottenere altre informazioni sul problema della conformità e su come risolverlo.

**Azure AD**autentica l'utente e il dispositivo, Microsoft Intune gestisce la conformità e criteri di accesso condizionale e **Exchange Online** gestisce l'accesso alla posta elettronica in base allo stato del dispositivo.

![Immagine che illustra il flusso di controllo di accesso per le app di posta elettronica native sui dispositivi iOS e Android](./media/ProtectEmail/Access-Control-Flow-For-Native-Email-Apps.png)

### Flusso di controllo degli accessi per le applicazioni Outlook
Analogamente al client EAS, l'app di posta elettronica Outlook che prova ad accedere alla posta elettronica in Exchange Online verrà esaminata in base alle proprietà seguenti:

-   Il dispositivo è gestito da Intune?

-   Il dispositivo è registrato con Azure Active Directory?

-   Il dispositivo è compatibile?

La conformità del dispositivo viene stabilita perlopiù in modo analogo a quanto descritto nel flusso di controllo degli accessi del client EAS. Tuttavia, per le app Outlook il flusso tra i componenti è leggermente diverso. Quando l'app Outlook prova a ricevere la posta elettronica, viene reindirizzata ad Azure AD. Azure AD rilascia un token di sicurezza se il dispositivo viene considerato conforme e idoneo per la registrazione. Il token di sicurezza viene quindi usato per ricevere la posta elettronica aziendale da Exchange Online. La sincronizzazione della posta elettronica viene effettivamente negoziata mediante il servizio cloud di Outlook, che ottiene un token di accesso al servizio EAS per conto dell'utente per completare l'autenticazione e recapita i messaggi di posta elettronica.

![Immagine che illustra il flusso di controllo di accesso per l'app Outlook](./media/ProtectEmail/Access-Control-Flow-For-Outlook-App.png)

## Esperienza dell'amministratore IT:
Questo processo non prevede alcuna installazione complessa dell'infrastruttura necessaria per Azure AD o Exchange. Gli amministratori IT:

-   Configurano e distribuiscono i criteri di conformità che vengono usati per esaminare lo stato di conformità del dispositivo.

-   Configurano i criteri di accesso condizionale di Exchange Online e specificano i gruppi di sicurezza di Azure AD che saranno interessati o esentati da questi criteri.

-   Scelgono di consentire o bloccare i dispositivi che non sono idonei per la registrazione in Intune. L'elenco dei sistemi operativi supportati per i dispositivi mobili è illustrato più avanti.

È prevista una fase di installazione facoltativa che potrebbe essere necessaria. La creazione di report che viene usata per gestire e monitorare lo stato e l'accesso ai dispositivi richiede l'installazione di Microsoft Intune Service to Service Connector.

## Esperienza dell'utente finale:
Quando l'utente prova ad accedere alla posta elettronica sul dispositivo per la prima volta o successivamente a eseguire la sincronizzazione, viene controllato lo stato della registrazione e di conformità del dispositivo. Il processo di registrazione o risoluzione dei problemi di conformità è un'esperienza interattiva. All'utente finale vengono forniti i passaggi necessari per registrare il dispositivo e renderlo conforme senza dover contattare l'help desk IT:

-   **Se il dispositivo non è registrato**, nella pagina di accesso viene visualizzato un messaggio di accesso negato e viene chiesto di eseguire la registrazione. Alla registrazione, il dispositivo viene registrato automaticamente in Azure Active Directory. Intune verifica la conformità del dispositivo e fornisce i passaggi correttivi per risolvere eventuali problemi di non conformità. Una volta che il dispositivo è conforme, Intune imposta lo stato di conformità del dispositivo con Azure Active Directory.

-   **Se il dispositivo è registrato ma non è conforme**, viene inviato al dispositivo un collegamento con i passaggi per risolvere i problemi. Quando l'utente finale corregge il problema, ad esempio relativo all'impostazione della password o alla crittografia, Intune che gestisce i criteri di conformità aggiorna lo stato di conformità del dispositivo in Azure AD.

Una volta che il dispositivo viene considerato registrato e conforme, entro pochi minuti dovrebbe essere eseguita la sincronizzazione della posta elettronica.

## Come proseguire
Dopo avere acquisito le informazioni sulla protezione di documenti e messaggi di posta elettronica aziendali, è possibile leggere le procedure di [protezione degli allegati di posta elettronica](protect-email-attachments.md). In alternativa, se si è pronti, approfondire l'[implementazione di una soluzione per la protezione della posta elettronica aziendale](implement-solution.md).


<!--HONumber=Apr16_HO4-->


