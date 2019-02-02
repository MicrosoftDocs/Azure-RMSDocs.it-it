---
title: Classe mip::PolicyProfile::Settings
description: Documenta la classe mip::policyprofile di Microsoft Information Protection (MIP) SDK.
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: d6a0c773226fff789889bd82a6075a65cff184bd
ms.sourcegitcommit: be05adc7750e22c110b261882de0389b9dfb2726
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/02/2019
ms.locfileid: "55651123"
---
# <a name="class-mippolicyprofilesettings"></a>Classe mip::PolicyProfile::Settings 
Oggetto [Settings](class_mip_policyprofile_settings.md) usato da [PolicyProfile](class_mip_policyprofile.md) durante la creazione e per tutta la sua durata.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
Impostazioni pubbliche (const std:: String & percorso, bool useInMemoryStorage, const std:: shared_ptr\<AuthDelegate\>& authDelegate, const std:: shared_ptr\<PolicyProfile::Observer\>& Observer, const ApplicationInfo & applicationInfo)  |  Interfaccia per la configurazione del profilo.
public const std::string& GetPath() const  |  Ottiene il percorso dello stato archiviato.
public bool GetUseInMemoryStorage() const  |  Ottiene il flag UseInMemoryStorage.
Public std:: shared_ptr const\<AuthDelegate\>& GetAuthDelegate() const  |  Ottiene il delegato dell'autenticazione.
Public std:: shared_ptr const\<PolicyProfile::Observer\>& GetObserver() const  |  Ottiene l'observer di eventi.
public const ApplicationInfo GetApplicationInfo() const  |  Ottiene le informazioni sull'applicazione.
Public std:: shared_ptr\<LoggerDelegate\> GetLoggerDelegate() const  |  Ottiene il delegato del logger (se disponibile) fornito dall'applicazione.
public void SetLoggerDelegate (const std:: shared_ptr\<LoggerDelegate\>& loggerDelegate)  |  Esegue l'override del logger predefinito.
Public std:: shared_ptr\<HttpDelegate\> GetHttpDelegate() const  |  Ottiene il delegato HTTP (se disponibile) specificato dall'applicazione.
public void SetHttpDelegate (const std:: shared_ptr\<HttpDelegate\>& httpDelegate)  |  Esegue l'override dello stack HTTP predefinito con quello del client.
public void OptOutTelemetry()  |  Rifiuta esplicitamente la raccolta di tutti i dati di telemetria.
public bool IsTelemetryOptedOut() const  |  Ottiene un valore che indica se la raccolta dei dati di telemetria deve essere disabilitata o meno.
public void SetMinimumLogLevel(LogLevel logLevel)  |  Imposta il livello di log minimo che attiverà un evento di registrazione.
public LogLevel GetMinimumLogLevel() const  |  Ottiene l'oggetto Livello di log minimo.
  
## <a name="members"></a>Membri
  
### <a name="settings-function"></a>Funzione impostazioni
Interfaccia per la configurazione del profilo.

Parametri:  
* **path**: Il percorso di una directory in cui il SDK archivierà lo stato del profilo. 


* **useInMemoryStorage**: Store qualsiasi stato memorizzato nella cache in memoria anziché su disco. 


* **authDelegate**: Il delegato di autenticazione usato dal SDK per acquisire i token di autenticazione. 


* **observer**: Una classe che implementa il [PolicyProfile::Observer](class_mip_policyprofile_observer.md) interfaccia. Può essere nullptr. 


* **applicationInfo**: Gli identificatori dell'applicazione usati per l'accesso del servizio.


  
### <a name="getpath-function"></a>GetPath (funzione)
Ottiene il percorso dello stato archiviato.

  
**Restituisce**: Percorso dello stato archiviato.
  
### <a name="getuseinmemorystorage-function"></a>GetUseInMemoryStorage (funzione)
Ottiene il flag UseInMemoryStorage.

  
**Restituisce**: True se l'utilizzo in memoria viene altrimenti impostato false.
  
### <a name="getauthdelegate-function"></a>GetAuthDelegate (funzione)
Ottiene il delegato dell'autenticazione.

  
**Restituisce**: Delegato dell'autenticazione.
  
### <a name="getobserver-function"></a>GetObserver (funzione)
Ottiene l'observer di eventi.

  
**Restituisce**: Observer di eventi.
  
### <a name="getapplicationinfo-function"></a>GetApplicationInfo function
Ottiene le informazioni sull'applicazione.

  
**Restituisce**: Le informazioni sull'applicazione.
  
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

  
**Restituisce**: Delegato di HTTP da utilizzare per le operazioni HTTP
  
### <a name="sethttpdelegate-function"></a>SetHttpDelegate (funzione)
Esegue l'override dello stack HTTP predefinito con quello del client.

Parametri:  
* **httpDelegate**: Interfaccia di callback HTTP implementato dall'applicazione client


  
### <a name="optouttelemetry-function"></a>OptOutTelemetry (funzione)
Rifiuta esplicitamente la raccolta di tutti i dati di telemetria.
  
### <a name="istelemetryoptedout-function"></a>IsTelemetryOptedOut (funzione)
Ottiene un valore che indica se la raccolta dei dati di telemetria deve essere disabilitata o meno.

  
**Restituisce**: True se la raccolta di dati di telemetria deve essere disabilitato in caso contrario false
  
### <a name="setminimumloglevel-function"></a>SetMinimumLogLevel (funzione)
Imposta il livello di log minimo che attiverà un evento di registrazione.

Parametri:  
* **logLevel**: livello di log minimo che attiverà un evento di registrazione. 



  
**Restituisce**: True
  
### <a name="getminimumloglevel-function"></a>GetMinimumLogLevel (funzione)
Ottiene l'oggetto Livello di log minimo.

  
**Restituisce**: Livello log minimo che attiverà un evento di registrazione.