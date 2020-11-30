---
title: Informazioni sul Azure Information Protection Unified Labeling scanner-AIP
description: Istruzioni per installare, configurare ed eseguire la versione corrente del Azure Information Protection scanner Unified Labeling per individuare, classificare e proteggere i file negli archivi dati.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 11/15/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: scanner
ms.reviewer: demizets
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 35bb27bbb6cbfeb8fa4291c9442c95190b92e28b
ms.sourcegitcommit: d31cb53de64bafa2097e682550645cadc612ec3e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/30/2020
ms.locfileid: "96316272"
---
# <a name="what-is-the-azure-information-protection-unified-labeling-scanner"></a>Informazioni sullo scanner di etichettatura unificata di Azure Information Protection

>*Si applica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), windows server 2019, windows server 2016, windows Server 2012 R2*

>[!NOTE] 
> Se si usa lo scanner classico, vedere [che cos'è il Azure Information Protection scanner classico?](deploy-aip-scanner-classic.md).
>
> Per analizzare ed etichettare i file nei repository cloud, usare [Cloud App Security](/cloud-app-security/) invece dello scanner.

Usare le informazioni contenute in questa sezione per informazioni sul Azure Information Protection scanner Unified Labeling, quindi su come installare, configurare, eseguire e, se necessario, risolverlo correttamente.

Lo scanner AIP viene eseguito come servizio in Windows Server e consente di individuare, classificare e proteggere i file negli archivi dati seguenti:

- **Percorsi UNC** per le condivisioni di rete che usano i protocolli SMB o NFS (anteprima).

- **Raccolte documenti di SharePoint e cartella** per sharepoint server 2019 tramite sharepoint Server 2013. Anche SharePoint 2010 è supportato per i clienti che hanno [esteso il supporto per questa versione di SharePoint](https://support.microsoft.com/lifecycle/search?alpha=SharePoint%20Server%202010).

Per classificare e proteggere i file, lo scanner usa le [etichette di riservatezza](/microsoft-365/compliance/sensitivity-labels) configurate in uno dei Microsoft 365 assegnare etichette ai centri di amministrazione, tra cui il centro sicurezza Microsoft 365, il centro di conformità Microsoft 365 e il Microsoft 365 Centro sicurezza e conformità. 

## <a name="azure-information-protection-unified-labeling-scanner-overview"></a>Panoramica di Azure Information Protection Unified Labeling scanner

Lo scanner AIP può ispezionare tutti i file che Windows può indicizzare. Se sono state configurate le etichette di riservatezza per applicare la classificazione automatica, lo scanner può etichettare i file individuati per applicare tale classificazione e, facoltativamente, applicare o rimuovere la protezione. 

La figura seguente mostra l'architettura dello scanner AIP, in cui lo scanner individua i file nei server locali e SharePoint.

:::image type="content" source="media/ul-scanner-arch.png" alt-text="Azure Information Protection architettura dello scanner per l'assegnazione di etichette unificata":::

Per esaminare i file, lo scanner usa i filtri IFilter installati nel computer. Per determinare se i file richiedono l'assegnazione di etichette, lo scanner usa Microsoft 365 i tipi di informazioni riservate per la prevenzione della perdita dei dati (DLP) incorporati e il rilevamento dei modelli o Microsoft 365 i modelli Regex.

Lo scanner usa il client Azure Information Protection e può classificare e proteggere gli stessi tipi di file del client. Per altre informazioni, vedere [tipi di file supportati dal client di Azure Information Protection Unified Labeling](./rms-client/clientv2-admin-guide-file-types.md).

Per configurare le analisi in base alle esigenze, eseguire una delle operazioni seguenti:

- **Eseguire lo scanner solo in modalità di individuazione** per creare report che verificano cosa accade quando i file vengono etichettati.
- **Eseguire lo scanner per individuare i file con informazioni riservate,** senza configurare le etichette che applicano la classificazione automatica.
- **Eseguire lo scanner automaticamente** per applicare le etichette come configurato. 
- **Definire un elenco di tipi di file** per specificare i file specifici da analizzare o da escludere.

> [!NOTE]
> Lo scanner non individua ed etichetta in tempo reale. Esegue sistematicamente la ricerca per indicizzazione nei file negli archivi dati specificati dall'utente. Configurare questo ciclo per l'esecuzione una sola volta o ripetutamente.

> [!TIP]
> Lo scanner Unified Labeling supporta i cluster di scanner con più nodi, consentendo la scalabilità orizzontale dell'organizzazione, ottenendo tempi di analisi più rapidi e un ambito più ampio. 
> 
> È possibile distribuire più nodi direttamente dall'inizio o iniziare con un cluster a nodo singolo e aggiungere altri nodi in un secondo momento quando si cresce. Distribuire più nodi usando lo stesso nome del cluster e il database per il cmdlet **Install-AIPScanner** .
> 

## <a name="aip-scanning-process"></a>Processo di analisi AIP

Durante l'analisi dei file, AIP scanner esegue i passaggi seguenti:

[1. determinare se i file sono inclusi o esclusi per l'analisi](#1-determine-whether-files-are-included-or-excluded-for-scanning)

[2. Ispezionare ed etichettare i file](#2-inspect-and-label-files)

[3. etichettare i file che non possono essere controllati](#3-label-files-that-cant-be-inspected) 

Per ulteriori informazioni, vedere [file non etichettati dallo scanner](#files-not-labeled-by-the-scanner).

### <a name="1-determine-whether-files-are-included-or-excluded-for-scanning"></a>1. determinare se i file sono inclusi o esclusi per l'analisi 

Lo scanner ignora automaticamente i file esclusi dalla classificazione e dalla protezione, ad esempio file eseguibili e file di sistema. Per ulteriori informazioni, vedere [tipi di file esclusi dalla classificazione e dalla protezione](./rms-client/clientv2-admin-guide-file-types.md#file-types-that-are-excluded-from-classification-and-protection).

Lo scanner considera anche eventuali elenchi di file definiti in modo esplicito per l'analisi o l'esclusione dall'analisi. Per impostazione predefinita, gli elenchi di file si applicano a tutti i repository di dati e possono anche essere definiti solo per repository specifici.

Per definire gli elenchi di file per l'analisi o l'esclusione, usare l'impostazione **tipi di file da analizzare** nel processo di analisi del contenuto. Ad esempio:

![Configurare i tipi di file da analizzare per lo scanner di Azure Information Protection](./media/scanner-file-types.png)

Per ulteriori informazioni, vedere [Deploying the Azure Information Protection scanner to classificare e proteggere automaticamente i file](deploy-aip-scanner-configure-install.md).

### <a name="2-inspect-and-label-files"></a>2. Ispezionare ed etichettare i file

Dopo aver identificato i file esclusi, lo scanner filtra di nuovo per identificare i file supportati per l'ispezione.

Questi filtri aggiuntivi sono quelli usati dal sistema operativo per la ricerca e l'indicizzazione di Windows e non richiedono alcuna configurazione aggiuntiva. IFilter di Windows viene usato anche per analizzare i tipi di file usati da Word, Excel e PowerPoint e per i documenti PDF e i file di testo.

Per un elenco completo dei tipi di file supportati per l'ispezione e istruzioni aggiuntive per la configurazione dei filtri per includere i file con estensione zip e TIFF, vedere [tipi di file supportati per l'ispezione](./rms-client/clientv2-admin-guide-file-types.md#file-types-supported-for-inspection).

Dopo l'ispezione, i tipi di file supportati vengono contrassegnati con le condizioni specificate per le etichette. Se si usa la modalità di individuazione, è possibile che i file vengano segnalati per contenere le condizioni specificate per le etichette o che siano presenti tipi di informazioni riservate note.

#### <a name="stopped-scanner-processes"></a>Processi scanner arrestati

Se lo scanner si arresta e non completa un'analisi per un numero elevato di file nel repository, potrebbe essere necessario aumentare il numero di porte dinamiche per il sistema operativo che ospita i file.

Ad esempio, la protezione avanzata dei server per SharePoint è uno dei motivi per cui lo scanner supera il numero di connessioni di rete consentite e pertanto si arresta.

Per verificare se questa è la conseguenza dell'arresto dello scanner, verificare la presenza del seguente messaggio di errore nei log dello scanner in **%LocalAppData%\Microsoft\MSIP\Logs\MSIPScanner.Iplog** (più log vengono compressi in un file zip):

`Unable to connect to the remote server ---> System.Net.Sockets.SocketException: Only one usage of each socket address (protocol/network address/port) is normally permitted IP:port`

Per ulteriori informazioni su come visualizzare l'intervallo di porte corrente e aumentarlo se necessario, vedere [impostazioni che possono essere modificate per migliorare le prestazioni di rete](/biztalk/technical-guides/settings-that-can-be-modified-to-improve-network-performance).

> [!TIP]
> Per le farm di SharePoint di grandi dimensioni, potrebbe essere necessario aumentare la soglia di visualizzazione elenco, il cui valore predefinito è **5.000.**
>
> Per ulteriori informazioni, vedere la pagina relativa alla [gestione di elenchi di grandi dimensioni e librerie in SharePoint](https://support.office.com/article/manage-large-lists-and-libraries-in-sharepoint-b8588dae-9387-48c2-9248-c24122f07c59#__bkmkchangelimit&ID0EAABAAA=Server).
>

### <a name="3-label-files-that-cant-be-inspected"></a>3. etichettare i file che non possono essere controllati

Per tutti i tipi di file che non possono essere controllati, lo scanner AIP applica l'etichetta predefinita nei criteri di Azure Information Protection o l'etichetta predefinita configurata per lo scanner.

### <a name="files-not-labeled-by-the-scanner"></a>File non contrassegnati dallo scanner
Lo scanner AIP non può etichettare i file nelle circostanze seguenti:

- Quando l'etichetta applica la classificazione, ma non la protezione, e il tipo di file non supporta solo la classificazione da parte del client. Per ulteriori informazioni, vedere [Unified Labeling client tipi di file](./rms-client/clientv2-admin-guide-file-types.md#file-types-supported-for-classification-only).

- Quando l'etichetta applica la classificazione e la protezione, ma lo scanner non supporta il tipo di file.
  
    Per impostazione predefinita lo scanner protegge solo i tipi di file di Office e i file PDF se questi sono protetti usando lo standard ISO per la crittografia dei file PDF. 

    Quando si [modificano i tipi di file da proteggere](deploy-aip-scanner-configure-install.md#change-which-file-types-to-protect), è possibile aggiungere altri tipi di file per la protezione.

**Esempio:** Dopo aver ispezionato i file con estensione txt, lo scanner non può applicare un'etichetta configurata solo per la classificazione, perché il tipo di file con estensione txt non supporta solo la classificazione. 

Tuttavia, se l'etichetta è configurata per la classificazione e la protezione e il tipo di file txt è incluso per la protezione dello scanner, lo scanner può etichettare il file.

## <a name="next-steps"></a>Passaggi successivi

Per ulteriori informazioni sulla distribuzione dello scanner, vedere gli articoli seguenti:

- [Prerequisiti per la distribuzione di AIP scanner](deploy-aip-scanner-prereqs.md)
- [Configurazione e installazione dello scanner AIP](deploy-aip-scanner-configure-install.md)
- [Esecuzione di analisi mediante lo scanner AIP](deploy-aip-scanner-manage.md)

**Ulteriori informazioni:**

- Consultare il Blog sulle procedure consigliate per lo scanner Unified Labeling: procedure consigliate [per la distribuzione e l'uso dello scanner AIP UL](https://aka.ms/AIPScannerBestPractices)

- Se si è interessati a scoprire come è stato implementato questo scanner dai team Microsoft Core Services Engineering e Operations,  leggere il case study tecnico: [Automating data protection with Azure Information Protection scanner](https://www.microsoft.com/itshowcase/Article/Content/1070/Automating-data-protection-with-Azure-Information-Protection-scanner) (Automatizzazione della protezione dei dati con lo scanner di Azure Information Protection).

- Ci si potrebbe chiedere: [Qual è la differenza tra il cluster di failover di Windows Server e il Azure Information Protection scanner?](faqs.md#whats-the-difference-between-windows-server-fci-and-the-azure-information-protection-scanner)

- È anche possibile usare PowerShell per classificare e proteggere in modo interattivo i file dal computer desktop. Per altre informazioni su questo e altri scenari in cui viene usato PowerShell, vedere [uso di PowerShell con il Azure Information Protection Unified Labeling client](./rms-client/clientv2-admin-guide-powershell.md)