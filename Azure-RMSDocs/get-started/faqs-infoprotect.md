---
title: Domande frequenti sulla classificazione e l&quot;assegnazione di etichette - AIP
description: "Di seguito sono riportate alcune possibili domande sulle funzionalità di classificazione e assegnazione di etichette di Azure Information Protection e le relative risposte."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 03/29/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 4b595b6a-7eb0-4438-b49a-686431f95ddd
ms.reviewer: adhall
ms.suite: ems
ms.openlocfilehash: 7f2bd30603f88ec72ee51f980c40903362cfdeba
ms.sourcegitcommit: 8733730882bea6f505f4c6d53d4bdf08c3106f40
translationtype: HT
---
# <a name="frequently-asked-questions-about-classification-and-labeling-in-azure-information-protection"></a>Domande frequenti sulla classificazione e l'assegnazione di etichette in Azure Information Protection

>*Si applica a: Azure Information Protection, Office 365*

Di seguito sono riportate alcune possibili domande sulle funzionalità di classificazione e assegnazione di etichette di Azure Information Protection  e le relative risposte. 

## <a name="what-can-i-do-with-the-classification-capabilities-in-azure-information-protection"></a>Che cosa si può fare con le funzionalità di classificazione di Azure Information Protection?

L'esercitazione introduttiva consente in pochi minuti di vedere queste caratteristiche in pratica: [Esercitazione introduttiva di Azure Information Protection](infoprotect-quick-start-tutorial.md).

Per sapere quando saranno disponibili altre funzionalità e nuove caratteristiche per la classificazione, seguire gli annunci nel [blog di Enterprise Mobility + Security](https://blogs.technet.microsoft.com/enterprisemobility/?product=azure-information-protection) e nel [sito Yammer](https://www.yammer.com/askipteam/#/threads/inGroup?type=in_group&feedId=8652489&view=all). Nella versione corrente sono presenti alcune limitazioni, incluse le seguenti:

- I nomi e le descrizioni delle etichette sono supportati solo in una lingua.

- Manca la funzione di registrazione centralizzata per la classificazione e l'aggiunta di etichette.

- Le condizioni per la classificazione automatica devono essere frasi o motivi.

- Non sono disponibili funzionalità di assegnazione di etichette per le app di Office per dispositivi mobili (iOS e Android) e computer Mac o per Office Web Apps (Office Online).

- Le funzionalità di classificazione e assegnazione di etichette non sono integrate con Exchange Online o SharePoint Online.

- Nell'SDK per sviluppatori e partner non sono ancora incluse le funzionalità di classificazione e assegnazione di etichette.

Nella versione di febbraio, molte delle limitazioni precedenti sono state rimosse. Per altre informazioni, vedere l'[annuncio del post di blog](https://blogs.technet.microsoft.com/enterprisemobility/2017/02/08/azure-information-protection-december-update-moves-to-general-availability/).

## <a name="do-i-need-to-be-a-global-admin-to-configure-classification-and-labels"></a>È necessario essere un amministratore globale per configurare la classificazione e le etichette?

Per configurare i criteri di Azure Information Protection, è necessario accedere al portale di Azure come amministratore globale di Azure Active Directory.

Se al momento dell'installazione del [client Azure Information Protection](https://www.microsoft.com/en-us/download/details.aspx?id=53018) si sceglie di installare i criteri demo, per provare a usare la funzionalità per l'assegnazione di etichette non è necessario accedere al portale. I criteri demo installano localmente i criteri predefiniti di Azure Information Protection. È quindi possibile provare ad aggiungere etichette a documenti e a messaggi di posta elettronica, ma per modificare etichette o aggiungerne nuove sarà necessario accedere al portale di Azure. 

## <a name="which-options-in-the-azure-portal-are-p1-or-p2"></a>Quali opzioni nel portale di Azure sono P1 o P2?

Per verificare quali sono le funzionalità incluse nella sottoscrizione di **Azure Information Protection Premium 1** (P1) rispetto alla sottoscrizione di **Azure Information Protection Premium 2** (P2), vedere l'[elenco delle funzionalità](https://www.microsoft.com/en-us/cloud-platform/azure-information-protection-features) nel sito di Azure Information Protection. Tuttavia, come guida generale, le funzionalità avanzate, ad esempio la classificazione automatica e HYOK sono specifiche della sottoscrizione di Azure Information Protection Premium 2.

## <a name="can-a-file-have-more-than-one-classification"></a>Un file può avere più di una classificazione?

Poiché gli utenti possono selezionare una sola etichetta alla volta per ogni documento o messaggio di posta elettronica, la classificazione è spesso una sola. Tuttavia, se gli utenti selezionano un'etichetta secondaria, vengono effettivamente applicate due etichette contemporaneamente, ovvero un'etichetta primaria e un'etichetta secondaria. Se si usano etichette secondarie, il file può avere due classificazioni che indicano una relazione padre/figlio per un ulteriore livello di controllo.

Ad esempio, l'etichetta **Confidential** (Riservato) potrebbe contenere le etichette secondarie **Legal** (Legale) e **Finance** (Contabilità). È possibile applicare contrassegni visivi di classificazione e modelli di Rights Management diversi alle etichette secondarie. L'utente non potrà selezionare direttamente l'etichetta **Confidential** (Riservato), ma solo una delle relative etichette secondarie, ad esempio **Legal** (Legale). Di conseguenza, l'etichetta impostata visualizzata dall'utente sarà **Confidential \ Legal** (Riservato \ Legale). I metadati del file includeranno una sola proprietà di testo personalizzato per **Confidential** (Riservato), una proprietà di testo personalizzato per **Legal** (Legale) e un'ulteriore proprietà che contiene entrambi i valori, **Confidential Legal** (Riservato Legale). 

Quando si usano etichette secondarie, non configurare contrassegni visivi, protezione e condizioni nell'etichetta principale. Quando si usano etichette secondarie, configurare queste impostazioni solo nell'etichetta secondaria. Se si configurano le impostazioni nell'etichetta principale e nella relativa etichetta secondaria, le impostazioni dell'etichetta secondaria hanno priorità.

## <a name="when-an-email-is-labeled-do-any-attachments-automatically-get-the-same-labeling"></a>Quando a un messaggio di posta elettronica viene applicata un'etichetta, eventuali allegati ottengono automaticamente la stessa etichetta?

No. Quando viene applicata un'etichetta a un messaggio di posta elettronica con allegati, tali allegati non ereditano la stessa etichetta. Gli allegati rimangono senza etichetta oppure mantengono un'etichetta applicata separatamente. Tuttavia, se l'etichetta per il messaggio di posta elettronica applica una protezione, tale protezione viene applicata agli allegati.

## <a name="how-is-azure-information-protection-classification-for-emails-different-from-exchange-message-classification"></a>Qual è la differenza tra la classificazione dei messaggi di posta elettronica di Azure Information Protection e la classificazione dei messaggi di Exchange?

La classificazione dei messaggi di Exchange è una funzionalità precedente che consente di classificare i messaggi di posta elettronica e viene implementata indipendentemente dalla classificazione di Azure Information Protection. Tuttavia, è possibile integrare le due soluzioni in modo che quando gli utenti classificano un messaggio di posta elettronica con Outlook Web App e in alcune applicazioni di posta per dispositivi mobili, vengono automaticamente aggiunti la classificazione di Azure Information Protection e i contrassegni di etichetta corrispondenti. Exchange aggiunge la classificazione e il client Azure Information Protection applica le impostazioni delle etichette corrispondenti per tale classificazione.

Sebbene Outlook Web App non supporta ancora in modo nativo la protezione e la classificazione di Azure Information Protection, è possibile adottare questa stessa tecnica per usare le etichette con questo client di posta elettronica oltre al client Outlook sul desktop.

Per ottenere questa soluzione: 

1. Usare il cmdlet [New-MessageClassification](https://technet.microsoft.com/library/bb124400) di Exchange PowerShell per creare le classificazioni dei messaggi con la proprietà Name che esegue il mapping ai nomi di etichetta nei criteri di Azure Information Protection. 

2. Creare una regola di trasporto di Exchange per ogni etichetta: applicare la regola quando le proprietà del messaggio includono la classificazione configurata e modificare le proprietà del messaggio per impostare un'intestazione del messaggio. 

    Per l'intestazione del messaggio, le informazioni da specificare sono disponibili nelle proprietà di un file Office classificato tramite l'etichetta di Azure Information Protection. Identificare la proprietà del file con il formato **MSIP_Label_<GUID>Enabled** e specificare questa stringa per l'intestazione del messaggio, quindi specificare **True** per il valore dell'intestazione. Ad esempio, l'intestazione del messaggio potrebbe essere simile a questa stringa: **MSIP_Label_132616b8-f72d-5d1e-aec1-dfd89eb8c5b2_Enabled**


Quando gli utenti usano l'app Outlook Web Access o un client del dispositivo mobile che supporta la protezione di Rights Management, si verifica quanto segue: 

- Gli utenti selezionano la classificazione dei messaggi di Exchange e inviano il messaggio di posta elettronica.

- La regola di Exchange rileva la classificazione di Exchange e di conseguenza modifica l'intestazione del messaggio per aggiungere la classificazione di Azure Information Protection.

- Quando i destinatari che eseguono il client Azure Information Protection visualizzano il messaggio di posta elettronica in Outlook, vedranno l'etichetta di Azure Information Protection assegnata e l'eventuale intestazione, piè di pagina o filigrana corrispondente del messaggio di posta elettronica. 

Se le etichette di Azure Information Protection applicano la protezione di Rights Management, aggiungerla alla configurazione della regola selezionando l'opzione per modificare la sicurezza del messaggio, applicare la protezione dei diritti, quindi selezionare il modello RMS o l'opzione Non inoltrare.

È anche possibile configurare le regole di trasporto per eseguire il mapping inverso: quando viene rilevata un'etichetta di Azure Information Protection, impostare una classificazione dei messaggi di Exchange corrispondente. A tale scopo, eseguire questa procedura:

- Per ogni etichetta di Azure Information Protection, creare una regola di trasporto da applicare quando l'intestazione **msip_labels** include il nome dell'etichetta (ad esempio, **Confidential**) e applicare una classificazione dei messaggi che esegua il mapping a questa etichetta.

## <a name="how-can-dlp-solutions-and-other-applications-integrate-with-azure-information-protection"></a>Come è possibile integrare soluzioni DLP e altre applicazioni con Azure Information Protection?

Per la classificazione, Azure Information Protection usa metadati persistenti che includono un'etichetta di testo non crittografata. Queste informazioni possono essere lette da soluzioni DLP e da altre applicazioni. Per i file, questi metadati vengono archiviati all'interno di proprietà personalizzate, per i messaggi di posta elettronica nelle intestazioni dei messaggi.


[!INCLUDE[Commenting house rules](../includes/houserules.md)]