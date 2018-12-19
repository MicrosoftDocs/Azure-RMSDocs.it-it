---
title: Visualizzare e usare i documenti protetti con il client AIP
description: Istruzioni per visualizzare e usare un documento protetto che richiede l'installazione del client Azure Information Protection.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 12/12/2018
ms.topic: conceptual
ms.service: information-protection
ms.assetid: ce1c7d4c-b5ff-4672-8b9a-a72129bac992
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 5a09cc6ecba5759c39717053f434396ade47a610
ms.sourcegitcommit: 1d2912b4f0f6e8d7596cbf31e2143a783158ab11
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/12/2018
ms.locfileid: "53305251"
---
# <a name="user-guide-view-and-use-files-that-have-been-protected-by-rights-management"></a>Manuale dell'utente: Visualizzare e usare i file che sono stati protetti da Rights Management

>*Si applica a: Active Directory Rights Management Services, [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8, Windows 7 con SP1*

Per visualizzare un documento protetto, spesso è sufficiente aprirlo. Ad esempio, è possibile fare doppio clic su un allegato in un messaggio di posta elettronica o fare doppio clic su un file in Esplora file oppure è possibile fare clic su un collegamento a un file.

Se i file non si aprono immediatamente, il **visualizzatore Azure Information Protection** potrebbe essere in grado di aprirli. Il visualizzatore è in grado di aprire file di testo protetti, file di immagine protetti, file PDF protetti e tutti i file con estensione **PFILE**.

Viene automaticamente installato con il client Azure Information Protection oppure può essere installato separatamente. Il client e il visualizzatore possono essere entrambi installati dalla pagina [Microsoft Azure Information Protection](https://go.microsoft.com/fwlink/?LinkId=303970) del sito Web Microsoft. Per altre informazioni sull'installazione del client, vedere [Scaricare e installare il client Azure Information Protection](install-client-app.md).

> [!NOTE]
> Benché l'installazione del client fornisca più funzionalità, richiede autorizzazioni di amministratore locale e la funzionalità completa richiede un servizio corrispondente per l'organizzazione. Ad esempio, Azure Information Protection o Active Directory Rights Management Services.
> 
> Installare il visualizzatore se si è ricevuto un documento protetto da un utente di un'altra organizzazione o se non si possiedono autorizzazioni di amministratore locale per il PC.

Per essere in grado di aprire un documento protetto, l'applicazione deve essere "abilitata per RMS". Le applicazioni Office e il visualizzatore Azure Information Protection sono esempi di applicazioni abilitate per RMS. Per visualizzare un elenco di applicazioni per tipo e i dispositivi supportati, vedere la [tabella delle applicazioni abilitate per RMS](../requirements-applications.md#rms-enlightened-applications).  
## <a name="messagerpmsg-as-an-email-attachment"></a>Message.rpmsg come allegato di posta elettronica

Se **message.rpmsg** appare come file allegato in un messaggio di posta elettronica, non si tratta di un documento protetto, ma di un messaggio di posta elettronica protetto visualizzato come allegato. Non è possibile usare il visualizzatore Azure Information Protection per Windows per visualizzare questo messaggio di posta elettronica protetto in un computer Windows. È invece necessaria un'applicazione di posta elettronica per Windows che supporti la protezione di Rights Management, ad esempio Office Outlook. Oppure si può usare Outlook sul Web.

Se tuttavia si usa un dispositivo iOS o Android, è possibile usare l'app di Azure Information Protection per aprire i messaggi di posta elettronica protetti. L'app per questi dispositivi mobili può essere scaricata dalla pagina [Microsoft Azure Information Protection](https://go.microsoft.com/fwlink/?LinkId=303970) del sito Web Microsoft.

## <a name="prompts-for-authentication"></a>Richieste di autorizzazione

Prima di poter visualizzare il file protetto, il servizio Rights Management usato per proteggere il file deve prima di tutto verificare che siano presenti le autorizzazioni necessarie per la visualizzazione del file. Il servizio esegue tale controllo verificando il nome utente e la password. In alcuni casi, le credenziali possono essere memorizzate nella cache e non verrà visualizzato un messaggio che richiede di eseguire l'accesso. In altri casi, verrà richiesto di immettere le credenziali.

Se l'organizzazione non può mettere a disposizione dell'utente un account basato sul cloud (per Office 365 o Azure) e non usa una versione locale equivalente (AD RMS), sono disponibili due opzioni:

- Se il messaggio di posta elettronica ricevuto è protetto, seguire le istruzioni per accedere tramite il provider di identità basato su social network (ad esempio Google per un account Gmail) o richiedere un passcode monouso.

- È possibile richiedere un account gratuito che accetti le credenziali dell'utente e consenta quindi di aprire i documenti protetti da Rights Management. Per richiedere un account di questo tipo, fare clic sul collegamento per [RMS per utenti singoli](https://go.microsoft.com/fwlink/?LinkId=309469) e usare l'indirizzo e-mail della società anziché un indirizzo personale. 

## <a name="to-view-and-use-a-protected-document"></a>Per visualizzare e usare un documento protetto

1. Aprire il file protetto (ad esempio, facendo doppio clic sul file o sull'allegato oppure facendo clic sul collegamento al file). Se viene chiesto di selezionare un'app, selezionare l'app **Visualizzatore Azure Information Protection**. 

2. Se viene visualizzata una pagina per **accedere** o **iscriversi**: fare clic su **Accedi** e immettere le proprie credenziali. Se il file protetto è stato inviato come allegato, assicurarsi di specificare lo stesso indirizzo di posta elettronica usato per l'invio del file.
    
    Se l'account specificato non viene accettato, vedere la sezione [Richieste di autorizzazione](#prompts-for-authentication) in questa pagina.

3. Una versione di sola lettura del file viene aperta nel **visualizzatore Azure Information Protection**. Se si hanno autorizzazioni sufficienti, è possibile stampare il file e modificarlo. 

    È possibile controllare le autorizzazioni per il file facendo clic su **Autorizzazioni**. Nella finestra di dialogo **Autorizzazioni** è possibile anche identificare il proprietario del file da contattare se si vuole richiedere una nuova versione del file con autorizzazioni aggiuntive.
    
    Per altre informazioni sulle autorizzazioni e sui diritti di utilizzo di ciascuna autorizzazione, vedere [Diritti inclusi nei livelli di autorizzazioni](../configure-usage-rights.md#rights-included-in-permissions-levels).

4. Per modificare il file, fare clic su **Salva con nome**, che consente di salvare il file protetto con l'estensione originale. È quindi possibile modificare il file usando l'applicazione associata al tipo di file. A questo punto, l'etichetta del file e la protezione vengono rimosse.
    
    Si noti che dal momento che il visualizzatore è per i file protetti, il pulsante **Salva con nome** è abilitato solo per i file protetti.
    
5. Dopo aver completato la modifica del file, in Esplora file fare clic con il pulsante destro del mouse sul file per riapplicare l'etichetta. Questa azione consente di riapplicare anche la protezione.

6. Per aprire altri file protetti, è possibile visualizzarli direttamente nel visualizzatore usando l'opzione **Apri**. Il file selezionato sostituisce il file originale nel visualizzatore. 

> [!TIP]
> Se il file protetto non si apre e nel sistema è installato il client di Azure Information Protection completo, provare con l'opzione **Ripristina le impostazioni**. Per accedere all'opzione, da un'app di Office, selezionare il pulsante **Proteggi** > **Guida e commenti** > **Ripristina le impostazioni**. 
> 
> [Altre informazioni sull'opzione Ripristina le impostazioni](client-admin-guide.md#more-information-about-the-reset-settings-option)

## <a name="other-instructions"></a>Altre istruzioni
Ulteriori procedure nella Guida per l'utente di Azure Information Protection:

-   [Per saperne di più](client-user-guide.md#what-do-you-want-to-do)

