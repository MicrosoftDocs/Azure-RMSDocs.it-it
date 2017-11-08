---
title: Distribuire lo scanner di Azure Information Protection
description: Istruzioni per installare, configurare ed eseguire lo scanner di Azure Information Protection per individuare, classificare e proteggere i file negli archivi dati.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 11/02/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 20d29079-2fc2-4376-b5dc-380597f65e8a
ms.reviewer: demizets
ms.suite: ems
ms.openlocfilehash: 924a9e0b19203f60827693adecc9b74fa62edef1
ms.sourcegitcommit: 92bbef77091c66300e0d2acce60c064ffe314752
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/03/2017
---
# <a name="deploying-the-azure-information-protection-scanner-to-automatically-classify-and-protect-files"></a>Distribuzione dello scanner di Azure Information Protection per classificare e proteggere automaticamente i file

>*Si applica a: Azure Information Protection, Windows Server 2016, Windows Server 2012 R2*

> [!NOTE]
> Al momento questa funzionalità è disponibile in anteprima ed è soggetta a modifiche.

Di seguito vengono illustrate le caratteristiche dello scanner di Azure Information Protection e le relative procedure per installarlo, configurarlo ed eseguirlo. 

Questo scanner viene eseguito come servizio in Windows Server e consente di individuare, classificare e proteggere i file negli archivi dati seguenti:

- Cartelle locali nel computer Windows Server che esegue lo scanner.

- Percorsi UNC per le condivisioni di rete che usano il protocollo CIFS (Common Internet File System).

- Siti e librerie per SharePoint Server 2016 e SharePoint Server 2013.

## <a name="overview-of-the-azure-information-protection-scanner"></a>Panoramica dello scanner di Azure Information Protection

Dopo aver configurato i [criteri di Azure Information Protection](configure-policy.md) per le etichette che applicano la classificazione automatica, è possibile etichettare i file rilevati dallo scanner. Le etichette applicano la classificazione e, facoltativamente, applicano o rimuovono la protezione:

![Panoramica dello scanner di Azure Information Protection](../media/infoprotect-scanner.png)

Per la classificazione automatica vengono usati i tipi di informazioni riservate e il rilevamento di modelli della prevenzione della perdita di dati (DLP) predefiniti in Office 365 o i criteri di espressione regolare di Office 365. Poiché usa il client di Azure Information Protection, lo scanner è in grado di classificare e proteggere gli stessi [tipi di file](../rms-client/client-admin-guide-file-types.md).

È possibile eseguire lo scanner solo in modalità di individuazione, in cui si usano i report per verificare che cosa accadrebbe se i file fossero etichettati. Oppure è possibile eseguire lo scanner per applicare automaticamente le etichette.

Si noti che lo scanner non individua e non applica etichette in tempo reale. Effettua sistematicamente una ricerca per indicizzazione nei file presenti negli archivi dati specificati ed è possibile configurare questo ciclo in modo da eseguirlo una o più volte.

## <a name="prerequisites-for-the-azure-information-protection-scanner"></a>Prerequisiti per lo scanner di Azure Information Protection
Prima di installare lo scanner di Azure Information Protection, verificare che i requisiti seguenti siano soddisfatti.

|Requisito|Altre informazioni|
|---------------|--------------------|
|Computer Windows Server per eseguire il servizio scanner:<br /><br />- 4 processi<br /><br />- 4 GB di RAM|Windows Server 2016 o Windows Server 2012 R2.<br /><br />Questo server può essere un computer fisico o virtuale con una connessione di rete veloce e affidabile agli archivi dati da analizzare. <br /><br />Verificare che il server usi la [connettività Internet](../get-started/requirements.md#firewalls-and-network-infrastructure) necessaria per Azure Information Protection. In alternativa, è necessario configurarlo come [computer disconnesso](../rms-client/client-admin-guide-customizations.md#support-for-disconnected-computers).|
|SQL Server per archiviare la configurazione dello scanner:<br /><br />- Istanza locale o remota|SQL Server 2012 R2 è la versione minima per le edizioni seguenti:<br /><br />- SQL Server Enterprise<br /><br />- SQL Server Standard<br /><br />- SQL Server Express|
|Account del servizio per eseguire il servizio scanner|Questo account deve essere un account di Active Directory sincronizzato con Azure AD, con i seguenti requisiti aggiuntivi:<br /><br />- Diritto di **accesso locale**. Questo diritto è richiesto per l'installazione e la configurazione dello scanner, ma non per il funzionamento. È necessario concedere questo diritto all'account del servizio, ma è possibile rimuoverlo dopo avere verificato che lo scanner è in grado di individuare, classificare e proteggere i file.<br /><br />- Diritto di **accesso come servizio**. Questo diritto viene concesso automaticamente all'account del servizio durante l'installazione dello scanner ed è richiesto per l'installazione, la configurazione e il funzionamento dello scanner. <br /><br />- Autorizzazioni per i repository di dati: è necessario concedere le autorizzazioni per la **lettura** e la **scrittura** per analizzare i file e quindi applicare la classificazione e la protezione ai file che soddisfano le condizioni indicate nei criteri di Azure Information Protection. Per eseguire lo scanner solo in modalità di individuazione, è sufficiente l'autorizzazione per la **lettura**.<br /><br />- Per le etichette che riproteggono o rimuovono la protezione: per garantire che lo scanner abbia sempre accesso ai file protetti, trasformare l'account in un [utente con privilegi avanzati](configure-super-users.md) per il servizio Azure Rights Management e verificare che sia abilitata la funzionalità per utenti con privilegi avanzati. Per altre informazioni sui requisiti dell'account per l'applicazione della protezione, vedere [Preparazione di utenti e gruppi per Azure Information Protection](../plan-design/prepare.md).|
|Il client di Azure Information Protection è installato nel computer Windows Server|Attualmente lo scanner di Azure Information Protection richiede la versione di anteprima del client di Azure Information Protection.<br /><br />Se si preferisce, è possibile installare il client solo con il modulo di PowerShell (AzureInformationProtection) usato per installare e configurare lo scanner.<br /><br />Per istruzioni sull'installazione del client, vedere la [guida per l'amministratore](../rms-client/client-admin-guide.md).|
|Etichette configurate che applicano la classificazione automatica e, facoltativamente, la protezione|Per altre informazioni sulle modalità di configurazione delle condizioni, vedere [Come configurare le condizioni per la classificazione automatica e consigliata per Azure Information Protection](/deploy-use/configure-policy-classification.md).<br /><br />Per altre informazioni sulla configurazione delle etichette che applicano la protezione ai file, vedere [Come configurare un'etichetta per la protezione di Rights Management](../deploy-use/configure-policy-protection.md). |


## <a name="install-the-azure-information-protection-scanner"></a>Installare lo scanner di Azure Information Protection

1. Usando l'account del servizio creato per eseguire lo scanner, accedere al computer Windows Server in cui verrà eseguito lo scanner.

2. Aprire una sessione di Windows PowerShell con l'opzione **Esegui come amministratore**.

3. Eseguire il cmdlet [Install-AIPScanner](/powershell/module/azureinformationprotection/Install-AIPScanner), che specifica l'istanza di SQL Server in cui creare un database per lo scanner di Azure Information Protection. Quando richiesto, inserire le credenziali per l'account del servizio scanner (\<dominio\nome utente>) e la password: 
    
    ```
    Install-AIPScanner -SqlServerInstance <database name>
    ```
    
    Esempi:
        
    - Per un'istanza predefinita: `Install-AIPScanner -SqlServerInstance SQLSERVER1`
    
    - Per un'istanza denominata: `Install-AIPScanner -SqlServerInstance SQLSERVER1\AIPSCANNER`
    
    - Per SQL Server Express: `Install-AIPScanner -SqlServerInstance SQLSERVER1\SQLEXPRESS`

4. Verificare che il servizio è ora installato usando **Strumenti di amministrazione** > **Servizi**. 
    
    Il servizio installato è denominato **Azure Information Protection Scanner** ed è configurato per essere eseguito usando l'account del servizio scanner creato.

Ora che è stato installato lo scanner, è necessario ottenere un token di Azure AD per l'account del servizio scanner da autenticare in modo che possa essere eseguito automaticamente. 

## <a name="get-an-azure-ad-token-for-the-scanner-service-account-to-authenticate-to-the-azure-information-protection-service"></a>Ottenere un token di Azure AD per l'account del servizio scanner da autenticare per il servizio Azure Information Protection

1. Dallo stesso computer Windows Server, o dal desktop, accedere al portale di Azure per creare due applicazioni di Azure AD necessarie per specificare un token di accesso per l'autenticazione. Dopo un accesso interattivo iniziale, questo token consente di eseguire lo scanner in modo non interattivo.
    
    Per creare queste applicazioni, seguire le istruzioni della sezione [Come assegnare un'etichetta ai file in modo non interattivo per Azure Information Protection](../rms-client/client-admin-guide-powershell.md#how-to-label-files-non-interactively-for-azure-information-protection) della guida per l'amministratore.

2. Dal computer Windows Server in cui viene mantenuto l'accesso con l'account del servizio scanner eseguire [Set-AIPAuthentication](/powershell/module/azureinformationprotection/set-aipauthentication), specificando i valori copiati dal passaggio precedente:
    
    ```
    Set-AIPAuthentication -webAppId <ID of the "Web app / API" application>  -webAppKey <key value generated in the "Web app / API" application> -nativeAppId <ID of the "Native" application >
    ```

3. Quando richiesto, specificare la password per le credenziali dell'account del servizio per Azure AD e quindi fare clic su **Accetto**.

Lo scanner ora ha un token per l'autenticazione ad Azure AD, che può essere valido per un anno, due anni, o senza scadenza, in base alla configurazione dell'**app Web/API** in Azure AD. Quando il token scade, è necessario ripetere i passaggi da 1 a 3.

A questo punto si è pronti a specificare gli archivi dati da analizzare. 

## <a name="specify-data-stores-for-the-azure-information-protection-scanner"></a>Specificare gli archivi dati per lo scanner di Azure Information Protection

Usare il cmdlet [Add-AIPScannerRepository](/powershell/module/azureinformationprotection/Add-AIPScannerRepository) per specificare gli archivi dati che devono essere analizzati dallo scanner di Azure Information Protection. È possibile specificare cartelle locali, percorsi UNC e URL di SharePoint Server per siti e librerie di SharePoint. 

Versioni di SharePoint supportate: SharePoint Server 2016 e SharePoint Server 2013.

1. Dallo stesso computer Windows Server, nella sessione di PowerShell, aggiungere il primo archivio dati eseguendo il comando seguente:
    
        Add-AIPScannerRepository -Path <path>
    
    Ad esempio: `Add-AIPScannerRepository -Path \\NAS\Documents`
    
    Per altri esempi, vedere la [guida online](/powershell/module/azureinformationprotection/Add-AIPScannerRepository#examples) per questo cmdlet.

2. Ripetere questo comando per tutti gli archivi dati da analizzare. Per rimuovere un archivio dati aggiunto in precedenza, usare il cmdlet [Remove-AIPScannerRepository](/powershell/module/azureinformationprotection/Remove-AIPScannerRepository).

3. Verificare di avere specificato correttamente tutti gli archivi dati eseguendo il cmdlet [Get-AIPScannerRepository](/powershell/module/azureinformationprotection/Get-AIPScannerRepository):
    
        Get-AIPScannerRepository

Con la configurazione predefinita dello scanner ora è possibile eseguire la prima analisi in modalità di individuazione.

## <a name="run-a-discovery-cycle-and-view-reports-for-the-azure-information-protection-scanner"></a>Eseguire un ciclo di individuazione e visualizzare i report per lo scanner di Azure Information Protection

1. Usando **Strumenti di amministrazione** > **Servizi**, avviare il servizio **Azure Information Protection Scanner**.

2. Attendere che lo scanner completi il proprio ciclo. Quando lo scanner ha eseguito la ricerca per indicizzazione di tutti i file negli archivi dati specificati, il servizio si arresta. Per verificare che il servizio si sia arrestato, usare il log eventi dell'**applicazione** di Windows, **Azure Information Protection Scanner**. Cercare l'ID evento informativo **911**.

3. Esaminare i report archiviati in %*localappdata*%\Microsoft\MSIP\Scanner\Reports con formato di file CSV. Con la configurazione predefinita dello scanner, solo i file che soddisfano le condizioni per la classificazione automatica vengono inclusi nei report.
    
    Se i risultati non sono quelli previsti, potrebbe essere necessario ottimizzare le condizioni specificate nei criteri di Azure Information Protection. In questo caso, ripetere i passaggi da 1 a 3 finché non si è pronti a modificare la configurazione per applicare la classificazione e, facoltativamente, la protezione. Ogni volta che si ripetono questi passaggi, eseguire per prima cosa il seguente comando di PowerShell nel computer Windows Server:
    
        Set-AIPScannerConfiguration -Schedule OneTime

Quando si è pronti ad etichettare automaticamente i file individuati dallo scanner, passare alla procedura successiva. 

## <a name="configure-the-azure-information-protection-scanner-to-apply-classification-and-protection-to-discovered-files"></a>Configurare lo scanner di Azure Information Protection per applicare la classificazione e la protezione ai file individuati

Per impostazione predefinita, lo scanner viene eseguito una volta e solo ai fini della creazione di report. Per modificare queste impostazioni, eseguire il cmdlet [Set-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Set-AIPScannerConfiguration).

1. Eseguire il comando seguente nel computer Windows Server, nella sessione di PowerShell:
    
        Set-AIPScannerConfiguration -ScanMode Enforce -Schedule Continuous
    
    Esistono altre impostazioni di configurazione che è opportuno modificare. Indicare ad esempio se gli attributi dei file vengono modificati e quali informazioni vengono registrate nei report. Inoltre, se i criteri di Azure Information Protection includono l'impostazione che richiede un messaggio di giustificazione per abbassare il livello di classificazione o rimuovere la protezione, specificare il messaggio usando questo cmdlet. Consultare la [guida online](/powershell/module/azureinformationprotection/Set-AIPScannerConfiguration#parameters) per altre informazioni sulle singole impostazioni di configurazione. 

2. Usando **Strumenti di amministrazione** > **Servizi**, riavviare il servizio **Azure Information Protection Scanner**.

3. Come in precedenza, monitorare il log eventi e i report per vedere quali file sono stati etichettati, quale classificazione è stata applicata e se è stata applicata la protezione.

Poiché la pianificazione è stata configurata in modo da essere eseguita continuamente, quando lo scanner ha completato l'analisi di tutti i file, avvia un nuovo ciclo per individuare i file nuovi e modificati.

## <a name="list-of-cmdlets-for-the-azure-information-protection-scanner"></a>Elenco di cmdlet per lo scanner di Azure Information Protection 

Altri cmdlet per lo scanner consentono di modificare l'account del servizio e il database per lo scanner, ottenere le impostazioni correnti per lo scanner e disinstallare il servizio scanner. Lo scanner usa i cmdlet seguenti:

- [Add-AIPScannerRepository](/powershell/module/azureinformationprotection/Add-AIPScannerRepository)

- [Get-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Get-AIPScannerConfiguration)

- [Get-AIPScannerRepository](/powershell/module/azureinformationprotection/Get-AIPScannerRepository)

- [Install-AIPScanner](/powershell/module/azureinformationprotection/Install-AIPScanner)

- [Remove-AIPScannerRepository](/powershell/module/azureinformationprotection/Remove-AIPScannerRepository)

- [Set-AIPScanner](/powershell/module/azureinformationprotection/Set-AIPScanner)

- [Set-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Set-AIPScannerConfiguration)

- [Uninstall-AIPScanner](/powershell/module/azureinformationprotection/Uninstall-AIPScanner)


## <a name="event-log-ids-and-descriptions"></a>ID registro eventi e descrizioni

Usare le sezioni seguenti per identificare gli ID evento e le descrizioni possibili per lo scanner.

-----

Informazione **910**

**Ciclo dello scanner avviato.**

Questo evento viene registrato quando il servizio scanner viene avviato e inizia a cercare i file negli archivi dati specificati.

----

Informazione **911**

**Ciclo dello scanner completato.**

Questo evento viene registrato quando lo scanner ha completato una singola analisi dopo l'avvio del server o ha completato un ciclo in caso di pianificazione continua.

----

Informazione **913**

**Lo scanner si è arrestato perché è impostato su Never.**

Questo evento viene registrato quando lo scanner è configurato per essere eseguito una volta anziché continuamente e il servizio scanner di Azure Information Protection è stato riavviato manualmente dopo l'avvio del computer.  

Per analizzare di nuovo i file, è necessario avviare manualmente il servizio. Per modificare questo comportamento in modo che lo scanner venga eseguito continuamente, usare il cmdlet [Set-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Set-AIPScannerConfiguration) e impostare il parametro **Schedule** su **Continuous**.

----

Errore **912**

**Si è verificato un errore sconosciuto.**

Altre informazioni vengono registrate nel report dettagliato archiviato in %localappdata%\Microsoft\MSIP\Scanner\Reports\DetailedReport_YYYY_MM_DD_HH_MM.csv.

Contattare il [supporto tecnico Microsoft](../get-started/information-support.md#to-contact-microsoft-support) se questo evento continua a essere registrato. 

----

Errore **914**

**Il servizio si è automaticamente arrestato a causa di una configurazione non valida: il file di criteri manca o è danneggiato.**

Questo evento viene registrato quando il client di Azure Information Protection non ha file di criteri valido per l'esecuzione dello scanner.

I criteri di Azure Information Protection sono archiviati in %localappdata%\Microsoft\MSIP e devono essere configurati con etichette che hanno le condizioni necessarie per applicare la classificazione automatica. Oppure, i criteri devono essere configurati per un'etichetta predefinita.

Verificare che i firewall non blocchino la connettività Internet necessaria. Per altre informazioni, vedere i requisiti relativi a [firewall e infrastruttura di rete](../get-started/requirements.md#firewalls-and-network-infrastructure) per Azure Information Protection. Se la connettività Internet non è possibile, seguire le istruzioni per il supporto dei [computer disconnessi](../rms-client/client-admin-guide-customizations.md#support-for-disconnected-computers).


## <a name="next-steps"></a>Passaggi successivi

È anche possibile usare PowerShell per classificare e proteggere in modo interattivo i file dal computer desktop. Per altre informazioni su questo e altri scenari che usano PowerShell, vedere [Uso di PowerShell con il client Azure Information Protection](../rms-client/client-admin-guide-powershell.md).


[!INCLUDE[Commenting house rules](../includes/houserules.md)]