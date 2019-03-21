---
title: Amministrazione di Azure Rights Management con PowerShell - AIP
description: Informazioni su come usare il modulo di PowerShell per il servizio Azure Rights Management (AADRM) per Azure Information Protection al fine di amministrare tale servizio per l'organizzazione.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 12/12/2018
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: a890e04a-4b70-41b5-8d5f-3c210a669faa
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 09308370778ae066bb2a19d81a111958b5a02f22
ms.sourcegitcommit: d716d3345a6a5adc63814dee28f7c01b55b96770
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/14/2019
ms.locfileid: "57828958"
---
# <a name="administering-the-azure-rights-management-service-by-using-windows-powershell"></a>Amministrazione del servizio Azure Rights Management tramite Windows PowerShell

>*Si applica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

È necessario usare PowerShell per l'amministrazione del servizio Azure Rights Management per Azure Information Protection? Potrebbe non essere necessario se tutte le configurazioni possono essere eseguite nel portale di Azure o nell'interfaccia di amministrazione di Microsoft 365. È tuttavia necessario usare PowerShell per alcune configurazioni avanzate. Potrebbe inoltre essere preferibile usare PowerShell per disporre di una maggiore efficienza di controllo dalla riga di comando e dello scripting.

La tabella nella sezione seguente elenca alcuni degli scenari di configurazione avanzata che usano PowerShell. Nella tabella è indicato inoltre quando la configurazione può essere eseguita anche senza l'uso di PowerShell.

Per un elenco completo dei cmdlet disponibili per questo modulo e le relative informazioni, vedere [AADRM](/powershell/module/aadrm/?view=azureipps#aadrm).

> [!NOTE]
> Per installare il modulo PowerShell, vedere [Installazione del modulo PowerShell AADRM](install-powershell.md).

Oltre a questo modulo di PowerShell sul lato servizio, il client Azure Information Protection installa un modulo supplementare di PowerShell, **AzureInformationProtection**. Questo modulo client supporta la classificazione e la protezione di più file in modo che, ad esempio, sia possibile proteggere in blocco tutti i file in una cartella. Per altre informazioni, vedere [Uso di PowerShell con il client Azure Information Protection](./rms-client/client-admin-guide-powershell.md) nella guida dell'amministratore.

## <a name="cmdlets-grouped-by-administration-task"></a>Cmdlet raggruppati in base all'attività di amministrazione

|Se è necessario…|…usare i seguenti cmdlet|
|-------------------|------------------------------|
|Eseguire la migrazione da un'istanza locale di Rights Management (AD RMS o Windows RMS) ad Azure Information Protection.|[Import-AadrmTpd](/powershell/aadrm/vlatest/import-aadrmtpd)<br /><br />[Set-AadrmKeyProperties](/powershell/module/aadrm/set-aadrmkeyproperties)|
|Connettersi o disconnettersi dal servizio Rights Management per l'organizzazione.|[Connect-AadrmService](/powershell/aadrm/vlatest/connect-aadrmservice)<br /><br />[Disconnect-AadrmService](/powershell/aadrm/vlatest/disconnect-aadrmservice)|
|Generare e gestire la propria chiave tenant (scenario BYOK, Bring Your Own Key)|[Set-AadrmKeyProperties](/powershell/module/aadrm/set-aadrmkeyproperties)<br /><br />[Use-AadrmKeyVaultKey](/powershell/aadrm/vlatest/use-aadrmkeyvaultkey)<br /><br />[Get-AadrmKeys](/powershell/aadrm/vlatest/get-aadrmkeys)|
|Attivare o disattivare il servizio Rights Management per l'organizzazione.<br /><br />È anche possibile eseguire queste azioni dai portali di gestione. Per altre informazioni, vedere [Attivazione di Azure Rights Management](activate-service.md).|[Enable-Aadrm](/powershell/aadrm/vlatest/enable-aadrm)<br /><br />[Disable-Aadrm](/powershell/aadrm/vlatest/disable-aadrm)|
|Gestire il sito di rilevamento dei documenti per Azure Information Protection.|[Disable-AadrmDocumentTrackingFeature](/powershell/aadrm/vlatest/disable-aadrmdocumenttrackingfeature)<br /><br />[Enable-AadrmDocumentTrackingFeature](/powershell/aadrm/vlatest/enable-aadrmdocumenttrackingfeature)<br /><br />[Get-AadrmDocumentTrackingFeature](/powershell/aadrm/vlatest/get-aadrmdocumenttrackingfeature)<br /><br />[Set-AadrmDoNotTrackUserGroup](/powershell/module/aadrm/set-aadrmdonottrackusergroup)<br /><br />[Clear-AadrmDoNotTrackUserGroup](/powershell/module/aadrm/Clear-AadrmDoNotTrackUserGroup)<br /><br />[Get-AadrmDoNotTrackUserGroup](/powershell/module/aadrm/get-AadrmDoNotTrackUserGroup)<br /><br />[Get-AadrmTrackingLog](/powershell/module/aadrm/Get-AadrmTrackingLog)<br /><br />[Get-AadrmDocumentLog](/powershell/module/aadrm/Get-AadrmDocumentLog)|
|Configurare i controlli di selezione utenti per una distribuzione graduale del servizio Azure Rights Management.|[Get-AadrmOnboardingControlPolicy](/powershell/aadrm/vlatest/get-aadrmonboardingcontrolpolicy)<br /><br />[Set-AadrmOnboardingControlPolicy](/powershell/aadrm/vlatest/set-aadrmonboardingcontrolpolicy)|
|Creare e generare modelli di Rights Management per l'organizzazione.<br /><br />È anche possibile eseguire la maggior parte di queste azioni dal portale di Azure, anche se PowerShell offre un controllo più granulare. Per altre informazioni, vedere [Configurazione e gestione dei modelli per Azure Information Protection](configure-policy-templates.md).|[Add-AadrmTemplate](/powershell/aadrm/vlatest/add-aadrmtemplate)<br /><br />[Export-AadrmTemplate](/powershell/aadrm/vlatest/export-aadrmtemplate)<br /><br />[Get-AadrmTemplate](/powershell/aadrm/vlatest/get-aadrmtemplate)<br /><br />[Get-AadrmTemplateProperty](/powershell/aadrm/vlatest/get-aadrmtemplateproperty)<br /><br />[Import-AadrmTemplate](/powershell/aadrm/vlatest/import-aadrmtemplate)<br /><br />[New-AadrmRightsDefinition](/powershell/aadrm/vlatest/new-aadrmrightsdefinition)<br /><br />[Remove-AadrmTemplate](/powershell/aadrm/vlatest/remove-aadrmtemplate)<br /><br />[Set-AadrmTemplateProperty](/powershell/aadrm/vlatest/set-aadrmtemplateproperty)|
|Configurare il numero massimo di giorni per cui è possibile accedere al contenuto che l'organizzazione protegge senza una connessione a Internet (il periodo di validità della licenza di utilizzo).|[Get-AadrmMaxUseLicenseValidityTime](/powershell/aadrm/vlatest/get-aadrmmaxuselicensevaliditytime)<br /><br />[Set-AadrmMaxUseLicenseValidityTime](/powershell/aadrm/vlatest/set-aadrmmaxuselicensevaliditytime)|
|Gestire la funzionalità per utenti con privilegi avanzati di Rights Management per l'organizzazione.|[Enable-AadrmSuperUserFeature](/powershell/aadrm/vlatest/enable-aadrmsuperuserfeature)<br /><br />[Disable-AadrmSuperUserFeature](/powershell/aadrm/vlatest/disable-aadrmsuperuserfeature)<br /><br />[Add-AadrmSuperUser](/powershell/aadrm/vlatest/add-aadrmsuperuser)<br /><br />[Get-AadrmSuperUser](/powershell/aadrm/vlatest/get-aadrmsuperuser)<br /><br />[Remove-AadrmSuperUser](/powershell/aadrm/vlatest/remove-aadrmsuperuser)<br /><br />[Set-AadrmSuperUserGroup](/powershell/aadrm/vlatest/set-aadrmsuperusergroup)<br /><br />[Get-AadrmSuperUserGroup](/powershell/aadrm/vlatest/get-aadrmsuperusergroup)<br /><br />[Clear-AadrmSuperUserGroup](/powershell/aadrm/vlatest/clear-aadrmsuperusergroup)|
|Gestire utenti e gruppi autorizzati ad amministrare il servizio Rights Management per l'organizzazione.|[Add-AadrmRoleBasedAdministrator](/powershell/aadrm/vlatest/add-aadrmrolebasedadministrator)<br /><br />[Get-AadrmRoleBasedAdministrator](/powershell/aadrm/vlatest/get-aadrmrolebasedadministrator)<br /><br />[Remove-AadrmRoleBasedAdministrator](/powershell/aadrm/vlatest/remove-aadrmrolebasedadministrator)|
|Ottenere un log delle attività amministrative relative a Rights Management per l'organizzazione.|[Get-AadrmAdminLog](/powershell/module/aadrm/get-aadrmadminlog)|
|Registrare e analizzare i dati d'uso per Rights Management.|[Get-AadrmUserLog](/powershell/aadrm/vlatest/get-aadrmuserlog)|
|Visualizzare la configurazione corrente del servizio Rights Management per l'organizzazione.|[Get-AadrmConfiguration](/powershell/aadrm/vlatest/get-aadrmconfiguration)|
|Eseguire la migrazione dell'organizzazione da Azure Information Protection a una distribuzione locale di AD RMS.|[Set-AadrmMigrationUrl](/powershell/aadrm/vlatest/set-aadrmmigrationurl)<br /><br />[Get-AadrmMigrationUrl](/powershell/aadrm/vlatest/get-aadrmmigrationurl)|

