---
title: Come determinare se gli utenti hanno effettuato l'iscrizione a RMS per utenti singoli | Azure RMS
description: "Per sapere se un utente si è iscritto per ottenere RMS per utenti singoli, un amministratore può usare uno o più di questi metodi."
author: cabailey
manager: mbaldwin
ms.date: 08/24/2016
ms.topic: article
ms.prod: 
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: a36c3d99-a794-4f7a-aafb-64a950f1fcf9
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 024a29d7c7db2e4c0578a95c93e22f8e7a5b173e
ms.openlocfilehash: dc8c0a69078ffa3be87a5fb02bf86d9afe2dc27e


---


# Come determinare se gli utenti hanno effettuato l'iscrizione per RMS per utenti singoli

>*Si applica a: Azure Rights Management*

Per sapere se un utente si è iscritto per ottenere RMS per utenti singoli, un amministratore può usare uno o più tra i metodi seguenti:

-   Chiedere agli utenti in che modo proteggono i file riservati, in particolar modo quando collaborano con altre persone all'esterno dell'organizzazione.

-   Quando è disponibile una sottoscrizione di Azure per l'organizzazione, usare il cmdlet [Get-MsolAccountSku](https://msdn.microsoft.com/library/azure/dn194118.aspx) per verificare se **RIGHTSMANAGEMENT_ADHOC** viene restituito come una delle sottoscrizioni. Se restituito, si tratta di RMS per le singole sottoscrizioni concesse all'organizzazione, con un pool di unità attive disponibili per permettere agli utenti di usare il processo di iscrizione self-service.

-   Usare una soluzione di gestione di sistema, ad esempio System Center Configuration Manager, per tenere traccia del software installato e di quello in uso. L'applicazione di condivisione Microsoft Rights Management viene eseguita tramite il programma **ipviewer.exe** ed è possibile [scaricare e installare l'applicazione](http://go.microsoft.com/fwlink/?LinkId=303970) gratuitamente per identificare altre caratteristiche dell'applicazione che è possibile usare a scopo di inventario del software.

-   Prestare attenzione alle estensioni dei nomi di file creati nell'applicazione di condivisione Microsoft Rights Management. Le estensioni di file .pfile e .ppdf sono gli esempi più evidenti, ma esistono altri file la cui estensione viene modificata quando sono protetti in modalità nativa con Rights Management. Per ulteriori informazioni, vedere la sezione [Tipi ed estensioni di file supportati](../rms-client/sharing-app-admin-guide-technical.md#supported-file-types-and-file-name-extensions) nella [Guida dell'amministratore dell'applicazione di condivisione Rights Management](http://technet.microsoft.com/library/dn339003.aspx).




<!--HONumber=Aug16_HO4-->


