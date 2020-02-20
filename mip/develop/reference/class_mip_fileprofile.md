---
title: Classe mip::FileProfile
description: "Documenta la classe MIP:: fileprofile dell'SDK Microsoft Information Protection (MIP)."
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 02/14/2020
ms.openlocfilehash: 44d6024473555c0745ff3156ff5cd004f83b6f6b
ms.sourcegitcommit: 2d3c638fb576f3f074330a33d077db0cf0e7d4e7
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/20/2020
ms.locfileid: "77488144"
---
# <a name="class-mipfileprofile"></a>Classe mip::FileProfile 
Fileprofile Class è la classe radice per l'uso delle operazioni di Microsoft Information Protection.
Un'applicazione comune richiede un solo profilo.
  
## <a name="summary"></a>Riepilogo
 Members                        | Descrizioni                                
--------------------------------|---------------------------------------------
public const Settings& GetSettings() const  |  Restituisce le impostazioni del profilo.
public std:: shared_ptr\<AsyncControl\> ListEnginesAsync (const std:: shared_ptr\<void\>& context)  |  Avvia l'operazione di elenco motori.
public std:: shared_ptr\<AsyncControl\> UnloadEngineAsync (const std:: String & ID, const std:: shared_ptr\<void\>& context)  |  Avvia lo scaricamento del motore di file con l'ID specificato.
public std:: shared_ptr\<AsyncControl\> AddEngineAsync (const fileengine:: Settings & Settings, const std:: shared_ptr\<void\>& context)  |  Avvia l'aggiunta di un nuovo motore di file al profilo.
public std:: shared_ptr\<AsyncControl\> DeleteEngineAsync (const std:: String & ID, const std:: shared_ptr\<void\>& context)  |  Avvia l'eliminazione del motore di file con l'ID specificato. Tutti i dati per il profilo specificato verranno eliminati.
  
## <a name="members"></a>Members
  
### <a name="getsettings-function"></a>GetSettings (funzione)
Restituisce le impostazioni del profilo.
  
### <a name="listenginesasync-function"></a>ListEnginesAsync (funzione)
Avvia l'operazione di elenco motori.

  
**Restituisce**: oggetto controllo asincrono.
Fileprofile:: Observer verrà chiamato in caso di esito positivo o negativo.
  
### <a name="unloadengineasync-function"></a>UnloadEngineAsync (funzione)
Avvia lo scaricamento del motore di file con l'ID specificato.

  
**Restituisce**: oggetto controllo asincrono.
Fileprofile:: Observer verrà chiamato in caso di esito positivo o negativo.
  
### <a name="addengineasync-function"></a>AddEngineAsync (funzione)
Avvia l'aggiunta di un nuovo motore di file al profilo.

  
**Restituisce**: oggetto controllo asincrono.
Fileprofile:: Observer verrà chiamato in caso di esito positivo o negativo.
  
### <a name="deleteengineasync-function"></a>DeleteEngineAsync (funzione)
Avvia l'eliminazione del motore di file con l'ID specificato. Tutti i dati per il profilo specificato verranno eliminati.

  
**Restituisce**: oggetto controllo asincrono.
Fileprofile:: Observer verrà chiamato in caso di esito positivo o negativo.