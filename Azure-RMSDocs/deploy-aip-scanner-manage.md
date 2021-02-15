---
title: Esecuzione dello scanner Azure Information Protection Unified Labeling scanner (AIP)
description: Istruzioni per l'esecuzione del Azure Information Protection scanner unificato per l'assegnazione di etichette per individuare, classificare e proteggere i file negli archivi dati.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 02/01/2021
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: scanner
ms.reviewer: demizets
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 13484ad0301ec8d7404c4127ff78720df81d8eb5
ms.sourcegitcommit: caf2978ab03e4893b59175ce753791867793dcfe
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/15/2021
ms.locfileid: "100524779"
---
# <a name="running-the-azure-information-protection-scanner"></a>Esecuzione dello scanner di Azure Information Protection

>***Si applica a**: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2 *
>
>***Pertinente per**: [AIP Unified Labeling client only](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients). Per lo scanner classico, vedere [esecuzione dello scanner classico Azure Information Protection](deploy-aip-scanner-manage-classic.md). *

Dopo aver verificato i [requisiti di sistema](deploy-aip-scanner-prereqs.md) e [configurato e installato lo scanner](deploy-aip-scanner-configure-install.md), [eseguire un'analisi di individuazione](#run-a-discovery-cycle-and-view-reports-for-the-scanner) per iniziare.

Per gestire le analisi in avanti, attenersi alla procedura descritta di seguito.

- [Arrestare un'analisi](#stopping-a-scan)
- [Ripetizione dell'analisi dei file](#rescanning-files)

Per ulteriori informazioni, vedere [Deploying the Azure Information Protection scanner to classificare e proteggere automaticamente i file](deploy-aip-scanner.md).

## <a name="run-a-discovery-cycle-and-view-reports-for-the-scanner"></a>Eseguire un ciclo di individuazione e visualizzare i report per lo scanner

Usare la procedura seguente dopo aver [configurato e installato lo scanner](deploy-aip-scanner-configure-install.md) per ottenere una conoscenza iniziale del contenuto.

Eseguire di nuovo questi passaggi in base alle esigenze quando il contenuto cambia.

1. Nella portale di Azure, nel riquadro **processi di analisi Azure Information Protection-contenuto** selezionare i processi di analisi del contenuto, quindi selezionare l'opzione **Analizza ora** :

    ![Avviare l'analisi per lo scanner di Azure Information Protection](./media/scanner-scan-now.png)

    In alternativa, nella sessione di PowerShell, eseguire il comando seguente:

    ```PowerShell
    Start-AIPScan
    ```

1. Attendere che lo scanner completi il proprio ciclo. L'analisi viene completata quando lo scanner ha sottoposto a ricerca per indicizzazione tutti i file negli archivi dati specificati.

    Per monitorare lo stato di avanzamento dello scanner, effettuare una delle operazioni seguenti:

    - **Aggiornare i processi di analisi.**  Nel riquadro **processi di analisi Azure Information Protection-contenuto** selezionare **Aggiorna**.

        Attendere fino a visualizzare i valori per la colonna **Last Scan Results** e **Last Scan (End Time)** .

    - **Usare un comando di PowerShell.** Eseguire `Get-AIPScannerStatus` per monitorare la modifica dello stato.

1. Una volta completata l'analisi, esaminare i report archiviati nella directory **% *LocalAppData*% \ Microsoft\MSIP\Scanner\Reports**

    - I file summary.txt includono il tempo impiegato per l'analisi, il numero di file analizzati e il numero di file con una corrispondenza per i tipi di informazioni.

    - I file con estensione csv includono ulteriori dettagli per ogni file. In questa cartella vengono archiviati fino a 60 report per ogni ciclo di analisi e tutti i report tranne l'ultimo vengono compressi per ridurre al minimo lo spazio su disco necessario.

Le [configurazioni iniziali](deploy-aip-scanner-configure-install.md#configure-the-scanner-in-the-azure-portal) indicano di impostare i **tipi di informazioni da** individuare solo per i **criteri**. Questa configurazione significa che nei report dettagliati vengono inclusi solo i file che soddisfano le condizioni configurate per la classificazione automatica.

Se non viene visualizzata alcuna etichetta, verificare che la configurazione dell'etichetta includa la classificazione automatica anziché quella consigliata oppure abilitare l' **etichettatura consigliata come automatica** (disponibile nella versione dello scanner 2.7. x. x e versioni successive).

Se i risultati non sono ancora quelli previsti, potrebbe essere necessario riconfigurare le condizioni specificate per le etichette. In tal caso, riconfigurare le condizioni in base alle esigenze e ripetere questa procedura fino a quando non si è soddisfatti dei risultati. Aggiornare quindi automaticamente la configurazione e, facoltativamente, la protezione.

### <a name="viewing-updates-in-the-azure-portal"></a>Visualizzazione degli aggiornamenti nella portale di Azure

Gli scanner inviano queste informazioni a Azure Information Protection ogni cinque minuti, in modo che sia possibile visualizzare i risultati quasi in tempo reale dall'portale di Azure. Per altre informazioni, vedere [Reporting per Azure Information Protection](reports-aip.md).

Il portale di Azure visualizza solo le informazioni sull'ultima analisi. Se è necessario visualizzare i risultati delle analisi precedenti, tornare ai report archiviati nel computer dello scanner, nella cartella %*localappdata*%\Microsoft\MSIP\Scanner\Reports.

### <a name="changing-log-levels-or-locations"></a>Modifica di livelli o posizioni del log

Modificare il livello di registrazione utilizzando il parametro *reportLevel* con [set-AIPScannerConfiguration](/powershell/module/azureinformationprotection/set-aipscannerconfiguration).

Impossibile modificare il percorso o il nome della cartella del report. Se si desidera archiviare i report in un percorso diverso, è consigliabile utilizzare una giunzione di directory per la cartella.

Ad esempio, usare il comando [mklink](/windows-server/administration/windows-commands/mklink) : `mklink /j D:\Scanner_reports C:\Users\aipscannersvc\AppData\Local\Microsoft\MSIP\Scanner\Reports`

Se questi passaggi sono stati eseguiti dopo una configurazione iniziale e l'installazione, continuare con [la configurazione dello scanner per applicare la classificazione e la protezione](deploy-aip-scanner-configure-install.md#configure-the-scanner-to-apply-classification-and-protection).

## <a name="stopping-a-scan"></a>Arresto di un'analisi

Per arrestare un'analisi attualmente in esecuzione prima che venga completata, usare uno dei metodi seguenti:

- **portale di Azure.** Selezionare **Arresta analisi**:

    ![Arrestare un'analisi per lo scanner Azure Information Protection](./media/scanner-stop-scan.png)

- **Eseguire un comando di PowerShell.** Eseguire il comando seguente:

    ```PowerShell
    Stop-AIPScan 
    ```

## <a name="rescanning-files"></a>Ripetizione dell'analisi dei file

Per il [primo ciclo di analisi](#run-a-discovery-cycle-and-view-reports-for-the-scanner), lo scanner controlla tutti i file negli archivi dati configurati. Per le analisi successive, vengono controllati solo i file nuovi o modificati.

Il controllo di tutti i file è in genere utile quando si desidera che i report includano tutti i file, quando si dispone di modifiche che si desidera applicare in tutti i file e quando lo scanner viene eseguito in modalità di individuazione.

**Per eseguire manualmente una ripetizione dell'analisi completa**:

1. Passare al riquadro **processi di analisi Azure Information Protection-contenuto** nel portale di Azure.

1. Selezionare il processo di analisi del contenuto dall'elenco e quindi selezionare l'opzione **Ripeti analisi di tutti i file** :

    ![Avviare un'altra analisi per lo scanner di Azure Information Protection](./media/scanner-rescan-files.png)

Al termine di un'analisi completa, il tipo di analisi viene automaticamente modificato in incrementale in modo che, per le analisi successive, vengano nuovamente analizzati solo i file nuovi o modificati.

> [!TIP]
> Se sono state apportate modifiche al [processo di analisi del contenuto](deploy-aip-scanner-configure-install.md#create-a-content-scan-job)AIP, il portale di Azure chiederà di ignorare una ripetizione completa. Per assicurarsi che la ripetizione dell'analisi avvenga, assicurarsi di selezionare **No** nel prompt visualizzato.
> 
### <a name="trigger-a-full-rescan-by-modifying-your-settings-versions-271010-and-lower"></a>Attivare una ripetizione dell'analisi completa modificando le impostazioni (versioni 2.7.101.0 e precedenti)

Nelle versioni dello scanner [2.7.101.0](rms-client/unifiedlabelingclient-version-release-history.md#version-271010) e versioni precedenti, tutti i file vengono analizzati ogni volta che lo scanner rileva impostazioni nuove o modificate per le etichette automatiche e consigliate. Lo scanner aggiorna automaticamente i criteri ogni quattro ore.

Per aggiornare prima il criterio, ad esempio durante il test, eliminare manualmente il contenuto della directory **%LocalAppData%\Microsoft\MSIP\mip \<processname> \mip** e riavviare il servizio Azure Information Protection.

Se sono state modificate anche le impostazioni di protezione per le etichette, attendere 15 minuti aggiuntivi dal momento in cui sono state salvate le impostazioni di protezione aggiornate prima di riavviare il servizio Azure Information Protection.

> [!IMPORTANT]
> Se è stato eseguito l'aggiornamento alla versione [2.8.85.0](rms-client/unifiedlabelingclient-version-release-history.md#version-28850) o successiva, AIP ignora la ripetizione dell'analisi completa per le impostazioni aggiornate per garantire prestazioni coerenti. Se è stato eseguito l'aggiornamento, assicurarsi di [eseguire una ripetizione dell'analisi completa manualmente](#rescanning-files) , se necessario. 
>
> Se, ad esempio, sono state modificate le impostazioni dei **criteri di riservatezza** da **Imponi = off** per applicare **= on**, assicurarsi di eseguire una ripetizione dell'analisi completa per applicare le etichette nel contenuto.
> 

## <a name="next-steps"></a>Passaggi successivi

- Se si è interessati a scoprire come è stato implementato questo scanner dai team Microsoft Core Services Engineering e Operations,  leggere il case study tecnico: [Automating data protection with Azure Information Protection scanner](https://www.microsoft.com/itshowcase/Article/Content/1070/Automating-data-protection-with-Azure-Information-Protection-scanner) (Automatizzazione della protezione dei dati con lo scanner di Azure Information Protection).

- È anche possibile usare PowerShell per classificare e proteggere in modo interattivo i file dal computer desktop. Per altre informazioni su questo e altri scenari in cui viene usato PowerShell, vedere [uso di PowerShell con il Azure Information Protection Unified Labeling client](./rms-client/clientv2-admin-guide-powershell.md).