---
title: Azure Information Protection unified client - versione l'assegnazione di etichette cronologia delle versioni e criteri di supporto
description: Vedere le informazioni sulla versione del client per l'etichettatura unificata di Azure Information Protection per Windows.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 04/17/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.reviewer: maayan
ms.suite: ems
ms.openlocfilehash: 1262a2f1a70002686aed0bad47354cdc5ac23bac
ms.sourcegitcommit: fff4c155c52c9ff20bc4931d5ac20c3ea6e2ff9e
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/24/2019
ms.locfileid: "60180886"
---
# <a name="azure-information-protection-unified-labeling-client---version-release-history-and-support-policy"></a>Azure Information Protection unified client - versione l'assegnazione di etichette cronologia delle versioni e criteri di supporto

>*Si applica a: Active Directory Rights Management Services, [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8, Windows 7 con SP1, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2*
>
> *Istruzioni per: [Azure Information Protection unified client per l'assegnazione di etichette per Windows](../faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*


È possibile scaricare il client di assegnazione di etichette unificato di Azure Information Protection dal [Microsoft Download Center](https://www.microsoft.com/en-us/download/details.aspx?id=53018).

### <a name="servicing-information-and-timelines"></a>Informazioni e tempistiche di manutenzione

Ogni versione di disponibilità generale (GA) del client Azure Information Protection unified imprevisto delle etichette è supportato per un massimo di sei mesi dopo il rilascio della versione disponibile a livello generale successiva. La documentazione non include informazioni sulle versioni non supportate del client. Le correzioni e le nuove funzionalità sono sempre valide per l'ultima versione disponibile a livello generale e non verranno applicate alle versioni precedenti.

Le versioni di anteprima non devono essere distribuite agli utenti finali nelle reti di produzione, ma è possibile usare la versione di anteprima più recente per visualizzare e provare le nuove funzionalità e correzioni che saranno disponibili nella prossima versione disponibile a livello generale. Non sono supportate le versioni di anteprima non aggiornate.

> [!NOTE]
> Per il supporto tecnico, vedere le informazioni riportate in [Opzioni di supporto e risorse per la community](../information-support.md#support-options-and-community-resources). È anche possibile rivolgersi al team di Azure Information Protection nel [sito di Yammer](https://www.yammer.com/askipteam/).

### <a name="release-information"></a>Informazioni sulla versione

Usare le informazioni seguenti per vedere cosa è supportato per la versione con disponibilità generale del client Azure Information Protection unified imprevisto delle etichette.

Il client installa un componente aggiuntivo di Office per i computer Windows, un'estensione per Esplora File e un modulo di PowerShell. Questo client ha gli stessi [prerequisiti](../requirements.md) del client Azure Information Protection che scarica i criteri da Azure.

Per confrontare funzioni e funzionalità con quelle del client Azure Information Protection, vedere [Confronto delle funzionalità dei client](use-client.md#compare-the-clients).

## <a name="version-20778"></a>Versione 2.0.778

**Data di rilascio**: 04/16/2019

Questa prima versione di disponibilità generale del client di assegnazione di etichette unificata di Azure Information Protection per Windows supporta le funzionalità seguenti: 

- Aggiornamento dal client Azure Information Protection.

- Assegnazione di etichette manuale, automatica e consigliata: Per altre informazioni sulla configurazione dell'assegnazione di etichette automatica e consigliata per questo client, vedere [Applicare automaticamente un'etichetta di riservatezza al contenuto](/Office365/SecurityCompliance/apply_sensitivity_label_automatically).

- Esplora file, azioni con il pulsante destro del mouse per classificare e proteggere i file, rimuovere la protezione e applicare autorizzazioni personalizzate.

- Un visualizzatore per file di testo e di immagine protetti, file PDF protetti e file protetti in modo generico.

- Comandi di PowerShell seguenti per le seguenti operazioni:
    - [Impostare o rimuovere un'etichetta in un documento](/powershell/module/azureinformationprotection/set-aipfilelabel)
    - [Applicare un'etichetta a un documento dopo averne esaminato il contenuto](/powershell/module/azureinformationprotection/set-aipfileclassification)
    - [Leggere le informazioni dell'etichetta applicate a un documento](/powershell/module/azureinformationprotection/get-aipfilestatus)
    - [Eseguire l'autenticazione per supportare le sessioni automatiche di PowerShell](/powershell/module/azureinformationprotection/set-aipauthentication)

- Il supporto di individuazione dati e l'endpoint per il reporting centralizzato tramite del controllo [analitica di Azure Information Protection](../reports-aip.md).

- Le impostazioni seguenti per etichette e criteri:
    - Contrassegno visivo (intestazioni, piè di pagina, filigrane)
    - Etichettatura predefinita
    - Etichette che applicano Non inoltrare e vengono visualizzate solo in Outlook
    - Richieste di giustificazione se gli utenti abbassano il livello di classificazione o rimuovono un'etichetta
    - Colori per le etichette

- Aggiornamento di criteri dai centri di amministrazione:
    - Ogni volta che viene avviata un'app Office e ogni 4 ore
    - Quando si fa clic con il pulsante destro del mouse per classificare e proteggere un file o una cartella
    - Quando si eseguono i cmdlet di PowerShell per l'assegnazione di etichette e la protezione

- Una finestra di dialogo Guida e commenti che include impostazioni per il ripristino e l'esportazione di log.


## <a name="next-steps"></a>Passaggi successivi

Per informazioni dettagliate, vedere le [tabelle di confronto](use-client.md#compare-the-clients).

Per altre informazioni sull'installazione e l'utilizzo di questo client: 

- Per gli utenti: [Scaricare e installare il client](install-unifiedlabelingclient-app.md)

- Per gli amministratori: [Azure Information Protection unified Guida dell'amministratore client l'assegnazione di etichette](clientv2-admin-guide.md)

