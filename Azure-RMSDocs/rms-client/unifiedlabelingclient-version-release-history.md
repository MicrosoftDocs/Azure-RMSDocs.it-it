---
title: "Client per l'etichettatura unificata di Azure Information Protection: informazioni di rilascio versione"
description: Vedere le informazioni sulla versione del client per l'etichettatura unificata di Azure Information Protection per Windows.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 10/23/2018
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.reviewer: maayan
ms.suite: ems
ms.openlocfilehash: 939ae3e367b14f722c38be023c70d9dcce21004f
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/14/2019
ms.locfileid: "56254833"
---
# <a name="azure-information-protection-unified-labeling-client-version-release-information"></a>Client per l'etichettatura unificata di Azure Information Protection: informazioni sulla versione

>*Si applica a: Active Directory Rights Management Services, [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8, Windows 7 con SP1, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2*

> [!NOTE]
> Questo client è in anteprima e soggetto a modifiche. Usa l'archivio di etichettatura unificata e scarica i criteri con etichette dal Centro sicurezza e conformità di Office 365. [Altre informazioni](/Office365/SecurityCompliance/sensitivity-labels)

È possibile scaricare la versione di anteprima più recente del client per l'etichettatura unificata di Azure Information Protection dall'[Area download Microsoft](https://www.microsoft.com/en-us/download/details.aspx?id=57440).

### <a name="release-information"></a>Informazioni sulla versione

Usare le informazioni seguenti per vedere il supporto offerto dalla versione di anteprima più recente del client per l'etichettatura unificata di Azure Information Protection. 

Questo client viene installato come un componente aggiuntivo di Office per i computer Windows e ha gli stessi [prerequisiti](../requirements.md) del client Azure Information Protection che scarica i criteri da Azure.

## <a name="current-preview-version"></a>Versione di anteprima corrente

**Data di rilascio**: 16/10/2018

Questa versione di anteprima del client per l'etichettatura unificata di Azure Information Protection per Windows supporta le funzionalità seguenti: 

- Aggiornamento dal client di Azure Information Protection

- Etichettatura manuale che applica la classificazione e protezione per Word, Excel, PowerPoint e Outlook.

- Contrassegno visivo (intestazioni, piè di pagina, filigrane)

- Etichettatura predefinita 

- Etichette che applicano Non inoltrare

- Richieste di giustificazione se gli utenti abbassano il livello di riservatezza

- Finestra di dialogo Guida e commenti che include impostazioni per il ripristino e l'esportazione di log

- Aggiornamento di criteri dal Centro sicurezza e conformità ogni 4 ore, per ogni app di Office.

Questa versione di anteprima non supporta le funzionalità seguenti:

- Classificazione automatica e consigliata

- Autorizzazioni personalizzate

- Un visualizzatore per file di testo e di immagine protetti, file PDF protetti e file protetti in modo generico

- Esplora file, azioni eseguite tramite il pulsante destro del mouse per classificare e proteggere file

- Comandi di PowerShell per classificare e proteggere i file dalla riga di comando

- Lo scanner per individuare, etichettare e proteggere i file negli archivi dati locali

- Supporto per lingue diverse dall'inglese

## <a name="instructions"></a>Istruzioni

1. Installare il client usando le istruzioni seguenti: [Manuale dell'utente: Scaricare e installare il client di Azure Information Protection (anteprima)](install-unifiedlabelingclient-app.md) 

2. Usare il client nelle app di Office come nel client Azure Information Protection, con l'eccezione del pulsante della barra multifunzione di Office che è denominato **Sensibilità** anziché **Proteggi**:
    
    - [Classificare un file o un messaggio di posta elettronica](client-classify.md) 
    
    - [Classificare e proteggere un file o un messaggio di posta elettronica](client-classify-protect.md)

3. Condividere l'esperienza: 
    
    - Per inviare commenti e suggerimenti o porre domande su questa anteprima del client, usare il [sito di Yammer per Azure Information Protection](https://www.yammer.com/AskIPTeam).
    
    - Per segnalare problemi con questo client di anteprima, usare l'opzione **Guida e commenti** del pulsante **Sensibilità** della barra multifunzione. Nella finestra di dialogo esportare i log e quindi allegare tali file di log al messaggio di posta elettronica che viene creato con l'opzione **Segnala un problema**. 

