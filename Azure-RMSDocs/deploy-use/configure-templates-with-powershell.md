---
title: PowerShell per i modelli di protezione - Azure Information Protection
description: "Tutte le operazioni che è possibile eseguire nel portale di Azure per creare e gestire i modelli di protezione possono essere eseguite anche nella riga di comando tramite PowerShell. È inoltre possibile esportare e importare modelli, affinché sia possibile copiarli tra tenant o eseguire modifiche in blocco di proprietà complesse nei modelli, ad esempio nomi e descrizioni in più lingue."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/23/2018
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 30ee2f77-ce16-4113-bcda-6089131849ec
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 051144562b1c26a22953f6e83a41b4902404fd2f
ms.sourcegitcommit: 85250f5ea80c2ee22197058ff2f65a79503b0f0c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/24/2018
---
# <a name="powershell-reference-for-protection-templates"></a>Informazioni di riferimento su PowerShell per i modelli di protezione

>*Si applica a: Azure Information Protection, Office 365*

Le impostazioni di protezione di Azure Information Protection vengono salvate in modelli di protezione. Tutte le operazioni che è possibile eseguire nel portale di Azure per creare e gestire le impostazioni di protezione possono essere eseguite anche nella riga di comando tramite PowerShell. 

È anche possibile esportare e importare i modelli di protezione. Queste due azioni consentono di copiare i modelli di protezione tra tenant o apportare modifiche in blocco per proprietà complesse, come i nomi e le descrizioni in più lingue.

È anche possibile usare l'esportazione e l'importazione per eseguire il backup e il ripristino dei modelli di protezione. Come procedura consigliata, eseguire regolarmente il backup dei modelli. In questo modo, se si apporta una modifica non appropriata alle impostazioni di protezione, è possibile ripristinare facilmente una versione precedente.

Per le istruzioni di installazione, vedere [Installazione del modulo PowerShell AADRM](install-powershell.md).

I cmdlet che supportano la creazione e la gestione dei modelli di protezione sono i seguenti:

- [Add-AadrmTemplate](/powershell/module/aadrm/add-aadrmtemplate)

- [Export-AadrmTemplate](/powershell/module/aadrm/export-aadrmtemplate)

- [Get-AadrmTemplate](/powershell/module/aadrm/get-aadrmtemplate)

- [Get-AadrmTemplateProperty](/powershell/module/aadrm/get-aadrmtemplateproperty)

- [Import-AadrmTemplate](/powershell/module/aadrm/import-aadrmtemplate)

- [New-AadrmRightsDefinition](/powershell/module/aadrm/new-aadrmrightsdefinition)

- [Remove-AadrmTemplate](/powershell/module/aadrm/remove-aadrmtemplate)

- [Set-AadrmTemplateProperty](/powershell/module/aadrm/set-aadrmtemplateproperty)



## <a name="see-also"></a>Vedere anche
[Configurazione e gestione dei modelli per Azure Information Protection](configure-policy-templates.md)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
