---
title: Classe mip ProtectionDescriptor
description: Riferimento per la classe mip ProtectionDescriptor
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: e723041af1eec7be7a839bf36f6d3db67b32447f
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/28/2018
ms.locfileid: "47446550"
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
public std::vector<UserRights> GetUserRights() const  |  Ottiene una raccolta di mapping dei diritti agli utenti.
public std::vector<UserRoles> GetUserRoles() const  |  Ottiene una raccolta di mapping dei ruoli agli utenti.
public std::chrono::time_point<std::chrono::system_clock> GetContentValidUntil() const  |  Ottiene l'ora di scadenza della protezione.
 public bool DoesAllowOfflineAccess() const  |  Ottiene un valore che indica se la protezione consente o meno l'accesso al contenuto offline.
 public std::string GetReferrer() const  |  Ottiene l'indirizzo del referrer della protezione.
public std::map<std::string, std::string> GetEncryptedAppData() const  |  Ottiene i dati specifici dell'app che sono stati crittografati.
public std::map<std::string, std::string> GetSignedAppData() const  |  Ottiene i dati specifici dell'app che sono stati firmati.
  
## <a name="members"></a>Membri
  
### <a name="protectiontype"></a>ProtectionType
Ottiene il tipo di protezione, indipendentemente dal fatto che abbia avuto origine da un modello di SDK di protezione o meno.

  
**Restituisce**: tipo di protezione
  
### <a name="getowner"></a>GetOwner
Ottiene il proprietario per la protezione.

  
**Restituisce**: proprietario della protezione
  
### <a name="getname"></a>GetName
Ottiene il nome della protezione.

  
**Restituisce**: nome della protezione
  
### <a name="getdescription"></a>GetDescription
Ottiene la descrizione della protezione.

  
**Restituisce**: descrizione della protezione
  
### <a name="gettemplateid"></a>GetTemplateId
Ottiene l'ID del modello di protezione, se presente.

  
**Restituisce**: ID modello
  
### <a name="getlabelid"></a>GetLabelId
Ottiene l'ID etichetta, se presente.

  
**Restituisce**: ID [etichetta](class_mip_label.md). Questa proprietà verrà popolata solo in ProtectionDescriptors per il contenuto protetto preesistente. È un campo popolato dal server nel momento in cui il contenuto protetto viene utilizzato.
  
### <a name="userrights"></a>UserRights
Ottiene una raccolta di mapping dei diritti agli utenti.

  
**Restituisce**: raccolta di mapping degli utenti ai diritti. Il valore della proprietà [UserRights](class_mip_userrights.md) sarà vuoto se l'utente corrente non ha accesso a queste informazioni, ovvero se l'utente non è il proprietario e non ha il diritto VIEWRIGHTSDATA.
  
### <a name="userroles"></a>UserRoles
Ottiene una raccolta di mapping dei ruoli agli utenti.

  
**Restituisce**: raccolta di mapping degli utenti ai ruoli
  
### <a name="getcontentvaliduntil"></a>GetContentValidUntil
Ottiene l'ora di scadenza della protezione.

  
**Restituisce**: ora di scadenza della protezione
  
### <a name="doesallowofflineaccess"></a>DoesAllowOfflineAccess
Ottiene un valore che indica se la protezione consente o meno l'accesso al contenuto offline.

  
**Restituisce**: valore che indica se la protezione consente o meno l'accesso al contenuto offline (impostazione predefinita = true)
  
### <a name="getreferrer"></a>GetReferrer
Ottiene l'indirizzo del referrer della protezione.

  
**Restituisce**: indirizzo del referrer della protezione. Il referrer è un URI visualizzabile per l'utente se non è possibile rimuovere la protezione dal contenuto. Contiene informazioni sul modo in cui tale utente può ottenere l'autorizzazione per accedere al contenuto.
  
### <a name="getencryptedappdata"></a>GetEncryptedAppData
Ottiene i dati specifici dell'app che sono stati crittografati.

  
**Restituisce**: dati specifici dell'app. Un oggetto [ProtectionHandler](class_mip_protectionhandler.md) può includere un dizionario di dati specifici dell'app che sono stati crittografati dal servizio di protezione. Questi dati crittografati sono indipendenti dai dati firmati accessibili tramite [ProtectionDescriptor::GetSignedAppData](class_mip_protectiondescriptor.md#getsignedappdata)
  
### <a name="getsignedappdata"></a>GetSignedAppData
Ottiene i dati specifici dell'app che sono stati firmati.

  
**Restituisce**: dati specifici dell'app. Un oggetto [ProtectionHandler](class_mip_protectionhandler.md) può includere un dizionario di dati specifici dell'app che sono stati firmati dal servizio di protezione. Questi dati firmati sono indipendenti dai dati crittografati accessibili tramite [ProtectionDescriptor::GetEncryptedAppData](class_mip_protectiondescriptor.md#getencryptedappdata)