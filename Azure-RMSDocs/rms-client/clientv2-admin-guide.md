---
title: Guida dell'amministratore client per l'assegnazione di etichette unificata Azure Information Protection
description: Istruzioni e informazioni per gli amministratori in una rete aziendale che sono responsabili della distribuzione del client Azure Information Protection Unified Labeling per Windows.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 07/16/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: v2client
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 95c855701b1fc8de2e3f9f458b2cd760a3abdd4b
ms.sourcegitcommit: 9968a003865ff2456c570cf552f801a816b1db07
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/05/2019
ms.locfileid: "68793220"
---
# <a name="azure-information-protection-unified-labeling-client-administrator-guide"></a>Guida dell'amministratore client per l'assegnazione di etichette unificata Azure Information Protection

>*Si applica a: Active Directory Rights Management Services, [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8, Windows 7 con SP1, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2*
>
> *Istruzioni per: [Azure Information Protection client di etichetta unificata per Windows](../faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*

Utilizzare le informazioni contenute in questa guida se si è responsabili del client Azure Information Protection Unified Labeling in una rete aziendale o se si desiderano informazioni più tecniche rispetto a quelle presenti nell' [Azure Information Protection utente client con etichetta unificata Guida](clientv2-user-guide.md). 

Ad esempio:

- Comprendere i diversi componenti di questo client e se è necessario installarlo

- Come installare il client per gli utenti, con informazioni su prerequisiti, opzioni e parametri di installazione e controlli di verifica

- Individuare i file e i log di utilizzo del client

- Identificare i tipi di file supportati dal client

- Usare il client con PowerShell per il controllo dalla riga di comando

**In caso di domande su argomenti non trattati in questa documentazione**, visitare il [sito di Yammer su Azure Information Protection](https://www.yammer.com/AskIPTeam). 

## <a name="technical-overview-of-the-azure-information-protection-unified-labeling-client"></a>Panoramica tecnica sul client di Azure Information Protection Unified Labeling

Il Azure Information Protection client Unified Labeling include quanto segue:

- Un componente aggiuntivo di Office, che installa un pulsante di riservatezza sulla barra multifunzione per consentire agli utenti di selezionare le etichette di riservatezza e un'opzione per visualizzare la barra di Azure Information Protection per una migliore visibilità delle etichette.

- Esplora file, opzioni tramite clic con il pulsante destro del mouse per l'applicazione di etichette di classificazione e della protezione ai file.

- Un visualizzatore per visualizzare file protetti quando un'applicazione nativa non è in grado di aprirli.

- Un modulo di PowerShell per applicare e rimuovere etichette di classificazione e la protezione dei file. 

- Il client Rights Management che comunica con il servizio di Azure Rights Management (Azure RMS) per crittografare e proteggere i file.

Ad eccezione del visualizzatore, il Azure Information Protection client Unified Labeling non può essere usato con le applicazioni e i servizi che comunicano direttamente con il servizio Rights Management di Azure o con Active Directory Rights Management Services.

Se si usa AD RMS e si vuole passare ad Azure Information Protection, vedere [Migrazione da AD RMS ad Azure Information Protection](../migrate-from-ad-rms-to-azure-rms.md).


## <a name="should-you-deploy-the-azure-information-protection-unified-labeling-client"></a>È consigliabile distribuire il client di Azure Information Protection Unified Labeling?

Distribuire il client di etichettatura unificata Azure Information Protection se si usano [le etichette di riservatezza nell'Centro sicurezza e conformità di Office 365](https://docs.microsoft.com/Office365/SecurityCompliance/sensitivity-labels)e si verifica una delle condizioni seguenti:

- Si vuole classificare e, facoltativamente, proteggere i documenti e i messaggi di posta elettronica selezionando etichette dalle app di Office (Word, Excel, PowerPoint, Outlook) nei computer Windows.

- Si vogliono classificare (e, facoltativamente, proteggere) file tramite Esplora file, che supporta altri tipi di file rispetto a quelli supportati da Office, la selezione multipla e le cartelle.

- Si vuole eseguire script che classifichino (e, facoltativamente, proteggano) documenti tramite comandi di PowerShell.

- Si vuole testare un servizio attualmente in anteprima che consente di individuare, classificare e, facoltativamente, proteggere i file archiviati in locale.

- Si vuole visualizzare documenti protetti quando non è installata un'applicazione nativa per visualizzare i file o questa applicazione non è in grado di aprire i documenti.

Esempio che illustra il componente aggiuntivo di Office per il client di Azure Information Protection Unified Labeling, visualizzando il nuovo pulsante Sensitivity sulla barra multifunzione e la barra di Azure Information Protection facoltativa:

![Barra Azure Information Protection con criterio predefinito](../media/v2word2016-calloutsv2.png)

## <a name="installing-and-supporting-the-azure-information-protection-unified-labeling-client"></a>Installazione e supporto del client Azure Information Protection Unified Labeling

È possibile installare il client di assegnazione di etichette Azure Information Protection unificato usando un file eseguibile o un file di Windows Installer. Per ulteriori informazioni su ogni scelta e istruzioni, vedere [Install the Azure Information Protection Unified Labeling client for users](clientv2-admin-guide-install.md).  

Usare le sezioni seguenti per informazioni sull'installazione del client. 

### <a name="installation-checks-and-troubleshooting"></a>Controlli per l'installazione e risoluzione dei problemi

Dopo aver installato il client, usare l'opzione **Guida e commenti** per aprire la finestra di dialogo **Microsoft Azure Information Protection**:

- Da un'applicazione di Office: Nella scheda **Home** , nel gruppo **Sensitivity** , selezionare **Sensitivity**, quindi scegliere **Guida e commenti**.

- Da Esplora file: fare clic con il pulsante destro del mouse su uno o più file o su una cartella, scegliere **Classifica e proteggi** e quindi **Guida e commenti**. 

#### <a name="help-and-feedback-section"></a>Sezione **Guida e commenti**

Per impostazione predefinita, il **collegamento altre informazioni** consente di passare al sito Web [Azure Information Protection](https://www.microsoft.com/cloud-platform/azure-information-protection) . È possibile configurare il proprio collegamento URL che passa a una pagina della Guida personalizzata come una delle impostazioni dei criteri nel portale di gestione delle etichette: Centro sicurezza e conformità di Office 365, Centro sicurezza di Microsoft 365 o Centro conformità di Microsoft 365.

Il **log di esportazione** raccoglie e collega automaticamente i file di log per il client Azure Information Protection Unified Labeling se è stato richiesto di inviarli a supporto tecnico Microsoft. Questa opzione può essere usata anche dagli utenti finali per inviare i file di log all'help desk.

Con le **Impostazioni** di reimpostazione l'utente viene disconnesso, Elimina le etichette di riservatezza attualmente scaricate e i criteri delle etichette e reimposta le impostazioni utente per il servizio Rights Management di Azure.

##### <a name="more-information-about-the-reset-settings-option"></a>Altre informazioni sull'opzione Ripristina le impostazioni

- Non è necessario essere un amministratore locale per usare questa opzione e questa azione non viene registrata nel Visualizzatore eventi. 

- A meno che i file non siano bloccati, questa azione elimina tutti i file nelle posizioni seguenti. Questi file includono i certificati client, i modelli di protezione, le etichette di riservatezza e i criteri del portale di gestione delle etichette e le credenziali utente memorizzate nella cache. I file di log del client non vengono eliminati.
    
    - %LocalAppData%\Microsoft\DRM
    
    - %LocalAppData%\Microsoft\MSIPC
    
    - %LocalAppData%\Microsoft\MSIP\Policy.msip
    
    - %LocalAppData%\Microsoft\MSIP\TokenCache

- Vengono eliminate le chiavi e le impostazioni del Registro di sistema seguenti. Se sono stati impostati valori personalizzati per queste chiavi del Registro di sistema, dopo la reimpostazione del client è necessario riconfigurarli. 
    
    Per le reti aziendali, queste impostazioni vengono in genere configurate tramite Criteri di gruppo e in questo caso vengono automaticamente riapplicate al momento dell'aggiornamento dei Criteri di gruppo nel computer. Potrebbero essere tuttavia presenti impostazioni configurate una sola volta tramite script o manualmente. In questi casi, è necessario intervenire per riconfigurare queste impostazioni. Ad esempio, è possibile che i computer eseguano un script una sola volta per configurare le impostazioni per il reindirizzamento ad Azure Information Protection, poiché si sta eseguendo la migrazione da AD RMS e nella rete è ancora presente un punto di connessione del servizio. Dopo aver reimpostato il client, il computer deve eseguire nuovamente lo script.
    
    - HKEY_CURRENT_USER\SOFTWARE\Microsoft\Office\15.0\Common\Identity
    
    - HKEY_CURRENT_USER\SOFTWARE\Microsoft\Office\14.0\Common\DRM
    
    - HKEY_CURRENT_USER\SOFTWARE\Microsoft\Office\15.0\Common\DRM
    
    - HKEY_CURRENT_USER\SOFTWARE\Microsoft\Office\16.0\Common\DRM
    
    - Settings\Software\Microsoft\MSIPC HKEY_CURRENT_USER\SOFTWARE\Classes\Local

- L'utente connesso viene disconnesso.

#### <a name="client-status-section"></a>Sezione **Stato del client**

Usare il valore di **Connessione effettuata come** per verificare se il nome utente visualizzato identifica l'account da usare per l'autenticazione di Azure Information Protection. Questo nome utente deve corrispondere a un account usato per Office 365 o Azure Active Directory. L'account deve appartenere anche a un tenant di Office 365 configurato per le etichette di riservatezza nel portale di gestione delle etichette.

Se è necessario accedere come utente diverso a quello visualizzato, vedere le istruzioni per l' [accesso come utente diverso](clientv2-admin-guide-customizations.md#sign-in-as-a-different-user) .

Usare le informazioni di **Versione** per verificare la versione del client installata. È possibile verificare se questa è la versione di rilascio più recente e le correzioni e le nuove funzionalità corrispondenti leggendo le [informazioni sulla versione](unifiedlabelingclient-version-release-history.md) per il client.

## <a name="support-for-multiple-languages"></a>Supporto di altre lingue

Il client di assegnazione unificata Azure Information Protection supporta le stesse lingue supportate da Office 365. Per un elenco di queste lingue, vedere la sezione **Office 365, Exchange Online Protection e Power BI** nella pagina [Disponibilità internazionale](https://products.office.com/business/international-availability) di Office.

Per questi linguaggi, le opzioni di menu, le finestre di dialogo e i messaggi della Azure Information Protection client Unified Labeling vengono visualizzati nella lingua dell'utente. È disponibile un singolo programma di installazione che rileva la lingua, pertanto non è necessaria alcuna configurazione aggiuntiva per installare il client di etichetta unificato Azure Information Protection per le diverse lingue. 

Tuttavia, la Azure Information Protection client di etichetta unificata attualmente non supporta lingue diverse per le etichette. Inoltre, i contrassegni visivi non vengono convertiti e non supportano più di una lingua.

## <a name="post-installation-tasks"></a>Attività post-installazione

Dopo aver installato il Azure Information Protection client di assegnazione unificata delle etichette, assicurarsi di fornire agli utenti le istruzioni per etichettare i documenti e i messaggi di posta elettronica e le linee guida per le etichette da scegliere per scenari specifici. Ad esempio:

- Istruzioni per l'utente online: [Guida dell'utente per l'assegnazione di etichette unificata Azure Information Protection](clientv2-user-guide.md)

- Scaricare un manuale dell'utente personalizzabile: [Azure Information Protection End User Adoption Guide](https://download.microsoft.com/download/7/1/2/712A280C-1C66-4EF9-8DC3-88EE43BEA3D4/Azure_Information_Protection_End_User_Adoption_Guide_EN_US.pdf) (Manuale d'uso di Azure Information Protection per utenti finali)

## <a name="upgrading-and-maintaining-the-azure-information-protection-unified-labeling-client"></a>Aggiornamento e gestione del client Azure Information Protection Unified Labeling

> [!NOTE]
> Il client Azure Information Protection Unified Labeling supporta l'aggiornamento del client di Azure Information Protection (classico), nonché l'aggiornamento da versioni precedenti del client Azure Information Protection Unified labeling.

Il team di Azure Information Protection aggiorna regolarmente il client di Azure Information Protection Unified Labeling per nuove funzionalità e correzioni. Gli annunci vengono pubblicati nel [sito Yammer](https://www.yammer.com/AskIPTeam) del team.

Se si utilizza Windows Update, il client di Azure Information Protection Unified Labeling aggiorna automaticamente la versione di disponibilità generale del client, indipendentemente dalla modalità di installazione del client. Le nuove versioni del client vengono pubblicate nel catalogo alcune settimane dopo il rilascio.

In alternativa, è possibile aggiornare manualmente il client scaricando la nuova versione dall'[Area download Microsoft](https://www.microsoft.com/en-us/download/details.aspx?id=53018). Installare quindi la nuova versione per aggiornare il client. È necessario utilizzare questo metodo per aggiornare le versioni di anteprima e se si esegue l'aggiornamento dal client di Azure Information Protection.

Se si esegue l'aggiornamento dal client di Azure Information Protection (versione classica) in Windows 7, tutte le applicazioni di Office verranno riavviate automaticamente durante l'aggiornamento del client. Questo riavvio automatico non si applica ai sistemi operativi successivi o se si esegue l'aggiornamento da una versione precedente del client di etichetta unificata.

Quando si esegue l'aggiornamento manuale, disinstallare prima la versione precedente solo se si sta modificando il metodo di installazione, ad esempio se si passa dalla versione eseguibile (EXE) del client alla versione di Windows Installer (MSI) del client, oppure se è necessario installare una versione precedente del client, ad esempio se è stata installata la versione di anteprima corrente per i test e ora è necessario tornare alla versione disponibile a livello generale corrente.

Usare la [cronologia](unifiedlabelingclient-version-release-history.md) delle versioni e i criteri di supporto per comprendere i criteri di supporto per il client Azure Information Protection Unified Labeling, le versioni attualmente supportate e le novità e le modifiche per le versioni supportate. 

## <a name="uninstalling-the-azure-information-protection-unified-labeling-client"></a>Disinstallazione del client Azure Information Protection Unified Labeling

Per disinstallare il client è possibile usare una delle opzioni seguenti:

- Usare il Pannello di controllo per disinstallare un programma: Fare clic su **Microsoft Azure Information Protection** > **Disinstalla**

- Eseguire nuovamente il file eseguibile (ad esempio, **AzInfoProtection_UL. exe**) e dalla pagina **Modifica installazione** fare clic su **Disinstalla**. 

- Eseguire l'eseguibile con **/uninstall**. ad esempio `AzInfoProtection.exe /uninstall`

## <a name="next-steps"></a>Passaggi successivi
Per installare il client, vedere [Install the Azure Information Protection Unified Labeling client for users](clientv2-admin-guide-install.md).

Se il client è già stato installato, vedere gli argomenti seguenti per altre informazioni che potrebbero essere necessarie per supportare il client:

- [Personalizzazioni](clientv2-admin-guide-customizations.md)

- [File del client e registrazione dell'utilizzo](client-admin-guide-files-and-logging.md)

- [Tipi di file supportati](client-admin-guide-file-types.md)

- [Comandi di PowerShell](client-admin-guide-powershell.md)


