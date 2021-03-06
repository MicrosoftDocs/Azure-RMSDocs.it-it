---
title: Domande frequenti sulla classificazione e l'assegnazione di etichette - AIP
description: Di seguito sono riportate alcune possibili domande sulle funzionalità di classificazione e assegnazione di etichette di Azure Information Protection vedere se la risposta è disponibile qui.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 03/07/2021
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 4b595b6a-7eb0-4438-b49a-686431f95ddd
ms.reviewer: adhall
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 22d655bc69fc5db7b4bad27eb09a826a1fde34b9
ms.sourcegitcommit: 8a45d209273d748ee0f2a96c97893288c0b7efa5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/08/2021
ms.locfileid: "102446882"
---
# <a name="frequently-asked-questions-about-classification-and-labeling-in-azure-information-protection"></a>Domande frequenti sulla classificazione e l'assegnazione di etichette in Azure Information Protection

>***Si applica a**: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*
>
>***Pertinente per**: [AIP Unified Labeling client e client classico](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients). Per ulteriori informazioni, vedere anche le [domande frequenti solo per il client classico](faqs-classic.md). *

>[!NOTE] 
> Per offrire un'esperienza per i clienti unificata e semplificata, il **client classico di Azure Information Protection** e **Gestione etichette** nel portale di Azure saranno **deprecati** a partire dal **31 marzo 2021**. In questo intervallo di tempo tutti i clienti correnti di Azure Information Protection possono passare alla soluzione di etichettatura unificata usando la piattaforma di etichettatura unificata di Microsoft Information Protection. Altre informazioni nell'[avviso ufficiale sulla deprecazione](https://aka.ms/aipclassicsunset).

Di seguito sono riportate alcune possibili domande sulle funzionalità di classificazione e assegnazione di etichette di Azure Information Protection  vedere se la risposta è disponibile qui. 

## <a name="which-client-do-i-install-for-testing-new-functionality"></a>Quale client si installa per testare nuove funzionalità?

Si consiglia di installare il **client di Azure Information Protection Unified Labeling**. Il client di etichettatura unificata Scarica le etichette e le impostazioni dei criteri da uno dei seguenti centri di amministrazione: 

- Centro sicurezza e conformità di Office 365
- Centro sicurezza Microsoft 365
- Centro di conformità Microsoft 365.

Questo client è ora disponibile a livello generale e potrebbe avere una versione di anteprima per testare funzionalità aggiuntive per una versione futura.

Se le etichette sono ancora state configurate nel portale di Azure di cui non è ancora stata [eseguita la migrazione nell'archivio di etichette unificate](configure-policy-migrate-labels.md), usare invece il **client di Azure Information Protection classico** .

Per altre informazioni, tra cui una tabella di confronto delle funzionalità e delle funzionalità, vedere [scegliere la soluzione per l'assegnazione di etichette Windows](rms-client/use-client.md#choose-your-windows-labeling-solution).

> [!TIP]
> Il client Azure Information Protection è supportato solo in Windows. 
>
> Per classificare e proteggere documenti e messaggi di posta elettronica in iOS, Android, macOS e sul Web, usare le [app di Office che supportano l'assegnazione di etichette incorporata](/microsoft-365/compliance/sensitivity-labels-office-apps#support-for-sensitivity-label-capabilities-in-apps). 
> 

## <a name="where-can-i-find-information-about-using-sensitivity-labels-for-office-apps"></a>Dove è possibile reperire informazioni sull'uso delle etichette di riservatezza per le app di Office?

Vedere le risorse di documentazione seguenti:

- [Informazioni sulle etichette di riservatezza](/microsoft-365/compliance/sensitivity-labels) 

- [Usare le etichette di riservatezza nelle app di Office](/microsoft-365/compliance/sensitivity-labels-office-apps)

- [Abilitare le etichette di riservatezza per i file di Office in SharePoint e OneDrive](/microsoft-365/compliance/sensitivity-labels-sharepoint-onedrive-files)

- [Applicare le etichette di riservatezza ai documenti e ai messaggi di posta elettronica in Office](https://support.office.com/article/Apply-sensitivity-labels-to-your-documents-and-email-within-Office-2f96e7cd-d5a4-403b-8bd7-4cc636bae0f9#ID0EBFAAA=Office_365)

Per informazioni su altri scenari che supportano le etichette di riservatezza, vedere [scenari comuni per le etichette di riservatezza](/microsoft-365/compliance/get-started-with-sensitivity-labels#common-scenarios-for-sensitivity-labels).

## <a name="how-do-i-prevent-somebody-from-removing-or-changing-a-label"></a>Come si può impedire a un utente di rimuovere o modificare un'etichetta?

Per impedire agli utenti di rimuovere o modificare un'etichetta, il contenuto deve essere già protetto e le autorizzazioni di protezione non concedono all'utente il [diritto di utilizzo](configure-usage-rights.md) Esportazione o Controllo completo. 

## <a name="when-an-email-is-labeled-do-any-attachments-automatically-get-the-same-labeling"></a>Quando a un messaggio di posta elettronica viene applicata un'etichetta, eventuali allegati ottengono automaticamente la stessa etichetta?

No. Quando viene applicata un'etichetta a un messaggio di posta elettronica con allegati, tali allegati non ereditano la stessa etichetta. Gli allegati rimangono senza etichetta oppure mantengono un'etichetta applicata separatamente. Se tuttavia l'etichetta per il messaggio di posta elettronica applica una protezione, tale protezione viene applicata agli allegati di Office.

## <a name="how-can-dlp-solutions-and-other-applications-integrate-with-azure-information-protection"></a>Come è possibile integrare soluzioni DLP e altre applicazioni con Azure Information Protection?

Per la classificazione, Azure Information Protection usa metadati persistenti che includono un'etichetta di testo non crittografata. Queste informazioni possono essere lette da soluzioni DLP e da altre applicazioni. 

Per esempi dell'uso di questi metadati con le regole del flusso di posta di Exchange Online, vedere [Configurazione delle regole del flusso di posta per le etichette di Exchange Online](configure-exo-rules.md).