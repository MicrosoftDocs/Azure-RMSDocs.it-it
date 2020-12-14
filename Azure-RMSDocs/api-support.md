---
title: 'Altre app che supportano le API di RMS: installazione e configurazione - AIP'
description: Informazioni su come il servizio Azure Rights Management di Azure Information Protection può supportare altre applicazioni per proteggere i dati dell'organizzazione.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 11/08/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: c50a8cbb-d12f-4a0e-bc29-74c463e6ac3e
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: fac36bf4c59608eb1393088024f39a9f936a9b5a
ms.sourcegitcommit: 8a141858e494dd1d3e48831e6cd5a5be48ac00d2
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2020
ms.locfileid: "97384010"
---
# <a name="other-applications-that-support-the-rights-management-apis"></a>Altre applicazioni che supportano le API di Rights Management

>***Si applica a**: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*
>
>***Pertinente per**: [AIP Unified Labeling client e client classico](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients). *

>[!NOTE] 
> Per offrire un'esperienza utente unificata e semplificata, **Azure Information Protection** la gestione classica di client e **etichette** nel portale di Azure verrà **deprecata** a partire dal **31 marzo 2021**. In questo intervallo di tempo tutti i clienti correnti di Azure Information Protection possono passare alla soluzione di etichettatura unificata usando la piattaforma di etichettatura unificata di Microsoft Information Protection. Altre informazioni nell'[avviso ufficiale sulla deprecazione](https://aka.ms/aipclassicsunset).

Usare le informazioni seguenti per comprendere in che modo il servizio Rights Management di Azure Azure Information Protection può supportare altre applicazioni per proteggere i dati dell'organizzazione.

Usando gli SDK di Azure Information Protection, gli sviluppatori interni di un'azienda possono scrivere applicazioni line-of-business per supportare il servizio Azure Rights Management in modalità nativa. Le modalità di integrazione della protezione delle informazioni con queste applicazioni dipende dal modo in cui queste ultime sono state scritte. L'integrazione potrebbe ad esempio essere applicata automaticamente con un intervento minimo dell'utente oppure, per un'esperienza più personalizzata, agli utenti potrebbe essere richiesto di configurare impostazioni specifiche per applicare la protezione delle informazioni ai file. Per altre informazioni, vedere la [guida per gli sviluppatori](./develop/developers-guide.md).

In modo analogo, molti fornitori di software offrono soluzioni di protezione delle informazioni, note anche come prodotti ERM (Enterprise Rights Management). Un esempio comune è quello di un lettore di file in formato PDF che supporta il servizio Azure Rights Management per piattaforme specifiche. È possibile usare la tabella in [Applicazioni che supportano la protezione dati di Azure Rights Management](./requirements-applications.md) per identificare le applicazioni che supportano Rights Management (applicazioni abilitate per RMS) e quindi usare una ricerca Web per acquistare o scaricare l'applicazione.

## <a name="next-steps"></a>Passaggi successivi

Per informazioni su come altri servizi e applicazioni supportano il servizio Azure Rights Management, vedere [Supporto del servizio Azure Rights Management da parte delle applicazioni](applications-support.md).
