---
title: Amministrazione della protezione da Azure Information Protection tramite PowerShell
description: Informazioni su come usare il modulo di PowerShell per il servizio di protezione da Azure Information Protection per amministrare questo servizio per il tenant.
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 04/28/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: a890e04a-4b70-41b5-8d5f-3c210a669faa
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: efb7f76b89e9918100c9fd092fe321c738fd44ba
ms.sourcegitcommit: 479b3aaea7011750ff85a217298e5ae9185c1dd1
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/28/2020
ms.locfileid: "82224649"
---
# <a name="administering-protection-from-azure-information-protection-by-using-powershell"></a>Amministrazione della protezione da Azure Information Protection tramite PowerShell

>*Si applica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

È necessario usare PowerShell per amministrare il servizio di protezione da Azure Information Protection? Potrebbe non essere necessario se tutte le configurazioni possono essere eseguite nel portale di Azure o nell'interfaccia di amministrazione di Microsoft 365. È tuttavia necessario usare PowerShell per alcune configurazioni avanzate. Potrebbe inoltre essere preferibile usare PowerShell per disporre di una maggiore efficienza di controllo dalla riga di comando e dello scripting.

La tabella nella sezione seguente elenca alcuni degli scenari di configurazione avanzata che usano PowerShell. Nella tabella è indicato inoltre quando la configurazione può essere eseguita anche senza l'uso di PowerShell.

Per un elenco completo dei cmdlet disponibili per questo modulo, con ulteriori informazioni su ciascuno di essi, vedere [AIPService](/powershell/module/aipservice/?view=azureipps#aipservice).

> [!NOTE]
> Per installare questo modulo di PowerShell, vedere [installazione del modulo PowerShell AIPService](install-powershell.md).

Oltre a questo modulo di PowerShell sul lato servizio, il client Azure Information Protection installa un modulo supplementare di PowerShell, **AzureInformationProtection**. Questo modulo client supporta la classificazione e la protezione di più file in modo che, ad esempio, sia possibile proteggere in blocco tutti i file in una cartella. Per altre informazioni, vedere [uso di PowerShell con il client Azure Information Protection](./rms-client/client-admin-guide-powershell.md) dalla guida dell'amministratore.

## <a name="cmdlets-grouped-by-administration-task"></a>Cmdlet raggruppati in base all'attività di amministrazione

|Se è necessario…|…usare i seguenti cmdlet|
|-------------------|------------------------------|
|Eseguire la migrazione da un'istanza locale di Rights Management (AD RMS o Windows RMS) ad Azure Information Protection.|[Import-AipServiceTpd](/powershell/module/aipservice/import-aipservicetpd)<br /><br />[Set-AipServiceKeyProperties](/powershell/module/aipservice/set-aipservicekeyproperties)|
|Connettersi o disconnettersi dal servizio Rights Management per l'organizzazione.|[Connect-AipService](/powershell/module/aipservice/connect-aipservice)<br /><br />[Disconnect-AipServiceService](/powershell/module/aipservice/disconnect-aipservice)|
|Generare e gestire la propria chiave tenant (scenario BYOK, Bring Your Own Key)|[Set-AipServiceKeyProperties](/powershell/module/aipservice/set-aipservicekeyproperties)<br /><br />[Use-AipServiceKeyVaultKey](/powershell/module/aipservice/use-aipservicekeyvaultkey)<br /><br />[Get-AipServiceKeys](/powershell/module/aipservice/get-aipservicekeys)|
|Attivare o disattivare il servizio Rights Management per l'organizzazione.<br /><br />È anche possibile eseguire queste azioni dai portali di gestione. Per altre informazioni, vedere [Attivazione del servizio di protezione da Azure Information Protection](activate-service.md).|[Enable-AipService](/powershell/module/aipservice/enable-aipservice)<br /><br />[Disable-AipService](/powershell/module/aipservice/disable-aipservice)|
|Gestire il sito di rilevamento dei documenti per Azure Information Protection.|[Disable-AipServiceDocumentTrackingFeature](/powershell/module/aipservice/disable-aipservicedocumenttrackingfeature)<br /><br />[Enable-AipServiceDocumentTrackingFeature](/powershell/module/aipservice/enable-aipservicedocumenttrackingfeature)<br /><br />[Get-AipServiceDocumentTrackingFeature](/powershell/module/aipservice/get-aipservicedocumenttrackingfeature)<br /><br />[Set-AipServiceDoNotTrackUserGroup](/powershell/module/aipservice/set-aipservicedonottrackusergroup)<br /><br />[Clear-AipServiceDoNotTrackUserGroup](/powershell/module/aipservice/Clear-AipServiceDoNotTrackUserGroup)<br /><br />[Get-AipServiceDoNotTrackUserGroup](/powershell/module/aipservice/get-AipServiceDoNotTrackUserGroup)<br /><br />[Get-AipServiceTrackingLog](/powershell/module/aipservice/Get-AipServiceTrackingLog)<br /><br />[Get-AipServiceDocumentLog](/powershell/module/aipservice/Get-AipServiceDocumentLog)|
|Configurare i controlli di selezione utenti per una distribuzione graduale del servizio Azure Rights Management.|[Get-AipServiceOnboardingControlPolicy](/powershell/module/aipservice/get-aipserviceonboardingcontrolpolicy)<br /><br />[Set-AipServiceOnboardingControlPolicy](/powershell/module/aipservice/set-aipserviceonboardingcontrolpolicy)|
|Creare e generare modelli di Rights Management per l'organizzazione.<br /><br />È anche possibile eseguire la maggior parte di queste azioni dal portale di Azure, anche se PowerShell offre un controllo più granulare. Per altre informazioni, vedere [Configurazione e gestione dei modelli per Azure Information Protection](configure-policy-templates.md).|[Add-AipServiceTemplate](/powershell/module/aipservice/add-aipservicetemplate)<br /><br />[Export-AipServiceTemplate](/powershell/module/aipservice/export-aipservicetemplate)<br /><br />[Get-AipServiceTemplate](/powershell/module/aipservice/get-aipservicetemplate)<br /><br />[Get-AipServiceTemplateProperty](/powershell/module/aipservice/get-aipservicetemplateproperty)<br /><br />[Import-AipServiceTemplate](/powershell/module/aipservice/import-aipservicetemplate)<br /><br />[New-AipServiceRightsDefinition](/powershell/module/aipservice/new-aipservicerightsdefinition)<br /><br />[Remove-AipServiceTemplate](/powershell/module/aipservice/remove-aipservicetemplate)<br /><br />[Set-AipServiceTemplateProperty](/powershell/module/aipservice/set-aipservicetemplateproperty)|
|Configurare il numero massimo di giorni per cui è possibile accedere al contenuto che l'organizzazione protegge senza una connessione Internet (periodo di validità della licenza d'uso).|[Get-AipServiceMaxUseLicenseValidityTime](/powershell/module/aipservice/get-aipservicemaxuselicensevaliditytime)<br /><br />[Set-AipServiceMaxUseLicenseValidityTime](/powershell/module/aipservice/set-aipservicemaxuselicensevaliditytime)|
|Gestire la funzionalità per utenti con privilegi avanzati di Rights Management per l'organizzazione.|[Enable-AipServiceSuperUserFeature](/powershell/module/aipservice/enable-aipservicesuperuserfeature)<br /><br />[Disable-AipServiceSuperUserFeature](/powershell/module/aipservice/disable-aipservicesuperuserfeature)<br /><br />[Add-AipServiceSuperUser](/powershell/module/aipservice/add-aipservicesuperuser)<br /><br />[Get-AipServiceSuperUser](/powershell/module/aipservice/get-aipservicesuperuser)<br /><br />[Remove-AipServiceSuperUser](/powershell/module/aipservice/remove-aipservicesuperuser)<br /><br />[Set-AAipServiceSuperUserGroup](/powershell/module/aipservice/set-aipservicesuperusergroup)<br /><br />[Get-AipServiceSuperUserGroup](/powershell/module/aipservice/get-aipservicesuperusergroup)<br /><br />[Clear-AipServiceSuperUserGroup](/powershell/module/aipservice/clear-aipservicesuperusergroup)|
|Gestire utenti e gruppi autorizzati ad amministrare il servizio Rights Management per l'organizzazione.|[Add-AIP-ServiceRoleBasedAdministrator](/powershell/module/aipservice/add-aipservicerolebasedadministrator)<br /><br />[Get-AIP-ServiceRoleBasedAdministrator](/powershell/module/aipservice/get-aipservicerolebasedadministrator)<br /><br />[Remove-AIP-ServiceRoleBasedAdministrator](/powershell/module/aipservice/remove-aipservicerolebasedadministrator)|
|Ottenere un log delle attività amministrative relative a Rights Management per l'organizzazione.|[Get-AipServiceAdminLog](/powershell/module/aipservice/get-aipserviceadminlog)|
|Registrare e analizzare i dati d'uso per Rights Management.|[Get-AipServiceUserLog](/powershell/module/aipservice/get-aipserviceuserlog)|
|Visualizzare la configurazione corrente del servizio Rights Management per l'organizzazione.|[Get-AipServiceConfiguration](/powershell/module/aipservice/get-aipserviceconfiguration)|
|Eseguire la migrazione dell'organizzazione da Azure Information Protection a una distribuzione locale di AD RMS.|[Set-AipServiceMigrationUrl](/powershell/module/aipservice/set-aipservicemigrationurl)<br /><br />[Get-AipServiceMigrationUrl](/powershell/module/aipservice/get-aipservicemigrationurl)|

