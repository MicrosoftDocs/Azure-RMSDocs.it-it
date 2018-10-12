---
title: Classe mip PolicyProfile Settings
description: Riferimento per la classe mip PolicyProfile Settings
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: 07cbcbc022c02a43f751e1cf55b5b0efdfb816d1
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/28/2018
ms.locfileid: "47446877"
---
# <a name="class-mippolicyprofilesettings"></a>Classe mip::PolicyProfile::Settings 
Oggetto [Settings](class_mip_policyprofile_settings.md) usato da [PolicyProfile](class_mip_policyprofile.md) durante la creazione e per tutta la sua durata.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public Settings(const std::string& path, bool useInMemoryStorage, const std::shared_ptr<AuthDelegate>& authDelegate, const std::shared_ptr<PolicyProfile::Observer>& observer, const ApplicationInfo& applicationInfo)  |  Interfaccia per la configurazione del profilo.
 public const std::string& GetPath() const  |  Ottiene il percorso dello stato archiviato.
 public bool GetUseInMemoryStorage() const  |  Ottiene il flag UseInMemoryStorage.
public const std::shared_ptr<AuthDelegate>& GetAuthDelegate() const  |  Ottiene il delegato dell'autenticazione.
public const std::shared_ptr<PolicyProfile::Observer>& GetObserver() const  |  Ottiene l'observer di eventi.
 public const ApplicationInfo GetApplicationInfo() const  |  Ottiene le informazioni sull'applicazione.
public std::shared_ptr<LoggerDelegate> GetLoggerDelegate() const  |  Ottiene il delegato del logger (se disponibile) fornito dall'applicazione.
public void SetLoggerDelegate(const std::shared_ptr<LoggerDelegate>& loggerDelegate)  |  Esegue l'override del logger predefinito.
public std::shared_ptr<HttpDelegate> GetHttpDelegate() const  |  Ottiene il delegato HTTP (se disponibile) specificato dall'applicazione.
public void SetHttpDelegate(const std::shared_ptr<HttpDelegate>& httpDelegate)  |  Esegue l'override dello stack HTTP predefinito con quello del client.
 public void OptOutTelemetry()  |  Rifiuta esplicitamente la raccolta di tutti i dati di telemetria.
 public bool IsTelemetryOptedOut() const  |  Ottiene un valore indicante se la raccolta dei dati di telemetria deve essere disabilitata o meno.
 public void SetMinimumLogLevel(LogLevel logLevel)  |  Imposta il livello di log minimo che attiverà un evento di registrazione.
 public LogLevel GetMinimumLogLevel() const  |  Ottiene l'oggetto Livello di log minimo.
  
## <a name="members"></a>Membri
  
### <a name="settings"></a>Impostazioni
Interfaccia per la configurazione del profilo.

Parametri:  
* **path**: percorso di una directory in cui l'SDK archivierà lo stato del profilo. 


* **useInMemoryStorage**: archivia nella memoria invece che su disco gli stati memorizzati nella cache. 


* **authDelegate**: delegato dell'autenticazione usato dall'SDK per acquisire i token di autenticazione. 


* **observer**: classe che implementa l'interfaccia [PolicyProfile::Observer](class_mip_policyprofile_observer.md). Può essere nullptr. 


* **applicationInfo**: identificatori dell'applicazione usati per l'accesso al servizio.


  
### <a name="getpath"></a>GetPath
Ottiene il percorso dello stato archiviato.

  
**Restituisce**: percorso dello stato archiviato.
  
### <a name="getuseinmemorystorage"></a>GetUseInMemoryStorage
Ottiene il flag UseInMemoryStorage.

  
**Restituisce**: true se è impostato l'uso dell'archiviazione in memoria, false in caso contrario.
  
### <a name="getauthdelegate"></a>GetAuthDelegate
Ottiene il delegato dell'autenticazione.

  
**Restituisce**: delegato dell'autenticazione.
  
### <a name="policyprofileobserver"></a>PolicyProfile::Observer
Ottiene l'observer di eventi.

  
**Restituisce**: observer di eventi.
  
### <a name="applicationinfo"></a>ApplicationInfo
Ottiene le informazioni sull'applicazione.

  
**Restituisce**: informazioni sull'applicazione.
  
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

  
**Restituisce**: il delegato HTTP da usare per le operazioni HTTP
  
### <a name="sethttpdelegate"></a>SetHttpDelegate
Esegue l'override dello stack HTTP predefinito con quello del client.

Parametri:  
* **httpDelegate**: interfaccia di callback HTTP implementata dall'applicazione client


  
### <a name="optouttelemetry"></a>OptOutTelemetry
Rifiuta esplicitamente la raccolta di tutti i dati di telemetria.
  
### <a name="istelemetryoptedout"></a>IsTelemetryOptedOut
Ottiene un valore indicante se la raccolta dei dati di telemetria deve essere disabilitata o meno.

  
**Restituisce**: un valore indicante se la raccolta dei dati di telemetria deve essere disabilitata o meno.
  
### <a name="setminimumloglevel"></a>SetMinimumLogLevel
Imposta il livello di log minimo che attiverà un evento di registrazione.

Parametri:  
* **logLevel**: livello di log minimo che attiverà un evento di registrazione. 



  
**Restituisce**: True
  
### <a name="loglevel"></a>LogLevel
Ottiene l'oggetto Livello di log minimo.

  
**Restituisce**: il livello di log minimo che attiverà un evento di registrazione.