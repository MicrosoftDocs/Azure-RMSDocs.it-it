---
title: Esercitazione introduttiva, passaggio 5 | Azure Information Protection
description: Passaggio 5 dell'esercitazione introduttiva che consente di provare rapidamente Microsoft Azure Information Protection nell'organizzazione. L'esecuzione dell'esercitazione richiede circa 30 minuti.
keywords: 
author: cabailey
manager: mbaldwin
ms.date: 09/25/2016
ms.topic: get-started-article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 4e59a3b3-f0f4-4535-8b96-cac68303d855
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 1af9f3b3451bf8ceafbaf3cddd2b26c37fe9d597
ms.openlocfilehash: d607c19d37da6b6fb23513067e9e30f33f0260de


---


# Passaggio 5: Vedere in azione la condivisione di file protetti e tenere traccia del documento 

>*Si applica a: Azure Information Protection*

Per questo passaggio finale dell'esercitazione, individuare un documento di Word già creato da inviare a un partner o a un collaboratore. Ai fini di questa esercitazione non è importante l’effettivo contenuto del testo. Verrà tuttavia definito un testo, in modo verificare con maggiore semplicità che il destinatario autorizzato possa leggerlo.

È quindi possibile condividere in modo sicuro il documento tramite posta elettronica. 

## Per condividere in modo sicuro il documento tramite posta elettronica

1.  Aprire il documento in Word. Si noterà che l'etichetta predefinita **Internal** (Interno) viene ancora applicata automaticamente. 

2.  Nella scheda **Home**, nel gruppo **RMS**, fare clic su **Share Protected** (Condividi file protetto) e quindi scegliere nuovamente **Share Protected** (Condividi file protetto) dal menu:

    ![Esercitazione introduttiva di Azure Information Protection, passaggio 5: Condividere i file protetti](../media/share-protected-callout.png)

    Viene visualizzata la finestra di dialogo **Share Protected** (Condividi file protetto), simile a quella riportata di seguito:

    ![Esercitazione introduttiva di Azure Information Protection, passaggio 5: Finestra di dialogo Share Protected (Condividi file protetto)](../media/example-share-protected-dialog.png)

3. Nella casella **USERS** (UTENTI) digitare uno o più indirizzi di posta elettronica aziendali, così come avviene di solito per inviare un documento a un utente con cui l'organizzazione intrattiene relazioni commerciali. In alternativa, è possibile specificare l'indirizzo di posta elettronica di un collaboratore. Assicurarsi di specificare un indirizzo di posta elettronica aziendale, ad esempio **janetm@contoso.com** o **p.dover@fabrikam.com**, perché attualmente Azure Information Protection non supporta gli indirizzi di posta elettronica personali. 

    Non è importante se la persona a cui si sta inviando il messaggio dispone o meno di Azure Information Protection.

4. Selezionare **Visualizzatore - Solo visualizzazione**.

    In questo modo i destinatari saranno in grado di visualizzare il documento, ma non di modificarlo o stamparlo.

5. Selezionare l'opzione per l' **invio di un messaggio di posta elettronica quando qualcuno tenta di aprire il documento**.

    Si riceverà una notifica tramite posta elettronica ogni volta che i destinatari tentano di aprire l'allegato. La notifica verrà inviata anche quando qualcun altro tenta di aprire il messaggio, ad esempio se il destinatario lo inoltra a un collega. Se il documento viene inoltrato, l'accesso viene negato e, in base ai dettagli dell'utente, sarà possibile decidere se inviare a tale persona una copia del documento che potrà aprire.

6. Selezionare l'opzione per la **revoca immediata dell'accesso a specifici documenti**.

    Per questa opzione è necessario che i destinatari siano connessi a Internet ogni volta che aprono l'allegato. L'opzione offre comunque il vantaggio che, se in un secondo momento si revoca il documento, il successivo tentativo di apertura da parte dei destinatari avrà esito negativo. 

4.  Fare clic su **Send** (Invia) per visualizzare un messaggio di posta elettronica pronto per l'invio ai destinatari specificati e con un testo di istruzioni predefinito. Ad esempio:

    ![Messaggio di posta elettronica di esempio per la condivisione di file protetti](../media/example-email-share-protected.png)
    
    **NOTA**: se Outlook è stato aperto al momento dell'installazione del client di Azure Information Protection, la barra di Information Protection mostrata nella figura precedente non verrà visualizzata. Questa barra non è usata specificamente in questo passaggio riguardante la condivisione di documenti protetti e quindi non è necessario chiudere e riaprire Outlook per completare l'esercitazione. Se Outlook è stato aperto dopo l'installazione del client di Azure Information Protection, si noterà che questo messaggio di posta elettronica, così come il documento di Word alla prima apertura, riporta l'etichetta **Internal** (Interno), applicata per impostazione predefinita a seguito della configurazione di questa impostazione globale nei criteri di Azure Information Protection.
    
    Sono presenti due allegati: il documento di Word originale e un file con lo stesso nome ma con estensione **ppdf**. La versione con estensione ppdf è un file PDF protetto creato automaticamente dall'applicazione Rights Management sharing nel caso in cui il destinatario non disponga di una versione di Office che supporta i documenti protetti. Questo file aggiuntivo consente al destinatario di leggere il documento protetto usando il visualizzatore installato con l'applicazione Rights Management sharing.

    Fare clic su **Send** (Invia) nel messaggio di posta elettronica.

Ora che è stato inviato il documento protetto, è possibile chiedere ai destinatari di attenderne l'arrivo e quindi di aprirlo. Non chiudere Word, poiché verrà usato di nuovo nella procedura finale per tenere traccia del documento condiviso.

## Chiedere ai destinatari di aprire il documento inviato tramite posta elettronica

I destinatari possono usare molti dispositivi per leggere il documento protetto inviato come allegato di posta elettronica. I dispositivi includono iPad, iPhone, tablet e telefoni Android, computer Mac e computer Windows.

Chiedere di leggere il messaggio di posta elettronica inviato. Supponendo che questa sia la prima volta che i destinatari ricevono allegati protetti da Rights Management, chiedere loro di fare clic sul collegamento di istruzioni. Verrà visualizzata la pagina [Schermata iniziale di Microsoft RMS](https://portal.azurerms.com/#/rmshelp), con istruzioni per installare l'applicazione RMS sharing e, se necessario, per iscriversi e ottenere un account gratuito. A questo punto è possibile leggere l'allegato protetto.

### Istruzioni per il destinatario: Per visualizzare l'allegato del documento protetto

1. Aprire uno degli allegati per leggere il documento:
    
    - Se sul dispositivo si dispone di una versione di Office che supporta Rights Management:
    
        -  Aprire il documento con estensione di file **docx**.
        
    - Se non si dispone di una versione di Office che supporta Rights Management, non si è sicuri o si vuole semplicemente provare il visualizzatore dall'applicazione Rights Management sharing: 
    
        - Aprire il documento con estensione **ppdf**.

2.  Se vengono richiesti il nome utente e la password, immettere il nome utente nello stesso formato dell'indirizzo di posta elettronica usato per inviare il messaggio di posta elettronica e l’allegato, ad esempio **janetm@contoso.com** o **p.dover@fabrikam.com**. Come password digitare quella fornita al momento dell'iscrizione a RMS per utenti singoli. In alternativa, se l'organizzazione dispone di un servizio cloud quale Office 365 o usa Azure, immettere la normale password aziendale.

3. Quando il documento viene aperto, leggere il contenuto. Dal momento che il documento è di sola lettura, non è possibile modificare il contenuto.

Come passaggio facoltativo, il destinatario dovrebbe inoltrare il messaggio di posta elettronica ad altri utenti non inclusi nel messaggio originale. Queste persone non saranno in grado di aprire l'allegato. Se vengono accettati per il nome utente, l'accesso al documento verrà comunque negato.

Ora che il destinatario ha aperto l'allegato e, facoltativamente, lo ha inoltrato a qualcun altro, si prevede di ricevere una notifica tramite posta elettronica che segnala questa attività. I messaggi di posta elettronica, tuttavia, vanno facilmente persi nel corso tempo. Il modo migliore per rilevare chi ha avuto accesso al documento consiste nell'usare il sito di rilevamento dei documenti, come illustrato nella procedura finale.

## Per rilevare il documento protetto

1.  Di nuovo in Word, nel gruppo **RMS** della scheda **Home** fare clic su **Share Protected** (Condividi file protetto) e quindi scegliere **Track Usage** (Rileva utilizzo) dal menu:

    ![Opzione Rileva utilizzo](../media/track-usage-callout.png)

    In questo modo si passa al sito di rilevamento dei documenti.

2.  Se viene visualizzata la pagina **Proteggere e condividere in base alle proprie esigenze**, fare clic su **Accedi** e inserire nuovamente il nome utente e la password.

3.  Nella pagina **Your shared documents** (Documenti condivisi) verrà visualizzato il nome del documento condiviso. Al momento è l'unico file visualizzato, ma se vengono condivisi altri documenti protetti, l'elenco si allunga di conseguenza.

    In questa pagina viene indicato quando il documento è stato condiviso (quando è stato inviato il messaggio di posta elettronica con l'allegato protetto), la data dell'ultima attività e il nome del destinatario a cui è stato inviato il messaggio. Fare clic sul nome del documento per altri dettagli.

4.  Nella nuova pagina, che ha il nome del file selezionato, verranno visualizzati i dettagli di riepilogo solo per il documento in questione e un elenco di altre opzioni disponibili per quest'ultimo (**Elenco**, **Sequenza temporale**, **Mappa**e **Impostazioni**).

    Fare clic su ogni opzione per esplorare i diversi modi di rilevare il documento protetto. In alternativa, sempre nella pagina **Riepilogo** , fare clic su **Apri in Excel** per esportare le informazioni in un foglio di calcolo oppure fare clic su **Revoca accesso** per arrestare la condivisione del documento.

È possibile tornare a questo sito per rilevare altre attività relative al documento protetto o, se necessario, per revocare l'accesso. È anche possibile accedere al sito dal dispositivo mobile o dal tablet, usando un browser con il collegamento seguente: [rilevamento documenti](http://go.microsoft.com/fwlink/?LinkId=529562)



|Se si desiderano altre informazioni|Informazioni aggiuntive|
|--------------------------------|--------------------------|
|Istruzioni complete e metodi alternativi per la protezione dei file condivisi tramite posta elettronica|[Proteggere un file che si condivide tramite posta elettronica usando l'applicazione Rights Management sharing](../rms-client/sharing-app-protect-by-email.md)|
|Informazioni sulle opzioni della finestra di dialogo **Condividi file protetto**|[Opzioni della finestra di dialogo per l'applicazione Rights Management sharing](../rms-client/sharing-app-dialog-box.md)|
|Account gratuito per l'iscrizione di altri utenti|[RMS per utenti singoli e Azure Rights Management](../understand-explore/rms-for-individuals.md)|
|Uso del sito di rilevamento dei documenti|[Tenere traccia dei documenti e revocarli](../rms-client/sharing-app-track-revoke.md)


## Passaggi successivi

Dopo aver esaminato il criterio predefinito di Azure Information Protection e dopo aver scoperto come personalizzarlo, oltre ad aver appreso come funziona l'aggiunta di etichette per un documento di Word, è consigliabile provare qualcuna delle altre impostazioni e verificarne il funzionamento in altre applicazioni di Office che supportano Azure Information Protection: Excel, PowerPoint, Outlook. Se al momento dell'installazione del client di Azure Information Protection queste applicazioni erano aperte, chiuderle e riaprirle prima di provare a usarle con Azure Information Protection.

Provare a condividere altri documenti, a tenere traccia del modo in cui vengono usati e a verificare il funzionamento della revoca dell'accesso ai documenti.

Può essere utile leggere alcune delle [domande frequenti](faqs.md) relative ad Azure Information Protection e consultare altri articoli della documentazione. Se tuttavia si è pronti a iniziare la distribuzione di Azure Information Protection nell'organizzazione, leggere le informazioni riportate nella [Guida di orientamento per la distribuzione di Azure Information Protection](../plan-design/deployment-roadmap.md). 


<!--HONumber=Sep16_HO4-->


