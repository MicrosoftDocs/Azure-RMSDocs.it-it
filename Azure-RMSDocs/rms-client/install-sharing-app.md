---
title: Scaricare e installare l'app RMS sharing - AIP
description: Istruzioni per l'installazione in modo interattivo dell'applicazione RMS sharing per Windows, affinché sia possibile condividere documenti in modo sicuro con altri utenti.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 01/23/2017
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 2bf09690-9dba-43b7-9e0a-0110915d4081
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 80ae87e28e02a208af9ea4ece2b74df1a7f841b0
ms.sourcegitcommit: 44ff610dec678604c449d42cc0b0863ca8224009
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/31/2018
ms.locfileid: "39374559"
---
# <a name="download-and-install-the-rights-management-sharing-application"></a>Scaricare e installare l'applicazione Rights Management sharing

>*Si applica a: Active Directory Rights Management Services, [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 7 con SP1, Windows 8, Windows 8.1*

> [!IMPORTANT]
> **Notifica di fine del supporto**: l'applicazione di condivisione Rights Management per Windows verrà sostituita dal [client Azure Information Protection](aip-client.md). Il supporto per questa applicazione precedente terminerà il 31 gennaio 2019.

Non è necessario essere un amministratore locale per installare l'applicazione RMS sharing. Tuttavia, se non si ricopre questo ruolo e si usa Office 2010, sono previste alcune limitazioni. Per ulteriori informazioni, vedere la sezione [Se non si è un amministratore locale e si usa Office 2010](#if-you-are-not-a-local-administrator-and-use-office-2010) di questa pagina.

## <a name="to-download-and-install-the-rights-management-sharing-application"></a>Per scaricare e installare l'applicazione Rights Management sharing

1.  Accedere alla pagina [Microsoft Rights Management](http://go.microsoft.com/fwlink/?LinkId=303970) nel sito Web Microsoft.

2.  Nella sezione **Computer** fare clic sull'icona relativa all'**app RMS per Windows** e salvare il file di installazione **Setup.exe** dell'applicazione Microsoft Rights Management sharing.

3.  Fare doppio clic sul file Setup.exe che è stato scaricato. Se viene chiesto di continuare, fare clic su **Sì**.

4.  Nella pagina **Installazione di Microsoft RMS** fare clic su **Avanti**e attendere il completamento dell'installazione.

    > [!NOTE]
    > L'applicazione RMS sharing richiede almeno la versione 4.0 di Microsoft .NET Framework. Il programma di installazione verifica se viene installato e in caso contrario, verrà visualizzato un messaggio con un collegamento per installarlo.

5.  Al termine dell'installazione, fare clic su **Riavvia** per riavviare il computer e completare l'installazione. Fare clic su **Chiudi** e riavviare il computer in un secondo momento per completare l'installazione.

Ora è possibile iniziare a proteggere i file o a leggere quelli protetti da altri utenti.

## <a name="if-you-are-not-a-local-administrator-and-use-office-2010"></a>Se non si è un amministratore locale e si usa Office 2010
Se si accede al computer senza diritti amministrativi locali e il programma di installazione rileva che nel sistema è installato Office 2010, verrà visualizzato un messaggio di avviso in cui si specifica che alcuni scenari non sono compatibili con questa configurazione. Questi scenari includono:

-   Se l'organizzazione usa il servizio Azure Rights Management di Azure Information Protection anziché una versione locale di Rights Management:

    -   Non saranno disponibili le funzionalità Information Rights Management (IRM) di Office, come l'opzione **Non inoltrare** per i messaggi di posta elettronica e le autorizzazioni **Limita accesso** che è possibile impostare dal menu **File** di Word ed Excel. È possibile invece usare l'opzione di condivisione protetta disponibile sulla barra multifunzione e le opzioni del menu di scelta rapida di Esplora file.

-   Se l'organizzazione usa una versione locale di Rights Management anziché il servizio Azure Rights Management di Azure Information Protection:

    -   Non sarà possibile leggere documenti protetti inviati da utenti appartenenti a un'altra organizzazione in cui viene usato il servizio Azure Rights Management.

Se non si è un amministratore locale ma si usa Office 365 o Office 2013, il messaggio non viene visualizzato e questi scenari sono supportati.

È possibile continuare l'installazione tenendo conto di queste limitazioni oppure è possibile interrompere l'installazione e scegliere di effettuarla di nuovo selezionando l'opzione **Esegui come amministratore** quando si esegue il file Setup.exe nel passaggio 3 o di affidarla a un amministratore. Gli amministratori possono infatti [generare lo script dell'installazione](sharing-app-admin-guide.md#automatic-deployment-for-the-microsoft-rights-management-sharing-application) in modo che venga eseguita automaticamente.

## <a name="examples-and-other-instructions"></a>Esempi e altre istruzioni
Per esempi di come è possibile usare l'applicazione Rights Management sharing e informazioni sulle procedure da seguire, vedere le sezioni seguenti della Guida dell'utente dell'applicazione Rights Management sharing:

-   [Esempi per l'uso dell'applicazione RMS sharing](sharing-app-user-guide.md#examples-for-using-the-rms-sharing-application)

-   [Per saperne di più](sharing-app-user-guide.md#what-do-you-want-to-do)

## <a name="see-also"></a>Vedere anche
[Guida dell'utente dell'applicazione di condivisione Rights Management](sharing-app-user-guide.md)

