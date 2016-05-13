---
# required metadata

title: Creare, configurare e pubblicare un modello personalizzato | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: d6e9aa0c-1694-4a53-8898-4939f31cc13f

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---


# Creare, configurare e pubblicare un modello personalizzato

Il portale di Azure classico consente di creare e gestire modelli personalizzati. È possibile eseguire questa operazione direttamente nel portale di Azure classico oppure accedendo all'interfaccia di amministrazione di Office 365 e scegliendo le **funzionalità avanzate** di Rights Management, che a loro volta reindirizzano al portale di Azure classico.

Per creare, configurare e pubblicare modelli personalizzati per Rights Management, seguire queste procedure.

## Per creare un modello personalizzato

1.  Seguire una di queste due procedure in base al tipo di accesso scelto, dall'interfaccia di amministrazione di Office 365 o dal portale di Azure classico:

    -   Dall'[interfaccia di amministrazione di Office 365](https://portal.office.com/):

        1.  Nel riquadro a sinistra, fare clic su **impostazioni servizio**.

        2.  Nella pagina **impostazioni servizio** fare clic su **rights management**.

        3.  Nella sezione **Proteggere le informazioni** fare clic su **Gestione**.

        4.  Nella sezione **rights management** fare clic su **funzionalità avanzate**.

            > [!NOTE]
            > Se Rights Management non è stato attivato, fare prima clic su **attiva** e confermare l'azione. Per altre informazioni, vedere [Attivazione di Azure Rights Management](activate-service.md).
            > 
            > Se l'opzione **funzionalità avanzate** non è mai stata selezionata prima, dopo aver attivato Rights Management seguire le istruzioni visualizzate per ottenere una sottoscrizione di Azure gratuita necessaria per accedere al portale di Azure classico.

            Facendo clic su **funzionalità avanzate** viene caricato il portale di Azure classico, in cui è possibile gestire il servizio **RIGHTS MANAGEMENT** relativo ad Azure Active Directory dell'organizzazione.

    -   Dal [portale di Azure classico](http://go.microsoft.com/fwlink/p/?LinkID=275081):

        1.  Nel riquadro sinistro fare clic su **ACTIVE DIRECTORY**.

        2.  Nella pagina **active directory** fare clic su **RIGHTS MANAGEMENT**.

        3.  Selezionare la directory da gestire per Rights Management.

        4.  Se Rights Management non è stato ancora attivato, fare clic su **ATTIVA** e confermare l'azione.

            > [!NOTE]
            > Per altre informazioni, vedere [Attivazione di Azure Rights Management](activate-service.md).

2.  Creare un nuovo modello:

    -   Nella pagina di avvio rapido **Introduzione a Rights Management** del portale di Azure classico fare clic su **Creare un nuovo modello di criteri di diritti**.

        Se questa pagina non viene visualizzata immediatamente dopo aver seguito le istruzioni per Office 365, è possibile usare le istruzioni di navigazione precedenti relative al portale di Azure classico.

3.  Nella pagina **Aggiungi un nuovo modello di criteri di diritti** selezionare la lingua in cui si intende specificare il nome e la descrizione del modello che saranno visibili agli utenti (più avanti si potranno aggiungere altre lingue). Digitare quindi un nome univoco e una descrizione e fare clic sul pulsante Completa.

Nella pagina di avvio rapido **Introduzione a Rights Management** fare clic su **Gestire i modelli di criteri di diritti**. Il modello appena creato sarà visualizzato nell'elenco dei modelli con lo stato **Archiviato**. A questo punto il modello è stato creato, ma non è configurato e non è visibile agli utenti.

## Per configurare e pubblicare un modello personalizzato

1.  Selezionare il modello appena creato nella pagina **MODELLI** del portale di Azure classico.

2.  Nella pagina di avvio rapido **Il modello è stato aggiunto** fare clic su **Introduzione** nel passaggio 1, **Configurare diritti di utenti e gruppi** , quindi fare clic su **PER INIZIARE** o **AGGIUNGI**e infine selezionare gli utenti e i gruppi che avranno i diritti per usare il contenuto protetto tramite il nuovo modello.

    > [!NOTE]
    > Gli utenti o i gruppi selezionati devono disporre di un indirizzo di posta elettronica. Questa condizione si verifica quasi sempre in un ambiente di produzione, ma in un ambiente di test semplice può essere necessario aggiungere gli indirizzi di posta elettronica agli account utente o ai gruppi.

    Come procedura consigliata, usare gruppi anziché utenti singoli perché la gestione dei modelli risulterà più agevole. Se si dispone di Active Directory locale e si esegue la sincronizzazione in Azure AD, è possibile utilizzare i gruppi abilitati alla posta che sono gruppi di protezione o gruppi di distribuzione. Se tuttavia si desidera concedere diritti a tutti gli utenti dell'organizzazione, la procedura più efficiente consiste nel copiare uno dei modelli predefiniti piuttosto che specificare più gruppi. Per altre informazioni, vedere l'articolo relativo alla [modalità per copiare un modello](copy-template.md).

    > [!TIP]
    > È quindi possibile aggiungere al modello utenti esterni all'organizzazione usando il [modulo Windows PowerShell per Azure Rights Management](install-powershell.md) e usando uno dei metodi seguenti:
    > 
    > -   **Usare un oggetto di definizione dei diritti per aggiornare un modello**: specificare gli indirizzi di posta elettronica esterni e i relativi diritti in un oggetto di definizione dei diritti, che verrà quindi usato per aggiornare il modello. È possibile specificare l'oggetto di definizione dei diritti usando il cmdlet [New-AadrmRightsDefinition](https://msdn.microsoft.com/library/azure/dn727080.aspx) per creare una variabile e quindi fornire questa variabile al parametro -RightsDefinition con il cmdlet [Set-AadrmTemplateProperty](https://msdn.microsoft.com/library/azure/dn727076.aspx) per modificare un modello esistente. Tuttavia, se si stanno aggiungendo questi utenti a un modello esistente, sarà necessario definire anche gli oggetti di definizione dei diritti per i gruppi esistenti nei modelli e non solo i nuovi utenti esterni.
    > -   **Esportare, modificare e importare il modello aggiornato**: usare il cmdlet [Export-AadrmTemplate](https://msdn.microsoft.com/library/azure/dn727078.aspx) per esportare il modello in un file che è possibile modificare in modo da aggiungere gli indirizzi di posta elettronica esterni degli utenti e i relativi diritti rispetto a gruppi e diritti esistenti. Usare quindi il cmdlet [Import-AadrmTemplate](https://msdn.microsoft.com/library/azure/dn727077.aspx) per importare di nuovo le modifiche in Azure RMS.

3.  Fare clic sul pulsante Avanti, quindi assegnare agli utenti e ai gruppi selezionati uno dei diritti elencati.

    Per altre informazioni su ogni diritto (e per i diritti personalizzati), usare la descrizione visualizzata. Informazioni più dettagliate sono inoltre disponibili nell'articolo relativo alla [configurazione dei diritti di utilizzo per Azure Rights Management](configure-usage-rights.md). Tuttavia, le applicazioni che supportano RMS possono implementare questi diritti in modo diverso. Consultare la relativa documentazione ed eseguire test personalizzati con le applicazioni usate dagli utenti per controllare il comportamento prima di distribuire il modello per gli utenti. Per fare in modo che il modello sia visibile solo agli amministratori per eseguirne il test, rendere questo modello un modello di reparto (passaggio 6).

4.  Se si seleziona **Personalizzato**, fare clic sul pulsante Avanti e quindi selezionare i diritti personalizzati.

    Benché sia possibile usare qualsiasi combinazione dei singoli diritti disponibili, in alcune applicazioni determinati diritti possono dipendere da altri diritti. In questo caso, i diritti dipendenti vengono selezionati automaticamente.

    > [!TIP]
    > Valutare l'opportunità di aggiungere il diritto **Copia ed estrai contenuto** e concedere questo diritto al personale o agli amministratori selezionati in altri ruoli responsabili del recupero di informazioni. Gli utenti con questo diritto possono rimuovere, se necessario, la protezione da file e messaggi di posta elettronica che verranno protetti mediante questo modello. La possibilità di rimuovere la protezione a livello del modello consente un controllo più accurato rispetto all'uso della funzionalità dell'utente con privilegi avanzati.

5.  Fare clic sul pulsante Completa.

6.  Se si vuole che il modello sia visibile solo a un subset di utenti quando viene visualizzato un elenco di modelli nelle applicazioni, fare clic su **AMBITO** per configurare questo modello come modello di reparto e fare clic su **PER INIZIARE**. In caso contrario, andare al passaggio 9.

    Altre informazioni sui modelli di reparto: per impostazione predefinita, tutti gli utenti nella directory di Azure visualizzano tutti i modelli pubblicati e possono quindi selezionarli dalle applicazioni quando vogliono proteggere il contenuto. Se si vuole consentire solo ad alcuni utenti specifici di visualizzare alcuni dei modelli pubblicati, è necessario definire l'ambito dei modelli per tali utenti. Quindi, solo tali utenti potranno selezionare questi modelli. Gli altri utenti che non sono stati specificati non potranno visualizzare i modelli e pertanto non potranno selezionarli. Questa tecnica semplifica la scelta del modello corretto da parte degli utenti, soprattutto quando si creano modelli che sono progettati per essere usati da gruppi o reparti specifici. Gli utenti visualizzeranno solo i modelli che sono stati progettati per loro.

    Ad esempio, si è creato un modello per il reparto Risorse umane che applica l'autorizzazione di sola lettura ai membri del reparto Finanze. Affinché solo i membri del reparto Risorse umane possano applicare questo modello quando usano l'applicazione di condivisione Rights Management, assegnare l'ambito del modello al gruppo abilitato alla posta elettronica denominato HumanResources. Quindi, solo i membri di questo gruppo potranno visualizzare e applicare questo modello.

7.  Nella pagina **VISIBILITÀ DEL MODELLO** selezionare gli utenti e i gruppi che potranno visualizzare e selezionare il modello nelle applicazioni che supportano RMS. Come indicato in precedenza, è consigliabile usare i gruppi anziché gli utenti e i gruppi o gli utenti selezionati dovranno avere un indirizzo di posta elettronica.

8.  Fare clic sul pulsante Avanti e stabilire se è necessario configurare la compatibilità delle applicazioni per il modello di reparto. Per configurarla, fare clic su **COMPATIBILITÀ DELL'APPLICAZIONE**, selezionare la casella di controllo e scegliere **Completa**.

    Per quale motivo potrebbe essere necessario configurare la compatibilità delle applicazioni? Non tutte le applicazioni possono supportare i modelli di reparto. A tale scopo, per poter scaricare i modelli, è necessario eseguire prima l'autenticazione dell'applicazione con il servizio RMS. Se il processo di autenticazione non viene eseguito, per impostazione predefinita non viene scaricato alcun modello di reparto. È possibile eseguire l'override di questo comportamento specificando che tutti i modelli di reparto devono essere scaricati, configurando la compatibilità dell’applicazione e selezionando la casella di controllo **Mostra questo modello a tutti gli utenti quando le applicazioni non supportano l'identità utente** .

    Ad esempio, se non si configura la compatibilità delle applicazioni per il modello di reparto nell'esempio delle Risorse umane, solo gli utenti del reparto Risorse umane visualizzeranno il modello di reparto quando useranno l'applicazione RMS sharing, ma nessun utente visualizzerà il modello di reparto quando userà Outlook Web Access (OWA) da Exchange Server 2013 poiché OWA di Exchange ed Exchange ActiveSync non supportano i modelli di reparto. Se si esegue l'override di questo comportamento predefinito configurando la compatibilità delle applicazioni, solo gli utenti del reparto Risorse umane visualizzeranno il modello di reparto quando useranno l'applicazione RMS sharing, ma tutti gli utenti visualizzeranno il modello di reparto quando useranno Outlook Web Access (OWA). Se gli utenti usano OWA o Exchange ActiveSync da Exchange Online, i modelli di reparto saranno visibili a tutti gli utenti o a nessun utente, a seconda dello stato del modello (archivio o pubblicato) in Exchange Online.

    Office 2016 supporta in modalità nativa i modelli di reparto, analogamente a Office 2013 a partire dalla versione 15.0.4727.1000, rilasciati nel mese di giugno 2015 come parte di [KB 3054853](https://support.microsoft.com/kb/3054853).

    > [!NOTE]
    > Se si hanno applicazioni che ancora non supportano in modalità nativa i modelli di reparti, è possibile usare uno script personalizzato per il download dei modelli di RMS o altri strumenti per distribuire questi modelli nella cartella locale del client RMS. In queste applicazioni quindi i modelli di reparto potranno essere visualizzati correttamente solo dagli utenti e i gruppi selezionati per l'ambito del modello:
    > 
    > -   Per Office 2010, la cartella client è **%localappdata%\Microsoft\DRM\Templates**.
    > -   Da un computer client in cui sono stati scaricati tutti i modelli, è possibile copiare e incollare i file modello in altri computer.
    > 
    > È possibile [scaricare lo script personalizzato dei modelli di RMS dal sito Microsoft Connect](http://go.microsoft.com/fwlink/?LinkId=524506). Se viene visualizzato un errore quando si fa clic su questo collegamento, probabilmente non è ancora stata eseguita la registrazione in Microsoft Connect.   Per eseguire la registrazione:
    > 
    > 1.  Passare al [sito Microsoft Connect](http://www.connect.microsoft.com) e accedere con il proprio account Microsoft.
    > 2.  Fare clic su **Directory** e selezionare la categoria **Visualizza prodotti Connect che attualmente non accettano commenti**.
    > 3.  Cercare **Rights Management Services** e, in corrispondenza del programma **Microsoft RMS Enterprise Features**, fare clic su **Aggiungi**.

9. Fare clic su **CONFIGURA** e aggiungere le altre lingue usate dagli utenti, nonché il nome e la descrizione del modello in tali lingue. Quando sono presenti utenti multilingue, è importante aggiungere ogni lingua usata e specificare un nome e una descrizione in tale lingua. In tal modo, gli utenti vedranno il nome e la descrizione del modello nella stessa lingua del sistema operativo client di cui dispongono e questo garantisce la piena comprensione dei criteri applicati a un documento o a un messaggio di posta elettronica. In caso di mancata corrispondenza con il sistema operativo client, il nome e la descrizione verranno visualizzati nella lingua definita al momento della creazione del modello.

    Verificare quindi se si desideri apportare modifiche alle impostazioni riportate di seguito.

    |Impostazione|Altre informazioni|
    |-----------|--------------------|
    |**scadenza contenuto**|Definire una data o un numero di giorni in cui i file protetti tramite il modello non devono essere aperti. È possibile specificare una data o un numero di giorni a partire dal momento in cui la protezione viene applicata al file.<br /><br />Quando si specifica una data, diventa effettiva alla mezzanotte del fuso orario corrente.|
    |**accesso offline**|Usare questa impostazione per far fronte agli eventuali requisiti di sicurezza previsti e, allo stesso tempo, all'esigenza degli utenti di aprire i file protetti quando non dispongono di una connessione Internet.<br /><br />Se si specifica che il contenuto non è disponibile senza una connessione Internet o che è disponibile solo per un determinato numero di giorni, al raggiungimento di tale soglia, gli utenti dovranno eseguire di nuovo l'autenticazione e l'accesso verrà registrato. In questo caso, se le credenziali non sono memorizzate nella cache, verrà chiesto agli utenti di eseguire l'accesso prima di poter aprire il file.<br /><br />Oltre alla riesecuzione dell'autenticazione, verrà nuovamente valutata l'appartenenza degli utenti ai criteri e ai gruppi. Questo significa che gli utenti potrebbero avere risultati di accesso diversi per lo stesso file se dall'ultimo accesso si sono verificati cambiamenti relativi all'appartenenza ai criteri o ai gruppi.|

10. Quando si è convinti che il modello sia configurato in modo appropriato per gli utenti, fare clic su **PUBBLICA** per renderlo visibile agli utenti e quindi su **SALVA**.

11. Fare clic sul pulsante Indietro nel portale classico per tornare alla pagina **MODELLI** in cui lo stato aggiornato del modello è ora impostato su **Pubblicato**.

Per apportare modifiche al modello, selezionarlo e quindi eseguire di nuovo i passaggi di avvio rapido. In alternativa, procedere in uno dei seguenti modi:

-   Per aggiungere altri utenti e gruppi e definirne i diritti, Fare clic su **DIRITTI**e quindi su **AGGIUNGI**.

-   Per rimuovere utenti o gruppi selezionati precedentemente, fare clic su **DIRITTI**, selezionare l'utente o il gruppo dall'elenco e quindi fare clic su **ELIMINA**.

-   Per modificare gli utenti che possono visualizzare i modelli da selezionare dalle applicazioni, fare clic su **AMBITO**, quindi fare clic su **AGGIUNGI** o su **ELIMINA**o su **COMPATIBILITÀ DELL'APPLICAZIONE**.

-   Per nascondere il modello a tutti gli utenti, fare clic su **CONFIGURA**, **ARCHIVIA**e **SALVA**.

-   Per apportare altre modifiche di configurazione, fare clic su **CONFIGURA**, apportare le modifiche e fare clic su **SALVA**.

> [!WARNING]
> Quando si apportano modifiche a un modello salvato in precedenza, le modifiche non saranno visibili ai client finché i modelli non vengono aggiornati nei computer. Per altre informazioni, vedere l'articolo relativo all'[aggiornamento dei modelli per gli utenti](refresh-templates.md).

## Vedere anche
[Configurare modelli personalizzati per Azure Rights Management](configure-custom-templates.md)

<!--HONumber=Apr16_HO3-->


