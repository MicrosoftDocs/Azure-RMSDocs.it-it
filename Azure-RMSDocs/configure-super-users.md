---
title: Configurare i diritti di utilizzo per Azure Rights Management - Azure Information Protection
description: Comprendere e implementare la funzionalità per utenti con privilegi avanzati del servizio Rights Management di Azure da Azure Information Protection, in modo che gli utenti e i servizi autorizzati possano sempre leggere e controllare ("motivo") i dati protetti dell'organizzazione.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 09/29/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: acb4c00b-d3a9-4d74-94fe-91eeb481f7e3
ms.subservice: azurerms
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: bf7b4d46c2dd63c87f48c244f38a515c7376fc1a
ms.sourcegitcommit: d01580c266de1019de5f895d65c4732f2c98456b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/19/2020
ms.locfileid: "95568238"
---
# <a name="configuring-super-users-for-azure-information-protection-and-discovery-services-or-data-recovery"></a>Configurazione degli utenti con privilegi avanzati per Azure Information Protection e servizi di individuazione o ripristino dei dati

>*Si applica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

La funzionalità per utenti con privilegi avanzati del servizio Azure Rights Management di Azure Information Protection garantisce che gli utenti e i servizi autorizzati possano sempre leggere e controllare i dati che Azure Rights Management protegge per l'organizzazione. Se necessario, la protezione può essere quindi rimossa o modificata.

Per i documenti e i messaggi di posta elettronica protetti dal tenant Azure Information Protection dell'organizzazione, un utente con privilegi avanzati dispone sempre dei [diritti di utilizzo](configure-usage-rights.md) di Controllo completo di Rights Management. Questa possibilità viene definita anche "ragionamento sui dati" e riveste un ruolo di importanza cruciale nel mantenimento del controllo sui dati dell'organizzazione. Ad esempio, utilizzare questa funzionalità per uno qualsiasi dei seguenti scenari:

- Un dipendente lascia l'organizzazione ed è necessario leggere i file che ha protetto.

- Un amministratore IT deve rimuovere il criterio di protezione corrente che è stato configurato per i file e applicare un nuovo criterio di protezione.

- Exchange Server deve indicizzare le caselle postali per le operazioni di ricerca.

- Si dispone di servizi IT esistenti per le soluzioni di prevenzione della perdita dei dati (DLP), per il gateway di crittografia del contenuto (CEG) e per i prodotti anti-malware che richiedono l'analisi dei file che sono già protetti.

- È necessario decrittografare i file per questioni di controllo, legali o per altri motivi di conformità.

## <a name="configuration-for-the-super-user-feature"></a>Configurazione per la funzionalità per utenti con privilegi avanzati

Per impostazione predefinita, questo ruolo non è abilitato e a esso non sono assegnati utenti. Viene abilitata automaticamente se si configura il connettore Rights Management per Exchange e non è necessario per i servizi standard che eseguono Exchange Online, Microsoft SharePoint Server o SharePoint in Microsoft 365.

Se è necessario abilitare manualmente la funzionalità per utenti con privilegi avanzati, usare il cmdlet di PowerShell [Enable-AipServiceSuperUserFeature](/powershell/module/aipservice/enable-aipservicesuperuserfeature)e quindi assegnare gli utenti (o gli account del servizio) in base alle esigenze usando il cmdlet [Add-AipServiceSuperUser](/powershell/module/aipservice/add-aipservicesuperuser) o il cmdlet [set-AipServiceSuperUserGroup](/powershell/module/aipservice/set-aipservicesuperusergroup) e aggiungere utenti (o altri gruppi) in base alle esigenze del gruppo. 

Anche se un gruppo per utenti con privilegi avanzati è più facile da gestire, tenere presente che, per motivi di prestazioni, Azure Rights Management [memorizza nella cache l'appartenenza ai gruppi](prepare.md#group-membership-caching-by-azure-information-protection). Se quindi è necessario assegnare un nuovo utente come utente con privilegi avanzati per decrittografare immediatamente il contenuto, aggiungere l'utente usando Add-AipServiceSuperUser, anziché aggiungere l'utente a un gruppo esistente configurato tramite set-AipServiceSuperUserGroup.

> [!NOTE]
> Se non è stato ancora installato il modulo di Windows PowerShell per Azure Rights Management, vedere [installazione del modulo PowerShell AIPService](install-powershell.md).

Non è importante quando si abilita la funzionalità per utenti con privilegi avanzati o quando si aggiungono utenti come utenti con privilegi avanzati. Ad esempio, se si abilita la funzionalità di giovedì e quindi si aggiunge un utente venerdì, tale utente può immediatamente aprire il contenuto protetto all'inizio della settimana.

## <a name="security-best-practices-for-the-super-user-feature"></a>Procedure di sicurezza consigliate per la funzionalità per utenti con privilegi avanzati

- Limitare e monitorare gli amministratori a cui viene assegnato un amministratore globale per il Microsoft 365 o Azure Information Protection tenant o a cui viene assegnato il ruolo GlobalAdministrator tramite il cmdlet [Add-AipServiceRoleBasedAdministrator](/powershell/module/aipservice/add-aipservicerolebasedadministrator) . Questi utenti possono abilitare la funzionalità per utenti con privilegi avanzati e assegnare agli utenti (e a se stessi) la condizione di utenti con privilegi avanzati, e potenzialmente decrittografare tutti i file che l'organizzazione protegge.

- Per visualizzare quali utenti e account di servizio vengono assegnati individualmente come utenti con privilegi avanzati, usare il cmdlet [Get-AipServiceSuperUser](/powershell/module/aipservice/get-aipservicesuperuser) . 

- Per verificare se è configurato un gruppo di utenti con privilegi avanzati, usare il cmdlet [Get-AipServiceSuperUserGroup](/powershell/module/aipservice/get-aipservicesuperusergroup) e gli strumenti standard per la gestione degli utenti per verificare quali utenti sono membri di questo gruppo. 

- Come tutte le azioni di amministrazione, l'abilitazione o la disabilitazione della funzionalità con privilegi avanzati e l'aggiunta o la rimozione di utenti con privilegi avanzati vengono registrate e possono essere controllate tramite il comando [Get-AipServiceAdminLog](/powershell/module/aipservice/get-aipserviceadminlog) . Vedere ad esempio [il controllo di esempio per la funzionalità per utenti con privilegi avanzati](#example-auditing-for-the-super-user-feature).

- Quando gli utenti con privilegi avanzati eseguono la decrittografia dei file, questa azione viene registrata e può essere controllata con la [registrazione dell'utilizzo](log-analyze-usage.md).

    > [!NOTE]
    > Mentre i log includono i dettagli relativi alla decrittografia, incluso l'utente che ha decrittografato il file, non si notano quando l'utente è un utente con privilegi avanzati. Usare i log con i cmdlet elencati sopra per raccogliere prima un elenco di utenti con privilegi avanzati che è possibile identificare nei log.
    >

- Se non è necessaria la funzionalità per utenti con privilegi avanzati per i servizi quotidiani, abilitare la funzionalità solo quando è necessario e disabilitarla nuovamente utilizzando il cmdlet [Disable-AipServiceSuperUserFeature](/powershell/module/aipservice/disable-aipservicesuperuserfeature) .

### <a name="example-auditing-for-the-super-user-feature"></a>Controllo di esempio per la funzionalità per utenti con privilegi avanzati

L'Estratto di log seguente mostra alcune voci di esempio relative all'uso del cmdlet [Get-AipServiceAdminLog](/powershell/module/aipservice/get-aipserviceadminlog) . 

In questo esempio, l'amministratore di Contoso Ltd verifica che la funzionalità per utenti con privilegi avanzati sia disabilitata, aggiunge Richard Simone come utente con privilegi avanzati, controlla che Richard sia l'unico utente con privilegi avanzati configurato per il servizio Azure Rights Management e quindi abilita la funzionalità per utenti con privilegi avanzati in modo che Richard sia in grado di decrittografare alcuni file che sono stati protetti da un dipendente che ora ha lasciato l'azienda.

`2015-08-01T18:58:20    admin@contoso.com   GetSuperUserFeatureState    Passed  Disabled`

`2015-08-01T18:59:44    admin@contoso.com   AddSuperUser -id rsimone@contoso.com    Passed  True`

`2015-08-01T19:00:51    admin@contoso.com   GetSuperUser    Passed  rsimone@contoso.com`

`2015-08-01T19:01:45    admin@contoso.com   SetSuperUserFeatureState -state Enabled Passed  True`

## <a name="scripting-options-for-super-users"></a>Opzioni di scripting per gli utenti con privilegi avanzati
L'utente a cui viene assegnato il ruolo di utente con privilegi avanzati per Azure Rights Management deve spesso rimuovere la protezione da più file, in più posizioni. Sebbene sia possibile effettuare questa operazione manualmente, è più efficiente (e spesso più affidabile) eseguire uno script. A tale scopo, è possibile usare i cmdlet [Unprotect-RMSFile](/powershell/module/azureinformationprotection/unprotect-rmsfile) e [Protect-RMSFile](/powershell/module/azureinformationprotection/protect-rmsfile) a seconda delle necessità. 

Se si usano la classificazione e la protezione, è possibile usare anche [Set-AIPFileLabel](/powershell/module/azureinformationprotection/set-aipfilelabel) per applicare una nuova etichetta che non applica la protezione oppure rimuovere l'etichetta che ha applicato la protezione. 

Per maggiori informazioni su questi cmdlet, vedere [Uso di PowerShell con il client Azure Information Protection](./rms-client/client-admin-guide-powershell.md) nella guida dell'amministratore del client Azure Information Protection.

> [!NOTE]
> Il modulo AzureInformationProtection è diverso da e integra il [modulo AIPService PowerShell](administer-powershell.md) che gestisce il servizio Azure Rights Management per Azure Information Protection.

### <a name="guidance-for-using-unprotect-rmsfile-for-ediscovery"></a>Linee guida per l'uso di Unprotect-RMSFile per eDiscovery

Benché sia possibile usare il cmdlet Unprotect-RMSFile per decrittografare il contenuto protetto nei file PST, è consigliabile usare questo cmdlet in modo strategico nell'ambito del processo di eDiscovery. L'esecuzione di Unprotect-RMSFile con file di grandi dimensioni in un computer è un'attività che richiede molte risorse (memoria e spazio su disco) e le dimensioni massime del file supportate per questo cmdlet sono 5 GB.

Idealmente, usare [eDiscovery in Microsoft 365](/microsoft-365/compliance/ediscovery) per cercare ed estrarre i messaggi di posta elettronica protetti e l'allegato protetto nei messaggi di posta elettronica. La capacità degli utenti con privilegi avanzati viene integrata automaticamente con Exchange Online in modo che eDiscovery nel Centro sicurezza e conformità di Office 365 o nel Centro conformità Microsoft 365 possa cercare gli elementi crittografati prima di esportare o di decrittografare i messaggi di posta elettronica crittografati in fase di esportazione.

Se non è possibile usare Microsoft 365 eDiscovery, è possibile che si disponga di un'altra soluzione eDiscovery che si integra con il servizio Azure Rights Management per un motivo analogo rispetto ai dati. In alternativa, se la soluzione di eDiscovery non è in grado di leggere e decrittografare automaticamente il contenuto protetto, è comunque possibile usare questa soluzione in un processo in più passaggi che consente di eseguire Unprotect-RMSFile in modo più efficiente:

1. Esportare il messaggio di posta elettronica in questione in un file PST da Exchange Online o Exchange Server oppure dalla workstation in cui l'utente ha archiviato la posta elettronica.

2. Importare il file PST nello strumento di eDiscovery. Poiché lo strumento non è in grado di leggere il contenuto protetto, è probabile che questi elementi generino errori.

3. Da tutti gli elementi che lo strumento non è riuscito ad aprire, generare un nuovo file PST contenente solo gli elementi protetti. Questo secondo file PST avrà probabilmente dimensioni molto inferiori rispetto al file PST originale.

4. Eseguire Unprotect-RMSFile nel secondo file PST per decrittografare il contenuto di questo file molto più piccolo. Dall'output, importare il file PST decrittografato nello strumento di individuazione.

Per informazioni più dettagliate e altre indicazioni per l'esecuzione di eDiscovery su cassette postali e file PST, vedere il post di blog seguente: [Azure Information Protection and eDiscovery Processes](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/Azure-Information-Protection-and-eDiscovery-Processes/ba-p/270216) (Azure Information Protection e processi di eDiscovery).