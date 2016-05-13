---
# required metadata

title: Configurare l'ambiente di test | Azure RMS
description: L'applicazione abilitata all'uso di diritti può essere testata con diverse opzioni del server.
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 4d32682c-754d-4e30-977d-95b08e0662cc

# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

﻿
# Configurare l'ambiente di test

L'applicazione abilitata all'uso di diritti può essere testata con diverse opzioni del server.

**Importante** È consigliabile testare l'applicazione Rights Management Services SDK 2.1 prima con l'ambiente di pre-produzione AD RMS in un server AD RMS. Quindi, se si vuole consentire al cliente di usare l'applicazione con il servizio Azure RMS, eseguire il test in tale ambiente. Per altre informazioni, vedere [Consentire all'applicazione di servizio di usare RMS basato su cloud](how-to-use-file-api-with-aadrm-cloud.md).

 

### Prerequisiti

-   [Installare l'SDK](create-your-first-rights-aware-application.md)

Istruzioni

### Passaggio 1: Configurare l'ambiente di test

Per testare l'applicazione abilitata all'uso di diritti, è necessario eseguirla in un server RMS configurato per la pre-produzione. Un server RMS di pre-produzione usa la gerarchia di certificati di pre-produzione/ISV per crittografare e decrittografare i file.

Per altre informazioni sulla gerarchia di certificati AD RMS, vedere [informazioni sulle catene di certificati](understanding-certificate-chains.md).

Per il test dell'applicazione in un server RMS sono disponibili due opzioni:

-   **È possibile eseguire l'applicazione nell'ambiente ISV AD RMS 1-box**. Se si esegue Windows Server 2012, Windows Server 2008 R2 o Windows Server 2008 e Hyper-V è installato, è possibile distribuire l'ambiente ISV AD RMS 1-box creando una macchina virtuale con VHD 1-box AD RMS. L'ambiente ISV AD RMS 1-box fornisce un server RMS configurato per la pre-produzione e in tale ambiente è anche installato Active Directory Rights Management Services Client 2.1. Le impostazioni del Registro di sistema per il client e il server RMS sono già configurate. Per testare l'applicazione, eseguirla nella macchina virtuale in cui viene distribuito l'ambiente 1-box.
-   **È possibile eseguire l'applicazione in un server RMS configurato per la pre-produzione e distribuito nella rete**. In questo caso, è anche necessario installare e configurare AD RMS Client 2.1 nel computer in cui verrà eseguita l'applicazione. Per informazioni su questa operazione, vedere [Configurare il client](how-to-configure-the-ad-rms-client-2-0.md). Per informazioni su come distribuire un server RMS e configurarlo per la pre-produzione, vedere [installare e configurare il server](how-to-install-and-configure-an-rms-server.md).

### Argomenti correlati

* [Modalità d'uso](how-to-use-msipc.md)
* [Pagina di download di documentazione e materiale aggiuntivo del webinar su AD RMS SDK](https://connect.microsoft.com/site1170/Downloads/DownloadDetails.aspx?DownloadID=42440)
* [Configurare il client](how-to-configure-the-ad-rms-client-2-0.md)
* [Installare l'SDK](create-your-first-rights-aware-application.md)
* [Installare e configurare il server](how-to-install-and-configure-an-rms-server.md)
* [Informazioni sulle catene di certificati](understanding-certificate-chains.md)
 

 





<!--HONumber=Apr16_HO3-->


