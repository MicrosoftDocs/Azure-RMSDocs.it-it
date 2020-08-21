---
title: Domande frequenti sulla classificazione e l'assegnazione di etichette - AIP
description: Di seguito sono riportate alcune possibili domande sulle funzionalità di classificazione e assegnazione di etichette di Azure Information Protection vedere se la risposta è disponibile qui.
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 03/16/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 4b595b6a-7eb0-4438-b49a-686431f95ddd
ms.reviewer: adhall
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: e54afaf29c01072a99bf943eec5326b5c839472f
ms.sourcegitcommit: b9ed44cc71e2fa4927e046a3819f758c3e098e82
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/21/2020
ms.locfileid: "88711970"
---
# <a name="frequently-asked-questions-about-classification-and-labeling-in-azure-information-protection"></a>Domande frequenti sulla classificazione e l'assegnazione di etichette in Azure Information Protection

>*Si applica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

>[!NOTE] 
> Per offrire un'esperienza per i clienti unificata e semplificata, il **client di Azure Information Protection client (versione classica)** e la **Gestione etichette** nel portale di Azure vengono **deprecati** a partire dal **31 marzo 2021**. In questo intervallo di tempo tutti i clienti correnti di Azure Information Protection possono passare alla soluzione di etichettatura unificata usando la piattaforma di etichettatura unificata di Microsoft Information Protection. Altre informazioni nell'[avviso ufficiale sulla deprecazione](https://aka.ms/aipclassicsunset).

Di seguito sono riportate alcune possibili domande sulle funzionalità di classificazione e assegnazione di etichette di Azure Information Protection  vedere se la risposta è disponibile qui. 

## <a name="which-client-do-i-install-for-testing-new-functionality"></a>Quale client si installa per testare nuove funzionalità?

Attualmente sono disponibili due client di Azure Information Protection per Windows: 

- Il **Azure Information Protection client di etichetta unificata** che Scarica le etichette e le impostazioni dei criteri da uno dei seguenti centri di amministrazione: Office 365 Security & Compliance center, Microsoft 365 Security center, Microsoft 365 Compliance Center. Questo client è ora disponibile a livello generale e potrebbe avere una versione di anteprima per testare funzionalità aggiuntive per una versione futura.

- Il **client Azure Information Protection (classico)** che Scarica le etichette e le impostazioni dei criteri dall'portale di Azure. Questo client si basa sulle versioni di disponibilità generale precedenti del client.

Si consiglia di eseguire il test con il client di etichettatura unificata se il set di funzionalità e le funzionalità correnti soddisfano i requisiti aziendali. In caso contrario, o se sono state configurate etichette nel portale di Azure di cui non è ancora stata [eseguita la migrazione nell'archivio Unified Labeling](configure-policy-migrate-labels.md), usare il client classico. Per altre informazioni, inclusa una tabella per il confronto di funzioni e funzionalità, vedere [Scegliere il client Azure Information Protection da usare](./rms-client/use-client.md#choose-which-labeling-client-to-use-for-windows-computers).

Il client Azure Information Protection è supportato solo in Windows. Per classificare e proteggere documenti e messaggi di posta elettronica in iOS, Android, macOS e sul Web, usare le [app di Office che supportano l'assegnazione di etichette incorporata](https://docs.microsoft.com/microsoft-365/compliance/sensitivity-labels-office-apps#support-for-sensitivity-label-capabilities-in-apps). 

## <a name="where-can-i-find-information-about-using-sensitivity-labels-for-office-apps"></a>Dove è possibile reperire informazioni sull'uso delle etichette di riservatezza per le app di Office?

Vedere le risorse di documentazione seguenti:

- [Informazioni sulle etichette di riservatezza](https://docs.microsoft.com/microsoft-365/compliance/sensitivity-labels) 

- [Usare le etichette di riservatezza nelle app di Office](https://docs.microsoft.com/microsoft-365/compliance/sensitivity-labels-office-apps)

- [Abilitare le etichette di riservatezza per i file di Office in SharePoint e OneDrive](https://docs.microsoft.com/microsoft-365/compliance/sensitivity-labels-sharepoint-onedrive-files)

- [Applicare le etichette di riservatezza ai documenti e ai messaggi di posta elettronica in Office](https://support.office.com/article/Apply-sensitivity-labels-to-your-documents-and-email-within-Office-2f96e7cd-d5a4-403b-8bd7-4cc636bae0f9#ID0EBFAAA=Office_365)

Per informazioni su altri scenari che supportano le etichette di riservatezza, vedere [scenari comuni per le etichette di riservatezza](https://docs.microsoft.com/microsoft-365/compliance/get-started-with-sensitivity-labels#common-scenarios-for-sensitivity-labels).

## <a name="can-a-file-have-more-than-one-classification"></a>Un file può avere più di una classificazione?

Poiché gli utenti possono selezionare una sola etichetta alla volta per ogni documento o messaggio di posta elettronica, la classificazione è spesso una sola. Tuttavia, se gli utenti selezionano un'etichetta secondaria, vengono effettivamente applicate due etichette contemporaneamente, ovvero un'etichetta primaria e un'etichetta secondaria. Se si usano etichette secondarie, il file può avere due classificazioni che indicano una relazione padre/figlio per un ulteriore livello di controllo.

Ad esempio, l'etichetta **Confidential** può contenere etichette secondarie, ad esempio **Legal** e **Finance**. È possibile applicare contrassegni visivi di classificazione e modelli di Rights Management diversi alle etichette secondarie. Un utente non può selezionare l'etichetta **riservata** autonomamente; solo una delle relative etichette secondarie, ad esempio **Legal**. Di conseguenza, l'etichetta impostata visualizzata dall'utente sarà **Confidential \ Legal** (Riservato \ Legale). I metadati di tale file includono una sola proprietà di testo personalizzato per **Confidential** (Riservato), una proprietà di testo personalizzato per **Legal** (Legale) e un'altra proprietà che contiene entrambi i valori, **Confidential Legal** (Riservato Legale). 

Quando si usano etichette secondarie, non configurare contrassegni visivi, protezione e condizioni nell'etichetta principale. Quando si usano etichette secondarie, configurare queste impostazioni solo nell'etichetta secondaria. Se si configurano le impostazioni nell'etichetta principale e nella relativa etichetta secondaria, le impostazioni dell'etichetta secondaria hanno priorità.

## <a name="how-do-i-prevent-somebody-from-removing-or-changing-a-label"></a>Come si può impedire a un utente di rimuovere o modificare un'etichetta?

Sebbene esista un' [impostazione dei criteri](configure-policy-settings.md) che richiede agli utenti di indicare perché abbassano un'etichetta di classificazione, rimuovendo un'etichetta o rimuovendo la protezione, questa impostazione non impedisce tali azioni. Per impedire agli utenti di rimuovere o modificare un'etichetta, il contenuto deve essere già protetto e le autorizzazioni di protezione non concedono all'utente il [diritto di utilizzo](configure-usage-rights.md) Esportazione o Controllo completo. 

## <a name="when-an-email-is-labeled-do-any-attachments-automatically-get-the-same-labeling"></a>Quando a un messaggio di posta elettronica viene applicata un'etichetta, eventuali allegati ottengono automaticamente la stessa etichetta?

No. Quando viene applicata un'etichetta a un messaggio di posta elettronica con allegati, tali allegati non ereditano la stessa etichetta. Gli allegati rimangono senza etichetta oppure mantengono un'etichetta applicata separatamente. Se tuttavia l'etichetta per il messaggio di posta elettronica applica una protezione, tale protezione viene applicata agli allegati di Office.

## <a name="how-can-dlp-solutions-and-other-applications-integrate-with-azure-information-protection"></a>Come è possibile integrare soluzioni DLP e altre applicazioni con Azure Information Protection?

Per la classificazione, Azure Information Protection usa metadati persistenti che includono un'etichetta di testo non crittografata. Queste informazioni possono essere lette da soluzioni DLP e da altre applicazioni. 

Per altre informazioni su questi metadati, vedere [Etichettare le informazioni archiviate in documenti e messaggi di posta elettronica](configure-policy.md#label-information-stored-in-emails-and-documents).

Per esempi dell'uso di questi metadati con le regole del flusso di posta di Exchange Online, vedere [Configurazione delle regole del flusso di posta per le etichette di Exchange Online](configure-exo-rules.md).

## <a name="can-i-create-a-document-template-that-automatically-includes-the-classification"></a>È possibile creare un modello di documento che include automaticamente la classificazione?

Sì. È possibile configurare un'etichetta per [applicare un'intestazione o un piè di pagina che include il nome dell'etichetta](configure-policy-markings.md). Tuttavia, se questo non soddisfa i requisiti, solo per il client di Azure Information Protection (classico), è possibile creare un modello di documento con la formattazione desiderata e aggiungere la classificazione come codice campo. 

Ad esempio, si potrebbe usare una tabella nell'intestazione del documento che visualizza la classificazione. Oppure usare una formulazione specifica per un'introduzione che fa riferimento alla classificazione del documento.

Per aggiungere questo codice di campo nel documento:

1. Etichettare il documento e salvarlo. Questa azione consente di creare nuovi campi di metadati che è ora possibile usare per il codice di campo.

2. Nel documento, posizionare il cursore dove si vuole aggiungere la classificazione dell'etichetta e quindi nella scheda **Inserisci** selezionare **Testo** > **Parti rapide** > **Campo**.

3. Nella finestra di dialogo **Campo** selezionare **Informazioni documento** nell'elenco a discesa **Categorie**. Nell'elenco a discesa **Nome campi** selezionare quindi **DOCPROPERTY**.

4. Nell'elenco a discesa **Proprietà** selezionare **Riservatezza** e selezionare **OK**.

La classificazione dell'etichetta corrente viene visualizzata nel documento e questo valore verrà aggiornato automaticamente ogni volta che si apre il documento o si usa il modello. Pertanto, se l'etichetta cambia, la classificazione visualizzata per questo codice di campo viene aggiornata automaticamente nel documento.

## <a name="how-is-classification-for-emails-using-azure-information-protection-different-from-exchange-message-classification"></a>In che modo la classificazione per i messaggi di posta elettronica utilizza Azure Information Protection diversa dalla classificazione dei messaggi di Exchange?

La classificazione dei messaggi di Exchange è una funzionalità precedente in grado di classificare i messaggi di posta elettronica e viene implementata indipendentemente dalle etichette Azure Information Protection o dalle etichette di riservatezza che applicano

Tuttavia, è possibile integrare questa funzionalità precedente con le etichette, in modo che quando gli utenti classificano un messaggio di posta elettronica usando Outlook sul Web e usando alcune applicazioni di posta elettronica per dispositivi mobili, la classificazione delle etichette e i contrassegni di etichetta corrispondenti vengono aggiunti automaticamente.

È possibile applicare la stessa tecnica per usare le etichette con Outlook sul web e le applicazioni di posta elettronica per dispositivi mobili.

Si noti che non è necessario eseguire questa operazione se si usa Outlook sul Web con Exchange Online, perché questa combinazione supporta l'etichettatura incorporata quando si pubblicano le etichette di riservatezza da Office 365 Security & Compliance Center, Microsoft 365 Security Center o Microsoft Compliance Center.

Se non è possibile usare le etichette predefinite con Outlook sul Web, vedere la procedura di configurazione per questa soluzione alternativa: [integrazione con la classificazione dei messaggi di Exchange legacy](rms-client/client-admin-guide-customizations.md#integration-with-the-legacy-exchange-message-classification)