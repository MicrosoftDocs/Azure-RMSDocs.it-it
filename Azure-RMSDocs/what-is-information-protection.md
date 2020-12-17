---
title: Che cos'è Azure Information Protection (AIP)?
description: Azure Information Protection (AIP) estende il framework Microsoft Information Protection (MIP) per ampliare le funzionalità di classificazione e etichettatura fornite da Microsoft 365.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 11/09/2020
ms.topic: overview
ms.collection: M365-security-compliance
ms.service: information-protection
Customer intent: As an administrator, I want to extend Microsoft 365's labeling and classification functionality to the File Explorer, PowerShell, third party apps and services, and more.
ms.custom: contperf-fy21q2
search.appverid:
- MET150
ms.openlocfilehash: aa41b20152df55f7153f4c8cedd013041460b596
ms.sourcegitcommit: ad2b3e0b6f438f9ffc0bca975653bd13f1b7d131
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/15/2020
ms.locfileid: "97514924"
---
# <a name="what-is-azure-information-protection"></a>Che cos'è Azure Information Protection?

>***Si applica a**: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*
>
>***Rilevante per**: [Client di etichettatura unificata e client classico di AIP](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

Azure Information Protection (AIP) è una soluzione basata sul cloud che consente alle organizzazioni di individuare, classificare e proteggere documenti e messaggi di posta elettronica mediante l'applicazione di etichette al contenuto.

AIP fa parte della soluzione Microsoft Information Protection (MIP) ed estende le funzionalità di classificazione e etichettatura fornite da Microsoft 365.

La figura seguente mostra le funzionalità di Azure Information Protection aggiunte a MIP, inclusi il [client di etichettatura unificata](#aip-unified-labeling-client), lo [scanner](#aip-on-premises-scanner) e l'[SDK](#microsoft-information-protection-sdk).

:::image type="content" source="media/what-is-mip.png" alt-text="Aree di Azure Information Protection del framework Microsoft Information Protection":::

Microsoft Information Protection è lo stack di protezione delle informazioni comune usato dal client di etichettatura unificata di AIP. Per altre informazioni, vedere la [documentazione di Microsoft 365](/microsoft-365/compliance/protect-information).

## <a name="aip-unified-labeling-client"></a>Client di etichettatura unificata di AIP

Il client di etichettatura unificata di Azure Information Protection estende le funzionalità di etichettatura, classificazione e protezione a tipi di file aggiuntivi, oltre a Esplora file e PowerShell. 

Ad esempio, in Esplora file, fare clic con il pulsante destro del mouse su uno o più file e scegliere **Classifica e proteggi** per gestire la funzionalità AIP nei file selezionati.

:::image type="content" source="media/protect-from-file-explorer.png" alt-text="Classifica e proteggi da Esplora file":::

Per informazioni dettagliate sulle funzionalità più recenti e sulla versione di anteprima pubblica del client di etichettatura unificata, vedere [Client per l'etichettatura unificata di Azure Information Protection - Cronologia delle versioni e criteri per il supporto](rms-client/unifiedlabelingclient-version-release-history.md).

Scaricare il client dalla [pagina di download di Microsoft Azure Information Protection](https://www.microsoft.com/download/details.aspx?id=53018).
    
## <a name="aip-on-premises-scanner"></a>Scanner locale di AIP

Lo scanner locale di Azure Information Protection consente agli amministratori di analizzare i repository di file locali per individuare il contenuto sensibile che deve essere etichettato, classificato e/o protetto.

Lo scanner locale viene installato usando i cmdlet di PowerShell forniti con il client di etichettatura unificata e può essere gestito con PowerShell e l'area Azure Information Protection nel portale di Azure.

Usare, ad esempio, i dati dello scanner visualizzati nel portale di Azure per trovare i repository nella rete che potrebbero includere contenuto sensibile a rischio:

:::image type="content" source="media/risky-repos-small.png" alt-text="Controllare le reti analizzate per individuare repository rischiosi" lightbox="media/risky-repos.png":::

Per altre informazioni, vedere:

- [Che cos'è lo scanner di etichettatura unificata di AIP?](deploy-aip-scanner.md)
- Sezioni dedicate allo scanner della [cronologia delle versioni del client di etichettatura unificata di AIP](rms-client/unifiedlabelingclient-version-release-history.md)

Scaricare l'installazione dello scanner insieme al client dalla [pagina di download di Microsoft Azure Information Protection](https://www.microsoft.com/download/details.aspx?id=53018).


## <a name="microsoft-information-protection-sdk"></a>Microsoft Information Protection SDK

Microsoft Information Protection SDK estende le etichette di riservatezza ad app e servizi di terze parti. Gli sviluppatori possono usare l'SDK per creare il supporto incorporato per l'applicazione di etichette e della protezione ai file.

Ad esempio, è possibile usare MIP SDK per:

- Un'applicazione line-of-business che applica etichette di classificazione ai file durante l'esportazione.
- Un'applicazione di progettazione CAD/CAM che offre il supporto incorporato per l'etichettatura di Microsoft Information Protection.
- Un CASB (Cloud Access Security Broker) o una soluzione di prevenzione della perdita dei dati che prende decisioni programmatiche per i dati crittografati con Azure Information Protection.

Per altre informazioni, vedere la [Panoramica di Microsoft Information Protection SDK](/information-protection/develop/overview).

## <a name="next-steps"></a>Passaggi successivi

**Per iniziare a usare AIP**, scaricare e installare il client e lo scanner di etichettatura unificata.

- [Iscriversi per una versione di valutazione gratuita](https://admin.microsoft.com/Signup/Signup.aspx?OfferId=87dd2714-d452-48a0-a809-d2f58c4f68b7) (Enterprise Mobility + Security E5)
- [Scaricare il client](https://www.microsoft.com/download/details.aspx?id=53018)
- [Avvio rapido: Distribuire il client di etichettatura unificata](quickstart-deploy-client.md)

**Acquisire familiarità con AIP** con le esercitazioni iniziali:

- [Esercitazione: Installazione dello scanner di etichettatura unificata di Azure Information Protection (AIP)](tutorial-install-scanner.md)
- [Esercitazione: Ricerca del contenuto sensibile con lo scanner di Azure Information Protection (AIP)](tutorial-scan-networks-and-content.md)
- [Esercitazione: Prevenzione dell'oversharing in Outlook con Azure Information Protection (AIP)](tutorial-preventing-oversharing.md)

**Quando si è pronti per personalizzare ulteriormente AIP**, vedere [Guida dell'amministratore: Configurazioni personalizzate per il client di etichettatura unificata di Azure Information Protection](rms-client/clientv2-admin-guide-customizations.md).

**Per iniziare a usare MIP SDK,** vedere [Installazione e configurazione di Microsoft Information Protection (MIP) SDK](/information-protection/develop/setup-configure-mip).

### <a name="additional-resources"></a>Risorse aggiuntive

|Risorsa  |Collegamenti e descrizione  |
|---------|---------|
|**Opzioni e prezzi per la sottoscrizione**     |    [Prezzi di Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)     |
|**Domande frequenti e problemi noti**     | [Domande frequenti su Azure Information Protection](faqs.md) </br> [Problemi noti - Azure Information Protection](known-issues.md)       |
|**Opzioni di supporto**     | [Opzioni di supporto per Azure Information Protection](information-support.md)        |
|**Yammer**     |  [Azure Information Protection](https://www.yammer.com/AskIPTeam)       |
|**Novità**     | Per le nuove funzionalità correlate a AIP, vedere l'interfaccia di amministrazione di Microsoft 365 e SharePoint:   </br>- [Novità dell'interfaccia di amministrazione di Microsoft 365](/microsoft-365/admin/whats-new-in-preview) </br>- [Novità dell'interfaccia di amministrazione di SharePoint](/sharepoint/what-s-new-in-admin-center)     |
|     |         |

#### <a name="top-ignite-sessions"></a>Principali sessioni Ignite

Vedere le sessioni seguenti registrate da Ignite 2020:

- [Supercharge information protection and governance across cloud, on-premise, endpoints and remote work environments](https://myignite.microsoft.com/sessions/ceba117f-9bc7-4426-9ebc-753d94c6a476) (Potenziare la governance e la protezione delle informazioni in ambienti cloud, locali, endpoint e di lavoro remoto)

- [Be a risk management hero with intelligent data protection and compliance solutions](https://myignite.microsoft.com/sessions/9a1e2716-55f5-4c3e-8626-0cb77e60eb87) (Diventare un eroe della gestione dei rischi con soluzioni intelligenti per la protezione dati e la conformità)

- [Know your data, protect your data and prevent data loss with Microsoft Information Protection](https://myignite.microsoft.com/sessions/46ff69cf-2c8f-4e61-a923-f72f5740f02f) (Conoscere i dati, proteggerli e prevenirne la perdita con Microsoft Information Protection)

- [Ask the Expert: Ask anything about Microsoft Compliance: information protection & governance, insider risks, Compliance Management, and more](https://myignite.microsoft.com/sessions/5ce48b36-9827-4d60-8540-90546333063d) (Chiedi all'esperto - Domande sulla conformità Microsoft: protezione e governance delle informazioni, rischi interni, gestione della conformità e altro ancora)
## <a name="aips-classic-client"></a>Client classico di AIP

Il client classico di Azure Information Protection è la versione precedente di AIP e consente agli amministratori di gestire le etichette di classificazione direttamente nel portale di Azure.

Le etichette di AIP gestite nel portale di Azure *non* sono supportate dalla piattaforma di etichettatura unificata, sono limitate all'uso con il client e lo scanner di Azure Information Protection e Microsoft Cloud App Security. 

È consigliabile eseguire la migrazione al client di etichettatura unificata per supportare queste funzionalità, oltre a SharePoint, Microsoft 365 Apps, Outlook per il Web e i dispositivi mobili, la protezione dei dati di Power BI e altro ancora. Per altre informazioni, vedere [Esercitazione: Migrazione dal client classico al client di etichettatura unificata di Azure Information Protection (AIP)](tutorial-migrating-to-ul.md).

>[!NOTE] 
> Per offrire un'esperienza per i clienti unificata e semplificata, il **client classico di Azure Information Protection** e **Gestione etichette** nel portale di Azure saranno **deprecati** a partire dal **31 marzo 2021**. 
>
> In questo intervallo di tempo tutti i clienti correnti di Azure Information Protection possono passare all'etichettatura unificata usando la soluzione di etichettatura unificata di Microsoft Information Protection. Altre informazioni nell'[avviso ufficiale sulla deprecazione](https://aka.ms/aipclassicsunset).
