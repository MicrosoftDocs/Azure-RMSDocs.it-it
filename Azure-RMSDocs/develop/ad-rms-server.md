---
# required metadata

title: Server AD RMS | Azure RMS
description: Il componente server di Rights Management Services (RMS) è implementato da un set di servizi Web in esecuzione in Microsoft Internet Information Services.
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: a7f11e25-9d27-4083-b604-a2d437671d91

# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Server AD RMS

Questo argomento descrive lo scopo e le funzioni del server RMS.

Il componente server di Rights Management Services (RMS) è implementato da un set di servizi Web in esecuzione in [Microsoft Internet Information Services](http://www.iis.net/overview) (IIS). È anche possibile usare l'implementazione basata su cloud tramite RMS in Azure. Per altre informazioni sull'uso del servizio Azure Rights Management, vedere [Consentire all'applicazione di servizio di usare RMS basato su cloud](how-to-use-file-api-with-aadrm-cloud.md).

Per i server locali, a partire da Windows Server 2008 è possibile installare e configurare il servizio RMS aggiungendolo come ruolo. Per installare il servizio nei sistemi operativi precedenti, scaricarlo dall'Area download Microsoft nella pagina relativa a[Microsoft Windows Rights Management Services con Service Pack 2](http://www.microsoft.com/download/en/details.aspx?id=4909).

Tra i numerosi servizi Web installati, quelli indicati di seguito sono importanti per lo sviluppo di applicazioni.

**Amministrazione**: ospita il sito Web di amministrazione che consente di gestire RMS. Il servizio viene eseguito nei server di certificazione radice e nei server licenze. È possibile usare l'[API di script di Active Directory Rights Management Services](https://msdn.microsoft.com/library/Bb968797) per scrivere script di amministrazione.

**Certificazione account**: crea i certificati della macchina che identificano i computer nella gerarchia di certificati RMS e i certificati per account con diritti che associano gli utenti a computer specifici. Per altre informazioni, vedere [Attivazione di un utente](https://msdn.microsoft.com/library/Cc530378).

Questo servizio viene eseguito nel server di certificazione radice.

**Licenza**: rilascia una licenza per l'utente finale che consente agli utenti di utilizzare il contenuto protetto. Il servizio viene eseguito nei server di certificazione radice e nei server licenze.

**Pubblicazione**: crea una [licenza di pubblicazione](https://msdn.microsoft.com/library/Aa362355). Il servizio viene eseguito nei server di certificazione radice e nei server licenze.

**Pre-certificazione**: consente a un server di richiedere un certificato per account con diritti per conto di un utente. Un certificato per account con diritti usa il certificato della macchina dell'attivazione di RMS per associare gli account utente a computer o gruppi di computer specifici e viene usato per consentire agli utenti di usare il contenuto protetto. Il servizio viene eseguito nei server di certificazione radice e nei server licenze.

**Localizzatore del servizio**: fornisce ad Active Directory l'URL dei servizi di certificazione account, licenza e pubblicazione, in modo che i client RMS possano individuarli. Il servizio viene eseguito nei server di certificazione radice e nei server licenze.

 

## Argomenti correlati ##
* [Panoramica](ad-rms-overview.md)
* [Microsoft Internet Information Services](http://www.iis.net/overview)
* [Consentire all'applicazione di servizio di usare RMS basato su cloud](how-to-use-file-api-with-aadrm-cloud.md)
* [Microsoft Windows Rights Management Services con Service Pack 2](http://www.microsoft.com/download/en/details.aspx?id=4909)
* [API di script di Active Directory Rights Management Services](https://msdn.microsoft.com/library/Bb968797)
* [Attivazione di un computer](https://msdn.microsoft.com/library/Cc530377)
* [Attivazione di un utente](https://msdn.microsoft.com/library/Cc530378)
* [Creazione di una licenza di pubblicazione](https://msdn.microsoft.com/library/Aa362355)

 

 


<!--HONumber=Apr16_HO3-->


