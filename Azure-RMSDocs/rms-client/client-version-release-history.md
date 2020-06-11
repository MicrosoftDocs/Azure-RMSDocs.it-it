---
title: Azure Information Protection & i criteri di supporto per la cronologia delle versioni client
description: Informazioni sugli elementi nuovi o modificati in una versione del client di Azure Information Protection per Windows e sui criteri del ciclo di vita per il supporto.
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 04/28/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: v1client
ms.reviewer: elkamins
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: bafbc183005200463ea73075f6c597cc73f61d38
ms.sourcegitcommit: f32928f7dcc03111fc72d958cda9933d15065a2b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/10/2020
ms.locfileid: "84665320"
---
# <a name="azure-information-protection-client-version-release-history-and-support-policy"></a>Client di Azure Information Protection: cronologia delle versioni e criteri per il supporto


>*Si applica a: Active Directory Rights Management Services, [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8, windows server 2019, windows server 2016, windows Server 2012 R2, windows Server 2012*
>
> *Istruzioni per: [client di Azure Information Protection per Windows](../faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*

>[!NOTE] 
> Per offrire un'esperienza per i clienti unificata e semplificata, il **client di Azure Information Protection client (versione classica)** e la **Gestione etichette** nel portale di Azure vengono **deprecati** a partire dal **31 marzo 2021**. In questo intervallo di tempo tutti i clienti correnti di Azure Information Protection possono passare alla soluzione di etichettatura unificata usando la piattaforma di etichettatura unificata di Microsoft Information Protection. Altre informazioni nell'[avviso ufficiale sulla deprecazione](https://aka.ms/aipclassicsunset).

È possibile scaricare la versione disponibile a livello generale più recente e la versione di anteprima corrente (se disponibile) dall'[Area download Microsoft](https://www.microsoft.com/download/details.aspx?id=53018). 

Dopo un breve ritardo di genere in un paio di settimane, la versione di disponibilità generale più recente è inclusa anche nel catalogo di Microsoft Update con il nome del prodotto **Microsoft Azure Information Protection**  >  **client Microsoft Azure Information Protection**e la classificazione degli **aggiornamenti**. L'inserimento nel catalogo significa che è possibile aggiornare il client tramite WSUS o Configuration Manager o altri meccanismi di distribuzione del software che usano Microsoft Update.

Per altre informazioni, vedere [Aggiornamento e gestione del client Azure Information Protection](client-admin-guide.md#upgrading-and-maintaining-the-azure-information-protection-client).

> [!TIP]
> Si è interessati all'uso del client Azure Information Protection Unified Labeling, perché le etichette vengono pubblicate dal centro sicurezza & conformità di Office 365, dal centro sicurezza Microsoft 365 o da Microsoft 365 Compliance Center? Quando si scarica e si installa il client di etichettatura unificata dall'area download Microsoft, è possibile aggiornare il client di Azure Information Protection al [client Unified Labeling](unifiedlabelingclient-version-release-history.md).

### <a name="servicing-information-and-timelines"></a>Informazioni e tempistiche di manutenzione

Ogni versione con disponibilità generale del client di Azure Information Protection è supportata per un massimo di sei mesi dopo il rilascio della versione con disponibilità generale successiva. Fatta eccezione per questa sezione, nella documentazione non sono incluse informazioni sulle versioni non supportate del client. Le correzioni e le nuove funzionalità sono sempre valide per l'ultima versione disponibile a livello generale e non verranno applicate alle versioni precedenti.

Le versioni di anteprima non devono essere distribuite agli utenti finali nelle reti di produzione, ma è possibile usare la versione di anteprima più recente per visualizzare e provare le nuove funzionalità e correzioni che saranno disponibili nella prossima versione disponibile a livello generale. Non sono supportate le versioni di anteprima non aggiornate.

##### <a name="general-availability-versions-that-are-no-longer-supported"></a>Versioni di disponibilità generale non più supportate:

|Versione client |Data di rilascio|
|--------------|-------------|
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

Tutte le versioni client di 1.4.21.0 rilasciate 03/15/2017 supportano TLS 1,2. Le versioni client **1.3.155.2**, **1.2.4.0**e **1.1.23.0** non usano TLS 1,2 e pertanto non possono più scaricare i criteri di Azure Information Protection.

### <a name="release-history"></a>Cronologia delle versioni

Usare le informazioni seguenti per visualizzare le novità o le modifiche per una versione supportata del client di Azure Information Protection per Windows. La versione più recente è elencata per prima.

> [!NOTE]
> Dato che le correzioni di minore rilevanza non sono elencate, se si verifica un problema con il client di Azure Information Protection, è consigliabile controllare se tale problema è stato risolto con la versione disponibile a livello generale più recente. Se il problema persiste, controllare la versione di anteprima corrente (se disponibile).
>  
> Per il supporto tecnico, vedere le informazioni riportate in [Opzioni di supporto e risorse per la community](../information-support.md#support-options-and-community-resources). È anche possibile rivolgersi al team di Azure Information Protection nel [sito di Yammer](https://www.yammer.com/askipteam/).

## <a name="version-154590"></a>Versione 1.54.59.0

**Rilasciata**: 12/02/2020

Questa versione include solo correzioni. 

**Correzioni**:

- Viene risolto il problema per cui i file protetti da IQP visualizzano le opzioni **Ripristina** e/o **Salva con nome dopo la** rimozione della protezione. 

- Molti testi della descrizione comando della funzionalità del prodotto sono stati migliorati per chiarezza e facilità di comprensione. 

- Problemi relativi alla stabilità dei client quando si lavora con i file PDF protetti vengono risolti. 

- Le etichette di protezione vengono ora rimosse come previsto se l'etichetta viene eliminata nel messaggio di posta elettronica durante il processo di creazione della posta elettronica. 

## <a name="version-154330"></a>Versione 1.54.33.0

**Rilasciata**: 10/23/2019

Supportato tramite 08/12/2020

Questa versione include MSIPC versione 1.0.4008.0813 del client RMS.

Questa versione include correzioni generali per la stabilità e le prestazioni.

## <a name="next-steps"></a>Passaggi successivi

Non si è certi che questo sia il client giusto da installare?  Vedere [scegliere il client di assegnazione di etichette da usare per i computer Windows](use-client.md#choose-which-labeling-client-to-use-for-windows-computers).

Per altre informazioni sull'installazione e l'uso del client: 

- Per utenti: [Scaricare e installare il client](install-client-app.md)

- Per amministratori: [Guida per l'amministratore del client di Azure Information Protection](client-admin-guide.md)
