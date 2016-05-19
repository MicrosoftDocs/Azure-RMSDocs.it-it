---
# required metadata

title: Procedura& #58; Aggiungere l'autenticazione all'app | Azure RMS
description: Descrive i concetti fondamentali dell'autenticazione utente per l'app con abilitazione per RMS.
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 94697eb5-1fab-4591-bd40-b5646daac8a3

# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

﻿
# Procedura: Aggiungere l'autenticazione all'app

Questo argomento descrive i concetti fondamentali dell'autenticazione utente per l'app con abilitazione per RMS.

## Autenticazione utente
L'autenticazione utente è un passaggio essenziale per stabilire la comunicazione tra l'app del dispositivo e l'infrastruttura di RMS. Il processo di autenticazione usa il protocollo OAuth 2.0 standard che richiede le seguenti di informazioni sull'utente corrente e la sua richiesta l'autenticazione; **autorità**, **risorse** e **userId**.

**Nota**: l'ambito non è attualmente usato, ma potrebbe esserlo e pertanto è riservato per uso futuro.

 

**Callback di autenticazione utente**: SDK Microsoft Rights Management 4.2 userà l'implementazione di un callback di autenticazione quando non si fornisce un token di accesso, quando il token di accesso deve essere aggiornato o quando è scaduto.

Ciascuna delle API RMS della piattaforma dispone di un callback da implementare per abilitare l'autenticazione dell'utente.

-   L'API di Android usa le interfacce [**AuthenticationRequestCallback**](/rights-management/sdk/4.2/api/android/com.microsoft.rightsmanagement#msipcthin2_authenticationrequestcallback_interface_java) e [**AuthenticationCompletionCallback**](/rights-management/sdk/4.2/api/android/authenticationcompletioncallback#msipcthin2_authenticationcompletioncallback_interface_java).
-   L'API di iOS/OS X usa il protocollo [**MSAuthenticationCallback**](/rights-management/sdk/4.2/api/iOS/iOS#msipcthin2_msauthenticationcallback_protocol_objc).
-   L'API di WinPhone usa l'interfaccia [**IAuthenticationCallback**](/rights-management/sdk/4.2/api/winrt/Microsoft.RightsManagement#msipcthin2_iauthenticationcallback).
-   L'API di Linux usa l'interfaccia [IAuthenticationCallback](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1IAuthenticationCallback.html).

## Libreria da usare per l'autenticazione

Per implementare il callback di autenticazione, è necessario scaricare una libreria appropriata e configurare l'ambiente di sviluppo per poterla usare. Per queste piattaforme sono disponibili le librerie ADAL su GitHub. Ciascuna delle risorse seguenti fornisce informazioni per configurare l'ambiente e usare la libreria.

-   [Microsoft Azure Active Directory Authentication Library (ADAL) per iOS](https://github.com/MSOpenTech/azure-activedirectory-library-for-ios/)
-   [Microsoft Azure Active Directory Authentication Library (ADAL) per MAC](https://github.com/MSOpenTech/azure-activedirectory-library-for-ios/)
-   [Microsoft Azure Active Directory Authentication Library (ADAL) per Android](https://github.com/MSOpenTech/azure-activedirectory-library-for-android)
-   [Microsoft Azure Active Directory Authentication Library (ADAL) per dotnet](https://github.com/AzureAD/azure-activedirectory-library-for-dotnet)
-   Per l'SDK di Linux, la libreria ADAL viene dispone dell'origine SDK, disponibile tramite [Github](https://github.com/AzureAD/rms-sdk-for-cpp).

**Nota**: si consiglia di usare una delle Active Directory Authentication Libraries (ADAL) di cui sopra, anche se è possibile usare altre librerie di autenticazione.

## Input per l'autenticazione con Azure Active Directory Authentication Library (ADAL)

ADAL richiede diversi parametri per autenticare un utente di Azure RMS (o AD RMS). Questi sono i parametri standard OAuth 2.0 in genere necessari di qualsiasi app di Azure AD, come con le app con abilitazione per RMS. Le linee guida correnti per l'uso di ADAL sono disponibili nel file LEGGIMI degli archivi di Github corrispondenti, elencato in precedenza.

Questi parametri e le linee guida sono necessari per i flussi di lavoro RMS:

-   **Autorità** : URL per l'endpoint di autenticazione, in genere AAD o ADFS. Questo parametro viene fornito all'app dal callback autenticazione SDK RMS.
-   **Risorsa**: URL/URI dell'applicazione di servizio a cui si sta tentando di accedere, in genere Azure RMS o AD RMS. Questo parametro viene fornito all'app dal callback autenticazione SDK RMS.
-   **Id utente**: nome UPN, in genere indirizzo email dell'utente che desidera accedere all'app. Questo parametro può essere vuoto se l'utente non è ancora noto e viene inoltre usato per la memorizzazione nella cache del token dell'utente o la richiesta di un token dalla cache. Viene inoltre usato come suggerimento per le richieste all'utente.
-   **Id client**: ID dell'applicazione client. Deve essere un ID applicazione di Azure AD. Per altre informazioni, vedere la procedura Ottenere un ID dell'applicazione Azure.
-   **Uri di reindirizzamento**: fornisce la libreria di autenticazione con una destinazione URI per il codice di autenticazione. Si noti che sono necessari formati specifici per iOS e Android e sono descritti nei file LEGGIMI degli archivi di GitHub corrispondenti della libreria ADAL.

    Android: `msauth://packagename/Base64UrlencodedSignature`

    iOS: `<app-scheme>://<bundle-id>`

**Nota**: se l'applicazione non si attiene a queste linee guida, è probabile che i flussi di lavoro di Azure RMS e Azure AD non vadano a buon fine e non saranno supportati dal sito Microsoft.com. Inoltre, il Rights Management License Agreement (RMLA) potrebbe essere violato se viene usato un Id Client non valido in un'app di produzione.

## Aspetto di un'implementazione del callback di autenticazione

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


**Autenticazione utente iOS/OS X**: per altre informazioni, vedere [Esempi di codice iOS/OS X](ios-os-x-code-examples.md),

**Passaggio 2** del primo scenario, "Uso di un file protetto RMS".


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



**Autenticazione utente Linux o C++** : per altre informazioni, vedere [Esempi di codice Linux](linux-c-code-examples.md).



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



 

 


<!--HONumber=Apr16_HO3-->


