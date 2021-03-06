---
title: Classe fileprofile
description: 'Documents The fileprofile:: undefined Class of the Microsoft Information Protection (MIP) SDK.'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/13/2021
ms.openlocfilehash: 10c5656328377a3ced0e24de22d957d016adf396
ms.sourcegitcommit: 76926b357bbfc8772ed132ce5f2426fbea59e98b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/14/2021
ms.locfileid: "98211601"
---
# <a name="class-fileprofile"></a>Classe fileprofile 
FileProfile è la classe radice per l'uso delle operazioni di Microsoft Information Protection.
Un'applicazione comune richiede un solo profilo.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public const Settings& GetSettings() const  |  Restituisce le impostazioni del profilo.
public std:: shared_ptr \<AsyncControl\> ListEnginesAsync (const std:: shared_ptr \<void\>& context)  |  Avvia l'operazione di elenco motori.
public std:: shared_ptr \<AsyncControl\> UnloadEngineAsync (const std:: string& ID, const std:: shared_ptr \<void\>& context)  |  Avvia lo scaricamento del motore di file con l'ID specificato.
public std:: shared_ptr \<AsyncControl\> AddEngineAsync (const fileengine:: settings& Settings, const std:: shared_ptr \<void\>& context)  |  Avvia l'aggiunta di un nuovo motore di file al profilo.
public std:: shared_ptr \<AsyncControl\> DeleteEngineAsync (const std:: string& ID, const std:: shared_ptr \<void\>& context)  |  Avvia l'eliminazione del motore di file con l'ID specificato. Tutti i dati per il profilo specificato verranno eliminati.
public void AcquirePolicyAuthToken (Cloud Cloud, const std:: shared_ptr \<AuthDelegate\>& authDelegate) const  |  Attivare un callback di autenticazione per i criteri.
  
## <a name="members"></a>Membri
  
### <a name="getsettings-function"></a>GetSettings (funzione)
Restituisce le impostazioni del profilo.
  
### <a name="listenginesasync-function"></a>ListEnginesAsync (funzione)
Avvia l'operazione di elenco motori.

  
**Restituisce**: oggetto controllo asincrono.
In base all'esito positivo o negativo dell'operazione verrà chiamato FileProfile::Observer.
  
### <a name="unloadengineasync-function"></a>UnloadEngineAsync (funzione)
Avvia lo scaricamento del motore di file con l'ID specificato.

  
**Restituisce**: oggetto controllo asincrono.
In base all'esito positivo o negativo dell'operazione verrà chiamato FileProfile::Observer.
  
### <a name="addengineasync-function"></a>AddEngineAsync (funzione)
Avvia l'aggiunta di un nuovo motore di file al profilo.

  
**Restituisce**: oggetto controllo asincrono.
In base all'esito positivo o negativo dell'operazione verrà chiamato FileProfile::Observer.
  
### <a name="deleteengineasync-function"></a>DeleteEngineAsync (funzione)
Avvia l'eliminazione del motore di file con l'ID specificato. Tutti i dati per il profilo specificato verranno eliminati.

  
**Restituisce**: oggetto controllo asincrono.
In base all'esito positivo o negativo dell'operazione verrà chiamato FileProfile::Observer.
  
### <a name="acquirepolicyauthtoken-function"></a>AcquirePolicyAuthToken (funzione)
Attivare un callback di autenticazione per i criteri.

Parametri  
* **cloud**: cloud di Azure 


* **authDelegate**: callback di autenticazione che verrà richiamato


MIP non memorizza nella cache o non esegue altre operazioni con il valore restituito dal delegato di autenticazione. Questa funzione è consigliata per le applicazioni che non sono "connesse" fino a quando MIP richiede un token di autenticazione. Consente a un'applicazione di recuperare un token prima che MIP ne richieda effettivamente uno.