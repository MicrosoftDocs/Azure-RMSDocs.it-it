---
title: Classe mip::PolicyProfile::Settings
description: Documenta la classe MIP::p olicyprofile dell'SDK Microsoft Information Protection (MIP).
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 08/27/2019
ms.openlocfilehash: 2edec96a34b6885aa6c38477d36e401ebc49242a
ms.sourcegitcommit: 1499790746145d40d667d138baa6e18598421f0e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/27/2019
ms.locfileid: "70055667"
---
# <a name="class-mippolicyprofilesettings"></a>Classe mip::PolicyProfile::Settings 
Oggetto [Settings](class_mip_policyprofile_settings.md) usato da [PolicyProfile](class_mip_policyprofile.md) durante la creazione e per tutta la sua durata.
  
## <a name="summary"></a>Riepilogo
 Members                        | Descrizioni                                
--------------------------------|---------------------------------------------
impostazioni pubbliche (const std:: String & path, CacheStorageType CacheStorageType, const std:\<:\>shared_ptr AuthDelegate & AuthDelegate, const std\<:: shared_ptr PolicyProfile:\> : Observer & Observer, const ApplicationInfo & applicationInfo)  |  Interfaccia per la configurazione del profilo.
impostazioni pubbliche (const std::\<shared_ptr\>MipContext & MipContext, CacheStorageType CacheStorageType, const std:\<:\>shared_ptr AuthDelegate & AuthDelegate, const std:: shared_ptr\< PolicyProfile:: Observer\>& Observer)  |  Interfaccia per la configurazione del profilo.
public const std::string& GetPath() const  |  Ottiene il percorso dello stato archiviato.
public CacheStorageType GetCacheStorageType () const  |  Ottiene un valore che indica se le cache sono archiviate in memoria o su disco.
public const std::\<shared_ptr\>AuthDelegate & GetAuthDelegate () const  |  Ottiene il delegato dell'autenticazione.
public const std::\<shared_ptr PolicyProfile::\>Observer & getobserver () const  |  Ottiene l'observer di eventi.
public const ApplicationInfo& GetApplicationInfo() const  |  Ottiene le informazioni sull'applicazione.
public std:: shared_ptr\<MipContext\> GetMipContext () const  |  Ottiene il contesto MIP che rappresenta lo stato condiviso in tutti i profili.
public std:: shared_ptr\<LoggerDelegate\> GetLoggerDelegate () const  |  Ottiene il delegato del logger (se disponibile) fornito dall'applicazione.
public void SetLoggerDelegate (const std::\<shared_ptr\>LoggerDelegate & LoggerDelegate)  |  Esegue l'override del logger predefinito.
public std:: shared_ptr\<HttpDelegate\> GetHttpDelegate () const  |  Ottiene il delegato HTTP (se disponibile) specificato dall'applicazione.
public void SetHttpDelegate (const std::\<shared_ptr\>HttpDelegate & HttpDelegate)  |  Esegue l'override dello stack HTTP predefinito con quello del client.
public std:: shared_ptr\<TaskDispatcherDelegate\> GetTaskDispatcherDelegate () const  |  Ottenere il delegato TaskDispatcher (se presente) fornito dall'applicazione.
public void SetTaskDispatcherDelegate (const std::\<shared_ptr\>TaskDispatcherDelegate & TaskDispatcherDelegate)  |  Eseguire l'override della gestione delle attività modo asincrono rispetto predefinite con il client.
public void OptOutTelemetry()  |  Rifiuta esplicitamente la raccolta di tutti i dati di telemetria.
public bool IsTelemetryOptedOut() const  |  Ottiene un valore che indica se la raccolta dei dati di telemetria deve essere disabilitata o meno.
public void SetMinimumLogLevel(LogLevel logLevel)  |  Imposta il livello di log minimo che attiverà un evento di registrazione.
public LogLevel GetMinimumLogLevel() const  |  Ottiene l'oggetto Livello di log minimo.
public void SetSessionId(const std::string& sessionId)  | _Non ancora documentato._
public const std::string& GetSessionId() const  | _Non ancora documentato._
public ~Settings()  | _Non ancora documentato._
  
## <a name="members"></a>Members
  
### <a name="settings-function"></a>Funzione Settings
Interfaccia per la configurazione del profilo.

Parametri:  
* **percorso**: Percorso di una directory in cui l'SDK archivia lo stato del profilo. 


* **cacheStorageType**: Archiviare lo stato memorizzato nella cache in memoria o su disco 


* **authDelegate**: Delegato di autenticazione usato dall'SDK per acquisire i token di autenticazione. 


* **observer**: Classe che implementa l'interfaccia [PolicyProfile:: Observer](class_mip_policyprofile_observer.md) . Può essere nullptr. 


* **applicationInfo**: Identificatori dell'applicazione utilizzati per l'accesso al servizio.


> Deprecato Questo costruttore sarà presto deprecato a favore di uno che richiede un parametro MIP:: MipContext
  
### <a name="settings-function"></a>Funzione Settings
Interfaccia per la configurazione del profilo.

Parametri:  
* **mipContext**: Impostazioni di contesto globali 


* **cacheStorageType**: Archiviare lo stato memorizzato nella cache in memoria o su disco 


* **authDelegate**: Delegato di autenticazione usato dall'SDK per acquisire i token di autenticazione. 


* **observer**: Classe che implementa l'interfaccia [PolicyProfile:: Observer](class_mip_policyprofile_observer.md) . Può essere nullptr.


  
### <a name="getpath-function"></a>GetPath (funzione)
Ottiene il percorso dello stato archiviato.

  
**Restituisce**: Percorso dello stato archiviato.
> Deprecato Questo metodo sarà presto deprecato a favore di ottenere/impostare i dati del contesto comuni tramite MIP:: MipContext.
  
### <a name="getcachestoragetype-function"></a>GetCacheStorageType (funzione)
Ottiene un valore che indica se le cache sono archiviate in memoria o su disco.

  
**Restituisce**: Tipo di archiviazione usato
  
### <a name="getauthdelegate-function"></a>GetAuthDelegate (funzione)
Ottiene il delegato dell'autenticazione.

  
**Restituisce**: Delegato auth.
  
### <a name="getobserver-function"></a>Getobserver (funzione)
Ottiene l'observer di eventi.

  
**Restituisce**: Observer dell'evento.
  
### <a name="getapplicationinfo-function"></a>GetApplicationInfo (funzione)
Ottiene le informazioni sull'applicazione.

  
**Restituisce**: Informazioni sull'applicazione.
> Deprecato Questo metodo sarà presto deprecato a favore di ottenere/impostare i dati del contesto comuni tramite MIP:: MipContext.
  
### <a name="getmipcontext-function"></a>GetMipContext (funzione)
Ottiene il contesto MIP che rappresenta lo stato condiviso in tutti i profili.

  
**Restituisce**: Contesto MIP
  
### <a name="getloggerdelegate-function"></a>GetLoggerDelegate (funzione)
Ottiene il delegato del logger (se disponibile) fornito dall'applicazione.

  
**Restituisce**: Logger
> Deprecato Questo metodo sarà presto deprecato a favore di ottenere/impostare i dati del contesto comuni tramite MIP:: MipContext.
  
### <a name="setloggerdelegate-function"></a>SetLoggerDelegate (funzione)
Esegue l'override del logger predefinito.

Parametri:  
* **loggerDelegate**: Interfaccia di callback di registrazione implementata dalle applicazioni client


Questo metodo deve essere chiamato dalle applicazioni client che usano la propria implementazione del logger 
> Deprecato Questo metodo sarà presto deprecato a favore di ottenere/impostare i dati del contesto comuni tramite MIP:: MipContext.
  
### <a name="gethttpdelegate-function"></a>GetHttpDelegate (funzione)
Ottiene il delegato HTTP (se disponibile) specificato dall'applicazione.

  
**Restituisce**: Delegato http da usare per le operazioni HTTP
  
### <a name="sethttpdelegate-function"></a>SetHttpDelegate (funzione)
Esegue l'override dello stack HTTP predefinito con quello del client.

Parametri:  
* **httpDelegate**: Interfaccia di callback http implementata dall'applicazione client


  
### <a name="gettaskdispatcherdelegate-function"></a>GetTaskDispatcherDelegate (funzione)
Ottenere il delegato TaskDispatcher (se presente) fornito dall'applicazione.

  
**Restituisce**: Delegato TaskDispatcher da usare per l'esecuzione di attività asincrone
  
### <a name="settaskdispatcherdelegate-function"></a>SetTaskDispatcherDelegate (funzione)
Eseguire l'override della gestione delle attività modo asincrono rispetto predefinite con il client.

Parametri:  
* **taskDispatcherDelegate**: Interfaccia di callback per l'invio di attività implementata dall'applicazione client


  
### <a name="optouttelemetry-function"></a>OptOutTelemetry (funzione)
Rifiuta esplicitamente la raccolta di tutti i dati di telemetria.
> Deprecato Questo metodo sarà presto deprecato a favore di ottenere/impostare i dati del contesto comuni tramite MIP:: MipContext.
  
### <a name="istelemetryoptedout-function"></a>IsTelemetryOptedOut (funzione)
Ottiene un valore che indica se la raccolta dei dati di telemetria deve essere disabilitata o meno.

  
**Restituisce**: True se la raccolta di dati di telemetria deve essere disabilitata altrimenti false
> Deprecato Questo metodo sarà presto deprecato a favore di ottenere/impostare i dati del contesto comuni tramite MIP:: MipContext.
  
### <a name="setminimumloglevel-function"></a>SetMinimumLogLevel (funzione)
Imposta il livello di log minimo che attiverà un evento di registrazione.

Parametri:  
* **logLevel**: livello di log minimo che attiverà un evento di registrazione.


> Deprecato Questo metodo sarà presto deprecato a favore di ottenere/impostare i dati del contesto comuni tramite MIP:: MipContext.
  
### <a name="getminimumloglevel-function"></a>GetMinimumLogLevel (funzione)
Ottiene l'oggetto Livello di log minimo.

  
**Restituisce**: Livello di registrazione minimo che attiverà un evento di registrazione.
> Deprecato Questo metodo sarà presto deprecato a favore di ottenere/impostare i dati del contesto comuni tramite MIP:: MipContext.
  
### <a name="setsessionid-function"></a>Funzione SessionId
_Non ancora documentato._

  
### <a name="getsessionid-function"></a>Funzione GetSessionID
_Non ancora documentato._

  
### <a name="settings-function"></a>~ Settings (funzione)
_Non ancora documentato._
