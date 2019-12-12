---
title: Concetti - Autenticazione con MIP SDK.
description: Questo articolo aiuterà a comprendere come MIP SDK implementa l'autenticazione e i requisiti per le applicazioni client per fornire la logica di acquisizione dei token di accesso OAuth2.
author: msmbaldwin
ms.service: information-protection
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.date: 07/30/2019
ms.author: mbaldwin
ms.openlocfilehash: 55bfba6da57fa07614165f4d5fcc5fba226cfca7
ms.sourcegitcommit: 474cd033de025bab280cb7a9721ac7ffc2d60b55
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/05/2019
ms.locfileid: "69886242"
---
# <a name="microsoft-information-protection-sdk---authentication-concepts"></a>Microsoft Information Protection SDK - Concetti relativi all'autenticazione

L'autenticazione in MIP SDK viene eseguita estendendo la classe `mip::AuthDelegate` per implementare il metodo di autenticazione preferito. `mip::AuthDelegate` contiene:

- `mip::AuthDelegate::OAuth2Challenge` -una classe che gestisce le informazioni dell'autorità OAuth2 e le fornisce all'applicazione client.
- `mip::AuthDelegate::OAuth2Token` -una classe che gestisce l'acquisizione del token di accesso OAuth2 (dall'applicazione client) e l'archiviazione dei token.
- `mip::AuthDelegate::AcquireOAuth2Token()` -una funzione virtuale pura, la cui implementazione determina il metodo di acquisizione del token di accesso. Dopo la chiamata dall'SDK, acquisisce il token di accesso, quindi lo restituisce alla logica di autenticazione dell'SDK.

`mip::AuthDelegate::AcquireOAuth2Token` accetta i parametri seguenti e restituisce un valore booleano che indica se l'acquisizione del token ha avuto esito positivo:

- `mip::Identity`: l'identità dell'utente o del servizio da autenticare, se nota.
- `mip::AuthDelegate::OAuth2Challenge`: accetta quattro parametri, **Authority**, **Resource**, **Claims**e **Scopes**. **Authority** è il servizio per cui verrà generato il token. **Resource** è il servizio a cui si tenta di accedere. L'SDK gestirà il passaggio di questi parametri al delegato quando viene chiamato. Le **attestazioni** sono le attestazioni specifiche dell'etichetta richieste dal servizio di protezione. Gli **ambiti** sono gli ambiti di autorizzazione Azure ad necessari per accedere alla risorsa. 
- `mip::AuthDelegate::OAuth2Token`: Il risultato del token viene scritto in questo oggetto. Verrà utilizzato dall'SDK quando viene caricato il motore. Al di fuori di questa implementazione dell'autenticazione non dovrebbe essere necessario ottenere o impostare questo valore in altre posizioni.

**Importante:** le applicazioni non chiamano `AcquireOAuth2Token` direttamente. L'SDK chiamerà questa funzione quando necessario.

## <a name="consent"></a>Consent

Azure AD richiede di dare il consenso per un'applicazione, prima che le venga concessa l'autorizzazione per accedere alle risorse/API protette con l'identità di un account. Il consenso viene registrato come riconoscimento permanente dell'autorizzazione nel tenant dell'account, per l'account specifico (consenso dell'utente) o per tutti gli account (consenso dell'amministratore). Gli scenari per il consenso sono vari, a seconda dell'API a cui si accede e delle autorizzazioni che cerca l'applicazione, nonché dell'account usato per l'accesso: 

- Gli account dallo *stesso tenant* in cui è registrata l'applicazione, se l'utente o un amministratore non ha fornito esplicitamente il pre-consenso tramite la funzionalità "Concedi autorizzazioni".
- Gli account da un *tenant diverso* se l'applicazione è registrata come multi-tenant e l'amministratore del tenant non ha già dato il consenso per tutti gli utenti in anticipo.

La classe enum `mip::Consent` implementa un approccio semplice che consente agli sviluppatori di applicazioni di fornire un'esperienza di consenso personalizzata in base all'endpoint a cui si accede dall'SDK. La notifica può informare un utente dei dati che verranno raccolti e di come ottenere la rimozione dei dati o fornire qualsiasi altra informazione necessaria per legge o in base ai criteri di conformità. Quando l'utente concede il consenso, l'applicazione può continuare. 

### <a name="implementation"></a>Implementazione

Il consenso viene implementato estendendo la classe di base `mip::Consent` e implementando `GetUserConsent` per restituire uno dei valori di enumerazione `mip::Consent`. 

L'oggetto derivato da `mip::Consent` viene passato al costruttore `mip::FileProfile::Settings` o `mip::ProtectionProfile::Settings`.

Quando un utente esegue un'operazione che richiede il consenso, l'SDK chiama il metodo `GetUserConsent` passando l'URL di destinazione come parametro. Questo è il metodo in cui si implementerebbe la visualizzazione delle informazioni necessarie per l'utente, consentendogli di decidere se acconsentire o meno all'uso del servizio. 

### <a name="consent-options"></a>Opzioni per il consenso

- **AcceptAlways**: fornisce il consenso e memorizza la decisione.
- **Accept**: fornisce il consenso una sola volta.
- **Reject**: non fornisce il consenso.

Quando l'SDK richiede il consenso dell'utente con questo metodo, l'applicazione client deve presentare all'utente l'URL. Le applicazioni client devono offrire un modo per ottenere il consenso dell'utente e restituire l'enumerazione di consenso appropriata che corrisponde alla decisione dell'utente.

### <a name="sample-implementation"></a>Implementazione di esempio

#### <a name="consent_delegate_implh"></a>consent_delegate_impl.h

```cpp
class ConsentDelegateImpl final : public mip::ConsentDelegate {
public:
  ConsentDelegateImpl() = default;
  
  virtual mip::Consent GetUserConsent(const std::string& url) override;

};
```

#### <a name="consent_delegate_implcpp"></a>consent_delegate_impl.cpp

Quando l'SDK richiede il consenso, il metodo `GetUserConsent` viene chiamato *dall'SDK* e l'URL viene passato come parametro. Nell'esempio seguente l'utente riceve una notifica che l'SDK si connetterà all'URL specificato e fornisce all'utente un'opzione nella riga di comando. In base alla scelta da parte dell'utente, l'utente accetta o rifiuta il consenso e viene passato all'SDK. Se l'utente rifiuta di concedere il consenso all'applicazione genererà un'eccezione e non verrà effettuata alcuna chiamata al servizio di protezione. 

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

A scopo di test e sviluppo, è possibile implementare un semplice `ConsentDelegate` simile al seguente:

```cpp
Consent ConsentDelegateImpl::GetUserConsent(const string& url) {
  return Consent::AcceptAlways;
}
```

Tuttavia, nel codice di produzione è possibile che l'utente debba presentare una scelta per il consenso, a seconda dei requisiti e delle normative regionali o aziendali. 

## <a name="next-steps"></a>Passaggi successivi

Per semplicità, gli esempi dimostrativi del delegato implementeranno l'acquisizione del token tramite la chiamata di uno script esterno. Questo script può essere sostituito da qualsiasi altro tipo di script, una libreria OAuth2 open source o una libreria OAuth2 personalizzata.

- [Acquisire un token di accesso con PowerShell](concept-authentication-acquire-token-ps.md)
- [Acquisire un token di accesso con Python](concept-authentication-acquire-token-py.md)
