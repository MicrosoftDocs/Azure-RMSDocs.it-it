---
title: Server AD RMS | Azure RMS
description: "Il componente server di Rights Management Services (RMS) è implementato da un set di servizi Web in esecuzione in Microsoft Internet Information Services."
keywords: 
author: bruceperlerms
ms.author: bruceper
manager: mbaldwin
ms.date: 02/23/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 17B05780-B0EF-4805-8304-52DCDEB3AADB
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 7068e0529409eb783f16bc207a17be27cd5d82a8
ms.openlocfilehash: e57b98e7ddbcdaef11f73d220eda42231c6c4141


---

# <a name="server"></a>Server

Questo argomento descrive lo scopo e le funzioni del server RMS, per Azure e Windows Server.

**Azure RMS**: per informazioni sull'uso del servizio Azure Rights Management, vedere [Enable your service application to work with cloud based RMS](how-to-use-file-api-with-aadrm-cloud.md) (Consentire all'applicazione di servizio di usare RMS basato su cloud).

> [!IMPORTANT] 
> È consigliabile sviluppare e testare l'applicazione tramite Azure RMS.

**Windows Server**: per i server locali RMS, a partire da Windows Server 2008 è possibile installare e configurare il servizio RMS aggiungendolo come ruolo. Per installare il servizio nei sistemi operativi precedenti, scaricarlo dall'Area download Microsoft nella pagina relativa a[Microsoft Windows Rights Management Services con Service Pack 2](http://www.microsoft.com/download/en/details.aspx?id=4909).

Tra i numerosi servizi Web installati, quelli indicati di seguito sono importanti per lo sviluppo di applicazioni per il server RMS in esecuzione su Windows Server.

| Servizio | Descrizione |
|---------|-------------|
| Administration | Ospita il sito Web di amministrazione che consente di gestire RMS. Il servizio viene eseguito nei server di certificazione radice e nei server licenze. È possibile usare l'API di script di Active Directory Rights Management Services per scrivere script di amministrazione.|
| Certificazione account |Crea i certificati del computer che identificano i computer nella gerarchia di certificati RMS e i certificati per account con diritti che associano gli utenti a computer specifici. Per altre informazioni, vedere Attivazione di un computer e Attivazione di un utente.<p><p>Questo servizio viene eseguito nel server di certificazione radice. |
|Licenze | Rilascia una *licenza per l'utente finale*. Il servizio viene eseguito nei server di certificazione radice e nei server licenze.|
|Pubblicazione | Crea una *licenza di pubblicazione* che definisce i criteri che possono essere enumerati in una licenza per l'utente finale. Per altre informazioni, vedere l'articolo [Creating an Issuance License](https://msdn.microsoft.com/library/Aa362355) (Creazione di una licenza di pubblicazione).<p><p>Il servizio viene eseguito nei server di certificazione radice e nei server licenze.|
|Pre-certificazione | Consente a un server di richiedere un *certificato per account con diritti* per conto di un utente. Il servizio viene eseguito nei server di certificazione radice e nei server licenze.|
|Localizzatore servizi | Indica ad Active Directory l'URL dei servizi di licenza, pubblicazione e certificazione degli account, in modo che i client RMS possano rilevarli. Il servizio viene eseguito nei server di certificazione radice e nei server licenze.|

## <a name="related-topics"></a>Argomenti correlati ##
* [Panoramica](ad-rms-overview.md)
* [Microsoft Internet Information Services](http://www.iis.net/overview)
* [Consentire all'applicazione di servizio di usare RMS basato su cloud](how-to-use-file-api-with-aadrm-cloud.md)
* [Microsoft Windows Rights Management Services con Service Pack 2](http://www.microsoft.com/download/en/details.aspx?id=4909)
* [API di script di Active Directory Rights Management Services](https://msdn.microsoft.com/library/Bb968797)
* [Attivazione di un computer](https://msdn.microsoft.com/library/Cc530377)
* [Attivazione di un utente](https://msdn.microsoft.com/library/Cc530378)
* C[reazione di una licenza di pubblicazione](https://msdn.microsoft.com/library/Aa362355)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]


<!--HONumber=Jan17_HO1-->


