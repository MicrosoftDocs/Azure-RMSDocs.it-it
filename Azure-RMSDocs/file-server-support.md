---
title: Informazioni su come i file server che usano FCI supportano Azure RMS da AIP
description: Come usare l'infrastruttura di classificazione file di Windows Server con Azure RMS quando si distribuisce il connettore RMS per proteggere automaticamente i documenti di Office.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 12/12/2018
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 8fdad425-5daf-4ce1-822f-9d2fb0b87df1
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 81754d9f7ac0ff1351d4298f23da31afcf8ed900
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/14/2019
ms.locfileid: "56254408"
---
# <a name="how-file-servers-that-run-windows-server-and-use-file-classification-infrastructure-fci-support-azure-rights-management"></a>Informazioni su come i file server che eseguono Windows Server e usano l'infrastruttura di classificazione file supportano Azure Rights Management

>*Si applica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*


Quando si configura Windows Server per usare Infrastruttura di classificazione file, questa funzionalità di Gestione risorse file server può analizzare i file locali per stabilire se contengono dati sensibili I file che soddisfano questi criteri vengono contrassegnati con proprietà di classificazione definite da un amministratore. A questo punto possono essere eseguite azioni automatiche, a seconda della classificazione, ad esempio l'applicazione della protezione delle informazioni usando Azure Rights Management e la distribuzione del connettore Rights Management (noto anche come connettore RMS). I file di Office vengono automaticamente protetti da Azure RMS.

Per proteggere tutti i tipi di file, non usare il connettore RMS, ma eseguire invece uno script di Windows PowerShell che usa i cmdlet del [modulo Azure Information Protection](./rms-client/client-admin-guide-powershell.md).

I criteri di classificazione sono completamente configurabili ed estendibili e consentono in tal modo di impedire la perdita potenziale di dati da parte di utenti autorizzati o meno. Tali criteri consentono inoltre di ridurre il rischio di perdita di dati da parte di amministratori di rete perché è possibile configurarli in modo che agli amministratori non venga richiesto l'accesso ai file.

Per istruzioni sulla distribuzione e configurazione del connettore RMS per i file di Office, vedere l'articolo relativo alla [distribuzione del connettore Azure Rights Management](deploy-rms-connector.md).

Per istruzioni sull'uso dello script di Windows PowerShell per tutti i tipi di file, vedere l'articolo [Protezione RMS con Infrastruttura di classificazione file per Windows Server](./rms-client/configure-fci.md).



## <a name="next-steps"></a>Passaggi successivi
Dopo aver compreso in che modo le applicazioni e i servizi supportano Azure RMS, si potrebbe essere interessati a un confronto tra Azure RMS e la versione locale di Rights Management, Active Directory Rights Management Services (AD RMS). Per un confronto delle funzionalità, dei requisiti e dei controlli di sicurezza, vedere [Confronto tra Azure Rights Management e AD RMS](compare-on-premise.md).


