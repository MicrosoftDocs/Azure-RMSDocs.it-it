---
title: Concetti - etichetta dei metadati in MIP SDK
description: Questo articolo aiuterà a comprendere i metadati che viene generato per il SDK di Microsoft Information Protection.
author: tommoser
ms.service: information-protection
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.date: 11/08/2018
ms.author: tommos
ms.openlocfilehash: 990f729edaa0a2e212812f84fc5a4c63f82e37fb
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/14/2019
ms.locfileid: "56253970"
---
# <a name="microsoft-information-protection-sdk---metadata"></a>Microsoft Information Protection SDK - Metadata

il SDK di Microsoft Information Protection genera il set di metadati che devono essere applicato a un file. Questi metadati sono una rappresentazione in forma dell'etichetta. Questo documento descrive i metadati che SDK genera per applicare a posta elettronica, documenti e altri record.

## <a name="labels"></a>Etichette

Le etichette nel SDK di Microsoft Information Protection sono applicate alle informazioni per descrivere la riservatezza delle informazioni. Dati etichetta vengono salvati in file o un record in un set di coppie chiave-valore che descrivono l'etichetta. Il nome dei metadati si basa la struttura seguente:

`DefinedPrefix_ElementType_GlobalIdentifier_AttributeName`

Quando applicato ai dati etichettati con Microsoft Information Protection, il risultato è:

`MSIP_Label_GUID_Enabled = true`

Il GUID è un identificatore univoco per ogni etichetta in un'organizzazione.

## <a name="microsoft-information-protection-sdk-metadata"></a>Microsoft Information Protection SDK Metadata

il SDK di MIP si applica il seguente set di metadati.

| Attributo | Tipo o valore                 | Descrizione                                                                                                                                                                                                                                        | obbligatorio |
|-----------|-------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------|
| **Enabled**   | True o False                 | Questo attributo indica se la classificazione rappresentata da questo set di coppie chiave-valore è abilitata per l'elemento di dati. In genere, i prodotti DLP convalidare l'esistenza di questa chiave per identificare l'etichetta di classificazione. | Yes       |
| **SiteId**    | GUID                          | ID Tenant di Azure Active Directory                                                                                                                                                                                                                   | Yes       |
| **ActionId**  | GUID                          | Elemento ActionID viene modificato ogni volta che viene impostata un'etichetta. I log di controllo includeranno actionID vecchi e nuovi per consentire il concatenamento di attività all'elemento di dati l'assegnazione di etichette.                                                                                 | Yes       |
| **Metodo**    | Standard, Privileged, o automaticamente        | Viene impostato tramite assignmentmethod                                                                                                                                                                                                                 | No        |
| **SetDate**   | Formato di data estesa ISO 8601 | Timestamp quando è stata impostata l'etichetta.                                                                                                                                                                                                              | No        |
| **Name**      | string                        | Nome univoco dell'etichetta all'interno del tenant. Non corrisponde necessariamente per nome visualizzato.                                                                                                                                                              | No      |
| **ContentBits** | integer | Maschera di bit che descrive i tipi di contenuto contrassegno che deve essere applicato a un file. CONTENT_HEADER = 0X1, CONTENT_FOOTER = 0X2, WATERMARK = 0X4
 | No |

Quando applicato a un file, il risultato è simile alla tabella riportata di seguito.

| Chiave                                                         | Valore                                |
|-------------------------------------------------------------|--------------------------------------|
| MSIP_Label_2096f6a2-d2f7-48be-b329-b73aaa526e5d_Enabled     | true                                 |
| MSIP_Label_2096f6a2-d2f7-48be-b329-b73aaa526e5d_SetDate     | 2018-11-08T21:13:16-0800             |
| MSIP_Label_2096f6a2-d2f7-48be-b329-b73aaa526e5d_Method      | Con privilegi                           |
| MSIP_Label_2096f6a2-d2f7-48be-b329-b73aaa526e5d_Name        | Confidential (Riservato)                         |
| MSIP_Label_2096f6a2-d2f7-48be-b329-b73aaa526e5d_SiteId      | cb46c030-1825-4e81-a295-151c039dbf02 |
| MSIP_Label_2096f6a2-d2f7-48be-b329-b73aaa526e5d_ContentBits | 2                                    |
| MSIP_Label_2096f6a2-d2f7-48be-b329-b73aaa526e5d_ActionId    | 88124cf5-1340-457d-90e1-0000a9427c99 |

## <a name="extending-metadata-with-custom-attributes"></a>Estensione di metadati con gli attributi personalizzati

Metadati personalizzati possono essere aggiunti tramite il File e dei criteri API. Gli attributi personalizzati devono mantenere la base `MSIP_Label_GUID` prefisso. 

Ad esempio, un'applicazione scritta per Contoso Corporation necessario applicare i metadati che indica quale sistema generato un file con etichettato. L'applicazione può creare una nuova etichetta, il prefisso `MSIP_Label_GUID`. Il nome del fornitore del software e attributi personalizzati vengono accodati come prefisso per generare metadati personalizzati.

```
MSIP_Label_f048e7b8-f3aa-4857-bf32-a317f4bc3f29_ContosoCorp_GeneratedBy = HRReportingSystem
```

> [!Note]
> Per garantire la compatibilità tra applicazioni comuni, la lunghezza massima della ognuno una chiave e il valore è di 255 caratteri.

## <a name="versioning"></a>Controllo versioni

Nel corso del tempo, gli attributi saranno introdotte, modificati o ritirati. Tuttavia, è necessario che le applicazioni continueranno a gestire questi precedente o ritirati attributi, come sostituire il valore in un'organizzazione potrebbero richiedere anni.

Quando si sostituisce un attributo con una versione più recente, un suffisso di versione deve essere aggiunto all'attributo:

`MSIP_Label_GUID_EnabledV2 = True | False | Condition`

## <a name="email"></a>Posta elettronica

Metadati applicati alla posta elettronica viene mantenuta una coppia chiave/valore di formato simile a quella dei documenti. La differenza principale è che tutti gli attributi vengono serializzati a un'intestazione di messaggio di posta elettronica singolo chiamata **MSIP_Labels**. Le coppie chiave/valore sono delimitate da punto e virgola e uno spazio vuoto e inserite nella nuova intestazione.

Utilizzando i metadati di esempio precedenti:

```
MSIP_Labels: MSIP_Label_2096f6a2-d2f7-48be-b329-b73aaa526e5d_Enabled=true; MSIP_Label_2096f6a2-d2f7-48be-b329-b73aaa526e5d_SetDate=2018-11-08T21:13:16-0800; MSIP_Label_2096f6a2-d2f7-48be-b329-b73aaa526e5d_Method=Privileged; MSIP_Label_2096f6a2-d2f7-48be-b329-b73aaa526e5d_Name=Confidential; MSIP_Label_2096f6a2-d2f7-48be-b329-b73aaa526e5d_SiteId=cb46c030-1825-4e81-a295-151c039dbf02; MSIP_Label_2096f6a2-d2f7-48be-b329-b73aaa526e5d_ContentBits=2; MSIP_Label_2096f6a2-d2f7-48be-b329-b73aaa526e5d_ActionId=88124cf5-1340-457d-90e1-0000a9427c99
```
