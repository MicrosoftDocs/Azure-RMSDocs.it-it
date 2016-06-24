<properties pageTitle="Creazione di contenuti per EMS in Markdown" description="Illustra come creare immagini in Markdown in base alle indicazioni fornite per i repository di Enterprise Mobility Suite." services=""     solutions="" documentationCenter="" authors="v-jocgar" manager="robmazz" />

<tags ms.service="contributor-guide" ms.devlang="" ms.topic="article" ms.tgt_pltfrm=""  ms.workload="" ms.date="02/25/2016" ms.author="v-jocgar" />

# Creazione di contenuti per EMS in Markdown

Per eseguire le operazioni seguenti: 
- [ ] n. 23 Verificare il layout dell'articolo su EMS per le immagini /articles/<directory-servizio>/media
- [ ] n. 24 Fornire un esempio per /articles/<directory-servizio>/media
- [ ] n. 25 Verificare la larghezza massima delle immagini nella colonna centrale della pagina della documentazione di EMS (580 o 600 px) in 3 paragrafi
- [ ] n. 26 Verificare se per le immagini concettuali EMS ha un set di simboli diverso da quello disponibile all'indirizzo http://aka.ms/CnESymbols. 
- [ ] n. 27 Verificare l'URL della guida del collaboratore
- [ ] n. 28 Verificare l'intero schema dei collegamenti
- [ ] n. 29 Gli articoli sono organizzati in sottodirectory dei servizi?
- [] n. 30 La metodologia di collegamento degli ancoraggi deve essere confermata
- [ ] n. 31 Verificare la metodologia di collegamento e l'uso dei selettori.
- [ ] n. 32 Testare lo schema di collegamento per assicurarsi che funzioni correttamente

Questo articolo contiene riferimenti relativi a come scrivere articoli tecnici sui servizi e le tecnologie EMS. Queste linee guida sono valide se si sta creando nuova documentazione o aggiornando la documentazione esistente.

## Perché scrivere per EMS?

Microsoft Enterprise Mobility Suite (EMS) è stata creata specificamente per affrontare con minori difficoltà il passaggio a servizi mobili, integrati e basati sul cloud. I tre componenti principali, Microsoft Azure Active Directory Premium, Microsoft Intune e Microsoft Azure Rights Management, sono stati creati fin dall'inizio come servizi cloud e progettati per interagire tra loro e costituire una famiglia di tecnologie integrate diversa da qualsiasi altra sul mercato. Per rilevare gli attacchi locali, EMS include anche Microsoft Advanced Threat Analytics. Con EMS gli utenti aziendali possono usare i dispositivi che preferiscono, garantendo la massima produttività, mentre i beni aziendali sono solidamente protetti.

La creazione di documentazione per i singoli prodotti è sempre una priorità. Ma poiché EMS è una famiglia di prodotti, sono anche necessari articoli e documenti di procedura che consentano ai clienti di usare con efficienza i prodotti in modo integrato. Gli scenari di integrazione di prodotti vengono già documentati. Tuttavia sono incoraggiati i commenti e i suggerimenti di dipendenti e utenti che usano ogni giorno questi prodotti all'interno della propria azienda.

Di conseguenza, la documentazione è stata resa pubblica su Github. Qui è possibile contribuire in modi diversi:
- **Correggendo gli errori del testo.** Nonostante l'impegno, non sempre gli errori vengono individuati. Gli utenti sono quindi invitati a mettersi in contatto tramite Github e a fornire il proprio aiuto.
- **Suggerendo nuovi argomenti.** Se una procedura o un argomento ricorre abbastanza frequentemente da meritare un argomento nella documentazione, ma l'argomento non è stato ancora creato, gli utenti sono incoraggiati a scriverlo e si cercherà di inserirlo.
- **Aggiungendo nuove domande frequenti.** In caso di dubbi su una questione non trattata nella documentazione più simile a una domanda che a un argomento vero e proprio, inviare un'aggiunta alle domande frequenti, che verrà sicuramente esaminata. 

Il concetto è che, come è noto, gli utenti hanno ottime idee e possono offrire utilissimi suggerimenti. È quindi opportuno che partecipino al miglioramento di EMS nel suo complesso. 

## Suggerimenti per articoli più efficaci

Quando si scrive un articolo per EMS, tenere presente quanto segue:

**Procedure specifiche per EMS**
- Il nome ufficiale del prodotto è "Microsoft Enterprise Mobility Suite" ma è quasi sempre possibile usare "EMS", come in "EMS Cloud Identity and Access Management".
- Usare "EMS" prima del nome di una caratteristica o di un servizio solo la prima volta che vi si fa riferimento. Ad esempio, dopo la prima citazione, "EMS Cloud Identity and Access Management" diventa "Cloud Identity and Access Management". 
- Tutti i titoli della documentazione di EMS iniziano con la lettera maiuscola. 
- In genere, evitare gli acronimi in generale, poiché creano solo confusione.

**Procedure consigliate per la scrittura**
- Usare uno stile discorsivo e amichevole, come se si parlasse di persona con un interlocutore. Per i dettagli, vedere l'[argomento relativo a stile e tono](./style-and-voice.md).
- Eseguire il controllo ortografico e grammaticale degli argomenti, anche se a tale scopo fosse necessario tagliare e incollare il testo in Word.
- Usare frasi semplici. Sono più facili da comprendere e più semplici da tradurre sia per i traduttori in carne e ossa che automatici.
- Non interrompere i passaggi delle procedure con commenti o digressioni.
- Includere le parole "seguente" o "indicato di seguito" in ogni frase che precede un elenco o un frammento di codice.
- Per i passaggi che includono frammenti di codice, inserire altre informazioni sul passaggio all'interno del codice sotto forma di commenti. 
    - In questo modo si riduce la quantità di testo che gli utenti dovranno leggere. 
    - Copiare le informazioni chiave nel progetto del codice per ricordare le operazioni eseguite dal codice stesso quando vi si fa riferimento in seguito.

## Guida generale per Markdown
- Per suggerimenti generali su Markdown, vedere la pagina di [nozioni di base su Markdown](https://help.github.com/articles/markdown-basics/) nel sito Web Github.
- È inoltre possibile scaricare il [foglio riassuntivo di Markdown per EMS](./media/ems-markdown-cheat-sheet.pdf?raw=true). 
- Se è necessario creare collegamenti incrociati in Markdown nell'articolo, vedere le [indicazioni sui collegamenti](#guidelines-for-linking-technical-articles) più avanti.
- Il sito Web <span style="color:red;">Verificare l'URL</span> http://docs.microsoft.com/ems supporta i [blocchi di codice delimitati](https://help.github.com/articles/creating-and-highlighting-code-blocks/#fenced-code-blocks). I blocchi di codice delimitati si creano inserendo una riga di 3 caratteri backquote (```) nella riga precedente e in quella successiva al blocco di codice. Si tratta di un modo pratico per disattivare il codice dal resto del testo.   
- EMS supporta inoltre [l'evidenziazione della sintassi](https://help.github.com/articles/creating-and-highlighting-code-blocks/#syntax-highlighting) all'interno dei blocchi di codice. Tuttavia, a differenza del Markdown di tipo GitHub, in cui [specificando una determinata lingua](https://help.github.com/articles/creating-and-highlighting-code-blocks/#syntax-highlighting) nella prima riga di codice si modifica la combinazione di colori della sintassi, EMS supporta **una sola** combinazione di colori di evidenziazione della sintassi, indipendentemente dal linguaggio di programmazione specificato.

## Creare immagini in Markdown
Seguendo la semplice sintassi Markdown è possibile inserire immagini all'interno degli articoli. 

### Creazione di una cartella di immagini e sintassi di collegamento

Per un nuovo articolo è necessario creare una cartella nel percorso seguente:
<span style="color:red;">Verificare il layout del repository degli articoli per le immagini</span>

    /articles/<service-directory>/media/

Ad esempio:
<span style="color:red;">Specificare un esempio</span>

    /articles/identity-access/media/

Dopo aver creato la cartella e aggiunto le immagini, usare la sintassi seguente per creare le immagini nell'articolo:

```
![Alt image text](./media/your-image-filename.png)
```

## Linee guida per le immagini specifiche per Enterprise Mobility Suite

Se non è possibile includere passaggi da riprodurre, sono consigliati gli screenshot. Scrivere il contenuto in modo che si possa fare a meno degli screenshot, se necessario.

Per la creazione e l'inserimento di file di grafica attenersi alle linee guida seguenti:
- Condividere file di grafica tra più documenti, se possibile. Copiare l'URL del file necessario e aggiungerlo all'articolo. 
- Il formato Portable Network Graphic (con estensione png) è di gran lunga preferito rispetto agli altri formati.
- Usare i quadrati rossi di larghezza predefinita, disponibili in Paint (5 px) per richiamare l'attenzione su determinati elementi nelle schermate.  

    Esempio:

    ![Esempio di un quadrato rosso usato come callout.](./media/gs13noauth.png)

- Evitare spazio vuoto sui bordi degli screenshot. Gli screenshot devono avere un bordo grigio di spessore pari a 1 pixel, in modo che le aree bianche dello screenshot non si confondano con la pagina Web.
    - Se si ritaglia uno screenshot in modo da lasciare sfondo bianco in corrispondenza dei bordi, aggiungere un bordo grigio di un unico pixel grigio intorno all'immagine.  
    - Se si usa Paint, usare il grigio più chiaro della tavolozza dei colori predefinita (#C3C3C3).
![Grigio per il bordo](./media/grey-border-in-paint.png)     
    - Se si usa un'app grafica che richiede valori RGB, i numeri di colore sono R195, G195, B195. 
- È possibile aggiungere facilmente un bordo grigio intorno a un'immagine in Visio. A tale scopo, eseguire l'operazione seguente: 
  - Selezionare l'immagine. 
  - Selezionare Linea e verificare che sia impostato il colore corretto. 
  - Modificare lo spessore della linea in 1 1/2 pt.  

    **Esempio:**

    ![Esempio di bordo grigio intorno a uno spazio vuoto.](./media/agent-700w.png)

- Per le immagini concettuali con spazio vuoto non è necessario un bordo grigio.  

    **Esempio:**

    ![Esempio di immagine concettuale con spazio vuoto e senza bordo grigio.](./media/ic727360.png)

- Non creare immagini troppo ampie. Se sono troppo ampie, le immagini vengono ridimensionate automaticamente. Se si ridimensiona un'immagine, tuttavia, questa talvolta diventa confusa. È quindi consigliabile limitare la larghezza delle immagini a <span style="color:red;">Verificare la larghezza massima delle immagini</span> 580 px e, se necessario, ridimensionare manualmente le immagini prima dell'invio.

- Visualizzare l'output dei comandi negli screenshot.  Se l'articolo include passaggi in cui l'utente deve usare una shell, è utile visualizzare l'output dei comandi negli screenshot. In questo caso, per avere la sicurezza di rimanere entro la larghezza indicata di <span style="color:red;">Verificare la larghezza massima delle immagini</span> 580 px, è in genere sufficiente limitare la larghezza della shell a circa 72 caratteri. Prima di acquisire uno screenshot dell'output, ridimensionare la finestra in modo da visualizzare solo i comandi e l'output pertinenti, facoltativamente con una riga vuota su un lato.
- Acquisire screenshot di finestre intere quando possibile. Quando si acquisisce uno screenshot di una finestra del browser, ridimensionarla a <span style="color:red;">Verificare la larghezza massima delle immagini</span> 580 pixel di larghezza al massimo e mantenere l'altezza della finestra del browser minore possibile, ma sufficiente per l'applicazione da visualizzare.

    Esempio:

    ![Esempio di screenshot di una finestra del browser.](./media/helloworldlocal.png)

- Prestare attenzione alle informazioni visualizzate all'interno degli screenshot, evitando di rivelare informazioni personali o aziendali interne.
- Nelle immagini concettuali o nei diagrammi usare le icone ufficiali nel set di simboli e icone del cloud e aziendali. Un set pubblico è disponibile all'indirizzo <span style="color:red;">Verificare l'effettivo uso di queste icone da parte di Microsoft</span> http://aka.ms/CnESymbols.


## Linee guida per il collegamento degli articoli tecnici

| Scenario di collegamento | Indicazioni per i collegamenti di destinazione  |
|---------------|-----------|
|Collegamento di un articolo tecnico EMS a un altro articolo tecnico EMS|Usare collegamenti relativi.|
|Collegamento a una pagina di EMS all'esterno della directory della documentazione, a un argomento di MSDN Library o della libreria TechNet oppure a un articolo della Knowledge Base|​Usare il collegamento effettivo all'articolo o all'argomento. Rimuovere l'impostazione locale en-us dal collegamento.|
|Collegamento di un articolo su EMS a qualsiasi altra pagina Web|Usare il collegamento diretto|

### Usare testo discorsivo per il collegamento

Le parole incluse in un collegamento devono essere discorsive, ovvero devono essere parole italiane di uso comune o il titolo della pagina di destinazione del collegamento. Non usare "Fare clic qui". Non è corretto per l'ottimizzazione motore di ricerca e non descrive la destinazione in modo adeguato.

**Corretto:**
<span style="color:red;">Verificare l'URL della guida del collaboratore</span> 
- `For more information, see the [contributor guide index](https://github.com/Microsoft/EMDocs/contributor-guide/contributor-guide-index.md).`

- `For more details, see the [SET TRANSACTION ISOLATION LEVEL](https://msdn.microsoft.com/library/ms173763.aspx) reference.`

**Non corretto:**

- `For more details, see [https://msdn.microsoft.com/library/ms173763.aspx](https://msdn.microsoft.com/library/ms173763.aspx).`

<span style="color:red;">Verificare l'URL della guida del collaboratore</span> 
- `For more information, click [here](https://github.com/Microsoft/EMDocs/contributor-guide/contributor-guide-index.md).`

### Sintassi Markdown per i collegamenti relativi EMS
<span style="color:red;">Verificare l'intero schema dei collegamenti</span> 

Per creare un collegamento incorporato da un articolo tecnico EMS a un altro articolo tecnico EMS, usare questo formato. Se si creano nuovi collegamenti verso o da articoli nelle directory, è necessario seguire la nuova sintassi di collegamento.

Collegamenti da un articolo di una sottodirectory a un articolo nella directory radice:

    [link text](../article-name.md)

Collegamenti da un articolo nella directory radice a un articolo in una sottodirectory del servizio: 
<span style="color:red;">Gli articoli sono organizzati in sottodirectory dei servizi?</span>

    [link text](service-directory/article-name.md)

Collegamenti da un articolo in una sottodirectory del servizio a un articolo in un'altra sottodirectory del servizio:

    [link text](../service-directory/article-name.md)
 
Collegamenti da un articolo in una directory a un altro articolo nella stessa directory:

    [link text](article-name.md)


Non è più necessario creare ancoraggi. Questi vengono generati automaticamente al momento della pubblicazione per tutte le intestazioni H2. L'unica cosa da fare è creare collegamenti alle sezioni H2:
<span style="color:red;">La metodologia di collegamento degli ancoraggi deve essere confermata</span>

    [link](#the-text-of-the-H2-section-separated-by-hyphens)
    [Create cache](#create-cache)

Per creare un collegamento a un ancoraggio in un altro articolo nella stessa sottodirectory:

    [link text](article-name.md#anchor-name)
    [Configure your profile](media-services-create-account.md#configure-your-profile)

Per creare un collegamento a un ancoraggio in un'altra sottodirectory del servizio:

    [link text](service-directory/article-name.md#anchor-name)
    [Configure your profile](service-directory/media-services-create-account.md#configure-your-profile)


## Sintassi Markdown per i collegamenti personalizzata
<span style="color:red;">Verificare la metodologia di collegamento e l'uso dei selettori.</span>

Poiché i file di inclusione si trovano in un'altra directory, è necessario usare percorsi relativi, come indicato di seguito. Per un collegamento a un solo articolo da un file di inclusione, usare questo formato:

    [link text](../articles/service-folder/article-name.md)
    
Altre informazioni su come usare un file di inclusione nelle [linee guida per le estensioni Markdown personalizzate](custom-markdown-extensions.md#includes).

Se in un file di inclusione sono incorporati selettori, usare collegamenti di questo tipo: 

    > [EMS.SELECTOR-LIST (Dropdown1 | Dropdown2)]
    - [(Text1 | Example1 )](../articles/service-folder/article-name1.md)
    - [(Text1 | Example2 )](../articles/service-folder/article-name2.md)
    - [(Text2 | Example3 )](../articles/service-folder/article-name3.md)
    - [(Text2 | Example4 )](../articles/service-folder/article-name4.md)

Per creare un collegamento a una pagina in EMS, ad esempio a una pagina relativa ai prezzi, a un contratto di servizio o a qualsiasi altro articolo diverso da un articolo di documentazione, usare un URL assoluto, omettendo l'impostazione locale *en-us*. L'obiettivo è che il collegamento funzioni in GitHub e nel sito visualizzato:

    [link text](https://www.microsoft.com/server-cloud/enterprise-mobility/pricing.aspx)

Per testare i collegamenti, eseguire il push della pagina nel fork, visualizzarne il rendering e pubblicarla in Sandbox. I collegamenti incrociati nella versione di GitHub della pagina funzionano a condizione che le destinazioni degli URL siano presenti nel ramo.

## Collegamenti con stile di riferimento

È possibile usare collegamenti con stile di riferimento per rendere il contenuto di origine più leggibile. I collegamenti con stile di riferimento sostituiscono la sintassi in linea con una sintassi semplificata che consente di spostare gli URL lunghi alla fine dell'articolo. Ecco un esempio in Daring Fireball:

Testo inline:

    I get 10 times more traffic from [Google][1] than from [Yahoo][2] or [MSN][3].

Riferimenti dei collegamenti alla fine dell'articolo:

    <!--Reference links in article-->
    [1]: http://google.com/
    [2]: http://search.yahoo.com/  
    [3]: http://search.msn.com/


## Torna alla pagina iniziale

- [Articolo di panoramica](./../README.md)
- [Indice degli articoli del materiale sussidiario](./contributor-guide-index.md)



<!--HONumber=Mar16_HO1-->


