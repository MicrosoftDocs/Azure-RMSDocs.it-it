---
title: Installare il client di etichettatura unificata Azure Information Protection per gli utenti
description: Istruzioni e informazioni per gli amministratori per la distribuzione del client di Azure Information Protection Unified Labeling per Windows nelle reti aziendali.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 12/07/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: v2client
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 427143c8ee2a93e60be683b3e80b5493c0bab441
ms.sourcegitcommit: 8a141858e494dd1d3e48831e6cd5a5be48ac00d2
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2020
ms.locfileid: "97385472"
---
# <a name="admin-guide-install-the-azure-information-protection-unified-labeling-client-for-users"></a>Guida dell'amministratore: installare il client di etichettatura unificata Azure Information Protection per gli utenti

>***Si applica a**: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8, Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012 *
>
>*Se si dispone di Windows 7 o Office 2010, vedere [AIP per le versioni di Windows e Office nel supporto esteso](../known-issues.md#aip-for-windows-and-office-versions-in-extended-support).*
>
>***Istruzioni per**: [Azure Information Protection client di etichetta unificato per Windows](../faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients). Per il client classico, vedere la [Guida dell'amministratore del client classico](client-admin-guide-install.md). *

Prima di installare il client Azure Information Protection Unified Labeling nella rete aziendale, verificare che i computer dispongano delle versioni e delle applicazioni del sistema operativo necessarie per Azure Information Protection: [requisiti per Azure Information Protection](../requirements.md). 

Verificare quindi i prerequisiti aggiuntivi che potrebbero essere necessari per il client di Azure Information Protection Unified Labeling, come descritto nella sezione successiva. Il programma di installazione non verifica tutti i prerequisiti.

## <a name="additional-prerequisites-for-the-azure-information-protection-unified-labeling-client"></a>Prerequisiti aggiuntivi per il client di Azure Information Protection Unified Labeling

I prerequisiti seguenti per il client di assegnazione unificata di AIP sono in aggiunta agli elementi elencati in [Azure Information Protection requirements](../requirements.md).

|Requisito  |Descrizione  |
|---------|---------|
|**4.6.2 Framework di Microsoft .NET**     | Per impostazione predefinita, l'installazione completa del client Azure Information Protection Unified Labeling richiede una versione minima di Microsoft .NET Framework 4.6.2. <br><br>Se questo Framework non è presente, l'installazione guidata dal programma di installazione eseguibile tenta di scaricare e installare questo prerequisito. Quando questo prerequisito viene installato come parte dell'installazione del client, è necessario riavviare il computer.       |
|**Microsoft .NET Framework 4.5.2**     | Se il Visualizzatore Azure Information Protection viene installato separatamente, l'applicazione Visualizzatore richiede una versione minima di Microsoft .NET Framework 4.5.2. <br><br>**Importante**: se questo Framework è mancante per il visualizzatore, il programma di installazione eseguibile *non* lo Scarica o lo installa.        |
|**Versione minima di Windows PowerShell 4,0**     |   Il modulo PowerShell per il client richiede una versione minima di Windows PowerShell 4,0, che potrebbe essere necessario installare in sistemi operativi precedenti. <br><br>Per altre informazioni, vedere [How to Install Windows PowerShell 4.0](https://social.technet.microsoft.com/wiki/contents/articles/21016.how-to-install-windows-powershell-4-0.aspx) (Come installare Windows PowerShell 4.0). <br><br>**Importante**: il programma di installazione *non* controlla né installa questo prerequisito. Per verificare quale versione di Windows PowerShell è in esecuzione, digitare `$PSVersionTable` in una sessione di PowerShell.      |
|**Risoluzione dello schermo superiore a 800x600**    |     Alle risoluzioni 800x600 e inferiori non è possibile visualizzare completamente la finestra di dialogo **Classifica e proteggi - Azure Information Protection** facendo clic con il pulsante destro del mouse su un file o una cartella in Esplora file.    |
|**Assistente per l'accesso ai Microsoft Online Services 7.250.4303.0**     |   I computer che eseguono Office 2010 richiedono l'assistente per l'accesso ai Microsoft Online Services versione 7.250.4303.0, inclusa nell'installazione del client. <br><br>Se si dispone di una versione più recente dell'assistente per l'accesso, disinstallarla prima di installare il client di Azure Information Protection Unified labeling. <br><br>Controllare, ad esempio, la versione e disinstallare l'assistente per l'accesso tramite il **Pannello di controllo**  >  **programmi e funzionalità**  >  **Disinstalla o modifica programma**.      |
|**KB 4482887**     | Solo per Windows 10 versione 1809, per le build del sistema operativo precedenti alla build 17763.348, installare [1 marzo 2019 - KB4482887 (build sistema operativo 17763.348)](https://support.microsoft.com/help/4482887/windows-10-update-kb4482887) per garantire che la barra di Information Protection venga visualizzata correttamente nelle applicazioni Office. <br><br>Questo aggiornamento non è necessario se si usa Office 365 1902 o versione successiva.        |
|**Autorizzazioni di amministratore**| L'installazione del client Azure Information Protection Unified Labeling richiede autorizzazioni amministrative locali.| 
|**Disabilitare la protezione dagli exploit (solo .NET 2 o 3)**   |Il client AIP non è supportato nei computer con .NET 2 o 3 con la [protezione dagli exploit](/windows/security/threat-protection/microsoft-defender-atp/enable-exploit-protection) abilitata. Se il computer dispone di .NET 2 o 3, oltre a una versione di .NET 4. x sopra elencata, assicurarsi di [disabilitare la protezione dagli exploit](../known-issues.md#known-issues-for-aip-and-exploit-protection) prima di installare il client AIP.  |
|||
        
### <a name="configure-your-group-policy-to-prevent-disabling-aip"></a>Configurare i criteri di gruppo per impedire la disabilitazione di AIP

Per le versioni di Office 2013 e successive, è consigliabile configurare i criteri di gruppo per assicurarsi che il componente aggiuntivo **Microsoft Azure Information Protection** per le applicazioni di Office sia sempre abilitato.  Senza questo componente aggiuntivo, gli utenti non saranno in grado di assegnare etichette ai documenti o ai messaggi di posta elettronica nelle applicazioni di Office.   

Per Word, Excel, PowerPoint e Outlook, usare l' **elenco delle impostazioni di criteri di gruppo dei componenti aggiuntivi gestiti** documentati in [nessun componente aggiuntivo caricato a causa delle impostazioni di criteri di gruppo per i programmi Office 2013 e Office 2016](https://support.microsoft.com/help/2733070/no-add-ins-loaded-due-to-group-policy-settings-for-office-2013-and-off). 

Specificare i seguenti identificatori programmatici (ProgID) per AIP e impostare l'opzione su **1: il componente aggiuntivo è sempre abilitato**.

|Applicazione  |ProgID  |
|---------|---------|
|Word     |     `MSIP.WordAddin`    |
|Excel     |  `MSIP.ExcelAddin`       |
|PowerPoint     |   `MSIP.PowerPointAddin`      |
|Outlook | `MSIP.OutlookAddin` |
| | | 

## <a name="applications"></a>Applicazioni

Il client di assegnazione di etichette unificato Azure Information Protection può etichettare e proteggere documenti e messaggi di posta elettronica usando le applicazioni di Office Word, Excel, PowerPoint e Outlook delle edizioni di Office seguenti:

- App di Office per le versioni elencate nella [tabella delle versioni supportate di Microsoft 365 App in base al canale di aggiornamento](/officeupdates/update-history-microsoft365-apps-by-date), da Microsoft 365 Apps for business o Microsoft 365 Business Premium quando all'utente è assegnata una licenza per Azure Rights Management (noto anche come Azure Information Protection per Office 365)
- Microsoft 365 Apps for enterprise
- Office Professional Plus 2019
- Office Professional Plus 2016
- Office Professional Plus 2013 con Service Pack 1
- Office Professional Plus 2010 con Service Pack 2

Le altre edizioni di Office, ad esempio **standard**, non possono proteggere documenti e messaggi di posta elettronica utilizzando un servizio Rights Management. Per queste edizioni, Azure Information Protection è supportato solo per l' **etichettatura** . Di conseguenza, le etichette che applicano la protezione non vengono visualizzate agli utenti sul pulsante Azure Information Protection sensibilità o sulla barra.

Per informazioni sulle edizioni di Office che supportano il servizio di protezione, vedere [Applicazioni che supportano la protezione dati di Azure Rights Management](../requirements-applications.md).

### <a name="office-features-and-capabilities-not-supported"></a>Funzionalità e capacità di Office non supportate

Il client di Azure Information Protection Unified Labeling non supporta più versioni di Office nello stesso computer o il cambio di account utente in Office.

La funzionalità di stampa unione di Office non è supportata con alcuna funzionalità di Azure Information Protection.

## <a name="options-to-install-the-azure-information-protection-unified-labeling-client-for-users"></a>Opzioni per installare il client di etichettatura unificata Azure Information Protection per gli utenti

Sono disponibili due opzioni per l'installazione del client per gli utenti:

**Eseguire la versione eseguibile (EXE) del client**: il metodo di installazione consigliato che è possibile usare in modo interattivo o automatico. Questo metodo offre la massima flessibilità ed è consigliato perché il programma di installazione verifica la maggior parte dei prerequisiti ed è in grado di installare automaticamente i prerequisiti mancanti. [Istruzioni](#to-install-the-azure-information-protection-unified-labeling-client-by-using-the-executable-installer)

**Distribuire la versione del programma di installazione di Windows (MSI) del client**: metodo supportato solo per le installazioni invisibili all'utente che usano un meccanismo di distribuzione centrale, ad esempio criteri di gruppo, Configuration Manager e Microsoft Intune. Questo metodo è necessario per i PC Windows 10 gestiti da Intune e dalla gestione dispositivi mobili (MDM) poiché per questi computer, i file eseguibili non sono supportati per l'installazione. Tuttavia, quando si usa questo metodo di installazione, è necessario verificare e installare o disinstallare manualmente il software dipendente che il programma di installazione eseguirebbe in ogni computer per il file eseguibile. [Istruzioni](#to-install-the-azure-information-protection-unified-labeling-client-by-using-the-msi-installer)

Al termine dell'installazione del client di Azure Information Protection Unified Labeling, è possibile aggiornare il client ripetendo il metodo di installazione scelto oppure utilizzare Windows Update per impedire l'aggiornamento automatico del client. Per altre informazioni sull'aggiornamento, vedere la sezione [Aggiornamento e gestione del client Azure Information Protection](clientv2-admin-guide.md#upgrading-and-maintaining-the-azure-information-protection-unified-labeling-client).

### <a name="to-install-the-azure-information-protection-unified-labeling-client-by-using-the-executable-installer"></a>Per installare il client di etichettatura unificata di Azure Information Protection usando il programma di installazione eseguibile

Usare le istruzioni riportate di seguito per installare il client quando non si usa il catalogo di Microsoft Update o si distribuisce il file con estensione MSI usando un metodo di distribuzione centrale, ad esempio Intune.

1. Scaricare la versione eseguibile del client di Azure Information Protection Unified Labeling (nome file di AzInfoProtection_UL) dall' [area download Microsoft](https://www.microsoft.com/download/details.aspx?id=53018). 
    
    Se è disponibile una versione di anteprima, mantenerla solo per i test. Le versioni di questo tipo non sono progettate per l'uso in un ambiente di produzione. 

2. Per un'installazione predefinita, è sufficiente eseguire il file eseguibile, ad esempio **AzInfoProtection_UL.exe**. Tuttavia, per visualizzare le opzioni di installazione, eseguire prima il file eseguibile con **/Help**: `AzInfoProtection_UL.exe /help`

    Esempio per installare automaticamente il client: `AzInfoProtection_UL.exe /quiet`
    
    Esempio per installare automaticamente solo i cmdlet di PowerShell: `AzInfoProtection_UL.exe  PowerShellOnly=true /quiet`
    
    Nella schermata della Guida non sono elencati i parametri seguenti:
    
    - **ServiceLocation**: usare questo parametro se si installa il client in computer che eseguono Office 2010 e gli utenti non sono amministratori locali dei rispettivi computer o non si vuole che vengano visualizzati messaggi di richiesta. [Altre informazioni](#more-information-about-the-servicelocation-installation-parameter) 
    
    - **AllowTelemetry = 0**: usare questo parametro per disabilitare l'opzione di installazione **Invia le statistiche di utilizzo a Microsoft per contribuire a migliorare Azure Information Protection**. 

3. Per completare l'installazione: 

    - Se nel computer viene eseguito Office 2010, riavviare il computer. 
        
        Se il client non è stato installato con il parametro ServiceLocation, quando si apre per la prima volta una delle applicazioni di Office che usano il client unificato di Azure Information Protection (ad esempio, Word), è necessario confermare le richieste di aggiornamento del registro di sistema per il primo utilizzo. Per il popolamento delle chiavi del Registro di sistema, viene usata l'[individuazione dei servizi](client-deployment-notes.md#rms-service-discovery). 
    
    - Per le altre versioni di Office, riavviare tutte le applicazioni di Office e tutte le istanze di Esplora file. 
        
5. È possibile verificare se l'installazione è stata completata controllando il file di log di installazione, che per impostazione predefinita viene creato nella cartella %temp%. È possibile modificare questo percorso con il parametro di installazione **/log**. 
 
    Questo file ha il formato di denominazione seguente: `Microsoft_Azure_Information_Protection_<number>_<number>_MSIP.Setup.Main.msi.log`
    
    Ad esempio: **Microsoft_Azure_Information_Protection_20161201093652_000_MSIP.Setup.Main.msi.log**
    
    In questo file di log cercare la stringa seguente: **prodotto: Microsoft Azure Information Protection--installazione completata correttamente**. Se l'installazione non è riuscita, questo file di log contiene informazioni dettagliate per identificare e risolvere i problemi.

#### <a name="more-information-about-the-servicelocation-installation-parameter"></a>Altre informazioni sul parametro di installazione ServiceLocation

Quando si installa il client per gli utenti che usano Office 2010 e che non hanno autorizzazioni di amministratore locale, specificare il parametro ServiceLocation e l'URL per il servizio Azure Rights Management. Questo parametro e il relativo valore consentono di creare e impostare le chiavi del Registro di sistema seguenti:

HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\MSDRM\ServiceLocation\Activation

HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\MSDRM\ServiceLocation\EnterprisePublishing

HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSDRM\ServiceLocation\EnterprisePublishing

HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSDRM\ServiceLocation\Activation

Usare la procedura seguente per identificare il valore da specificare per il parametro ServiceLocation. 

##### <a name="to-identify-the-value-to-specify-for-the-servicelocation-parameter"></a>Per identificare il valore da specificare per il parametro ServiceLocation

1. Da una sessione di PowerShell eseguire prima di tutto [Connect-AipService](/powershell/module/aipservice/connect-aipservice) e specificare le credenziali di amministratore per connettersi al servizio Rights Management di Azure. Quindi eseguire [Get-AipServiceConfiguration](/powershell/module/aipservice/get-aipserviceconfiguration). 
 
    Se il modulo PowerShell per il servizio Rights Management di Azure non è già stato installato, vedere [installazione del modulo PowerShell AIPService](../install-powershell.md).

2. Nell'output identificare il valore **LicensingIntranetDistributionPointUrl**.

    Ad esempio: **LicensingIntranetDistributionPointUrl: https://5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com/_wmcs/licensing**

3. In questo valore rimuovere **/_wmcs/licensing** dalla stringa. Per esempio: **https://5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com**

    La stringa rimanente è il valore da specificare per il parametro ServiceLocation.

Esempio per installare il client in modo invisibile all'utente per Office 2010 e Azure RMS: `AzInfoProtection_UL.exe /quiet ServiceLocation=https://5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com`


### <a name="to-install-the-azure-information-protection-unified-labeling-client-by-using-the-msi-installer"></a>Per installare il client di assegnazione di etichette Azure Information Protection unificato usando il programma di installazione MSI

Per la distribuzione centrale, usare le informazioni seguenti specifiche per la versione di installazione con estensione msi del client Azure Information Protection Unified labeling. 

Se si usa Intune per il metodo di distribuzione del software, usare queste istruzioni insieme a quelle incluse in [Aggiungere app con Microsoft Intune](/mem/intune/apps/apps-add).

1. Scaricare la versione MSI della Azure Information Protection Unified Labeling client (AzInfoProtection_UL) dall' [area download Microsoft](https://www.microsoft.com/download/details.aspx?id=53018). 
    
    Se è disponibile una versione di anteprima, mantenerla solo per i test. Le versioni di questo tipo non sono progettate per l'uso in un ambiente di produzione.

1. Per ogni computer che esegue il file con estensione msi è necessario verificare che siano soddisfatte le seguenti dipendenze software. Ad esempio, creare un pacchetto con le dipendenze e la versione MSI del client oppure distribuire solo ai computer che soddisfano queste dipendenze:
    
    |Versione di Office|Sistema operativo|Software|Azione|
    |--------------------|--------------|----------------|---------------------|
    |Tutte le versioni, ad eccezione di Office 365 1902 o versione successiva|Solo Windows 10 versione 1809, build del sistema operativo precedenti alla build 17763.348|[KB 4482887](https://support.microsoft.com/help/4482887/windows-10-update-kb4482887)|Installare|
    |Office 2016|Tutte le versioni supportate|64 bit: [KB3178666](https://www.microsoft.com/download/details.aspx?id=55007)<br /><br />32 bit: [KB3178666](https://www.microsoft.com/download/details.aspx?id=54999)<br /><br /> Versione: 1.0|Installare|
    |Office 2013|Tutte le versioni supportate|64 bit: [KB3172523](https://www.microsoft.com/download/details.aspx?id=54992)<br /><br /> 32 bit: [KB3172523](https://www.microsoft.com/download/details.aspx?id=54979) <br /><br />Versione: 1.0|Installare|
    |Office 2010|Tutte le versioni supportate|[Assistente per l'accesso ai Microsoft Online Services](https://www.microsoft.com/download/details.aspx?id=28177)<br /><br /> Versione: 2.1|Installare|
    |Office 2010|Windows 8.1 e Windows Server 2012 R2|[KB2843630](https://www.microsoft.com/download/details.aspx?id=41708)<br /><br /> Numero di versione nel nome file: v3|Installare se non è installato KB2843630 o KB2919355|
    |Office 2010|Windows 8 e Windows Server 2012|[KB2843630](https://www.microsoft.com/download/details.aspx?id=41708)<br /><br /> Numero di versione nel nome file: v3|Installare|
    
   

1. Per un'installazione predefinita, eseguire il file MSI con **/quiet/**, ad esempio, `AzInfoProtection_UL.msi /quiet`.

    Potrebbe essere necessario specificare parametri di installazione aggiuntivi. Per ulteriori informazioni, vedere le [istruzioni del programma di installazione eseguibile](#to-install-the-azure-information-protection-unified-labeling-client-by-using-the-executable-installer).

    > [!NOTE]
    > Per impostazione predefinita, l'opzione **migliora Azure Information Protection inviando le statistiche di utilizzo all'** opzione di installazione Microsoft è abilitata. Per disabilitare questa opzione, assicurarsi di eseguire una delle operazioni seguenti:
    >
    >- Durante l'installazione, specificare **AllowTelemetry = 0**
    >- Dopo l'installazione, aggiornare la chiave del registro di sistema come indicato di seguito: **EnableTelemetry = 0**.
    >

## <a name="next-steps"></a>Passaggi successivi
Ora che è stato installato il client di etichettatura Azure Information Protection Unified, vedere gli argomenti seguenti per informazioni aggiuntive che potrebbero essere necessarie per supportare questo client:

- [File del client e registrazione dell'utilizzo](clientv2-admin-guide-files-and-logging.md)

- [Tipi di file supportati](clientv2-admin-guide-file-types.md)

- [Comandi di PowerShell](clientv2-admin-guide-powershell.md)