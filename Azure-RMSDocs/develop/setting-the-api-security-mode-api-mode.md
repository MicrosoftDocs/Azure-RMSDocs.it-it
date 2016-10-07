---
title: "Come impostare la modalità di sicurezza dell'API | Azure RMS"
description: "Scegliere la modalità di sicurezza eseguita dall'applicazione API file."
keywords: 
author: bruceperlerms
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
ms.sourcegitcommit: b4abffcbe6e49ea25f3cf493a1e68fcd6ea25b26
ms.openlocfilehash: f10129cb907cafa0e0c717b02153bbcdea012959


---

# Procedura: Impostare la modalità di sicurezza dell'API

È possibile scegliere la modalità di sicurezza eseguita dall'applicazione API file tramite la funzione [**IpcSetGlobalProperty**](/information-protection/sdk/2.1/api/win/functions#msipc_ipcsetglobalproperty).

Per inizializzare l'applicazione con esecuzione in *modalità server*, chiamare la funzione [**IpcSetGlobalProperty**](/information-protection/sdk/2.1/api/win/functions#msipc_ipcsetglobalproperty) e impostare la modalità di sicurezza su [**IPC\_API\_MODE\_SERVER**](/information-protection/sdk/2.1/api/win/api%20mode%20values#msipc_api_mode_values_IPC_API_MODE_SERVER). Per impostazione predefinita l'applicazione verrà eseguita in *modalità client*, **IPC\_API\_MODE\_CLIENT**.

Per altre informazioni sulla *modalità server*, vedere [Tipi di applicazioni](application-types.md).

**Importante**: la modalità di sicurezza deve essere impostata prima di chiamare qualsiasi altra funzione di Rights Management Services SDK 2.1. Dopo averla impostata, la modalità di sicurezza non può essere modificata per il processo corrente.

## Argomenti correlati

* [Tipi di applicazioni](application-types.md)
* [**Valori della modalità API**](/information-protection/sdk/2.1/api/win/api%20mode%20values#msipc_api_mode_values_IPC_API_MODE_SERVER)
* [**IpcSetGlobalProperty**](/information-protection/sdk/2.1/api/win/functions#msipc_ipcsetglobalproperty)
 

 



<!--HONumber=Sep16_HO5-->


