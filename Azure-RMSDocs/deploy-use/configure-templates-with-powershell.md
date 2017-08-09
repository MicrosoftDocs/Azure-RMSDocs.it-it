---
title: PowerShell per modelli personalizzati di Azure RMS - AIP
description: "Tutte le operazioni che è possibile eseguire nel portale di Azure per creare e gestire modelli di gestione dei diritti possono essere eseguite anche dalla riga di comando tramite PowerShell. È inoltre possibile esportare e importare modelli, affinché sia possibile copiarli tra tenant o eseguire modifiche in blocco di proprietà complesse nei modelli, ad esempio nomi e descrizioni in più lingue."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 07/31/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 30ee2f77-ce16-4113-bcda-6089131849ec
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: c3b1662275b051ea75dcc104c4f09b5db53dbe3e
ms.sourcegitcommit: 55a71f83947e7b178930aaa85a8716e993ffc063
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/31/2017
---
# <a name="powershell-reference-for-custom-templates"></a>Guida di riferimento di PowerShell per i modelli personalizzati

>*Si applica a: Azure Information Protection, Office 365*

Tutte le operazioni che è possibile eseguire nel portale di Azure per creare e gestire modelli possono essere eseguite anche nella riga di comando tramite PowerShell. È inoltre possibile esportare e importare modelli, affinché sia possibile copiarli tra tenant o eseguire modifiche in blocco di proprietà complesse nei modelli, ad esempio nomi e descrizioni in più lingue.

È anche possibile usare l'esportazione e l'importazione per eseguire il backup e il ripristino dei modelli personalizzati. Come procedura consigliata, eseguire regolarmente il backup dei modelli personalizzati, in modo da poter ripristinare facilmente una versione precedente se si apporta una modifica imprevista.

> [!IMPORTANT]
> Se si vuole usare PowerShell per creare e gestire i modelli di Azure Rights Management, è necessario avere almeno la versione 2.0.0.0 del [modulo Windows PowerShell per Azure RMS](https://go.microsoft.com/fwlink/?LinkId=257721).
> 
> Se il modulo PowerShell è stato installato in precedenza, eseguire il comando seguente in una finestra di PowerShell per verificare il numero di versione: `(Get-Module aadrm -ListAvailable).Version`

Per istruzioni di installazione, vedere [Installazione di Windows PowerShell per Azure Rights Management](install-powershell.md).

I cmdlet che supportano la creazione e la gestione di modelli sono i seguenti:

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