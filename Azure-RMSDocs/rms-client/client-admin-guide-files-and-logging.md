---
title: Azure Information Protection i file client classici e la registrazione dell'utilizzo
description: Informazioni sui file client classici e la registrazione dell'utilizzo per il client classico Azure Information Protection per Windows.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 09/29/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 5a34ab85-773f-4782-ba09-c321cddf5bc0
ms.subservice: v1client
ms.reviewer: eymanor
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 3188392475a9da39f4187c30014ecc189248fd28
ms.sourcegitcommit: 8a141858e494dd1d3e48831e6cd5a5be48ac00d2
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2020
ms.locfileid: "97386118"
---
# <a name="admin-guide-azure-information-protection-classic-client-files-and-client-usage-logging"></a>Guida dell'amministratore: Azure Information Protection i file client classici e la registrazione dell'utilizzo del client

>***Si applica a**: Active Directory Rights Management Services, [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8, Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012 *
>
>***Pertinente per**: [Azure Information Protection client classico per Windows](../faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

> [!NOTE] 
> Per offrire un'esperienza utente unificata e semplificata, **Azure Information Protection** la gestione classica di client e **etichette** nel portale di Azure verrà **deprecata** a partire dal **31 marzo 2021**. In questo intervallo di tempo tutti i clienti correnti di Azure Information Protection possono passare alla soluzione di etichettatura unificata usando la piattaforma di etichettatura unificata di Microsoft Information Protection. Altre informazioni nell'[avviso ufficiale sulla deprecazione](https://aka.ms/aipclassicsunset).

Dopo aver installato il client di Azure Information Protection classico, potrebbe essere necessario individuare il percorso dei file e monitorare la modalità di utilizzo del client.

## <a name="file-locations-for-the-azure-information-protection-client"></a>Percorsi dei file per il client Azure Information Protection

File del client:    

- Per i sistemi operativi a 64 bit: **\Programmi (x86)\Microsoft Azure Information Protection**

- Per i sistemi operativi a 32 bit: **\Programmi\Microsoft Azure Information Protection**

File di log del client e file di criteri attualmente installati:

- Per i sistemi operativi a 64 e 32 bit: **%localappdata%\Microsoft\MSIP**

## <a name="usage-logging-for-the-azure-information-protection-classic-client"></a>Registrazione dell'utilizzo per il client di Azure Information Protection classico

Il client registra l'attività dell'utente nel registro eventi di Windows locale **registri applicazioni e servizi**  >  **Azure Information Protection**. Gli eventi includono le informazioni seguenti:

- Versione del client, ID criterio

- Indirizzi IP dell'utente connesso

- Nome file e percorso

- Azione:

    - Imposta etichetta: ID informazioni 101
    
    - Imposta etichetta (inferiore): ID informazioni 102
    
    - Imposta etichetta (superiore): ID informazioni 103
    
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
    
    - Manuale 
    
    - Consigliato
    
    - Automatico  
    
    - Sistema (per l'accesso e il download dei criteri)
    
    - Predefinito
    
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

