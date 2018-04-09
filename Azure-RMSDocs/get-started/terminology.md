---
title: Terminologia di Azure Information Protection
description: In caso di dubbio su una parola, un'espressione o un acronimo correlato a Microsoft Azure Information Protection, è possibile trovare qui i termini e le abbreviazioni specifici di Azure Information Protection o che assumono un particolare significato se usati nel contesto di questo servizio.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 03/30/2018
ms.topic: get-started-article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 742877bf-26f5-40e3-b1f7-8475e7c3ce11
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 20ec9893bba090b1d17d67b06fb614a2baee3403
ms.sourcegitcommit: b17432ed155394111c878eb57b5fa7adf9df9755
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/03/2018
---
# <a name="terminology-for-azure-information-protection"></a>Terminologia di Azure Information Protection

>*Si applica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](http://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

In caso di dubbio su una parola, un'espressione o un acronimo correlato a Microsoft Azure Information Protection, è possibile trovare qui i termini e le abbreviazioni specifici di Azure Information Protection o che assumono un particolare significato se usati nel contesto di questo servizio.

|Termine|Definizione|
|--------|--------------|
|AADRM|Nome del modulo di Windows PowerShell per il servizio Azure Rights Management, derivato dall'abbreviazione non ufficiale di Azure Rights Management quando in precedenza era denominato (Windows) Azure Active Directory Rights Management.|
|attivare|Consente di abilitare il servizio Azure Rights Management in modo che un'organizzazione possa proteggere i propri documenti e i propri messaggi di posta elettronica. Questa azione abilita le funzionalità di Rights Management anche in Exchange Online e SharePoint Online.|
|Active Directory Rights Management Services|Spesso abbreviato in *AD RMS*.<br /><br />Ruolo di Windows Server che fornisce la protezione basata sulla gestione dei diritti tramite crittografia e criteri che consentono di proteggere documenti, file e messaggi di posta elettronica.|
|AD RMS|Vedere *Active Directory Rights Management Services*.|
|Azure Information Protection|Servizio basato sul cloud che usa funzionalità di classificazione, assegnazione di etichette e protezione per proteggere documenti e messaggi di posta elettronica. Azure Rights Management garantisce la protezione tramite criteri di crittografia, identità e autorizzazione.|
|Azure Rights Management|Spesso abbreviato in *Azure RMS*.<br /><br />Servizio Azure usato da Azure Information Protection che consente di proteggere documenti, file e messaggi di posta elettronica tramite crittografia e criteri.  Noto anche come *servizio Azure Rights Management*. I nomi precedenti includono:<br /><br />- *Windows Azure Active Directory Rights Management*: spesso abbreviato in servizio Windows Azure AD Rights Management.<br /><br />- *RMS Online*: il nome proposto in origine, che è possibile incontrare nei messaggi di errore e nelle voci dei file di log.|
|Azure RMS|Vedere *Azure Rights Management*.|
|BYOK|Vedere *bring your own key*.|
|bring your own key|Spesso abbreviato in *BYOK*.<br /><br />Opzione di topologia e configurazione disponibile per un'organizzazione che vuole generare e gestire la propria chiave del tenant per Azure Information Protection.|
|chiave simmetrica|Chiave univoca creata da applicazioni abilitate per RMS per ogni documento o messaggio e-mail protetto mediante [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] che consente di limitare il rischio di diffusione delle informazioni.|
|utilizzare|Sbloccare un file protetto da [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] per l'uso o la lettura.|
|disattivare|Disabilitare il servizio Rights Management in modo che l'organizzazione non possa più usare Azure Information Protection.|
|modello di reparto|Modello di criteri relativi ai diritti creato dall'utente (modello personalizzato) e configurato in modo da essere visibile per utenti selezionati, invece che per tutti gli utenti dell'organizzazione.|
|applicazioni abilitate|Applicazioni che supportano Rights Management in modo nativo, ad esempio applicazioni di Office quali Word ed Excel. I fornitori di software indipendenti (ISV) e gli sviluppatori possono anche creare applicazioni che supportano [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] in modo nativo.|
|enterprise rights management|Termine generico e conforme agli standard del settore spesso usato per descrivere prodotti e soluzioni che consentono alle organizzazioni di proteggere informazioni sensibili o importanti tramite una combinazione di strumenti per l'autorizzazione di crittografia e criteri. Azure Information Protection è un esempio di soluzione ERM (Enterprise Rights Management).|
|ERM|Vedere *enterprise rights management*.|
|protezione generica|Livello di protezione che consente di eseguire la crittografia di qualsiasi tipo di file e impedire l'apertura del file da parte di utenti non autorizzati. Una volta aperto, il file non è più crittografato e può essere usato in un'applicazione che non supporta [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] in modo nativo.|
|HYOK|Vedere *hold your own key*.|
|hold your own key|Spesso abbreviato in *HYOK*.<br /><br />Opzione di topologia e configurazione per un'organizzazione che vuole generare e archiviare la propria chiave locale, in genere per motivi legati alla conformità o alle normative.|
|oggetto chiave|Nel contesto della chiave del tenant, entità che contiene i metadati richiesti dal servizio Azure Rights Management per le operazioni di crittografia.|
|protezione di informazioni|Spesso abbreviato in *IP*.<br /><br />Termine generico e conforme agli standard del settore che fa riferimento alla protezione di dati e file da accessi non autorizzati, anche quando questi ultimi vengono diffusi oltre i confini dell'organizzazione tramite e-mail o condivisione di documenti. Microsoft Azure Information Protection è un esempio di soluzione per la protezione di informazioni.|
|Information Rights Management|Spesso abbreviato in *IRM*.<br /><br />Termine usato in combinazione con i servizi Office, quali Exchange Server, Word e SharePoint Online, per indicare la capacità di supporto dei servizi Microsoft Rights Management.|
|IRM|Vedere *Information Rights Management*.|
|Crittografia messaggi di Office|Spesso abbreviato in *OME*.<br /><br />Le nuove funzionalità di crittografia messaggi di Office 365 sono integrate a livello nativo con il servizio Azure Rights Management e offrono gli stessi livelli di protezione della posta elettronica per utenti interni ed esterni, aggiornamento automatico dei modelli e supporto dello scenario BYOK (Bring Your Own Key). L'implementazione della crittografia messaggi di Office precedente supportava solo i destinatari esterni, richiedeva una regola per il flusso della posta elettronica e non supportava BYOK.|
|MSDRM|Termine usato talvolta in riferimento al client RMS 1.0, sostituito dal client più recente, MSIPC. Questo client meno recente supporta applicazioni sviluppate con RMS SDK 1.0 e supporta Office 2010 e 2007, Exchange 2010 e 2013 nonché SharePoint 2007 e 2010.|
|MSIPC|A volte usato in riferimento al client RMS 2.0, che ha sostituito il meno recente client RMS, MSDRM. Questo client più recente supporta le applicazioni sviluppate con RMS SDK 2.0 e supporta Office 2016 e Office 2013, SharePoint 2013, l'applicazione RMS sharing e il client Azure Information Protection.|
|protezione nativa|Livello di protezione disponibile in tutte le applicazioni abilitate per RMS che impedisce l'apertura di file da parte di utenti non autorizzati e permette anche di implementare criteri più severi, ad esempio consentire la sola lettura di file e vietarne la stampa. Questo tipo di protezione è inoltre associato al file anche quando quest'ultimo viene inoltrato ad altri utenti o salvato in posizioni pubbliche accessibili da altri utenti.|
|pfile|Estensione di file aggiunta a tutti i file protetti genericamente dal servizio Rights Management.|
|ppdf|Estensione di file creata da un servizio Rights Management quando genera automaticamente una copia PDF di un file (Word, Excel, PowerPoint o PDF) condivisa tramite posta elettronica, in modo che il file sia leggibile (ma non modificabile) su tutti i dispositivi.|
|livello di autorizzazioni|Un raggruppamento logico di diritti di utilizzo che rendono più facile per gli utenti finali e gli amministratori scegliere le opzioni di configurazione basate sul ruolo. Ad esempio, Revisore e Coautore.|
|proteggere|Applicare i controlli di Rights Management a file o messaggi di posta elettronica tramite criteri di crittografia, identità e controllo di accesso per proteggere i dati.|
|pubblicare|Proteggere un file per impedirne l'uso e l'accesso da parte di utenti non autorizzati.|
|connettore Rights Management|Servizio di inoltro proxy in uscita che può essere distribuito per servizi locali, ad esempio Exchange Server e SharePoint, per proteggere i dati mediante il servizio Azure Rights Management.|
|Autorità di certificazione di Rights Management|Account che ha protetto un documento o un messaggio di posta elettronica.|
|Proprietario di Rights Management|Account che mantiene il controllo completo di un documento o di un messaggio di posta elettronica protetto. A questo account è automaticamente concesso il diritto di utilizzo Controllo completo di Rights Management, senza alcuna data di scadenza o impostazione modalità offline.|
|servizi Rights Management|Termine generico che fa riferimento sia alla versione cloud di [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] ([!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)]) sia alla versione locale di [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] (AD RMS).|
|Applicazione Rights Management sharing|Applicazione facoltativa per Windows e per i più diffusi dispositivi mobili, che supporta la condivisione sicura di file sul posto e tramite posta elettronica, ora sostituita dal client Azure Information Protection.|
|RMS|Vedere *Servizi Rights Management*.|
|connettore RMS|Vedere *Connettore Rights Management*.|
|RMS per utenti singoli|Sottoscrizione gratuita per l'uso di [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] quando l'organizzazione non ha una sottoscrizione a Office 365 o Azure Active Directory.|
|App di condivisione RMS|Vedere *Applicazione Rights Management sharing*.|
|Modalità di sola protezione|Modalità operativa per il client di Azure Information Protection quando non sono presenti criteri di Azure Information Protection per l'applicazione delle etichette. In questa modalità le etichette di classificazione non vengono visualizzate, ma gli utenti possono applicare la protezione di Rights Management.|
|utente con privilegi avanzati|Gruppo di amministratori altamente affidabili che possono decrittografare e aprire i file protetti dall'organizzazione tramite un servizio Rights Management. In genere, questo livello di accesso è obbligatorio per documenti eDiscovery legali e team di controllo.|
|chiave del tenant|Nota anche come chiave del certificato concessore di licenze server (SLC).<br /><br />Chiave univoca di un'organizzazione che protegge tutte le funzionalità di crittografia di [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] correlate alla chiave del tenant.|
|rimuovere la protezione|Rimuovere da file o messaggi di posta elettronica i controlli di Rights Management, applicati tramite criteri di crittografia, identità e controllo di accesso per la protezione dei dati.|
|licenza d'uso|Certificato associato a un documento che viene concesso a un utente che apre un file o un messaggio di posta elettronica protetto da un servizio Rights Management. Questo certificato contiene i diritti dell'utente per il file o il messaggio e-mail e la chiave di crittografia usata per crittografare il contenuto, nonché ulteriori restrizioni di accesso definite nei criteri del documento.|

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
