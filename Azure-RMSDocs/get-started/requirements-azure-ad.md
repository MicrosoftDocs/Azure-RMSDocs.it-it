---
title: Requisiti di Azure Active Directory per AIP
description: Identificare i requisiti di Azure AD per l'uso di Azure Information Protection, in modo che gli utenti possano essere autenticati.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 04/26/2018
ms.topic: get-started-article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: ed25aa83-e272-437b-b445-3f01e985860c
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 53d9d9b25ab71c91275bf770a6038eccbaa2659c
ms.sourcegitcommit: f4a97427d61e4b539c91c49c952658aa2dc729ce
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2018
ms.locfileid: "32018485"
---
# <a name="azure-active-directory-requirements-for-azure-information-protection"></a>Requisiti di Azure Active Directory per Azure Information Protection

>*Si applica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](http://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

Per usare Azure Information Protection, è necessario avere una directory di Azure AD. L'account usato da questa directory consente di accedere al portale di Azure, in cui è possibile, ad esempio, configurare e gestire le etichette di Azure Information Protection e i modelli di Azure Rights Management.

Se si ha una sottoscrizione che include Azure Information Protection o Azure Rights Management, la directory di Azure AD viene creata automaticamente se necessario.  

Per altre informazioni su Azure AD, vedere [Che cos'è una directory di Azure AD?](/active-directory/active-directory-whatis)

Per integrare la directory di Azure AD con le foreste di AD locali, vedere [Integrare le entità locali con Azure Active Directory](/active-directory/active-directory-aadconnect).

### <a name="scenarios-that-have-specific-requirements"></a>Scenari che hanno requisiti specifici 

Computer che eseguono Office 2010: 

- Per autenticarsi ad Azure Information Protection e al relativo servizio di protezione dei dati, Azure Rights Management, questi computer richiedono il [client di Azure Information Protection](../rms-client/aip-client.md) (scelta consigliata) o l'[applicazione di condivisione Rights Management per Windows](../rms-client/sharing-app-windows.md).

- Gli account utente federati, ad esempio AD FS, devono usare l'Autenticazione integrata di Windows. In questo scenario l'autenticazione basata su moduli non riesce ad autenticare gli utenti per Azure Information Protection.

Supporto dell'autenticazione basata sui certificati:

- Le app Azure Information Protection per iOS e Android supportano l'autenticazione basata su certificati. Per istruzioni per la configurazione dell'autenticazione basata sui certificati, vedere [Get started with certificate-based authentication in Azure Active Directory](/azure/active-directory/active-directory-certificate-based-authentication-get-started) (Introduzione all'autenticazione basata sui certificati in Azure Active Directory).

Il valore del nome UPN degli utenti non corrisponde al rispettivo indirizzo di posta elettronica:

- Questa configurazione non è consigliata. Se non è possibile cambiare il valore UPN, configurare un ID di accesso alternativo per gli utenti fornendo loro le istruzioni necessarie per l'accesso a Office con questo ID. Per altre informazioni, vedere [Configurazione di ID di accesso alternativo](/windows-server/identity/ad-fs/operations/configuring-alternate-login-id) e [Le applicazioni di Office richiedono periodicamente le credenziali per SharePoint Online, OneDrive e Lync Online](https://support.microsoft.com/help/2913639/office-applications-periodically-prompt-for-credentials-to-sharepoint-online,-onedrive,-and-lync-online).
    
    Quando il nome di dominio presente nel nome UPN corrisponde a un dominio verificato per il tenant, aggiungere il nome UPN di ciascun utente all'attributo proxyAddresses di Azure AD come indirizzo di posta elettronica aggiuntivo. In questo modo, se il nome UPN è stato specificato nel periodo in cui usufruiva dei diritti di utilizzo, l'autorizzazione di ciascun utente per Azure Rights Management può avere esito positivo. Per altre informazioni su questo punto e sul modo in cui viene eseguita l'autorizzazione degli account utente, vedere [Preparazione di utenti e gruppi per Azure Information Protection](../plan-design/prepare.md).

Dispositivi mobili o computer Mac che eseguono l'autenticazione locale tramite AD FS o un provider di autenticazione equivalente:

- È necessario usare AD FS nella versione server minima di **Windows Server 2012 R2** oppure un provider di autenticazione alternativo che supporti il protocollo OAuth 2.0.

## <a name="multi-factor-authentication-mfa-and-azure-information-protection"></a>Multi-Factor Authentication (MFA) e Azure Information Protection
Per usare Multi-Factor Authentication (MFA) con Azure Information Protection, è necessario almeno uno degli elementi seguenti:

-   Office 2013 (versione minima):

    -   Se si ha Office 2013, per supportare Active Directory Authentication Library (ADAL) può essere necessario installare un aggiornamento aggiuntivo, ad esempio l'[aggiornamento del 9 giugno 2015 per 2013 Office (KB3054853)](https://support.microsoft.com/kb/3054853). Per altre informazioni su questo aggiornamento e su come l'autenticazione moderna introduce l'accesso basato su Active Directory Authentication Library (ADAL) in Office 2013, vedere il post [Office 2013 modern authentication public preview announced](https://blogs.office.com/2015/03/23/office-2013-modern-authentication-public-preview-announced/) (Annuncio di anteprima pubblica dell'autenticazione moderna di Office 2013) nel blog di Office.

- Client Azure Information Protection:

    - Il [client Azure Information Protection](../rms-client/aip-client.md) per Windows e per iOS e Android ha sempre supportato MFA. Non è richiesta una versione minima. 

-   Applicazione Rights Management sharing per Windows:

    - È necessario avere installato la versione minima 1.0.1908.0. Verificare l'impostazione in Pannello di controllo > Programmi e funzionalità. L'applicazione di condivisione Rights Management è stata ora sostituita dal client Azure Information Protection. Per altre informazioni sull'applicazione di condivisione, vedere [Applicazione di condivisione Rights Management per Windows](../rms-client/sharing-app-windows.md).

-   App di condivisione Rights Management per dispositivi mobili e computer Mac:

    -   Assicurarsi di avere la versione più recente installata. Il supporto di MFA è entrato nella versione di settembre 2015 dell’app di RMS sharing.

Quindi, configurare la soluzione MFA:

-   Per i tenant gestiti da Microsoft (si dispone di Azure Active Directory o Office 365):

    - Configurare Azure MFA per forzare l'autenticazione a più fattori per gli utenti. Per istruzioni, vedere [Introduzione ad Azure Multi-Factor Authentication nel cloud](/multi-factor-authentication/multi-factor-authentication-get-started-cloud) nella documentazione di Multi-factor Authentication.

        Per altre informazioni su Azure MFA, vedere [Informazioni su Azure Multi-Factor Authentication](/multi-factor-authentication/multi-factor-authentication).

- Per i tenant federativi (si gestiscono i server in locale):

    - Configurare i server federativi per Azure Active Directory o Office 365. Ad esempio, se si usa AD FS, vedere [Configurare metodi di autenticazione aggiuntivi per ADFS](https://technet.microsoft.com/library/dn758113.aspx) su TechNet.

        Per altre informazioni su questo scenario, vedere il post relativo al [programma di gestione delle identità per Office 365](https://blogs.office.com/2014/01/30/the-works-with-office-365-identity-program-now-streamlined/) sul blog di Office.

Il connettore Rights Management e lo scanner di Azure Information Protection non supportano l'autenticazione a più fattori. Se si distribuisce il connettore o lo scanner, gli account seguenti non richiedono l'autenticazione a più fattori:

- L'account che installa e configura il connettore.

- L'account dell'entità servizio in Azure AD **Aadrm_S-1-7-0**, creato dal connettore.
 
- L'account del servizio che esegue lo scanner.

## <a name="next-steps"></a>Passaggi successivi
Per verificare gli altri requisiti, vedere [Requisiti per Azure Information Protection](requirements-azure-rms.md).

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
