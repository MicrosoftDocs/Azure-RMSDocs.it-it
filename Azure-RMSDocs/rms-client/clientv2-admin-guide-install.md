---
title: Installare il client di etichettatura unificata Azure Information Protection per gli utenti
description: Istruzioni e informazioni per gli amministratori per la distribuzione del client di Azure Information Protection Unified Labeling per Windows nelle reti aziendali.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 12/21/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: v2client
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 8c2441a9272e62577fcaf88c14fb7e6bb6cdbdde
ms.sourcegitcommit: 5e5631e03959034f37705b4f61aead3d35e8cd8c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/17/2021
ms.locfileid: "98540176"
---
# <a name="admin-guide-install-the-azure-information-protection-unified-labeling-client-for-users"></a>Guida dell'amministratore: installare il client di etichettatura unificata Azure Information Protection per gli utenti

>***Si applica a**: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8, Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012 *
>
>*Se si dispone di Windows 7 o Office 2010, vedere [AIP per le versioni di Windows e Office nel supporto esteso](../known-issues.md#aip-for-windows-and-office-versions-in-extended-support).*
>
>***Pertinente per**: [Azure Information Protection client di etichetta unificato per Windows](../faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients). Per il client classico, vedere la [Guida dell'amministratore del client classico](client-admin-guide-install.md). *

Prima di installare il client Azure Information Protection Unified Labeling nella rete aziendale, verificare che i computer dispongano delle versioni e delle applicazioni del sistema operativo necessarie per Azure Information Protection: [requisiti per Azure Information Protection](../requirements.md) e [requisiti aggiuntivi per l'installazione del client Unified Labeling nelle reti aziendali](reqs-ul-client.md).

## <a name="supported-applications-for-the-unified-labeling-client"></a>Applicazioni supportate per il client Unified Labeling

Il client di assegnazione di etichette unificato Azure Information Protection può etichettare e proteggere documenti e messaggi di posta elettronica usando le applicazioni di Office Word, Excel, PowerPoint e Outlook delle edizioni di Office seguenti:

- **App di Office** per le versioni elencate nella [tabella delle versioni supportate di Microsoft 365 App in base al canale di aggiornamento](/officeupdates/update-history-microsoft365-apps-by-date), da Microsoft 365 Apps for business o Microsoft 365 Business Premium quando all'utente è assegnata una licenza per Azure Rights Management (noto anche come Azure Information Protection per Office 365)
- **Microsoft 365 Apps for enterprise**
- **Office Professional Plus 2019**
- **Office Professional Plus 2016**
- **Office Professional Plus 2013 con Service Pack 1**
- **Office Professional Plus 2010 con Service Pack 2**

Altre edizioni di Office, ad esempio **standard**, non possono proteggere documenti e messaggi di posta elettronica tramite un servizio Rights Management. Per queste edizioni, Azure Information Protection è supportato solo per l' **etichettatura** . 

Di conseguenza, le etichette che applicano la protezione non vengono visualizzate agli utenti sul pulsante Azure Information Protection sensibilità o sulla barra.

Per informazioni sulle edizioni di Office che supportano il servizio di protezione, vedere [Applicazioni che supportano la protezione dati di Azure Rights Management](../requirements-applications.md).

Per ulteriori informazioni, vedere la pagina relativa ai [problemi noti di AIP nelle applicazioni di Office](../known-issues.md#aip-known-issues-in-office-applications).

## <a name="unified-labeling-client-installation-options"></a>Opzioni di installazione client per l'assegnazione di etichette unificate

Sono disponibili due opzioni per l'installazione del client per gli utenti:

|Opzione  |Descrizione  | I
|---------|---------|
|**Eseguire la versione eseguibile (con estensione exe) del client**     |   il metodo di installazione consigliato che è possibile usare in modo interattivo o automatico. <br><br>Questo metodo offre la massima flessibilità ed è consigliato perché il programma di installazione verifica la maggior parte dei prerequisiti ed è in grado di installare automaticamente i prerequisiti mancanti. <br><br>Per altre informazioni, vedere [installare AIP Unified Labeling client usando il programma di installazione eseguibile](#install-the-aip-unified-labeling-client-using-the-executable-installer).|
|**Distribuire la versione di Windows Installer (MSI) del client**     |     metodo supportato solo per le installazioni invisibili all'utente che usano un meccanismo di distribuzione centrale, ad esempio criteri di gruppo, Configuration Manager e Microsoft Intune. <br><br>Questo metodo è necessario per i PC Windows 10 gestiti da Intune e dalla gestione dispositivi mobili (MDM) poiché per questi computer, i file eseguibili non sono supportati per l'installazione. <br><br> Tuttavia, quando si usa questo metodo di installazione, è necessario verificare e installare o disinstallare manualmente il software dipendente che il programma di installazione eseguirebbe in ogni computer per il file eseguibile. <br><br>Per altre informazioni, vedere [installare il client Unified Labeling usando il programma di installazione MSI](#install-the-unified-labeling-client-using-the-msi-installer). |
|     |         |


Al termine dell'installazione del client di Azure Information Protection Unified Labeling, è possibile aggiornare il client ripetendo il metodo di installazione scelto oppure utilizzare Windows Update per impedire l'aggiornamento automatico del client. 

Per altre informazioni sull'aggiornamento, vedere la sezione [Aggiornamento e gestione del client Azure Information Protection](clientv2-admin-guide.md#upgrading-and-maintaining-the-azure-information-protection-unified-labeling-client).

## <a name="install-the-aip-unified-labeling-client-using-the-executable-installer"></a>Installare AIP Unified Labeling client usando il programma di installazione eseguibile

Usare le istruzioni seguenti per installare il client di quando *non* si usa il catalogo Microsoft Update o si [distribuisce il file con **estensione msi**](#install-the-unified-labeling-client-using-the-msi-installer) usando un metodo di distribuzione centrale, ad esempio Intune.

**Per installare il client di etichettatura unificata usando il file con estensione exe**:

1. Scaricare la versione eseguibile del client di Azure Information Protection Unified Labeling (nome file di **AzInfoProtection_UL**) dall' [area download Microsoft](https://www.microsoft.com/download/details.aspx?id=53018). 
    
    > [!IMPORTANT]
    > Se è disponibile una versione di anteprima, mantenerla solo per i test. Le versioni di questo tipo non sono progettate per l'uso in un ambiente di produzione. 
    >
 
1. Per un'installazione predefinita, è sufficiente eseguire il file eseguibile, ad esempio **AzInfoProtection_UL.exe**. 

    Per visualizzare tutte le opzioni di installazione, eseguire prima il file eseguibile con **/Help**: `AzInfoProtection_UL.exe /help`

    Ad esempio: 
    - Per installare automaticamente il client: `AzInfoProtection_UL.exe /quiet`
    
    - Per installare automaticamente solo i cmdlet di PowerShell: `AzInfoProtection_UL.exe  PowerShellOnly=true /quiet`
    
    Nella schermata della Guida non sono elencati i parametri seguenti:
        
    |Parametro  |Descrizione  |
    |---------|---------|
    |**AllowTelemetry = 0**     |    usare questo parametro per disabilitare l'opzione di installazione **Invia le statistiche di utilizzo a Microsoft per contribuire a migliorare Azure Information Protection**.     |
    |**ServiceLocation**     |  usare questo parametro se si installa il client in computer che eseguono Office 2010 e gli utenti non sono amministratori locali dei rispettivi computer o non si vuole che vengano visualizzati messaggi di richiesta. <br><br>Per altre informazioni, vedere: <br>- [Ulteriori informazioni sul parametro di installazione **ServiceLocation**](#more-information-about-the-servicelocation-installation-parameter) <br> - [AIP per versioni di Windows e Office nel supporto esteso](../known-issues.md#aip-for-windows-and-office-versions-in-extended-support)      |
    | | |

1. Per completare l'installazione: 

    - **Se il computer esegue [Office 2010](../known-issues.md#aip-for-windows-and-office-versions-in-extended-support)**, riavviare il computer. 
        
        Se il client non è stato installato con il parametro **ServiceLocation** , quando si apre per la prima volta una delle applicazioni di Office che usano il client unificato di Azure Information Protection (ad esempio, Word), è necessario confermare le richieste di aggiornamento del registro di sistema per il primo utilizzo. 

        Per il popolamento delle chiavi del Registro di sistema, viene usata l'[individuazione dei servizi](client-deployment-notes.md#rms-service-discovery). 
    
    - **Per le altre versioni di Office**, riavviare tutte le applicazioni di Office e tutte le istanze di Esplora file. 
        
1. Verificare che l'installazione abbia avuto esito positivo controllando il file di log di installazione, che per impostazione predefinita viene creato nella cartella **% Temp%** . 

    Il file di log di installazione ha il formato di denominazione seguente: `Microsoft_Azure_Information_Protection_<number>_<number>_MSIP.Setup.Main.msi.log`
    
    Ad esempio: **Microsoft_Azure_Information_Protection_20161201093652_000_MSIP.Setup.Main.msi.log**
    
    In questo file di log cercare la stringa seguente: **prodotto: Microsoft Azure Information Protection--installazione completata correttamente**. Se l'installazione non è riuscita, questo file di log contiene informazioni dettagliate per identificare e risolvere i problemi.

    > [!TIP]
    > È possibile modificare il percorso del file di log dell'installazione con il parametro di installazione **/log** . 
    >  
### <a name="more-information-about-the-servicelocation-installation-parameter"></a>Altre informazioni sul parametro di installazione ServiceLocation

Quando si installa il client per gli utenti che hanno [Office 2010](../known-issues.md#aip-for-windows-and-office-versions-in-extended-support) e non hanno autorizzazioni amministrative locali, specificare il parametro **SERVICELOCATION** e l'URL per il servizio Rights Management di Azure. 

Questo parametro e il relativo valore consentono di creare e impostare le chiavi del Registro di sistema seguenti:

`HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\MSDRM\ServiceLocation\Activation`

`HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\MSDRM\ServiceLocation\EnterprisePublishing`

`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSDRM\ServiceLocation\EnterprisePublishing`

`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSDRM\ServiceLocation\Activation`


**Per identificare il valore da specificare per il parametro ServiceLocation:**

1. Da una sessione di PowerShell eseguire prima di tutto [Connect-AipService](/powershell/module/aipservice/connect-aipservice) e specificare le credenziali di amministratore per connettersi al servizio Rights Management di Azure. Quindi eseguire [Get-AipServiceConfiguration](/powershell/module/aipservice/get-aipserviceconfiguration). 
 
    Se il modulo PowerShell per il servizio Rights Management di Azure non è già stato installato, vedere [installazione del modulo PowerShell AIPService](../install-powershell.md).

2. Nell'output identificare il valore **LicensingIntranetDistributionPointUrl**.

    Ad esempio: **LicensingIntranetDistributionPointUrl: https://5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com/_wmcs/licensing**

3. In questo valore rimuovere **/_wmcs/licensing** dalla stringa. Per esempio: **https://5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com**

    La stringa rimanente è il valore da specificare per il parametro ServiceLocation.

Ad esempio, per installare il client in modalità invisibile all'utente per [Office 2010](../known-issues.md#aip-for-windows-and-office-versions-in-extended-support) e Azure RMS:

```powershell
AzInfoProtection_UL.exe /quiet ServiceLocation=https://5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com
```


## <a name="install-the-unified-labeling-client-using-the-msi-installer"></a>Installare il client di etichettatura unificata usando il programma di installazione MSI

Per la distribuzione centrale, usare le informazioni seguenti specifiche per la versione di installazione con **estensione msi** del client Azure Information Protection Unified labeling. 

Se si usa Intune per il metodo di distribuzione del software, usare queste istruzioni insieme a quelle incluse in [Aggiungere app con Microsoft Intune](/mem/intune/apps/apps-add).

**Per installare il client di etichettatura unificata con il file con estensione msi**

1. Scaricare la versione **MSI** della Azure Information Protection Unified Labeling client (**AzInfoProtection_UL**) dall' [area download Microsoft](https://www.microsoft.com/download/details.aspx?id=53018). 
    
    > [!IMPORTANT]
    > Se è disponibile una versione di anteprima, mantenerla solo per i test. Le versioni di questo tipo non sono progettate per l'uso in un ambiente di produzione.
    > 

1. Per ogni computer che esegue il file con **estensione msi** , è necessario verificare che siano presenti le seguenti dipendenze software. 

    Ad esempio, creare un pacchetto con la versione **MSI** del client o distribuirla solo nei computer che soddisfano le dipendenze seguenti:
    
    |Versione di Office|Sistema operativo|Software|Action|
    |--------------------|--------------|----------------|---------------------|
    |**Tutte le versioni, ad eccezione di Office 365 1902 o versione successiva**|Solo Windows 10 versione 1809, build del sistema operativo precedenti alla build 17763.348|[KB 4482887](https://support.microsoft.com/help/4482887/windows-10-update-kb4482887)|Installazione|
    |**Office 2016**|Tutte le versioni supportate|64 bit: [KB3178666](https://www.microsoft.com/download/details.aspx?id=55007)<br /><br />32 bit: [KB3178666](https://www.microsoft.com/download/details.aspx?id=54999)<br /><br /> Versione: 1.0|Installazione|
    |**Office 2013**|Tutte le versioni supportate|64 bit: [KB3172523](https://www.microsoft.com/download/details.aspx?id=54992)<br /><br /> 32 bit: [KB3172523](https://www.microsoft.com/download/details.aspx?id=54979) <br /><br />Versione: 1.0|Installazione|
    |[**Office 2010**](../known-issues.md#aip-for-windows-and-office-versions-in-extended-support)|Tutte le versioni supportate|[Assistente per l'accesso ai Microsoft Online Services](https://www.microsoft.com/download/details.aspx?id=28177)<br /><br /> Versione: 2.1|Installazione|
    |[**Office 2010**](../known-issues.md#aip-for-windows-and-office-versions-in-extended-support)|Windows 8.1 e Windows Server 2012 R2|[KB2843630](https://www.microsoft.com/download/details.aspx?id=41708)<br /><br /> Numero di versione nel nome file: v3|Installare se non è installato KB2843630 o KB2919355|
    |[**Office 2010**](../known-issues.md#aip-for-windows-and-office-versions-in-extended-support)|Windows 8 e Windows Server 2012|[KB2843630](https://www.microsoft.com/download/details.aspx?id=41708)<br /><br /> Numero di versione nel nome file: v3|Installazione|
    | | | | |

1. Per un'installazione predefinita, eseguire il file MSI con **/quiet/**, ad esempio, `AzInfoProtection_UL.msi /quiet`.

    Potrebbe essere necessario specificare parametri di installazione aggiuntivi. Per ulteriori informazioni, vedere le [istruzioni del programma di installazione eseguibile](#install-the-aip-unified-labeling-client-using-the-executable-installer).

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