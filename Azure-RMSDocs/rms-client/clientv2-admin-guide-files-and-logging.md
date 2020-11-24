---
title: Azure Information Protection l'assegnazione unificata di file client e registrazione dell'utilizzo
description: Informazioni sui file client e la registrazione dell'utilizzo per il client di Azure Information Protection Unified Labeling per Windows.
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 09/03/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: v2client
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 7cc966fa126c459a27dc45091a32cb6fe835b1f0
ms.sourcegitcommit: b763a7204421a4c5f946abb7c5cbc06e2883199c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/28/2020
ms.locfileid: "95567729"
---
# <a name="admin-guide-azure-information-protection-unified-labeling-client-files-and-client-usage-logging"></a>Guida dell'amministratore: Azure Information Protection Unified Labeling client files and client usage logging

>*Si applica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8, windows server 2019, windows server 2016, windows Server 2012 R2, windows Server 2012*
>
>*Se si dispone di Windows 7 o Office 2010, vedere [AIP per le versioni di Windows e Office nel supporto esteso](../known-issues.md#aip-for-windows-and-office-versions-in-extended-support).*
>
> *Istruzioni per: [Client di etichettatura unificata di Azure Information Protection per Windows](../faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

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

