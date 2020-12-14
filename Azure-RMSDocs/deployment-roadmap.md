---
title: Guida di orientamento per la distribuzione di Azure Information Protection
description: Per preparare l'ambiente e per implementare e gestire Azure Information Protection per l'organizzazione, eseguire questa procedura.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 06/10/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 086600c2-c5d8-47ec-a4c0-c782e1797486
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 251b193012dc32518a0a236cf1ee751545d4391e
ms.sourcegitcommit: 8a141858e494dd1d3e48831e6cd5a5be48ac00d2
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2020
ms.locfileid: "97382395"
---
# <a name="azure-information-protection-deployment-roadmap"></a>Guida di orientamento per la distribuzione di Azure Information Protection

>***Si applica a**: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*
>
>***Pertinente per**: [AIP Unified Labeling client e client classico](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*


>[!NOTE] 
> Per offrire un'esperienza utente unificata e semplificata, **Azure Information Protection** la gestione classica di client e **etichette** nel portale di Azure verrà **deprecata** a partire dal **31 marzo 2021**. In questo intervallo di tempo tutti i clienti correnti di Azure Information Protection possono passare alla soluzione di etichettatura unificata usando la piattaforma di etichettatura unificata di Microsoft Information Protection. Altre informazioni nell'[avviso ufficiale sulla deprecazione](https://aka.ms/aipclassicsunset).

> [!TIP]
> In alternativa, è possibile cercare uno degli articoli seguenti:
> - [Guide pratiche per scenari comuni che usano Azure Information Protection](how-to-guides.md)
>- [Roadmap della versione Azure Information Protection](information-support.md#information-about-new-releases-and-updates)

Utilizzare i passaggi nelle pagine di roadmap seguenti come consigli per la preparazione, l'implementazione e la gestione di Azure Information Protection per la propria organizzazione.

## <a name="identify-your-deployment-roadmap"></a>Identificare la guida di orientamento per la distribuzione

Prima di distribuire AIP, esaminare i [requisiti di sistema per AIP](./requirements.md).

Scegliere quindi una delle roadmap seguenti, a seconda delle esigenze e della [sottoscrizione](https://azure.microsoft.com/pricing/details/information-protection/)dell'organizzazione:

- **Usare la classificazione, l'assegnazione di etichette e la protezione**:

    Consigliato per tutti i clienti con una sottoscrizione di supporto. Funzionalità aggiuntive includono l'individuazione di informazioni riservate e l'assegnazione di etichette a documenti e messaggi di posta elettronica per la classificazione 

    Le etichette possono anche applicare la protezione, semplificando questo passaggio per gli utenti. 

    Questa roadmap è supportata sia per le etichette AIP create con il client classico sia per le etichette di riservatezza che usano la [piattaforma di assegnazione di etichette unificata](faqs.md#how-can-i-determine-if-my-tenant-is-on-the-unified-labeling-platform).

    Per ulteriori informazioni, vedere [la pagina relativa alla roadmap AIP per classificare, etichettare e proteggere i dati](deployment-roadmap-classify-label-protect.md).

- **Usa solo la protezione**: 

    Consigliato per i clienti con una sottoscrizione che non supporta la classificazione e le etichette, ma supporta la protezione senza etichette. È necessario che sia installato il client classico.

    Per altre informazioni, vedere [la roadmap di AIP solo per la protezione dei dati](deployment-roadmap-protect-only.md).

## <a name="next-steps"></a>Passaggi successivi

Quando si distribuisce Azure Information Protection, potrebbe essere utile consultare le [domande frequenti](faqs.md)e la pagina [informazioni e supporto](information-support.md) per ulteriori risorse.