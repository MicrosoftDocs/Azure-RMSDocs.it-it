---
title: Esecuzione dello scanner di Azure Information Protection classico (AIP)
description: Istruzioni per l'esecuzione dello scanner classico Azure Information Protection per individuare, classificare e proteggere i file negli archivi dati.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 06/29/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: information-protection
ROBOTS: NOINDEX
ms.subservice: scanner
ms.reviewer: demizets
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: c23eb1770063bd0df18582125855580aa762b750
ms.sourcegitcommit: b32c16e41ba36167b5a3058b56a73183bdd4306d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/29/2020
ms.locfileid: "97806261"
---
# <a name="running-the-azure-information-protection-classic-scanner"></a>Esecuzione dello scanner classico Azure Information Protection

>***Si applica a**: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2 *
>
>***Pertinente per**: [Azure Information Protection client classico per Windows](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients). Per il client di etichettatura unificata, vedere [esecuzione dello scanner di Azure Information Protection](deploy-aip-scanner-manage.md)*.

> [!NOTE] 
> Per offrire un'esperienza per i clienti unificata e semplificata, il **client classico di Azure Information Protection** e **Gestione etichette** nel portale di Azure saranno **deprecati** a partire dal **31 marzo 2021**. In questo intervallo di tempo tutti i clienti correnti di Azure Information Protection possono passare alla soluzione di etichettatura unificata usando la piattaforma di etichettatura unificata di Microsoft Information Protection. Altre informazioni nell'[avviso ufficiale sulla deprecazione](https://aka.ms/aipclassicsunset).

Dopo aver verificato i [requisiti di sistema](deploy-aip-scanner-prereqs-classic.md) e [configurato e installato lo scanner](deploy-aip-scanner-configure-install-classic.md), [eseguire un'analisi di individuazione](#run-a-discovery-cycle-and-view-reports-for-the-scanner) per iniziare.

Per gestire le analisi in avanti, attenersi alla procedura descritta di seguito.

- [Arrestare un'analisi](#stopping-a-scan)
- [Ripetizione dell'analisi dei file](#rescanning-files)
- [Risoluzione dei problemi relativi a un'analisi arrestata](#troubleshooting-a-stopped-scan)
- [Risoluzione dei problemi con lo strumento di diagnostica dello scanner](#troubleshooting-using-the-scanner-diagnostic-tool)
- [ID e descrizioni del registro eventi dello scanner](#event-log-ids-and-descriptions-for-the-scanner)

Per ulteriori informazioni, vedere [Deploying the Azure Information Protection scanner to classificare e proteggere automaticamente i file](deploy-aip-scanner.md).

## <a name="run-a-discovery-cycle-and-view-reports-for-the-scanner"></a>Eseguire un ciclo di individuazione e visualizzare i report per lo scanner

Usare la procedura seguente dopo aver [configurato e installato lo scanner](deploy-aip-scanner-configure-install.md) per ottenere una conoscenza iniziale del contenuto.

Eseguire di nuovo questi passaggi in base alle esigenze quando il contenuto cambia.

1. Nella portale di Azure, nel riquadro **processi di analisi Azure Information Protection-contenuto** selezionare i processi di analisi del contenuto, quindi selezionare l'opzione **Analizza ora** :

    ![Avviare l'analisi per lo scanner di Azure Information Protection](./media/scanner-scan-now.png)

    In alternativa, nella sessione di PowerShell, eseguire il comando seguente:
    
    ```ps
    Start-AIPScan
    ```

1. Attendere che lo scanner completi il proprio ciclo. L'analisi viene completata quando lo scanner ha sottoposto a ricerca per indicizzazione tutti i file negli archivi dati specificati.

    Per monitorare lo stato di avanzamento dello scanner, effettuare una delle operazioni seguenti:

    - **Aggiornare i processi di analisi.**  Nel riquadro **processi di analisi Azure Information Protection-contenuto** selezionare **Aggiorna**.

        Attendere fino a visualizzare i valori per la colonna **Last Scan Results** e **Last Scan (End Time)** .

    - **Usare un comando di PowerShell.** Eseguire `Get-AIPScannerStatus` per monitorare la modifica dello stato.

    - **Controllare i registri eventi di Windows.** Controllare il registro eventi dei **Servizi e delle applicazioni** Windows locali, denominato **Azure Information Protection**.

        Questo log segnala anche quando lo scanner ha terminato l'analisi, incluso un riepilogo dei risultati. Cercare l'ID evento informativo **911**. Per altre informazioni, vedere [ID e descrizioni del registro eventi per lo scanner](#event-log-ids-and-descriptions-for-the-scanner).

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
    
    ```ps
    Stop-AIPScan 
    ```

## <a name="rescanning-files"></a>Ripetizione dell'analisi dei file

Per il [primo ciclo di analisi](#run-a-discovery-cycle-and-view-reports-for-the-scanner), lo scanner controlla tutti i file negli archivi dati configurati. Per le analisi successive, vengono controllati solo i file nuovi o modificati.

Il controllo di tutti i file è in genere utile quando si desidera che i report includano tutti i file e quando lo scanner viene eseguito in modalità di individuazione.

Eseguire una nuova analisi di tutti i file usando uno dei metodi seguenti:

- [Esegui manualmente una ripetizione dell'analisi completa](#manually-run-a-full-rescan)
- [Attivare una ripetizione dell'analisi completa aggiornando il criterio](#trigger-a-full-rescan-by-refreshing-the-policy)

### <a name="manually-run-a-full-rescan"></a>Esegui manualmente una ripetizione dell'analisi completa

Forza lo scanner a ispezionare nuovamente tutti i file, in base alle esigenze, dal riquadro **processi di analisi Azure Information Protection-contenuto** nel portale di Azure.

Selezionare il processo di analisi del contenuto dall'elenco e quindi selezionare l'opzione **Ripeti analisi di tutti i file** :

![Avviare un'altra analisi per lo scanner di Azure Information Protection](./media/scanner-rescan-files.png)

Al termine di un'analisi completa, il tipo di analisi viene automaticamente modificato in incrementale in modo che, per le analisi successive, vengano nuovamente analizzati solo i file nuovi o modificati.

### <a name="trigger-a-full-rescan-by-refreshing-the-policy"></a>Attivare una ripetizione dell'analisi completa aggiornando il criterio

Tutti i file vengono controllati anche negli scenari seguenti ogni volta che lo scanner Scarica un criterio di Azure Information Protection con condizioni nuove o modificate.

Lo scanner aggiorna automaticamente i criteri ogni ora, nonché ogni volta che il servizio viene avviato e il criterio viene trovato più di un'ora prima.

Per aggiornare prima il criterio, ad esempio durante il test, eliminare manualmente il file dei criteri **Policy.msip**  dalla directory **%LocalAppData%\Microsoft\MSIP** e riavviare il servizio di Azure Information Protection.

> [!NOTE]
> Se sono state modificate anche le impostazioni di protezione per le etichette, attendere 15 minuti aggiuntivi dal momento in cui sono state salvate le impostazioni di protezione aggiornate prima di riavviare il servizio Azure Information Protection.
>

## <a name="troubleshooting-a-stopped-scan"></a>Risoluzione dei problemi relativi a un'analisi arrestata

Se lo scanner si interrompe in modo imprevisto e non completa l'analisi di un numero elevato di file in un repository, potrebbe essere necessario modificare una delle impostazioni seguenti:

- **Numero di porte dinamiche**. Potrebbe essere necessario aumentare il numero di porte dinamiche per il sistema operativo che ospita i file. Uno dei motivi per cui lo scanner supera il numero di connessioni di rete consentite e pertanto si arresta può essere la protezione avanzata dei server per SharePoint.

    Per verificare se questa è la conseguenza dell'arresto dello scanner, verificare se il seguente messaggio di errore viene registrato per lo scanner nel file **% *LocalAppData*% \ Microsoft\MSIP\Logs\MSIPScanner.Iplog** .

    **Impossibile connettersi al server remoto---> System .NET. Sockets. SocketException: un solo utilizzo di ogni indirizzo del socket (protocollo/indirizzo di rete/porta) è in genere consentito IP: porta**

    > [!NOTE]
    > Il file verrà compresso se sono presenti più log.

    Per altre informazioni su come visualizzare l'intervallo di porte corrente e aumentarlo, vedere [Impostazioni che possono essere modificate per migliorare le prestazioni di rete](/biztalk/technical-guides/settings-that-can-be-modified-to-improve-network-performance).

- **Soglia visualizzazione elenco.** Per le farm di SharePoint di grandi dimensioni, potrebbe essere necessario aumentare la soglia di visualizzazione elenco. Per impostazione predefinita, la soglia di visualizzazione elenco è impostata su 5.000.

    Per ulteriori informazioni, vedere [gestire elenchi e librerie di grandi dimensioni in SharePoint](https://support.office.com/article/manage-large-lists-and-libraries-in-sharepoint-b8588dae-9387-48c2-9248-c24122f07c59#__bkmkchangelimit&ID0EAABAAA=Server).

## <a name="troubleshooting-using-the-scanner-diagnostic-tool"></a>Risoluzione dei problemi con lo strumento di diagnostica dello scanner

Se si verificano problemi con Azure Information scanner, verificare se la distribuzione è integra usando il comando PowerShell seguente:

```ps
Start-AIPScannerDiagnostics
```

Lo strumento di diagnostica controlla i dettagli seguenti e quindi Esporta un file di log con i risultati:

- Indica se il database è aggiornato
- Indica se gli URL di rete sono accessibili
- Indica se è presente un token di autenticazione valido e se è possibile acquisire i criteri
- Indica se il profilo è definito nel portale di Azure
- Se la configurazione offline/online esiste e può essere acquisita
- Indica se le regole configurate sono valide

> [!TIP]
> Se si esegue il comando con un utente che non è l'utente dello scanner, assicurarsi di aggiungere il parametro **-onconto** . 
>

> [!NOTE]
> Lo strumento **Start-AIPScannerDiagnostics** non esegue un controllo dei prerequisiti completo. Se si verificano problemi con lo scanner, verificare anche che il sistema sia conforme ai [requisiti dello scanner](deploy-aip-scanner-prereqs.md)e che la [configurazione e l'installazione dello scanner](deploy-aip-scanner-configure-install.md) siano completate.
>

## <a name="event-log-ids-and-descriptions-for-the-scanner"></a>ID registro eventi e descrizioni per lo scanner

Gli eventi di log dello scanner AIP seguenti vengono archiviati nel registro eventi di **applicazioni e servizi** di Windows denominato **Azure Information Protection**.

|ID evento  |Attività  |Descrizione  |
|---------|---------|---------|
|**910**     | Ciclo dello scanner avviato        | Registrato quando il servizio scanner viene avviato e inizia a cercare i file nei repository di dati specificati.        |
|**911**     |   Ciclo dello scanner completato      | Registrato al termine di un'analisi manuale da parte dello scanner oppure quando lo scanner ha completato un ciclo per una pianificazione continua.       |
| | | |

> [!TIP]
> Se lo scanner è stato configurato per essere eseguito manualmente anziché in modo continuo, per eseguire nuovamente la scansione dei file, impostare la **pianificazione** su **manuale** o **sempre** nel processo di analisi del contenuto, quindi riavviare il servizio. Per ulteriori informazioni, vedere ripetizione dell' [analisi dei file](#rescanning-files).
>

## <a name="next-steps"></a>Passaggi successivi

- Se si è interessati a scoprire come è stato implementato questo scanner dai team Microsoft Core Services Engineering e Operations,  leggere il case study tecnico: [Automating data protection with Azure Information Protection scanner](https://www.microsoft.com/itshowcase/Article/Content/1070/Automating-data-protection-with-Azure-Information-Protection-scanner) (Automatizzazione della protezione dei dati con lo scanner di Azure Information Protection).

- Ci si potrebbe chiedere: [Qual è la differenza tra il cluster di failover di Windows Server e il Azure Information Protection scanner?](faqs-classic.md#whats-the-difference-between-windows-server-fci-and-the-azure-information-protection-scanner)

- È anche possibile usare PowerShell per classificare e proteggere in modo interattivo i file dal computer desktop. Per altre informazioni su questo e altri scenari che usano PowerShell, vedere [Uso di PowerShell con il client Azure Information Protection](./rms-client/client-admin-guide-powershell.md).