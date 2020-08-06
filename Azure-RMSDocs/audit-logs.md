---
title: Log di controllo generati da Azure Information Protection-AIP
description: Informazioni sui log di controllo generati da Azure Information Protection-AIP.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 06/29/2020
ms.topic: reference
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: prereqs
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: cbffb68eb997b5d539ddd31a1f85fb25bb797976
ms.sourcegitcommit: 89e3434c5c6486b1adb6f91739a1e6b24687e367
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/20/2020
ms.locfileid: "86471740"
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
|Azure Information Protection:</br>-Client classico</br>-Client con etichetta unificata     | WINDOWS        | Office        |Generato per la prima volta in ogni sessione in cui viene salvato un file con etichetta o protetto.<br>Il log include qualsiasi tipo di informazione corrispondente.  <!-- plan to be removed -->    |
|Azure Information Protection:</br>-Client classico</br>-Client con etichetta unificata     |WINDOWS         |Office         |Generato ogni volta che viene creato un file con etichetta o protetto.<!-- plan to be removed -->       |
|Azure Information Protection:</br>-Client classico</br>-Client con etichetta unificata     | Windows, SharePoint, OneDrive        | Office        | Generato ogni volta che viene aperto un file con etichetta o protetto. </br></br>**Nota:** Per i file protetti, i log di controllo degli accessi vengono generati solo quando il file viene aperto e il contenuto viene correttamente decrittografato ed esposto all'utente. </br>Per i messaggi di posta elettronica protetti in Outlook, vengono generati anche i log di controllo dell'accesso ogni volta che l'utente tenta di aprire un messaggio di posta elettronica crittografato, anche se la decrittografia è bloccata a causa di una mancanza di autorizzazioni. <!--limitations-->         |
|SDK di Microsoft Information Protection (MIP)     | Qualsiasi        | Applicazioni di terze parti        | Generato ogni volta che viene eseguito l'accesso a un file con etichetta o protetto da un'applicazione di terze parti che la supporta.       |
|Servizio RMS     | WINDOWS        | Office         |Generato ogni volta che si accede a un documento con etichetta o protetto.<!-- plan to be removed -->       |


## <a name="access-denied-audit-logs"></a>Accesso negato log di controllo

I log di controllo per **accesso negato** vengono generati per le attività seguenti:

|Segnalato da  |Piattaforma  |Applicazione  |Azione/descrizione   |
|---------|---------|---------|---------|
|Servizio RMS     | WINDOWS        | Office         |Generato ogni volta che un utente tenta di accedere a un documento protetto per il quale non sono disponibili autorizzazioni.

## <a name="change-protection-audit-logs"></a>Modificare i log di controllo della protezione

Vengono generati i log di controllo della **protezione delle modifiche** per le attività seguenti:

|Segnalato da  |Piattaforma  |Applicazione  |Azione/descrizione   |
|---------|---------|---------|---------|
|Azure Information Protection:</br>-Client classico</br>-Client con etichetta unificata     | Windows, SharePoint, OneDrive        | Office        | Generato ogni volta che la protezione su un documento senza etichetta viene modificata manualmente.         |
|SDK di Microsoft Information Protection (MIP)     | Qualsiasi        | Applicazioni di terze parti        | Generato ogni volta che la protezione su un documento senza etichetta viene modificata manualmente.<br>Generato solo se supportato dall'applicazione di terze parti.       |

## <a name="discover-audit-logs"></a>Individuare i log di controllo

**Individuare** i log di controllo generati per le attività seguenti:

|Segnalato da  |Piattaforma  |Applicazione  |Azione/descrizione   |
|---------|---------|---------|---------|
|Azure Information Protection:</br>-Scanner classico </br>-Scanner di etichette unificato     | WINDOWS        | Office        |Generato ogni volta che un file viene sottoposta a scansione dallo scanner AIP.<br>Il log include i dettagli seguenti:<br>-Tipi di informazioni corrispondenti<br>-Etichette |
|SDK di Microsoft Information Protection (MIP) | Qualsiasi | Applicazioni di terze parti | Generato ogni volta che un file viene sottoposta a scansione da un'applicazione di terze parti che la supporta. </br>Il log include i dettagli seguenti:</br>-Tipi di informazioni corrispondenti</br>-Etichette|

## <a name="downgrade-label-audit-logs"></a>Downgrade log di controllo etichetta

I log di controllo delle **etichette di downgrade** vengono generati per le attività seguenti:

| Segnalato da      | Piattaforma                       | Applicazione              | Azione/descrizione      |
| ---------------- | ------------------------------ | ------------------------ | --------------- |
|Azure Information Protection:</br>-Scanner e client classici</br>-Scanner unificato per l'assegnazione di etichette e client | Windows, SharePoint, un'unità | Office                   | Generato ogni volta che un'etichetta di documento viene aggiornata con un'etichetta meno sensibile.|
| Microsoft Defender ATP            | WINDOWS                        | Sistema operativo                       | Generato ogni volta che un'etichetta di documento viene aggiornata con un'etichetta meno sensibile. |
| SDK di Microsoft Information Protection (MIP)          | Qualsiasi                            | Applicazioni di terze parti | Generato ogni volta che un'etichetta di documento viene aggiornata con un'etichetta meno sensibile.<br>Generato solo se supportato dall'applicazione di terze parti. |

## <a name="file-removed-audit-logs"></a>Log di controllo rimossi dal file

> [!NOTE]
> I log di controllo rimossi dal file sono supportati solo in Azure Information Protection scanner versione [2.7.96.0](rms-client/unifiedlabelingclient-version-release-history.md#version-27960) e versioni successive.

I log di controllo **rimossi dal file** vengono generati per le attività seguenti:

| Segnalato da                                                                              | Piattaforma | Applicazione                     | Azione/descrizione                                                          |
| ---------------------------------------------------------------------------------------- | -------- | ------------------------------- | ------------------------------------------------------------------------------ |
| Azure Information Protection scanner, Unified Labeling client | WINDOWS  | Office e tipi di file supportati | Generato ogni volta che lo scanner AIP rileva che un file precedentemente sottoposta a scansione è stato rimosso. |

## <a name="new-label-audit-logs"></a>Nuovi log di controllo etichetta

Vengono generati nuovi log di controllo **etichetta** per le attività seguenti:

| Segnalato da                                                                      | Piattaforma                       | Applicazione              | Azione/descrizione                                                                                      |
| -------------------------------------------------------------------------------- | ------------------------------ | ------------------------ | ---------------------------------------------------------------------------------------------------------- |
| Azure Information Protection:</br>-Scanner e client classici</br>-Scanner unificato per l'assegnazione di etichette e client | Windows, SharePoint, un'unità | Office                   | Generato ogni volta che viene applicata una nuova etichetta.                                                                  |
| Microsoft Defender ATP                                                                            | WINDOWS                        | Sistema operativo                       | Generato ogni volta che viene applicata una nuova etichetta del documento.                                                                  |
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
| Azure Information Protection:</br>-Scanner e client classici</br>-Scanner unificato per l'assegnazione di etichette e client | Windows, SharePoint, un'unità | Office                   | Generato ogni volta che un'etichetta viene rimossa.                                                                  |
| Microsoft Defender ATP                                                                            | WINDOWS                        | Sistema operativo                       | Generato ogni volta che un'etichetta viene rimossa.                                                                  |
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
| Azure Information Protection:</br>-Scanner e client classici</br>-Scanner unificato per l'assegnazione di etichette e client | Windows, SharePoint, un'unità | Office                   | Generato ogni volta che un'etichetta di documento viene aggiornata con un'etichetta più sensibile.                                                                   |
| Microsoft Defender ATP                                                                            | WINDOWS                        | Sistema operativo                       | Generato ogni volta che un'etichetta di documento viene aggiornata con un'etichetta più sensibile.                                                                   |
| SDK di Microsoft Information Protection (MIP)                                                                          | Qualsiasi                            | Applicazioni di terze parti | Generato ogni volta che un'etichetta di documento viene aggiornata con un'etichetta più sensibile.<br>Generato solo se supportato dall'applicazione di terze parti. |