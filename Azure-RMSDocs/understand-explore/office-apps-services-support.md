---
title: Applicazioni e servizi Office | Azure RMS
description: Informazioni su come le applicazioni Office, ad esempio Word, Excel, PowerPoint e Outlook, e i servizi Office, ad esempio Exchange e SharePoint, possono usare Microsoft Azure Rights Management per proteggere i dati dell'organizzazione.
author: cabailey
manager: mbaldwin
ms.date: 09/06/2016
ms.topic: article
ms.prod: 
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 388e67cd-c16f-4fa0-a7bb-ffe0def2be81
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: f0871436caef79187349d700d190564b08cc9e46
ms.openlocfilehash: 1e1a52e637671d857fac22c51a635e726fa99b01


---


# Applicazioni e servizi Office

>*Si applica a: Azure Rights Management, Office 365*

Le applicazioni dell'utente finale, ad esempio Word, Excel, PowerPoint e Outlook, e i servizi Office, ad esempio Exchange e SharePoint, possono usare Microsoft Azure Rights Management per proteggere i dati dell'organizzazione.

## Applicazioni Office: Word, Excel, PowerPoint, Outlook
Queste applicazioni supportano Rights Management a livello nativo usando Information Rights Management (IRM) e consentono agli utenti di applicare la protezione a un documento salvato oppure a un messaggio e-mail da inviare Gli utenti possono applicare i modelli oppure, per Word, Excel e PowerPoint, possono scegliere impostazioni con un elevato livello di personalizzazione per limitare l'accesso, i diritti e l'uso. 

Gli utenti possono ad esempio configurare un file di Word in modo che possano accedervi solo le persone appartenenti all'organizzazione o per controllare se un foglio di calcolo Excel può essere modificato, per impostarne l'accesso in sola lettura o per impedirne la stampa. Per file soggetti a vincoli temporali, è possibile configurare un'ora di scadenza (direttamente oppure applicando un modello) per stabilire il momento in cui non è più possibile accedere al file. Oltre a scegliere un modello, per Outlook gli utenti possono scegliere l'opzione **Non inoltrare** per impedire la perdita di dati.

## Exchange Online ed Exchange Server
Quando si usa Exchange Online oppure Exchange Server, è possibile usare l'integrazione IRM (Information Rights Management) che fornisce soluzioni di protezione delle informazioni aggiuntive:

-   **Exchange ActiveSync IRM** per proteggere dispositivi mobili e usare messaggi di posta elettronica protetti.

-   Supporto RMS per **Outlook Web App**, implementato in modo analogo al client Outlook, in modo che gli utenti possano proteggere i messaggi di posta elettronica tramite modelli o tramite la specifica di singole opzioni e che possano leggere e usare i messaggi di posta elettronica ricevuti in modo protetto.

-   **Regole di protezione** per client Outlook che un amministratore configura per applicare automaticamente modelli RMS ai messaggi di posta elettronica per destinatari specifici. Quando ad esempio vengono inviati messaggi e-mail interni all'ufficio legale dell'organizzazione, è possibile configurare tali messaggi in modo che possano essere letti solo dai membri dell'ufficio e che non possano essere inoltrati. Prima di inviare il messaggio e-mail gli utenti vedono la regola di protezione applicata e, per impostazione predefinita, possono rimuoverla se ritengono non sia necessaria. I messaggi e-mail vengono crittografati prima dell'invio. Per altre informazioni, vedere [Regole di protezione di Outlook](https://technet.microsoft.com/library/dd638178%28v=exchg.150%29.aspx) e [Creare una regola di protezione di Outlook](https://technet.microsoft.com/library/dd638196%28v=exchg.150%29.aspx) nella libreria di Exchange.

-   **Regole di trasporto** che un amministratore configura per applicare automaticamente modelli RMS a messaggi di posta elettronica in base a determinate proprietà, ad esempio mittente, destinatario, oggetto del messaggio e contenuto. Tali regole sono concettualmente analoghe alle regole di protezione, ma non consentono agli utenti di rimuovere la protezione, possono essere applicate a Outlook Web Access e a messaggi e-mail inviati da dispositivi mobili e non crittografano i messaggi e-mail prima che vengano inviati dal client. Per altre informazioni, vedere [Creare una regola di protezione del trasporto](https://technet.microsoft.com/library/dd302432.aspx) nella libreria di Exchange.

-   **Criteri di prevenzione della perdita dei dati** che contengono set di condizioni per filtrare i messaggi di posta elettronica e intraprendere azioni per prevenire la perdita di dati nel caso di informazioni riservate o sensibili, ad esempio quelle personali o correlate alla carta di credito. Quando si rilevano dati sensibili, è possibile usare i suggerimenti relativi ai criteri per avvertire gli utenti che potrebbe essere necessario applicare la protezione in base alle informazioni presenti nel messaggio e-mail. Per altre informazioni, vedere [Prevenzione della perdita di dati](https://technet.microsoft.com/library/jj150527%28v=exchg.150%29.aspx) nella libreria di Exchange.

-   **Crittografia dei messaggi di Office 365** che usa regole di trasporto per inviare messaggi di posta elettronica crittografati a persone all'esterno dell'organizzazione e che comporta la lettura del messaggio in un browser con un'interfaccia analoga a Outlook Web App. Nei messaggi e-mail crittografati della società è possibile personalizzare il testo della dichiarazione di non responsabilità e dell'intestazione nonché aggiungere il logo della società. Per altre informazioni, vedere [Crittografia messaggi di Office 365](https://office.microsoft.com/o365-message-encryption-FX104179182.aspx) nel sito Web di Office.

Se si usa Exchange Server, è possibile usare le funzionalità di protezione delle informazioni con [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] grazie all'implementazione del connettore RMS, che opera come un relè tra i server locali e il servizio cloud RMS. Per altre informazioni, vedere [Distribuzione del connettore di Azure Rights Management](../deploy-use/deploy-rms-connector.md).

## SharePoint Online e SharePoint Server
Quando si usa SharePoint Online o SharePoint Server, è possibile usare l'integrazione IRM (Information Rights Management) che consente agli amministratori di proteggere elenchi o raccolte, in modo che quando un utente estrae un documento il file venga protetto per consentirne la visualizzazione e l'uso solo alle persone autorizzate in base ai criteri di protezione delle informazioni specificati. Il file ad esempio potrebbe essere di sola lettura, potrebbe esserne stata disabilitata la copia del testo oppure potrebbe esserne stato impedito il salvataggio di una copia locale e la stampa.

La protezione delle informazioni per elenchi e raccolte viene sempre applicata da un amministratore e mai da un utente finale e viene applicata a livello di elenco o di raccolta per tutti i documenti contenuti anziché sui file singoli.  Se si usa SharePoint Online, gli utenti possono anche applicare IRM alla raccolta OneDrive for Business.

È necessario inoltre che il servizio IRM sia abilitato per SharePoint. Specificare quindi il servizio Information Rights Management per una libreria. Nel caso di SharePoint Online e OneDrive for Business, gli utenti possono specificare anche Information Rights Management per la raccolta OneDrive for Business. SharePoint non usa i modelli di criteri di diritti, anche se è possibile selezionare alcune impostazioni di configurazione di SharePoint, molto simili alle impostazioni che possono essere specificate nei modelli.

Se si usa SharePoint Server, è possibile usare le funzionalità di protezione delle informazioni con [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] grazie all'implementazione del connettore RMS, che opera come un relè tra i server locali e il servizio cloud RMS. Per ulteriori informazioni, vedere [Distribuzione del connettore di Azure Rights Management](../deploy-use/deploy-rms-connector.md).

> [!NOTE]
> Attualmente, ci sono alcune limitazioni quando si usa IRM con SharePoint:
> 
> -   Non è possibile usare i modelli predefiniti o personalizzati gestiti nel portale di Azure classico.
> -   I file con un'estensione di file PPDF per i file PDF protetti non sono supportati. I file con un'estensione di file PDF e che sono protetti a livello nativo da RMS sono supportati quando si usa un programma per leggere i file PDF che supporta RMS a livello nativo.

Azure RMS applica le restrizioni d'uso e la crittografia dei dati per i documenti quando questi vengono scaricati da SharePoint e non quando il documento viene creato inizialmente in SharePoint o caricato nella raccolta. Per informazioni su come vengono protetti i documenti di essere scaricati, vedere [Crittografia dei dati in OneDrive for Business e SharePoint Online](https://technet.microsoft.com/library/dn905447.aspx) nella documentazione di SharePoint.

Per altre informazioni sull'uso di Azure RMS con SharePoint, vedere il post seguente del blog di Office: [Novità di Information Rights Management in SharePoint e SharePoint Online](http://blogs.office.com/2012/11/09/whats-new-with-information-rights-management-in-sharepoint-and-sharepoint-online/)

## Passaggi successivi

Per altre informazioni sul supporto di Azure Rights Management da parte di altre applicazioni e servizi, vedere [Supporto di Azure Rights Management da parte delle applicazioni](applications-support.md).


<!--HONumber=Sep16_HO1-->


