---
title: Classe MIP::P rotectionHandler::P ublishingSettings
description: Documenta la classe MIP::p rotectionhandler dell'SDK Microsoft Information Protection (MIP).
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 02/14/2020
ms.openlocfilehash: e61eb300cbc787ecbb7fd14ec5dcb060d4f47d0a
ms.sourcegitcommit: 2d3c638fb576f3f074330a33d077db0cf0e7d4e7
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/20/2020
ms.locfileid: "77490762"
---
# <a name="class-mipprotectionhandlerpublishingsettings"></a>Classe MIP::P rotectionHandler::P ublishingSettings 
Impostazioni usate per creare un ProtectionHandler per proteggere il nuovo contenuto.
  
## <a name="summary"></a>Riepilogo
 Members                        | Descrizioni                                
--------------------------------|---------------------------------------------
public PublishingSettings (const std:: shared_ptr\<ProtectionDescriptor\>& protectionDescriptor)  |  Costruttore ProtectionHandler:: Settings per la creazione di un nuovo motore.
public std:: shared_ptr\<ProtectionDescriptor\> GetProtectionDescriptor () const  | _Non ancora documentato._
public bool GetIsAuditedExtractionAllowed () const  |  Ottiene un valore che indica se le applicazioni non compatibili con MIP possono aprire contenuto protetto.
public void SetIsAuditedExtractionAllowed (bool isAuditedExtractionAllowed)  |  Imposta un valore che indica se le applicazioni non compatibili con MIP possono aprire contenuto protetto.
public bool GetIsDeprecatedAlgorithmPreferred () const  |  Ottiene un valore che indica se per la compatibilità con le versioni precedenti è preferibile l'algoritmo di crittografia (BCE) deprecato.
public void SetIsDeprecatedAlgorithmPreferred (bool isDeprecatedAlgorithmPreferred)  |  Imposta un valore che indica se è preferibile un algoritmo di crittografia (BCE) deprecato per la compatibilità con le versioni precedenti.
public void SetDelegatedUserEmail (const std:: String & delegatedUserEmail)  |  Imposta l'utente delegato.
public const std:: String & GetDelegatedUserEmail () const  |  Ottiene l'utente delegato.
public bool IsPublishingFormatJson () const  |  Ottiene un valore che indica se il valore pl restituito è in formato JSON (il formato XML è più ampiamente accettato ed è l'impostazione predefinita).
public void SetPublishingFormatJson (bool isPublishingFormatJson)  |  indica se il pl restituito è in formato JSON (il formato XML è più ampiamente accettato ed è l'impostazione predefinita).
  
## <a name="members"></a>Members
  
### <a name="publishingsettings-function"></a>PublishingSettings (funzione)
Costruttore ProtectionHandler:: Settings per la creazione di un nuovo motore.

Parametri:  
* **protectionDescriptor**: dettagli sulla protezione


  
### <a name="getprotectiondescriptor-function"></a>GetProtectionDescriptor (funzione)
_Non ancora documentato._

  
### <a name="getisauditedextractionallowed-function"></a>GetIsAuditedExtractionAllowed (funzione)
Ottiene un valore che indica se le applicazioni non compatibili con MIP possono aprire contenuto protetto.

  
**Restituisce**: se le applicazioni non compatibili con MIP possono aprire il contenuto protetto
  
### <a name="setisauditedextractionallowed-function"></a>SetIsAuditedExtractionAllowed (funzione)
Imposta un valore che indica se le applicazioni non compatibili con MIP possono aprire contenuto protetto.

Parametri:  
* **isAuditedExtractionAllowed**: se le applicazioni non compatibili con MIP possono aprire il contenuto protetto


  
### <a name="getisdeprecatedalgorithmpreferred-function"></a>GetIsDeprecatedAlgorithmPreferred (funzione)
Ottiene un valore che indica se per la compatibilità con le versioni precedenti è preferibile l'algoritmo di crittografia (BCE) deprecato.

  
**Restituisce**: se è preferibile l'algoritmo di crittografia deprectated
  
### <a name="setisdeprecatedalgorithmpreferred-function"></a>SetIsDeprecatedAlgorithmPreferred (funzione)
Imposta un valore che indica se è preferibile un algoritmo di crittografia (BCE) deprecato per la compatibilità con le versioni precedenti.

Parametri:  
* **Se**: è preferibile l'algoritmo di crittografia deprectated


  
### <a name="setdelegateduseremail-function"></a>SetDelegatedUserEmail (funzione)
Imposta l'utente delegato.

Parametri:  
* **delegatedUserEmail**: il messaggio di posta elettronica di delega.


Un utente delegato viene specificato quando l'utente o l'applicazione di autenticazione agisce per conto di un altro utente
  
### <a name="getdelegateduseremail-function"></a>GetDelegatedUserEmail (funzione)
Ottiene l'utente delegato.

  
**Returns**: utente delegato specificato quando l'utente o l'applicazione di autenticazione agisce per conto di un altro utente
  
### <a name="ispublishingformatjson-function"></a>IsPublishingFormatJson (funzione)
Ottiene un valore che indica se il valore pl restituito è in formato JSON (il formato XML è più ampiamente accettato ed è l'impostazione predefinita).

  
**Restituisce**: true se è impostato su output in formato JSON.
  
### <a name="setpublishingformatjson-function"></a>SetPublishingFormatJson (funzione)
indica se il pl restituito è in formato JSON (il formato XML è più ampiamente accettato ed è l'impostazione predefinita).

Parametri:  
* **isPublishingFormatJson**: se il formato JSON è abilitato.

