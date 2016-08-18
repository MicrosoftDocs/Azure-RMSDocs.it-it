---
title: Requisiti per Azure Rights Management | Azure RMS
description: 
keywords: 
author: cabailey
manager: mbaldwin
ms.date: 07/15/2016
ms.topic: get-started-article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: dc78321d-d759-4653-8818-80da74b6cdeb
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 2fab331a26e18730e9cc64a24c0501b7ae21aa1b
ms.openlocfilehash: f225d8579e2440d2eb00a4f821a78727b6442fdd


---

# Requisiti per Azure Rights Management

*Si applica a: Azure Rights Management, Office 365*


Per distribuire Microsoft Azure Rights Management (Azure RMS) nell'organizzazione, assicurarsi di disporre dei prerequisiti seguenti. Per distribuire Rights Management per l'organizzazione, usare la [guida di orientamento per la distribuzione di Azure Rights Management](../plan-design/deployment-roadmap.md).

|Requisito|Altre informazioni|
|---------------|--------------------|
|Sottoscrizione cloud per RMS|L'organizzazione deve avere una sottoscrizione cloud che supporti RMS.<br /><br />Per informazioni sulle licenze, vedere l'articolo relativo alle [sottoscrizioni cloud che supportano Azure RMS](requirements-subscriptions.md).|
|Directory di Azure AD|Per supportare l'autenticazione utente per RMS, l'organizzazione deve disporre di una directory di Azure AD. Inoltre, se si vuole usare gli account utente dalla directory locale (AD DS), è necessario anche configurare l'integrazione delle directory.<br /><br />Multi-Factor Authentication (MFA) è supportato in Azure RMS quando si ha il software client richiesto e l'infrastruttura di supporto MFA è configurata correttamente.<br /><br />Per altre informazioni, vedere [Directory di Azure AD](requirements-azure-ad.md).|
|Dispositivi client|Gli utenti devono avere dispositivi client, quali computer o dispositivi mobili, che eseguono un sistema operativo che supporta RMS.<br /><br />Per altre informazioni, vedere [Dispositivi client che supportano Azure RMS](requirements-client-devices.md).|
|Applicazioni|Le applicazioni eseguite dagli utenti devono supportare RMS.<br /><br />Per altre informazioni, vedere la pagina relativa alle [applicazioni che supportano Azure RMS](requirements-applications.md).|
|Infrastruttura in grado di supportare la connettività a Internet e ai servizi cloud dipendenti.|Se è presente un firewall o dispositivi di rete di protezione simili che devono essere configurati per consentire connessioni specifiche, vedere le informazioni relative ad **Azure Rights Management (RMS)** nella sezione [Portale e condivisione di Office 365](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2#BKMK_Portal-identity) dell'articolo [URL e intervalli di indirizzi IP per Office 365](https://support.office.com/en-US/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2).<br /><br />Usare le istruzioni in questo articolo per mantenersi aggiornati sulle modifiche apportate a queste informazioni tramite la sottoscrizione a un feed RSS.<br /><br />Oltre alle informazioni nell'articolo di Office, specifiche per Azure RMS:<br /><br />- Non terminare la connessione TLS dal client al servizio, ad esempio per il controllo a livello di pacchetti. In questo modo viene interrotta l'associazione del certificato usata dai client RMS con le autorità di certificazione gestite da Microsoft per la protezione delle comunicazioni con Azure RMS.<br /><br />- Se si usa un proxy Web che richiede l'autenticazione, è necessario configurarlo per l'uso dell'autenticazione integrata di Windows con le credenziali di accesso di Active Directory dell'utente.|

Se si vuole usare RMS con server locali, sono supportati i prodotti seguenti:

-   Exchange Server

-   SharePoint Server

-   File server di Windows Server che supportano la funzionalità Infrastruttura di classificazione file

Per informazioni sui requisiti aggiuntivi di Azure RMS per questo scenario, vedere [Server locali che supportano Azure RMS](requirements-servers.md).

> [!IMPORTANT]
> Lo scenario di distribuzione seguente non è supportato:
> 
> -   Esecuzione side-by-side di AD RMS e di Azure RMS nella stessa organizzazione, tranne che durante la migrazione, come descritto in [Migrazione da AD RMS ad Azure Rights Management](../plan-design/migrate-from-ad-rms-to-azure-rms.md).
> 
> È disponibile un percorso di migrazione supportato [da AD RMS ad Azure RMS](http://technet.microsoft.com/library/Dn858447.aspx) e [da Azure RMS ad AD RMS](http://msdn.microsoft.com/library/azure/dn629429.aspx). Se si distribuisce Azure RMS e poi si decide di interrompere l'uso di servizio cloud, vedere [Rimozione delle autorizzazioni e disattivazione di Azure Rights Management](../deploy-use/decommission-deactivate.md).






<!--HONumber=Jul16_HO3-->


