---
title: Classe mip ProtectionDescriptorBuilder
description: Riferimento per la classe mip ProtectionDescriptorBuilder
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: 42e44cfaf269a43d0210c0c040ea70ccc1fb192e
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/28/2018
ms.locfileid: "47446635"
---
# <a name="class-mipprotectiondescriptorbuilder"></a>Classe mip::ProtectionDescriptorBuilder 
Costruisce un [ProtectionDescriptor](class_mip_protectiondescriptor.md) che descrive la protezione associata a una parte del contenuto.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public MIP_API std::shared_ptr<ProtectionDescriptor> Build()  |  Crea una classe [ProtectionDescriptor](class_mip_protectiondescriptor.md) le cui autorizzazioni di accesso vengono definite da questa istanza di [ProtectionDescriptorBuilder](class_mip_protectiondescriptorbuilder.md).
 public void SetName(const std::string& value)  |  Imposta il nome dei criteri di protezione.
 public void SetDescription(const std::string& value)  |  Imposta la descrizione dei criteri di protezione.
public void SetContentValidUntil(const std::chrono::time_point<std::chrono::system_clock>& value)  |  Imposta la descrizione dell'ora di scadenza dei criteri di protezione.
 public void SetAllowOfflineAccess(bool value)  |  Imposta un valore che indica se i criteri di protezione consentono l'accesso al contenuto offline.
 public void SetReferrer(const std::string& uri)  |  Imposta l'indirizzo del referrer dei criteri di protezione.
public void SetEncryptedAppData(const std::map<std::string, std::string>& value)  |  Imposta i dati specifici dell'app da crittografare.
public void SetSignedAppData(const std::map<std::string, std::string>& value)  |  Imposta i dati specifici dell'app da firmare.
 public virtual ~ProtectionDescriptorBuilder()  | _Non ancora documentato._
  
## <a name="members"></a>Membri
  
### <a name="protectiondescriptor"></a>ProtectionDescriptor
Crea una classe [ProtectionDescriptor](class_mip_protectiondescriptor.md) le cui autorizzazioni di accesso vengono definite da questa istanza di [ProtectionDescriptorBuilder](class_mip_protectiondescriptorbuilder.md).

  
**Restituisce**: nuova istanza di [ProtectionDescriptor](class_mip_protectiondescriptor.md)
  
### <a name="setname"></a>SetName
Imposta il nome dei criteri di protezione.

Parametri:  
* **value**: nome dei criteri di protezione


  
### <a name="setdescription"></a>SetDescription
Imposta la descrizione dei criteri di protezione.

Parametri:  
* **value**: descrizione del criterio


  
### <a name="setcontentvaliduntil"></a>SetContentValidUntil
Imposta la descrizione dell'ora di scadenza dei criteri di protezione.

Parametri:  
* **value**: scadenza del criterio


  
### <a name="setallowofflineaccess"></a>SetAllowOfflineAccess
Imposta un valore che indica se i criteri di protezione consentono l'accesso al contenuto offline.

Parametri:  
* **value**: valore che indica se i criteri consentono l'accesso al contenuto offline


  
### <a name="setreferrer"></a>SetReferrer
Imposta l'indirizzo del referrer dei criteri di protezione.

Parametri:  
* **uri**: indirizzo del referrer del criterio


Il referrer è un URI che può essere visualizzato se l'acquisizione dei criteri di protezione non riesce e contiene informazioni sul modo in cui l'utente può ottenere l'autorizzazione ad accedere al contenuto.
  
### <a name="setencryptedappdata"></a>SetEncryptedAppData
Imposta i dati specifici dell'app da crittografare.

Parametri:  
* **value**: dati specifici dell'app


Un'applicazione può specificare un dizionario di dati specifici dell'app che saranno crittografati dal servizio di protezione. Questi dati crittografati sono indipendenti dai dati firmati impostati da SetSignedAppData.
  
### <a name="setsignedappdata"></a>SetSignedAppData
Imposta i dati specifici dell'app da firmare.

Parametri:  
* **value**: dati specifici dell'app


Un'applicazione può specificare un dizionario di dati specifici dell'app che saranno firmati dal servizio di protezione. Questi dati firmati sono indipendenti dai dati crittografati impostati da SetEncryptedAppData.
  
### <a name="protectiondescriptorbuilder"></a>~ProtectionDescriptorBuilder
_Non ancora documentato._
