---
title: PowerShell per i modelli di protezione - Azure Information Protection
description: Usare i cmdlet di PowerShell per aggiungere, ottenere, esportare, importare, rimuovere e configurare i modelli di protezione per Azure Information Protection.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 11/03/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 30ee2f77-ce16-4113-bcda-6089131849ec
ROBOTS: NOINDEX
ms.reviewer: esaggese
ms.subservice: azurerms
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: c8e4c54dee7494aaecadb6de943544e7a1f6c109
ms.sourcegitcommit: b32c16e41ba36167b5a3058b56a73183bdd4306d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/29/2020
ms.locfileid: "97806363"
---
# <a name="powershell-reference-for-protection-templates"></a>Informazioni di riferimento su PowerShell per i modelli di protezione

>***Si applica a**: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*
>
>***Pertinente per**: [Azure Information Protection client classico per Windows](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients). Per il client di etichettatura unificata, vedere [informazioni sulle etichette di riservatezza](/microsoft-365/compliance/sensitivity-labels) dalla documentazione di Microsoft 365. *

> [!NOTE] 
> Per offrire un'esperienza per i clienti unificata e semplificata, il **client classico di Azure Information Protection** e **Gestione etichette** nel portale di Azure saranno **deprecati** a partire dal **31 marzo 2021**. In questo intervallo di tempo tutti i clienti correnti di Azure Information Protection possono passare alla soluzione di etichettatura unificata usando la piattaforma di etichettatura unificata di Microsoft Information Protection. Altre informazioni nell'[avviso ufficiale sulla deprecazione](https://aka.ms/aipclassicsunset).
>

Le impostazioni di protezione di Azure Information Protection vengono salvate in modelli di protezione. Tutte le operazioni che è possibile eseguire nel portale di Azure per creare e gestire le impostazioni di protezione possono essere eseguite anche nella riga di comando tramite PowerShell. 

È anche possibile esportare e importare i modelli di protezione. Queste due azioni consentono di copiare i modelli di protezione tra tenant o apportare modifiche in blocco per proprietà complesse, come i nomi e le descrizioni in più lingue.

È anche possibile usare l'esportazione e l'importazione per eseguire il backup e il ripristino dei modelli di protezione. Come procedura consigliata, eseguire regolarmente il backup dei modelli. In questo modo, se si apporta una modifica non appropriata alle impostazioni di protezione, è possibile ripristinare facilmente una versione precedente.

Per le istruzioni di installazione, vedere [installazione del modulo PowerShell AIPService](install-powershell.md).

I cmdlet che supportano la creazione e la gestione dei modelli di protezione sono i seguenti:

- [Add-AipServiceTemplate](/powershell/module/aipservice/add-aipservicetemplate)

- [Export-AipServiceTemplate](/powershell/module/aipservice/export-aipservicetemplate)

- [Get-AipServiceTemplate](/powershell/module/aipservice/get-aipservicetemplate)

- [Get-AipServiceTemplateProperty](/powershell/module/aipservice/get-aipservicetemplateproperty)

- [Import-AipServiceTemplate](/powershell/module/aipservice/import-aipservicetpd)

- [New-AipServiceRightsDefinition](/powershell/module/aipservice/new-aipservicerightsdefinition)

- [Remove-AipServiceTemplate](/powershell/module/aipservice/remove-aipservicetemplate)

- [Set-AipServiceTemplateProperty](/powershell/module/aipservice/set-aipservicetemplateproperty)

## <a name="see-also"></a>Vedere anche
[Configurazione e gestione dei modelli per Azure Information Protection](configure-policy-templates.md)

