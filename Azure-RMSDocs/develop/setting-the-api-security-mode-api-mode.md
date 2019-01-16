---
title: Come impostare la modalità di sicurezza dell'API | Azure RMS
description: Scegliere la modalità di sicurezza eseguita dall'applicazione API file.
keywords: ''
author: bryanla
ms.author: bryanla
manager: mbaldwin
ms.date: 02/23/2017
ms.topic: conceptual
ms.service: information-protection
ms.assetid: 3B088F14-81C5-4C78-8DED-F5F153353EE0
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
ms.openlocfilehash: c1f6b30fa15ac050b77314e1baf8d355f6887f24
ms.sourcegitcommit: bd2b31dd97c8ae08c28b0f5688517110a726e3a1
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/08/2019
ms.locfileid: "54071404"
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
