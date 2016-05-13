---
# required metadata

title: Requisiti per Azure RMS&#58; Directory di Azure AD | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: ed25aa83-e272-437b-b445-3f01e985860c

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Requisiti per Azure RMS: directory di Azure AD

Per usare Azure Rights Management (Azure RMS), è necessario avere una directory di Azure AD. L'account aziendale per questa directory consente di accedere al portale di Azure classico, in cui è possibile, ad esempio, configurare e gestire i modelli di Rights Management.

Se non si ha una sottoscrizione di Azure aziendale, è possibile ottenerne una registrandosi per una versione di valutazione gratuita: andare alla pagina [Introduzione - Microsoft Azure](https://account.windowsazure.com/organization) e seguire le istruzioni.

Per altre informazioni, vedere le risorse seguenti contenute nella documentazione di Azure Active Directory:

-   [Che cos'è una directory di Azure AD?](/active-directory/active-directory-whatis)

-   [Associazione delle sottoscrizioni di Azure ad Azure Active Directory](/active-directory/active-directory-how-subscriptions-associated-directory)

Se si vuole integrare la directory di Azure AD con le foreste di AD locali, vedere [Integrazione delle identità locali con Azure Active Directory](/active-directory/active-directory-aadconnect).

> [!NOTE]
> Se si hanno dispositivi mobili o computer Mac che eseguono l'autenticazione locale tramite AD FS o un provider di autenticazione equivalente:
> 
> -   È necessario usare AD FS nella versione server minima di **Windows Server 2012 R2** oppure un provider di autenticazione alternativo che supporti il protocollo OAuth 2.0.

## Multi-Factor Authentication (MFA) e Azure RMS
Per utilizzare Multi-Factor Authentication (MFA) con Azure RMS, è necessario almeno uno dei seguenti elementi:

-   Office 2013 (versione minima):

    -   Se si ha Office 2013, è necessario installare anche l'[aggiornamento del 9 giugno 2015 per Office 2013 (KB3054853)](https://support.microsoft.com/kb/3054853). Per altre informazioni su questo aggiornamento e su come l'autenticazione moderna porta Active Directory Authentication Library in Office 2013, vedere il post relativo all'[anteprima pubblica di autenticazione moderna di Office 2013 annunciata](https://blogs.office.com/2015/03/23/office-2013-modern-authentication-public-preview-announced/) sul blog di Office.

-   Applicazione di condivisione Rights Management per Windows:

    -   È necessario avere installato la versione minima 1.0.1908.0, che può essere confermata tramite Pannello di controllo, Programmi e funzionalità. Per altre informazioni sull'applicazione, vedere [Applicazione Rights Management sharing per Windows](../rms-client/sharing-app-windows.md).

-   App di condivisione Rights Management per dispositivi mobili e computer Mac:

    -   Assicurarsi di avere la versione più recente installata. Il supporto di MFA è entrato nella versione di settembre 2015 dell’app di RMS sharing.

Quindi, configurare la soluzione MFA:

-   Per i tenant gestiti da Microsoft (si dispone di Azure Active Directory o Office 365):

    -   Configurare Azure MFA per forzare l'autenticazione a più fattori per gli utenti. Per istruzioni, vedere [Introduzione ad Azure Multi-Factor Authentication nel cloud](/multi-factor-authentication/multi-factor-authentication-get-started-cloud) nella documentazione di Multi-factor Authentication.

        Per altre informazioni su Azure MFA, vedere [Informazioni su Azure Multi-Factor Authentication](/multi-factor-authentication/multi-factor-authentication).

-   Per i tenant federativi (si gestiscono i server in locale):

    -   Configurare i server federativi per Azure Active Directory o Office 365. Ad esempio, se si usa AD FS, vedere [Configurare metodi di autenticazione aggiuntivi per ADFS](https://technet.microsoft.com/library/dn758113.aspx) su TechNet.

        Per altre informazioni su questo scenario, vedere il post relativo al [programma di gestione delle identità per Office 365](https://blogs.office.com/2014/01/30/the-works-with-office-365-identity-program-now-streamlined/) sul blog di Office.

## Passaggi successivi
Per verificare gli altri requisiti, vedere [Requisiti per Azure Rights Management](requirements-azure-rms.md).



<!--HONumber=Apr16_HO4-->


