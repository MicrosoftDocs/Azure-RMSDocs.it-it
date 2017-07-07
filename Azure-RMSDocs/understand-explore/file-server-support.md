---
title: File server che usano l'infrastruttura di classificazione file - Azure Information Protection
description: Come usare l'infrastruttura di classificazione file di Windows Server con Azure RMS quando si distribuisce il connettore RMS per proteggere automaticamente i documenti di Office.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/08/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 8fdad425-5daf-4ce1-822f-9d2fb0b87df1
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 909ff4f7c96af65172604bb903173dd38d95dcf9
ms.sourcegitcommit: 04eb4990e2bf0004684221592cb93df35e6acebe
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/30/2017
---
# <a name="file-servers-that-run-windows-server-and-use-file-classification-infrastructure-fci"></a>File server che eseguono Windows Server e usano l'infrastruttura di classificazione file

>*Si applica a: Azure Information Protection, Office 365*


Quando si configura Windows Server per usare Infrastruttura di classificazione file, questa funzionalità di Gestione risorse file server può analizzare i file locali per stabilire se contengono dati sensibili I file che soddisfano questi criteri vengono contrassegnati con proprietà di classificazione definite da un amministratore. A questo punto possono essere eseguite azioni automatiche, a seconda della classificazione, ad esempio l'applicazione della protezione delle informazioni usando [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] e la distribuzione del connettore Rights Management (noto anche come connettore RMS). I file di Office vengono automaticamente protetti da Azure RMS.

Per proteggere tutti i tipi di file, non si userà il connettore RMS, ma si eseguirà invece uno script di Windows PowerShell che usa i cmdlet del [modulo Azure Information Protection](../rms-client/client-admin-guide-powershell.md).

I criteri di classificazione sono completamente configurabili ed estendibili e consentono in tal modo di impedire la perdita potenziale di dati da parte di utenti autorizzati o meno. Tali criteri consentono inoltre di ridurre il rischio di perdita di dati da parte di amministratori di rete perché è possibile configurarli in modo che agli amministratori non venga richiesto l'accesso ai file.

Per istruzioni sulla distribuzione e configurazione del connettore RMS per i file di Office, vedere l'articolo relativo alla [distribuzione del connettore Azure Rights Management](../deploy-use/deploy-rms-connector.md).

Per istruzioni sull'uso dello script di Windows PowerShell per tutti i tipi di file, vedere l'articolo [Protezione RMS con Infrastruttura di classificazione file per Windows Server](../rms-client/configure-fci.md).



## <a name="next-steps"></a>Passaggi successivi
Dopo aver compreso in che modo le applicazioni e i servizi supportano Azure RMS, si potrebbe essere interessati a un confronto tra Azure RMS con la versione locale di Rights Management, Active Directory Rights Management Services (AD RMS). Per un confronto delle funzionalità, dei requisiti e dei controlli di sicurezza, vedere [Confronto tra Azure Rights Management e AD RMS](compare-azure-rms-ad-rms.md).

[!INCLUDE[Commenting house rules](../includes/houserules.md)]

