---
title: classe MIP
description: Documenta la classe di MIP di Microsoft Information Protection (MIP) SDK.
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: 75d11fae7d79cadc4dd8909be371cbde2e87f289
ms.sourcegitcommit: 682dc48cbbcbee93b26ab3872231b3fa54d3f6eb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "60173542"
---
# <a name="class-mipidentity"></a>classe MIP 
Astrazione per l'identità.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public Identity()  |  Default [identità](class_mip_identity.md) costruttore utilizzato quando un indirizzo di posta elettronica utente non è noto.
Identità pubblica (const Identity & altro)  |  [Identità](class_mip_identity.md) costruttore di copia.
pubblica Identity espliciti (const std:: String & messaggio di posta elettronica)  |  [Identità](class_mip_identity.md) costruttore utilizzato quando un indirizzo di posta elettronica utente è noto.
Public std:: String const & GetEmail() const  |  Ottenere l'indirizzo di posta elettronica.
public void SetDelegatedEmail (const std:: String & delegatedEmail)  |  Set di messaggio di posta elettronica delegata, un indirizzo di posta elettronica delegato è un per conto dell'utente per il quale vengono eseguite le opertations.
public const std::string& GetDelegatedEmail() const  |  Ottenere l'indirizzo di posta elettronica delegata, un indirizzo di posta elettronica delegato è un per conto dell'utente per il quale vengono eseguite le opertations.
  
## <a name="members"></a>Membri
  
### <a name="identity-function"></a>Funzione Identity
Default [identità](class_mip_identity.md) costruttore utilizzato quando un indirizzo di posta elettronica utente non è noto.
  
### <a name="identity-function"></a>Funzione Identity
[Identità](class_mip_identity.md) costruttore di copia.

Parametri:  
* **[Identity](class_mip_identity.md)**: usato per creare la copia.


  
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