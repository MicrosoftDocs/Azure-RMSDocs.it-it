---
title: Installare il client di Azure Information Protection classico per gli utenti
description: Istruzioni e informazioni per gli amministratori per la distribuzione di Azure Information Protection client classico per Windows nelle reti aziendali.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 11/15/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: ea3ec965-3720-4614-8564-3ecfe60bc175
ROBOTS: NOINDEX
ms.subservice: v1client
ms.reviewer: eymanor
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 2efab361e4ea1b74fdedf6cc6cc9735338d3633b
ms.sourcegitcommit: 78c7ab80be7c292ea4bc62954a4e29c449e97439
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/13/2021
ms.locfileid: "98164097"
---
# <a name="admin-guide-install-the-azure-information-protection-classic-client-for-users"></a>Guida dell'amministratore: installare il client classico Azure Information Protection per gli utenti

>***Si applica a**: Active Directory Rights Management Services, [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8, Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012 *
>
>***Pertinente per**: [Azure Information Protection client classico per Windows](../faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients). Per il client di etichettatura unificata, vedere la [Guida dell'amministratore del client Unified Labeling](clientv2-admin-guide-install.md). *

> [!NOTE] 
> Per offrire un'esperienza per i clienti unificata e semplificata, il **client classico di Azure Information Protection** e **Gestione etichette** nel portale di Azure saranno **deprecati** a partire dal **31 marzo 2021**. In questo intervallo di tempo tutti i clienti correnti di Azure Information Protection possono passare alla soluzione di etichettatura unificata usando la piattaforma di etichettatura unificata di Microsoft Information Protection. Altre informazioni nell'[avviso ufficiale sulla deprecazione](https://aka.ms/aipclassicsunset).
>
> **Per distribuire il client classico di AIP**, aprire un ticket di supporto per ottenere l'accesso al download.

Prima di installare il client Azure Information Protection nella rete aziendale, verificare che nei computer siano installate le versioni del sistema operativo e le applicazioni richieste per Azure Information Protection: [Requisiti per Azure Information Protection](../requirements.md).

Verificare quindi gli altri prerequisiti che possono essere necessari per il client Azure Information Protection descritti nella sezione seguente. Il programma di installazione non verifica tutti i prerequisiti.

## <a name="additional-prerequisites-for-the-azure-information-protection-client"></a>Altri prerequisiti per il client Azure Information Protection

- **4.6.2 Framework di Microsoft .NET**

    Per impostazione predefinita, l'installazione completa del client Azure Information Protection richiede almeno Microsoft .NET Framework 4.6.2. Se questo prerequisito non è soddisfatto, la configurazione guidata dal programma di installazione eseguibile prova a scaricare e installare la versione richiesta. Quando questo prerequisito viene installato come parte dell'installazione del client, è necessario riavviare il computer. Anche se non è consigliabile, è possibile ignorare questo prerequisito quando si esegue la configurazione guidata usando un [parametro di installazione personalizzato](#more-information-about-the-downgradedotnetrequirement-installation-parameter).

    Questo prerequisito non viene installato automaticamente quando si installa il client in modalità invisibile all'utente tramite il programma di installazione eseguibile, Windows Update o Windows Installer. Per questi scenari, è necessario installare questo prerequisito separatamente, se necessario, altrimenti l'installazione non riesce. È possibile scaricare Microsoft .NET Framework 4.6.2 (programma di installazione offline) dall'[Area download Microsoft](https://www.microsoft.com/download/details.aspx?id=53344).

- **Microsoft .NET Framework 4.5.2**

    Se il visualizzatore Azure Information Protection viene installato separatamente, è necessario Microsoft .NET Framework 4.5.2 come versione minima. In caso contrario, il programma di installazione eseguibile non esegue il download o l'installazione.

- **Versione minima di Windows PowerShell 4,0**

    Il modulo PowerShell per il client richiede una versione minima di 4,0 per Windows PowerShell, che potrebbe essere necessario installare in sistemi operativi precedenti. Per altre informazioni, vedere [How to Install Windows PowerShell 4.0](https://social.technet.microsoft.com/wiki/contents/articles/21016.how-to-install-windows-powershell-4-0.aspx) (Come installare Windows PowerShell 4.0). Il programma di installazione non controlla né installa questo prerequisito per l'utente. Per verificare quale versione di Windows PowerShell è in esecuzione, digitare `$PSVersionTable` in una sessione di PowerShell.

- **Risoluzione dello schermo superiore a 800x600**

    Alle risoluzioni 800x600 e inferiori non è possibile visualizzare completamente la finestra di dialogo **Classifica e proteggi - Azure Information Protection** facendo clic con il pulsante destro del mouse su un file o una cartella in Esplora file.

- **Assistente per l'accesso ai Microsoft Online Services 7.250.4303.0**

    I computer che eseguono Office 2010 richiedono l'Assistente per l'accesso ai Microsoft Online Services versione 7.250.4303.0. Questa versione è inclusa nell'installazione del client. 

    Se si usa una versione successiva dell'Assistente per l'accesso, disinstallarla prima di installare il client Azure Information Protection. Controllare, ad esempio, la versione e disinstallare l'assistente per l'accesso tramite il **Pannello di controllo**  >  **programmi e funzionalità**  >  **Disinstalla o modifica programma**.

    Per ulteriori informazioni, vedere [AIP per le versioni di Windows e Office nel supporto esteso](../known-issues.md#aip-for-windows-and-office-versions-in-extended-support).


- **KB 4482887**

    Solo per Windows 10 versione 1809, per le build del sistema operativo precedenti alla build 17763.348, installare [1 marzo 2019 - KB4482887 (build sistema operativo 17763.348)](https://support.microsoft.com/help/4482887/windows-10-update-kb4482887) per garantire che la barra di Information Protection venga visualizzata correttamente nelle applicazioni Office. Questo aggiornamento non è necessario se si usa Office 365 1902 o versione successiva.

- **Configurare i criteri di gruppo per impedire la disabilitazione del componente aggiuntivo Azure Information Protection**

    Per Office 2013 e versioni successive, configurare i criteri di gruppo per garantire che il componente aggiuntivo **Microsoft Azure Information Protection** per le applicazioni di Office sia sempre abilitato. Senza questa configurazione, è possibile che il componente aggiuntivo Microsoft Azure Information Protection venga disabilitato e gli utenti non potranno assegnare etichette a documenti e messaggi di posta elettronica nella propria applicazione Office.

    - **Per Outlook:** Utilizzare l'impostazione di criteri di gruppo documentata in [controllo amministratore di sistema sui componenti](/office/vba/outlook/concepts/getting-started/support-for-keeping-add-ins-enabled#system-administrator-control-over-add-ins) aggiuntivi dalla documentazione di Office.

    - **Per Word, Excel e PowerPoint:** Usare l' **elenco delle impostazioni di criteri di gruppo dei componenti aggiuntivi gestiti** documentati nell'articolo del supporto tecnico [nessun componente aggiuntivo caricato a causa delle impostazioni di criteri di gruppo per i programmi Office 2013 e Office 2016](https://support.microsoft.com/help/2733070/no-add-ins-loaded-due-to-group-policy-settings-for-office-2013-and-off).

        Specificare gli identificatori seguenti a livello di codice (ProgID) per Azure Information Protection e impostare l'opzione su **1: The add-in is always enabled** (1: Sempre attivato).

        **Per Word:**`MSIP.WordAddin`

        **Per Excel:**`MSIP.ExcelAddin`

        **Per PowerPoint:**`MSIP.PowerPointAddin`

- **Protezione dagli exploit.** 

    Il client AIP non è supportato nei computer con .NET versione 2 o 3 con [protezione dagli exploit](/windows/security/threat-protection/microsoft-defender-atp/enable-exploit-protection) abilitata. Se il computer dispone di .NET versione 2 o 3, oltre a una versione di .NET 4. x sopra elencata, assicurarsi di [disabilitare la protezione dagli exploit](../known-issues.md#known-issues-for-aip-and-exploit-protection) prima di installare il client AIP.  

> [!IMPORTANT]
> L'installazione del client Azure Information Protection richiede autorizzazioni amministrative locali.

## <a name="options-to-install-the-azure-information-protection-client-for-users"></a>Opzioni di installazione del client Azure Information Protection per gli utenti

Usare una delle opzioni seguenti per installare il client per gli utenti:

|Opzione di installazione  |Description  |
|---------|---------|
|**Eseguire il file eseguibile del client (exe)**  <br><br> [Istruzioni](#to-install-the-azure-information-protection-client-by-using-the-executable-installer)      | È consigliabile eseguire la versione exe del client per eseguire l'installazione in modo interattivo o invisibile all'utente.<br><br> L'esecuzione del file con estensione exe presenta la massima flessibilità ed è consigliata perché controlla anche la presenza di molti prerequisiti e può anche installare eventuali prerequisiti mancanti. |
|**Distribuire il programma di installazione di Windows (MSI) del client** <br><br> [Istruzioni](#to-install-the-azure-information-protection-client-by-using-the-msi-installer)    | Il programma di installazione di Windows client Azure Information Protection è supportato solo per le installazioni automatiche che utilizzano un meccanismo di distribuzione centrale.<br><br> Usare, ad esempio, il file con estensione msi quando si distribuisce con criteri di gruppo, Configuration Manager e Microsoft Intune.<br><br> È necessario usare questo metodo per i PC Windows 10 gestiti da Intune e la gestione di dispositivi mobili (MDM) come file con estensione exe non supportati per questi computer.<br><br>**Nota**: quando si usa l'installazione con estensione msi, è necessario verificare manualmente la presenza di prerequisiti e installare o disinstallare il software dipendente necessario. |

Dopo aver installato il client, eseguire gli aggiornamenti ripetendo lo stesso metodo di installazione o utilizzare Windows Update per aggiornare automaticamente il client. Non è necessario disinstallare le versioni legacy del client prima di installare una nuova versione.

Per altre informazioni, vedere [Aggiornamento e gestione del client Azure Information Protection](client-admin-guide.md#upgrading-and-maintaining-the-azure-information-protection-client).

> [!NOTE]
> Per disinstallare il client, utilizzare l'opzione **Installazione applicazioni** di Windows, ad esempio [dal pannello di controllo di Windows](https://support.microsoft.com/help/4028054/windows-10-repair-or-remove-programs).

### <a name="to-install-the-azure-information-protection-client-by-using-the-executable-installer"></a>Per installare il client Azure Information Protection usando il programma di installazione del file eseguibile

Usare le istruzioni riportate di seguito per installare il client quando non si usa il catalogo di Microsoft Update o si distribuisce il file con estensione MSI usando un metodo di distribuzione centrale, ad esempio Intune.

1. Per un'installazione predefinita, basta eseguire il file eseguibile, ad esempio **AzInfoProtection.exe**. 

    Per visualizzare altre opzioni di installazione, eseguire prima il file eseguibile con **/Help**: `AzInfoProtection.exe /help`

    Esempio per installare automaticamente il client: `AzInfoProtection.exe /quiet`

    Esempio per installare automaticamente solo i cmdlet di PowerShell: `AzInfoProtection.exe  PowerShellOnly=true /quiet`

    Nella schermata della Guida non sono elencati i parametri seguenti:

    - **ServiceLocation**: usare questo parametro se si installa il client in computer che eseguono Office 2010 e gli utenti non sono amministratori locali dei rispettivi computer o non si vuole che vengano visualizzati messaggi di richiesta. 
    
        Per ulteriori informazioni, vedere [altre informazioni sul parametro di installazione ServiceLocation](#more-information-about-the-servicelocation-installation-parameter) e [AIP per le versioni di Windows e Office nel supporto esteso](../known-issues.md#aip-for-windows-and-office-versions-in-extended-support).

    - **DowngradeDotNetRequirement**: usare questo parametro per ignorare il requisito relativo a Microsoft .NET Framework versione 4.6.2. [Altre informazioni](#more-information-about-the-downgradedotnetrequirement-installation-parameter)

    - **AllowTelemetry = 0**: usare questo parametro per disabilitare l'opzione di installazione **Invia le statistiche di utilizzo a Microsoft per contribuire a migliorare Azure Information Protection**.

1. Se si installa in modo interattivo, selezionare l'opzione per l'installazione di un **criterio demo** se non si riesce a connettersi a Microsoft 365 o Azure Active Directory, ma si vuole vedere e provare il lato client di Azure Information Protection usando un criterio locale a scopo dimostrativo. Quando il client si connette a un servizio di Azure Information Protection, questo criterio demo viene sostituito dai criteri di Azure Information Protection dell'organizzazione.

1. Per completare l'installazione:

    - **Se il computer esegue Office 2010**, riavviare il computer.

        Se il client non è stato installato con il parametro **ServiceLocation** , quando si apre per la prima volta una delle applicazioni di Office che usano la barra Azure Information Protection (ad esempio, Word), è necessario confermare le richieste di aggiornamento del registro di sistema per il primo utilizzo. Per il popolamento delle chiavi del Registro di sistema, viene usata l'[individuazione dei servizi](client-deployment-notes.md#rms-service-discovery).

        Per ulteriori informazioni, vedere [AIP per le versioni di Windows e Office nel supporto esteso](../known-issues.md#aip-for-windows-and-office-versions-in-extended-support).


    - **Per le altre versioni di Office**, riavviare tutte le applicazioni di Office e tutte le istanze di Esplora file.

1. È possibile verificare se l'installazione è stata completata controllando il file di log di installazione, che per impostazione predefinita viene creato nella cartella %temp%. È possibile modificare questo percorso con il parametro di installazione **/log**.

    Questo file ha il formato di denominazione seguente: `Microsoft_Azure_Information_Protection_<number>_<number>_MSIP.Setup.Main.msi.log`

    Ad esempio: **Microsoft_Azure_Information_Protection_20161201093652_000_MSIP.Setup.Main.msi.log**

    In questo file di log, cercare la stringa seguente: **Product: Microsoft Azure Information Protection -- Installation completed successfully.** (Prodotto: Microsoft Azure Information Protection -- Installazione completata.) Se l'installazione non è riuscita, questo file di log contiene informazioni dettagliate per identificare e risolvere i problemi.

#### <a name="more-information-about-the-servicelocation-installation-parameter"></a>Altre informazioni sul parametro di installazione ServiceLocation

Quando si installa il client per gli utenti che hanno Office 2010 e non hanno autorizzazioni amministrative locali, specificare il parametro **ServiceLocation** e l'URL per il servizio Rights Management di Azure. Questo parametro e il relativo valore consentono di creare e impostare le chiavi del Registro di sistema seguenti:

`HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\MSDRM\ServiceLocation\Activation`

`HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\MSDRM\ServiceLocation\EnterprisePublishing`

`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSDRM\ServiceLocation\EnterprisePublishing`

`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSDRM\ServiceLocation\Activation`

Utilizzare la [procedura seguente](#to-identify-the-value-to-specify-for-the-servicelocation-parameter) per identificare il valore da specificare per il parametro **ServiceLocation** .

Per ulteriori informazioni, vedere [AIP per le versioni di Windows e Office nel supporto esteso](../known-issues.md#aip-for-windows-and-office-versions-in-extended-support).

##### <a name="to-identify-the-value-to-specify-for-the-servicelocation-parameter"></a>Per identificare il valore da specificare per il parametro ServiceLocation

1. Da una sessione di PowerShell eseguire prima di tutto [Connect-AipService](/powershell/module/aipservice/connect-aipservice) e specificare le credenziali di amministratore per connettersi al servizio Rights Management di Azure. Quindi eseguire [Get-AipServiceConfiguration](/powershell/module/aipservice/get-aipserviceconfiguration).

    Se il modulo PowerShell per il servizio Rights Management di Azure non è già stato installato, vedere [installazione del modulo PowerShell AIPService](../install-powershell.md).

2. Nell'output identificare il valore **LicensingIntranetDistributionPointUrl**.

    Ad esempio: **LicensingIntranetDistributionPointUrl: https://5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com/_wmcs/licensing**

3. In questo valore rimuovere **/_wmcs/licensing** dalla stringa. Per esempio: **https://5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com**

    La stringa rimanente è il valore da specificare per il parametro **ServiceLocation** .

Esempio per installare il client in modalità invisibile all'utente per [Office 2010](../known-issues.md#aip-for-windows-and-office-versions-in-extended-support) e Azure RMS: 

`AzInfoProtection_UL.exe /quiet ServiceLocation=https://5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com`

#### <a name="more-information-about-the-downgradedotnetrequirement-installation-parameter"></a>Altre informazioni sul parametro di installazione DowngradeDotNetRequirement installation

Per il supporto degli aggiornamenti automatici tramite Windows Update e per l'integrazione affidabile con le applicazioni di Office, il client Azure Information Protection usa Microsoft .NET Framework versione 4.6.2. Per impostazione predefinita, l'installazione interattiva tramite file eseguibile controlla se questa versione è presente e, in caso negativo, prova a installarla. A questo punto è necessario riavviare il computer.

Se l'installazione di questa versione più recente di Microsoft .NET Framework non è una soluzione efficace, è possibile installare il client con il parametro **DowngradeDotNetRequirement=True**, in modo da ignorare questo requisito se è installato Microsoft .NET Framework versione 4.5.1.

Ad esempio: `AzInfoProtection.exe DowngradeDotNetRequirement=True`

È consigliabile usare questo parametro con cautela, tenendo presente che sono stati segnalati problemi di blocco delle applicazioni di Office quando il client Azure Information Protection viene usato con questa versione precedente di Microsoft .NET Framework. Se si riscontrano problemi di blocco delle applicazioni, eseguire l'aggiornamento alla versione consigliata prima di provare altre soluzioni. 

Tenere anche presente che se si usa Windows Update per mantenere aggiornato il client Azure Information Protection, è necessario adottare un altro meccanismo di distribuzione del software per aggiornare il client alle versioni successive.

### <a name="to-install-the-azure-information-protection-client-by-using-the-msi-installer"></a>Per installare il client Azure Information Protection usando il programma di installazione MSI

Per la distribuzione centrale, usare le seguenti informazioni specifiche della versione dell'installazione MSI del client Azure Information Protection. 

Se si usa Intune per il metodo di distribuzione del software, usare queste istruzioni insieme a quelle incluse in [Aggiungere app con Microsoft Intune](/intune/apps/apps-add).

1. Per ogni computer che esegue il file con **estensione msi** , è necessario verificare che siano presenti le seguenti dipendenze software. Ad esempio, creare un pacchetto con la versione **MSI** del client o distribuirla solo nei computer che soddisfano le dipendenze seguenti:
    
    |Versione di Office|Sistema operativo|Software|Azione|
    |--------------------|--------------|----------------|---------------------|
    |**Tutte le versioni, ad eccezione di Office 365 1902 o versione successiva**|Solo Windows 10 versione 1809, build del sistema operativo precedenti alla build 17763.348|[KB 4482887](https://support.microsoft.com/help/4482887/windows-10-update-kb4482887)|Installazione|
    |**Office 2013**|Tutte le versioni supportate|64 bit: [KB3172523](https://www.microsoft.com/download/details.aspx?id=54992)<br /><br /> 32 bit: [KB3172523](https://www.microsoft.com/download/details.aspx?id=54979) <br /><br />Versione: 1.0|Installazione|
    |**Office 2010**|Tutte le versioni supportate|[Assistente per l'accesso ai Microsoft Online Services](https://www.microsoft.com/download/details.aspx?id=28177)<br /><br /> Versione: 2.1|Installazione|
    |**Office 2016**|Tutte le versioni supportate|64 bit: [KB3178666](https://www.microsoft.com/download/details.aspx?id=55007)<br /><br />32 bit: [KB3178666](https://www.microsoft.com/download/details.aspx?id=54999)<br /><br /> Versione: 1.0|Installazione|
    |**Office 2010**|Tutte le versioni supportate|[Assistente per l'accesso ai Microsoft Online Services](https://www.microsoft.com/download/details.aspx?id=28177)<br /><br /> Versione: 2.1|Installazione|
    |**Office 2010**|Windows 8.1 e Windows Server 2012 R2|[KB2843630](https://www.microsoft.com/download/details.aspx?id=41708)<br /><br /> Numero di versione nel nome file: v3|Installare se non è installato KB2843630 o KB2919355|
    |**Office 2010**|Windows 8 e Windows Server 2012|[KB2843630](https://www.microsoft.com/download/details.aspx?id=41708)<br /><br /> Numero di versione nel nome file: v3|Installazione|
    | | | | |

    Per ulteriori informazioni su AIP e Office 2010, vedere [AIP per le versioni di Windows e Office nel supporto esteso](../known-issues.md#aip-for-windows-and-office-versions-in-extended-support).

1. Per un'installazione predefinita, eseguire il file MSI con **/quiet/**, ad esempio, `AzInfoProtection.msi /quiet`. Tuttavia, può essere necessario specificare parametri di installazione aggiuntivi, che sono documentati nelle [istruzioni del programma di installazione del file eseguibile](#to-install-the-azure-information-protection-client-by-using-the-executable-installer).

    > [!NOTE]
    > Per impostazione predefinita, l'opzione **migliora Azure Information Protection inviando le statistiche di utilizzo all'** opzione di installazione Microsoft è abilitata. Per disabilitare questa opzione, assicurarsi di eseguire una delle operazioni seguenti:
    >
    >- Durante l'installazione, specificare **AllowTelemetry = 0**
    >- Dopo l'installazione, aggiornare la chiave del registro di sistema come indicato di seguito: **EnableTelemetry = 0**.
    >

## <a name="how-to-install-the-azure-information-protection-scanner"></a>Come installare lo scanner Azure Information Protection

Il modulo PowerShell incluso con il client di Azure Information Protection contiene i cmdlet per installare e configurare lo scanner. Per usare lo scanner è tuttavia necessario installare la versione completa del client. Non è possibile installare solo il modulo PowerShell.

Per installare il client per lo scanner, seguire le istruzioni delle sezioni precedenti. A questo punto si è pronti per configurare e quindi installare lo scanner. Per altre informazioni, vedere [che cos'è il Azure Information Protection scanner classico?](../deploy-aip-scanner-classic.md).

## <a name="next-steps"></a>Passaggi successivi

Dopo aver installato il client Azure Information Protection, vedere gli argomenti seguenti per altre informazioni che potrebbero essere necessarie per supportare il client:

- [Personalizzazioni](client-admin-guide-customizations.md)

- [File del client e registrazione dell'utilizzo](client-admin-guide-files-and-logging.md)

- [Rilevamento dei documenti](client-admin-guide-document-tracking.md)

- [Tipi di file supportati](client-admin-guide-file-types.md)

- [Comandi di PowerShell](client-admin-guide-powershell.md)