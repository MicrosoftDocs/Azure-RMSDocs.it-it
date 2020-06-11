---
title: Installare il client di etichettatura unificata Azure Information Protection per gli utenti
description: Istruzioni e informazioni per gli amministratori per la distribuzione del client di Azure Information Protection Unified Labeling per Windows nelle reti aziendali.
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 05/24/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: v2client
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 6640ac4706f064e8e7f3ba87b691268a17aa0f41
ms.sourcegitcommit: f32928f7dcc03111fc72d958cda9933d15065a2b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/10/2020
ms.locfileid: "84666116"
---
# <a name="admin-guide-install-the-azure-information-protection-unified-labeling-client-for-users"></a>Guida dell'amministratore: installare il client di etichettatura unificata Azure Information Protection per gli utenti

>*Si applica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8, windows server 2019, windows server 2016, windows Server 2012 R2, windows Server 2012*
>
> *Istruzioni per: [Azure Information Protection client di etichetta unificata per Windows](../faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*

Prima di installare il client Azure Information Protection Unified Labeling nella rete aziendale, verificare che i computer dispongano delle versioni e delle applicazioni del sistema operativo necessarie per Azure Information Protection: [requisiti per Azure Information Protection](../requirements.md). 

Verificare quindi i prerequisiti aggiuntivi che potrebbero essere necessari per il client di Azure Information Protection Unified Labeling, come descritto nella sezione successiva. Il programma di installazione non verifica tutti i prerequisiti.

## <a name="additional-prerequisites-for-the-azure-information-protection-unified-labeling-client"></a>Prerequisiti aggiuntivi per il client di Azure Information Protection Unified Labeling

- Microsoft .NET Framework 4.6.2
    
    Per impostazione predefinita, l'installazione completa del client Azure Information Protection Unified Labeling richiede una versione minima di Microsoft .NET Framework 4.6.2 e, se non è presente, l'installazione guidata dal programma di installazione eseguibile tenta di scaricare e installare questo prerequisito. Quando questo prerequisito viene installato come parte dell'installazione del client, è necessario riavviare il computer. Anche se non è consigliabile, è possibile ignorare questo prerequisito quando si esegue la configurazione guidata usando un [parametro di installazione personalizzato](#more-information-about-the-downgradedotnetrequirement-installation-parameter).
    
    - Microsoft .NET Framework 4.5.2
    
    Se il visualizzatore Azure Information Protection viene installato separatamente, è necessario Microsoft .NET Framework 4.5.2 come versione minima. In caso contrario, il programma di installazione eseguibile non esegue il download o l'installazione.

- Versione minima di Windows PowerShell 4,0
    
    Il modulo PowerShell per il client richiede una versione minima di 4,0 per Windows PowerShell, che potrebbe essere necessario installare in sistemi operativi precedenti. Per altre informazioni, vedere [How to Install Windows PowerShell 4.0](https://social.technet.microsoft.com/wiki/contents/articles/21016.how-to-install-windows-powershell-4-0.aspx) (Come installare Windows PowerShell 4.0). Il programma di installazione non controlla né installa questo prerequisito per l'utente. Per verificare quale versione di Windows PowerShell è in esecuzione, digitare `$PSVersionTable` in una sessione di PowerShell.

- Risoluzione dello schermo superiore a 800x600
    
    Alle risoluzioni 800x600 e inferiori non è possibile visualizzare completamente la finestra di dialogo **Classifica e proteggi - Azure Information Protection** facendo clic con il pulsante destro del mouse su un file o una cartella in Esplora file.


- Assistente per l'accesso ai Microsoft Online Services 7.250.4303.0
    
    I computer che eseguono Office 2010 richiedono l'Assistente per l'accesso ai Microsoft Online Services versione 7.250.4303.0. Questa versione è inclusa nell'installazione del client. Se si dispone di una versione più recente dell'assistente per l'accesso, disinstallarla prima di installare il client di Azure Information Protection Unified labeling. Controllare, ad esempio, la versione e disinstallare l'assistente per l'accesso tramite il **Pannello di controllo**  >  **programmi e funzionalità**  >  **Disinstalla o modifica programma**.

- KB 4482887
    
    Solo per Windows 10 versione 1809, per le build del sistema operativo precedenti alla build 17763.348, installare [1 marzo 2019 - KB4482887 (build sistema operativo 17763.348)](https://support.microsoft.com/help/4482887/windows-10-update-kb4482887) per garantire che la barra di Information Protection venga visualizzata correttamente nelle applicazioni Office. Questo aggiornamento non è necessario se si usa Office 365 1902 o versione successiva.

- Configurare i criteri di gruppo per impedire la disabilitazione del componente aggiuntivo Azure Information Protection
    
    Per Office 2013 e versioni successive, configurare i criteri di gruppo per garantire che il componente aggiuntivo **Microsoft Azure Information Protection** per le applicazioni di Office sia sempre abilitato. Senza questa configurazione, è possibile che il componente aggiuntivo Microsoft Azure Information Protection venga disabilitato e gli utenti non potranno assegnare etichette a documenti e messaggi di posta elettronica nella propria applicazione Office.
    
    - Per Outlook: usare l'impostazione dei criteri di gruppo documentata in [System Administrator control over add-ins](https://docs.microsoft.com/office/vba/outlook/concepts/getting-started/support-for-keeping-add-ins-enabled#system-administrator-control-over-add-ins) (Controllo dell'amministratore sui componenti aggiuntivi) nella documentazione di Office.
    
    - Per Word, Excel e PowerPoint: usare l'impostazione dei criteri di gruppo **Elenco dei componenti aggiuntivi gestiti** documentata nell'articolo del supporto tecnico [No Add-ins loaded due to group policy settings for Office 2013 and Office 2016 programs](https://support.microsoft.com/help/2733070/no-add-ins-loaded-due-to-group-policy-settings-for-office-2013-and-off) (Nessun componente aggiuntivo caricato a causa di impostazioni criteri di gruppo per Office 2013 e Office 2016). 
        
        Specificare gli identificatori seguenti a livello di codice (ProgID) per Azure Information Protection e impostare l'opzione su **1: The add-in is always enabled** (1: Sempre attivato).
        
        Per Word: `MSIP.WordAddin`
        
        Per Excel: `MSIP.ExcelAddin`
        
        Per PowerPoint: `MSIP.PowerPointAddin`

> [!IMPORTANT]
> L'installazione del client Azure Information Protection Unified Labeling richiede autorizzazioni amministrative locali.

## <a name="applications"></a>Applicazioni

Il client di assegnazione di etichette unificato Azure Information Protection può etichettare e proteggere documenti e messaggi di posta elettronica usando le applicazioni di Office Word, Excel, PowerPoint e Outlook delle edizioni di Office seguenti:

App di Office versione minima 1805, Build 9330,2078 da Office 365 business o Microsoft 365 Business quando all'utente viene assegnata una licenza per Azure Rights Management (noto anche come Azure Information Protection per Office 365) Office 365 ProPlus Office Professional Plus 2019 Office Professional Plus 2016 Office Professional Plus 2013 con Service Pack 1 Office Professional Plus 2010 con Service Pack 2

Le altre edizioni di Office, ad esempio **standard**, non possono proteggere documenti e messaggi di posta elettronica utilizzando un servizio Rights Management. Per queste edizioni, Azure Information Protection è supportato solo per l' **etichettatura** . Di conseguenza, le etichette che applicano la protezione non vengono visualizzate agli utenti sul pulsante Azure Information Protection sensibilità o sulla barra.

Per informazioni sulle edizioni di Office che supportano il servizio di protezione, vedere [Applicazioni che supportano la protezione dati di Azure Rights Management](https://docs.microsoft.com/azure/information-protection/requirements-applications).

### <a name="office-features-and-capabilities-not-supported"></a>Funzionalità e funzionalità di Office non supportate

Il client di Azure Information Protection Unified Labeling non supporta più versioni di Office nello stesso computer o il cambio di account utente in Office.

La funzionalità di Unione di Office mail non è supportata con alcuna funzionalità Azure Information Protection.

## <a name="options-to-install-the-azure-information-protection-unified-labeling-client-for-users"></a>Opzioni per installare il client di etichettatura unificata Azure Information Protection per gli utenti

Sono disponibili due opzioni per l'installazione del client per gli utenti:

**Eseguire la versione eseguibile (EXE) del client**: il metodo di installazione consigliato che è possibile usare in modo interattivo o automatico. Questo metodo offre la massima flessibilità ed è consigliato perché il programma di installazione verifica la maggior parte dei prerequisiti ed è in grado di installare automaticamente i prerequisiti mancanti. [Istruzioni](#to-install-the-azure-information-protection-unified-labeling-client-by-using-the-executable-installer)

**Distribuire la versione del programma di installazione di Windows (MSI) del client**: metodo supportato solo per le installazioni invisibili all'utente che usano un meccanismo di distribuzione centrale, ad esempio criteri di gruppo, Configuration Manager e Microsoft Intune. Questo metodo è necessario per i PC Windows 10 gestiti da Intune e dalla gestione dispositivi mobili (MDM) poiché per questi computer, i file eseguibili non sono supportati per l'installazione. Tuttavia, quando si usa questo metodo di installazione, è necessario verificare e installare o disinstallare manualmente il software dipendente che il programma di installazione eseguirebbe in ogni computer per il file eseguibile. [Istruzioni](#to-install-the-azure-information-protection-unified-labeling-client-by-using-the-msi-installer)

Al termine dell'installazione del client di Azure Information Protection Unified Labeling, è possibile aggiornare il client ripetendo il metodo di installazione scelto oppure utilizzare Windows Update per impedire l'aggiornamento automatico del client. Per altre informazioni sull'aggiornamento, vedere la sezione [Aggiornamento e gestione del client Azure Information Protection](clientv2-admin-guide.md#upgrading-and-maintaining-the-azure-information-protection-unified-labeling-client).

### <a name="to-install-the-azure-information-protection-unified-labeling-client-by-using-the-executable-installer"></a>Per installare il client di etichettatura unificata di Azure Information Protection usando il programma di installazione eseguibile

Usare le istruzioni riportate di seguito per installare il client quando non si usa il catalogo di Microsoft Update o si distribuisce il file con estensione MSI usando un metodo di distribuzione centrale, ad esempio Intune.

1. Scaricare la versione eseguibile del client di Azure Information Protection Unified Labeling (nome file di AzInfoProtection_UL) dall' [area download Microsoft](https://www.microsoft.com/download/details.aspx?id=53018). 
    
    Se è disponibile una versione di anteprima, mantenerla solo per i test. Le versioni di questo tipo non sono progettate per l'uso in un ambiente di produzione. 

2. Per un'installazione predefinita, è sufficiente eseguire il file eseguibile, ad esempio **AzInfoProtection_UL.exe**. Tuttavia, per visualizzare le opzioni di installazione, eseguire prima il file eseguibile con **/Help**:`AzInfoProtection_UL.exe /help`

    Esempio per installare automaticamente il client: `AzInfoProtection_UL.exe /quiet`
    
    Esempio per installare automaticamente solo i cmdlet di PowerShell: `AzInfoProtection_UL.exe  PowerShellOnly=true /quiet`
    
    Nella schermata della Guida non sono elencati i parametri seguenti:
    
    - **ServiceLocation**: usare questo parametro se si installa il client in computer che eseguono Office 2010 e gli utenti non sono amministratori locali dei rispettivi computer o non si vuole che vengano visualizzati messaggi di richiesta. [Altre informazioni](#more-information-about-the-servicelocation-installation-parameter) 
    
    - **DowngradeDotNetRequirement**: usare questo parametro per ignorare il requisito relativo a Microsoft .NET Framework versione 4.6.2. [Altre informazioni](#more-information-about-the-downgradedotnetrequirement-installation-parameter)
    
    - **AllowTelemetry = 0**: usare questo parametro per disabilitare l'opzione di installazione **Invia le statistiche di utilizzo a Microsoft per contribuire a migliorare Azure Information Protection**. 

3. Per completare l'installazione: 

    - Se nel computer viene eseguito Office 2010, riavviare il computer. 
        
        Se il client non è stato installato con il parametro ServiceLocation, quando si apre per la prima volta una delle applicazioni di Office che usano il client unificato di Azure Information Protection (ad esempio, Word), è necessario confermare le richieste di aggiornamento del registro di sistema per il primo utilizzo. Per il popolamento delle chiavi del Registro di sistema, viene usata l'[individuazione dei servizi](client-deployment-notes.md#rms-service-discovery). 
    
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

1. Da una sessione di PowerShell eseguire prima di tutto [Connect-AipService](https://docs.microsoft.com/powershell/module/aipservice/connect-aipservice) e specificare le credenziali di amministratore per connettersi al servizio Rights Management di Azure. Quindi eseguire [Get-AipServiceConfiguration](https://docs.microsoft.com/powershell/module/aipservice/get-aipserviceconfiguration). 
 
    Se il modulo PowerShell per il servizio Rights Management di Azure non è già stato installato, vedere [installazione del modulo PowerShell AIPService](../install-powershell.md).

2. Nell'output identificare il valore **LicensingIntranetDistributionPointUrl**.

    Ad esempio: **LicensingIntranetDistributionPointUrl: https://5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com/_wmcs/licensing**

3. In questo valore rimuovere **/_wmcs/licensing** dalla stringa. Per esempio:**https://5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com**

    La stringa rimanente è il valore da specificare per il parametro ServiceLocation.

Esempio per installare il client in modo invisibile all'utente per Office 2010 e Azure RMS: `AzInfoProtection_UL.exe /quiet ServiceLocation=https://5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com`


#### <a name="more-information-about-the-downgradedotnetrequirement-installation-parameter"></a>Altre informazioni sul parametro di installazione DowngradeDotNetRequirement installation

Per supportare gli aggiornamenti automatici usando Windows Update e per l'integrazione affidabile con le applicazioni di Office, il client Azure Information Protection Unified labeling usa Microsoft .NET Framework versione 4.6.2. Per impostazione predefinita, l'installazione interattiva tramite file eseguibile controlla se questa versione è presente e, in caso negativo, prova a installarla. A questo punto è necessario riavviare il computer.

Se l'installazione di questa versione più recente di Microsoft .NET Framework non è una soluzione efficace, è possibile installare il client con il parametro **DowngradeDotNetRequirement=True**, in modo da ignorare questo requisito se è installato Microsoft .NET Framework versione 4.5.1.

Ad esempio: `AzInfoProtection_UL.exe DowngradeDotNetRequirement=True`

Si consiglia di usare questo parametro con cautela e con la conoscenza della presenza di problemi segnalati con le applicazioni di Office sospese quando viene usato il client per l'assegnazione di etichette unificata Azure Information Protection con questa versione precedente di Microsoft .NET Framework. Se si riscontrano problemi di blocco delle applicazioni, eseguire l'aggiornamento alla versione consigliata prima di provare altre soluzioni. 

Tenere inoltre presente che se si utilizza Windows Update per tenere aggiornato il client di Azure Information Protection Unified Labeling, è necessario disporre di un altro meccanismo di distribuzione del software per aggiornare il client alle versioni successive.

### <a name="to-install-the-azure-information-protection-unified-labeling-client-by-using-the-msi-installer"></a>Per installare il client di assegnazione di etichette Azure Information Protection unificato usando il programma di installazione MSI

Per la distribuzione centrale, usare le informazioni seguenti specifiche per la versione di installazione con estensione msi del client Azure Information Protection Unified labeling. 

Se si usa Intune per il metodo di distribuzione del software, usare queste istruzioni insieme a quelle incluse in [Aggiungere app con Microsoft Intune](/intune/deploy-use/add-apps).

1. Scaricare la versione MSI della Azure Information Protection Unified Labeling client (AzInfoProtection_UL) dall' [area download Microsoft](https://www.microsoft.com/download/details.aspx?id=53018). 
    
    Se è disponibile una versione di anteprima, mantenerla solo per i test. Le versioni di questo tipo non sono progettate per l'uso in un ambiente di produzione.

2. Per ogni computer che esegue il file con estensione msi è necessario verificare che siano soddisfatte le seguenti dipendenze software. Ad esempio, creare un pacchetto con le dipendenze e la versione MSI del client oppure distribuire solo ai computer che soddisfano queste dipendenze:
    
    |Versione di Office|Sistema operativo|Software|Azione|
    |--------------------|--------------|----------------|---------------------|
    |Tutte le versioni, ad eccezione di Office 365 1902 o versione successiva|Solo Windows 10 versione 1809, build del sistema operativo precedenti alla build 17763.348|[KB 4482887](https://support.microsoft.com/help/4482887/windows-10-update-kb4482887)|Installazione di|
    |Office 2016|Tutte le versioni supportate|64 bit: [KB3178666](https://www.microsoft.com/download/details.aspx?id=55007)<br /><br />32 bit: [KB3178666](https://www.microsoft.com/download/details.aspx?id=54999)<br /><br /> Versione: 1.0|Installazione di|
    |Office 2013|Tutte le versioni supportate|64 bit: [KB3172523](https://www.microsoft.com/download/details.aspx?id=54992)<br /><br /> 32 bit: [KB3172523](https://www.microsoft.com/download/details.aspx?id=54979) <br /><br />Versione: 1.0|Installazione di|
    |Office 2010|Tutte le versioni supportate|[Assistente per l'accesso ai Microsoft Online Services](https://www.microsoft.com/download/details.aspx?id=28177)<br /><br /> Versione: 2.1|Installazione di|
    |Office 2010|Windows 8.1 e Windows Server 2012 R2|[KB2843630](https://www.microsoft.com/download/details.aspx?id=41708)<br /><br /> Numero di versione nel nome file: v3|Installare se non è installato KB2843630 o KB2919355|
    |Office 2010|Windows 8 e Windows Server 2012|[KB2843630](https://www.microsoft.com/download/details.aspx?id=41708)<br /><br /> Numero di versione nel nome file: v3|Installazione di|
    
   

3. Per un'installazione predefinita, eseguire il file MSI con **/quiet/**, ad esempio, `AzInfoProtection_UL.msi /quiet`. Tuttavia, potrebbe essere necessario specificare parametri di installazione aggiuntivi che sono documentati nelle [istruzioni del programma di installazione eseguibile](#to-install-the-azure-information-protection-unified-labeling-client-by-using-the-executable-installer) con un'unica eccezione:
    
    - Anziché **AllowTelemetry = 0** per disabilitare l'opzione di installazione **consente di migliorare Azure Information Protection inviando le statistiche di utilizzo a Microsoft**, specificare **ENABLETELEMETRY = 0**. 

## <a name="next-steps"></a>Passaggi successivi
Ora che è stato installato il client di etichettatura Azure Information Protection Unified, vedere gli argomenti seguenti per informazioni aggiuntive che potrebbero essere necessarie per supportare questo client:

- [File del client e registrazione dell'utilizzo](clientv2-admin-guide-files-and-logging.md)

- [Tipi di file supportati](clientv2-admin-guide-file-types.md)

- [Comandi di PowerShell](clientv2-admin-guide-powershell.md)

