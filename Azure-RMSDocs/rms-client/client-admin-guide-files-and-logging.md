---
title: File e registrazione dell&quot;utilizzo del client Azure Information Protection
description: Informazioni sui file e sulla registrazione dell&quot;utilizzo per il client Azure Information Protection per Windows.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/08/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 5a34ab85-773f-4782-ba09-c321cddf5bc0
ms.reviewer: eymanor
ms.suite: ems
ms.openlocfilehash: 78c355acd1bc87347ef2d4b02ffbb24f2c08bc70
ms.sourcegitcommit: 31e128cc1b917bf767987f0b2144b7f3b6288f2e
translationtype: HT
---
# <a name="azure-information-protection-client-files-and-client-usage-logging"></a>File e registrazione dell'utilizzo del client Azure Information Protection

>*Si applica a: Active Directory Rights Management Services, Azure Information Protection, Windows 10, Windows 8.1, Windows 8, Windows 7 con SP1*

Dopo aver installato il client Azure Information Protection, potrebbe essere necessario individuare il percorso dei file e monitorare l'utilizzo del client.

## <a name="file-locations-for-the-azure-information-protection-client"></a>Percorsi dei file per il client Azure Information Protection

File del client:    

- Per i sistemi operativi a 64 bit: **\Programmi (x86)\Microsoft Azure Information Protection**

- Per i sistemi operativi a 32 bit: **\Programmi\Microsoft Azure Information Protection**

File di log del client e file di criteri attualmente installati:

- Per i sistemi operativi a 64 e 32 bit: **%localappdata%\Microsoft\MSIP**

## <a name="usage-logging-for-the-azure-information-protection-client"></a>Registrazione dell'utilizzo per il client Azure Information Protection

Il client registra l'attività dell'utente nel registro eventi locale **Applicazioni e servizi** di Windows, **Azure Information Protection**. Gli eventi includono le informazioni seguenti:

- Data, versione del client, ID criterio

- Nome utente connesso, nome computer

- Nome file e percorso

- Action:

    - Impostare l'etichetta: ID informazioni 101
    
    - Impostare l'etichetta (inferiore): ID informazioni 102
    
    - Impostare l'etichetta (superiore): ID informazioni 103
    
    - Rimuovere l'etichetta: ID informazioni 104
   
    - Suggerimento consigliato: ID informazioni 105
    
    - Applicare la protezione personalizzata: ID informazioni 201
    
    - Rimuovere la protezione personalizzata: ID informazioni 202
    
    - Accesso (operativo): ID informazioni 902
    
    - Download dei criteri (operativo): ID informazioni 901
    
- Origine azione:
    
    - Manuale 
    
    - Consigliato
    
    - Automatico  
    
    - Sistema (per l'accesso e il download dei criteri)
    
- Etichetta prima e dopo l'azione 
    
- Protezione prima e dopo l'azione
    
- Giustificazione utente (se applicabile)
    

Per informazioni sulla registrazione dell'utilizzo per il servizio Azure Rights Management, vedere [Registrazione e analisi dell'utilizzo del servizio Azure Rights Management](../deploy-use/log-analyze-usage.md)



## <a name="next-steps"></a>Passaggi successivi
Dopo aver identificato tutti i file di log associati al client Azure Information Protection, vedere gli argomenti seguenti per altre informazioni che potrebbero essere necessarie per supportare il client:


- [Rilevamento dei documenti](client-admin-guide-document-tracking.md)

- [Tipi di file supportati](client-admin-guide-file-types.md)

- [Comandi di PowerShell](client-admin-guide-powershell.md)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
