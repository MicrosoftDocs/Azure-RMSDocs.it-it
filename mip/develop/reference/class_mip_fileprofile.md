---
title: Classe mip::FileProfile
description: 'Classe MIP:: fileprofile di Microsoft Information Protection (MIP) SDK vengono documentate.'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: 4bdd96e7f9f414062d969de1ffaf7195ad71d214
ms.sourcegitcommit: 471b3683367d93f0673c1cf276a15f83572aa80e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/05/2019
ms.locfileid: "57329404"
---
# <a name="class-mipfileprofile"></a>Classe mip::FileProfile 
[FileProfile](class_mip_fileprofile.md) è la classe radice per l'uso delle operazioni di Microsoft Information Protection.
Un'applicazione comune richiede un solo profilo.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public const Settings& GetSettings() const  |  Restituisce le impostazioni del profilo.
public void ListEnginesAsync (const std:: shared_ptr\<void\>& contesto)  |  Avvia l'operazione di elenco motori.
public void UnloadEngineAsync (const std:: String & id, const std:: shared_ptr\<void\>& contesto)  |  Avvia lo scaricamento del motore di file con l'ID specificato.
pubblica AddEngineAsync void (FileEngine::Settings const & impostazioni, const std:: shared_ptr\<void\>& contesto)  |  Avvia l'aggiunta di un nuovo motore di file al profilo.
public void DeleteEngineAsync (const std:: String & id, const std:: shared_ptr\<void\>& contesto)  |  Avvia l'eliminazione del motore di file con l'ID specificato. Tutti i dati per il profilo specificato verranno eliminati.
  
## <a name="members"></a>Membri
  
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
