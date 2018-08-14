---
title: Aprire file protetti da RMS con l'app RMS sharing - AIP
description: Istruzioni per visualizzare e usare un file protetto che rende necessario avere l'applicazione Rights Management (RMS) sharing installata.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 07/18/2017
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: e5fa4666-6906-405a-9e0c-2c52d4cd27c8
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 4143cd12138e82bcf94331ef0911033acdb1942c
ms.sourcegitcommit: 949bf02d5d12bef8e26d89ad5d6a0d5cc7826135
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/02/2018
ms.locfileid: "39474376"
---
# <a name="view-and-use-files-that-have-been-protected-by-rights-management"></a>Visualizzare e usare i file che sono stati protetti da Rights Management

>*Si applica a: Active Directory Rights Management Services, [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 7 con SP1, Windows 8, Windows 8.1*

Quando l'[applicazione Rights Management (RMA) sharing viene installata nel computer in uso](install-sharing-app.md), viene visualizzato un file protetto semplicemente facendo doppio clic su di esso. Il file potrebbe essere un allegato in un messaggio di posta elettronica oppure è possibile vederlo quando si utilizza Esplora file.

> [!NOTE]
> Per consentire a un utente di visualizzare il file protetto, il servizio Rights Management deve prima verificare che sia autorizzato e a questo scopo controlla il nome utente e la password. In alcuni casi, questo potrebbe essere memorizzato nella cache e non verrà visualizzato un messaggio che richiede l'immissione delle credenziali. In altri casi, verrà richiesto di fornire le credenziali.
>
> Se l'organizzazione non usa Azure Information Protection o AD RMS, è possibile richiedere un account gratuito che accetterà le credenziali in modo che sia possibile aprire i file protetti tramite RMS:
>
> -   Per richiedere questo account, fare clic sul collegamento per richiedere [RMS per utenti singoli](http://go.microsoft.com/fwlink/?LinkId=309469).
>
>     Quando si effettua l'iscrizione, utilizzare l'indirizzo di posta elettronica della società anziché un indirizzo di posta elettronica personale. Se si esegue l'iscrizione perché è stato inviato un allegato protetto tramite posta elettronica, utilizzare lo stesso indirizzo di posta elettronica utilizzato per inviare il messaggio di posta elettronica.
> -   Per ulteriori informazioni, vedere [RMS per utenti singoli e Azure Rights Management](../rms-for-individuals.md).

## <a name="to-view-a-protected-file"></a>Per visualizzare un file protetto
Utilizzando Esplora file o il messaggio di posta elettronica contenente l'allegato, fare doppio clic sul file protetto e immettere le credenziali se viene richiesto.

Se si visualizzano due versioni del file, ma con estensioni del nome di file diverse, aprire il file con estensione .ppdf solo se gli altri file non si aprono. Se non è possibile aprire nemmeno la versione con estensione ppdf, installare innanzitutto l'[applicazione RMS sharing](install-sharing-app.md), che è in grado di aprire i file con estensione del nome di file ppdf.

> [!NOTE]
> Per altre informazioni, vedere [Che cos'è il file .ppdf che viene creato automaticamente?](sharing-app-dialog-box.md#whats-the-ppdf-file-thats-automatically-created)

Come il file verrà aperto dipende da come è stato protetto; è possibile saperlo esaminando l'estensione del file. In ogni caso, l’apertura del file potrebbe essere controllata e rimane controllata finché è protetto. Inoltre, se il file è stato inviato come allegato di posta elettronica, il mittente potrebbe ricevere una notifica tramite posta elettronica ogni volta che si apre il file.

- **Il file ha estensione del nome di file** *.pfile*

    Il file è stato protetto in modo generico.

    Quando si apre il file, viene visualizzata una finestra di dialogo del **file protetto** dall'applicazione di condivisione che indica chi ha protetto il file e che è necessario rispettare le autorizzazioni di comproprietario. Fare clic su **Apri** per leggere il file.

    ![Finestra di dialogo per un pfile condiviso tramite posta elettronica quando si usa l'applicazione RMS sharing](../media/ADRMS_MSRMSApp_PfilePermission.png)

- **Il file ha estensione *.ppdf* o è un file di testo o immagine protetto, (ad esempio *.ptxt* o *.pjpg*)**

    Il file è stato protetto in modo nativo come copia di sola lettura.

    Il file si apre tramite il visualizzatore che viene installato con l'applicazione di RMS sharing. Questo file è di sola lettura, anche se lo si salva in un altro percorso o lo si rinomina.

- **Altre estensioni del nome di file**

    Il file è protetto in modo nativo.

    Il file si apre tramite l'applicazione associata all'estensione del nome di file originale e viene visualizzato un banner di limitazione nella parte superiore del file. Nel banner possono essere visualizzate le autorizzazioni applicate al file o può essere presente un collegamento per visualizzarle. Ad esempio, si potrebbe visualizzare quanto segue dove è necessario fare clic su **L'autorizzazione è attualmente soggetta a restrizioni** per visualizzare le autorizzazioni effettive applicate al file e le persone che possono accedervi:

    ![Banner di accesso limitato quando il file è protetto](../media/ADRMS_MSRMSApp_RestrictedAccess.png)



Per un elenco completo delle estensioni di file supportate dai servizi Rights Management, vedere la sezione [Tipi ed estensioni di file supportati](sharing-app-admin-guide-technical.md#supported-file-types-and-file-name-extensions) della [Guida dell'amministratore dell'applicazione Rights Management sharing](sharing-app-admin-guide.md). Se un'estensione di nome di file non è elencata, eseguire una ricerca sul Web per determinare se si tratta di un'estensione di nome di file supportata da un'altra applicazione.

## <a name="to-use-files-that-have-been-protected-for-example-edit-and-print-the-file"></a>Per utilizzare i file protetti (ad esempio, modificare e stampare il file)
Se dopo avere aperto il file protetto si vuole eseguire altre operazioni oltre alla lettura (ad esempio, modifica, copia e stampa), seguire le istruzioni in base all'estensione del nome di file:

- **Il file ha estensione del nome di file** *.pfile*

    Salvare il file aperto e assegnargli una nuova estensione del nome di file associata all'applicazione che si desidera utilizzare.

    Ad esempio, se un file è stato protetto utilizzando il nome di file document.vsdx.pfile, visualizzarlo e in Esplora file salvarlo come document.vsdx.

    Il nuovo file non è più protetto. Se si desidera proteggerlo, è necessario eseguire questa operazione manualmente. Per istruzioni, vedere [Proteggere un file in un dispositivo (protezione sul posto) tramite l'applicazione Rights Management sharing](sharing-app-protect-in-place.md).

- **Il file ha estensione *PPDF* o è un file di testo o immagine protetto, ad esempio *PTXT* o *PJPG*.**

    È possibile solo visualizzare il file e se lo si rinomina o lo si sposta, la protezione rimane con il file.

- **Altre estensioni del nome di file**

    Il dispositivo deve disporre di un'applicazione che riconosca la protezione Rights Management per usare questi file. Queste applicazioni vengono chiamate applicazioni abilitate per RMS. Le applicazioni di Office 2016, Office 2013 e Office 2010 (come Word, Excel, PowerPoint e Outlook) sono esempi di applicazioni abilitate per Rights Management. Tuttavia, anche applicazioni che non provengono da Microsoft, come altre aziende software e applicazioni line-of-business, potrebbero essere abilitate per Rights Management.

    Le applicazioni abilitate per Rights Management sono in grado di aprire i file che sono stati protetti con altre applicazioni abilitate per Rights Management. Anche queste mantengono la protezione applicata ad essi, anche se si modifica il file o lo si salva con un altro nome di file o in un altro percorso. Queste applicazioni consentono di utilizzare il file in base alle autorizzazioni applicate ad esso, in modo che se si dispone delle autorizzazioni per utilizzare il file, è possibile farlo. Ad esempio, si potrebbe essere in grado di modificare il file, ma non di stamparlo.


## <a name="examples-and-other-instructions"></a>Esempi e altre istruzioni
Per esempi di come è possibile usare l'applicazione Rights Management sharing e informazioni sulle procedure da seguire, vedere le sezioni seguenti della Guida dell'utente dell'applicazione Rights Management sharing:

-   [Esempi per l'uso dell'applicazione RMS sharing](sharing-app-user-guide.md#examples-for-using-the-rms-sharing-application)

-   [Per saperne di più](sharing-app-user-guide.md#what-do-you-want-to-do)

## <a name="see-also"></a>Vedere anche
[Guida dell'utente dell'applicazione di condivisione Rights Management](sharing-app-user-guide.md)
