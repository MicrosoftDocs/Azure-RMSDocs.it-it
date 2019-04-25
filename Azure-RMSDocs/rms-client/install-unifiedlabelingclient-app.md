---
title: Scaricare e installare il client di assegnazione di etichette unificato di Azure Information Protection
description: Istruzioni per gli utenti possano installare il client di assegnazione di etichette unificato di Azure Information Protection per Windows, in modo che è possibile classificare e proteggere documenti e messaggi di posta elettronica.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 04/17/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.suite: ems
ms.openlocfilehash: 563ddb6d91ef59ee96cf00dba973b7e612bbc780
ms.sourcegitcommit: fff4c155c52c9ff20bc4931d5ac20c3ea6e2ff9e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/24/2019
ms.locfileid: "60180954"
---
# <a name="user-guide-download-and-install-the-azure-information-protection-unified-labeling-client"></a>Manuale dell'utente: Scaricare e installare il client di assegnazione di etichette unificato di Azure Information Protection

>*Si applica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8, Windows 7 con SP1*
>
> *Istruzioni per: [Azure Information Protection unified client per l'assegnazione di etichette per Windows](../faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*

Se l'amministratore non viene installato il client per l'assegnazione di etichette unificato Azure Information Protection, è possibile eseguire manualmente. Per installare questo client è necessario essere un amministratore locale del PC in modo che sia possibile assegnare etichette a documenti e messaggi di posta elettronica e proteggerli.

Inoltre:

- Il client per l'etichettatura unificata di Azure Information Protection richiede Microsoft .NET Framework 4.6.2 come versione minima. Se non è disponibile, il programma di installazione prova a scaricare e installare questo prerequisito. Quando questo prerequisito viene installato come parte dell'installazione del client, è necessario riavviare il computer.

- Se si usa Windows 7 SP1, il client per l'etichettatura unificata di Azure Information Protection richiede un aggiornamento specifico, ovvero KB 2533623. Se il PC richiede l'aggiornamento ma questo non è installato, l'installazione viene completata, ma viene visualizzato un messaggio per indicare che il client per l'etichettatura unificata di Azure Information Protection richiede l'aggiornamento. Fino a quando l'aggiornamento non è installato, non sarà possibile usare tutte le funzionalità del client per l'etichettatura unificata di Azure Information Protection. 

## <a name="to-download-and-install-the-azure-information-protection-unified-labeling-client"></a>Per scaricare e installare il client per l'etichettatura unificata di Azure Information Protection

Prima di installare il client di assegnazione di etichette unificato di Azure Information Protection, verificare con l'amministratore o l'help desk che si siano utilizzando le etichette di riservatezza di Office 365.

1. Scaricare **AzInfoProtection_UL.exe** dalle [area download Microsoft](https://www.microsoft.com/en-us/download/details.aspx?id=53018).

2. Eseguire il file eseguibile che è stato scaricato, se viene chiesto di continuare, fare clic su **Sì**.

3. Nella pagina **Installa il client Azure Information Protection** fare clic su **Accetto** dopo aver letto i termini e le condizioni di licenza.

4. Se viene richiesto di continuare, fare clic su **Sì** e attendere il completamento dell'installazione.

6. Fare clic su **Chiudi**. Prima di iniziare a usare il client per l'etichettatura unificata di Azure Information Protection:

    - Se il computer esegue Office 2010, riavviare il computer e quindi passare alla sezione successiva per il passaggio finale.    
        
    - Per le altre versioni di Office, riavviare tutte le applicazioni di Office e tutte le istanze di Esplora file. L'installazione è ora completa ed è possibile usare il client per applicare etichette e protezione a documenti e messaggi di posta elettronica.

### <a name="installing-the-azure-information-protection-unified-labeling-client-with-office-2010"></a>Installazione del client per l'etichettatura unificata di Azure Information Protection con Office 2010

Dopo aver installato il client per l'etichettatura unificata di Azure Information Protection con le istruzioni precedenti:

1. Aprire Microsoft Word. La prima volta che si esegue un'applicazione di Office 2010 dopo aver installato il client di Azure Information Protection, viene visualizzata la finestra di dialogo **Microsoft Azure Information Protection**. Questa finestra di dialogo indica che sono necessarie le credenziali dell'amministratore per completare il processo di accesso.

2. Nella finestra di dialogo **Microsoft Azure Information Protection** fare clic su **OK**.

3. Se viene visualizzata una finestra di dialogo di **Controllo di accesso utente**, fare clic su **Sì** in modo che il client di Azure Information Protection possa aggiornare il Registro di sistema.

L'installazione è ora completa ed è possibile usare il client per l'etichettatura unificata di Azure Information Protection per etichettare e proteggere documenti e messaggi di posta elettronica.

## <a name="other-instructions"></a>Altre istruzioni    
Altre istruzioni sulle procedure di Azure Information Protection unified imprevisto delle etichette manuale dell'utente client:

- [Per saperne di più](clientv2-user-guide.md#what-do-you-want-to-do)

## <a name="additional-information-for-administrators"></a>Informazioni aggiuntive per gli amministratori    
Visualizzare [installare il client di assegnazione di etichette unificato di Azure Information Protection per gli utenti](clientv2-admin-guide-install.md) dalle [Guida dell'amministratore](clientv2-admin-guide.md).
