---
title: Scenario AIP - Proteggere i file in una condivisione di file server
description: "Questo scenario e la documentazione di supporto per l&quot;utente usano la tecnologia di protezione Azure Rights Management per proteggere tutti i file desiderati in un file server e garantire così che solo i dipendenti dell&quot;organizzazione possano accedervi, anche se vengono copiati e salvati in un archivio fuori dal controllo del reparto IT o inviati tramite posta elettronica ad altri utenti."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/23/2017
ms.topic: get-started-article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 283c7db3-5730-439e-a215-40a1088ed506
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 2131f40b51f34de7637c242909f10952b1fa7d9f
ms.openlocfilehash: e9cd548d2f2335753349d6a0248c81c0d76c6c97
ms.lasthandoff: 02/24/2017


---

# <a name="scenario---protect-files-on-a-file-server-share"></a>Scenario - Proteggere i file in una condivisione di file server

>*Si applica a: Azure Information Protection, Office 365*

Questo scenario e la documentazione di supporto per l'utente usano la tecnologia Azure Rights Management di Azure Information Protection per proteggere tutti i file desiderati in un file server e garantire così che solo i dipendenti dell'organizzazione possano accedervi, anche se vengono copiati e salvati in un archivio fuori dal controllo del reparto IT o inviati tramite posta elettronica ad altri utenti.

Queste istruzioni usano uno dei modelli predefiniti, che limita l'accesso a tutti i dipendenti con tutti i diritti di utilizzo. Tuttavia, se necessario, è possibile limitare i diritti di accesso e utilizzo tramite la configurazione di un modello personalizzato al posto di un modello predefinito.

Le istruzioni sono adatte ai casi seguenti:

-   È necessario proteggere tutti i tipi di file e non solo i file di Office. I file che non possono essere protetti in modo nativo da Azure RMS verranno protetti in modo generico.

-   Tutti i file nel percorso specificato (incluse le sottocartelle) saranno protetti.

-   Su tutti i file la protezione viene riapplicata in base a una pianificazione per garantire che le modifiche ai modelli dei criteri dei diritti vengano applicate ai file protetti.

## <a name="deployment-instructions"></a>Istruzioni sulla distribuzione
![Istruzioni per l'amministratore per la distribuzione rapida di Azure RMS](../media/AzRMS_AdminBanner.png)

Verificare che siano soddisfatti i requisiti seguenti e quindi seguire le istruzioni per le procedure di supporto prima di passare alla documentazione dell'utente.

## <a name="requirements-for-this-scenario"></a>Requisiti per questo scenario
Per le istruzioni di funzionamento di questo scenario, sono necessari i requisiti seguenti:

|Requisito|Altre informazioni|
|---------------|--------------------------------|
|Azure Rights Management non è attivato|[Attivazione di Azure Rights Management](../deploy-use/activate-service.md)|
|Si sono sincronizzati gli account utente di Active Directory locali con Azure Active Directory oppure Office 365, compreso il relativo indirizzo di posta elettronica. Ciò è necessario per tutti gli utenti che potrebbero avere la necessità di accedere ai file una volta protetti con FCI e Azure Rights Management.|[Preparazione per Azure Information Protection](../plan-design/prepare.md)|
|Uno dei seguenti:<br /><br />- Per usare un modello predefinito per tutti gli utenti: non è stato archiviato il modello predefinito, &lt;nome organizzazione&gt; - Riservato<br /><br />- Per usare un modello personalizzato per utenti specifici: il modello personalizzato è stato creato e pubblicato|[Configurazione di modelli personalizzati per il servizio Azure Rights Management](../deploy-use/configure-custom-templates.md)|
|L'applicazione Rights Management sharing viene distribuita nei computer degli utenti che eseguono Windows|[Distribuzione automatica dell'applicazione Microsoft Rights Management sharing](../rms-client/sharing-app-admin-guide.md#automatic-deployment-for-the-microsoft-rights-management-sharing-application)|
|È stato scaricato lo strumento di protezione RMS e i prerequisiti per Azure RMS sono stati configurati|Per le istruzioni sul download dello strumento e sui prerequisiti: [Cmdlet di protezione RMS](https://msdn.microsoft.com/library/mt433195.aspx)<br /><br />Per configurare altri prerequisiti per Azure RMS, ad esempio l'account dell'entità servizio: [about_RMSProtection_AzureRMS](https://msdn.microsoft.com/library/mt433202.aspx)|

### <a name="configuring-a-file-server-to-protect-all-files-by-using-azure-rms-and-file-server-resource-manager-with-file-classification-infrastructure"></a>Configurazione di un file server per proteggere tutti i file tramite Azure RMS e Gestione risorse file server con Infrastruttura di classificazione file

1.  Avviare una sessione di Windows PowerShell. Non è necessario eseguire questa sessione come amministratore.

2.  Autenticarsi in Azure RMS:

    ```
    Set-RMSServerAuthentication
    ```
    Quando richiesto, fornire i valori per l'account dell'entità servizio che è stato creato come prerequisito per i cmdlet di protezione di RMS.

3.  Eseguire il comando seguente per identificare l'ID del modello che verrà usato per proteggere i file:

    ```
    Get-RMSTemplate
    ```
    Per usare il modello predefinito che limita l'accesso a tutti i dipendenti con tutti i diritti d'uso, cercare il nome del modello di **&lt;nome organizzazione&gt; - Riservato**. Ad esempio, **VanArsdel, Ltd - Riservato**.

4.  Seguire la procedura dettagliata in [Protezione RMS con l'infrastruttura di classificazione file (FCI, File Classification Infrastructure) per Windows Server](../rms-client/configure-fci.md).

    Queste istruzioni includono uno script di Windows PowerShell specificato per l'esecuzione come eseguibile personalizzato in Gestione risorse file server. Le istruzioni includono anche le procedure per verificare che i file siano protetti da Azure Rights Management.

## <a name="user-documentation-instructions"></a>Istruzioni sulla documentazione per l'utente
Se i file che si desidera proteggere sono solo file di Office, non è necessario fornire agli utenti le istruzioni relative ai file protetti. Quando gli utenti autorizzati aprono i documenti, si aprono normalmente in Office, con la sola differenza che potrebbe essere richiesto di eseguire l'autenticazione e gli utenti probabilmente visualizzeranno una barra di informazioni nella parte superiore del documento che comunica che il documento è protetto.

Se i file protetti dispongono di un file con estensione del nome **ppdf** o sono file di testo o immagine protetto (ad esempio, hanno estensione del nome **ptxt** o.**pjpg**), questi file sono di sola lettura e non possono essere modificati. Gli utenti possono visualizzarli tramite il visualizzatore dell'applicazione RMS sharing, che si carica automaticamente per questi tipi di file. Questi file sono protetti in modo nativo da Azure RMS e si applicano tutte le impostazioni dei criteri del modello applicato, fatta eccezione per i diritti di utilizzo, poiché il file è di sola lettura. A meno che non si sappia che la protezione verrà estesa anche a questi tipi di file, è improbabile che si necessitino istruzioni per l'utente per questo scenario. Avvisare tuttavia il supporto tecnico poiché potrebbe essere necessario spiegare agli utenti il motivo per cui non è possibile modificare questi file.

Se i file protetti dispongono di un file con estensione del nome **pfile**, gli utenti possono visualizzare questi file, ma dopo averli salvati con il nome originale del file (rimuovere l'estensione pfile) qualora gli utenti desiderano modificare e salvare le modifiche. Questi file vengono generalmente protetti da Azure RMS e non possono applicare i diritti di utilizzo dal modello applicato, ovvero la protezione è annullata se il file viene salvato con un nuovo nome. Per questo scenario sono necessarie istruzioni per gli utenti.

Tramite il modello seguente, copiare e incollare le istruzioni per gli utenti finali in modo che sappiano come modificare i file protetti in modo generico. Apportare queste modifiche in base all'ambiente:

-   Sostituire *&lt;tipo di file&gt;* e *&lt;condivisione di file server&gt;* con il tipo di file che verrà protetto in modo generico e il nome della condivisione di file server.

-   Sostituire *&lt;nome organizzazione&gt;* con il nome dell'organizzazione visualizzato nei modelli predefiniti di Azure Rights Management.

-   Sostituire *&lt;nome organizzazione&gt;* con il nome dell'organizzazione.

-   Sostituire *&lt;Istruzioni per salvare il file e rimuovere l'estensione pfile&gt;* con le istruzioni specifiche dell'applicazione per questo tipo di file.

-   Sostituire i dettagli di contatto con istruzioni su come gli utenti possono contattare il supporto tecnico, ad esempio un collegamento di sito Web, indirizzo di posta elettronica o numero di telefono.

-   Apportare eventuali modifiche aggiuntive a questo set di istruzioni e quindi inviarlo agli utenti.

La documentazione di esempio mostra come questo set di istruzioni appare agli utenti dopo le personalizzazioni.

![Documentazione dell'utente del modello per la distribuzione rapida di Azure RMS](../media/AzRMS_UsersBanner.png)

### <a name="how-to-edit-lttype-of-filegt-from-the-ltfile-server-sharegt"></a>Come modificare il &lt;tipo di file&gt; dalla &lt;condivisione di file server&gt;

1.  Fare doppio clic sul file per aprirlo. È possibile che vengano richieste le credenziali.

2.  Viene visualizzata una finestra di dialogo del **file protetto** dell'applicazione Microsoft Rights Management sharing, che indica che è necessario rispettare le autorizzazioni per **&lt;nome organizzazione&gt; - Riservato**. Per questa ragione, non condividere questo documento con altri utenti che non lavorano per &lt;nome organizzazione&gt;.

3.  Fare clic su **Apri**.

4.  Per modificare il file, salvare innanzitutto il file e rimuovere l'estensione del nome pfile:

    -   &lt;Istruzioni per salvare il file e rimuovere l'estensione pfile&gt;

5.  È ora possibile modificare e salvare il file normalmente.

Periodicamente, il file sarà protetto nuovamente per aggiungere l'estensione del nome file pfile e sarà necessario ripetere questi passaggi.

**Serve assistenza?**

-   Per informazioni aggiuntive:

    -   [Visualizzare e usare i file che sono stati protetti](../rms-client/sharing-app-view-use-files.md)

-   Contattare il supporto tecnico:

    -   *&lt;dettagli contatto&gt;*

### <a name="example-customized-user-documentation"></a>Esempio di documentazione personalizzata per l'utente
![Esempio di documentazione dell'utente per la distribuzione rapida di Azure RMS](../media/AzRMS_ExampleBanner.png)

#### <a name="how-to-edit-cad-drawings-from-the-projectnextgen-share"></a>Come modificare disegni CAD dalla condivisione ProjectNextGen

1.  Fare doppio clic sul file per aprirlo. È possibile che vengano richieste le credenziali.

2.  Viene visualizzata una finestra di dialogo del **file protetto** dell'applicazione Microsoft Rights Management sharing, che indica che è necessario rispettare le autorizzazioni per **VanArsdel, Ltd - Riservato**. In questo modo, questo documento non viene condiviso con altri utenti che non lavorano per VanArsdel, Ltd.

3.  Fare clic su **Apri**.

4.  Per modificare il file, salvare innanzitutto il file e rimuovere l'estensione del nome pfile:

    -   **File** &gt; **Salva con nome**

    -   Eliminare il suffisso **pfile** dalla fine del nome del file e fare clic su **OK**.

5.  È ora possibile modificare e salvare il file normalmente.

Periodicamente, il file sarà protetto nuovamente per aggiungere l'estensione del nome file pfile e sarà necessario ripetere questi passaggi.

**Serve assistenza?**

-   Per informazioni aggiuntive:

    -   [Visualizzare e usare i file che sono stati protetti](../rms-client/sharing-app-view-use-files.md)

-   Contattare il supporto tecnico: helpdesk@vanarsdelltd.com

[!INCLUDE[Commenting house rules](../includes/houserules.md)]

