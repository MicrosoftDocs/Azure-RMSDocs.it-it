---
title: Prerequisiti aggiuntivi per Azure AD e Azure Information Protection
description: Informazioni sui prerequisiti aggiuntivi Azure AD per Azure Information Protection in scenari specifici, ad esempio l'autenticazione a più fattori o basata su certificati oppure i computer che usano Office 2010 e altro ancora.
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
ms.openlocfilehash: b23afa0975f5d8f353b3ed8a5d4cf5332712f3b7
ms.sourcegitcommit: d1f6f10c9cb95de535d8121e90b211f421825caf
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/28/2020
ms.locfileid: "87298190"
---
# <a name="additional-azure-ad-requirements-for-azure-information-protection"></a>Ulteriori requisiti di Azure AD per Azure Information Protection

>*Si applica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

Una [directory Azure ad è un requisito](requirements.md#azure-active-directory) per l'uso di Azure Information Protection. Usare un account di una directory Azure AD per accedere al portale di Azure, in cui è possibile configurare Azure Information Protection impostazioni.

Se si ha una sottoscrizione che include Azure Information Protection o Azure Rights Management, la directory di Azure AD viene creata automaticamente se necessario.

Nelle sezioni seguenti sono elencati i requisiti aggiuntivi per AIP e Azure AD per scenari specifici. 

## <a name="computers-running-office-2010"></a>Computer che eseguono Office 2010

Oltre all'account Azure AD, i computer che eseguono Microsoft Office 2010 richiedono il [client Azure Information Protection Unified Labeling](./rms-client/aip-clientv2.md) o [Azure Information Protection client classico](./rms-client/aip-client.md) per l'autenticazione a Azure Information Protection e il relativo servizio di protezione dati, Azure Rights Management.

Se gli account utente sono federati (ad esempio, si usa AD FS), questi computer devono usare l'autenticazione integrata di Windows. In questo scenario l'autenticazione basata su moduli non riesce ad autenticare gli utenti per Azure Information Protection.

## <a name="support-for-certificate-based-authentication-cba"></a>Supporto per l'autenticazione basata su certificati (CBA)

Le app Azure Information Protection per iOS e Android supportano l'autenticazione basata su certificati. 

Per ulteriori informazioni, vedere [Introduzione all'autenticazione basata su certificati in Azure Active Directory](/azure/active-directory/active-directory-certificate-based-authentication-get-started).

## <a name="multi-factor-authentication-mfa-and-azure-information-protection"></a>Multi-Factor Authentication (MFA) e Azure Information Protection

Per usare multi-factor authentication con Azure Information Protection, è necessario che sia installato almeno uno dei seguenti elementi:

- **Microsoft Office,** versione 2013 o successiva
- **Un client AIP**. Nessuna versione minima richiesta. I client AIP per Windows, nonché le app visualizzatore per iOS e Android supportano multi-factor authentication.
- **L'app di condivisione Rights Management per i computer Mac**. Le app RMS sharing hanno supportato l'autenticazione a più fattori dalla versione di settembre 2015.

> [!NOTE]
> Se si dispone di Office 2013, potrebbe essere necessario installare un aggiornamento aggiuntivo per supportare Active Directory Authentication Library (ADAL), ad esempio il [9 giugno 2015, aggiornamento per Office 2013 (KB3054853)](https://support.microsoft.com/kb/3054853). 
>
> Per ulteriori informazioni, vedere l' [anteprima pubblica dell'autenticazione moderna di office 2013 annunciata](https://blogs.office.com/2015/03/23/office-2013-modern-authentication-public-preview-announced/) nel Blog di Office.       

Dopo aver confermato questi prerequisiti, eseguire una delle operazioni seguenti, a seconda della configurazione del tenant:

- **Tenant gestiti da Microsoft, con Azure ad o Office 365**. Configurare Azure MFA per forzare l'autenticazione a più fattori per gli utenti. 

    Per altre informazioni, vedere: 
    - [Introduzione ad Azure Multi-Factor Authentication nel cloud](/multi-factor-authentication/multi-factor-authentication-get-started-cloud)
    - [Informazioni su Azure Multi-Factor Authentication](/multi-factor-authentication/multi-factor-authentication)

- **Tenant federati, in cui i server federativi operano in locale**. Configurare i server federativi per Azure Active Directory o Office 365. Se ad esempio si usa AD FS, vedere [configurare metodi di autenticazione aggiuntivi per ad FS](/windows-server/identity/ad-fs/operations/configure-additional-authentication-methods-for-ad-fs). 

    Per ulteriori informazioni su questo scenario, vedere [la pagina relativa al funzionamento di office 365 – Identity Program ora semplificata](https://blogs.office.com/2014/01/30/the-works-with-office-365-identity-program-now-streamlined/) nel Blog di Office. 

## <a name="rights-management-connector--aip-scanner-requirements"></a>Requisiti di Rights Management Connector/AIP scanner

Il connettore Rights Management e lo scanner di Azure Information Protection non supportano l'autenticazione a più fattori. 

Se si distribuisce il connettore o lo scanner, gli account seguenti non richiedono l'autenticazione a più fattori:

- L'account che installa e configura il connettore.
- L'account dell'entità servizio in Azure AD **Aadrm_S-1-7-0**, creato dal connettore.
- L'account del servizio che esegue lo scanner.

## <a name="user-upn-values-dont-match-their-email-addresses"></a>I valori UPN dell'utente non corrispondono agli indirizzi di posta elettronica

Le configurazioni in cui i valori UPN degli utenti non corrispondono agli indirizzi di posta elettronica non sono una configurazione consigliata e non supportano l'accesso Single Sign-on per Azure Information Protection.

Se non è possibile modificare il valore UPN, configurare gli ID alternativi per gli utenti rilevanti e indicare come accedere a Office usando questo ID alternativo. 

Per altre informazioni, vedere:

- [Configurazione di un ID di accesso alternativo](/windows-server/identity/ad-fs/operations/configuring-alternate-login-id)
- [Le applicazioni di Office richiedono periodicamente le credenziali per SharePoint, OneDrive e Lync Online](https://support.microsoft.com/help/2913639/office-applications-periodically-prompt-for-credentials-to-sharepoint-online,-onedrive,-and-lync-online).

> [!TIP]
> Se il nome di dominio nel valore UPN è un dominio verificato per il tenant, aggiungere il valore UPN dell'utente come un altro indirizzo di posta elettronica all'attributo Azure AD **proxyAddresses** . Ciò consente all'utente di essere autorizzato per Azure Rights Management se il relativo valore UPN viene specificato al momento della concessione dei diritti di utilizzo. 

Per altre informazioni, vedere [Preparazione di utenti e gruppi per Azure Information Protection](prepare.md).

## <a name="authenticating-on-premises-using-adfs-or-another-authentication-provider"></a>Autenticazione locale con AD FS o un altro provider di autenticazione

Se si usa un dispositivo mobile o un computer Mac che esegue l'autenticazione in locale usando AD FS o un provider di autenticazione equivalente, è necessario usare AD FS in una delle configurazioni seguenti:

- Versione minima del server di **Windows server 2012 R2**
- Un provider di autenticazione alternativo che supporta il protocollo OAuth 2,0

## <a name="next-steps"></a>Passaggi successivi
Per verificare gli altri requisiti, vedere [Requisiti per Azure Information Protection](requirements.md).
