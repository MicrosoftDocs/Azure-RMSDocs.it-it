---
title: Esercitazione per l'avvio rapido - Passaggio 5 - AIP
description: "Passaggio 5 di un'esercitazione introduttiva per provare rapidamente a usare Azure Information Protection: condividere file protetti e tenere traccia del documento."
keywords: ''
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 05/09/2018
ms.topic: conceptual
ms.service: information-protection
ms.assetid: 4e59a3b3-f0f4-4535-8b96-cac68303d855
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 076c7f78f4a1458a4d83272b0a8b281341ebb75d
ms.sourcegitcommit: 26a2c1becdf3e3145dc1168f5ea8492f2e1ff2f3
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/07/2018
ms.locfileid: "44148631"
---
# <a name="step-5-see-sharing-of-protected-files-in-action-and-track-your-document"></a>Passaggio 5: Vedere in azione la condivisione di file protetti e tenere traccia del documento 

>*Si applica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*

Per questo passaggio finale dell'esercitazione, individuare un documento di Word o un foglio di calcolo di Excel già creato da inviare a un partner o a un collaboratore. Ai fini di questa esercitazione non è importante l’effettivo contenuto del testo. Verrà tuttavia definito un testo, in modo verificare con maggiore semplicità che il destinatario autorizzato possa leggerlo.

È quindi possibile condividere in modo sicuro il documento tramite posta elettronica. 

## <a name="to-safely-share-your-document-by-email"></a>Per condividere in modo sicuro il documento tramite posta elettronica

1. In Esplora file fare clic con il pulsante destro del mouse sul documento e scegliere **Classifica e proteggi**. Verrà visualizzata la finestra di dialogo **Classifica e proteggi - Azure Information Protection**:

    ![Esercitazione introduttiva di Azure Information Protection, passaggio 5: comando Classifica e proteggi](./media/classify-protect-dialog.png)

2. Selezionare **Proteggi con autorizzazioni personalizzate** per visualizzare opzioni aggiuntive.

3. Per **Selezionare le autorizzazioni** mantenere il valore predefinito **Visualizzatore - Solo visualizzazione**.

    In questo modo i destinatari potranno visualizzare il documento, ma non modificarlo o stamparlo.

4. Per **Selezionare gli utenti** digitare uno o più indirizzi di posta elettronica aziendali, come si farebbe per inviare un documento a un utente con cui l'organizzazione intrattiene relazioni commerciali. Per specificare più indirizzi usare un punto e virgola o premere INVIO. 

    Assicurarsi di specificare un indirizzo di posta elettronica aziendale, ad esempio **janetm@contoso.com** o **p.dover@fabrikam.com**, perché attualmente Azure Information Protection non supporta gli indirizzi di posta elettronica personali per questo scenario. 

    In alternativa fare clic sull'icona **Seleziona utenti, gruppi o organizzazione** per selezionare l'indirizzo di posta elettronica di un collega:

    ![Esercitazione introduttiva di Azure Information Protection, passaggio 5: Proteggi con autorizzazioni personalizzate](./media/protect-custom-permissions.png)  
    
    Dopo aver specificato gli indirizzi, copiarli negli Appunti perché verranno usati in un passaggio successivo.

5. Fare clic su **Applica** e attendere la visualizzazione del messaggio **Operazione completata** per vedere i risultati. Fare quindi clic su **Chiudi**.

4. In Esplora file fare di nuovo clic con il pulsante destro del mouse su un file e, questa volta, scegliere **Invia a** > **Destinatario posta**. Il documento verrà così allegato a un messaggio di posta elettronica con un testo predefinito che sarà possibile modificare.

5. Prima di modificare il testo predefinito, incollare gli indirizzi di posta elettronica specificati in precedenza nella casella **A**. 

6. Facoltativamente, digitare l'oggetto desiderato nella casella **Oggetto**, ad esempio: **Sto condividendo un documento protetto**. 

7. Modificare la descrizione predefinita del messaggio in base a ciò che si vuole comunicare ai destinatari. Aggiungere tuttavia il testo seguente:

    **Questo file è protetto con Microsoft Azure Information Protection. In caso di primo utilizzo, vedere queste istruzioni: https://aka.ms/rms-signup.** 

    ![Esercitazione introduttiva di Azure Information Protection, passaggio 5: Condividere un documento protetto tramite posta elettronica](./media/share-protected-emailv2.png)

    Fare clic su **Invia**.

Ora che è stato inviato il documento protetto, è possibile chiedere ai destinatari di attenderne l'arrivo e quindi di aprirlo. 

## <a name="ask-your-recipients-to-open-the-emailed-document"></a>Chiedere ai destinatari di aprire il documento inviato tramite posta elettronica

I destinatari possono usare molti dispositivi per leggere il documento protetto inviato come allegato di posta elettronica. I dispositivi includono iPad, iPhone, tablet e telefoni Android, computer Mac e computer Windows.

Chiedere di leggere il messaggio di posta elettronica inviato. Supponendo che questa sia la prima volta che i destinatari ricevono allegati protetti da Rights Management, chiedere loro di fare clic sul collegamento di istruzioni. Verrà quindi visualizzata la pagina **iniziale** di Microsoft Azure Information Protection, in cui viene richiesto di immettere l'indirizzo di posta elettronica dell'ufficio.

Facendo clic su **Iscriviti**, Azure Information Protection controllerà se l'organizzazione ha una sottoscrizione che include il servizio di protezione dei dati Azure Rights Management. In caso contrario, è possibile richiedere un account gratuito.

### <a name="instructions-for-recipient-to-view-the-protected-document-attachment"></a>Istruzioni per il destinatario: Per visualizzare l'allegato del documento protetto

1. In un computer o un dispositivo mobile con Office installato, aprire l'allegato per leggere il documento.  

2.  Se vengono richiesti il nome utente e la password, immettere il nome utente nello stesso formato dell'indirizzo di posta elettronica usato per inviare il messaggio di posta elettronica e l’allegato, ad esempio **janetm@contoso.com** o **p.dover@fabrikam.com**. Come password digitare quella fornita al momento dell'iscrizione a RMS per utenti singoli. In alternativa, se l'organizzazione dispone di un servizio cloud quale Office 365 o usa Azure, immettere la normale password aziendale.

3. Quando il documento viene aperto, leggere il contenuto. Dal momento che il documento è di sola lettura, non è possibile modificare il contenuto.

Come passaggio facoltativo, il destinatario dovrebbe inoltrare il messaggio di posta elettronica ad altri utenti non inclusi nel messaggio originale. Queste persone non saranno in grado di aprire l'allegato. Se vengono accettati per il nome utente, l'accesso al documento verrà comunque negato.

Ora che il destinatario ha aperto l'allegato e, facoltativamente, lo ha inoltrato a qualcun altro, è possibile tenere traccia del documento.

## <a name="to-track-your-protected-document"></a>Per rilevare il documento protetto

1.  Aprire il documento protetto e condiviso. Un messaggio informativo indica le impostazioni di protezione personalizzata specificate:

    ![Messaggio informativo per la protezione personalizzata](./media/information-banner-custom-protection.png)

2.  Nella scheda **Home** fare clic su **Proteggi** > **Rileva e revoca**:

    ![Opzione Rileva utilizzo](./media/track-usage-calloutv3.png)

    In questo modo si passa al sito di rilevamento dei documenti.

2.  Se viene visualizzata la pagina **Proteggere e condividere in base alle proprie esigenze**, fare clic su **Accedi** e inserire nuovamente il nome utente e la password.

3.  Nella pagina **Documenti condivisi** verrà visualizzato il nome del documento condiviso. Al momento è l'unico file visualizzato, ma se vengono condivisi altri documenti protetti, l'elenco si allunga di conseguenza.

    In questa pagina viene indicato quando il documento è stato condiviso (quando è stato inviato il messaggio di posta elettronica con l'allegato protetto), lo stato corrente del documento (attivo, revocato o scaduto) e il nome del destinatario a cui è stato inviato il messaggio. Fare clic sul nome del documento per altri dettagli.

4.  Nella nuova pagina, che ha il nome del file selezionato, verranno visualizzati i dettagli di riepilogo solo per il documento in questione e un elenco di altre opzioni disponibili per quest'ultimo (**Elenco**, **Sequenza temporale**, **Mappa**e **Impostazioni**).

    Fare clic su ogni opzione per esplorare i diversi modi di rilevare il documento protetto. In alternativa, sempre nella pagina **Riepilogo** , fare clic su **Apri in Excel** per esportare le informazioni in un foglio di calcolo oppure fare clic su **Revoca accesso** per arrestare la condivisione del documento.

È possibile tornare a questo sito per rilevare altre attività relative al documento protetto o, se necessario, per revocare l'accesso. È anche possibile accedere al sito dal dispositivo mobile o dal tablet, usando un browser con il collegamento seguente: [rilevamento documenti](http://go.microsoft.com/fwlink/?LinkId=529562)



|Se si desiderano altre informazioni|Informazioni aggiuntive|
|--------------------------------|--------------------------|
|Istruzioni complete per la protezione dei file in modo da poterli condividere in tutta sicurezza|[Classificare e proteggere un file o un messaggio di posta elettronica](./rms-client/client-classify-protect.md)|
|Account gratuito per l'iscrizione di altri utenti|[RMS per utenti singoli e Azure Rights Management](./rms-for-individuals.md)|
|Uso del sito di rilevamento dei documenti|[Tenere traccia dei documenti e revocarli](./rms-client/client-track-revoke.md)


## <a name="next-steps"></a>Passaggi successivi

Dopo aver esaminato il criterio predefinito di Azure Information Protection e dopo aver scoperto come personalizzarlo, oltre ad aver appreso come funziona l'aggiunta di etichette per un documento di Word, è consigliabile provare qualcuna delle altre impostazioni e verificarne il funzionamento in altre applicazioni di Office che supportano Azure Information Protection: Excel, PowerPoint, Outlook. Se al momento dell'installazione del client di Azure Information Protection queste applicazioni erano aperte, chiuderle e riaprirle prima di provare a usarle con Azure Information Protection.

Provare a condividere altri documenti, a tenere traccia del modo in cui vengono usati e a verificare il funzionamento della revoca dell'accesso ai documenti.

Può essere utile tornare alla pagina **Avvio rapido** nel portale di Azure, leggere alcune delle [domande frequenti](faqs.md) relative ad Azure Information Protection e vedere altri articoli della documentazione. Se tuttavia si è pronti a iniziare la distribuzione di Azure Information Protection nell'organizzazione, leggere le informazioni riportate nella [Guida di orientamento per la distribuzione di Azure Information Protection](deployment-roadmap.md). 
