<properties pageTitle="Estensioni markdown personalizzate usate negli articoli tecnici"  description="Elenca le estensioni markdown personalizzate che consentono di includere video incorporati, note e suggerimenti, contenuto riutilizzabile e altri elementi negli articoli tecnici in docs.microsoft.com/ems." services="" solutions="" documentationCenter="" authors="v-jocgar" manager="robmazz" editor=""/>

<tags ms.service="contributor-guide" ms.devlang="" ms.topic="article" ms.tgt_pltfrm=""  ms.workload="" ms.date="02/26/2016" ms.author="v-jocgar"/>

## Estensioni markdown personalizzate per EMS
Attività:
- [ ] #34 Confermare l'uso di estensioni markdown per Nota, Importante e così via. 
- [ ] #35 Confermare che EMS usa i token e specificare la posizione della directory corretta.
- [ ] #36 Confermare che i file delle icone personalizzate sono disponibili e installati nel percorso corretto.
- [ ] #37 Confermare il nome della directory per i token che usano file multimediali.
- [ ] #38 Confermare le procedure corrette per l'uso dei token.
- [ ] #39 Specificare un esempio di sintassi per l'uso dei token. 
- [ ] #40 Confermare l'URL della documentazione EMS.
- [ ] #41 Confermare che i video di Channel 9 possono essere usati dai writer esterni. 
- [ ] #42 Confermare il percorso dei video EMS in Channel 9.
- [ ] #43 Confermare l'uso dei video EMS in Channel 9.
- [ ] #44 Confermare la sintassi per incorporare i video.
- [ ] #45 È necessario un esempio visualizzabile di Github.
- [ ] #46 È necessario un esempio di video visualizzabile di Github.
- [ ] #47 È necessario un esempio visualizzabile del sito Web di documentazione EMS. 
- [ ] #48 Confermare che i selettori sono disponibili per gli articoli EMS.
- [ ] #49 È necessario un esempio di sostituzione di selettori semplici.
- [ ] #50 Confermare la sintassi dei selettori semplici.
- [ ] #51 È necessaria la sintassi dei selettori semplici sostitutivi.
- [ ] #52 È necessario un esempio di selettore semplice sostitutivo.
- [ ] #53 Confermare che i selettori bidirezionali funzionano come descritto.
- [ ] #54 È necessario un esempio di selettori bidirezionali.
- [ ] #55 Confermare la sintassi dei selettori bidirezionali.
- [ ] #56 È necessario un esempio di selettori bidirezionali sostitutivi.


## Guida generale per il markdown

Se non è stato letto l'argomento [Creazione di contenuti per EMS in markdown](./authoring-in-markdown.md), è consigliabile leggerlo prima di continuare con questo argomento. 

## Estensioni markdown personalizzate usate negli articoli tecnici

Gli articoli usano la notazione markdown tipica di GitHub per la maggior parte delle formattazioni: paragrafi, collegamenti, elenchi, intestazioni e così via. Tuttavia, quando le pagine visualizzabili di Microsoft.com/ems richiedono elementi di formattazione più completi, si usano estensioni markdown personalizzate. Le estensioni usate attualmente sono le seguenti:

+ [Note e suggerimenti]
+ [Token]
+ [Video incorporati]
+ [Selettori di tecnologia e piattaforma]

## Note e suggerimenti
<span style="color:red;">Confermare l'uso di estensioni markdown per Nota, Importante e così via.</span>
È possibile scegliere tra 4 tipi di note e suggerimenti:

- EMS.NOTE
- EMS.WARNING
- EMS.TIP
- EMS.IMPORTANT

### Utilizzo
In generale, usare il numero minimo possibile di note e suggerimenti negli articoli. Quando si decide di usarli, scegliere il tipo di nota o suggerimento appropriato:

- Usare EMS.NOTE per evidenziare informazioni neutre o positive, che sottolineano o riaffermano punti chiave del testo principale. Una nota include informazioni che risultano utili solo in casi specifici.

  ![](./media/notes-note.png)

- Usare EMS.WARNING per avvisare l'utente di una condizione che potrebbe causare un problema un futuro. Ad esempio, la selezione di un'opzione o una determinata scelta potrebbero causare una condizione di blocco.

  ![](./media/notes-warning.png)

- Usare EMS.TIP per aiutare gli utenti ad applicare le tecniche e le procedure descritte nel testo per esigenze specifiche. Un suggerimento può anche proporre metodi alternativi non evidenti a prima vista. Tuttavia i suggerimenti non sono indispensabili per la comprensione di base del testo.

  ![](./media/notes-tip.png)

- Usare EMS.IMPORTANT per offrire informazioni essenziali per il completamento di un'attività.

  ![](./media/notes-important.png)

Queste note e suggerimenti supportano blocchi di codice, immagini, elenchi e collegamenti; tuttavia è consigliabile creare note e suggerimenti semplici e diretti. Quando ci si trova a creare note complesse e molto formattate, in realtà potrebbe essere utile aggiungere un'altra sezione nel testo principale dell'articolo. Una quantità eccessiva di note in un articolo può anche essere fonte di distrazione e complicare la consultazione o la lettura.

### Markdown di esempio

Tutti gli esempi visualizzano EMS.NOTE. Per usare un formato TIP, WARNING o IMPORTANT, sostituire "NOTE" nella notazione markdown:

    > [EMS.TIP]

    > [EMS.WARNING]

    > [EMS.IMPORTANT]

Paragrafo singolo:

    > [EMS.NOTE] To complete this tutorial, you must have an active Microsoft account. If you don't have an account, you can create a free account in just a couple of minutes.

Più paragrafi:

    > [EMS.NOTE] To complete this tutorial, you must have an active Microsoft account.
    >
    > If you don't have an account, you can [create a free account](https://signup.live.com/signup) in just a couple of minutes.

## Token
<span style="color:red;">Confermare che EMS usa i token e specificare il percorso corretto della directory.</span>
I frammenti di testo riutilizzabili nel repository GitHub sono detti "token". Per usare un determinato testo in più articoli, è possibile includere un riferimento al frammento di testo nei file markdown. Il frammento di testo (token) in sé è un semplice file markdown ( con estensione md). Può contenere qualsiasi elemento markdown valido, inclusi testo, collegamenti e immagini. 

Tutti i file token markdown devono trovarsi nella <span style="color:red;">Confermare che i file icona personalizzati siano disponibili e installati nel percorso corretto.</span> [directory /tokens](è necessario il percorso corretto) nella directory radice del repository. Quando viene pubblicato l'articolo, il testo del token viene integrato correttamente nell'argomento pubblicato.

- Per creare il riferimento a un token si usa una sintassi specifica.

- I file multimediali inseriti in un token devono essere creati nella cartella `/media` specifica per il token. Le cartelle multimediali per i token si trovano nella <span style="color:red;">Confermare il nome della directory dei token che usano file multimediali</span> [cartella ems-content/tokens/media](è necessario il percorso corretto). 

## Utilizzo
<span style="color:red;">Confermare le procedure corrette per l'uso dei token.</span>
- Usare i token ogni volta che si vuole visualizzare lo stesso testo in più articoli.
- I token vanno usati con quantità di contenuto importanti: uno o due paragrafi, una procedura condivisa o una sezione condivisa. Evitare di usarli per elementi di testo più piccoli di una frase. I token non vanno usati per nomi prodotto o frasi incomplete.
- Evitare di incorporare token all'interno di altri token. Il sistema di pubblicazione può produrre errori.
- Evitare la condivisione di file multimediali tra i file. Usare un file distinto con un nome univoco per ogni token e ogni articolo. Archiviare il file multimediale nella cartella multimediale associata al token.
- Non usare solo token come contenuto di un articolo. I token devono essere elementi complementari del contenuto presente nel resto dell'articolo.
- Poiché tutti i token devono trovarsi nella directory `/token`, il percorso da un articolo a un token è sempre

    ../token

- NON ripetere il riferimento a un nome file immagine o a un collegamento nell'articolo e nel token. Aggiungere "-token" al riferimento del collegamento o al nome file multimediale per evitare di ripetere il riferimento:

 **Riferimento al collegamento**

 Sostituire: odata.org
 con: odata.org-token

 **Riferimento all'immagine**

 Sostituire: table.png
 con: table-token.png

### Markdown di esempio per i token
<span style="color:red;">Specificare un esempio di sintassi per l'uso dei token. </span>
La sintassi per l'aggiunta di un token a un articolo di documentazione è la seguente:

    [EMS.TOKEN [token-short-name](../tokens/token-file-name.md)]

Esempio

    [EMS.INCLUDE [howto-blob-storage](../tokens/howto-blob-storage.md)]

La prima parte del token è il nome del token, senza il percorso e senza l'estensione md. La seconda parte è il percorso relativo del token nella directory /token, con l'estensione md.

### Rendering

Nella pagina GitHub visualizzabile, il token viene restituito come segue:

 [EMS.TOKEN howto-blob-storage]

Nel codice HTML visualizzabile in <span style="color:red;">Confermare l'URL della documentazione EMS</span> http://docs.microsoft.com/ems, il codice HTML dei token viene unito al codice HTML delle altre parti del documento. Tuttavia il codice HTML contiene un commento HTML con il nome del file markdown del token originale e l'hash commit di GitHub. Questo commento viene incluso per la risoluzione dei problemi, in modo da identificare e individuare facilmente il contenuto di origine in GitHub:

  ![](./media/token.png)


## Video incorporati
<span style="color:red;">Confermare che i video di Channel 9 possono essere usati dai writer esterni.</span>
Gli articoli tecnici supportano i video incorporati, a condizione che i video si trovino nel sito Microsoft [Channel 9](http://channel9.msdn.com/). I video di Channel 9 devono essere integrati con <span style="color:red;">Confermare il percorso dei video EMS in Channel 9.</span> [Video Center in docs.microsoft.com] (è necessario il percorso effettivo). Attualmente i video di YouTube incorporati non sono supportati; i collaboratori della community possono creare collegamenti a YouTube se il video da includere si trova in quell'interfaccia.

### Utilizzo
<span style="color:red;">Confermare l'uso dei video EMS in Channel 9.</span>
- Assicurarsi che il video si trovi nell'area video di Channel 9.

- Copiare l'ID del video dall'URL descrittivo del video in Channel 9. Ad esempio l'ID del video [https://channel9.msdn.com/Shows/This+Week+On+Channel+9/TWC9-Stacking-Microsoft-Windows-10-Pi-Bobble-Head-your-Nodejs-and-more](https://channel9.msdn.com/Shows/This+Week+On+Channel+9/TWC9-Stacking-Microsoft-Windows-10-Pi-Bobble-Head-your-Nodejs-and-more) è ** ??? **.

### Sintassi
<span style="color:red;">Confermare la sintassi di incorporamento dei video. </span>
    > [EMS.VIDEO video-id-string]

### Rendering
<span style="color:red;">È necessario un esempio di video visualizzabile di Github. </span>
In GitHub: [è necessario un esempio dell'aspetto di un articolo quando viene aggiunto a Github](something.md)

<span style="color:red;">È necessario un esempio visualizzabile del sito Web di documentazione EMS. </span>
Articolo pubblicato: [è necessario un esempio dell'aspetto di un articolo pubblicato nel sito della documentazione](è necessario il percorso effettivo)

## Selettori di tecnologia e piattaforma
<span style="color:red;">Confermare che i selettori sono disponibili per gli articoli EMS</span>
È possibile usare selettori di tecnologia e piattaforma negli articoli tecnici quando si creano più versioni dello stesso articolo, per adattarlo alle variazioni dell'implementazione in piattaforme o tecnologie diverse. In genere questa funzionalità è destinata soprattutto ai contenuti per le piattaforme mobili destinati agli sviluppatori. Attualmente esistono due tipi di selettori, i [selettori semplici](#simple-selectors) e i [selettori bidirezionali](#two-way-selectors).

Dato che lo stesso markdown del selettore viene incluso in ogni argomento della selezione, è consigliabile posizionare il selettore per l'argomento in un token, quindi creare riferimenti a tale token in tutti gli argomenti che usano lo stesso selettore.

### Selettori semplici

I selettori semplici (unidirezionali) appaiono come un gruppo di pulsanti di opzione appena sotto il titolo. Usare questi pulsanti quando i clienti devono scegliere argomenti in una singola piattaforma o set di tecnologie, ad esempio .NET, Node.js e Java.  Usare l'estensione markdown personalizzata per tutti i selettori: evitare l'uso di codice HTML per i selettori.  

<span style="color:red;">È necessario un esempio di sostituzione di selettori semplici; la presente versione Azure viene lasciata qui come riferimento.</span>
In [Introduzione agli hub di notifica](http://azure.microsoft.com/documentation/articles/notification-hubs-windows-phone-get-started/) si può vedere come l'autore ha creato 8 versioni dello stesso articolo, ma ha usato i selettori per attivare la navigazione tra tutti gli articoli.

![Esempio di selettore semplice](./media/selectors.png)

#### Sintassi
<span style="color:red;">Confermare la sintassi dei selettori semplici</span>
    > [EMS.SELECTOR]
    - [Link #1 Label](link #1 url)
    - [Link #2 Label](link #2 url)

#### Esempio
<span style="color:red;">È necessaria la sintassi dei selettori semplici sostitutivi</span>
    > [EMS.SELECTOR]
    - [Windows Runtime 8.1 Universal](../articles/notification-hubs-windows-store-dotnet-get-started/)
    - [Windows Phone Silverlight 8.x](../articles/notification-hubs-windows-phone-get-started/)
    - [iOS](../articles/notification-hubs-ios-get-started/)
    - [Android](../articles/notification-hubs-android-get-started/)
    - [Kindle](../articles/notification-hubs-kindle-get-started/)
    - [Baidu](../articles/notification-hubs-baidu-get-started/)
    - [Xamarin.iOS](../articles/partner-xamarin-notification-hubs-ios-get-started/)
    - [Xamarin.Android](../articles/partner-xamarin-notification-hubs-android-get-started/)
    - [Chrome](../articles/notification-hubs-chrome-get-started/)

#### Rendering

<span style="color:red;">È necessario un esempio di sostituzione di selettori semplici; la presente versione viene lasciata qui come riferimento.</span>
L'immagine precedente visualizza il risultato in docs.microsoft.com/ems. Nelle pagine di GitHub visualizzabili i selettori appaiono come un elenco puntato di collegamenti.

### Selettori bidirezionali
<span style="color:red;">Confermare che i selettori bidirezionali funzionano come descritto.</span>
I selettori bidirezionali consentono agli utenti di selezionare un argomento da una matrice bidirezionale. Questa funzionalità è essenziale quando una tecnologia di EMS, ad esempio Servizi mobili, supporta più piattaforme back-end ma anche più client. Tenere presente quanto segue:

- Anche se è stato progettato come `(Platform | Backend)`, ora il testo dell'elenco a discesa può essere personalizzato.
- Non è necessaria una voce di elenco per ogni punto della matrice, ma è necessario avere una voce in cui l'URL di un argomento esiste e non è un duplicato.
- Il collegamento può essere qualsiasi URL, anche se in genere è un altro argomento di GitHub.

<span style="color:red;">È necessario un esempio di selettori bidirezionali sostitutivi; la presente versione Azure viene lasciata qui come riferimento.</span>
In [Introduzione a Servizi mobili](http://azure.microsoft.com/en-us/documentation/articles/mobile-services-ios-get-started/) si può vedere come l'autore ha creato 15 versioni dello stesso articolo, (9 piattaforme client mobili e 2 piattaforme di back-end), ma ha usato i selettori per attivare la navigazione tra tutti gli articoli. Osservare che 3 articoli non hanno entrambe le versioni di back-end.

![Esempio di selettori bidirezionali](./media/selector-list.png)

#### Sintassi
<span style="color:red;">Confermare la sintassi dei selettori bidirezionali</span>
    > [AZURE.SELECTOR-LIST (Dropdown1 | Dropdown2 )]
    - [(Dropdown1Text1 | Dropdown2Text1 )](../articles/dropdown1-text1-dropdown2-text1.md)
    - [(Dropdown1Text1 | Dropdown2Text2 )](../articles/dropdown1-text1-dropdown2-text1.md)
    - [(Dropdown1Text2 | Dropdown2Text3 )](../articles/dropdown1-text1-dropdown2-text1.md)
    - [(Dropdown1Text3 | Dropdown2Text4 )](../articles/dropdown1-text1-dropdown2-text1.md)

#### Esempio
<span style="color:red;">È necessario un esempio di selettori bidirezionali sostitutivi</span>
    > [AZURE.SELECTOR-LIST (Platform | Backend )]
    - [(iOS | .NET)](./mobile-services-dotnet-backend-ios-get-started-push.md)
    - [(iOS | JavaScript)](./mobile-services-javascript-backend-ios-get-started-push.md)
    - [(Windows Runtime 8.1 universal | C#)](./mobile-services-dotnet-backend-windows-universal-dotnet-get-started-push.md)
    - [(Windows Runtime 8.1 universal C# | Javascript)](./mobile-services-javascript-backend-windows-universal-dotnet-get-started-push.md)
    - [(Windows Phone | .NET)](./mobile-services-dotnet-backend-windows-phone-get-started-push.md)
    - [(Windows Phone | Javascript)](./mobile-services-javascript-backend-windows-phone-get-started-push.md)
    - [(Android | .NET)](./mobile-services-dotnet-backend-android-get-started-push.md)
    - [(Android | Javascript)](./mobile-services-javascript-backend-android-get-started-push.md)
    - [(Xamarin iOS | Javascript)](./partner-xamarin-mobile-services-ios-get-started-push.md)
    - [(Xamarin Android | Javascript)](./partner-xamarin-mobile-services-android-get-started-push.md)
    - [HTML](../articles/mobile-services-html-get-started/)
    - [PhoneGap](../articles/mobile-services-javascript-backend-phonegap-get-started/)
    - [Sencha](../articles/partner-sencha-mobile-services-get-started/)

#### Rendering
<span style="color:red;">È necessario un esempio di selettori bidirezionali sostitutivi; la presente versione viene mantenuta qui come riferimento.</span>
L'immagine precedente visualizza il risultato in azure.microsoft.com. Nelle pagine di GitHub visualizzabili i selettori appaiono come un elenco puntato di collegamenti.

<!--Anchors-->
[Notes and tips]: #notes-and-tips
[Tokens]: #tokens
[Embedded videos]: #embedded-videos
[Technology and platform selectors]: #technology-and-platform-selectors

## Torna alla pagina iniziale

- [Overview article](./../README.md)
- [Index of guidance articles](./contributor-guide-index.md)


<!--HONumber=Mar16_HO1-->


