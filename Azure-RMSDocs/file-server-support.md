---
title: Come i file server Windows che usano l'istanza FCI supportano Azure RMS-AIP
description: Come usare l'infrastruttura di classificazione file di Windows Server con Azure RMS quando si distribuisce il connettore RMS per proteggere automaticamente i documenti di Office.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 11/08/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 8fdad425-5daf-4ce1-822f-9d2fb0b87df1
ROBOTS: NOINDEX
ms.subservice: fci
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 2de7d165c72dbd6c96f76d7027c1a2d3ba62bff1
ms.sourcegitcommit: b32c16e41ba36167b5a3058b56a73183bdd4306d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/29/2020
ms.locfileid: "97806193"
---
# <a name="how-windows-file-servers-that-use-fci-support-azure-rights-management"></a>Come i file server Windows che usano l'istanza FCI supportano Azure Rights Management

>***Si applica a**: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*
>
>***Rilevante per**: [Client classico Azure Information Protection per Windows](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

>[!NOTE] 
> Per offrire un'esperienza per i clienti unificata e semplificata, il **client classico di Azure Information Protection** e **Gestione etichette** nel portale di Azure saranno **deprecati** a partire dal **31 marzo 2021**. In questo intervallo di tempo tutti i clienti correnti di Azure Information Protection possono passare alla soluzione di etichettatura unificata usando la piattaforma di etichettatura unificata di Microsoft Information Protection. Altre informazioni nell'[avviso ufficiale sulla deprecazione](https://aka.ms/aipclassicsunset).

Quando si configura Windows Server per usare Infrastruttura di classificazione file, questa funzionalità di Gestione risorse file server può analizzare i file locali per stabilire se contengono dati sensibili 

I file che soddisfano questi criteri vengono contrassegnati con proprietà di classificazione definite da un amministratore. A questo punto possono essere eseguite azioni automatiche, a seconda della classificazione, 

Una di queste azioni include l'applicazione della protezione delle informazioni tramite Rights Management di Azure e la distribuzione del connettore Rights Management (noto anche come connettore RMS). I file di Office vengono automaticamente protetti da Azure RMS.

> [!TIP]
> Per proteggere tutti i tipi di file, non usare il connettore RMS, ma eseguire invece uno script di Windows PowerShell che usa i cmdlet del [modulo Azure Information Protection](./rms-client/client-admin-guide-powershell.md).
> 

I criteri di classificazione sono completamente configurabili ed estendibili e consentono in tal modo di impedire la perdita potenziale di dati da parte di utenti autorizzati o meno. Tali criteri consentono inoltre di ridurre il rischio di perdita di dati da parte di amministratori di rete perché è possibile configurarli in modo che agli amministratori non venga richiesto l'accesso ai file.

Per istruzioni su come distribuire e configurare il connettore RMS per i file di Office, vedere [Deploying the Azure Rights Management Connector](deploy-rms-connector.md).

Per istruzioni sull'uso dello script di Windows PowerShell per tutti i tipi di file, vedere 

- [Protezione RMS con infrastruttura di classificazione file di Windows Server &#40;FCI&#41;](./rms-client/configure-fci.md)
- [Script di Windows PowerShell per la protezione Azure RMS usando l'infrastruttura di classificazione file di Gestione risorse file server](rms-client/fci-script.md)


## <a name="next-steps"></a>Passaggi successivi

Dopo aver compreso in che modo le applicazioni e i servizi supportano Azure RMS, si potrebbe essere interessati a un confronto tra Azure RMS e la versione locale di Rights Management, Active Directory Rights Management Services (AD RMS). Per un confronto delle funzionalità, dei requisiti e dei controlli di sicurezza, vedere [confronto tra Rights Management e ad RMS di Azure](compare-on-premise.md).


