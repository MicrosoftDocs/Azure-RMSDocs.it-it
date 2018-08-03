---
title: Conformità e supporto per Azure Information Protection
description: Informazioni di supporto per Azure Information Protection che includono note legali, informazioni sulla conformità e contratti di servizio.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 03/12/2018
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: b3a7127b-6d24-4439-bc4e-2a0a325e8ea3
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 1e4db3996a201909fcf861a4190cbe6647a7326c
ms.sourcegitcommit: 949bf02d5d12bef8e26d89ad5d6a0d5cc7826135
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/02/2018
ms.locfileid: "39474618"
---
# <a name="compliance-and-supporting-information-for-azure-information-protection"></a>Informazioni su conformità e supporto per Azure Information Protection

Azure Information Protection supporta altri servizi e si basa anche su altri servizi. Per informazioni correlate ad Azure Information Protection, ma non riferite alla modalità d'uso del servizio Azure Information Protection, esaminare le risorse seguenti:

## <a name="suitability-for-different-countries"></a>Idoneità per paesi diversi

Tenendo conto della variabilità di leggi e regolamenti nei diversi paesi, così come dei differenti casi d'uso e scenari e dei requisiti variabili a seconda del settore, sarà necessario rivolgersi al consulente legale di fiducia per appurare se Azure Information Protection è una soluzione appropriata per il proprio paese.

Tuttavia, alcune informazioni rilevanti possono essere utili al consulente legale per giungere a una decisione:

- Azure Information Protection usa AES 256 e AES 128 per crittografare i documenti. [Altre informazioni](./how-does-it-work.md#cryptographic-controls-used-by-azure-rms-algorithms-and-key-lengths)

- Tutte le chiavi di crittografia usate da Azure Information Protection sono protette con una chiave radice specifica del cliente che usa RSA 2048 bit. È comunque supportato anche RSA 1024 per compatibilità con versioni precedenti. [Altre informazioni](./how-does-it-work.md#cryptographic-controls-used-by-azure-rms-algorithms-and-key-lengths)

- Le chiavi radice specifiche del cliente sono gestite da Microsoft o ne viene eseguito il provisioning dal cliente in un modulo di protezione hardware Thales in base al modello "[Bring Your Own Key](./plan-design/plan-implement-tenant-key.md)" (BYOK). Azure Information Protection supporta anche funzionalità limitate con una chiave locale usando il modello "[Hold Your Own Key](./deploy-use/configure-adrms-restrictions.md)" (HYOK) per il contenuto a cui si applicano requisiti che indicano che non deve essere protetto con un chiave basata sul cloud.

- Il servizio Azure Information Protection è ospitato in data center regionali in tutto il mondo. Le chiavi e i criteri di Azure Information Protection rimangono sempre nell'area di distribuzione originale.
 
- Azure Information Protection non trasmette contenuto dei documenti dai client al servizio Azure Information Protection. Le operazioni di crittografia e decrittografia del contenuto vengono eseguite sul posto nel dispositivo client. Per il rendering basato su servizi, invece, le operazioni vengono eseguite all'interno del servizio che esegue il rendering del contenuto. [Altre informazioni](./how-does-it-work.md)

## <a name="legal-and-privacy"></a>Note legali e privacy

- Per informazioni sul contratto di Microsoft Azure: [Contratto di Microsoft Azure](http://azure.microsoft.com/support/legal/subscription-agreement/)

- Per informazioni sulla privacy di Microsoft Azure: [Informativa sulla privacy di Microsoft Azure](http://azure.microsoft.com/support/legal/privacy-statement/)

## <a name="security-compliance-and-auditing"></a>Sicurezza, conformità e controllo

Vedere la sezione [Requisiti di sicurezza, conformità e normativi](./azure-rms-problems-it-solves.md#security-compliance-and-regulatory-requirements) dell'articolo [Problemi risolti da Azure RMS](./azure-rms-problems-it-solves.md) per informazioni sulle certificazioni specifiche per il servizio di Azure Rights Management. Inoltre:

- Per le certificazioni esterne per Azure Information Protection: [Centro protezione di Microsoft Azure](http://azure.microsoft.com/support/trust-center/)

- Per informazioni su FIPS 140: [Convalida di FIPS 140](https://technet.microsoft.com/library/security/cc750357.aspx)

Per informazioni tecniche approfondite sul funzionamento della tecnologia di protezione, vedere [Funzionamento di Azure RMS:](./how-does-it-work.md) 

## <a name="service-level-agreements"></a>Contratti di servizio

- [Contratto di servizio per Azure Information Protection](https://azure.microsoft.com/support/legal/sla/information-protection/v1_0/)

- [Contratto di servizio per Azure Active Directory](https://azure.microsoft.com/support/legal/sla/active-directory/v1_0/)

- [Contratto di servizio per Azure Key Vault](https://azure.microsoft.com/support/legal/sla/key-vault/v1_0/)

## <a name="documentation"></a>Documentazione

- Documentazione di Azure Active Directory: [Azure Active Directory](/active-directory/)

- Libreria di Office 365: [Office 365](http://technet.microsoft.com/library/dn127064%28v=office.14%29.aspx)

