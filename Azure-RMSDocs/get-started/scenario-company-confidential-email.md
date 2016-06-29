---
# required metadata

title: Scenario - Invio di email aziendali riservate | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 05/20/2016
ms.topic: get-started-article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 950799e9-2289-48c7-b95a-f54a8ead520a

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Scenario - Invio di email aziendali riservate

*Si applica a: Azure Rights Management, Office 365*

Questo scenario e la documentazione di supporto per l'utente usano Azure Rights Management in modo che qualsiasi utente dell'organizzazione possa inviare in modo sicuro comunicazioni tramite email non leggibili all'esterno dell'organizzazione. Ad esempio, se qualcuno inoltra l'email a qualcuno di un'altra organizzazione o a un account di posta elettronica personale. Le email e gli allegati saranno protetti da Azure Rights Management e da un modello selezionato dagli utenti dal client di posta elettronica.

Il modo più semplice per abilitare questo scenario è usare uno dei modelli predefiniti integrati che limitano automaticamente l'accesso a tutti gli utenti dell'organizzazione. Tuttavia se necessario, è possibile impostare limitazioni più restrittive creando un modello personalizzato che, ad esempio, limita l'accesso a un sottoinsieme di utenti o prevede altre restrizioni, ad esempio sola lettura o con data di scadenza, oppure disattiva il pulsante Inoltra nei client di posta elettronica.

> [!IMPORTANT]
> In questo scenario, anche se è possibile rimuovere **Inoltra** direttamente da un modello personalizzato configurato e il pulsante Inoltra sarà disabilitato nei client di posta elettronica, questa configurazione non impedisce agli utenti di condividere l'email con un altro utente autorizzato. Il destinatario può salvare l'email (e tutti gli allegati) e quindi condividere le informazioni tramite altri meccanismi di condivisione.
> 
> Ad esempio, Bob invia un'email ad Alice usando un modello personalizzato che applica i diritti personalizzati di salvataggio del file e modifica del contenuto al gruppo Marketing e non include il diritto di inoltro. Anche se Alice non può inoltrare l'email ad altri utenti, può salvare il messaggio e gli allegati su un'unità USB o un server di condivisione file, che qualsiasi membro del gruppo Marketing può leggere e modificare se può accedere a tali file. Gli utenti che non appartengono al gruppo Marketing non saranno in grado di aprire il contenuto.

Le istruzioni sono adatte ai casi seguenti:

-   Qualsiasi utente all'interno dell'organizzazione desidera condividere informazioni con altri utenti dell'organizzazione, ma tali informazioni non devono essere condivise all'esterno dell'organizzazione.

-   Le informazioni da condividere possono essere all'interno dell'email o dell'allegato.

-   Gli utenti devono selezionare manualmente il modello all'interno del client di posta elettronica.

## Istruzioni sulla distribuzione
![Istruzioni per l'amministratore per la distribuzione rapida di Azure RMS](../media/AzRMS_AdminBanner.png)

Prima di passare alla documentazione per l'utente, assicurarsi che i requisiti seguenti siano soddisfatti.

## Requisiti per questo scenario
Per le istruzioni di funzionamento di questo scenario, sono necessari i requisiti seguenti:

|Requisito|Se sono necessarie ulteriori informazioni|
|---------------|--------------------------------|
|Sono stati preparati account e gruppi per Office 365 o Azure Active Directory|[Preparazione per Azure Rights Management](https://technet.microsoft.com/library/jj585029.aspx)|
|Gestione della chiave tenant di Azure Rights Management tramite Microsoft. Non viene usato il sistema BYOK|[Pianificazione e implementazione della chiave del tenant di Azure Rights Management](https://technet.microsoft.com/library/dn440580.aspx)|
|Azure Rights Management non è attivato|[Attivazione di Azure Rights Management](https://technet.microsoft.com/library/jj658941.aspx)|
|Uno dei seguenti:<br /><br />- Exchange Online è abilitato per Azure Rights Management<br /><br />- Il connettore RMS è installato e configurato per Exchange locale|Per Exchange Online: vedere la sezione **Exchange Online: configurazione di IRM** di [Configurazione di applicazioni per Rights Management di Windows Azure](https://technet.microsoft.com/library/jj585031.aspx).<br /><br />Per Exchange locale: [Distribuzione del connettore di Azure Rights Management](https://technet.microsoft.com/library/dn375964.aspx)|
|Non è stato archiviato il modello di Azure Rights Management predefinito **&lt;organizzazione&gt; - Riservato**. In alternativa, è stato configurato un modello personalizzato per questo scopo, poiché sono necessarie impostazioni più restrittive, oppure solo un sottoinsieme di utenti nell'organizzazione deve poter leggere le email protette.|[Configurazione di modelli personalizzati per Azure Rights Management](https://technet.microsoft.com/library/dn642472.aspx)<br /><br />Suggerimento: se sono necessarie impostazioni di criteri di uso più restrittivi, per tutti gli utenti dell'organizzazione, copiare e quindi modificare uno dei modelli predefiniti, anziché crearne uno daccapo.<br /><br />I modelli aggiornati non vengono aggiornati immediatamente per i client di posta elettronica in questo scenario. Per informazioni, controllare la sezione [Aggiornamento dei modelli per gli utenti](https://technet.microsoft.com/library/dn642472.aspx) dell'articolo dedicato alla configurazione dei modelli.|
|Gli utenti che inviano email protette dispongono di Outlook 2013 o 2016 Outlook o Outlook Web Access.<br /><br />Gli utenti che ricevono l'email dispongono di un client di posta elettronica che supporti Azure Rights Management.|È possibile usare Outlook 2010, ma è necessario [installare l'applicazione di condivisione Rights Management per Windows](https://technet.microsoft.com/library/dn339003.aspx) e modificare di conseguenza le istruzioni utente.<br /><br />Per un elenco dei client di posta elettronica che supportano Azure Rights Management, vedere la colonna **Email** nella tabella [Funzionalità dei dispositivi Client](https://technet.microsoft.com/library/dn655136.aspx), da [Requisiti per Azure Rights Management](https://technet.microsoft.com/library/dn655136.aspx)|

## Istruzioni sulla documentazione per l'utente
Usando il modello seguente, copiare e incollare le istruzioni per l'utente in una comunicazione per gli utenti finali e apportare tali modifiche in base all'ambiente:

1.  Sostituire tutte le istanze di *&lt;nome organizzazione&gt;* con il nome dell'organizzazione.

2.  Sostituire tutte le istanze di *&lt;nome organizzazione - Riservato&gt;* con il nome del modello predefinito o personalizzato.

3.  Sostituire le schermate in modo che siano visualizzati i nomi dei modelli dell'organizzazione.

4.  Sostituire *&lt;dettagli contatto&gt;* con istruzioni su come gli utenti possono contattare il supporto tecnico, ad esempio il collegamento a un sito Web, un indirizzo di posta elettronica o un numero di telefono.

5.  **Personalizzazioni aggiuntive che si vuole apportare:**

    -   Se è possibile limitare le istruzioni a un solo client di posta elettronica, è consigliabile eseguire questa operazione per motivi di semplicità ed eliminare l'altro set di istruzioni.

    -   Se si usa un modello personalizzato anziché il modello predefinito suggerito, rivedere il testo in conseguenza:

        -   Rendere il titolo più specifico.

        -   Specificare gli utenti o gruppi da selezionare nel passaggio 1.

        -   Specificare il nome del modello personalizzato nel passaggio 2.

        -   Modificare il paragrafo finale per illustrare le restrizioni a cui saranno soggetti i destinatari.

6.  Apportare altre modifiche a questo set di istruzioni e quindi inviarlo agli utenti.

7.  Poiché alcuni client non supportano Rights Management, potrebbe essere necessario fornire linee guida e consigli per i destinatari delle email protette. Queste informazioni saranno basate sui dispositivi e le applicazioni di posta elettronica in uso nell'organizzazione e su eventuali preferenze dell'utente. Ad esempio, è consigliabile che gli utenti iOS leggano le email protette con Outlook per iPad e iPhone anziché sul client nativo di posta elettronica di iOS.

    Per altre informazioni sui client di posta elettronica, vedere la colonna **Email** nella tabella [Funzionalità dei dispositivi Client](https://technet.microsoft.com/library/dn655136.aspx), da [Requisiti per Azure Rights Management](https://technet.microsoft.com/library/dn655136.aspx)

La documentazione di esempio mostra come questo set di istruzioni appare agli utenti dopo le personalizzazioni.

![Documentazione dell'utente del modello per la distribuzione rapida di Azure RMS](../media/AzRMS_UsersBanner.png)

### Procedura per inviare email che contengono informazioni aziendali riservate tramite Outlook

1.  In Outlook creare un nuovo messaggio di posta elettronica, aggiungere eventuali allegati e selezionare gli utenti o i gruppi di *&lt;nome organizzazione&gt;*.

2.  Nella scheda **Opzioni** fare clic su **Autorizzazioni** e quindi selezionare **&lt;nome organizzazione - Riservato&gt;**:

    ![Screenshot sull'invio di messaggi di posta elettronica contenenti informazioni aziendali riservate tramite Outlook](../media/AzRMS_OutlookTemplate.PNG)

3.  Inviare il messaggio.

### Procedura per inviare email che contengono informazioni aziendali riservate tramite Outlook Web App

1.  In Outlook Web App, creare un nuovo messaggio di posta elettronica, aggiungere eventuali allegati e selezionare gli utenti o i gruppi di *&lt;nome organizzazione&gt;* dalla rubrica.

2.  Fare clic su **…**, quindi su **Imposta autorizzazioni** e selezionare **&lt;nome organizzazione - Riservato&gt;**:

    ![Screenshot sull'invio di messaggi di posta elettronica contenenti informazioni aziendali riservate tramite Outlook Web App](../media/AzRMS_OWATemplate.png)

3.  Inviare il messaggio.

È possibile che ad alcuni destinatari specificati nella riga **A**, **Cc**, o **Ccn** venga richiesto di eseguire l'autenticazione prima di leggere il messaggio per verificare che siano utenti di *&lt;nome organizzazione&gt;*. In altri casi, agli utenti non viene richiesto, poiché sono già autenticati.

Le persone che ricevono il messaggio di posta elettronica potranno inoltrarlo ad altre persone, ma solo gli utenti di *&lt;nome organizzazione&gt;* potranno leggerlo. Se si collega un documento di Office, disporrà della stessa protezione, anche se tale allegato viene salvato con un nome diverso, in un'altra posizione. Tuttavia, agli utenti autenticati possono copiare e incollare dal email o allegato o stamparlo. Se è necessaria una protezione più restrittiva che impedisca azioni del genere, rivolgersi al supporto tecnico.

**Serve assistenza?**

-   Contattare il supporto tecnico:

    -   *&lt;dettagli contatto&gt;*

### Esempio di documentazione personalizzata per l'utente
![Esempio di documentazione dell'utente per la distribuzione rapida di Azure RMS](../media/AzRMS_ExampleBanner.png)

#### Procedura per inviare email che contengono informazioni aziendali riservate tramite Outlook

1.  In Outlook, creare una nuova email, aggiungere tutti gli allegati da includere e quindi selezionare gli utenti o i gruppi VanArsdel dalla rubrica.

2.  Nella scheda **OPZIONI**, fare clic su **Autorizzazione**, quindi selezionare **VanArsdel, Ltd - riservato**:

    ![Screenshot sull'invio di messaggi di posta elettronica contenenti informazioni aziendali riservate tramite Outlook](../media/AzRMS_OutlookTemplate.PNG)

3.  Inviare il messaggio.

#### Procedura per inviare email che contengono informazioni aziendali riservate tramite Outlook Web App

1.  In Outlook Web App, creare una nuova email, aggiungere tutti gli allegati da includere e quindi selezionare gli utenti o i gruppi VanArsdel dalla rubrica.

2.  Fare clic su **...**, fare clic su **Impostare le autorizzazioni**, quindi selezionare **VanArsdel, Ltd - Riservato**:

    ![Screenshot sull'invio di messaggi di posta elettronica contenenti informazioni aziendali riservate tramite Outlook Web App](../media/AzRMS_OWATemplate.png)

3.  Inviare il messaggio.

Quando qualcuno nella riga **A**, **Cc**, o **Ccn** riceve quest’email, gli potrebbe essere richiesto di eseguire l'autenticazione prima di poter leggere il messaggio, per verificare si tratti di un utente di VanArsdel, Ltd. In altri casi, agli utenti non viene richiesto, poiché sono già autenticati.

Le persone a cui si invia l'email saranno in grado di inoltrarla ad altre persone, ma solo gli utenti di VanArsdel saranno in grado di leggerla. Se si collega un documento di Office, disporrà della stessa protezione, anche se tale allegato viene salvato con un nome diverso, in un'altra posizione. Tuttavia, agli utenti autenticati possono copiare e incollare dal email o allegato o stamparlo. Se è necessaria una protezione più restrittiva che impedisca azioni del genere, rivolgersi al supporto tecnico.

**Serve assistenza?**

-   Contattare il supporto tecnico:

    -   E-mail: helpdesk@vanarsdelltd.com



<!--HONumber=May16_HO3-->


