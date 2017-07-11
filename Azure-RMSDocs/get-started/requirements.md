---
title: Requisiti per Azure Information Protection
description: Identificare i prerequisiti per distribuire Azure Information Protection per l'organizzazione.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 06/09/2017
ms.topic: get-started-article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: dc78321d-d759-4653-8818-80da74b6cdeb
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 66874f6e60c2cd5efb2dedaae470170811a84a67
ms.sourcegitcommit: 04eb4990e2bf0004684221592cb93df35e6acebe
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/30/2017
---
<a id="requirements-for-azure-information-protection" class="xliff"></a>

# Requisiti per Azure Information Protection

>*Si applica a: Azure Information Protection, Office 365*

Prima di distribuire Azure Information Protection per l'organizzazione, verificare di soddisfare i prerequisiti seguenti. 

|Requisito|Altre informazioni|
|---------------|--------------------|
|Una sottoscrizione di Azure Information Protection|Per le funzionalità di classificazione, etichettatura e protezione, è necessario un [piano Azure Information Protection](https://www.microsoft.com/cloud-platform/azure-information-protection-pricing). Per la sola funzionalità di protezione, è necessario un [piano di Office 365 che include Rights Management](http://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf).<br /><br /> Esaminare le [informazioni sulla sottoscrizione](https://www.microsoft.com/cloud-platform/azure-information-protection-pricing) e l'[elenco delle funzionalità](https://www.microsoft.com/cloud-platform/azure-information-protection-features) nel sito Azure Information Protection per verificare che la sottoscrizione dell'organizzazione includa le funzionalità di Azure Information Protection che si vogliono usare.<br /><br />Nota: se si hanno domande sulle sottoscrizioni o sulle licenze, non pubblicarle su questa pagina, ma contattare l'Account Manager designato da Microsoft o il [supporto tecnico Microsoft](information-support.md#to-contact-microsoft-support). |
|Azure Active Directory|Per supportare l'autenticazione e l'autorizzazione utente per Azure Information Protection, l'organizzazione deve avere Azure Active Directory (Azure AD). Inoltre, se si vuole usare gli account utente dalla directory locale (AD DS), è necessario anche configurare l'integrazione delle directory.<br /><br />Multi-Factor Authentication (MFA) è supportato in Azure Information Protection quando si ha il software client richiesto e l'infrastruttura di supporto MFA è configurata correttamente.<br /><br />Per altre informazioni sui requisiti di autenticazione, vedere [Requisiti di Azure Active Directory per Azure Information Protection](requirements-azure-ad.md). <br /><br />Per altre informazioni sui requisiti relativi agli account utente e di gruppo per l'autorizzazione, vedere [Preparazione di utenti e gruppi per Azure Information Protection](../plan-design/prepare.md).|
|Dispositivi client|Gli utenti devono avere dispositivi client, quali computer o dispositivi mobili, che eseguono un sistema operativo che supporta Azure Information Protection.<br /><br />I dispositivi seguenti supportano il client di Azure Information Protection, che consente agli utenti di classificare ed etichettare i messaggi di posta elettronica e i documenti di Office:<br /><br />- Windows 10 (x86, x64)<br /><br />- Windows 8.1 (x86, x64)<br /><br />- Windows 8 (x86, x64)<br /><br />- Windows 7 Service Pack 1 (x86, x64)<br /><br />- Windows Server 2016 <br /><br /> - Windows Server 2012 R2 e Windows Server 2012<br /><br />Quando questo client protegge i dati tramite il servizio Azure Rights Management, i dati possono essere utilizzati dagli stessi dispositivi (Windows, Mac, iOS, Android) che supportano il servizio Azure Rights Management. <br /><br />Per informazioni dettagliate sui dispositivi che supportano il servizio Azure Rights Management, vedere [Dispositivi client che supportano la protezione dati di Azure Rights Management](../get-started/requirements-client-devices.md).|
|Applicazioni|Il client Azure Information Protection consente di etichettare e proteggere file e messaggi di posta elettronica usando le applicazioni di Office **Word**, **Excel**, **PowerPoint** e **Outlook** delle edizioni di Office seguenti:<br /><br /> - Office 365 ProPlus con le app di Office 2016 o 2013 (installazione basata su A portata di clic o Windows Installer)<br /><br />- Office Professional Plus 2016<br /><br />- Office Professional Plus 2013 con Service Pack 1<br /><br />- Office Professional Plus 2010 <br /><br />Con le altre edizioni di Office non è possibile proteggere i documenti e i messaggi di posta elettronica usando un servizio Rights Management. Per queste edizioni, Azure Information Protection è supportato solo per la classificazione e le etichette che applicano la protezione non vengono visualizzate sulla barra di Azure Information Protection. <br /><br />Per informazioni sulle edizioni di Office che supportano il servizio di protezione dati, vedere [Applicazioni che supportano la protezione dati di Azure Rights Management](requirements-applications.md).|
|Infrastruttura in grado di supportare la connettività a Internet e ai servizi cloud dipendenti.|Se è presente un firewall o dispositivi di rete di protezione simili che devono essere configurati per consentire connessioni specifiche, vedere le informazioni relative ad **Azure Rights Management (RMS)** nella sezione [Portale e condivisione di Office 365](https://support.office.com/en-us/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2?ui=en-US&rs=en-US&ad=US#bkmk_portal-identity) dell'articolo [URL e intervalli di indirizzi IP per Office 365](https://support.office.com/en-US/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2).<br /><br />Usare le istruzioni in questo articolo per mantenersi aggiornati sulle modifiche apportate a queste informazioni tramite la sottoscrizione a un feed RSS.<br /><br />Oltre alle informazioni nell'articolo di Office, le istruzioni seguenti sono specifiche per Azure Information Protection:<br /><br />- Consentire il traffico HTTPS sulla porta TCP 443 per **api.informationprotection.azure.com**.<br /><br />- Non terminare la connessione TLS dal client al servizio, ad esempio per il controllo a livello di pacchetti. In questo modo viene interrotta l'associazione del certificato usata dai client RMS con le autorità di certificazione gestite da Microsoft per la protezione delle comunicazioni con Azure RMS.<br /><br />- Se si usa un proxy Web che richiede l'autenticazione, è necessario configurarlo per l'uso dell'autenticazione integrata di Windows con le credenziali di accesso di Active Directory dell'utente.|

Se si vuole usare il servizio Azure Rights Management di Azure Information Protection con server locali, sono supportati i prodotti seguenti:

-   Exchange Server

-   SharePoint Server

-   File server di Windows Server che supportano la funzionalità Infrastruttura di classificazione file

Per informazioni sui requisiti aggiuntivi per questo scenario, vedere [Server locali che supportano la protezione dati di Azure Rights Management](requirements-servers.md).

> [!IMPORTANT]
> Lo scenario di distribuzione seguente non è supportato, a meno che non si usi la protezione di AD RMS con Azure Information Protection (configurazione "hold your own key" o HYOK):
> 
> -   Esecuzione side-by-side di AD RMS e di Azure RMS nella stessa organizzazione, tranne che durante la migrazione, come descritto in [Migrazione da AD RMS ad Azure Information Protection](../plan-design/migrate-from-ad-rms-to-azure-rms.md).
> 
> È disponibile un percorso di migrazione supportato [da AD RMS ad Azure Information Protection](http://technet.microsoft.com/library/Dn858447.aspx) e da [Azure Information Protection ad AD RMS](/powershell/module/aadrm/Set-AadrmMigrationUrl). Se si distribuisce Azure Information Protection e poi si decide di interrompere l'uso del servizio cloud, vedere [Rimozione delle autorizzazioni e disattivazione di Azure Information Protection](../deploy-use/decommission-deactivate.md).

[!INCLUDE[Commenting house rules](../includes/houserules.md)]


