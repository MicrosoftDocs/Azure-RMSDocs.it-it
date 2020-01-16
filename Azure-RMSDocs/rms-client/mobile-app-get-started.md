---
title: Introduzione - App AIP per iOS e Android
description: Visualizzare file o messaggi di posta elettronica con l'app Azure Information Protection per iOS e Android
author: rkarlin
ms.author: mlottner
manager: rkarlin
ms.date: 1/13/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 3d5d18d8-7b2e-456c-bb45-48da4eb55544
ms.reviewer: esaggese
ms.suite: ems
ms.custom: user
ms.openlocfilehash: cfae5de653497a448d10e0ac65c10ea2a6e9e4f3
ms.sourcegitcommit: 03dc2eb973b20897b30659c2ac6cb43ce0a40e71
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/15/2020
ms.locfileid: "75960834"
---
# <a name="get-started-with-the-microsoft-azure-information-protection-app-for-ios-and-android"></a>Introduzione all'app Microsoft Azure Information Protection per iOS e Android

*Si applica a: Active Directory Rights Management Services, [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*

Prima di usare le istruzioni riportate in questa pagina, leggere le [domande frequenti per l'app Azure Information Protection per iOS e Android](mobile-app-faq.md). La pagina descrive lo scopo dell'app e i dispositivi supportati e contiene informazioni di base sull'uso dell'app.

La maggior parte degli utenti usa l'app Azure Information Protection per aprire un file o un messaggio di posta elettronica protetto. Se l'amministratore vuole testare l'app per gli utenti o semplicemente provarla prima, può usare le istruzioni seguenti.

> [!NOTE]
> Evitare di aprire l'app prima di selezionare i documenti e i messaggi di posta elettronica da visualizzare. Aprire il documento o il messaggio di posta elettronica, quindi selezionare l'app per visualizzarlo.
>
> In modo analogo, accedere all'app solo dopo aver ricevuto la richiesta corrispondente.

Per usare le istruzioni seguenti è necessario accedere dal dispositivo mobile a uno dei file supportati dall'app. Ad esempio:

- **Un file con estensione rpmsg**: si tratta di un messaggio di posta elettronica protetto da diritti visualizzato come allegato in un messaggio di posta elettronica quando l'app di posta elettronica del dispositivo mobile non supporta la protezione dei dati di gestione dei diritti in modo nativo. 
    
    Usare un altro dispositivo per inviare a se stessi un messaggio di posta elettronica protetto da diritti a cui è possibile accedere dal dispositivo mobile. Ad esempio, usare Outlook da un computer Windows. Per un elenco dei client di posta elettronica che supportano Rights Management in modo nativo, vedere la colonna **posta elettronica** della prima tabella in [applicazioni che supportano la pagina protezione dati di Azure Rights Management](../requirements-applications.md) .

- **Un file PDF protetto da diritti**: da un computer Windows, usare un client Azure Information Protection ( [classico](client-classify-protect.md) o [Unified Labeling client](clientv2-classify-protect.md)) per proteggere un file PDF e quindi inviare manualmente questo file PDF protetto da diritti come allegato nel messaggio di posta elettronica. In alternativa, caricare un file PDF in una raccolta protetta di SharePoint e condividerlo usando l'indirizzo di posta elettronica.

- **A. ptxt o. pjpg o. ppng**: da un computer Windows, usare un client Azure Information Protection per proteggere un file di testo o di immagine e quindi inviare manualmente questo file protetto come allegato di posta elettronica. Per l'elenco completo dei tipi di file che è possibile usare per il test, vedere la prima tabella nella sezione [Tipi di file supportati per la classificazione e la protezione](client-admin-guide-file-types.md#supported-file-types-for-classification-and-protection) della Guida dell'amministratore del client Azure Information Protection. 

Per visualizzare questi file nell'app visualizzatore Azure Information Protection, toccare l'allegato di posta elettronica o il collegamento. Quando viene chiesto di selezionare un'app per aprire i file, selezionare l'app visualizzatore **AIP**. Verrà quindi chiesto di accedere con l'account aziendale o dell'istituto di istruzione oppure di selezionare un certificato. Dopo l'autenticazione delle credenziali, l'app Azure Information Protection visualizza il messaggio di posta elettronica o il file da leggere.

## <a name="next-steps"></a>Passaggi successivi

Per domande o commenti e suggerimenti sull'app non presenti nelle [domande frequenti](mobile-app-faq.md), visitare il [sito Yammer](https://www.yammer.com/AskIPTeam).
