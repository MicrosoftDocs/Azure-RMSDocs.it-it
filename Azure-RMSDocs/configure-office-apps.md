---
title: Configurazione dei client per usare le app di Office con Azure RMS da AIP
description: Informazioni e istruzioni per gli amministratori per configurare le app di Office per l'uso con il servizio Azure Rights Management di Azure Information Protection.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 08/31/2018
ms.topic: conceptual
ms.service: information-protection
ms.assetid: ec269afe-4e87-4cc1-9144-5fbb594b412e
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 4b93d1f860ec3e894571da70a0b09aa4b37d59a1
ms.sourcegitcommit: 5b4eb0e17fb831d338d8c25844e9e6f4ca72246d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/10/2018
ms.locfileid: "53174285"
---
# <a name="office-apps-configuration-for-clients-to-use-the-azure-rights-management-service"></a>Applicazioni di Office: configurazione per i client per l'uso del servizio Azure Rights Management

>*Si applica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*


Usare queste informazioni per determinare i requisiti necessari per l'esecuzione delle app di Office con il servizio Azure Rights Management di Azure Information Protection.

## <a name="office2016-and-office-2013"></a>Office 2016 e Office 2013
Dal momento che queste ultime versioni di Office supportano in modo nativo il servizio Azure Rights Management, non è necessario eseguire alcuna attività di configurazione dei computer client per supportare le funzionalità IRM (Information Rights Management) per applicazioni quali Word, Excel, PowerPoint, Outlook e Outlook sul Web. Gli utenti dovranno solo eseguire l'accesso alle applicazioni Office con le proprie credenziali Rights Management. Potranno quindi proteggere file e messaggi di posta elettronica e usare file e messaggi di posta elettronica protetti da altri utenti.

È tuttavia consigliabile usare tali applicazioni insieme al client Azure Information Protection, in modo che gli utenti possano sfruttare i vantaggi offerti dal componente aggiuntivo per Office e il supporto per altri tipi di file. Per altre informazioni, vedere [Client Azure Information Protection: installazione e configurazione dei client](configure-client.md).

## <a name="office2010"></a>Office 2010
Per poter usare il servizio Azure Rights Management con Office 2010, nei computer client deve essere presente il client Azure Information Protection o l'applicazione di condivisione Microsoft Rights Management per Windows. Non sono necessarie configurazioni aggiuntive, in quanto gli utenti devono solo eseguire l'accesso con le credenziali di Rights Management per poter proteggere i file e usare i file protetti da altri.

Per altre informazioni sul client Azure Information Protection, vedere [Client Azure Information Protection: installazione e configurazione dei client](configure-client.md).

