---
# required metadata

title: Usare l'accesso condizionale in Exchange Online e in locale con Microsoft Intune e Configuration Manager
description:
keywords:
author: craigcaseyMSFT
manager: swadhwa
ms.date: 04/28/2016
ms.topic: article
ms.prod:
ms.service:
ms.technology:
ms.assetid: 5ccd033f-bc31-4fae-b6bf-9e1c2722627f

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: 
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Distribuire Exchange Online locale con Microsoft Intune e Configuration Manager
Ora che si sono lette con attenzione le [indicazioni sull'architettura per la protezione di documenti e messaggi di posta elettronica aziendali](architecture-guidance-for-protecting-company-email-and-documents.md) è possibile procedere alla distribuzione di una soluzione.

Un ambiente in cui viene usato sia Exchange locale che Exchange Online per gestire i profili di posta elettronica offre alle aziende la possibilità di estendere l'esperienza ricca di funzionalità e il controllo amministrativo che hanno con la propria organizzazione di Microsoft Exchange locale nel cloud. Questo tipo "ibrido" di distribuzione fornisce l'aspetto semplice di una singola organizzazione di Exchange tra un'organizzazione di Exchange Server 2013 locale ed Exchange Online in Microsoft Office 365. Inoltre, questo tipo di distribuzione può essere usato come un passaggio intermedio per lo spostamento completo in un'organizzazione di Exchange Online.

Se si usa già Configuration Manager assieme a Exchange locale ed Exchange Online, è possibile incorporare Intune in modo da gestire l'accesso alla posta elettronica e proteggere i dati di posta elettronica nei dispositivi mobili. È possibile implementare questa soluzione seguendo le istruzioni riportate in precedenza per l'implementazione separata di ciascuna soluzione.

## Prerequisiti
Per configurare un tipo di coesistenza di ambiente che implementi Exchange locale ed Exchange Online, l'organizzazione di Exchange esistente deve soddisfare determinati requisiti. Se si non soddisfano questi requisiti, non sarà possibile completare i passaggi necessari per configurare una distribuzione ibrida tra l'organizzazione di Exchange locale e l'organizzazione di Exchange Online in Microsoft Office 365.

Per esaminare i requisiti per la creazione e la configurazione di questo tipo di ambiente, vedere [Prerequisiti per la distribuzione ibrida](https://technet.microsoft.com/en-us/library/hh534377.aspx) .

## Passaggi per la distribuzione
Per distribuire una soluzione di coesistenza, seguire i passaggi precedenti, che consentono la distribuzione sia della soluzione [Exchange Server locale](conditional-access-intune-configmgr-exchange.md) che della soluzione [Exchange Online](conditional-access-intune-configmgr-exchange-online.md).

## Come proseguire
Dopo aver distribuito una soluzione per la protezione della posta elettronica aziendale e dei dati di questa all'interno dei dispositivi mobili, è possibile scoprire di più sull'[esperienza dell'utente finale relativa all'accesso condizionale](end-user-experience-conditional-access.md). Ciò consente di prepararsi ad affrontare i problemi che potrebbero verificarsi quando gli utenti finali registrano dispositivi specifici.


<!--HONumber=Apr16_HO4-->


