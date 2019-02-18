---
title: Istruzioni per gli scenari comuni che usano Azure Information Protection.
description: Identificare i casi d'uso in cui è necessario proteggere e classificare i dati dell'organizzazione usando Azure Information Protection.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 02/13/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.reviewer: eymanor
ms.suite: ems
ms.openlocfilehash: 69ae0a504ffcdaa201b1d4ce9762b22470e05eb7
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/14/2019
ms.locfileid: "56259032"
---
# <a name="how-to-guides-for-common-scenarios-that-use-azure-information-protection"></a>Guide procedurali per gli scenari comuni che usano Azure Information Protection

>*Si applica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*

Esistono diversi modi in cui è possibile usare Azure Information Protection per classificare ed eventualmente proteggere documenti e messaggi di posta elettronica dell'organizzazione. 

Le distribuzioni più efficienti sono quelle in cui si identificano casi d'uso specifici che consentano all'organizzazione di ottenere il massimo beneficio. Usare l'elenco seguente di istruzioni e scenari comuni per eseguire avviare la procedura di distribuzione corretta.

## <a name="common-scenarios"></a>Scenari comuni

|Scenario: Opzione richiesta:|Istruzioni|
|----------------|---------------|
|Trovare le informazioni riservate che la mia organizzazione archivia in locale|[Avvio rapido: trovare le informazioni riservate presenti nei file archiviati in locale](quickstart-findsensitiveinfo.md)|
|Consentire agli utenti di proteggere facilmente i messaggi di posta elettronica contenenti informazioni riservate|[Avvio rapido: configurare un'etichetta che consente di proteggere facilmente i messaggi di posta elettronica contenenti informazioni riservate](quickstart-label-dnf-protectedemail.md)|
|Consentire agli utenti di classificare i dati nel momento in cui vengono creati o modificati e proteggerli se contengono informazioni riservate| [Esercitazione: Modificare i criteri e creare una nuova etichetta](infoprotect-quick-start-tutorial.md)|
|Consentire agli utenti di collaborare facilmente su un documento protetto|[Configurazione della collaborazione per i documenti protetti con Azure Information Protection](secure-collaboration-documents.md)|
|Proteggere automaticamente i messaggi di posta elettronica degli utenti inviati all'esterno dell'organizzazione| [Configurazione delle regole del flusso di posta per le etichette di Azure Information Protection](configure-exo-rules.md)
|Classificare e proteggere automaticamente i dati esistenti negli archivi dati locali|[Distribuzione dello scanner di Azure Information Protection](deploy-aip-scanner.md)|
|Usare la chiave personale per proteggere i dati dell'organizzazione| [Pianificazione e implementazione della chiave del tenant](plan-implement-tenant-key.md)|
|Eseguire la migrazione da AD RMS|[Migrazione da AD RMS ad Azure Information Protection](migrate-from-ad-rms-to-azure-rms.md)|

## <a name="additional-deployment-instructions"></a>Istruzioni aggiuntive per la distribuzione

Nel [blog tecnico di Azure Information Protection](https://aka.ms/AIPblog) sono disponibili altre linee guida dal team di Analisi utilizzo software.

Ad esempio, una metodologia con le procedure consigliate per i decisori aziendali e i responsabili dell'implementazione IT:

- [Azure Information Protection Deployment Acceleration Guide](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/Azure-Information-Protection-Deployment-Acceleration-Guide/ba-p/334423) (Guida per velocizzare l'adozione e la distribuzione di Azure Information Protection)

Istruzioni dettagliate:

- [Uso di Azure Information Protection per proteggere i file PDF e di Adobe Acrobat Reader per visualizzarli](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/Using-Azure-Information-Protection-to-protect-PDF-s-and-Adobe/ba-p/282010)

- [Catalogazione dei dati sensibili con Azure Information Protection, anche prima di configurare le etichette](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/Cataloging-your-Sensitive-Data-with-AIP-Even-Before-Configuring/ba-p/267241)

- [Installazione rapida dello scanner di Azure Information Protection](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/Azure-Information-Protection-Scanner-Express-Installation/ba-p/265424)

- [Individuazione dei dati sensibili con lo scanner di Azure Information Protection (Azure Information Protection Premium P1)](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/Discovery-of-Sensitive-Data-Using-the-AIP-Scanner-AIP-Premium-P1/ba-p/252040)

## <a name="next-steps"></a>Passaggi successivi

Se il proprio scenario non è presente nell'elenco, consultare l'articolo [Guida di orientamento per la distribuzione](deployment-roadmap.md) per un elenco completo dei passaggi di pianificazione e distribuzione.

Se non si ha familiarità con Azure Information Protection, prima di iniziare la distribuzione consultare l'articolo [Che cos'è Azure Information Protection?](what-is-information-protection.md) per una rapida introduzione al servizio.
