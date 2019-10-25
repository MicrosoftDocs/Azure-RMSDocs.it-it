---
title: Azure Information Protection l'assegnazione unificata di file client e registrazione dell'utilizzo
description: Informazioni sui file client e la registrazione dell'utilizzo per il client di Azure Information Protection Unified Labeling per Windows.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 09/26/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: v2client
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 8e2b6d0b3e0436800cd73959107bd544dae348b0
ms.sourcegitcommit: 47d5765e1b76309a81aaf5e660256f2fb30eb2b2
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/23/2019
ms.locfileid: "72805593"
---
# <a name="admin-guide-azure-information-protection-unified-labeling-client-files-and-client-usage-logging"></a>Guida dell'amministratore: Azure Information Protection Unified Labeling client files and client usage logging

>*Si applica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8, Windows 7 con SP1, windows server 2019, windows server 2016, windows Server 2012 R2, windows Server 2012, windows Server 2008 R2*
>
> *Istruzioni per: [Azure Information Protection client di etichetta unificata per Windows](../faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*

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

