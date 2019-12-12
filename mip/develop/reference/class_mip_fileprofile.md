---
title: Classe mip::FileProfile
description: "Documenta la classe MIP:: fileprofile dell'SDK Microsoft Information Protection (MIP)."
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 10/29/2019
ms.openlocfilehash: a436024aefe58a73ea03747fce5c5f2f4b4fc4b1
ms.sourcegitcommit: 474cd033de025bab280cb7a9721ac7ffc2d60b55
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/05/2019
ms.locfileid: "73558796"
---
# <a name="class-mipfileprofile"></a>Classe mip::FileProfile 
Fileprofile Class è la classe radice per l'uso delle operazioni di Microsoft Information Protection.
Un'applicazione comune richiede un solo profilo.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public const Settings& GetSettings() const  |  Restituisce le impostazioni del profilo.
public void ListEnginesAsync (const std:: shared_ptr\<void\>& context)  |  Avvia l'operazione di elenco motori.
public void UnloadEngineAsync (const std:: String & ID, const std:: shared_ptr\<void\>& context)  |  Avvia lo scaricamento del motore di file con l'ID specificato.
public void AddEngineAsync (const fileengine:: Settings & Settings, const std:: shared_ptr\<void\>& context)  |  Avvia l'aggiunta di un nuovo motore di file al profilo.
public void DeleteEngineAsync (const std:: String & ID, const std:: shared_ptr\<void\>& context)  |  Avvia l'eliminazione del motore di file con l'ID specificato. Tutti i dati per il profilo specificato verranno eliminati.
public static FILE_API void __CDECL MIP:: fileprofile:: LoadAsync | Avvia il caricamento di un profilo in base alle impostazioni fornite
public static const FILE_API char * __CDECL MIP:: fileprofile:: GetVersion | Ottiene la versione della libreria.

## <a name="members"></a>Membri
  
### <a name="getsettings-function"></a>GetSettings (funzione)
Restituisce le impostazioni del profilo.
  
### <a name="listenginesasync-function"></a>ListEnginesAsync (funzione)
Avvia l'operazione di elenco motori.
Fileprofile:: Observer verrà chiamato in caso di esito positivo o negativo.
  
### <a name="unloadengineasync-function"></a>UnloadEngineAsync (funzione)
Avvia lo scaricamento del motore di file con l'ID specificato.
Fileprofile:: Observer verrà chiamato in caso di esito positivo o negativo.
  
### <a name="addengineasync-function"></a>AddEngineAsync (funzione)
Avvia l'aggiunta di un nuovo motore di file al profilo.
Fileprofile:: Observer verrà chiamato in caso di esito positivo o negativo.
  
### <a name="deleteengineasync-function"></a>DeleteEngineAsync (funzione)
Avvia l'eliminazione del motore di file con l'ID specificato. Tutti i dati per il profilo specificato verranno eliminati.
Fileprofile:: Observer verrà chiamato in caso di esito positivo o negativo.

### <a name="loadasync-function"></a>LoadAsync (funzione)
Avvia il caricamento di un profilo in base alle impostazioni fornite.

In base all'esito positivo o negativo dell'operazione verrà chiamato [FileProfile::Observer](class_mip_fileprofile_observer.md).

### <a name="getversion-function"></a>GetVersion (funzione)
Ottiene la versione della libreria.