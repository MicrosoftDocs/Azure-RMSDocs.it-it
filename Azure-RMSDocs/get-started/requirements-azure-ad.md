---
title: Requisiti di Azure Active Directory per AIP
description: Identificare i requisiti di Azure AD per l&quot;uso di Azure Information Protection, in modo che gli utenti possano essere autenticati.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 04/05/2017
ms.topic: get-started-article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: ed25aa83-e272-437b-b445-3f01e985860c
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 729d66e8d55d045b74ac5c794cf83ddcc2848d35
ms.sourcegitcommit: 1671466a42e7e00e1cc2702b1f609fb112aac7db
translationtype: HT
---
# <a name="azure-active-directory-requirements-for-azure-information-protection"></a>Requisiti di Azure Active Directory per Azure Information Protection

>*Si applica a: Azure Information Protection, Office 365*

Per usare Azure Information Protection, è necessario avere una directory di Azure AD. L'account aziendale per questa directory consente di accedere al portale di Azure classico, in cui è possibile, ad esempio, configurare e gestire i modelli di Rights Management.

Se l'organizzazione non ha una sottoscrizione di Azure, è possibile ottenerne una registrandosi per una versione di valutazione gratuita. Passare alla pagina di [introduzione ad Azure](https://account.windowsazure.com/organization) e seguire le istruzioni.

Per altre informazioni, vedere le risorse seguenti contenute nella documentazione di Azure Active Directory:

-   [Che cos'è una directory di Azure AD?](/active-directory/active-directory-whatis)

-   [Associare le sottoscrizioni di Azure ad Azure Active Directory](/active-directory/active-directory-how-subscriptions-associated-directory)

Se si vuole integrare la directory di Azure AD con le foreste di AD locali, vedere [Integrazione delle identità locali con Azure Active Directory](/active-directory/active-directory-aadconnect).

### <a name="scenarios-that-have-specific-requirements"></a>Scenari che hanno requisiti specifici 

Computer che eseguono Office 2010: 

- Per autenticarsi ad Azure Information Protection e al relativo servizio di protezione dei dati, Azure Rights Management, questi computer richiedono il [client di Azure Information Protection](../rms-client/aip-client.md) (scelta consigliata) o l'[applicazione di condivisione Rights Management per Windows](../rms-client/sharing-app-windows.md).

- Gli account utente federati, ad esempio AD FS, devono usare l'Autenticazione integrata di Windows. L'autenticazione basata su moduli in questo scenario non riuscirà ad autenticare gli utenti per Azure Information Protection.

Supporto dell'autenticazione basata sui certificati:

- L'app Azure Information Protection per Android supporta l'autenticazione basata sui certificati se si dispone almeno della versione 5.0 di Android. Per istruzioni per la configurazione dell'autenticazione basata sui certificati, vedere [Get started with certificate-based authentication in Azure Active Directory](/active-directory/active-directory-certificate-based-authentication-get-started) (Introduzione all'autenticazione basata sui certificati in Azure Active Directory).

Dispositivi mobili o computer Mac che eseguono l'autenticazione locale tramite AD FS o un provider di autenticazione equivalente:

- È necessario usare AD FS nella versione server minima di **Windows Server 2012 R2** oppure un provider di autenticazione alternativo che supporti il protocollo OAuth 2.0.

## <a name="multi-factor-authentication-mfa-and-azure-information-protection"></a>Multi-Factor Authentication (MFA) e Azure Information Protection
Per usare Multi-Factor Authentication (MFA) con Azure Information Protection, è necessario almeno uno degli elementi seguenti:

-   Office 2013 (versione minima):

    -   Se si ha Office 2013, per supportare Active Directory Authentication Library (ADAL) può essere necessario installare un aggiornamento aggiuntivo, ad esempio l'[aggiornamento del 9 giugno 2015 per 2013 Office (KB3054853)](https://support.microsoft.com/kb/3054853). Per altre informazioni su questo aggiornamento e su come l'autenticazione moderna porta Active Directory Authentication Library in Office 2013, vedere il post relativo all'[anteprima pubblica di autenticazione moderna di Office 2013 annunciata](https://blogs.office.com/2015/03/23/office-2013-modern-authentication-public-preview-announced/) sul blog di Office.

- Client Azure Information Protection:

    - Il [client Azure Information Protection](../rms-client/aip-client.md) per Windows e per iOS e Android ha sempre supportato MFA. Non è richiesta una versione minima. 

-   Applicazione Rights Management sharing per Windows:

    -   È necessario avere installato la versione minima 1.0.1908.0, che può essere confermata tramite Pannello di controllo, Programmi e funzionalità. L'applicazione di condivisione Rights Management è stata ora sostituita dal client Azure Information Protection. Per altre informazioni sull'applicazione di condivisione, vedere [Applicazione di condivisione Rights Management per Windows](../rms-client/sharing-app-windows.md).

-   App di condivisione Rights Management per dispositivi mobili e computer Mac:

    -   Assicurarsi di avere la versione più recente installata. Il supporto di MFA è entrato nella versione di settembre 2015 dell’app di RMS sharing.

Quindi, configurare la soluzione MFA:

-   Per i tenant gestiti da Microsoft (si dispone di Azure Active Directory o Office 365):

    -   Configurare Azure MFA per forzare l'autenticazione a più fattori per gli utenti. Per istruzioni, vedere [Introduzione ad Azure Multi-Factor Authentication nel cloud](/multi-factor-authentication/multi-factor-authentication-get-started-cloud) nella documentazione di Multi-factor Authentication.

        Per altre informazioni su Azure MFA, vedere [Informazioni su Azure Multi-Factor Authentication](/multi-factor-authentication/multi-factor-authentication).

-   Per i tenant federativi (si gestiscono i server in locale):

    -   Configurare i server federativi per Azure Active Directory o Office 365. Ad esempio, se si usa AD FS, vedere [Configurare metodi di autenticazione aggiuntivi per ADFS](https://technet.microsoft.com/library/dn758113.aspx) su TechNet.

        Per altre informazioni su questo scenario, vedere il post relativo al [programma di gestione delle identità per Office 365](https://blogs.office.com/2014/01/30/the-works-with-office-365-identity-program-now-streamlined/) sul blog di Office.

## <a name="next-steps"></a>Passaggi successivi
Per verificare gli altri requisiti, vedere [Requisiti per Azure Information Protection](requirements-azure-rms.md).

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
