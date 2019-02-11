---
title: Configurazione dei client per usare le app di Office con Azure RMS da AIP
description: Informazioni e istruzioni per gli amministratori per configurare le app di Office per l'uso con il servizio Azure Rights Management di Azure Information Protection.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/01/2019
ms.topic: conceptual
ms.service: information-protection
ms.assetid: ec269afe-4e87-4cc1-9144-5fbb594b412e
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 7896e1c8a342ce8a430d9133950a2fe47a7de602
ms.sourcegitcommit: 8558af7116f62414054feffa346aba197a1250d9
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/01/2019
ms.locfileid: "55559768"
---
# <a name="office-apps-configuration-for-clients-to-use-the-azure-rights-management-service"></a>Applicazioni di Office: configurazione per i client per l'uso del servizio Azure Rights Management

>*Si applica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*


Usare queste informazioni per determinare i requisiti necessari per l'esecuzione delle app di Office con il servizio Azure Rights Management di Azure Information Protection.

## <a name="office2016-and-office-2013"></a>Office 2016 e Office 2013
Dal momento che queste ultime versioni di Office supportano in modo nativo il servizio Azure Rights Management, non è necessario eseguire alcuna attività di configurazione dei computer client per supportare le funzionalità IRM (Information Rights Management) per applicazioni quali Word, Excel, PowerPoint, Outlook e Outlook sul Web. Gli utenti dovranno solo eseguire l'accesso alle applicazioni di Office con le credenziali di Office 365. Potranno quindi proteggere file e messaggi di posta elettronica e usare file e messaggi di posta elettronica protetti da altri utenti.

È tuttavia consigliabile usare tali applicazioni insieme al client Azure Information Protection, in modo che gli utenti possano sfruttare i vantaggi offerti dal componente aggiuntivo per Office e il supporto per altri tipi di file. Per altre informazioni, vedere [Client Azure Information Protection: installazione e configurazione dei client](configure-client.md).

## <a name="office2010"></a>Office 2010
Per poter usare il servizio Azure Rights Management con Office 2010, nei computer client deve essere presente il client Azure Information Protection. Non sono necessarie altre configurazioni. Per proteggere i file e usare quelli protetti da altri utenti è sufficiente accedere con le credenziali di Office 365.

Per altre informazioni sul client Azure Information Protection, vedere [Client Azure Information Protection: installazione e configurazione dei client](configure-client.md).

