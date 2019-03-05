---
title: Scaricare e installare il client per l'etichettatura unificata di Azure Information Protection (anteprima)
description: Istruzioni per gli utenti per installare la versione di anteprima del client che supporta l'etichettatura unificata di Azure Information Protection per Windows, in modo da potere classificare e proteggere documenti e messaggi di posta elettronica.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 02/26/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 2bf09690-9dba-43b7-9e0a-0110915d4081
ms.reviewer: eymanor
ms.suite: ems
ms.openlocfilehash: cbe97fc619de9b7bda73ebb419bfc254f237f372
ms.sourcegitcommit: 55782e58508051f0ecf460e8b126f70ab9b9ceec
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/25/2019
ms.locfileid: "56756131"
---
# <a name="download-and-install-the-azure-information-protection-unified-labeling-client-preview"></a>Scaricare e installare il client per l'etichettatura unificata di Azure Information Protection (anteprima)

>*Si applica a: Active Directory Rights Management Services, [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8, Windows 7 con SP1*

> [!NOTE]
> Questo client è in anteprima e soggetto a modifiche. Usa l'archivio di etichettatura unificata e scarica i criteri con etichette di riservatezza dal Centro sicurezza e conformità di Office 365. Per usare queste etichette, è necessario prima pubblicarle dal Centro sicurezza e conformità. [Altre informazioni](https://techcommunity.microsoft.com/t5/Security-Privacy-and-Compliance/Announcing-the-availability-of-unified-labeling-management-in/ba-p/262492)

Per installare questa versione di anteprima del client è necessario essere un amministratore locale del PC in modo che sia possibile assegnare etichette a documenti e messaggi di posta elettronica e proteggerli.

Inoltre:

- Il client per l'etichettatura unificata di Azure Information Protection richiede Microsoft .NET Framework 4.6.2 come versione minima. Se non è disponibile, il programma di installazione prova a scaricare e installare questo prerequisito. Quando questo prerequisito viene installato come parte dell'installazione del client, è necessario riavviare il computer.

- Se si usa Windows 7 SP1, il client per l'etichettatura unificata di Azure Information Protection richiede un aggiornamento specifico, ovvero KB 2533623. Se il PC richiede l'aggiornamento ma questo non è installato, l'installazione viene completata, ma viene visualizzato un messaggio per indicare che il client per l'etichettatura unificata di Azure Information Protection richiede l'aggiornamento. Fino a quando l'aggiornamento non è installato, non sarà possibile usare tutte le funzionalità del client per l'etichettatura unificata di Azure Information Protection. 

## <a name="to-download-and-install-the-azure-information-protection-unified-labeling-client"></a>Per scaricare e installare il client per l'etichettatura unificata di Azure Information Protection

Prima di installare il client per l'etichettatura unificata di Azure Information Protection, verificare che nel Centro sicurezza e conformità di Office 365 siano disponibili etichette di riservatezza pubblicate per gli utenti. 

Se sono disponibili etichette che attualmente vengono pubblicate dal portale di Azure per Azure Information Protection, è possibile [eseguire la migrazione di queste etichette](../configure-policy-migrate-labels.md) nel Centro sicurezza e conformità.

1. Scaricare la versione di anteprima del client dall'[Area download Microsoft](https://www.microsoft.com/en-us/download/details.aspx?id=57440).

2. Eseguire il file eseguibile scaricato in precedenza, **AzInfoProtection_For_Unified_Labeling.exe**. Se viene chiesto di continuare, fare clic su **Sì**.    

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

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sull'archivio di etichettatura unificata ora usato dal Centro sicurezza e conformità di Office 365, leggere il post di blog seguente: [Announcing the availability of unified labeling management in the Security & Compliance Center](https://techcommunity.microsoft.com/t5/Security-Privacy-and-Compliance/Announcing-the-availability-of-unified-labeling-management-in/ba-p/262492) (Annuncio della disponibilità della gestione dell'etichettatura unificata nel Centro sicurezza e conformità).
