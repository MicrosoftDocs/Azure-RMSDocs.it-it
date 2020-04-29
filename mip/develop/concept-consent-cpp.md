---
title: 'Concetti: consenso in MIP SDK.'
description: Questo articolo consente di comprendere in che modo l'SDK MIP implementa i flussi di consenso per consentire agli utenti di accettare la connessione al servizio RMS.
author: msmbaldwin
ms.service: information-protection
ms.topic: conceptual
ms.date: 07/30/2019
ms.author: mbaldwin
ms.openlocfilehash: 7025e042d0ded7164b26efbe9b453b4546c5ca05
ms.sourcegitcommit: f54920bf017902616589aca30baf6b64216b6913
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/22/2020
ms.locfileid: "81766542"
---
# <a name="microsoft-information-protection-sdk---consent"></a>Microsoft Information Protection SDK-consenso

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

A scopo di test e sviluppo, è `ConsentDelegate` possibile implementare un semplice aspetto simile al seguente:

```cpp
Consent ConsentDelegateImpl::GetUserConsent(const string& url) {
  return Consent::AcceptAlways;
}
```

Tuttavia, nel codice di produzione è possibile che l'utente debba presentare una scelta per il consenso, a seconda dei requisiti e delle normative regionali o aziendali. 