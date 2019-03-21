---
title: File e registrazione dell'utilizzo del client Azure Information Protection
description: Informazioni sui file e sulla registrazione dell'utilizzo per il client Azure Information Protection per Windows.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 03/11/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 5a34ab85-773f-4782-ba09-c321cddf5bc0
ms.reviewer: eymanor
ms.suite: ems
ms.openlocfilehash: 72e29d19ddbfc3189d498724fc8353829820ab4e
ms.sourcegitcommit: f4fe64474999954e0c013c3901edbb3048670935
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/10/2019
ms.locfileid: "57725750"
---
# <a name="admin-guide-azure-information-protection-client-files-and-client-usage-logging"></a>Guida dell'amministratore: File e registrazione dell'utilizzo del client Azure Information Protection

>*Si applica a: Active Directory Rights Management Services, [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8, Windows 7 con SP1, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2*

Dopo aver installato il client Azure Information Protection, potrebbe essere necessario individuare il percorso dei file e monitorare l'utilizzo del client.

## <a name="file-locations-for-the-azure-information-protection-client"></a>Percorsi dei file per il client Azure Information Protection

File del client:   

- Per i sistemi operativi a 64 bit: **\Programmi (x86)\Microsoft Azure Information Protection**

- Per i sistemi operativi a 32 bit: **\Programmi\Microsoft Azure Information Protection**

File di log del client e file di criteri attualmente installati:

- Per i sistemi operativi a 64 e 32 bit: **%localappdata%\Microsoft\MSIP**

## <a name="usage-logging-for-the-azure-information-protection-client"></a>Registrazione dell'utilizzo per il client Azure Information Protection

Il client registra l'attività dell'utente nel registro eventi locale di Windows **Applicazioni e servizi** > **Azure Information Protection**. Gli eventi includono le informazioni seguenti:

- Versione del client, ID criterio

- Indirizzi IP dell'utente connesso

- Nome file e percorso

- Action:

    - Impostare l'etichetta: ID informazioni 101
    
    - Impostare l'etichetta (inferiore): ID informazioni 101
    
    - Impostare l'etichetta (superiore): ID informazioni 101
    
    - Rimuovere l'etichetta: ID informazioni 104
    
    - Descrizione comando dell'etichetta consigliata: Informazioni 105
    
    - Applicare la protezione personalizzata: ID informazioni 201
    
    - Rimuovere la protezione personalizzata: ID informazioni 202
    
    - Messaggio di avviso di Outlook: ID informazioni 301
    
    - Messaggio di giustificazione di Outlook: ID informazioni 302
    
    - Messaggio di blocco di Outlook: ID informazioni 303
    
    - Accesso (operativo): ID informazioni 902
    
    - Scaricare i criteri (operativo): ID informazioni 901
    
- Origine azione:
    
    - Manuale 
    
    - Consigliato
    
    - Automatico  
    
    - Sistema (per l'accesso e il download dei criteri)
    
    - Predefinito
    
- Etichetta prima e dopo l'azione 
    
- Protezione prima e dopo l'azione
    
- Giustificazione utente (se applicabile)

- Autorizzazioni personalizzate (se applicabile) che includono i [diritti di utilizzo in base al nome di codifica](../configure-usage-rights.md#usage-rights-and-descriptions) per gli utenti, i gruppi o le organizzazioni specificati

Gli eventi per i messaggi di avviso, di giustificazione e di blocco di Outlook richiedono le impostazioni client di anteprima e avanzate. Per altre informazioni, vedere [Implementare messaggi popup in Outlook che avvisano, giustificano o bloccano l'invio di messaggi di posta elettronica](client-admin-guide-customizations.md#implement-pop-up-messages-in-outlook-that-warn-justify-or-block-emails-being-sent).

Per informazioni sulla registrazione dell'utilizzo per il servizio di protezione, vedere [Registrazione e analisi dell'utilizzo del servizio Azure Rights Management](../log-analyze-usage.md).

## <a name="next-steps"></a>Passaggi successivi
Dopo aver identificato tutti i file di log associati al client Azure Information Protection, vedere gli argomenti seguenti per altre informazioni che potrebbero essere necessarie per supportare il client:

- [Personalizzazioni](client-admin-guide-customizations.md)

- [Rilevamento dei documenti](client-admin-guide-document-tracking.md)

- [Tipi di file supportati](client-admin-guide-file-types.md)

- [Comandi di PowerShell](client-admin-guide-powershell.md)

