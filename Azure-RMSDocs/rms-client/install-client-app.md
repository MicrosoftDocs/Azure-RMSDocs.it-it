---
title: Scaricare & installare il client di Azure Information Protection classico
description: Istruzioni per consentire agli utenti di installare il client classico di Azure Information Protection per Windows, in modo che sia possibile classificare e proteggere documenti e messaggi di posta elettronica.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 08/17/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 2bf09690-9dba-43b7-9e0a-0110915d4081
ROBOTS: NOINDEX
ms.subservice: v1client
ms.reviewer: eymanor
ms.suite: ems
ms.custom: user
ms.openlocfilehash: df5328b94112342276028e2a74da02de14170418
ms.sourcegitcommit: af7ac2eeb8f103402c0036dd461c77911fbc9877
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/18/2021
ms.locfileid: "98560240"
---
# <a name="user-guide-download-and-install-the-azure-information-protection-classic-client"></a>Guida dell'utente: scaricare e installare il client di Azure Information Protection classico

>***Si applica a**: Active Directory Rights Management Services, [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8 *
>
>***Pertinente per**: [Azure Information Protection client classico per Windows](../faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients). Per il client di etichettatura unificata, vedere la guida dell'utente per l' [assegnazione di etichette unificata](install-unifiedlabelingclient-app.md). *

> [!NOTE] 
> Per offrire un'esperienza per i clienti unificata e semplificata, il **client classico di Azure Information Protection** e **Gestione etichette** nel portale di Azure saranno **deprecati** a partire dal **31 marzo 2021**. In questo intervallo di tempo tutti i clienti correnti di Azure Information Protection possono passare alla soluzione di etichettatura unificata usando la piattaforma di etichettatura unificata di Microsoft Information Protection. Altre informazioni nell'[avviso ufficiale sulla deprecazione](https://aka.ms/aipclassicsunset).

Se il client di Azure Information Protection non viene installato dall'amministratore, è possibile procedere autonomamente. Per installare questo client è necessario essere un amministratore locale del PC in modo che sia possibile assegnare etichette a documenti e messaggi di posta elettronica e proteggerli.

Inoltre:

- Il client Azure Information Protection richiede Microsoft .NET Framework 4.6.2 come versione minima. Se questo non è presente, il programma di installazione prova a scaricare e installare questo prerequisito. Quando questo prerequisito viene installato come parte dell'installazione del client, è necessario riavviare il computer.


## <a name="to-download-and-install-the-azure-information-protection-client"></a>Per scaricare e installare il client di Azure Information Protection

Il client di Azure Information Protection classico verrà deprecato nel marzo 2021. 

Per distribuire il client classico AIP, aprire un ticket di supporto per ottenere l'accesso al download.

1. Eseguire il file di **AzInfoProtection.exe** per avviare l'installazione. Se viene richiesto di continuare, fare clic su **Sì**.    

1. Nella pagina **Installare il client di Azure Information Protection**:     
    - Selezionare l'opzione per l'installazione di un criterio demo se non si riesce a connettersi al cloud, ma si vuole vedere e provare Azure Information Protection sul lato client usando un criterio locale per scopi dimostrativi. Quando il client si connette a un servizio di Azure Information Protection, questo criterio demo viene sostituito dai criteri di Azure Information Protection dell'organizzazione.    

    - Fare clic su **Accetto** dopo avere letto i termini e le condizioni di licenza.    

1. Se viene richiesto di continuare, fare clic su **Sì** e attendere il completamento dell'installazione.    

1. Fare clic su **Close**. 

    Prima di iniziare a usare il client di Azure Information Protection, riavviare tutte le applicazioni di Office e tutte le istanze di Esplora file. L'installazione è ora completa ed è possibile usare il client per applicare etichette e protezione a documenti e messaggi di posta elettronica.

    > [!NOTE]
    > Se il computer esegue Office 2010, riavviare il computer e passare alla [sezione successiva](#installing-the-azure-information-protection-client-with-office-2010) per il passaggio finale.  

### <a name="installing-the-azure-information-protection-client-with-office-2010"></a>Installazione del client di Azure Information Protection con Office 2010

> [!IMPORTANT]
> Il supporto esteso per Office 2010 è terminato il 13 ottobre 2020. Per altre informazioni, vedere [AIP e versioni legacy di Windows e Office](../known-issues.md#aip-and-legacy-windows-and-office-versions).
> 

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
 
  
