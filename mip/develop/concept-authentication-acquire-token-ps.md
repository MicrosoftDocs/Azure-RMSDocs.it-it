---
title: Concetti - Uso di PowerShell per acquisire un token di accesso.
description: Questo articolo aiuterà a comprendere come usare PowerShell per acquisire un token di accesso OAuth2. Questa operazione è necessaria per l'implementazione del delegato di autenticazione.
author: msmbaldwin
ms.service: information-protection
ms.topic: conceptual
ms.date: 02/04/2019
ms.author: mbaldwin
ms.custom: has-adal-ref
ms.openlocfilehash: c66199f7ae22f6b4dca4406e847f41b56317beae
ms.sourcegitcommit: 298843953f9792c5879e199fd1695abf3d25aa70
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/08/2020
ms.locfileid: "82971660"
---
# <a name="acquire-an-access-token-powershell"></a>Acquisire un token di accesso (PowerShell)

Nell'esempio illustrato viene illustrato come chiamare uno script di PowerShell esterno per ottenere un token OAuth2. Per l'implementazione del delegato di autenticazione è richiesto un token di accesso OAuth2 valido.

## <a name="prerequisites"></a>Prerequisiti

- [Installazione e configurazione dell'SDK complete (MIP)](setup-configure-mip.md). Tra le altre attività, l'applicazione client verrà registrata nel tenant di Azure Active Directory (Azure AD). Azure AD fornirà un ID applicazione, noto anche come ID client, che viene usato nella logica di acquisizione dei token.

Questo codice non è destinato all'uso in produzione. Può essere utilizzato solo per lo sviluppo e la comprensione dei concetti di autenticazione.

## <a name="sampleauthacquiretoken"></a>sample::auth::AcquireToken()

### <a name="authh"></a>auth.h

Viene creata una singola funzione chiamata AcquireToken. Poiché il valore restituito sarà hardcoded per questa esercitazione, non vengono accettati parametri e viene restituita una stringa (il token).

```cpp
//auth.h
#include <string>

namespace sample {
  namespace auth {
    std::string AcquireToken();
  }
}
```

### <a name="authcpp"></a>auth.cpp

Il file di origine restituisce un valore di token che verrà hardcoded in un passaggio successivo.

```cpp
//auth.cpp
#include <string>
#include "auth.h"

namespace sample {
  namespace auth {
    string AcquireToken() {
      std::string mToken = "your token here";
      return mToken;
    }
  }
}
```

## <a name="mint-a-token"></a>Creare un token

Infine, creare un token da inserire nella variabile mToken. L'esempio seguente illustra uno script di PowerShell che può essere usato per ottenere rapidamente il token OAuth2 tramite ADAL e PowerShell in Windows. Questo token viene concesso solo per l'endpoint del Centro sicurezza e conformità di Office 365. Di conseguenza, le azioni di protezione avranno esito negativo se l'URL della risorsa non viene aggiornato.

### <a name="install-adalps-from-ps-gallery"></a>Installare [ADAL.PS](https://www.powershellgallery.com/packages/ADAL.PS/3.19.4.2) da PowerShell Gallery

È possibile ignorare questo passaggio se è stato completato in precedenza in [installazione e configurazione dell'SDK (MIP)](setup-configure-mip.md).

```PowerShell
Install-Module -Name ADAL.PS
```

### <a name="use-get-adaltoken-to-obtain-the-access-token"></a>Usare Get-ADALToken per ottenere il token di accesso

```PowerShell
#Install the ADAL.PS package if it's not installed.
if(!(Get-Package adal.ps)) { Install-Package -Name adal.ps }

$authority = "https://login.windows.net/common/oauth2/authorize"
#this is the security and compliance center endpoint
$resourceUrl = "https://syncservice.o365syncservice.com/"
#replace <application-id> and <redirect-uri>, with the Redirect URI and Application ID from your Azure AD application registration.
$clientId = "<application-id>"
$redirectUri = "<redirect-uri>"

$response = Get-ADALToken -Resource $resourceUrl -ClientId $clientId -RedirectUri $redirectUri -Authority $authority -PromptBehavior:Always
$response.AccessToken | clip
```

Copiare il token dagli Appunti in auth.cpp come valore per `string mToken`, sostituendo "your token here" nel codice riportato in precedenza. Potrebbe essere necessario eseguire di nuovo lo script, a seconda del tempo richiesto per i passaggi seguenti.
