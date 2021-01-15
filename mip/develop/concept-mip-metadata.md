---
title: "Concetti: etichettare i metadati nell'SDK MIP"
description: Questo articolo consente di comprendere i metadati generati da Microsoft Information Protection SDK.
author: tommoser
ms.service: information-protection
ms.topic: conceptual
ms.date: 11/08/2018
ms.author: tommos
ms.openlocfilehash: 1e211cf19c5d90f4c1e6e60c808bb38d701720bf
ms.sourcegitcommit: 76926b357bbfc8772ed132ce5f2426fbea59e98b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/14/2021
ms.locfileid: "98212638"
---
# <a name="microsoft-information-protection-sdk---metadata"></a>Microsoft Information Protection SDK-metadati

Microsoft Information Protection SDK genera il set di metadati da applicare a un file. Questi metadati sono una rappresentazione dell'etichetta. Questo documento descrive i metadati generati dall'SDK da applicare alla posta elettronica, ai documenti e ad altri record.

## <a name="labels"></a>Etichette

Le etichette in Microsoft Information Protection SDK vengono applicate alle informazioni per descrivere la riservatezza delle informazioni. I dati dell'etichetta vengono salvati in modo permanente in un file o in un record in un set di coppie chiave-valore che descrivono l'etichetta. Il nome dei metadati è basato sulla struttura seguente:

`DefinedPrefix_ElementType_GlobalIdentifier_AttributeName`

Quando viene applicato ai dati contrassegnati con Microsoft Information Protection, il risultato è:

`MSIP_Label_GUID_Enabled = true`

Il GUID è un identificatore univoco per ogni etichetta in un'organizzazione.

## <a name="microsoft-information-protection-sdk-metadata"></a>Metadati di Microsoft Information Protection SDK

L'SDK MIP applica il seguente set di metadati.

| Attributo                                       | Tipo o valore                 | Descrizione                                                                                                                                                                                                                  | Obbligatorio |
| ----------------------------------------------- | ----------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------- |
| **Enabled**                                     | true o false                 | Questo attributo indica se la classificazione rappresentata da questo set di coppie chiave-valore è abilitata per l'elemento dati. In genere, i prodotti DLP convalidano l'esistenza di questa chiave per identificare l'etichetta di classificazione. | Sì       |
| **SiteId**                                      | GUID                          | ID tenant Azure Active Directory                                                                                                                                                                                             | Sì       |
| **ActionId** (rimosso in MIP SDK 1,8 e versioni successive) | GUID                          | ActionID viene modificato ogni volta che viene impostata un'etichetta. I log di controllo includeranno sia vecchi che nuovi actionID per consentire il concatenamento dell'attività di assegnazione di etichette all'elemento di dati.                                                                     | Sì       |
| **Metodo**                                      | Standard o con privilegi        | Impostare tramite [MIP:: AssignmentMethod](reference/mip-enums-and-structs.md#assignmentmethod-enum). Standard implica che l'etichetta venga applicata per impostazione predefinita o automaticamente. Privileged implica che l'etichetta è stata selezionata manualmente.  | No        |
| **SetDate**                                     | Formato data ISO 8601 esteso | Timestamp del momento in cui è stata impostata l'etichetta.                                                                                                                                                                                        | No        |
| **Nome**                                        | string                        | Etichetta nome univoco all'interno del tenant. Non corrisponde necessariamente al nome visualizzato.                                                                                                                                      | No        |
| **ContentBits**                                 | integer                       | Maschera di maschera che descrive i tipi di contrassegno del contenuto da applicare a un file. CONTENT_HEADER = 0X1, CONTENT_FOOTER = 0X2, WATERMARK = 0X4, ENCRYPT = 0x8                                                             |
| No                                              |

Quando viene applicato a un file, il risultato è simile alla tabella seguente.

| Chiave                                                         | Valore                                |
| ----------------------------------------------------------- | ------------------------------------ |
| MSIP_Label_2096f6a2-d2f7-48be-B329-b73aaa526e5d_Enabled     | true                                 |
| MSIP_Label_2096f6a2-d2f7-48be-B329-b73aaa526e5d_SetDate     | 2018-11-08T21:13:16-0800             |
| MSIP_Label_2096f6a2-d2f7-48be-B329-b73aaa526e5d_Method      | Con privilegi                           |
| MSIP_Label_2096f6a2-d2f7-48be-B329-b73aaa526e5d_Name        | Riservato                         |
| MSIP_Label_2096f6a2-d2f7-48be-B329-b73aaa526e5d_SiteId      | cb46c030-1825-4e81-a295-151c039dbf02 |
| MSIP_Label_2096f6a2-d2f7-48be-B329-b73aaa526e5d_ContentBits | 2                                    |
| MSIP_Label_2096f6a2-d2f7-48be-B329-b73aaa526e5d_ActionId    | 88124cf5-1340-457d-90e1-0000a9427c99 |

## <a name="extending-metadata-with-custom-attributes"></a>Estensione di metadati con attributi personalizzati

I metadati personalizzati possono essere accodati tramite l'API di file e criteri. Gli attributi personalizzati devono mantenere il `MSIP_Label_GUID` prefisso di base.

Ad esempio, un'applicazione scritta da Contoso Corporation deve applicare i metadati indicanti il sistema che ha generato un file con etichetta. L'applicazione può creare una nuova etichetta con prefisso `MSIP_Label_GUID` . Il nome del fornitore del software e l'attributo personalizzato vengono aggiunti al prefisso per generare i metadati personalizzati.

```
MSIP_Label_f048e7b8-f3aa-4857-bf32-a317f4bc3f29_ContosoCorp_GeneratedBy = HRReportingSystem
```

> [!Note]
> Per mantenere la compatibilità tra applicazioni comuni, la lunghezza massima per ogni chiave e un valore è di 255 caratteri.

## <a name="versioning"></a>Controllo delle versioni

Nel corso del tempo, gli attributi verranno introdotti, modificati o ritirati. Si prevede che le applicazioni continuino a gestire questi attributi obsoleti o ritirati, in quanto la sostituzione del valore in un'organizzazione potrebbe richiedere anni.

Quando si sostituisce un attributo con una versione più recente, è necessario aggiungere un suffisso di versione all'attributo:

`MSIP_Label_GUID_EnabledV2 = True | False | Condition`

## <a name="email"></a>E-mail

I metadati applicati alla posta elettronica mantengono un formato di coppia chiave/valore simile a quello dei documenti. La differenza principale consiste nel fatto che tutti gli attributi vengono serializzati in una singola intestazione di messaggio di posta elettronica denominata **MSIP_Labels**. Le coppie chiave/valore sono delimitate da un punto e virgola e da uno spazio vuoto e inserite nella nuova intestazione.

Utilizzando i metadati di esempio precedenti:

```
MSIP_Labels: MSIP_Label_2096f6a2-d2f7-48be-b329-b73aaa526e5d_Enabled=true; MSIP_Label_2096f6a2-d2f7-48be-b329-b73aaa526e5d_SetDate=2018-11-08T21:13:16-0800; MSIP_Label_2096f6a2-d2f7-48be-b329-b73aaa526e5d_Method=Privileged; MSIP_Label_2096f6a2-d2f7-48be-b329-b73aaa526e5d_Name=Confidential; MSIP_Label_2096f6a2-d2f7-48be-b329-b73aaa526e5d_SiteId=cb46c030-1825-4e81-a295-151c039dbf02; MSIP_Label_2096f6a2-d2f7-48be-b329-b73aaa526e5d_ContentBits=2; MSIP_Label_2096f6a2-d2f7-48be-b329-b73aaa526e5d_ActionId=88124cf5-1340-457d-90e1-0000a9427c99
```
