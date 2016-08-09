---
title: Esercitazione introduttiva di Azure Information Protection | Azure Rights Management
description: "Esercitazione introduttiva che consente di provare rapidamente Microsoft Azure Information Protection nell'organizzazione. L'esercitazione è articolata in 4 passaggi, eseguibili in meno di 15 minuti."
author: cabailey
manager: mbaldwin
ms.date: 07/29/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 1260b9e5-dba1-41de-84fd-609076587842
translationtype: Human Translation
ms.sourcegitcommit: 93444affe94b280db2c9e4e2960c6902e491dec6
ms.openlocfilehash: 17670eadc7cbf6111ab7fd0a9322e51d401b86e1


---

# Esercitazione introduttiva di Azure Information Protection 

>*Si applica a: Azure Information Protection (anteprima)*

**[ Informazioni preliminari soggette a modifiche. ]**

Usare questa esercitazione per provare rapidamente l'anteprima di Microsoft Azure Information Protection nell'organizzazione. L'esercitazione è articolata in 4 passaggi, eseguibili in meno di 15 minuti. Facoltativamente, è possibile attivare il servizio Azure Rights Management, esaminare e modificare i criteri di Azure Information Protection predefiniti, installare il client di Azure Information Protection e quindi usare un documento di Word per vedere in azione le funzionalità di classificazione, aggiunta di etichette e protezione.

Questa esercitazione, rivolta ai consulenti e agli amministratori IT, consente di valutare Azure Information Protection come soluzione di protezione delle informazioni aziendali per un'organizzazione. In un ambiente di produzione le istruzioni per attivare il servizio, configurare i criteri di Information Protection e installare il client per gli utenti possono essere eseguite da un amministratore. Le istruzioni per aggiungere etichette al documento possono essere eseguite dagli utenti finali. In questa esercitazione sono inclusi entrambi i set di istruzioni, per illustrare lo scenario end-to-end di classificazione, aggiunta di etichette e protezione dei dati dell'organizzazione. 

In caso di problemi durante l'esecuzione di questa esercitazione o durante l'uso della versione di anteprima di Azure Information Protection, o se si vogliono vedere le opinioni di altri utenti su questa funzionalità, visitare il [sito Azure Information Protection in Yammer](https://www.yammer.com/askipteam/#/threads/inGroup?type=in_group&feedId=8652489&view=all).

## Prerequisiti 
Per completare questa esercitazione, è necessario quanto segue:

- Una sottoscrizione che includa Azure Rights Management e consenta l'accesso alla versione di anteprima di Azure Information Protection. Azure Information Protection è disponibile in tutte le aree che supportano Azure Rights Management. Per altre informazioni sulle opzioni di sottoscrizione disponibili e sui collegamenti alle versioni di valutazione gratuite, vedere [Requisiti per Azure RMS: sottoscrizioni cloud che supportano Azure RMS](../get-started/requirements-subscriptions.md).

- Una sottoscrizione di Azure, per accedere al portale di Azure e configurare i criteri di Azure Information Protection. Se l'organizzazione non ha una sottoscrizione di Azure, è possibile ottenerne una registrandosi per una versione di valutazione gratuita: andare alla pagina [Microsoft Azure - Introduzione](https://account.windowsazure.com/organization) e seguire le istruzioni.

  > [!TIP] 
  > Se è necessario richiedere una di queste sottoscrizioni o entrambe, eseguire questa operazione in anticipo perché talvolta il processo può richiedere alcuni minuti.

- Un account amministratore globale per accedere all'interfaccia di amministrazione di Office 365 o al portale di Azure classico, se è necessario attivare il servizio Rights Management. Questo account deve disporre inoltre di un indirizzo di posta elettronica e di un servizio di posta elettronica funzionante (ad esempio, Exchange Online o Exchange Server).

- Un computer che esegue Windows (almeno Windows 7 con Service Pack 1) e in cui è installato Office Professional Plus 2016, Office Professional Plus 2013 con Service Pack 1 o Office Professional Plus 2010. 

- Se nell'organizzazione è distribuito Active Directory Rights Management Services (AD RMS), il computer deve appartenere a un gruppo di lavoro e non aver usato AD RMS in precedenza. Ciò è obbligatorio se si vogliono proteggere i documenti e assicurarsi che il computer scarichi modelli solo da Azure Rights Management. Non è supportata la connessione contemporanea del computer ad AD RMS e ad Azure RMS. Per informazioni sulla migrazione, vedere [Migrazione da AD RMS ad Azure Rights Management](../plan-design/migrate-from-ad-rms-to-azure-rms.md).   

A questo punto, procedere con l'esercitazione.

>[!div class="step-by-step"]
[&#187; Passaggio 1](infoprotect-tutorial-step1.md)





<!--HONumber=Jul16_HO5-->


