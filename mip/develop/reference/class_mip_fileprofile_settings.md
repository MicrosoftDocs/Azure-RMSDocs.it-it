---
title: Classe mip::FileProfile::Settings
description: 'Classe MIP:: fileprofile di Microsoft Information Protection (MIP) SDK vengono documentate.'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: fa61567ce2ca239db7cbde9b69837dacb4fc5fe0
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/14/2019
ms.locfileid: "56253236"
---
# <a name="class-mipfileprofilesettings"></a>Classe mip::FileProfile::Settings 
Oggetto [Settings](class_mip_fileprofile_settings.md) usato da [FileProfile](class_mip_fileprofile.md) durante la creazione e per tutta la sua durata.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
Impostazioni pubbliche (std:: shared_ptr const std:: String & percorso, useInMemoryStorage, bool\<AuthDelegate\> authDelegate, std:: shared_ptr\<ConsentDelegate\> consentDelegate, std:: shared_ptr\< Osservatore\> observer, const ApplicationInfo & applicationInfo)  |  Costruttore [FileProfile::Settings](class_mip_fileprofile_settings.md).
public const std::string& GetPath() const  |  Ottiene il percorso in cui sono archiviati i dati di registrazione e telemetria e altre informazioni sugli stati persistenti.
public bool GetUseInMemoryStorage() const  |  Ottiene un valore che indica se tutti gli stati devono essere archiviati in memoria (invece che su disco)
Public std:: shared_ptr\<AuthDelegate\> GetAuthDelegate() const  |  Ottiene il delegato dell'autenticazione usato per l'acquisizione dei token di autenticazione.
Public std:: shared_ptr\<ConsentDelegate\> GetConsentDelegate() const  |  Ottiene il delegato del consenso usato per richiedere il consenso dell'utente che si connette ai servizi.
Public std:: shared_ptr\<osservatore\> GetObserver() const  |  Ottiene l'observer che riceve le notifiche degli eventi correlati a [FileProfile](class_mip_fileprofile.md).
public const ApplicationInfo GetApplicationInfo() const  |  Ottiene informazioni sull'applicazione che sta utilizzando l'SDK.
public bool GetSkipTelemetryInit() const  |  Ottiene un valore che indica se l'inizializzazione della telemetria deve essere ignorata o meno.
public void SetSkipTelemetryInit()  |  Disabilita l'inizializzazione della telemetria.
public void SetNewFeaturesDisabled()  |  Disabilita le nuove funzionalità.
public bool AreNewFeaturesDisabled() const  |  Ottiene un valore che indica se le nuove funzionalità sono disabilitate o meno.
Public std:: shared_ptr\<LoggerDelegate\> GetLoggerDelegate() const  |  Ottiene il delegato del logger (se disponibile) fornito dall'applicazione.
public void SetLoggerDelegate (const std:: shared_ptr\<LoggerDelegate\>& loggerDelegate)  |  Esegue l'override del logger predefinito.
Public std:: shared_ptr\<HttpDelegate\> GetHttpDelegate() const  |  Ottiene il delegato HTTP (se disponibile) specificato dall'applicazione.
public void SetHttpDelegate (const std:: shared_ptr\<HttpDelegate\>& httpDelegate)  |  Esegue l'override dello stack HTTP predefinito con quello del client.
public void OptOutTelemetry()  |  Rifiuta esplicitamente la raccolta di tutti i dati di telemetria.
public bool IsTelemetryOptedOut() const  |  Ottiene un valore che indica se la raccolta dei dati di telemetria deve essere disabilitata o meno.
public void SetSessionId(const std::string& sessionId)  |  Imposta l'ID sessione.
public const std::string& GetSessionId() const  |  Ottiene l'ID sessione.
public void SetMinimumLogLevel(LogLevel logLevel)  |  Imposta il livello di log minimo che attiverà un evento di registrazione.
public LogLevel GetMinimumLogLevel() const  |  Ottiene il livello di log minimo che attiverà un evento di registrazione.
  
## <a name="members"></a>Membri
  
### <a name="settings-function"></a>Funzione impostazioni
Costruttore [FileProfile::Settings](class_mip_fileprofile_settings.md).

Parametri:  
* **path**: Percorso del file in cui la registrazione, la telemetria e altre viene archiviato lo stato permanente 


* **useInMemoryStorage**: true se tutti gli stati devono essere archiviati in memoria, false se lo stato può essere memorizzato nella cache su disco 


* **authDelegate**: Delegato dell'autenticazione usato per l'acquisizione dei token di autenticazione 


* **observer**: [Osservatore](class_mip_fileprofile_observer.md) istanza che riceverà le notifiche degli eventi correlati a [FileProfile](class_mip_fileprofile.md)


* **applicationInfo**: Informazioni sull'applicazione che utilizza il SDK


  
### <a name="getpath-function"></a>GetPath (funzione)
Ottiene il percorso in cui sono archiviati i dati di registrazione e telemetria e altre informazioni sugli stati persistenti.

  
**Restituisce**: Percorso in cui la registrazione, la telemetria e altre viene archiviato lo stato permanente
  
### <a name="getuseinmemorystorage-function"></a>GetUseInMemoryStorage (funzione)
Ottiene un valore che indica se tutti gli stati devono essere archiviati in memoria (invece che su disco)

  
**Restituisce**: Se tutti gli stati devono essere archiviati in memoria (in contrapposizione a su disco)
  
### <a name="getauthdelegate-function"></a>GetAuthDelegate (funzione)
Ottiene il delegato dell'autenticazione usato per l'acquisizione dei token di autenticazione.

  
**Restituisce**: Delegato dell'autenticazione usato per l'acquisizione dei token di autenticazione
  
### <a name="getconsentdelegate-function"></a>GetConsentDelegate (funzione)
Ottiene il delegato del consenso usato per richiedere il consenso dell'utente che si connette ai servizi.

  
**Restituisce**: Delegato usato per richiedere il consenso dell'utente di consenso
  
### <a name="getobserver-function"></a>GetObserver (funzione)
Ottiene l'observer che riceve le notifiche degli eventi correlati a [FileProfile](class_mip_fileprofile.md).

  
**Restituisce**: [Osservatore](class_mip_fileprofile_observer.md) che riceve le notifiche degli eventi correlati alla [FileProfile](class_mip_fileprofile.md)
  
### <a name="getapplicationinfo-function"></a>GetApplicationInfo function
Ottiene informazioni sull'applicazione che sta utilizzando l'SDK.

  
**Restituisce**: Informazioni sull'applicazione che utilizza il SDK
  
### <a name="getskiptelemetryinit-function"></a>GetSkipTelemetryInit (funzione)
Ottiene un valore che indica se l'inizializzazione della telemetria deve essere ignorata o meno.

  
**Restituisce**: Se l'inizializzazione della telemetria deve essere ignorata o No
  
### <a name="setskiptelemetryinit-function"></a>SetSkipTelemetryInit (funzione)
Disabilita l'inizializzazione della telemetria.
Questo metodo non viene in genere chiamato dalle applicazioni client, ma viene usato dall'SDK per i file per impedire l'inizializzazione duplicata
  
### <a name="setnewfeaturesdisabled-function"></a>SetNewFeaturesDisabled (funzione)
Disabilita le nuove funzionalità.
Per le applicazioni che non vogliono provare le nuove funzionalità
  
### <a name="arenewfeaturesdisabled-function"></a>AreNewFeaturesDisabled (funzione)
Ottiene un valore che indica se le nuove funzionalità sono disabilitate o meno.

  
**Restituisce**: Se le nuove funzionalità sono disabilitate o non
  
### <a name="getloggerdelegate-function"></a>GetLoggerDelegate (funzione)
Ottiene il delegato del logger (se disponibile) fornito dall'applicazione.

  
**Restituisce**: Logger
  
### <a name="setloggerdelegate-function"></a>SetLoggerDelegate (funzione)
Esegue l'override del logger predefinito.

Parametri:  
* **loggerDelegate**: La registrazione di interfaccia di callback implementata dalle applicazioni client


Questo metodo deve essere chiamato dalle applicazioni client che usano la propria implementazione del logger
  
### <a name="gethttpdelegate-function"></a>GetHttpDelegate (funzione)
Ottiene il delegato HTTP (se disponibile) specificato dall'applicazione.

  
**Restituisce**: Delegato HTTP da utilizzare per le operazioni HTTP
  
### <a name="sethttpdelegate-function"></a>SetHttpDelegate (funzione)
Esegue l'override dello stack HTTP predefinito con quello del client.

Parametri:  
* **httpDelegate**: Interfaccia di callback HTTP implementato dall'applicazione client


  
### <a name="optouttelemetry-function"></a>OptOutTelemetry (funzione)
Rifiuta esplicitamente la raccolta di tutti i dati di telemetria.
  
### <a name="istelemetryoptedout-function"></a>IsTelemetryOptedOut (funzione)
Ottiene un valore che indica se la raccolta dei dati di telemetria deve essere disabilitata o meno.

  
**Restituisce**: Se la raccolta di dati di telemetria deve essere disabilitata o non
  
### <a name="setsessionid-function"></a>SetSessionId (funzione)
Imposta l'ID sessione.

Parametri:  
* **sessionId**: ID di sessione che verrà usato per correlare i log e telemetria


  
### <a name="getsessionid-function"></a>GetSessionId (funzione)
Ottiene l'ID sessione.

  
**Restituisce**: ID di sessione che verrà usato per correlare i log e telemetria
  
### <a name="setminimumloglevel-function"></a>SetMinimumLogLevel (funzione)
Imposta il livello di log minimo che attiverà un evento di registrazione.

Parametri:  
* **logLevel**: livello di log minimo che attiverà un evento di registrazione. 



  
**Restituisce**: True
  
### <a name="getminimumloglevel-function"></a>GetMinimumLogLevel (funzione)
Ottiene il livello di log minimo che attiverà un evento di registrazione.

  
**Restituisce**: Più basso livello di registrazione che attiverà un evento di registrazione.
