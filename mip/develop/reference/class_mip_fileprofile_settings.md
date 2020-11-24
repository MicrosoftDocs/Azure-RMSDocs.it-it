---
title: 'Classe fileprofile:: Settings'
description: "Documenta la classe fileprofile:: Settings dell'SDK Microsoft Information Protection (MIP)."
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 09/21/2020
ms.openlocfilehash: 5ab95e72c1b6198b8619f1fe6b0f850562ff00df
ms.sourcegitcommit: 3f5f9f7695b9ed3c45e9230cd8b8cb39a1c5a5ed
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/23/2020
ms.locfileid: "95566912"
---
# <a name="class-fileprofilesettings"></a>Classe fileprofile:: Settings 
Oggetto Settings usato da FileProfile durante la creazione e per tutta la sua durata.
  
## <a name="summary"></a>Riepilogo
 Members                        | Descrizioni                                
--------------------------------|---------------------------------------------
Impostazioni pubbliche (const std:: shared_ptr \<MipContext\>& mipContext, cacheStorageType CacheStorageType, std:: shared_ptr \<ConsentDelegate\> consentDelegate, std:: shared_ptr \<Observer\> Observer)  |  Costruttore FileProfile::Settings.
public CacheStorageType GetCacheStorageType () const  |  Ottiene un valore che indica se le cache sono archiviate in memoria o su disco.
public std::shared_ptr\<ConsentDelegate\> GetConsentDelegate() const  |  Ottiene il delegato del consenso usato per richiedere il consenso dell'utente che si connette ai servizi.
public std::shared_ptr\<Observer\> GetObserver() const  |  Ottiene l'observer che riceve le notifiche degli eventi correlati a FileProfile.
public std:: shared_ptr \<MipContext\> GetMipContext () const  |  Ottiene il contesto MIP che rappresenta lo stato condiviso in tutti i profili.
public std::shared_ptr\<HttpDelegate\> GetHttpDelegate() const  |  Ottiene il delegato HTTP (se disponibile) specificato dall'applicazione.
public void SetHttpDelegate(const std::shared_ptr\<HttpDelegate\>& httpDelegate)  |  Esegue l'override dello stack HTTP predefinito con quello del client.
public std:: shared_ptr \<TaskDispatcherDelegate\> GetTaskDispatcherDelegate () const  |  Ottenere il delegato TaskDispatcher (se presente) fornito dall'applicazione.
public void SetTaskDispatcherDelegate (const std:: shared_ptr \<TaskDispatcherDelegate\>& taskDispatcherDelegate)  |  Eseguire l'override della gestione delle attività modo asincrono rispetto predefinite con il client.
public void SetSessionId(const std::string& sessionId)  |  Imposta l'ID sessione.
public const std::string& GetSessionId() const  |  Ottiene l'ID sessione.
public void SetCanCacheLicenses (bool canCacheLicenses)  |  Configura se le licenze dell'utente finale (contratti) verranno memorizzate nella cache locale.
public bool CanCacheLicenses () const  |  Ottiene un valore che indica se le licenze dell'utente finale (contratti) sono memorizzate nella cache locale.
  
## <a name="members"></a>Members
  
### <a name="settings-function"></a>Funzione Settings
Costruttore FileProfile::Settings.

Parametri  
* **mipContext**: impostazioni di contesto globali 


* **cacheStorageType**: archivia lo stato memorizzato nella cache in memoria o su disco 


* **consentDelegate**: delegato usato per ottenere l'autorizzazione utente per accedere alle risorse esterne 


* **Observer**: istanza Observer che riceverà le notifiche degli eventi correlati a fileprofile


  
### <a name="getcachestoragetype-function"></a>GetCacheStorageType (funzione)
Ottiene un valore che indica se le cache sono archiviate in memoria o su disco.

  
**Restituisce**: tipo di archiviazione usato
  
### <a name="getconsentdelegate-function"></a>GetConsentDelegate (funzione)
Ottiene il delegato del consenso usato per richiedere il consenso dell'utente che si connette ai servizi.

  
**Restituisce**: delegato del consenso usato per richiedere il consenso dell'utente
  
### <a name="getobserver-function"></a>Getobserver (funzione)
Ottiene l'observer che riceve le notifiche degli eventi correlati a FileProfile.

  
**Restituisce**: Observer che riceve le notifiche degli eventi correlati a fileprofile
  
### <a name="getmipcontext-function"></a>GetMipContext (funzione)
Ottiene il contesto MIP che rappresenta lo stato condiviso in tutti i profili.

  
**Restituisce**: contesto MIP
  
### <a name="gethttpdelegate-function"></a>GetHttpDelegate (funzione)
Ottiene il delegato HTTP (se disponibile) specificato dall'applicazione.

  
**Restituisce**: delegato HTTP da usare per le operazioni HTTP
  
### <a name="sethttpdelegate-function"></a>SetHttpDelegate (funzione)
Esegue l'override dello stack HTTP predefinito con quello del client.

Parametri  
* **httpDelegate**: interfaccia di callback http implementata dall'applicazione client


  
### <a name="gettaskdispatcherdelegate-function"></a>GetTaskDispatcherDelegate (funzione)
Ottenere il delegato TaskDispatcher (se presente) fornito dall'applicazione.

  
**Restituisce**: delegato TaskDispatcher da usare per l'esecuzione di attività asincrone
  
### <a name="settaskdispatcherdelegate-function"></a>SetTaskDispatcherDelegate (funzione)
Eseguire l'override della gestione delle attività modo asincrono rispetto predefinite con il client.

Parametri  
* **taskDispatcherDelegate**: interfaccia di callback di invio dell'attività implementata dall'applicazione client


le attività possono fare riferimento a oggetti del profilo che ne impediscono la distruzione come risultato taskdispatcher le code non devono essere condivise.
  
### <a name="setsessionid-function"></a>Funzione SessionId
Imposta l'ID sessione.

Parametri  
* **sessionId**: ID sessione che verrà usato per la correlazione di log/telemetria


  
### <a name="getsessionid-function"></a>Funzione GetSessionID
Ottiene l'ID sessione.

  
**Restituisce**: ID sessione che verrà usato per la correlazione di log/telemetria
  
### <a name="setcancachelicenses-function"></a>SetCanCacheLicenses (funzione)
Configura se le licenze dell'utente finale (contratti) verranno memorizzate nella cache locale.

Parametri  
* **canCacheLicenses**: indica se il motore deve memorizzare nella cache una licenza quando apre il contenuto protetto


Se true, l'apertura del contenuto protetto memorizza nella cache la licenza associata localmente. Se false, l'apertura del contenuto protetto eseguirà sempre l'operazione HTTP per acquisire la licenza dal servizio RMS.
  
### <a name="cancachelicenses-function"></a>CanCacheLicenses (funzione)
Ottiene un valore che indica se le licenze dell'utente finale (contratti) sono memorizzate nella cache locale.

  
**Restituisce**: configurazione della memorizzazione nella cache delle licenze