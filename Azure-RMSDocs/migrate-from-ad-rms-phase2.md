---
title: Eseguire la migrazione da AD RMS ad Azure Information Protection - Fase 2
description: Fase 2 della migrazione da AD RMS ad Azure Information Protection, che include i passaggi da 4 a 6 della migrazione da AD RMS ad Azure Information Protection.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 07/03/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 5a189695-40a6-4b36-afe6-0823c94993ef
ms.subservice: migration
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: ff2f088358d6f15b4e5b67c3cc6929b1f29f19f4
ms.sourcegitcommit: 9968a003865ff2456c570cf552f801a816b1db07
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/05/2019
ms.locfileid: "68793998"
---
# <a name="migration-phase-2---server-side-configuration-for-ad-rms"></a>Fase 2 della migrazione: configurazione lato server per AD RMS

>*Si applica a: Active Directory Rights Management Services, [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

Usare le informazioni seguenti per la fase 2 della migrazione da AD RMS ad Azure Information Protection. Queste procedure illustrano i passaggi da 4 a 6 della [Migrazione da AD RMS ad Azure Information Protection](migrate-from-ad-rms-to-azure-rms.md).


## <a name="step-4-export-configuration-data-from-ad-rms-and-import-it-to-azure-information-protection"></a>Passaggio 4. Esportare i dati di configurazione da AD RMS e importarli in Azure Information Protection
Questo passaggio è un processo costituito da due parti:

1. Esportare i dati di configurazione da AD RMS esportando i domini di pubblicazione trusted in un file XML. Questo processo è identico per tutte le migrazioni.

2. Importare i dati di configurazione in Azure Information Protection. Per questo passaggio esistono diversi processi, a seconda della configurazione della distribuzione corrente di AD RMS e della topologia preferita per la chiave del tenant di Azure RMS.

### <a name="export-the-configuration-data-from-ad-rms"></a>Esportare i dati di configurazione da AD RMS.

Eseguire le operazioni seguenti in tutti i cluster AD RMS, per tutti i domini di pubblicazione trusted con contenuto protetto per l'organizzazione. Non è necessario eseguire questa procedura nei cluster usati per la sola gestione delle licenze.

#### <a name="to-export-the-configuration-data-trusted-publishing-domain-information"></a>Per esportare i dati di configurazione (informazioni su domini di pubblicazione trusted)

1. Accedere al cluster AD RMS come utente con autorizzazioni di amministratore di AD RMS.

2. Dalla console di gestione di AD RMS (**Active Directory Rights Management Services**), espandere il nome del cluster AD RMS, espandere **Criteri di attendibilità**e quindi fare clic su **Domini di pubblicazione trusted**.

3. Nel riquadro dei risultati selezionare il dominio di pubblicazione trusted e quindi nel riquadro Azioni fare clic su **Esporta dominio di pubblicazione Trusted**.

4. Nella finestra di dialogo **Esporta dominio di pubblicazione trusted** :

    - Fare clic su **Salva con nome** e salvare in un percorso e con un nome file a propria scelta. Assicurarsi di specificare **.xml** come estensione di file (non viene aggiunta automaticamente).

    - Specificare e confermare una password complessa. Prendere nota della password, perché sarà necessaria in seguito per l'importazione dei dati di configurazione in Azure Information Protection.

    - Non selezionare la casella di controllo per salvare il file di dominio trusted in RMS versione 1.0.

Dopo l'esportazione di tutti i domini di pubblicazione trusted, sarà possibile avviare la procedura di importazione dei dati in Azure Information Protection.

Si noti che i domini di pubblicazione trusted includono le chiavi del certificato concessore licenze server per decrittografare i file protetti in precedenza, quindi è importante esportare (e successivamente importare in Azure) tutti i domini di pubblicazione trusted e non solo quello attualmente attivo.

Ad esempio, si avranno più domini di pubblicazione trusted se sono stati aggiornati i server AD RMS dalla modalità di crittografia 1 alla modalità di crittografia 2. Se non si esporta e importa il dominio di pubblicazione trusted che contiene la chiave archiviata che usava la modalità di crittografia 1, alla fine della migrazione gli utenti non riusciranno ad aprire il contenuto protetto con la chiave di modalità di crittografia 1.


### <a name="import-the-configuration-data-to-azure-information-protection"></a>Importare i dati di configurazione in Azure Information Protection
Le procedure esatte per questo passaggio dipendono dalla configurazione della distribuzione corrente di AD RMS e dalla topologia preferita per la chiave del tenant di Azure Information Protection.

La distribuzione corrente di AD RMS usa una delle seguenti configurazioni per la chiave del certificato concessore di licenze server (SLC):

- Password di protezione nel database AD RMS. Questa è la configurazione predefinita.

- Protezione con HSM usando un modulo di protezione hardware nCipher.

- Protezione HSM tramite un modulo di protezione hardware (HSM) di un fornitore diverso da nCipher.

- Protezione con password tramite un provider del servizio di crittografia esterno.

> [!NOTE]
> Per altre informazioni sull'uso di moduli di protezione hardware con AD RMS, vedere [Uso di AD RMS con moduli di protezione hardware](https://technet.microsoft.com/library/jj651024.aspx).

Le due opzioni di topologia di chiave del tenant di Azure Information Protection sono: la chiave del tenant viene gestita da Microsoft (**gestione di Microsoft**) oppure dall'utente (**gestione del cliente**) in Azure Key Vault. Quando la chiave del tenant di Azure Information Protection è gestita dall'utente, viene a volte definita BYOK (Bring Your Own Key). Per altre informazioni, vedere l'articolo [Pianificazione e implementazione della chiave del tenant di Azure Information Protection](plan-implement-tenant-key.md).

Usare la tabella seguente per identificare la procedura da eseguire per la migrazione. 

|Distribuzione di AD RMS corrente|Topologia di chiave del tenant di Azure Information Protection scelta|Istruzioni relative alla migrazione|
|-----------------------------|----------------------------------------|--------------------------|
|Password di protezione nel database AD RMS|Gestione di Microsoft|Vedere la procedura **Migrazione da una chiave protetta tramite software a un'altra** dopo questa tabella.<br /><br />Questo è il percorso di migrazione più semplice e richiede solo il trasferimento dei dati di configurazione ad Azure Information Protection.|
|Protezione HSM con un modulo di protezione hardware nCipher nShield (HSM) |Gestione del cliente (scenario BYOK)|Vedere la procedura **Migrazione da una chiave protetta tramite HSM a un'altra** dopo questa tabella.<br /><br />Sono necessari il set di strumenti BYOK di Azure Key Vault e tre procedure: il trasferimento della chiave dal modulo di protezione hardware locale ai moduli di protezione hardware di Azure Key Vault, l'autorizzazione del servizio Azure Rights Management di Azure Information Protection all'uso della chiave del tenant e infine il trasferimento dei dati di configurazione in Azure Information Protection.|
|Password di protezione nel database AD RMS|Gestione del cliente (scenario BYOK)|Vedere la procedura di migrazione **Da una chiave protetta tramite software a una chiave protetta tramite HSM** dopo questa tabella.<br /><br />Sono necessari il set di strumenti BYOK di Insieme di credenziali delle chiavi di Azure e quattro procedure: innanzitutto estrarre la chiave software e importarla nel modulo di protezione hardware locale, quindi trasferire la chiave dal modulo di protezione hardware locale ai moduli di protezione hardware di Azure Information Protection, successivamente trasferire i dati dell'insieme di credenziali in Azure Information Protection e infine trasferire i dati di configurazione in Azure Information Protection.|
|Protezione con HSM tramite un modulo di protezione hardware di un fornitore diverso da nCipher |Gestione del cliente (scenario BYOK)|Contattare il fornitore del modulo di protezione hardware per istruzioni su come trasferire la chiave da questo modulo di protezione hardware a un modulo di protezione hardware nCipher nShield (HSM). Seguire quindi le istruzioni per la procedura di migrazione **Da una chiave protetta tramite HSM a un’altra** dopo questa tabella.|
|Protezione con password tramite un provider del servizio di crittografia esterno|Gestione del cliente (scenario BYOK)|Contattare il fornitore del provider del servizio di crittografia per istruzioni su come trasferire la chiave a un modulo di protezione hardware nCipher nShield (HSM). Seguire quindi le istruzioni per la procedura di migrazione **Da una chiave protetta tramite HSM a un’altra** dopo questa tabella.|

Se la chiave protetta tramite modulo di protezione hardware non è esportabile, è comunque possibile eseguire la migrazione ad Azure Information Protection configurando il cluster AD RMS con la modalità di sola lettura. In questa modalità è comunque possibile aprire il contenuto protetto in precedenza, ma il contenuto appena protetto usa una nuova chiave del tenant gestita dall'utente (BYOK) o gestita da Microsoft. Per altre informazioni, vedere [An update is available for Office to support migrations from AD RMS to Azure RMS](https://support.microsoft.com/help/4023955/an-update-is-available-for-office-to-support-migrations-from-ad-rms-to) (È disponibile un aggiornamento con cui Office supporta le migrazioni da AD RMS ad Azure RMS).

Prima di iniziare queste procedure per la migrazione di chiavi, verificare che sia possibile accedere ai file con estensione XML creati in precedenza durante l'esportazione dei domini di pubblicazione trusted. Ad esempio, è possibile salvarli su una chiavetta USB che può essere spostata dal server AD RMS alla workstation connessa a Internet.

> [!NOTE]
> Indipendentemente dalla modalità di archiviazione di questi file, per proteggerli attenersi alle procedure consigliate per la sicurezza, poiché tali dati includono la chiave privata.

Per completare il passaggio 4, scegliere e selezionare le istruzioni per il percorso di migrazione: 

- [Da una chiave protetta tramite software a un'altra](migrate-softwarekey-to-softwarekey.md)
- [Da una chiave protetta tramite HSM a un'altra](migrate-hsmkey-to-hsmkey.md)
- [Da una chiave protetta tramite software a una chiave protetta tramite HSM](migrate-softwarekey-to-hsmkey.md)

## <a name="step-5-activate-the-azure-rights-management-service"></a>Passaggio 5. Attivare il servizio Azure Rights Management

Aprire una sessione di PowerShell ed eseguire i comandi seguenti:

1. Connettersi al servizio Azure Rights Management e, quando richiesto, specificare le credenziali di amministratore globale:
    
        Connect-AipService

2. Attivare il servizio Azure Rights Management:
    
        Enable-AipService

**Che cosa accade se il tenant di Azure Information Protection è già attivato?** Se il servizio Azure Rights Management è già attivato per l'organizzazione e sono stati creati modelli personalizzati che si vogliono usare dopo la migrazione, è necessario esportare e importare questi modelli. Questa procedura viene descritta nel passaggio successivo. 

## <a name="step-6-configure-imported-templates"></a>Passaggio 6. Configurare i modelli importati

Poiché i modelli importati hanno uno stato predefinito **Archiviato**, è necessario impostare questo stato su **Pubblicato** se si vuole consentire agli utenti di usarli con il servizio Azure Rights Management.

I modelli importati da AD RMS hanno lo stesso aspetto e comportamento dei modelli personalizzati che è possibile creare nel portale di Azure. Per modificare i modelli importati in modo da pubblicarli e renderli visualizzabili e selezionabili per gli utenti dalle applicazioni, vedere [Configuring and managing templates for Azure Information Protection](./configure-policy-templates.md) (Configurazione e gestione di modelli per Azure Information Management).

Oltre a pubblicare i modelli importati, vi sono due importanti modifiche per i modelli che potrebbe essere necessario apportare prima di continuare con la migrazione. Per un'esperienza più coerente per gli utenti durante il processo di migrazione, in questa fase non apportare altre modifiche ai modelli importati, non pubblicare i due modelli predefiniti specificati con Azure Information Protection e non crearne di nuovi. Attendere invece che il processo di migrazione sia completo e che sia stato effettuato il deprovisioning dei server AD RMS.

Le modifiche del modello che potrebbe essere necessario apportare per questo passaggio sono le seguenti:

- Se sono stati creati modelli personalizzati in Azure Information Protection prima della migrazione, è necessario esportarli e importarli manualmente.

- Se i modelli in AD RMS usavano il gruppo **ANYONE**, potrebbe essere necessario aggiungere manualmente utenti o gruppi. 
    
    In AD RMS il gruppo ANYONE concedeva i diritti a tutti gli utenti autenticati da Active Directory in locale e questo gruppo non è supportato da Azure Information Protection. L'equivalente più simile è un gruppo che viene creato automaticamente per tutti gli utenti nel tenant di Azure AD. Se veniva usato il gruppo ANYONE per i modelli di AD RMS, potrebbe essere necessario aggiungere gli utenti e i diritti da concedere loro.

### <a name="procedure-if-you-created-custom-templates-before-the-migration"></a>Procedura da seguire se i modelli personalizzati sono stati creati prima della migrazione

Se i modelli personalizzati sono stati creati prima della migrazione, prima o dopo l'attivazione del servizio Azure Rights Management, i modelli non saranno disponibili per gli utenti dopo la migrazione, anche se sono stati impostati su **Pubblicato**. Per renderli disponibili agli utenti, è necessario eseguire prima le operazioni seguenti: 

1. Identificare questi modelli e prendere nota dell'ID modello, eseguendo [Get-AipServiceTemplate](/powershell/module/aipservice/get-aipservicetemplate). 

2. Esportare i modelli tramite il cmdlet Azure RMS PowerShell, [Export-AipServiceTemplate](/powershell/module/aipservice/export-aipservicetemplate).

3. Importare i modelli tramite il cmdlet Azure RMS PowerShell, [Import-AipServiceTemplate](/powershell/module/aipservice/import-aipservicetpd).

È quindi possibile pubblicare o archiviare questi modelli come qualsiasi altro modello creato dopo la migrazione.

### <a name="procedure-if-your-templates-in-ad-rms-used-the-anyone-group"></a>Procedura da seguire se i modelli in AD RMS hanno usato il gruppo **ANYONE**

Se i modelli in AD RMS usavano il gruppo **ANYONE**, il gruppo equivalente più simile in Azure Information Protection è denominato **AllStaff-7184AB3F-CCD1-46F3-8233-3E09E9CF0E66@\<nome_tenant>.onmicrosoft.com**. Ad esempio, questo gruppo può essere simile al seguente per Contoso: <strong>AllStaff-7184AB3F-CCD1-46F3-8233-3E09E9CF0E66@contoso.onmicrosoft.com</strong>. Questo gruppo contiene tutti gli utenti del tenant di Azure AD.

Quando si gestiscono i modelli e le etichette nel portale di Azure, questo gruppo viene visualizzato come nome di dominio del tenant di Azure AD. Ad esempio, questo gruppo potrebbe essere simile al seguente per Contoso: **contoso.onmicrosoft.com**. Per aggiungere questo gruppo, l'opzione visualizza **Aggiungi \<nome organizzazione>-Tutti i membri**.

Se non si è certi che i modelli AD RMS includano il gruppo ANYONE, è possibile usare lo script di Windows PowerShell di esempio seguente per identificare tali modelli. Per altre informazioni sull'uso di Windows PowerShell con AD RMS, vedere l'articolo relativo a [Using Windows PowerShell to Administer AD RMS (Uso di Windows PowerShell per amministrare AD RMS)](https://technet.microsoft.com/library/ee221079%28v=ws.10%29.aspx).

È possibile aggiungere con facilità utenti esterni ai modelli, quando si convertono questi modelli in etichette nel portale di Azure. Sul pannello **Aggiungi autorizzazioni**, scegliere **Immetti i dettagli** per specificare manualmente gli indirizzi di posta elettronica per questi utenti. 

Per altre informazioni su questa configurazione, vedere [Come configurare un'etichetta per la protezione di Rights Management](./configure-policy-protection.md).

#### <a name="sample-windows-powershell-script-to-identify-ad-rms-templates-that-include-the-anyone-group"></a>Esempio di script di Windows PowerShell per identificare modelli AD RMS che includono il gruppo ANYONE
Questa sezione include lo script di esempio per facilitare l'identificazione dei modelli AD RMS per i quali è definito un gruppo ANYONE, come descritto nella sezione precedente.

**Dichiarazione di non responsabilità:** Questo script di esempio non è supportato in alcun programma o servizio di supporto standard Microsoft. Questo script di esempio viene fornito "nello stato in stato in cui si trova" senza garanzia di alcun tipo.

```
import-module adrmsadmin 

New-PSDrive -Name MyRmsAdmin -PsProvider AdRmsAdmin -Root https://localhost -Force 

$ListofTemplates=dir MyRmsAdmin:\RightsPolicyTemplate

foreach($Template in $ListofTemplates) 
{ 
                $templateID=$Template.id

                $rights = dir MyRmsAdmin:\RightsPolicyTemplate\$Templateid\userright

     $templateName=$Template.DefaultDisplayName 

        if ($rights.usergroupname -eq "anyone")

                         {
                           $templateName = $Template.defaultdisplayname

                           write-host "Template " -NoNewline

                           write-host -NoNewline $templateName -ForegroundColor Red

                           write-host " contains rights for " -NoNewline

                           write-host ANYONE  -ForegroundColor Red
                         }
 } 
Remove-PSDrive MyRmsAdmin -force
```


## <a name="next-steps"></a>Passaggi successivi
Passare A [Fase 3: configurazione lato client](migrate-from-ad-rms-phase3.md).
