---
title: Configurazione dei client per usare le app di Office con Azure RMS da AIP
description: Informazioni e istruzioni per gli amministratori per configurare le app di Office per l'uso con il servizio Azure Rights Management di Azure Information Protection.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 06/24/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: ec269afe-4e87-4cc1-9144-5fbb594b412e
ms.suite: ems
ms.openlocfilehash: 09f7eaaaafb6c1ecbce584876a7e8bf254e0c0d5
ms.sourcegitcommit: 2af2297319265c1f91aa76eb227c6f4d316df42a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/25/2019
ms.locfileid: "67348815"
---
# <a name="office-apps-configuration-for-clients-to-use-the-azure-rights-management-service"></a>Applicazioni di Office: configurazione per i client per l'uso del servizio Azure Rights Management

>*Si applica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*


Usare queste informazioni per determinare i requisiti necessari per l'esecuzione delle app di Office con il servizio Azure Rights Management di Azure Information Protection.

## <a name="office365-apps-office-2019-office-2016-and-office-2013"></a>App di Office 365, Office 2019, Office 2016 e Office 2013
Dal momento che queste ultime versioni di Office supportano in modo nativo il servizio Azure Rights Management, non è necessario eseguire alcuna attività di configurazione dei computer client per supportare le funzionalità IRM (Information Rights Management) per applicazioni quali Word, Excel, PowerPoint, Outlook e Outlook sul Web. Tutti gli utenti devono eseguire per queste App in Windows, accesso alle applicazioni di Office con le proprie credenziali di Office 365. Potranno quindi proteggere file e messaggi di posta elettronica e usare file e messaggi di posta elettronica protetti da altri utenti.

### <a name="user-instructions-for-office-for-mac"></a>Le istruzioni per Office per Mac

Gli utenti che dispongono di Office per Mac prima di tutto necessario verificare le proprie credenziali prima che essi possono proteggere il contenuto. Ad esempio:

1. Aprire Outlook e creare un profilo mediante l'account aziendale o dell'istituto di istruzione di Office 365. 

2. Creare un nuovo messaggio e, nella **le opzioni** scheda, seleziona **autorizzazioni**e quindi selezionare **verifica credenziali**. Quando richiesto, specificare nuovamente il proprio account aziendale o dell'istituto di istruzione di Office 365 e selezionare **Accedi**.
    
    Questa azione Scarica i modelli di Azure Rights Management e **verifica credenziali** è stato sostituito da opzioni che includono **nessuna restrizione**, **non inoltrare**, e eventuali modelli di Azure Rights Management pubblicati per il tenant. 

3. È ora possibile annullare questo nuovo messaggio.

4. Per proteggere un messaggio di posta elettronica o un documento: Nel **le opzioni** scheda, seleziona **autorizzazioni** e scegliere un'opzione o un modello che protegga il messaggio di posta elettronica o documento.

## <a name="office2010"></a>Office 2010
Per i computer client usare il servizio Azure Rights Management con Office 2010, devono avere il client Azure Information Protection (versione classica). Non sono necessarie altre configurazioni. Per proteggere i file e usare quelli protetti da altri utenti è sufficiente accedere con le credenziali di Office 365.

Per altre informazioni sul client Azure Information Protection (versione classica), vedere [client Azure Information Protection: installazione e configurazione dei client](configure-client.md).

