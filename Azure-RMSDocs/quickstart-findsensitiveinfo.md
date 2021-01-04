---
title: Avvio rapido - Trovare le informazioni riservate con lo scanner di Azure Information Protection
description: Usare lo scanner di Azure Information Protection per trovare le informazioni riservate presenti nei file archiviati in locale.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 11/10/2020
ms.topic: quickstart
ms.collection: M365-security-compliance
ms.service: information-protection
ROBOTS: NOINDEX
ms.custom: admin
ms.subservice: aiplabels
ms.openlocfilehash: f57d8722cc1e42c196253a76f7338cd2a8e6c700
ms.sourcegitcommit: b32c16e41ba36167b5a3058b56a73183bdd4306d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/29/2020
ms.locfileid: "97807009"
---
# <a name="quickstart-find-what-sensitive-information-you-have-in-files-stored-on-premises"></a>Guida introduttiva: Trovare le informazioni riservate presenti nei file archiviati in locale

>***Si applica a**: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*
>
> ***Rilevante per**: [Client classico Azure Information Protection per Windows](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

>[!NOTE]
> Per offrire un'esperienza per i clienti unificata e semplificata, il **client classico di Azure Information Protection** e **Gestione etichette** nel portale di Azure saranno **deprecati** a partire dal **31 marzo 2021**. In questo intervallo di tempo tutti i clienti correnti di Azure Information Protection possono passare alla soluzione di etichettatura unificata usando la piattaforma di etichettatura unificata di Microsoft Information Protection. Altre informazioni nell'[avviso ufficiale sulla deprecazione](https://aka.ms/aipclassicsunset).

In questo avvio rapido si abilita SharePoint per consentire la scansione e si installa e si configura lo scanner di Azure Information Protection per trovare le informazioni riservate presenti in un archivio dati locale.

**Tempo necessario**: È possibile completare questa configurazione in meno di 15 minuti.

## <a name="prerequisites"></a>Prerequisiti

Per completare l'esercitazione introduttiva, sono necessari gli elementi seguenti:

|Requisito  |Descrizione  |
|---------|---------|
|**Una sottoscrizione di supporto**     |  Sarà necessaria una sottoscrizione che includa [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection/). </br></br>In assenza di una di queste sottoscrizioni, è possibile creare un account [gratuito](https://admin.microsoft.com/Signup/Signup.aspx?OfferId=87dd2714-d452-48a0-a809-d2f58c4f68b7) per l'organizzazione.       |
|**Client installato**    |   È necessario il client classico o il client di etichettatura unificata installato nel computer. </br></br>- Per installare il client di etichettatura unificata, passare all'[Area download Microsoft](https://www.microsoft.com/download/details.aspx?id=53018) e scaricare **AzInfoProtection_UL.exe** dalla pagina di Azure Information Protection. </br>- Per distribuire il client classico AIP, aprire un ticket di supporto per ottenere l'accesso al download.       |
|**SQL Server Express**     | È necessario avere installato SQL Server Express nel computer. </br></br> Per eseguire l'installazione, accedere all'[Area download Microsoft](https://www.microsoft.com/sql-server/sql-server-editions-express) e selezionare **Scarica ora** nell'opzione Express. Nel programma di installazione selezionare il tipo di installazione **Basic**.        |
|**Azure AD**     |  L'account di dominio deve essere sincronizzato con Azure AD. </br></br>Se non si è certi del proprio account, contattare uno degli amministratori di sistema.      |
|**Accesso a SharePoint**     | Per abilitare un'analisi di SharePoint, sono necessari l'accesso e le autorizzazioni per i criteri di SharePoint. |
| | |

## <a name="prepare-a-test-folder-and-file"></a>Preparare una cartella e un file di test

Per un test iniziale per confermare il funzionamento dello scanner:

1. Creare una nuova cartella in una condivisione di rete accessibile. Ad esempio, denominare questa cartella **TestScanner**.

1. Creare e salvare un documento di Word in tale cartella, con il testo **Credit card: 4242-4242-4242-4242**.

## <a name="permission-users-to-scan-sharepoint-repositories"></a>Consentire agli utenti di analizzare i repository SharePoint

Per usare lo scanner nei repository SharePoint, specificare l'URL del sito in modo che Azure Information Protection individui e analizzi tutti i siti corrispondenti all'URL.

Per abilitare le analisi tra i repository, aggiungere le seguenti autorizzazioni SharePoint per l'utente da usare per l'analisi:

1. Aprire SharePoint e selezionare **Criteri di autorizzazione** e selezionare **Aggiungi livello di criteri di autorizzazione**.

    ![Creare un nuovo livello di criteri di autorizzazione per un utente specifico](./media/aip-quick-set-sp-permissions.png)

1. In **Autorizzazioni raccolta siti** selezionare l'opzione **Controllore raccolta siti**.

1. In **Autorizzazione** selezionare **Concedi** per l'opzione **Visualizzazione pagine applicazione** e scegliere **Salva** per salvare le modifiche.  

    ![Selezionare Controllore raccolta siti e le opzioni delle autorizzazioni per un utente specifico](./media/aip-quick-set-site-permissions.png)

1. Dopo aver confermato le modifiche fare clic su **OK** nel messaggio **Criteri per l'applicazione Web** che viene visualizzato.

1. Nella pagina **Aggiungi utenti** aggiungere l'utente che si vuole usare per l'analisi nel campo **Scegli utenti**. In **Selezione autorizzazioni** selezionare l'opzione **Raccolta siti** e fare clic su **Fine** per applicare le autorizzazioni create all'utente aggiunto o selezionato.

    ![Aggiungere l'utente alle nuove opzioni di autorizzazioni](./media/aip-quick-set-user-permissions.png)

## <a name="configure-a-profile-for-the-scanner"></a>Configurare un profilo per lo scanner

Prima di installare lo scanner, creare un profilo per lo scanner nel portale di Azure. Questo profilo contiene le impostazioni dello scanner e le posizioni dei repository di dati da analizzare.

1. Aprire una nuova finestra del browser e [accedere al portale di Azure](configure-policy.md#signing-in-to-the-azure-portal). Quindi passare al riquadro **Azure Information Protection**.

    Ad esempio, nella casella di ricerca di risorse, servizi e documentazione: iniziare a digitare **Informazioni** e selezionare **Azure Information Protection**.

1. Individuare le opzioni **Scanner** nel riquadro a sinistra e selezionare **Profili**.

1. Nel riquadro **Azure Information Protection - Profili** selezionare **Aggiungi**:

    :::image type="content" source="media/scanner-add-profile.png" alt-text="Aggiungere il profilo per lo scanner di Azure Information Protection":::

1. Nel riquadro **Aggiungi un nuovo profilo** specificare un nome per lo scanner, usato per identificarne le impostazioni di configurazione e i repository di dati da analizzare. Ad esempio, per questa guida di avvio rapido è possibile specificare **Avvio rapido**. Quando in un secondo momento si installa lo scanner, sarà necessario specificare lo stesso nome di profilo.

    Facoltativamente, specificare una descrizione per scopi amministrativi, per facilitare l'identificazione del nome di profilo dello scanner.

1. Individuare la sezione **Applicazione dei criteri** in cui, per questo avvio rapido, selezionare solo un'impostazione: In **Applica** selezionare **Disattivato**. Selezionare quindi **Salva**, ma non chiudere il riquadro.

    Le impostazioni configurano lo scanner per eseguire un'individuazione una tantum di tutti i file nei repository di dati specificati. Questa analisi individua tutti i tipi noti di informazioni riservate e non richiede la configurazione preliminare delle etichette o delle impostazioni dei criteri di Azure Information Protection.

1. Dopo aver creato e salvato il profilo, si è pronti per tornare all'opzione **Configura i repository** e specificare la cartella di rete come archivio dati da analizzare.

    Sempre nel riquadro **Aggiungi un nuovo profilo** selezionare **Configura i repository** per aprire il riquadro **Repository**:

    :::image type="content" source="./media/scanner-repositories-bar.png" alt-text="Configurare i repository di dati per lo scanner di Azure Information Protection":::

1. Nel riquadro **Repository** selezionare **Aggiungi**:

    :::image type="content" source="media/scanner-repository-add.png" alt-text="Aggiungere il repository di dati per lo scanner di Azure Information Protection":::

1. Nel riquadro **Repository** specificare la cartella creata in precedenza, ad esempio `\\server\TestScanner`

    Non modificare le impostazioni rimanenti in questo riquadro e mantenerle come **Impostazione predefinita del profilo** in modo che il repository dei dati erediti le impostazioni dal profilo dello scanner.

    Selezionare **Salva**.

1. Tornare al riquadro **Azure Information Protection - Profili**. Ora viene elencato il nome del profilo, con la colonna **PIANIFICA** che indica **Manuale** e la colonna **APPLICA** vuota.

    Nella colonna **NODI** viene visualizzato **0** perché non è stato ancora installato lo scanner per questo profilo.

A questo punto si è pronti per installare lo scanner con il profilo di scanner creato.

## <a name="install-the-scanner"></a>Installare lo scanner

1. Aprire una sessione di PowerShell con l'opzione **Esegui come amministratore**.

1. Usare il comando seguente per installare lo scanner, specificando il nome della condivisione di rete e il nome del profilo che è stato salvato nel portale di Azure:

    ```ps
    Install-AIPScanner -SqlServerInstance <your network share name>\SQLEXPRESS -Profile <profile name>
    ```

    Quando richiesto, fornire le proprie credenziali per lo scanner usando il formato \<domain\user name> e quindi specificare la password.

## <a name="start-the-scan-and-confirm-it-finished"></a>Avviare l'analisi e confermarne il completamento

1. Tornare al portale di Azure e aggiornare il riquadro **Azure Information Protection - Profili**. Ora la colonna **NODI** visualizza **1**.

1. Selezionare il nome del profilo e quindi l'opzione **Avvia analisi**:

    :::image type="content" source="media/scanner-scan-now.png" alt-text="Avviare l'analisi per lo scanner di Azure Information Protection":::

    Se questa opzione non è disponibile dopo aver selezionato il profilo, lo scanner non è connesso a Azure Information Protection. Verificare la configurazione e la connettività Internet.

1. È presente solo un file di piccole dimensioni da controllare, quindi questa analisi di test iniziale sarà rapida:

    Attendere fino a quando non sono visualizzati i valori per le colonne **RISULTATI DELL'ULTIMA ANALISI** e **ULTIMA ANALISI (ORA DI FINE)** .

> [!TIP]
> In alternativa, solo per lo scanner del client classico:
>
> Controllare il registro eventi locale **Applicazioni e servizi** di Windows, **Azure Information Protection**. Verificare l'ID evento informativo **911** per il processo **MSIP.Scanner**. La voce del log eventi include anche un riepilogo dei risultati dell'analisi.
>
## <a name="see-detailed-results"></a>Visualizzare i risultati dettagliati

In Esplora file individuare i report dello scanner in **%*localappdata*%\Microsoft\MSIP\Scanner\Reports**. Aprire il file di report dettagliato in formato **CSV**.

In Excel:

- le prime due colonne visualizzano il repository dell'archivio dati e il nome file.
- Durante l'analisi, si noterà una colonna denominata **Information Type Name** (Nome tipo di informazioni), che è quella di maggiore interesse.

    Per il test iniziale, viene visualizzato il **numero di carta di credito**, uno dei diversi tipi di informazioni riservate che lo scanner può rilevare.

## <a name="scan-your-own-data"></a>Analizzare i dati personali

1. Modificare il profilo dello scanner e aggiungere un nuovo repository di dati, questa volta specificando il proprio archivio dati locale da analizzare per trovare le informazioni riservate.

    Specificare una condivisione di rete (percorso UNC) o un URL di SharePoint Server per un sito o una raccolta di SharePoint.

    Ad esempio:

    - **Per una condivisione di rete**: `\\NAS\HR`
    - **Per una cartella di SharePoint**: `http://sp2016/Shared Documents`

1. Riavviare di nuovo lo scanner.

    nel riquadro **Azure Information Protection - Profili** verificare che il profilo sia selezionato e quindi selezionare l'opzione **Avvia analisi**:

    :::image type="content" source="media/scanner-scan-now.png" alt-text="Avviare l'analisi per lo scanner di Azure Information Protection":::

1. Visualizzare i nuovi risultati al termine dell'analisi.

    La durata dell'analisi dipende dal numero di file presenti nell'archivio dati, dalla loro dimensione e dal tipo di file.

## <a name="clean-up-resources"></a>Pulizia delle risorse

In un ambiente di produzione lo scanner viene eseguito in Windows Server, usando un account del servizio che esegue automaticamente l'autenticazione al servizio Azure Information Protection. È anche possibile usare una versione di livello aziendale di SQL Server e specificare diversi repository dei dati.

Per pulire le risorse e preparare il sistema per una distribuzione di produzione, nella sessione di PowerShell eseguire il comando seguente per disinstallare lo scanner:

```ps
Uninstall-AIPScanner
```

Riavviare quindi il computer.

Questo comando non rimuove gli elementi seguenti, che è pertanto necessario rimuovere manualmente se non si vuole conservarli dopo questa guida introduttiva:

- Il database di SQL Server creato eseguendo il cmdlet Install-AIPScanner durante l'installazione dello strumento di analisi di Azure Information Protection: **AIPScanner_\<profile>**

- I report dello scanner presenti in **%*localappdata*%\Microsoft\MSIP\Scanner\Reports**.

- L'assegnazione del diritto utente di **accesso come servizio** per l'account di dominio per il computer locale.

## <a name="next-steps"></a>Passaggi successivi

Questo avvio rapido include la configurazione minima, in modo da poter vedere rapidamente in che modo lo scanner può individuare le informazioni riservate in archivi dati locali. Se si è pronti per installare lo scanner in un ambiente di produzione, vedere [Distribuzione dello scanner di Azure Information Protection per classificare e proteggere automaticamente i file](deploy-aip-scanner.md).

Se si vogliono classificare e proteggere i file contenenti informazioni sensibili, è necessario configurare le etichette per la classificazione automatica e la protezione:

- [Come configurare le condizioni per la classificazione automatica e consigliata per Azure Information Protection](configure-policy-classification.md)
- [Come configurare un'etichetta per la protezione di Rights Management](configure-policy-protection.md)
