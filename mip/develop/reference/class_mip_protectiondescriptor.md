---
title: Classe mip::ProtectionDescriptor
description: Documenta la classe mip::protectiondescriptor di Microsoft Information Protection (MIP) SDK.
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: d04d1fe3c3d59592084a60b68d50d74ae10291c0
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/14/2019
ms.locfileid: "56259627"
---
# <a name="class-mipprotectiondescriptor"></a>Classe mip::ProtectionDescriptor 
Descrizione della protezione associata a una parte del contenuto.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public ProtectionType GetProtectionType() const  |  Ottiene il tipo di protezione, indipendentemente dal fatto che abbia avuto origine da un modello di SDK di protezione o meno.
public std::string GetOwner() const  |  Ottiene il proprietario per la protezione.
public std::string GetName() const  |  Ottiene il nome della protezione.
public std::string GetDescription() const  |  Ottiene la descrizione della protezione.
public std::string GetTemplateId() const  |  Ottiene l'ID del modello di protezione, se presente.
public std::string GetLabelId() const  |  Ottiene l'ID etichetta, se presente.
Public std:: Vector\<UserRights\> GetUserRights() const  |  Ottiene una raccolta di mapping dei diritti agli utenti.
Public std:: Vector\<UserRoles\> GetUserRoles() const  |  Ottiene una raccolta di mapping dei ruoli agli utenti.
public bool DoesContentExpire() const  |  Controlla se il contenuto contiene un'ora di scadenza o meno.
public std::chrono::time_point\<std::chrono::system_clock\> GetContentValidUntil() const  |  Ottiene l'ora di scadenza della protezione.
public bool DoesAllowOfflineAccess() const  |  Ottiene un valore che indica se la protezione consente o meno l'accesso al contenuto offline.
public std::string GetReferrer() const  |  Ottiene l'indirizzo del referrer della protezione.
Public std:: map\<std:: String, std:: String\> GetEncryptedAppData() const  |  Ottiene i dati specifici dell'app che sono stati crittografati.
Public std:: map\<std:: String, std:: String\> GetSignedAppData() const  |  Ottiene i dati specifici dell'app che sono stati firmati.
  
## <a name="members"></a>Membri
  
### <a name="getprotectiontype-function"></a>GetProtectionType (funzione)
Ottiene il tipo di protezione, indipendentemente dal fatto che abbia avuto origine da un modello di SDK di protezione o meno.

  
**Restituisce**: Tipo di protezione
  
### <a name="getowner-function"></a>GetOwner (funzione)
Ottiene il proprietario per la protezione.

  
**Restituisce**: Proprietario della protezione
  
### <a name="getname-function"></a>GetName (funzione)
Ottiene il nome della protezione.

  
**Restituisce**: Nome di protezione dati
  
### <a name="getdescription-function"></a>GetDescription (funzione)
Ottiene la descrizione della protezione.

  
**Restituisce**: Descrizione di protezione
  
### <a name="gettemplateid-function"></a>GetTemplateId (funzione)
Ottiene l'ID del modello di protezione, se presente.

  
**Restituisce**: ID del modello
  
### <a name="getlabelid-function"></a>GetLabelId (funzione)
Ottiene l'ID etichetta, se presente.

  
**Restituisce**: [Etichetta](class_mip_label.md) contenuto protetto con ID di questa proprietà verrà popolata solo in ProtectionDescriptors per preesistente. È un campo popolato dal server nel momento in cui il contenuto protetto viene utilizzato.
  
### <a name="getuserrights-function"></a>GetUserRights (funzione)
Ottiene una raccolta di mapping dei diritti agli utenti.

  
**Restituisce**: Raccolta di mapping dei diritti agli utenti il valore della [UserRights](class_mip_userrights.md) proprietà sarà vuota se l'utente corrente non ha accesso a queste informazioni (vale a dire, se l'utente non è il proprietario e non dispone del diritto VIEWRIGHTSDATA).
  
### <a name="getuserroles-function"></a>GetUserRoles (funzione)
Ottiene una raccolta di mapping dei ruoli agli utenti.

  
**Restituisce**: Raccolta di mapping dei ruoli agli utenti
  
### <a name="doescontentexpire-function"></a>DoesContentExpire (funzione)
Controlla se il contenuto contiene un'ora di scadenza o meno.

  
**Restituisce**: True se il contenuto può scadere, in caso contrario false
  
### <a name="getcontentvaliduntil-function"></a>GetContentValidUntil (funzione)
Ottiene l'ora di scadenza della protezione.

  
**Restituisce**: Ora di scadenza di protezione
  
### <a name="doesallowofflineaccess-function"></a>DoesAllowOfflineAccess (funzione)
Ottiene un valore che indica se la protezione consente o meno l'accesso al contenuto offline.

  
**Restituisce**: Se protezione dati consente l'accesso al contenuto offline o non (predefinito = true)
  
### <a name="getreferrer-function"></a>GetReferrer (funzione)
Ottiene l'indirizzo del referrer della protezione.

  
**Restituisce**: Indirizzo del referrer protezione il referrer è un URI che è visualizzabile all'utente se è possibile disattivare la protezione del contenuto. Contiene informazioni sul modo in cui tale utente può ottenere l'autorizzazione per accedere al contenuto.
  
### <a name="getencryptedappdata-function"></a>Funzione GetEncryptedAppData
Ottiene i dati specifici dell'app che sono stati crittografati.

  
**Restituisce**: Dati specifici dell'App un [ProtectionHandler](class_mip_protectionhandler.md) può contenere un dizionario di dati specifici dell'app è stata crittografata con il servizio di protezione. Questi dati crittografati sono indipendenti dai dati firmati accessibili tramite [ProtectionDescriptor::GetSignedAppData](class_mip_protectiondescriptor.md#getappsigneddata-function)
  
### <a name="getsignedappdata-function"></a>Funzione GetSignedAppData
Ottiene i dati specifici dell'app che sono stati firmati.

  
**Restituisce**: Dati specifici dell'App un [ProtectionHandler](class_mip_protectionhandler.md) può contenere un dizionario di dati specifici dell'app che sono stati firmati dal servizio di protezione. Questi dati firmati sono indipendenti dai dati crittografati accessibili tramite [ProtectionDescriptor::GetEncryptedAppData](class_mip_protectiondescriptor.md#getencryptedappdata-function)
