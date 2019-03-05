---
title: Concetti - Autenticazione con MIP SDK.
description: Questo articolo aiuterà a comprendere come MIP SDK implementa l'autenticazione e i requisiti per le applicazioni client per fornire la logica di acquisizione dei token di accesso OAuth2.
author: msmbaldwin
ms.service: information-protection
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.date: 09/27/2018
ms.author: mbaldwin
ms.openlocfilehash: f4d96da36eb41025df5d280c62a3831cd5afa9a1
ms.sourcegitcommit: 471b3683367d93f0673c1cf276a15f83572aa80e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/05/2019
ms.locfileid: "57330847"
---
# <a name="microsoft-information-protection-sdk---authentication-concepts"></a>Microsoft Information Protection SDK - Concetti relativi all'autenticazione

L'autenticazione in MIP SDK viene eseguita estendendo la classe `mip::AuthDelegate` per implementare il metodo di autenticazione preferito. `mip::AuthDelegate` contiene:

- `mip::AuthDelegate::OAuth2Challenge` -una classe che gestisce le informazioni dell'autorità OAuth2 e le fornisce all'applicazione client.
- `mip::AuthDelegate::OAuth2Token` -una classe che gestisce l'acquisizione del token di accesso OAuth2 (dall'applicazione client) e l'archiviazione dei token.
- `mip::AuthDelegate::AcquireOAuth2Token()` -una funzione virtuale pura, la cui implementazione determina il metodo di acquisizione del token di accesso. Dopo la chiamata dall'SDK, acquisisce il token di accesso, quindi lo restituisce alla logica di autenticazione dell'SDK.

`mip::AuthDelegate::AcquireOAuth2Token` accetta i parametri seguenti e restituisce un valore booleano che indica se l'acquisizione del token ha avuto esito positivo:

- `mip::Identity`: L'identità dell'utente o del servizio per l'autenticazione, se noto.
- `mip::AuthDelegate::OAuth2Challenge`: Accetta due parametri, **autorità** e **resource**. **Authority** è il servizio per cui verrà generato il token. **Resource** è il servizio a cui si tenta di accedere. L'SDK gestirà il passaggio di questi parametri al delegato quando viene chiamato.
- `mip::AuthDelegate::OAuth2Token`: Il risultato di token è scritto in questo oggetto. Verrà utilizzato dall'SDK quando viene caricato il motore. Al di fuori di questa implementazione dell'autenticazione non dovrebbe essere necessario ottenere o impostare questo valore in altre posizioni.

**Importante:** Le applicazioni non chiamare `AcquireOAuth2Token` direttamente. L'SDK chiamerà questa funzione quando necessario.

## <a name="consent"></a>Fornire il consenso

Azure AD richiede di dare il consenso per un'applicazione, prima che le venga concessa l'autorizzazione per accedere alle risorse/API protette con l'identità di un account. Il consenso viene registrato come conferma permanente dell'autorizzazione nel tenant dell'account, per l'account specifico (consenso dell'utente) o tutti gli account (consenso dell'amministratore). Gli scenari per il consenso sono vari, a seconda dell'API a cui si accede e delle autorizzazioni che cerca l'applicazione, nonché dell'account usato per l'accesso: 

- Gli account dallo *stesso tenant* in cui è registrata l'applicazione, se l'utente o un amministratore non ha fornito esplicitamente il pre-consenso tramite la funzionalità "Concedi autorizzazioni".
- Gli account da un *tenant diverso* se l'applicazione è registrata come multi-tenant e l'amministratore del tenant non ha già dato il consenso per tutti gli utenti in anticipo.

La classe enum `mip::Consent` implementa un approccio semplice che consente agli sviluppatori di applicazioni di fornire un'esperienza di consenso personalizzata in base all'endpoint a cui si accede dall'SDK. La notifica può informare un utente dei dati che verranno raccolti e di come ottenere la rimozione dei dati o fornire qualsiasi altra informazione necessaria per legge o in base ai criteri di conformità. Quando l'utente concede il consenso, l'applicazione può continuare. 

### <a name="implementation"></a>Implementazione

Il consenso viene implementato estendendo la classe di base `mip::Consent` e implementando `GetUserConsent` per restituire uno dei valori di enumerazione `mip::Consent`. 

L'oggetto derivato da `mip::Consent` viene passato al costruttore `mip::FileProfile::Settings` o `mip::ProtectionProfile::Settings`.

Quando un utente esegue un'operazione che richiede il consenso, l'SDK chiama il metodo `GetUserConsent` passando l'URL di destinazione come parametro. Questo è il metodo in cui si implementerebbe la visualizzazione delle informazioni necessarie per l'utente, consentendogli di decidere se acconsentire o meno all'uso del servizio. 

### <a name="consent-options"></a>Opzioni per il consenso

- **AcceptAlways**: Fornire il consenso e ricordare la decisione.
- **Accettare**: Una volta il consenso.
- **Rifiutare**: Non fornire il consenso.

Quando l'SDK richiede il consenso dell'utente con questo metodo, l'applicazione client deve presentare all'utente l'URL. Le applicazioni client devono offrire un modo per ottenere il consenso dell'utente e restituire l'enumerazione di consenso appropriata che corrisponde alla decisione dell'utente.

### <a name="sample-implementation"></a>Implementazione di esempio

#### <a name="consentdelegateimplh"></a>consent_delegate_impl.h

```cpp
class ConsentDelegateImpl final : public mip::ConsentDelegate {
public:
  ConsentDelegateImpl() = default;
  
  virtual mip::Consent GetUserConsent(const std::string& url) override;

};
```

#### <a name="consentdelegateimplcpp"></a>consent_delegate_impl.cpp

Quando l'SDK richiede il consenso, il metodo `GetUserConsent` viene chiamato *dall'SDK* e l'URL viene passato come parametro. L'esempio seguente informa l'utente che l'SDK si connetterà all'URL specificato, quindi restituisce `Consent::AcceptAlways`. Non si tratta di un esempio ottimale, perché all'utente non viene presentata effettivamente una scelta.

```cpp
Consent ConsentDelegateImpl::GetUserConsent(const string& url) {
  //Print the consent URL, ask user to choose
  std::cout << "SDK will connect to: " << url << std::endl;

  std::cout << "1) Accept Always" << std::endl;
  std::cout << "2) Accept" << std::endl;
  std::cout << "3) Reject" << std::endl;
  std::cout << "Select an option: ";
  char input;
  std::cin >> input;

  switch (input)
  {
  case '1':
    return Consent::AcceptAlways;
    break;
  case '2':
    return Consent::Accept;
    break;
  case '3':
    return Consent::Reject;
    break;
  default:
    return Consent::Reject;
  }  
}
```

## <a name="next-steps"></a>Passaggi successivi

Per semplicità, gli esempi dimostrativi del delegato implementeranno l'acquisizione del token tramite la chiamata di uno script esterno. Questo script può essere sostituito da qualsiasi altro tipo di script, una libreria OAuth2 open source o una libreria OAuth2 personalizzata.

- [Acquisire un token di accesso con PowerShell](concept-authentication-acquire-token-ps.md)
- [Acquisire un token di accesso con Python](concept-authentication-acquire-token-py.md)
