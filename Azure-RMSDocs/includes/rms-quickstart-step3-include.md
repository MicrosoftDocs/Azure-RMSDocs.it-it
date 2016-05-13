![](../media/AzRMS_QuickStartSteps3.PNG)

Per questo passaggio, creare e salvare un documento di Word che rappresenta il documento che si desidera proteggere e denominarlo **Confidential.docx**. Ai fini di questa esercitazione non è importante l’effettivo contenuto del testo. Verrà tuttavia definito un testo, in modo verificare con maggiore semplicità che il destinatario autorizzato possa leggerlo. Ad esempio, si potrebbe scrivere: **Se il testo è leggibile dall'allegato di posta elettronica, il mittente ha correttamente condiviso un file protetto con Azure RMS.**

È quindi possibile condividere in modo sicuro il documento tramite posta elettronica.

![Condivisione di Azure RMS per schermate di posta elettronica](../media/AzRMS_Tutorial_3_Screenshots.png)

#### Per condividere in modo sicuro il documento tramite posta elettronica

1.  Usando Outlook, creare un nuovo messaggio e allegare il file appena creato.

2.  Nella casella **A** digitare uno o più indirizzi di posta elettronica aziendali. Assicurarsi di specificare un indirizzo di posta elettronica aziendale, ad esempio **janetm@contoso.com** o **p.dover@fabrikam.com**. Azure Rights Management, infatti, non supporta gli indirizzi di posta elettronica personali che è possibile usare a casa dal proprio provider Internet. Non è importante se la persona a cui si sta inviando il messaggio dispone o meno di Azure Rights Management.

3.  Digitare un oggetto, ad esempio  **Documento riservato** , quindi digitare un breve messaggio di posta elettronica, ad esempio **Questo documento è riservato e non può essere condiviso con altri utenti.**

4.  Nella scheda **Messaggio** , nel gruppo **RMS** , fare clic su **Condividi file protetto** e quindi fare di nuovo clic su **Condividi file protetto** :

5.  Nella finestra di dialogo **Condividi file protetto** :

    1.  Selezionare **Visualizzatore - Solo visualizzazione**.

        In questo modo i destinatari saranno in grado di visualizzare il documento, ma non di modificarlo o stamparlo.

    2.  Selezionare l'opzione per l' **invio di un messaggio di posta elettronica quando qualcuno tenta di aprire il documento**.

        Si riceverà una notifica tramite posta elettronica ogni volta che i destinatari tentano di aprire l'allegato. La notifica verrà inviata anche quando qualcun altro tenta di aprire il messaggio, ad esempio se il destinatario lo inoltra a un collega. In quest'ultimo scenario l'accesso viene negato e, in base ai dettagli dell'utente, sarà possibile decidere se inviare a tale persona una copia del documento che potrà aprire.

    3.  Selezionare l'opzione per la **revoca immediata dell'accesso a specifici documenti**.

        Per questa opzione è necessario che i destinatari siano connessi a Internet ogni volta che aprono l'allegato. L'opzione offre comunque il vantaggio che, se in un secondo momento si revoca il documento, il successivo tentativo di apertura da parte dei destinatari avrà esito negativo. Se non si seleziona questa opzione, i destinatari potrebbero essere in grado di aprire il documento anche senza una connessione Internet, con lo svantaggio che, se in un secondo momento si revoca il documento, potrebbe verificarsi un ritardo nell’applicazione di tale scelta.

    4.  Fare clic su **Invia subito**.

        Il messaggio con l’allegato viene inviato agli indirizzi di posta elettronica specificati. Oltre al messaggio di posta elettronica, vengono visualizzate le istruzioni per leggere il documento allegato e protetto da Azure Rights Management.

Ora che è stato inviato il documento protetto, è possibile chiedere ai destinatari di attenderne l'arrivo e quindi di aprirlo. Non chiudere Outlook, perché verrà usato di nuovo nel passaggio finale per rilevare l'allegato.

|Se si desiderano altre informazioni|Informazioni aggiuntive|
|--------------------------------|--------------------------|
|Istruzioni complete e metodi alternativi per la protezione dei file condivisi tramite posta elettronica   →|[Proteggere un file che si condivide tramite posta elettronica usando l'applicazione di condivisione Rights Management](../rms-client/sharing-app-protect-by-email.md)|
|Informazioni sulle opzioni della finestra di dialogo **Condividi file protetto** →|[Opzioni della finestra di dialogo per l’applicazione di condivisione Rights Management](../rms-client/sharing-app-dialog-box.md)|


<!--HONumber=Apr16_HO3-->


