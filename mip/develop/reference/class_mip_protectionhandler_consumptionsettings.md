---
title: 'Classe MIP::P rotectionHandler:: ConsumptionSettings'
description: Documenta la classe MIP::p rotectionhandler dell'SDK Microsoft Information Protection (MIP).
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 07/16/2019
ms.openlocfilehash: 259c29cb0da2635bc1aa8973b5e975e526fb81b3
ms.sourcegitcommit: fcde8b31f8685023f002044d3a1d1903e548d207
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/21/2019
ms.locfileid: "69893141"
---
# <a name="class-mipprotectionhandlerconsumptionsettings"></a>Classe MIP::P rotectionHandler:: ConsumptionSettings 
Impostazioni utilizzate per creare un [ProtectionHandler](class_mip_protectionhandler.md) per utilizzare il contenuto esistente.
  
## <a name="summary"></a>Riepilogo
 Members                        | Descrizioni                                
--------------------------------|---------------------------------------------
public ConsumptionSettings (const std::\<vector\>uint8_t & serializedPublishingLicense)  | Costruttore ProtectionHandler:: ConsumptionSettings per la creazione di un nuovo gestore.
public ConsumptionSettings (const std::\<shared_ptr\>PublishingLicenseInfo & licenseInfo)  |  Costruttore ProtectionHandler:: ConsumptionSettings per la creazione di un nuovo gestore.
public std:: shared_ptr\<PublishingLicenseInfo\> GetPublishingLicenseInfo () const  |  Ottenere la licenza di pubblicazione associata al contenuto protetto.
public bool GetIsOfflineOnly () const  |  Ottiene un valore che indica se la creazione [ProtectionHandler](class_mip_protectionhandler.md) consente operazioni http online.
public void SetIsOfflineOnly (bool isOfflineOnly)  |  Imposta un valore che indica se la creazione [ProtectionHandler](class_mip_protectionhandler.md) consente operazioni http online.
public void SetDelegatedUserEmail (const std:: String & delegatedUserEmail)  |  Imposta l'utente delegato.
public const std:: String & GetDelegatedUserEmail () const  |  Ottiene l'utente delegato.
  
## <a name="members"></a>Members
  
### <a name="consumptionsettings-function"></a>ConsumptionSettings (funzione)
Costruttore ProtectionHandler:: ConsumptionSettings per la creazione di un nuovo gestore.

Parametri:  
* **serializedPublishingLicense**: Licenza di pubblicazione serializzata dal contenuto protetto


  
### <a name="consumptionsettings-function"></a>ConsumptionSettings (funzione)
Costruttore ProtectionHandler:: ConsumptionSettings per la creazione di un nuovo gestore.

Parametri:  
* **licenseInfo**: Pubblicazione delle informazioni sulla licenza dal contenuto protetto


La fornitura di un PublishingLicenseInfo (in contrapposizione a una licenza di pubblicazione serializzata non elaborata) eliminerà la necessità dell'SDK MIP di analizzare la licenza di pubblicazione.
  
### <a name="getpublishinglicenseinfo-function"></a>GetPublishingLicenseInfo (funzione)
Ottenere la licenza di pubblicazione associata al contenuto protetto.

  
**Restituisce**: Pubblicazione delle informazioni sulle licenze
  
### <a name="getisofflineonly-function"></a>GetIsOfflineOnly (funzione)
Ottiene un valore che indica se la creazione [ProtectionHandler](class_mip_protectionhandler.md) consente operazioni http online.

  
**Restituisce**: True se le operazioni HTTP non sono consentite; in caso contrario, false se è impostato su true, la creazione di [ProtectionHandler](class_mip_protectionhandler.md) avrà esito positivo solo se il contenuto è già stato decrittografato e la relativa licenza non è scaduta. Se il contenuto memorizzato nella cache non viene trovato, verrà generata un'eccezione MIP:: NetworkError =.
  
### <a name="setisofflineonly-function"></a>SetIsOfflineOnly (funzione)
Imposta un valore che indica se la creazione [ProtectionHandler](class_mip_protectionhandler.md) consente operazioni http online.

Parametri:  
* **isOfflineOnly**: True se le operazioni HTTP non sono consentite; in caso contrario, false.


Se questa proprietà è impostata su true, la creazione di [ProtectionHandler](class_mip_protectionhandler.md) avrà esito positivo solo se il contenuto è già stato precedentemente decrittografato e la relativa licenza non scaduta viene memorizzata nella cache. Se il contenuto memorizzato nella cache non viene trovato, verrà generata un'eccezione MIP:: NetworkError.
  
### <a name="setdelegateduseremail-function"></a>SetDelegatedUserEmail (funzione)
Imposta l'utente delegato.

Parametri:  
* **delegatedUserEmail**: il messaggio di posta elettronica di delega.


Un utente delegato viene specificato quando l'utente o l'applicazione di autenticazione agisce per conto di un altro utente
  
### <a name="getdelegateduseremail-function"></a>GetDelegatedUserEmail (funzione)
Ottiene l'utente delegato.

  
**Restituisce**: Utente delegato viene specificato un utente delegato quando l'utente o l'applicazione di autenticazione agisce per conto di un altro utente