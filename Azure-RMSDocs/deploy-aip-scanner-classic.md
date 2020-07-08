---
title: Informazioni sul Azure Information Protection scanner classico-AIP
description: Istruzioni per installare, configurare ed eseguire il Azure Information Protection scanner classico per individuare, classificare e proteggere i file negli archivi dati.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 06/29/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: scanner
ms.reviewer: demizets
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 65c3a37f68676616d7342879d9621a143842f4bf
ms.sourcegitcommit: 223e26b0ca4589317167064dcee82ad0a6a8d663
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/07/2020
ms.locfileid: "86049541"
---
# <a name="what-is-the-azure-information-protection-classic-scanner"></a>Che cos'è il Azure Information Protection scanner classico?

>*Si applica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), windows server 2019, windows server 2016, windows Server 2012 R2*

>[!NOTE]
> Per offrire un'esperienza per i clienti unificata e semplificata, il **client di Azure Information Protection client (versione classica)** e la **Gestione etichette** nel portale di Azure vengono **deprecati** a partire dal **31 marzo 2021**. In questo intervallo di tempo tutti i clienti correnti di Azure Information Protection possono passare alla soluzione di etichettatura unificata usando la piattaforma di etichettatura unificata di Microsoft Information Protection. Altre informazioni nell'[avviso ufficiale sulla deprecazione](https://aka.ms/aipclassicsunset).
>
> Se si usa il client Unified Labeling, vedere [che cos'è il Azure Information Protection scanner Unified Labeling?](deploy-aip-scanner.md).

Usare le informazioni contenute in questa sezione per informazioni sul Azure Information Protection scanner e su come installare, configurare, eseguire e, se necessario, risolverlo.

Lo scanner AIP viene eseguito come servizio in Windows Server e consente di individuare, classificare e proteggere i file negli archivi dati seguenti:

- **Percorsi UNC** per le condivisioni di rete che usano il protocollo SMB (Server Message Block).

- **Raccolte documenti di SharePoint e cartella** per sharepoint server 2019 tramite sharepoint Server 2013. Anche SharePoint 2010 è supportato per i clienti che hanno [esteso il supporto per questa versione di SharePoint](https://support.microsoft.com/lifecycle/search?alpha=SharePoint%20Server%202010).

> [!NOTE]
> Per analizzare ed etichettare i file nei repository cloud, usare [Cloud App Security](https://docs.microsoft.com/cloud-app-security/) invece dello scanner.
>
## <a name="azure-information-protection-classic-scanner-overview"></a>Panoramica dello scanner classico Azure Information Protection

Lo scanner AIP può ispezionare tutti i file che Windows può indicizzare. Se sono state configurate etichette che applicano la classificazione automatica, lo scanner può etichettare i file individuati per applicare tale classificazione e, facoltativamente, applicare o rimuovere la protezione.

La figura seguente mostra l'architettura dello scanner AIP, in cui lo scanner individua i file nei server locali e SharePoint.

:::image type="content" source="media/classic-scanner-arch.png" alt-text="Azure Information Protection architettura dello scanner classico":::

Per esaminare i file, lo scanner usa i filtri IFilter installati nel computer. Per determinare se i file richiedono l'assegnazione di etichette, lo scanner usa i tipi di informazioni riservate per la prevenzione della perdita dei dati (DLP) di Office 365 e il rilevamento dei pattern o i modelli Regex di Office 365.

Lo scanner usa il client Azure Information Protection e può classificare e proteggere gli stessi tipi di file del client. Per ulteriori informazioni, vedere [tipi di file supportati dal client Azure Information Protection](./rms-client/client-admin-guide-file-types.md).

Per configurare le analisi in base alle esigenze, eseguire una delle operazioni seguenti:

- **Eseguire lo scanner solo in modalità di individuazione** per creare report che verificano cosa accade quando i file vengono etichettati.
- **Eseguire lo scanner per individuare i file con informazioni riservate,** senza configurare le etichette che applicano la classificazione automatica.
- **Eseguire lo scanner automaticamente** per applicare le etichette come configurato.
- **Definire un elenco di tipi di file** per specificare i file specifici da analizzare o da escludere.

> [!NOTE]
> Lo scanner non individua ed etichetta in tempo reale. Esegue sistematicamente la ricerca per indicizzazione nei file negli archivi dati specificati dall'utente. Configurare questo ciclo per l'esecuzione una sola volta o ripetutamente.

## <a name="aip-scanning-process"></a>Processo di analisi AIP

Durante l'analisi dei file, AIP scanner esegue i passaggi seguenti:

[1. determinare se i file sono inclusi o esclusi per l'analisi](#1-determine-whether-files-are-included-or-excluded-for-scanning)

[2. Ispezionare ed etichettare i file](#2-inspect-and-label-files)

[3. etichettare i file che non possono essere controllati](#3-label-files-that-cant-be-inspected)

> [!NOTE]
> Per ulteriori informazioni, vedere [file non etichettati dallo scanner](#files-not-labeled-by-the-scanner).

### <a name="1-determine-whether-files-are-included-or-excluded-for-scanning"></a>1. determinare se i file sono inclusi o esclusi per l'analisi

Lo scanner ignora automaticamente i file esclusi dalla classificazione e dalla protezione, ad esempio file eseguibili e file di sistema. Per ulteriori informazioni, vedere [tipi di file esclusi dalla classificazione e dalla protezione](./rms-client/client-admin-guide-file-types.md#file-types-that-are-excluded-from-classification-and-protection).

Lo scanner considera anche eventuali elenchi di file definiti in modo esplicito per l'analisi o l'esclusione dall'analisi. Per impostazione predefinita, gli elenchi di file si applicano a tutti i repository di dati e possono anche essere definiti solo per repository specifici.

Per definire gli elenchi di file per l'analisi o l'esclusione, usare l'impostazione **tipi di file da analizzare** nel processo di analisi del contenuto. Ad esempio:

![Configurare i tipi di file da analizzare per lo scanner di Azure Information Protection](./media/scanner-file-types.png)

Per ulteriori informazioni, vedere [Deploying the Azure Information Protection scanner to classificare e proteggere automaticamente i file](deploy-aip-scanner-configure-install.md).

### <a name="2-inspect-and-label-files"></a>2. Ispezionare ed etichettare i file

Dopo aver identificato i file esclusi, lo scanner filtra di nuovo per identificare i file supportati per l'ispezione.

Questi filtri aggiuntivi sono quelli usati dal sistema operativo per la ricerca e l'indicizzazione di Windows e non richiedono alcuna configurazione aggiuntiva. IFilter di Windows viene usato anche per analizzare i tipi di file usati da Word, Excel e PowerPoint e per i documenti PDF e i file di testo.

Per un elenco completo dei tipi di file supportati per l'ispezione e istruzioni aggiuntive per la configurazione dei filtri per includere i file con estensione zip e TIFF, vedere [tipi di file supportati per l'ispezione](./rms-client/client-admin-guide-file-types.md#file-types-supported-for-inspection).

Dopo l'ispezione, i tipi di file supportati vengono contrassegnati con le condizioni specificate per le etichette. Se si usa la modalità di individuazione, è possibile che i file vengano segnalati per contenere le condizioni specificate per le etichette o che siano presenti tipi di informazioni riservate note.

### <a name="3-label-files-that-cant-be-inspected"></a>3. etichettare i file che non possono essere controllati

Per tutti i tipi di file che non possono essere controllati, lo scanner AIP applica l'etichetta predefinita nei criteri di Azure Information Protection o l'etichetta predefinita configurata per lo scanner.

### <a name="files-not-labeled-by-the-scanner"></a>File non contrassegnati dallo scanner

Lo scanner AIP non può etichettare i file nelle circostanze seguenti:

- Quando l'etichetta applica la classificazione, ma non la protezione, e il tipo di file non supporta solo la classificazione da parte del client. Per altre informazioni, vedere [tipi di file client classici](./rms-client/client-admin-guide-file-types.md#file-types-supported-for-classification-only).

- Quando l'etichetta applica la classificazione e la protezione, ma lo scanner non supporta il tipo di file.
  
    Per impostazione predefinita lo scanner protegge solo i tipi di file di Office e i file PDF se questi sono protetti usando lo standard ISO per la crittografia dei file PDF.

    Quando si [modificano i tipi di file da proteggere](deploy-aip-scanner-configure-install.md#change-which-file-types-to-protect), è possibile aggiungere altri tipi di file per la protezione.

**Esempio:** Dopo aver ispezionato i file con estensione txt, lo scanner non può applicare un'etichetta configurata solo per la classificazione, perché il tipo di file con estensione txt non supporta solo la classificazione.

Tuttavia, se l'etichetta è configurata per la classificazione e la protezione e il tipo di file txt è incluso per la protezione dello scanner, lo scanner può etichettare il file.

## <a name="upgrading-your-scanner"></a>Aggiornamento dello scanner

Se lo scanner è stato installato in precedenza e si vuole eseguire l'aggiornamento, vedere [aggiornamento dello scanner Azure Information Protection](./rms-client/client-admin-guide.md#upgrading-the-azure-information-protection-scanner).

Quindi, [configurare](deploy-aip-scanner-configure-install.md) e [usare lo scanner](deploy-aip-scanner-manage.md) come di consueto, ignorando i passaggi per installare lo scanner.

>[!NOTE]
> Se si dispone di una versione dello scanner precedente a 1.48.204.0 e non si è pronti per aggiornarla, vedere [distribuzione di versioni precedenti dello scanner Azure Information Protection per classificare e proteggere automaticamente i file](deploy-aip-scanner-previousversions.md).

## <a name="next-steps"></a>Passaggi successivi

Per ulteriori informazioni sulla distribuzione dello scanner, vedere gli articoli seguenti:

- [Prerequisiti per la distribuzione di AIP scanner](deploy-aip-scanner-prereqs.md)
- [Configurazione e installazione dello scanner AIP](deploy-aip-scanner-configure-install.md)
- [Esecuzione di analisi mediante lo scanner AIP](deploy-aip-scanner-manage.md)

**Ulteriori informazioni:**

- Se si è interessati a scoprire come è stato implementato questo scanner dai team Microsoft Core Services Engineering e Operations,  leggere il case study tecnico: [Automating data protection with Azure Information Protection scanner](https://www.microsoft.com/itshowcase/Article/Content/1070/Automating-data-protection-with-Azure-Information-Protection-scanner) (Automatizzazione della protezione dei dati con lo scanner di Azure Information Protection).

- Ci si potrebbe chiedere: [Qual è la differenza tra il cluster di failover di Windows Server e il Azure Information Protection scanner?](faqs.md#whats-the-difference-between-windows-server-fci-and-the-azure-information-protection-scanner)

- È anche possibile usare PowerShell per classificare e proteggere in modo interattivo i file dal computer desktop. Per altre informazioni su questo e altri scenari che usano PowerShell, vedere [Uso di PowerShell con il client Azure Information Protection](./rms-client/client-admin-guide-powershell.md).
