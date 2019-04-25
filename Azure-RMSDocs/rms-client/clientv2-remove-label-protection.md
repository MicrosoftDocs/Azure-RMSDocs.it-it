---
title: Rimuovere etichette di riservatezza usando il client di assegnazione di etichette unificato di Azure Information Protection per Windows
description: Istruzioni per rimuovere etichette di riservatezza e protezione da file che sono stati etichettati tramite Azure Information Protection.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 04/17/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: ''
ms.suite: ems
ms.openlocfilehash: 187c36acddb8a6b2e5b1451500640dfd832a8f3f
ms.sourcegitcommit: fff4c155c52c9ff20bc4931d5ac20c3ea6e2ff9e
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/24/2019
ms.locfileid: "60181135"
---
# <a name="user-guide-remove-labels-and-protection-from-files-and-emails-that-have-been-labeled-by-azure-information-protection"></a>Manuale dell'utente: Rimuovere etichette e protezione da file e messaggi di posta elettronica che sono stati etichettati tramite Azure Information Protection

>*Si applica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8, Windows 7 con SP1*
>
> *Istruzioni per: [Azure Information Protection unified client per l'assegnazione di etichette per Windows](../faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*

Quando il client unificato di Azure Information Protection è [installata nel computer](install-client-app.md), è possibile rimuovere etichette di riservatezza e protezione da file e messaggi di posta elettronica.

Quando l'etichetta di riservatezza da eliminare è configurato per applicare la protezione, questa azione rimuove anche la protezione dal file. Potrebbe essere richiesto di registrare il motivo della rimozione dell'etichetta.

> [!IMPORTANT]
> Per rimuovere la protezione, è necessario essere il proprietario del file oppure aver ricevuto le autorizzazioni per la rimozione della protezione (autorizzazione **Esporta** o **Controllo completo** di Rights Management).

Se si vuole scegliere un'altra etichetta o un set diverso di impostazioni di protezione, non è necessario rimuovere l'etichetta o la protezione. Al contrario, scegliere una nuova etichetta e se necessario, è possibile definire autorizzazioni personalizzate usando Esplora File. 

È possibile rimuovere etichette e protezione da documenti e messaggi di posta elettronica di Office quando questi vengono ricreati o modificati nelle app desktop di Office: **Word**, **Excel**, **PowerPoint**, **Outlook**. 

È anche possibile rimuovere etichette e protezione tramite **Esplora file**, che supporta altri tipi di file ed è un pratico strumento per rimuovere etichette e protezione da più file contemporaneamente.

## <a name="using-office-apps-to-remove-labels-and-protection-from-documents-and-emails"></a>Uso delle app di Office per rimuovere etichette e protezione da documenti e messaggi di posta elettronica

Dal **Home** scheda, seleziona la **sensibilità** nella barra multifunzione e deselezionare l'etichetta selezionata.

Oppure, se si è scelto **Mostra barra** dal **sensibilità** pulsante, è possibile selezionare il **Elimina l'etichetta** icona dalla barra di Azure Information Protection:

![Barra di Azure Information Protection - Elimina l'etichetta](../media/v2delete-label.png)

Se il **Elimina l'etichetta** icona non è immediatamente disponibile, selezionare innanzitutto la **modifica l'etichetta** icona:

![Barra di Azure Information Protection - Modifica l'etichetta](../media/v2edit-label.png)

Se ancora non viene visualizzato il **Elimina l'etichetta** icona, l'amministratore non consente di usare questa opzione perché tutti i documenti e indirizzo di posta elettronica devono avere un'etichetta.

## <a name="using-file-explorer-to-remove-labels-and-protection-from-files"></a>Uso di Esplora file per rimuovere etichette e protezione dai file

Quando si usa Esplora file, è possibile rimuovere rapidamente etichette e protezione da un singolo file, più file o una cartella. Quando si seleziona una cartella, vengono selezionati automaticamente tutti i file e tutte le sottocartelle al suo interno. 

1. In Esplora File selezionare un file, più file o una cartella. Fare clic con il pulsante destro del mouse e scegliere **Classifica e proteggi**.

2. Per rimuovere un'etichetta: nella finestra di dialogo **Classifica e proteggi - Azure Information Protection** fare clic su **Elimina l'etichetta**. Se l'etichetta è stata configurata per l'applicazione della protezione, la protezione viene automaticamente rimossa.

3. Per rimuovere la protezione personalizzata da un singolo file: nella finestra di dialogo **Classifica e proteggi - Azure Information Protection** deselezionare l'opzione **Proteggi con autorizzazioni personalizzate**. 

4. Per rimuovere la protezione personalizzata da più file: nella finestra di dialogo **Classifica e proteggi - Azure Information Protection** fare clic su **Rimuovi le autorizzazioni personalizzate**.

5. Fare clic su **Applica** e attendere la visualizzazione del messaggio **Operazione completata** per vedere i risultati. Fare clic su **Chiudi**.


## <a name="other-instructions"></a>Altre istruzioni
Ulteriori procedure nella Guida per l'utente di Azure Information Protection:

- [Per saperne di più](client-user-guide.md#what-do-you-want-to-do)

## <a name="additional-information-for-administrators"></a>Informazioni aggiuntive per gli amministratori    

Visualizzare [Panoramica di etichette di riservatezza](/Office365/SecurityCompliance/sensitivity-labels).

