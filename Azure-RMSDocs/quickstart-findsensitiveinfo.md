---
title: Avvio rapido - Trovare le informazioni riservate con lo scanner di Azure Information Protection
description: Usare lo scanner di Azure Information Protection per trovare le informazioni riservate presenti nei file archiviati in locale.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 11/01/2019
ms.topic: quickstart
ms.collection: M365-security-compliance
ms.service: information-protection
ms.custom: admin
ms.subservice: aiplabels
ms.openlocfilehash: c00aebd2af57dfbb7d9897d200ef3601ebf26ed3
ms.sourcegitcommit: f5d8cf4440a35afaa1ff1a58b2a022740ed85ffd
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/04/2019
ms.locfileid: "73559942"
---
# <a name="quickstart-find-what-sensitive-information-you-have-in-files-stored-on-premises"></a>Guida introduttiva: Trovare le informazioni riservate presenti nei file archiviati in locale

>*Si applica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*

In questa guida introduttiva verrà installato e configurato lo scanner di Azure Information Protection per trovare le informazioni riservate presenti nei file archiviati in un archivio dati locale, ad esempio una cartella locale, una condivisione di rete o SharePoint Server.

> [!NOTE]
> È possibile usare questa guida di avvio rapido con la versione disponibile a livello generale corrente del client Azure Information Protection (classico) o la versione disponibile a livello generale corrente del client di etichettatura unificata di Azure Information Protection che include una versione di anteprima dello scanner.
>  
> Non si è certi della differenza tra questi client? Vedere queste [domande frequenti](faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client).

È possibile completare questa configurazione in meno di 10 minuti.

## <a name="prerequisites"></a>Prerequisiti

Per completare questa guida introduttiva, è necessario:

1. Disporre di una sottoscrizione che includa un piano 1 o 2 di Azure Information Protection.
    
    In assenza di una di queste sottoscrizioni, è possibile creare un account [gratuito](https://admin.microsoft.com/Signup/Signup.aspx?OfferId=87dd2714-d452-48a0-a809-d2f58c4f68b7) per l'organizzazione.

2. Nel computer è installato uno dei client di Azure Information Protection seguenti:
    
    - Client classico: Per installare questo client, passare all'[Area download Microsoft](https://www.microsoft.com/en-us/download/details.aspx?id=53018) e scaricare **AzInfoProtection.exe** dalla pagina di Azure Information Protection.
    
    - Client per l'etichettatura unificata: Per installare il client, passare all'[Area download Microsoft](https://www.microsoft.com/en-us/download/details.aspx?id=53018) e scaricare **AzInfoProtection_UL_Preview.exe** dalla pagina di Azure Information Protection.
    
3. Aver installato anche SQL Server Express nel computer in uso.
    
    Se questa edizione di SQL Server non è già installata, è possibile scaricarla dall'[Area download Microsoft](https://www.microsoft.com/en-us/sql-server/sql-server-editions-express) e selezionare un'installazione di base.

4. Aver sincronizzato l'account di dominio con Azure AD.

Per un elenco completo dei prerequisiti per l'uso di Azure Information Protection, vedere [Requisiti per Azure Information Protection](requirements.md).

## <a name="prepare-a-test-folder-and-file"></a>Preparare una cartella e un file di test

Per un test iniziale per confermare il funzionamento dello scanner:

1. Creare una cartella locale nel computer, ad esempio **TestScanner** nell'unità C locale.

2. Creare e salvare un documento di Word in tale cartella, con il testo **Credit card: 4242-4242-4242-4242**.

## <a name="configure-a-profile-for-the-scanner"></a>Configurare un profilo per lo scanner

Prima di installare lo scanner, creare un profilo per lo scanner nel portale di Azure. Questo profilo contiene le impostazioni dello scanner e le posizioni dei repository di dati da analizzare.

1. Aprire una nuova finestra del browser e [accedere al portale di Azure](configure-policy.md#signing-in-to-the-azure-portal). Quindi passare al riquadro **Azure Information Protection**. 
    
    Ad esempio, nella casella di ricerca di risorse, servizi e documentazione: iniziare a digitare **Informazioni** e selezionare **Azure Information Protection**.
    
2. Individuare le opzioni **Scanner** nel riquadro a sinistra e selezionare **Profili**.

3. Nel riquadro **Azure Information Protection - Profili** selezionare **Aggiungi**:
    
    ![Aggiungere il profilo per lo scanner di Azure Information Protection](./media/scanner-add-profile.png)

4. Nel riquadro **Aggiungi un nuovo profilo** specificare un nome per lo scanner, usato per identificarne le impostazioni di configurazione e i repository di dati da analizzare. Ad esempio, per questa guida di avvio rapido è possibile specificare **Avvio rapido**. Quando in un secondo momento si installa lo scanner, sarà necessario specificare lo stesso nome di profilo.
    
    Facoltativamente, specificare una descrizione per scopi amministrativi, per facilitare l'identificazione del nome di profilo dello scanner.

5. Individuare la sezione **Applicazione dei criteri** in cui, per questo avvio rapido, selezionare solo un'impostazione: In **Applica** selezionare **Disattivato**. Selezionare quindi **Salva**, ma non chiudere il riquadro.
    
    Le impostazioni configurano lo scanner per eseguire un'individuazione una tantum di tutti i file nei repository di dati specificati. Questa analisi individua tutti i tipi noti di informazioni riservate e non richiede la configurazione preliminare delle etichette o delle impostazioni dei criteri di Azure Information Protection.

6. Dopo aver creato e salvato il profilo, si è pronti per tornare all'opzione **Configura i repository** e specificare la cartella locale come archivio dati da analizzare.
    
    Sempre nel riquadro **Aggiungi un nuovo profilo** selezionare **Configura i repository** per aprire il riquadro **Repository**:
    
    ![Configurare i repository di dati per lo scanner di Azure Information Protection](./media/scanner-repositories-bar.png)

7. Nel riquadro **Repository** selezionare **Aggiungi**:
    
    ![Aggiungere il repository di dati per lo scanner di Azure Information Protection](./media/scanner-repository-add.png)

8. Nel riquadro **Repository** specificare la cartella locale creata nel primo passaggio, ad esempio `C:\TestScanner`
    
    Non modificare le altre impostazioni in questo riquadro, ma mantenere **Impostazione predefinita del profilo**. Questo significa che il repository dei dati eredita le impostazioni dal profilo dello scanner. 
    
    Selezionare **Salva**.

9. Tornare al riquadro **Azure Information Protection - Profili**. Ora viene elencato il nome del profilo, con la colonna **PIANIFICA** che indica **Manuale** e la colonna **APPLICA** vuota. 
    
    Nella colonna **NODI** viene visualizzato **0** perché non è stato ancora installato lo scanner per questo profilo.

A questo punto si è pronti per installare lo scanner con il profilo di scanner appena creato.

## <a name="install-the-scanner"></a>Installare lo scanner

1. Aprire una sessione di PowerShell con l'opzione **Esegui come amministratore**.

2. Usare il comando seguente per installare lo scanner, specificando il nome del proprio computer e il nome del profilo che è stato salvato nel portale di Azure:
    
        Install-AIPScanner -SqlServerInstance <your computer name>\SQLEXPRESS -Profile <profile name>
    
    Quando richiesto, fornire le proprie credenziali per lo scanner usando il formato \<dominio\nome utente> e quindi specificare la password. 

## <a name="start-the-scan-and-confirm-it-finished"></a>Avviare l'analisi e confermarne il completamento

1. Tornare al portale di Azure e aggiornare il riquadro **Azure Information Protection - Profili**. Ora la colonna **NODI** visualizza **1**.

2. Selezionare il nome del profilo e quindi l'opzione **Avvia analisi**:
    
    ![Avviare l'analisi per lo scanner di Azure Information Protection](./media/scanner-scan-now.png)
    
    Se questa opzione non è disponibile dopo aver selezionato il profilo, lo scanner non è connesso a Azure Information Protection. Verificare la configurazione e la connettività Internet.

3. È presente solo un file di piccole dimensioni da controllare, quindi questa analisi di test iniziale sarà molto rapida:
    
    Attendere fino a quando non sono visualizzati i valori per le colonne **RISULTATI DELL'ULTIMA ANALISI** e **ULTIMA ANALISI (ORA DI FINE)** .
    
    In alternativa, solo per lo scanner del client classico: Controllare il registro eventi locale **Applicazioni e servizi** di Windows, **Azure Information Protection**. Verificare l'ID evento informativo **911** per il processo **MSIP.Scanner**. La voce del log eventi include anche un riepilogo dei risultati dell'analisi.

## <a name="see-detailed-results"></a>Visualizzare i risultati dettagliati

In Esplora file individuare i report dello scanner in %*localappdata*%\Microsoft\MSIP\Scanner\Reports. Aprire il file di report dettagliato in formato CSV.

In Excel le prime due colonne visualizzano il repository dell'archivio dati e il nome file. Durante l'analisi, si noterà una colonna denominata **Information Type Name** (Nome tipo di informazioni), che è quella di maggiore interesse. Per il test iniziale, viene visualizzato il **numero di carta di credito**, uno dei diversi tipi di informazioni riservate che lo scanner può rilevare.

## <a name="scan-your-own-data"></a>Analizzare i dati personali

1. Modificare il profilo dello scanner e aggiungere un nuovo repository di dati, questa volta specificando il proprio archivio dati locale da analizzare per trovare le informazioni riservate.     
    È possibile specificare una cartella locale, una condivisione di rete (percorso UNC) o un URL di SharePoint Server per un sito o una raccolta di SharePoint. 
    
    - Esempio per una cartella locale:
        
            D:\Data\Finance
    
    - Esempio per una condivisione di rete:
        
            \\NAS\HR
    
    - Esempio per una cartella di SharePoint:
        
            http://sp2016/Shared Documents

2. Riavviare lo scanner: nel riquadro **Azure Information Protection - Profili** verificare che il profilo sia selezionato e quindi selezionare l'opzione **Avvia analisi**:
    
    ![Avviare l'analisi per lo scanner di Azure Information Protection](./media/scanner-scan-now.png)

3. Visualizzare i nuovi risultati al termine dell'analisi. 
    
    La durata dell'analisi dipende dal numero di file presenti nell'archivio dati, dalla loro dimensione e dal tipo di file. 

## <a name="clean-up-resources"></a>Pulizia delle risorse

In un ambiente di produzione lo scanner viene eseguito in Windows Server, usando un account del servizio che esegue automaticamente l'autenticazione al servizio Azure Information Protection. È anche possibile usare una versione di livello aziendale di SQL Server e specificare diversi repository dei dati. 

Per pulire le risorse, in preparazione alla distribuzione di produzione, nella sessione di PowerShell eseguire il comando seguente per disinstallare lo scanner:

    Uninstall-AIPScanner

Riavviare quindi il computer.

Questo comando non rimuove gli elementi seguenti, che è pertanto necessario rimuovere manualmente se non si vuole conservarli dopo questa guida introduttiva:

- Il database di SQL Server creato eseguendo il cmdlet Install-AIPScanner durante l'installazione dello strumento di analisi di Azure Information Protection:
    - Per il client classico: **AIPScanner_\<profilo>**
    - Per il client per l'etichettatura unificata: **AIPScannerUL_\<nome_profilo>**

- I report dello scanner presenti in %*localappdata*%\Microsoft\MSIP\Scanner\Reports.

- L'assegnazione del diritto utente di **accesso come servizio** per l'account di dominio per il computer locale.


## <a name="next-steps"></a>Passaggi successivi

Questo avvio rapido include la configurazione minima, in modo da poter vedere rapidamente in che modo lo scanner può individuare le informazioni riservate in archivi dati locali. Se si è pronti per installare lo scanner in un ambiente di produzione, vedere [Distribuzione dello scanner di Azure Information Protection per classificare e proteggere automaticamente i file](deploy-aip-scanner.md).

Se si vogliono classificare e proteggere i file contenenti informazioni sensibili, è necessario configurare le etichette per la classificazione automatica e la protezione:

- Per il client classico:
    - [Come configurare le condizioni per la classificazione automatica e consigliata per Azure Information Protection](configure-policy-classification.md)
    - [Come configurare un'etichetta per la protezione di Rights Management](configure-policy-protection.md)

- Per il client per l'etichettatura unificata:
    - [Applicare automaticamente un'etichetta di riservatezza al contenuto](https://docs.microsoft.com/microsoft-365/compliance/apply-sensitivity-label-automatically)
    - [Limitare l'accesso al contenuto usando la crittografia nelle etichette di riservatezza](https://docs.microsoft.com/microsoft-365/compliance/encryption-sensitivity-labels)
