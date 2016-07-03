---
title: Configurazione di modelli personalizzati per Azure Rights Management | Azure RMS
description: 
keywords: 
author: cabailey
manager: mbaldwin
ms.date: 06/03/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 1775d8d0-9a59-42c8-914f-ce285b71ac1c
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 8e72b68c03ee7da58adaff96f3f4611a227214b0
ms.openlocfilehash: 26afa04c5041d0b8c952d3d6b3da5a2215acda87


---

# Configurazione di modelli personalizzati per Azure Rights Management

*Si applica a: Azure Rights Management, Office 365*

Dopo l'[attivazione di Azure Rights Management](activate-service.md) (Azure RMS), gli utenti sono automaticamente in grado di usare due modelli predefiniti che facilitano l'applicazione di criteri ai file riservati allo scopo di limitare l'accesso ai soli utenti autorizzati all'interno dell'organizzazione. Questi due modelli prevedono le seguenti restrizioni relativamente ai criteri per i diritti d'uso:

-   Visualizzazione di sola lettura per il contenuto protetto

    -   Nome visualizzato: **&lt;nome organizzazione&gt; - Solo visione riservata**

    -   Autorizzazione specifica: Visualizza contenuto

-   Autorizzazioni di lettura o modifica per il contenuto protetto

    -   Nome visualizzato: **&lt;nome organizzazione&gt; - Riservato**

    -   Autorizzazioni specifiche: Visualizza contenuto, Salva file, Modifica contenuto, Visualizza diritti assegnati, Consenti macro, Inoltra, Rispondi, Rispondi a tutti

Inoltre, l'[applicazione RMS sharing](../rms-client/sharing-app-windows.md) consente agli utenti di definire il proprio set di autorizzazioni. Per il client di Outlook e Outlook Web Access, gli utenti possono selezionare l'opzione [Non inoltrare](../deploy-use/configure-usage-rights.md#do-not-forward-option-for-emails).

Per molte organizzazioni, i modelli predefiniti potrebbero essere sufficienti. È tuttavia possibile creare modelli personalizzati di criteri per i diritti d'uso, se lo si desidera. È possibile decidere di creare un modello personalizzato per diversi motivi, tra cui i seguenti:

-   Si desidera disporre di un modello per concedere diritti a un sottoinsieme di utenti anziché a tutti gli utenti dell'organizzazione.

-   Si desidera che solo un subset di utenti sia in grado di visualizzare e selezionare un modello (modello di reparto) dalle applicazioni, anziché tutti gli utenti dell'organizzazione.

-   Si desidera definire un diritto personalizzato per un modello, ad esempio la visualizzazione e la modifica, ma non la copia e la stampa.

-   Si desidera configurare in un modello opzioni aggiuntive quali una data di scadenza e la possibilità di accedere al contenuto senza una connessione Internet.

Per consentire agli utenti di selezionare un modello personalizzato contenente impostazioni come queste, è necessario prima crearlo, configurarlo e quindi pubblicarlo. Anche se probabilmente si richiederanno solo alcuni modelli, è possibile configurare un massimo di 500 modelli personalizzati salvati in Azure. 

Per configurare e usare i modelli personalizzati, usare le informazioni seguenti:

-   [Come creare, configurare e pubblicare un modello personalizzato](create-template.md)

-   [Come copiare un modello](copy-template.md)

-   [Come rimuovere (archiviare) modelli](remove-template.md)

-   [Come aggiornare i modelli per gli utenti](refresh-templates.md)

-   [Usare PowerShell per gestire i modelli](configure-templates-with-powershell.md)





<!--HONumber=Jun16_HO4-->


