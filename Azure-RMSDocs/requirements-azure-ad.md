---
title: Altri prerequisiti per Azure AD e Azure Information Protection
description: Informazioni su prerequisiti aggiuntivi di Azure AD per Azure Information Protection in scenari specifici, ad esempio l'autenticazione a più fattori o basata sui certificati e altro ancora.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 07/22/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: ed25aa83-e272-437b-b445-3f01e985860c
ms.subservice: prereqs
ms.suite: ems
ms.custom: admin, has-adal-ref
ms.openlocfilehash: 7ba843beac002261cd1ada865767b414e22560ae
ms.sourcegitcommit: af7ac2eeb8f103402c0036dd461c77911fbc9877
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/18/2021
ms.locfileid: "98560391"
---
# <a name="additional-azure-ad-requirements-for-azure-information-protection"></a>Requisiti aggiuntivi di Azure AD per Azure Information Protection - AIP

>***Si applica a**: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*
>
>***Rilevante per**: [Client di etichettatura unificata di AIP e client classico di AIP](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients).*

> [!NOTE]
> Per offrire un'esperienza per i clienti unificata e semplificata, il **client classico di Azure Information Protection** e **Gestione etichette** nel portale di Azure saranno **deprecati** a partire dal **31 marzo 2021**. 
>
> In questo intervallo di tempo tutti i clienti correnti di Azure Information Protection potranno eseguire la transizione alla soluzione di etichettatura unificata di Microsoft Information Protection. Altre informazioni nell'[avviso ufficiale sulla deprecazione](https://aka.ms/aipclassicsunset).

Una [directory Azure AD è un requisito](requirements.md#azure-active-directory) per l'uso di Azure Information Protection. Usare un account da una directory Azure AD per accedere al portale di Azure, in cui è possibile configurare le impostazioni di Azure Information Protection.

Se si ha una sottoscrizione che include Azure Information Protection o Azure Rights Management, la directory di Azure AD viene creata automaticamente se necessario.

Nelle sezioni seguenti sono elencati i requisiti aggiuntivi per AIP e Azure AD per scenari specifici. 

## <a name="support-for-certificate-based-authentication-cba"></a>Supporto dell'autenticazione basata sui certificati

Le app Azure Information Protection per iOS e Android supportano l'autenticazione basata su certificati. 

Per altre informazioni, vedere [Introduzione all'autenticazione basata su certificati in Azure Active Directory](/azure/active-directory/active-directory-certificate-based-authentication-get-started).

## <a name="multi-factor-authentication-mfa-and-azure-information-protection"></a>Multi-Factor Authentication (MFA) e Azure Information Protection

Per usare l'autenticazione a più fattori (MFA) con Azure Information Protection, è necessario almeno uno degli elementi seguenti installati:

- **Microsoft Office** versione 2013 o successive
- **Client AIP**. Non è richiesta alcuna versione minima. I client AIP per Windows, nonché le app visualizzatore per iOS e Android supportano tutti MFA.
- **App di condivisione Microsoft Rights Management per computer Mac**. Le app di condivisione Microsoft Rights Management hanno supportato l'autenticazione MFA sin dalla versione di settembre 2015.

> [!NOTE]
> Se si ha Office 2013, può essere necessario installare un aggiornamento aggiuntivo per supportare Active Directory Authentication Library (ADAL), come l'[aggiornamento del 9 giugno 2015 per Office 2013 (KB3054853)](https://support.microsoft.com/kb/3054853). 
>
> Per altre informazioni, vedere l'[annuncio dell'anteprima pubblica di autenticazione moderna di Office 2013](https://blogs.office.com/2015/03/23/office-2013-modern-authentication-public-preview-announced/) nel blog di Office.       

Dopo aver confermato questi prerequisiti, eseguire una delle operazioni seguenti, a seconda della configurazione del tenant:

- **Tenant gestiti da Microsoft, con Azure AD o Microsoft 365**. Configurare Azure MFA per forzare l'autenticazione a più fattori per gli utenti. 

    Per altre informazioni, vedere: 
    - [Introduzione ad Azure Multi-Factor Authentication nel cloud](/multi-factor-authentication/multi-factor-authentication-get-started-cloud)
    - [Informazioni su Azure Multi-Factor Authentication](/multi-factor-authentication/multi-factor-authentication)

- **Tenant federati, in cui i server federativi operano in locale**. Configurare i server federativi per Azure Active Directory o Microsoft 365. Ad esempio, se si usa AD FS, vedere [Configurare metodi di autenticazione aggiuntivi per AD FS](/windows-server/identity/ad-fs/operations/configure-additional-authentication-methods-for-ad-fs). 

    Per altre informazioni su questo scenario, vedere [The Works with Microsoft 365 – Identity program now streamlined](https://blogs.office.com/2014/01/30/the-works-with-office-365-identity-program-now-streamlined/) (Progetti per Microsoft 365 - Programma di gestione delle identità ora semplificato) nel blog di Office. 

## <a name="rights-management-connector--aip-scanner-requirements"></a>Requisiti del connettore Rights Management e dello scanner AIP

Il connettore Rights Management e lo scanner di Azure Information Protection non supportano l'autenticazione a più fattori. 

Se si distribuisce il connettore o lo scanner, gli account seguenti non richiedono l'autenticazione a più fattori:

- L'account che installa e configura il connettore.
- L'account dell'entità servizio in Azure AD **Aadrm_S-1-7-0**, creato dal connettore.
- L'account del servizio che esegue lo scanner.

## <a name="user-upn-values-dont-match-their-email-addresses"></a>I valori UPN degli utenti non corrispondono ai rispettivi indirizzi di posta elettronica

Le configurazioni in cui i valori UPN degli utenti non corrispondono ai rispettivi indirizzi di posta elettronica non sono una configurazione consigliata e non supportano l'accesso Single Sign-on per Azure Information Protection.

Se non è possibile cambiare il valore UPN, configurare ID di accesso alternativi per gli utenti interessati fornendo loro le istruzioni necessarie per l'accesso a Office con questo ID alternativo. 

Per altre informazioni, vedere:

- [Configurazione di un ID di accesso alternativo](/windows-server/identity/ad-fs/operations/configuring-alternate-login-id)
- [Le applicazioni di Office richiedono periodicamente le credenziali per SharePoint, OneDrive e Lync Online](https://support.microsoft.com/help/2913639/office-applications-periodically-prompt-for-credentials-to-sharepoint-online,-onedrive,-and-lync-online).

> [!TIP]
> Se il nome di dominio presente nel valore UPN corrisponde a un dominio verificato per il tenant, aggiungere il valore UPN dell'utente all'attributo **proxyAddresses** di Azure AD come indirizzo di posta elettronica aggiuntivo. In questo modo, se il valore UPN è stato specificato nel periodo in cui usufruiva dei diritti di utilizzo, l'autorizzazione dell'utente per Azure Rights Management può avere esito positivo. 

Per altre informazioni, vedere [Preparazione di utenti e gruppi per Azure Information Protection](prepare.md).

## <a name="authenticating-on-premises-using-ad-fs-or-another-authentication-provider"></a>Autenticazione locale con AD FS o un altro provider di autenticazione

Se si usa un dispositivo mobile o un computer Mac che esegue l'autenticazione in locale con AD FS o un provider di autenticazione equivalente, è necessario usare AD FS in una delle configurazioni seguenti:

- Versione minima del server **Windows Server 2012 R2**
- Un provider di autenticazione alternativo che supporta il protocollo OAuth 2.0

## <a name="computers-running-office-2010"></a>Computer che eseguono Office 2010

> [!IMPORTANT]
> Supporto "Extended" per Office 2010 terminato il 13 ottobre 2020. Per altre informazioni, vedere [AIP e versioni legacy di Windows e Office](known-issues.md#aip-and-legacy-windows-and-office-versions).
> 

Oltre a un account di Azure AD, i computer che eseguono Microsoft 2010 devono disporre del client di Azure Information Protection per Windows per autenticarsi per Azure Information Protection e il relativo servizio di protezione dei dati, Azure Rights Management. 

Gli account utente federati, ad esempio AD FS, devono usare l'Autenticazione integrata di Windows nei loro computer. In questo scenario l'autenticazione basata su moduli non riesce ad autenticare gli utenti per Azure Information Protection.

Si consiglia di distribuire il client di etichettatura unificata di Azure Information Protection. Se non è ancora stato eseguito l'aggiornamento, è possibile che nel sistema sia ancora distribuito il [client classico di Azure Information Protection](./rms-client/aip-client.md). 

Per altre informazioni, vedere [Lato client di Azure Information Protection](rms-client/use-client.md).
## <a name="next-steps"></a>Passaggi successivi
Per verificare gli altri requisiti, vedere [Requisiti per Azure Information Protection](requirements.md).
