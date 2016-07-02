---
title: Scenario - Proteggere i file in una condivisione di file server | Azure RMS
description: 
keywords: 
author: cabailey
manager: mbaldwin
ms.date: 05/20/2016
ms.topic: get-started-article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 283c7db3-5730-439e-a215-40a1088ed506
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 332e102cb27854314b93a71bfeae82a95c9a7812
ms.openlocfilehash: c16098a2d0fe41748280704716a2eeef8921a6fa


---

# Scenario - Proteggere i file in una condivisione di file server

*Si applica a: Azure Rights Management, Office 365*

Questo scenario e la documentazione di supporto per l'utente usano Azure Rights Management per proteggere tutti i file che si desidera proteggere in un file server per garantire che solo i dipendenti dell'organizzazione possano accedervi, anche se vengono copiati e salvati in un archivio fuori dal controllo del reparto IT o inviati tramite posta elettronica ad altri utenti.

Queste istruzioni usano uno dei modelli predefiniti, che limita l'accesso a tutti i dipendenti con tutti i diritti di utilizzo. Tuttavia, se necessario, è possibile limitare i diritti di accesso e utilizzo tramite la configurazione di un modello personalizzato al posto di un modello predefinito.

Le istruzioni sono adatte ai casi seguenti:

-   È necessario proteggere tutti i tipi di file e non solo i file di Office. I file che non possono essere protetti in modo nativo da Azure RMS verranno protetti in modo generico.

-   Tutti i file nel percorso specificato (incluse le sottocartelle) saranno protetti.

-   Su tutti i file la protezione viene riapplicata in base a una pianificazione per garantire che le modifiche ai modelli dei criteri dei diritti vengano applicate ai file protetti.

## Istruzioni sulla distribuzione
![Istruzioni per l'amministratore per la distribuzione rapida di Azure RMS](../media/AzRMS_AdminBanner.png)

Verificare che siano soddisfatti i requisiti seguenti e quindi seguire le istruzioni per le procedure di supporto prima di passare alla documentazione dell'utente.

## Requisiti per questo scenario
Per le istruzioni di funzionamento di questo scenario, sono necessari i requisiti seguenti:

|Requisito|Se sono necessarie ulteriori informazioni|
|---------------|--------------------------------|
|Azure Rights Management non è attivato|[Attivazione di Azure Rights Management](https://technet.microsoft.com/library/jj658941.aspx)|
|Si sono sincronizzati gli account utente di Active Directory locali con Azure Active Directory oppure Office 365, compreso il relativo indirizzo di posta elettronica. Ciò è necessario per tutti gli utenti che potrebbero avere la necessità di accedere ai file una volta protetti con FCI e Azure Rights Management.|[Preparazione per Azure Rights Management](https://technet.microsoft.com/library/jj585029.aspx)|
|Uno dei seguenti:<br /><br />- Per usare un modello predefinito per tutti gli utenti: non è stato archiviato il modello predefinito, &lt;nome organizzazione&gt; - Riservato<br /><br />- Per usare un modello personalizzato per utenti specifici: il modello personalizzato è stato creato e pubblicato|[Configurazione di modelli personalizzati per Azure Rights Management](https://technet.microsoft.com/library/dn642472.aspx)|
|L’applicazione di condivisione Rights Management è distribuita nei computer degli utenti che eseguono Windows|[Distribuzione automatica dell'applicazione di condivisione Microsoft Rights Management](https://technet.microsoft.com/library/dn339003%28v=ws.10%29.aspx)|
|È stato scaricato lo strumento di protezione RMS e i prerequisiti per Azure RMS sono stati configurati|Per le istruzioni sul download dello strumento e sui prerequisiti: [Cmdlet di protezione RMS](https://msdn.microsoft.com/library/mt433195.aspx)<br /><br />Per configurare altri prerequisiti per Azure RMS, ad esempio l'account dell'entità servizio: [about_RMSProtection_AzureRMS](https://msdn.microsoft.com/library/mt433202.aspx)|

### Configurazione di un file server per proteggere tutti i file tramite Azure RMS e Gestione risorse file server con Infrastruttura di classificazione file

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

4.  Seguire la procedura dettagliata in [Protezione RMS con l'infrastruttura di classificazione file (FCI, File Classification Infrastructure) per Windows Server](https://technet.microsoft.com/library/mt601315%28v=ws.10%29.aspx).

    Queste istruzioni includono uno script di Windows PowerShell specificato per l'esecuzione come eseguibile personalizzato in Gestione risorse file server. Le istruzioni includono anche le procedure per verificare che i file siano protetti da Azure Rights Management.

## Istruzioni sulla documentazione per l'utente
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

### Come modificare il &lt;tipo di file&gt; dalla &lt;condivisione di file server&gt;

1.  Fare doppio clic sul file per aprirlo. È possibile che vengano richieste le credenziali.

2.  Viene visualizzata una finestra di dialogo di **file protetto** dell'applicazione di condivisione Microsoft Rights Management che indica che è necessario rispettare le autorizzazioni per **&lt;nome organizzazione&gt; - Riservato**. Per questa ragione, non condividere questo documento con altri utenti che non lavorano per &lt;nome organizzazione&gt;.

3.  Fare clic su **Apri**.

4.  Per modificare il file, salvare innanzitutto il file e rimuovere l'estensione del nome pfile:

    -   &lt;Istruzioni per salvare il file e rimuovere l'estensione pfile&gt;

5.  È ora possibile modificare e salvare il file normalmente.

Periodicamente, il file sarà protetto nuovamente per aggiungere l'estensione del nome file pfile e sarà necessario ripetere questi passaggi.

**Serve assistenza?**

-   Per informazioni aggiuntive:

    -   [Visualizzare e utilizzare i file che sono stati protetti](https://technet.microsoft.com/library/dn574741%28v=ws.10%29)

-   Contattare il supporto tecnico:

    -   *&lt;dettagli contatto&gt;*

### Esempio di documentazione personalizzata per l'utente
![Esempio di documentazione dell'utente per la distribuzione rapida di Azure RMS](../media/AzRMS_ExampleBanner.png)

#### Come modificare disegni CAD dalla condivisione ProjectNextGen

1.  Fare doppio clic sul file per aprirlo. È possibile che vengano richieste le credenziali.

2.  Viene visualizzato una finestra di dialogo **file protetto** dall'applicazione di condivisione Microsoft Rights Management, che indica che sono previste autorizzazioni per **VanArsdel, Ltd - Riservato**. In questo modo, questo documento non viene condiviso con altri utenti che non lavorano per VanArsdel, Ltd.

3.  Fare clic su **Apri**.

4.  Per modificare il file, salvare innanzitutto il file e rimuovere l'estensione del nome pfile:

    -   **File** &gt; **Salva con nome**

    -   Eliminare il suffisso **pfile** dalla fine del nome del file e fare clic su **OK**.

5.  È ora possibile modificare e salvare il file normalmente.

Periodicamente, il file sarà protetto nuovamente per aggiungere l'estensione del nome file pfile e sarà necessario ripetere questi passaggi.

**Serve assistenza?**

-   Per informazioni aggiuntive:

    -   [Visualizzare e utilizzare i file che sono stati protetti](https://technet.microsoft.com/library/dn574741%28v=ws.10%29)

-   Contattare l'help desk: helpdesk@vanarsdelltd.com




<!--HONumber=Jun16_HO4-->


