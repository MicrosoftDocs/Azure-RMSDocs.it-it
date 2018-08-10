---
title: Gestire i dati personali per Azure Information Protection
description: Informazioni sui dati personali usati da Azure Information Protection e su come visualizzarli, esportarli ed eliminarli.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 05/16/2018
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 99a51862-83e9-4a1e-873a-a84ae1465f07
ms.reviewer: aashishr
ms.suite: ems
ms.openlocfilehash: 17ec391c31285687819fe1a2d1b40baf4c31cd44
ms.sourcegitcommit: 5fdf013fe05b65517b56245e1807875d80be6e70
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2018
ms.locfileid: "39490394"
---
# <a name="manage-personal-data-for-azure-information-protection"></a>Gestire i dati personali per Azure Information Protection

Quando si configura e usa Azure Information Protection, gli indirizzi di posta elettronica e gli indirizzi IP vengono archiviati e usati dal servizio Azure Information Protection. Questi dati personali si trovano negli elementi seguenti:

- Criteri di Azure Information Protection

- Modelli di protezione per il servizio Azure Rights Management

- Utenti con privilegi avanzati e amministratori con delega per il servizio Azure Rights Management 

- Log di amministrazione per il servizio Azure Rights Management

- Log sull'utilizzo per il servizio Azure Rights Management

- Log di rilevamento dei documenti

- Log sull'utilizzo per il client Azure Information Protection e il client RMS 


[!INCLUDE [GDPR-related guidance](./includes/gdpr-intro-sentence.md)]


## <a name="viewing-personal-data-that-azure-information-protection-uses"></a>Visualizzazione dei dati personali usati da Azure Information Protection

Usando il portale di Azure, un amministratore può specificare un indirizzo di posta elettronica per i criteri con ambito e per le impostazioni di protezione all'interno di una configurazione di etichette. Per altre informazioni, vedere [How to configure the Azure Information Protection policy for specific users by using scoped policies](configure-policy-scope.md) (Come configurare i criteri di Azure Information Protection per utenti specifici tramite criteri con ambito) e [Come configurare un'etichetta per la protezione di Rights Management](configure-policy-protection.md). 

Per le etichette configurate per applicare la protezione dal servizio Azure Rights Management, l'indirizzo di posta elettronica è anche disponibile nei modelli di protezione, usando i cmdlet di PowerShell del [modulo AADRM](/powershell/module/aadrm). Questo modulo di PowerShell permette anche a un amministratore di specificare gli utenti tramite l'indirizzo di posta elettronica come [utenti con privilegi avanzati](configure-super-users.md) o amministratori per il servizio Azure Rights Management. 

Quando si usa Azure Information Protection per classificare e proteggere documenti e messaggi di posta elettronica, è possibile che gli indirizzi di posta elettronica e gli indirizzi IP degli utenti vengano salvati in file di log.


### <a name="protection-templates"></a>Modelli di protezione

Eseguire il cmdlet [Get-AadrmTemplate](/powershell/module/aadrm/get-aadrmtemplate) per ottenere un elenco di modelli di protezione. È possibile usare l'ID modello per ottenere i dettagli di un modello specifico. L'oggetto `RightsDefinitions` visualizza i dati personali, se presenti. 

Esempio:
```
PS C:\Users> Get-AadrmTemplate -TemplateId fcdbbc36-1f48-48ca-887f-265ee1268f51 | select *


TemplateId              : fcdbbc36-1f48-48ca-887f-265ee1268f51
Names                   : {1033 -> Confidential}
Descriptions            : {1033 -> This data includes sensitive business information. Exposing this data to
                          unauthorized users may cause damage to the business. Examples for Confidential information
                          are employee information, individual customer projects or contracts and sales account data.}
Status                  : Archived
RightsDefinitions       : {admin@aip500.onmicrosoft.com -> VIEW, VIEWRIGHTSDATA, EDIT, DOCEDIT, PRINT, EXTRACT,
                          REPLY, REPLYALL, FORWARD, EXPORT, EDITRIGHTSDATA, OBJMODEL, OWNER,
                          AllStaff-7184AB3F-CCD1-46F3-8233-3E09E9CF0E66@aip500.onmicrosoft.com -> VIEW,
                          VIEWRIGHTSDATA, EDIT, DOCEDIT, PRINT, EXTRACT, REPLY, REPLYALL, FORWARD, EXPORT,
                          EDITRIGHTSDATA, OBJMODEL, OWNER, admin2@aip500.onmicrosoft.com -> VIEW, VIEWRIGHTSDATA, EDIT,
                          DOCEDIT, PRINT, EXTRACT, REPLY, REPLYALL, FORWARD, EXPORT, EDITRIGHTSDATA, OBJMODEL, OWNER}
ContentExpirationDate   : 1/1/0001 12:00:00 AM
ContentValidityDuration : 0
ContentExpirationOption : Never
LicenseValidityDuration : 7
ReadOnly                : False
LastModifiedTimeStamp   : 1/26/2018 6:17:00 PM
ScopedIdentities        : {}
EnableInLegacyApps      : False
LabelId                 :
```

### <a name="super-users-and-delegated-administrators-for-the-azure-rights-management-service"></a>Utenti con privilegi avanzati e amministratori con delega per il servizio Azure Rights Management

Eseguire i cmdlet [Get-AadrmSuperUser](/powershell/module/aadrm/get-aadrmsuperuser) e [Get-AadrmRoleBasedAdministrator](/powershell/module/aadrm/get-aadrmrolebasedadministrator) per visualizzare gli utenti ai quali è stato assegnato il ruolo di utente con privilegi avanzati o di amministratore globale per il servizio Azure Rights Management. Per gli utenti cui sono stati assegnati questi ruoli, vengono visualizzati i rispettivi indirizzi e-mail.


### <a name="administration-logs-for-the-azure-rights-management-service"></a>Log di amministrazione per il servizio Azure Rights Management

Eseguire il cmdlet [Get-AadrmAdminLog](/powershell/module/aadrm/get-aadrmadminlog) per ottenere un log delle azioni di amministrazione per il servizio Azure Rights Management, che protegge i dati per Azure Information Protection. Questo log include dati personali sotto forma di indirizzi di posta elettronica e indirizzi IP. Il log è in testo normale e, una volta scaricato, è possibile cercare offline le informazioni su un amministratore specifico.

Ad esempio:
```
PS C:\Users> Get-AadrmAdminLog -Path '.\Desktop\admin.log' -FromTime 4/1/2018 -ToTime 4/30/2018 -Verbose
The Rights Management administration log was successfully generated and can be found at .\Desktop\admin.log.
```

### <a name="usage-logs-for-the-azure-rights-management-service"></a>Log sull'utilizzo per il servizio Azure Rights Management
Eseguire il cmdlet [Get-AadrmUserLog](/powershell/module/aadrm/get-aadrmuserlog) per recuperare un log delle azioni degli utenti finali che usano il servizio Azure Rights Management. Il servizio protegge i dati per Azure Information Protection. Il log può includere dati personali sotto forma di indirizzi di posta elettronica e indirizzi IP. Il log è in testo normale e, una volta scaricato, è possibile cercare offline le informazioni su un amministratore specifico.

Ad esempio:
```
PS C:\Users> Get-AadrmUserLog -Path '.\Desktop\' -FromDate 4/1/2018 -ToDate 4/30/2018 -NumberOfThreads 10
Acquiring access to your user log…
Downloading the log for 2018-04-01.
Downloading the log for 2018-04-03.
Downloading the log for 2018-04-06.
Downloading the log for 2018-04-09.
Downloading the log for 2018-04-10.
Downloaded the log for 2018-04-01. The log is available at .\Desktop\rmslog-2018-04-01.log.
Downloaded the log for 2018-04-03. The log is available at .\Desktop\rmslog-2018-04-03.log.
Downloaded the log for 2018-04-06. The log is available at .\Desktop\rmslog-2018-04-06.log.
Downloaded the log for 2018-04-09. The log is available at .\Desktop\rmslog-2018-04-09.log.
Downloaded the log for 2018-04-10. The log is available at .\Desktop\rmslog-2018-04-10.log.
Downloading the log for 2018-04-12.
Downloading the log for 2018-04-13.
Downloading the log for 2018-04-14.
Downloading the log for 2018-04-16.
Downloading the log for 2018-04-18.
Downloaded the log for 2018-04-12. The log is available at .\Desktop\rmslog-2018-04-12.log.
Downloaded the log for 2018-04-13. The log is available at .\Desktop\rmslog-2018-04-13.log.
Downloaded the log for 2018-04-14. The log is available at .\Desktop\rmslog-2018-04-14.log.
Downloaded the log for 2018-04-16. The log is available at .\Desktop\rmslog-2018-04-16.log.
Downloaded the log for 2018-04-18. The log is available at .\Desktop\rmslog-2018-04-18.log.
Downloading the log for 2018-04-24.
Downloaded the log for 2018-04-24. The log is available at .\Desktop\rmslog-2018-04-24.log.
```   

### <a name="document-tracking-logs"></a>Log di rilevamento dei documenti

Eseguire il cmdlet [Get-AadrmDocumentLog](/powershell/module/aadrm/get-aadrmdocumentlog) per recuperare informazioni dal sito di rilevamento dei documenti su un utente specifico. Per ottenere informazioni sul rilevamento associate ai log dei documenti, usare il cmdlet [Get-AadrmTrackingLog](/powershell/module/aadrm/get-aadrmtrackinglog?view=azureipps).

Ad esempio:
```
PS C:\Users> Get-AadrmDocumentLog -UserEmail "admin@aip500.onmicrosoft.com"


ContentId             : 6326fcb2-c465-4c24-a7f6-1cace7a9cb6f
Issuer                : admin@aip500.onmicrosoft.com
Owner                 : admin@aip500.onmicrosoft.com
ContentName           :
CreatedTime           : 3/6/2018 10:24:00 PM
Recipients            : {
                        PrimaryEmail: johndoe@contoso.com
                        DisplayName: JOHNDOE@CONTOSO.COM
                        UserType: External,
                        PrimaryEmail: alice@contoso0110.onmicrosoft.com
                        DisplayName: ALICE@CONTOSO0110.ONMICROSOFT.COM
                        UserType: External
                        }
TemplateId            :
PolicyExpires         :
EULDuration           :
SendRegistrationEmail : True
NotificationInfo      : Enabled: False
                        DeniedOnly: False
                        Culture:
                        TimeZoneId:
                        TimeZoneOffset: 0
                        TimeZoneDaylightName:
                        TimeZoneStandardName:

RevocationInfo        : Revoked: False
                        RevokedTime:
                        RevokedBy:


PS C:\Users> Get-AadrmTrackingLog -UserEmail "admin@aip500.onmicrosoft.com"

ContentId            : 6326fcb2-c465-4c24-a7f6-1cace7a9cb6f
Issuer               : admin@aip500.onmicrosoft.com
RequestTime          : 3/6/2018 10:45:57 PM
RequesterType        : External
RequesterEmail       : johndoe@contoso.com
RequesterDisplayName : johndoe@contoso.com
RequesterLocation    : IP: 167.220.1.54
                       Country: US
                       City: redmond
                       Position: 47.6812453974602,-122.120736471666

Rights               : {VIEW,OBJMODEL}
Successful           : False
IsHiddenInfo         : False
```

Non è possibile cercare per ObjectID. Tuttavia, il parametro `-UserEmail` non impone una restrizione e l'indirizzo di posta elettronica specificato non deve necessariamente fare parte del tenant. Se l'indirizzo di posta elettronica è archiviato in un punto qualsiasi nei log di rilevamento dei documenti, la voce di rilevamento dei documenti viene restituita nell'output del cmdlet.

### <a name="usage-logs-for-the-azure-information-protection-client-and-rms-client"></a>Log sull'utilizzo per il client Azure Information Protection e il client RMS

Quando vengono applicate etichette e protezione a documenti e messaggi di posta elettronica, gli indirizzi di posta elettronica e gli indirizzi IP possono essere archiviati nel computer di un utente nei percorsi seguenti:

- Per il client Azure Information Protection: %localappdata%\Microsoft\MSIP\Logs

- Per il client RMS: %localappdata%\Microsoft\MSIPC\msip\Logs

Inoltre, il client Azure Information Protection registra questi dati personali nel registro eventi di Windows locale: **Registri applicazioni e servizi** > **Azure Information Protection**.

Quando il client Azure Information Protection esegue lo scanner, i dati personali vengono salvati in %localappdata%\Microsoft\MSIP\Scanner\Reports nel computer Windows Server che esegue lo scanner.

[!INCLUDE [GDPR-related guidance](./includes/gdpr-hybrid-note.md)]

## <a name="securing-and-controlling-access-to-personal-information"></a>Protezione e controllo dell'accesso a informazioni personali
I dati personali visualizzati e specificati nel portale di Azure sono accessibili solo agli utenti cui è stato assegnato uno dei [ruoli di amministratore di Azure Active Directory](/azure/active-directory/active-directory-assign-admin-roles-azure-portal) seguenti:
    
- **Amministratore di Information Protection**

- **Amministratore della sicurezza**

- **Amministratore globale / Amministratore società**

I dati personali visualizzati e specificati tramite il modulo AADRM sono accessibili solo agli utenti cui è stato assegnato il ruolo **Amministratore di Information Protection** o i ruoli **Amministratore globale/Amministratore società** di Azure Active Directory oppure il ruolo di amministratore globale per il servizio Azure Rights Management.  

## <a name="updating-personal-data"></a>Aggiornamento dei dati personali

È possibile aggiornare gli indirizzi di posta elettronica per i criteri con ambito e le impostazioni di protezione nei criteri di Azure Information Protection. Per altre informazioni, vedere [How to configure the Azure Information Protection policy for specific users by using scoped policies](configure-policy-scope.md) (Come configurare i criteri di Azure Information Protection per utenti specifici tramite criteri con ambito) e [Come configurare un'etichetta per la protezione di Rights Management](configure-policy-protection.md). 

Per le impostazioni di protezione, è possibile aggiornare le stesse informazioni tramite i cmdlet di PowerShell del [modulo AADRM](/powershell/module/aadrm).

Non è possibile aggiornare gli indirizzi di posta elettronica per gli utenti con privilegi avanzati e gli amministratori con delega. Rimuovere invece l'account utente specificato e aggiungere l'account utente con l'indirizzo di posta elettronica aggiornato. 

### <a name="protection-templates"></a>Modelli di protezione

Eseguire il cmdlet [Set-AadrmTemplateProperty](/powershell/module/aadrm/set-aadrmtemplateproperty) per aggiornare il modello di protezione. Poiché i dati personali si trovano all'interno della proprietà `RightsDefinitions`, sarà necessario usare anche il cmdlet [New-AadrmRightsDefinition](/powershell/module/aadrm/new-aadrmrightsdefinition) per creare un oggetto RightsDefinitions con le informazioni aggiornate e usare questo oggetto con il cmdlet `Set-AadrmTemplateProperty`.

### <a name="super-users-and-delegated-administrators-for-the-azure-rights-management-service"></a>Utenti con privilegi avanzati e amministratori con delega per il servizio Azure Rights Management

Quando è necessario aggiornare un indirizzo di posta elettronica per un utente con privilegi avanzati:

1. Usare [Remove-AadrmSuperUser](/powershell/module/aadrm/Remove-AadrmSuperUser) per rimuovere l'utente e il vecchio indirizzo di posta elettronica.

2. Usare [Add-AadrmSuperUser](/powershell/module/aadrm/Add-AadrmSuperUser) per aggiungere l'utente e il nuovo indirizzo di posta elettronica.

Quando è necessario aggiornare un indirizzo di posta elettronica per un amministratore con delega:

1. Usare [Remove-AadrmRoleBasedAdministrator](/powershell/module/aadrm/Remove-AadrmRoleBasedAdministrator) per rimuovere l'utente e il vecchio indirizzo di posta elettronica.

2. Usare [Add-AadrmRoleBasedAdministrator](/powershell/module/aadrm/Add-AadrmRoleBasedAdministrator) per aggiungere l'utente e il nuovo indirizzo di posta elettronica.

## <a name="deleting-personal-data"></a>Eliminazione dei dati personali
È possibile eliminare gli indirizzi di posta elettronica per i criteri con ambito e le impostazioni di protezione nei criteri di Azure Information Protection. Per altre informazioni, vedere [How to configure the Azure Information Protection policy for specific users by using scoped policies](configure-policy-scope.md) (Come configurare i criteri di Azure Information Protection per utenti specifici tramite criteri con ambito) e [Come configurare un'etichetta per la protezione di Rights Management](configure-policy-protection.md). 

Per le impostazioni di protezione, è possibile eliminare le stesse informazioni tramite i cmdlet di PowerShell del [modulo AADRM](/powershell/module/aadrm).

Per eliminare gli indirizzi di posta elettronica per utenti con privilegi avanzati e amministratori con delega, rimuovere questi utenti usando i cmdlet [Remove-AadrmSuperUser](/powershell/module/aadrm/Remove-AadrmSuperUser) e [Remove-AadrmRoleBasedAdministrator](/powershell/module/aadrm/Remove-AadrmRoleBasedAdministrator). 

Per eliminare dati personali nei log di rilevamento dei documenti, nei log di amministrazione o nei log sull'utilizzo per il servizio Azure Rights Management, usare la sezione seguente per generare una richiesta per il supporto tecnico Microsoft.

Per eliminare dati personali nei file di log dei client e nei log dello scanner archiviati nei computer, usare qualsiasi strumento di Windows standard per eliminare i file o i dati personali all'interno dei file. 

### <a name="to-delete-personal-data-with-microsoft-support"></a>Per eliminare dati personali con il supporto tecnico Microsoft

Usare i tre passaggi seguenti per richiedere a Microsoft di eliminare i dati personali nei log di rilevamento dei documenti, nei log di amministrazione o nei log sull'utilizzo per il servizio Azure Rights Management. 

**Passaggio 1: Generare la richiesta di eliminazione**
[Contattare il supporto tecnico Microsoft](information-support.md#to-contact-microsoft-support) per aprire un caso di supporto per Azure Information Protection con una richiesta di eliminazione dei dati dal tenant. È necessario dimostrare di essere un amministratore del tenant di Azure Information Protection e tenere presente che la conferma di questo processo richiede diversi giorni. Nell'inviare la richiesta, è necessario fornire informazioni aggiuntive, a seconda dei dati che devono essere eliminati.

- Per eliminare il log di amministrazione, specificare la **data di fine**. Verranno eliminati tutti i log di amministrazione fino alla data di fine specificata.
- Per eliminare i log sull'utilizzo, specificare la **data di fine**. Verranno eliminati tutti i log sull'utilizzo fino alla data di fine specificata.
- Per eliminare i log di rilevamento dei documenti, specificare il parametro **UserEmail**. Verranno eliminate tutte le informazioni sul rilevamento dei documenti correlate a UserEmail.

L'eliminazione di questi dati è un'operazione permanente. Al termine dell'elaborazione di una richiesta di eliminazione, non sarà possibile recuperare i dati in alcun modo. Si consiglia agli amministratori di esportare i dati necessari prima di inviare una richiesta di eliminazione.

**Passaggio 2: Attendere la verifica** Microsoft verificherà la legittimità della richiesta di eliminazione di uno o più log. Questo processo può richiedere fino a cinque giorni lavorativi.

**Fase 3: Ottenere la conferma dell'eliminazione** Il servizio di supporto tecnico Microsoft invierà un messaggio di posta elettronica di conferma dell'avvenuta eliminazione dei dati. 

## <a name="exporting-personal-data"></a>Esportazione dei dati personali
Quando si usano i cmdlet del modulo AADRM di PowerShell, i dati personali vengono resi disponibili per la ricerca e l'esportazione come oggetto di PowerShell. L'oggetto di PowerShell può essere convertito in JSON e salvato tramite il cmdlet `ConvertTo-Json`.

## <a name="restricting-the-use-of-personal-data-for-profiling-or-marketing-without-consent"></a>Limitazione dell'uso di dati personali per profilatura e marketing senza consenso
Azure Information Protection segue l'[condizioni per la privacy](https://privacy.microsoft.com/privacystatement) Microsoft per la profilatura e il marketing basati su dati personali.

## <a name="auditing-and-reporting"></a>Controllo e segnalazione
Solo gli utenti cui sono state assegnate [autorizzazioni di amministratore](#securing-and-controlling-access-to-personal-information) possono usare il modulo AADRM per cercare ed esportare dati personali. Queste operazioni vengono registrate nel log di amministrazione, che può essere scaricato.

Per le azioni di eliminazione, la richiesta di supporto funge da audit trail e percorso di segnalazione per le azioni eseguite da Microsoft. Dopo l'eliminazione, i dati eliminati non saranno disponibili per la ricerca o l'esportazione e l'amministratore potrà verificare questo aspetto usando i cmdlet Get del modulo AADRM.

