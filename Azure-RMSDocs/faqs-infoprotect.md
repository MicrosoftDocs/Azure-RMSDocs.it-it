---
title: Domande frequenti sulla classificazione e l'assegnazione di etichette - AIP
description: Di seguito sono riportate alcune possibili domande sulle funzionalità di classificazione e assegnazione di etichette di Azure Information Protection e le relative risposte.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 01/25/2019
ms.topic: conceptual
ms.service: information-protection
ms.assetid: 4b595b6a-7eb0-4438-b49a-686431f95ddd
ms.reviewer: adhall
ms.suite: ems
ms.openlocfilehash: 706989f3461e8df540d351aed7e21d331fc8e307
ms.sourcegitcommit: 0fad4196f397fa32c60e6d24791fcad43689c4ba
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/28/2019
ms.locfileid: "55088089"
---
# <a name="frequently-asked-questions-about-classification-and-labeling-in-azure-information-protection"></a>Domande frequenti sulla classificazione e l'assegnazione di etichette in Azure Information Protection

>*Si applica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

Di seguito sono riportate alcune possibili domande sulle funzionalità di classificazione e assegnazione di etichette di Azure Information Protection  e le relative risposte. 

## <a name="what-can-i-do-with-the-classification-capabilities-in-azure-information-protection"></a>Che cosa si può fare con le funzionalità di classificazione di Azure Information Protection?

L'esercitazione [Modificare i criteri e creare una nuova etichetta](infoprotect-quick-start-tutorial.md) consente in pochi minuti di vedere queste funzionalità in pratica.

Per sapere quando saranno disponibili altre funzionalità e nuove caratteristiche per la classificazione, seguire gli annunci nel [blog di Enterprise Mobility + Security](https://techcommunity.microsoft.com/t5/Enterprise-Mobility-Security/bg-p/enterprisemobilityandsecurity/label-name/Azure%20Information%20Protection) e nel [sito Yammer](https://www.yammer.com/askipteam/#/threads/inGroup?type=in_group&feedId=8652489&view=all). Nella versione corrente sono presenti alcune limitazioni, incluse le seguenti:

- L'assegnazione di etichette non funziona nelle app Web di Office (Office Online).

- Le funzionalità di classificazione e assegnazione di etichette non sono integrate con Exchange Online o SharePoint Online.

> [!NOTE]
> **Ora disponibile in anteprima**:
> - Reporting centralizzato per la classificazione e l'aggiunta di etichette. Per altre informazioni, vedere [Reporting centralizzato per Azure Information Protection](reports-aip.md).
>
>**Rilasciate di recente**:
> - funzionalità di etichettatura inclusa nelle app di Office per dispositivi mobili (iOS e Android) e per i computer Mac. Per altre informazioni, vedere [Applicare etichette di riservatezza a documenti e messaggi di posta elettronica all'interno di Office](https://aka.ms/officemipdocs).

Per richiedere nuove funzionalità e votare per le richieste, visitare il [sito User Voice](https://msip.uservoice.com/) per Azure Information Protection.

## <a name="do-i-need-to-be-a-global-admin-to-configure-classification-and-labels"></a>È necessario essere un amministratore globale per configurare la classificazione e le etichette?

Con l'introduzione del nuovo ruolo di amministratore di Information Protection, la risposta a questa domanda si trova nella pagina principale delle Domande frequenti: [È necessario essere un amministratore globale per configurare Azure Information Protection oppure tale configurazione può essere delegata ad altri amministratori?](faqs.md#do-you-need-to-be-a-global-admin-to-configure-azure-information-protection-or-can-i-delegate-to-other-administrators)

Se al momento dell'installazione del [client Azure Information Protection](https://www.microsoft.com/en-us/download/details.aspx?id=53018) si sceglie di installare i criteri demo, per provare a usare la funzionalità per l'assegnazione di etichette non è necessario accedere al portale. I criteri demo installano localmente i criteri predefiniti di Azure Information Protection. È quindi possibile provare ad aggiungere etichette a documenti e a messaggi di posta elettronica, ma per modificare etichette o aggiungerne nuove sarà necessario accedere al portale di Azure. 

## <a name="can-a-file-have-more-than-one-classification"></a>Un file può avere più di una classificazione?

Poiché gli utenti possono selezionare una sola etichetta alla volta per ogni documento o messaggio di posta elettronica, la classificazione è spesso una sola. Tuttavia, se gli utenti selezionano un'etichetta secondaria, vengono effettivamente applicate due etichette contemporaneamente, ovvero un'etichetta primaria e un'etichetta secondaria. Se si usano etichette secondarie, il file può avere due classificazioni che indicano una relazione padre/figlio per un ulteriore livello di controllo.

Ad esempio, l'etichetta **Confidential** (Riservato) potrebbe contenere le etichette secondarie **Legal** (Legale) e **Finance** (Contabilità). È possibile applicare contrassegni visivi di classificazione e modelli di Rights Management diversi alle etichette secondarie. L'utente non potrà selezionare direttamente l'etichetta **Confidential** (Riservato), ma solo una delle relative etichette secondarie, ad esempio **Legal** (Legale). Di conseguenza, l'etichetta impostata visualizzata dall'utente sarà **Confidential \ Legal** (Riservato \ Legale). I metadati di tale file includono una sola proprietà di testo personalizzato per **Confidential** (Riservato), una proprietà di testo personalizzato per **Legal** (Legale) e un'altra proprietà che contiene entrambi i valori, **Confidential Legal** (Riservato Legale). 

Quando si usano etichette secondarie, non configurare contrassegni visivi, protezione e condizioni nell'etichetta principale. Quando si usano etichette secondarie, configurare queste impostazioni solo nell'etichetta secondaria. Se si configurano le impostazioni nell'etichetta principale e nella relativa etichetta secondaria, le impostazioni dell'etichetta secondaria hanno priorità.

## <a name="how-do-i-prevent-somebody-from-removing-or-changing-a-label"></a>Come si può impedire a un utente di rimuovere o modificare un'etichetta?

Anche se esiste un'[impostazione dei criteri](configure-policy-settings.md) che richiede agli utenti di dichiarare per quali motivi abbassano un'etichetta di classificazione, rimuovono un'etichetta o rimuovono la protezione, questa impostazione non impedisce queste azioni. Per impedire agli utenti di rimuovere o modificare un'etichetta, il contenuto deve essere già protetto e le autorizzazioni di protezione non concedono all'utente il [diritto di utilizzo](configure-usage-rights.md) Esportazione o Controllo completo. 

## <a name="when-an-email-is-labeled-do-any-attachments-automatically-get-the-same-labeling"></a>Quando a un messaggio di posta elettronica viene applicata un'etichetta, eventuali allegati ottengono automaticamente la stessa etichetta?

No. Quando viene applicata un'etichetta a un messaggio di posta elettronica con allegati, tali allegati non ereditano la stessa etichetta. Gli allegati rimangono senza etichetta oppure mantengono un'etichetta applicata separatamente. Se tuttavia l'etichetta per il messaggio di posta elettronica applica una protezione, tale protezione viene applicata agli allegati di Office.

## <a name="how-can-dlp-solutions-and-other-applications-integrate-with-azure-information-protection"></a>Come è possibile integrare soluzioni DLP e altre applicazioni con Azure Information Protection?

Per la classificazione, Azure Information Protection usa metadati persistenti che includono un'etichetta di testo non crittografata. Queste informazioni possono essere lette da soluzioni DLP e da altre applicazioni. 

Per altre informazioni ed esempi dell'uso di questi metadati con le regole del flusso di posta di Exchange Online, vedere [Configurazione delle regole del flusso di posta per le etichette di Exchange Online](configure-exo-rules.md).

## <a name="can-i-create-a-document-template-that-automatically-includes-the-classification"></a>È possibile creare un modello di documento che include automaticamente la classificazione?

Sì. È possibile configurare un'etichetta per [applicare un'intestazione o un piè di pagina che include il nome dell'etichetta](configure-policy-markings.md). Se ciò non soddisfa requisiti specifici, è possibile creare un modello di documento con la formattazione desiderata e aggiungere la classificazione come codice di campo. 

Ad esempio, si potrebbe usare una tabella nell'intestazione del documento che visualizza la classificazione. Oppure usare una formulazione specifica per un'introduzione che fa riferimento alla classificazione del documento.

Per aggiungere questo codice di campo nel documento:

1. Etichettare il documento e salvarlo. Questa azione consente di creare nuovi campi di metadati che è ora possibile usare per il codice di campo.

2. Nel documento, posizionare il cursore dove si vuole aggiungere la classificazione dell'etichetta e quindi nella scheda **Inserisci** selezionare **Testo** > **Parti rapide**  >  **Campo**.

3. Nella finestra di dialogo **Campo** selezionare **Informazioni documento** nell'elenco a discesa **Categorie**. Nell'elenco a discesa **Nome campi** selezionare quindi **DOCPROPERTY**.

4. Nell'elenco a discesa **Proprietà** selezionare **Riservatezza** e selezionare **OK**.

La classificazione dell'etichetta corrente viene visualizzata nel documento e questo valore verrà aggiornato automaticamente ogni volta che si apre il documento o si usa il modello. Pertanto, se l'etichetta cambia, la classificazione visualizzata per questo codice di campo viene aggiornata automaticamente nel documento.

## <a name="how-is-azure-information-protection-classification-for-emails-different-from-exchange-message-classification"></a>Qual è la differenza tra la classificazione dei messaggi di posta elettronica di Azure Information Protection e la classificazione dei messaggi di Exchange?

La classificazione dei messaggi di Exchange è una funzionalità precedente che consente di classificare i messaggi di posta elettronica e viene implementata indipendentemente dalla classificazione di Azure Information Protection. 

È tuttavia possibile integrare le due soluzioni in modo che quando gli utenti classificano un messaggio di posta elettronica con Outlook sul web e con alcune applicazioni di posta elettronica per dispositivi mobili, vengono automaticamente aggiunti la classificazione di Azure Information Protection e i contrassegni di etichetta corrispondenti. 

È possibile applicare la stessa tecnica per usare le etichette con Outlook sul web e le applicazioni di posta elettronica per dispositivi mobili.

Per i passaggi di configurazione, vedere [Integrate Exchange message classification with Azure Information Protection for a mobile device labeling solution](./rms-client/client-admin-guide-customizations.md#integration-with-exchange-message-classification-for-a-mobile-device-labeling-solution) (Integrare la classificazione messaggi di Exchange ad Azure Information Protection per una soluzione di etichettatura per dispositivi mobili). 



