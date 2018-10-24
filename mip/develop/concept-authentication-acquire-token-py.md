---
title: Concetti - Uso di Python per acquisire un token di accesso.
description: Questo articolo aiuterà a comprendere come usare Python per acquisire un token di accesso OAuth2. Questa operazione è necessaria per l'implementazione del delegato di autenticazione.
author: BryanLa
ms.service: information-protection
ms.topic: conceptual
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: a7577bab58b701e945bea9829d7ed31b41909f88
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/28/2018
ms.locfileid: "47445785"
---
# <a name="acquire-an-access-token-python"></a>Acquisire un token di accesso (Python)

Questo esempio dimostra come chiamare uno script Python esterno per ottenere un token OAuth2. Questa operazione è necessaria per l'implementazione del delegato di autenticazione.

Questo codice non è destinato all'uso in produzione, ma può essere usato per lo sviluppo e per comprendere i concetti relativi all'autenticazione. Questo esempio è multipiattaforma.

## <a name="prerequisites"></a>Prerequisiti

Per eseguire l'esempio seguente, è necessario completare queste operazioni:

- Installare Python 2.7.
- Implementare utils.h/cpp nel progetto. 
- auth.py deve essere aggiunto al progetto ed essere disponibile nella stessa directory dei file binari in fase di compilazione.

## <a name="sampleauthacquiretoken"></a>sample::auth::AcquireToken()

Nel semplice esempio di autenticazione è stata illustrata una semplice funzione `AcquireToken()` che non accetta parametri e restituisce un valore di token hardcoded. In questo esempio, si eseguirà l'overload di AcquireToken() per accettare i parametri di autenticazione e chiamare uno script Python esterno per restituire il token.

### <a name="authh"></a>auth.h

In auth.h, la funzione `AcquireToken()` viene sottoposta a overload e la funzione in overload e i parametri aggiornati sono i seguenti:

```cpp
//auth.h
#include <string>

namespace sample {
  namespace auth {
    std::string AcquireToken();

    std::string AcquireToken(
        const std::string& userName, //A string value containing the user's UPN.
        const std::string& password, //The user's password in plaintext
        const std::string& clientId, //The AAD client ID of your application.
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

    string AcquireToken() { //ignore in this sample
    }

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
    cmd += (!clientId.empty() ? clientId : "6b069eef-9dde-4a29-b402-8ce866edc897");

    string result = sample::Execute(cmd.c_str());
    if (result.empty())
        throw runtime_error("Failed to acquire token. Ensure Python is installed correctly.");

    return result;
    }
    }
}

```

## <a name="python-script"></a>Script Python

Questo script acquisisce i token di autenticazione direttamente tramite una semplice richiesta HTTP. Lo script è incluso solo come mezzo per acquisire token di autenticazione per l'uso tramite le app di esempio e non è destinato all'uso in codice di produzione. Lo script funziona solo su tenant che supportano l'autenticazione HTTP semplice tradizionale con nome utente/password. L'autenticazione MFA o basata sui certificati avrà esito negativo.

```python
import getopt
import sys
import json
import urllib
import urllib2
import re

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
    authority = authority + 'token'

  # Build REST call
  headers = {
    'Content-Type': 'application/x-www-form-urlencoded',
    'Accept': 'application/json'
  }

  params = {
    'resource': resource,
    'client_id': clientId,
    'grant_type': 'password',
    'username': username,
    'password': password
  }

  req = urllib2.Request(
    url = authority,
    headers = headers,
    data = urllib.urlencode(params))

  f = urllib2.urlopen(req)
  response = f.read()
  f.close()
  sys.stdout.write(json.loads(response)['access_token'])

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


