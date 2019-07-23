---
title: Azure Information Protection l'assegnazione unificata di file client e registrazione dell'utilizzo
description: Informazioni sui file client e la registrazione dell'utilizzo per il client di Azure Information Protection Unified Labeling per Windows.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 07/19/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.suite: ems
ms.openlocfilehash: e90672438efff30d378699f36b3037f04d420b22
ms.sourcegitcommit: ae48f7cea01b4d615052659072305abb8698a7f7
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/22/2019
ms.locfileid: "68375442"
---
# <a name="admin-guide-azure-information-protection-unified-labeling-client-files-and-client-usage-logging"></a>Guida dell'amministratore: Azure Information Protection l'assegnazione unificata di file client e registrazione dell'utilizzo del client

>*Si applica a: Active Directory Rights Management Services, [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8, Windows 7 con SP1, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2*
>
> *Istruzioni per: [Azure Information Protection client di etichetta unificata per Windows](../faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*

Dopo aver installato il client di etichettatura unificata di Azure Information Protection, potrebbe essere necessario individuare la posizione dei file e monitorare la modalità di utilizzo del client.

## <a name="file-locations-for-the-azure-information-protection-client"></a>Percorsi dei file per il client Azure Information Protection

File del client:   

- Per i sistemi operativi a 64 bit: **\Programmi (x86)\Microsoft Azure Information Protection**

- Per i sistemi operativi a 32 bit: **\Programmi\Microsoft Azure Information Protection**

File di log del client:

- Per i sistemi operativi a 64 e 32 bit: **%localappdata%\Microsoft\MSIP**


## <a name="next-steps"></a>Passaggi successivi
Ora che sono stati identificati tutti i file di log associati al client di Azure Information Protection Unified Labeling, vedere gli argomenti seguenti per informazioni aggiuntive che potrebbero essere necessarie per supportare questo client:

- [Personalizzazioni](clientv2-admin-guide-customizations.md)

- [Tipi di file supportati](clientv2-admin-guide-file-types.md)

- [Comandi di PowerShell](clientv2-admin-guide-powershell.md)

