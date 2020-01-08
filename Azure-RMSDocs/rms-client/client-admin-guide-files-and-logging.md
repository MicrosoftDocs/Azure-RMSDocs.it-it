---
title: File e registrazione dell'utilizzo del client Azure Information Protection
description: Informazioni sui file e sulla registrazione dell'utilizzo per il client Azure Information Protection per Windows.
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 1/06/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 5a34ab85-773f-4782-ba09-c321cddf5bc0
ms.subservice: v1client
ms.reviewer: eymanor
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 56214db01a603cde5a09de99d49868bc353c4ce6
ms.sourcegitcommit: d0012de76c9156dd9239f7ba09c044a4b42ffc71
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/06/2020
ms.locfileid: "75675721"
---
# <a name="admin-guide-azure-information-protection-client-files-and-client-usage-logging"></a>Guida dell'amministratore: File e registrazione dell'utilizzo del client Azure Information Protection

>*Si applica a: Active Directory Rights Management Services, [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8, Windows 7 con SP1, windows server 2019, windows server 2016, windows Server 2012 R2, windows Server 2012, windows Server 2008 R2*
>
> *Istruzioni per: [client di Azure Information Protection per Windows](../faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*

> [!NOTE] 
> Per offrire un'esperienza utente unificata e semplificata, **Azure Information Protection client (versione classica)** e la **gestione delle etichette** nel portale di Azure verranno **deprecati** a partire dal **31 marzo 2021**. Questo intervallo di tempo consente a tutti i clienti correnti Azure Information Protection di passare alla soluzione di assegnazione di etichette unificata usando la piattaforma Microsoft Information Protection Unified labeling. Ulteriori informazioni sono disponibili nell' [avviso ufficiale di deprecazione](https://aka.ms/aipclassicsunset).

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

    - Imposta etichetta: ID informazioni 101
    
    - Imposta etichetta (inferiore): ID informazioni 101
    
    - Imposta etichetta (superiore): ID informazioni 101
    
    - Rimuovere l'etichetta: ID informazioni 104
    
    - Descrizione comando etichetta consigliata: informazioni 105
    
    - Applicare la protezione personalizzata: ID informazioni 201
    
    - Rimuovere la protezione personalizzata: ID informazioni 202
    
    - Messaggio di avviso di Outlook: ID informazioni 301
    
    - Messaggio giustificativo di Outlook: ID informazioni 302
    
    - Messaggio di blocco di Outlook: ID informazioni 303
    
    - Accesso (operativo): ID informazioni 902
    
    - Download dei criteri (operativo): ID informazioni 901
    
- Origine azione:
    
    - Manual 
    
    - Implementazione consigliata
    
    - Automatica  
    
    - Sistema (per l'accesso e il download dei criteri)
    
    - Valore predefinito
    
- Etichetta prima e dopo l'azione 
    
- Protezione prima e dopo l'azione
    
- Giustificazione utente (se applicabile)

- Autorizzazioni personalizzate (se applicabile) che includono i [diritti di utilizzo in base al nome di codifica](../configure-usage-rights.md#usage-rights-and-descriptions) per gli utenti, i gruppi o le organizzazioni specificati

Gli eventi per i messaggi di avviso, giustificazione e blocco di Outlook richiedono impostazioni client avanzate. Per altre informazioni, vedere [Implementare messaggi popup in Outlook che avvisano, giustificano o bloccano l'invio di messaggi di posta elettronica](client-admin-guide-customizations.md#implement-pop-up-messages-in-outlook-that-warn-justify-or-block-emails-being-sent).


## <a name="next-steps"></a>Passaggi successivi
Dopo aver identificato tutti i file di log associati al client Azure Information Protection, vedere gli argomenti seguenti per altre informazioni che potrebbero essere necessarie per supportare il client:

- [Personalizzazioni](client-admin-guide-customizations.md)

- [Rilevamento dei documenti](client-admin-guide-document-tracking.md)

- [Tipi di file supportati](client-admin-guide-file-types.md)

- [Comandi di PowerShell](client-admin-guide-powershell.md)

