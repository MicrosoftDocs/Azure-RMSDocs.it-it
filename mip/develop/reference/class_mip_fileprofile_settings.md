---
title: Classe mip FileProfile Settings
description: Riferimento per la classe mip FileProfile Settings
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: 4b79d8eb75a54a56f1b3e48645bdd5eec0afaa19
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/28/2018
ms.locfileid: "47446380"
---
# <a name="class-mipfileprofilesettings"></a>Classe mip::FileProfile::Settings 
Oggetto [Settings](class_mip_fileprofile_settings.md) usato da [FileProfile](class_mip_fileprofile.md) durante la creazione e per tutta la sua durata.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public Settings(const std::string& path, bool useInMemoryStorage, std::shared_ptr<AuthDelegate> authDelegate, std::shared_ptr<ConsentDelegate> consentDelegate, std::shared_ptr<Observer> observer, const ApplicationInfo& applicationInfo)  |  Costruttore [FileProfile::Settings](class_mip_fileprofile_settings.md).
 public const std::string& GetPath() const  |  Ottiene il percorso in cui sono archiviati i dati di registrazione e telemetria e altre informazioni sugli stati persistenti.
 public bool GetUseInMemoryStorage() const  |  Ottiene un valore che indica se tutti gli stati devono essere archiviati in memoria (invece che su disco)
public std::shared_ptr<AuthDelegate> GetAuthDelegate() const  |  Ottiene il delegato dell'autenticazione usato per l'acquisizione dei token di autenticazione.
public std::shared_ptr<ConsentDelegate> GetConsentDelegate() const  |  Ottiene il delegato del consenso usato per richiedere il consenso dell'utente che si connette ai servizi.
public std::shared_ptr<Observer> GetObserver() const  |  Ottiene l'observer che riceve le notifiche degli eventi correlati a [FileProfile](class_mip_fileprofile.md).
 public const ApplicationInfo GetApplicationInfo() const  |  Ottiene informazioni sull'applicazione che sta utilizzando l'SDK.
 public bool GetSkipTelemetryInit() const  |  Ottiene un valore che indica se l'inizializzazione della telemetria deve essere ignorata o meno.
 public void SetSkipTelemetryInit()  |  Disabilita l'inizializzazione della telemetria.
 public void SetNewFeaturesDisabled()  |  Disabilita le nuove funzionalità.
 public bool AreNewFeaturesDisabled() const  |  Ottiene un valore che indica se le nuove funzionalità sono disabilitate o meno.
public std::shared_ptr<LoggerDelegate> GetLoggerDelegate() const  |  Ottiene il delegato del logger (se disponibile) fornito dall'applicazione.
public void SetLoggerDelegate(const std::shared_ptr<LoggerDelegate>& loggerDelegate)  |  Esegue l'override del logger predefinito.
public std::shared_ptr<HttpDelegate> GetHttpDelegate() const  |  Ottiene il delegato HTTP (se disponibile) specificato dall'applicazione.
public void SetHttpDelegate(const std::shared_ptr<HttpDelegate>& httpDelegate)  |  Esegue l'override dello stack HTTP predefinito con quello del client.
 public void OptOutTelemetry()  |  Rifiuta esplicitamente la raccolta di tutti i dati di telemetria.
 public bool IsTelemetryOptedOut() const  |  Ottiene un valore che indica se la raccolta dei dati di telemetria deve essere disabilitata o meno.
 public void SetSessionId(const std::string& sessionId)  |  Imposta l'ID sessione.
 public const std::string& GetSessionId() const  |  Ottiene l'ID sessione.
 public void SetMinimumLogLevel(LogLevel logLevel)  |  Imposta il livello di log minimo che attiverà un evento di registrazione.
 public LogLevel GetMinimumLogLevel() const  |  Ottiene il livello di log minimo che attiverà un evento di registrazione.
  
## <a name="members"></a>Membri
  
### <a name="settings"></a>Impostazioni
Costruttore [FileProfile::Settings](class_mip_fileprofile_settings.md).

Parametri:  
* **path**: percorso in cui sono archiviati i dati di registrazione e telemetria e altre informazioni sugli stati persistenti 


* **useInMemoryStorage**: true se tutti gli stati devono essere archiviati in memoria, false se lo stato può essere memorizzato nella cache su disco 


* **authDelegate**: delegato dell'autenticazione usato per l'acquisizione dei token di autenticazione 


* **observer**: istanza di [Observer](class_mip_fileprofile_observer.md) che riceverà le notifiche degli eventi correlati a [FileProfile](class_mip_fileprofile.md)


* **applicationInfo**: informazioni sull'applicazione che sta utilizzando l'SDK


  
### <a name="getpath"></a>GetPath
Ottiene il percorso in cui sono archiviati i dati di registrazione e telemetria e altre informazioni sugli stati persistenti.

  
**Restituisce**: percorso in cui sono archiviati i dati di registrazione e telemetria e altre informazioni sugli stati persistenti
  
### <a name="getuseinmemorystorage"></a>GetUseInMemoryStorage
Ottiene un valore che indica se tutti gli stati devono essere archiviati in memoria (invece che su disco)

  
**Restituisce**: valore che indica se tutti gli stati devono essere archiviati in memoria (invece che su disco)
  
### <a name="getauthdelegate"></a>GetAuthDelegate
Ottiene il delegato dell'autenticazione usato per l'acquisizione dei token di autenticazione.

  
**Restituisce**: delegato dell'autenticazione usato per l'acquisizione dei token di autenticazione
  
### <a name="consentdelegate"></a>ConsentDelegate
Ottiene il delegato del consenso usato per richiedere il consenso dell'utente che si connette ai servizi.

  
**Restituisce**: delegato del consenso usato per richiedere il consenso dell'utente
  
### <a name="observer"></a>Osservatore
Ottiene l'observer che riceve le notifiche degli eventi correlati a [FileProfile](class_mip_fileprofile.md).

  
**Restituisce**: [observer](class_mip_fileprofile_observer.md) che riceve le notifiche degli eventi correlati a [FileProfile](class_mip_fileprofile.md)
  
### <a name="applicationinfo"></a>ApplicationInfo
Ottiene informazioni sull'applicazione che sta utilizzando l'SDK.

  
**Restituisce**: informazioni sull'applicazione che sta utilizzando l'SDK
  
### <a name="getskiptelemetryinit"></a>GetSkipTelemetryInit
Ottiene un valore che indica se l'inizializzazione della telemetria deve essere ignorata o meno.

  
**Restituisce**: valore che indica se l'inizializzazione della telemetria deve essere ignorata o meno
  
### <a name="setskiptelemetryinit"></a>SetSkipTelemetryInit
Disabilita l'inizializzazione della telemetria.
Questo metodo non viene in genere chiamato dalle applicazioni client, ma viene usato dall'SDK per i file per impedire l'inizializzazione duplicata
  
### <a name="setnewfeaturesdisabled"></a>SetNewFeaturesDisabled
Disabilita le nuove funzionalità.
Per le applicazioni che non vogliono provare le nuove funzionalità
  
### <a name="arenewfeaturesdisabled"></a>AreNewFeaturesDisabled
Ottiene un valore che indica se le nuove funzionalità sono disabilitate o meno.

  
**Restituisce**: valore che indica se le nuove funzionalità sono disabilitate o meno
  
### <a name="loggerdelegate"></a>LoggerDelegate
Ottiene il delegato del logger (se disponibile) fornito dall'applicazione.

  
**Restituisce**: logger
  
### <a name="setloggerdelegate"></a>SetLoggerDelegate
Esegue l'override del logger predefinito.

Parametri:  
* **loggerDelegate**: interfaccia di callback di registrazione implementata dalle applicazioni client


Questo metodo deve essere chiamato dalle applicazioni client che usano la propria implementazione del logger
  
### <a name="httpdelegate"></a>HttpDelegate
Ottiene il delegato HTTP (se disponibile) specificato dall'applicazione.

  
**Restituisce**: delegato HTTP da usare per le operazioni HTTP
  
### <a name="sethttpdelegate"></a>SetHttpDelegate
Esegue l'override dello stack HTTP predefinito con quello del client.

Parametri:  
* **httpDelegate**: interfaccia di callback HTTP implementata dall'applicazione client


  
### <a name="optouttelemetry"></a>OptOutTelemetry
Rifiuta esplicitamente la raccolta di tutti i dati di telemetria.
  
### <a name="istelemetryoptedout"></a>IsTelemetryOptedOut
Ottiene un valore che indica se la raccolta dei dati di telemetria deve essere disabilitata o meno.

  
**Restituisce**: valore che indica se la raccolta dei dati di telemetria deve essere disabilitata o meno
  
### <a name="setsessionid"></a>SetSessionId
Imposta l'ID sessione.

Parametri:  
* **sessionId**: ID sessione che verrà usato per la correlazione di log/telemetria


  
### <a name="getsessionid"></a>GetSessionId
Ottiene l'ID sessione.

  
**Restituisce**: ID sessione che verrà usato per la correlazione di log/telemetria
  
### <a name="setminimumloglevel"></a>SetMinimumLogLevel
Imposta il livello di log minimo che attiverà un evento di registrazione.

Parametri:  
* **logLevel**: livello di log minimo che attiverà un evento di registrazione. 



  
**Restituisce**: true
  
### <a name="loglevel"></a>LogLevel
Ottiene il livello di log minimo che attiverà un evento di registrazione.

  
**Restituisce**: livello di log minimo che attiverà un evento di registrazione.