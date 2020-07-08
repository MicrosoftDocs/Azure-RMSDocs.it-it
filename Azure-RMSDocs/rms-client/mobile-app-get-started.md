---
title: Introduzione - App AIP per iOS e Android
description: Visualizzare file o messaggi di posta elettronica con l'app Azure Information Protection per iOS e Android
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 07/07/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 3d5d18d8-7b2e-456c-bb45-48da4eb55544
ms.reviewer: esaggese
ms.suite: ems
ms.custom: user
ms.openlocfilehash: 4b50f89c9f8d0a965b630c82461f1190bb893938
ms.sourcegitcommit: 223e26b0ca4589317167064dcee82ad0a6a8d663
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/07/2020
ms.locfileid: "86048698"
---
# <a name="get-started-with-the-microsoft-azure-information-protection-app-for-ios-and-android"></a>Introduzione all'app Microsoft Azure Information Protection per iOS e Android

*Si applica a: Active Directory Rights Management Services, [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*

Questa pagina descrive come testare l'esecuzione delle app Azure Information Protection per iOS o Android.

La maggior parte degli utenti usa l'app Azure Information Protection per aprire un file o un messaggio di posta elettronica protetto. Tuttavia, se si è un amministratore che testa l'app per gli utenti o se si vuole semplicemente provarla prima di usarla, usare le istruzioni riportate di seguito per visualizzare i file protetti nel dispositivo.

> [!IMPORTANT]
> Prima di iniziare, leggere i requisiti e le istruzioni per informazioni sull' [app Azure Information Protection per iOS o Android.](mobile-app-faq.md)
> 

## <a name="access-a-protected-file-from-your-device"></a>Accedere a un file protetto dal dispositivo

Per testare l'app per dispositivi mobili AIP, verificare che sia possibile accedere a uno dei seguenti tipi di file protetti dal dispositivo:

|Tipo file  |Istruzioni  |
|---------|---------|
|**Un file con estensione rpmsg**     | Un messaggio di posta elettronica protetto da diritti. Se l'app di posta elettronica mobile non supporta in modo nativo la protezione dati di Rights Management, i messaggi di posta elettronica protetti vengono visualizzati come allegati di posta elettronica </br></br>Usare un altro dispositivo, ad esempio Outlook, da un computer Windows, per inviare a se stessi un messaggio di posta elettronica protetto da diritti a cui è possibile accedere dal dispositivo mobile. </br></br>**Nota:** Per un elenco dei client di posta elettronica che supportano Rights Management in modo nativo, vedere la colonna **posta elettronica** nelle [applicazioni abilitate per RMS](../requirements-applications.md#rms-enlightened-applications). |
|**Un file PDF protetto da diritti**     | 1. da un computer Windows proteggere un file PDF usando il client client AIP [classico](client-classify-protect.md) o [Unified Labeling](clientv2-classify-protect.md) . </br>2. inviare manualmente il file PDF protetto oppure caricarlo in una libreria protetta da SharePoint e condividerlo con il proprio indirizzo di posta elettronica.        |
|**A. ptxt o. pjpg o. ppng**     | 1. da un computer Windows proteggere un file di testo o di immagine usando il client client AIP [classico](client-classify-protect.md) o [Unified Labeling](clientv2-classify-protect.md) . </br></br>2. inviare manualmente il file protetto oppure caricarlo in una raccolta protetta di SharePoint e condividerlo con il proprio indirizzo di posta elettronica. </br></br>**Nota:** Per ulteriori informazioni, vedere [tipi di file supportati per la classificazione e la protezione](client-admin-guide-file-types.md#supported-file-types-for-classification-and-protection)   |
| | |

### <a name="open-the-protected-file-on-your-mobile"></a>Aprire il file protetto sul dispositivo mobile

1. Toccare l'allegato di posta elettronica o il collegamento per aprire il contenuto protetto.

1. Quando richiesto, selezionare l'app **Visualizzatore AIP** per visualizzare il contenuto protetto.

1. Quando richiesto, accedere con l'account aziendale o dell'Istituto di istruzione o selezionare un certificato.

Una volta eseguita l'autenticazione, l'app visualizzatore AIP Visualizza il messaggio di posta elettronica o il file.

> [!NOTE]
> Aprire sempre l'app AIP aprendo il contenuto protetto. Non tentare di accedere all'app fino a quando non viene richiesto o aprire un file protetto dall'app di AIP Viewer.
> 

## <a name="next-steps"></a>Passaggi successivi

Per fornire commenti e suggerimenti sulle app per dispositivi mobili AIP, usare uno dei metodi seguenti:

- Passare a **Impostazioni**  >  **Invia feedback**
- Invia una domanda nel [sito di Yammer](https://www.yammer.com/AskIPTeam)