---
title: Concetti-scenari di autenticazione per i client C# Microsoft Information Protection (MIP) SDK
description: Dettagli tecnici sugli scenari di autenticazione per le applicazioni client C# Microsoft Information Protection SDK.
author: msmbaldwin
ms.author: mbaldwin
ms.date: 09/02/2020
ms.topic: conceptual
ms.service: information-protection
ms.openlocfilehash: 7a22bc297b3330b3cdb738ff16e013d0d1f0dc87
ms.sourcegitcommit: 8e48016754e6bc6d051138b3e3e3e3edbff56ba5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/04/2021
ms.locfileid: "97865332"
---
# <a name="quickstart-public-and-confidential-clients-c"></a>Guida introduttiva: client pubblici e riservati (C#)

Esistono due scenari comuni usati per la compilazione di applicazioni con l'SDK MIP. Uno scenario prevede che l'utente esegua l'autenticazione direttamente rispetto a Azure AD, dove, come nell'altra, l'autenticazione dell'applicazione usa una chiave o un certificato dell'entità servizio segreta.

## <a name="public-client-applications"></a>Applicazioni client pubbliche

Si tratta in genere di applicazioni desktop o per dispositivi mobili in cui l'applicazione in esecuzione nel dispositivo richiederà all'utente di eseguire l'autenticazione e l'utente si connette direttamente ai servizi MIP back-end. In questo scenario, le librerie di autenticazione devono essere usate per assicurarsi che l'utente sia in grado di accedere a Azure AD, che soddisfi tutti i requisiti di accesso condizionale o a più fattori e ottenga un token OAuth2 per la risorsa appropriata.

Per ulteriori informazioni, vedere la [documentazione di Azure ad flusso di autenticazione client pubblico](/azure/active-directory/develop/msal-net-initializing-client-applications#initializing-a-public-client-application-from-configuration-options)

Di seguito è riportato un rapido codice snip che illustra il flusso di autenticazione client pubblico per l'applicazione client Microsoft Information Protection SDK usando Microsoft Authentication Library (MSAL).

```csharp

public string AcquireToken(Identity identity, string authority, string resource, string claims)
{
     var authorityUri = new Uri(authority);
     authority = String.Format("https://{0}/{1}", authorityUri.Host, "<Tenant-GUID>");

     _app = PublicClientApplicationBuilder.Create("<Application-Id>").WithAuthority(authority).WithDefaultRedirectUri().Build();

     var accounts = (_app.GetAccountsAsync()).GetAwaiter().GetResult();

     // Append .default to the resource passed in to AcquireToken().
     string[] scopes = new string[] { resource[resource.Length - 1].Equals('/') ? $"{resource}.default" : $"{resource}/.default" };
     var result = _app.AcquireTokenInteractive(scopes).WithAccount(accounts.FirstOrDefault()).WithPrompt(Prompt.SelectAccount)
                    .ExecuteAsync().ConfigureAwait(false).GetAwaiter().GetResult();

     return result.AccessToken;
}
```

Tenant-GUID rappresenta il GUID del tenant per il tenant di Azure AD, mentre Application-ID è l'ID applicazione nella registrazione dell'applicazione nel portale di Azure AD.

## <a name="confidential-client-applications"></a>Applicazioni client riservate

Si tratta in genere di applicazioni basate su cloud o sui servizi in cui l'utente non si connette direttamente ai servizi MIP di back-end, ma il servizio deve etichettare, proteggere o rimuovere la protezione del contenuto abilitato per MIP. In questo scenario, l'applicazione deve archiviare un certificato o un segreto dell'applicazione da usare per l'autenticazione per Azure AD e usare tale segreto per recuperare i token per i servizi MIP back-end. Il licenziatario potrà quindi utilizzare le funzionalità di delega dell'SDK MIP per proteggere o utilizzare il contenuto per conto dell'utente autenticato.

Per ulteriori informazioni, vedere la [documentazione relativa al flusso di autenticazione client Azure ad riservata](/azure/active-directory/develop/msal-net-initializing-client-applications#initializing-a-confidential-client-application-from-code)

Di seguito è riportato un rapido codice snip che illustra il flusso di autenticazione client riservato per l'applicazione client Microsoft Information Protection SDK usando Microsoft Authentication Library (MSAL). Un'applicazione può eseguire l'autenticazione usando il certificato di Active Directory o il segreto client.

```csharp
public string AcquireToken(Identity identity, string authority, string resource, string claim)
{
     AuthenticationResult result;
     var authorityUri = new Uri(authority);
     authority = string.Format("https://{0}/{1}", authorityUri.Host, "<Tenant-GUID>");

     // Certification Based Auth
     if (doCertAuth)
     {
          // Build ConfidentialClientApplication using certificate.
          _app = ConfidentialClientApplicationBuilder.Create("<Application-Id>")
               .WithCertificate(certificate) //Assumption here is Application passes a certificate created using certificate thumbprint
               .WithAuthority(new Uri(authority))
               .Build();
     }

     // Client secret based Auth
     else
     {
          // Build ConfidentialClientApplication using app secret
          _app = ConfidentialClientApplicationBuilder.Create("<Application-Id>")
               .WithClientSecret(clientSecret)
               .WithAuthority(new Uri(authority))
               .Build();
     }

     // Append .default to the resource passed in to AcquireToken().
     string[] scopes = new string[] { resource[resource.Length - 1].Equals('/') ? $"{resource}.default" : $"{resource}/.default" };

     try{
          result = _app.AcquireTokenForClient(scopes).ExecuteAsync().Result;
     }
     catch (MsalServiceException ex) when (ex.Message.Contains("AADSTS70011"))
     {
          // Invalid scope. The scope has to be of the form "https://resourceurl/.default"
          // Mitigation: change the scope to be as expected
          Console.WriteLine("Scope provided is not supported");
          return null;
     }
            return result.AccessToken;
}

```

Tenant-GUID rappresenta il GUID del tenant per il tenant di Azure AD, mentre Application-ID è l'ID applicazione nella registrazione dell'applicazione nel portale di Azure AD.