---
title: Come registrare l'app con Azure AD - AIP
description: Descrive i concetti fondamentali dell'autenticazione utente per l'app con abilitazione per RMS.
keywords: ''
author: lleonard-msft
ms.author: alleonar
manager: mbaldwin
ms.date: 03/13/2017
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 200D9B23-F35D-4165-9AC4-C482A5CE1D28
audience: developer
ms.reviewer: kartikk
ms.suite: ems
ms.openlocfilehash: cb9e5ef5cd60fff43174071938525b7544e5eb9e
ms.sourcegitcommit: 44ff610dec678604c449d42cc0b0863ca8224009
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/31/2018
ms.locfileid: "39369599"
---
# <a name="how-to-register-and-rms-enable-your-app-with-azure-ad"></a>Come registrare l'app e abilitarla per RMS con Azure AD

Questo argomento illustra i concetti fondamentali relativi alla registrazione e all'abilitazione per RMS dell'app tramite il portale di Azure e all'autenticazione utente con Azure Active Directory Authentication Library (ADAL).

## <a name="what-is-user-authentication"></a>Autenticazione utente
L'autenticazione utente è un passaggio essenziale per stabilire la comunicazione tra l'app del dispositivo e l'infrastruttura di RMS. Questo processo di autenticazione usa il protocollo OAuth 2.0 standard che richiede alcune informazioni fondamentali sull'utente corrente e sulla sua richiesta di autenticazione.

## <a name="registration-via-azure-portal"></a>Registrazione tramite il portale di Azure
Per iniziare, configurare la registrazione dell'app tramite il portale di Azure seguendo le istruzioni riportate in [Configurare Azure RMS per l'autenticazione ADAL](adal-auth.md). Assicurarsi di copiare e salvare i valori di **ID client** e **URI di reindirizzamento** da questo processo per usarli in seguito.

## <a name="complete-your-information-protection-integration-agreement-ipia"></a>Sottoscrivere il contratto per l'integrazione di Information Protection (IPIA)
Prima di distribuire l'applicazione è necessario sottoscrivere un contratto per l'integrazione di Information Protection (IPIA, Information Protection Integration Agreement) con il team di Microsoft Information Protection. Per tutti i dettagli, vedere la prima sezione dell'argomento [Distribuire in ambiente di produzione](deploying-your-application.md).

## <a name="implement-user-authentication-for-your-app"></a>Implementare l'autenticazione utente per l'app
Ogni API RMS dispone di un callback che è necessario implementare per abilitare l'autenticazione dell'utente. RMS SDK 4.2 userà l'implementazione del callback quando non si fornisce un token di accesso, quando il token di accesso deve essere aggiornato o quando è scaduto.

- Android: interfacce [AuthenticationRequestCallback](https://msdn.microsoft.com/library/dn758255.aspx) e [AuthenticationCompletionCallback](https://msdn.microsoft.com/library/dn758250.aspx).
- iOS/OS X: protocollo [MSAuthenticationCallback](https://msdn.microsoft.com/library/dn758312.aspx).
-  Windows Phone/Windows RT: interfaccia [IAuthenticationCallback](https://msdn.microsoft.com/library/microsoft.rightsmanagement.iauthenticationcallback.aspx).
- Linux: interfaccia [IAuthenticationCallback](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1IAuthenticationCallback.html).

### <a name="what-library-to-use-for-authentication"></a>Libreria da usare per l'autenticazione
Per implementare il callback di autenticazione, è necessario scaricare una libreria appropriata e configurare l'ambiente di sviluppo per poterla usare. Per queste piattaforme sono disponibili le librerie ADAL su GitHub.

Ciascuna delle risorse seguenti fornisce informazioni per configurare l'ambiente e usare la libreria.

-   [Microsoft Azure Active Directory Authentication Library (ADAL) per iOS](https://github.com/MSOpenTech/azure-activedirectory-library-for-ios/)
-   [Microsoft Azure Active Directory Authentication Library (ADAL) per MAC](https://github.com/MSOpenTech/azure-activedirectory-library-for-ios/)
-   [Microsoft Azure Active Directory Authentication Library (ADAL) per Android](https://github.com/MSOpenTech/azure-activedirectory-library-for-android)
-   [Microsoft Azure Active Directory Authentication Library (ADAL) per dotnet](https://github.com/AzureAD/azure-activedirectory-library-for-dotnet)
-   Per l'SDK di Linux, la libreria ADAL viene dispone dell'origine SDK, disponibile tramite [Github](https://github.com/AzureAD/rms-sdk-for-cpp).

>[!NOTE]  
> È consigliabile usare una delle librerie ADAL, anche se possono essere usate altre librerie di autenticazione.

### <a name="authentication-parameters"></a>Parametri di autenticazione

ADAL richiede alcune informazioni per autenticare un utente ad Azure RMS (o AD RMS). Questi sono i parametri standard di OAuth 2.0 generalmente necessari per qualsiasi app di Azure AD. Le linee guida correnti per l'uso di ADAL sono disponibili nel file README dei repository Github corrispondenti, indicato in precedenza.

- **Autorità** : URL per l'endpoint di autenticazione, in genere AAD o ADFS.
- **Risorsa**: URL/URI dell'applicazione di servizio a cui si sta tentando di accedere, in genere Azure RMS o AD RMS.
- **Id utente**: nome UPN, in genere indirizzo email dell'utente che desidera accedere all'app. Questo parametro può essere vuoto se l'utente non è ancora noto e viene inoltre usato per la memorizzazione nella cache del token dell'utente o la richiesta di un token dalla cache. Viene inoltre generalmente usato come *suggerimento* per le richieste all'utente.
- **Id client**: ID dell'applicazione client. Deve essere un ID applicazione di Azure AD.
Viene ricavato dal passaggio di registrazione precedente tramite il portale di Azure.
- **Uri di reindirizzamento**: fornisce la libreria di autenticazione con una destinazione URI per il codice di autenticazione. Per iOS e Android sono necessari formati specifici, descritti nei file README dei repository GitHub corrispondenti di ADAL. Questo valore viene ricavato dal passaggio di registrazione precedente tramite il portale di Azure.

>[!NOTE]
> Il parametro **Ambito** non è attualmente usato, ma potrebbe esserlo ed è pertanto riservato per un uso futuro.

    Android: `msauth://packagename/Base64UrlencodedSignature`

    iOS: `<app-scheme>://<bundle-id>`

>[!NOTE] 
> Se l'app non è conforme a queste linee guida, è probabile che i flussi di lavoro di Azure RMS e Azure AD non vadano a buon fine e non siano supportati da Microsoft.com. Inoltre, il Rights Management License Agreement (RMLA) potrebbe essere violato se viene usato un Id Client non valido in un'app di produzione.

### <a name="what-should-an-authentication-callback-implementation-look-like"></a>Aspetto di un'implementazione del callback di autenticazione
**Esempi di codice di autenticazione**: questo SDK contiene un codice di esempio che illustra l'uso di callback di autenticazione. Per praticità, questi esempi di codice sono rappresentati in questo caso, nonché in ognuno dei seguenti argomenti collegati.

**Autenticazione utente Android**: per altre informazioni, vedere [Esempi di codice Android](android-code.md), **passaggio 2** del primo scenario, "uso di un file protetto RMS".


    class MsipcAuthenticationCallback implements AuthenticationRequestCallback
    {
    ...

    @Override
    public void getToken(Map<String, String> authenticationParametersMap,
                         final AuthenticationCompletionCallback authenticationCompletionCallbackToMsipc)
    {
        String authority = authenticationParametersMap.get("oauth2.authority");
        String resource = authenticationParametersMap.get("oauth2.resource");
        String userId = authenticationParametersMap.get("userId");
        mClientId = “12345678-ABCD-ABCD-ABCD-ABCDEFGHIJ”; // get your registered Azure AD application ID here
        mRedirectUri = “urn:ietf:wg:oauth:2.0:oob”;
        final String userHint = (userId == null)? "" : userId;
        AuthenticationContext authenticationContext = App.getInstance().getAuthenticationContext();
        if (authenticationContext == null || !authenticationContext.getAuthority().equalsIgnoreCase(authority))
        {
            try
            {
                authenticationContext = new AuthenticationContext(App.getInstance().getApplicationContext(), authority, …);
                App.getInstance().setAuthenticationContext(authenticationContext);
            }
            catch (NoSuchAlgorithmException e)
            {
                …
                authenticationCompletionCallbackToMsipc.onFailure();
            }
            catch (NoSuchPaddingException e)
            {
                …
                authenticationCompletionCallbackToMsipc.onFailure();
            }
       }
        App.getInstance().getAuthenticationContext().acquireToken(mParentActivity, resource, mClientId, mRedirectURI, userId, mPromptBehavior,
                       "&USERNAME=" + userHint, new AuthenticationCallback<AuthenticationResult>()
                        {
                            @Override
                            public void onError(Exception exc)
                            {
                                …
                                if (exc instanceof AuthenticationCancelError)
                                {
                                     …
                                    authenticationCompletionCallbackToMsipc.onCancel();
                                }
                                else
                                {
                                     …
                                    authenticationCompletionCallbackToMsipc.onFailure();
                                }
                            }

                            @Override
                            public void onSuccess(AuthenticationResult result)
                            {
                                …
                                if (result == null || result.getAccessToken() == null
                                        || result.getAccessToken().isEmpty())
                                {
                                     …
                                }
                                else
                                {
                                    // request is successful
                                    …
                                    authenticationCompletionCallbackToMsipc.onSuccess(result.getAccessToken());
                                }
                            }
                        });
                         }


**Autenticazione utente iOS/OS**: per altre informazioni, vedere [Esempi di codice iOS/OS X](ios-os-x-code-examples.md) e il *passaggio 2 del primo scenario, "Uso di un file protetto RMS".*


    // AuthenticationCallback holds the necessary information to retrieve an access token.
    @interface MsipcAuthenticationCallback : NSObject<MSAuthenticationCallback>

    @end

    @implementation MsipcAuthenticationCallback

    - (void)accessTokenWithAuthenticationParameters:
         (MSAuthenticationParameters *)authenticationParameters
                                completionBlock:
         (void(^)(NSString *accessToken, NSError *error))completionBlock
    {
    ADAuthenticationError *error;
    ADAuthenticationContext* context = [ADAuthenticationContext authenticationContextWithAuthority:authenticationParameters.authority error:&error];

    NSString *appClientId = @”12345678-ABCD-ABCD-ABCD-ABCDEFGHIJ”;

    // get your registered Azure AD application ID here

    NSURL *redirectURI = [NSURL URLWithString:@”ms-sample://com.microsoft.sampleapp”];

    // get your <app-scheme>://<bundle-id> here
    // Retrieve token using ADAL
    [context acquireTokenWithResource:authenticationParameters.resource
                             clientId:appClientId
                          redirectUri:redirectURI
                               userId:authenticationParameters.userId
                      completionBlock:^(ADAuthenticationResult *result)
                      {
                          if (result.status != AD_SUCCEEDED)
                          {
                              NSLog(@"Auth Failed");
                              completionBlock(nil, result.error);
                          }
                          else
                          {
                              completionBlock(result.accessToken, result.error);
                          }
                      }

        ];
    }



**Autenticazione utente Linux**: per altre informazioni, vedere [Esempi di codice Linux](linux-c-code-examples.md).



    // Class Header
    class AuthCallback : public IAuthenticationCallback {
    private:

      std::shared_ptr<rmsauth::FileCache> FileCachePtr;
      std::string clientId_;
      std::string redirectUrl_;

      public:

      AuthCallback(const std::string& clientId,
               const std::string& redirectUrl);
      virtual std::string GetToken(shared_ptr<AuthenticationParameters>& ap) override;
    };

    class ConsentCallback : public IConsentCallback {
      public:

      virtual ConsentList Consents(ConsentList& consents) override;
    };

    // Class Implementation
    AuthCallback::AuthCallback(const string& clientId, const string& redirectUrl)
    : clientId_(clientId), redirectUrl_(redirectUrl) {
      FileCachePtr = std::make_shared<FileCache>();
    }

    string AuthCallback::GetToken(shared_ptr<AuthenticationParameters>& ap)
    {
      string redirect =
      ap->Scope().empty() ? redirectUrl_ : ap->Scope();

      try
      {
        if (redirect.empty()) {
        throw rmscore::exceptions::RMSInvalidArgumentException(
              "redirect Url is empty");
      }

      if (clientId_.empty()) {
      throw rmscore::exceptions::RMSInvalidArgumentException("client Id is empty");
      }

      AuthenticationContext authContext(
        ap->Authority(), AuthorityValidationType::False, FileCachePtr);

      auto result = authContext.acquireToken(ap->Resource(),
                                           clientId_, redirect,
                                           PromptBehavior::Auto,
                                           ap->UserId());
      return result->accessToken();
      }

      catch (const rmsauth::Exception& ex)
      {
        // out logs
        throw;
      }
    }
