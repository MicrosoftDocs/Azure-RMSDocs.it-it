---
title: Come determinare se gli utenti hanno effettuato l&quot;iscrizione a RMS per utenti singoli | Azure Information Protection
description: "Per sapere se un utente si è iscritto per ottenere RMS per utenti singoli, È possibile usare uno qualsiasi o una combinazione dei metodi descritti in questo articolo."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 10/24/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: a36c3d99-a794-4f7a-aafb-64a950f1fcf9
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 9d8354f2d68f211d349226970fd2f83dd0ce810b
ms.openlocfilehash: b9979d48af7146f8021de840248f71cb1399b777


---


# <a name="how-to-find-out-if-your-users-have-signed-up-for-rms-for-individuals"></a>Come determinare se gli utenti hanno effettuato l'iscrizione per RMS per utenti singoli

>*Si applica a: Azure Information Protection*

Per sapere se un utente si è iscritto per ottenere RMS per utenti singoli, un amministratore può usare uno o più tra i metodi seguenti:

-   Chiedere agli utenti in che modo proteggono i file riservati, in particolar modo quando collaborano con altre persone all'esterno dell'organizzazione.

-   Quando è disponibile una sottoscrizione di Azure per l'organizzazione, usare il cmdlet [Get-MsolAccountSku](https://msdn.microsoft.com/library/azure/dn194118.aspx) per verificare se **RIGHTSMANAGEMENT_ADHOC** viene restituito come una delle sottoscrizioni. Se restituito, si tratta di RMS per le singole sottoscrizioni concesse all'organizzazione, con un pool di unità attive disponibili per permettere agli utenti di usare il processo di iscrizione self-service.

-   Usare una soluzione di gestione di sistema, ad esempio System Center Configuration Manager, per tenere traccia del software installato e di quello in uso. L'applicazione Rights Management sharing viene eseguita tramite il programma **ipviewer.exe** ed è possibile [scaricare e installare l'applicazione](http://go.microsoft.com/fwlink/?LinkId=303970) gratuitamente per identificare altre caratteristiche dell'applicazione che è possibile usare a scopo di inventario del software.

-   Prestare attenzione alle estensioni dei nomi di file creati dall'applicazione Rights Management sharing. Le estensioni .pfile e .ppdf sono gli esempi più evidenti, ma esistono altri file la cui estensione viene modificata quando sono protetti in modalità nativa con il servizio Rights Management. Per altre informazioni, vedere la sezione [Tipi ed estensioni di file supportati](../rms-client/sharing-app-admin-guide-technical.md#supported-file-types-and-file-name-extensions) nella [Guida dell'amministratore dell'applicazione Rights Management sharing](http://technet.microsoft.com/library/dn339003.aspx).




<!--HONumber=Nov16_HO2-->


