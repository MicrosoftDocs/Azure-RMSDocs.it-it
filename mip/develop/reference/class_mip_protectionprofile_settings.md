---
title: Classe mip ProtectionProfile Settings
description: Riferimento per la classe mip ProtectionProfile Settings
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: fe2413b2265cf4994dce0e57a7c472d59336902a
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/28/2018
ms.locfileid: "47446669"
---
# <a name="class-mipprotectionprofilesettings"></a>Classe mip::ProtectionProfile::Settings 
Oggetto [Settings](class_mip_protectionprofile_settings.md) usato da [ProtectionProfile](class_mip_protectionprofile.md) durante la creazione e per tutta la sua durata.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public Settings(const std::string& path, bool useInMemoryStorage, const std::shared_ptr<AuthDelegate>& authDelegate, const std::shared_ptr<ConsentDelegate>& consentDelegate, const std::shared_ptr<ProtectionProfile::Observer>& observer, const ApplicationInfo& applicationInfo)  |  Costruttore [ProtectionProfile::Settings](class_mip_protectionprofile_settings.md) che specifica un observer da usare per le operazioni asincrone.
public Settings(const std::string& path, bool useInMemoryStorage, const std::shared_ptr<AuthDelegate>& authDelegate, const std::shared_ptr<ConsentDelegate>& consentDelegate, const ApplicationInfo& applicationInfo)  |  Costruttore [ProtectionProfile::Settings](class_mip_protectionprofile_settings.md), usato per le operazioni sincrone.
 public const std::string& GetPath() const  |  Ottiene il percorso in cui sono archiviati i dati di registrazione e telemetria e altre informazioni collaterali di protezione.
 public bool GetUseInMemoryStorage() const  |  Ottiene un valore indicante se le cache vengono archiviate o meno solo nella memoria (invece che su disco)
public std::shared_ptr<AuthDelegate> GetAuthDelegate() const  |  Ottiene il delegato dell'autenticazione usato per l'acquisizione dei token di autenticazione.
public std::shared_ptr<ConsentDelegate> GetConsentDelegate() const  |  Ottiene il delegato del consenso usato per la connessione ai servizi.
public std::shared_ptr<ProtectionProfile::Observer> GetObserver() const  |  Ottiene l'observer che riceve le notifiche degli eventi correlati a [ProtectionProfile](class_mip_protectionprofile.md).
 public const ApplicationInfo& GetApplicationInfo() const  |  Ottiene informazioni sull'applicazione che sta utilizzando l'SDK di protezione.
 public void OptOutTelemetry()  |  Rifiuta esplicitamente la raccolta di tutti i dati di telemetria.
 public bool IsTelemetryOptedOut() const  |  Ottiene un valore che indica se la raccolta dei dati di telemetria deve essere disabilitata o meno.
public std::shared_ptr<LoggerDelegate> GetLoggerDelegate() const  |  Ottiene il delegato del logger (se disponibile) fornito dall'applicazione.
public void SetLoggerDelegate(const std::shared_ptr<LoggerDelegate>& loggerDelegate)  |  Esegue l'override del logger predefinito.
public std::shared_ptr<HttpDelegate> GetHttpDelegate() const  |  Ottiene il delegato HTTP (se disponibile) specificato dall'applicazione.
public void SetHttpDelegate(const std::shared_ptr<HttpDelegate>& httpDelegate)  |  Esegue l'override dello stack HTTP predefinito con quello del client.
 public bool GetSkipTelemetryInit() const  |  Ottiene un valore che indica se l'inizializzazione della telemetria deve essere ignorata o meno.
 public void SetSkipTelemetryInit()  |  Disabilita l'inizializzazione della telemetria.
 public void SetNewFeaturesDisabled()  |  Disabilita le nuove funzionalità.
 public bool AreNewFeaturesDisabled() const  |  Ottiene un valore che indica se le nuove funzionalità sono disabilitate o meno.
 public void SetSessionId(const std::string& sessionId)  |  Imposta l'ID sessione.
 public const std::string& GetSessionId() const  |  Ottiene l'ID sessione.
 public void SetMinimumLogLevel(LogLevel logLevel)  |  Imposta il livello di log minimo che attiverà un evento di registrazione.
 public LogLevel GetMinimumLogLevel() const  |  Ottiene l'oggetto Livello di log minimo.
  
## <a name="members"></a>Membri
  
### <a name="settings"></a>Impostazioni
Costruttore [ProtectionProfile::Settings](class_mip_protectionprofile_settings.md) che specifica un observer da usare per le operazioni asincrone.

Parametri:  
* **path**: percorso in cui sono archiviati i dati di registrazione e telemetria e altre informazioni collaterali di protezione 


* **useInMemoryStorage**: archivia nella memoria invece che su disco gli stati memorizzati nella cache 


* **authDelegate**: oggetto di callback da usare per l'autenticazione, implemento dall'applicazione client 


* **observer**: istanza di [Observer](class_mip_protectionprofile_observer.md) che riceverà le notifiche degli eventi correlati a [ProtectionProfile](class_mip_protectionprofile.md)


* **applicationInfo**: informazioni sull'applicazione che sta utilizzando l'SDK di protezione


  
### <a name="settings"></a>Impostazioni
Costruttore [ProtectionProfile::Settings](class_mip_protectionprofile_settings.md), usato per le operazioni sincrone.

Parametri:  
* **path**: percorso in cui sono archiviati i dati di registrazione e telemetria e altre informazioni collaterali di protezione 


* **useInMemoryStorage**: archivia nella memoria invece che su disco gli stati memorizzati nella cache 


* **authDelegate**: oggetto di callback da usare per l'autenticazione, implemento dall'applicazione client 


* **applicationInfo**: informazioni sull'applicazione che sta utilizzando l'SDK di protezione


  
### <a name="getpath"></a>GetPath
Ottiene il percorso in cui sono archiviati i dati di registrazione e telemetria e altre informazioni collaterali di protezione.

  
**Restituisce**: percorso in cui sono archiviati i dati di registrazione e telemetria e altre informazioni collaterali di protezione
  
### <a name="getuseinmemorystorage"></a>GetUseInMemoryStorage
Ottiene un valore indicante se le cache vengono archiviate o meno solo nella memoria (invece che su disco)

  
**Restituisce**: true se le cache vengono archiviate solo nella memoria
  
### <a name="getauthdelegate"></a>GetAuthDelegate
Ottiene il delegato dell'autenticazione usato per l'acquisizione dei token di autenticazione.

  
**Restituisce**: delegato dell'autenticazione usato per l'acquisizione dei token di autenticazione
  
### <a name="consentdelegate"></a>ConsentDelegate
Ottiene il delegato del consenso usato per la connessione ai servizi.

  
**Restituisce**: delegato del consenso usato per la connessione ai servizi
  
### <a name="protectionprofileobserver"></a>ProtectionProfile::Observer
Ottiene l'observer che riceve le notifiche degli eventi correlati a [ProtectionProfile](class_mip_protectionprofile.md).

  
**Restituisce**: [observer](class_mip_protectionprofile_observer.md) che riceve le notifiche degli eventi correlati a [ProtectionProfile](class_mip_protectionprofile.md)
  
### <a name="applicationinfo"></a>ApplicationInfo
Ottiene informazioni sull'applicazione che sta utilizzando l'SDK di protezione.

  
**Restituisce**: informazioni sull'applicazione che sta utilizzando l'SDK di protezione
  
### <a name="optouttelemetry"></a>OptOutTelemetry
Rifiuta esplicitamente la raccolta di tutti i dati di telemetria.
  
### <a name="istelemetryoptedout"></a>IsTelemetryOptedOut
Ottiene un valore che indica se la raccolta dei dati di telemetria deve essere disabilitata o meno.

  
**Restituisce**: valore che indica se la raccolta dei dati di telemetria deve essere disabilitata o meno
  
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
Ottiene l'oggetto Livello di log minimo.

  
**Restituisce**: livello di log minimo che attiverà un evento di registrazione.