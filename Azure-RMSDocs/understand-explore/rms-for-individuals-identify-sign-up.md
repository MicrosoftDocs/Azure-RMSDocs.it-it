---
title: Come determinare se gli utenti hanno effettuato l'iscrizione a RMS per utenti singoli | Azure RMS
description: 
keywords: 
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: a36c3d99-a794-4f7a-aafb-64a950f1fcf9
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 0f355da35dff62ecee111737eb1793ae286dc93e
ms.openlocfilehash: e577366be26f7296079751e72fb6531b9e28c504


---


# Come determinare se gli utenti hanno effettuato l'iscrizione per RMS per utenti singoli

*Si applica a: Azure Rights Management*

Per sapere se un utente si è iscritto per ottenere RMS per utenti singoli, un amministratore può usare uno o più tra i metodi seguenti:

-   Chiedere agli utenti in che modo proteggono i file riservati, in particolar modo quando collaborano con altre persone all'esterno dell'organizzazione.

-   Quando è disponibile una sottoscrizione di Azure per l'organizzazione, usare il cmdlet [Get-MsolAccountSku](https://msdn.microsoft.com/library/azure/dn194118.aspx) per verificare se **RIGHTSMANAGEMENT_ADHOC** viene restituito come una delle sottoscrizioni. Se restituito, si tratta di RMS per le singole sottoscrizioni concesse all'organizzazione, con un pool di unità attive disponibili per permettere agli utenti di usare il processo di iscrizione self-service.

-   Usare una soluzione di gestione di sistema, ad esempio System Center Configuration Manager, per tenere traccia del software installato e di quello in uso. L'applicazione di condivisione Microsoft Rights Management viene eseguita tramite il programma **ipviewer.exe** ed è possibile [scaricare e installare l'applicazione](http://go.microsoft.com/fwlink/?LinkId=303970) gratuitamente per identificare altre caratteristiche dell'applicazione che è possibile usare a scopo di inventario del software.

-   Prestare attenzione alle estensioni dei nomi di file creati nell'applicazione di condivisione Microsoft Rights Management. Le estensioni di file .pfile e .ppdf sono gli esempi più evidenti, ma esistono altri file la cui estensione viene modificata quando sono protetti in modalità nativa con Rights Management. Per ulteriori informazioni, vedere la sezione [Tipi ed estensioni di file supportati](../rms-client/sharing-app-admin-guide-technical.md#supported-file-types-and-file-name-extensions) nella [Guida dell'amministratore dell'applicazione di condivisione Rights Management](http://technet.microsoft.com/library/dn339003.aspx).




<!--HONumber=Jun16_HO4-->


