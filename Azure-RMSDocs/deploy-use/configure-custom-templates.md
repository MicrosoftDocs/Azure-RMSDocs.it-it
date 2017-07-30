---
title: Configurare modelli personalizzati per Azure RMS - AIP
description: Informazioni e istruzioni per gli amministratori per configurare e gestire i modelli dei diritti di utilizzo. I modelli semplificano, per utenti e amministratori, l'applicazione ai file riservati di criteri che limitano l'accesso agli utenti autorizzati.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 07/21/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 1775d8d0-9a59-42c8-914f-ce285b71ac1c
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 6c3f066a373d253d8488c805828a65513370e3a4
ms.sourcegitcommit: 7bec3dfe3ce61793a33d53691046c5b2bdba3fb9
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/27/2017
---
# <a name="configuring-custom-templates-for-the-azure-rights-management-service"></a>Configurazione di modelli personalizzati per il servizio Azure Rights Management

>*Si applica a: Azure Information Protection, Office 365*

Dopo che il servizio Azure Rights Management è [attivato](activate-service.md) gli utenti possono usare automaticamente due modelli predefiniti. I modelli semplificano l'applicazione ai file riservati di criteri di gestione dei diritti, che limitano l'accesso agli utenti autorizzati dell'organizzazione. I due modelli includono le seguenti restrizioni dei criteri per i diritti:

-   Visualizzazione di sola lettura per il contenuto protetto

    -   Nome visualizzato: **&lt;nome organizzazione&gt;, solo visione riservata** o **Riservatezza elevata\Tutti i dipendenti**

    -   Autorizzazione specifica: Visualizza contenuto

-   Autorizzazioni di lettura o modifica per il contenuto protetto

    -   Nome visualizzato: **&lt;nome organizzazione&gt;, riservato** o **Riservato\Tutti i dipendenti**

    -   Autorizzazioni specifiche: Visualizza contenuto, Salva file, Modifica contenuto, Visualizza diritti assegnati, Consenti macro, Inoltra, Rispondi, Rispondi a tutti

Il [client Azure Information Protection](../rms-client/aip-client.md) consente inoltre agli utenti di definire set di autorizzazioni personalizzati. Per il client di Outlook e Outlook Web Access, gli utenti possono selezionare l'opzione [Non inoltrare](../deploy-use/configure-usage-rights.md#do-not-forward-option-for-emails).

Per molte organizzazioni, i modelli predefiniti potrebbero essere sufficienti. È tuttavia possibile creare modelli personalizzati di criteri per i diritti d'uso, se lo si desidera. È possibile decidere di creare un modello personalizzato per diversi motivi, tra cui i seguenti:

-   Si desidera disporre di un modello per concedere diritti a un sottoinsieme di utenti anziché a tutti gli utenti dell'organizzazione.

-   Si desidera che solo un subset di utenti sia in grado di visualizzare e selezionare un modello (modello di reparto) dalle applicazioni, anziché tutti gli utenti dell'organizzazione.

-   Si desidera definire un diritto personalizzato per un modello, ad esempio la visualizzazione e la modifica, ma non la copia e la stampa.

-   Si desidera configurare in un modello opzioni aggiuntive quali una data di scadenza e la possibilità di accedere al contenuto senza una connessione Internet.

Per consentire agli utenti di selezionare un modello personalizzato contenente impostazioni come queste, è necessario prima crearlo, configurarlo e quindi pubblicarlo. Anche se è probabile che siano necessari solo alcuni modelli, è possibile configurare fino a 500 modelli personalizzati salvati in Azure. 

Per configurare e usare i modelli personalizzati, usare le informazioni seguenti:

-   [Come creare, configurare e pubblicare un modello personalizzato](create-template.md)

-   [Come copiare un modello](copy-template.md)

-   [Come rimuovere (archiviare) modelli](remove-template.md)

-   [Come aggiornare i modelli per gli utenti](refresh-templates.md)

-   [Usare PowerShell per gestire i modelli](configure-templates-with-powershell.md)

> [!TIP]
> È in corso lo spostamento di modelli e nuove opzioni per la configurazione della protezione di Azure Rights Management nel portale di Azure. Questa funzionalità è attualmente disponibile nell'anteprima. Per altre informazioni, vedere l'annuncio del post di blog [Azure Information Protection unified administration now in Preview](https://blogs.technet.microsoft.com/enterprisemobility/2017/04/26/azure-information-protection-unified-administration-now-in-preview/) (Amministrazione unificata di Azure Information Protection nella versione di anteprima). 


[!INCLUDE[Commenting house rules](../includes/houserules.md)]

