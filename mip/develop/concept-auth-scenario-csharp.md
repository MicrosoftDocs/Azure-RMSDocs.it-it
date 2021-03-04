---
title: Concetti-scenari di autenticazione per i client C# Microsoft Information Protection (MIP) SDK
description: Dettagli tecnici sugli scenari di autenticazione per le applicazioni client C# Microsoft Information Protection SDK.
author: Pathak-Aniket
ms.author: v-anikep
ms.date: 09/02/2020
ms.topic: conceptual
ms.service: information-protection
ms.openlocfilehash: 8d210d74ecfd4ebdc50ec618415191894431fcdc
ms.sourcegitcommit: 7420cf0200c90687996124424a254c289b11a26f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/04/2021
ms.locfileid: "101844320"
---
# <a name="quickstart-public-and-confidential-clients-c"></a>Guida introduttiva: client pubblici e riservati (C#)

Esistono due scenari comuni usati per la compilazione di applicazioni con l'SDK MIP. Il primo scenario rileva che l'utente esegue l'autenticazione direttamente rispetto a Azure AD. Nel secondo, l'applicazione esegue l'autenticazione usando un certificato o una chiave dell'entità servizio segreta.

## <a name="public-client-applications"></a>Applicazioni client pubbliche

Queste applicazioni sono applicazioni desktop o per dispositivi mobili in cui l'applicazione in esecuzione nel dispositivo richiederà all'utente di eseguire l'autenticazione. L'utente si connette direttamente ai servizi MIP di back-end. In questo scenario, le librerie di autenticazione devono essere usate per assicurarsi che l'utente possa accedere a Azure AD, che soddisfi tutti i requisiti di accesso condizionale o a più fattori e ottenga un token OAuth2 per la risorsa appropriata.

Per ulteriori informazioni, vedere la [documentazione relativa al flusso di autenticazione client pubblico](/azure/active-directory/develop/msal-net-initializing-client-applications#initializing-a-public-client-application-from-configuration-options)

Di seguito è riportato un rapido codice snip che illustra il flusso di autenticazione client pubblico per l'applicazione client Microsoft Information Protection SDK utilizzando Microsoft Authentication Library (MSAL).

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

**Tenant-GUID** è il GUID univoco del tenant per il tenant Azure ad.
**Application-ID** è l'ID applicazione nella registrazione dell'applicazione nel portale di Azure ad.

## <a name="confidential-client-applications"></a>Applicazioni client riservate

Queste applicazioni sono applicazioni basate su cloud o sui servizi in cui l'utente non si connette direttamente ai servizi MIP di back-end. Il servizio ha la necessità di etichettare, proteggere o rimuovere la protezione del contenuto abilitato per MIP. In questo scenario, l'applicazione deve archiviare un certificato o un segreto dell'applicazione. Questi segreti verranno usati per l'autenticazione Azure AD e useranno il segreto per recuperare i token per i servizi MIP di back-end. Il licenziatario potrà quindi utilizzare le funzionalità di delega dell'SDK MIP per proteggere o utilizzare il contenuto per conto dell'utente autenticato.

L'integrazione di MIP SDK con le applicazioni basate su servizi richiede l'uso del flusso di concessione delle credenziali client. Microsoft Authentication Library (MSAL) può essere usato per implementarlo in un modello simile a quello che verrebbe visualizzato in un'applicazione client pubblica. Questo articolo illustra brevemente come aggiornare il MIP SDK `IAuthDelegate` in .NET per eseguire l'autenticazione per le applicazioni basate su servizi che usano questo flusso. Al momento della pubblicazione non è disponibile una versione di MSAL per C++, tuttavia è possibile implementare questo flusso tramite [chiamate REST dirette](/azure/active-directory/develop/v2-oauth2-client-creds-grant-flow#get-a-token).

Per ulteriori informazioni, vedere la [documentazione relativa al flusso di autenticazione client riservata](/azure/active-directory/develop/msal-net-initializing-client-applications#initializing-a-confidential-client-application-from-code)

Di seguito è riportato un rapido codice snip che illustra il flusso di autenticazione client riservato per l'applicazione client Microsoft Information Protection SDK utilizzando Microsoft Authentication Library (MSAL). Un'applicazione può eseguire l'autenticazione usando il certificato di Active Directory o il segreto client.

> [!NOTE]
> Prestare particolare attenzione a questa riga nell'esempio seguente. 
>
> ```csharp
> string[] scopes = new string[] { resource[resource.Length - 1].Equals('/') ? $"{resource}.default" : $"{resource}/.default" };
> ```
> Questo costrutti gli ambiti MSAL dalla risorsa fornita al `AcquireToken()` metodo. 

### <a name="msal-confidential-client-example"></a>Esempio di client riservato MSAL

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
**Tenant-GUID** è il GUID univoco del tenant per il tenant Azure ad.
**Application-ID** è l'ID applicazione nella registrazione dell'applicazione nel portale di Azure ad.