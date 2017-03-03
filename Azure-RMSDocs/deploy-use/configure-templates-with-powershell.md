---
title: PowerShell per modelli personalizzati di Azure RMS - AIP
description: "Tutte le operazioni che è possibile eseguire nel portale di Azure classico per creare e gestire modelli di gestione dei diritti possono essere eseguite anche dalla riga di comando tramite PowerShell. È inoltre possibile esportare e importare modelli, affinché sia possibile copiarli tra tenant o eseguire modifiche in blocco di proprietà complesse nei modelli, ad esempio nomi e descrizioni in più lingue."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/23/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 30ee2f77-ce16-4113-bcda-6089131849ec
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 2131f40b51f34de7637c242909f10952b1fa7d9f
ms.openlocfilehash: fac6f2180c8b108ea237cb36d29058b4907db18a
ms.lasthandoff: 02/24/2017


---



# <a name="powershell-reference-for-custom-templates"></a>Guida di riferimento di PowerShell per i modelli personalizzati

>*Si applica a: Azure Information Protection, Office 365*

Tutte le operazioni che è possibile eseguire nel portale di Azure classico per creare e gestire modelli di gestione dei diritti possono essere eseguite anche dalla riga di comando tramite PowerShell. È inoltre possibile esportare e importare modelli, affinché sia possibile copiarli tra tenant o eseguire modifiche in blocco di proprietà complesse nei modelli, ad esempio nomi e descrizioni in più lingue.

È anche possibile usare l'esportazione e l'importazione per eseguire il backup e il ripristino dei modelli personalizzati. Come procedura consigliata, eseguire regolarmente il backup dei modelli personalizzati, in modo da poter ripristinare facilmente una versione precedente se si apporta una modifica imprevista.

> [!IMPORTANT]
> Per usare Windows PowerShell per creare e gestire i modelli di Azure Rights Management, è necessario avere almeno la versione 2.0.0.0 del [modulo Windows PowerShell per Azure RMS](http://go.microsoft.com/fwlink/?LinkId=257721).
> 
> Se il modulo PowerShell è stato installato in precedenza, eseguire il comando seguente in una finestra di PowerShell per verificare il numero di versione: `(Get-Module aadrm -ListAvailable).Version`

Per istruzioni di installazione, vedere [Installazione di Windows PowerShell per Azure Rights Management](install-powershell.md).

I cmdlet che supportano la creazione e la gestione di modelli sono i seguenti:

-   [Add-AadrmTemplate](https://msdn.microsoft.com/library/azure/dn727075.aspx)

-   [Export-AadrmTemplate](https://msdn.microsoft.com/library/azure/dn727078.aspx)

-   [Get-AadrmTemplate](https://msdn.microsoft.com/library/azure/dn727079.aspx)

-   [Get-AadrmTemplateProperty](https://msdn.microsoft.com/library/azure/dn727081.aspx)

-   [Import-AadrmTemplate](https://msdn.microsoft.com/library/azure/dn727077.aspx)

-   [New-AadrmRightsDefinition](https://msdn.microsoft.com/library/azure/dn727080.aspx)

-   [Remove-AadrmTemplate](https://msdn.microsoft.com/library/azure/dn727082.aspx)

-   [Set-AadrmTemplateProperty](https://msdn.microsoft.com/library/azure/dn727076.aspx)



## <a name="see-also"></a>Vedere anche
[Configurare modelli personalizzati per Azure Rights Management](configure-custom-templates.md)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
