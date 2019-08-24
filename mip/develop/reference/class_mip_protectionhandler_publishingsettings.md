---
title: Classe MIP::P rotectionHandler::P ublishingSettings
description: Documenta la classe MIP::p rotectionhandler dell'SDK Microsoft Information Protection (MIP).
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 07/16/2019
ms.openlocfilehash: 83489b41811cdaaf46b7336b21eeccb8289eb9f1
ms.sourcegitcommit: fcde8b31f8685023f002044d3a1d1903e548d207
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/21/2019
ms.locfileid: "69893124"
---
# <a name="class-mipprotectionhandlerpublishingsettings"></a>Classe MIP::P rotectionHandler::P ublishingSettings 
Impostazioni usate per creare un [ProtectionHandler](class_mip_protectionhandler.md) per proteggere il nuovo contenuto.
  
## <a name="summary"></a>Riepilogo
 Members                        | Descrizioni                                
--------------------------------|---------------------------------------------
public PublishingSettings (const std::\<shared_ptr\>ProtectionDescriptor & ProtectionDescriptor)  |  Costruttore ProtectionHandler:: Settings per la creazione di un nuovo motore.
public std:: shared_ptr\<ProtectionDescriptor\> GetProtectionDescriptor () const  | _Non ancora documentato._
public bool GetIsAuditedExtractionAllowed () const  |  Ottiene un valore che indica se le applicazioni non compatibili con MIP possono aprire contenuto protetto.
public void SetIsAuditedExtractionAllowed (bool isAuditedExtractionAllowed)  |  Imposta un valore che indica se le applicazioni non compatibili con MIP possono aprire contenuto protetto.
public bool GetIsDeprecatedAlgorithmPreferred () const  |  Ottiene un valore che indica se per la compatibilità con le versioni precedenti è preferibile l'algoritmo di crittografia (BCE) deprecato.
public void SetIsDeprecatedAlgorithmPreferred (bool isDeprecatedAlgorithmPreferred)  |  Imposta un valore che indica se è preferibile un algoritmo di crittografia (BCE) deprecato per la compatibilità con le versioni precedenti.
public void SetDelegatedUserEmail (const std:: String & delegatedUserEmail)  |  Imposta l'utente delegato.
public const std:: String & GetDelegatedUserEmail () const  |  Ottiene l'utente delegato.
  
## <a name="members"></a>Members
  
### <a name="publishingsettings-function"></a>PublishingSettings (funzione)
Costruttore ProtectionHandler:: Settings per la creazione di un nuovo motore.

Parametri:  
* **protectionDescriptor**: Dettagli sulla protezione


  
### <a name="getprotectiondescriptor-function"></a>GetProtectionDescriptor (funzione)
_Non ancora documentato._

  
### <a name="getisauditedextractionallowed-function"></a>GetIsAuditedExtractionAllowed (funzione)
Ottiene un valore che indica se le applicazioni non compatibili con MIP possono aprire contenuto protetto.

  
**Restituisce**: Se le applicazioni non compatibili con MIP possono aprire il contenuto protetto
  
### <a name="setisauditedextractionallowed-function"></a>SetIsAuditedExtractionAllowed (funzione)
Imposta un valore che indica se le applicazioni non compatibili con MIP possono aprire contenuto protetto.

Parametri:  
* **isAuditedExtractionAllowed**: Se le applicazioni non compatibili con MIP possono aprire il contenuto protetto


  
### <a name="getisdeprecatedalgorithmpreferred-function"></a>GetIsDeprecatedAlgorithmPreferred (funzione)
Ottiene un valore che indica se per la compatibilità con le versioni precedenti è preferibile l'algoritmo di crittografia (BCE) deprecato.

  
**Restituisce**: Se è preferibile l'algoritmo di crittografia deprectated
  
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

  
**Restituisce**: Utente delegato viene specificato un utente delegato quando l'utente o l'applicazione di autenticazione agisce per conto di un altro utente