---
title: Configurare utenti con privilegi avanzati per Azure Rights Management - AIP
description: "Informazioni sulla funzionalità per utenti con privilegi avanzati del servizio Azure Rights Management di Azure Information Protection e relativa implementazione in modo che gli utenti e i servizi autorizzati possano sempre leggere e controllare i dati che Azure Rights Management protegge per l&quot;organizzazione. Questa possibilità viene definita anche &quot;ragionamento sui dati&quot; e riveste un ruolo di importanza critica nel mantenimento del controllo sui dati dell&quot;organizzazione."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/08/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: acb4c00b-d3a9-4d74-94fe-91eeb481f7e3
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 2131f40b51f34de7637c242909f10952b1fa7d9f
ms.openlocfilehash: f1c50d67ba03cee9846e81f98aad6da0da33a951
ms.lasthandoff: 02/24/2017


---

# <a name="configuring-super-users-for-azure-rights-management-and-discovery-services-or-data-recovery"></a>Configurazione degli utenti con privilegi avanzati per Azure Rights Management e servizi di individuazione o ripristino dei dati

>*Si applica a: Azure Information Protection, Office 365*

La funzionalità per utenti con privilegi avanzati del servizio Azure Rights Management di Azure Information Protection garantisce che gli utenti e i servizi autorizzati possano sempre leggere e controllare i dati che Azure Rights Management protegge per l'organizzazione. Se necessario, rimuovere la protezione o modificare la protezione applicata in precedenza. Un utente con privilegi avanzati dispone sempre dei diritti completi di proprietario per tutte le licenze concesse dal tenant Azure Information Protection dell'organizzazione. Questa possibilità viene definita anche "ragionamento sui dati" e riveste un ruolo di importanza critica nel mantenimento del controllo sui dati dell'organizzazione. Ad esempio, utilizzare questa funzionalità per uno qualsiasi dei seguenti scenari:

-   Un dipendente lascia l'organizzazione ed è necessario leggere i file che ha protetto.

-   Un amministratore IT deve rimuovere il criterio di protezione corrente che è stato configurato per i file e applicare un nuovo criterio di protezione.

-   Exchange Server deve indicizzare le caselle postali per le operazioni di ricerca.

-   Si dispone di servizi IT esistenti per le soluzioni di prevenzione della perdita dei dati, per il gateway di crittografia del contenuto (CEG) e per i prodotti anti-malware che richiedono l'analisi dei file che sono già protetti.

-   È necessario decrittografare i file per questioni di controllo, legali o per altri motivi di conformità.

Per impostazione predefinita, questo ruolo non è abilitato e a esso non sono assegnati utenti. Viene abilitata automaticamente per l'utente se si configura il connettore Rights Management per Exchange, e non è necessaria per i servizi standard che eseguono Exchange Online, SharePoint Online o SharePoint Server.

Se è necessario abilitare manualmente la funzionalità per utenti con privilegi avanzati, usare il cmdlet [Enable-AadrmSuperUserFeature](https://msdn.microsoft.com/library/azure/dn629400.aspx) di Windows PowerShell, quindi assegnare utenti o account del servizio in base alla necessità mediante il cmdlet [Add-AadrmSuperUser](https://msdn.microsoft.com/library/azure/dn629411.aspx) o il cmdlet [Set-AadrmSuperUserGroup](https://msdn.microsoft.com/library/azure/mt653943.aspx) e aggiungere utenti o altri gruppi a questo gruppo in base alla necessità. 

> [!NOTE]
> Se non è stato ancora installato il modulo di Windows PowerShell per [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)], vedere [Installazione di Windows PowerShell per Azure Rights Management](install-powershell.md).

Le procedure consigliate per la funzionalità per utenti con privilegi avanzati:

-   Limitare e monitorare gli amministratori a cui viene assegnato un ruolo di amministratore globale per il tenant di Office 365 o Azure Information Protection o a cui viene assegnato il ruolo GlobalAdministrator mediante il cmdlet [Add-AadrmRoleBasedAdministrator](https://msdn.microsoft.com/library/azure/dn629417.aspx). Questi utenti possono abilitare la funzionalità per utenti con privilegi avanzati e assegnare agli utenti (e a se stessi) la condizione di utenti con privilegi avanzati, e potenzialmente decrittografare tutti i file che l'organizzazione protegge.

-   Per verificare gli utenti e gli account del servizio che vengono assegnati individualmente come utenti con privilegi avanzati, usare il cmdlet [Get-AadrmSuperUser](https://msdn.microsoft.com/library/azure/dn629408.aspx). Per verificare se è stato configurato un gruppo di utenti con privilegi avanzati, usare il cmdlet [Get-AadrmSuperUser](https://msdn.microsoft.com/library/azure/mt653942.aspx) e gli strumenti standard per la gestione degli utenti per verificare i membri che appartengono a questo gruppo. Come tutte le azioni di amministrazione, quelle di abilitare o disabilitare la caratteristica con privilegi avanzati, e aggiungere o rimuovere gli utenti con privilegi avanzati che vengono registrati, possono essere controllate tramite il comando [Get-AadrmAdminLog](https://msdn.microsoft.com/library/azure/dn629430.aspx) . Quando gli utenti con privilegi avanzati eseguono la decrittografia dei file, questa azione viene registrata e può essere controllata con la [registrazione dell'utilizzo](log-analyze-usage.md).

-   Se non è necessaria la funzionalità per utenti con privilegi avanzati per i servizi quotidiani, abilitare la funzionalità solo quando è necessario e disabilitarla nuovamente utilizzando il cmdlet [Disable AadrmSuperUserFeature](https://msdn.microsoft.com/library/azure/dn629428.aspx) .

L'estratto dal log seguente mostra alcune voci di esempio relative all'uso del cmdlet Get-AadrmAdminLog. In questo esempio, l'amministratore di Contoso Ltd verifica che la funzionalità per utenti con privilegi avanzati sia disabilitata, aggiunge Richard Simone come utente con privilegi avanzati, controlla che Richard sia l'unico utente con privilegi avanzati configurato per il servizio Azure Rights Management e quindi abilita la funzionalità per utenti con privilegi avanzati in modo che Richard sia in grado di decrittografare alcuni file che sono stati protetti da un dipendente che ora ha lasciato l'azienda.

`2015-08-01T18:58:20    admin@contoso.com    GetSuperUserFeatureState    Passed    Disabled`

`2015-08-01T18:59:44    admin@contoso.com    AddSuperUser -id rsimone@contoso.com    Passed    True`

`2015-08-01T19:00:51    admin@contoso.com    GetSuperUser    Passed    rsimone@contoso.com`

`2015-08-01T19:01:45    admin@contoso.com    SetSuperUserFeatureState -state Enabled    Passed    True`

## <a name="scripting-options-for-super-users"></a>Opzioni di scripting per gli utenti con privilegi avanzati
Spesso, la persona cui viene assegnato il ruolo di utente con privilegi avanzati per [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] dovrà rimuovere la protezione da più file, in più posizioni. Sebbene sia possibile effettuare questa operazione manualmente, è più efficiente (e spesso più affidabile) eseguire uno script. A tale scopo, è possibile usare i cmdlet [Unprotect-RMSFile](/powershell/azureinformationprotection/vlatest/unprotect-rmsfile) e [Protect-RMSFile](/powershell/azureinformationprotection/vlatest/protect-rmsfile) come necessario. 

Se si usano la classificazione e la protezione, è anche possibile usare [Set-AIPFileLabel](/powershell/azureinformationprotection/vlatest/set-aipfilelabel) per applicare una nuova etichetta che non applica la protezione oppure rimuovere l'etichetta che ha applicato la protezione. 

Per altre informazioni su questi cmdlet, vedere [Uso di PowerShell con il client Azure Information Protection](../rms-client/client-admin-guide-powershell.md) nella Guida dell'amministratore del client Azure Information Protection.

> [!NOTE]
> Il modulo AIP sostituisce il modulo di protezione RMS di PowerShell installato con lo strumento di protezione RMS. Entrambi questi moduli si differenziano dal [modulo di Windows PowerShell per Azure Rights Management](administer-powershell.md) principale e lo integrano. Il modulo AIP supporta Azure Information Protection, il servizio Azure Rights Management (Azure RMS) per Azure Information Protection e Active Directory Rights Management Services (AD RMS).

[!INCLUDE[Commenting house rules](../includes/houserules.md)]


