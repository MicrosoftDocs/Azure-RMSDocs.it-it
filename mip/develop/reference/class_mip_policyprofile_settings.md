---
title: Classe mip::PolicyProfile::Settings
description: Documenta la classe MIP::p olicyprofile dell'SDK Microsoft Information Protection (MIP).
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 02/14/2020
ms.openlocfilehash: 6c2d7f26e12f03bd886f2a3fedab8e0a3d976c45
ms.sourcegitcommit: 2d3c638fb576f3f074330a33d077db0cf0e7d4e7
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/20/2020
ms.locfileid: "77489759"
---
# <a name="class-mippolicyprofilesettings"></a>Classe mip::PolicyProfile::Settings 
Impostazioni utilizzate da PolicyProfile durante la sua creazione e per tutta la sua durata.
  
## <a name="summary"></a>Riepilogo
 Members                        | Descrizioni                                
--------------------------------|---------------------------------------------
Impostazioni pubbliche (const std:: shared_ptr\<MipContext\>& mipContext, CacheStorageType cacheStorageType, const std:: shared_ptr\<AuthDelegate\>& authDelegate, const std:: shared_ptr\<PolicyProfile:: Observer\>& Observer)  |  Interfaccia per la configurazione del profilo.
public CacheStorageType GetCacheStorageType () const  |  Ottiene un valore che indica se le cache sono archiviate in memoria o su disco.
public const std:: shared_ptr\<AuthDelegate\>& GetAuthDelegate () const  |  Ottiene il delegato dell'autenticazione.
public const std:: shared_ptr\<PolicyProfile:: Observer\>& getobserver () const  |  Ottiene l'observer di eventi.
public std:: shared_ptr\<MipContext\> GetMipContext () const  |  Ottiene il contesto MIP che rappresenta lo stato condiviso in tutti i profili.
public std:: shared_ptr\<HttpDelegate\> GetHttpDelegate () const  |  Ottiene il delegato HTTP (se disponibile) specificato dall'applicazione.
public void SetHttpDelegate (const std:: shared_ptr\<HttpDelegate\>& httpDelegate)  |  Esegue l'override dello stack HTTP predefinito con quello del client.
public std:: shared_ptr\<TaskDispatcherDelegate\> GetTaskDispatcherDelegate () const  |  Ottenere il delegato TaskDispatcher (se presente) fornito dall'applicazione.
public void SetTaskDispatcherDelegate (const std:: shared_ptr\<TaskDispatcherDelegate\>& taskDispatcherDelegate)  |  Esegue l'override della gestione predefinita dell'invio delle attività asincrone con il proprio client.
public void SetSessionId(const std::string& sessionId)  | _Non ancora documentato._
public const std::string& GetSessionId() const  | _Non ancora documentato._
public void SetCustomSettings (const std:: Vector\<std::p Air\<std:: String, std:: String\>\>& customSettings)  |  Imposta le impostazioni personalizzate, usate a scopi di controllo e test delle funzionalità.
public const std:: Vector\<std::p Air\<std:: String, std:: String\>\>& GetCustomSettings () const  |  Ottiene le impostazioni personalizzate, usate a scopi di controllo e test delle funzionalità.
public ~Settings()  | _Non ancora documentato._
  
## <a name="members"></a>Members
  
### <a name="settings-function"></a>Funzione Settings
Interfaccia per la configurazione del profilo.

Parametri:  
* **mipContext**: impostazioni di contesto globali 


* **cacheStorageType**: archivia lo stato memorizzato nella cache in memoria o su disco 


* **authDelegate**: delegato dell'autenticazione usato dall'SDK per acquisire i token di autenticazione. 


* **Observer**: classe che implementa l'interfaccia PolicyProfile:: Observer. Può essere nullptr.


  
### <a name="getcachestoragetype-function"></a>GetCacheStorageType (funzione)
Ottiene un valore che indica se le cache sono archiviate in memoria o su disco.

  
**Restituisce**: tipo di archiviazione usato
  
### <a name="getauthdelegate-function"></a>GetAuthDelegate (funzione)
Ottiene il delegato dell'autenticazione.

  
**Restituisce**: delegato dell'autenticazione.
  
### <a name="getobserver-function"></a>Getobserver (funzione)
Ottiene l'observer di eventi.

  
**Restituisce**: observer di eventi.
  
### <a name="getmipcontext-function"></a>GetMipContext (funzione)
Ottiene il contesto MIP che rappresenta lo stato condiviso in tutti i profili.

  
**Restituisce**: contesto MIP
  
### <a name="gethttpdelegate-function"></a>GetHttpDelegate (funzione)
Ottiene il delegato HTTP (se disponibile) specificato dall'applicazione.

  
**Restituisce**: il delegato HTTP da usare per le operazioni HTTP
  
### <a name="sethttpdelegate-function"></a>SetHttpDelegate (funzione)
Esegue l'override dello stack HTTP predefinito con quello del client.

Parametri:  
* **httpDelegate**: interfaccia di callback HTTP implementata dall'applicazione client


  
### <a name="gettaskdispatcherdelegate-function"></a>GetTaskDispatcherDelegate (funzione)
Ottenere il delegato TaskDispatcher (se presente) fornito dall'applicazione.

  
**Restituisce**: delegato TaskDispatcher da usare per l'esecuzione di attività asincrone
  
### <a name="settaskdispatcherdelegate-function"></a>SetTaskDispatcherDelegate (funzione)
Esegue l'override della gestione predefinita dell'invio delle attività asincrone con il proprio client.

Parametri:  
* **taskDispatcherDelegate**: interfaccia di callback di invio dell'attività implementata dall'applicazione client


le attività possono fare riferimento a oggetti del profilo che ne impediscono la distruzione come risultato taskdispatcher le code non devono essere condivise.
  
### <a name="setsessionid-function"></a>Funzione SessionId
_Non ancora documentato._

  
### <a name="getsessionid-function"></a>Funzione GetSessionID
_Non ancora documentato._

  
### <a name="setcustomsettings-function"></a>SetCustomSettings (funzione)
Imposta le impostazioni personalizzate, usate a scopi di controllo e test delle funzionalità.

Parametri:  
* **customSettings**: elenco di coppie nome/valore.


  
### <a name="getcustomsettings-function"></a>GetCustomSettings (funzione)
Ottiene le impostazioni personalizzate, usate a scopi di controllo e test delle funzionalità.

  
**Restituisce:** : elenco di coppie nome/valore.
  
### <a name="settings-function"></a>~ Settings (funzione)
_Non ancora documentato._
