---
title: Terminologia di Azure Information Protection
description: In caso di dubbio su una parola, un'espressione o un acronimo correlato a Microsoft Azure Information Protection, è possibile trovare qui i termini e le abbreviazioni specifici di Azure Information Protection o che assumono un particolare significato se usati nel contesto di questo servizio.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 08/14/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 742877bf-26f5-40e3-b1f7-8475e7c3ce11
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
search.appverid:
- MET150
ms.openlocfilehash: f05c5cae2b0bc38929fb2bba3e060f4e521aa053
ms.sourcegitcommit: fc467e30b67ac218491fccea2d501350d3a656fb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/14/2019
ms.locfileid: "69023979"
---
# <a name="terminology-for-azure-information-protection"></a>Terminologia di Azure Information Protection

>*Si applica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

In caso di dubbio su una parola, un'espressione o un acronimo correlato a Microsoft Azure Information Protection, è possibile trovare qui i termini e le abbreviazioni specifici di Azure Information Protection o che assumono un particolare significato se usati nel contesto di questo servizio.

|Termine|Definizione|
|--------|--------------|
|AADRM|Nome del primo modulo di PowerShell per il servizio di protezione (Azure Rights Management), derivato dall'abbreviazione non ufficiale di Azure Rights Management quando in precedenza era denominato (Windows) Azure Active Directory Rights Management. Questo modulo di PowerShell è ora sostituito con il modulo AIPService.|
|attiva|Per abilitare il servizio di protezione (Azure Rights Management) in modo che un'organizzazione possa proteggere i propri documenti e messaggi di posta elettronica. Questa azione abilita anche le funzionalità IRM in Exchange Online e SharePoint Online.|
|Active Directory Rights Management Services|Spesso abbreviato in *AD RMS*.<br /><br />Ruolo di Windows Server che rende disponibile la protezione basata sulla gestione dei diritti usando la crittografia e i criteri per proteggere documenti, file e messaggi di posta elettronica.|
|AD RMS|Vedere *Active Directory Rights Management Services*.|
|AIPService|Nome corrente del modulo di PowerShell per il servizio di protezione, che sostituisce con il modulo AADRM precedente.|
AzureInformationProtection|Il nome del modulo di PowerShell per il client di Azure Information Protection (classico) e il Azure Information Protection client di etichetta unificata.
|Azure Information Protection|Servizio basato sul cloud che usa le etichette per classificare e proteggere documenti e messaggi di posta elettronica. Azure Rights Management garantisce la protezione tramite criteri di crittografia, identità e autorizzazione.|
Client di Azure Information Protection (versione classica)|Talvolta abbreviato in *client classico*.<br /><br />Lato client originale di Azure Information Protection che consente a utenti, amministratori e servizi di usare le etichette e le impostazioni dei criteri di Azure Information Protection. Ora viene sostituito con il client di Azure Information Protection Unified labeling.|
|Etichetta per Azure Information Protection|Elemento che applica sempre un valore di classificazione a documenti e a messaggi di posta elettronica e può anche proteggerli. Quando viene applicata un'etichetta, le informazioni dell'etichetta vengono archiviate nei metadati per le applicazioni e i servizi in modo da consentire la lettura ed eventualmente l'uso.|
|Criteri di Azure Information Protection|Configurazione definita dall'amministratore per i client e i servizi che usano le etichette e le impostazioni dei criteri di Azure Information Protection.|
|Scanner di Azure Information Protection|Servizio eseguito in Windows Server che consente di individuare, classificare e proteggere i documenti in cartelle locali, condivisioni di rete e siti e raccolte di SharePoint Server.|
|Client per l'etichettatura unificata di Azure Information Protection|Talvolta abbreviato in *client con etichetta unificata*.<br /><br />Il client per i computer Windows che consente a utenti, amministratori e servizi di usare le etichette di riservatezza e le impostazioni dei criteri di etichetta dall'Centro sicurezza e conformità di Office 365, dal centro sicurezza Microsoft 365 e da Microsoft 365 Compliance Center. Sostituisce il client di Azure Information Protection (classico).|
|Azure RMS|Vedere *Azure Rights Management*.|
|Visualizzatore di Azure Information Protection|App eseguita su computer Windows e dispositivi mobili, per visualizzare i file protetti.|
|Azure Rights Management|Spesso abbreviato in *Azure RMS*.<br /><br />Servizio Azure usato da Azure Information Protection che consente di proteggere documenti, file e messaggi di posta elettronica tramite crittografia e criteri.  Noto anche come *servizio Azure Rights Management*. I nomi precedenti includono:<br /><br />- *Windows Azure Active Directory Rights Management*: Spesso abbreviato in Windows Azure AD Rights Management servizio.<br /><br />- *RMS Online*: Nome proposto originale, che talvolta può essere visualizzato nei messaggi di errore e nelle voci del file di log.|
|modello predefinito|Modello di protezione che viene creato automaticamente quando si ottiene una sottoscrizione di Azure Information Protection, in modo da poter subito iniziare a proteggere documenti e messaggi di posta elettronica che contengono informazioni riservate.|
|BYOK|Vedere *bring your own key*.|
|bring your own key|Spesso abbreviato in *BYOK*.<br /><br />Opzione di topologia e configurazione disponibile per un'organizzazione che vuole generare e gestire la propria chiave del tenant per Azure Information Protection.|
|chiave simmetrica|Chiave univoca creata da applicazioni abilitate per RMS per ogni documento o messaggio di posta elettronica protetto tramite Rights Management che consente di limitare il rischio di diffusione delle informazioni.|
|utilizzare|Solo nel contesto protetto: per aprire un documento o un messaggio di posta elettronica da leggere o usare quando il contenuto è protetto dal servizio Rights Management. Per un documento, l'utilizzo include la modifica e l'aggiunta di nuovo contenuto a un documento protetto. Per un messaggio di posta elettronica, l'utilizzo include la risposta a un messaggio protetto.<br /><br />Nel contesto di etichettatura (con o senza protezione): per leggere e potenzialmente usare le informazioni dell'etichetta archiviate nei metadati di file e messaggi di posta elettronica.|
|disattivare|Disabilitare il servizio Rights Management in modo che l'organizzazione non possa più usare Azure Information Protection.|
|modello di reparto|Modello di protezione creato dall'utente e configurato in modo da essere visibile per utenti selezionati, invece che per tutti gli utenti dell'organizzazione. Noto anche come *modello con ambito*.|
|applicazioni abilitate|Applicazioni che supportano Rights Management in modo nativo, ad esempio applicazioni di Office quali Word ed Excel. I fornitori di software indipendenti (ISV) e gli sviluppatori possono anche creare applicazioni che supportano Rights Management in modo nativo.|
|enterprise rights management|Termine generico e conforme agli standard del settore spesso usato per descrivere prodotti e soluzioni che consentono alle organizzazioni di proteggere informazioni sensibili o importanti tramite una combinazione di strumenti per l'autorizzazione di crittografia e criteri. Azure Information Protection è un esempio di soluzione ERM (Enterprise Rights Management).|
|ERM|Vedere *enterprise rights management*.|
|protezione generica|Livello di protezione che consente di eseguire la crittografia di qualsiasi tipo di file e impedire l'apertura del file da parte di utenti non autorizzati. Dopo l'apertura, il file non è più crittografato e può essere usato in un'applicazione che non supporta Rights Management in modo nativo.|
|HYOK|Vedere *hold your own key*.|
|hold your own key|Spesso abbreviato in *HYOK*.<br /><br />Opzione di topologia e configurazione per un'organizzazione che vuole generare e archiviare la propria chiave locale, in genere per motivi legati alla conformità o alle normative.|
|oggetto chiave|Nel contesto della chiave del tenant, entità che contiene i metadati richiesti dal servizio Azure Rights Management per le operazioni di crittografia.|
|label|Vedere *Etichetta di Azure Information Protection*.|
|protezione di informazioni|Spesso abbreviato in *IP*.<br /><br />Termine generico e conforme agli standard del settore che fa riferimento alla protezione di dati e file da accessi non autorizzati, anche quando questi ultimi vengono diffusi oltre i confini dell'organizzazione tramite e-mail o condivisione di documenti. Microsoft Azure Information Protection è un esempio di soluzione per la protezione di informazioni.|
|Information Rights Management|Spesso abbreviato in *IRM*.<br /><br />Termine usato in combinazione con i servizi Office, ad esempio Exchange Server, Word e SharePoint Online, per indicare la capacità di supporto dei servizi Microsoft Rights Management.|
|IRM|Vedere *Information Rights Management*.|
|Crittografia messaggi di Office|Spesso abbreviato in *OME*.<br /><br />Le nuove funzionalità di crittografia messaggi di Office 365 sono integrate a livello nativo con il servizio Azure Rights Management e offrono gli stessi livelli di protezione della posta elettronica per utenti interni ed esterni, aggiornamento automatico dei modelli e supporto dello scenario BYOK (Bring Your Own Key). L'implementazione della crittografia messaggi di Office precedente supportava solo i destinatari esterni, richiedeva una regola per il flusso della posta elettronica e non supportava BYOK.|
|Microsoft Information Protection| Talvolta abbreviato in *MIP*.<br /><br /> Framework per prodotti e funzionalità integrate che usano lo stesso archivio di etichette ("etichette unificate") e consentono di proteggere le informazioni riservate dell'organizzazione.|
|MIP| Vedere *Information Protection Microsoft*|
|MSDRM|Termine usato talvolta in riferimento al client RMS 1.0, sostituito dal client più recente, MSIPC. Questo client meno recente supporta applicazioni sviluppate con RMS SDK 1.0 e supporta Office 2010 e 2007, Exchange 2010 e 2013 nonché SharePoint 2007 e 2010.|
|MSIPC|A volte usato in riferimento al client RMS 2.0, che ha sostituito il meno recente client RMS, MSDRM. Questo client più recente supporta le applicazioni sviluppate con RMS SDK 2.0 e supporta Office 365 ProPlus, Office 2019, Office 2016, Office 2013, SharePoint 2013 e il client Azure Information Protection.|
|protezione nativa|Livello di protezione disponibile in tutte le applicazioni abilitate per RMS che impedisce l'apertura di file da parte di utenti non autorizzati e permette anche di implementare criteri più severi, ad esempio consentire la sola lettura di file e vietarne la stampa. Questo tipo di protezione è inoltre associato al file anche quando quest'ultimo viene inoltrato ad altri utenti o salvato in posizioni pubbliche accessibili da altri utenti.|
|pfile|Estensione di file aggiunta a tutti i file protetti genericamente dal servizio Rights Management.|
|livello di autorizzazioni|Un raggruppamento logico di diritti di utilizzo che rendono più facile per gli utenti finali e gli amministratori scegliere le opzioni di configurazione basate sul ruolo. Ad esempio, Revisore e Coautore.|
|proteggere|Applicare i controlli di Rights Management a file o messaggi di posta elettronica tramite criteri di crittografia, identità e controllo di accesso per proteggere i dati.|
|modello di protezione|Noto anche come *modello di criteri di diritti*, *modello di Rights Management* e *modello RMS*.<br /><br />Gruppo di impostazioni di protezione gestite da un amministratore e che includono i diritti di utilizzo definiti per gli utenti autorizzati e i controlli di accesso per l'accesso con scadenza e offline. |
|publish|Proteggere un file per impedirne l'uso e l'accesso da parte di utenti non autorizzati. Termine usato anche in combinazione con i modelli di protezione e i criteri di Azure Information Protection, per indicare il rendere disponibili questi elementi per l'uso da parte di client e servizi.|
|connettore Rights Management|Servizio di inoltro proxy in uscita che può essere distribuito per servizi locali, ad esempio Exchange Server e SharePoint, per proteggere i dati usando il servizio Azure Rights Management.|
|Autorità di certificazione di Rights Management|Account che ha protetto un documento o un messaggio di posta elettronica.|
|Proprietario di Rights Management|Account che mantiene il controllo completo di un documento o di un messaggio di posta elettronica protetto. A questo account è automaticamente concesso il diritto di utilizzo Controllo completo di Rights Management, senza alcuna data di scadenza o impostazione modalità offline.|
|servizi Rights Management|Termine generico che si applica sia alla versione cloud (Azure Rights Management) che alla versione locale (AD RMS) di Rights Management.|
|applicazione di condivisione Rights Management|Ora sostituita dal client Azure Information Protection.|
|RMS|Vedere *Servizi Rights Management*.|
|connettore RMS|Vedere *Connettore Rights Management*.|
|RMS per utenti singoli|Sottoscrizione gratuita per l'uso di Rights Management se l'organizzazione non ha una sottoscrizione di Office 365 o Azure Active Directory.|
|App RMS sharing|Vedere *Applicazione Rights Management sharing*.|
|modello RMS|Vedere *modello di protezione*.|
|Modalità di sola protezione|Modalità operativa per il client di Azure Information Protection quando non sono presenti criteri di Azure Information Protection per l'applicazione delle etichette. In questa modalità le etichette di classificazione non vengono visualizzate, ma gli utenti possono applicare la protezione di Rights Management.|
|scanner|Vedere *Scanner di Azure Information Protection*.|
|utente con privilegi avanzati|Gruppo di amministratori altamente affidabili che possono decrittografare e aprire i file protetti dall'organizzazione tramite un servizio Rights Management. In genere, questo livello di accesso è obbligatorio per documenti eDiscovery legali e team di controllo.|
|chiave del tenant|Noto anche come *chiave del certificato concessore di licenze server (SLC)* .<br /><br />Chiave univoca di un'organizzazione che protegge tutte le funzionalità di crittografia di Rights Management correlate alla chiave del tenant.|
|etichetta unificata| Nota anche come *etichetta*di riservatezza unificata.<br /><br /> Etichetta che può essere applicata da app, client e servizi che supportano Microsoft Information Protection Framework, per applicare la classificazione e, facoltativamente, la protezione. Nelle app e nei servizi di Office, le etichette unificate vengono implementate come etichette di riservatezza.|
|rimuovere la protezione|Rimuovere i controlli di protezione da file o messaggi di posta elettronica, applicati tramite criteri di crittografia, identità, diritti di utilizzo e controllo di accesso per la protezione dei dati.|
|licenza d'uso|Certificato associato a un documento che viene concesso a un utente che apre un file o un messaggio di posta elettronica protetto da un servizio Rights Management. Questo certificato contiene i diritti dell'utente per il file o il messaggio e-mail e la chiave di crittografia usata per crittografare il contenuto, nonché ulteriori restrizioni di accesso definite nei criteri del documento.|

