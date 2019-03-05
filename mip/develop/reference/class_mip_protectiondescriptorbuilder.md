---
title: Classe mip::ProtectionDescriptorBuilder
description: Documenta la classe mip::protectiondescriptorbuilder di Microsoft Information Protection (MIP) SDK.
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: 7ed2c118d2f57f93d0445c113fd6127704e52637
ms.sourcegitcommit: 471b3683367d93f0673c1cf276a15f83572aa80e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/05/2019
ms.locfileid: "57331376"
---
# <a name="class-mipprotectiondescriptorbuilder"></a>Classe mip::ProtectionDescriptorBuilder 
Costruisce un [ProtectionDescriptor](class_mip_protectiondescriptor.md) che descrive la protezione associata a una parte del contenuto.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
Public std:: shared_ptr MIP_API\<ProtectionDescriptor\> Build()  |  Crea una classe [ProtectionDescriptor](class_mip_protectiondescriptor.md) le cui autorizzazioni di accesso vengono definite da questa istanza di [ProtectionDescriptorBuilder](class_mip_protectiondescriptorbuilder.md).
public void SetName(const std::string& value)  |  Imposta il nome dei criteri di protezione.
public void SetDescription(const std::string& value)  |  Imposta la descrizione dei criteri di protezione.
public void SetContentValidUntil (const std::chrono::time_point\<std\>& valore)  |  Imposta la descrizione dell'ora di scadenza dei criteri di protezione.
public void SetAllowOfflineAccess(bool value)  |  Imposta un valore che indica se i criteri di protezione consentono l'accesso al contenuto offline.
public void SetReferrer(const std::string& uri)  |  Imposta l'indirizzo del referrer dei criteri di protezione.
public void SetEncryptedAppData (const std:: map\<std:: String, std:: String\>& valore)  |  Imposta i dati specifici dell'app da crittografare.
public void SetSignedAppData (const std:: map\<std:: String, std:: String\>& valore)  |  Imposta i dati specifici dell'app da firmare.
public virtual ~ProtectionDescriptorBuilder()  | _Non ancora documentato._
  
## <a name="members"></a>Membri
  
### <a name="build-function"></a>Compilare (funzione)
Crea una classe [ProtectionDescriptor](class_mip_protectiondescriptor.md) le cui autorizzazioni di accesso vengono definite da questa istanza di [ProtectionDescriptorBuilder](class_mip_protectiondescriptorbuilder.md).

  
**Restituisce**: Nuove [ProtectionDescriptor](class_mip_protectiondescriptor.md) istanza
  
### <a name="setname-function"></a>SetName (funzione)
Imposta il nome dei criteri di protezione.

Parametri:  
* **value**: Nome dei criteri di protezione


  
### <a name="setdescription-function"></a>SetDescription (funzione)
Imposta la descrizione dei criteri di protezione.

Parametri:  
* **value**: Descrizione del criterio


  
### <a name="setcontentvaliduntil-function"></a>SetContentValidUntil (funzione)
Imposta la descrizione dell'ora di scadenza dei criteri di protezione.

Parametri:  
* **value**: Scadenza del criterio


  
### <a name="setallowofflineaccess-function"></a>SetAllowOfflineAccess (funzione)
Imposta un valore che indica se i criteri di protezione consentono l'accesso al contenuto offline.

Parametri:  
* **value**: Se i criteri consentono l'accesso al contenuto offline o non


  
### <a name="setreferrer-function"></a>SetReferrer (funzione)
Imposta l'indirizzo del referrer dei criteri di protezione.

Parametri:  
* **uri**: Indirizzo del referrer del criterio


Il referrer è un URI che può essere visualizzato se l'acquisizione dei criteri di protezione non riesce e contiene informazioni sul modo in cui l'utente può ottenere l'autorizzazione ad accedere al contenuto.
  
### <a name="setencryptedappdata-function"></a>SetEncryptedAppData (funzione)
Imposta i dati specifici dell'app da crittografare.

Parametri:  
* **value**: Dati specifici dell'App


Un'applicazione può specificare un dizionario di dati specifici dell'app che saranno crittografati dal servizio di protezione. Questi dati crittografati sono indipendenti dai dati firmati impostati da SetSignedAppData.
  
### <a name="setsignedappdata-function"></a>SetSignedAppData (funzione)
Imposta i dati specifici dell'app da firmare.

Parametri:  
* **value**: Dati specifici dell'App


Un'applicazione può specificare un dizionario di dati specifici dell'app che saranno firmati dal servizio di protezione. Questi dati firmati sono indipendenti dai dati crittografati impostati da SetEncryptedAppData.
  
### <a name="protectiondescriptorbuilder-function"></a>~ ProtectionDescriptorBuilder (funzione)
_Non ancora documentato._
