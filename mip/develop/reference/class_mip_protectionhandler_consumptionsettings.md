---
title: 'Classe MIP::P rotectionHandler:: ConsumptionSettings'
description: Documenta la classe MIP::p rotectionhandler dell'SDK Microsoft Information Protection (MIP).
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 02/14/2020
ms.openlocfilehash: 0f505d919f36819ce77285c77d6eebf7156d481c
ms.sourcegitcommit: 2d3c638fb576f3f074330a33d077db0cf0e7d4e7
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/20/2020
ms.locfileid: "77486784"
---
# <a name="class-mipprotectionhandlerconsumptionsettings"></a>Classe MIP::P rotectionHandler:: ConsumptionSettings 
Impostazioni utilizzate per creare un ProtectionHandler per utilizzare il contenuto esistente.
  
## <a name="summary"></a>Riepilogo
 Members                        | Descrizioni                                
--------------------------------|---------------------------------------------
public ConsumptionSettings (const std:: Vector\<uint8_t\>& serializedPublishingLicense)  |  Costruttore ProtectionHandler:: ConsumptionSettings per la creazione di un nuovo gestore.
public ConsumptionSettings (const std:: Vector\<uint8_t\>& serializedPreLicense, const std:: Vector\<uint8_t\>& serializedPublishingLicense)  |  Costruttore ProtectionHandler:: ConsumptionSettings per la creazione di un nuovo gestore.
public ConsumptionSettings (const std:: shared_ptr\<PublishingLicenseInfo\>& licenseInfo)  |  Costruttore ProtectionHandler:: ConsumptionSettings per la creazione di un nuovo gestore.
public std:: shared_ptr\<PublishingLicenseInfo\> GetPublishingLicenseInfo () const  |  Ottenere la licenza di pubblicazione associata al contenuto protetto.
public bool GetIsOfflineOnly () const  |  Ottiene un valore che indica se la creazione ProtectionHandler consente operazioni HTTP online.
public void SetIsOfflineOnly (bool isOfflineOnly)  |  Imposta un valore che indica se la creazione ProtectionHandler consente operazioni HTTP online.
public void SetDelegatedUserEmail (const std:: String & delegatedUserEmail)  |  Imposta l'utente delegato.
public const std:: String & GetDelegatedUserEmail () const  |  Ottiene l'utente delegato.
  
## <a name="members"></a>Members
  
### <a name="consumptionsettings-function"></a>ConsumptionSettings (funzione)
Costruttore ProtectionHandler:: ConsumptionSettings per la creazione di un nuovo gestore.

Parametri:  
* **serializedPublishingLicense**: licenza di pubblicazione serializzata dal contenuto protetto


  
### <a name="consumptionsettings-function"></a>ConsumptionSettings (funzione)
Costruttore ProtectionHandler:: ConsumptionSettings per la creazione di un nuovo gestore.

Parametri:  
* **serializedPreLicense**: pre-licenza serializzata da collegata al contenuto. 


* **serializedPublishingLicense**: licenza di pubblicazione serializzata dal contenuto protetto


  
### <a name="consumptionsettings-function"></a>ConsumptionSettings (funzione)
Costruttore ProtectionHandler:: ConsumptionSettings per la creazione di un nuovo gestore.

Parametri:  
* **licenseInfo**: pubblicazione delle informazioni sulla licenza dal contenuto protetto


La fornitura di un PublishingLicenseInfo (in contrapposizione a una licenza di pubblicazione serializzata non elaborata) eliminerà la necessità dell'SDK MIP di analizzare la licenza di pubblicazione.
  
### <a name="getpublishinglicenseinfo-function"></a>GetPublishingLicenseInfo (funzione)
Ottenere la licenza di pubblicazione associata al contenuto protetto.

  
**Restituzione**: pubblicazione delle informazioni sulla licenza
  
### <a name="getisofflineonly-function"></a>GetIsOfflineOnly (funzione)
Ottiene un valore che indica se la creazione ProtectionHandler consente operazioni HTTP online.

  
**Restituisce**: true se le operazioni HTTP non sono consentite; in caso contrario, false se è impostato su true, la creazione di ProtectionHandler avrà esito positivo solo se il contenuto è già stato precedentemente decrittografato e la relativa licenza non scaduta viene memorizzata nella cache. Se il contenuto memorizzato nella cache non viene trovato, verrà generata un'eccezione MIP:: NetworkError.
  
### <a name="setisofflineonly-function"></a>SetIsOfflineOnly (funzione)
Imposta un valore che indica se la creazione ProtectionHandler consente operazioni HTTP online.

Parametri:  
* **isOfflineOnly**: true se non sono consentite operazioni HTTP; in caso contrario, false


Se questa proprietà è impostata su true, la creazione di ProtectionHandler avrà esito positivo solo se il contenuto è già stato precedentemente decrittografato e la relativa licenza non scaduta viene memorizzata nella cache. Se il contenuto memorizzato nella cache non viene trovato, verrà generata un'eccezione MIP:: NetworkError.
  
### <a name="setdelegateduseremail-function"></a>SetDelegatedUserEmail (funzione)
Imposta l'utente delegato.

Parametri:  
* **delegatedUserEmail**: il messaggio di posta elettronica di delega.


Un utente delegato viene specificato quando l'utente o l'applicazione di autenticazione agisce per conto di un altro utente
  
### <a name="getdelegateduseremail-function"></a>GetDelegatedUserEmail (funzione)
Ottiene l'utente delegato.

  
**Returns**: utente delegato specificato quando l'utente o l'applicazione di autenticazione agisce per conto di un altro utente