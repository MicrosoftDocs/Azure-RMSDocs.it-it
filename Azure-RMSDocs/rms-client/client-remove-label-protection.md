---
title: Rimuovere le etichette di Azure Information Protection
description: Istruzioni per rimuovere etichette di classificazione e protezione da file etichettati tramite Azure Information Protection o protetti tramite Rights Management.
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 1/13/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: ''
ms.subservice: v1client
ms.reviewer: eymanor
ms.suite: ems
ms.custom: user
ms.openlocfilehash: d65fc0e8dc7b3cea75b0ab076e81eea88dea4217
ms.sourcegitcommit: 223e26b0ca4589317167064dcee82ad0a6a8d663
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/07/2020
ms.locfileid: "86047406"
---
# <a name="user-guide-remove-labels-and-protection-from-files-and-emails-that-have-been-labeled-by-azure-information-protection-or-protected-by-rights-management"></a>Guida dell'utente: Rimuovere etichette e protezione da file e messaggi di posta elettronica etichettati tramite Azure Information Protection o protetti tramite Rights Management

>*Si applica a: Active Directory Rights Management Services, [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8*
>
> *Istruzioni per: [Client Azure Information Protection per Windows](../faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

Quando il [client Azure Information Protection viene installato nel computer](install-client-app.md), è possibile rimuovere etichette di classificazione e protezione da file e messaggi di posta elettronica.

Quando l'etichetta rimossa è configurata per l'applicazione della protezione, questa azione comporta anche la rimozione della protezione dal file. Potrebbe essere richiesto di registrare il motivo della rimozione dell'etichetta.

> [!IMPORTANT]
> Per rimuovere la protezione, è necessario essere il proprietario del file oppure aver ricevuto le autorizzazioni per la rimozione della protezione (autorizzazione **Esporta** o **Controllo completo** di Rights Management).

Se si vuole scegliere un'altra etichetta o un set diverso di impostazioni di protezione, non è necessario rimuovere l'etichetta o la protezione. È invece possibile scegliere una nuova etichetta e, se necessario, definire autorizzazioni personalizzate, a condizione che questa configurazione sia autorizzata dall'amministratore. 

È possibile rimuovere etichette e protezione da documenti e messaggi di posta elettronica di Office quando questi vengono ricreati o modificati nelle app desktop di Office, come **Word**, **Excel**, **PowerPoint** e **Outlook**. 

È anche possibile rimuovere etichette e protezione tramite **Esplora file**, che supporta altri tipi di file ed è un pratico strumento per rimuovere etichette e protezione da più file contemporaneamente.

## <a name="using-office-apps-to-remove-labels-and-protection-from-documents-and-emails"></a>Uso delle app di Office per rimuovere etichette e protezione da documenti e messaggi di posta elettronica

Sulla barra di Information Protection fare clic sull'icona **Elimina l'etichetta**:

![Barra di Azure Information Protection - Elimina l'etichetta](../media/delete-label.png)

Se l'icona **Elimina l'etichetta** non è immediatamente disponibile, fare clic sull'icona **Modifica l'etichetta**:

![Barra di Azure Information Protection - Modifica l'etichetta](../media/edit-label.png)

Se l'icona **Elimina etichetta** non è ancora visualizzata, l'amministratore non consente di usare questa opzione perché tutti i documenti e i messaggi di posta elettronica devono avere un'etichetta.

> [!NOTE]
> Se la barra di Information Protection non viene visualizzata nelle app di Office:
>
> - Se viene visualizzato un pulsante **Proteggi** nella barra multifunzione: selezionare **Proteggi**, quindi selezionare **Mostra barra**.
> 
> - Il client Azure Information Protection potrebbe non essere [installato](install-client-app.md) oppure potrebbe essere in esecuzione in [modalità di sola protezione](client-protection-only-mode.md).

## <a name="using-file-explorer-to-remove-labels-and-protection-from-files"></a>Uso di Esplora file per rimuovere etichette e protezione dai file

Quando si usa Esplora file, è possibile rimuovere rapidamente etichette e protezione da un singolo file, più file o una cartella. Quando si seleziona una cartella, vengono selezionati automaticamente tutti i file e tutte le sottocartelle al suo interno. 

1. In Esplora File selezionare un file, più file o una cartella. Fare clic con il pulsante destro del mouse e scegliere **Classifica e proteggi**.

2. Per rimuovere un'etichetta: nella finestra di dialogo **Classifica e proteggi - Azure Information Protection** fare clic su **Elimina l'etichetta**. Se l'etichetta è stata configurata per l'applicazione della protezione, la protezione viene automaticamente rimossa.

3. Per rimuovere protezione personalizzata da un singolo file: nella finestra di dialogo **Classifica e proteggi - Azure Information Protection** deselezionare l'opzione **Proteggi con autorizzazioni personalizzate**. 
    
    Se l'opzione **Proteggi con autorizzazioni personalizzate** non è visualizzata, l'amministratore non consente l'uso di questa opzione.
    
4. Per rimuovere protezione personalizzata da più file: nella finestra di dialogo **Classifica e proteggi - Azure Information Protection** fare clic su **Rimuovi le autorizzazioni personalizzate**.
    
    Se l'opzione **Rimuovi le autorizzazioni personalizzate** non è visualizzata, l'amministratore non consente l'uso di questa opzione.

5. Fare clic su **Applica** e attendere la visualizzazione del messaggio **Operazione completata** per vedere i risultati. e quindi fare clic su **Chiudi**.


## <a name="other-instructions"></a>Altre istruzioni
Ulteriori procedure nella Guida per l'utente di Azure Information Protection:

- [Per saperne di più](client-user-guide.md#what-do-you-want-to-do)

## <a name="additional-information-for-administrators"></a>Informazioni aggiuntive per gli amministratori    
Per istruzioni sulla configurazione per abilitare l'impostazione dei criteri **Make the custom permissions option available to users** (Rendi l'opzione delle autorizzazioni personalizzate disponibile per gli utenti), vedere [Come configurare le impostazioni dei criteri per Azure Information Protection](../configure-policy-settings.md).

Altre istruzioni sulla configurazione: [Configurazione dei criteri di Azure Information Protection](../configure-policy.md).

