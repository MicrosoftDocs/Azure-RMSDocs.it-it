---
title: Azure Information Protection l'assegnazione unificata di file client e registrazione dell'utilizzo
description: Informazioni sui file client e la registrazione dell'utilizzo per il client di Azure Information Protection Unified Labeling per Windows.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 09/03/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: v2client
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 36dae0d339059020b9e95d2671bc64f7a1f77c1f
ms.sourcegitcommit: af7ac2eeb8f103402c0036dd461c77911fbc9877
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/18/2021
ms.locfileid: "98560323"
---
# <a name="admin-guide-azure-information-protection-unified-labeling-client-files-and-client-usage-logging"></a>Guida dell'amministratore: Azure Information Protection Unified Labeling client files and client usage logging

>***Si applica a**: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8, Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012 *
>
>*Se si dispone di Windows 7 o Office 2010, vedere [AIP e versioni legacy di Windows e Office](../known-issues.md#aip-and-legacy-windows-and-office-versions).*
>
>***Pertinente per**: [Azure Information Protection client di etichetta unificato per Windows](../faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients). Per il client classico, vedere la [Guida dell'amministratore del client classico](client-admin-guide-files-and-logging.md). *

Dopo aver installato il client di etichettatura unificata di Azure Information Protection, potrebbe essere necessario individuare la posizione dei file e monitorare la modalità di utilizzo del client.

## <a name="file-locations-for-the-azure-information-protection-unified-labeling-client"></a>Percorsi dei file per il client Azure Information Protection Unified Labeling

File del client:    

- Per i sistemi operativi a 64 bit: **\Programmi (x86)\Microsoft Azure Information Protection**

- Per i sistemi operativi a 32 bit: **\Programmi\Microsoft Azure Information Protection**

File di log del client e file di criteri attualmente installati:

- Per i sistemi operativi a 64 e 32 bit: **%localappdata%\Microsoft\MSIP**


## <a name="usage-logging-for-the-azure-information-protection-unified-labeling-client"></a>Registrazione dell'utilizzo per il client Azure Information Protection Unified Labeling

Il client di etichettatura unificata non registra l'attività dell'utente nel registro eventi di Windows locale. Usare invece la funzionalità di [creazione di report centrale](../reports-aip.md) di Azure Information Protection. 


## <a name="next-steps"></a>Passaggi successivi
Ora che sono stati identificati tutti i file di log associati al client di Azure Information Protection Unified Labeling, vedere gli argomenti seguenti per informazioni aggiuntive che potrebbero essere necessarie per supportare questo client:

- [Personalizzazioni](clientv2-admin-guide-customizations.md)

- [Tipi di file supportati](clientv2-admin-guide-file-types.md)

- [Comandi di PowerShell](clientv2-admin-guide-powershell.md)

