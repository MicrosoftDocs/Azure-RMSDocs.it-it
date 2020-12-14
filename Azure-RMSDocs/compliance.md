---
title: Conformità e supporto per Azure Information Protection
description: Informazioni di supporto per Azure Information Protection che includono note legali, informazioni sulla conformità e contratti di servizio.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 12/08/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: b3a7127b-6d24-4439-bc4e-2a0a325e8ea3
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: d3de605c8427745e51df2ea1ffbee110c9106138
ms.sourcegitcommit: 8a141858e494dd1d3e48831e6cd5a5be48ac00d2
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2020
ms.locfileid: "97383888"
---
# <a name="compliance-and-supporting-information-for-azure-information-protection"></a>Informazioni su conformità e supporto per Azure Information Protection

>***Si applica a**: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*
>
>***Pertinente per**: [AIP Unified Labeling client e client classico](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

>[!NOTE] 
> Per offrire un'esperienza utente unificata e semplificata, **Azure Information Protection** la gestione classica di client e **etichette** nel portale di Azure verrà **deprecata** a partire dal **31 marzo 2021**. In questo intervallo di tempo tutti i clienti correnti di Azure Information Protection possono passare alla soluzione di etichettatura unificata usando la piattaforma di etichettatura unificata di Microsoft Information Protection. Altre informazioni nell'[avviso ufficiale sulla deprecazione](https://aka.ms/aipclassicsunset).

Azure Information Protection supporta altri servizi e si basa anche su altri servizi. Per informazioni correlate ad Azure Information Protection, ma non riferite alla modalità d'uso del servizio Azure Information Protection, esaminare le risorse seguenti:

## <a name="suitability-for-different-countries"></a>Idoneità per paesi diversi

Tenendo conto della variabilità di leggi e regolamenti nei diversi paesi, così come dei differenti casi d'uso e scenari e dei requisiti variabili a seconda del settore, sarà necessario rivolgersi al consulente legale di fiducia per appurare se Azure Information Protection è una soluzione appropriata per il proprio paese.

Tuttavia, alcune informazioni rilevanti possono essere utili al consulente legale per giungere a una decisione:

- Azure Information Protection usa AES 256 e AES 128 per crittografare i documenti. [Altre informazioni](./how-does-it-work.md#cryptographic-controls-used-by-azure-rms-algorithms-and-key-lengths)

- Tutte le chiavi di crittografia usate da Azure Information Protection sono protette con una chiave radice specifica del cliente che usa RSA 2048 bit. È supportato anche RSA 1024 per compatibilità con versioni precedenti. [Altre informazioni](./how-does-it-work.md#cryptographic-controls-used-by-azure-rms-algorithms-and-key-lengths)

- Le chiavi radice specifiche del cliente sono gestite da Microsoft o sottoposte a provisioning da parte del cliente in un modulo di protezione hardware nCipher usando "Bring your own key" (BYOK). Azure Information Protection supporta anche le funzionalità per la protezione locale, per il contenuto che non può essere protetto con una chiave basata sul cloud. Per altre informazioni, vedere [Planning and implementing your Azure Information Protection tenant key](plan-implement-tenant-key.md) (Pianificazione e implementazione della chiave del tenant Azure Information Protection).

- Il servizio Azure Information Protection è ospitato in data center regionali in tutto il mondo. Le chiavi e i criteri di Azure Information Protection rimangono sempre nell'area di distribuzione originale.

    > [!NOTE]
    > I criteri di Azure Information Protection sono rilevanti solo per il client AIP classico.
    >
  
- Azure Information Protection non trasmette contenuto dei documenti dai client al servizio Azure Information Protection. Le operazioni di crittografia e decrittografia del contenuto vengono eseguite sul posto nel dispositivo client. Per il rendering basato su servizi, invece, le operazioni vengono eseguite all'interno del servizio che esegue il rendering del contenuto. [Altre informazioni](./how-does-it-work.md)

## <a name="legal-and-privacy"></a>Note legali e privacy

- Per informazioni sul contratto di Microsoft Azure: [Contratto di Microsoft Azure](https://azure.microsoft.com/support/legal/subscription-agreement/)

- Per informazioni sulla privacy di Microsoft Azure: [Informativa sulla privacy di Microsoft Azure](https://azure.microsoft.com/support/legal/privacy-statement/)

## <a name="security-compliance-and-auditing"></a>Sicurezza, conformità e controllo

Vedere la sezione [Requisiti di sicurezza, conformità e normativi](./what-is-azure-rms.md#security-compliance-and-regulatory-requirements) dell'articolo [Problemi risolti da Azure RMS](./what-is-azure-rms.md#business-problems-solved-by-azure-rights-management) per informazioni sulle certificazioni specifiche per il servizio di Azure Rights Management. Inoltre:

- Per le certificazioni esterne per Azure Information Protection: [Centro protezione di Microsoft Azure](https://azure.microsoft.com/support/trust-center/)

- Per informazioni su FIPS 140: [Convalida di FIPS 140](/windows/security/threat-protection/fips-140-validation)

Per informazioni tecniche approfondite sul funzionamento della tecnologia di protezione, vedere [Funzionamento di Azure RMS:](./how-does-it-work.md) 

## <a name="service-level-agreements"></a>Contratti di servizio

- [Contratto di servizio per Azure Information Protection](https://azure.microsoft.com/support/legal/sla/information-protection/v1_0/)

- [Contratto di servizio per Azure Active Directory](https://azure.microsoft.com/support/legal/sla/active-directory/v1_0/)

- [Contratto di servizio per Azure Key Vault](https://azure.microsoft.com/support/legal/sla/key-vault/v1_0/)

## <a name="documentation"></a>Documentazione

- Documentazione di Azure Active Directory: [Azure Active Directory](/azure/active-directory/fundamentals/active-directory-whatis)

- Documentazione di Microsoft 365: [Microsoft 365 per la documentazione e le risorse aziendali](/Office365/Enterprise/)

