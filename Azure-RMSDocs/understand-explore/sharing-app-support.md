---
title: App RMS sharing per piattaforme Windows e mobili - AIP
description: Informazioni su come l'applicazione RMS sharing supporta Azure RMS come applicazione scaricabile gratuita, necessaria per supportare Office 2010, ma consigliata anche per computer Windows e Mac e dispositivi mobili.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/08/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 1da6e372-2b3f-4af7-80f7-6b9073dff7f5
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 3c96d8718f42dcedebba03354c149bb2b9667d66
ms.sourcegitcommit: 04eb4990e2bf0004684221592cb93df35e6acebe
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/30/2017
---
# <a name="rms-sharing-application-for-windows-and-mobile-platforms"></a>Applicazione RMS sharing per piattaforme Windows e mobili

>*Si applica a: Azure Information Protection, Office 365*

> [!IMPORTANT]
> **Notifica di fine del supporto**: l'applicazione di condivisione Rights Management per Windows verrà sostituita dal [client Azure Information Protection](../rms-client/aip-client.md). Il supporto per questa applicazione precedente terminerà il 31 gennaio 2018. 
 
L'applicazione RMS sharing è un'applicazione scaricabile che supporta Office 2010 per i computer Windows, ma in passato consigliata anche per tutti i computer Windows e i dispositivi mobili. È ancora consigliata per i computer Mac e i dispositivi Windows Phone. L'applicazione RMS sharing è particolarmente vantaggiosa perché consente di applicare la protezione generica ad applicazioni e file senza supporto nativo per il servizio Azure Rights Management, il che significa che tutti i file possono essere protetti. Per altre informazioni sui diversi livelli di protezione, vedere la sezione [Livelli di protezione – nativo e generico](../rms-client/sharing-app-admin-guide-technical.md#levels-of-protection--native-and-generic) della [Guida dell'amministratore dell'applicazione Rights Management sharing](../rms-client/sharing-app-admin-guide.md).

Quando gli utenti proteggono i file usando l'applicazione RMS sharing, possono anche tenere traccia dei documenti protetti e, se necessario, revocarne l'accesso. A tale scopo, usare il [sito di rilevamento del documento](http://go.microsoft.com/fwlink/?LinkId=529562).

Per computer Windows, l'applicazione RMS sharing si integra in modo semplice con le applicazioni giù usate dagli utenti, contribuendo anche a migliorarle:

-   Viene installato un componente aggiuntivo di Office per Word, Excel, PowerPoint e Outlook. In questo modo gli utenti possono usare un pulsante **Condividi file protetto** sulla barra multifunzione che consente di visualizzare una semplice finestra di dialogo con le impostazioni usate più di frequente per proteggere i file da inviare tramite posta elettronica. Questo pulsante consente anche un rapido accesso al sito di rilevamento del documento.

-   È disponibile una nuova opzione di scelta rapida in Esplora file In questo modo gli utenti possono usare l'opzione **Proteggi sul posto** che consente di visualizzare una semplice finestra di dialogo con le impostazioni usate più di frequente per proteggere file archiviati su un disco.

-   Viene installato un visualizzatore per aprire i file protetti con il servizio Azure Rights Management, richiamato automaticamente quando non è installata alcuna applicazione in grado di aprire il file protetto.

-   Configurazione back-end per Office 2010 che consente alle versioni di Word, Excel, PowerPoint e Outlook di questa famiglia di prodotti di integrarsi facilmente con il servizio Azure Rights Management.

Sebbene sia possibile scaricare l'applicazione RMS sharing per Windows e installarla in un singolo computer tramite la [pagina di Microsoft Rights Management](http://go.microsoft.com/fwlink/?LinkId=303970), è supportata anche una distribuzione aziendale per l'installazione invisibile all'utente e la configurazione personalizzata. Per altre informazioni, vedere le risorse seguenti:

-   [Guida dell'amministratore dell'applicazione di condivisione Rights Management](../rms-client/sharing-app-admin-guide.md)

-   [Guida dell'utente dell'applicazione di condivisione Rights Management](../rms-client/sharing-app-user-guide.md)

L'applicazione RMS sharing per dispositivi mobili supporta i dispositivi di questo tipo usati più di frequente, ad esempio iPad e iPhone nonché dispositivi Android, Windows Phone e Windows RT. Gli utenti possono scaricare questa app dallo Store pertinente cui è possibile accedere dai collegamenti presenti nella [pagina di Microsoft Rights Management](http://go.microsoft.com/fwlink/?LinkId=303970).

**Se si ha Microsoft Intune**: poiché l'app RMS sharing include il kit di sviluppo del software per l'app Microsoft Intune, sono disponibili le opzioni seguenti:

-   Distribuire e gestire l'app per i dispositivi iOS e Android registrati da Intune.

-   Gestire l'app per i dispositivi Android non registrati da Intune.


## <a name="next-steps"></a>Passaggi successivi
Per informazioni su come altri servizi e applicazioni supportano il servizio Azure Rights Management di Azure Information Protection, vedere [Supporto del servizio Azure Rights Management da parte delle applicazioni](applications-support.md).

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
