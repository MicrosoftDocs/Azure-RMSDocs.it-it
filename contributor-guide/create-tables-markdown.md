<properties title="Create tables in markdown" pageTitle="Creare tabelle in markdown per gli articoli di EMS" description="Illustra come creare tabelle con la notazione markdown." metaKeywords="" services="" solutions="" documentationCenter="" authors="v-jocgar" videoId="" scriptId="" manager="robmazz" />

<tags ms.service="contributor-guide" ms.devlang="" ms.topic="article" ms.tgt_pltfrm="" ms.workload="" ms.date="02/26/2016" ms.author="v-jocgar" />

# Creare tabelle in markdown

Attività:
- [ ] #33 Aggiungere la sintassi della nota markdown personalizzata alla nota in basso.

Negli articoli, le tabelle vanno usate con cautela. Usarle solo se i dati sono realmente tabulari.

**Nota**
Le tabelle markdown hanno capacità limitate per la gestione delle stringhe di testo lunghe; il ritorno a capo in una cella di tabella non è previsto. La cella si espande fino alla larghezza massima del contenuto; di conseguenza la visualizzazione della tabella sugli schermi di piccole dimensioni può creare problemi. Usare le tabelle per set di informazioni ridotti e adottare altri metodi più pratici per visualizzare i set di contenuti più lunghi.

## Sintassi della tabella markdown
Il modo più semplice per creare una tabella in markdown è l'uso di caratteri barra verticale e trattini. Per far sì che ogni colonna includa l'intestazione della tabella, è necessario includere almeno 3 trattini nella seconda riga. Il testo dell'intestazione della tabella viene centrato e visualizzato in grassetto automaticamente.  

 ![1]

Il markdown visualizza automaticamente l'ombreggiatura alternata delle righe della tabella.  
 ![2]

È possibile giustificare le colonne mediante caratteri due punti:

  	|:-----|   - this is left aligned (default -- can be omitted)
  	|-----:|   - this is right aligned
  	|:-----:|  - this is centered

I caratteri barra verticale esterni sono facoltativi e non è necessario allineare perfettamente il testo e i caratteri barra verticale per ottenere la visualizzazione corretta della tabella. Questo esempio di formattazione rapida:

 ![3]

viene interpretato e visualizzato correttamente in markdown.  
 ![4]

Se si usano le tabelle HTML e il markdown non viene visualizzato correttamente tra le due tabelle, è necessario aggiungere un tag di chiusura BR dopo il tag di chiusura TABLE.

![5]

Per una soluzione semplice e rapida per la creazione di tabelle in markdown, provare il generatore di tabelle markdown: http://www.tablesgenerator.com/markdown_tables


## Torna alla pagina iniziale

- [Articolo di panoramica](./../README.md)
- [Indice di articoli di linee guida](./contributor-guide-index.md)

<!--image references-->
[1]: ./media/table-markdown-1.png
[2]: ./media/table-markdown-2.png
[3]: ./media/table-markdown-3.png
[4]: ./media/table-markdown-4.png
[5]: ./media/break-tables.png


<!--HONumber=Mar16_HO1-->


