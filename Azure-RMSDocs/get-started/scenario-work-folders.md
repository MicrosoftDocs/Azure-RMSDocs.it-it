---
title: Scenario - Configurare le cartelle di lavoro per una protezione permanente | Azure RMS
description: Questo scenario e la documentazione di supporto per l'utente usano Azure Rights Management per applicare la protezione permanente ai documenti di Office in Cartelle di lavoro. Cartelle di lavoro usa un servizio di ruolo per i file server che esegue Windows Server, che fornisce un metodo coerente agli utenti per accedere ai file di lavoro dal proprio PC e dai propri dispositivi. Sebbene Cartelle di lavoro fornisca la propria crittografia per proteggere i file, questa protezione viene persa se i file vengono spostati all'esterno dell'ambiente di Cartelle di lavoro.
author: cabailey
manager: mbaldwin
ms.date: 08/24/2016
ms.topic: get-started-article
ms.prod: 
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 1f189345-a69e-4bf5-8a45-eb0fe5bb542b
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 024a29d7c7db2e4c0578a95c93e22f8e7a5b173e
ms.openlocfilehash: ce61f22be934ec9817a22737417514468b5c6528


---

# Scenario - Configurare le cartelle di lavoro per una protezione permanente

>*Si applica a: Azure Rights Management, Office 365*

Questo scenario e la documentazione di supporto per l'utente usano Azure Rights Management per applicare la protezione permanente ai documenti di Office in [Cartelle di lavoro](https://technet.microsoft.com/library/dn265974.aspx). Cartelle di lavoro usa un servizio di ruolo per i file server che esegue Windows Server, che fornisce un metodo coerente agli utenti per accedere ai file di lavoro dal proprio PC e dai propri dispositivi. Sebbene Cartelle di lavoro fornisca la propria crittografia per proteggere i file, questa protezione viene persa se i file vengono spostati all'esterno dell'ambiente di Cartelle di lavoro. Ad esempio, gli utenti copiano i file sincronizzati e li salvano in un archivio fuori dal controllo del reparto IT o i file vengono inviati tramite posta elettronica ad altri utenti.

La protezione aggiuntiva che fornisce Azure Rights Management consente di evitare la perdita accidentale dei dati e impedire che i file vengano visualizzati da utenti esterni all'organizzazione. A tale scopo, è possibile usare uno dei modelli dei criteri sui diritti incorporati e predefiniti. Tuttavia, prima di distribuire questo scenario, considerare se gli utenti potrebbero dover condividere in modo legittimo uno di questi file con utenti esterni all'organizzazione. Ad esempio, dopo aver lavorato sulla bozza di un listino prezzi, un utente invia tramite messaggio di posta elettronica la versione finale al cliente di un'altra organizzazione. Quando si usa il modello di Rights Management predefinito per Cartelle di lavoro, il cliente dell'organizzazione potrebbe non essere in grado di leggere il documento inviato tramite posta elettronica. È possibile soddisfare questo requisito tramite la creazione di un modello personalizzato che consente agli utenti di applicare al file un nuovo criterio dei diritti, che sostituisce la restrizione originale di tutti i dipendenti alle persone specificate nel messaggio di posta elettronica.

> [!NOTE]
> Quando si usa il modello personalizzato indicato per questo scenario, anche se gli utenti possono condividere intenzionalmente i file con utenti che non definiti nel modello, la protezione aggiuntiva di Azure Rights Management offre numerosi vantaggi. Questa protezione aggiuntiva impedisce la perdita accidentale dei dati se il contenuto viene spostato all'esterno dei limiti di Cartelle di lavoro, poiché il contenuto rimane protetto da utenti non autorizzati, sia che sia fermo o che venga trasmesso. Ad esempio, un utente perde un dispositivo che usa Cartelle di lavoro, il dispositivo viene rubato o il contenuto sincronizzato da e verso il dispositivo viene trasferito su un'infrastruttura non protetta.
> 
> Se un utente condivide il contenuto con qualcuno in un'altra organizzazione, usando la funzionalità di condivisione protetta dell'applicazione di condivisione Rights Management, l'utente sostituisce la protezione originale con i propri criteri di protezione. Di conseguenza, il contenuto è comunque protetto da accessi non autorizzati e solo le persone specificate dall'utente possono accedere al contenuto.

È possibile applicare questa protezione permanente per tutti i documenti di Office in Cartelle di lavoro degli utenti o solo ai file che contengono dati sensibili o ad alto impatto aziendale.

Le istruzioni sono adatte ai casi seguenti:

-   I file di Cartelle di lavoro da proteggere con protezione permanente sono file di Office. Questi file possono essere protetti in modo nativo da Azure Rights Management e non modificano l'estensione del nome o richiedono un flusso di lavoro diverso per aprirli.

-   Si desidera applicare la protezione permanente a tutti i file di Office in Cartelle di lavoro degli utenti o ai file selettivi identificati tramite l'Infrastruttura di classificazione file da Gestione risorse file server in Windows Server.

-   Per i file che devono essere condivisi con utenti non specificati nel modello dei criteri dei diritti (ad esempio gli utenti di un'altra organizzazione), gli utenti devono applicare un nuovo criterio dei diritti per sostituire la protezione dei criteri dei diritti originale.

## Istruzioni sulla distribuzione
![Istruzioni per l'amministratore per la distribuzione rapida di Azure RMS](../media/AzRMS_AdminBanner.png)

Verificare che siano soddisfatti i requisiti seguenti e quindi seguire le istruzioni per le procedure di supporto prima di passare alla documentazione dell'utente.

## Requisiti per questo scenario
Per le istruzioni di funzionamento di questo scenario, sono necessari i requisiti seguenti:

|Requisito|Altre informazioni|
|---------------|--------------------------------|
|Azure Rights Management non è attivato|[Attivazione di Azure Rights Management](https://technet.microsoft.com/library/jj658941.aspx)|
|Si sono sincronizzati gli account utente di Active Directory locali con Azure Active Directory oppure Office 365, compreso il relativo indirizzo di posta elettronica. Questa operazione è necessaria per tutti gli utenti che usano Cartelle di lavoro.|[Preparazione per Azure Rights Management](https://technet.microsoft.com/library/jj585029.aspx)|
|Uno dei seguenti:<br /><br />- Per usare un modello predefinito per tutti gli utenti che non consenta di applicare nuovi criteri di diritti: non è stato archiviato il modello predefinito, **&lt;nome organizzazione&gt; - Riservato**<br /><br />- Per usare un modello personalizzato adatto all'applicazione di nuovi criteri di diritti da parte degli utenti: viene creato un modello personalizzato usando le istruzioni seguenti|[Configurazione di modelli personalizzati per Azure Rights Management](https://technet.microsoft.com/library/dn642472.aspx)|
|Il connettore Rights Management è installato, autorizzato per il computer Windows Server e configurato per il ruolo **FCI Server**.|[Distribuzione del connettore di Azure Rights Management](https://technet.microsoft.com/library/dn375964.aspx)|
|L’applicazione di condivisione Rights Management è distribuita nei computer degli utenti che eseguono Windows|[Distribuzione automatica dell'applicazione di condivisione Microsoft Rights Management](https://technet.microsoft.com/library/dn339003%28v=ws.10%29.aspx)|

### Configurazione del modello dei criteri dei diritti personalizzato in modo che gli utenti possano condividere i file di Cartelle di lavoro all'esterno dell'organizzazione

1.  Accedere al portale classico di Azure e passare ai modelli di Azure Rights Management.

2.  Copiare il modello **&lt;nome organizzazione&gt; - Riservato** e specificare un nome e una descrizione per questo scenario Cartelle di lavoro. Si consiglia quanto segue:

    -   Nome: **Contenuto protetto da Cartelle di lavoro**

    -   Descrizione: **questo contenuto è protetto da Cartelle di lavoro ed è limitato ai soli dipendenti della società. Per condividere il contenuto con utenti esterni all'organizzazione, allegare il documento a un messaggio di posta elettronica e usare la funzione Condividi file protetto.**

3.  Nella pagina **Diritti**:

    -   modificare i diritti esistenti da **Personalizzato** a **Comproprietario**.

4.  Nella pagina **Configura**:

    -   verificare che lo **Stato** sia impostato su **Pubblico**

    -   Per **nome e descrizione**, eliminare le voci per le lingue che non si usano. Per le lingue che si usano, aggiornare **Nome** e **Descrizione** in modo che corrispondono al nome e alla descrizione assegnati al modello, usando la lingua specificata.

5.  Salvare il modello.

### Configurazione di Cartelle di lavoro per applicare la protezione permanente ai file di Office

1.  Implementare Cartelle di lavoro per gli utenti in modo che i file salvati in locale vengano sincronizzate su una cartella del file server, dal nome *condivisione di sincronizzazione*. La condivisione di sincronizzazione sul file server non deve verificarsi nello stesso server che esegue il connettore Rights Management.

    Questa soluzione richiede il servizio ruolo Cartelle di lavoro in Server Manager per il ruolo Servizi file e archiviazione. Il file server deve eseguire una versione minima di Windows Server 2012 R2 e può trovarsi in locale o in una macchina virtuale su Azure. Per altre informazioni sulle Cartelle di lavoro, vedere [Panoramica di Cartelle di lavoro](https://technet.microsoft.com/library/dn265974.aspx).

    Per istruzioni sulla distribuzione, vedere [Distribuzione di Cartelle di lavoro](https://technet.microsoft.com/library/dn528861.aspx). Selezionare la crittografia incorporata (ovvero l'opzione **Crittografa Cartelle di lavoro**), che verrà applicata in aggiunta alla crittografia di Azure Rights Management. Inoltre:

    -   Quando si associa il certificato SSL nel server di sincronizzazione (passaggio 4): usare il comando netsh (anziché la console di gestione IIS) per associare il certificato all'interfaccia https del sito Web predefinito.

    -   Per evitare che gli utenti riscontrino un errore di installazione di Cartelle di lavoro **Problema con l'applicazione dei criteri di sicurezza** e il requisito di amministratore locale nei propri computer appartenenti a un dominio: usare il cmdlet [Set-SyncShare](https://technet.microsoft.com/library/dn296649%28v=wps.630%29.aspx) con il parametro PasswordAutolockExcludeDomain e specificare i nomi di dominio appartenenti a questi computer (ad esempio contoso.com).

2.  Per completare la configurazione del connettore Rights Management:

    1.  Con Gestione risorse File Server, creare un'attività di gestione di file che identifica la cartella di condivisione di sincronizzazione dell'ambito.

    2.  Per l'azione, scegliere **Crittografia RMS** e selezionare un modello:

        -   Se non è stato creato un modello personalizzato perché non si vuole che gli utenti possano condividere i file con altri utenti all'esterno dell'organizzazione, selezionare il nome del modello **&lt;nome organizzazione&gt; - Riservato**. Ad esempio, **VanArsdel, Ltd - Riservato**.

        -   Se è stato creato un modello personalizzato tramite le istruzioni precedenti, selezionare questo modello. Ad esempio **Contenuto protetto da Cartelle di lavoro**

    3.  Specificare una pianificazione che consente una notevole quantità di tempo per tutti i file di Office da crittografare con Azure Rights Management e l'opzione **Esegui in modo continuo sui nuovi file**.

3.  Per testare manualmente questa configurazione, verificare che la cartella contenga alcuni file di Office e quindi usare l'opzione **Esegui attività di gestione file** e selezionare **Attendi il completamento dell'attività**.

    Attendere la chiusura della finestra di dialogo **Esecuzione attività di gestione file** e visualizzare i risultati del report visualizzato automaticamente. Verrà visualizzato il numero di file contenuti nella cartella selezionata nel campo **File** . Confermare che i file della cartella selezionata sono ora protetti da Azure Rights Management. Ad esempio, aprire un file e verificare di visualizzare il banner informativo nella parte superiore del documento che visualizza il nome e descrizione del modello di Rights Management.

4.  Se si è deciso di proteggere in modo selettivo i file usando l'Infrastruttura di classificazione file, configurare la regola di classificazione e la pianificazione e quindi modificare l'attività di gestione del file per includere la proprietà di classificazione come condizione.

## Istruzioni sulla documentazione per l'utente
Se i file che si desidera proteggere con Azure Rights Management non devono essere condivisi con utenti esterni all'organizzazione, potrebbe non essere necessario fornire agli utenti le istruzioni aggiuntive rispetto a quelle fornite per l'uso di Cartelle di lavoro. Quando gli utenti aprono i file che sono protetti da Azure Rights Management e il modello predefinito, i file si aprono normalmente in Office, con la sola differenza che agli utenti potrebbe essere richiesto di eseguire l'autenticazione. A quel punto gli utenti visualizzeranno un banner informativo nella parte superiore del documento che informa che il contenuto include informazioni proprietarie destinate solo agli utenti interni.

Se è stato configurato il modello personalizzato come descritto in questo scenario, gli utenti visualizzeranno la descrizione del modello nel banner informativo: **Questo contenuto è protetto da Cartelle di lavoro ed è limitato ai soli dipendenti della società. Per condividere il contenuto con utenti esterni all'organizzazione, allegare il documento a un messaggio di posta elettronica e usare la funzione Condividi file protetto.** Sebbene questa descrizione fornisca un riepilogo su come condividere il file all'esterno dell'organizzazione, gli utenti avranno probabilmente necessità di istruzioni dettagliate sull'operazione, in particolare le prime volte. Per supportare questo scenario successivo, usare le istruzioni per utente finale e amministratore [Scenario - Condividere un file di Office con utenti in un'altra organizzazione](scenario-share-office-file-externally.md).

> [!TIP]
> Se si decide di non usare il modello personalizzato descritto in queste istruzioni, perché non si desidera che gli utenti condividano i file all'esterno dell'organizzazione senza supervisione del reparto IT, informare il supporto tecnico in modo che se il requisito di condivisione è legittimo, può essere risolto tramite il meccanismo più appropriato per l'azienda. Ad esempio, una persona che è [utente con privilegi avanzati](https://technet.microsoft.com/library/mt147272.aspx) può applicare un nuovo modello per il contenuto che concede diritti di controllo completo all'utente richiedente, in modo che l'utente possa usare la funzione Condividi file protetto.
> 
> Dopo un intervallo di tempo, se si scopre che esistono molte richieste di utenti, è possibile decidere di definire il proprio modello personalizzato per questo scenario che conceda solo a specifici utenti (ad esempio responsabili o supporto tecnico) l'opzione Comproprietario, mentre agli utenti standard vengono concessi diritti di Coautore o qualsiasi altro [diritto](https://technet.microsoft.com/library/mt169423.aspx) si ritenga adatto.




<!--HONumber=Aug16_HO4-->


