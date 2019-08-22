---
title: Classe mip::ProtectionDescriptorBuilder
description: Documenta la classe MIP::p rotectiondescriptorbuilder dell'SDK Microsoft Information Protection (MIP).
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 07/16/2019
ms.openlocfilehash: 5985aad4f4cb9b8276ca855026119507febc9445
ms.sourcegitcommit: fcde8b31f8685023f002044d3a1d1903e548d207
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/21/2019
ms.locfileid: "69885118"
---
# <a name="class-mipprotectiondescriptorbuilder"></a>Classe mip::ProtectionDescriptorBuilder 
Costruisce un [ProtectionDescriptor](class_mip_protectiondescriptor.md) che descrive la protezione associata a una parte del contenuto.
  
## <a name="summary"></a>Riepilogo
 Members                        | Descrizioni                                
--------------------------------|---------------------------------------------
public MIP_API std:: shared_ptr\<ProtectionDescriptor\> Build ()  |  Crea una classe [ProtectionDescriptor](class_mip_protectiondescriptor.md) le cui autorizzazioni di accesso vengono definite da questa istanza di [ProtectionDescriptorBuilder](class_mip_protectiondescriptorbuilder.md).
public void SetName(const std::string& value)  |  Imposta il nome dei criteri di protezione.
public void SetDescription(const std::string& value)  |  Imposta la descrizione dei criteri di protezione.
public void SetContentValidUntil (const std:: Chrono::\<time_point std:: Chrono::\>system_clock & valore)  |  Imposta la descrizione dell'ora di scadenza dei criteri di protezione.
public void SetAllowOfflineAccess(bool value)  |  Imposta un valore che indica se i criteri di protezione consentono l'accesso al contenuto offline.
public void SetReferrer(const std::string& uri)  |  Imposta l'indirizzo del referrer dei criteri di protezione.
public void SetEncryptedAppData (const std::\<map std:: String, std::\>String & valore)  |  Imposta i dati specifici dell'app da crittografare.
public void SetSignedAppData (const std::\<map std:: String, std::\>String & valore)  |  Imposta i dati specifici dell'app da firmare.
public virtual ~ProtectionDescriptorBuilder()  | _Non ancora documentato._
  
## <a name="members"></a>Members
  
### <a name="build-function"></a>Funzione di compilazione
Crea una classe [ProtectionDescriptor](class_mip_protectiondescriptor.md) le cui autorizzazioni di accesso vengono definite da questa istanza di [ProtectionDescriptorBuilder](class_mip_protectiondescriptorbuilder.md).

  
**Restituisce**: Nuova istanza di [ProtectionDescriptor](class_mip_protectiondescriptor.md)
  
### <a name="setname-function"></a>Funzione Sename
Imposta il nome dei criteri di protezione.

Parametri:  
* **valore**: Nome dei criteri di protezione


  
### <a name="setdescription-function"></a>Funzione sedescription
Imposta la descrizione dei criteri di protezione.

Parametri:  
* **valore**: Descrizione del criterio


  
### <a name="setcontentvaliduntil-function"></a>SetContentValidUntil (funzione)
Imposta la descrizione dell'ora di scadenza dei criteri di protezione.

Parametri:  
* **valore**: Scadenza del criterio


  
### <a name="setallowofflineaccess-function"></a>SetAllowOfflineAccess (funzione)
Imposta un valore che indica se i criteri di protezione consentono l'accesso al contenuto offline.

Parametri:  
* **valore**: Se il criterio consente l'accesso al contenuto offline


  
### <a name="setreferrer-function"></a>SetReferrer (funzione)
Imposta l'indirizzo del referrer dei criteri di protezione.

Parametri:  
* **URI**: Indirizzo del referrer del criterio


Il referrer è un URI che può essere visualizzato se l'acquisizione dei criteri di protezione non riesce e contiene informazioni sul modo in cui l'utente può ottenere l'autorizzazione ad accedere al contenuto.
  
### <a name="setencryptedappdata-function"></a>SetEncryptedAppData (funzione)
Imposta i dati specifici dell'app da crittografare.

Parametri:  
* **valore**: Dati specifici dell'app


Un'applicazione può specificare un dizionario di dati specifici dell'app che saranno crittografati dal servizio di protezione. Questi dati crittografati sono indipendenti dai dati firmati impostati da SetSignedAppData.
  
### <a name="setsignedappdata-function"></a>SetSignedAppData (funzione)
Imposta i dati specifici dell'app da firmare.

Parametri:  
* **valore**: Dati specifici dell'app


Un'applicazione può specificare un dizionario di dati specifici dell'app che saranno firmati dal servizio di protezione. Questi dati firmati sono indipendenti dai dati crittografati impostati da SetEncryptedAppData.
  
### <a name="protectiondescriptorbuilder-function"></a>~ ProtectionDescriptorBuilder (funzione)
_Non ancora documentato._
