---
title: PowerShell per i modelli di protezione - Azure Information Protection
description: Usare PowerShell per creare e gestire i modelli di protezione per Azure Information Protection.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 09/03/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 30ee2f77-ce16-4113-bcda-6089131849ec
ms.reviewer: esaggese
ms.subservice: azurerms
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: b75242487f3a32d0e6ea0f912d9bc75f8109e0fe
ms.sourcegitcommit: 9484744702a82b8adc45f78e0b127a3857794d29
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/18/2019
ms.locfileid: "74160876"
---
# <a name="powershell-reference-for-protection-templates"></a>Informazioni di riferimento su PowerShell per i modelli di protezione

>*Si applica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

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

