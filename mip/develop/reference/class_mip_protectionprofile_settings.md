---
title: 'Classe ProtectionProfile:: Settings'
description: "Documenta la classe protectionprofile:: Settings dell'SDK Microsoft Information Protection (MIP)."
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/13/2021
ms.openlocfilehash: 0521d1c14081527f760a24e773edad0a07685fac
ms.sourcegitcommit: 76926b357bbfc8772ed132ce5f2426fbea59e98b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/14/2021
ms.locfileid: "98214372"
---
# <a name="class-protectionprofilesettings"></a>Classe ProtectionProfile:: Settings 
Oggetto Settings usato da ProtectionProfile durante la creazione e per tutta la sua durata.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
Impostazioni pubbliche (const std:: shared_ptr \<MipContext\>& mipContext, cacheStorageType CacheStorageType, const std:: shared_ptr \<ConsentDelegate\>& consentDelegate, const std:: shared_ptr \<ProtectionProfile::Observer\>& Observer)  |  Costruttore ProtectionProfile::Settings che specifica un observer da usare per le operazioni asincrone.
Impostazioni pubbliche (const std:: shared_ptr \<MipContext\>& mipContext, cacheStorageType CacheStorageType, const std:: shared_ptr \<ConsentDelegate\>& consentDelegate)  |  Costruttore ProtectionProfile::Settings, usato per le operazioni sincrone.
public CacheStorageType GetCacheStorageType () const  |  Ottiene un valore che indica se le cache sono archiviate in memoria o su disco.
public std::shared_ptr\<ConsentDelegate\> GetConsentDelegate() const  |  Ottiene il delegato del consenso usato per la connessione ai servizi.
public std::shared_ptr\<ProtectionProfile::Observer\> GetObserver() const  |  Ottiene l'observer che riceve le notifiche degli eventi correlati a ProtectionProfile.
public std:: shared_ptr \<MipContext\> GetMipContext () const  |  Ottiene il contesto MIP che rappresenta lo stato condiviso in tutti i profili.
public std::shared_ptr\<HttpDelegate\> GetHttpDelegate() const  |  Ottiene il delegato HTTP (se disponibile) specificato dall'applicazione.
public void SetHttpDelegate(const std::shared_ptr\<HttpDelegate\>& httpDelegate)  |  Esegue l'override dello stack HTTP predefinito con quello del client.
public std:: shared_ptr \<TaskDispatcherDelegate\> GetTaskDispatcherDelegate () const  |  Ottenere il delegato TaskDispatcher (se presente) fornito dall'applicazione.
public void SetTaskDispatcherDelegate (const std:: shared_ptr \<TaskDispatcherDelegate\>& taskDispatcherDelegate)  |  Eseguire l'override della gestione delle attività modo asincrono rispetto predefinite con il client.
public void SetSessionId(const std::string& sessionId)  |  Imposta l'ID sessione.
public const std::string& GetSessionId() const  |  Ottiene l'ID sessione.
public void SetCanCacheLicenses (bool canCacheLicenses)  |  Configura se le licenze dell'utente finale (contratti) verranno memorizzate nella cache locale.
public bool CanCacheLicenses () const  |  Ottiene un valore che indica se le licenze dell'utente finale (contratti) sono memorizzate nella cache locale.
public void SetCustomSettings (const std:: Vector \<std::pair\<std::string, std::string\> \>& customSettings)  |  Imposta le impostazioni personalizzate, usate a scopi di controllo e test delle funzionalità.
public const std:: Vector \<std::pair\<std::string, std::string\> \>& GetCustomSettings () const  |  Ottiene le impostazioni personalizzate, usate a scopi di controllo e test delle funzionalità.
  
## <a name="members"></a>Membri
  
### <a name="settings-function"></a>Funzione Settings
Costruttore ProtectionProfile::Settings che specifica un observer da usare per le operazioni asincrone.

Parametri  
* **mipContext**: impostazioni di contesto globali 


* **cacheStorageType**: archivia lo stato memorizzato nella cache in memoria o su disco 


* **consentDelegate**: delegato usato per ottenere l'autorizzazione utente per accedere alle risorse esterne 


* **Observer**: istanza Observer che riceverà le notifiche degli eventi correlati a ProtectionProfile


* **applicationInfo**: informazioni sull'applicazione che sta utilizzando l'SDK di protezione


  
### <a name="settings-function"></a>Funzione Settings
Costruttore ProtectionProfile::Settings, usato per le operazioni sincrone.

Parametri  
* **mipContext**: impostazioni di contesto globali 


* **cacheStorageType**: archivia lo stato memorizzato nella cache in memoria o su disco 


* **consentDelegate**: delegato usato per ottenere l'autorizzazione utente per accedere alle risorse esterne 


* **applicationInfo**: informazioni sull'applicazione che sta utilizzando l'SDK di protezione


  
### <a name="getcachestoragetype-function"></a>GetCacheStorageType (funzione)
Ottiene un valore che indica se le cache sono archiviate in memoria o su disco.

  
**Restituisce**: tipo di archiviazione usato
  
### <a name="getconsentdelegate-function"></a>GetConsentDelegate (funzione)
Ottiene il delegato del consenso usato per la connessione ai servizi.

  
**Restituisce**: delegato del consenso usato per la connessione ai servizi
  
### <a name="getobserver-function"></a>Getobserver (funzione)
Ottiene l'observer che riceve le notifiche degli eventi correlati a ProtectionProfile.

  
**Restituisce**: Observer che riceve le notifiche degli eventi correlati a ProtectionProfile
  
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
  
### <a name="setcustomsettings-function"></a>SetCustomSettings (funzione)
Imposta le impostazioni personalizzate, usate a scopi di controllo e test delle funzionalità.

Parametri  
* **customSettings**: elenco di coppie nome/valore.


  
### <a name="getcustomsettings-function"></a>GetCustomSettings (funzione)
Ottiene le impostazioni personalizzate, usate a scopi di controllo e test delle funzionalità.

  
**Restituisce:**: elenco di coppie nome/valore.