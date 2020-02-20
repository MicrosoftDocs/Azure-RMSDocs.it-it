---
title: Classe mip::ProtectionProfile::Settings
description: Documenta la classe MIP::p rotectionprofile dell'SDK Microsoft Information Protection (MIP).
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 02/14/2020
ms.openlocfilehash: 0622f4db00c2f4baca7845aa0ca061bf2ccf294b
ms.sourcegitcommit: 2d3c638fb576f3f074330a33d077db0cf0e7d4e7
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/20/2020
ms.locfileid: "77489606"
---
# <a name="class-mipprotectionprofilesettings"></a>Classe mip::ProtectionProfile::Settings 
Impostazioni utilizzate da ProtectionProfile durante la sua creazione e per tutta la sua durata.
  
## <a name="summary"></a>Riepilogo
 Members                        | Descrizioni                                
--------------------------------|---------------------------------------------
Impostazioni pubbliche (const std:: shared_ptr\<MipContext\>& mipContext, CacheStorageType cacheStorageType, const std:: shared_ptr\<AuthDelegate\>& AuthDelegate, const std:: shared_ptr\<ConsentDelegate\>& consentDelegate, const std:: shared_ptr\<ProtectionProfile:: Observer\>& Observer)  |  Costruttore ProtectionProfile:: Settings che specifica un Observer da usare per le operazioni asincrone.
Impostazioni pubbliche (const std:: shared_ptr\<MipContext\>& mipContext, CacheStorageType cacheStorageType, const std:: shared_ptr\<AuthDelegate\>& authDelegate, const std:: shared_ptr\<ConsentDelegate\>& consentDelegate)  |  Costruttore ProtectionProfile:: Settings, usato per le operazioni sincrone.
public CacheStorageType GetCacheStorageType () const  |  Ottiene un valore che indica se le cache sono archiviate in memoria o su disco.
public std:: shared_ptr\<AuthDelegate\> GetAuthDelegate () const  |  Ottiene il delegato dell'autenticazione usato per l'acquisizione dei token di autenticazione.
public std:: shared_ptr\<ConsentDelegate\> GetConsentDelegate () const  |  Ottiene il delegato del consenso usato per la connessione ai servizi.
public std:: shared_ptr\<ProtectionProfile:: Observer\> getobserver () const  |  Ottiene l'osservatore che riceve le notifiche degli eventi correlati a ProtectionProfile.
public std:: shared_ptr\<MipContext\> GetMipContext () const  |  Ottiene il contesto MIP che rappresenta lo stato condiviso in tutti i profili.
public std:: shared_ptr\<HttpDelegate\> GetHttpDelegate () const  |  Ottiene il delegato HTTP (se disponibile) specificato dall'applicazione.
public void SetHttpDelegate (const std:: shared_ptr\<HttpDelegate\>& httpDelegate)  |  Esegue l'override dello stack HTTP predefinito con quello del client.
public std:: shared_ptr\<TaskDispatcherDelegate\> GetTaskDispatcherDelegate () const  |  Ottenere il delegato TaskDispatcher (se presente) fornito dall'applicazione.
public void SetTaskDispatcherDelegate (const std:: shared_ptr\<TaskDispatcherDelegate\>& taskDispatcherDelegate)  |  Eseguire l'override della gestione delle attività modo asincrono rispetto predefinite con il client.
public void SetSessionId(const std::string& sessionId)  |  Imposta l'ID sessione.
public const std::string& GetSessionId() const  |  Ottiene l'ID sessione.
public void SetCanCacheLicenses (bool canCacheLicenses)  |  Configura se le licenze dell'utente finale (contratti) verranno memorizzate nella cache locale.
public bool CanCacheLicenses () const  |  Ottiene un valore che indica se le licenze dell'utente finale (contratti) sono memorizzate nella cache locale.
public void SetCustomSettings (const std:: Vector\<std::p Air\<std:: String, std:: String\>\>& customSettings)  |  Imposta le impostazioni personalizzate, usate a scopi di controllo e test delle funzionalità.
public const std:: Vector\<std::p Air\<std:: String, std:: String\>\>& GetCustomSettings () const  |  Ottiene le impostazioni personalizzate, usate a scopi di controllo e test delle funzionalità.
  
## <a name="members"></a>Members
  
### <a name="settings-function"></a>Funzione Settings
Costruttore ProtectionProfile:: Settings che specifica un Observer da usare per le operazioni asincrone.

Parametri:  
* **mipContext**: impostazioni di contesto globali 


* **cacheStorageType**: archivia lo stato memorizzato nella cache in memoria o su disco 


* **authDelegate**: oggetto di callback da usare per l'autenticazione, implemento dall'applicazione client 


* **consentDelegate**: delegato usato per ottenere l'autorizzazione utente per accedere alle risorse esterne 


* **Observer**: istanza Observer che riceverà le notifiche degli eventi correlati a ProtectionProfile


* **applicationInfo**: informazioni sull'applicazione che sta utilizzando l'SDK di protezione


  
### <a name="settings-function"></a>Funzione Settings
Costruttore ProtectionProfile:: Settings, usato per le operazioni sincrone.

Parametri:  
* **mipContext**: impostazioni di contesto globali 


* **cacheStorageType**: archivia lo stato memorizzato nella cache in memoria o su disco 


* **authDelegate**: oggetto di callback da usare per l'autenticazione, implemento dall'applicazione client 


* **consentDelegate**: delegato usato per ottenere l'autorizzazione utente per accedere alle risorse esterne 


* **applicationInfo**: informazioni sull'applicazione che sta utilizzando l'SDK di protezione


  
### <a name="getcachestoragetype-function"></a>GetCacheStorageType (funzione)
Ottiene un valore che indica se le cache sono archiviate in memoria o su disco.

  
**Restituisce**: tipo di archiviazione usato
  
### <a name="getauthdelegate-function"></a>GetAuthDelegate (funzione)
Ottiene il delegato dell'autenticazione usato per l'acquisizione dei token di autenticazione.

  
**Restituisce**: delegato dell'autenticazione usato per l'acquisizione dei token di autenticazione
  
### <a name="getconsentdelegate-function"></a>GetConsentDelegate (funzione)
Ottiene il delegato del consenso usato per la connessione ai servizi.

  
**Restituisce**: delegato del consenso usato per la connessione ai servizi
  
### <a name="getobserver-function"></a>Getobserver (funzione)
Ottiene l'osservatore che riceve le notifiche degli eventi correlati a ProtectionProfile.

  
**Restituisce**: Observer che riceve le notifiche degli eventi correlati a ProtectionProfile
  
### <a name="getmipcontext-function"></a>GetMipContext (funzione)
Ottiene il contesto MIP che rappresenta lo stato condiviso in tutti i profili.

  
**Restituisce**: contesto MIP
  
### <a name="gethttpdelegate-function"></a>GetHttpDelegate (funzione)
Ottiene il delegato HTTP (se disponibile) specificato dall'applicazione.

  
**Restituisce**: delegato HTTP da usare per le operazioni HTTP
  
### <a name="sethttpdelegate-function"></a>SetHttpDelegate (funzione)
Esegue l'override dello stack HTTP predefinito con quello del client.

Parametri:  
* **httpDelegate**: interfaccia di callback HTTP implementata dall'applicazione client


  
### <a name="gettaskdispatcherdelegate-function"></a>GetTaskDispatcherDelegate (funzione)
Ottenere il delegato TaskDispatcher (se presente) fornito dall'applicazione.

  
**Restituisce**: delegato TaskDispatcher da usare per l'esecuzione di attività asincrone
  
### <a name="settaskdispatcherdelegate-function"></a>SetTaskDispatcherDelegate (funzione)
Eseguire l'override della gestione delle attività modo asincrono rispetto predefinite con il client.

Parametri:  
* **taskDispatcherDelegate**: interfaccia di callback di invio dell'attività implementata dall'applicazione client


le attività possono fare riferimento a oggetti del profilo che ne impediscono la distruzione come risultato taskdispatcher le code non devono essere condivise.
  
### <a name="setsessionid-function"></a>Funzione SessionId
Imposta l'ID sessione.

Parametri:  
* **sessionId**: ID sessione che verrà usato per la correlazione di log/telemetria


  
### <a name="getsessionid-function"></a>Funzione GetSessionID
Ottiene l'ID sessione.

  
**Restituisce**: ID sessione che verrà usato per la correlazione di log/telemetria
  
### <a name="setcancachelicenses-function"></a>SetCanCacheLicenses (funzione)
Configura se le licenze dell'utente finale (contratti) verranno memorizzate nella cache locale.

Parametri:  
* **canCacheLicenses**: indica se il motore deve memorizzare nella cache una licenza quando apre il contenuto protetto


Se true, l'apertura del contenuto protetto memorizza nella cache la licenza associata localmente. Se false, l'apertura del contenuto protetto eseguirà sempre l'operazione HTTP per acquisire la licenza dal servizio RMS.
  
### <a name="cancachelicenses-function"></a>CanCacheLicenses (funzione)
Ottiene un valore che indica se le licenze dell'utente finale (contratti) sono memorizzate nella cache locale.

  
**Restituisce**: configurazione della memorizzazione nella cache delle licenze
  
### <a name="setcustomsettings-function"></a>SetCustomSettings (funzione)
Imposta le impostazioni personalizzate, usate a scopi di controllo e test delle funzionalità.

Parametri:  
* **customSettings**: elenco di coppie nome/valore.


  
### <a name="getcustomsettings-function"></a>GetCustomSettings (funzione)
Ottiene le impostazioni personalizzate, usate a scopi di controllo e test delle funzionalità.

  
**Restituisce:** : elenco di coppie nome/valore.