---
title: Concetti-concetti di base in MIP SDK-supporto proxy
description: Questo articolo consente di comprendere il supporto del proxy in MIP SDK.
author: tommoser
ms.service: information-protection
ms.topic: conceptual
ms.date: 07/29/2020
ms.author: tommos
ms.openlocfilehash: 54d675b44088550a07c549ff6c10621fa351fdf1
ms.sourcegitcommit: edd0614ef6f687ff2745f56e4171cd72e03edc9c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/30/2020
ms.locfileid: "87440651"
---
# <a name="microsoft-information-protection-sdk---proxy-support"></a>Microsoft Information Protection SDK-supporto proxy

## <a name="proxies-and-the-mip-sdk"></a>Proxy e l'SDK MIP

Attualmente nell'SDK MIP, i proxy non trasparenti sono supportati solo in Windows.

* Il **proxy trasparente** si riferisce a qualsiasi tipo di proxy che non richiede una configurazione lato client, incluse le impostazioni esplicite o individuate automaticamente.
* Il **proxy autenticato** fa riferimento a qualsiasi tipo di proxy che richiede l'autenticazione del chiamante.
* Il **rilevamento automatico del proxy** si riferisce a proxy o impostazioni trovati tramite Web Proxy Auto-Discovery (WPAD).
* Il **proxy esplicito** fa riferimento a un proxy fornito direttamente al sistema operativo o all'applicazione.
  
| Piattaforma        | Proxy trasparente | Proxy autenticati | Individuazione automatica proxy | Proxy esplicito |
| --------------- | ----------------- | --------------------- | -------------------- | -------------- |
| **Windows**     | Supportato         | Non supportato         | Supportato            | Funzionalità supportata      |
| **Linux (tutti)** | Supportato         | Non supportato         | Non Supportato        | Non Supportato  |
| **MacOS**       | Supportato         | Non supportato         | Non Supportato        | Non Supportato  |
| **Android**     | Supportato         | Non supportato         | Non Supportato        | Non Supportato  |
| **iOS**         | Supportato         | Non supportato         | Non Supportato        | Non Supportato  |

## <a name="proxies-on-windows"></a>Proxy in Windows

Le applicazioni PIP SDK in esecuzione in Windows utilizzeranno WinHTTP per accedere alla rete. L'impostazione di configurazione WinHTTP è indipendente dalle impostazioni del proxy di esplorazione Internet di Windows Internet (WinINet) e può solo individuare un server proxy usando i seguenti metodi di individuazione:

* Metodi di individuazione automatica:
  * Proxy trasparente
  * Protocollo WPAD (Web Proxy Auto-Discovery)
* Configurazione manuale tramite proxy statico:
  * Configurazione di WinHTTP con il comando netsh

Per ulteriori informazioni sulla configurazione di WinHTTP, consultare la [documentazione di WinHTTP](/windows/win32/winhttp/winhttp-start-page).

## <a name="proxies-on-other-platforms"></a>Proxy su altre piattaforme

MIP SDK non supporta alcun proxy completamente trasparente di qualsiasi tipo nelle piattaforme non Windows. Se questa funzionalità è obbligatoria, vedere le sezioni relative al delegato HTTP personalizzato e alla soluzione alternativa per altri dettagli.

## <a name="custom-http-delegate"></a>Delegato HTTP personalizzato

Microsoft Information Protection SDK supporta l'implementazione di un delegato HTTP personalizzato che può eseguire l'override dello stack HTTP predefinito dell'SDK. Se non sono presenti funzionalità o è necessaria un'implementazione HTTP specifica, questo delegato può essere implementato aggiungendo una nuova classe che eredita [`mip::HttpDelegate`](./reference/class_mip_httpdelegate.md) .

Questa `mip::HttpDelegate` classe derivata da viene impostata tramite `mip::FileProfile::Settings` :

```cpp
std::shared_ptr<MyHttpDelegate> httpDelegate = std::make_shared<MyHttpDelegate>();
            
FileProfile::Settings profileSettings(mMipContext,
    mip::CacheStorageType::OnDisk,
    std::make_shared<sample::consent::ConsentDelegateImpl>(),
    std::make_shared<FileProfileObserver>());

profileSettings.SetHttpDelegate(httpDelegate);
```

## <a name="other-workarounds"></a>Altre soluzioni alternative

Se un delegato HTTP personalizzato non è un'opzione, sarà necessario ignorare il proxy e consentire la connettività di rete diretta per gli endpoint di etichettatura e protezione MIP, oltre a Azure Active Directory. Se si desidera la [registrazione di controllo](/azure/information-protection/reports-aip) , è necessario anche l'endpoint di registrazione di controllo.

| Endpoint           | nomehost                                                                                                                                                                |
| ------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Servizio di protezione | https://api.aadrm.com                                                                                                                                                   |
| Criteri             | https:// \* . Protection.Outlook.com                                                                                                                                       |
| Registrazione di controllo      | https:// \* . Events.Data.Microsoft.com, https:// \* . aria.Microsoft.com (solo iOS)                                                                                          |
| Authentication     | [Consultare Azure AD documentazione](/azure/active-directory/develop/authentication-national-cloud#azure-ad-authentication-endpoints) |