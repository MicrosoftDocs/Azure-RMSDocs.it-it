---
title: "Come impostare la modalità di sicurezza dell&quot;API | Azure RMS"
description: "Scegliere la modalità di sicurezza eseguita dall&quot;applicazione API file."
keywords: 
author: bruceperlerms
ms.author: bruceper
manager: mbaldwin
ms.date: 09/25/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 3B088F14-81C5-4C78-8DED-F5F153353EE0
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 9d8354f2d68f211d349226970fd2f83dd0ce810b
ms.openlocfilehash: f7acef7fa69c836c5d57d8c1705007f919a9dbf2


---

# <a name="howto-set-the-api-security-mode"></a>Procedura: Impostare la modalità di sicurezza dell'API

È possibile scegliere la modalità di sicurezza in cui viene eseguita l'applicazione API file tramite la funzione [IpcSetGlobalProperty](https://msdn.microsoft.com/library/hh535270.aspx).

Per inizializzare l'applicazione in modo che venga eseguita in *modalità server*, chiamare la funzione [IpcSetGlobalProperty](https://msdn.microsoft.com/library/hh535270.aspx) e impostare la modalità di sicurezza su [IPC\_API\_MODE\_SERVER](https://msdn.microsoft.com/library/hh535236.aspx). Per impostazione predefinita l'applicazione verrà eseguita in *modalità client*, **IPC\_API\_MODE\_CLIENT**.

Per altre informazioni sulla *modalità server*, vedere [Tipi di applicazioni](application-types.md).

**Importante**: la modalità di sicurezza deve essere impostata prima di chiamare qualsiasi altra funzione di Rights Management Services SDK 2.1. Dopo averla impostata, la modalità di sicurezza non può essere modificata per il processo corrente.

## <a name="related-topics"></a>Argomenti correlati

* [Tipi di applicazioni](application-types.md)
* [Valori della modalità API](https://msdn.microsoft.com/library/hh535236.aspx)
* [IpcSetGlobalProperty](https://msdn.microsoft.com/library/hh535270.aspx)
 

 



<!--HONumber=Nov16_HO2-->


