---
title: Classe ProtectionDescriptor
description: 'Documenta la classe protectiondescriptor:: undefined di Microsoft Information Protection (MIP) SDK.'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 04/16/2020
ms.openlocfilehash: b4257be5475b1225f79efe00c11df4b79ee67ee9
ms.sourcegitcommit: f54920bf017902616589aca30baf6b64216b6913
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/22/2020
ms.locfileid: "81763954"
---
# <a name="class-protectiondescriptor"></a>Classe ProtectionDescriptor 
Descrizione della protezione associata a una parte del contenuto.
  
## <a name="summary"></a>Riepilogo
 Members                        | Descrizioni                                
--------------------------------|---------------------------------------------
public ProtectionType GetProtectionType() const  |  Ottiene il tipo di protezione, indipendentemente dal fatto che abbia avuto origine da un modello di SDK di protezione o meno.
public std::string GetOwner() const  |  Ottiene il proprietario per la protezione.
public std::string GetName() const  |  Ottiene il nome della protezione.
public std::string GetDescription() const  |  Ottiene la descrizione della protezione.
public std::string GetTemplateId() const  |  Ottiene l'ID del modello di protezione, se presente.
public std::string GetLabelId() const  |  Ottiene l'ID etichetta, se presente.
public std:: String GetContentId () const  |  Ottiene l'ID contenuto, se disponibile.
public std:: Vector\<UserRights\> GetUserRights () const  |  Ottiene una raccolta di mapping dei diritti agli utenti.
public std:: Vector\<UserRoles\> GetUserRoles () const  |  Ottiene una raccolta di mapping dei ruoli agli utenti.
public bool DoesContentExpire () const  |  Verifica se il contenuto ha una data di scadenza.
public std:: Chrono:: time_point\<std:: Chrono:: system_clock\> GetContentValidUntil () const  |  Ottiene l'ora di scadenza della protezione.
public bool DoesAllowOfflineAccess() const  |  Ottiene un valore che indica se la protezione consente o meno l'accesso al contenuto offline.
public std::string GetReferrer() const  |  Ottiene l'indirizzo del referrer della protezione.
public std:: Map\<std:: String, std:: String\> GetEncryptedAppData () const  |  Ottiene i dati specifici dell'app che sono stati crittografati.
public std:: Map\<std:: String, std:: String\> GetSignedAppData () const  |  Ottiene i dati specifici dell'app che sono stati firmati.
public std:: String GetDoubleKeyUrl () const  |  Ottiene l'URL della chiave doppia da utilizzare per la protezione personalizzata.
  
## <a name="members"></a>Members
  
### <a name="getprotectiontype-function"></a>GetProtectionType (funzione)
Ottiene il tipo di protezione, indipendentemente dal fatto che abbia avuto origine da un modello di SDK di protezione o meno.

  
**Restituisce**: tipo di protezione
  
### <a name="getowner-function"></a>Funzione GetOwner
Ottiene il proprietario per la protezione.

  
**Restituisce**: proprietario della protezione
  
### <a name="getname-function"></a>GetName (funzione)
Ottiene il nome della protezione.

  
**Restituisce**: nome della protezione
  
### <a name="getdescription-function"></a>Funzione GetDescription
Ottiene la descrizione della protezione.

  
**Restituisce**: descrizione della protezione
  
### <a name="gettemplateid-function"></a>GetTemplateId (funzione)
Ottiene l'ID del modello di protezione, se presente.

  
**Restituisce**: ID modello
  
### <a name="getlabelid-function"></a>GetLabelId (funzione)
Ottiene l'ID etichetta, se presente.

  
**Restituisce**: ID etichetta questa proprietà verrà popolata solo in ProtectionDescriptors per il contenuto protetto preesistente. È un campo popolato dal server nel momento in cui il contenuto protetto viene utilizzato.
  
### <a name="getcontentid-function"></a>GetContentId (funzione)
Ottiene l'ID contenuto, se disponibile.

  
**Restituisce**: ID contenuto
  
### <a name="getuserrights-function"></a>GetUserRights (funzione)
Ottiene una raccolta di mapping dei diritti agli utenti.

  
**Restituisce**: raccolta di mapping degli utenti ai diritti. Il valore della proprietà [UserRights](class_mip_userrights.md) sarà vuoto se l'utente corrente non ha accesso a queste informazioni, ovvero se l'utente non è il proprietario e non ha il diritto VIEWRIGHTSDATA.
  
### <a name="getuserroles-function"></a>GetUserRoles (funzione)
Ottiene una raccolta di mapping dei ruoli agli utenti.

  
**Restituisce**: raccolta di mapping degli utenti ai ruoli
  
### <a name="doescontentexpire-function"></a>DoesContentExpire (funzione)
Verifica se il contenuto ha una data di scadenza.

  
**Restituisce**: true se il contenuto può scadere, altrimenti false
  
### <a name="getcontentvaliduntil-function"></a>GetContentValidUntil (funzione)
Ottiene l'ora di scadenza della protezione.

  
**Restituisce**: ora di scadenza della protezione
  
### <a name="doesallowofflineaccess-function"></a>DoesAllowOfflineAccess (funzione)
Ottiene un valore che indica se la protezione consente o meno l'accesso al contenuto offline.

  
**Restituisce**: valore che indica se la protezione consente o meno l'accesso al contenuto offline (impostazione predefinita = true)
  
### <a name="getreferrer-function"></a>GetReferrer (funzione)
Ottiene l'indirizzo del referrer della protezione.

  
**Restituisce**: indirizzo del referrer della protezione. Il referrer è un URI visualizzabile per l'utente se non è possibile rimuovere la protezione dal contenuto. Contiene informazioni sul modo in cui tale utente può ottenere l'autorizzazione per accedere al contenuto.
  
### <a name="getencryptedappdata-function"></a>GetEncryptedAppData (funzione)
Ottiene i dati specifici dell'app che sono stati crittografati.

  
**Restituisce**: dati specifici dell'app. Un oggetto ProtectionHandler può includere un dizionario di dati specifici dell'app che sono stati crittografati dal servizio di protezione. Questi dati crittografati sono indipendenti dai dati firmati accessibili tramite ProtectionDescriptor:: GetSignedAppData.
  
### <a name="getsignedappdata-function"></a>GetSignedAppData (funzione)
Ottiene i dati specifici dell'app che sono stati firmati.

  
**Restituisce**: dati specifici dell'app. Un oggetto ProtectionHandler può includere un dizionario di dati specifici dell'app che sono stati firmati dal servizio di protezione. Questi dati firmati sono indipendenti dai dati crittografati accessibili tramite ProtectionDescriptor:: GetEncryptedAppData.
  
### <a name="getdoublekeyurl-function"></a>GetDoubleKeyUrl (funzione)
Ottiene l'URL della chiave doppia da utilizzare per la protezione personalizzata.

  
**Returns**: URL a doppia chiave che viene usato nelle richieste personalizzate per proteggere le informazioni con una seconda chiave