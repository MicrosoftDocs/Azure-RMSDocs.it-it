---
title: Come impostare la modalità di sicurezza dell'API | Azure RMS
description: Scegliere la modalità di sicurezza eseguita dall'applicazione API file.
keywords: ''
author: msmbaldwin
ms.author: mbaldwin
manager: barbkess
ms.date: 02/23/2017
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 3B088F14-81C5-4C78-8DED-F5F153353EE0
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
ms.openlocfilehash: de05a0331e347dbfa4c10237433fcf370f088388
ms.sourcegitcommit: fff4c155c52c9ff20bc4931d5ac20c3ea6e2ff9e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/24/2019
ms.locfileid: "60175950"
---
# <a name="how-to-set-the-api-security-mode"></a>Procedura: Impostare la modalità di sicurezza dell'API

È possibile scegliere la modalità di sicurezza in cui viene eseguita l'applicazione API file tramite la funzione [IpcSetGlobalProperty](https://msdn.microsoft.com/library/hh535270.aspx).

Per inizializzare l'applicazione in modo che venga eseguita in *modalità server*, chiamare la funzione [IpcSetGlobalProperty](https://msdn.microsoft.com/library/hh535270.aspx) e impostare la modalità di sicurezza su [IPC\_API\_MODE\_SERVER](https://msdn.microsoft.com/library/hh535236.aspx). Per impostazione predefinita l'applicazione verrà eseguita in *modalità client*, **IPC\_API\_MODE\_CLIENT**.

Per altre informazioni sulla *modalità server*, vedere [Tipi di applicazioni](application-types.md).

**Importante**  La modalità di sicurezza deve essere impostata prima di chiamare qualsiasi altra funzione di Rights Management Services SDK 2.1. Dopo averla impostata, la modalità di sicurezza non può essere modificata per il processo corrente.

## <a name="related-topics"></a>Argomenti correlati

* [Tipi di applicazioni](application-types.md)
* [Valori della modalità API](https://msdn.microsoft.com/library/hh535236.aspx)
* [IpcSetGlobalProperty](https://msdn.microsoft.com/library/hh535270.aspx)
