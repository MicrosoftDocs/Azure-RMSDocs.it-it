---
title: Azure Information Protection la cronologia delle versioni del client classica & i criteri di supporto
description: Vedere le novità o le modifiche apportate in una versione di Azure Information Protection client classico e comprendere i criteri del ciclo di vita per il supporto.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 11/09/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: v1client
ms.reviewer: elkamins
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 4eabec082a6124689d6ef6e8c34698b73fb9162e
ms.sourcegitcommit: 8a141858e494dd1d3e48831e6cd5a5be48ac00d2
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2020
ms.locfileid: "97385727"
---
# <a name="azure-information-protection-classic-client-version-release-history-and-support-policy"></a>Azure Information Protection client classico: cronologia delle versioni e criteri di supporto


>***Si applica a**: Active Directory Rights Management Services, [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8, Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012 *
>
>***Pertinente per**: [Azure Information Protection client classico per Windows](../faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients). Per il client di assegnazione di etichette unificata, vedere [cronologia delle versioni client unificata](unifiedlabelingclient-version-release-history.md)per l'assegnazione di etichette.

> [!NOTE] 
> Per offrire un'esperienza utente unificata e semplificata, **Azure Information Protection** la gestione classica di client e **etichette** nel portale di Azure verrà **deprecata** a partire dal **31 marzo 2021**. In questo intervallo di tempo tutti i clienti correnti di Azure Information Protection possono passare alla soluzione di etichettatura unificata usando la piattaforma di etichettatura unificata di Microsoft Information Protection. Altre informazioni nell'[avviso ufficiale sulla deprecazione](https://aka.ms/aipclassicsunset).

**Per distribuire il client AIP classico**, aprire un ticket di supporto per ottenere l'accesso al download.

Per altre informazioni, vedere [Aggiornamento e gestione del client Azure Information Protection](client-admin-guide.md#upgrading-and-maintaining-the-azure-information-protection-client).

### <a name="servicing-information-and-timelines"></a>Informazioni e tempistiche di manutenzione

Ogni versione con disponibilità generale del client di Azure Information Protection è supportata per un massimo di sei mesi dopo il rilascio della versione con disponibilità generale successiva. Fatta eccezione per questa sezione, nella documentazione non sono incluse informazioni sulle versioni non supportate del client. Le correzioni e le nuove funzionalità sono sempre valide per l'ultima versione disponibile a livello generale e non verranno applicate alle versioni precedenti.

##### <a name="general-availability-versions-that-are-no-longer-supported"></a>Versioni di disponibilità generale non più supportate:

|Versione client|Data di rilascio|
|--------------|-------------|
|1.54.33.0 | 23/10/2019|
|1.53.10|07/15/2019|
|1.48.204.0|04/16/2019|
|1.41.51.0|27/11/2018|
|1.37.19.0|17/09/2018|
|1.29.5.0|26/06/2018|
|1.27.48.0|30/05/2018|
|1.26.6.0|04/17/2018|
|1.10.56.0|09/18/2017|
|1.7.210.0|06/06/2017|
|1.4.21.0|15/03/2017|
|1.3.155.2|02/08/2017|
|1.2.4.0.0|27/10/2016|
|1.1.23.0|10/01/2016|

Il formato della data usato in questa pagina è *mese/giorno/anno*.

A partire da 6/2/2019, il servizio di assegnazione di etichette per Azure Information Protection richiede connessioni che usano TLS 1,2.

Tutte le versioni client di 1.4.21.0 rilasciate 03/15/2017 supportano TLS 1,2. Le versioni client **1.3.155.2**, **1.2.4.0** e **1.1.23.0** non usano TLS 1,2 e pertanto non possono più scaricare i criteri di Azure Information Protection.

### <a name="release-history"></a>Cronologia delle versioni

Usare le informazioni seguenti per visualizzare le novità o le modifiche per una versione supportata di Azure Information Protection client classico per Windows. La versione più recente è elencata per prima.

Si noti che Azure Information Protection funzionalità sono attualmente in anteprima. Le [condizioni aggiuntive per l'anteprima di Azure](https://azure.microsoft.com/support/legal/preview-supplemental-terms/) includono termini legali aggiuntivi che si applicano a funzionalità di Azure in versione beta, anteprima o diversamente non ancora disponibili a livello generale. 

> [!NOTE]
> Dato che le correzioni di minore rilevanza non sono elencate, se si verifica un problema con il client di Azure Information Protection, è consigliabile controllare se tale problema è stato risolto con la versione disponibile a livello generale più recente. Se il problema persiste, controllare la versione di anteprima corrente (se disponibile).
>  
> Per il supporto tecnico, vedere le informazioni riportate in [Opzioni di supporto e risorse per la community](../information-support.md#support-options-and-community-resources). È anche possibile rivolgersi al team di Azure Information Protection nel [sito di Yammer](https://www.yammer.com/askipteam/).

## <a name="version-154590"></a>Versione 1.54.59.0

**Rilasciata**: 02/12/2020

Questa versione include solo correzioni. 

**Correzioni**:

- Viene risolto il problema per cui i file protetti da IQP visualizzano le opzioni **Ripristina** e/o **Salva con nome dopo la** rimozione della protezione. 

- Molti testi della descrizione comando della funzionalità del prodotto sono stati migliorati per chiarezza e facilità di comprensione. 

- Problemi relativi alla stabilità dei client quando si lavora con i file PDF protetti vengono risolti. 

- Le etichette di protezione vengono ora rimosse come previsto se l'etichetta viene eliminata nel messaggio di posta elettronica durante il processo di creazione della posta elettronica. 

## <a name="next-steps"></a>Passaggi successivi

Non si è certi che questo sia il client giusto da installare?  Vedere [scegliere la soluzione di etichettatura di Windows](use-client.md#choose-your-windows-labeling-solution).

Per altre informazioni sull'installazione e l'uso del client: 

- Per utenti: [Scaricare e installare il client](install-client-app.md)

- Per amministratori: [Guida per l'amministratore del client di Azure Information Protection](client-admin-guide.md)
