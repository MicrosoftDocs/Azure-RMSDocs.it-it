---
title: Client | Azure Information Protection
description: Microsoft Azure Information Protection offre una soluzione client-server che consente di proteggere i dati di un&quot;organizzazione. Il client (di Azure Information Protection o di Rights Management) si integra con le applicazioni che vengono eseguite su computer e dispositivi mobili.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 09/25/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: a6fa85be-f92a-4e00-9efc-9dbfd4dfbfcb
ROBOTS: noindex,nofollow
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 9d8354f2d68f211d349226970fd2f83dd0ce810b
ms.openlocfilehash: 70f10569884811b0b8dfab9b138399720ff48267


---

# <a name="the-client-side-of-azure-information-protection"></a>Lato client di Azure Information Protection

>*Si applica a: Active Directory Rights Management Services, Azure Rights Management, Windows 10, Windows 7 con SP1, Windows 8, Windows 8.1*

Azure Information Protection offre una soluzione client-server che consente di proteggere i documenti e i messaggi di posta elettronica di un'organizzazione:

- Il client, che può essere di Azure Information Protection o di Rights Management, si integra con le applicazioni che vengono eseguite su computer e dispositivi mobili. 

- Il servizio risiede nel cloud (Azure Information Protection, che usa il servizio Azure Rights Management per la protezione dei dati) o in locale (Active Directory Rights Management Services). 

Il client di Azure Information Protection supporta funzionalità di classificazione e assegnazione di etichette, oltre alla protezione. Questo client si integra con le applicazioni di Office e deve essere installato separatamente.

Il client di Rights Management (RMS) viene installato automaticamente con alcune applicazioni, ad esempio le applicazioni di Office, l'applicazione RMS sharing e le applicazioni con il supporto predefinito per RMS dei fornitori di software. È possibile tuttavia installarlo anche separatamente, ad esempio in scenari in cui gli sviluppatori vogliono integrare la protezione Rights Management nelle applicazioni line-of-business e gli amministratori o gli utenti esperti vogliono proteggere i file in blocco usando lo strumento di protezione RMS.

Per altre informazioni sulla distribuzione e sull'uso di questi client, che possono essere usati con Azure Information Protection e Active Directory Rights Management Services per la protezione dei dati dell'organizzazione, fare riferimento alla documentazione seguente:

- [Installazione del client di Azure Information Protection](info-protect-client.md)

- [Note sulla distribuzione del client RMS](client-deployment-notes.md)

- [Protezione RMS con l'infrastruttura di classificazione file (FCI, File Classification Infrastructure) per Windows Server](configure-fci.md)

- [Applicazione Rights Management sharing per Windows](sharing-app-windows.md)


## <a name="see-also"></a>Vedere anche
[Confronto tra Azure Information Protection e AD RMS](../understand-explore/compare-azure-rms-ad-rms.md)



<!--HONumber=Nov16_HO2-->


