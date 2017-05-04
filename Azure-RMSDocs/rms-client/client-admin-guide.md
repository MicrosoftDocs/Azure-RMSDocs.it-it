---
title: Guida dell&quot;amministratore del client Azure Information Protection
description: Istruzioni e informazioni per gli amministratori in una rete aziendale che sono responsabili della distribuzione del client Azure Information Protection per Windows.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 04/26/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 
ms.reviewer: eymanor
ms.suite: ems
ms.openlocfilehash: 74abbe0db07a155afe500388810945a3ff5a35a5
ms.sourcegitcommit: 3ff6c072a228994308402778c493727cc682c6b7
translationtype: HT
---
# <a name="azure-information-protection-client-administrator-guide"></a>Guida dell'amministratore del client Azure Information Protection

>*Si applica a: Active Directory Rights Management Services, Azure Information Protection, Windows 10, Windows 8.1, Windows 8, Windows 7 con SP1*


Usare le informazioni seguenti se si è responsabili del client Azure Information Protection in una rete aziendale o se sono necessarie maggiori informazioni rispetto a quelle disponibili nella [Guida per l'utente del client Azure Information Protection](client-user-guide.md).

Il client Azure Information Protection include gli elementi seguenti:

- Un componente aggiuntivo per Office, che installa la barra di Azure Information Protection per la selezione di etichette di classificazione, e un pulsante **Proteggi** sulla barra multifunzione per offrire altre opzioni.

- Esplora file, opzioni tramite clic con il pulsante destro del mouse per l'applicazione di etichette di classificazione e della protezione ai file.

- Un visualizzatore per visualizzare file protetti quando un'applicazione nativa non è in grado di aprirli.

- Un modulo di PowerShell per applicare e rimuovere etichette di classificazione e la protezione dei file.

- Il client Rights Management che comunica con Azure Rights Management (Azure RMS) o Active Directory Rights Management Services (AD RMS).

Il client Azure Information Protection si integra al meglio con i servizi di Azure, Azure Information Protection e il relativo servizio di protezione dei dati, Azure Rights Management. Tuttavia, con alcune limitazioni, il client Azure Information Protection si integra anche con la versione locale di Rights Management, AD RMS. Per un confronto completo delle funzionalità supportate da Azure Information Protection e AD RMS, vedere [Confronto tra Azure Information Protection e AD RMS](../understand-explore/compare-azure-rms-ad-rms.md). 

Se si usa AD RMS e si vuole passare ad Azure Information Protection, vedere [Migrazione da AD RMS ad Azure Information Protection](../plan-design/migrate-from-ad-rms-to-azure-rms.md).

**In caso di altre domande a cui questa documentazione non risponde**, visitare il [sito di Yammer su Azure Information Protection](https://www.yammer.com/AskIPTeam). 


## <a name="should-you-deploy-the-azure-information-protection-client"></a>È consigliabile distribuire il client Azure Information Protection?

Distribuire il client Azure Information Protection in uno o più dei casi seguenti:

- Si vuole classificare (e, facoltativamente, proteggere) documenti e messaggi di posta elettronica selezionando etichette dalle applicazioni di Office (Word, Excel, PowerPoint, Outlook).

- Si vuole classificare (e, facoltativamente, proteggere) documenti e messaggi di posta elettronica tramite Esplora file, che supporta altri tipi di file, la selezione multipla e le cartelle.

- Si vuole eseguire script che classifichino (e, facoltativamente, proteggano) documenti tramite comandi di PowerShell.

- Si vuole visualizzare documenti protetti quando non è installata un'applicazione nativa per visualizzare i file o questa applicazione non è in grado di aprire i documenti.

- Si vuole semplicemente proteggere file tramite Esplora file o i comandi di PowerShell.

- Si vuole che utenti e amministratori siano in grado di monitorare e revocare documenti protetti.

- Si vuole rimuovere la crittografia da file e contenitori (rimozione della protezione) in blocco per scopi di ripristino dei dati.

- Si usa Office 2010 e si vuole proteggere documenti e messaggi di posta elettronica tramite il servizio Azure Rights Management.

Esempio che mostra il componente aggiuntivo del client Azure Information Protection in un'applicazione di Office, che visualizza le etichette di classificazione per l'organizzazione, e il nuovo pulsante **Proteggi** sulla barra multifunzione:

![Barra Azure Information Protection con criterio predefinito](../media/word2016-calloutsv2.png)

## <a name="how-to-install-the-azure-information-protection-client-for-users"></a>Come installare il client Azure Information Protection per gli utenti

Prima di installare il client, verificare di avere le versioni del sistema operativo e le applicazioni per il client di Azure Information Protection richieste: [Requisiti per Azure Information Protection](../get-started/requirements-azure-rms.md). 

Altri prerequisiti per il client di Azure Information Protection:

- Per impostazione predefinita, l'installazione completa del client Azure Information Protection richiede almeno Microsoft .NET Framework 4.6.2. Se questo prerequisito non è soddisfatto, il programma di installazione prova a scaricare e installare la versione richiesta. Quando questo prerequisito viene installato come parte dell'installazione del client, è necessario riavviare il computer. Anche se non è consigliabile, è possibile ignorare questo prerequisito con un parametro di installazione personalizzata.

- Se il visualizzatore Azure Information Protection viene installato separatamente, è necessario Microsoft .NET Framework 4.5.2 come versione minima. Se questo non è presente, il programma di installazione non lo scarica e installa.

- Il modulo PowerShell richiede Windows PowerShell versione 4.0, che potrebbe essere necessario installare in sistemi operativi precedenti. Per altre informazioni, vedere [How to Install Windows PowerShell 4.0](http://social.technet.microsoft.com/wiki/contents/articles/21016.how-to-install-windows-powershell-4-0.aspx) (Come installare Windows PowerShell 4.0). Il programma di installazione non controlla né installa questo prerequisito per l'utente. Per verificare quale versione di Windows PowerShell è in esecuzione, digitare **$PSVersionTable** in una sessione di PowerShell.

- I computer con Windows 7 Service Pack 1 richiedono l'aggiornamento KB 2533623. Per altre informazioni su questo aggiornamento, vedere [Avviso di sicurezza Microsoft: possibile esecuzione di codice remoto durante un caricamento della libreria non protetto](https://support.microsoft.com/en-us/kb/2533623). Questo aggiornamento può essere installato direttamente dall'utente. In alternativa, è possibile sostituirlo con un altro aggiornamento che lo installa automaticamente.
    
    Se questo aggiornamento richiesto non è installato, l'installazione client avvisa che è necessario installarlo. Questo aggiornamento può essere installato dopo l'installazione del client. Alcune azioni, tuttavia, verranno bloccate e verrà visualizzato di nuovo l'avviso.  

> [!NOTE]
> Per l'installazione sono necessarie autorizzazioni di amministratore locale.

Il client di Azure Information Protection è anche incluso nel Microsoft Update Catalog, per cui è possibile installare e aggiornare il client tramite qualsiasi servizio di aggiornamento software che usa il catalogo. 

1. Scaricare il client di Azure Information Protection dall'[Area download Microsoft](https://www.microsoft.com/en-us/download/details.aspx?id=53018). 
    
    Se è disponibile una versione di anteprima, mantenerla solo a scopo di test. Le versioni di questo tipo non sono progettate per l'uso in un ambiente di produzione. 

2. Per un'installazione predefinita, basta eseguire il file eseguibile, ad esempio **AzInfoProtection.exe**. Al contrario, per visualizzare le opzioni di installazione, eseguire prima di tutto l'eseguibile con **/help**: `AzInfoProtection.exe /help`

    Esempio per installare automaticamente il client: `AzInfoProtection.exe /quiet`
    
    Esempio per installare automaticamente solo i cmdlet di PowerShell: `AzInfoProtection.exe  PowerShellOnly=true /quiet`
    
    Nella schermata della Guida non sono elencati i parametri seguenti:
    
    - **ServiceLocation**: usare questo parametro se si installa il client in computer che eseguono Office 2010 e gli utenti non sono amministratori locali dei rispettivi computer o non si vuole che vengano visualizzati messaggi di richiesta. [Altre informazioni](#more-information-about-the-servicelocation-installation-parameter) 
    
    - **DowngradeDotNetRequirement**: usare questo parametro per ignorare il requisito relativo a Microsoft .NET Framework versione 4.6.2. [Altre informazioni](#more-information-about-the-downgradedotnetrequirement-installation-parameter)

3. Se si sceglie l'installazione interattiva, selezionare l'opzione per l'installazione di un **criterio demo** se non si riesce a connettersi a Office 365 o ad Azure Active Directory, ma si vuole esaminare e provare il lato client di Azure Information Protection usando un criterio locale per scopi dimostrativi. Quando il client si connette a un servizio di Azure Information Protection, questo criterio demo viene sostituito dai criteri di Azure Information Protection dell'organizzazione.
    
4. Per completare l'installazione: 

    - Se nel computer viene eseguito Office 2010, riavviare il computer. 
        
        Se il client non è stato installato con il parametro ServiceLocation, quando si apre per la prima volta una delle applicazioni di Office che usano la barra di Azure Information Protection, ad esempio Word, è necessario confermare tutti i messaggi relativi all'aggiornamento del Registro di sistema per il primo utilizzo. Per il popolamento delle chiavi del Registro di sistema, viene usata l'[individuazione dei servizi](../rms-client/client-deployment-notes.md#rms-service-discovery). 
    
    - Per le altre versioni di Office, riavviare tutte le applicazioni di Office e tutte le istanze di Esplora file. 
        
5. È possibile verificare se l'installazione è stata completata controllando il file di log di installazione, che per impostazione predefinita viene creato nella cartella %temp%. È possibile modificare questo percorso con il parametro di installazione **/log**. 
 
    Questo file ha il formato di denominazione seguente: `Microsoft_Azure_Information_Protection_<number>_<number>_MSIP.Setup.Main.msi.log`
    
    Ad esempio: **Microsoft_Azure_Information_Protection_20161201093652_000_MSIP.Setup.Main.msi.log**
    
    In questo file di log, cercare la stringa seguente: **Product: Microsoft Azure Information Protection -- Installation completed successfully.** (Prodotto: Microsoft Azure Information Protection -- Installazione completata.) Se l'installazione non è riuscita, questo file di log contiene informazioni dettagliate per identificare e risolvere i problemi.

### <a name="more-information-about-the-servicelocation-installation-parameter"></a>Altre informazioni sul parametro di installazione ServiceLocation

Quando si installa il client per gli utenti che usano Office 2010 e che non hanno autorizzazioni di amministratore locale, specificare il parametro ServiceLocation e l'URL per il servizio Azure Rights Management. Questo parametro e il relativo valore consentono di creare e impostare le chiavi del Registro di sistema seguenti:

HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\MSDRM\ServiceLocation\Activation

HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\MSDRM\ServiceLocation\EnterprisePublishing

HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSDRM\ServiceLocation\EnterprisePublishing

HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSDRM\ServiceLocation\Activation

Usare la procedura seguente per identificare il valore da specificare per il parametro ServiceLocation. 

#### <a name="to-identify-the-value-to-specify-for-the-servicelocation-parameter"></a>Per identificare il valore da specificare per il parametro ServiceLocation

1. Da una sessione di PowerShell eseguire prima di tutto [Connect-AadrmService](https://docs.microsoft.com/powershell/aadrm/vlatest/connect-aadrmservice) e specificare le credenziali di amministratore per connettersi al servizio Azure Rights Management. Eseguire quindi [Get-AadrmConfiguration](https://docs.microsoft.com/powershell/aadrm/vlatest/get-aadrmconfiguration). 
 
    Se non è stato ancora installato il modulo di PowerShell per il servizio Azure Rights Management, vedere [Installazione di Windows PowerShell per Azure Rights Management](../deploy-use/install-powershell.md).

2. Nell'output identificare il valore **LicensingIntranetDistributionPointUrl** .

    Ad esempio, **LicensingIntranetDistributionPointUrl   : https://5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com/_wmcs/licensing**

3. In questo valore rimuovere **/_wmcs/licensing** dalla stringa. Ad esempio: **https://5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com**

    La stringa rimanente è il valore da specificare per il parametro ServiceLocation.

Esempio per installare il client in modo invisibile all'utente per Office 2010 e Azure RMS: `AzInfoProtection.exe /quiet ServiceLocation=https://5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com`


### <a name="more-information-about-the-downgradedotnetrequirement-installation-parameter"></a>Altre informazioni sul parametro di installazione DowngradeDotNetRequirement installation

Per il supporto degli aggiornamenti automatici tramite Windows Update e per l'integrazione affidabile con le applicazioni di Office, il client Azure Information Protection usa Microsoft .NET Framework versione 4.6.2. Per impostazione predefinita, il programma di installazione controlla se questa versione è presente e, in caso negativo, prova a installarla. A questo punto, il computer deve essere riavviato.

Se l'installazione di questa versione più recente di Microsoft .NET Framework non è una soluzione efficace, è possibile installare il client con il parametro **DowngradeDotNetRequirement=True**, in modo da ignorare questo requisito se è installato Microsoft .NET Framework versione 4.5.1.

Ad esempio: `AzInfoProtection.exe DowngradeDotNetRequirement=True`

È consigliabile usare questo parametro con cautela, tenendo presente che sono stati segnalati problemi di blocco delle applicazioni di Office quando il client Azure Information Protection viene usato con questa versione precedente di Microsoft .NET Framework. Se si riscontrano problemi di blocco delle applicazioni, eseguire l'aggiornamento alla versione consigliata prima di provare altre soluzioni. 

Tenere inoltre presente che, se si usa Windows Update per mantenere aggiornato il client Azure Information Protection, è necessario adottare un altro meccanismo di distribuzione del software per aggiornare il client alle versioni successive.

## <a name="additional-checks-and-troubleshooting"></a>Controlli aggiuntivi e risoluzione dei problemi

Usare l'opzione **Guida e commenti** per aprire la finestra di dialogo **Microsoft Azure Information Protection**:

- Da un'applicazione di Office: nel gruppo **Protezione** della scheda **Home** fare clic su **Proteggi** e quindi su **Guida e commenti**.

- Da Esplora file: fare clic con il pulsante destro del mouse su uno o più file o su una cartella, scegliere **Classifica e proteggi** e quindi **Guida e commenti**. 

### <a name="help-and-feedback-section"></a>Sezione **Guida e commenti**

Il collegamento **Altre informazioni** reindirizza per impostazione predefinita al sito Web di [Azure Information Protection](https://www.microsoft.com/cloud-platform/azure-information-protection), ma può essere configurato con un URL personalizzato nell'ambito delle [impostazioni dei criteri](../deploy-use/configure-policy-settings.md) di Azure Information Protection.

Usare il collegamento **Invia commenti e suggerimenti** per inviare suggerimenti o richieste al team di Information Protection. Non usare questa opzione se si vuole ottenere supporto tecnico. In questo caso, vedere invece [Opzioni di supporto e risorse per la community](../get-started/information-support.md#support-options-and-community-resources). 

L'opzione **Esporta log** consente di raccogliere e allegare automaticamente i file di log relativi al client Azure Information Protection se è stato chiesto di inviarli al supporto tecnico Microsoft. Questa opzione può essere usata anche dagli utenti finali per inviare i file di log all'help desk.

Per visualizzare informazioni di diagnostica e reimpostare il client, selezionare **Esegui la diagnostica**. Al termine dei test di diagnostica, fare clic su **Copy results** (Copia risultati) per incollare le informazioni in un messaggio di posta elettronica che l'amministratore e gli utenti finali possono inviare rispettivamente al supporto tecnico Microsoft e all'help desk. Al termine dei test, è anche possibile reimpostare il client.

Altre informazioni sull'opzione **Reset** (Reimposta):

- Non è necessario essere un amministratore locale per usare questa opzione e questa azione non viene registrata nel Visualizzatore eventi. 

- A meno che i file non siano bloccati, con questa azione vengono eliminati tutti i file presenti in **%localappdata%\Microsoft\MSIPC**, dove sono archiviati i certificati del client e i modelli per Rights Management. Non vengono eliminati i criteri di Azure Information Protection e i file di log del client, né l'utente viene disconnesso.

- Viene eliminata le chiave del Registro di sistema seguente con le relative impostazioni: **HKEY_CURRENT_USER\Software\Classes\Local Settings\Software\Microsoft\MSIPC**. Se si configurano le impostazioni per questa chiave del Registro di sistema (ad esempio le impostazioni per il reindirizzamento al tenant di Azure Information Protection poiché si sta eseguendo la migrazione da AD RMS e nella rete è ancora presente un punto di connessione del servizio), è necessario riconfigurare le impostazioni del Registro di sistema dopo la reimpostazione del client.

- Dopo aver reimpostato il client, è necessario inizializzare nuovamente l'ambiente utente. In questo modo verranno scaricati i certificati per il client e i modelli più recenti. A tale scopo, chiudere tutte le istanze di Office e quindi riavviare un'applicazione di Office. Questa azione verifica anche che siano stati scaricati i criteri di Azure Information Protection più recenti. Non eseguire di nuovo i test diagnostici prima che ciò sia stato fatto.


### <a name="client-status-section"></a>Sezione **Stato del client**

Usare il valore di **Connessione effettuata come** per verificare se il nome utente visualizzato identifica l'account da usare per l'autenticazione di Azure Information Protection. Il nome utente deve corrispondere a un account usato per Office 365 o Azure Active Directory che appartiene a un tenant configurato per Azure Information Protection.

Se è necessario accedere con un nome utente diverso da quello visualizzato, vedere la sezione [Accedere come utente diverso](#sign-in-as-a-different-user) in questa pagina.

Il campo **Ultima connessione** indica quando è stata eseguita l'ultima connessione del client al servizio Azure Information Protection dell'organizzazione e può essere usato con la data e l'ora specificate in **Il criterio di Information Protection è stato installato il giorno** per verificare quando sono stati installati o aggiornati i criteri di Azure Information Protection. Quando si connette al servizio, il client scarica automaticamente i criteri più recenti se rileva variazioni rispetto a quelli correnti e anche ogni 24 ore. Se si sono apportate modifiche ai criteri dopo l'ora visualizzata, chiudere e riaprire l'applicazione di Office.

Se viene visualizzato il messaggio **Questo client non ha la licenza per Office Professional Plus**, il client Azure Information Protection ha rilevato che l'edizione installata di Office non supporta l'applicazione della protezione di Rights Management. Quando viene effettuato questo rilevamento, le etichette che applicano la protezione non vengono visualizzate sulla barra di Azure Information Protection.

Usare le informazioni di **Versione** per verificare la versione del client installata. È possibile controllare se la versione installata è quella più recente e verificare le nuove funzionalità e le correzioni di tale versione facendo clic sul collegamento **Novità** che consente di accedere alla [cronologia delle versioni](client-version-release-history.md) del client.

## <a name="custom-configurations"></a>Configurazioni personalizzate

Usare le informazioni seguenti per le configurazioni avanzate che possono essere necessarie per scenari specifici o per un subset di utenti. 

### <a name="prevent-sign-in-prompts-for-ad-rms-only-computers"></a>Evitare le richieste di accesso per i computer solo AD RMS

Per impostazione predefinita, il client Azure Information Protection prova automaticamente a connettersi al servizio Azure Information Protection. Per i computer che comunicano solo con AD RMS questo può comportare una richiesta di accesso non necessaria per gli utenti. È possibile evitare questa richiesta di accesso modificando il Registro di sistema:

Individuare il nome di valore seguente e quindi impostare i dati del valore su **0**:

**HKEY_CURRENT_USER\SOFTWARE\Microsoft\MSIP\EnablePolicyDownload** 

Indipendentemente da questa impostazione, il client Azure Information Protection segue il normale [processo di individuazione del servizio RMS](../rms-client/client-deployment-notes.md#rms-service-discovery) per trovare il proprio cluster AD RMS.

### <a name="sign-in-as-a-different-user"></a>Accedere come utente diverso

In un ambiente di produzione, in genere gli utenti non hanno bisogno di accedere con un nome utente diverso quando usano il client Azure Information Protection. Può tuttavia essere necessario eseguire questa operazione come amministratore se sono presenti più tenant, ad esempio se si ha un tenant di prova oltre a Office 365 o un tenant di Azure usato dall'organizzazione.

È possibile verificare con quale account è stato eseguito l'accesso usando la finestra di dialogo di **Microsoft Azure Information Protection**: nell'applicazione di Office, nel gruppo **Protezione** della scheda **Home** fare clic su **Proteggi** e quindi su **Guida e commenti**. Il nome dell'account verrà visualizzato nella sezione **Stato del client**.

In particolare quando si usa un account amministratore, assicurarsi di controllare il nome di dominio dell'account di accesso che viene visualizzato. Ad esempio, se si ha un account "amministratore" in due diversi tenant, può essere facile non notare che è stato effettuato l'accesso con il nome dell'account giusto, ma con il dominio errato. Un sintomo di questo errore può essere l'impossibilità di scaricare i criteri di Azure Information Protection o di visualizzare le etichette o un comportamento previsto.

Per accedere come utente diverso:

1. Usando un editor del Registro di sistema, passare a **HKEY_CURRENT_USER\SOFTWARE\Microsoft\MSIP** ed eliminare il valore **TokenCache** (con i dati associati).

2. Riavviare tutte le applicazioni Office aperte e accedere con l'account utente diverso. Se non viene visualizzato un prompt dei comandi nell'applicazione Office per accedere al servizio Azure Information Protection, tornare alla finestra di dialogo **Microsoft Azure Information Protection** e fare clic su **Accedi** dalla sezione **Stato del client** aggiornata.

Inoltre:

- Se si usa Single Sign-On, è necessario disconnettersi da Windows e accedere con un account utente diverso dopo aver modificato il Registro di sistema. Il client Azure Information Protection eseguirà automaticamente l'autenticazione tramite l'account utente usato per l'accesso.

- Se si vuole reinizializzare l'ambiente per il servizio Azure Rights Management (noto anche come bootstrap), è possibile farlo usando l'opzione **Reimposta** dello [strumento RMS Analyzer](https://www.microsoft.com/en-us/download/details.aspx?id=46437).

- Per eliminare i criteri di Azure Information Protection attualmente scaricati, rimuovere il file **Policy.msip** dalla cartella **%localappdata%\Microsoft\MSIP**.

### <a name="hide-the-classify-and-protect-menu-option-in-windows-file-explorer"></a>Nascondere l'opzione di menu Classifica e proteggi in Esplora file di Windows

È possibile definire questa configurazione avanzata modificando il Registro di sistema quando si usa il client Azure Information Protection versione 1.3.0.0 o successiva. 

Creare il nome del valore DWORD seguente (con i dati associati):

**HKEY_CLASSES_ROOT\AllFilesystemObjects\shell\Microsoft.Azip.RightClick\LegacyDisable**

### <a name="support-for-disconnected-computers"></a>Supporto per i computer disconnessi

Per impostazione predefinita, il client Azure Information Protection prova automaticamente a connettersi al servizio Azure Information Protection per scaricare i criteri più recenti. Se si è conoscenza che il computer in uso non sarà in grado di connettersi a Internet per un determinato periodo di tempo, è possibile impedire al client di provare a connettersi al servizio modificando il Registro di sistema. Individuare il nome di valore seguente e impostare i dati del valore su **0**:

**HKEY_CURRENT_USER\SOFTWARE\Microsoft\MSIP\EnablePolicyDownload** 

Verificare che nel client sia presente un file di criteri validi denominato **Policy.msip**, nella cartella **%localappdata%\Microsoft\MSIP**. Se necessario, è possibile esportare i criteri dal portale di Azure e copiare il file esportato nel computer client. È inoltre possibile usare questo metodo per sostituire un file di criteri non aggiornato con i criteri pubblicati più recenti.

## <a name="to-uninstall-the-azure-information-protection-client"></a>Per disinstallare il client di Azure Information Protection

È possibile usare una delle seguenti opzioni:

- Per disinstallare un programma, usare il Pannello di controllo: fare clic su **Microsoft Azure Information Protection** > **Disinstalla**

- Rieseguire l'eseguibile, ad esempio **AzInfoProtection.exe**, e fare clic su **Disinstalla** nella pagina **Modifica installazione**. 

- Eseguire l'eseguibile con **/uninstall**. Ad esempio: `AzInfoProtection.exe /uninstall`

## <a name="next-steps"></a>Passaggi successivi
Dopo aver installato il client Azure Information Protection, vedere gli argomenti seguenti per altre informazioni che potrebbero essere necessarie per supportare il client:

- [File del client e registrazione dell'utilizzo](client-admin-guide-files-and-logging.md)

- [Rilevamento dei documenti](client-admin-guide-document-tracking.md)

- [Tipi di file supportati](client-admin-guide-file-types.md)

- [Comandi di PowerShell](client-admin-guide-powershell.md)


[!INCLUDE[Commenting house rules](../includes/houserules.md)]
