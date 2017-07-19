---
title: Protezione di Azure RMS con l'infrastruttura di classificazione file per Windows Server - AIP
description: "Istruzioni per usare il client Rights Management (RMS) con lo strumento di protezione RMS per configurare Gestione risorse file server e la funzionalità Infrastruttura di classificazione file."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 05/18/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 9aa693db-9727-4284-9f64-867681e114c9
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: b56955d8a01876f4107cafa5b1b8df922c0f8ad0
ms.sourcegitcommit: 04eb4990e2bf0004684221592cb93df35e6acebe
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/30/2017
---
# <a name="rms-protection-with-windows-server-file-classification-infrastructure-fci"></a>Protezione RMS con l'infrastruttura di classificazione file (FCI, File Classification Infrastructure) per Windows Server

>*Si applica a: Azure Information Protection, Windows Server 2016, Windows Server 2012, Windows Server 2012 R2*

Usare questo articolo per ottenere istruzioni e uno script che consentono di usare il client Azure Information Protection e PowerShell per configurare Gestione risorse file server e Infrastruttura di classificazione file (FCI, File Classification Infrastructure).

Questa soluzione consente di proteggere automaticamente tutti i file contenuti in una cartella di un file server che esegue Windows Server o proteggere automaticamente i file che soddisfano criteri specifici. File, ad esempio, che sono stati classificati come contenenti informazioni riservate o personali. Questa soluzione si connette direttamente al servizio Azure Rights Management di Azure Information Protection per proteggere i file, quindi è necessario che questo servizio sia distribuito nell'organizzazione.

> [!NOTE]
> Anche se Azure Information Protection include un [connettore](../deploy-use/deploy-rms-connector.md) che supporta Infrastruttura di classificazione file, questa soluzione supporta solo la protezione nativa, ad esempio per i file di Office.
> 
> Per supportare più tipi di file con Infrastruttura di classificazione file di Windows Server, è necessario usare il modulo di PowerShell **AzureInformationProtection**, come descritto in questo articolo. I cmdlet di Azure Information Protection, come il client Azure Information Protection, supportano la protezione generica oltre che quella nativa, per cui è possibile proteggere tipi di file diversi dai documenti di Office. Per altre informazioni, vedere [Tipi di file supportati dal client Azure Information Protection](client-admin-guide-file-types.md) nella Guida dell'amministratore del client Azure Information Protection.

Le istruzioni qui di seguito sono per Windows Server 2012 R2 o Windows Server 2012. Se si eseguono altre versioni supportate di Windows, potrebbe essere necessario adattare alcuni di questi passaggi a causa delle differenze tra la versione del proprio sistema operativo e quello descritto in questo articolo.

## <a name="prerequisites-for-azure-rights-management-protection-with-windows-server-fci"></a>Prerequisiti per la protezione Azure Rights Management con FCI per Windows Server
Prerequisiti per queste istruzioni:

-  Su ogni file server su cui si esegue Gestione risorse file con l'infrastruttura di classificazione file:
    
    - Gestione risorse file è stato installato come uno dei servizi ruolo per il ruolo Servizi file.
    
    - È stata identificata una cartella locale che contiene file da proteggere con Rights Management. Ad esempio, C:\FileShare.
    
    - È stato installato il modulo di PowerShell AzureInformationProtection e sono stati configurati i prerequisiti per connettere il modulo al servizio Azure Rights Management.
    
    Il modulo di PowerShell AzureInformationProtection è incluso nel client Azure Information Protection. Per le istruzioni di installazione, vedere [Come installare il client Azure Information Protection per gli utenti](client-admin-guide.md#how-to-install-the-azure-information-protection-client-for-users) nella guida dell'amministratore di Azure Information Protection. Se necessario, è possibile installare il modulo di PowerShell usando il parametro `PowerShellOnly=true`.
    
    I [prerequisiti per l'uso di questo modulo di PowerShell](client-admin-guide-powershell.md#azure-information-protection-service-and-azure-rights-management-service) includono l'attivazione del servizio Azure Rights Management, la creazione di un'entità servizio e la modifica del Registro di sistema se il tenant si trova al di fuori del Nord America. Prima di iniziare a seguire le istruzioni riportate in questo articolo, assicurarsi di avere i valori di **BposTenantId**, **AppPrincipalId** e **della chiave simmetrica** come descritto nei prerequisiti. 
    
    - Se si vuole modificare il livello predefinito di protezione (nativa o generica) per estensioni di file specifiche, si deve modificare il Registro di sistema come descritto nella sezione relativa alla [modifica del livello di protezione predefinito dei file](client-admin-guide-file-types.md#changing-the-default-protection-level-of-files) della guida dell'amministratore.
    
    - È disponibile una connessione Internet con le impostazioni del computer configurate, se necessario per un server proxy Ad esempio: `netsh winhttp import proxy source=ie`
    
- L'utente ha sincronizzato gli account utente di Active Directory locali e i relativi indirizzi di posta elettronica con Azure Active Directory oppure con Office 365. Ciò è necessario per tutti gli utenti che potrebbero avere la necessità di accedere ai file una volta protetti da FCI e dal servizio Azure Rights Management. Se non si completa questo passaggio (ad esempio, in un ambiente di test), è possibile che l'accesso degli utenti a questi file sia bloccato. Per altre informazioni su questi requisiti, vedere [Preparazione di utenti e gruppi per Azure Information Protection](../plan-design/prepare.md).
    
- Sono stati scaricati i modelli di Rights Management nel file server ed è stato identificato l'ID del modello che proteggerà i file. A tale scopo, usare il cmdlet [Get-RMSTemplate](/powershell/azureinformationprotection/vlatest/get-rmstemplate). Questo scenario non supporta i modelli di reparto. Pertanto, è necessario usare un modello non configurato per un ambito oppure la configurazione dell'ambito deve includere l'opzione di compatibilità dell'applicazione, in modo che la casella di controllo **Mostra questo modello a tutti gli utenti quando le applicazioni non supportano l'identità utente** sia selezionata.

## <a name="instructions-to-configure-file-server-resource-manager-fci-for-azure-rights-management-protection"></a>Istruzioni per configurare Infrastruttura di classificazione file di Gestione risorse file server per la protezione di Azure Rights Management
Seguire queste istruzioni per proteggere automaticamente tutti i file di una cartella usando uno script di Windows PowerShell come attività personalizzata. Eseguire questa procedura secondo l'ordine seguente:

1. Salvare lo script di PowerShell

2. Creare una proprietà di classificazione per Rights Management (RMS)

3. Creare una regola di classificazione (Classifica per RMS)

4. Configurare la pianificazione di classificazione

5. Creare un'attività personalizzata di gestione file (Proteggi file con RMS)

6. Testare la configurazione eseguendo manualmente la regola e l'attività

Al termine di queste istruzioni tutti i file della cartella selezionata saranno classificati con la proprietà personalizzata di RMS e saranno protetti da Rights Management. Per una configurazione più complessa che protegge in modo selettivo alcuni file e non altri, è possibile creare o usare una proprietà e una regola di classificazione diverse con un'attività di gestione file che protegge solo quei file.

Si tenga presente che, se si apportano modifiche al modello di Rights Management usato per Infrastruttura di classificazione file, è necessario eseguire `Get-RMSTemplate -Force` sul computer del file server per ottenere il modello aggiornato. Il modello aggiornato verrà quindi usato per proteggere i nuovi file. Se le modifiche apportate al modello sono abbastanza importanti da rendere necessaria una nuova protezione dei file nel file server, è possibile effettuare questa operazione eseguendo il cmdlet Protect-RMSFile in modo interattivo con un account dotato dei diritti di esportazione e controllo completo sui file. È inoltre necessario eseguire `Get-RMSTemplate -Force` sul computer del file server se si pubblica un nuovo modello da usare per Infrastruttura di classificazione file.

### <a name="save-the-windows-powershell-script"></a>Salvare uno script di Windows PowerShell

1.  Copiare il contenuto dello [script di Windows PowerShell](fci-script.md) per la protezione Azure RMS usando Gestione risorse file server. Incollare il contenuto dello script e il nome del file **RMS-Protect-FCI.ps1** nel proprio computer.

2.  Rivedere lo script e apportare le seguenti modifiche:
    
    - Cercare la stringa seguente e sostituirla con il proprio AppPrincipalId usato con il cmdlet [Set-RMSServerAuthentication](/powershell/azureinformationprotection/vlatest/set-rmsserverauthentication) per connettersi al servizio Azure Rights Management:

        ```
        <enter your AppPrincipalId here>
        ```
        Il seguente, ad esempio, è un tipico script:

        `[Parameter(Mandatory = $false)]`

        `[Parameter(Mandatory = $false)]             [string]$AppPrincipalId = "b5e3f76a-b5c2-4c96-a594-a0807f65bba4",`

    -   Cercare la stringa seguente e sostituirla con la propria chiave simmetrica usata con il cmdlet [Set-RMSServerAuthentication](/powershell/azureinformationprotection/vlatest/set-rmsserverauthentication) per connettersi al servizio Azure Rights Management:

        ```
        <enter your key here>
        ```
        Il seguente, ad esempio, è un tipico script:

        `[Parameter(Mandatory = $false)]`

        `[string]$SymmetricKey = "zIeMu8zNJ6U377CLtppkhkbl4gjodmYSXUVwAO5ycgA="`

    -   Cercare la stringa seguente e sostituirla con il proprio BposTenantId (ID tenant) usato con il cmdlet [Set-RMSServerAuthentication](/powershell/azureinformationprotection/vlatest/set-rmsserverauthentication) per connettersi al servizio Azure Rights Management:

        ```
        <enter your BposTenantId here>
        ```
        Il seguente, ad esempio, è un tipico script:

        `[Parameter(Mandatory = $false)]`

        `[string]$BposTenantId = "23976bc6-dcd4-4173-9d96-dad1f48efd42",`

3.  Firmare lo script. Se non si firma lo script (più sicuro), è necessario configurare Windows PowerShell sui server che lo eseguono. Eseguire, ad esempio, una sessione di Windows PowerShell con l'opzione **Esegui come amministratore** e digitare: **Set-ExecutionPolicy RemoteSigned**. Questa configurazione, tuttavia, consente l'esecuzione di tutti gli script non firmati quando vengono archiviati nel server (meno sicuri).

    Per altre informazioni sulla firma degli script di Windows PowerShell, vedere [about_Signing](https://technet.microsoft.com/library/hh847874.aspx) nella raccolta di documentazione di PowerShell.

4.  Salvare il file localmente su ogni file server che eseguirà Gestione risorse file con l'interfaccia di classificazione file. Ad esempio, salvare il file in **C:\RMS-Protection**. Se si usa un percorso o un nome di cartella diverso, scegliere un percorso e una cartella che non includono spazi. Proteggere questo file usando le autorizzazioni NTFS in modo che utenti non autorizzati non possano modificarlo.

A questo punto si è pronti per iniziare la configurazione di Gestione risorse file server.

### <a name="create-a-classification-property-for-rights-management-rms"></a>Creare una proprietà di classificazione per Rights Management (RMS)

-   In Gestione classificazioni di Gestione risorse file server creare una nuova proprietà locale:

    -   **Name**: Digitare **RMS**

    -   **Descrizione**:   Digitare **Protezione di Rights Management**

    -   **Tipo di proprietà**: selezionare **Sì/No**

    -   **Valore**: Selezionare **Sì**

È ora possibile creare una regola di classificazione che usa questa proprietà.

### <a name="create-a-classification-rule-classify-for-rms"></a>Creare una regola di classificazione (Classifica per RMS)

-   Creare una nuova regola di classificazione:

    -   Fare clic sulla scheda **Generale** :

        -   **Name**: Digitare **Classifica per RMS**

        -   **Enabled**: Mantenere il valore predefinito,cioè quello selezionato in questa casella di controllo.

        -   **Descrizione**: digitare **Classifica tutti i file nella cartella &lt;nome cartella&gt; per Rights Management**.

            Sostituire *&lt;nome cartella&gt;* con il nome della cartella scelta. Ad esempio, **Classifica tutti i file nella cartella C:\FileShare per Rights Management**

        -   **Ambito**: Aggiungere la cartella scelta. Ad esempio, **C:\FileShare**.

            Non selezionare le caselle di controllo.

    -   Nella scheda **Classificazione** :

    -   **Metodo di classificazione**: Selezionare **Utilità di classificazione cartelle**

    -   **Proprietà** : Selezionare **RMS**

    -   **Valore**proprietà: Selezionare **Sì**

Nonostante sia possibile eseguire manualmente le regole di classificazione per le operazioni in corso, si vuole che questa regola venga eseguita in una pianificazione in modo tale che i nuovi file vengano classificati con la proprietà RMS.

### <a name="configure-the-classification-schedule"></a>Configurare la pianificazione di classificazione

-   Nella scheda **Classificazione automatica** :

    -   **Abilita pianificazione fissa**: Selezionare questa casella di controllo.

    -   Configurare la pianificazione per tutte le regole di classificazione da eseguire, che includono la nuova regola per classificare file con la proprietà RMS.

    -   **Consenti classificazione continua per i nuovi file**: selezionare questa casella di controllo per fare in modo che i nuovi file vengano classificati.

    -   Facoltativa: Apportare eventuali altre modifiche, come la configurazione di opzioni per report e notifiche.

Quando si è completata la configurazione per la classificazione, si è pronti per la configurazione di un'attività di gestione per applicare la protezione RMS ai file.

### <a name="create-a-custom-file-management-task-protect-files-with-rms"></a>Creare un'attività personalizzata di gestione file (Proteggi file con RMS)

-   In **Attività di gestione file**creare una nuova attività di gestione file:

    -   Fare clic sulla scheda **Generale** :

        -   **Nome attività**: Digitare **Proteggi file con RMS**

        -   Mantenere selezionata la casella di controllo **Abilita** .

        -   **Descrizione**: Digitare **Proteggi i file in &lt;nome cartella&gt; con Rights Management e un modello usando uno script di Windows PowerShell.**

            Sostituire *&lt;nome cartella&gt;* con il nome della cartella scelta. Digitare, ad esempio, **Proteggi i file in C:\FileShare con Rights Management e un modello usando uno script di Windows PowerShell**

        -   **Ambito**: Selezionare la cartella scelta. Ad esempio, **C:\FileShare**.

            Non selezionare le caselle di controllo.

    -   Nella scheda **Azione** :

        -   **Type**: Selezionare **Personalizzata**

        -   **Eseguibile**: Specificare quanto segue:

            ```
            C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe
            ```
            Se Windows non è disponibile sull'unità C:, modificare questo percorso o selezionare questo file.

        -   **Argomento**: Specificare quanto segue immettendo i propri valori per &lt;percorso&gt; e &lt;ID modello&gt;:

            ```
            -Noprofile -Command "<path>\RMS-Protect-FCI.ps1 -File '[Source File Path]' -TemplateID <template GUID> -OwnerMail [Source File Owner Email]"
            ```
            Se, ad esempio, si copia lo script in C:\RMS-Protection e l'ID modello identificato dai prerequisiti è e6ee2481-26b9-45e5-b34a-f744eacd53b0, specificare quanto segue:

            `-Noprofile -Command "C:\RMS-Protection\RMS-Protect-FCI.ps1 -File '[Source File Path]' -TemplateID e6ee2481-26b9-45e5-b34a-f744eacd53b0 -OwnerMail [Source File Owner Email]"`

            In questo comando **[Percorso file di origine]** e **[Indirizzo posta elettronica proprietario file di origine]** sono entrambe variabili specifiche dell'infrastruttura di classificazione dei file, per cui digitarle nel comando riportato sopra esattamente così come sono visualizzate. La prima viene usata dall'infrastruttura di classificazione file per specificare in modo automatico il file identificato della cartella e la seconda è per l'infrastruttura di classificazione file per richiamare automaticamente l'indirizzo di posta elettronica del proprietario del file identificato. Questo comando viene ripetuto per ogni file della cartella, che nel nostro esempio è ogni file della cartella C:\FileShare che inoltre ha RMS come proprietà di classificazione file.

            > [!NOTE]
            > Il valore del parametro **-OwnerMail [Indirizzo posta elettronica proprietario file di origine]** garantisce che il proprietario originale del file disponga dei diritti Rights Management del file dopo che quest'ultimo è stato protetto. Questo assicura che il proprietario del file originale disponga di tutti i diritti Rights Management per i propri file. Quando i file vengono creati da un utente di dominio, l'indirizzo di posta elettronica viene recuperato automaticamente da Active Directory utilizzando il nome dell'account utente nella proprietà Proprietario del file. Per effettuare questa operazione, il file server deve essere nello stesso dominio o dominio trusted dell’utente.
            > 
            > Quando possibile, assegnare i proprietari originali ai documenti protetti per assicurare che questi utenti continuino ad avere il pieno controllo dei file creati. Tuttavia, se si utilizza la variabile [Indirizzo posta elettronica proprietario file di origine] come indicato sopra e un file non dispone di un utente di dominio definito come proprietario (ad esempio, un account locale è stato utilizzato per creare il file, quindi il proprietario visualizza SYSTEM), lo script non verrà eseguito.
            > 
            > Per i file che non hanno un utente di dominio come proprietario, è possibile copiare e salvare questi file come utente di dominio in modo da diventare il proprietario solo di questi file. In alternativa, se si dispone di autorizzazioni, è possibile modificare manualmente il proprietario.  O, in alternativa, è possibile fornire un indirizzo di posta elettronica specifico (come indirizzo personale o di gruppo per il reparto IT) anziché la variabile [Indirizzo posta elettronica proprietario file di origine], il che significa che tutti i file protetti con questo script utilizzeranno questo indirizzo di posta elettronica per definire il nuovo proprietario.

    -   **Esegui il comando come**: Selezionare **Sistema locale**

    -   Nella scheda **Condizione** :

        -   **Proprietà**: Selezionare **RMS**

        -   **Operatore**: Selezionare **Uguale**

        -   **Valore**: Selezionare **Sì**

    -   Nella scheda **Pianificazione** :

        -   **Esegui alle**: Configurare la pianificazione preferita.

            Attendere il completamento dello script. Nonostante questa soluzione protegga tutti i file della cartella, lo script viene eseguito una volta per file ogni volta. Sebbene questa operazione richieda più tempo della protezione contemporanea di tutti i file, supportata dal client Azure Information Protection, questa configurazione file per file per l'infrastruttura di classificazione file è molto più efficace. Ad esempio, i file protetti possono avere proprietari diversi (mantenere il proprietario originale) quando si usa la variabile [Source File Owner Email] e questa azione file per file sarà obbligatoria se si modifica in seguito la configurazione per proteggere solo i file selezionati anziché tutti i file della cartella.

        -   **Esegui in modo continuo sui nuovi file**: Selezionare questa casella di controllo.

### <a name="test-the-configuration-by-manually-running-the-rule-and-task"></a>Testare la configurazione eseguendo manualmente la regola e l'attività

1.  Eseguire la regola di classificazione:

    1.  Fare clic su **Regole di classificazione** &gt; **Esegui classificazione con tutte le regole**.

    2.  Fare clic su **Attendi il completamento della classificazione**e quindi fare clic su **OK**.

2.  Attendere la chiusura della finestra di dialogo **Esecuzione classificazione** e visualizzare i risultati del report visualizzato automaticamente. Verrà visualizzato **1** per il campo **Proprietà** e il numero di file della cartella. Confermare usando Esplora file e selezionando le proprietà dei file nella cartella selezionata. Nella scheda **Classificazione** verrà visualizzato **RMS** come nome proprietà e **Sì** per il **Valore**.

3.  Eseguire l'attività di gestione file:

    1.  Fare clic su **Attività di gestione file** &gt; **Proteggi file con RMS** &gt; **Esegui attività di gestione file**.

    2.  Fare clic su **Attendi il completamento dell'attività**e quindi fare clic su **OK**.

4.  Attendere la chiusura della finestra di dialogo **Esecuzione attività di gestione file** e visualizzare i risultati del report visualizzato automaticamente. Verrà visualizzato il numero di file contenuti nella cartella selezionata nel campo **File** . Confermare che i file della cartella selezionata sono ora protetti con Rights Management. Ad esempio, se la cartella selezionata è C:\FileShare, digitare quanto segue in una sessione di Windows PowerShell e confermare che non sono presenti file con stato **Non protetto**:

    ```
    foreach ($file in (Get-ChildItem -Path C:\FileShare -Force | where {!$_.PSIsContainer})) {Get-RMSFileStatus -f $file.PSPath}
    ```
    > [!TIP]
    > Alcuni suggerimenti per la risoluzione dei problemi:
    > 
    > -   Se viene visualizzato **0** nel report, invece del numero di file della cartella, questo valore indicherà che lo script non è stato eseguito. Prima di tutto, verificare lo script caricandolo in Windows PowerShell ISE per convalidare il contenuto dello script e cercare di eseguirlo per vedere se sono visualizzati errori. Se non è specificato alcun argomento, lo script tenta di connettersi e di eseguire l'autenticazione per il servizio Azure Rights Management.
    > 
    >     -   Se lo script non riesce a connettersi al servizio Azure Rights Management (Azure RMS), verificare i valori visualizzati per l'account dell'entità servizio specificato nello script. Per altre informazioni su come creare l'account dell'entità servizio, vedere [Prerequisito 3: per proteggere i file o rimuoverne la protezione senza interazione da parte dell'utente](client-admin-guide-powershell.md#prerequisite-3-to-protect-or-unprotect-files-without-user-interaction) nella Guida dell'amministrazione del client Azure Information Protection.
    >     -   Se lo script segnala che è riuscito a connettersi ad Azure RMS, verificare che possa trovare il modello specificato eseguendo [Get-RMSTemplate](/powershell/azureinformationprotection/vlatest/get-rmstemplate) direttamente da Windows PowerShell nel server. Verrà visualizzato il modello specificato nei risultati restituiti.
    > -   Se lo script da solo viene eseguito in Windows PowerShell ISE senza errori, cercare di eseguirlo come indicato da una sessione PowerShell, specificando il nome file da proteggere e senza il parametro -OwnerEmail:
    > 
    >     ```
    >     powershell.exe -Noprofile -Command "<path>\RMS-Protect-FCI.ps1 -File '<full path and name of a file>' -TemplateID <template GUID>"
    >     ```
    >     -   Se lo script viene eseguito correttamente in questa sessione di Windows PowerShell, verificare le voci relative a **Executive** e **Argomento** nell'azione per le attività di gestione file.  Se si è specificato **-OwnerEmail [Indirizzo posta elettronica proprietario file di origine]**, provare a rimuovere questo parametro.
    > 
    >         Se l'attività di gestione dei file funziona correttamente senza **-OwnerEmail [Indirizzo posta elettronica proprietario file di origine]**, verificare che i file non protetti abbiano un utente di dominio elencato come proprietario del file, piuttosto che **SYSTEM**.  Per effettuare questa operazione, usare la scheda **Sicurezza** per le proprietà del file, quindi fare clic su **Avanzate**. Il valore **proprietario** visualizzato immediatamente dopo il **nome** del file. Inoltre, verificare che il file server si trova nello stesso dominio o in un dominio trusted per ricercare l'indirizzo di posta elettronica dell'utente dai servizi di dominio Active Directory.
    > -   Se si visualizza il numero corretto di file nel report, ma i file non sono protetti, provare a proteggerli manualmente usando il cmdlet [Protect-RMSFile](/powershell/azureinformationprotection/vlatest/protect-rmsfile) per vedere se sono visualizzati eventuali errori.

Dopo aver verificato che queste operazioni vengono eseguite correttamente, è possibile chiudere Gestione risorse file. I file nuovi vengono classificati e protetti automaticamente quando vengono eseguite le attività pianificate. 

## <a name="modifying-the-instructions-to-selectively-protect-files"></a>Modifica delle istruzioni per proteggere i file in modo selettivo
Quando le istruzioni appena descritte risultano efficaci, è molto semplice modificarle per ottenere una configurazione più avanzata. Ad esempio, proteggere i file usando lo stesso script ma solo per i file che contengono informazioni personali e magari selezionare un modello che ha diritti più restrittivi.

A tale scopo, usare una delle proprietà di classificazione predefinite (ad esempio, **Informazioni personali**) o creare una nuova proprietà personale. Creare quindi una nuova regola che usi questa proprietà. Ad esempio, si potrebbe selezionare **Classificazione contenuto**, scegliere la proprietà **Informazioni personali** con un valore **Alto**e configurare la stringa o il modello di espressione che identifica il file da configurare per questa proprietà (ad esempio la stringa "**Data di nascita**").

A questo punto è sufficiente creare una nuova attività di gestione file che usa lo stesso script ma forse con un modello diverso e configurare la condizione per la proprietà di classificazione appena configurata. Ad esempio, invece della condizione configurata in precedenza (la proprietà**RMS** , **Uguale**, **Sì**), selezionare la proprietà **Informazioni personali** con il valore **Operatore** impostato su **Uguale** e il **Valore** **Alto**.

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
