---
title: Domande frequenti sulla classificazione e l'assegnazione di etichette - AIP
description: "Di seguito sono riportate alcune possibili domande sulle funzionalità di classificazione e assegnazione di etichette di Azure Information Protection e le relative risposte."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 08/31/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 4b595b6a-7eb0-4438-b49a-686431f95ddd
ms.reviewer: adhall
ms.suite: ems
ms.openlocfilehash: 2ac8211b338b9d35bb7962455a117d02f9c1fa32
ms.sourcegitcommit: 4b7f025e9f78d25c6f3079cceb42bc33f3f3a612
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/01/2017
---
# <a name="frequently-asked-questions-about-classification-and-labeling-in-azure-information-protection"></a>Domande frequenti sulla classificazione e l'assegnazione di etichette in Azure Information Protection

>*Si applica a: Azure Information Protection, Office 365*

Di seguito sono riportate alcune possibili domande sulle funzionalità di classificazione e assegnazione di etichette di Azure Information Protection  e le relative risposte. 

## <a name="what-can-i-do-with-the-classification-capabilities-in-azure-information-protection"></a>Che cosa si può fare con le funzionalità di classificazione di Azure Information Protection?

L'esercitazione introduttiva consente in pochi minuti di vedere queste caratteristiche in pratica: [Esercitazione introduttiva di Azure Information Protection](infoprotect-quick-start-tutorial.md).

Per sapere quando saranno disponibili altre funzionalità e nuove caratteristiche per la classificazione, seguire gli annunci nel [blog di Enterprise Mobility + Security](https://blogs.technet.microsoft.com/enterprisemobility/?product=azure-information-protection) e nel [sito Yammer](https://www.yammer.com/askipteam/#/threads/inGroup?type=in_group&feedId=8652489&view=all). Nella versione corrente sono presenti alcune limitazioni, incluse le seguenti:

- I nomi e le descrizioni delle etichette sono supportati solo in una lingua. Il supporto multilingue è tuttavia ora in anteprima. Per altre informazioni, vedere [Come configurare etichette e modelli per varie lingue in Azure Information Protection](../deploy-use/configure-policy-languages.md).

- Manca la funzione di registrazione centralizzata per la classificazione e l'aggiunta di etichette.

- Non sono disponibili funzionalità di assegnazione di etichette nelle app di Office per dispositivi mobili (iOS e Android) e computer Mac o per Office Web Apps (Office Online).

- Le funzionalità di classificazione e assegnazione di etichette non sono integrate con Exchange Online o SharePoint Online.

Per richiedere nuove funzionalità e votare per le richieste, visitare il [sito User Voice](https://msip.uservoice.com/) per Azure Information Protection.

## <a name="do-i-need-to-be-a-global-admin-to-configure-classification-and-labels"></a>È necessario essere un amministratore globale per configurare la classificazione e le etichette?

Per configurare i criteri di Azure Information Protection, non è più necessario accedere al portale di Azure come amministratore globale di Azure Active Directory. Ora è anche possibile usare un account con un ruolo di amministratore della sicurezza.

Se al momento dell'installazione del [client Azure Information Protection](https://www.microsoft.com/en-us/download/details.aspx?id=53018) si sceglie di installare i criteri demo, per provare a usare la funzionalità per l'assegnazione di etichette non è necessario accedere al portale. I criteri demo installano localmente i criteri predefiniti di Azure Information Protection. È quindi possibile provare ad aggiungere etichette a documenti e a messaggi di posta elettronica, ma per modificare etichette o aggiungerne nuove sarà necessario accedere al portale di Azure. 

## <a name="which-options-in-the-azure-portal-are-p2"></a>Quali opzioni nel portale di Azure sono P2?

Le opzioni nel portale di Azure che richiedono una sottoscrizione ad **Azure Information Protection Premium 2** (P2) hanno ora un messaggio popup di informazioni che le identificano. Per altre informazioni sulle funzionalità incluse in P1 e sulle sottoscrizioni a P1, vedere l'[elenco delle funzionalità](https://www.microsoft.com/cloud-platform/azure-information-protection-features) nel sito di Azure Information Protection.

## <a name="can-a-file-have-more-than-one-classification"></a>Un file può avere più di una classificazione?

Poiché gli utenti possono selezionare una sola etichetta alla volta per ogni documento o messaggio di posta elettronica, la classificazione è spesso una sola. Tuttavia, se gli utenti selezionano un'etichetta secondaria, vengono effettivamente applicate due etichette contemporaneamente, ovvero un'etichetta primaria e un'etichetta secondaria. Se si usano etichette secondarie, il file può avere due classificazioni che indicano una relazione padre/figlio per un ulteriore livello di controllo.

Ad esempio, l'etichetta **Confidential** (Riservato) potrebbe contenere le etichette secondarie **Legal** (Legale) e **Finance** (Contabilità). È possibile applicare contrassegni visivi di classificazione e modelli di Rights Management diversi alle etichette secondarie. L'utente non potrà selezionare direttamente l'etichetta **Confidential** (Riservato), ma solo una delle relative etichette secondarie, ad esempio **Legal** (Legale). Di conseguenza, l'etichetta impostata visualizzata dall'utente sarà **Confidential \ Legal** (Riservato \ Legale). I metadati di tale file includono una sola proprietà di testo personalizzato per **Confidential** (Riservato), una proprietà di testo personalizzato per **Legal** (Legale) e un'altra proprietà che contiene entrambi i valori, **Confidential Legal** (Riservato Legale). 

Quando si usano etichette secondarie, non configurare contrassegni visivi, protezione e condizioni nell'etichetta principale. Quando si usano etichette secondarie, configurare queste impostazioni solo nell'etichetta secondaria. Se si configurano le impostazioni nell'etichetta principale e nella relativa etichetta secondaria, le impostazioni dell'etichetta secondaria hanno priorità.

## <a name="when-an-email-is-labeled-do-any-attachments-automatically-get-the-same-labeling"></a>Quando a un messaggio di posta elettronica viene applicata un'etichetta, eventuali allegati ottengono automaticamente la stessa etichetta?

No. Quando viene applicata un'etichetta a un messaggio di posta elettronica con allegati, tali allegati non ereditano la stessa etichetta. Gli allegati rimangono senza etichetta oppure mantengono un'etichetta applicata separatamente. Tuttavia, se l'etichetta per il messaggio di posta elettronica applica una protezione, tale protezione viene applicata agli allegati.

## <a name="how-can-dlp-solutions-and-other-applications-integrate-with-azure-information-protection"></a>Come è possibile integrare soluzioni DLP e altre applicazioni con Azure Information Protection?

Per la classificazione, Azure Information Protection usa metadati persistenti che includono un'etichetta di testo non crittografata. Queste informazioni possono essere lette da soluzioni DLP e da altre applicazioni. Nei file questi metadati vengono archiviati in proprietà personalizzate. Nei messaggi di posta elettronica queste informazioni si trovano nelle intestazioni del messaggio.

## <a name="how-is-azure-information-protection-classification-for-emails-different-from-exchange-message-classification"></a>Qual è la differenza tra la classificazione dei messaggi di posta elettronica di Azure Information Protection e la classificazione dei messaggi di Exchange?

La classificazione dei messaggi di Exchange è una funzionalità precedente che consente di classificare i messaggi di posta elettronica e viene implementata indipendentemente dalla classificazione di Azure Information Protection. 

È tuttavia possibile integrare le due soluzioni in modo che quando gli utenti classificano un messaggio di posta elettronica con Outlook sul web e con alcune applicazioni di posta elettronica per dispositivi mobili, vengono automaticamente aggiunti la classificazione di Azure Information Protection e i contrassegni di etichetta corrispondenti. 

È possibile applicare la stessa tecnica per usare le etichette con Outlook sul web e le applicazioni di posta elettronica per dispositivi mobili.

Per i passaggi di configurazione, vedere [Integrate Exchange message classification with Azure Information Protection for a mobile device labeling solution](../rms-client/client-admin-guide-customizations.md#integration-with-exchange-message-classification-for-a-mobile-device-labeling-solution) (Integrare la classificazione messaggi di Exchange ad Azure Information Protection per una soluzione di etichettatura per dispositivi mobili). 



[!INCLUDE[Commenting house rules](../includes/houserules.md)]
