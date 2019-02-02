---
title: classe MIP
description: Documenta la classe di MIP di Microsoft Information Protection (MIP) SDK.
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: 8c2946e312caeb6d87d66004fa306ca1c68e7f92
ms.sourcegitcommit: be05adc7750e22c110b261882de0389b9dfb2726
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/02/2019
ms.locfileid: "55651878"
---
# <a name="class-mipidentity"></a>classe MIP 
Astrazione per l'identità.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public Identity()  |  Default [identità](class_mip_identity.md) costruttore utilizzato quando un indirizzo di posta elettronica utente non è noto.
pubblica Identity espliciti (const std:: String & messaggio di posta elettronica)  |  [Identità](class_mip_identity.md) costruttore utilizzato quando un indirizzo di posta elettronica utente è noto.
Public std:: String const & GetEmail() const  |  Ottenere l'indirizzo di posta elettronica.
public void SetDelegatedEmail (const std:: String & delegatedEmail)  |  Set di messaggio di posta elettronica delegata, un indirizzo di posta elettronica delegato è un per conto dell'utente per il quale vengono eseguite le opertations.
public const std::string& GetDelegatedEmail() const  |  Ottenere l'indirizzo di posta elettronica delegata, un indirizzo di posta elettronica delegato è un per conto dell'utente per il quale vengono eseguite le opertations.
  
## <a name="members"></a>Membri
  
### <a name="identity-function"></a>Funzione Identity
Default [identità](class_mip_identity.md) costruttore utilizzato quando un indirizzo di posta elettronica utente non è noto.
  
### <a name="identity-function"></a>Funzione Identity
[Identità](class_mip_identity.md) costruttore utilizzato quando un indirizzo di posta elettronica utente è noto.

Parametri:  
* **messaggio di posta elettronica**: indirizzo di posta elettronica utente.


  
### <a name="getemail-function"></a>Getemail consente (funzione)
Ottenere l'indirizzo di posta elettronica.

  
**Restituisce**: Messaggio di posta elettronica.
  
### <a name="setdelegatedemail-function"></a>SetDelegatedEmail (funzione)
Set di messaggio di posta elettronica delegata, un indirizzo di posta elettronica delegato è un per conto dell'utente per il quale vengono eseguite le opertations.

Parametri:  
* **delegatedEmail**: messaggio di posta elettronica la delega.


  
### <a name="getdelegatedemail-function"></a>GetDelegatedEmail (funzione)
Ottenere l'indirizzo di posta elettronica delegata, un indirizzo di posta elettronica delegato è un per conto dell'utente per il quale vengono eseguite le opertations.

  
**Restituisce**: Messaggio di posta elettronica delegata.