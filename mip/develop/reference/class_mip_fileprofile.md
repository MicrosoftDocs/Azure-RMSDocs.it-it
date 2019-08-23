---
title: Classe mip::FileProfile
description: "Documenta la classe MIP:: fileprofile dell'SDK Microsoft Information Protection (MIP)."
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 07/16/2019
ms.openlocfilehash: 00b56c5b45c8c05bf50229c3b462611ce48945c4
ms.sourcegitcommit: fcde8b31f8685023f002044d3a1d1903e548d207
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/21/2019
ms.locfileid: "69884284"
---
# <a name="class-mipfileprofile"></a>Classe mip::FileProfile 
[FileProfile](class_mip_fileprofile.md) è la classe radice per l'uso delle operazioni di Microsoft Information Protection.
Un'applicazione comune richiede un solo profilo.
  
## <a name="summary"></a>Riepilogo
 Members                        | Descrizioni                                
--------------------------------|---------------------------------------------
public const Settings& GetSettings() const  |  Restituisce le impostazioni del profilo.
public void ListEnginesAsync (const std::\<shared_ptr\>void & context)  |  Avvia l'operazione di elenco motori.
public void UnloadEngineAsync (const std:: String & ID, const std:\<:\>shared_ptr void & context)  |  Avvia lo scaricamento del motore di file con l'ID specificato.
public void AddEngineAsync (const fileengine:: Settings & Settings, const std:\<:\>shared_ptr void & context)  |  Avvia l'aggiunta di un nuovo motore di file al profilo.
public void DeleteEngineAsync (const std:: String & ID, const std:\<:\>shared_ptr void & context)  |  Avvia l'eliminazione del motore di file con l'ID specificato. Tutti i dati per il profilo specificato verranno eliminati.
  
## <a name="members"></a>Members
  
### <a name="getsettings-function"></a>GetSettings (funzione)
Restituisce le impostazioni del profilo.
  
### <a name="listenginesasync-function"></a>ListEnginesAsync (funzione)
Avvia l'operazione di elenco motori.
In base all'esito positivo o negativo dell'operazione verrà chiamato [FileProfile::Observer](class_mip_fileprofile_observer.md).
  
### <a name="unloadengineasync-function"></a>UnloadEngineAsync (funzione)
Avvia lo scaricamento del motore di file con l'ID specificato.
In base all'esito positivo o negativo dell'operazione verrà chiamato [FileProfile::Observer](class_mip_fileprofile_observer.md).
  
### <a name="addengineasync-function"></a>AddEngineAsync (funzione)
Avvia l'aggiunta di un nuovo motore di file al profilo.
In base all'esito positivo o negativo dell'operazione verrà chiamato [FileProfile::Observer](class_mip_fileprofile_observer.md).
  
### <a name="deleteengineasync-function"></a>DeleteEngineAsync (funzione)
Avvia l'eliminazione del motore di file con l'ID specificato. Tutti i dati per il profilo specificato verranno eliminati.
In base all'esito positivo o negativo dell'operazione verrà chiamato [FileProfile::Observer](class_mip_fileprofile_observer.md).