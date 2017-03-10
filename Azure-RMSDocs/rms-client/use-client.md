---
title: Client per Azure Information Protection
description: Microsoft Azure Information Protection offre una soluzione client-server che consente di proteggere i dati di un&quot;organizzazione. Il client (di Azure Information Protection o di Rights Management) si integra con le applicazioni che vengono eseguite su computer e dispositivi mobili.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/08/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: a6fa85be-f92a-4e00-9efc-9dbfd4dfbfcb
ROBOTS: noindex,nofollow
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: cee5b0499a434894e284d4cc8157af962ade99cb
ms.sourcegitcommit: 31e128cc1b917bf767987f0b2144b7f3b6288f2e
translationtype: HT
---
# <a name="the-client-side-of-azure-information-protection"></a>Lato client di Azure Information Protection

>*Si applica a: Active Directory Rights Management Services, Azure Rights Management, Windows 10, Windows 8.1, Windows 8, Windows 7 con SP1*

Azure Information Protection offre una soluzione client-server che consente di proteggere i documenti e i messaggi di posta elettronica di un'organizzazione:

- Il client, che può essere di Azure Information Protection o di Rights Management, si integra con le applicazioni che vengono eseguite su computer e dispositivi mobili. 

- Il servizio risiede nel cloud (Azure Information Protection, che usa il servizio Azure Rights Management per la protezione dei dati) o in locale (Active Directory Rights Management Services). 

Il client di Azure Information Protection supporta funzionalità di classificazione e assegnazione di etichette, oltre alla protezione. Questo client si integra con le applicazioni di Office e deve essere installato separatamente.

Il client Rights Management (RMS) viene installato automaticamente con alcune applicazioni, ad esempio le applicazioni di Office, il client Azure Information Protection e applicazioni RMS a cura di fornitori software. È tuttavia possibile installarlo anche separatamente, ad esempio in scenari in cui gli sviluppatori vogliono integrare la protezione di Rights Management in applicazioni line-of-business.

Per altre informazioni sulla distribuzione e sull'uso di questi client, che possono essere usati con Azure Information Protection e Active Directory Rights Management Services per la protezione dei dati dell'organizzazione, fare riferimento alla documentazione seguente:

- [Client di Azure Information Protection](AIP-client.md)

- [Note sulla distribuzione del client RMS](client-deployment-notes.md)

- [Protezione RMS con l'infrastruttura di classificazione file (FCI, File Classification Infrastructure) per Windows Server](configure-fci.md)

- [Applicazione di condivisione Rights Management per Windows](sharing-app-windows.md)

L'applicazione di condivisione Rights Management per Windows e lo strumento di protezione RMS sono stati sostituiti dal client Azure Information Protection. 


## <a name="see-also"></a>Vedere anche
[Confronto tra Azure Information Protection e AD RMS](../understand-explore/compare-azure-rms-ad-rms.md)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]