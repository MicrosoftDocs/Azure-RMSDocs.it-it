---
# required metadata

title: [TITOLO DELL'ARTICOLO | NOME DEL SERVIZIO]
description:
keywords:
author: [GITHUB USERNAME]
manager: [ALIAS]
ms.date: 04/28/2016
ms.topic: article
ms.prod:
ms.service:
ms.technology:
ms.assetid: [GET ONE FROM guidgenerator.com]

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
#ms.reviewer: [ALIAS]
#ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# I metadati e il modello markdown

Questo modello docs.ms contiene esempi di sintassi markdown, nonché indicazioni su come impostare i metadati. È disponibile nella directory principale di ogni repository EM pilota (ad esempio ~/Azure-RMSDocs-pr
/ template.md) e deve essere letto come un file markdown, anche se è possibile fare riferimento [alla versione pubblicata](https://stage.docs.microsoft.com/en-us/rights-management/template) per vedere come l'esempio di markdown viene reso.

Quando si crea un file markdown, è necessario copiare il modello in un nuovo file, compilare i metadati come specificato di seguito, impostare l'intestazione H1 sopra il titolo dell'articolo ed eliminare il contenuto. 


## Metadati 

Il blocco di metadati completo è riportato qui sopra, suddiviso nei campi obbligatori e facoltativi; vedere il [foglio riassuntivo dei metadati OPS](https://ppe.msdn.microsoft.com/en-us/ce-csi-docs/ops/ops-onboarding/managing-content/content-meta-data) per ulteriori dettagli. Alcune note importanti:

- È **necessario** inserire uno spazio tra i due punti (:) e il valore di un elemento dei metadati.
- Se un elemento facoltativo dei metadati non ha un valore, impostare come commento il simbolo # (non lasciare vuoto oppure usare "na"); se si aggiunge un valore a un elemento che è stato commentato, assicurarsi di rimuovere il simbolo #.
- I due punti in un valore (ad esempio, un titolo) interrompono il parser di metadati. Al loro posto, utilizzare la codifica HTML di & #58; (ad esempio, "titolo: Azure Rights Management & #58; nozioni di base | Azure RMS").
- **titolo**: questo titolo verrà visualizzato nei risultati dei motori di ricerca. Il titolo deve terminare con una barra verticale (|) seguita dal nome del servizio (ad esempio, vedere sopra). Non è necessario che il titolo debba essere identico al titolo dell'intestazione H1 (e probabilmente non deve esserlo). Deve includere approssimativamente 65 caratteri (compreso | NOME DEL SERVIZIO)
- **autore**, **manager**, **revisore**: il campo dell'autore deve contenere il **nome utente Github** dell'autore, non il relativo alias.  I campi "manager" e "revisore", al contratio, devono contenere gli alias. ms.reviewer specifica il nome del PM associato all'articolo o servizio.
- **ms.assetid**: si tratta del GUID dell'articolo da CAPS. Quando si crea un nuovo file markdown, ottenere un GUID da [https://www.guidgenerator.com](https://www.guidgenerator.com). 
- **ms.Prod**, **ms.service**, **ms.technology**, **ms.devlang**, **ms.topic**, **ms.tgt_pltfrm**: i valori possibili per questi elementi sono reperibili [qui](https://microsoft.sharepoint.com/teams/STBCSI/Insights/_layouts/15/WopiFrame.aspx?sourcedoc=%7b7A321BF1-0611-4184-84DA-A0E964C435FA%7d&file=WEDCS_MasterList_CSIValues.xlsx&action=default).

## GFM e markdown base

Sono supportati tutti i markdown di base e per Github. Per ulteriori informazioni, vedere:

- [Sintassi di base dell markdown](https://daringfireball.net/projects/markdown/syntax)
- [Documentazione relativa al markdown di Github (GFM)](https://guides.github.com/features/mastering-markdown)

## Intestazioni

Esempi di intestazioni di primo e secondo livello sono riportati qui sopra. 

Vi **deve** essere solo un'intestazione di primo livello all'argomento, che verrà visualizzata come titolo nella pagina.  

Le intestazioni di secondo livello generano il sommario della pagina che viene visualizzata nella sezione "In questo articolo" sotto il titolo della pagina.

### Intestazione di terzo livello
#### Intestazione di quarto livello
##### Intestazione di quinto livello
###### Intestazione di sesto livello

## Stile di testo

*corsivo* 

**Grassetto** 

~~barrato~~



## Links

Per collegare un file markdown nello stesso repository, usare i [relativi collegamenti](https://www.w3.org/TR/WD-html40-970917/htmlweb.html#h-5.1.2). 

- Esempio: [Informazioni su Microsoft Azure Rights Management](./understand-explore/what-is-azure-rms.md)

Per creare un collegamento a un'intestazione nello stesso file markdown, visualizzare l'origine dell'articolo pubblicato, trovare l'id dell'intestazione (ad esempio `id="blockquote"`) e il collegamento utilizzando # + id (ad esempio `#blockquote`).

- Esempio: [Blockquotes](#blockquote)

Per creare un collegamento a un'intestazione in un file markdown nello stesso repository, usare i relativi collegamenti + hashtag.

- Esempio: [panoramica tecnica del processo di registrazione](./understand-explore/rms-for-individuals-user-sign-up.md#technical-overview-of-the-sign-up-process)

Per creare un collegamento a un file esterno, usare l'URL completo come collegamento.

- Esempio: [Github](http://www.github.com)

Se viene visualizzato un URL in un file markdown, questo verrà trasformato in un collegamento ipertestuale.

- Esempio: http://www.github.com

## Elenchi

### Elenchi ordinati

1. Questo parametro 
1. è
1. un
1. Ordinato
1. Elenco  


#### Elenco ordinato con un elenco incorporato

1. qui
1. viene fornito
1. un
1. incorporato
    1. Miss Scarlett
    1. Professore Plum
1. ordinato
1. list


### Elenchi non ordinati

- Questo parametro
- is
- a
- elenco puntato
- list


##### Elenco non ordinato con elenchi incorporati

- Questo parametro 
- elenco puntato 
- list
    - Mrs. Peacock
    - Mr. Green
- contains  
- other
    1. Senape Colonel
    1. Mrs. White
- elenchi


## Regola orizzontale

---

## Tabelle

| Tabelle        | Sono           | Interessanti  |
| ------------- |:-------------:| -----:|
| la colonna 3 è      | allineata a destra | $1600 |
| la colonna 2 è      | centrata      |   $12 |
| la colonna 1 è allineata a sinistra | per impostazione predefinita     |    $1 |


## Codice

### Codeblock

    function fancyAlert(arg) {
      if(arg) {
        $.docs({div:'#foo'})
      }
    }

### Codice in linea

Questo è un esempio di `in-line code`.

## Blockquotes

> La siccità è durata per dieci milioni di anni e il regno dei terribili serpenti è terminato da allora. Qui sull'equatore, nel continente che un giorno sarà noto come Africa, la battaglia per l'esistenza ha raggiunto un nuovo apice di ferocia, e la vittoria è ancora lontana. In questa terra arida e secca, solo gli organismi più piccoli o rapidi o feroci possono progredire, o addirittura sperare di sopravvivere.

## Immagini

### Immagine statica

![questo è il testo alternativo](./media/AzRMS_elements.png)

### Immagine collegata

[![aTesto informatico per l'immagine collegata](./media/AzRMS_elements.png)](https://azure.microsoft.com) 

### Gif animata

![gif animata](./media/hololens.gif)

## Avvisi

### Nota

> [!NOTE]
> Questo è NOTA

### Avviso

> [!WARNING]
> Questo è AVVISO

### Suggerimento

> [!TIP]
> Questo è SUGGERIMENTO

### Importante

> [!IMPORTANT]
> Questo è IMPORTANTE

## Video

### Channel 9

<iframe src="http://channel9.msdn.com/Series/Azure-Active-Directory-Videos-Demos/Azure-Active-Directory-Connect-Express-Settings/player" width="960" height="540" allowFullScreen frameBorder="0"></iframe>


### Youtube

<iframe width="420" height="315" src="https://www.youtube.com/embed/R6_eWWfNB54" frameborder="0" allowfullscreen></iframe>

## estensioni docs.ms

### Pulsante

> [!div class="button"]
[collegamenti al pulsante](/rights-management)

### Selettore

> [!div class="op_single_selector"]
- [foo](/rights-management/template.md)
- [barra](/rights-management/scratch.md)

### Procedura dettagliata

>[!div class="step-by-step"]
[Indietro](https://www.example.com)
[Avanti](https://www.example.com)

<!--HONumber=Apr16_HO3-->


