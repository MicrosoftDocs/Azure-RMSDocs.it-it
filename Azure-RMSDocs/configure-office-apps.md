---
title: Configurazione dei client per usare le app di Office con Azure RMS da AIP
description: Informazioni e istruzioni per gli amministratori per configurare le app di Office per l'uso con il servizio Azure Rights Management di Azure Information Protection.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 11/30/2019
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: ec269afe-4e87-4cc1-9144-5fbb594b412e
ms.subservice: azurerms
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: ea6b8afa02b9555924bcd1df5dfae1b7b37a217a
ms.sourcegitcommit: 8a141858e494dd1d3e48831e6cd5a5be48ac00d2
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2020
ms.locfileid: "97383534"
---
# <a name="office-apps-configuration-for-clients-to-use-the-azure-rights-management-service"></a>Applicazioni di Office: configurazione per i client da usare con il servizio Azure Rights Management

>***Si applica a**: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*
>
>***Pertinente per**: [AIP Unified Labeling client e client classico](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*


Usare queste informazioni per determinare i requisiti necessari per l'esecuzione delle app di Office con il servizio Azure Rights Management di Azure Information Protection.

## <a name="office-365-apps-office-2019-office-2016-and-office-2013"></a>App di Office 365, Office 2019, Office 2016 e Office 2013

Poiché queste versioni successive di Office forniscono supporto incorporato per il servizio Azure Rights Management, non è necessaria alcuna configurazione dei computer client per supportare le funzionalità IRM (Information Rights Management) per applicazioni quali Word, Excel, PowerPoint, Outlook e Outlook sul Web. 

Tutti gli utenti devono eseguire queste app in Windows per accedere alle applicazioni di Office con le credenziali Microsoft 365. Potranno quindi proteggere file e messaggi di posta elettronica e usare file e messaggi di posta elettronica protetti da altri utenti.

### <a name="user-instructions-for-office-for-mac"></a>Istruzioni per gli utenti di Office per Mac

Gli utenti che hanno Office per Mac devono prima verificare le proprie credenziali prima di poter proteggere il contenuto. ad esempio:

1. Aprire Outlook e creare un profilo usando il Microsoft 365 account aziendale o dell'Istituto di istruzione. 

2. Creare un nuovo messaggio e nella scheda **Opzioni** selezionare **autorizzazioni**, quindi selezionare **Verifica credenziali**. Quando richiesto, specificare di nuovo Microsoft 365 i dettagli dell'account aziendale o dell'Istituto di istruzione e selezionare **Accedi**.
    
    Questa azione Scarica i modelli di Rights Management di Azure e verifica che le **credenziali** vengano ora sostituite con le opzioni che **non includono restrizioni**, non **inoltri** e tutti i modelli di Rights Management di Azure pubblicati per il tenant. 

3. Ora è possibile annullare questo nuovo messaggio.

4. Per proteggere un messaggio di posta elettronica o un documento: nella scheda **Opzioni** selezionare **autorizzazioni** e scegliere un'opzione o un modello che protegga la posta elettronica o il documento.

## <a name="office-2010"></a>Office 2010

Per poter usare il servizio Azure Rights Management con Office 2010, nei computer client deve essere presente il client Azure Information Protection. Non è necessaria alcuna configurazione aggiuntiva, ad eccezione del fatto che gli utenti devono accedere con le credenziali Microsoft 365 e possono quindi proteggere i file e usare i file protetti da altri utenti.

Per altre informazioni, vedere [Client Azure Information Protection: installazione e configurazione per i client](configure-client.md).

