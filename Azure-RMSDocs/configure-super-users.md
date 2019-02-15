---
title: Configurare utenti con privilegi avanzati per Azure Rights Management - AIP
description: Informazioni sulla funzionalità per utenti con privilegi avanzati del servizio Azure Rights Management di Azure Information Protection e relativa implementazione in modo che gli utenti e i servizi autorizzati possano sempre leggere e controllare i dati che Azure Rights Management protegge per l'organizzazione. Questa possibilità viene definita anche "ragionamento sui dati" e riveste un ruolo di importanza critica nel mantenimento del controllo sui dati dell'organizzazione.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 10/12/2018
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: acb4c00b-d3a9-4d74-94fe-91eeb481f7e3
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 1590fded6abab3ca2848d9eb216e9f49f35f0cfb
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/14/2019
ms.locfileid: "56255326"
---
# <a name="configuring-super-users-for-azure-rights-management-and-discovery-services-or-data-recovery"></a>Configurazione degli utenti con privilegi avanzati per Azure Rights Management e servizi di individuazione o ripristino dei dati

>*Si applica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

La funzionalità per utenti con privilegi avanzati del servizio Azure Rights Management di Azure Information Protection garantisce che gli utenti e i servizi autorizzati possano sempre leggere e controllare i dati che Azure Rights Management protegge per l'organizzazione. Se necessario, la protezione può essere quindi rimossa o modificata.

Per i documenti e i messaggi di posta elettronica protetti dal tenant Azure Information Protection dell'organizzazione, un utente con privilegi avanzati dispone sempre dei [diritti di utilizzo](configure-usage-rights.md) di Rights Management corrispondenti al controllo completo. Questa possibilità viene definita anche "ragionamento sui dati" e riveste un ruolo di importanza cruciale nel mantenimento del controllo sui dati dell'organizzazione. Ad esempio, utilizzare questa funzionalità per uno qualsiasi dei seguenti scenari:

- Un dipendente lascia l'organizzazione ed è necessario leggere i file che ha protetto.

- Un amministratore IT deve rimuovere il criterio di protezione corrente che è stato configurato per i file e applicare un nuovo criterio di protezione.

- Exchange Server deve indicizzare le caselle postali per le operazioni di ricerca.

- Si dispone di servizi IT esistenti per le soluzioni di prevenzione della perdita dei dati, per il gateway di crittografia del contenuto (CEG) e per i prodotti anti-malware che richiedono l'analisi dei file che sono già protetti.

- È necessario decrittografare i file per questioni di controllo, legali o per altri motivi di conformità.

## <a name="configuration-for-the-super-user-feature"></a>Configurazione per la funzionalità per utenti con privilegi avanzati

Per impostazione predefinita, questo ruolo non è abilitato e a esso non sono assegnati utenti. Viene abilitata automaticamente per l'utente se si configura il connettore Rights Management per Exchange, e non è necessaria per i servizi standard che eseguono Exchange Online, SharePoint Online o SharePoint Server.

Se è necessario abilitare manualmente la funzionalità per utenti con privilegi avanzati, usare il cmdlet [Enable-AadrmSuperUserFeature](/powershell/aadrm/vlatest/enable-aadrmsuperuserfeature) di PowerShell e quindi assegnare utenti (o account del servizio) mediante il cmdlet [Add-AadrmSuperUser](/powershell/aadrm/vlatest/add-aadrmsuperuser) o [Set-AadrmSuperUserGroup](/powershell/aadrm/vlatest/set-aadrmsuperusergroup) e aggiungere utenti (o altri gruppi) a questo gruppo in base alla necessità. 

Anche se un gruppo per utenti con privilegi avanzati è più facile da gestire, tenere presente che, per motivi di prestazioni, Azure Rights Management [memorizza nella cache l'appartenenza ai gruppi](prepare.md#group-membership-caching-by-azure-information-protection). Pertanto, se è necessario assegnare privilegi avanzati a un nuovo utente per decrittografare immediatamente il contenuto, aggiungere l'utente usando Add-AadrmSuperUser, anziché aggiungerlo a un gruppo esistente configurato tramite Set-AadrmSuperUserGroup.

> [!NOTE]
> Se non è stato ancora installato il modulo di Windows PowerShell per Azure Rights Management, vedere [Installing the AADRM PowerShell module](install-powershell.md) (Installazione del modulo di PowerShell AADRM).

Non è importante quando si abilita la funzionalità per utenti con privilegi avanzati o quando si aggiungono utenti come utenti con privilegi avanzati. Ad esempio, se si abilita la funzionalità di giovedì e quindi si aggiunge un utente venerdì, tale utente può immediatamente aprire il contenuto protetto all'inizio della settimana.

## <a name="security-best-practices-for-the-super-user-feature"></a>Procedure di sicurezza consigliate per la funzionalità per utenti con privilegi avanzati

- Limitare e monitorare gli amministratori a cui viene assegnato un ruolo di amministratore globale per il tenant di Office 365 o Azure Information Protection o a cui viene assegnato il ruolo GlobalAdministrator mediante il cmdlet [Add-AadrmRoleBasedAdministrator](/powershell/module/aadrm/add-aadrmrolebasedadministrator). Questi utenti possono abilitare la funzionalità per utenti con privilegi avanzati e assegnare agli utenti (e a se stessi) la condizione di utenti con privilegi avanzati, e potenzialmente decrittografare tutti i file che l'organizzazione protegge.

- Per verificare gli utenti e gli account del servizio che vengono assegnati individualmente come utenti con privilegi avanzati, usare il cmdlet [Get-AadrmSuperUser](/powershell/module/aadrm/get-aadrmsuperuser). Per verificare se è stato configurato un gruppo di utenti con privilegi avanzati, usare il cmdlet [Get-AadrmSuperUserGroup](/powershell/module/aadrm/get-aadrmsuperusergroup) e gli strumenti standard per la gestione degli utenti per verificare i membri che appartengono a questo gruppo. Come tutte le azioni di amministrazione, quelle di abilitare o disabilitare la caratteristica con privilegi avanzati, e aggiungere o rimuovere gli utenti con privilegi avanzati che vengono registrati, possono essere controllate tramite il comando [Get-AadrmAdminLog](/powershell/module/aadrm/get-aadrmadminlog) . Vedere la sezione successiva per un esempio. Quando gli utenti con privilegi avanzati eseguono la decrittografia dei file, questa azione viene registrata e può essere controllata con la [registrazione dell'utilizzo](log-analyze-usage.md).

- Se non è necessaria la funzionalità per utenti con privilegi avanzati per i servizi quotidiani, abilitare la funzionalità solo quando è necessario e disabilitarla nuovamente utilizzando il cmdlet [Disable AadrmSuperUserFeature](/powershell/module/aadrm/disable-aadrmsuperuserfeature) .

### <a name="example-auditing-for-the-super-user-feature"></a>Controllo di esempio per la funzionalità per utenti con privilegi avanzati

L'estratto dal log seguente mostra alcune voci di esempio relative all'uso del cmdlet [Get-AadrmAdminLog](/powershell/module/aadrm/get-aadrmadminlog). 

In questo esempio, l'amministratore di Contoso Ltd verifica che la funzionalità per utenti con privilegi avanzati sia disabilitata, aggiunge Richard Simone come utente con privilegi avanzati, controlla che Richard sia l'unico utente con privilegi avanzati configurato per il servizio Azure Rights Management e quindi abilita la funzionalità per utenti con privilegi avanzati in modo che Richard sia in grado di decrittografare alcuni file che sono stati protetti da un dipendente che ora ha lasciato l'azienda.

`2015-08-01T18:58:20    admin@contoso.com   GetSuperUserFeatureState    Passed  Disabled`

`2015-08-01T18:59:44    admin@contoso.com   AddSuperUser -id rsimone@contoso.com    Passed  True`

`2015-08-01T19:00:51    admin@contoso.com   GetSuperUser    Passed  rsimone@contoso.com`

`2015-08-01T19:01:45    admin@contoso.com   SetSuperUserFeatureState -state Enabled Passed  True`

## <a name="scripting-options-for-super-users"></a>Opzioni di scripting per gli utenti con privilegi avanzati
L'utente a cui viene assegnato il ruolo di utente con privilegi avanzati per Azure Rights Management deve spesso rimuovere la protezione da più file, in più posizioni. Sebbene sia possibile effettuare questa operazione manualmente, è più efficiente (e spesso più affidabile) eseguire uno script. A tale scopo, è possibile usare i cmdlet [Unprotect-RMSFile](/powershell/module/azureinformationprotection/unprotect-rmsfile) e [Protect-RMSFile](/powershell/module/azureinformationprotection/protect-rmsfile) come necessario. 

Se si usano la classificazione e la protezione, è anche possibile usare [Set-AIPFileLabel](/powershell/module/azureinformationprotection/set-aipfilelabel) per applicare una nuova etichetta che non applica la protezione oppure rimuovere l'etichetta che ha applicato la protezione. 

Per altre informazioni su questi cmdlet, vedere [Uso di PowerShell con il client Azure Information Protection](./rms-client/client-admin-guide-powershell.md) nella Guida dell'amministratore del client Azure Information Protection.

> [!NOTE]
> Il modulo AzureInformationProtection è diverso dal [modulo AADRM di PowerShell](administer-powershell.md) per la gestione del servizio Azure Rights Management per Azure Information Protection e lo integra.

### <a name="guidance-for-using-unprotect-rmsfile-for-ediscovery"></a>Linee guida per l'uso di Unprotect-RMSFile per eDiscovery

Benché sia possibile usare il cmdlet Unprotect-RMSFile per decrittografare il contenuto protetto nei file PST, è consigliabile usare questo cmdlet in modo strategico nell'ambito del processo di eDiscovery. L'esecuzione di Unprotect-RMSFile con file di grandi dimensioni in un computer è un'attività che richiede molte risorse (memoria e spazio su disco) e le dimensioni massime del file supportate per questo cmdlet sono 5 GB.

Idealmente, usare [Office 365 eDiscovery](/office365/securitycompliance/ediscovery) per cercare ed estrarre i messaggi di posta elettronica protetti e gli allegati protetti in essi contenuti. La capacità degli utenti con privilegi avanzati viene integrata automaticamente con Exchange Online in modo che eDiscovery nel Centro sicurezza e conformità di Office 365 possa cercare gli elementi crittografati prima di esportare o di decrittografare i messaggi di posta elettronica crittografati in fase di esportazione.

Se non è possibile usare Office 365 eDiscovery, potrebbe essere disponibile un'altra soluzione di eDiscovery in grado di integrarsi con il servizio Azure Rights Management per un'analisi analoga dei dati. In alternativa, se la soluzione di eDiscovery non è in grado di leggere e decrittografare automaticamente il contenuto protetto, è comunque possibile usare questa soluzione in un processo in più passaggi che consente di eseguire Unprotect-RMSFile in modo più efficiente:

1. Esportare il messaggio di posta elettronica in questione in un file PST da Exchange Online o Exchange Server oppure dalla workstation in cui l'utente ha archiviato la posta elettronica.

2. Importare il file PST nello strumento di eDiscovery. Poiché lo strumento non è in grado di leggere il contenuto protetto, è probabile che questi elementi generino errori.

3. Da tutti gli elementi che lo strumento non è riuscito ad aprire, generare un nuovo file PST contenente solo gli elementi protetti. Questo secondo file PST avrà probabilmente dimensioni molto inferiori rispetto al file PST originale.

4. Eseguire Unprotect-RMSFile nel secondo file PST per decrittografare il contenuto di questo file molto più piccolo. Dall'output, importare il file PST decrittografato nello strumento di individuazione.

Per informazioni più dettagliate e altre indicazioni per l'esecuzione di eDiscovery tra le cassette postali e i file PST, vedere il post di blog seguente: [Azure Information Protection and eDiscovery Processes](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/Azure-Information-Protection-and-eDiscovery-Processes/ba-p/270216) (Azure Information Protection e processi di eDiscovery).

