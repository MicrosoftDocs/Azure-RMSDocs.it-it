---
title: Rimuovere le etichette di Azure Information Protection
description: Istruzioni per rimuovere etichette di classificazione e protezione da file etichettati tramite Azure Information Protection o protetti tramite Rights Management.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 12/12/2018
ms.topic: conceptual
ms.service: information-protection
ms.assetid: ''
ms.reviewer: eymanor
ms.suite: ems
ms.openlocfilehash: ab98e211bf0f346359c6f6627a68db3071f7482e
ms.sourcegitcommit: 1d2912b4f0f6e8d7596cbf31e2143a783158ab11
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/12/2018
ms.locfileid: "53305081"
---
# <a name="user-guide-remove-labels-and-protection-from-files-and-emails-that-have-been-labeled-by-azure-information-protection-or-protected-by-rights-management"></a>Manuale dell'utente: Rimuovere etichette di classificazione e protezione da file e messaggi di posta elettronica etichettati tramite Azure Information Protection o protetti tramite Rights Management

>*Si applica a: Active Directory Rights Management Services, [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8, Windows 7 con SP1*

Quando il [client Azure Information Protection viene installato nel computer](install-client-app.md), è possibile rimuovere etichette di classificazione e protezione da file e messaggi di posta elettronica.

Quando l'etichetta rimossa è configurata per l'applicazione della protezione, questa azione comporta anche la rimozione della protezione dal file. Potrebbe essere richiesto di registrare il motivo della rimozione dell'etichetta.

> [!IMPORTANT]
> Per rimuovere la protezione, è necessario essere il proprietario del file oppure aver ricevuto le autorizzazioni per la rimozione della protezione (autorizzazione **Esporta** o **Controllo completo** di Rights Management).

Se si vuole scegliere un'altra etichetta o un set diverso di impostazioni di protezione, non è necessario rimuovere l'etichetta o la protezione. È invece possibile scegliere una nuova etichetta e, se necessario, definire autorizzazioni personalizzate, a condizione che questa configurazione sia autorizzata dall'amministratore. 

È possibile rimuovere etichette e protezione da documenti e messaggi di posta elettronica di Office quando questi vengono ricreati o modificati nelle app desktop di Office: **Word**, **Excel**, **PowerPoint**, **Outlook**. 

È anche possibile rimuovere etichette e protezione tramite **Esplora file**, che supporta altri tipi di file ed è un pratico strumento per rimuovere etichette e protezione da più file contemporaneamente.

## <a name="using-office-apps-to-remove-labels-and-protection-from-documents-and-emails"></a>Uso delle app di Office per rimuovere etichette e protezione da documenti e messaggi di posta elettronica

Sulla barra di Information Protection fare clic sull'icona **Elimina l'etichetta**:

![Barra di Azure Information Protection - Elimina l'etichetta](../media/delete-label.png)

Se l'icona **Elimina l'etichetta** non è immediatamente disponibile, fare clic sull'icona **Modifica l'etichetta**:

![Barra di Azure Information Protection - Modifica l'etichetta](../media/edit-label.png)

Se l'opzione **Elimina l'etichetta** ancora non è visualizzata, l'amministratore non consente l'uso di questa opzione.

> [!NOTE]
> Se la barra di Information Protection non viene visualizzata nelle app di Office:
>
> - Se viene visualizzato un pulsante **Proteggi** nella barra multifunzione: selezionare **Proteggi** e quindi **Mostra barra**.
> 
> - Il client Azure Information Protection potrebbe non essere [installato](install-client-app.md) oppure potrebbe essere in esecuzione in [modalità di sola protezione](client-protection-only-mode.md).

## <a name="using-file-explorer-to-remove-labels-and-protection-from-files"></a>Uso di Esplora file per rimuovere etichette e protezione dai file

Quando si usa Esplora file, è possibile rimuovere rapidamente etichette e protezione da un singolo file, più file o una cartella. Quando si seleziona una cartella, vengono selezionati automaticamente tutti i file e tutte le sottocartelle al suo interno. 

1. In Esplora File selezionare un file, più file o una cartella. Fare clic con il pulsante destro del mouse e scegliere **Classifica e proteggi**.

2. Per rimuovere un'etichetta: nella finestra di dialogo **Classifica e proteggi - Azure Information Protection** fare clic su **Elimina l'etichetta**. Se l'etichetta è stata configurata per l'applicazione della protezione, la protezione viene automaticamente rimossa.

3. Per rimuovere la protezione personalizzata da un singolo file: nella finestra di dialogo **Classifica e proteggi - Azure Information Protection** deselezionare l'opzione **Proteggi con autorizzazioni personalizzate**. 
    
    Se l'opzione **Proteggi con autorizzazioni personalizzate** non è visualizzata, l'amministratore non consente l'uso di questa opzione.
    
4. Per rimuovere la protezione personalizzata da più file: nella finestra di dialogo **Classifica e proteggi - Azure Information Protection** fare clic su **Rimuovi le autorizzazioni personalizzate**.
    
    Se l'opzione **Rimuovi le autorizzazioni personalizzate** non è visualizzata, l'amministratore non consente l'uso di questa opzione.

5. Fare clic su **Applica** e attendere la visualizzazione del messaggio **Operazione completata** per vedere i risultati. Fare clic su **Chiudi**.


## <a name="other-instructions"></a>Altre istruzioni
Ulteriori procedure nella Guida per l'utente di Azure Information Protection:

- [Per saperne di più](client-user-guide.md#what-do-you-want-to-do)

## <a name="additional-information-for-administrators"></a>Informazioni aggiuntive per gli amministratori    
Per istruzioni sulla configurazione per abilitare l'impostazione dei criteri **Make the custom permissions option available to users** (Rendi l'opzione delle autorizzazioni personalizzate disponibile per gli utenti), vedere [Come configurare le impostazioni dei criteri per Azure Information Protection](../configure-policy-settings.md).

Altre istruzioni di configurazione: [Configurazione dei criteri di Azure Information Protection](../configure-policy.md).

