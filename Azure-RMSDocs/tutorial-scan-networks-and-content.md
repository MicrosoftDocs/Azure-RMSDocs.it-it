---
title: Esercitazione - Individuazione del contenuto sensibile con lo scanner di Azure Information Protection (AIP)
description: Usare lo scanner di Azure Information Protection (AIP) per individuare i repository che potrebbero essere rischiosi. Eseguire quindi il drill-down per analizzare tali condivisioni file alla ricerca di eventuale contenuto sensibile.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 11/09/2020
ms.topic: tutorial
ms.collection: M365-security-compliance
ms.service: information-protection
ms.custom: admin
ms.subservice: aiplabels
ms.openlocfilehash: e3b8c14c63c3ac6300c84349212db0e177a0dd7d
ms.sourcegitcommit: e8e4ca39278f1557e14cc8586fe357d8ebce2072
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/15/2021
ms.locfileid: "98240887"
---
# <a name="tutorial-discovering-your-sensitive-content-with-the-azure-information-protection-aip-scanner"></a>Esercitazione: Individuazione del contenuto sensibile con lo scanner di Azure Information Protection (AIP)

>***Si applica a**: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*
>
> ***Rilevante per**: [Client di etichettatura unificata di Azure Information Protection per Windows](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

Il client di Azure Information Protection include uno scanner locale che consente agli amministratori di sistema di analizzare i repository di file locali per individuare eventuale contenuto sensibile. 

In questa esercitazione si apprenderà come:

> [!div class="checklist"]
> * Creare un processo di analisi di rete per cercare i repository rischiosi
> * Aggiungere eventuali repository rischiosi trovati a un processo di analisi dei contenuti
> * Analizzare le condivisioni di contenuto per individuare eventuale contenuto sensibile e comprendere i risultati trovati

> [!NOTE]
> Il servizio di individuazione della rete è disponibile solo a partire dalla versione [2.8.85.0](rms-client/unifiedlabelingclient-version-release-history.md#version-28850) del client di etichettatura unificata ed è attualmente in ANTEPRIMA. Le [condizioni aggiuntive per l'anteprima di Azure](https://azure.microsoft.com/support/legal/preview-supplemental-terms/) includono termini legali aggiuntivi che si applicano a funzionalità di Azure in versione beta, anteprima o diversamente non ancora disponibili a livello generale.
>
> Se questa versione del client e dello scanner non è installata, controllare i [prerequisiti dell'esercitazione](#tutorial-prerequisites) e quindi passare direttamente a [Definire ed eseguire il processo di analisi dei contenuti](#define-and-run-your-content-scan-job).


**Tempo necessario**: è possibile completare questa configurazione in 15 minuti.

## <a name="tutorial-prerequisites"></a>Prerequisiti per l'esercitazione

|Requisito  |Descrizione  |
|---------|---------|
|**Una sottoscrizione di supporto**     |  Sarà necessaria una sottoscrizione di Azure che includa [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection/). <br /><br />In assenza di una di queste sottoscrizioni, è possibile creare un account [gratuito](https://admin.microsoft.com/Signup/Signup.aspx?OfferId=87dd2714-d452-48a0-a809-d2f58c4f68b7) per l'organizzazione.       |
|**Accesso amministrativo al portale di Azure** |Verificare che sia possibile accedere al [portale di Azure](https://portal.azure.com/) con un account amministratore supportato e che la protezione sia abilitata. Gli account amministratore supportati includono: <br /><br />- **Amministratore di conformità**<br />- **Amministratore dati di conformità**<br />- **Amministratore della sicurezza**<br />- **Amministratore globale**   |
|**Client e scanner di AIP e servizio di individuazione della rete**   |   Per completare questa esercitazione, è necessario aver installato il client e lo scanner di etichettatura unificata di Azure Information Protection, nonché il servizio di individuazione della rete (anteprima pubblica). <br /><br />Per altre informazioni, vedere: <br /><br />- [Avvio rapido: Distribuzione del client di etichettatura unificata di Azure Information Protection (AIP)](quickstart-deploy-client.md) <br />- [Esercitazione: Installazione dello scanner di etichettatura unificata di Azure Information Protection (AIP)](tutorial-install-scanner.md) |
|**Un processo di analisi dei contenuti** | Assicurarsi di avere a disposizione un processo di analisi dei contenuti di base che è possibile usare per i test. È possibile che ne sia stato creato uno al momento dell'[installazione dello scanner](tutorial-install-scanner.md).<br /><br />Se è necessario crearne uno ora, è possibile usare le istruzioni riportate in [Configurare Azure Information Protection nel portale di Azure](tutorial-install-scanner.md#configure-azure-information-protection-in-the-azure-portal). Quando è disponibile un processo di analisi dei contenuti di base, tornare qui per completare questa esercitazione. |
|**SQL Server**     | Per eseguire lo scanner, è necessario SQL Server installato nel computer dello scanner. <br /><br /> Per eseguire l'installazione, passare alla [pagina di download di SQL Server](https://www.microsoft.com/sql-server/sql-server-downloads) e selezionare **Scarica ora** per l'opzione di installazione desiderata. Nel programma di installazione selezionare il tipo di installazione **Basic**. <br /><br />**Nota**: Si consiglia di installare SQL Server Enterprise per gli ambienti di produzione ed Express solo per i test.    |
|**Account di Azure Active Directory**     |  Quando si lavora in un ambiente standard e connesso al cloud, l'account di dominio deve essere sincronizzato con [Azure Active Directory](https://azure.microsoft.com/services/active-directory/). Ciò non è necessario se si lavora offline. <br /><br />In caso di dubbi per il proprio account, contattare uno degli amministratori di sistema per verificare lo stato di sincronizzazione. Per altre informazioni, vedere [Distribuzione dello scanner con configurazioni alternative](deploy-aip-scanner-prereqs.md#deploying-the-scanner-with-alternative-configurations).  |
|**Etichette di riservatezza e criteri pubblicati** |È necessario avere creato etichette di riservatezza e aver pubblicato criteri con almeno un'etichetta nell'interfaccia di amministrazione dell'etichettatura per l'account del servizio scanner. <br /><br />Configurare le etichette di riservatezza nell'interfaccia di amministrazione dell'etichettatura, ovvero il Centro conformità di Microsoft 365, il Centro sicurezza Microsoft 365 o il Centro sicurezza e conformità di Microsoft 365. Per altre informazioni, vedere la [documentazione di Microsoft 365](/microsoft-365/compliance/create-sensitivity-labels). |
| | | 


Quando si è pronti, continuare con [Creare un processo di analisi della rete](#create-a-network-scan-job).

## <a name="create-a-network-scan-job"></a>Creare un processo di analisi della rete

Creare un processo di analisi della rete per analizzare un indirizzo IP o un intervallo IP specificato per individuare eventuali repository rischiosi.

> [!NOTE]
> Questa funzionalità è disponibile solo a partire dalla versione [2.8.85.0](rms-client/unifiedlabelingclient-version-release-history.md#version-28850) ed è attualmente in ANTEPRIMA. Le [condizioni aggiuntive per l'anteprima di Azure](https://azure.microsoft.com/support/legal/preview-supplemental-terms/) includono termini legali aggiuntivi che si applicano a funzionalità di Azure in versione beta, anteprima o diversamente non ancora disponibili a livello generale.
> 

**Per creare un processo di analisi della rete**:

1. Accedere al [portale di Azure](https://portal.azure.com/) come [amministratore supportato](#tutorial-prerequisites) e passare all'area **Azure Information Protection**.
        
1. Nel menu **Scanner** a sinistra selezionare :::image type="icon" source="media/qs-tutor/i-network-scan-jobs.png" border="false"::: **Processi di analisi della rete (anteprima)** .

1. Selezionare :::image type="icon" source="media/i-add.PNG" border="false"::: **Aggiungi** per aggiungere un nuovo processo. Nel riquadro **Aggiungi un nuovo processo di analisi della rete** immettere i dettagli seguenti:
    
    |Opzione  |Descrizione  |
    |---------|---------|
    |**Nome del processo di analisi della rete** e **Descrizione**     |Immettere un nome significativo, ad esempio `Quickstart` e una descrizione facoltativa.         |
    |**Selezionare il cluster**     | Selezionare il nome del cluster nell'elenco a discesa.<br /><br /> Ad esempio, se è stata completata l'[Esercitazione: Installazione dello scanner di etichettatura unificata di Azure Information Protection (AIP)](tutorial-install-scanner.md) e il cluster è ancora disponibile, selezionare **Avvio rapido**.       |
    |**Configura gli intervalli IP da individuare**     | Selezionare la riga per aprire il riquadro **Scegliere gli intervalli IP**. Immettere un indirizzo IP o un intervallo IP da analizzare. <br /><br />**Nota**: assicurarsi di immettere indirizzi IP accessibili dal computer dello scanner.      |
    |**Imposta la pianificazione**     | Mantenere il valore predefinito **Una sola volta**.        |
    |**Imposta l'ora di inizio (UTC)**     |  Calcolare l'ora UTC corrente, considerando il fuso orario corrente, e impostare l'ora di inizio in modo che l'esecuzione parta tra 5 minuti.     |
    |     |         |

    Ad esempio: 

    :::image type="content" source="media/qs-tutor/network-scan-job.png" alt-text="Immettere i dettagli per il processo di analisi della rete":::

1. Fare clic su :::image type="icon" source="media/qs-tutor/save-icon.png" border="false"::: **Salva** nella parte superiore della pagina.

1. Tornare alla griglia :::image type="icon" source="media/qs-tutor/i-network-scan-jobs.png" border="false"::: **Processi di analisi della rete (anteprima)** e attendere l'avvio dell'analisi.

I dati della griglia vengono aggiornati al termine dell'analisi. Ad esempio:

:::image type="content" source="media/qs-tutor/scanned-network.png" alt-text="Processi di analisi della rete aggiornati":::

> [!TIP]
> Se il processo di analisi della rete non viene eseguito, verificare che il [servizio di individuazione della rete sia installato correttamente](tutorial-install-scanner.md#install-the-network-discovery-service) nel computer dello scanner.

Continuare con [Aggiungere i repository rischiosi a un processo di analisi dei contenuti](#add-risky-repositories-to-a-content-scan-job).

## <a name="add-risky-repositories-to-a-content-scan-job"></a>Aggiungere i repository rischiosi a un processo di analisi dei contenuti

Al termine del processo di analisi della rete, è possibile verificare la presenza di repository rischiosi trovati. 

Ad esempio, se si trova un repository con accesso pubblico sia in lettura che in scrittura, è possibile eseguire un'analisi più approfondita e verificare che in tale posizione non siano archiviati dati sensibili.

> [!NOTE]
> Questa funzionalità è disponibile solo a partire dalla versione [2.8.85.0](rms-client/unifiedlabelingclient-version-release-history.md#version-28850) ed è attualmente in ANTEPRIMA. Le [condizioni aggiuntive per l'anteprima di Azure](https://azure.microsoft.com/support/legal/preview-supplemental-terms/) includono termini legali aggiuntivi che si applicano a funzionalità di Azure in versione beta, anteprima o diversamente non ancora disponibili a livello generale.
> 

**Per aggiungere repository rischiosi al processo di analisi dei contenuti**:

1. Accedere al [portale di Azure](https://portal.azure.com/) come [amministratore supportato](#tutorial-prerequisites) e passare al riquadro **Azure Information Protection**.
        
1. Nel menu **Scanner** a sinistra selezionare :::image type="icon" source="media/qs-tutor/i-repos.png" border="false"::: **Repository (anteprima)** .

    :::image type="content" source="media/small/risky-repos-small.png" alt-text="Visualizzare i repository trovati dal processo di analisi della rete" lightbox="media/qs-tutor/risky-repos.png":::

1. Nella griglia sotto i grafici individuare un repository non ancora gestito dallo scanner. Non gestito dallo scanner significa non incluso in un processo di analisi dei contenuti e non analizzato per l'individuazione di eventuale contenuto sensibile.

    > [!TIP]
    > Ad esempio, i repository con **Accesso pubblico effettivo** di tipo **L** (lettura) o **LS** (lettura/scrittura) sono disponibili per il pubblico e potrebbero includere contenuto sensibile a rischio.
    > 

1. Selezionare la riga e quindi sopra la griglia selezionare :::image type="icon" source="media/i-add.PNG" border="false"::: **Assegna gli elementi selezionati**. 

1. Nel riquadro **Assegna al processo di analisi dei contenuti** visualizzato a destra selezionare il processo di analisi dei contenuti nell'elenco a discesa e quindi selezionare :::image type="icon" source="media/qs-tutor/save-icon.png" border="false"::: **Salva**.

    Ad esempio:

    :::image type="content" source="media/qs-tutor/assign-content-scan-job.png" alt-text="Assegnare un repository rischioso a un processo di analisi dei contenuti":::

Alla successiva esecuzione del processo di analisi dei contenuti verrà incluso il repository appena individuato e verrà identificato, etichettato, classificato e protetto l'eventuale contenuto sensibile trovato, in base a quanto configurato nei criteri.

Continuare con [Definire ed eseguire il processo di analisi dei contenuti](#define-and-run-your-content-scan-job).

## <a name="define-and-run-your-content-scan-job"></a>Definire ed eseguire il processo di analisi dei contenuti

Usare il processo di analisi dei contenuti preparato con i [prerequisiti dell'esercitazione](#tutorial-prerequisites) per analizzare il contenuto. 

Se non è ancora disponibile un processo di analisi dei contenuti, eseguire [Configurare le impostazioni iniziali nel portale di Azure](tutorial-install-scanner.md#configure-initial-scanner-settings-in-the-azure-portal) e quindi tornare qui per continuare.


1. Accedere al [portale di Azure](https://portal.azure.com/) come [amministratore supportato](#tutorial-prerequisites) e passare al riquadro **Azure Information Protection**.
        
1. Nel menu **Scanner** a sinistra, selezionare :::image type="icon" source="media/i-content-scan-jobs.png" border="false"::: **Processi di analisi dei contenuti** e quindi selezionare il processo di analisi dei contenuti.
 
1. Modificare le impostazioni del processo di analisi dei contenuti, assicurandosi di specificare un nome significativo e una descrizione facoltativa. 

    Mantenere i valori predefiniti per la maggior parte delle impostazioni, ad eccezione delle modifiche seguenti:

    -  **Gestisci l'etichettatura consigliata come automatica**. Impostare su **Sì**.
    
    - **Configura i repository**. Assicurarsi che sia presente almeno un repository definito. 
    
        > [!TIP]
        > Se sono stati aggiunti repository aggiuntivi al processo di analisi dei contenuti dopo aver analizzato la rete in [Aggiungere i repository rischiosi a un processo di analisi dei contenuti](#add-risky-repositories-to-a-content-scan-job), è possibile selezionarli per visualizzarli qui. 

    - **Imponi**. Impostare su **Sì**.
    
1. Selezionare :::image type="icon" source="media/qs-tutor/save-icon.png" border="false"::: **Salva** e quindi tornare alla griglia :::image type="icon" source="media/i-content-scan-jobs.PNG" border="false"::: **Processi di analisi dei contenuti**.

1. Per analizzare il contenuto, tornare all'area :::image type="icon" source="media/i-content-scan-jobs.png" border="false"::: **Processi di analisi dei contenuti** e selezionare il processo di analisi dei contenuti.

    Nella barra degli strumenti sopra la griglia selezionare :::image type="icon" source="media/i-scan-now.PNG" border="false"::: **Avvia analisi** per avviare l'analisi.

    Al termine dell'analisi, continuare con [Visualizzare i risultati dell'analisi](#view-scan-results).

### <a name="view-scan-results"></a>Visualizzare i risultati dell'analisi

Dopo aver completato l'analisi, controllare i report nell'area **Azure Information Protection > Analisi** nel portale di Azure.

Ad esempio:

:::image type="content" source="media/qs-tutor/content-scan-job-data-discovery.PNG" alt-text="Risultati dello scanner - Report di individuazione dei dati di analisi":::
    
> [!TIP]
> Se i risultati sono vuoti e si vuole eseguire un'analisi significativa, creare un file denominato **Info di pagamento** in uno dei repository inclusi nel processo di analisi dei contenuti. Salvare il file con il contenuto seguente:
> 
> **Carta di credito**: 2384 2328 5436 3489
>
> Eseguire di nuovo l'analisi per visualizzare la differenza nei risultati.
> 

Per altre informazioni, vedere [Reporting centralizzato per Azure Information Protection (anteprima pubblica)](reports-aip.md)

#### <a name="local-scanner-reports"></a>Report dello scanner locali

I log vengono anche archiviati in locale nella **directory %localappdata%\Microsoft\MSIP\Scanner\Reports** nel computer dello scanner e includono:

|Tipo  |Descrizione  |
|---------|---------|
|**File di riepilogo con estensione txt**     |  Includono il tempo impiegato per l'analisi, il numero di file analizzati e il numero di file con una corrispondenza per i tipi di informazioni.       |
|**File di dettaglio con estensione csv**     | Contengono descrizioni dettagliate per ogni file analizzato. La directory può contenere fino a 60 report per ogni ciclo di analisi.         |
|     |         |

## <a name="next-steps"></a>Passaggi successivi

Per altre esercitazioni, vedere:

- [Esercitazione: Prevenzione dell'oversharing con Azure Information Protection (AIP)](tutorial-preventing-oversharing.md)
- [Esercitazione: Migrazione dal client classico al client di etichettatura unificata di Azure Information Protection (AIP)](tutorial-migrating-to-ul.md)

**Vedere anche**:

- [Informazioni sullo scanner di etichettatura unificata di Azure Information Protection](deploy-aip-scanner.md)
- [Prerequisiti per l'installazione e la distribuzione dello scanner di etichettatura unificata di Azure Information Protection](deploy-aip-scanner-prereqs.md)
- [Configurazione e installazione dello scanner di etichettatura unificata di Azure Information Protection](deploy-aip-scanner-configure-install.md)
- [Esecuzione dello scanner di Azure Information Protection](deploy-aip-scanner-manage.md)