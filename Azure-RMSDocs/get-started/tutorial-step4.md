---
# required metadata

title: Esercitazione per l'avvio rapido di Azure RMS - Passaggio 4 | Azure RMS
description: Il quarto passaggio di questa esercitazione consente di provare rapidamente Microsoft Azure Rights Management per l'organizzazione. L'esercitazione è articolata in 5 passaggi, eseguibili in meno di 15 minuti.
keywords:
author: Cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: azure
ms.service: rights-management
ms.assetid: f8340056-87a1-4daa-8b63-3d95fc381b9c

# optional metadata

ROBOTS: 
audience:
ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
ms.tgt_pltfrm:
ms.technology:
ms.custom:

---


# Passaggio 4 dell'esercitazione per l'avvio rapido di Azure RMS: Chiedere ai destinatari di aprire il documento inviato tramite posta elettronica

Passare a: 
> [!div class="op_single_selector"]
- [Introduzione](quick-start-tutorial.md)
- [Passaggio 1: Attivare Azure RMS](tutorial-step1.md)
- [Passaggio 2: Installare l'app di condivisione RMS](tutorial-step2.md)
- [Passaggio 3: Inviare il documento riservato tramite posta elettronica](tutorial-step3.md)
- [Passaggio 4: Leggere il documento](tutorial-step4.md)
- [Passaggio 5: Tenere traccia del documento](tutorial-step5.md)


![](../media/AzRMS_QuickStartSteps4.PNG)

I destinatari possono usare molti dispositivi per leggere il documento protetto inviato come allegato di posta elettronica. I dispositivi includono iPad, iPhone, tablet e telefoni Android, computer Mac e computer Windows.

Chiedere di leggere il messaggio di posta elettronica inviato. Verrà visualizzato il messaggio di posta elettronica e, prima di esso, il testo seguente:

**Il mittente ha protetto gli allegati con Microsoft RMS. È necessario** [eseguire l'accesso](http://aka.ms/rms)
      **per aprirli.**

Quando si fa clic sul collegamento, vengono visualizzate le istruzioni per installare l'app di condivisione RMS e, se necessario, per accedere a un account gratuito. L'account gratuito concede una sottoscrizione per RMS per utenti singoli. Questa sottoscrizione assicura che gli utenti autorizzati possano sempre leggere un documento protetto, anche se l'organizzazione non dispone di Azure RMS. A questo punto è possibile leggere l'allegato protetto seguendo le istruzioni seguenti.

![](../media/AzRMS_Tutorial_4_Screenshots.png)

### Per visualizzare l'allegato del documento protetto

1.  Poiché si tratta di un documento di Word protetto da Azure Rights Management, il messaggio di posta elettronica presenta due allegati. Si tratta in effetti di due versioni dello stesso file con estensioni diverse. Aprire la versione con l’estensione di file **ppdf** (**Confidential.ppdf**).

    Se si dispone di una versione di [Office sul dispositivo che supporta Rights Management](https://technet.microsoft.com/library/dn655136.aspx), è possibile aprire l'altra versione del file (**Confidential.docx**) in modo da aprirla in Word.

2.  Se vengono richiesti il nome utente e la password, immettere il nome utente nello stesso formato dell'indirizzo di posta elettronica usato per inviare il messaggio di posta elettronica e l’allegato, ad esempio **janetm@contoso.com** o **p.dover@fabrikam.com**. Come password digitare quella fornita al momento dell'iscrizione a RMS per utenti singoli. In alternativa, se l'organizzazione dispone di Azure RMS, immettere la normale password aziendale.

Il documento viene aperto ed è possibile leggerne il contenuto. Ad esempio, si potrebbe leggere **Se il testo è leggibile dall'allegato di posta elettronica, il mittente ha correttamente condiviso un file protetto con Azure RMS.** Dal momento che il documento è di sola lettura, non è possibile modificare il contenuto.

Come passaggio facoltativo, è possibile richiedere al destinatario di inoltrare il messaggio di posta elettronica ad altri utenti non inclusi nel messaggio originale Anche se questi utenti lavorano per un'organizzazione dotata di Azure Rights Management o richiedono una propria sottoscrizione a RMS per utenti singoli, non saranno in grado di aprire l'allegato. Se vengono accettati per il nome utente, l'accesso al documento verrà comunque negato.

Ora che il destinatario ha aperto l'allegato e, facoltativamente, lo ha inoltrato a qualcun altro, si prevede di ricevere una notifica tramite posta elettronica che segnala questa attività. I messaggi di posta elettronica, tuttavia, vanno facilmente persi nel corso tempo. Il modo migliore per rilevare chi ha avuto accesso al documento consiste nell'usare il sito di rilevamento dei documenti, come illustrato nel passaggio finale.

|Se si desiderano altre informazioni|Informazioni aggiuntive|
|--------------------------------|--------------------------|
|Istruzioni complete per la visualizzazione dei file protetti da Azure Rights Management|[Visualizzare e usare i file che sono stati protetti da Rights Management](../rms-client/sharing-app-view-use-files.md)|
|Informazioni sulla sottoscrizione gratuita, RMS per utenti singoli|[RMS per utenti singoli e Azure Rights Management](../understand-explore/rms-for-individuals.md)|
|Informazioni sulle due versioni del file allegato al messaggio di posta elettronica|[Che cos'è il file .ppdf che viene creato automaticamente?](../rms-client/sharing-app-dialog-box.md#what-s-the-ppdf-file-that-s-automatically-created-)|


>[!div class="step-by-step"]
[« Passaggio 3](tutorial-step3.md)
[Passaggio 5 »](tutorial-step5.md)

<!--HONumber=Apr16_HO3-->


