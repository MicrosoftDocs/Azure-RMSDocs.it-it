---
title: Introduzione - App AIP per iOS e Android
description: 
keywords: Come visualizzare file o messaggi di posta elettronica con l'app Azure Information Protection per iOS e Android
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 10/16/2017
ms.topic: article
ms.prod: azure
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 3d5d18d8-7b2e-456c-bb45-48da4eb55544
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: db44f73c20d7440d403b1d3a7a7ea0201f8a7abb
ms.sourcegitcommit: 965108d50739148864b2ae7dcc661ae65f1b154c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/17/2017
---
# <a name="get-started-with-the-microsoft-azure-information-protection-app-for-ios-and-android"></a>Introduzione all'app Microsoft Azure Information Protection per iOS e Android

*Si applica a: Active Directory Rights Management Services, Azure Information Protection*

Prima di usare le istruzioni riportate in questa pagina, leggere le [domande frequenti per l'app Azure Information Protection per iOS e Android](mobile-app-faq.md). La pagina descrive lo scopo dell'app e i dispositivi supportati e contiene informazioni di base sull'uso dell'app.

La maggior parte degli utenti usa l'app Azure Information Protection per aprire un file o un messaggio di posta elettronica protetto. Se l'amministratore vuole testare l'app per gli utenti o semplicemente provarla prima, può usare le istruzioni seguenti.

> [!NOTE]
> Evitare di aprire l'app prima di selezionare i documenti e i messaggi di posta elettronica da visualizzare. Aprire il documento o il messaggio di posta elettronica, quindi selezionare l'app per visualizzarlo.
>
> In modo analogo, accedere all'app solo dopo aver ricevuto la richiesta corrispondente.

Per usare le istruzioni seguenti è necessario accedere dal dispositivo mobile a uno dei file supportati dall'app. Ad esempio:

- **Un file con estensione rpmsg**: si tratta di un messaggio di posta elettronica protetto da diritti visualizzato come allegato in un messaggio di posta elettronica quando l'app di posta elettronica del dispositivo mobile non supporta la protezione dei dati di gestione dei diritti in modo nativo. 
    
    Usare un altro dispositivo per inviare a se stessi un messaggio di posta elettronica protetto da diritti a cui è possibile accedere dal dispositivo mobile. Ad esempio, usare Outlook da un computer Windows. Per un elenco dei client di posta elettronica che supportano la gestione dei diritti in modo nativo, vedere la colonna POSTA ELETTRONICA nella pagina [Applicazioni che supportano la protezione dati di Azure Rights Management](../get-started/requirements-applications.md).

- **Un file PDF protetto tramite diritti**: da un computer Windows usare il client Azure Information Protection per [proteggere un file PDF](client-classify-protect.md) e quindi inviare a se stessi il file PDF protetto tramite diritti come allegato di un messaggio di posta elettronica. In alternativa, caricare un file PDF in una raccolta protetta di SharePoint e condividerlo usando l'indirizzo di posta elettronica.

- **Un file PTXT o PJPG o PPNG**: da un computer Windows usare il client Azure Information Protection per proteggere un file di testo o immagine e quindi inviare a se stessi il file protetto come allegato di un messaggio di posta elettronica. Per l'elenco completo dei tipi di file che è possibile usare per il test, vedere la prima tabella nella sezione [Tipi di file supportati per la classificazione e la protezione](client-admin-guide-file-types.md#supported-file-types-for-classification-and-protection) della Guida dell'amministratore del client Azure Information Protection. 

Per visualizzare questi file nell'app visualizzatore Azure Information Protection, toccare l'allegato di posta elettronica o il collegamento. Quando viene chiesto di selezionare un'app per aprire i file, selezionare l'app visualizzatore **AIP**. Verrà quindi chiesto di accedere con l'account aziendale o dell'istituto di istruzione oppure di selezionare un certificato. Dopo l'autenticazione delle credenziali, l'app Azure Information Protection visualizza il messaggio di posta elettronica o il file da leggere.

## <a name="next-steps"></a>Passaggi successivi

Per domande o commenti e suggerimenti sull'app non presenti nelle [domande frequenti](mobile-app-faq.md), visitare il [sito Yammer](https://www.yammer.com/AskIPTeam).

Se l'app non funziona come descritto, vedere le risorse elencate nella pagina delle [regole interne](../house-rules.md).

[!INCLUDE[Commenting house rules](../includes/houserules.md)]