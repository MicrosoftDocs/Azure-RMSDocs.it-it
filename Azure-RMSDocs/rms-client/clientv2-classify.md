---
title: Classificazione tramite il client di assegnazione di etichette unificato di Azure Information Protection
description: Istruzioni classificare i documenti e messaggi di posta elettronica quando si usa Azure Information Protection client per l'assegnazione di etichette per Windows unificata.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 04/17/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.suite: ems
ms.openlocfilehash: c7ec1c5f6a929d9b6b810b647e6cb6dbe3c42316
ms.sourcegitcommit: f9077101a974459a4252e763b5fafe51ff15a16f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/28/2019
ms.locfileid: "64767967"
---
# <a name="user-guide-classify-a-file-or-email-by-using-the-azure-information-protection-unified-labeling-client-for-windows"></a>Manuale dell'utente: Classificare un file o un messaggio di posta elettronica usando il client di assegnazione di etichette unificato di Azure Information Protection per Windows

>*Si applica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8, Windows 7 con SP1*
>
> *Istruzioni per: [Azure Information Protection unified client per l'assegnazione di etichette per Windows](../faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*

> [!NOTE]
> Usare queste istruzioni per classificare senza proteggere i documenti e i messaggi di posta elettronica. Se è necessario proteggere i documenti e i messaggi di posta elettronica, vedere le [istruzioni per classificare e proteggere](clientv2-classify-protect.md). Se non si sa quali istruzioni usare, rivolgersi al proprio amministratore o al supporto tecnico.

È più semplice classificare i documenti e i messaggi di posta elettronica durante la creazione o la modifica all'interno delle app desktop di Office: **Word**, **Excel**, **PowerPoint**, **Outlook**. 

Tuttavia, è anche possibile classificare i file usando **Esplora file**. Questo metodo supporta altri tipi di file ed è un modo pratico per classificare più file contemporaneamente. 

## <a name="using-office-apps-to-classify-your-documents-and-emails"></a>Uso delle app di Office per classificare documenti e messaggi di posta elettronica

Dal **Home** scheda, seleziona la **sensibilità** nella barra multifunzione e quindi selezionare una delle etichette che è stato configurato per l'utente. Ad esempio: 

![Esempio di pulsante di sensibilità](../media/sensitivity-not-set-callout.png)

Oppure, se si è scelto **Mostra barra** dal **sensibilità** pulsante, è possibile selezionare un'etichetta dalla barra di Azure Information Protection. Ad esempio: 

![Esempio della barra di Azure Information Protection](../media/info-protect-barv2-not-set-callout.png)

Per impostare un'etichetta, ad esempio "Generale", selezionare **generali**. Se non si è certi dell'etichetta da applicare al documento o al messaggio di posta elettronica corrente, usare le descrizioni comando delle etichette per altre informazioni su ogni etichetta e su quando applicarla. 

Se al documento è già applicata un'etichetta e si desidera modificarla, è possibile selezionare un'etichetta diversa. Se è stato visualizzato la barra Azure Information Protection e le etichette non vengono visualizzate sulla barra per poter selezionare, fare clic il **modifica l'etichetta** sull'icona accanto al valore di etichetta corrente.

Oltre a selezionare manualmente le etichette, è anche possibile applicarle nei modi seguenti:

- L'amministratore ha configurato un'etichetta predefinita che è possibile mantenere o modificare.

- L'amministratore configurato etichette impostato automaticamente quando viene rilevate le informazioni riservate.

- L'amministratore ha configurato consigliato etichette quando viene rilevate le informazioni riservate e viene richiesto di accettare il suggerimento (e viene applicata l'etichetta), o rifiutarlo (l'etichetta consigliata non viene applicata).

### <a name="exceptions-for-the-sensitivity-button"></a>Eccezioni per il pulsante di sensibilità

##### <a name="dont-see-the-sensitivity-button-in-your-office-apps"></a>Il pulsante tra maiuscole e minuscole nelle app di Office non è visualizzato?

- Il client di assegnazione di etichette unificato di Azure Information Protection non si dispone [installato](install-unifiedlabelingclient-app.md).

- Se non viene visualizzata una **sensibilità** nella barra multifunzione, ma viene visualizzato un **Proteggi** pulsante invece con le etichette, aver installato il client Azure Information Protection e non di Azure Information Protection client unificato di assegnazione di etichette. [Altre informazioni](../faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)

##### <a name="is-the-label-that-you-expect-to-see-not-displayed"></a>Un'etichetta che ci si aspetta di vedere non è visualizzata? 

- Se l'amministratore ha configurato di recente una nuova etichetta, provare a chiudere tutte le istanze dell'app di Office e riaprirle. In questo modo, verrà eseguito un controllo della presenza di modifiche alle etichette.

- L'etichetta potrebbe essere in un criterio con ambito che non include l'account in uso. Rivolgersi all'help desk o all'amministratore.


## <a name="using-file-explorer-to-classify-files"></a>Uso di Esplora file per classificare i file

Quando si usa Esplora file, è possibile classificare rapidamente un singolo file, più file o una cartella. 

Quando si seleziona una cartella, tutti i file nella cartella e tutte le relative sottocartelle vengono selezionate automaticamente per la classificazione impostata. Tuttavia, i nuovi file creati nella cartella o nelle sottocartelle non vengono classificati automaticamente.

Quando si usa Esplora file per classificare i file, se una o più etichette vengono visualizzate in grigio, i file selezionati non supportano la classificazione senza protezione.

La guida dell'amministratore include l'elenco completo dei tipi di file che supportano la classificazione senza protezione: [Tipi di file supportati solo per la classificazione](clientv2-admin-guide-file-types.md#file-types-supported-for-classification-only).

### <a name="to-classify-a-file-by-using-file-explorer"></a>Per classificare un file mediante Esplora file

1. In Esplora File selezionare un file, più file o una cartella. Fare clic con il pulsante destro del mouse e scegliere **Classifica e proteggi**. Ad esempio: 
    
    ![Comando Classifica e proteggi nel menu di scelta rapida in Esplora file con Azure Information Protection](../media/right-click-classify-protect-folder.png)

2. Nella finestra di dialogo **Classifica e proteggi - Azure Information Protection** usare le etichette in modo analogo a un'applicazione di Office che consente di impostare la classificazione definita dall'amministratore. 
    
    Se nessuna delle etichette può essere selezionata (sono visualizzate in grigio): il file selezionato non supporta la classificazione. Ad esempio:
    
    ![Nessuna etichetta disponibile nella finestra di dialogo Classifica e proteggi - Azure Information Protection**](../media/v2info-protect-dialog-labels-dimmed.png)

3. Se è stato selezionato un file non supporta la classificazione, fare clic su **Chiudi**. Non è possibile classificare il file senza proteggerlo.
    
    Se è stata selezionata un'etichetta, fare clic su **Applica** e attendere la visualizzazione del messaggio **Operazione completata** per vedere i risultati. e quindi fare clic su **Chiudi**.

Se si vuole cambiare selezionare un'altra etichetta, ripetere la procedura e scegliere un'etichetta diversa.

La classificazione specificata rimane associata al file, anche se si invia il file per posta elettronica o lo si salva in un altro percorso. 

## <a name="other-instructions"></a>Altre istruzioni

Guidano per altre istruzioni sulle procedure da parte dell'utente per il client di assegnazione di etichette unificato di Azure Information Protection per Windows:

- [Per saperne di più](clientv2-user-guide.md#what-do-you-want-to-do)

## <a name="additional-information-for-administrators"></a>Informazioni aggiuntive per gli amministratori

Visualizzare [Panoramica di etichette di riservatezza](/Office365/SecurityCompliance/sensitivity-labels).

