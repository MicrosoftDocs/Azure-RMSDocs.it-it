---
title: Log di controllo generati da Azure Information Protection-AIP
description: Informazioni sui log di controllo generati da Azure Information Protection-AIP.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 06/01/2020
ms.topic: reference
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: prereqs
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: b851372494a3215a1db3f118809ec2bdf438affd
ms.sourcegitcommit: fa16364879823b86b4e56ac18a1fc8de5a5dae57
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/01/2020
ms.locfileid: "84250435"
---
# <a name="azure-information-protection-audit-log-reference-public-preview"></a>Azure Information Protection riferimento al log di controllo (anteprima pubblica)

>*Si applica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

Microsoft Azure Information Protection genera log di controllo negli eventi di attività seguenti:
* [Accesso](#access-audit-logs)
* [Accesso negato](#access-denied-audit-logs)
* [Modificare la protezione](#change-protection-audit-logs)
* [Rilevazione](#discover-audit-logs)
* [Etichetta downgrade](#downgrade-label-audit-logs)
* [File rimosso](#file-removed-audit-logs)
* [Nuova etichetta](#new-label-audit-logs)
* [Nuova protezione](#new-protection-audit-logs)
* [Rimuovi etichetta](#remove-label-audit-logs)
* [Rimuovere la protezione](#remove-protection-audit-logs)
* [Aggiorna etichetta](#upgrade-label-audit-logs)




## <a name="access-audit-logs"></a>Accedere ai log di controllo
I log di controllo di **accesso** vengono generati per le attività seguenti:

|Segnalato da  |Piattaforma  |Applicazione  |Azione/descrizione  |
|---------|---------|---------|---------|
|Azure Information Protection:</br>-Client classico</br>-Client con etichetta unificata     | Windows        | Office        |Generato per la prima volta in ogni sessione in cui viene salvato un file con etichetta o protetto.<br>I file di log includono qualsiasi tipo di informazione corrispondente.  <!-- plan to be removed -->    |
|Azure Information Protection:</br>-Client classico</br>-Client con etichetta unificata     |Windows         |Office         |Generato ogni volta che viene creato un file con etichetta o protetto.<!-- plan to be removed -->       |
|Azure Information Protection:</br>-Client classico</br>-Client con etichetta unificata     | Windows, SharePoint, OneDrive        | Office        | Generato ogni volta che viene aperto un file con etichetta o protetto.         |
|SDK di Microsoft Information Protection (MIP)     | Qualsiasi        | Applicazioni di terze parti        | Generato ogni volta che viene eseguito l'accesso a un file con etichetta o protetto da un'applicazione di terze parti che la supporta.       |
|Servizio RMS     | Windows        | Office         |Generato ogni volta che si accede a un documento con etichetta o protetto.<!-- plan to be removed -->       |

## <a name="access-denied-audit-logs"></a>Accesso negato log di controllo
I log di controllo per **accesso negato** vengono generati per le attività seguenti:

|Segnalato da  |Piattaforma  |Applicazione  |Azione/descrizione   |
|---------|---------|---------|---------|
|Servizio RMS     | Windows        | Office         |Generato ogni volta che un utente tenta di accedere a un documento protetto per il quale non ha accesso.|

## <a name="change-protection-audit-logs"></a>Modificare i log di controllo della protezione
Vengono generati i log di controllo della **protezione delle modifiche** per le attività seguenti:

|Segnalato da  |Piattaforma  |Applicazione  |Azione/descrizione   |
|---------|---------|---------|---------|
|Azure Information Protection:</br>-Client classico</br>-Client con etichetta unificata     | Windows, SharePoint, OneDrive        | Office        | Generato ogni volta che la protezione viene modificata manualmente, senza un'etichetta.  |
|SDK di Microsoft Information Protection (MIP)     | Qualsiasi        | Applicazioni di terze parti        | Generato ogni volta che la protezione viene modificata manualmente, senza un'etichetta.<br>Generato solo se supportato dall'applicazione di terze parti. |

## <a name="discover-audit-logs"></a>Individuare i log di controllo
**Individuare** i log di controllo generati per le attività seguenti:

|Segnalato da  |Piattaforma  |Applicazione  |Azione/descrizione   |
|---------|---------|---------|---------|
|Azure Information Protection:</br>-Scanner classico </br>-Scanner di etichette unificato     | Windows        | Office        |Generato ogni volta che un file viene sottoposta a scansione dallo scanner AIP.<br>I file di log includono i dettagli seguenti:<br>-Tipi di informazioni corrispondenti<br>-Etichette |
|SDK di Microsoft Information Protection (MIP) | Qualsiasi | Applicazioni di terze parti | Generato ogni volta che un file viene sottoposta a scansione da un'applicazione di terze parti che la supporta. </br>I file di log includono i dettagli seguenti:</br>-Tipi di informazioni corrispondenti</br>-Etichette|

## <a name="downgrade-label-audit-logs"></a>Downgrade log di controllo etichetta
I log di controllo delle **etichette di downgrade** vengono generati per le attività seguenti:

| Segnalato da      | Piattaforma                       | Applicazione              | Azione/descrizione      |
| ---------------- | ------------------------------ | ------------------------ | --------------- |
|Azure Information Protection:</br>-Client classico</br>-Client con etichetta unificata | Windows, SharePoint, un'unità | Office                   | Generato ogni volta che un'etichetta di documento viene aggiornata con un'etichetta meno sensibile.|
| Microsoft Defender ATP            | Windows                        | OS                       | Generato ogni volta che un'etichetta di documento viene aggiornata con un'etichetta meno sensibile. |
| SDK di Microsoft Information Protection (MIP)          | Qualsiasi                            | Applicazioni di terze parti | Generato ogni volta che un'etichetta di documento viene aggiornata con un'etichetta meno sensibile.<br>Generato solo se supportato dall'applicazione di terze parti. |

## <a name="file-removed-audit-logs"></a>Log di controllo rimossi dal file

> [!NOTE]
> I log di controllo rimossi dal file sono supportati solo in Azure Information Protection scanner versione [2.7.95.0](rms-client/unifiedlabelingclient-version-release-history.md#version-27950-public-preview) e versioni successive.

I log di controllo **rimossi dal file** vengono generati per le attività seguenti:

| Segnalato da                                                                              | Piattaforma | Applicazione                     | Azione/descrizione                                                          |
| ---------------------------------------------------------------------------------------- | -------- | ------------------------------- | ------------------------------------------------------------------------------ |
| Azure Information Protection scanner, Unified Labeling client | Windows  | Office e tipi di file supportati | Generato ogni volta che lo scanner rileva che un file precedentemente analizzato è stato rimosso. |


## <a name="new-label-audit-logs"></a>Nuovi log di controllo etichetta
Vengono generati nuovi log di controllo **etichetta** per le attività seguenti:

| Segnalato da                                                                      | Piattaforma                       | Applicazione              | Azione/descrizione                                                                                      |
| -------------------------------------------------------------------------------- | ------------------------------ | ------------------------ | ---------------------------------------------------------------------------------------------------------- |
| Azure Information Protection:</br>-Client classico</br>-Client con etichetta unificata | Windows, SharePoint, un'unità | Office                   | Generato ogni volta che viene applicata una nuova etichetta.                                                                  |
| Microsoft Defender ATP                                                                            | Windows                        | OS                       | Generato ogni volta che viene applicata una nuova etichetta del documento.                                                                  |
| SDK di Microsoft Information Protection (MIP)                                                                          | Qualsiasi                            | Applicazioni di terze parti | Generato ogni volta che viene applicata una nuova etichetta del documento.<br>Generato solo se supportato dall'applicazione di terze parti. |

## <a name="new-protection-audit-logs"></a>Nuovi log di controllo della protezione
Vengono generati nuovi log di controllo della **protezione** per le attività seguenti:

| Segnalato da                                                                      | Piattaforma                       | Applicazione              | Azione/descrizione                                                                                      |
| -------------------------------------------------------------------------------- | ------------------------------ | ------------------------ | ---------------------------------------------------------------------------------------------------------- |
| Azure Information Protection:</br>-Client classico</br>-Client con etichetta unificata | Windows, SharePoint, un'unità | Office                   | Generato ogni volta che la protezione viene aggiunta manualmente, senza un'etichetta.                                                                  |
| SDK di Microsoft Information Protection (MIP)                                                                          | Qualsiasi                            | Applicazioni di terze parti | Generato ogni volta che la protezione viene aggiunta manualmente, senza un'etichetta.<br>Generato solo se supportato dall'applicazione di terze parti. |

## <a name="remove-label-audit-logs"></a>Rimuovi log di controllo etichetta
**Rimuovere** i log di controllo delle etichette per le attività seguenti:


| Segnalato da                                                                      | Piattaforma                       | Applicazione              | Azione/descrizione                                                                                      |
| -------------------------------------------------------------------------------- | ------------------------------ | ------------------------ | ---------------------------------------------------------------------------------------------------------- |
| Azure Information Protection:</br>-Client classico</br>-Client con etichetta unificata | Windows, SharePoint, un'unità | Office                   | Generato ogni volta che un'etichetta viene rimossa.                                                                  |
| Microsoft Defender ATP                                                                            | Windows                        | OS                       | Generato ogni volta che un'etichetta viene rimossa.                                                                  |
| SDK di Microsoft Information Protection (MIP)                                                                          | Qualsiasi                            | Applicazioni di terze parti | Generato ogni volta che un'etichetta viene rimossa.<br>Generato solo se supportato dall'applicazione di terze parti. |

## <a name="remove-protection-audit-logs"></a>Rimuovere i log di controllo della protezione
**Rimuovere** i log di controllo della protezione per le attività seguenti:

| Segnalato da                                                                      | Piattaforma                       | Applicazione              | Azione/descrizione                                                                                      |
| -------------------------------------------------------------------------------- | ------------------------------ | ------------------------ | ---------------------------------------------------------------------------------------------------------- |
| Azure Information Protection:</br>-Client classico</br>-Client con etichetta unificata | Windows, SharePoint, un'unità | Office                   | Generato ogni volta che la protezione viene rimossa manualmente, senza un'etichetta.                                                                  |
| SDK di Microsoft Information Protection (MIP)                                                                          | Qualsiasi                            | Applicazioni di terze parti | Generato ogni volta che la protezione viene rimossa manualmente, senza un'etichetta.<br>Generato solo se supportato dall'applicazione di terze parti. |

## <a name="upgrade-label-audit-logs"></a>Aggiornare i log di controllo dell'etichetta
Vengono generati i log di controllo dell' **etichetta di aggiornamento** per le attività seguenti:

| Segnalato da                                                                      | Piattaforma                       | Applicazione              | Azione/descrizione                                                                                      |
| -------------------------------------------------------------------------------- | ------------------------------ | ------------------------ | ---------------------------------------------------------------------------------------------------------- |
| Azure Information Protection:</br>-Client classico</br>-Client con etichetta unificata | Windows, SharePoint, un'unità | Office                   | Generato ogni volta che un'etichetta di documento viene aggiornata con un'etichetta più sensibile.                                                                   |
| Microsoft Defender ATP                                                                            | Windows                        | OS                       | Generato ogni volta che un'etichetta di documento viene aggiornata con un'etichetta più sensibile.                                                                   |
| SDK di Microsoft Information Protection (MIP)                                                                          | Qualsiasi                            | Applicazioni di terze parti | Generato ogni volta che un'etichetta di documento viene aggiornata con un'etichetta più sensibile.<br>Generato solo se supportato dall'applicazione di terze parti. |
