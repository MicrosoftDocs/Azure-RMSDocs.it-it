---
title: Concetti - Implementazione del delegato di autenticazione (C++)
description: Questo articolo aiuterà a comprendere come implementare un delegato di autenticazione in C++.
author: BryanLa
ms.service: information-protection
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: adf82006219a24b39d44a75e22d5ef1dd282aa79
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/14/2019
ms.locfileid: "56251280"
---
# <a name="microsoft-information-protection-sdk---implementing-an-authentication-delegate-c"></a>Microsoft Information Protection SDK - Implementazione di un delegato di autenticazione (C++)

MIP SDK implementa un delegato di autenticazione per la gestione delle richieste di autenticazione e la risposta con un token. Non implementa direttamente l'acquisizione del token. Il processo di acquisizione di token è compito dello sviluppatore e viene eseguito estendendo la classe `mip::AuthDelegate`, in particolare la funzione membro `AcquireOAuth2Token`.

## <a name="building-authdelegateimpl"></a>Creazione di AuthDelegateImpl

Per estendere la classe di base `mip::AuthDelegate`, viene creata una nuova classe denominata `sample::auth::AuthDelegateImpl`. Questa classe implementa la funzionalità `AcquireOAuth2Token` e configura il costruttore per accettare i parametri di autenticazione.

### <a name="authdelegateimplh"></a>auth_delegate_impl.h

Per questo esempio, il costruttore predefinito accetta solo nome utente, password e [ID applicazione](/azure/active-directory/develop/developer-glossary#application-id-client-id) dell'applicazione. Queste informazioni verranno archiviate nelle variabili private `mUserName`, `mPassword` e `mClientId`.

È importante notare che informazioni come il provider di identità o l'URI della risorsa non sono necessarie per l'implementazione, almeno non nel costruttore `AuthDelegateImpl`. Queste informazioni vengono passate come parte di `AcquireOAuth2Token` nell'oggetto `OAuth2Challenge`. Questi dettagli verranno invece passati alla chiamata `AcquireToken` in `AcquireOAuth2Token`.

```cpp
//auth_delegate_impl.h
#include <string.h>
#include "mip/common_types.h"

namespace sample {
namespace auth {
class AuthDelegateImpl final : public mip::AuthDelegate { //extend mip::AuthDelegate base class
public:
  AuthDelegateImpl() = delete;

  //constructor accepts username, password, and clientId, all plain strings.
  AuthDelegateImpl(
    const std::string& userName,
    const std::string& password,
    const std::string& clientId
  );

  bool AcquireOAuth2Token(const mip::Identity& identity, const OAuth2Challenge& challenge, OAuth2Token& token) override;

private:
  std::string mUserName;
  std::string mPassword;
  std::string mClientId;
};

}
}
```

### <a name="authdelegateimplcpp"></a>auth_delegate_impl.cpp

`AcquireOAuth2Token` è la posizione in cui verrà effettuata la chiamata al provider OAuth2. Nell'esempio di seguito sono presenti due chiamate a `AcquireToken()`. Nella pratica, verrebbe effettuata una sola chiamata. Queste implementazioni verranno trattate nelle sezioni indicate in [Passaggi successivi](#next-steps)

```cpp
//auth_delegate_impl.cpp
#include "auth_delegate_impl.h"
#include <stdexcept>
#include "auth.h" //contains the auth class used later for token acquisition

using std::runtime_error;
using std::string;

namespace sample {
namespace auth {

AuthDelegateImpl::AuthDelegateImpl(
    const string& userName,
    const string& password,
    const string& clientId)
    : mUserName(userName),
    mPassword(password),
    mClientId(clientId) {
}

//Here we could simply add our token acquisition code to AcquireOAuth2Token
//Instead, that code is implemented in auth.h/cpp to demonstrate calling an external library
bool AuthDelegateImpl::AcquireOAuth2Token(
    const mip::Identity& /*identity*/, //This won't be used
    const OAuth2Challenge& challenge,
    const OAuth2Token& token) {

      //sample::auth::AcquireToken is the code where the token acquisition routine is implemented.
      //AcquireToken() returns a string that contains the OAuth2 token.

      //Simple example for getting hard coded token. Comment out if not used.
      string accessToken = sample::auth::AcquireToken();

      //Practical example for calling external OAuth2 library with provided authentication details.
      string accessToken = sample::auth::AcquireToken(mUserName, mPassword, mClientId, challenge.GetAuthority(), challenge.GetResource());  

      //set the passed in OAuth2Token value to the access token acquired by our provider
      token.SetAccessToken(accessToken);
      return true;
    }
}
}
```

## <a name="next-steps"></a>Passaggi successivi

Per completare l'implementazione dell'autenticazione, è necessario sviluppare il codice dietro la funzione `AcquireToken()`. Gli esempi seguenti illustrano alcuni modi per acquisire il token.

- [Esempio di acquisizione del token semplice con PowerShell](concept-authentication-acquire-token-ps.md)
- [Esempio di acquisizione del token con Python](concept-authentication-acquire-token-py.md)
