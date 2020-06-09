---
title: Concetto di giustificazione dell'azione in MIP SDK (C++)
description: Questo articolo consente di comprendere lo scenario di come effettuare il downgrade o la rimozione di un'etichetta che necessita di giustificazione.
author: Pathak-Aniket
ms.service: information-protection
ms.topic: conceptual
ms.date: 04/14/2020
ms.author: v-anikep
ms.openlocfilehash: 1b0926114dd4d494593bd0d2340fee35edfe5fe6
ms.sourcegitcommit: a1feede30ac1f54e900e52eb45b3e6634e0f13f3
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/08/2020
ms.locfileid: "84548242"
---
# <a name="action-justification-in-mip-sdk-c"></a>Giustificazione dell'azione in MIP SDK (C++)

## <a name="overview"></a>Panoramica

I criteri di etichetta in Security and Compliance Center consentono agli amministratori di richiedere una **giustificazione** alla rimozione o al downgrade di un'etichetta. Il downgrade viene definito come applicazione di un'etichetta con un valore di sensibilità inferiore al posto dell'etichetta esistente.

Come illustrato in precedenza, l'API file fornisce interfacce di facile utilizzo per la lettura delle etichette dal servizio, l'applicazione di etichette ai tipi di file definiti e la lettura di etichette da tali tipi di file. Supporta inoltre le operazioni sui file per la rimozione delle etichette e la modifica delle etichette sui tipi di file supportati. Le modifiche apportate all'etichetta file sono supportate tramite la `mip::FileHandler` `SetLabel()` funzione di che consente di impostare una nuova etichetta su un file non protetto o precedentemente protetto e `mip::FileHandler` `DeleteLabel()` la funzione di che rimuove l'etichetta da un file protetto in precedenza.

Per alcune delle etichette di riservatezza, gli amministratori della sicurezza possono applicare criteri più restrittivi quando un utente tenta di effettuare il downgrade della riservatezza eliminando un'etichetta o cambiando l'etichetta in uno meno restrittivo. Gli amministratori possono configurare questa impostazione usando la configurazione dei criteri di etichetta in [Security and Compliance Center](https://sip.compliance.microsoft.com/) selezionando la casella di controllo.

![Giustificazione dell'azione obbligatoria](./media/justify-action.png)

Se il file ha un'etichetta esistente e se i criteri dell'etichetta richiedono la giustificazione in caso di downgrade del livello di riservatezza, le `SetLabel()` / `DeleteLabel()` funzioni generano un errore `mip::JustificationRequiredError` . In uno scenario di questo tipo, l'API offre la possibilità di registrare la giustificazione dell'utente. I consumer SDK devono fornire all'utente un'interfaccia dell'applicazione per fornire l'input sul motivo del downgrade. Una volta registrata la giustificazione, l'applicazione può impostare `isDowngradeJustified` la proprietà di, nonché impostare `mip::LabelingOptions` la `Justification` Proprietà.

## <a name="next-steps"></a>Passaggi successivi

- [Guida introduttiva alla valutazione delle azioni (C++)](quick-file-justify-actions-cpp.md)
- [Guida introduttiva alla valutazione delle azioni (C#)](quick-file-justify-actions-csharp.md)