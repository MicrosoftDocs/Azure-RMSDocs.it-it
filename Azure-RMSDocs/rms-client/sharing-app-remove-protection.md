---
title: Rimuovere la protezione da un file usando l'applicazione Rights Management sharing | Azure Information Protection
description: Istruzioni per rimuovere la protezione da un file protetto in precedenza con l'applicazione RMS sharing.
author: cabailey
manager: mbaldwin
ms.date: 09/25/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: da95b938-eaad-4c83-a21e-ff1d4872aae4
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: aac3c6c7b5167d729d9ac89d9ae71c50dd1b6a10
ms.openlocfilehash: ceb726e47c4eb9413b7d7eb5b1469e2a99992dda


---

# Rimuovere la protezione da un file mediante l'applicazione Rights Management sharing

>*Si applica a: Active Directory Rights Management Services, Azure Information Protection, Windows 10, Windows 7 con SP1, Windows 8, Windows 8.1*

Per rimuovere la protezione da un file (ovvero lasciare un file non protetto) che in precedenza è stato protetto mediante l'applicazione RMS sharing, usare l'opzione **Rimuovi protezione** da Esplora file.

> [!IMPORTANT]
> Per rimuovere la protezione, è necessario essere proprietario del file.

## Per rimuovere la protezione da un file

1.  Da Esplora File, fare clic con il pulsante destro sul file (ad esempio, Sample.ptxt), selezionare **Proteggi tramite RMS**, fare clic su **Proteggi sul posto**, quindi fare clic su **Rimuovi protezione**:

    ![Rimuovere l'opzione di menu di protezione per l'applicazione RMS sharing](../media/ADRMS_MSRMSApp_RemoveProtection.png)

    è possibile che vengano richieste le credenziali.

Nota: se queste opzioni non sono visualizzate, è probabile che l'applicazione RMS sharing non sia installata nel computer, che non sia installata la versione più recente o che sia necessario riavviare il computer per completare l'installazione. Per ulteriori informazioni su come installare l'applicazione di condivisione, vedere [Scaricare e installare l'applicazione Rights Management sharing](install-sharing-app.md).

Il file protetto originale viene eliminato (ad esempio, Sample.ptxt) e sostituito con un file con lo stesso nome ma con l'estensione del nome del file non protetto (ad esempio Sample.txt).

## Esempi e altre istruzioni
Per esempi di come è possibile usare l'applicazione Rights Management sharing e informazioni sulle procedure da seguire, vedere le sezioni seguenti della Guida dell'utente dell'applicazione Rights Management sharing:

-   [Esempi per l'uso dell'applicazione RMS sharing](sharing-app-user-guide.md#examples-for-using-the-rms-sharing-application)

-   [Come procedere](sharing-app-user-guide.md#what-do-you-want-to-do)

## Vedere anche
[Guida dell'utente dell'applicazione Rights Management sharing](sharing-app-user-guide.md)



<!--HONumber=Sep16_HO4-->


