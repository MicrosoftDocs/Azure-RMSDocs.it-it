---
title: Installare il client Azure Information Protection per gli utenti
description: Istruzioni e informazioni per gli amministratori per la distribuzione del client Azure Information Protection per Windows nelle reti aziendali.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/13/2018
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: ea3ec965-3720-4614-8564-3ecfe60bc175
ms.reviewer: eymanor
ms.suite: ems
ms.openlocfilehash: 92e4f6c05378b36165db0628f14941b0ccd26cb7
ms.sourcegitcommit: c157636577db2e2a2ba5df81eb985800cdb82054
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/14/2018
---
# <a name="admin-guide-install-the-azure-information-protection-client-for-users"></a>Guida dell'amministratore: Installare il client Azure Information Protection per gli utenti

>*Si applica a: Active Directory Rights Management Services, Azure Information Protection, Windows 10, Windows 8.1, Windows 8, Windows 7 con SP1, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2*

Prima di installare il client Azure Information Protection nella rete aziendale, verificare che nei computer siano installate le versioni del sistema operativo e le applicazioni richieste per Azure Information Protection: [Requisiti per Azure Information Protection](../get-started/requirements-azure-rms.md). 

Verificare quindi gli altri prerequisiti che possono essere necessari per il client Azure Information Protection descritti nella sezione seguente. Il programma di installazione non verifica tutti i prerequisiti.

## <a name="additional-prerequisites-for-the-azure-information-protection-client"></a>Altri prerequisiti per il client Azure Information Protection

- Microsoft .NET Framework 4.6.2
    
    Per impostazione predefinita, l'installazione completa del client Azure Information Protection richiede almeno Microsoft .NET Framework 4.6.2. Se questo prerequisito non è soddisfatto, il programma di installazione prova a scaricare e installare la versione richiesta. Quando questo prerequisito viene installato come parte dell'installazione del client, è necessario riavviare il computer. Anche se non è consigliabile, è possibile ignorare questo prerequisito con un [parametro di installazione personalizzata](#more-information-about-the-downgradedotnetrequirement-installation-parameter).

- Microsoft .NET Framework 4.5.2
    
    Se il visualizzatore Azure Information Protection viene installato separatamente, è necessario Microsoft .NET Framework 4.5.2 come versione minima. Se questo non è presente, il programma di installazione non lo scarica e installa.

- Windows PowerShell versione 4.0
    
    Il modulo PowerShell per il client richiede Windows PowerShell versione 4.0, che potrebbe essere necessario installare in sistemi operativi precedenti. Per altre informazioni, vedere [How to Install Windows PowerShell 4.0](http://social.technet.microsoft.com/wiki/contents/articles/21016.how-to-install-windows-powershell-4-0.aspx) (Come installare Windows PowerShell 4.0). Il programma di installazione non controlla né installa questo prerequisito per l'utente. Per verificare quale versione di Windows PowerShell è in esecuzione, digitare `$PSVersionTable` in una sessione di PowerShell.

- Assistente per l'accesso ai Microsoft Online Services 7.250.4303.0
    
    I computer che eseguono Office 2010 richiedono l'Assistente per l'accesso ai Microsoft Online Services versione 7.250.4303.0. Questa versione è inclusa nell'installazione del client. Se si usa una versione successiva dell'Assistente per l'accesso, disinstallarla prima di installare il client Azure Information Protection. Ad esempio, per verificare la versione e disinstallare l'Assistente per l'accesso, usare **Pannello di controllo** > **Programmi e funzionalità** > **Disinstalla o modifica programma**.

- KB 2533623
    
    I computer con Windows 7 Service Pack 1 richiedono l'aggiornamento KB 2533623. Per altre informazioni su questo aggiornamento, vedere [Avviso di sicurezza Microsoft: possibile esecuzione di codice remoto durante un caricamento della libreria non protetto](https://support.microsoft.com/en-us/kb/2533623). Questo aggiornamento può essere installato direttamente dall'utente. In alternativa, è possibile sostituirlo con un altro aggiornamento che lo installa automaticamente.
    
    Se questo aggiornamento richiesto non è installato, l'installazione client avvisa che è necessario installarlo. Questo aggiornamento può essere installato dopo l'installazione del client. Alcune azioni, tuttavia, verranno bloccate e verrà visualizzato di nuovo l'avviso.  

- Visual C++ Redistributable per Visual Studio 2015 (versione a 32 bit)
    
    Per i computer che eseguono Windows 7 Service Pack 1, installare **vc_redist.x86.exe** dalla pagina di download seguente: [Visual C++ Redistributable per Visual Studio 2015](https://www.microsoft.com/en-us/download/details.aspx?id=48145)
    
    L'installazione del client non verifica il rispetto di questo prerequisito, che è tuttavia necessario perché il client di Azure Information Protection possa classificare e proteggere i file PDF.

- Non disabilitare il componente aggiuntivo **Microsoft Azure Information Protection** per le applicazioni di Office
    
    Se è stata configurata l'impostazione criteri di gruppo **Elenco dei componenti aggiuntivi gestiti**, includere il componente aggiuntivo Microsoft Azure Information Protection per le applicazioni Office specificando i seguenti identificatori ProgID per Azure Information Protection e impostare l'opzione su **1: The add-in is always enabled** (1: Sempre attivato).
    
    - Per Outlook: `MSIP.OutlookAddin`
    
    - Per Word: `MSIP.WordAddin`
    
    - Per Excel: `MSIP.ExcelAddin`
    
    - Per PowerPoint: `MSIP.PowerPointAddin`
    
    Se l'impostazione criteri di gruppo **Elenco dei componenti aggiuntivi gestiti** non è stata configurata, può risultare necessario configurarla quando si ricevono report indicanti che il componente aggiuntivo Microsoft Azure Information Protection sta per essere disattivato. Quando questo componente aggiuntivo viene disattivato, gli utenti non visualizzano la barra di Azure Information Protection nell'applicazione di Office.
    
    Per altre informazioni su questa impostazione criteri di gruppo, vedere [No Add-ins loaded due to group policy settings for Office 2013 and Office 2016 programs](https://support.microsoft.com/help/2733070/no-add-ins-loaded-due-to-group-policy-settings-for-office-2013-and-off) (Nessun componente aggiuntivo caricato a causa di impostazioni criteri di gruppo per Office 2013 e Office 2016).

- Per Office 16.0.8628.2010 e versioni successive (A portata di clic): abilitare il supporto legacy per i monitor
    
    Nota: questo requisito non è obbligatorio per la versione di anteprima corrente del client di Azure Information Protection. 
    
    Per evitare la visualizzazione della barra di Azure Information Protection al di fuori delle applicazioni di Office per queste versioni di Office, è necessario abilitare il supporto legacy per i monitor. Quando la barra non viene visualizzata correttamente in questo scenario, è possibile visualizzarla come **AdxTaskPane**. 
    
    Per configurare le applicazioni di Office per questo requisito: **File** > **Opzioni** > **Generale** > **Opzioni interfaccia utente**:
    
    - Se l'opzione **When using multiple displays** (Quando si usano più schermi) è impostata su **Optimize for best appearance** (Ottimizza in modo da ottenere l'aspetto migliore), selezionare **Optimize for compatibility (application restart required)** (Ottimizza per compatibilità (riavvio necessario)). 
        
    - Se è selezionata l'opzione **Use best settings for my display** (Usa le impostazioni più adatte al mio schermo), deselezionarla.
    
    - Se non viene visualizzata nessuna di queste opzioni, non è richiesta alcuna configurazione aggiuntiva.

> [!IMPORTANT]
> L'installazione del client Azure Information Protection richiede autorizzazioni amministrative locali.


## <a name="options-to-install-the-azure-information-protection-client-for-users"></a>Opzioni di installazione del client Azure Information Protection per gli utenti

Sono disponibili tre opzioni per l'installazione del client per gli utenti:

**Windows Update**: il client Azure Information Protection è incluso nel catalogo di Microsoft Update, quindi è possibile installare e aggiornare il client usando qualsiasi servizio di aggiornamento del software che usa il catalogo.

**Eseguire la versione eseguibile (EXE) del client**: il metodo di installazione consigliato che è possibile usare in modo interattivo o automatico. Questo metodo offre la massima flessibilità ed è consigliato perché il programma di installazione verifica la maggior parte dei prerequisiti ed è in grado di installare automaticamente i prerequisiti mancanti. [Istruzioni](#to-install-the-azure-information-protection-client-by-using-the-executable-installer)

**Distribuire la versione del programma di installazione di Windows (MSI) del client**: metodo supportato solo per le installazioni invisibili all'utente che usano un meccanismo di distribuzione centrale, ad esempio criteri di gruppo, Configuration Manager e Microsoft Intune. Questo metodo è necessario per i PC Windows 10 gestiti da Intune e dalla gestione dispositivi mobili (MDM) poiché per questi computer, i file eseguibili non sono supportati per l'installazione. Tuttavia, quando si usa questo metodo di installazione, è necessario verificare e installare o disinstallare manualmente il software dipendente che il programma di installazione eseguirebbe in ogni computer per il file eseguibile. [Istruzioni](#to-install-the-azure-information-protection-client-by-using-the-msi-installer)

### <a name="to-install-the-azure-information-protection-client-by-using-the-executable-installer"></a>Per installare il client Azure Information Protection usando il programma di installazione del file eseguibile

Usare le istruzioni riportate di seguito per installare il client quando non si usa il catalogo di Microsoft Update o si distribuisce il file con estensione MSI usando un metodo di distribuzione centrale, ad esempio Intune.

1. Scaricare la versione eseguibile del client Azure Information Protection dall'[Area download Microsoft](https://www.microsoft.com/en-us/download/details.aspx?id=53018). 
    
    Se è disponibile una versione di anteprima, mantenerla solo per i test. Le versioni di questo tipo non sono progettate per l'uso in un ambiente di produzione. 

2. Per un'installazione predefinita, basta eseguire il file eseguibile, ad esempio **AzInfoProtection.exe**. Al contrario, per visualizzare le opzioni di installazione, eseguire prima di tutto l'eseguibile con **/help**: `AzInfoProtection.exe /help`

    Esempio per installare automaticamente il client: `AzInfoProtection.exe /quiet`
    
    Esempio per installare automaticamente solo i cmdlet di PowerShell: `AzInfoProtection.exe  PowerShellOnly=true /quiet`
    
    Nella schermata della Guida non sono elencati i parametri seguenti:
    
    - **ServiceLocation**: usare questo parametro se si installa il client in computer che eseguono Office 2010 e gli utenti non sono amministratori locali dei rispettivi computer o non si vuole che vengano visualizzati messaggi di richiesta. [Altre informazioni](#more-information-about-the-servicelocation-installation-parameter) 
    
    - **DowngradeDotNetRequirement**: usare questo parametro per ignorare il requisito relativo a Microsoft .NET Framework versione 4.6.2. [Altre informazioni](#more-information-about-the-downgradedotnetrequirement-installation-parameter)
    
    - **AllowTelemetry = 0**: usare questo parametro per disabilitare l'opzione di installazione **Invia le statistiche di utilizzo a Microsoft per contribuire a migliorare Azure Information Protection**. 
    
3. Se si sceglie l'installazione interattiva, selezionare l'opzione per l'installazione di un **criterio demo** se non si riesce a connettersi a Office 365 o ad Azure Active Directory, ma si vuole esaminare e provare il lato client di Azure Information Protection usando un criterio locale per scopi dimostrativi. Quando il client si connette a un servizio di Azure Information Protection, questo criterio demo viene sostituito dai criteri di Azure Information Protection dell'organizzazione.
    
4. Per completare l'installazione: 

    - Se nel computer viene eseguito Office 2010, riavviare il computer. 
        
        Se il client non è stato installato con il parametro ServiceLocation, quando si apre per la prima volta una delle applicazioni di Office che usano la barra di Azure Information Protection, ad esempio Word, è necessario confermare tutti i messaggi relativi all'aggiornamento del Registro di sistema per il primo utilizzo. Per il popolamento delle chiavi del Registro di sistema, viene usata l'[individuazione dei servizi](../rms-client/client-deployment-notes.md#rms-service-discovery). 
    
    - Per le altre versioni di Office, riavviare tutte le applicazioni di Office e tutte le istanze di Esplora file. 
        
5. È possibile verificare se l'installazione è stata completata controllando il file di log di installazione, che per impostazione predefinita viene creato nella cartella %temp%. È possibile modificare questo percorso con il parametro di installazione **/log**. 
 
    Questo file ha il formato di denominazione seguente: `Microsoft_Azure_Information_Protection_<number>_<number>_MSIP.Setup.Main.msi.log`
    
    Ad esempio: **Microsoft_Azure_Information_Protection_20161201093652_000_MSIP.Setup.Main.msi.log**
    
    In questo file di log, cercare la stringa seguente: **Product: Microsoft Azure Information Protection -- Installation completed successfully.** (Prodotto: Microsoft Azure Information Protection -- Installazione completata.) Se l'installazione non è riuscita, questo file di log contiene informazioni dettagliate per identificare e risolvere i problemi.

#### <a name="more-information-about-the-servicelocation-installation-parameter"></a>Altre informazioni sul parametro di installazione ServiceLocation

Quando si installa il client per gli utenti che usano Office 2010 e che non hanno autorizzazioni di amministratore locale, specificare il parametro ServiceLocation e l'URL per il servizio Azure Rights Management. Questo parametro e il relativo valore consentono di creare e impostare le chiavi del Registro di sistema seguenti:

HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\MSDRM\ServiceLocation\Activation

HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\MSDRM\ServiceLocation\EnterprisePublishing

HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSDRM\ServiceLocation\EnterprisePublishing

HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSDRM\ServiceLocation\Activation

Usare la procedura seguente per identificare il valore da specificare per il parametro ServiceLocation. 

##### <a name="to-identify-the-value-to-specify-for-the-servicelocation-parameter"></a>Per identificare il valore da specificare per il parametro ServiceLocation

1. Da una sessione di PowerShell eseguire prima di tutto [Connect-AadrmService](https://docs.microsoft.com/powershell/aadrm/vlatest/connect-aadrmservice) e specificare le credenziali di amministratore per connettersi al servizio Azure Rights Management. Eseguire quindi [Get-AadrmConfiguration](https://docs.microsoft.com/powershell/aadrm/vlatest/get-aadrmconfiguration). 
 
    Se non è stato ancora installato il modulo di PowerShell per il servizio Azure Rights Management, vedere [Installazione di Windows PowerShell per Azure Rights Management](../deploy-use/install-powershell.md).

2. Nell'output identificare il valore **LicensingIntranetDistributionPointUrl** .

    Ad esempio, **LicensingIntranetDistributionPointUrl   : https://5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com/_wmcs/licensing**

3. In questo valore rimuovere **/_wmcs/licensing** dalla stringa. Ad esempio: **https://5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com**

    La stringa rimanente è il valore da specificare per il parametro ServiceLocation.

Esempio per installare il client in modo invisibile all'utente per Office 2010 e Azure RMS: `AzInfoProtection.exe /quiet ServiceLocation=https://5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com`


#### <a name="more-information-about-the-downgradedotnetrequirement-installation-parameter"></a>Altre informazioni sul parametro di installazione DowngradeDotNetRequirement installation

Per il supporto degli aggiornamenti automatici tramite Windows Update e per l'integrazione affidabile con le applicazioni di Office, il client Azure Information Protection usa Microsoft .NET Framework versione 4.6.2. Per impostazione predefinita, il programma di installazione controlla se questa versione è presente e, in caso negativo, prova a installarla. A questo punto è necessario riavviare il computer.

Se l'installazione di questa versione più recente di Microsoft .NET Framework non è una soluzione efficace, è possibile installare il client con il parametro **DowngradeDotNetRequirement=True**, in modo da ignorare questo requisito se è installato Microsoft .NET Framework versione 4.5.1.

ad esempio `AzInfoProtection.exe DowngradeDotNetRequirement=True`

È consigliabile usare questo parametro con cautela, tenendo presente che sono stati segnalati problemi di blocco delle applicazioni di Office quando il client Azure Information Protection viene usato con questa versione precedente di Microsoft .NET Framework. Se si riscontrano problemi di blocco delle applicazioni, eseguire l'aggiornamento alla versione consigliata prima di provare altre soluzioni. 

Tenere anche presente che se si usa Windows Update per mantenere aggiornato il client Azure Information Protection, è necessario adottare un altro meccanismo di distribuzione del software per aggiornare il client alle versioni successive.

### <a name="to-install-the-azure-information-protection-client-by-using-the-msi-installer"></a>Per installare il client Azure Information Protection usando il programma di installazione MSI

Per la distribuzione centrale, usare le seguenti informazioni specifiche della versione dell'installazione MSI del client Azure Information Protection. 

Se si usa Intune per il metodo di distribuzione del software, usare queste istruzioni insieme a quelle incluse in [Aggiungere app con Microsoft Intune](/intune/deploy-use/add-apps).

1. Scaricare la versione MSI del client Azure Information Protection dall'[Area download Microsoft](https://www.microsoft.com/en-us/download/details.aspx?id=53018). 
    
    Se è disponibile una versione di anteprima, mantenerla solo per i test. Le versioni di questo tipo non sono progettate per l'uso in un ambiente di produzione. 

2. Per ogni computer che esegue il file con estensione msi è necessario verificare che siano soddisfatte le seguenti dipendenze software. Ad esempio, creare un pacchetto con le dipendenze e la versione MSI del client oppure distribuire solo ai computer che soddisfano queste dipendenze:
    
    |Versione di Office|Sistema operativo|Software|Azione|
    |--------------------|--------------|----------------|---------------------|
    |Office 2016|Tutte le versioni supportate|64 bit: [KB3178666](https://www.microsoft.com/en-us/download/details.aspx?id=55007)<br /><br />32 bit: [KB3178666](https://www.microsoft.com/en-us/download/details.aspx?id=54999)<br /><br /> Versione: 1.0|Installare|
    |Office 2013|Tutte le versioni supportate|64 bit: [KB3172523](https://www.microsoft.com/en-us/download/details.aspx?id=54992)<br /><br /> 32 bit: [KB3172523](https://www.microsoft.com/en-us/download/details.aspx?id=54979) <br /><br />Versione: 1.0|Installare|
    |Office 2010|Tutte le versioni supportate|[Assistente per l'accesso ai Microsoft Online Services](https://www.microsoft.com/en-us/download/details.aspx?id=28177)<br /><br /> Versione: 2.1|Installare|
    |Office 2010|Windows 8.1 e Windows Server 2012 R2|[KB2843630](https://www.microsoft.com/en-us/download/details.aspx?id=41708)<br /><br /> Numero di versione nel nome file: v3|Installare se non è installato KB2843630 o KB2919355|
    |Office 2010|Windows 8 e Windows Server 2012|[KB2843630](https://www.microsoft.com/en-us/download/details.aspx?id=41708)<br /><br /> Numero di versione nel nome file: v3|Installare|
    |Office 2010|Windows 7 e Windows Server 2008 R2|[KB2843630](https://www.microsoft.com/en-us/download/details.aspx?id=41709)<br /><br /> Numero di versione nel nome file: v3|Installare se non è installato KB3125574|
    |Non applicabile|Windows 7|[vc_redist.x86.exe](https://www.microsoft.com/en-us/download/details.aspx?id=48145)|Installare|
    |Non applicabile|Windows 7|KB2627273 <br /><br /> Numero di versione incluso nel nome file: v4|Uninstall|

3. Per un'installazione predefinita, eseguire il file MSI con **/quiet/**, ad esempio, `AzInfoProtection.msi /quiet`. Tuttavia, può essere necessario specificare parametri di installazione aggiuntivi, che sono documentati nelle [istruzioni del programma di installazione del file eseguibile](#to-install-the-azure-information-protection-client-by-using-the-executable-installer).  


## <a name="how-to-install-the-azure-information-protection-scanner"></a>Come installare lo scanner Azure Information Protection

Attualmente, la versione disponibile a livello generale dello scanner di Azure Information Protection è un download distinto denominato **AzInfoProtectionScanner.exe** nell'[Area download Microsoft](https://www.microsoft.com/en-us/download/details.aspx?id=53018). Le versioni successive dello scanner saranno incluse nel client di Azure Information Protection.

La versione di anteprima corrente del client Azure Information Protection include anche lo scanner Azure Information Protection. 

Il modulo PowerShell incluso con lo scanner e il client di anteprima contiene i cmdlet per installare e configurare lo scanner.

Per installare il client per lo scanner, seguire le istruzioni delle sezioni precedenti. Si noti che se non si necessita di tutti i componenti del client, ad esempio il componente aggiuntivo di Office e il visualizzatore, è possibile installare soltanto il modulo PowerShell. È possibile, ad esempio, eseguire l'eseguibile con `PowerShellOnly=true /quiet`.

Dopo aver installato il client, si è pronti per installare lo scanner. Per istruzioni, vedere [Distribuzione dello scanner Azure Information Protection per classificare e proteggere automaticamente i file](../deploy-use/deploy-aip-scanner.md).


## <a name="next-steps"></a>Passaggi successivi
Dopo aver installato il client Azure Information Protection, vedere gli argomenti seguenti per altre informazioni che potrebbero essere necessarie per supportare il client:

- [Personalizzazioni](client-admin-guide-customizations.md)

- [File del client e registrazione dell'utilizzo](client-admin-guide-files-and-logging.md)

- [Rilevamento dei documenti](client-admin-guide-document-tracking.md)

- [Tipi di file supportati](client-admin-guide-file-types.md)

- [Comandi di PowerShell](client-admin-guide-powershell.md)


[!INCLUDE[Commenting house rules](../includes/houserules.md)]
