---
title: Amministrazione di Azure Rights Management con PowerShell - AIP
description: Informazioni su come usare il modulo di PowerShell per il servizio Azure Rights Management (AADRM) per Azure Information Protection al fine di amministrare tale servizio per l&quot;organizzazione.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/14/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: a890e04a-4b70-41b5-8d5f-3c210a669faa
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 2131f40b51f34de7637c242909f10952b1fa7d9f
ms.openlocfilehash: 085dc82fcb9632bfdf4fb1b14ca5c632846e81d0
ms.lasthandoff: 02/24/2017


---

# <a name="administering-the-azure-rights-management-service-by-using-windows-powershell"></a>Amministrazione del servizio Azure Rights Management tramite Windows PowerShell

>*Si applica a: Azure Information Protection, Office 365*

È necessario usare PowerShell per l'amministrazione del servizio Azure Rights Management per Azure Information Protection? Potrebbe non essere necessario se si è un amministratore globale e l'unica configurazione richiesta per il servizio consiste nell'attivazione (o disattivazione) e nella configurazione di modelli di Rights Management.

È tuttavia necessario usare PowerShell per le configurazioni più avanzate e anche se non si è un amministratore globale, ma sono state ricevute da un amministratore globale le autorizzazioni per amministrare il servizio. Potrebbe inoltre essere preferibile usare PowerShell per disporre di una maggiore efficienza di controllo dalla riga di comando e dello scripting.

La tabella nella sezione seguente elenca alcuni degli scenari di configurazione avanzata che usano PowerShell. Nella tabella è indicato inoltre quando la configurazione può essere eseguita anche senza l'uso di PowerShell.

Per un elenco completo dei cmdlet disponibili con ulteriori informazioni su ciascuno di essi, vedere [cmdlet di Azure Rights Management](http://msdn.microsoft.com/library/azure/dn629398.aspx).

> [!NOTE]
> Per installare questo modulo di PowerShell, vedere [Installazione di Windows PowerShell per Microsoft Azure Rights Management](install-powershell.md).

Oltre a questo modulo di PowerShell sul lato servizio, il client Azure Information Protection installa un modulo supplementare di PowerShell, **AzureInformationProtection**. Questo modulo client supporta la classificazione e la protezione di più file in modo che, ad esempio, sia possibile proteggere in blocco tutti i file in una cartella. Per altre informazioni, vedere [Uso di PowerShell con il client Azure Information Protection](../rms-client/client-admin-guide-powershell.md) nella guida dell'amministratore.

## <a name="cmdlets-grouped-by-administration-task"></a>Cmdlet raggruppati in base all'attività di amministrazione

|Se è necessario…|…usare i seguenti cmdlet|
|-------------------|------------------------------|
|Eseguire la migrazione da un'istanza locale di Rights Management (AD RMS o Windows RMS) ad Azure Information Protection.|[Import-AadrmTpd](http://msdn.microsoft.com/library/azure/dn857523.aspx)|
|Connettersi o disconnettersi dal servizio [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] per l'organizzazione|[Connect-AadrmService](http://msdn.microsoft.com/library/azure/dn629415.aspx)<br /><br />[Disconnect-AadrmService](http://msdn.microsoft.com/library/azure/dn629416.aspx)|
|Generare e gestire la propria chiave tenant (scenario BYOK, Bring Your Own Key)|[Use-AadrmKeyVaultKey](https://msdn.microsoft.com/library/azure/mt759829.aspx)<br /><br />[Get-AadrmKeys](http://msdn.microsoft.com/library/azure/dn629420.aspx)|
|Attivare o disattivare il servizio [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] per l'organizzazione<br /><br />È anche possibile eseguire queste azioni dai portali di gestione. Per altre informazioni, vedere [Attivazione di Azure Rights Management](activate-service.md).|[Enable-Aadrm](http://msdn.microsoft.com/library/azure/dn629412.aspx)<br /><br />[Disable-Aadrm](http://msdn.microsoft.com/library/azure/dn629422.aspx)|
|Disabilitare o abilitare il sito di rilevamento dei documenti per Azure Information Protection.|[Disable-AadrmDocumentTrackingFeature](https://msdn.microsoft.com/library/azure/mt548471.aspx)<br /><br />[Enable-AadrmDocumentTrackingFeature](https://msdn.microsoft.com/library/azure/mt548469.aspx)<br /><br />[Get-AadrmDocumentTrackingFeature](https://msdn.microsoft.com/library/azure/mt548470.aspx)|
|Configurare i controlli di selezione utenti per una distribuzione graduale del servizio Azure Rights Management.|[Get-AadrmOnboardingControlPolicy](http://msdn.microsoft.com/library/azure/dn857522.aspx)<br /><br />[Set-AadrmOnboardingControlPolicy](http://msdn.microsoft.com/library/azure/dn857521.aspx)|
|Creare e generare modelli di Rights Management per l'organizzazione.<br /><br />È anche possibile eseguire la maggior parte di queste azioni dal portale di Azure classico, anche se PowerShell offre un controllo più granulare. Per altre informazioni, vedere [Configurazione di modelli personalizzati per il servizio Azure Rights Management](configure-custom-templates.md).|[Add-AadrmTemplate](http://msdn.microsoft.com/library/azure/dn727075.aspx)<br /><br />[Export-AadrmTemplate](http://msdn.microsoft.com/library/azure/dn727078.aspx)<br /><br />[Get-AadrmTemplate](http://msdn.microsoft.com/library/azure/dn727079.aspx)<br /><br />[Get-AadrmTemplateProperty](http://msdn.microsoft.com/library/azure/dn727081.aspx)<br /><br />[Import-AadrmTemplate](http://msdn.microsoft.com/library/azure/dn727077.aspx)<br /><br />[New-AadrmRightsDefinition](http://msdn.microsoft.com/library/azure/dn727080.aspx)<br /><br />[Remove-AadrmTemplate](http://msdn.microsoft.com/library/azure/dn727082.aspx)<br /><br />[Set-AadrmTemplateProperty](http://msdn.microsoft.com/library/azure/dn727076.aspx)|
|Configurare il numero massimo di giorni per cui è possibile accedere al contenuto che l'organizzazione protegge senza una connessione a Internet (il periodo di validità della licenza di utilizzo).|[Get-AadrmMaxUseLicenseValidityTime](https://msdn.microsoft.com/library/azure/dn932062.aspx)<br /><br />[Set-AadrmMaxUseLicenseValidityTime](https://msdn.microsoft.com/library/azure/dn932063.aspx)|
|Gestire la funzionalità per utenti con privilegi avanzati di [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] per l'organizzazione|[Enable-AadrmSuperUserFeature](https://msdn.microsoft.com/library/azure/dn629400.aspx)<br /><br />[Disable-AadrmSuperUserFeature](https://msdn.microsoft.com/library/azure/dn629428.aspx)<br /><br />[Add-AadrmSuperUser](http://msdn.microsoft.com/library/azure/dn629411.aspx)<br /><br />[Get-AadrmSuperUser](https://msdn.microsoft.com/library/azure/dn629408.aspx)<br /><br />[Remove-AadrmSuperUser](https://msdn.microsoft.com/library/azure/dn629405.aspx)<br /><br />[Set-AadrmSuperUserGroup](https://msdn.microsoft.com/library/azure/mt653943.aspx)<br /><br />[Get-AadrmSuperUserGroup](https://msdn.microsoft.com/library/azure/mt653942.aspx)<br /><br />[Clear-AadrmSuperUserGroup](https://msdn.microsoft.com/library/azure/mt653944.aspx)|
|Gestire utenti e gruppi autorizzati ad amministrare il servizio [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] per l'organizzazione|[Add-AadrmRoleBasedAdministrator](http://msdn.microsoft.com/library/azure/dn629417.aspx)<br /><br />[Get-AadrmRoleBasedAdministrator](https://msdn.microsoft.com/library/azure/dn629407.aspx)<br /><br />[Remove-AadrmRoleBasedAdministrator](https://msdn.microsoft.com/library/azure/dn629424.aspx)|
|Ottenere un log delle attività amministrative relative a [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] per l'organizzazione|[Get-AadrmAdminLog](https://msdn.microsoft.com/library/azure/dn629430.aspx)|
|Registrare e analizzare i dati d'uso per [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)]|[Get-AadrmUserLog](https://msdn.microsoft.com/library/azure/mt653941.aspx)|
|Visualizzare la configurazione corrente del servizio [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] per l'organizzazione|[Get-AadrmConfiguration](http://msdn.microsoft.com/library/azure/dn629410.aspx)|
|Eseguire la migrazione dell'organizzazione da Azure Information Protection a una distribuzione locale di AD RMS.|[Set-AadrmMigrationUrl](https://msdn.microsoft.com/library/azure/dn629429.aspx)<br /><br />[Get-AadrmMigrationUrl](http://msdn.microsoft.com/library/azure/dn629403.aspx)|

[!INCLUDE[Commenting house rules](../includes/houserules.md)]



