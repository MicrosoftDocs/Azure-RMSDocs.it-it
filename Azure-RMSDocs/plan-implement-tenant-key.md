---
title: Chiave del tenant di Azure Information Protection
description: Anziché Microsoft gestire la chiave radice per Azure Information Protection, è possibile creare e gestire questa chiave (denominata "Bring your own key" o BYOK) per il tenant, per conformarsi a normative specifiche.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 07/14/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: f0d33c5f-a6a6-44a1-bdec-5be1bc8e1e14
ms.subservice: kms
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 35c898ded852970e380c8061ba8f97d040860017
ms.sourcegitcommit: 8a141858e494dd1d3e48831e6cd5a5be48ac00d2
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2020
ms.locfileid: "97386390"
---
# <a name="planning-and-implementing-your-azure-information-protection-tenant-key"></a>Pianificazione e implementazione della chiave del tenant di Azure Information Protection

>***Si applica a**: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*
>
>***Pertinente per**: [AIP Unified Labeling client e client classico](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

>[!NOTE] 
> Per offrire un'esperienza utente unificata e semplificata, **Azure Information Protection** la gestione classica di client e **etichette** nel portale di Azure verrà **deprecata** a partire dal **31 marzo 2021**. In questo intervallo di tempo tutti i clienti correnti di Azure Information Protection possono passare alla soluzione di etichettatura unificata usando la piattaforma di etichettatura unificata di Microsoft Information Protection. Altre informazioni nell'[avviso ufficiale sulla deprecazione](https://aka.ms/aipclassicsunset).

La chiave del tenant di Azure Information Protection è una chiave radice per l'organizzazione. È possibile derivare altre chiavi da questa chiave radice, inclusi chiavi utente, chiavi computer o chiavi di crittografia del documento. Ogni volta che Azure Information Protection usa queste chiavi per l'organizzazione, vengono concatenate in modo crittografico alla chiave del tenant Azure Information Protection radice.

Oltre alla chiave radice del tenant, è possibile che l'organizzazione richieda una sicurezza locale per documenti specifici. La protezione della chiave locale è in genere necessaria solo per una piccola quantità di contenuto e pertanto viene configurata insieme a una chiave radice del tenant.

## <a name="azure-information-protection-key-types"></a>Tipi di chiavi di Azure Information Protection

La chiave radice del tenant può essere:

- [Generato da Microsoft](#tenant-root-keys-generated-by-microsoft)
- Generato dai clienti con la protezione [Bring your own key (BYOK)](#bring-your-own-key-byok-protection) .

Se si dispone di contenuto altamente sensibile che richiede una protezione aggiuntiva locale, è consigliabile usare la [crittografia a chiave doppia (DKE)](#double-key-encryption-dke).

> [!TIP]
> Se si usa il client classico e si necessita di una protezione aggiuntiva locale, usare invece [HYOK (Mantieni la propria chiave)](#hold-your-own-key-hyok) .
>

## <a name="tenant-root-keys-generated-by-microsoft"></a>Chiavi radice del tenant generate da Microsoft

La chiave predefinita, generata automaticamente da Microsoft, è la chiave predefinita usata esclusivamente per Azure Information Protection per gestire la maggior parte degli aspetti del ciclo di vita della chiave del tenant.

Continuare a usare la chiave Microsoft predefinita quando si vuole distribuire Azure Information Protection rapidamente e senza hardware speciale, software o una sottoscrizione di Azure. Gli esempi includono ambienti di testing o organizzazioni senza requisiti normativi per la gestione delle chiavi.

Per la chiave predefinita, non sono necessari altri passaggi ed è possibile passare direttamente a Introduzione alla [chiave radice del tenant](get-started-tenant-root-keys.md).

> [!NOTE]
> La chiave predefinita generata da Microsoft è l'opzione più semplice con il sovraccarico amministrativo più basso.
>
> Nella maggior parte dei casi, è possibile che non si disponga di una chiave del tenant, in quanto è possibile iscriversi a Azure Information Protection e il resto del processo di gestione delle chiavi è gestito da Microsoft.

## <a name="bring-your-own-key-byok-protection"></a>Protezione Bring Your Own Key (BYOK)

BYOK-Protection usa le chiavi create dai clienti, sia nel Azure Key Vault che in locale nell'organizzazione del cliente. Queste chiavi vengono quindi trasferite a Azure Key Vault per una gestione aggiuntiva.

Usare BYOK quando l'organizzazione dispone di normative di conformità per la generazione di chiavi, incluso il controllo su tutte le operazioni del ciclo di vita. Ad esempio, quando la chiave deve essere protetta da un modulo di protezione hardware.

Per altre informazioni, vedere [Configure BYOK Protection](byok-price-restrictions.md). 

Una volta configurata, continuare [con l'introduzione alla chiave radice del tenant](get-started-tenant-root-keys.md) per altre informazioni sull'uso e sulla gestione della chiave.

## <a name="double-key-encryption-dke"></a>Crittografia a chiave doppia (DKE)

**Pertinente per**: AIP Unified Labeling solo client

La protezione DKE offre una maggiore sicurezza per i contenuti usando due chiavi: una creata e conservata da Microsoft in Azure e un'altra creata e mantenuta in locale dal cliente.

DKE richiede entrambe le chiavi per accedere al contenuto protetto, assicurando che Microsoft e altre terze parti non possano mai accedere ai dati protetti autonomamente.

DKE può essere distribuito nel cloud o in locale, garantendo una flessibilità completa per i percorsi di archiviazione.

Usare DKE quando l'organizzazione:

- Si vuole assicurare che solo gli utenti possano decrittografare il contenuto protetto, in tutte le circostanze.
- Non si vuole che Microsoft abbia accesso ai dati protetti autonomamente.
- Dispone di requisiti normativi per mantenere le chiavi all'interno di un confine geografico. Con DKE, le chiavi detenute dal cliente vengono mantenute all'interno del data center del cliente.

> [!NOTE]
> DKE è simile a una cassetta di sicurezza che richiede l'accesso sia a una chiave della banca che a una chiave del cliente.
> DKE-Protection richiede che sia la chiave di Microsoft e la chiave posseduta dal cliente per decrittografare il contenuto protetto.

Per ulteriori informazioni, vedere [crittografia a chiave doppia](/microsoft-365/compliance/double-key-encryption) nella documentazione di Microsoft 365.

## <a name="hold-your-own-key-hyok"></a>Mantieni la tua chiave (HYOK)

**Pertinente per**: solo client di AIP classico

HYOK-Protection usa una chiave creata e mantenuta dai clienti, in una località isolata dal cloud. Poiché HYOK-Protection consente solo l'accesso ai dati per le applicazioni e i servizi locali, i clienti che usano HYOK hanno anche una chiave basata sul cloud per i documenti cloud.

Usare HYOK per i documenti:

- Limitato a poche persone
- Non condiviso all'esterno dell'organizzazione
- Vengono utilizzati solo nella rete interna.

Questi documenti in genere hanno la classificazione più alta nell'organizzazione, come "Top Secret".

Il contenuto può essere crittografato con la protezione HYOK solo se si dispone del client classico. Tuttavia, se si dispone di contenuto protetto da HYOK, può essere visualizzato sia nel client di etichettatura classico che in quello unificato.  

Per ulteriori informazioni, vedere la pagina relativa ai [Dettagli HYOK](configure-adrms-restrictions.md).

