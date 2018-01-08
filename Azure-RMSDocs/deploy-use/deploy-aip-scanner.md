---
title: Distribuire lo scanner di Azure Information Protection
description: Istruzioni per installare, configurare ed eseguire lo scanner di Azure Information Protection per individuare, classificare e proteggere i file negli archivi dati.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 01/08/2018
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 20d29079-2fc2-4376-b5dc-380597f65e8a
ms.reviewer: demizets
ms.suite: ems
ms.openlocfilehash: 7dfd670df89b652f8ff55452198d8483b55c59cd
ms.sourcegitcommit: 2a7f20684a041385e2d2425ab886e46917d2da9a
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/03/2018
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

Lo scanner può controllare tutti i file indicizzabili da Windows, tramite iFilter installati nel computer. In seguito, per stabilire se i file devono essere etichettati, lo scanner usa il rilevamento di modelli e di tipi di dati sensibili della prevenzione della perdita di dati (DLP) predefiniti in Office 365 o i modelli regex di Office 365. Poiché usa il client di Azure Information Protection, lo scanner è in grado di classificare e proteggere gli stessi [tipi di file](../rms-client/client-admin-guide-file-types.md).

È possibile eseguire lo scanner solo in modalità di individuazione, in cui si usano i report per verificare che cosa accadrebbe se i file fossero etichettati. Oppure è possibile eseguire lo scanner per applicare automaticamente le etichette.

Si noti che lo scanner non individua e non applica etichette in tempo reale. Effettua sistematicamente una ricerca per indicizzazione nei file presenti negli archivi dati specificati ed è possibile configurare questo ciclo in modo da eseguirlo una o più volte.

## <a name="prerequisites-for-the-azure-information-protection-scanner"></a>Prerequisiti per lo scanner di Azure Information Protection
Prima di installare lo scanner di Azure Information Protection, verificare che i requisiti seguenti siano soddisfatti.

|Requisito|Altre informazioni|
|---------------|--------------------|
|Computer Windows Server per eseguire il servizio scanner:<br /><br />- 4 processori<br /><br />- 4 GB di RAM|Windows Server 2016 o Windows Server 2012 R2. <br /><br />Nota: per scopi di test o valutazione in un ambiente non di produzione, è possibile usare un sistema operativo client Windows [supportato dal client di Azure Information Protection](../get-started/requirements.md#client-devices).<br /><br />Il computer può essere un computer fisico o virtuale con una connessione di rete veloce e affidabile agli archivi dati da analizzare. <br /><br />Verificare che il computer abbia la [connettività Internet](../get-started/requirements.md#firewalls-and-network-infrastructure) necessaria per Azure Information Protection. In alternativa, è necessario configurarlo come [computer disconnesso](../rms-client/client-admin-guide-customizations.md#support-for-disconnected-computers). |
|SQL Server per archiviare la configurazione dello scanner:<br /><br />- Istanza locale o remota|SQL Server 2012 è la versione minima per le edizioni seguenti:<br /><br />- SQL Server Enterprise<br /><br />- SQL Server Standard<br /><br />- SQL Server Express|
|Account del servizio per eseguire il servizio scanner|Questo account deve essere un account di Active Directory sincronizzato con Azure AD, con i seguenti requisiti aggiuntivi:<br /><br />- Diritto di **accesso locale**. Questo diritto è richiesto per l'installazione e la configurazione dello scanner, ma non per il funzionamento. È necessario concedere questo diritto all'account del servizio, ma è possibile rimuoverlo dopo avere verificato che lo scanner è in grado di individuare, classificare e proteggere i file.<br /><br />- Diritto di **accesso come servizio**. Questo diritto viene concesso automaticamente all'account del servizio durante l'installazione dello scanner ed è richiesto per l'installazione, la configurazione e il funzionamento dello scanner. <br /><br />- Autorizzazioni per i repository di dati: è necessario concedere le autorizzazioni per la **lettura** e la **scrittura** per analizzare i file e quindi applicare la classificazione e la protezione ai file che soddisfano le condizioni indicate nei criteri di Azure Information Protection. Per eseguire lo scanner solo in modalità di individuazione, è sufficiente l'autorizzazione per la **lettura**.<br /><br />- Per le etichette che riproteggono o rimuovono la protezione: per garantire che lo scanner abbia sempre accesso ai file protetti, trasformare l'account in un [utente con privilegi avanzati](configure-super-users.md) per il servizio Azure Rights Management e verificare che sia abilitata la funzionalità per utenti con privilegi avanzati. Per altre informazioni sui requisiti dell'account per l'applicazione della protezione, vedere [Preparazione di utenti e gruppi per Azure Information Protection](../plan-design/prepare.md).|
|Il client di Azure Information Protection è installato nel computer Windows Server|Attualmente lo scanner di Azure Information Protection richiede la versione di anteprima del client di Azure Information Protection.<br /><br />È necessario installare il client completo per lo scanner. Non installare solo il modulo PowerShell del client.<br /><br />Per istruzioni sull'installazione del client, vedere la [guida per l'amministratore](../rms-client/client-admin-guide.md).|
|Etichette configurate che applicano la classificazione automatica e, facoltativamente, la protezione|Per altre informazioni sulle modalità di configurazione delle condizioni, vedere [Come configurare le condizioni per la classificazione automatica e consigliata per Azure Information Protection](configure-policy-classification.md).<br /><br />Per altre informazioni sulla configurazione delle etichette che applicano la protezione ai file, vedere [Come configurare un'etichetta per la protezione di Rights Management](configure-policy-protection.md).<br /><br />Queste etichette possono essere nei criteri globali oppure in uno o più [criteri con ambito](configure-policy-scope.md).|


## <a name="install-the-azure-information-protection-scanner"></a>Installare lo scanner di Azure Information Protection

1. Usando l'account del servizio creato per eseguire lo scanner, accedere al computer Windows Server in cui verrà eseguito lo scanner.

2. Aprire una sessione di Windows PowerShell con l'opzione **Esegui come amministratore**.

3. Eseguire il cmdlet [Install-AIPScanner](/powershell/module/azureinformationprotection/Install-AIPScanner), che specifica l'istanza di SQL Server in cui creare un database per lo scanner di Azure Information Protection: 
    
    ```
    Install-AIPScanner -SqlServerInstance <database name>
    ```
    
    Esempi:
    
    Per un'istanza predefinita: `Install-AIPScanner -SqlServerInstance SQLSERVER1`
    
    Per un'istanza denominata: `Install-AIPScanner -SqlServerInstance SQLSERVER1\AIPSCANNER`
    
    Per SQL Server Express: `Install-AIPScanner -SqlServerInstance SQLSERVER1\SQLEXPRESS`
    
    Usare la Guida in linea di questo cmdlet per visualizzare [esempi più dettagliati](/powershell/module/azureinformationprotection/install-aipscanner#examples).
    
    Quando richiesto, specificare le credenziali per l'account del servizio scanner (\<dominio\nome utente>) e la password.

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
    
    ad esempio `Add-AIPScannerRepository -Path \\NAS\Documents`
    
    Per altri esempi, vedere la [guida online](/powershell/module/azureinformationprotection/Add-AIPScannerRepository#examples) per questo cmdlet.

2. Ripetere questo comando per tutti gli archivi dati da analizzare. Per rimuovere un archivio dati aggiunto in precedenza, usare il cmdlet [Remove-AIPScannerRepository](/powershell/module/azureinformationprotection/Remove-AIPScannerRepository).

3. Verificare di avere specificato correttamente tutti gli archivi dati eseguendo il cmdlet [Get-AIPScannerRepository](/powershell/module/azureinformationprotection/Get-AIPScannerRepository):
    
        Get-AIPScannerRepository

Con la configurazione predefinita dello scanner ora è possibile eseguire la prima analisi in modalità di individuazione.

## <a name="run-a-discovery-cycle-and-view-reports-for-the-azure-information-protection-scanner"></a>Eseguire un ciclo di individuazione e visualizzare i report per lo scanner di Azure Information Protection

1. Usando **Strumenti di amministrazione** > **Servizi**, avviare il servizio **Azure Information Protection Scanner**.

2. Attendere che lo scanner completi il proprio ciclo. Quando lo scanner ha eseguito la ricerca per indicizzazione di tutti i file negli archivi dati specificati, il servizio si arresta. Per verificare che il servizio si sia arrestato, usare il registro eventi locale di **applicazioni e servizi** di Windows, **Azure Information Protection**. Cercare l'ID evento informativo **911**.

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

## <a name="when-files-are-rescanned-by-the-azure-information-protection-scanner"></a>Quando i file vengono analizzati di nuovo dallo scanner di Azure Information Protection

Per il primo ciclo di analisi, lo scanner analizza tutti i file negli archivi dati configurati e quindi per le analisi successive, vengono controllati solo i file nuovi o modificati. 

È possibile imporre allo scanner di ripetere l'analisi di tutti i file eseguendo [Set AIPScannerConfiguration](/powershell/module/azureinformationprotection/Set-AIPScannerConfiguration) con il parametro `-Type` impostato su **Full**. Questa configurazione è utile quando si vuole che i report includano tutti i file e viene in genere usata quando lo scanner viene eseguito in modalità di individuazione. Al termine di un'analisi completa, il tipo di analisi diventa automaticamente incrementale in modo che per le analisi successive vengono analizzati solo i file nuovi o modificati.

Inoltre, tutti i file vengono controllati quando lo scanner scarica un criterio di Azure Information Protection con condizioni nuove o modificate. Lo scanner aggiorna i criteri ogni ora e all'avvio del servizio.

## <a name="optimizing-the-performance-of-the-azure-information-protection-scanner"></a>Ottimizzazione delle prestazioni dello scanner di Azure Information Protection

Per ottimizzare le prestazioni dello scanner:

- **Disporre di una connessione di rete ad alta velocità e affidabile tra il computer dello scanner e l'archivio dei dati analizzati**
    
    Ad esempio, inserire il computer dello scanner nella stessa rete LAN o (scelta consigliata) nello stesso segmento di rete dell'archivio dei dati analizzati.
    
    La qualità della connessione di rete influisce sulle prestazioni dello scanner perché per controllare i file lo scanner trasferisce il contenuto dei file nel computer che esegue il servizio di analisi. Quando si riduce o si elimina il numero di hop di rete per i dati, si riduce anche il carico sulla rete. 

- **Verificare che il computer dello scanner abbia risorse del processore disponibili**
    
    La ricerca di una corrispondenza nel contenuto dei file in base alle condizioni configurate e la crittografia e la decrittografia dei file sono operazioni che richiedono un uso intensivo del processore. Monitorare i cicli di analisi tipici degli archivi dati specificati per identificare se una mancanza di risorse del processore influisce negativamente sulle prestazioni dello scanner.
    
- **Non eseguire l'analisi delle cartelle locali nel computer che esegue il servizio di analisi**
    
    Se sono presenti cartelle da analizzare in un server di Windows, installare lo scanner in un computer diverso e configurare le cartelle come condivisioni di rete da analizzare. La separazione delle due funzioni di hosting dei file e di analisi dei file fa in modo che le risorse di elaborazione di questi servizi non siano in competizione tra loro.

Altri fattori che influenzano le prestazioni dello scanner:

- Carico corrente e tempi di risposta degli archivi dati che contengono i file da analizzare

- Esecuzione dello scanner in modalità di individuazione o applicazione
    
    La modalità di individuazione ha in genere una velocità di analisi maggiore rispetto alla modalità di applicazione poiché l'individuazione richiede una sola azione di lettura dei file, mentre la modalità di applicazione richiede azioni di lettura e scrittura.

- Modifica delle condizioni in Azure Information Protection
    
    Il primo ciclo di analisi nel quale lo scanner deve controllare ogni file richiede più tempo rispetto ai cicli di analisi successivi in cui, per impostazione predefinita, vengono analizzati solo i file nuovi e modificati. Tuttavia, se si modificano le condizioni nei criteri di Azure Information Protection, tutti i file vengono analizzati nuovamente come descritto nella [sezione precedente](#when-files-are-rescanned-by-the-azure-information-protection-scanner).

- Livello di registrazione selezionato
    
    È possibile scegliere tra **Debug**, **Info** (Informazioni), **Error** (Errore) e **Off** (Disattivato) per i report dello scanner. **Off** (Disattivato) offre le prestazioni migliori; **Debug** rallenta considerevolmente lo scanner ed è consigliabile usarlo solo per la ricerca e la risoluzione dei problemi. Per altre informazioni, vedere il parametro *ReportLevel* del cmdlet [Set-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Set-AIPScannerConfiguration).

- File:
    
    - I file di Office vengono analizzati più rapidamente rispetto ai file PDF.
    
    - I file non protetti sono più veloci da analizzare rispetto ai file protetti.
    
    - I file di grandi dimensioni richiedono più tempo per l'analisi rispetto ai file di piccole dimensioni.

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

Usare le sezioni seguenti per identificare gli ID evento e le descrizioni possibili per lo scanner. Gli eventi vengono registrati nel server su cui viene seguito il servizio scanner, nel registro eventi di **applicazioni e servizi** di Windows, **Azure Information Protection**.

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

L'evento viene registrato quando lo scanner è configurato per essere eseguito una volta anziché continuamente e il servizio scanner di Azure Information Protection è stato riavviato manualmente dopo l'avvio del computer.  

Per analizzare nuovamente i file, è necessario impostare la pianificazione su **Una volta** o **Continuo** e riavviare manualmente il servizio. Per modificare la pianificazione, usare il cmdlet [Set AIPScannerConfiguration](/powershell/module/azureinformationprotection/Set-AIPScannerConfiguration) e il parametro **Pianificazione**.

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

Scoprire [Qual è la differenza tra Infrastruttura di classificazione file di Windows Server e lo scanner di Azure Information Protection](../get-started/faqs.md#whats-the-difference-between-windows-server-fci-and-the-azure-information-protection-scanner).

È anche possibile usare PowerShell per classificare e proteggere in modo interattivo i file dal computer desktop. Per altre informazioni su questo e altri scenari che usano PowerShell, vedere [Uso di PowerShell con il client Azure Information Protection](../rms-client/client-admin-guide-powershell.md).


[!INCLUDE[Commenting house rules](../includes/houserules.md)]
