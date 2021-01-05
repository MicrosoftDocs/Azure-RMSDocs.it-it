---
title: Concetto di giustificazione dell'azione nell'SDK MIP
description: Le informazioni in questo articolo sono utili per comprendere come effettuare il downgrade o la rimozione di un'etichetta che richiede una giustificazione.
author: msmbaldwin
ms.service: information-protection
ms.topic: conceptual
ms.date: 04/14/2020
ms.author: mbaldwin
ms.openlocfilehash: b6f5ebaa08a2726671f891c583d46f310952d1d2
ms.sourcegitcommit: 8e48016754e6bc6d051138b3e3e3e3edbff56ba5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/04/2021
ms.locfileid: "97864941"
---
# <a name="action-justification-in-mip-sdk"></a>Giustificazione dell'azione in MIP SDK

## <a name="overview"></a>Panoramica

I criteri di etichetta in Security and Compliance Center consentono agli amministratori di richiedere una **giustificazione** alla rimozione o al downgrade di un'etichetta. Il downgrade viene definito come applicazione di un'etichetta con un valore di sensibilità inferiore al posto dell'etichetta esistente.

Come illustrato in precedenza, l'API file fornisce interfacce di facile utilizzo per la lettura delle etichette dal servizio, l'applicazione di etichette ai tipi di file definiti e la lettura di etichette da tali tipi di file. Supporta inoltre le operazioni sui file per la rimozione e la modifica delle etichette per i tipi di file supportati. Le modifiche apportate all'etichetta file sono supportate tramite la `mip::FileHandler` `SetLabel()` funzione di che consente di impostare una nuova etichetta su un file non protetto o precedentemente protetto e `mip::FileHandler` `DeleteLabel()` la funzione di che rimuove l'etichetta da un file protetto in precedenza.

Per alcune delle etichette di riservatezza, gli amministratori della sicurezza possono applicare criteri più restrittivi quando un utente tenta di effettuare il downgrade della riservatezza eliminando un'etichetta o cambiando l'etichetta in uno meno restrittivo. Gli amministratori possono configurare questa impostazione usando la configurazione dei criteri di etichetta in [Security and Compliance Center](https://sip.compliance.microsoft.com/) selezionando la casella di controllo.

![Giustificazione dell'azione obbligatoria](./media/justify-action.png)

Se il file ha un'etichetta esistente e i criteri dell'etichetta richiedono la giustificazione in caso di downgrade di un'etichetta, le `SetLabel()` / `DeleteLabel()` funzioni generano un errore `mip::JustificationRequiredError` . L'applicazione deve rilevare questa eccezione, quindi fornire un'interfaccia dell'applicazione all'utente per fornire l'input sul motivo del downgrade. Una volta registrata la giustificazione, l'applicazione può impostare `isDowngradeJustified` la proprietà di, nonché impostare `mip::LabelingOptions` la `Justification` Proprietà.

## <a name="next-steps"></a>Passaggi successivi

- [Guida introduttiva alla valutazione delle azioni (C++)](quick-file-justify-actions-cpp.md)
- [Guida introduttiva alla valutazione delle azioni (C#)](quick-file-justify-actions-csharp.md)