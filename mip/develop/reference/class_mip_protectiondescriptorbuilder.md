---
title: Classe ProtectionDescriptorBuilder
description: 'Documenta la classe protectiondescriptorbuilder:: undefined di Microsoft Information Protection (MIP) SDK.'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/13/2021
ms.openlocfilehash: 388e8b46aa125e3de2429098ec6a59b0ddb9fffc
ms.sourcegitcommit: 76926b357bbfc8772ed132ce5f2426fbea59e98b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/14/2021
ms.locfileid: "98214712"
---
# <a name="class-protectiondescriptorbuilder"></a>Classe ProtectionDescriptorBuilder 
Costruisce un ProtectionDescriptor che descrive la protezione associata a una parte del contenuto.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public MIP_API std::shared_ptr\<ProtectionDescriptor\> Build()  |  Crea una classe ProtectionDescriptor le cui autorizzazioni di accesso vengono definite da questa istanza di ProtectionDescriptorBuilder.
public void SetName(const std::string& value)  |  Imposta il nome dei criteri di protezione.
public void SetDescription(const std::string& value)  |  Imposta la descrizione dei criteri di protezione.
public void SetContentValidUntil (const std:: Chrono:: time_point \<std::chrono::system_clock\>& value)  |  Imposta la descrizione dell'ora di scadenza dei criteri di protezione.
public void SetAllowOfflineAccess(bool value)  |  Imposta un valore che indica se i criteri di protezione consentono l'accesso al contenuto offline.
public void SetReferrer(const std::string& uri)  |  Imposta l'indirizzo del referrer dei criteri di protezione.
public void SetEncryptedAppData (const std:: Map \<std::string, std::string\>& valore)  |  Imposta i dati specifici dell'app da crittografare.
public void SetSignedAppData (const std:: Map \<std::string, std::string\>& valore)  |  Imposta i dati specifici dell'app da firmare.
public void SetDoubleKeyUrl (const std:: String& doubleKeyUrl)  |  Imposta l'URL della chiave doppia da utilizzare per la protezione personalizzata.
  
## <a name="members"></a>Membri
  
### <a name="build-function"></a>Funzione di compilazione
Crea una classe ProtectionDescriptor le cui autorizzazioni di accesso vengono definite da questa istanza di ProtectionDescriptorBuilder.

  
**Restituisce**: nuova istanza di ProtectionDescriptor
  
### <a name="setname-function"></a>Funzione Sename
Imposta il nome dei criteri di protezione.

Parametri  
* **value**: nome dei criteri di protezione


  
### <a name="setdescription-function"></a>Funzione sedescription
Imposta la descrizione dei criteri di protezione.

Parametri  
* **valore**: Descrizione del criterio


  
### <a name="setcontentvaliduntil-function"></a>SetContentValidUntil (funzione)
Imposta la descrizione dell'ora di scadenza dei criteri di protezione.

Parametri  
* **valore**: ora di scadenza dei criteri


  
### <a name="setallowofflineaccess-function"></a>SetAllowOfflineAccess (funzione)
Imposta un valore che indica se i criteri di protezione consentono l'accesso al contenuto offline.

Parametri  
* **value**: valore che indica se i criteri consentono l'accesso al contenuto offline


  
### <a name="setreferrer-function"></a>SetReferrer (funzione)
Imposta l'indirizzo del referrer dei criteri di protezione.

Parametri  
* **uri**: indirizzo del referrer del criterio


Il referrer è un URI che può essere visualizzato se l'acquisizione dei criteri di protezione non riesce e contiene informazioni sul modo in cui l'utente può ottenere l'autorizzazione ad accedere al contenuto.
  
### <a name="setencryptedappdata-function"></a>SetEncryptedAppData (funzione)
Imposta i dati specifici dell'app da crittografare.

Parametri  
* **value**: dati specifici dell'app


Un'applicazione può specificare un dizionario di dati specifici dell'app che saranno crittografati dal servizio di protezione. Questi dati crittografati sono indipendenti dai dati firmati impostati da SetSignedAppData.
  
### <a name="setsignedappdata-function"></a>SetSignedAppData (funzione)
Imposta i dati specifici dell'app da firmare.

Parametri  
* **value**: dati specifici dell'app


Un'applicazione può specificare un dizionario di dati specifici dell'app che saranno firmati dal servizio di protezione. Questi dati firmati sono indipendenti dai dati crittografati impostati da SetEncryptedAppData.
  
### <a name="setdoublekeyurl-function"></a>SetDoubleKeyUrl (funzione)
Imposta l'URL della chiave doppia da utilizzare per la protezione personalizzata.

Parametri  
* **valore**: URL chiave doppia

