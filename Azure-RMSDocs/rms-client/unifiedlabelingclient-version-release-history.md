---
title: "Client per l'etichettatura unificata di Azure Information Protection: informazioni di rilascio versione"
description: Vedere le informazioni sulla versione del client per l'etichettatura unificata di Azure Information Protection per Windows.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 02/28/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.reviewer: maayan
ms.suite: ems
ms.openlocfilehash: 699e2807c700b90b98bbc855dd8792aa607696f3
ms.sourcegitcommit: 8ba63c0f4cd7d2ad7614af4ea9cfe8aec7fac4c0
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/27/2019
ms.locfileid: "56956254"
---
# <a name="azure-information-protection-unified-labeling-client-version-release-information"></a>Client per l'etichettatura unificata di Azure Information Protection: informazioni sulla versione

>*Si applica a: Active Directory Rights Management Services, [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8, Windows 7 con SP1, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2*

> [!NOTE]
> Questo client è in anteprima e soggetto a modifiche. Usa l'archivio di etichettatura unificata e scarica i criteri con etichette dal Centro sicurezza e conformità di Office 365. [Altre informazioni](/Office365/SecurityCompliance/sensitivity-labels)

È possibile scaricare la versione di anteprima più recente del client per l'etichettatura unificata di Azure Information Protection dall'[Area download Microsoft](https://www.microsoft.com/en-us/download/details.aspx?id=57440).

### <a name="release-information"></a>Informazioni sulla versione

Usare le informazioni seguenti per vedere il supporto offerto dalla versione di anteprima più recente del client per l'etichettatura unificata di Azure Information Protection.

Il client installa un componente aggiuntivo di Office per i computer Windows, un'estensione per Esplora File e un modulo di PowerShell. Questo client ha gli stessi [prerequisiti](../requirements.md) del client Azure Information Protection che scarica i criteri da Azure.

Per confrontare funzioni e funzionalità con quelle del client Azure Information Protection, vedere [Confronto delle funzionalità dei client](use-client.md#feature-comparisons-for-the-clients).

## <a name="current-preview-version"></a>Versione di anteprima corrente

**Data di rilascio**: 25/02/2019

Questa versione di anteprima del client per l'etichettatura unificata di Azure Information Protection per Windows supporta le funzionalità seguenti: 

- Aggiornamento dal client Azure Information Protection.

- Assegnazione di etichette manuale, automatica e consigliata: Usare l'**applicazione automatica di etichette** del Centro sicurezza e conformità di Office 365 per configurare l'applicazione di etichette automatica e consigliata. Per altre informazioni, vedere [Applicare automaticamente un'etichetta di riservatezza al contenuto](/Office365/SecurityCompliance/apply_sensitivity_label_automatically).

- Esplora file, azioni con il pulsante destro del mouse per classificare e proteggere i file, rimuovere la protezione e applicare autorizzazioni personalizzate.

- Un visualizzatore per file di testo e di immagine protetti, file PDF protetti e file protetti in modo generico.

- Comandi di PowerShell seguenti per le seguenti operazioni:
    - [Impostare o rimuovere un'etichetta in un documento](/powershell/module/azureinformationprotection/set-aipfilelabel)
    - [Applicare un'etichetta a un documento dopo averne esaminato il contenuto](/powershell/module/azureinformationprotection/set-aipfileclassification)
    - [Leggere le informazioni dell'etichetta applicate a un documento](/powershell/module/azureinformationprotection/get-aipfilestatus)
    - [Eseguire l'autenticazione per supportare le sessioni automatiche di PowerShell](/powershell/module/azureinformationprotection/set-aipauthentication)

- Supporto per la creazione di report centrale con l'[analisi di Azure Information Protection](../reports-aip.md).

- Le impostazioni seguenti per etichette e criteri:
    - Contrassegno visivo (intestazioni, piè di pagina, filigrane)
    - Etichettatura predefinita
    - Etichette che applicano Non inoltrare e vengono visualizzate solo in Outlook
    - Richieste di giustificazione se gli utenti abbassano il livello di classificazione o rimuovono un'etichetta
    - Colori per le etichette

- Aggiornamento di criteri dal Centro sicurezza e conformità:
    - Ogni volta che viene avviata un'app Office e ogni 4 ore
    - Quando si fa clic con il pulsante destro del mouse per classificare e proteggere un file o una cartella
    - Quando si eseguono i cmdlet di PowerShell per l'assegnazione di etichette e la protezione

- Una finestra di dialogo Guida e commenti che include impostazioni per il ripristino e l'esportazione di log.

### <a name="features-that-do-not-work-in-this-preview-version-or-are-not-available"></a>Funzionalità che non funzionano in questa versione di anteprima o non sono disponibili

Include:

- Lo scanner per individuare, etichettare e proteggere i file negli archivi dati locali non è disponibile.

- Le etichette di cui viene eseguita la migrazione dal portale di Azure e che sono configurate per la protezione HYOK vengono visualizzate nel client quando vengono pubblicate, ma non applicano la protezione.

- Non è disponibile il set completo di cmdlet del modulo AzureInformationProtection, che include i cmdlet che si connettono direttamente a un servizio di protezione. Ad esempio, Unprotect-RMSFile per rimuovere la protezione dai file in blocco.

Per informazioni dettagliate, vedere le [tabelle di confronto](use-client.md#feature-comparisons-for-the-clients).

## <a name="instructions"></a>Istruzioni

1. Installare il client usando le istruzioni seguenti: [Manuale dell'utente: Scaricare e installare il client di Azure Information Protection (anteprima)](install-unifiedlabelingclient-app.md) 

2. Usare il client come si farebbe con il client Azure Information Protection, con le eccezioni seguenti per le app Office:
    - Il pulsante sulla barra multifunzione di Office è denominato **Riservatezza** invece di **Proteggi**.
    - Gli amministratori non possono visualizzare la barra di Information Protection per impostazione predefinita, ma gli utenti possono visualizzarla selezionando **Mostra barra** dal pulsante **Riservatezza**. 
    - Non sono disponibili le autorizzazioni personalizzate
    - L'opzione Rileva e revoca non è disponibile
    
    Per le istruzioni per l'utente:
    
    - [Classificare un file o un messaggio di posta elettronica](client-classify.md) 
    
    - [Classificare e proteggere un file o un messaggio di posta elettronica](client-classify-protect.md)

3. Condividere l'esperienza: 
    
    - Per inviare commenti e suggerimenti o porre domande su questa anteprima del client, usare il [sito di Yammer per Azure Information Protection](https://www.yammer.com/AskIPTeam).
