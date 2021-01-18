---
title: Scaricare & installare il client di Azure Information Protection Unified Labeling
description: Istruzioni per consentire agli utenti di installare il client di Azure Information Protection Unified Labeling per Windows, in modo che sia possibile classificare e proteggere i documenti e i messaggi di posta elettronica.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 05/06/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: v2client
ms.suite: ems
ms.custom: user
ms.openlocfilehash: d6c4ea5c07330efd429577ee569f8f899f63ae0d
ms.sourcegitcommit: af7ac2eeb8f103402c0036dd461c77911fbc9877
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/18/2021
ms.locfileid: "98559745"
---
# <a name="user-guide-download-and-install-the-azure-information-protection-unified-labeling-client"></a>Guida dell'utente: scaricare e installare il client di Azure Information Protection Unified Labeling

>***Si applica a**: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8 *
>
> ***Pertinente per**: [Azure Information Protection client di etichetta unificato per Windows](../faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients). Per il client classico, vedere la [Guida per l'utente del client classico](install-client-app.md). *

Se l'amministratore non installa il client di etichettatura unificato di Azure Information Protection, è possibile eseguire questa operazione manualmente. Per installare questo client è necessario essere un amministratore locale del PC in modo che sia possibile assegnare etichette a documenti e messaggi di posta elettronica e proteggerli.

> [!NOTE]
> Il client per l'assegnazione di etichette unificata Azure Information Protection richiede una versione minima di Microsoft .NET Framework 4.6.2. Se questo non è presente, il programma di installazione tenterà di scaricare e installare questo prerequisito. Quando questo prerequisito viene installato come parte dell'installazione del client, è necessario riavviare il computer.
>

## <a name="to-download-and-install-the-azure-information-protection-unified-labeling-client"></a>Per scaricare e installare il client per l'etichettatura unificata di Azure Information Protection

Prima di installare il client Azure Information Protection Unified Labeling, verificare con l'amministratore o help desk di usare le etichette di [riservatezza](/microsoft-365/compliance/sensitivity-labels) per classificare e proteggere documenti e messaggi di posta elettronica.

1. Scaricare **AzInfoProtection_UL.exe** dall' [area download Microsoft](https://www.microsoft.com/download/details.aspx?id=53018).

2. Eseguire il file eseguibile scaricato. Se viene richiesto di continuare, fare clic su **Sì**.

3. Nella pagina **Installa il client Azure Information Protection** fare clic su **Accetto** dopo aver letto i termini e le condizioni di licenza.

4. Se viene richiesto di continuare, fare clic su **Sì** e attendere il completamento dell'installazione.

6. Fare clic su **Close**. 

    Prima di iniziare a usare il client di Azure Information Protection Unified Labeling, riavviare tutte le applicazioni di Office e tutte le istanze di Esplora file. L'installazione è ora completa ed è possibile usare il client per applicare etichette e protezione a documenti e messaggi di posta elettronica.

    > [!NOTE]
    > Se il computer esegue Office 2010, riavviare il computer e passare alla [sezione successiva](#installing-the-azure-information-protection-unified-labeling-client-with-office-2010) per il passaggio finale.   
    >
     
### <a name="installing-the-azure-information-protection-unified-labeling-client-with-office-2010"></a>Installazione del client per l'etichettatura unificata di Azure Information Protection con Office 2010

> [!IMPORTANT]
> Il supporto esteso per Office 2010 è terminato il 13 ottobre 2020. Per altre informazioni, vedere [AIP e versioni legacy di Windows e Office](../known-issues.md#aip-and-legacy-windows-and-office-versions).
> 

Dopo aver installato il client per l'etichettatura unificata di Azure Information Protection con le istruzioni precedenti:

1. Aprire Microsoft Word. La prima volta che si esegue un'applicazione di Office 2010 dopo aver installato il client di Azure Information Protection, viene visualizzata la finestra di dialogo **Microsoft Azure Information Protection**. Questa finestra di dialogo indica che sono necessarie le credenziali dell'amministratore per completare il processo di accesso.

2. Nella finestra di dialogo **Microsoft Azure Information Protection** fare clic su **OK**.

3. Se viene visualizzata una finestra di dialogo di **Controllo di accesso utente**, fare clic su **Sì** in modo che il client di Azure Information Protection possa aggiornare il Registro di sistema.

L'installazione è ora completa ed è possibile usare il client per l'etichettatura unificata di Azure Information Protection per etichettare e proteggere documenti e messaggi di posta elettronica.

## <a name="other-instructions"></a>Altre istruzioni    
Altre istruzioni sulle procedure sono disponibili nella Guida per l'utente del client di Azure Information Protection Unified labeling.

- [Per saperne di più](clientv2-user-guide.md#what-do-you-want-to-do)

## <a name="additional-information-for-administrators"></a>Informazioni aggiuntive per gli amministratori    
Vedere [installare il client di etichettatura unificata Azure Information Protection per gli utenti](clientv2-admin-guide-install.md) nella [Guida dell'amministratore](clientv2-admin-guide.md).