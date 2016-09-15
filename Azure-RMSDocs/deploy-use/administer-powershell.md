---
title: Amministrazione di Rights Management di Windows Azure mediante Windows PowerShell | Azure RMS
description: Informazioni su come usare il modulo di Windows PowerShell per Azure RMS (AADRM) per gestire tale servizio per l'organizzazione.
author: cabailey
manager: mbaldwin
ms.date: 08/25/2016
ms.topic: article
ms.prod: 
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: a890e04a-4b70-41b5-8d5f-3c210a669faa
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: ad32910b482ca9d92b4ac8f3f123eda195db29cd
ms.openlocfilehash: 1660fa08af036267094784cb729215836208a9a1


---

# Amministrazione di Rights Management di Windows Azure mediante Windows PowerShell

>*Si applica a: Azure Rights Management, Office 365*

Nonostante sia possibile attivare Microsoft [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] (Azure RMS) usando l'interfaccia di amministrazione di [!INCLUDE[o365_2](../includes/o365_2_md.md)] o il portale di Azure classico, a tale scopo è anche possibile usare il modulo Windows PowerShell per [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] (AADRM).

Dopo l'attivazione di [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)], potrebbero non essere necessarie altre operazioni di amministrazione per il servizio. Alcuni scenari di configurazione avanzata potrebbero tuttavia richiedere l'uso del modulo Windows PowerShell per [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)]. La tabella riportata di seguito elenca alcuni degli scenari di configurazione avanzata che usano Windows PowerShell. Per un elenco completo dei cmdlet disponibili con ulteriori informazioni su ciascuno di essi, vedere [cmdlet di Azure Rights Management](http://msdn.microsoft.com/library/azure/dn629398.aspx).

> [!NOTE]
> Se è necessario installare il modulo di Windows PowerShell per [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)], vedere [Installazione di Windows PowerShell per Microsoft Azure Rights Management](install-powershell.md).

È inoltre disponibile un modulo di Windows PowerShell supplementare, **RMSProtection**, che supporta sia Azure RMS che AD RMS. Questo modulo supporta la protezione e la rimozione della protezione da più file in modo che, ad esempio, sia possibile proteggere in gruppo tutti i file in una cartella. Per altre informazioni, vedere la sezione [Opzioni di scripting per gli utenti con privilegi avanzati](configure-super-users.md#scripting-options-for-super-users) dell'articolo [Configurazione degli utenti con privilegi avanzati per Rights Management di Azure e servizi di individuazione o ripristino dei dati](configure-super-users.md).

|Se è necessario…|…usare i seguenti cmdlet|
|-------------------|------------------------------|
|Eseguire la migrazione da un'istanza locale di Rights Management (AD RMS o Windows RMS) a [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)].|[Import-AadrmTpd](http://msdn.microsoft.com/library/azure/dn857523.aspx)|
|Connettersi o disconnettersi dal servizio [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] per l'organizzazione|[Connect-AadrmService](http://msdn.microsoft.com/library/azure/dn629415.aspx)<br /><br />[Disconnect-AadrmService](http://msdn.microsoft.com/library/azure/dn629416.aspx)|
|Generare e gestire la propria chiave tenant (scenario BYOK, Bring Your Own Key)|[Use-AadrmKeyVaultKey](https://msdn.microsoft.com/library/azure/mt759829.aspx)<br /><br />[Get-AadrmKeys](http://msdn.microsoft.com/library/azure/dn629420.aspx)|
|Attivare o disattivare il servizio [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] per l'organizzazione|[Enable-Aadrm](http://msdn.microsoft.com/library/azure/dn629412.aspx)<br /><br />[Disable-Aadrm](http://msdn.microsoft.com/library/azure/dn629422.aspx)|
|Disabilitare o abilitare il sito di rilevamento dei documenti per Azure Rights Management.|[Disable-AadrmDocumentTrackingFeature](https://msdn.microsoft.com/library/azure/mt548471.aspx)<br /><br />[Enable-AadrmDocumentTrackingFeature](https://msdn.microsoft.com/library/azure/mt548469.aspx)<br /><br />[Get-AadrmDocumentTrackingFeature](https://msdn.microsoft.com/library/azure/mt548470.aspx)|
|Configurare i controlli di implementazione per una distribuzione graduale di Azure Rights Management.|[Get-AadrmOnboardingControlPolicy](http://msdn.microsoft.com/library/azure/dn857522.aspx)<br /><br />[Set-AadrmOnboardingControlPolicy](http://msdn.microsoft.com/library/azure/dn857521.aspx)|
|Creare e generare modelli di criteri per i diritti d'uso per l'organizzazione|[Add-AadrmTemplate](http://msdn.microsoft.com/library/azure/dn727075.aspx)<br /><br />[Expot-AadrmTemplate](http://msdn.microsoft.com/library/azure/dn727078.aspx)<br /><br />[Get-AadrmTemplate](http://msdn.microsoft.com/library/azure/dn727079.aspx)<br /><br />[Get-AadrmTemplateProperty](http://msdn.microsoft.com/library/azure/dn727081.aspx)<br /><br />[Impot-AadrmTemplate](http://msdn.microsoft.com/library/azure/dn727077.aspx)<br /><br />[New-AadrmRightsDefinition](http://msdn.microsoft.com/library/azure/dn727080.aspx)<br /><br />[Remove-AadrmTemplate](http://msdn.microsoft.com/library/azure/dn727082.aspx)<br /><br />[Set-AadrmTemplateProperty](http://msdn.microsoft.com/library/azure/dn727076.aspx)|
|Configurare il numero massimo di giorni per cui è possibile accedere al contenuto che l'organizzazione protegge senza una connessione a Internet (il periodo di validità della licenza di utilizzo).|[Get-AadrmMaxUseLicenseValidityTime](https://msdn.microsoft.com/library/azure/dn932062.aspx)<br /><br />[Set-AadrmMaxUseLicenseValidityTime](https://msdn.microsoft.com/library/azure/dn932063.aspx)|
|Gestire la funzionalità per utenti con privilegi avanzati di [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] per l'organizzazione|[Enable-AadrmSuperUserFeature](https://msdn.microsoft.com/library/azure/dn629400.aspx)<br /><br />[Disable-AadrmSuperUserFeature](https://msdn.microsoft.com/library/azure/dn629428.aspx)<br /><br />[Add-AadrmSuperUser](http://msdn.microsoft.com/library/azure/dn629411.aspx)<br /><br />[Get-AadrmSuperUser](https://msdn.microsoft.com/library/azure/dn629408.aspx)<br /><br />[Remove-AadrmSuperUser](https://msdn.microsoft.com/library/azure/dn629405.aspx)<br /><br />[Set-AadrmSuperUserGroup](https://msdn.microsoft.com/library/azure/mt653943.aspx)<br /><br />[Get-AadrmSuperUserGroup](https://msdn.microsoft.com/library/azure/mt653942.aspx)<br /><br />[Clear-AadrmSuperUserGroup](https://msdn.microsoft.com/library/azure/mt653944.aspx)|
|Gestire utenti e gruppi autorizzati ad amministrare il servizio [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] per l'organizzazione|[Add-AadrmRoleBasedAdministrator](http://msdn.microsoft.com/library/azure/dn629417.aspx)<br /><br />[Get-AadrmRoleBasedAdministrator](https://msdn.microsoft.com/library/azure/dn629407.aspx)<br /><br />[Remove-AadrmRoleBasedAdministrator](https://msdn.microsoft.com/library/azure/dn629424.aspx)|
|Ottenere un log delle attività amministrative relative a [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] per l'organizzazione|[Get-AadrmAdminLog](https://msdn.microsoft.com/library/azure/dn629430.aspx)|
|Registrare e analizzare i dati d'uso per [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)]|[Get-AadrmUserLog](https://msdn.microsoft.com/library/azure/mt653941.aspx)|
|Visualizzare la configurazione corrente del servizio [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] per l'organizzazione|[Get-AadrmConfiguration](http://msdn.microsoft.com/library/azure/dn629410.aspx)|
|Eseguire la migrazione dell'organizzazione da [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] a una distribuzione locale di AD RMS.|[Set-AadrmMigrationUrl](https://msdn.microsoft.com/library/azure/dn629429.aspx)<br /><br />[Get-AadrmMigrationUrl](http://msdn.microsoft.com/library/azure/dn629403.aspx)|






<!--HONumber=Aug16_HO4-->


