---
# required metadata

title: Scenario - Condividere un file di Office con utenti in un'altra organizzazione | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: c10a4d7b-f57a-4a43-b66e-477777be59cc

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Scenario - Condividere un file di Office con utenti in un'altra organizzazione

*Si applica a: Azure Rights Management, Office 365*

Questo scenario e la documentazione di supporto per l'utente usano Azure Rights Management in modo che gli utenti possano inviare in modo sicuro un file di Office tramite posta elettronica alle persone in un'altra organizzazione. Il file di Office, ad esempio, potrebbe essere un documento di Word, un foglio di calcolo di Excel o una presentazione di PowerPoint contenente informazioni del listino prezzi di un partner, un elenco di prodotti per un rivenditore o un elenco dei tempi di consegna con potenziali clienti. Quando gli utenti seguono le istruzioni, il file allegato al messaggio di posta elettronica sarà protetto da Rights Management di Azure.

Questo scenario è adatto ai casi seguenti:

-   Il dipendente deve inviare informazioni al di fuori dell'organizzazione, sotto forma di allegato di un documento di Office.

-   Il documento contiene informazioni che non sono pubbliche, ma non sono esclusivamente per uso interno.

-   I destinatari non hanno i requisiti per condividere ulteriormente le informazioni con altri utenti, stamparle o utilizzarle come parte della propria documentazione. Se questo non si verifica, è possibile modificare le istruzioni modificando le autorizzazioni di sola visualizzazione in un'altra opzione che consenta al destinatario di modificare l'allegato.

-   Il dipendente è potenzialmente interessato a sapere quando il documento viene aperto da un utente esterno.

## Istruzioni sulla distribuzione
![Istruzioni per l'amministratore per la distribuzione rapida di Azure RMS](../media/AzRMS_AdminBanner.png)

Prima di passare alla documentazione per l'utente, assicurarsi che i requisiti seguenti siano soddisfatti.

## Requisiti per questo scenario
Affinché le istruzioni per l'utente per questo scenario funzionino, devono verificarsi le seguenti condizioni:

|Requisito|Se sono necessarie ulteriori informazioni|
|---------------|--------------------------------|
|Sono stati preparati account e gruppi per Office 365 o Azure Active Directory|[Preparazione per Azure Rights Management](https://technet.microsoft.com/library/jj585029.aspx)|
|Azure Rights Management non è attivato|[Attivazione di Azure Rights Management](https://technet.microsoft.com/library/jj658941.aspx)|
|L’applicazione di condivisione Rights Management è distribuita nei computer degli utenti che eseguono Windows|[Distribuzione automatica dell'applicazione di condivisione Microsoft Rights Management](https://technet.microsoft.com/library/dn339003%28v=ws.10%29.aspx)|
|Gli utenti dispongono di Outlook da Office 2013|Se gli utenti dispongono di Office 2010, sostituire la schermata con una versione equivalente, in modo che l'immagine corrisponda a ciò che gli utenti vedono.|
|La sottoscrizione di Azure RMS include il rilevamento dei documenti|Se la sottoscrizione per Azure RMS non include la revoca e il rilevamento dei documenti, gli utenti non saranno in grado di completare tutti i passaggi delle istruzioni per l’utente. In questo caso, acquistare una sottoscrizione che supporti queste funzionalità o modificare le istruzioni per l’utente per rimuovere i passaggi che utilizzano queste funzionalità.<br /><br />Per verificare il supporto della propria sottoscrizione: [Confronto tra le offerte di Rights Management Services (RMS)](https://technet.microsoft.com/dn858608)|

## Istruzioni sulla documentazione per l'utente
Usando il modello seguente, copiare e incollare le istruzioni per l'utente in una comunicazione per gli utenti finali e apportare tali modifiche in base all'ambiente:

1.  Sostituire *&lt;nome del tipo di documento di Office&gt;* con il tipo di documento che verrà inviato dagli utenti. Utilizzare termini specifici e familiari per i loro flussi di lavoro, ad esempio "listino", "tempi di consegna" e "proposta di offerta" anziché "documento di Word" e "foglio di calcolo di Excel". Grazie a questo testo più specifico la probabilità che gli utenti seguano le istruzioni quando lavorano con tali documenti è maggiore.

2.  Sostituire *&lt;dettagli contatto&gt;* con istruzioni su come gli utenti possono contattare il supporto tecnico, ad esempio il collegamento a un sito Web, un indirizzo di posta elettronica o un numero di telefono.

3.  **Personalizzazioni aggiuntive che si vuole apportare:**

    -   Nel passaggio 2 suggeriamo **Visualizzatore - Solo visualizzazione** per le autorizzazioni, rendendo il documento allegato, ma non l'originale, di sola lettura per i destinatari. Se questa restrizione non è adatta per il proprio requisito aziendale, modificare questa opzione per un altro set di autorizzazioni, ad esempio **Revisore - Visualizzazione e modifica**.

    -   Nel passaggio 3, è consigliabile selezionare **Consenti di revocare immediatamente l'accesso a questi documenti** in modo che non si verifichino ritardi se gli utenti revocano il documento in un secondo momento, ma questa opzione richiede che il destinatario abbia sempre una connessione a Internet per aprire l’allegato. Questo passaggio richiede anche di disporre di una sottoscrizione che supporti il rilevamento e la revoca dei documenti. Eliminare questo passaggio se non è adatto per gli utenti.

    -   Nel passaggio 4, è consigliabile l'opzione **Invia un messaggio di posta elettronica quando qualcuno tenta di aprire il documento**. Se gli utenti tracciano i documenti utilizzando il portale di rilevamento dei documenti, è possibile decidere che la notifica tramite posta elettronica non è necessaria ed eliminare questo passaggio.

    -   I passaggi non includono l'impostazione di una data di scadenza. Se le informazioni non devono essere usate dopo una determinata data, aggiungere un altro passaggio per impostare una scadenza appropriata, ad esempio 90 giorni dall'invio del messaggio di posta elettronica.

    > [!NOTE] Per altre informazioni sulle singole opzioni selezionabili dagli utenti, vedere [Opzioni della finestra di dialogo per l'applicazione di condivisione Rights Management](https://technet.microsoft.com/library/dn574738.aspx)

4.  Apportare altre modifiche a questo set di istruzioni e quindi inviarlo agli utenti.

La documentazione di esempio mostra come questo set di istruzioni appare agli utenti dopo le personalizzazioni.

![Documentazione dell'utente del modello per la distribuzione rapida di Azure RMS](../media/AzRMS_UsersBanner.png)

### Come condividere un &lt;nome del tipo di documento di Office&gt;

1.  Creare il messaggio di posta elettronica specificando l'indirizzo o gli indirizzi di posta elettronica, digitare il messaggio e allegare *&lt;nome del tipo di documento di Office&gt;* al messaggio di posta elettronica. Quindi nella scheda **MESSAGGIO** fare clic su **Condividi file protetto** all’interno del gruppo **RMS** , quindi fare nuovamente clic su **Condividi file protetto** :

    ![Schermata sulla condivisione di un documento di Office tramite Outlook](../media/AzRMSUserInstructions_ShareProtectedRibbon2013.png)

2.  Nella finestra di dialogo **Condividi file protetto** selezionare **Visualizzatore - Solo visualizzazione**:

    ![finestra di dialogo Condividi file protetto - Visualizzatore - Solo visualizzazione](../media/AzRMS_SharedProtected_ViewerOnly.PNG)

3.  Selezionare **Consenti di revocare immediatamente l'accesso a questi documenti**.

    ![finestra di dialogo Condividi file protetto - revoca immediata](../media/AzRMS_SharedProtected_InstantRevoke.PNG)

4.  Selezionare **Inviami un messaggio di posta elettronica quando qualcuno tenta di aprire questi documenti**:

    ![finestra di dialogo Condividi file protetto - Inviami un messaggio di posta elettronica](../media/AzRMS_SharedProtected_EmailMe.PNG)

5.  Fare clic su **Invia subito**.

Quando un destinatario specificato nella riga **A**, **Cc** o **Ccn** riceve questo messaggio di posta elettronica, viene visualizzato un messaggio che fornisce le istruzioni da seguire per leggere il file *&lt;nome del tipo di documento di Office&gt;* allegato. Essi possono leggere il documento su diversi dispositivi, tra cui iPad, iPhone, tablet e telefoni Android, computer Mac e computer Windows.

Usare il [portale di rilevamento dei documenti](https://track.azurerms.com/) per rilevare se e quando aprono il file &lt;nome del tipo di documento di Office&gt; allegato. È possibile contattarli con una chiamata telefonica di follow-up non appena hanno aperto il file &lt;nome del tipo di documento di Office&gt;.

**Serve assistenza?**

-   Per informazioni aggiuntive:

    -   [Proteggere un file che si condivide tramite posta elettronica](https://technet.microsoft.com/library/dn574735%28v=ws.10%29.aspx)

    -   [Tenere traccia e revocare i documenti](https://technet.microsoft.com/library/dn986611.aspx)

-   Contattare il supporto tecnico:

    -   *&lt;dettagli contatto&gt;*

### Esempio di documentazione personalizzata per l'utente
![Esempio di documentazione dell'utente per la distribuzione rapida di Azure RMS](../media/AzRMS_ExampleBanner.png)

#### Come condividere un listino prezzi con il cliente

1.  Creare il messaggio di posta elettronica specificando l'indirizzo o gli indirizzi di posta elettronica, digitare il messaggio e allegare l’ultimo listino prezzi al messaggio di posta elettronica. Quindi nella scheda **MESSAGGIO** fare clic su **Condividi file protetto** all’interno del gruppo **RMS** , quindi fare nuovamente clic su **Condividi file protetto** :

    ![Schermata sulla condivisione di un documento di Office tramite Outlook](../media/AzRMSUserInstructions_ShareProtectedRibbon2013.png)

2.  Nella finestra di dialogo **Condividi file protetto** selezionare **Visualizzatore - Solo visualizzazione**:

    ![finestra di dialogo Condividi file protetto - Visualizzatore - Solo visualizzazione](../media/AzRMS_SharedProtected_ViewerOnly.PNG)

3.  Selezionare **Consenti di revocare immediatamente l'accesso a questi documenti**.

    ![finestra di dialogo Condividi file protetto - revoca immediata](../media/AzRMS_SharedProtected_InstantRevoke.PNG)

4.  Selezionare **Inviami un messaggio di posta elettronica quando qualcuno tenta di aprire questi documenti**:

    ![finestra di dialogo Condividi file protetto - Inviami un messaggio di posta elettronica](../media/AzRMS_SharedProtected_EmailMe.PNG)

5.  Fare clic su **Invia subito**.

Quando un utente nella riga **A**, **Cc**o **Ccn** riceve questo messaggio di posta elettronica, viene visualizzato un messaggio che fornisce le istruzioni da seguire per leggere il listino prezzi allegato. Essi possono leggere il documento su diversi dispositivi, tra cui iPad, iPhone, tablet e telefoni Android, computer Mac e computer Windows.

Utilizzare il [portale di rilevamento dei documenti](https://track.azurerms.com/) per rilevare se e quando aprono il listino prezzi allegato. Considerare di contattarli con una chiamata telefonica di follow-up appena si nota che hanno aperto il listino prezzi.

**Serve assistenza?**

-   Per informazioni aggiuntive:

    -   [Proteggere un file che si condivide tramite posta elettronica](https://technet.microsoft.com/library/dn574735%28v=ws.10%29.aspx)

    -   [Tenere traccia e revocare i documenti](https://technet.microsoft.com/library/dn986611.aspx)

-   Contattare il supporto tecnico:

    -   E-mail: helpdesk@vanarsdelltd.com



<!--HONumber=May16_HO2-->


