---
title: Rimuovere la protezione da un file usando l'applicazione di condivisione Rights Management | Azure RMS
description: 
keywords: 
author: cabailey
manager: mbaldwin
ms.date: 05/09/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: da95b938-eaad-4c83-a21e-ff1d4872aae4
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: c611fa8a846612fed238e59e5077be67f6f9531a
ms.openlocfilehash: 78ceb74a3dd8492ac5c754eea179525cae819fd0


---

# Rimuovere la protezione da un file mediante l'applicazione di condivisione Rights Management

*Si applica a: Active Directory Rights Management Services, Azure Rights Management, Windows 10, Windows 7 con SP1, Windows 8, Windows 8.1*

Per rimuovere la protezione da un file (ovvero lasciare un file non protetto) che in precedenza è stato protetto utilizzando l'applicazione di condivisione RMS, utilizzare l’opzione **Rimuovi protezione** da Esplora File.

> [!IMPORTANT]
> Per rimuovere la protezione, è necessario essere proprietario del file.

## Per rimuovere la protezione da un file

1.  Da Esplora File, fare clic con il pulsante destro sul file (ad esempio, Sample.ptxt), selezionare **Proteggi tramite RMS**, fare clic su **Proteggi sul posto**, quindi fare clic su **Rimuovi protezione**:

    ![Rimuovere l'opzione di menu di protezione per l'applicazione di condivisione RMS](../media/ADRMS_MSRMSApp_RemoveProtection.png)

    è possibile che vengano richieste le credenziali.

Nota: se non vengono visualizzate queste opzioni, è probabile che l'applicazione di condivisione RMS non sia installata nel computer, che non sia installata la versione più recente o che sia necessario riavviare il computer per completare l'installazione. Per ulteriori informazioni su come installare l’applicazione di condivisione, vedere [Scaricare e installare l’applicazione di condivisione Rights Management](install-sharing-app.md).

Il file protetto originale viene eliminato (ad esempio, Sample.ptxt) e sostituito con un file con lo stesso nome ma con l'estensione del nome del file non protetto (ad esempio Sample.txt).

## Esempi e altre istruzioni
Per esempi di come è possibile utilizzare l'applicazione di condivisione Rights Management e procedure, vedere le sezioni seguenti della Guida dell’utente dell’applicazione di condivisione Rights Management:

-   [Esempi per l'utilizzo dell’applicazione di condivisione RMS](sharing-app-user-guide.md#examples-for-using-the-rms-sharing-application)

-   [Come procedere](sharing-app-user-guide.md#what-do-you-want-to-do-)

## Vedere anche
[Guida dell'utente dell'applicazione di condivisione Rights Management](sharing-app-user-guide.md)



<!--HONumber=Jun16_HO4-->


