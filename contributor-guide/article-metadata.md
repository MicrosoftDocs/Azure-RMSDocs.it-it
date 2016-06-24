<properties pageTitle="Metadati per gli articoli tecnici di Enterprise Mobility Suite" description="Descrive i metadati necessari per gli articoli." metaKeywords="" services="" solutions="" documentationCenter="" authors="v-jocgar" videoId="" scriptId="" manager="required" />

<tags ms.service="contributor-guide" ms.devlang="" ms.topic="article" ms.tgt_pltfrm="" ms.workload="" ms.date="02/24/2016" ms.author="v-jocgar" />

# Metadati per gli articoli tecnici di Enterprise Mobility Suite

Attività: 
- [ ] #11 Verificare che le istruzioni per ogni proprietà siano corrette.
- [ ] #12 Verificare l'URL nella sezione Properties:Description.
- [ ] #13 Aggiornare l'elenco dei servizi e l'elenco dei valori dei servizi ms (vedere il messaggio di posta elettronica di RobMazz n. 3 del 18-02-2016).
- [ ] #14 Verificare l'URL nella sezione Properties:Tags (posizione degli articoli EMS).
- [ ] #15 Verificare il breve elenco (3) di tag facoltativi in Properties:Tags. È necessario inserire più tag? 
- [ ] #16 Verificare l'elenco dei servizi nella sezione Tags:ms-services.
- [ ] #17 Aggiornare l'elenco dei tipi di articolo (tipi di risorsa) nella sezione Tags:mstopic (messaggio di posta elettronica di RobMazz n. 1 del 18-02-2016).
- [ ] #18 Aggiornare e approvare l'elenco dei linguaggi di programmazione nella sezione Tags:ms.devlang (messaggio di posta elettronica di RobMazz n. 4 del 18-02-2016).
- [ ] #19 Verificare l'elenco delle piattaforme di destinazione nella sezione Tags:ms.tgt_pltfrm (messaggio di posta elettronica di RobMazz n. 2 del 18-02-2016).
- [ ] #20 Verificare che tutti i collegamenti, in particolare gli ancoraggi, funzionino correttamente. 

Tutti gli articoli tecnici EMS contengono due sezioni di metadati: una sezione Properties e una sezione Tags. La sezione Properties abilita parte dell'automazione del sito Web e alcuni elementi SEO, mentre la sezione Tags abilita molte delle attività di reporting dei contenuti interni. Entrambe le sezioni sono obbligatorie.

- [Syntax]
- [Usage]
- [Attributes and values for the properties section]
- [Attributes and values for the tags section]

## Sintassi

La sezione Properties usa la sintassi seguente:

    <properties
       pageTitle="Page title that displays in search results and the browser tab | Microsoft EMS"
       description="Article description that will be displayed on landing pages and in most search results"
       services="service-name"
       documentationCenter="dev-center-name"
       authors="GitHub-alias-of-only-one-author"
       manager="manager-alias"
       editor=""
       tags="optional"
       keywords="Separate terms with commas. Check with your SEO champ before you change content in this article containing these terms."/>

La sezione Tags usa la sintassi seguente:

    <tags
       ms.service="required"
       ms.devlang="may be required"
       ms.topic="article"
       ms.tgt_pltfrm="may be required"
       ms.workload="na"
       ms.date="mm/dd/yyyy"
       ms.author="Your MSFT alias or your full email address;semicolon separates two or more"/>

## Utilizzo

- Nel nome dell'elemento e nei nomi degli attributi viene fatta distinzione tra maiuscole e minuscole.
- La sezione Properties deve essere la prima riga del file.
- Lasciare una riga vuota dopo ogni sezione di metadati e prima del titolo della pagina per assicurarsi che il titolo della pagina venga convertito correttamente in HTML durante il processo di pubblicazione.

## Attributi e valori della sezione Properties

![](./media/checkmark-small.png)**pageTitle**: obbligatorio; importante per SEO. Il testo di questo attributo viene visualizzato nella scheda del browser e come titolo nei risultati di ricerca. Usare 55-60 caratteri, inclusi gli spazi e l'identificatore del sito *| EMS Microsoft * (digitato come: spazio barra verticale spazio EMS Microsoft).  pageTitle deve essere diverso da H1.

![](./media/checkmark-small.png)**description**: obbligatorio; importante per SEO (rilevanza) e la funzionalità del sito. description deve avere una lunghezza compresa tra 125 e 155 caratteri, inclusi gli spazi. Descrivere la finalità del contenuto per consentire ai clienti di scegliere da un elenco di risultati di ricerca. Il valore è:

- Questo testo può essere visualizzato come descrizione o sommario nei risultati della ricerca in Google.
- Questo testo viene visualizzato in <span style="color:red;">Confirm URL</span> [i risultati dell'indice dell'articolo](http://docs.microsoft.com/ems/articles/).

![](./media/checkmark-small.png)**services**: obbligatorio per gli articoli relativi a un servizio. Questo valore è spesso chiamato "slug del servizio". Creare un elenco di tutti i servizi disponibili, separati da virgole. Il primo servizio dell'elenco determinerà i percorsi di navigazione della pagina e il riquadro di spostamento visualizzato con la pagina.

Negli articoli che specificano sia un valore services sia un valore documentationCenter, il valore services determinerà la navigazione. Gli altri valori inclusi nell'elenco verranno visualizzati come tag nell'articolo pubblicato. Valori possibili:

- active-directory
- active-directory-b2c
- active-directory-ds
- app-service-api
- api-management
- app-service
- app-service-mobile
- app-service-web
- application-gateway
- application-insights
- automazione
- backup
- batch
- best-practice
- fatturazione
- biztalk-services
- cache
- cdn
- cloud-services
- data-catalog
- data-factory
- data-lake-analytics
- data-lake-store
- devtest-lab
- dns
- documentdb
- expressroute
- event-hubs
- hdinsight
- iot-hub
- key-vault
- load-balancer
- machine-learning
- marketplace
- media-services
- mobile-engagement
- mobile-services
- multi-factor-authentication
- notification-hubs
- operational-insights
- operations-management-suite
- powerapps
- recovery-manager
- redis-cache
- remoteapp
- rights-management
- utilità di pianificazione
- cerca
- security-center
- service-bus
- service-fabric
- site-recovery
- sql-database
- sql-data-warehouse
- sql-reporting
- archiviazione
- store
- storsimple
- stream-analytics
- traffic-manager
- virtual-machines
- virtual-network
- visual-studio-online
- vpn-gateway
- web-sites

![](./media/checkmark-small.png)**documentationCenter**: obbligatorio per gli articoli dev-centric pubblicati in modo ottimale attraverso un Dev Center. Specificare il singolo Dev Center o la lingua che si applica all'articolo. Il valore specificato determinerà i percorsi di navigazione della pagina. Negli articoli che specificano sia un valore services sia un valore documentationCenter, il valore services determinerà la navigazione. Valori possibili:

- **.net**
- **nodejs**
- **java**
- **php**
- **python**
- **ruby**
- **mobile**: obsoleto. Sostituire con la piattaforma mobile specifica.
- **ios**: valore nuovo in corso di verifica
- **android**: valore nuovo in corso di verifica
- **windows**: valore nuovo in corso di verifica
- **xamarin**: valore nuovo in corso di verifica

![](./media/checkmark-small.png)**authors**: obbligatorio, specificare un solo valore. Visualizza l'account GitHub dell'autore principale o SME dell'articolo. Questo attributo determina la riga autore dell'articolo pubblicato. Visualizza un solo autore, nonostante la forma plurale del nome dell'attributo.

![](./media/checkmark-small.png)**manager**: obbligatorio per i collaboratori Microsoft. Visualizza l'alias e-mail del responsabile della pubblicazione del contenuto per l'area tecnologica. Se si è un collaboratore della community, includere l'attributo ma lasciarlo vuoto per consentire la compilazione automatica.

![](./media/checkmark-small.png)**editor**: non usato. Non usarlo per altre finalità.

![](./media/checkmark-small.png)**tags**: facoltativo. Includere solo se si vuole abilitare un collegamento sotto il percorso di navigazione dell'articolo per la pagina di indice <span style="color:red;">Confirm URL</span> (http://docs.microsoft.com/ems/articles/) a un elenco di articoli prefiltrato corrispondente a uno dei valori approvati. Questi valori sono progettati per consentire di riunire il contenuto quando il raggruppamento del contenuto non è specifico del servizio. Questi tag possono anche specificare un'etichetta che indica lo stack di tecnologie a cui si applica l'articolo. Questo valore **non** supporta i tag freeform o hashtag. I tag devono essere abilitati nel sito. È possibile specificare più valori di tag in un articolo, separati da virgole. I valori approvati sono:

<span style="color:red;">Verificare i valori dei tag</span>
  - esistente
  - fatturazione
  - mysql

![](./media/checkmark-small.png)**keywords**: facoltativo. A uso esclusivo di SEO champ. Separare i termini con virgole. **Prima di modificare o eliminare il contenuto di questo articolo contenente tali termini, rivolgersi al proprio SEO champ.** Questo attributo registra le parole chiave configurate come target e registrate dal SEO champ allo scopo di migliorare la classificazione delle ricerche. Il rendering delle parole chiave non viene eseguito nell'HTML pubblicato. La convalida non richiede questo attributo.

## Attributi e valori della sezione Tags

![](./media/checkmark-small.png)**ms.service**: obbligatorio. Specifica il servizio, lo strumento o la funzionalità a cui si applica l'articolo. Un solo valore per pagina.

 Se una pagina si applica a più servizi, scegliere il servizio a cui si applica più direttamente. Ad esempio, un articolo che usa un'app ospitata in siti Web per illustrare la funzionalità del bus di servizio dovrà includere il valore **service-bus** anziché il valore **web-sites**. Se una pagina si applica equamente a più servizi, scegliere **multiple**. Nel caso raro in cui una pagina non si applica ad alcun servizio, scegliere **NA**.

<span style="color:red;">Verificare questi valori.</span>
 - **active-directory**
 - **api-management**
 - **app-service**: si applica soltanto al materiale concettuale generale del servizio app
 - **app-service-api**
 - **app-service-logic**
 - **app-service-mobile**
 - **app-service-web**
 - **application-insights**
 - **automazione**
 - **backup**
 - **batch**
 - **biztalk-services**
 - **fatturazione**
 - **cache**
 - **cdn**
 - **cloud-services**
 - **expressroute**
 - **hdinsight**
 - **iot-hub**
 - **key-vault**
 - **machine-learning**
 - **media-services**
 - **mobile-engagement**
 - **mobile-services**
 - **multi-factor-authentication**
 - **multiple**: la pagina si applica equamente a più servizi
 - **na**: la pagina non si applica ad alcun servizio (raro)
 - **notification-hubs**
 - **operational-insights**
 - **powerapps**
 - **recovery-manager**
 - **redis-cache**
 - **remoteapp**
 - **rights-management**
 - **utilità di pianificazione**
 - **service-bus**
 - **service-fabric**
 - **site-recovery**: in precedenza recovery-services
 - **sql-database**
 - **sql-data-warehouse**
 - **sql-reporting**
 - **archiviazione**
 - **storsimple**
 - **traffic-manager**
 - **virtual-machines**
 - **virtual-network**
 - **visual-studio-online**
 - **vpn-gateway**
 - **web-sites**

![](./media/checkmark-small.png)**ms.devlang**: obbligatorio. Specifica il linguaggio di programmazione a cui si applica l'articolo. Un solo valore per pagina.

 Se una pagina si applica equamente a due linguaggi di programmazione, scegliere **multiple**. Se una pagina è principalmente concettuale e il relativo contenuto è applicabile a più linguaggi di programmazione, scegliere **multiple**. Se una pagina non è indirizzata agli sviluppatori e l'applicabilità a un linguaggio di programmazione non è rilevante, scegliere **NA**. Usare **rest-api** per identificare gli argomenti di riferimento dell'API REST.

<span style="color:red;">Verificare questi valori</span>
 - **cpp**
 - **dotnet**
 - **java**
 - **javascript**
 - **multiple**: la pagina si applica equamente a più linguaggi di programmazione.
 - **na**: la pagina non è indirizzata agli sviluppatori e non è specifica di alcun linguaggio di programmazione.
 - **nodejs**
 - **objective-c**
 - **php**
 - **python**
 - **rest-api**
 - **ruby**


![](./media/checkmark-small.png)**ms.topic**: obbligatorio. Specifica il tipo di argomento. La maggior parte delle pagine create dai collaboratori sono articoli o riferimenti.

<span style="color:red;">Verificare questi valori</span>
 - **article**: argomento concettuale, esercitazione, guida alle funzioni o altro articolo non riferimento

 - **get-started-article**: da assegnare agli articoli pubblicati nella sezione Guida introduttiva del riquadro di navigazione sinistro per un servizio.

 - **hero-article**: esercitazione progettata per presentare un servizio o una funzionalità che offre ai visitatori una breve introduzione all'uso del servizio e promuove registrazioni di prova gratuite e attivazioni MSDN. Assegnare questo valore SOLO agli articoli disponibili nella parte superiore della pagina di destinazione della documentazione del servizio.

 - **reference**: pagina di riferimento di un'API, inclusa l'API REST, o pagina di riferimento di un cmdlet PowerShell

![](./media/checkmark-small.png)**ms.tgt_pltfrm**: obbligatorio. Specifica la piattaforma di destinazione, ad esempio Windows, Linux, Windows Phone, iOS, Android o piattaforme cache speciali. Un solo valore per pagina. Questo valore sarà **NA** per la maggior parte degli argomenti, ad eccezione delle macchine virtuali e dei dispositivi mobili.

<span style="color:red;">Verificare questi valori</span>
 - **cache-in-role**
 - **cache-multiple**
 - **cache-redis**
 - **cache-service**
 - **cache-shared**
 - **command-line-interface**
 - **ibiza**: contenuto che usa il portale Ibiza. Usare solo nei casi in cui la funzionalità descritta è disponibile sia attraverso il portale Ibiza sia attraverso il portale corrente.
 - **mobile-android** 
 - **mobile-html**
 - **mobile-ios**
 - **mobile-kindle**
 - **mobile-multiple**
 - **mobile-nokia-x**
 - **mobile-phonegap**
 - **mobile-sencha**
 - **mobile-windows**
 - **mobile-windows-phone**
 - **mobile-windows-store**
 - **mobile-xamarin**
 - **mobile-xamarin-android**
 - **mobile-xamarin-ios**
 - **multiple**: la pagina si applica equamente a più piattaforme
 - **na**: per la pagina non è applicabile alcun identificatore di piattaforma
 - **powershell**
 - **vm-linux**
 - **vm-multiple**
 - **vm-windows**
 - **vm-windows-sharepoint**
 - **vm-windows-sql-server**
 - **vs-getting-started**: identifica il gruppo di pagine della Guida introduttiva VS. Tag aggiunto: 12/1/14.
 - **vs-what-happened**: identifica la pagina di informazioni sull'evento della Guida introduttiva VS. Tag aggiunto: 12/1/14.

![](./media/checkmark-small.png)**ms.workload**: obbligatorio. Specifica il carico di lavoro a cui si applica la pagina. Un solo valore per articolo. 

![](./media/checkmark-small.png) **ms.date**: obbligatorio. Specifica la data dell'ultima revisione dell'articolo relativa a pertinenza, accuratezza, correttezza degli screenshot e funzionamento dei collegamenti. Immettere la data nel formato mm/gg/aaaa. La data viene visualizzata anche nell'articolo pubblicato come data dell'ultimo aggiornamento.

![](./media/checkmark-small.png) **ms.author**: obbligatorio. Specifica l'autore o gli autori associati all'argomento. Per specificare più valori è necessario separarli con punti e virgola. Alias Microsoft o indirizzi di posta elettronica completi sono validi. La lunghezza non può superare i 200 caratteri.

## Torna alla pagina iniziale

- [Articolo di panoramica](./../README.md)
- [Indice degli articoli del materiale sussidiario](./contributor-guide-index.md)


<!--Anchors-->
[Syntax]: #syntax
[Usage]: #usage
[Attributes and values for the properties section]: #attributes-and-values-for-the-properties-section
[Attributes and values for the tags section]: #attributes-and-values-for-the-tags-section


<!--HONumber=Mar16_HO1-->


