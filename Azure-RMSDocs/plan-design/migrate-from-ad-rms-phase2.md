---
title: Eseguire la migrazione da AD RMS ad Azure Information Protection - Fase 2
description: Fase 2 della migrazione da AD RMS ad Azure Information Protection, che include i passaggi da 4 a 6 della migrazione da AD RMS ad Azure Information Protection.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 07/31/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 5a189695-40a6-4b36-afe6-0823c94993ef
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 9f04698064037343719d274e793eb560b703b031
ms.sourcegitcommit: 55a71f83947e7b178930aaa85a8716e993ffc063
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/31/2017
---
# <a name="migration-phase-2---server-side-configuration-for-ad-rms"></a>Fase 2 della migrazione: configurazione lato server per AD RMS

>*Si applica a: Active Directory Rights Management Services, Azure Information Protection, Office 365*

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

- Protezione tramite un modulo di protezione hardware Thales.

- Modulo di protezione hardware tramite un modulo di protezione hardware di un fornitore diverso da Thales.

- Protezione con password tramite un provider del servizio di crittografia esterno.

> [!NOTE]
> Per altre informazioni sull'uso di moduli di protezione hardware con AD RMS, vedere [Uso di AD RMS con moduli di protezione hardware](http://technet.microsoft.com/library/jj651024.aspx).

Per la topologia della chiave del tenant di Azure Information Protection esistono due opzioni: la chiave viene gestita da Microsoft (**gestione di Microsoft**) oppure dall'utente (**gestione del cliente**) in Insieme di credenziali delle chiavi di Azure. Quando la chiave del tenant di Azure Information Protection è gestita dall'utente, viene a volte definita BYOK (Bring Your Own Key) e richiede un modulo di protezione hardware di Thales. Per altre informazioni, vedere l'articolo [Pianificazione e implementazione della chiave del tenant di Azure Information Protection](plan-implement-tenant-key.md).

> [!IMPORTANT]
> Exchange Online non è attualmente compatibile con la modalità BYOK in Azure Information Protection. Se si vuole usare la modalità BYOK dopo la migrazione e si prevede di usare Exchange Online, verificare come questa configurazione riduce la funzionalità IRM per Exchange Online. Rivedere le informazioni fornite in [Prezzi e restrizioni della modalità BYOK](byok-price-restrictions.md) per poter scegliere la migliore topologia di chiave del tenant di Azure Information Protection per la migrazione.

Usare la tabella seguente per identificare la procedura da eseguire per la migrazione. 

|Distribuzione di AD RMS corrente|Topologia di chiave del tenant di Azure Information Protection scelta|Istruzioni relative alla migrazione|
|-----------------------------|----------------------------------------|--------------------------|
|Password di protezione nel database AD RMS|Gestione di Microsoft|Vedere la procedura **Migrazione da una chiave protetta tramite software a un'altra** dopo questa tabella.<br /><br />Questo è il percorso di migrazione più semplice e richiede solo il trasferimento dei dati di configurazione ad Azure Information Protection.|
|Modulo di protezione hardware tramite un modulo di protezione hardware nShield di Thales |Gestione del cliente (scenario BYOK)|Vedere la procedura **Migrazione da una chiave protetta tramite HSM a un'altra** dopo questa tabella.<br /><br />Sono necessari il set di strumenti BYOK di Azure Key Vault e tre procedure: il trasferimento della chiave dal modulo di protezione hardware locale ai moduli di protezione hardware di Azure Key Vault, l'autorizzazione del servizio Azure Rights Management di Azure Information Protection all'uso della chiave del tenant e infine il trasferimento dei dati di configurazione in Azure Information Protection.|
|Password di protezione nel database AD RMS|Gestione del cliente (scenario BYOK)|Vedere la procedura di migrazione **Da una chiave protetta tramite software a una chiave protetta tramite HSM** dopo questa tabella.<br /><br />Sono necessari il set di strumenti BYOK di Insieme di credenziali delle chiavi di Azure e quattro procedure: innanzitutto estrarre la chiave software e importarla nel modulo di protezione hardware locale, quindi trasferire la chiave dal modulo di protezione hardware locale ai moduli di protezione hardware di Azure Information Protection, successivamente trasferire i dati dell'insieme di credenziali in Azure Information Protection e infine trasferire i dati di configurazione in Azure Information Protection.|
|Modulo di protezione hardware tramite un modulo di protezione hardware di un fornitore diverso da Thales. |Gestione del cliente (scenario BYOK)|Per istruzioni sul trasferimento della chiave da questo modulo a un modulo di protezione hardware nShield di Thales, contattare il fornitore del modulo di protezione hardware. Seguire quindi le istruzioni per la procedura di migrazione **Da una chiave protetta tramite HSM a un’altra** dopo questa tabella.|
|Protezione con password tramite un provider del servizio di crittografia esterno|Gestione del cliente (scenario BYOK)|Per istruzioni sul trasferimento della chiave a un modulo di protezione hardware nShield di Thales, contattare il fornitore del servizio di crittografia. Seguire quindi le istruzioni per la procedura di migrazione **Da una chiave protetta tramite HSM a un’altra** dopo questa tabella.|

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
    
        Connect-Aadrmservice

2. Attivare il servizio Azure Rights Management:
    
        Enable-Aadrmservice

**Che cosa accade se il tenant di Azure Information Protection è già attivato?** Se il servizio Azure Rights Management è già attivato per l'organizzazione, gli utenti potrebbero avere già usato Azure Information Protection per proteggere il contenuto con una chiave del tenant generata automaticamente (e con i modelli predefiniti) invece che con le chiavi (e i modelli) esistenti inclusi in AD RMS. È poco probabile che questo accada in computer gestiti correttamente nell'intranet, perché questi sono automaticamente configurati per l'infrastruttura AD RMS. Può però verificarsi su computer di un gruppo di lavoro o su computer che non si connettono spesso alla Intranet. Dal momento che sfortunatamente è anche difficile identificare questi computer, si consiglia di non attivare il servizio prima di importare i dati di configurazione da AD RMS.

Se il tenant di Azure Information Protection è già attivato ed è possibile identificare questi computer, assicurarsi di eseguire lo script CleanUpRMS.cmd nei computer, come descritto nel [Passaggio 7](migrate-from-ad-rms-phase3.md#step-7-reconfigure-clients-to-use-azure-information-protection). L'esecuzione dello script li obbliga a reinizializzare l'ambiente utente e quindi a scaricare la chiave del tenant aggiornata e i modelli importati.

Se sono stati creati anche modelli personalizzati da usare dopo la migrazione, è necessario esportare e importare questi modelli. Questa procedura viene descritta nel passaggio successivo. 

## <a name="step-6-configure-imported-templates"></a>Passaggio 6. Configurare i modelli importati

Poiché i modelli importati hanno uno stato predefinito **Archiviato**, è necessario impostare questo stato su **Pubblicato** se si vuole consentire agli utenti di usarli con il servizio Azure Rights Management.

I modelli importati da AD RMS hanno lo stesso aspetto e comportamento dei modelli personalizzati che è possibile creare nel portale di Azure. Per modificare i modelli importati in modo da pubblicarli e renderli visualizzabili e selezionabili per gli utenti dalle applicazioni, vedere [Configuring and managing templates for Azure Information Protection](../deploy-use/configure-policy-templates.md) (Configurazione e gestione di modelli per Azure Information Management).

Oltre a pubblicare i modelli importati, vi sono due importanti modifiche per i modelli che potrebbe essere necessario apportare prima di continuare con la migrazione. Per un'esperienza più coerente per gli utenti durante il processo di migrazione, in questa fase non apportare altre modifiche ai modelli importati, non pubblicare i due modelli predefiniti specificati con Azure Information Protection e non crearne di nuovi. Attendere invece che il processo di migrazione sia completo e che sia stato effettuato il deprovisioning dei server AD RMS.

Le modifiche del modello che potrebbe essere necessario apportare per questo passaggio sono le seguenti:

- Se sono stati creati modelli personalizzati in Azure Information Protection prima della migrazione, è necessario esportarli e importarli manualmente.

- Se i modelli di AD RMS hanno usato il gruppo **ANYONE**, è necessario aggiungere manualmente i diritti e il gruppo equivalente.

### <a name="procedure-if-you-created-custom-templates-before-the-migration"></a>Procedura da seguire se i modelli personalizzati sono stati creati prima della migrazione

Se i modelli personalizzati sono stati creati prima della migrazione, prima o dopo l'attivazione del servizio Azure Rights Management, i modelli non saranno disponibili per gli utenti dopo la migrazione, anche se sono stati impostati su **Pubblicato**. Per renderli disponibili agli utenti, è necessario eseguire prima le operazioni seguenti: 

1. Identificare i modelli e prendere nota del relativo ID modello, eseguendo [Get-AadrmTemplate](/powershell/aadrm/vlatest/get-aadrmtemplate). 

2. Esportare i modelli tramite il cmdlet PowerShell di Azure RMS, [Export-AadrmTemplate](/powershell/aadrm/vlatest/export-aadrmtemplate).

3. Importare i modelli tramite il cmdlet PowerShell di Azure RMS, [Import-AadrmTemplate](/powershell/aadrm/vlatest/Import-AadrmTpd).

È quindi possibile pubblicare o archiviare questi modelli come qualsiasi altro modello creato dopo la migrazione.

### <a name="procedure-if-your-templates-in-ad-rms-used-the-anyone-group"></a>Procedura da seguire se i modelli in AD RMS hanno usato il gruppo **ANYONE**

Se i modelli in AD RMS hanno usato il gruppo **ANYONE**, questo gruppo viene rimosso automaticamente quando si importano i modelli in Azure Information Protection. È necessario aggiungere manualmente il gruppo o gli utenti equivalenti e gli stessi diritti ai modelli importati. Il gruppo equivalente per Azure Information Protection viene denominato **AllStaff-7184AB3F-CCD1-46F3-8233-3E09E9CF0E66@\<nome_tenant>.onmicrosoft.com**. Ad esempio, questo gruppo può essere simile al seguente per Contoso: **AllStaff-7184AB3F-CCD1-46F3-8233-3E09E9CF0E66@contoso.onmicrosoft.com**.

Se non si è certi che i modelli AD RMS includano il gruppo ANYONE, è possibile usare lo script di Windows PowerShell di esempio seguente per identificare tali modelli. Per altre informazioni sull'uso di Windows PowerShell con AD RMS, vedere l'articolo relativo all'[uso di Windows PowerShell per amministrare AD RMS](https://technet.microsoft.com/library/ee221079%28v=ws.10%29.aspx).

È possibile vedere il gruppo creato automaticamente dell'organizzazione copiando uno dei modelli di criteri per i diritti predefiniti nel portale di Azure classico e quindi identificando il **NOME UTENTE** nella pagina **DIRITTI**. Non è tuttavia possibile usare il portale di Azure classico per aggiungere questo gruppo a un modello creato manualmente o importato. È invece necessario usare una delle opzioni di Azure RMS PowerShell seguenti:

- Usare il cmdlet di PowerShell [New-AadrmRightsDefinition](/powershell/aadrm/vlatest/new-aadrmrightsdefinition) per definire il gruppo "AllStaff" e i diritti come un oggetto di definizione dei diritti ed eseguire di nuovo questo comando per ognuno degli altri gruppi o utenti a cui sono già stati concessi diritti nel modello originale, in aggiunta al gruppo ANYONE. Aggiungere quindi tutti questi oggetti di definizione dei diritti ai modelli con il cmdlet [Set-AadrmTemplateProperty](/powershell/aadrm/vlatest/set-aadrmtemplateproperty).

- Usare il cmdlet [Export-AadrmTemplate](/powershell/aadrm/vlatest/export-aadrmtemplate) per esportare il modello in un file con estensione xml che è possibile modificare per aggiungere il gruppo "AllStaff" e i diritti ai gruppi e ai diritti esistenti. Usare quindi il cmdlet [Import-AadrmTemplate](/powershell/aadrm/vlatest/import-aadrmtemplate) per importare di nuovo le modifiche in Azure Information Protection.

> [!NOTE]
> Questo gruppo equivalente "AllStaff" non corrisponde esattamente al gruppo ANYONE in AD RMS: il gruppo "AllStaff" include tutti gli utenti nel tenant di Azure, mentre il gruppo ANYONE comprende tutti gli utenti autenticati, che potrebbero essere esterni all'organizzazione.
> 
> A causa di questa differenza tra i due gruppi, potrebbe essere necessario aggiungere anche gli utenti esterni in aggiunta al gruppo "AllStaff". Gli indirizzi email esterni per i gruppi attualmente non sono supportati.


#### <a name="sample-windows-powershell-script-to-identify-ad-rms-templates-that-include-the-anyone-group"></a>Esempio di script di Windows PowerShell per identificare modelli AD RMS che includono il gruppo ANYONE
Questa sezione include lo script di esempio per facilitare l'identificazione dei modelli AD RMS per i quali è definito un gruppo ANYONE, come descritto nella sezione precedente.

**Dichiarazione di non responsabilità:** questo script di esempio non è supportato in alcun programma o servizio di supporto standard Microsoft. Questo script di esempio viene fornito "nello stato in stato in cui si trova" senza garanzia di alcun tipo.

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
Passare A [Fase 3: configurazione lato client](migrate-from-ad-rms-phase2.md).

[!INCLUDE[Commenting house rules](../includes/houserules.md)]