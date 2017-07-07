---
title: Determinare se gli utenti hanno effettuato l'iscrizione a RMS per utenti singoli - AIP
description: "Per sapere se un utente si è iscritto per ottenere RMS per utenti singoli, È possibile usare uno qualsiasi o una combinazione dei metodi descritti in questo articolo."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/08/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: a36c3d99-a794-4f7a-aafb-64a950f1fcf9
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: e696bf596255b5e28aa5589cfc18715f100c5b07
ms.sourcegitcommit: 04eb4990e2bf0004684221592cb93df35e6acebe
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/30/2017
---
# <a name="how-to-find-out-if-your-users-have-signed-up-for-rms-for-individuals"></a>Come determinare se gli utenti hanno effettuato l'iscrizione per RMS per utenti singoli

>*Si applica a: Azure Information Protection*

Per sapere se un utente si è iscritto per ottenere RMS per utenti singoli, un amministratore può usare uno o più tra i metodi seguenti:

-   Chiedere agli utenti in che modo proteggono i file riservati, in particolar modo quando collaborano con altre persone all'esterno dell'organizzazione.

-   Quando si ha una sottoscrizione di Azure per l'organizzazione, usare il cmdlet [Get-MsolAccountSku](https://msdn.microsoft.com/library/azure/dn194118.aspx) per verificare se agli utenti è assegnata la licenza **RIGHTSMANAGEMENT_ADHOC**. Questa licenza è associata alla sottoscrizione di RMS per utenti singoli concessa all'organizzazione, con un pool di unità attive disponibili per permettere agli utenti di usare il processo di iscrizione self-service.

-   Usare una soluzione di gestione di sistema, ad esempio System Center Configuration Manager, per tenere traccia del software installato e di quello in uso. Cercare, ad esempio, **MSIP.App.exe**, usato dal client Azure Information Protection, e **ipviewer.exe** per l'applicazione di condivisione Rights Management. È possibile scaricare e installare questo client e questa applicazione gratuitamente, per identificare altre caratteristiche da usare per l'inventario software.

-   Prestare attenzione alle estensioni di file create dal client Azure Information Protection o dall'applicazione di condivisione Rights Management. Le estensioni .pfile e .ppdf sono gli esempi più evidenti, ma esistono altri file la cui estensione viene modificata quando sono protetti in modalità nativa con il servizio Rights Management. Per altre informazioni, vedere la sezione [Tipi di file supportati per la protezione](../rms-client/client-admin-guide-file-types.md#file-types-supported-for-protection) nella Guida dell'amministratore del client Azure Information Protection.

[!INCLUDE[Commenting house rules](../includes/houserules.md)]