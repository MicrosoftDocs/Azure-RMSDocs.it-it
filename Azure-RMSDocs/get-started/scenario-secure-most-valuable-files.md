---
title: "Scenario - Proteggere i file più importanti (few) | Azure RMS"
description: 
keywords: 
author: cabailey
manager: mbaldwin
ms.date: 05/20/2016
ms.topic: get-started-article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 95f1844a-612c-4e67-bbe6-4b6b92295221
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 332e102cb27854314b93a71bfeae82a95c9a7812
ms.openlocfilehash: d4325fb8a0b27d0a8d4fd7451b9d11d10153ed8d


---

# Scenario - Proteggere i file più importanti (few)

*Si applica a: Azure Rights Management, Office 365*

Questo scenario e la documentazione di supporto per l'utente usano Azure Rights Management per proteggere in modo manuale e personalizzato un numero limitato di file identificati come i più importanti, garantendo il massimo livello di protezione dall'accesso non autorizzato. In genere questi sono file a cui possono accedere solo alcuni utenti. Ad esempio, le istruzioni per la ricetta di un prodotto alimentare o i piani di acquisizione dell'azienda che non devono essere pubblici prima di una data specifica.

Le istruzioni sono adatte ai casi seguenti:

-   È stato identificato il piccolo set di file da proteggere.

-   I file si presentano in uno dei formati di file Office che supportano Rights Management. Se i file si presentano in altri formati di file (ad esempio CAD) verificare che questi formati supportano Azure RMS e distribuire le applicazioni che supportano in modo nativo Azure RMS. Per altre informazioni, vedere [Supporto di Azure Rights Management da parte delle applicazioni](https://technet.microsoft.com/library/jj585004.aspx).

-   I file contengono informazioni estremamente riservate e sensibili che devono essere accessibili solo ad alcuni utenti.

-   Richiedere una connessione Internet per autorizzare il singolo accesso a ogni file è un compromesso accettabile per questi utenti, poiché offre una maggiore sicurezza.

-   Queste persone non dispongono di un requisito per condividere le informazioni con altri utenti, ma possono modificare le informazioni e salvare le modifiche.

-   L'amministratore deve essere in grado di monitorare chi e quando accede ai file, revocando l'accesso se necessario.

## Istruzioni sulla distribuzione
![Istruzioni per l'amministratore per la distribuzione rapida di Azure RMS](../media/AzRMS_AdminBanner.png)

Verificare che siano soddisfatti i requisiti seguenti e quindi seguire le istruzioni per le procedure di supporto prima di passare alla documentazione dell'utente.

## Requisiti per questo scenario
Per questo scenario, sono necessari i requisiti seguenti:

|Requisito|Altre informazioni|
|---------------|--------------------------------|
|Definizione di account e gruppi per Office 365 o Azure Active Directory:<br /><br />- Un gruppo abilitato alla posta elettronica denominato **Accesso con privilegi** che include i pochi utenti che devono avere accesso a questi documenti riservati<br /><br />- Un gruppo abilitato alla posta elettronica denominato **Responsabili della conformità IT** che include gli utenti il cui compito include l'eDiscovery, il monitoraggio e il controllo<br /><br />- Un gruppo abilitato alla posta elettronica denominato **Amministratori RMS** e tutti gli amministratori che configurano Azure RMS membri di questo gruppo|[Preparazione per Azure Rights Management](https://technet.microsoft.com/library/jj585029.aspx)|
|Azure Rights Management non è attivato|[Attivazione di Azure Rights Management](https://technet.microsoft.com/library/jj658941.aspx)|
|Configurazione di un modello personalizzato, come descritto di seguito|[Configurazione di modelli personalizzati per Azure Rights Management](https://technet.microsoft.com/library/dn642472.aspx)|
|L'applicazione di condivisione Rights Management viene distribuita su un computer Windows, in modo che sia possibile proteggere questi file sul posto, come descritto nella sezione successiva|[Scaricare e installare l’applicazione di condivisione Rights Management](https://technet.microsoft.com/library/dn574734%28v=ws.10%29.aspx)|
|Gli utenti autorizzati dispongano di una versione minima di Office 2013|Se gli utenti dispongono di Office 2010, è necessario installare anche l'applicazione di condivisione Rights Management.|
|La sottoscrizione di Azure RMS include il rilevamento dei documenti|Se la sottoscrizione ad Azure RMS non include il monitoraggio e la revoca dei documenti, non sarà possibile accedere al sito di monitoraggio del documento per vedere chi accede al documento e revocarne l'accesso se necessario. In questo caso, acquistare una sottoscrizione che supporta il monitoraggio dei documenti o accettare questa limitazione. È opportuno considerare anche la funzionalità di [registrazione utilizzo](https://technet.microsoft.com/library/dn529121.aspx) di Azure RMS, che può fornire informazioni sugli utenti e sul momento in cui ogni file è stato consultato, per rilevare potenziali comportamenti sospetti.<br /><br />Per verificare il supporto della propria sottoscrizione: [Confronto tra le offerte di Rights Management Services (RMS)](https://technet.microsoft.com/dn858608)|

### Per configurare il modello personalizzato

1.  Nel portale classico di Azure: Creare un nuovo modello personalizzato per Azure Rights Management, contenente i valori e le impostazioni seguenti:

    -   Nome: **Accesso con privilegi**

    -   Diritti: concedere al gruppo abilitato per la posta elettronica con **Accesso con privilegi** diritti di **Coautore**

    -   Ambito: Selezionare i gruppi abilitati per la posta elettronica **Accesso con privilegi**, **Responsabili della conformità IT** e **Amministratori RMS**.

    -   Accesso offline: selezionare **Il contenuto è disponibile solo con una connessione a Internet**

2.  Pubblicare il nuovo modello.

### Per proteggere il file sul posto

1.  In Esplora File, passare alla prima cartella che contiene i file da proteggere:

    -   Se si desidera proteggere tutti i file nella cartella, selezionare la cartella.

    -   Se si desidera proteggere solo alcuni file nella cartella, selezionare tutti i file da proteggere.

2.  Pulsante destro del mouse, selezionare **Proteggi tramite RMS** e quindi selezionare **Proteggi sul posto**.

3.  Selezionare **Accesso con privilegi**.

4.  è possibile che vengano richieste le credenziali. Attendere che i file vengano protetti e quindi fare clic su **Chiudi** quando viene visualizzata la pagina che informa che **i file sono stati protetti**.

5.  Se si dispone di più file da proteggere in altre cartelle, ripetere i passaggi da 1 a 4 per ogni cartella.

Per altre informazioni sulla protezione dei file sul posto, vedere [Proteggere un file in un dispositivo (protezione sul posto) tramite l'applicazione di condivisione Rights Management](https://technet.microsoft.com/library/dn574733%28v=ws.10%29.aspx).

> [!TIP]
> Se il numero di file da proteggere è eccessivo per questo processo manuale, è consigliabile usare lo [strumento di protezione RMS](https://www.microsoft.com/en-us/download/details.aspx?id=47256) per proteggere i file in blocco tramite il modello.

### Per monitorare e, se necessario, revocare l'accesso ai file

1.  In Esplora file, fare clic con il pulsante destro del mouse sul file, selezionare **Proteggi tramite RMS** e quindi selezionare **Rileva utilizzo**:

2.  Se richiesto, accedere al sito di rilevamento del documento.

3.  Verificare chi ha eseguito l'accesso ai file protetti, prestando particolare attenzione ai tentativi non riusciti nel caso in cui indicano comportamenti sospetti. Se si ritiene utile, è possibile revocare l'accesso a ogni file.

## Istruzioni sulla documentazione per l'utente
Non sono disponibili istruzioni specifiche per gli utenti relative a questo scenario, in quanto questi file non richiedono alcuna azione particolare da parte degli utenti. I file sono stati protetti da parte dell'utente e verranno monitorati dall'utente. Tuttavia, può essere necessario informare gli utenti e i canali di supporto su quali siano i file protetti e su come limitare l'uso dei documenti. Ad esempio, se un utente autorizzato non dispone di connessione a Internet, non sarà in grado di aprire il file.

Usando il modello seguente, copiare e incollare l'annuncio in una comunicazione per gli utenti finali e apportare tali modifiche:

1.  Specificare i nomi effettivi dei file o usare un riferimento chiaro comprensibile da parete degli utenti autorizzati.

2.  Sostituire *&lt;dettagli contatto&gt;* con le istruzioni sulla modalità in cui gli utenti possono contattare il supporto tecnico o il reparto IT con un canale di supporto in base all'importanza di questi documenti. Ad esempio, fornire un numero di telefono disponibile 24 ore per le chiamate al supporto di importanza elevata.

3.  Apportare altre eventuali modifiche a questo annuncio e quindi inviarlo agli utenti.

La documentazione dell'esempio mostra come questo annuncio viene visualizzato dagli utenti, dopo le personalizzazioni.

![Documentazione dell'utente del modello per la distribuzione rapida di Azure RMS](../media/AzRMS_UsersBanner.png)

### Annuncio IT: protezione dei documenti top secret di &lt;nome organizzazione&gt;
Poiché i file seguenti dispongono di un elevato livello di protezione, solo gli &lt;utenti con restrizioni&gt; possono accedere e modificare i file. Per proteggere questi file da accessi non autorizzati, l'applicazione richiederà automaticamente di proteggere i file ogni volta che vengono aperti, in modo che non sia necessaria una connessione Internet per accedervi e potrebbe essere richiesto di immettere le credenziali:

-   &lt;documento, tipo o posizione top secret 1&gt;

-   &lt;documento, tipo o posizione top secret 2&gt;

-   &lt;documento, tipo o posizione top secret 3&gt;

**Serve assistenza?**

-   Se non è possibile accedere a questi file o se si notano modifiche sospette nei file, &lt;azione e dettagli contatto&gt;.

#### Esempio di documentazione personalizzata per l'utente
![Esempio di documentazione dell'utente per la distribuzione rapida di Azure RMS](../media/AzRMS_ExampleBanner.png)

##### Annuncio IT: Protezione dei documenti top secret di VanArsdel
I seguenti file dispongono di un elevato livello di protezione, in modo che solo le persone nella riga A del messaggio di posta elettronica possano accedere e modificare questi file. Per proteggere questi file da accessi non autorizzati, le applicazioni richiederanno automaticamente di proteggere i file ogni volta che vengono aperti, in modo che non sia necessaria una connessione Internet per aprirli e potrebbe essere richiesto di immettere le credenziali:

-   Specifiche di progettazione per il nome in codice "Mercury"

-   Specifiche di progettazione per il nome in codice "Jupiter"

-   Specifiche di progettazione per il nome in codice "Saturn"

-   Specifiche di progettazione per il nome in codice "Neptune"

**Serve assistenza?**

-   Se non è possibile accedere a questi file o se si notano modifiche sospette, chiamare la linea di supporto aperta 24 ore che è stata inviata all'utente dal reparto IT tramite un messaggio di posta elettronica protetto.




<!--HONumber=Jul16_HO3-->


