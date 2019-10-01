---
title: Guida dell'amministratore client per l'assegnazione di etichette unificata Azure Information Protection
description: Istruzioni e informazioni per gli amministratori in una rete aziendale che sono responsabili della distribuzione del client Azure Information Protection Unified Labeling per Windows.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 09/26/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: v2client
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 4468ce10a79c31c4f3c3be625f84b5cbd69c74da
ms.sourcegitcommit: 1e25e7a32cc0b2a3a6c9b80575927009d8a96838
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/30/2019
ms.locfileid: "71690092"
---
# <a name="azure-information-protection-unified-labeling-client-administrator-guide"></a>Guida dell'amministratore client per l'assegnazione di etichette unificata Azure Information Protection

>*Si applica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8, Windows 7 con SP1, windows server 2019, windows server 2016, windows Server 2012 R2, windows Server 2012, windows Server 2008 R2*
>
> *Istruzioni per: [Azure Information Protection client di etichetta unificata per Windows](../faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*

Utilizzare le informazioni contenute in questa guida se si è responsabili del client Azure Information Protection Unified Labeling in una rete aziendale o se si desiderano informazioni più tecniche rispetto a quelle presenti nell' [Azure Information Protection utente client con etichetta unificata Guida](clientv2-user-guide.md). 

Esempio:

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

- Un modulo di PowerShell per individuare informazioni riservate nei file e applicare o rimuovere le etichette di classificazione e la protezione dai file. 
    
    La versione di anteprima del client include i cmdlet per installare e configurare il [Azure Information Protection scanner](../deploy-aip-scanner.md) eseguito come servizio in Windows Server. Questo servizio consente di individuare, classificare e proteggere i file negli archivi dati, ad esempio le condivisioni di rete e le librerie di SharePoint Server

- Il client Rights Management che comunica con il servizio di protezione (Azure Rights Management) per crittografare e proteggere i file.

Ad eccezione del visualizzatore, il Azure Information Protection client Unified Labeling non può essere usato con le applicazioni e i servizi che comunicano direttamente con il servizio di protezione o con Active Directory Rights Management Services.

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

Per impostazione predefinita, il **collegamento altre informazioni** consente di passare al sito Web [Azure Information Protection](https://www.microsoft.com/cloud-platform/azure-information-protection) . È possibile configurare il proprio collegamento URL che passa a una pagina della Guida personalizzata come una delle impostazioni dei criteri nel centro di gestione delle etichette: Centro sicurezza e conformità di Office 365, Centro sicurezza di Microsoft 365 o Centro conformità di Microsoft 365.

Il collegamento **segnala un problema** viene visualizzato solo se si specifica un' [impostazione avanzata](clientv2-admin-guide-customizations.md#add-report-an-issue-for-users). Quando si configura questa impostazione, si specifica un collegamento HTTP, ad esempio l'indirizzo e-mail dell'help desk. 

Il **log di esportazione** raccoglie e collega automaticamente i file di log per il client Azure Information Protection Unified Labeling se è stato richiesto di inviarli a supporto tecnico Microsoft. Questa opzione può essere usata anche dagli utenti finali per inviare i file di log all'help desk. In alternativa, è possibile usare il cmdlet [Export-AIPLogs](/powershell/module/azureinformationprotection/export-aiplogs) di PowerShell (richiede il client di anteprima).

Con le **Impostazioni** di reimpostazione l'utente viene disconnesso, Elimina le etichette di riservatezza attualmente scaricate e i criteri delle etichette e reimposta le impostazioni utente per il servizio Rights Management di Azure.

> [!NOTE]
> In caso di problemi tecnici con il client, vedere [Opzioni di supporto e risorse della community](../information-support.md#support-options-and-community-resources).

##### <a name="more-information-about-the-reset-settings-option"></a>Altre informazioni sull'opzione Ripristina le impostazioni

- Non è necessario essere un amministratore locale per usare questa opzione e questa azione non viene registrata nel Visualizzatore eventi. 

- A meno che i file non siano bloccati, questa azione elimina tutti i file nelle posizioni seguenti. Questi file includono i certificati client, i modelli di protezione, le etichette di riservatezza e i criteri dal centro di gestione delle etichette e le credenziali utente memorizzate nella cache. I file di log del client non vengono eliminati.
    
    - %LocalAppData%\Microsoft\DRM
    
    - %LocalAppData%\Microsoft\MSIPC
    
    - %LocalAppData%\Microsoft\MSIP\mip @ no__t-0 *\<processname @ no__t-3*\mip
    
    - %LocalAppData%\Microsoft\MSIP\AppDetails
    
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

Tuttavia, i nomi di etichetta e le descrizioni specificati non vengono convertiti automaticamente quando si configurano le etichette nel centro di etichette. Per consentire agli utenti di visualizzare le etichette nella lingua preferita, fornire le proprie traduzioni e configurarle per le etichette usando usando Office 365 Sicurezza e conformità PowerShell e il parametro *LocaleSettings* per [set-label](https://docs.microsoft.com/powershell/module/exchange/policy-and-compliance/set-label?view=exchange-ps). I contrassegni visivi non vengono convertiti e non supportano più di una lingua.

## <a name="post-installation-tasks"></a>Attività post-installazione

Dopo aver installato il Azure Information Protection client di assegnazione unificata delle etichette, assicurarsi di fornire agli utenti le istruzioni per etichettare i documenti e i messaggi di posta elettronica e le linee guida per le etichette da scegliere per scenari specifici. Esempio:

- Istruzioni per l'utente online: [Guida dell'utente per l'assegnazione di etichette unificata Azure Information Protection](clientv2-user-guide.md)

- Scaricare un manuale dell'utente personalizzabile: [Azure Information Protection End User Adoption Guide](https://download.microsoft.com/download/7/1/2/712A280C-1C66-4EF9-8DC3-88EE43BEA3D4/Azure_Information_Protection_End_User_Adoption_Guide_EN_US.pdf) (Manuale d'uso di Azure Information Protection per utenti finali)

## <a name="installing-the-azure-information-protection-scanner"></a>Installazione dello scanner Azure Information Protection

La versione corrente dello scanner per il client Unified Labeling è in anteprima per i test. Durante questa anteprima, installare la versione di anteprima corrente del client Unified Labeling dall' [area download Microsoft](https://www.microsoft.com/en-us/download/details.aspx?id=53018).

Se si installa lo scanner per la prima volta in un computer, scaricare e installare il client e seguire le istruzioni riportate in [distribuzione di Azure Information Protection scanner per classificare e proteggere automaticamente i file](../deploy-aip-scanner.md).

Se si sta aggiornando lo scanner dal client di Azure Information Protection (classico), vedere la sezione [aggiornamento dello scanner Azure Information Protection](#upgrading-the-azure-information-protection-scanner) per istruzioni.

## <a name="upgrading-and-maintaining-the-azure-information-protection-unified-labeling-client"></a>Aggiornamento e gestione del client Azure Information Protection Unified Labeling

> [!NOTE]
> Il client Azure Information Protection Unified Labeling supporta l'aggiornamento del client di Azure Information Protection (classico), nonché l'aggiornamento da versioni precedenti del client Azure Information Protection Unified labeling.

Il team di Azure Information Protection aggiorna regolarmente il client di Azure Information Protection Unified Labeling per nuove funzionalità e correzioni. Gli annunci vengono pubblicati nel [sito Yammer](https://www.yammer.com/AskIPTeam) del team.

Se si utilizza Windows Update, il client di Azure Information Protection Unified Labeling aggiorna automaticamente la versione di disponibilità generale del client, indipendentemente dalla modalità di installazione del client. Le nuove versioni del client vengono pubblicate nel catalogo alcune settimane dopo il rilascio.

In alternativa, è possibile aggiornare manualmente il client scaricando la nuova versione dall'[Area download Microsoft](https://www.microsoft.com/en-us/download/details.aspx?id=53018). Installare quindi la nuova versione per aggiornare il client. È necessario utilizzare questo metodo per aggiornare le versioni di anteprima e se si esegue l'aggiornamento dal client di Azure Information Protection.

Se si esegue l'aggiornamento dal client di Azure Information Protection (versione classica) in Windows 7, tutte le applicazioni di Office verranno riavviate automaticamente durante l'aggiornamento del client. Questo riavvio automatico non si applica ai sistemi operativi successivi o se si esegue l'aggiornamento da una versione precedente del client di etichetta unificata.

Quando si esegue l'aggiornamento manuale, disinstallare prima la versione precedente solo se si sta modificando il metodo di installazione, ad esempio se si passa dalla versione eseguibile (EXE) del client alla versione di Windows Installer (MSI) del client, oppure se è necessario installare una versione precedente del client, ad esempio se è stata installata la versione di anteprima corrente per i test e ora è necessario tornare alla versione disponibile a livello generale corrente.

Usare la [cronologia](unifiedlabelingclient-version-release-history.md) delle versioni e i criteri di supporto per comprendere i criteri di supporto per il client Azure Information Protection Unified Labeling, le versioni attualmente supportate e le novità e le modifiche per le versioni supportate. 

### <a name="upgrading-the-azure-information-protection-scanner"></a>Aggiornamento dello scanner di Azure Information Protection

Se attualmente si usa lo scanner Azure Information Protection dal client di Azure Information Protection (versione classica), è possibile aggiornarlo per usare i tipi di informazioni riservate e le etichette di riservatezza pubblicate dalla sicurezza di Office 365 & Centro di conformità (oppure il Centro sicurezza Microsoft 365 o il centro di conformità Microsoft 365).

#### <a name="to-upgrade-the-scanner-to-the-preview-version"></a>Per aggiornare lo scanner alla versione di anteprima

Le modalità di aggiornamento dello scanner dipendono dalla versione del client di Azure Information Protection (classica) attualmente in esecuzione:

- [Aggiornamento dalla versione 1.48.204.0 e versioni successive](#upgrade-from-the-azure-information-protection-client-classic-version-1482040-and-later-versions-of-this-client)

- [Aggiornamento da versioni precedenti a 1.48.204.0](#upgrade-from-the-azure-information-protection-client-classic-versions-earlier-than-1482040)

Si noti che, a differenza dello scanner dal client di Azure Information Protection (classico), questa versione di anteprima dello scanner per il client unificato non supporta l'esecuzione in un computer disconnesso.

Con l'aggiornamento viene creato un nuovo database denominato **AIPScannerUL_ @ no__t-1profile_name >** e il database dello scanner precedente viene mantenuto nel caso in cui sia necessario per la versione precedente. Quando si è certi che non è necessario il database scanner precedente, è possibile eliminarlo. Poiché l'aggiornamento crea un nuovo database, lo scanner ripete l'analisi di tutti i file la prima volta che viene eseguito.

##### <a name="upgrade-from-the-azure-information-protection-client-classic-version-1482040-and-later-versions-of-this-client"></a>Aggiornamento dal client di Azure Information Protection (versione classica) 1.48.204.0 e versioni successive di questo client

1. Nel computer dello scanner arrestare il servizio dello scanner **Azure Information Protection Scanner**.

2. Eseguire l'aggiornamento al client di Azure Information Protection Unified Labeling scaricando e installando la versione di anteprima del client Unified Labeling dall' [area download Microsoft](https://www.microsoft.com/en-us/download/details.aspx?id=53018).

3. In una sessione di PowerShell eseguire il comando Update-AIPScanner con il profilo dello scanner. Ad esempio: `Update-AIPScanner –Profile Europe`.
    
    Con questo passaggio viene creato un nuovo database denominato **AIPScannerUL_ @ no__t-1profile_name >**

4. Riavviare il servizio dello scanner di Azure Information Protection **Scanner Azure Information Protection**.

È ora possibile usare le altre istruzioni riportate in [distribuzione di Azure Information Protection scanner per classificare e proteggere automaticamente i file](../deploy-aip-scanner.md), omettendo il passaggio per installare lo scanner. Poiché lo scanner è già installato, non c'è alcun motivo per installarlo di nuovo.

##### <a name="upgrade-from-the-azure-information-protection-client-classic-versions-earlier-than-1482040"></a>Eseguire l'aggiornamento dalla versione client di Azure Information Protection (classica) precedente a 1.48.204.0

> [!IMPORTANT]
> Per un percorso di aggiornamento uniforme, non installare il Azure Information Protection client Unified Labeling nel computer che esegue lo scanner come primo passaggio per aggiornare lo scanner. Usare invece le istruzioni di aggiornamento seguenti.

A partire dalla versione 1.48.204.0, lo scanner ottiene le impostazioni di configurazione dalla portale di Azure, usando un profilo di configurazione. Con l'aggiornamento dello scanner è necessario indicare allo scanner di usare questa configurazione online e per il client Unified Labeling, la configurazione offline per lo scanner non è supportata.

1. Usare il portale di Azure per creare un nuovo profilo di scanner che include le impostazioni per lo scanner e i repository di dati con le eventuali impostazioni necessarie. Per informazioni su questo passaggio, vedere la sezione [configurare lo scanner nella sezione portale di Azure](../deploy-aip-scanner.md#configure-the-scanner-in-the-azure-portal) dalle istruzioni per la distribuzione dello scanner.

2. Nel computer dello scanner arrestare il servizio dello scanner **Azure Information Protection Scanner**.

3. Eseguire l'aggiornamento al client di Azure Information Protection Unified Labeling scaricando e installando la versione di anteprima del client Unified Labeling dall' [area download Microsoft](https://www.microsoft.com/en-us/download/details.aspx?id=53018).

4. In una sessione di PowerShell eseguire il comando Update-AIPScanner con lo stesso nome di profilo specificato nel passaggio 1. Ad esempio: `Update-AIPScanner –Profile Europe`

5. Riavviare il servizio dello scanner di Azure Information Protection **Scanner Azure Information Protection**.

È ora possibile usare le altre istruzioni riportate in [distribuzione di Azure Information Protection scanner per classificare e proteggere automaticamente i file](../deploy-aip-scanner.md), omettendo il passaggio per installare lo scanner. Poiché lo scanner è già installato, non c'è alcun motivo per installarlo di nuovo.

###### <a name="upgrading-in-a-different-order-to-the-recommended-steps"></a>Aggiornamento in un ordine diverso rispetto alla procedura consigliata

Quando si esegue l'aggiornamento da una versione precedente a 1.48.204.0 e non si configura lo scanner nella portale di Azure prima di eseguire il comando Update-AIPScanner, non è presente un nome di profilo per specificare che identifichi le impostazioni di configurazione dello scanner per l'aggiornamento processo. 

In questo scenario, quando si configura lo scanner nel portale di Azure, è necessario specificare esattamente lo stesso nome di profilo usato quando è stato eseguito il comando Update-AIPScanner. Se il nome non corrisponde, lo scanner non verrà configurato per le impostazioni. 

> [!TIP]
> Per identificare gli scanner con questo errore di configurazione, usare il pannello **Azure Information Protection - Nodi** nel portale di Azure.
>  
> Per gli scanner con connettività Internet, visualizzano il nome del computer con il numero di versione GA del client Azure Information Protection, ma senza nome profilo. Solo per gli scanner con numero di versione 1.41.51.0 non dovrebbe essere visualizzato il nome di profilo in questo pannello. 

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


