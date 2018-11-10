---
title: Concetti - Uso di PowerShell per acquisire un token di accesso.
description: Questo articolo aiuterà a comprendere come usare PowerShell per acquisire un token di accesso OAuth2. Questa operazione è necessaria per l'implementazione del delegato di autenticazione.
author: BryanLa
ms.service: information-protection
ms.topic: conceptual
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: a5ce346d044a9a56d37777e569582087026c9ce6
ms.sourcegitcommit: fa0be701b85b1fba5e75428714bb4525dd739a93
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/07/2018
ms.locfileid: "51223883"
---
# <a name="acquire-an-access-token-powershell"></a>Acquisire un token di accesso (PowerShell)

Questo esempio dimostra come chiamare uno script di PowerShell esterno per ottenere un token OAuth2. Questa operazione è necessaria per l'implementazione del delegato di autenticazione.

Questo codice non è destinato all'uso in produzione, ma può essere usato per lo sviluppo e per comprendere i concetti relativi all'autenticazione. 

## <a name="sampleauthacquiretoken"></a>sample::auth::AcquireToken()

### <a name="authh"></a>auth.h

Viene creata una singola funzione chiamata AcquireToken. Dato che il valore restituito sarà hardcoded per questa esercitazione, non vengono accettati parametri e viene restituita semplicemente una stringa (il token).

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

Infine, creare un token da inserire nella variabile mToken. L'esempio seguente illustra uno script di PowerShell che può essere usato per ottenere rapidamente il token OAuth2 tramite ADAL e PowerShell in Windows. Questo token viene concesso solo per l'endpoint del Centro sicurezza e conformità di Office 365. Di conseguenza, le azioni di protezione avranno esito negativo se l'URL della risorsa non viene aggiornato. È consigliabile ignorare la sezione [Passaggi successivi](#next-steps) se si desidera eseguire il test sia con l'etichettatura che con la protezione a questo punto.

### <a name="install-adalpshttpswwwpowershellgallerycompackagesadalps31942-from-ps-gallery"></a>Installare [ADAL.PS](https://www.powershellgallery.com/packages/ADAL.PS/3.19.4.2) da PowerShell Gallery

```PowerShell
Install-Module -Name ADAL.PS
```

### <a name="use-get-adaltoken-to-obtain-the-access-token"></a>Usare Get-ADALToken per ottenere il token di accesso

```PowerShell
#Install the ADAL.PS package if it's not installed.
if(!(Get-Package adal.ps)) { Install-Package -Name adal.ps }

$authority = "https://login.windows.net/common/oauth2/authorize" 
#this is the security and compliance center endpoint
$resourceUrl = "https://dataservice.o365filtering.com"
#clientId and redirectUri are from the RMS Sharing Application. 
#Once custom app registration is supported, a custom id and uri will be required. 
$clientId = "0edbblll-8773-44de-b87c-b8c6276d41eb"
$redirectUri = "com.microsoft.rms-sharing-for-win://authorize"

$response = Get-ADALToken -Resource $resourceUrl -ClientId $clientId -RedirectUri $redirectUri -Authority $authority -PromptBehavior:Always
$response.AccessToken | clip
```

Copiare il token dagli Appunti in auth.cpp come valore per `string mToken`, sostituendo "your token here" nel codice riportato in precedenza. Potrebbe essere necessario eseguire di nuovo lo script, a seconda del tempo richiesto per i passaggi seguenti.


