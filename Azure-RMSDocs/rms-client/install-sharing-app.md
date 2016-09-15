---
title: Scaricare e installare l'applicazione di condivisione Rights Management | Azure RMS
description: "Istruzioni per l'installazione in modo interattivo dell'applicazione RMS sharing per Windows, affinché sia possibile condividere documenti in modo sicuro con altri utenti."
author: cabailey
manager: mbaldwin
ms.date: 08/25/2016
ms.topic: article
ms.prod: 
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 2bf09690-9dba-43b7-9e0a-0110915d4081
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 44541b6fe2567d23174b26cb42fec0731f5d3f58
ms.openlocfilehash: b01896dc49a6c581427393f9e3fc21dbbd235238


---

# Scaricare e installare l’applicazione di condivisione Rights Management

>*Si applica a: Active Directory Rights Management Services, Azure Rights Management, Windows 10, Windows 7 con SP1, Windows 8, Windows 8.1*

Non è necessario essere un amministratore locale per installare l'applicazione di condivisione RMS. Tuttavia, se non si ricopre questo ruolo e si usa Office 2010, sono previste alcune limitazioni. Per ulteriori informazioni, vedere la sezione [Se non si è un amministratore locale e si usa Office 2010](#if-you-are-not-a-local-administrator-and-use-office-2010) di questa pagina.

## Per scaricare e installare l’applicazione di condivisione Rights Management

1.  Accedere alla pagina [Microsoft Rights Management](http://go.microsoft.com/fwlink/?LinkId=303970) nel sito Web Microsoft.

2.  Nella sezione **Computer** fare clic sull'icona relativa all’ **app RMS per Windows** e salvare il file di installazione **Setup.exe** dell’applicazione di condivisione Microsoft Rights Management.

3.  Fare doppio clic sul file Setup.exe che è stato scaricato. Se viene chiesto di continuare, fare clic su **Sì**.

4.  Nella pagina **Installazione di Microsoft RMS** fare clic su **Avanti**e attendere il completamento dell'installazione.

    > [!NOTE]
    > L'applicazione di condivisione RMS richiede il Framework Microsoft .NET, versione minima 4.0. Il programma di installazione verifica se viene installato e in caso contrario, verrà visualizzato un messaggio con un collegamento per installarlo.

5.  Al termine dell'installazione, fare clic su **Riavvia** per riavviare il computer e completare l'installazione. Fare clic su **Chiudi** e riavviare il computer in un secondo momento per completare l'installazione.

Ora è possibile iniziare a proteggere i file o a leggere quelli protetti da altri utenti.

## Se non si è un amministratore locale e si usa Office 2010
Se si accede al computer senza diritti amministrativi locali e il programma di installazione rileva che nel sistema è installato Office 2010, verrà visualizzato un messaggio di avviso in cui si specifica che alcuni scenari non sono compatibili con questa configurazione. Questi scenari includono:

-   Se l'organizzazione usa Azure RMS anziché una versione locale di RMS:

    -   Non saranno disponibili le funzionalità Information Rights Management (IRM) di Office, come l'opzione **Non inoltrare** per i messaggi di posta elettronica e le autorizzazioni **Limita accesso** che è possibile impostare dal menu **File** di Word ed Excel. È possibile invece usare l'opzione di condivisione protetta disponibile sulla barra multifunzione e le opzioni del menu di scelta rapida di Esplora file.

-   Se l'organizzazione usa una versione locale di RMS anziché Azure RMS:

    -   Non sarà possibile leggere documenti protetti inviati da utenti appartenenti a un'altra organizzazione in cui viene usato Azure RMS.

Se non si è un amministratore locale ma si usa Office 365 o Office 2013, il messaggio non viene visualizzato e questi scenari sono supportati.

È possibile continuare l'installazione tenendo conto di queste limitazioni oppure è possibile interrompere l'installazione e scegliere di effettuarla di nuovo selezionando l'opzione **Esegui come amministratore** quando si esegue il file Setup.exe nel passaggio 3 o di affidarla a un amministratore. Gli amministratori possono infatti [generare lo script dell'installazione](sharing-app-admin-guide.md#automatic-deployment-for-the-microsoft-rights-management-sharing-application) in modo che venga eseguita automaticamente.

## Esempi e altre istruzioni
Per esempi di come è possibile utilizzare l'applicazione di condivisione Rights Management e procedure, vedere le sezioni seguenti della Guida dell’utente dell’applicazione di condivisione Rights Management:

-   [Esempi per l'utilizzo dell’applicazione di condivisione RMS](sharing-app-user-guide.md#examples-for-using-the-rms-sharing-application)

-   [Come procedere](sharing-app-user-guide.md#what-do-you-want-to-do)

## Vedere anche
[Guida dell'utente dell'applicazione di condivisione Rights Management](sharing-app-user-guide.md)




<!--HONumber=Aug16_HO4-->


