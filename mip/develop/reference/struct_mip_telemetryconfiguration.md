---
title: 'struct MIP:: TelemetryConfiguration'
description: Documents Structures associati a Microsoft Information Protection (MIP) SDK.
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 10/29/2019
ms.openlocfilehash: 4e3e9be086bbcddea5398ccfbe549ffc2ca1aae6
ms.sourcegitcommit: 474cd033de025bab280cb7a9721ac7ffc2d60b55
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/05/2019
ms.locfileid: "73567528"
---
# <a name="struct-miptelemetryconfiguration"></a>struct MIP:: TelemetryConfiguration 
Impostazioni di telemetria personalizzate (non usate comunemente)
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public std:: String hostNameOverride  |  Nome dell'istanza di telemetria host. Se non è impostato, MIP fungerà da host.
public std:: String libraryNameOverride  |  Nome file della libreria di telemetria alternativa (DLL).
public std:: shared_ptr\<HttpDelegate\> httpDelegateOverride  |  Se impostato, la gestione HTTP verrà gestita da questa istanza
public std:: shared_ptr\<TaskDispatcherDelegate\> taskDispatcherDelegateOverride  |  Se impostato, la gestione asincrona delle attività verrà gestita da questa istanza, taskDispatcherDelegateOverides non deve essere condivisa perché può contenere oggetti di telemetria e impedire il rilascio fino a quando non viene liberato taskDispatcher.
public bool isNetworkDetectionEnabled  |  Se impostato, il componente di telemetria effettuerà il ping dello stato della rete sul thread in background
public bool isLocalCachingEnabled  |  Se impostato, il componente di telemetria utilizzerà la memorizzazione nella cache su disco
public bool isTraceLoggingEnabled  |  Se impostato, il componente di telemetria scriverà i log di avviso/errore sul disco
public bool isTelemetryOptedOut  |  Se impostato, verranno inviati solo i dati di telemetria del servizio necessari
public bool isFastShutdownEnabled  |  Se impostato, nessun evento verrà caricato al momento dell'arresto, gli eventi di controllo verranno caricati immediatamente dopo la registrazione
public std:: Map\<std:: String, std:: String\> customSettings  |  Impostazioni di telemetria personalizzate >
  
## <a name="members"></a>Membri
  
### <a name="hostnameoverride-struct-member"></a>membro struct hostNameOverride
Nome dell'istanza di telemetria host. Se non è impostato, MIP fungerà da host.
  
### <a name="librarynameoverride-struct-member"></a>membro struct libraryNameOverride
Nome file della libreria di telemetria alternativa (DLL).
  
### <a name="httpdelegate"></a>HttpDelegate
Se impostato, la gestione HTTP verrà gestita da questa istanza
  
### <a name="taskdispatcherdelegate"></a>TaskDispatcherDelegate
Se impostato, la gestione asincrona delle attività verrà gestita da questa istanza, taskDispatcherDelegateOverides non deve essere condivisa perché può contenere oggetti di telemetria e impedire il rilascio fino a quando non viene liberato taskDispatcher.
  
### <a name="isnetworkdetectionenabled-struct-member"></a>membro struct isNetworkDetectionEnabled
Se impostato, il componente di telemetria effettuerà il ping dello stato della rete sul thread in background
  
### <a name="islocalcachingenabled-struct-member"></a>membro struct isLocalCachingEnabled
Se impostato, il componente di telemetria utilizzerà la memorizzazione nella cache su disco
  
### <a name="istraceloggingenabled-struct-member"></a>membro struct isTraceLoggingEnabled
Se impostato, il componente di telemetria scriverà i log di avviso/errore sul disco
  
### <a name="istelemetryoptedout-struct-member"></a>membro struct isTelemetryOptedOut
Se impostato, verranno inviati solo i dati di telemetria del servizio necessari
  
### <a name="isfastshutdownenabled-struct-member"></a>membro struct isFastShutdownEnabled
Se impostato, nessun evento verrà caricato al momento dell'arresto, gli eventi di controllo verranno caricati immediatamente dopo la registrazione
  
### <a name="customsettings-struct-member"></a>membro struct customSettings
Impostazioni di telemetria personalizzate >