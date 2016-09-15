---
title: Requisiti per Azure Information Protection | Azure RMS
description: Identificare i prerequisiti necessari per valutare la versione di anteprima di Azure Information Protection.
author: cabailey
manager: mbaldwin
ms.date: 08/29/2016
ms.topic: get-started-article
ms.prod: 
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: aa4353e5-c5b0-47f6-a6f9-87d13e8f075f
ms.reviewer: eymanor
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: ba6887a5c9bab18867d07cfc98e8416bf102c211
ms.openlocfilehash: 85bed6554140525fabc1ab863e3196ac5a37366b


---

# Requisiti per Azure Information Protection

>*Si applica a: Azure Information Protection (anteprima)*

**[ Informazioni preliminari soggette a modifiche. ]**

Per valutare la versione di anteprima di Azure Information Protection, assicurarsi di soddisfare i prerequisiti seguenti. 

|Requisito|Altre informazioni|
|---------------|--------------------|
|Una sottoscrizione di Office 365 che includa Azure Rights Management|Ad esempio, una sottoscrizione di Office 365 E3, E4 o E5.<br /><br />Per altre informazioni sulle opzioni di sottoscrizione disponibili e sui collegamenti alle versioni di valutazione gratuite, vedere la sezione relativa alla [sottoscrizione di Office 365](../get-started/requirements-subscriptions.md#office-365-subscription) nella documentazione sui requisiti per Azure RMS.|
|Directory di Azure AD|Per supportare l'autenticazione utente per Azure RMS e Azure Information Protection, nell'organizzazione deve essere disponibile una directory di Azure AD. Inoltre, se si vuole usare gli account utente dalla directory locale (AD DS), è necessario anche configurare l'integrazione delle directory.<br /><br />Multi-Factor Authentication (MFA) è supportato in Azure RMS quando si ha il software client richiesto e l'infrastruttura di supporto MFA è configurata correttamente.<br /><br />Per altre informazioni, vedere [Requisiti per Azure RMS: directory di Azure AD](../get-started/requirements-azure-ad.md). Queste informazioni si applicano anche ad Azure Information Protection.|
|Dispositivi client|Per questa versione di anteprima sono supportati i dispositivi client seguenti:<br /><br />- Windows 10 (x86, x64)<br /><br />- Windows 8.1 (x86, x64)<br /><br />- Windows 8 (x86, x64)<br /><br />- Windows 7 Service Pack 1 (x86, x64)<br /><br />Quando si proteggono i dati, questi possono essere usati dagli stessi dispositivi (Windows, Mac, iOS, Android) che supportano Azure Rights Management. Per i dettagli relativi a questi dispositivi e alle versioni supportate, vedere [Requisiti per Azure RMS: dispositivi client che supportano Azure RMS](../get-started/requirements-client-devices.md).|
|Applicazioni|Con la versione di anteprima e al momento della disponibilità generale (GA, General Availability) Azure Information Protection supporterà l'assegnazione di etichette e la protezione dei file e dei messaggi di posta elettronica creati dalle applicazioni di Office **Word**, **Excel**, **PowerPoint** e **Outlook** delle famiglie di prodotti Office seguenti:<br /><br />- Office Professional Plus 2016<br /><br />- Office Professional Plus 2013 con Service Pack 1<br /><br />- Office Professional Plus 2010<br /><br />Per sapere quando Azure Information Protection supporterà altri tipi di file, ad esempio file PDF, audio, video e immagine, dopo la disponibilità generale, seguire gli annunci in [Enterprise Mobility and Security Blog](https://blogs.technet.microsoft.com/enterprisemobility/?product=azure-rights-management-services) (blog sulla mobilità e la sicurezza aziendale).|
|Infrastruttura in grado di supportare la connettività a Internet e ai servizi cloud dipendenti.|Se è presente un firewall o dispositivi di rete di protezione simili che devono essere configurati per consentire connessioni specifiche, vedere le informazioni relative ad **Azure Rights Management (RMS)** nella sezione [Portale e condivisione di Office 365](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2#BKMK_Portal-identity) dell'articolo [URL e intervalli di indirizzi IP per Office 365](https://support.office.com/en-US/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2)<br /><br />Inoltre:<br /><br />- Consentire il traffico HTTPS sulla porta TCP 443 per **api.informationprotection.azure.com**.<br /><br />- Non terminare la connessione TLS dal client al servizio, ad esempio per il controllo a livello di pacchetti. <br /><br />- Se si usa un proxy Web che richiede l'autenticazione, è necessario configurarlo per l'uso dell'autenticazione integrata di Windows con le credenziali di accesso di Active Directory dell'utente.|

## Passaggi successivi

Se si soddisfano questi requisiti, provare la demo guidata per configurare e provare Azure Information Protection in autonomia: [Esercitazione introduttiva di Azure Information Protection](infoprotect-quick-start-tutorial.md).




<!--HONumber=Aug16_HO5-->


