---
# required metadata

title: Usare l'accesso condizionale con Exchange Server locale, Microsoft Intune e Configuration Manager
description:
keywords:
author: craigcaseyMSFT
manager: swadhwa
ms.date: 04/28/2016
ms.topic: article
ms.prod:
ms.service:
ms.technology:
ms.assetid: 56b6cd2d-3dea-468b-9f1c-92717c9ec5f5

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: 
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Distribuire Exchange Server locale con Microsoft Intune e Configuration Manager
Ora che si sono lette con attenzione le [indicazioni sull'architettura per la protezione di documenti e messaggi di posta elettronica aziendali](architecture-guidance-for-protecting-company-email-and-documents.md) è possibile procedere alla distribuzione di una soluzione.

Se si usano già System Center Configuration Manager ed Exchange nell'infrastruttura locale, è possibile incorporare Intune in modo da gestire l'accesso alla posta elettronica e proteggere i dati di posta elettronica nei dispositivi mobili. Il processo di alto livello per l'implementazione di questa soluzione è il seguente:

-   Configurare lo strumento Intune Exchange Connector locale nella console di Configuration Manager, in modo che questo possa comunicare con l'istanza di Exchange Server che ospita le cassette postali dei dispositivi mobili.

-   Eseguire una sincronizzazione completa del connettore Exchange Server per individuare gli utenti e per eseguire l'inventario di tutti gli ID di Exchange ActiveSync (EASID) dei dispositivi mobili che si connettono a Exchange Server locale.

-   Creare raccolte di utenti per gruppi di utenti che saranno interessati o esentati dai criteri di accesso condizionale. Creare quindi i criteri di conformità che definiscono le regole e le impostazioni che un dispositivo deve soddisfare per essere considerato conforme ai criteri di accesso condizionale.

-   Avviare l'applicazione dell'accesso condizionale.

## Flusso di controllo dell'accesso condizionale per Exchange Server locale
Questo diagramma mostra il flusso di controllo per i client che provano ad accedere alla posta elettronica di Exchange locale.

![Diagramma di flusso di controllo dell'accesso condizionale in Configuration Manager con Intune ed Exchange Server locale](./media/ProtectEmail/Hybrid-on-prem-CA-architecture.png)

-   Microsoft Intune: gestisce i criteri di conformità e di accesso condizionale per il dispositivo

-   Microsoft Azure Active Directory: autentica l'utente e fornisce lo stato di conformità del dispositivo

-   Configuration Manager: gestisce la registrazione del dispositivo e fornisce i report

-   Exchange locale: applica l'accesso alla posta elettronica in base allo stato del dispositivo

## Prima di iniziare
Assicurarsi che l'ambiente presenti questi requisiti per l'implementazione di questa soluzione.

> [!NOTE]
> Se Configuration Manager è già stato configurato per gestire i dispositivi mobili con il servizio Intune, è possibile passare a [Passaggi per la distribuzione](#deployment-steps).

-   Verificare che i [requisiti hardware per On-Premises Connector](/intune/get-started/network-infrastructure-requirements-for-microsoft-intune) siano soddisfatti.

-   Verificare che sia in esecuzione System Center 2012 R2 Configuration Manager SP1 con aggiornamento cumulativo 1 o versione successiva.

-   Assicurarsi che l'[endpoint di Servizi Web Exchange (EWS)](https://technet.microsoft.com/library/hh529912.aspx) sia configurato correttamente per l'individuazione. Se necessario, contattare il team di supporto di Configuration Manager per uno strumento che consenta di identificare i problemi di connessione EWS. EWS consente agli sviluppatori di interagire con le cassette postali di Exchange e il contenuto usando il protocollo HTTP standard.

-   Installare e assegnare i servizi di Exchange a un [certificato digitale valido ](https://technet.microsoft.com/library/dd351044.aspx) acquistato da un'autorità di certificazione pubblica attendibile.

-   Configurare un account (amministratore locale o di dominio) con le autorizzazioni per eseguire i cmdlet di Exchange Server seguenti:

    Clear-ActiveSyncDevice

    Get-ActiveSyncDevice

    Get-ActiveSyncDeviceAccessRule

    Get-ActiveSyncDeviceStatistics

    Get-ActiveSyncMailboxPolicy

    Get-ActiveSyncOrganizationSettings

    Get-ExchangeServer

    Get-Recipient

    Set-ADServerSettings

    Set-ActiveSyncDeviceAccessRule

    Set-ActiveSyncMailboxPolicy

    Set-CASMailbox

    New-ActiveSyncDeviceAccessRule

    New-ActiveSyncMailboxPolicy

    Remove-ActiveSyncDevice

> [!IMPORTANT]
> Se si prova a installare o a usare il connettore Exchange Server senza i cmdlet necessari, viene visualizzato un errore, che viene registrato con il messaggio _Chiamata del cmdlet &lt;cmdlet&gt; non riuscita nel file EasDisc.log nel computer del server del sito_.

## Passaggi per la distribuzione
Seguire questi passaggi per distribuire la soluzione Exchange locale:

### Passaggio 1: Verificare che sia installato il ruolo del connettore Intune.
Assicurarsi che sia installato il ruolo del connettore Intune in modo che Configuration Manager possa interagire con Intune. Per altre informazioni, vedere [Gestire i dispositivi mobili con Configuration Manager e Microsoft Intune](https://technet.microsoft.com/en-us/library/JJ884158.aspx) .

### Passaggio 2: Installare e configurare un connettore Exchange Server.
Configuration Manager supporta un solo connettore in un'organizzazione Exchange.

> [!IMPORTANT]
> Prima di installare il connettore Exchange Server, confermare il supporto della versione di Microsoft Exchange usata da parte di Configuration Manager. Per altre informazioni, vedere [Configurazioni supportate per Configuration Manager](https://technet.microsoft.com/en-us/library/gg682077.aspx).

Per installare e configurare il connettore Exchange Server, seguire i passaggi illustrati nell'argomento [Come gestire i dispositivi mobili utilizzando Configuration Manager e Exchange](https://technet.microsoft.com/en-us/library/gg682001.aspx) .

### Passaggio 3: Eseguire una sincronizzazione completa per individuare gli utenti.

1.  Nella console di Configuration Manager, fare clic su **Amministrazione**, espandere **Configurazione della gerarchia**e quindi selezionare **Connettori Exchange Server**.

2.  Selezionare il connettore Exchange Server che è stato installato nel passaggio 2.

3.  Fare clic su **Sincronizza ora**.

    ![Screenshot che illustra come eseguire una sincronizzazione completa nella console di Configuration Manager](./media/ProtectEmail/Hybrid-Onprem-Run-FullSync.png)

La sincronizzazione completa può richiedere diverse ore, a seconda del numero di dispositivi. Una sincronizzazione completa verrà eseguita una volta ogni 24 ore per impostazione predefinita. Una sincronizzazione delta individua le connessioni ai dispositivi dopo la sincronizzazione completa precedente e viene eseguita per ogni intervallo impostato durante l'installazione del connettore Exchange Server. Ciò garantisce che vengano rilevati rapidamente nuovi utenti (e nuovi utenti di Exchange) in modo che sia possibile applicare l'accesso condizionale.

Con lo strumento di registro traccia di Configuration Manager è possibile aprire il file EasDisc.log, che si trova nella cartella **Microsoft Configuration Manager/Logs** in cui è installato Configuration Manager, per verificare che il connettore sia in esecuzione e invii query per le connessioni ai dispositivi. Al termine della sincronizzazione completa, verrà eseguito l'inventario di tutti gli ID di Exchange ActiveSync (EASID) dei dispositivi mobili che si connettono a Exchange locale.

### Passaggio 4: Creare raccolte di utenti.
Determinare i gruppi di utenti di Intune a cui saranno destinati i criteri di accesso condizionale. Creare quindi raccolte di utenti per gruppi di utenti che saranno interessati o esentati dai criteri di accesso condizionale. Quando si applica l'accesso condizionale in un secondo momento, sarà necessario specificare tali gruppi.

Per creare raccolte di utenti, seguire i passaggi in [Come creare raccolte in Configuration Manager](https://technet.microsoft.com/en-us/library/gg712295.aspx) .

### Passaggio 5: Creare criteri di conformità e distribuirli agli utenti.
I criteri di conformità definiscono le regole e le impostazioni che un dispositivo deve soddisfare per essere considerato conforme ai criteri di accesso condizionale. Per creare i criteri di conformità, seguire i passaggi in [Criteri di conformità in Configuration Manager](https://technet.microsoft.com/en-us/library/mt131417.aspx) .

Se si vuole avere la possibilità di rimuovere tutti i messaggi di posta elettronica aziendale da un dispositivo iOS quando non fa più parte dell'azienda, è necessario creare e distribuire un profilo di posta elettronica e quindi impostare i criteri di conformità che specificano che i profili di posta elettronica sono gestiti da Intune. È necessario distribuire il profilo di posta elettronica allo stesso set di utenti a cui sono destinati questi criteri di conformità.

![Screenshot che illustra la pagina "Regole" della Creazione guidata criteri di conformità in cui è possibile specificare che un profilo di posta elettronica deve essere gestito da Intune](./media/ProtectEmail/Hybrid-Onprem-ExchSrvr-Wizard6.PNG)

Se si specificano questi criteri di conformità, un utente che ha già configurato il proprio account di posta elettronica dovrà rimuoverlo manualmente. Intune quindi lo aggiungerà nuovamente attraverso il processo di registrazione descritto in [Esperienza utente finale di accesso condizionale](end-user-experience-conditional-access.md).

Dopo aver creato i criteri di conformità, selezionare il nome del criterio di conformità nell'elenco e fare clic su **Distribuisci**.

### Passaggio 6: Configurare i criteri di accesso condizionale.
Prima di tutto, decidere come e quando si vuole applicare l'accesso condizionale e quali dipendenti ne saranno interessati. Seguire quindi i passaggi elencati in [Accesso condizionale per la posta elettronica di Exchange in Configuration Manager](https://technet.microsoft.com/en-us/library/mt131421.aspx) per configurare i criteri di accesso condizionale per Exchange locale.

### Passaggio 7: Monitorare le registrazioni e applicare l'accesso condizionale.
Se si ha già un numero significativo di utenti iscritti a Intune e conformi, è possibile avviare l'applicazione dell'accesso condizionale distribuendolo a circa 500 utenti al giorno. Ciò richiederà circa 4-5 mesi per 70.000 utenti e consente di ordinare gli eventuali problemi che potrebbero verificarsi senza limitare l'accesso alla posta elettronica a troppi utenti nello stesso momento.

Se il numero di utenti già registrati in Intune non è elevato, l'accesso condizionale offre una procedura di registrazione guidata, come descritto in [Esperienza utente finale di accesso condizionale](end-user-experience-conditional-access.md).

## Passaggi di verifica
Usando lo strumento di registro traccia di Configuration Manager, aprire il file EasDisc.og (nella cartella Microsoft Configuration Manager/Logs in cui è installato Configuration Manager). Cercare il file di log "Exchange Connector" per trovare informazioni sull'eventuale esecuzione dei Exchange Connector e sul numero di dispositivi connessi.

![Screenshot che illustra il file EasDisc.log aperto nello strumento per il log di traccia di Configuration Manager](./media/ProtectEmail/Hybrid-Onprem-Eas-DiscLog-Sample.PNG)

Lo strumento per il log di traccia di Configuration Manager è incluso in [System Center 2012 R2 Configuration Manager Toolkit](http://www.microsoft.com/en-us/download/details.aspx?id=50012).

## Reporting
È possibile usare la console di Configuration Manager per visualizzare informazioni specifiche sui dispositivi che sono stati individuati da Exchange Connector. Per i dispositivi a cui viene applicato l'accesso condizionale, è possibile visualizzare lo stato corrente di ogni dispositivo, l'ultima volta che il dispositivo si è connesso al server Exchange e così via.

Nella console di Configuration Manager fare clic su **Asset e conformità** e quindi fare clic su **Dispositivi**. È possibile visualizzare lo stato corrente di ogni dispositivo (Bloccato o Consentito) nella colonna **Stato di accesso di Exchange** . Aggiungere questa colonna se non è già visualizzata facendo clic con il pulsante destro del mouse sull'area della barra del titolo della colonna. È anche possibile visualizzare l'ora dell'ultima sincronizzazione riuscita per ogni dispositivo come riportato da Exchange aggiungendo la colonna **Ultima sincronizzazione riuscita in Exchange Server** .

![Screenshot che illustra un elenco di dispositivi nella console di Configuration Manager](./media/ProtectEmail/Hybrid-Onprem-Verify-Devices-State.png)

Se si esegue SQL Server Reporting Services (SSRS), è possibile visualizzare un report di accesso condizionale che mostra lo stato di conformità dei dispositivi, se è stato installato e in esecuzione Exchange Connector e lo stato di accesso EAS. Fornirà anche  informazioni sulla registrazione di Active Directory, l'attivazione EAS, nonché il proprietario del dispositivo.

![Screenshot che illustra un esempio di report di SQL Server Reporting Services](./media/ProtectEmail/Hybrid-Reports-CA.png)

Per visualizzare i report SSRS, è necessario aver installato un ruolo report nel server primario:

1.  In Configuration Manager, fare clic su **Amministrazione**, fare clic su **Configurazione della gerarchia**, fare clic su **Configurazione del sito**e quindi fare clic su **Server e ruoli del sistema del sito**.

2.  Selezionare un server e fare clic su **Aggiungi ruoli del sistema del sito** per aprire l'aggiunta guidata ruoli del sistema del sito.

3.  Nella pagina Selezione ruolo del sistema selezionare la casella di controllo **Punto di Reporting Services** . Il punto di Reporting Services mostra i report relativi alla gestione dei client.

4.  Fare clic su **Avanti**.

Di seguito viene illustrato lo stato della distribuzione dei criteri di configurazione:

![Screenshot che illustra lo stato della distribuzione dei criteri di configurazione](./media/ProtectEmail/Hybrid-Reports-Deployment-Status.png)

### Latenza
Un dispositivo viene bloccato non appena viene individuato da Exchange Connector. La latenza di blocco dipende dagli intervalli configurati per la sincronizzazione completa e la sincronizzazione delta e dal tempo trascorso tra questi intervalli quando il dispositivo si connette al server di Exchange. Per impostazione predefinita, una sincronizzazione completa avviene ogni 24 ore mentre una sincronizzazione delta avviene ogni 240 minuti. Durante questo periodo di latenza, un dispositivo può essere considerato conforme.

## Come proseguire
Dopo aver distribuito una soluzione per la protezione della posta elettronica aziendale e dei dati di questa all'interno dei dispositivi mobili, è possibile scoprire di più sull'[esperienza dell'utente finale relativa all'accesso condizionale](end-user-experience-conditional-access.md). Ciò consente di prepararsi ad affrontare i problemi che potrebbero verificarsi quando gli utenti finali registrano dispositivi specifici.


<!--HONumber=Apr16_HO4-->


