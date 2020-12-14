---
title: Classificazione tramite il client di etichettatura unificato di Azure Information Protection
description: Istruzioni su come classificare i documenti e i messaggi di posta elettronica quando si usa il client di etichettatura unificata di Azure Information Protection per Windows.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 09/03/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: v2client
ms.suite: ems
ms.custom: user
ms.openlocfilehash: 3718c6b93fba7abb08dcbe08675f361b0b666c0d
ms.sourcegitcommit: 8a141858e494dd1d3e48831e6cd5a5be48ac00d2
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2020
ms.locfileid: "97385404"
---
# <a name="user-guide-classify-a-file-or-email-by-using-the-azure-information-protection-unified-labeling-client-for-windows"></a>Guida dell'utente: classificare un file o un messaggio di posta elettronica usando il client di etichettatura unificato di Azure Information Protection per Windows

>***Si applica a**: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8 *
>
>*Se si dispone di Windows 7 o Office 2010, vedere [AIP per le versioni di Windows e Office nel supporto esteso](../known-issues.md#aip-for-windows-and-office-versions-in-extended-support).*
>
>***Istruzioni per**: [Azure Information Protection client di etichetta unificato per Windows](../faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients). Per il client classico, vedere la [Guida per l'utente del client classico](client-classify.md). *

> [!NOTE]
> Usare queste istruzioni per classificare senza proteggere i documenti e i messaggi di posta elettronica. Se è necessario proteggere i documenti e i messaggi di posta elettronica, vedere le [istruzioni per classificare e proteggere](clientv2-classify-protect.md). Se non si sa quali istruzioni usare, rivolgersi al proprio amministratore o al supporto tecnico.

È più semplice classificare i documenti e i messaggi di posta elettronica durante la creazione o la modifica all'interno delle app desktop di Office: **Word**, **Excel**, **PowerPoint**, **Outlook**. 

Tuttavia, è anche possibile classificare i file usando **Esplora file**. Questo metodo supporta altri tipi di file ed è un modo pratico per classificare più file contemporaneamente. 

## <a name="using-office-apps-to-classify-your-documents-and-emails"></a>Uso delle app di Office per classificare documenti e messaggi di posta elettronica

Nella scheda **Home** selezionare il pulsante **sensibilità** sulla barra multifunzione e quindi selezionare una delle etichette configurate. ad esempio:

![Esempio di pulsante Sensitivity](../media/sensitivity-not-set-callout.png)

In alternativa, se è stata selezionata l'opzione **Mostra barra** dal pulsante **sensibilità** , è possibile selezionare un'etichetta dalla barra Azure Information Protection. ad esempio:

![Esempio della barra di Azure Information Protection](../media/info-protect-barv2-not-set-callout.png)

Per impostare un'etichetta, ad esempio "generale", selezionare **generale**. Se non si è certi dell'etichetta da applicare al documento o al messaggio di posta elettronica corrente, usare le descrizioni comando delle etichette per altre informazioni su ogni etichetta e su quando applicarla. 

Se al documento è già applicata un'etichetta e si desidera modificarla, è possibile selezionare un'etichetta diversa. Se è stata visualizzata la barra di Azure Information Protection e le etichette non sono visualizzate sulla barra da selezionare, fare prima clic sull'icona **Modifica etichetta** accanto al valore etichetta corrente.

Oltre a selezionare manualmente le etichette, è anche possibile applicarle nei modi seguenti:

- L'amministratore ha configurato un'etichetta predefinita che è possibile mantenere o modificare.

- L'amministratore ha configurato le etichette da impostare automaticamente quando vengono rilevate informazioni riservate.

- L'amministratore ha configurato le etichette consigliate quando vengono rilevate informazioni riservate e viene richiesto di accettare la raccomandazione (e l'etichetta viene applicata) o di rifiutarla (l'etichetta consigliata non viene applicata).

### <a name="exceptions-for-the-sensitivity-button"></a>Eccezioni per il pulsante Sensitivity

##### <a name="dont-see-the-sensitivity-button-in-your-office-apps"></a>Non viene visualizzato il pulsante Sensitivity nelle app di Office?

- Potrebbe non essere [installato](install-unifiedlabelingclient-app.md)il client di Azure Information Protection Unified labeling.

- Se non viene visualizzato un pulsante di **riservatezza** sulla barra multifunzione, ma viene visualizzato un pulsante **Proteggi** con etichette, il client Azure Information Protection classico è installato e non il Azure Information Protection client di etichetta unificata. [Altre informazioni](../faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)

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
    
    Se non è possibile selezionare alcuna etichetta (sono tutte visualizzate in grigio) significa che il file selezionato non supporta la classificazione. ad esempio:
    
    ![Nessuna etichetta disponibile nella finestra di dialogo Classifica e proteggi - Azure Information Protection**](../media/v2info-protect-dialog-labels-dimmed.png)

3. Se è stato selezionato un file non supporta la classificazione, fare clic su **Chiudi**. Non è possibile classificare il file senza proteggerlo.
    
    Se è stata selezionata un'etichetta, fare clic su **Applica** e attendere la visualizzazione del messaggio **Operazione completata** per vedere i risultati. e quindi fare clic su **Chiudi**.

Se si vuole cambiare selezionare un'altra etichetta, ripetere la procedura e scegliere un'etichetta diversa.

La classificazione specificata rimane associata al file, anche se si invia il file per posta elettronica o lo si salva in un altro percorso. 

## <a name="other-instructions"></a>Altre istruzioni

Ulteriori istruzioni sulle procedure sono disponibili nel manuale dell'utente per il client di Azure Information Protection Unified Labeling per Windows:

- [Per saperne di più](clientv2-user-guide.md#what-do-you-want-to-do)

## <a name="additional-information-for-administrators"></a>Informazioni aggiuntive per gli amministratori

Vedere [informazioni sulle etichette di riservatezza](/microsoft-365/compliance/sensitivity-labels).

