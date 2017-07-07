---
title: "Come impostare la modalità di sicurezza dell'API | Azure RMS"
description: "Scegliere la modalità di sicurezza eseguita dall'applicazione API file."
keywords: 
author: bruceperlerms
ms.author: bruceper
manager: mbaldwin
ms.date: 02/23/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 3B088F14-81C5-4C78-8DED-F5F153353EE0
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
ms.openlocfilehash: 5ad73cdb72957425ce71f77ba3d11ec457a4f72f
ms.sourcegitcommit: 04eb4990e2bf0004684221592cb93df35e6acebe
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/30/2017
---
# <a name="how-to-set-the-api-security-mode"></a>Procedura: Impostare la modalità di sicurezza dell'API

È possibile scegliere la modalità di sicurezza in cui viene eseguita l'applicazione API file tramite la funzione [IpcSetGlobalProperty](https://msdn.microsoft.com/library/hh535270.aspx).

Per inizializzare l'applicazione in modo che venga eseguita in *modalità server*, chiamare la funzione [IpcSetGlobalProperty](https://msdn.microsoft.com/library/hh535270.aspx) e impostare la modalità di sicurezza su [IPC\_API\_MODE\_SERVER](https://msdn.microsoft.com/library/hh535236.aspx). Per impostazione predefinita l'applicazione verrà eseguita in *modalità client*, **IPC\_API\_MODE\_CLIENT**.

Per altre informazioni sulla *modalità server*, vedere [Tipi di applicazioni](application-types.md).

**Importante**: la modalità di sicurezza deve essere impostata prima di chiamare qualsiasi altra funzione di Rights Management Services SDK 2.1. Dopo averla impostata, la modalità di sicurezza non può essere modificata per il processo corrente.

## <a name="related-topics"></a>Argomenti correlati

* [Tipi di applicazioni](application-types.md)
* [Valori della modalità API](https://msdn.microsoft.com/library/hh535236.aspx)
* [IpcSetGlobalProperty](https://msdn.microsoft.com/library/hh535270.aspx)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]