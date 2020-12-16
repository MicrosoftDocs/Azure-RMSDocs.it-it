---
title: Avvio rapido - Distribuzione del client di etichettatura unificata di Azure Information Protection (AIP)
description: Introduzione rapida per il client di etichettatura unificata di Azure Information Protection (AIP)
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 11/09/2020
ms.topic: quickstart
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: aiplabels
ms.custom: admin
ms.openlocfilehash: fa795fa29e39bc9fe5abc9a68febcd168a5bb502
ms.sourcegitcommit: 8a141858e494dd1d3e48831e6cd5a5be48ac00d2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2020
ms.locfileid: "97386339"
---
# <a name="quickstart-deploying-the-azure-information-protection-aip-unified-labeling-client"></a>Guida introduttiva: Distribuzione del client di etichettatura unificata di Azure Information Protection (AIP)

>***Si applica a**: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*
>
> ***Rilevante per**: [Client di etichettatura unificata di Azure Information Protection per Windows](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

Il client di etichettatura unificata di Azure Information Protection (AIP) fa parte della soluzione [Microsoft Information Protection](https://aka.ms/MIPdocs) ed estende le funzionalità predefinite per l'assegnazione di etichette di riservatezza fornite da Microsoft 365. 

Il client offre supporto all'utente finale per l'etichettatura e la protezione in Esplora file e PowerShell, oltre che nelle applicazioni Office. Lo scanner incluso nel client di etichettatura unificata consente agli amministratori di analizzare le reti e le condivisioni di contenuto per individuare eventuale contenuto sensibile. 

Per le organizzazioni senza una piattaforma di protezione delle informazioni, il client fornisce un visualizzatore per il contenuto protetto da altre organizzazioni che usano Microsoft Information Protection.

## <a name="review-aip-client-prerequisites"></a>Esaminare i prerequisiti del client di AIP

Usare gli articoli collegati di seguito per informazioni sui prerequisiti per la distribuzione dell'etichettatura unificata di Azure Information Protection nell'organizzazione:

- **[Requisiti per Azure Information Protection](requirements.md).** Descrizione dei requisiti di sistema dettagliati per la distribuzione del client di AIP nell'organizzazione, ad esempio una sottoscrizione di Azure Information Protection e Azure Active Directory. Sono inoltre elencati i dispositivi client e le applicazioni supportati.

- **[Prerequisiti del client di etichettatura unificata](rms-client/clientv2-admin-guide-install.md#additional-prerequisites-for-the-azure-information-protection-unified-labeling-client).** Elenco dei requisiti di sistema per ogni computer in cui è installato il client di AIP.

## <a name="install-the-aip-client"></a>Installare il client di AIP

AIP offre le opzioni di installazione client seguenti:

- **[Scaricare ed eseguire il file EXE.](rms-client/clientv2-admin-guide-install.md#to-install-the-azure-information-protection-unified-labeling-client-by-using-the-executable-installer)** Questa installazione è l'opzione consigliata per la maggior parte dei casi d'uso. L'installazione può essere eseguita in modo interattivo o invisibile all'utente.

    Al termine dell'installazione potrebbe essere richiesto di riavviare il computer o il software di Office. Riavviare come richiesto per continuare.

- **[Scaricare ed eseguire il file MSI.](rms-client/clientv2-admin-guide-install.md#to-install-the-azure-information-protection-unified-labeling-client-by-using-the-msi-installer)** Metodo supportato per le installazioni invisibili all'utente che usano un meccanismo di distribuzione centralizzato, ad esempio Criteri di gruppo, Configuration Manager e Microsoft Intune.

I file di installazione del client di AIP sono disponibili nel [sito di download di Microsoft](https://www.microsoft.com/download/details.aspx?id=53018). 

Per altre informazioni, vedere [Opzioni per l'installazione del client di AIP](rms-client/clientv2-admin-guide-install.md#options-to-install-the-azure-information-protection-unified-labeling-client-for-users).

> [!TIP]
> Per provare le funzionalità più recenti disponibili per il client di AIP, distribuire la versione di anteprima pubblica in un sistema di test. Per altre informazioni, vedere la [cronologia delle versioni](rms-client/unifiedlabelingclient-version-release-history.md) del client di etichettatura unificata di AIP.
> 

## <a name="next-steps"></a>Passaggi successivi

Per iniziare a usare il client di Azure Information Protection, vedere le guide di avvio rapido e le esercitazioni seguenti:

- [Esercitazione: Installazione dello scanner di etichettatura unificata di Azure Information Protection (AIP)](tutorial-install-scanner.md)
- [Esercitazione: Individuazione del contenuto sensibile con lo scanner di Azure Information Protection (AIP)](tutorial-scan-networks-and-content.md)
- [Esercitazione: Prevenzione dell'oversharing con Azure Information Protection (AIP)](tutorial-preventing-oversharing.md)
- [Esercitazione: Migrazione dal client classico al client di etichettatura unificata di Azure Information Protection (AIP)](tutorial-migrating-to-ul.md) 

**Vedere anche**:

- [Problemi noti - Azure Information Protection](known-issues.md) 
- [Domande frequenti su Azure Information Protection](faqs.md) 
- [Guida dell'amministratore: Configurazioni personalizzate per il client di etichettatura unificata di Azure Information Protection](rms-client/clientv2-admin-guide-customizations.md)        
    
