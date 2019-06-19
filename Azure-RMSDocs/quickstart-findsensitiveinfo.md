---
title: Avvio rapido - Trovare le informazioni riservate con lo scanner di Azure Information Protection
description: Usare lo scanner di Azure Information Protection per trovare le informazioni riservate presenti nei file archiviati in locale.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 06/18/2019
ms.topic: quickstart
ms.collection: M365-security-compliance
ms.service: information-protection
ms.openlocfilehash: 9678aeed589c1b4d9beee5f304ac9d8fdbd5cbf1
ms.sourcegitcommit: a26d033ccd557839b61736284456370393f3b52a
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2019
ms.locfileid: "67156707"
---
# <a name="quickstart-find-what-sensitive-information-you-have-in-files-stored-on-premises"></a>Guida introduttiva: Trovare le informazioni riservate presenti nei file archiviati in locale

>*Si applica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*
>
> *Istruzioni per: [Client Azure Information Protection per Windows](faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*

In questa guida introduttiva verrà installato e configurato lo scanner di Azure Information Protection per trovare le informazioni riservate presenti nei file archiviati in un archivio dati locale, ad esempio una cartella locale, una condivisione di rete o SharePoint Server.

Nota: in questa guida di avvio rapido viene usata la versione disponibile a livello generale corrente dello scanner che usa il portale di Azure per la configurazione al posto dei cmdlet di PowerShell usati nelle versioni precedenti.

È possibile completare questa configurazione in meno di 10 minuti.

## <a name="prerequisites"></a>Prerequisiti

Per completare questa guida introduttiva, è necessario:

1. Disporre di una sottoscrizione che includa un piano 1 o 2 di Azure Information Protection.
    
    In assenza di una di queste sottoscrizioni, è possibile creare un account [gratuito](https://admin.microsoft.com/Signup/Signup.aspx?OfferId=87dd2714-d452-48a0-a809-d2f58c4f68b7) per l'organizzazione.

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

## <a name="configure-a-profile-for-the-scanner"></a>Configurare un profilo per lo scanner

Prima di installare lo scanner, creare un profilo per lo scanner nel portale di Azure. Questo profilo contiene le impostazioni dello scanner e le posizioni dei repository di dati da analizzare.

1. Aprire una nuova finestra del browser e [accedere al portale di Azure](configure-policy.md#signing-in-to-the-azure-portal). Quindi passare al pannello **Azure Information Protection**. 
    
    Ad esempio, dal menu hub fare clic su **Tutti i servizi** e iniziare a digitare **Informazioni** nella casella Filtro. Selezionare **Azure Information Protection**.
    
2. Individuare le opzioni del menu **Scanner** e selezionare **Profili**.

3. Nel pannello **Azure Information Protection - Profili** selezionare **Aggiungi**:
    
    ![Aggiungere il profilo per lo scanner di Azure Information Protection](./media/scanner-add-profile.png)

4. Nel pannello **Aggiungi un nuovo profilo** specificare un nome per lo scanner, usato per identificare le impostazioni di configurazione e i repository di dati da analizzare corrispondenti. Ad esempio, per questa guida di avvio rapido è possibile specificare **Avvio rapido**. Quando in un secondo momento si installa lo scanner, sarà necessario specificare lo stesso nome di profilo.
    
    Facoltativamente, specificare una descrizione per scopi amministrativi, per facilitare l'identificazione del nome di profilo dello scanner.

5. Per questa guida di avvio rapido selezionare una sola impostazione: Per **Applicazione dei criteri**, selezionare **No**. Selezionare quindi **Salva**, ma non chiudere il pannello.
    
    Le impostazioni configurano lo scanner per eseguire un'individuazione una tantum di tutti i file nei repository di dati specificati. Questa analisi individua tutti i tipi noti di informazioni riservate e non richiede la configurazione preliminare delle etichette o delle impostazioni dei criteri di Azure Information Protection.

6. Dopo aver creato e salvato il profilo, si è pronti per tornare all'opzione **Configura i repository** e specificare la cartella locale come archivio dati da analizzare.
    
    Sempre nel pannello **Aggiungi un nuovo profilo** selezionare **Configura repository** per aprire il pannello **Repository**:
    
    ![Configurare i repository di dati per lo scanner di Azure Information Protection](./media/scanner-repositories-bar.png)

7. Nel pannello **Repository** selezionare **Aggiungi**:
    
    ![Aggiungere il repository di dati per lo scanner di Azure Information Protection](./media/scanner-repository-add.png)

8. Nel pannello **Repository** specificare la cartella locale creata nel primo passaggio, ad esempio `C:\TestScanner`
    
    Non modificare le altre impostazioni in questo pannello, ma mantenere **Impostazione predefinita del profilo**. Questo significa che il repository dei dati eredita le impostazioni dal profilo dello scanner. 
    
    Selezionare **Salva**.

9. È ora possibile chiudere il pannello **Aggiungi un nuovo profilo**. Verrà visualizzato il nome del profilo nel pannello **Azure Information Protection - Profili** insieme alla colonna **PIANIFICAZIONE** con l'impostazione **Manuale** e la colonna **IMPONI** vuota.

A questo punto si è pronti per installare lo scanner con il profilo di scanner appena creato.

## <a name="install-the-scanner"></a>Installare lo scanner

1. Aprire una sessione di PowerShell con l'opzione **Esegui come amministratore**.

2. Usare il comando seguente per installare lo scanner, specificando il nome del proprio computer e il nome del profilo che è stato salvato nel portale di Azure:
    
        Install-AIPScanner -SqlServerInstance <your computer name>\SQLEXPRESS -Profile <profile name>
    
    Quando richiesto, fornire le proprie credenziali per lo scanner usando il formato \<dominio\nome utente> e quindi specificare la password. 

## <a name="start-the-scan-and-confirm-it-finished"></a>Avviare l'analisi e confermarne il completamento

1. Nel portale di Azure tornare ad Azure Information Protection per avviare lo scanner. Dall'opzione di menu **Scanner** selezionare **Nodi**. Selezionare il nome del computer, quindi l'opzione **Avvia analisi**:
    
    ![Avviare l'analisi per lo scanner di Azure Information Protection](./media/scanner-scan-now.png)

2. È presente solo un file di piccole dimensioni da controllare, quindi questa analisi di test iniziale sarà molto rapida:
    
    - Nel pannello **Azure Information Protection - Nodi** il valore della colonna **STATO** passa da **Analisi in corso** a **Inattivo**.
    
    - In alternativa controllare il log eventi locale **Applicazioni e servizi** di Windows, **Azure Information Protection**. Verificare l'ID evento informativo **911** per il processo **MSIP.Scanner**. La voce del log eventi include anche un riepilogo dei risultati dell'analisi.

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

2. Riavviare lo scanner: Dall'opzione di menu **Scanner** selezionare **Nodi**, il nome del computer e quindi **Avvia analisi**:
    
    ![Avviare l'analisi per lo scanner di Azure Information Protection](./media/scanner-scan-now.png)

3. Visualizzare i nuovi risultati al termine dell'analisi. 
    
    La durata dell'analisi dipende dal numero di file presenti nell'archivio dati, dalla loro dimensione e dal tipo di file. 

## <a name="clean-up-resources"></a>Pulizia delle risorse

In un ambiente di produzione lo scanner viene eseguito in Windows Server, usando un account del servizio che esegue automaticamente l'autenticazione al servizio Azure Information Protection. È anche possibile usare una versione di livello aziendale di SQL Server e specificare diversi repository dei dati. 

Per pulire le risorse, in preparazione alla distribuzione di produzione, nella sessione di PowerShell eseguire il comando seguente per disinstallare lo scanner:

    Uninstall-AIPScanner

Riavviare quindi il computer.

Questo comando non rimuove gli elementi seguenti, che è pertanto necessario rimuovere manualmente se non si vuole conservarli dopo questa guida introduttiva:

- Il database SQL Server denominato **AIPScanner_\<profile>** che è stato creato eseguendo il cmdlet Install-AIPScanner durante l'installazione dello scanner Azure Information Protection. 

- I report dello scanner presenti in %*localappdata*%\Microsoft\MSIP\Scanner\Reports.

- L'assegnazione del diritto utente di **accesso come servizio** per l'account di dominio per il computer locale.


## <a name="next-steps"></a>Passaggi successivi

Questa guida introduttiva include la configurazione minima, in modo da poter vedere rapidamente in che modo lo scanner può individuare le informazioni riservate in una condivisione di rete. Se si è pronti per installare lo scanner in un ambiente di produzione, vedere [Distribuzione dello scanner di Azure Information Protection per classificare e proteggere automaticamente i file](deploy-aip-scanner.md).

Se si vogliono classificare e proteggere i file contenenti informazioni riservate, è necessario configurare le etichette di Azure Information Protection per la classificazione automatica e la protezione:

- [Come configurare le condizioni per la classificazione automatica e consigliata per Azure Information Protection](configure-policy-classification.md)

- [Come configurare un'etichetta per la protezione di Rights Management](configure-policy-protection.md)
