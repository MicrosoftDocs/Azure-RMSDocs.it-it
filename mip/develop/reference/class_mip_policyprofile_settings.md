---
title: 'Classe PolicyProfile:: Settings'
description: "Documenta la classe policyprofile:: Settings dell'SDK Microsoft Information Protection (MIP)."
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 09/21/2020
ms.openlocfilehash: 2ec38a34f2522448704f1be91d03c62761cafdf6
ms.sourcegitcommit: 3f5f9f7695b9ed3c45e9230cd8b8cb39a1c5a5ed
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/23/2020
ms.locfileid: "95566660"
---
# <a name="class-policyprofilesettings"></a>Classe PolicyProfile:: Settings 
Oggetto Settings usato da PolicyProfile durante la creazione e per tutta la sua durata.
  
## <a name="summary"></a>Riepilogo
 Members                        | Descrizioni                                
--------------------------------|---------------------------------------------
Impostazioni pubbliche (const std:: shared_ptr \<MipContext\>& mipContext, cacheStorageType CacheStorageType, const std:: shared_ptr \<PolicyProfile::Observer\>& Observer)  |  Interfaccia per la configurazione del profilo.
public CacheStorageType GetCacheStorageType () const  |  Ottiene un valore che indica se le cache sono archiviate in memoria o su disco.
public const std:: shared_ptr \<PolicyProfile::Observer\>& getobserver () const  |  Ottiene l'observer di eventi.
public std:: shared_ptr \<MipContext\> GetMipContext () const  |  Ottiene il contesto MIP che rappresenta lo stato condiviso in tutti i profili.
public std::shared_ptr\<HttpDelegate\> GetHttpDelegate() const  |  Ottiene il delegato HTTP (se disponibile) specificato dall'applicazione.
public void SetHttpDelegate(const std::shared_ptr\<HttpDelegate\>& httpDelegate)  |  Esegue l'override dello stack HTTP predefinito con quello del client.
public std:: shared_ptr \<TaskDispatcherDelegate\> GetTaskDispatcherDelegate () const  |  Ottenere il delegato TaskDispatcher (se presente) fornito dall'applicazione.
public void SetTaskDispatcherDelegate (const std:: shared_ptr \<TaskDispatcherDelegate\>& taskDispatcherDelegate)  |  Esegue l'override della gestione predefinita dell'invio delle attività asincrone con il proprio client.
public void SetSessionId(const std::string& sessionId)  | _Non ancora documentato._
public const std::string& GetSessionId() const  | _Non ancora documentato._
public void SetCustomSettings (const std:: Vector \<std::pair\<std::string, std::string\> \>& customSettings)  |  Imposta le impostazioni personalizzate, usate a scopi di controllo e test delle funzionalità.
public const std:: Vector \<std::pair\<std::string, std::string\> \>& GetCustomSettings () const  |  Ottiene le impostazioni personalizzate, usate a scopi di controllo e test delle funzionalità.
public ~Settings()  | _Non ancora documentato._
  
## <a name="members"></a>Members
  
### <a name="settings-function"></a>Funzione Settings
Interfaccia per la configurazione del profilo.

Parametri  
* **mipContext**: impostazioni di contesto globali 


* **cacheStorageType**: archivia lo stato memorizzato nella cache in memoria o su disco 


* **observer**: classe che implementa l'interfaccia PolicyProfile::Observer. Può essere nullptr.


  
### <a name="getcachestoragetype-function"></a>GetCacheStorageType (funzione)
Ottiene un valore che indica se le cache sono archiviate in memoria o su disco.

  
**Restituisce**: tipo di archiviazione usato
  
### <a name="getobserver-function"></a>Getobserver (funzione)
Ottiene l'observer di eventi.

  
**Restituisce**: observer di eventi.
  
### <a name="getmipcontext-function"></a>GetMipContext (funzione)
Ottiene il contesto MIP che rappresenta lo stato condiviso in tutti i profili.

  
**Restituisce**: contesto MIP
  
### <a name="gethttpdelegate-function"></a>GetHttpDelegate (funzione)
Ottiene il delegato HTTP (se disponibile) specificato dall'applicazione.

  
**Restituisce**: delegato http da usare per le operazioni http
  
### <a name="sethttpdelegate-function"></a>SetHttpDelegate (funzione)
Esegue l'override dello stack HTTP predefinito con quello del client.

Parametri  
* **httpDelegate**: interfaccia di callback HTTP implementata dall'applicazione client


  
### <a name="gettaskdispatcherdelegate-function"></a>GetTaskDispatcherDelegate (funzione)
Ottenere il delegato TaskDispatcher (se presente) fornito dall'applicazione.

  
**Restituisce**: delegato TaskDispatcher da usare per l'esecuzione di attività asincrone
  
### <a name="settaskdispatcherdelegate-function"></a>SetTaskDispatcherDelegate (funzione)
Esegue l'override della gestione predefinita dell'invio delle attività asincrone con il proprio client.

Parametri  
* **taskDispatcherDelegate**: interfaccia di callback di invio dell'attività implementata dall'applicazione client


le attività possono fare riferimento a oggetti del profilo che ne impediscono la distruzione come risultato taskdispatcher le code non devono essere condivise.
  
### <a name="setsessionid-function"></a>Funzione SessionId
Non ancora documentato.

  
### <a name="getsessionid-function"></a>Funzione GetSessionID
Non ancora documentato.

  
### <a name="setcustomsettings-function"></a>SetCustomSettings (funzione)
Imposta le impostazioni personalizzate, usate a scopi di controllo e test delle funzionalità.

Parametri  
* **customSettings**: elenco di coppie nome/valore.


  
### <a name="getcustomsettings-function"></a>GetCustomSettings (funzione)
Ottiene le impostazioni personalizzate, usate a scopi di controllo e test delle funzionalità.

  
**Restituisce:**: elenco di coppie nome/valore.
  
### <a name="settings-function"></a>~ Settings (funzione)
Non ancora documentato.
