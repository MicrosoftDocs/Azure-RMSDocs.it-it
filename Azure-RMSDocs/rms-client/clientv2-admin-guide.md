---
title: Azure Information Protection unified Guida dell'amministratore client l'assegnazione di etichette
description: Istruzioni e informazioni per gli amministratori in una rete aziendale che sono responsabili della distribuzione di Azure Information Protection unified client per l'assegnazione di etichette per Windows.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 05/17/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.suite: ems
ms.openlocfilehash: 6564980da8ad4067d83c408c2baf0afd8ab5c181
ms.sourcegitcommit: 2d08bee51c26af3159bd52456e12e0166c8369c1
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/17/2019
ms.locfileid: "65822227"
---
# <a name="azure-information-protection-unified-labeling-client-administrator-guide"></a>Azure Information Protection unified Guida dell'amministratore client l'assegnazione di etichette

>*Si applica a: Active Directory Rights Management Services, [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8, Windows 7 con SP1, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2*
>
> *Istruzioni per: [Azure Information Protection unified client per l'assegnazione di etichette per Windows](../faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*

Usare le informazioni in questa Guida se si è responsabili per Azure Information Protection unified client l'assegnazione di etichette in una rete aziendale, o se si desiderano informazioni più tecniche rispetto di [Azure Information Protection unified l'assegnazione di etichette Guida dell'utente client](clientv2-user-guide.md). 

Ad esempio: 

- Comprendere i diversi componenti di questo client e se è necessario installarlo

- Come installare il client per gli utenti, con informazioni su prerequisiti, opzioni e parametri di installazione e controlli di verifica

- Individuare i file e i log di utilizzo del client

- Identificare i tipi di file supportati dal client

- Usare il client con PowerShell per il controllo dalla riga di comando

**In caso di domande su argomenti non trattati in questa documentazione**, visitare il [sito di Yammer su Azure Information Protection](https://www.yammer.com/AskIPTeam). 

## <a name="technical-overview-of-the-azure-information-protection-unified-labeling-client"></a>Panoramica tecnica del client Azure Information Protection unified l'assegnazione di etichette

Il client di assegnazione di etichette unificato di Azure Information Protection include quanto segue:

- Un componente aggiuntivo Office, che consente di installare una **sensibilità** pulsante della barra multifunzione agli utenti di selezionare le etichette di riservatezza e un'opzione per visualizzare la barra di Azure Information Protection per una migliore visibilità dell'etichetta.

- Esplora file, opzioni tramite clic con il pulsante destro del mouse per l'applicazione di etichette di classificazione e della protezione ai file.

- Un visualizzatore per visualizzare file protetti quando un'applicazione nativa non è in grado di aprirli.

- Un modulo di PowerShell per applicare e rimuovere etichette di classificazione e la protezione dei file. 

- Il client Rights Management che comunica con il servizio Azure Rights Management (Azure RMS) per crittografare e proteggere i file.

Fatta eccezione per il visualizzatore, il client di assegnazione di etichette unificato di Azure Information Protection non può essere utilizzato con applicazioni e servizi che comunicano direttamente con il servizio Azure Rights Management o Active Directory Rights Management Services.

Se si usa AD RMS e si vuole passare ad Azure Information Protection, vedere [Migrazione da AD RMS ad Azure Information Protection](../migrate-from-ad-rms-to-azure-rms.md).


## <a name="should-you-deploy-the-azure-information-protection-unified-labeling-client"></a>È necessario distribuire il client di assegnazione di etichette unificato di Azure Information Protection?

Distribuire il client di assegnazione di etichette unificato di Azure Information Protection se si usa [etichette di riservatezza nel centro di conformità e sicurezza di Office 365](https://docs.microsoft.com/Office365/SecurityCompliance/sensitivity-labels), e applica le seguenti operazioni:

- Si vuole classificare (e, facoltativamente, proteggere) documenti e messaggi di posta elettronica selezionando etichette all'interno delle app di Office (Word, Excel, PowerPoint, Outlook) nei computer Windows.

- Si vogliono classificare (e, facoltativamente, proteggere) file tramite Esplora file, che supporta altri tipi di file rispetto a quelli supportati da Office, la selezione multipla e le cartelle.

- Si vuole eseguire script che classifichino (e, facoltativamente, proteggano) documenti tramite comandi di PowerShell.

- Si vuole visualizzare documenti protetti quando non è installata un'applicazione nativa per visualizzare i file o questa applicazione non è in grado di aprire i documenti.

Esempio che illustra l'Office componente aggiuntivo per Azure Information Protection unified client l'assegnazione di etichette, visualizzare la nuova **sensibilità** pulsante sulla barra multifunzione e la barra di Azure Information Protection facoltativa:

![Barra Azure Information Protection con criterio predefinito](../media/v2word2016-calloutsv2.png)

## <a name="installing-and-supporting-the-azure-information-protection-unified-labeling-client"></a>Installazione e il supporto del client di assegnazione di etichette unificato di Azure Information Protection

È possibile installare il client di assegnazione di etichette unificato di Azure Information Protection usando un file eseguibile o un file di programma di installazione di Windows. Per altre informazioni su ogni scelta e istruzioni, vedere [installare il client di assegnazione di etichette unificato di Azure Information Protection per gli utenti](clientv2-admin-guide-install.md).  

Usare le sezioni seguenti per informazioni sull'installazione del client. 

### <a name="installation-checks-and-troubleshooting"></a>Controlli per l'installazione e risoluzione dei problemi

Dopo aver installato il client, usare l'opzione **Guida e commenti** per aprire la finestra di dialogo **Microsoft Azure Information Protection**:

- Da un'applicazione di Office: Nel **Home** nella scheda il **sensibilità** gruppo, selezionare **sensibilità**e quindi selezionare **Guida e commenti**.

- Da Esplora file: fare clic con il pulsante destro del mouse su uno o più file o su una cartella, scegliere **Classifica e proteggi** e quindi **Guida e commenti**. 

#### <a name="help-and-feedback-section"></a>Sezione **Guida e commenti**

Il **avvisare collegamento ulteriori** reindirizza per impostazione predefinita per il [Azure Information Protection](https://www.microsoft.com/cloud-platform/azure-information-protection) sito Web. È possibile configurare il proprio collegamento all'URL che rimanda a una pagina della Guida personalizzata come una delle impostazioni dei criteri nel centro di conformità e sicurezza di Office 365.

Il **Esporta log** automaticamente a raccogliere e allegare i file di log per Azure Information Protection unified imprevisto delle etichette client se è stato chiesto di inviarli al supporto tecnico Microsoft. Questa opzione può essere usata anche dagli utenti finali per inviare i file di log all'help desk.

Il **Ripristina le impostazioni** disconnette l'utente, consente di eliminare le etichette di riservatezza attualmente scaricato e i criteri e reimposta le impostazioni utente per il servizio Azure Rights Management.

##### <a name="more-information-about-the-reset-settings-option"></a>Altre informazioni sull'opzione Ripristina le impostazioni

- Non è necessario essere un amministratore locale per usare questa opzione e questa azione non viene registrata nel Visualizzatore eventi. 

- A meno che i file non siano bloccati, questa azione elimina tutti i file nelle posizioni seguenti. Questi file includono i certificati client, i modelli di Rights Management, etichette di riservatezza e i criteri da Office 365 Security & centro conformità e le credenziali utente memorizzato nella cache. I file di log del client non vengono eliminati.
    
    - %LocalAppData%\Microsoft\DRM
    
    - %LocalAppData%\Microsoft\MSIPC
    
    - %LocalAppData%\Microsoft\MSIP\Policy.msip
    
    - %LocalAppData%\Microsoft\MSIP\TokenCache

- Vengono eliminate le chiavi e le impostazioni del Registro di sistema seguenti. Se sono stati impostati valori personalizzati per queste chiavi del Registro di sistema, dopo la reimpostazione del client è necessario riconfigurarli. 
    
    Per le reti aziendali, queste impostazioni vengono in genere configurate tramite Criteri di gruppo e in questo caso vengono automaticamente riapplicate al momento dell'aggiornamento dei Criteri di gruppo nel computer. Potrebbero essere tuttavia presenti impostazioni configurate una sola volta tramite script o manualmente. In questi casi, è necessario intervenire per riconfigurare queste impostazioni. Ad esempio, è possibile che i computer eseguano un script una sola volta per configurare le impostazioni per il reindirizzamento ad Azure Information Protection, poiché si sta eseguendo la migrazione da AD RMS e nella rete è ancora presente un punto di connessione del servizio. Dopo aver reimpostato il client, il computer deve eseguire nuovamente lo script.
    
    - HKEY_CURRENT-USER\SOFTWARE\Microsoft\Office\15.0\Common\Identity
    
    - HKEY_CURRENT-USER\SOFTWARE\Microsoft\Office\14.0\Common\DRM
    
    - HKEY_CURRENT-USER\SOFTWARE\Microsoft\Office\15.0\Common\DRM
    
    - HKEY_CURRENT-USER\SOFTWARE\Microsoft\Office\16.0\Common\DRM
    
    - HKEY_CURRENT-USER\SOFTWARE\Classes\Local Settings\Software\Microsoft\MSIPC    

- L'utente connesso viene disconnesso.

#### <a name="client-status-section"></a>Sezione **Stato del client**

Usare il valore di **Connessione effettuata come** per verificare se il nome utente visualizzato identifica l'account da usare per l'autenticazione di Azure Information Protection. Questo nome utente deve corrispondere a un account usato per Office 365 o Azure Active Directory. L'account deve anche appartenere a un tenant di Office 365 è configurato per le etichette di riservatezza in Centro di conformità e di sicurezza di Office 365.

Se è necessario accedere come utente diverso da quello visualizzato, vedere la [Accedi come utente diverso](clientv2-admin-guide-customizations.md#sign-in-as-a-different-user) istruzioni.

Usare le informazioni di **Versione** per verificare la versione del client installata. È possibile controllare se questa è la versione più recente di rilascio versione e le nuove funzionalità e correzioni, vedere la [le informazioni sulla versione di versione](unifiedlabelingclient-version-release-history.md) per il client.

## <a name="support-for-multiple-languages"></a>Supporto di altre lingue

Il client di assegnazione di etichette unificato di Azure Information Protection supporta le stesse lingue supportate da Office 365. Per un elenco di queste lingue, vedere la sezione **Office 365, Exchange Online Protection e Power BI** nella pagina [Disponibilità internazionale](https://products.office.com/business/international-availability) di Office.

Per queste lingue, le opzioni di menu, finestre di dialogo e messaggi di Azure Information Protection client unificato imprevisto delle etichette visualizzati nella lingua dell'utente. È disponibile un unico programma di installazione che rileva la lingua, pertanto è richiesta alcuna configurazione aggiuntiva per installare il client di assegnazione di etichette unificato di Azure Information Protection per lingue diverse. 

Tuttavia, il client di assegnazione di etichette unificato di Azure Information Protection non supporta attualmente lingue diverse per le etichette. Inoltre, i contrassegni visivi non vengono convertiti e non supportano più lingue.

## <a name="post-installation-tasks"></a>Attività post-installazione

Dopo aver installato il client di assegnazione di etichette unificato di Azure Information Protection, accertarsi di assegnare agli utenti istruzioni per informazioni su come etichettare i documenti e messaggi di posta elettronica e linee guida per le etichette da scegliere per scenari specifici. Ad esempio: 

- Istruzioni per l'utente online: [Guida per l'utente di Azure Information Protection](client-user-guide.md)

- Scaricare un manuale dell'utente personalizzabile: [Azure Information Protection End User Adoption Guide](https://download.microsoft.com/download/7/1/2/712A280C-1C66-4EF9-8DC3-88EE43BEA3D4/Azure_Information_Protection_End_User_Adoption_Guide_EN_US.pdf) (Manuale d'uso di Azure Information Protection per utenti finali)

## <a name="upgrading-and-maintaining-the-azure-information-protection-unified-labeling-client"></a>L'aggiornamento e la gestione di Azure Information Protection unified client l'assegnazione di etichette

> [!NOTE]
> Azure Information Protection unified imprevisto delle etichette client supporta l'aggiornamento del client Azure Information Protection, nonché l'aggiornamento da versioni precedenti del client Azure Information Protection unified imprevisto delle etichette.

Il team di Azure Information Protection aggiorna regolarmente il client di assegnazione di etichette unificato di Azure Information Protection per nuove funzionalità e correzioni. Gli annunci vengono pubblicati nel [sito Yammer](https://www.yammer.com/AskIPTeam) del team.

Se si usa Windows Update, il client di assegnazione di etichette unificato di Azure Information Protection Aggiorna automaticamente la versione con disponibilità generale del client, indipendentemente dal modo in cui è stato installato il client. Le nuove versioni del client vengono pubblicate nel catalogo alcune settimane dopo il rilascio.

In alternativa, è possibile aggiornare manualmente il client scaricando la nuova versione dall'[Area download Microsoft](https://www.microsoft.com/en-us/download/details.aspx?id=53018). Installare quindi la nuova versione per aggiornare il client. È necessario utilizzare questo metodo per aggiornare le versioni di anteprima e se si esegue l'aggiornamento del client Azure Information Protection.

Se esegue l'aggiornamento dal client Azure Information Protection in Windows 7, le applicazioni di Office verranno riavviata automaticamente durante l'aggiornamento del client. Il riavvio automatico non si applica a sistemi operativi successivi, o se si esegue l'aggiornamento da una versione precedente del client unificato imprevisto delle etichette.

Quando si esegue l'aggiornamento manuale, disinstallare prima la versione precedente solo se si sta modificando il metodo di installazione, ad esempio se si passa dalla versione eseguibile (EXE) del client alla versione di Windows Installer (MSI) del client, oppure se è necessario installare una versione precedente del client, ad esempio se è stata installata la versione di anteprima corrente per i test e ora è necessario tornare alla versione disponibile a livello generale corrente.

Usare la [criteri di cronologia e il supporto di rilascio versione](unifiedlabelingclient-version-release-history.md) per comprendere i criteri di supporto per Azure Information Protection unified client l'assegnazione di etichette, le versioni attualmente supportate, e ciò che è nuove e modificate per supportati versioni. 

## <a name="uninstalling-the-azure-information-protection-unified-labeling-client"></a>Disinstallazione di Azure Information Protection unified client l'assegnazione di etichette

Per disinstallare il client è possibile usare una delle opzioni seguenti:

- Usare il Pannello di controllo per disinstallare un programma: Fare clic su **Microsoft Azure Information Protection** > **Disinstalla**

- Eseguire nuovamente il file eseguibile (ad esempio, **AzInfoProtection_UL.exe**) e dal **Modifica installazione** fare clic su **Disinstalla**. 

- Eseguire l'eseguibile con **/uninstall**. ad esempio `AzInfoProtection.exe /uninstall`

## <a name="next-steps"></a>Passaggi successivi
Per installare il client, vedere [installare il client di assegnazione di etichette unificato di Azure Information Protection per gli utenti](clientv2-admin-guide-install.md).

Se il client è già stato installato, vedere gli argomenti seguenti per altre informazioni che potrebbero essere necessarie per supportare il client:

- [Personalizzazioni](clientv2-admin-guide-customizations.md)

- [File del client e registrazione dell'utilizzo](client-admin-guide-files-and-logging.md)

- [Tipi di file supportati](client-admin-guide-file-types.md)

- [Comandi di PowerShell](client-admin-guide-powershell.md)


