---
title: Concetti - Uso di Python per acquisire un token di accesso.
description: Questo articolo aiuterà a comprendere come usare Python per acquisire un token di accesso OAuth2. Questa operazione è necessaria per l'implementazione del delegato di autenticazione.
author: msmbaldwin
ms.service: information-protection
ms.topic: conceptual
ms.date: 07/30/2019
ms.author: mbaldwin
ms.openlocfilehash: 7cb49e161b3718a54bcdb8601cc857a47b1e9f16
ms.sourcegitcommit: 99eccfe44ca1ac0606952543f6d3d767088de425
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/31/2019
ms.locfileid: "75556249"
---
# <a name="acquire-an-access-token-python"></a>Acquisire un token di accesso (Python)

Questo esempio dimostra come chiamare uno script Python esterno per ottenere un token OAuth2. Per l'implementazione del delegato di autenticazione è richiesto un token di accesso OAuth2 valido.

## <a name="prerequisites"></a>Prerequisiti

Per eseguire l'esempio seguente:

- Installare Python 2,7 o versione successiva.
- Implementare utils.h/cpp nel progetto. 
- Auth.py deve essere aggiunto al progetto e presente nella stessa directory dei file binari in fase di compilazione.
- [Installazione e configurazione dell'SDK complete (MIP)](setup-configure-mip.md). Tra le altre attività, l'applicazione client verrà registrata nel tenant di Azure Active Directory (Azure AD). Azure AD fornirà un ID applicazione, noto anche come ID client, che viene usato nella logica di acquisizione dei token.

Questo codice non è destinato all'uso in produzione. Può essere utilizzato solo per lo sviluppo e la comprensione dei concetti di autenticazione. Questo esempio è multipiattaforma.

## <a name="sampleauthacquiretoken"></a>sample::auth::AcquireToken()

Nell'esempio di autenticazione semplice è stata illustrata una semplice funzione `AcquireToken()` che non ha accettato parametri e ha restituito un valore di token hardcoded. In questo esempio, si eseguirà l'overload di AcquireToken() per accettare i parametri di autenticazione e chiamare uno script Python esterno per restituire il token.

### <a name="authh"></a>auth.h

In auth.h, la funzione `AcquireToken()` viene sottoposta a overload e la funzione in overload e i parametri aggiornati sono i seguenti:

```cpp
//auth.h
#include <string>

namespace sample {
  namespace auth {    
    std::string AcquireToken(
        const std::string& userName, //A string value containing the user's UPN.
        const std::string& password, //The user's password in plaintext
        const std::string& clientId, //The Azure AD client ID (also known as Application ID) of your application.
        const std::string& resource, //The resource URL for which an OAuth2 token is required. Provided by challenge object.
        const std::string& authority); //The authentication authority endpoint. Provided by challenge object.
    }
}
```

I primi tre parametri verranno forniti dall'input dell'utente o saranno hardcoded nell'applicazione. Gli ultimi due parametri vengono forniti dall'SDK al delegato di autenticazione. 


### <a name="authcpp"></a>auth.cpp

In auth.cpp viene aggiunta la definizione della funzione in overload e quindi si definisce il codice necessario per chiamare lo script Python. La funzione accetta tutti i parametri specificati e li passa allo script Python. Lo script viene eseguito e restituisce il token in formato stringa.

```cpp
#include "auth.h"
#include "utils.h"

#include <fstream>
#include <functional>
#include <memory>
#include <string>

using std::string;
using std::runtime_error;

namespace sample {
    namespace auth {

    //This function implements token acquisition in the application by calling an external Python script.
    //The Python script requires username, password, clientId, resource, and authority.
    //Username, Password, and ClientId are provided by the user/developer
    //Resource and Authority are provided as part of the OAuth2Challenge object that is passed in by the SDK to the AuthDelegate.
    string AcquireToken(
        const string& userName,
        const string& password,
        const string& clientId,
        const string& resource,
        const string& authority) {

    string cmd = "python";
    if (sample::FileExists("auth.py"))
        cmd += " auth.py -u ";

    else
        throw runtime_error("Unable to find auth script.");

    cmd += userName;
    cmd += " -p ";
    cmd += password;
    cmd += " -a ";
    cmd += authority;
    cmd += " -r ";
    cmd += resource;
    cmd += " -c ";
    // Replace <application-id> with the Application ID provided during your Azure AD application registration.
    cmd += (!clientId.empty() ? clientId : "<application-id>");

    string result = sample::Execute(cmd.c_str());
    if (result.empty())
        throw runtime_error("Failed to acquire token. Ensure Python is installed correctly.");

    return result;
    }
    }
}

```

## <a name="python-script"></a>Script Python

Questo script acquisisce i token di autenticazione direttamente tramite [adal per Python](https://github.com/AzureAD/azure-activedirectory-library-for-python). Questo codice è incluso solo come mezzo per acquisire i token di autenticazione per l'uso da parte delle app di esempio e non è destinato all'uso nell'ambiente di produzione. Lo script funziona solo su tenant che supportano l'autenticazione HTTP semplice tradizionale con nome utente/password. L'autenticazione MFA o basata sui certificati avrà esito negativo.

> [!NOTE] 
> Prima di eseguire questo esempio, è necessario installare ADAL per Python eseguendo uno dei comandi seguenti:

```shell
pip install adal
pip3 install adal
```

```python
import getopt
import sys
import json
import re
from adal import AuthenticationContext

def printUsage():
  print('auth.py -u <username> -p <password> -a <authority> -r <resource> -c <clientId>')

def main(argv):
  try:
    options, args = getopt.getopt(argv, 'hu:p:a:r:c:')
  except getopt.GetoptError:
    printUsage()
    sys.exit(-1)

  username = ''
  password = ''
  authority = ''
  resource = ''

  clientId = ''
    
  for option, arg in options:
    if option == '-h':
      printUsage()
      sys.exit()
    elif option == '-u':
      username = arg
    elif option == '-p':
      password = arg
    elif option == '-a':
      authority = arg
    elif option == '-r':
      resource = arg
    elif option == '-c':
      clientId = arg

  if username == '' or password == '' or authority == '' or resource == '' or clientId == '':
    printUsage()
    sys.exit(-1)

  # Find everything after the last '/' and replace it with 'token'
  if not authority.endswith('token'):
    regex = re.compile('^(.*[\/])')
    match = regex.match(authority)
    authority = match.group()
    authority = authority + username.split('@')[1]

  auth_context = AuthenticationContext(authority)
  token = auth_context.acquire_token_with_username_password(resource, username, password, clientId)
  print(token["accessToken"])

if __name__ == '__main__':  
  main(sys.argv[1:])
```

## <a name="update-acquireoauth2token"></a>Aggiornare AcquireOAuth2Token

Infine, aggiornare la funzione `AcquireOAuth2Token` in `AuthDelegateImpl` per chiamare la funzione `AcquireToken` in overload. Gli URL delle risorse e dell'autorità vengono ottenuti leggendo `challenge.GetResource()` e `challenge.GetAuthority()`. `OAuth2Challenge` viene passato al delegato di autenticazione quando viene aggiunto il motore. Queste operazioni vengono eseguite dall'SDK e non sono richiesti ulteriori interventi da parte dello sviluppatore. 

```cpp
bool AuthDelegateImpl::AcquireOAuth2Token(
    const mip::Identity& /*identity*/,
    const OAuth2Challenge& challenge,
    OAuth2Token& token) {

    //call our AcquireToken function, passing in username, password, clientId, and getting the resource/authority from the OAuth2Challenge object
    string accessToken = sample::auth::AcquireToken(mUserName, mPassword, mClientId, challenge.GetResource(), challenge.GetAuthority());
    token.SetAccessToken(accessToken);
    return true;
}
```

Quando viene aggiunto l'`engine`, l'SDK chiamerà la funzione AcquireOAuth2Token, che passa la richiesta, esegue lo script Python, riceve un token e quindi presenta il token al servizio.


