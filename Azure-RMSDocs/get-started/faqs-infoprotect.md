---
title: Domande frequenti sulla classificazione e l'assegnazione di etichette - AIP
description: Di seguito sono riportate alcune possibili domande sulle funzionalità di classificazione e assegnazione di etichette di Azure Information Protection e le relative risposte.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 06/26/2018
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 4b595b6a-7eb0-4438-b49a-686431f95ddd
ms.reviewer: adhall
ms.suite: ems
ms.openlocfilehash: 6aafa526e8061ef01f2cdd554c2843d814b623d1
ms.sourcegitcommit: 44ff610dec678604c449d42cc0b0863ca8224009
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/31/2018
ms.locfileid: "39370126"
---
# <a name="frequently-asked-questions-about-classification-and-labeling-in-azure-information-protection"></a>Domande frequenti sulla classificazione e l'assegnazione di etichette in Azure Information Protection

>*Si applica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](http://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

Di seguito sono riportate alcune possibili domande sulle funzionalità di classificazione e assegnazione di etichette di Azure Information Protection  e le relative risposte. 

## <a name="what-can-i-do-with-the-classification-capabilities-in-azure-information-protection"></a>Che cosa si può fare con le funzionalità di classificazione di Azure Information Protection?

L'esercitazione introduttiva consente in pochi minuti di vedere queste caratteristiche in pratica: [Esercitazione introduttiva di Azure Information Protection](infoprotect-quick-start-tutorial.md).

Per sapere quando saranno disponibili altre funzionalità e nuove caratteristiche per la classificazione, seguire gli annunci nel [blog di Enterprise Mobility + Security](https://cloudblogs.microsoft.com/enterprisemobility/?product=azure-information-protection) e nel [sito Yammer](https://www.yammer.com/askipteam/#/threads/inGroup?type=in_group&feedId=8652489&view=all). Nella versione corrente sono presenti alcune limitazioni, incluse le seguenti:

- Manca la funzione di registrazione centralizzata per la classificazione e l'aggiunta di etichette.

- Non sono disponibili funzionalità di assegnazione di etichette nelle app di Office per dispositivi mobili (iOS e Android) e computer Mac o per Office Web Apps (Office Online).

- Le funzionalità di classificazione e assegnazione di etichette non sono integrate con Exchange Online o SharePoint Online.

Per richiedere nuove funzionalità e votare per le richieste, visitare il [sito User Voice](https://msip.uservoice.com/) per Azure Information Protection.

## <a name="do-i-need-to-be-a-global-admin-to-configure-classification-and-labels"></a>È necessario essere un amministratore globale per configurare la classificazione e le etichette?

Con l'introduzione del nuovo ruolo Amministratore di Information Protection, la risposta a questa domanda è disponibile nella pagina principale delle domande frequenti: [È necessario essere un amministratore globale per configurare Azure Information Protection oppure tale configurazione può essere delegata ad altri amministratori?](faqs.md#do-you-need-to-be-a-global-admin-to-configure-azure-information-protection-or-can-i-delegate-to-other-administrators)

Se al momento dell'installazione del [client Azure Information Protection](https://www.microsoft.com/en-us/download/details.aspx?id=53018) si sceglie di installare i criteri demo, per provare a usare la funzionalità per l'assegnazione di etichette non è necessario accedere al portale. I criteri demo installano localmente i criteri predefiniti di Azure Information Protection. È quindi possibile provare ad aggiungere etichette a documenti e a messaggi di posta elettronica, ma per modificare etichette o aggiungerne nuove sarà necessario accedere al portale di Azure. 

## <a name="can-a-file-have-more-than-one-classification"></a>Un file può avere più di una classificazione?

Poiché gli utenti possono selezionare una sola etichetta alla volta per ogni documento o messaggio di posta elettronica, la classificazione è spesso una sola. Tuttavia, se gli utenti selezionano un'etichetta secondaria, vengono effettivamente applicate due etichette contemporaneamente, ovvero un'etichetta primaria e un'etichetta secondaria. Se si usano etichette secondarie, il file può avere due classificazioni che indicano una relazione padre/figlio per un ulteriore livello di controllo.

Ad esempio, l'etichetta **Confidential** (Riservato) potrebbe contenere le etichette secondarie **Legal** (Legale) e **Finance** (Contabilità). È possibile applicare contrassegni visivi di classificazione e modelli di Rights Management diversi alle etichette secondarie. L'utente non potrà selezionare direttamente l'etichetta **Confidential** (Riservato), ma solo una delle relative etichette secondarie, ad esempio **Legal** (Legale). Di conseguenza, l'etichetta impostata visualizzata dall'utente sarà **Confidential \ Legal** (Riservato \ Legale). I metadati di tale file includono una sola proprietà di testo personalizzato per **Confidential** (Riservato), una proprietà di testo personalizzato per **Legal** (Legale) e un'altra proprietà che contiene entrambi i valori, **Confidential Legal** (Riservato Legale). 

Quando si usano etichette secondarie, non configurare contrassegni visivi, protezione e condizioni nell'etichetta principale. Quando si usano etichette secondarie, configurare queste impostazioni solo nell'etichetta secondaria. Se si configurano le impostazioni nell'etichetta principale e nella relativa etichetta secondaria, le impostazioni dell'etichetta secondaria hanno priorità.

## <a name="how-do-i-prevent-somebody-from-removing-or-changing-a-label"></a>Come si può impedire a un utente di rimuovere o modificare un'etichetta?

Anche se esiste un'[impostazione dei criteri](../deploy-use/configure-policy-settings.md) che richiede agli utenti di dichiarare per quali motivi abbassano un'etichetta di classificazione, rimuovono un'etichetta o rimuovono la protezione, questa impostazione non impedisce queste azioni. Per impedire agli utenti di rimuovere o modificare un'etichetta, il contenuto deve essere già protetto e le autorizzazioni di protezione non concedono all'utente il [diritto di utilizzo](../deploy-use/configure-usage-rights.md) Esportazione o Controllo completo. 

## <a name="when-an-email-is-labeled-do-any-attachments-automatically-get-the-same-labeling"></a>Quando a un messaggio di posta elettronica viene applicata un'etichetta, eventuali allegati ottengono automaticamente la stessa etichetta?

No. Quando viene applicata un'etichetta a un messaggio di posta elettronica con allegati, tali allegati non ereditano la stessa etichetta. Gli allegati rimangono senza etichetta oppure mantengono un'etichetta applicata separatamente. Se tuttavia l'etichetta per il messaggio di posta elettronica applica una protezione, tale protezione viene applicata agli allegati di Office.

## <a name="how-can-dlp-solutions-and-other-applications-integrate-with-azure-information-protection"></a>Come è possibile integrare soluzioni DLP e altre applicazioni con Azure Information Protection?

Per la classificazione, Azure Information Protection usa metadati persistenti che includono un'etichetta di testo non crittografata. Queste informazioni possono essere lette da soluzioni DLP e da altre applicazioni. 

Per altre informazioni ed esempi dell'uso di questi metadati con le regole del flusso di posta di Exchange Online, vedere [Configurazione delle regole del flusso di posta per le etichette di Exchange Online](../deploy-use/configure-exo-rules.md).

## <a name="how-is-azure-information-protection-classification-for-emails-different-from-exchange-message-classification"></a>Qual è la differenza tra la classificazione dei messaggi di posta elettronica di Azure Information Protection e la classificazione dei messaggi di Exchange?

La classificazione dei messaggi di Exchange è una funzionalità precedente che consente di classificare i messaggi di posta elettronica e viene implementata indipendentemente dalla classificazione di Azure Information Protection. 

È tuttavia possibile integrare le due soluzioni in modo che quando gli utenti classificano un messaggio di posta elettronica con Outlook sul web e con alcune applicazioni di posta elettronica per dispositivi mobili, vengono automaticamente aggiunti la classificazione di Azure Information Protection e i contrassegni di etichetta corrispondenti. 

È possibile applicare la stessa tecnica per usare le etichette con Outlook sul web e le applicazioni di posta elettronica per dispositivi mobili.

Per i passaggi di configurazione, vedere [Integrate Exchange message classification with Azure Information Protection for a mobile device labeling solution](../rms-client/client-admin-guide-customizations.md#integration-with-exchange-message-classification-for-a-mobile-device-labeling-solution) (Integrare la classificazione messaggi di Exchange ad Azure Information Protection per una soluzione di etichettatura per dispositivi mobili). 



