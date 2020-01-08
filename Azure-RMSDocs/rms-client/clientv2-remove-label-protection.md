---
title: Rimuovere le etichette usando il client Azure Information Protection Unified Labeling
description: Istruzioni su come rimuovere le etichette di riservatezza e la protezione da file e messaggi di posta elettronica usando il Azure Information Protection client Unified labeling.
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 11/24/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: ''
ms.subservice: v2client
ms.suite: ems
ms.custom: user
ms.openlocfilehash: 83ab06748ade003ea39d2fb15fde6d43acb3c5ad
ms.sourcegitcommit: 40693000ce86110e14ffce3b553e42149d6b7dc2
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/22/2019
ms.locfileid: "75326559"
---
# <a name="user-guide-remove-labels-and-protection-from-files-and-emails-that-have-been-labeled-by-azure-information-protection"></a>Guida dell'utente: rimuovere etichette e protezione da file e messaggi di posta elettronica che sono stati etichettati da Azure Information Protection

>*Si applica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8, Windows 7 con SP1*
>
> *Istruzioni per: [Azure Information Protection client di etichetta unificata per Windows](../faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*

Quando il Azure Information Protection client unificato è [installato nel computer](install-client-app.md), è possibile rimuovere le etichette di riservatezza e la protezione da file e messaggi di posta elettronica.

Quando l'etichetta di riservatezza da rimuovere è configurata per applicare la protezione, questa azione rimuove anche la protezione dal file. Potrebbe essere richiesto di registrare il motivo della rimozione dell'etichetta.

> [!IMPORTANT]
> Per rimuovere la protezione, è necessario essere il proprietario del file oppure aver ricevuto le autorizzazioni per la rimozione della protezione (autorizzazione **Esporta** o **Controllo completo** di Rights Management).

Se si vuole scegliere un'altra etichetta o un set diverso di impostazioni di protezione, non è necessario rimuovere l'etichetta o la protezione. Scegliere invece una nuova etichetta e, se necessario, è possibile definire autorizzazioni personalizzate usando Esplora file. 

È possibile rimuovere etichette e protezione da documenti e messaggi di posta elettronica di Office quando questi vengono ricreati o modificati nelle app desktop di Office, come **Word**, **Excel**, **PowerPoint** e **Outlook**. 

È anche possibile rimuovere etichette e protezione tramite **Esplora file**, che supporta altri tipi di file ed è un pratico strumento per rimuovere etichette e protezione da più file contemporaneamente.

## <a name="using-office-apps-to-remove-labels-and-protection-from-documents-and-emails"></a>Uso delle app di Office per rimuovere etichette e protezione da documenti e messaggi di posta elettronica

Nella scheda **Home** selezionare il pulsante **sensibilità** sulla barra multifunzione e deselezionare l'etichetta attualmente selezionata.

In alternativa, se è stata selezionata l'opzione **Mostra barra** dal pulsante **sensibilità** , è possibile selezionare l'icona **Elimina etichetta** dalla barra Azure Information Protection:

![Barra di Azure Information Protection - Elimina l'etichetta](../media/v2delete-label.png)

Se l'icona **Elimina etichetta** non è immediatamente disponibile, selezionare prima l'icona **Modifica etichetta** :

![Barra di Azure Information Protection - Modifica l'etichetta](../media/v2edit-label.png)

Se l'icona **Elimina etichetta** non è ancora visualizzata, l'amministratore non consente di usare questa opzione perché tutti i documenti e i messaggi di posta elettronica devono avere un'etichetta.

## <a name="using-file-explorer-to-remove-labels-and-protection-from-files"></a>Uso di Esplora file per rimuovere etichette e protezione dai file

Quando si usa Esplora file, è possibile rimuovere rapidamente etichette e protezione da un singolo file, più file o una cartella. Quando si seleziona una cartella, vengono selezionati automaticamente tutti i file e tutte le sottocartelle al suo interno. 

1. In Esplora File selezionare un file, più file o una cartella. Fare clic con il pulsante destro del mouse e scegliere **Classifica e proteggi**.

2. Per rimuovere un'etichetta: nella finestra di dialogo **Classifica e proteggi - Azure Information Protection** fare clic su **Elimina l'etichetta**. Se l'etichetta è stata configurata per l'applicazione della protezione, la protezione viene automaticamente rimossa.

3. Per rimuovere protezione personalizzata da un singolo file: nella finestra di dialogo **Classifica e proteggi - Azure Information Protection** deselezionare l'opzione **Proteggi con autorizzazioni personalizzate**. 

4. Per rimuovere protezione personalizzata da più file: nella finestra di dialogo **Classifica e proteggi - Azure Information Protection** fare clic su **Rimuovi le autorizzazioni personalizzate**.

5. Fare clic su **Applica** e attendere la visualizzazione del messaggio **Operazione completata** per vedere i risultati. e quindi fare clic su **Chiudi**.


## <a name="other-instructions"></a>Altre istruzioni
Ulteriori procedure nella Guida per l'utente di Azure Information Protection:

- [Per saperne di più](client-user-guide.md#what-do-you-want-to-do)

## <a name="additional-information-for-administrators"></a>Informazioni aggiuntive per gli amministratori    

Vedere [Panoramica delle etichette di riservatezza](/microsoft-365/compliance/sensitivity-labels).

