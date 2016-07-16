---
title: "Come impostare la modalità di sicurezza dell'API | Azure RMS"
description: "Scegliere la modalità di sicurezza eseguita dall'applicazione API file."
keywords: 
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 3B088F14-81C5-4C78-8DED-F5F153353EE0
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 11b998addd14fdde0592ed948b956ddb2ed6e570
ms.openlocfilehash: 2be40c9caf33f391f8be9fe116d3473ce995613b


---

# Procedura: Impostare la modalità di sicurezza dell'API

È possibile scegliere la modalità di sicurezza eseguita dall'applicazione API file tramite la funzione [**IpcSetGlobalProperty**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcsetglobalproperty).

Per inizializzare l'applicazione con esecuzione in *modalità server*, chiamare la funzione [**IpcSetGlobalProperty**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcsetglobalproperty) e impostare la modalità di sicurezza su [**IPC\_API\_MODE\_SERVER**](/rights-management/sdk/2.1/api/win/api%20mode%20values#msipc_api_mode_values_IPC_API_MODE_SERVER). Per impostazione predefinita l'applicazione verrà eseguita in *modalità client*, **IPC\_API\_MODE\_CLIENT**.

Per altre informazioni sulla *modalità server*, vedere [Tipi di applicazioni](application-types.md).

**Importante**: la modalità di sicurezza deve essere impostata prima di chiamare qualsiasi altra funzione di Rights Management Services SDK 2.1. Dopo averla impostata, la modalità di sicurezza non può essere modificata per il processo corrente.

## Argomenti correlati

* [Tipi di applicazioni](application-types.md)
* [**Valori della modalità API**](/rights-management/sdk/2.1/api/win/api%20mode%20values#msipc_api_mode_values_IPC_API_MODE_SERVER)
* [**IpcSetGlobalProperty**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcsetglobalproperty)
 

 



<!--HONumber=Jun16_HO4-->


