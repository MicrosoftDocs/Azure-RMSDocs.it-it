---
title: Avvio rapido - Trovare le informazioni riservate nei file tramite lo scanner di Azure Information Protection - AIP
description: Usare lo scanner di Azure Information Protection per trovare le informazioni riservate presenti nei file archiviati in locale.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 01/16/2019
ms.topic: quickstart
ms.service: information-protection
ms.openlocfilehash: 12bde16a9b1659d00137720ad7c804db32cb1556
ms.sourcegitcommit: 2c90f5bf11ec34ab94824a39ccab75bde71fc3aa
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/15/2019
ms.locfileid: "54314833"
---
# <a name="quickstart-find-what-sensitive-information-you-have-in-files-stored-on-premises"></a>Guida introduttiva: Trovare le informazioni riservate presenti nei file archiviati in locale

In questa guida introduttiva verrà installato e configurato lo scanner di Azure Information Protection per trovare le informazioni riservate presenti nei file archiviati in un archivio dati locale, ad esempio una cartella locale, una condivisione di rete o SharePoint Server.

Nota: in questo articolo di avvio rapido viene usata la versione disponibile a livello generale corrente dello scanner e non la versione di anteprima, che usa il portale di Azure per la configurazione.

È possibile completare questa configurazione in meno di 10 minuti.

## <a name="prerequisites"></a>Prerequisiti

Per completare questa guida introduttiva, è necessario:

1. Disporre di una sottoscrizione che includa un piano 1 o 2 di Azure Information Protection.
    
    In assenza di una di queste sottoscrizioni, è possibile creare un account [gratuito](https://portal.office.com/Signup/Signup.aspx?OfferId=87dd2714-d452-48a0-a809-d2f58c4f68b7) per l'organizzazione.

2. Aver installato il client Azure Information Protection nel computer in uso. 
    
    Per installare il client, andare all'[Area download Microsoft](https://www.microsoft.com/en-us/download/details.aspx?id=53018) e scaricare **AzInfoProtection.exe** dalla pagina di Azure Information Protection.
    
3. Aver installato anche SQL Server Express nel computer in uso.
    
    Se questa edizione di SQL Server non è già installata, è possibile scaricarla dall'[Area download Microsoft](https://www.microsoft.com/en-us/sql-server/sql-server-editions-express) e selezionare un'installazione di base.

4. Aver sincronizzato l'account di dominio con Azure AD.

Per un elenco completo dei prerequisiti per l'uso di Azure Information Protection, vedere [Requisiti per Azure Information Protection](requirements.md).

## <a name="prepare-a-test-folder-and-file"></a>Preparare una cartella e un file di test

Per un test iniziale per confermare il funzionamento dello scanner:

1. Creare una cartella locale nel computer, ad esempio **TestScanner** nell'unità C locale.

2. Creare e salvare un documento di Word nella cartella, con il testo **4242-4242-4242-4242** (un numero di carta di credito noto per il test).

## <a name="install-the-scanner"></a>Installare lo scanner

1. Aprire una sessione di PowerShell con l'opzione **Esegui come amministratore**.

2. Usare il comando seguente per installare lo scanner, specificando il proprio nome computer:
    
        Install-AIPScanner -SqlServerInstance <your computer name>\SQLEXPRESS
    
    Quando richiesto, fornire le proprie credenziali per lo scanner usando il formato \<dominio\nome utente> e quindi specificare la password. 

## <a name="specify-your-test-data-store"></a>Specificare l'archivio dati di test

Nella sessione di PowerShell digitare il comando seguente:

    Add-AIPScannerRepository -Path C:\TestScanner

## <a name="configure-the-scanner-to-discover-all-information-types"></a>Configurare lo scanner per individuare tutti i tipi di informazioni

Nella sessione di PowerShell digitare il comando seguente:

    Set-AIPScannerConfiguration -Enforce Off -Schedule Manual -DiscoverInformationTypes All

Questo comando consente di configurare lo scanner per eseguire un'individuazione singola di tutti i file nel repository dei dati specificato. Questa analisi individua tutti i tipi noti di informazioni riservate e non richiede la configurazione preliminare delle etichette o delle impostazioni dei criteri di Azure Information Protection.

## <a name="start-the-scan-and-confirm-it-finished"></a>Avviare l'analisi e confermarne il completamento

1. Nella sessione di PowerShell digitare il comando seguente per avviare lo scanner:
    
        Start-AIPScan
    
    È presente solo un file di piccole dimensioni da controllare, pertanto questa analisi di test iniziale sarà molto rapida. 

2. Passare a **Visualizzatore eventi di Windows** > **Applicazioni e servizi** > **log eventi di Azure Information Protection**. 
    
    Verificare che Azure Information Protection riporti l'ID evento informativo **911** per il processo **MSIP.Scanner**. La voce del log eventi include anche un riepilogo dei risultati dell'analisi.

## <a name="see-detailed-results"></a>Visualizzare i risultati dettagliati

In Esplora file individuare i report dello scanner in %*localappdata*%\Microsoft\MSIP\Scanner\Reports. Aprire il file di report dettagliato in formato CSV.

In Excel le prime due colonne visualizzano il repository dell'archivio dati e il nome file. Durante l'analisi, si noterà una colonna denominata **Information Type Name** (Nome tipo di informazioni), che è quella di maggiore interesse. Per il test iniziale, viene visualizzato il **numero di carta di credito**, uno dei diversi tipi di informazioni riservate che lo scanner può rilevare.

## <a name="scan-your-own-data"></a>Analizzare i dati personali

1. Eseguire nuovamente Add-AIPScannerRepository, questa volta specificando il proprio archivio dati in locale da analizzare per trovare le informazioni riservate. 
    
    È possibile specificare una cartella locale, una condivisione di rete (percorso UNC) o un URL di SharePoint Server per un sito o una raccolta di SharePoint. 
    
    - Esempio per una cartella locale:
        
            Add-AIPScannerRepository -Path D:\Data\Finance
    
    - Esempio per una condivisione di rete:
        
            Add-AIPScannerRepository -Path \\NAS\HR
    
    - Esempio per una cartella di SharePoint:
        
            Add-AIPScannerRepository -Path "http://sp2016/Shared Documents"

2. Riavviare lo scanner:
    
        Start-AIPScan

3. Visualizzare i nuovi risultati al termine dell'analisi. 
    
    La durata dell'analisi dipende dal numero di file presenti nell'archivio dati, dalla loro dimensione e dal tipo di file. 

## <a name="clean-up-resources"></a>Pulizia delle risorse

In un ambiente di produzione lo scanner viene eseguito in Windows Server, usando un account del servizio che esegue automaticamente l'autenticazione al servizio Azure Information Protection. È anche possibile usare una versione di livello aziendale di SQL Server e specificare diversi repository dei dati. 

Per pulire le risorse, in preparazione alla distribuzione di produzione, nella sessione di PowerShell eseguire il comando seguente per disinstallare lo scanner:

    Uninstall-AIPScanner

Riavviare quindi il computer.

Questo comando non rimuove gli elementi seguenti, che è pertanto necessario rimuovere manualmente se non si vuole conservarli dopo questa guida introduttiva:

- Il database SQL Server denominato **AzInfoProtection** che è stato creato eseguendo il cmdlet Install-AIPScanner durante l'installazione dello scanner Azure Information Protection. 

- I report dello scanner presenti in %*localappdata*%\Microsoft\MSIP\Scanner\Reports.

- L'assegnazione del diritto utente di **accesso come servizio** per l'account di dominio per il computer locale.


## <a name="next-steps"></a>Passaggi successivi

Questa guida introduttiva include la configurazione minima, in modo da poter vedere rapidamente in che modo lo scanner può individuare le informazioni riservate in una condivisione di rete. Se si è pronti per installare lo scanner in un ambiente di produzione, vedere [Distribuzione dello scanner di Azure Information Protection per classificare e proteggere automaticamente i file](deploy-aip-scanner.md).

Se si vogliono classificare e proteggere i file contenenti informazioni riservate, è necessario configurare le etichette di Azure Information Protection per la classificazione automatica e la protezione:

- [Come configurare le condizioni per la classificazione automatica e consigliata per Azure Information Protection](configure-policy-classification.md)

- [Come configurare un'etichetta per la protezione di Rights Management](configure-policy-protection.md)