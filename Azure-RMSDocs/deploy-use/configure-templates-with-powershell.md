---
# required metadata

title: Guida di riferimento di PowerShell per i modelli personalizzati | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 30ee2f77-ce16-4113-bcda-6089131849ec

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---



# Guida di riferimento di PowerShell per i modelli personalizzati
Tutte le operazioni che è possibile eseguire nel portale di Azure classico per creare e gestire modelli possono essere eseguite anche nella riga di comando tramite PowerShell. È inoltre possibile esportare e importare modelli, affinché sia possibile copiarli tra tenant o eseguire modifiche in blocco di proprietà complesse nei modelli, ad esempio nomi e descrizioni in più lingue.

È anche possibile usare l'esportazione e l'importazione per eseguire il backup e il ripristino dei modelli personalizzati. Come procedura consigliata, eseguire regolarmente il backup dei modelli personalizzati, in modo da poter ripristinare facilmente una versione precedente se si apporta una modifica imprevista.

> [!IMPORTANT]
> Per utilizzare Windows PowerShell per creare e gestire i modelli di criteri dei diritti di Azure RMS, è necessario avere almeno la versione 2.0.0.0 del [modulo Windows PowerShell per Azure RMS](http://go.microsoft.com/fwlink/?LinkId=257721).
> 
> Se il modulo PowerShell è stato installato in precedenza, eseguire il seguente comando in una finestra di PowerShell per verificare il numero di versione: `(Get-Module aadrm -ListAvailable).Version`

Per le istruzioni di installazione, vedere [Installazione di Windows PowerShell per Microsoft Azure Rights Management](install-powershell.md).

I cmdlet che supportano la creazione e la gestione di modelli sono i seguenti:

-   [Add-AadrmTemplate](https://msdn.microsoft.com/library/azure/dn727075.aspx)

-   [Expot-AadrmTemplate](https://msdn.microsoft.com/library/azure/dn727078.aspx)

-   [Get-AadrmTemplate](https://msdn.microsoft.com/library/azure/dn727079.aspx)

-   [Get-AadrmTemplateProperty](https://msdn.microsoft.com/library/azure/dn727081.aspx)

-   [Impot-AadrmTemplate](https://msdn.microsoft.com/library/azure/dn727077.aspx)

-   [New-AadrmRightsDefinition](https://msdn.microsoft.com/library/azure/dn727080.aspx)

-   [Remove-AadrmTemplate](https://msdn.microsoft.com/library/azure/dn727082.aspx)

-   [Set-AadrmTemplateProperty](https://msdn.microsoft.com/library/azure/dn727076.aspx)



## Vedere anche
[Configurare modelli personalizzati per Azure Rights Management](configure-custom-templates.md)

<!--HONumber=Apr16_HO3-->


