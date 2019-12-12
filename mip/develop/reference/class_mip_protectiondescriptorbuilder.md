---
title: Classe mip::ProtectionDescriptorBuilder
description: Documenta la classe MIP::p rotectiondescriptorbuilder dell'SDK Microsoft Information Protection (MIP).
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 10/29/2019
ms.openlocfilehash: cdc72fd45a4b82611aa02d0a9182cd829b6d8a9e
ms.sourcegitcommit: 474cd033de025bab280cb7a9721ac7ffc2d60b55
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/05/2019
ms.locfileid: "73560779"
---
# <a name="class-mipprotectiondescriptorbuilder"></a>Classe mip::ProtectionDescriptorBuilder 
Costruisce un ProtectionDescriptor che descrive la protezione associata a una porzione di contenuto.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public MIP_API std:: shared_ptr\<ProtectionDescriptor\> Build ()  |  Crea un ProtectionDescriptor le cui autorizzazioni di accesso sono definite da questa istanza di ProtectionDescriptorBuilder.
public void SetName(const std::string& value)  |  Imposta il nome dei criteri di protezione.
public void SetDescription(const std::string& value)  |  Imposta la descrizione dei criteri di protezione.
public void SetContentValidUntil (const std:: Chrono:: time_point\<std:: Chrono:: system_clock\>& value)  |  Imposta la descrizione dell'ora di scadenza dei criteri di protezione.
public void SetAllowOfflineAccess(bool value)  |  Imposta un valore che indica se i criteri di protezione consentono l'accesso al contenuto offline.
public void SetReferrer(const std::string& uri)  |  Imposta l'indirizzo del referrer dei criteri di protezione.
public void SetEncryptedAppData (const std:: Map\<std:: String, std:: String\>& value)  |  Imposta i dati specifici dell'app da crittografare.
public void SetSignedAppData (const std:: Map\<std:: String, std:: String\>& value)  |  Imposta i dati specifici dell'app da firmare.
public virtual ~ProtectionDescriptorBuilder()  | Non ancora documentato.
public static MIP_API std:: shared_ptr&lt;ProtectionDescriptorBuilder&gt; MIP::P rotectionDescriptorBuilder:: CreateFromUserRights | Crea un ProtectionDescriptorBuilder le cui autorizzazioni di accesso sono definite da utenti e diritti.
public static MIP_API std:: shared_ptr&lt;ProtectionDescriptorBuilder&gt; MIP::P rotectionDescriptorBuilder:: CreateFromUserRoles | Crea un ProtectionDescriptorBuilder le cui autorizzazioni di accesso sono definite da utenti e ruoli.
public static MIP_API std:: shared_ptr&lt;ProtectionDescriptorBuilder&gt; MIP::P rotectionDescriptorBuilder:: CreateFromTemplate | Crea un ProtectionDescriptorBuilder le cui autorizzazioni di accesso sono definite dal modello di protezione. 

## <a name="members"></a>Membri
  
### <a name="build-function"></a>Funzione di compilazione
Crea un ProtectionDescriptor le cui autorizzazioni di accesso sono definite da questa istanza di ProtectionDescriptorBuilder.

  
**Restituisce**: nuova istanza di ProtectionDescriptor
  
### <a name="setname-function"></a>Funzione Sename
Imposta il nome dei criteri di protezione.

Parametri:  
* **value**: nome dei criteri di protezione


  
### <a name="setdescription-function"></a>Funzione sedescription
Imposta la descrizione dei criteri di protezione.

Parametri:  
* **value**: descrizione del criterio


  
### <a name="setcontentvaliduntil-function"></a>SetContentValidUntil (funzione)
Imposta la descrizione dell'ora di scadenza dei criteri di protezione.

Parametri:  
* **value**: scadenza del criterio


  
### <a name="setallowofflineaccess-function"></a>SetAllowOfflineAccess (funzione)
Imposta un valore che indica se i criteri di protezione consentono l'accesso al contenuto offline.

Parametri:  
* **value**: valore che indica se i criteri consentono l'accesso al contenuto offline


  
### <a name="setreferrer-function"></a>SetReferrer (funzione)
Imposta l'indirizzo del referrer dei criteri di protezione.

Parametri:  
* **uri**: indirizzo del referrer del criterio


Il referrer è un URI che può essere visualizzato se l'acquisizione dei criteri di protezione non riesce e contiene informazioni sul modo in cui l'utente può ottenere l'autorizzazione ad accedere al contenuto.
  
### <a name="setencryptedappdata-function"></a>SetEncryptedAppData (funzione)
Imposta i dati specifici dell'app da crittografare.

Parametri:  
* **value**: dati specifici dell'app


Un'applicazione può specificare un dizionario di dati specifici dell'app che saranno crittografati dal servizio di protezione. Questi dati crittografati sono indipendenti dai dati firmati impostati da SetSignedAppData.
  
### <a name="setsignedappdata-function"></a>SetSignedAppData (funzione)
Imposta i dati specifici dell'app da firmare.

Parametri:  
* **value**: dati specifici dell'app


Un'applicazione può specificare un dizionario di dati specifici dell'app che saranno firmati dal servizio di protezione. Questi dati firmati sono indipendenti dai dati crittografati impostati da SetEncryptedAppData.
  
### <a name="protectiondescriptorbuilder-function"></a>~ ProtectionDescriptorBuilder (funzione)
_Non ancora documentato._

### <a name="createfromuserrights-function"></a>CreateFromUserRights (funzione)
Crea un ProtectionDescriptorBuilder le cui autorizzazioni di accesso sono definite da utenti e diritti.

Parametri:
* **usersAndRights**: raccolta di mapping tra utenti e diritti.

**Restituisce**: nuova istanza di [ProtectionDescriptor](class_mip_protectiondescriptor.md) 

### <a name="createfromuserroles-function"></a>CreateFromUserRoles (funzione)
Crea un ProtectionDescriptorBuilder le cui autorizzazioni di accesso sono definite da utenti e ruoli.

Parametri:
* **usersAndRoles**: raccolta di mapping tra utenti e ruoli.

**Returns**: crea un [ProtectionDescriptor](class_mip_protectiondescriptor.md) le cui autorizzazioni di accesso sono definite da utenti e ruoli.

### <a name="createfromtemplate-function"></a>CreateFromTemplate (funzione)
Crea un ProtectionDescriptorBuilder le cui autorizzazioni di accesso sono definite dal modello di protezione. 

Parametri:
* **TemplateID**: ID modello di protezione.

**Restituisce**: nuova istanza di [ProtectionDescriptor](class_mip_protectiondescriptor.md) .