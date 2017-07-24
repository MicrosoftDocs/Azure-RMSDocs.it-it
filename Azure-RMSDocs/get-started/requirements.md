---
title: Requisiti per Azure Information Protection
description: Identificare i prerequisiti per distribuire Azure Information Protection per l'organizzazione.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 07/17/2017
ms.topic: get-started-article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: dc78321d-d759-4653-8818-80da74b6cdeb
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 2a41876a8c307b0736901de895e10cf3d3201809
ms.sourcegitcommit: 12c9a4e3fe8e92d816f0a13003062f20dd2716df
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/17/2017
---
# <a name="requirements-for-azure-information-protection"></a>Requisiti per Azure Information Protection

>*Si applica a: Azure Information Protection, Office 365*

Prima di distribuire Azure Information Protection per l'organizzazione, verificare di soddisfare i prerequisiti seguenti. 

## <a name="subscription-for-azure-information-protection"></a>Sottoscrizione di Azure Information Protection

Per le funzionalità di classificazione, etichettatura e protezione, è necessario un [piano Azure Information Protection](https://www.microsoft.com/cloud-platform/azure-information-protection-pricing). 

Per la sola funzionalità di protezione, è necessario un [piano di Office 365 che include Rights Management](http://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf).

Per verificare che la sottoscrizione dell'organizzazione includa le funzionalità di Azure Information Protection che si vogliono usare, esaminare le [informazioni sulla sottoscrizione](https://www.microsoft.com/cloud-platform/azure-information-protection-pricing) e l'[elenco delle funzionalità](https://www.microsoft.com/cloud-platform/azure-information-protection-features) nel sito di Azure Information Protection.

> [!NOTE]
> Se si hanno domande sulle sottoscrizioni o sulle licenze evitare di pubblicarle su questa pagina e contattare l'Account Manager designato da Microsoft o il [supporto tecnico Microsoft](information-support.md#to-contact-microsoft-support).

## <a name="azure-active-directory"></a>Azure Active Directory

Per supportare l'autenticazione e l'autorizzazione utente per Azure Information Protection, l'organizzazione deve avere Azure Active Directory (Azure AD). Inoltre, se si vuole usare gli account utente dalla directory locale (AD DS), è necessario anche configurare l'integrazione delle directory.

Multi-Factor Authentication (MFA) è supportato in Azure Information Protection quando si ha il software client richiesto e l'infrastruttura di supporto MFA è configurata correttamente.

Per altre informazioni sui requisiti di autenticazione, vedere [Requisiti di Azure Active Directory per Azure Information Protection](requirements-azure-ad.md). 

Per altre informazioni sui requisiti relativi agli account utente e di gruppo per l'autorizzazione, vedere [Preparazione di utenti e gruppi per Azure Information Protection](../plan-design/prepare.md).

## <a name="client-devices"></a>Dispositivi client

Gli utenti devono avere dispositivi client, quali computer o dispositivi mobili, che eseguono un sistema operativo che supporta Azure Information Protection.

I dispositivi seguenti supportano il client di Azure Information Protection, che consente agli utenti di classificare ed etichettare i messaggi di posta elettronica e i documenti:

- Windows 10 (x86, x64)

- Windows 8.1 (x86, x64)

- Windows 8 (x86, x64)

- Windows 7 Service Pack 1 (x86, x64)

- Windows Server 2016 

- Windows Server 2012 R2 e Windows Server 2012

- Windows Server 2008 R2 

Per le versioni server elencate, il client Azure Information Protection è supportato per Servizi Desktop remoto. Se si eliminano profili utente quando si usa il client Azure Information Protection con Servizi Desktop remoto, non eliminare la cartella **%Appdata%\Microsoft\Protect**.

Quando il client Azure Information Protection protegge i dati tramite il servizio Azure Rights Management, i dati possono essere usati dagli [stessi dispositivi](requirements-client-devices.md) (Windows, Mac, iOS, Android) che supportano il servizio Azure Rights Management.

## <a name="applications"></a>Applicazioni

Il client Azure Information Protection consente di etichettare e proteggere documenti e messaggi di posta elettronica usando le applicazioni di Office **Word**, **Excel**, **PowerPoint** e **Outlook** delle edizioni di Office seguenti:

- Office 365 ProPlus con le app di Office 2016 o 2013 (installazione basata su A portata di clic o Windows Installer)

- Office Professional Plus 2016

- Office Professional Plus 2013 con Service Pack 1

- Office Professional Plus 2010 con Service Pack 2

Con le altre edizioni di Office non è possibile proteggere i documenti e i messaggi di posta elettronica usando un servizio Rights Management. Per queste edizioni Azure Information Protection è supportato solo per la classificazione. Le etichette che applicano la protezione non vengono visualizzate sulla barra di Azure Information Protection. 

Per informazioni sulle edizioni di Office che supportano il servizio di protezione dati, vedere [Applicazioni che supportano la protezione dati di Azure Rights Management](requirements-applications.md).

## <a name="firewalls-and-network-infrastructure"></a>Firewall e infrastruttura di rete

Se è presente un firewall o dispositivi di rete simili configurati per consentire connessioni specifiche, vedere le informazioni relative ad **Azure Rights Management (RMS)** nella sezione [Portale e condivisione di Office 365](https://support.office.com/en-us/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2?ui=en-US&rs=en-US&ad=US#bkmk_portal-identity) dell'articolo [URL e intervalli di indirizzi IP per Office 365](https://support.office.com/en-US/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2).

Usare le istruzioni in questo articolo per mantenersi aggiornati sulle modifiche apportate a queste informazioni tramite la sottoscrizione a un feed RSS.

Oltre alle informazioni nell'articolo di Office, le istruzioni seguenti sono specifiche per Azure Information Protection:

- Consentire il traffico HTTPS sulla porta TCP 443 per **api.informationprotection.azure.com**.

- Non terminare la connessione TLS dal client al servizio, ad esempio per il controllo a livello di pacchetti. In questo modo viene interrotta l'associazione del certificato usata dai client RMS con le autorità di certificazione gestite da Microsoft per la protezione delle comunicazioni con Azure RMS.

- Se si usa un proxy Web che richiede l'autenticazione, configurarlo per l'uso dell'autenticazione integrata di Windows con le credenziali di accesso di Active Directory dell'utente.


### <a name="on-premises-servers"></a>Server locali

Se si vuole usare il servizio Azure Rights Management di Azure Information Protection con server locali, sono supportati i prodotti seguenti:

- Exchange Server

- SharePoint Server

- File server di Windows Server che supportano la funzionalità Infrastruttura di classificazione file

Per informazioni sui requisiti aggiuntivi per questo scenario, vedere [Server locali che supportano la protezione dati di Azure Rights Management](requirements-servers.md).

### <a name="coexistence-of-ad-rms-with-azure-rms"></a>Coesistenza di AD RMS con Azure RMS

Lo scenario di distribuzione seguente non è supportato, a meno che non si usi la protezione di AD RMS con Azure Information Protection (configurazione "hold your own key" o HYOK):

- Esecuzione side-by-side di AD RMS e di Azure RMS nella stessa organizzazione tranne che durante la migrazione, come descritto in [Migrazione da AD RMS ad Azure Information Protection](../plan-design/migrate-from-ad-rms-to-azure-rms.md).

È disponibile un percorso di migrazione supportato [da AD RMS ad Azure Information Protection](http://technet.microsoft.com/library/Dn858447.aspx) e da [Azure Information Protection ad AD RMS](/powershell/module/aadrm/Set-AadrmMigrationUrl). Se si distribuisce Azure Information Protection e poi si decide di interrompere l'uso del servizio cloud, vedere [Rimozione delle autorizzazioni e disattivazione di Azure Information Protection](../deploy-use/decommission-deactivate.md).

[!INCLUDE[Commenting house rules](../includes/houserules.md)]


