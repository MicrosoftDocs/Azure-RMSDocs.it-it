---
title: Visualizzare i file protetti con il client di Azure Information Protection Unified Labeling
description: Istruzioni per visualizzare un file protetto per il quale è necessario che sia installato il Azure Information Protection visualizzatore unificato delle etichette.
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 06/16/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: v2client
ms.suite: ems
ms.custom: user
ms.openlocfilehash: 8d7779a14b7fd7ca4a78a7b69e0c8c243c0fe07d
ms.sourcegitcommit: c133ada59dffcb9d8ee35688290d2b027bd63425
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/03/2020
ms.locfileid: "89423061"
---
# <a name="user-guide-view-protected-files-with-the-azure-information-protection-unified-labeling-client"></a>Guida dell'utente: visualizzare i file protetti con il client di Azure Information Protection Unified Labeling

>*Si applica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8*
>
>*Se si dispone di Windows 7 o Office 2010, vedere [AIP per le versioni di Windows e Office nel supporto esteso](../known-issues.md#aip-for-windows-and-office-versions-in-extended-support).*
>
> *Istruzioni per: [Azure Information Protection client di etichetta unificata per Windows](../faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

Per visualizzare un file protetto, spesso è sufficiente aprirlo. Ad esempio, è possibile fare doppio clic su un allegato in un messaggio di posta elettronica o fare doppio clic su un file in Esplora file oppure è possibile fare clic su un collegamento a un file.

Se i file non si aprono immediatamente, il **visualizzatore Azure Information Protection** potrebbe essere in grado di aprirli. Il visualizzatore è in grado di aprire file di testo protetti, file di immagine protetti, file PDF protetti e tutti i file con estensione **PFILE**.

Il visualizzatore viene installato automaticamente come parte del client di Azure Information Protection Unified Labeling oppure è possibile installarlo separatamente. È possibile installare sia il client che il visualizzatore dalla pagina [Microsoft Azure Information Protection](https://go.microsoft.com/fwlink/?LinkId=303970) nel sito Web Microsoft. Per altre informazioni sull'installazione di questo client, vedere [scaricare e installare il client di etichettatura unificata Azure Information Protection](install-unifiedlabelingclient-app.md).

> [!NOTE]
> Benché l'installazione del client fornisca più funzionalità, richiede autorizzazioni di amministratore locale e la funzionalità completa richiede un servizio corrispondente per l'organizzazione. Ad esempio, Azure Information Protection.
> 
> Installare il visualizzatore se si è ricevuto un documento protetto da un utente di un'altra organizzazione o se non si possiedono autorizzazioni di amministratore locale per il PC.

Per essere in grado di aprire un documento protetto, l'applicazione deve essere "abilitata per RMS". Le applicazioni Office e il visualizzatore Azure Information Protection sono esempi di applicazioni abilitate per RMS. Per visualizzare un elenco di applicazioni per tipo e per i dispositivi supportati, vedere le tabelle [applicazioni abilitate per RMS](../requirements-applications.md) . 

## <a name="messagerpmsg-as-an-email-attachment"></a>Message.rpmsg come allegato di posta elettronica

Se **message.rpmsg** appare come file allegato in un messaggio di posta elettronica, non si tratta di un documento protetto, ma di un messaggio di posta elettronica protetto visualizzato come allegato. Non è possibile usare il visualizzatore Azure Information Protection per Windows per visualizzare questo messaggio di posta elettronica protetto in un computer Windows. È invece necessaria un'applicazione di posta elettronica per Windows che supporti la protezione di Rights Management, ad esempio Office Outlook. Oppure si può usare Outlook sul Web.

Se tuttavia si usa un dispositivo iOS o Android, è possibile usare l'app di Azure Information Protection per aprire i messaggi di posta elettronica protetti. L'app per questi dispositivi mobili può essere scaricata dalla pagina [Microsoft Azure Information Protection](https://go.microsoft.com/fwlink/?LinkId=303970) del sito Web Microsoft.

## <a name="prompts-for-authentication"></a>Richieste di autorizzazione

Prima di poter visualizzare il file protetto, il servizio Rights Management usato per proteggere il file deve prima di tutto verificare che siano presenti le autorizzazioni necessarie per la visualizzazione del file. Il servizio esegue tale controllo verificando il nome utente e la password. In alcuni casi, le credenziali possono essere memorizzate nella cache e non verrà visualizzato un messaggio che richiede di eseguire l'accesso. In altri casi, verrà richiesto di immettere le credenziali.

Se l'organizzazione non può mettere a disposizione dell'utente un account basato sul cloud (per Office 365 o Azure) e non usa una versione locale equivalente (AD RMS), sono disponibili due opzioni:

- Se il messaggio di posta elettronica ricevuto è protetto, seguire le istruzioni per accedere tramite il provider di identità basato su social network (ad esempio Google per un account Gmail) o richiedere un passcode monouso.

- È possibile richiedere un account gratuito che accetti le credenziali dell'utente e consenta quindi di aprire i documenti protetti da Rights Management. Per richiedere un account di questo tipo, fare clic sul collegamento per [RMS per utenti singoli](https://go.microsoft.com/fwlink/?LinkId=309469) e usare l'indirizzo e-mail della società anziché un indirizzo personale. 

## <a name="to-view-a-protected-file"></a>Per visualizzare un file protetto

1. Aprire il file protetto (ad esempio, facendo doppio clic sul file o sull'allegato oppure facendo clic sul collegamento al file). Se viene chiesto di selezionare un'app, selezionare l'app **Visualizzatore Azure Information Protection**. 

2. Se viene visualizzata una pagina di **accesso** o **iscrizione**: fare clic su **Accedi** e immettere le credenziali. Se il file protetto è stato inviato come allegato, assicurarsi di specificare lo stesso indirizzo di posta elettronica usato per l'invio del file.
    
    Se l'account specificato non viene accettato, vedere la sezione [Richieste di autorizzazione](#prompts-for-authentication) in questa pagina.

3. Viene aperta una versione di sola lettura del file nel **visualizzatore Azure Information Protection** o nell'applicazione associata all'estensione del nome file.

4. Per aprire altri file protetti, è possibile visualizzarli direttamente nel visualizzatore usando l'opzione **Apri**. Il file selezionato sostituisce il file originale nel visualizzatore. 

> [!TIP]
> Se il file protetto non si apre e nel sistema è installato il client di Azure Information Protection completo, provare con l'opzione **Ripristina le impostazioni**. Per accedere a questa opzione, da un'app di Office selezionare il pulsante **Sensitivity (sensibilità** ) > le impostazioni della **Guida e**della  >  **reimpostazione**del feedback. 
> 
> [Altre informazioni sull'opzione Ripristina le impostazioni](clientv2-admin-guide.md#more-information-about-the-reset-settings-option)

## <a name="other-instructions"></a>Altre istruzioni
Ulteriori procedure nella Guida per l'utente di Azure Information Protection:

- [Per saperne di più](client-user-guide.md#what-do-you-want-to-do)

