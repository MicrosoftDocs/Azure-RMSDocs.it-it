---
title: Gestire i dati personali per Azure Information Protection
description: Informazioni sui dati personali usati da Azure Information Protection e su come visualizzarli, esportarli ed eliminarli.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 10/04/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 99a51862-83e9-4a1e-873a-a84ae1465f07
ms.reviewer: aashishr
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 985f567189cbc65920b53af3f797d5c62d2671c5
ms.sourcegitcommit: f6d536b6a3b5e14e24f0b9e58d17a3136810213b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/26/2021
ms.locfileid: "98809464"
---
# <a name="manage-personal-data-for-azure-information-protection"></a>Gestire i dati personali per Azure Information Protection

>***Si applica a**: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*
>
>***Rilevante per**: [Client di etichettatura unificata e client classico di AIP](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

>[!NOTE] 
> Per offrire un'esperienza per i clienti unificata e semplificata, il **client classico di Azure Information Protection** e **Gestione etichette** nel portale di Azure saranno **deprecati** a partire dal **31 marzo 2021**. In questo intervallo di tempo tutti i clienti correnti di Azure Information Protection possono passare alla soluzione di etichettatura unificata usando la piattaforma di etichettatura unificata di Microsoft Information Protection. Altre informazioni nell'[avviso ufficiale sulla deprecazione](https://aka.ms/aipclassicsunset).

Quando si configura e usa Azure Information Protection, gli indirizzi di posta elettronica e gli indirizzi IP vengono archiviati e usati dal servizio Azure Information Protection. Questi dati personali si trovano negli elementi seguenti:

- Utenti con privilegi avanzati e amministratori delegati per il servizio di protezione 

- Log di amministrazione per il servizio di protezione

- Log di utilizzo per il servizio di protezione

- Log di utilizzo per i client di Azure Information Protection e RMS 

**Solo client classico AIP**:

- Criteri di Azure Information Protection

- Modelli per il servizio di protezione

- Log di rilevamento dei documenti

[!INCLUDE [GDPR-related guidance](./includes/gdpr-intro-sentence.md)]

## <a name="viewing-personal-data-that-azure-information-protection-uses"></a>Visualizzazione dei dati personali usati da Azure Information Protection

- **Client di etichettatura unificata**:

    Per il client di etichettatura unificata, le etichette di riservatezza e i criteri delle etichette sono configurati nel centro sicurezza Microsoft 365, nel centro di conformità Microsoft 365 o nel Microsoft 365 Security & Compliance Center. Per altre informazioni, vedere la [documentazione di Microsoft 365](/microsoft-365/compliance/sensitivity-labels).

- **Client classico**:

    Per il client classico, usare il portale di Azure per specificare gli indirizzi di posta elettronica per i criteri con ambito e per le impostazioni di protezione all'interno di una configurazione di etichetta. Per altre informazioni, vedere [How to configure the Azure Information Protection policy for specific users by using scoped policies](configure-policy-scope.md) (Come configurare i criteri di Azure Information Protection per utenti specifici tramite criteri con ambito) e [Come configurare un'etichetta per la protezione di Rights Management](configure-policy-protection.md). 

    Per le etichette configurate per applicare la protezione dal servizio Rights Management di Azure, è possibile trovare l'indirizzo di posta elettronica anche nei modelli di protezione usando i cmdlet di PowerShell del [modulo AIPService](/powershell/module/aipservice). Questo modulo di PowerShell permette anche a un amministratore di specificare gli utenti tramite l'indirizzo di posta elettronica come [utenti con privilegi avanzati](configure-super-users.md) o amministratori per il servizio Azure Rights Management. 

> [!NOTE]
> Quando si usa Azure Information Protection per classificare e proteggere documenti e messaggi di posta elettronica, è possibile che gli indirizzi di posta elettronica e gli indirizzi IP degli utenti vengano salvati in file di log.
> 

### <a name="super-users-and-delegated-administrators-for-the-protection-service"></a>Utenti con privilegi avanzati e amministratori delegati per il servizio di protezione

Eseguire il cmdlet [Get-AipServiceSuperUser](/powershell/module/aipservice/get-aipservicesuperuser) e il cmdlet [Get-aipservicerolebasedadministrator](/powershell/module/aipservice/get-aipservicerolebasedadministrator) per vedere quali utenti sono stati assegnati al ruolo utente con privilegi avanzati o al ruolo di amministratore globale per il servizio di protezione (Rights Management di Azure) da Azure Information Protection. Per gli utenti cui sono stati assegnati questi ruoli, vengono visualizzati i rispettivi indirizzi e-mail.


### <a name="administration-logs-for-the-protection-service"></a>Log di amministrazione per il servizio di protezione

Eseguire il cmdlet [Get-AipServiceAdminLog](/powershell/module/aipservice/get-aipserviceadminlog) per ottenere un log delle azioni di amministrazione per il servizio di protezione (Rights Management di Azure) da Azure Information Protection. Questo log include dati personali sotto forma di indirizzi di posta elettronica e indirizzi IP. Il log è in testo normale e, una volta scaricato, è possibile cercare offline le informazioni su un amministratore specifico.

Ad esempio:
```PowerShell
PS C:\Users> Get-AipServiceAdminLog -Path '.\Desktop\admin.log' -FromTime 4/1/2018 -ToTime 4/30/2018 -Verbose
The Rights Management administration log was successfully generated and can be found at .\Desktop\admin.log.
```

### <a name="usage-logs-for-the-protection-service"></a>Log di utilizzo per il servizio di protezione
Eseguire il cmdlet [Get-AipServiceUserLog](/powershell/module/aipservice/get-aipserviceuserlog) per recuperare un log delle azioni dell'utente finale che usano il servizio di protezione da Azure Information Protection. Il log può includere dati personali sotto forma di indirizzi di posta elettronica e indirizzi IP. Il log è in testo normale e, una volta scaricato, è possibile cercare offline le informazioni su un amministratore specifico.

Ad esempio:
```PowerShell
PS C:\Users> Get-AipServiceUserLog -Path '.\Desktop\' -FromDate 4/1/2018 -ToDate 4/30/2018 -NumberOfThreads 10
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

### <a name="usage-logs-for-the-azure-information-protection-clients-and-rms-client"></a>Log di utilizzo per i client di Azure Information Protection e RMS

Quando vengono applicate etichette e protezione a documenti e messaggi di posta elettronica, gli indirizzi di posta elettronica e gli indirizzi IP possono essere archiviati nel computer di un utente nei percorsi seguenti:

- Per il Azure Information Protection le etichette unificate e i client classici: **%LocalAppData%\Microsoft\MSIP\Logs**

- Per il client RMS: **%LocalAppData%\Microsoft\MSIPC\msip\Logs**

Inoltre, il client Azure Information Protection registra questi dati personali nel registro eventi di Windows locale **registri applicazioni e servizi**  >  **Azure Information Protection**.

Quando il client di Azure Information Protection esegue lo scanner, i dati personali vengono salvati in **%LocalAppData%\Microsoft\MSIP\Scanner\Reports** nel computer Windows Server che esegue lo scanner.

È possibile disattivare la registrazione di informazioni per il client Azure Information Protection e lo scanner usando le configurazioni seguenti:

- Per il client Azure Information Protection: creare un' [impostazione client avanzata](./rms-client/clientv2-admin-guide-customizations.md#change-the-local-logging-level) che configuri il **LogLevel** su **off**.

- Per lo scanner Azure Information Protection: usare il cmdlet [set-AIPScannerConfiguration](/powershell/module/azureinformationprotection/set-aipscannerconfiguration) per impostare il parametro *reportLevel* su **off**.

[!INCLUDE [GDPR-related guidance](./includes/gdpr-hybrid-note.md)]

### <a name="protection-templates"></a>Modelli di protezione

**Pertinente per**: solo client di AIP classico

Eseguire il cmdlet [Get-AipServiceTemplate](/powershell/module/aipservice/get-aipservicetemplate) per ottenere un elenco di modelli di protezione. È possibile usare l'ID modello per ottenere i dettagli di un modello specifico. L'oggetto `RightsDefinitions` visualizza i dati personali, se presenti. 

Esempio:
```PowerShell
PS C:\Users> Get-AipServiceTemplate -TemplateId fcdbbc36-1f48-48ca-887f-265ee1268f51 | select *


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

### <a name="document-tracking-logs"></a>Log di rilevamento dei documenti

**Pertinente per**: solo client di AIP classico

Eseguire il cmdlet [Get-AipServiceDocumentLog](/powershell/module/aipservice/get-aipservicedocumentlog) per recuperare le informazioni dal sito di rilevamento dei documenti relativi a un utente specifico. Per ottenere le informazioni di rilevamento associate ai log del documento, usare il cmdlet [Get-AipServiceTrackingLog](/powershell/module/aipservice/get-aipservicetrackinglog) .

Ad esempio:
```PowerShell
PS C:\Users> Get-AipServiceDocumentLog -UserEmail "admin@aip500.onmicrosoft.com"


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


PS C:\Users> Get-AipServiceTrackingLog -UserEmail "admin@aip500.onmicrosoft.com"

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

## <a name="securing-and-controlling-access-to-personal-information"></a>Sicurezza e controllo dell'accesso alle informazioni personali

I dati personali visualizzati e specificati nel portale di Azure sono accessibili solo agli utenti cui è stato assegnato uno dei [ruoli di amministratore di Azure Active Directory](/azure/active-directory/active-directory-assign-admin-roles-azure-portal) seguenti:
    
- **Amministratore Azure Information Protection**

- **Amministratore di conformità**

- **Amministratore dati di conformità**

- **Amministratore della sicurezza**

- **Ruolo con autorizzazioni di lettura per la sicurezza**

- **Amministratore globale**

- **Lettore globale**

I dati personali che è possibile visualizzare e specificare usando il modulo AIPService (o il modulo precedente, AADRM) sono accessibili solo agli utenti a cui sono stati assegnati i ruoli amministratore **Azure Information Protection**, **amministratore conformità**, **amministratore dati di conformità** o **amministratore globale** da Azure Active Directory o ruolo di amministratore globale per il servizio di protezione.

## <a name="updating-personal-data"></a>Aggiornamento dei dati personali

**Client di etichettatura unificata**:

Per il client di etichettatura unificata, le etichette di riservatezza e i criteri delle etichette sono configurati nel centro sicurezza Microsoft 365, nel centro di conformità Microsoft 365 o nel Microsoft 365 Security & Compliance Center. Per altre informazioni, vedere la [documentazione di Microsoft 365](/microsoft-365/compliance/sensitivity-labels).

**Client classico**:

Per il client classico, è possibile aggiornare gli indirizzi di posta elettronica per i criteri con ambito e le impostazioni di protezione nei criteri di Azure Information Protection. Per altre informazioni, vedere [How to configure the Azure Information Protection policy for specific users by using scoped policies](configure-policy-scope.md) (Come configurare i criteri di Azure Information Protection per utenti specifici tramite criteri con ambito) e [Come configurare un'etichetta per la protezione di Rights Management](configure-policy-protection.md). 

Per le impostazioni di protezione, è possibile aggiornare le stesse informazioni usando i cmdlet di PowerShell del [modulo AIPService](/powershell/module/aipservice).

Non è possibile aggiornare gli indirizzi di posta elettronica per gli utenti con privilegi avanzati e gli amministratori con delega. Rimuovere invece l'account utente specificato e aggiungere l'account utente con l'indirizzo di posta elettronica aggiornato. 

### <a name="super-users-and-delegated-administrators-for-the-protection-service"></a>Utenti con privilegi avanzati e amministratori delegati per il servizio di protezione

Quando è necessario aggiornare un indirizzo di posta elettronica per un utente con privilegi avanzati:

1. Usare [Remove-AipServiceSuperUser](/powershell/module/aipservice/Remove-AipServiceSuperUser) per rimuovere l'utente e l'indirizzo di posta elettronica precedente.

2. Usare [Add-AipServiceSuperUser](/powershell/module/aipservice/Add-AipServiceSuperUser) per aggiungere l'utente e il nuovo indirizzo di posta elettronica.

Quando è necessario aggiornare un indirizzo di posta elettronica per un amministratore con delega:

1. Usare [Remove-AipServiceRoleBasedAdministrator](/powershell/module/aipservice/Remove-AipServiceRoleBasedAdministrator) per rimuovere l'utente e l'indirizzo di posta elettronica precedente.

2. Usare [Add-AipServiceRoleBasedAdministrator](/powershell/module/aipservice/Add-AipServiceRoleBasedAdministrator) per aggiungere l'utente e il nuovo indirizzo di posta elettronica.

### <a name="protection-templates"></a>Modelli di protezione

**Pertinente per**: solo client classico

Eseguire il cmdlet [set-AipServiceTemplateProperty](/powershell/module/aipservice/set-aipservicetemplateproperty) per aggiornare il modello di protezione. Poiché i dati personali si trovano all'interno della `RightsDefinitions` proprietà, è necessario usare anche il cmdlet [New-AipServiceRightsDefinition](/powershell/module/aipservice/new-aipservicerightsdefinition) per creare un oggetto delle definizioni dei diritti con le informazioni aggiornate e usare l'oggetto delle definizioni dei diritti con il `Set-AipServiceTemplateProperty` cmdlet.

## <a name="deleting-personal-data"></a>Eliminazione dei dati personali

- **Client di etichettatura unificata**:

    Per il client di etichettatura unificata, le etichette di riservatezza e i criteri delle etichette sono configurati nel centro sicurezza Microsoft 365, nel centro di conformità Microsoft 365 o nel Microsoft 365 Security & Compliance Center. Per altre informazioni, vedere la [documentazione di Microsoft 365](/microsoft-365/compliance/sensitivity-labels).

- **Client classico**:

    Per il client classico, è possibile eliminare gli indirizzi di posta elettronica per i criteri con ambito e le impostazioni di protezione nei criteri di Azure Information Protection. Per altre informazioni, vedere [How to configure the Azure Information Protection policy for specific users by using scoped policies](configure-policy-scope.md) (Come configurare i criteri di Azure Information Protection per utenti specifici tramite criteri con ambito) e [Come configurare un'etichetta per la protezione di Rights Management](configure-policy-protection.md). 

Per le impostazioni di protezione, è possibile eliminare le stesse informazioni usando i cmdlet di PowerShell del [modulo AIPService](/powershell/module/aipservice).

Per eliminare gli indirizzi di posta elettronica per utenti con privilegi avanzati e amministratori delegati, rimuovere questi utenti usando il cmdlet [Remove-AipServiceSuperUser](/powershell/module/aipservice/Remove-AipServiceSuperUser) e [Remove-AipServiceRoleBasedAdministrator](/powershell/module/aipservice/Remove-AipServiceRoleBasedAdministrator). 

Per eliminare i dati personali nei log di rilevamento dei documenti, nei log di amministrazione o nei log di utilizzo per il servizio di protezione, utilizzare la sezione seguente per generare una richiesta con supporto tecnico Microsoft.

Per eliminare dati personali nei file di log dei client e nei log dello scanner archiviati nei computer, usare qualsiasi strumento di Windows standard per eliminare i file o i dati personali all'interno dei file. 

### <a name="to-delete-personal-data-with-microsoft-support"></a>Per eliminare dati personali con il supporto tecnico Microsoft

Utilizzare i tre passaggi seguenti per richiedere che Microsoft elimini i dati personali nei log di rilevamento dei documenti, nei log di amministrazione o nei log di utilizzo per il servizio di protezione. 

**Passaggio 1: avviare la richiesta** 
 di eliminazione [Contattare supporto tecnico Microsoft](information-support.md#to-contact-microsoft-support) per aprire un caso di supporto Azure Information Protection con una richiesta di eliminazione dei dati dal tenant. È necessario dimostrare di essere un amministratore del tenant di Azure Information Protection e tenere presente che la conferma di questo processo richiede diversi giorni. Nell'inviare la richiesta, è necessario fornire informazioni aggiuntive, a seconda dei dati che devono essere eliminati.

- Per eliminare il log di amministrazione, specificare la **data di fine**. Verranno eliminati tutti i log di amministrazione fino alla data di fine specificata.
- Per eliminare i log sull'utilizzo, specificare la **data di fine**. Verranno eliminati tutti i log sull'utilizzo fino alla data di fine specificata.
- Per eliminare i log di rilevamento dei documenti, specificare il parametro **UserEmail**. Verranno eliminate tutte le informazioni sul rilevamento dei documenti correlate a UserEmail.

L'eliminazione di questi dati è un'operazione permanente. Al termine dell'elaborazione di una richiesta di eliminazione, non sarà possibile recuperare i dati in alcun modo. Si consiglia agli amministratori di esportare i dati necessari prima di inviare una richiesta di eliminazione.

**Passaggio 2: Attendere la verifica** Microsoft verificherà la legittimità della richiesta di eliminazione di uno o più log. Questo processo può richiedere fino a cinque giorni lavorativi.

**Fase 3: Ottenere la conferma dell'eliminazione** Il servizio di supporto tecnico Microsoft invierà un messaggio di posta elettronica di conferma dell'avvenuta eliminazione dei dati. 

## <a name="exporting-personal-data"></a>Esportazione dei dati personali
Quando si usano i cmdlet di PowerShell AIPService o AADRM, i dati personali vengono resi disponibili per la ricerca e l'esportazione come oggetto PowerShell. L'oggetto di PowerShell può essere convertito in JSON e salvato tramite il cmdlet `ConvertTo-Json`.

## <a name="restricting-the-use-of-personal-data-for-profiling-or-marketing-without-consent"></a>Limitazione dell'uso dei dati personali per la profilatura o il marketing senza consenso dell'utente
Azure Information Protection segue l'[condizioni per la privacy](https://privacy.microsoft.com/privacystatement) Microsoft per la profilatura e il marketing basati su dati personali.

## <a name="auditing-and-reporting"></a>Controllo e creazione di report
Solo gli utenti a cui sono state assegnate [autorizzazioni di amministratore](#securing-and-controlling-access-to-personal-information) possono usare il modulo AIPSERVICE o addr per la ricerca e l'esportazione di dati personali. Queste operazioni vengono registrate nel log di amministrazione, che può essere scaricato.

Per le azioni di eliminazione, la richiesta di supporto funge da audit trail e percorso di segnalazione per le azioni eseguite da Microsoft. Dopo l'eliminazione, i dati eliminati non saranno disponibili per la ricerca e l'esportazione e l'amministratore potrà verificarla usando i cmdlet Get del modulo AIPService.
