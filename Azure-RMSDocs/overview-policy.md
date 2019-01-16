---
title: Panoramica dei criteri di Azure Information Protection
description: Informazioni sulle etichette e sulle impostazioni dei criteri di Azure Information Protection.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 12/27/2018
ms.topic: conceptual
ms.service: information-protection
ms.reviewer: eymanor
ms.suite: ems
ms.openlocfilehash: 6483600d8ba74a29a54965010441fe10dc309d8e
ms.sourcegitcommit: b10df82d9f00b3f826bce38beb7b666ce3f56e84
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/28/2018
ms.locfileid: "53814187"
---
# <a name="overview-of-the-azure-information-protection-policy"></a>Panoramica dei criteri di Azure Information Protection

>*Si applica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*

Un criterio di Azure Information Protection contiene gli elementi seguenti che è possibile configurare:
    
- Etichette incluse che consentono ad amministratori e utenti di classificare (e, facoltativamente, proteggere) documenti e messaggi di posta elettronica.

- Titolo e descrizione comando della barra Information Protection visualizzata nelle applicazioni di Office.

- Opzione per impostare un'etichetta predefinita come punto di partenza per la classificazione di documenti e messaggi di posta elettronica.

- Opzione per applicare la classificazione quando gli utenti salvano documenti e inviano messaggi di posta elettronica.

- Opzione per richiedere agli utenti di specificare un motivo quando selezionano un'etichetta con un livello di riservatezza inferiore rispetto all'originale.

- Opzione per etichettare automaticamente un messaggio di posta elettronica, in base ai relativi allegati.

- Opzione per controllare se la barra di Information Protection viene visualizzata nelle applicazioni di Office.

- Opzione per controllare se il pulsante Non inoltrare viene visualizzato in Outlook.

- Opzione per consentire agli utenti di specificare le proprie autorizzazioni per i documenti.

- Opzione per fornire un collegamento alla guida personalizzata per gli utenti.

Azure Information Protection viene distribuito con [criteri predefiniti](configure-policy-default.md), che contengono cinque etichette principali. Due di queste etichette contengono etichette secondarie che forniscono sottocategorie in caso di necessità. 

Quando un'etichetta è configurata con etichette secondarie, gli utenti non possono selezionare l'etichetta principale ma devono selezionare una delle etichette secondarie. In questo scenario l'etichetta principale è supportata solo come contenitore di visualizzazione per il nome e il colore.

Le etichette di Azure Information Protection possono essere usate con l'intera gamma di dati che in genere vengono creati e archiviati da un'organizzazione, dalla classificazione minima per i dati personali alla classificazione più elevata per dati particolarmente riservati. 

È possibile usare le etichette predefinite così come sono oppure personalizzarle, eliminarle e crearne di nuove. Per istruzioni complete, vedere [Configurazione dei criteri di Azure Information Protection](configure-policy.md).


## <a name="next-steps"></a>Passaggi successivi

Per esempi su come personalizzare i criteri di Azure Information Protection e osservare il comportamento risultante per gli utenti, eseguire le esercitazioni seguenti:

- [Modificare i criteri di Azure Information Protection e creare una nuova etichetta](infoprotect-quick-start-tutorial.md)

- [Configurare impostazioni dei criteri di Azure Information Protection che interagiscono tra loro](infoprotect-settings-tutorial.md)
