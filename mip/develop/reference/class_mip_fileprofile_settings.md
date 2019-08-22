---
title: Classe mip::FileProfile::Settings
description: "Documenta la classe MIP:: fileprofile dell'SDK Microsoft Information Protection (MIP)."
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 07/16/2019
ms.openlocfilehash: f6d28ae7803834138b1e8c61270bcad3fcc1eb11
ms.sourcegitcommit: fcde8b31f8685023f002044d3a1d1903e548d207
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/21/2019
ms.locfileid: "69884177"
---
# <a name="class-mipfileprofilesettings"></a>Classe mip::FileProfile::Settings 
Oggetto [Settings](class_mip_fileprofile_settings.md) usato da [FileProfile](class_mip_fileprofile.md) durante la creazione e per tutta la sua durata.
  
## <a name="summary"></a>Riepilogo
 Members                        | Descrizioni                                
--------------------------------|---------------------------------------------
impostazioni pubbliche (const std:: String & path, CacheStorageType CacheStorageType, std::\<shared_ptr\> AuthDelegate AuthDelegate, std::\<shared_ptr\> ConsentDelegate ConsentDelegate, std:: Observer Observer shared_ptr\<, const ApplicationInfo & ApplicationInfo)\>  |  Costruttore [FileProfile::Settings](class_mip_fileprofile_settings.md).
impostazioni pubbliche (const std::\<shared_ptr\>MipContext & MipContext, CacheStorageType CacheStorageType, std::\<shared_ptr\> AuthDelegate AuthDelegate, std::\< shared_ptr ConsentDelegate\> ConsentDelegate, std:: shared_ptr\<Observer\> Observer)  |  Costruttore [FileProfile::Settings](class_mip_fileprofile_settings.md).
public const std::string& GetPath() const  |  Ottiene il percorso in cui sono archiviati i dati di registrazione e telemetria e altre informazioni sugli stati persistenti.
public CacheStorageType GetCacheStorageType () const  |  Ottiene un valore che indica se le cache sono archiviate in memoria o su disco.
public std:: shared_ptr\<AuthDelegate\> GetAuthDelegate () const  |  Ottiene il delegato dell'autenticazione usato per l'acquisizione dei token di autenticazione.
public std:: shared_ptr\<ConsentDelegate\> GetConsentDelegate () const  |  Ottiene il delegato del consenso usato per richiedere il consenso dell'utente che si connette ai servizi.
public std:: shared_ptr\<\> Observer getobserver () const  |  Ottiene l'observer che riceve le notifiche degli eventi correlati a [FileProfile](class_mip_fileprofile.md).
public const ApplicationInfo& GetApplicationInfo() const  |  Ottiene informazioni sull'applicazione che sta utilizzando l'SDK.
public std:: shared_ptr\<MipContext\> GetMipContext () const  |  Ottiene il contesto MIP che rappresenta lo stato condiviso in tutti i profili.
public std:: shared_ptr\<LoggerDelegate\> GetLoggerDelegate () const  |  Ottiene il delegato del logger (se disponibile) fornito dall'applicazione.
public void SetLoggerDelegate (const std::\<shared_ptr\>LoggerDelegate & LoggerDelegate)  |  Esegue l'override del logger predefinito.
public std:: shared_ptr\<HttpDelegate\> GetHttpDelegate () const  |  Ottiene il delegato HTTP (se disponibile) specificato dall'applicazione.
public void SetHttpDelegate (const std::\<shared_ptr\>HttpDelegate & HttpDelegate)  |  Esegue l'override dello stack HTTP predefinito con quello del client.
public std:: shared_ptr\<TaskDispatcherDelegate\> GetTaskDispatcherDelegate () const  |  Ottenere il delegato TaskDispatcher (se presente) fornito dall'applicazione.
public void SetTaskDispatcherDelegate (const std::\<shared_ptr\>TaskDispatcherDelegate & TaskDispatcherDelegate)  |  Eseguire l'override della gestione delle attività modo asincrono rispetto predefinite con il client.
public void OptOutTelemetry()  |  Rifiuta esplicitamente la raccolta di tutti i dati di telemetria.
public bool IsTelemetryOptedOut() const  |  Ottiene un valore che indica se la raccolta dei dati di telemetria deve essere disabilitata o meno.
public void SetSessionId(const std::string& sessionId)  |  Imposta l'ID sessione.
public const std::string& GetSessionId() const  |  Ottiene l'ID sessione.
public void SetMinimumLogLevel(LogLevel logLevel)  |  Imposta il livello di log minimo che attiverà un evento di registrazione.
public LogLevel GetMinimumLogLevel() const  |  Ottiene il livello di log minimo che attiverà un evento di registrazione.
public void SetCanCacheLicenses (bool canCacheLicenses)  |  Configura se le licenze dell'utente finale (contratti) verranno memorizzate nella cache locale.
public bool CanCacheLicenses () const  |  Ottiene un valore che indica se le licenze dell'utente finale (contratti) sono memorizzate nella cache locale.
  
## <a name="members"></a>Members
  
### <a name="settings-function"></a>Funzione Settings
Costruttore [FileProfile::Settings](class_mip_fileprofile_settings.md).

Parametri:  
* **percorso**: Percorso del file in cui sono archiviati i dati di registrazione, telemetria e altro stato persistente 


* **cacheStorageType**: Archiviare lo stato memorizzato nella cache in memoria o su disco 


* **authDelegate**: Delegato di autenticazione usato per l'acquisizione dei token di autenticazione 


* **consentDelegate**: Delegato usato per ottenere l'autorizzazione utente per accedere alle risorse esterne 


* **observer**: Istanza [Observer](class_mip_fileprofile_observer.md) che riceverà le notifiche degli eventi correlati a [fileprofile](class_mip_fileprofile.md)


* **applicationInfo**: Informazioni sull'applicazione che utilizza l'SDK


> Deprecato Questo costruttore sarà presto deprecato a favore di uno che richiede un parametro MIP:: MipContext
  
### <a name="settings-function"></a>Funzione Settings
Costruttore [FileProfile::Settings](class_mip_fileprofile_settings.md).

Parametri:  
* **mipContext**: Impostazioni di contesto globali 


* **cacheStorageType**: Archiviare lo stato memorizzato nella cache in memoria o su disco 


* **authDelegate**: Delegato di autenticazione usato per l'acquisizione dei token di autenticazione 


* **consentDelegate**: Delegato usato per ottenere l'autorizzazione utente per accedere alle risorse esterne 


* **observer**: Istanza [Observer](class_mip_fileprofile_observer.md) che riceverà le notifiche degli eventi correlati a [fileprofile](class_mip_fileprofile.md)


  
### <a name="getpath-function"></a>GetPath (funzione)
Ottiene il percorso in cui sono archiviati i dati di registrazione e telemetria e altre informazioni sugli stati persistenti.

  
**Restituisce**: Percorso in cui sono archiviati i dati di registrazione, telemetria e altro stato persistente
> Deprecato Questo metodo sarà presto deprecato a favore di ottenere/impostare i dati del contesto comuni tramite MIP:: MipContext
  
### <a name="getcachestoragetype-function"></a>GetCacheStorageType (funzione)
Ottiene un valore che indica se le cache sono archiviate in memoria o su disco.

  
**Restituisce**: Tipo di archiviazione usato
  
### <a name="getauthdelegate-function"></a>GetAuthDelegate (funzione)
Ottiene il delegato dell'autenticazione usato per l'acquisizione dei token di autenticazione.

  
**Restituisce**: Delegato di autenticazione usato per l'acquisizione dei token di autenticazione
  
### <a name="getconsentdelegate-function"></a>GetConsentDelegate (funzione)
Ottiene il delegato del consenso usato per richiedere il consenso dell'utente che si connette ai servizi.

  
**Restituisce**: Delegato di consenso usato per richiedere il consenso dell'utente
  
### <a name="getobserver-function"></a>Getobserver (funzione)
Ottiene l'observer che riceve le notifiche degli eventi correlati a [FileProfile](class_mip_fileprofile.md).

  
**Restituisce**: [Observer](class_mip_fileprofile_observer.md) che riceve le notifiche degli eventi correlati a [fileprofile](class_mip_fileprofile.md)
  
### <a name="getapplicationinfo-function"></a>GetApplicationInfo (funzione)
Ottiene informazioni sull'applicazione che sta utilizzando l'SDK.

  
**Restituisce**: Informazioni sull'applicazione che utilizza l'SDK
> Deprecato Questo metodo sarà presto deprecato a favore di ottenere/impostare i dati del contesto comuni tramite MIP:: MipContext
  
### <a name="getmipcontext-function"></a>GetMipContext (funzione)
Ottiene il contesto MIP che rappresenta lo stato condiviso in tutti i profili.

  
**Restituisce**: Contesto MIP
  
### <a name="getloggerdelegate-function"></a>GetLoggerDelegate (funzione)
Ottiene il delegato del logger (se disponibile) fornito dall'applicazione.

  
**Restituisce**: Logger
> Deprecato Questo metodo sarà presto deprecato a favore di ottenere/impostare i dati del contesto comuni tramite MIP:: MipContext
  
### <a name="setloggerdelegate-function"></a>SetLoggerDelegate (funzione)
Esegue l'override del logger predefinito.

Parametri:  
* **loggerDelegate**: Interfaccia di callback di registrazione implementata dalle applicazioni client


Questo metodo deve essere chiamato dalle applicazioni client che usano la propria implementazione del logger 
> Deprecato Questo metodo sarà presto deprecato a favore di ottenere/impostare i dati del contesto comuni tramite MIP:: MipContext
  
### <a name="gethttpdelegate-function"></a>GetHttpDelegate (funzione)
Ottiene il delegato HTTP (se disponibile) specificato dall'applicazione.

  
**Restituisce**: Delegato HTTP da usare per le operazioni HTTP
  
### <a name="sethttpdelegate-function"></a>SetHttpDelegate (funzione)
Esegue l'override dello stack HTTP predefinito con quello del client.

Parametri:  
* **httpDelegate**: Interfaccia di callback HTTP implementata dall'applicazione client


  
### <a name="gettaskdispatcherdelegate-function"></a>GetTaskDispatcherDelegate (funzione)
Ottenere il delegato TaskDispatcher (se presente) fornito dall'applicazione.

  
**Restituisce**: Delegato TaskDispatcher da usare per l'esecuzione di attività asincrone
  
### <a name="settaskdispatcherdelegate-function"></a>SetTaskDispatcherDelegate (funzione)
Eseguire l'override della gestione delle attività modo asincrono rispetto predefinite con il client.

Parametri:  
* **taskDispatcherDelegate**: Interfaccia di callback per l'invio di attività implementata dall'applicazione client


  
### <a name="optouttelemetry-function"></a>OptOutTelemetry (funzione)
Rifiuta esplicitamente la raccolta di tutti i dati di telemetria.
> Deprecato Questo metodo sarà presto deprecato a favore di ottenere/impostare i dati del contesto comuni tramite MIP:: MipContext
  
### <a name="istelemetryoptedout-function"></a>IsTelemetryOptedOut (funzione)
Ottiene un valore che indica se la raccolta dei dati di telemetria deve essere disabilitata o meno.

  
**Restituisce**: Se la raccolta di dati di telemetria deve essere disabilitata o meno
> Deprecato Questo metodo sarà presto deprecato a favore di ottenere/impostare i dati del contesto comuni tramite MIP:: MipContext
  
### <a name="setsessionid-function"></a>Funzione SessionId
Imposta l'ID sessione.

Parametri:  
* **sessionId**: ID sessione che verrà usato per correlare log/telemetria


  
### <a name="getsessionid-function"></a>Funzione GetSessionID
Ottiene l'ID sessione.

  
**Restituisce**: ID sessione che verrà usato per correlare log/telemetria
  
### <a name="setminimumloglevel-function"></a>SetMinimumLogLevel (funzione)
Imposta il livello di log minimo che attiverà un evento di registrazione.

Parametri:  
* **logLevel**: livello di log minimo che attiverà un evento di registrazione.


> Deprecato Questo metodo sarà presto deprecato a favore di ottenere/impostare i dati del contesto comuni tramite MIP:: MipContext
  
### <a name="getminimumloglevel-function"></a>GetMinimumLogLevel (funzione)
Ottiene il livello di log minimo che attiverà un evento di registrazione.

  
**Restituisce**: Livello di registrazione più basso che attiverà un evento di registrazione.
> Deprecato Questo metodo sarà presto deprecato a favore di ottenere/impostare i dati del contesto comuni tramite MIP:: MipContext
  
### <a name="setcancachelicenses-function"></a>SetCanCacheLicenses (funzione)
Configura se le licenze dell'utente finale (contratti) verranno memorizzate nella cache locale.

Parametri:  
* **canCacheLicenses**: Indica se il motore deve memorizzare nella cache una licenza quando apre il contenuto protetto


Se true, l'apertura del contenuto protetto memorizza nella cache la licenza associata localmente. Se false, l'apertura del contenuto protetto eseguirà sempre l'operazione HTTP per acquisire la licenza dal servizio RMS.
  
### <a name="cancachelicenses-function"></a>CanCacheLicenses (funzione)
Ottiene un valore che indica se le licenze dell'utente finale (contratti) sono memorizzate nella cache locale.

  
**Restituisce**: Configurazione della memorizzazione nella cache delle licenze