---
title: Scaricare e installare il client di Azure Information Protection | Azure Information Protection
description: Istruzioni per gli utenti per installare il client di Azure Information Protection per Windows, in modo da potere classificare e proteggere documenti e messaggi di posta elettronica.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 01/13/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 2bf09690-9dba-43b7-9e0a-0110915d4081
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 22af60687ad030e686ba843ced6d450487353a0e
ms.openlocfilehash: 72266181c5334ed7e03b2022df61c4065f1c3ac7


---

# <a name="download-and-install-the-azure-information-protection-client"></a>Scaricare e installare il client di Azure Information Protection

>*Si applica a: Active Directory Rights Management Services, Azure Information Protection, Windows 10, Windows 8.1, Windows 8, Windows 7 con SP1*

**[Questa versione del client è in anteprima e soggetta a modifiche].**

Se il client di Azure Information Protection non viene installato dall'amministratore, è possibile procedere autonomamente. Per installare questo client, è necessario essere un amministratore locale per il PC. 

### <a name="office-2010-only"></a>Solo Office 2010

Quando si usa questa versione di Office, il client di Azure Information Protection deve impostare le chiavi del Registro di sistema che richiedono le autorizzazioni di amministratore: 

Usare le istruzioni per scaricare e installare il client e quindi usare le istruzioni nella sezione seguente per Office 2010.

## <a name="to-download-and-install-the-azure-information-protection-client"></a>Per scaricare e installare il client di Azure Information Protection

1.  Accedere all'[Area download Microsoft](https://www.microsoft.com/en-us/download/details.aspx?id=53018) e scaricare la versione di **anteprima** del client di Azure Information Protection.

2. Fare doppio clic sul file eseguibile che è stato scaricato. 

3. Nella pagina **Installare il client di Azure Information Protection**: 
    
    - Selezionare l'opzione per l'installazione di un criterio demo se non si riesce a connettersi al cloud, ma si vuole vedere e provare Azure Information Protection sul lato client usando un criterio locale per scopi dimostrativi. Quando il client si connette a un servizio di Azure Information Protection, questo criterio demo viene sostituito dai criteri di Azure Information Protection dell'organizzazione.
    
    - Fare clic su **Accetto** dopo avere letto i termini e le condizioni di licenza.

4. Se viene richiesto di continuare, fare clic su **Sì** e attendere il completamento dell'installazione.

3. Fare clic su **Chiudi**. Prima di iniziare a usare il client di Azure Information Protection:

    - Se il computer esegue Office 2010, riavviare il computer e quindi passare alla sezione successiva per il passaggio finale.
    
    - Per le altre versioni di Office, riavviare tutte le applicazioni di Office e tutte le istanze di Esplora file. L'installazione è ora completa ed è possibile usare il client per etichettare e proteggere documenti e messaggi di posta elettronica.

> [!NOTE]
> Se si usa Windows 7 SP1, il client di Azure Information Protection richiede un aggiornamento specifico, [KB 2533623](https://support.microsoft.com/en-us/kb/2533623). Se il computer richiede questo aggiornamento ma non è installato, verrà visualizzato un messaggio quando si prova a usare il client in cui viene richiesto di installare questo aggiornamento prima di potere usare tutte le funzionalità del client di Azure Information Protection.

### <a name="installing-the-azure-information-protection-client-with-office-2010"></a>Installazione del client di Azure Information Protection con Office 2010

Dopo aver installato il client di Azure Information Protection con le istruzioni precedenti:

1. Aprire Microsoft Word. La prima volta che si esegue un'applicazione di Office 2010 dopo aver installato il client di Azure Information Protection, viene visualizzata la finestra di dialogo **Microsoft Azure Information Protection**. Questa finestra di dialogo indica che sono necessarie le credenziali dell'amministratore per completare il processo di accesso.

2. Nella finestra di dialogo **Microsoft Azure Information Protection** fare clic su **OK**.

2. Se viene visualizzata una finestra di dialogo di **Controllo di accesso utente**, fare clic su **Sì** in modo che il client di Azure Information Protection possa aggiornare il Registro di sistema.

L'installazione è ora completa ed è possibile usare il client di Azure Information Protection per etichettare e proteggere documenti e messaggi di posta elettronica.

## <a name="other-instructions"></a>Altre istruzioni
Per le istruzioni d'uso, vedere le sezioni seguenti della Guida per l'utente di Azure Information Protection:

-   [Per saperne di più](client-user-guide.md#what-do-you-want-to-do)

## <a name="additional-information-for-administrators"></a>Informazioni aggiuntive per gli amministratori
[Installazione del client di Azure Information Protection](info-protect-client.md)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]



<!--HONumber=Jan17_HO4-->


