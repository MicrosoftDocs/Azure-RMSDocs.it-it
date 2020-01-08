---
title: Scaricare e installare il client di Azure Information Protection
description: Istruzioni per gli utenti per installare il client di Azure Information Protection per Windows, in modo da potere classificare e proteggere documenti e messaggi di posta elettronica.
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 11/30/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 2bf09690-9dba-43b7-9e0a-0110915d4081
ms.subservice: v1client
ms.reviewer: eymanor
ms.suite: ems
ms.custom: user
ms.openlocfilehash: 2a4242bf87b5cb1ab461fdd7bf4a79231c8cb7f6
ms.sourcegitcommit: 40693000ce86110e14ffce3b553e42149d6b7dc2
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/22/2019
ms.locfileid: "75326364"
---
# <a name="user-guide-download-and-install-the-azure-information-protection-client"></a>Guida dell'utente: Scaricare e installare il client Azure Information Protection

>*Si applica a: Active Directory Rights Management Services, [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8, Windows 7 con SP1*
>
> *Istruzioni per: [client di Azure Information Protection per Windows](../faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*


Se il client di Azure Information Protection non viene installato dall'amministratore, è possibile procedere autonomamente. Per installare questo client è necessario essere un amministratore locale del PC in modo che sia possibile assegnare etichette a documenti e messaggi di posta elettronica e proteggerli.

Inoltre:

- Il client Azure Information Protection richiede Microsoft .NET Framework 4.6.2 come versione minima. Se questo non è presente, il programma di installazione prova a scaricare e installare questo prerequisito. Quando questo prerequisito viene installato come parte dell'installazione del client, è necessario riavviare il computer.

- Se si usa Windows 7 SP1, il client di Azure Information Protection richiede un aggiornamento specifico, ovvero KB 2533623. Se il PC richiede l'aggiornamento ma questo non è installato, l'installazione viene completata, ma viene visualizzato un messaggio per indicare che il client di Azure Information Protection richiede l'aggiornamento. Fino a quando l'aggiornamento non è installato, non sarà possibile usare tutte le funzionalità del client di Azure Information Protection. 

## <a name="to-download-and-install-the-azure-information-protection-client"></a>Per scaricare e installare il client di Azure Information Protection    

1. Accedere alla pagina [Microsoft Azure Information Protection](https://go.microsoft.com/fwlink/?LinkId=303970) nel sito Web Microsoft.

    In questa pagina sono disponibili collegamenti per tutti i dispositivi più diffusi, in modo da consentire di scaricare facilmente un'eventuale app visualizzatore necessaria per aprire i file protetti. Se non si è un amministratore locale del PC, è comunque possibile installare l'app visualizzatore per Windows. Tuttavia, in questa procedura si installerà il client completo, che consente di assegnare etichette ai file e proteggerli. 

2. Individuare la sezione del **client Azure Information Protection** e fare clic sull'icona di Windows. Fare clic su **Download** e salvare il file **AzInfoProtection.exe**.     

3. Eseguire il file eseguibile che è stato scaricato. Se viene chiesto di continuare, fare clic su **Sì**.    

4. Nella pagina **Installare il client di Azure Information Protection**:     
    - Selezionare l'opzione per l'installazione di un criterio demo se non si riesce a connettersi al cloud, ma si vuole vedere e provare Azure Information Protection sul lato client usando un criterio locale per scopi dimostrativi. Quando il client si connette a un servizio di Azure Information Protection, questo criterio demo viene sostituito dai criteri di Azure Information Protection dell'organizzazione.    

    - Fare clic su **Accetto** dopo avere letto i termini e le condizioni di licenza.    

5. Se viene richiesto di continuare, fare clic su **Sì** e attendere il completamento dell'installazione.    

6. Fare clic su **Chiudi**. Prima di iniziare a usare il client di Azure Information Protection:    

    - Se il computer esegue Office 2010, riavviare il computer e quindi passare alla sezione successiva per il passaggio finale.    
        
    - Per le altre versioni di Office, riavviare tutte le applicazioni di Office e tutte le istanze di Esplora file. L'installazione è ora completa ed è possibile usare il client per applicare etichette e protezione a documenti e messaggi di posta elettronica.    

### <a name="installing-the-azure-information-protection-client-with-office-2010"></a>Installazione del client di Azure Information Protection con Office 2010    
Dopo aver installato il client di Azure Information Protection con le istruzioni precedenti:    

1. Aprire Microsoft Word. La prima volta che si esegue un'applicazione di Office 2010 dopo aver installato il client di Azure Information Protection, viene visualizzata la finestra di dialogo **Microsoft Azure Information Protection**. Questa finestra di dialogo indica che sono necessarie le credenziali dell'amministratore per completare il processo di accesso.

2. Nella finestra di dialogo **Microsoft Azure Information Protection** fare clic su **OK**.

3. Se viene visualizzata una finestra di dialogo di **Controllo di accesso utente**, fare clic su **Sì** in modo che il client di Azure Information Protection possa aggiornare il Registro di sistema.

L'installazione è ora completa ed è possibile usare il client di Azure Information Protection per etichettare e proteggere documenti e messaggi di posta elettronica.

## <a name="other-instructions"></a>Altre istruzioni    
Ulteriori procedure nella Guida per l'utente di Azure Information Protection:

- [Per saperne di più](client-user-guide.md#what-do-you-want-to-do)

## <a name="additional-information-for-administrators"></a>Informazioni aggiuntive per gli amministratori    
Vedere [Installare il client Azure Information Protection per gli utenti](client-admin-guide-install.md) nella [guida dell'amministratore](client-admin-guide.md).
 
  
