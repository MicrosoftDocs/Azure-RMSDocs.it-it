---
title: Guida dell'amministratore del client Azure Information Protection
description: Istruzioni e informazioni per gli amministratori in una rete aziendale che sono responsabili della distribuzione del client Azure Information Protection per Windows.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 06/20/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 33a5982f-7125-4031-92c2-05daf760ced1
ms.reviewer: eymanor
ms.suite: ems
ms.openlocfilehash: d353eac9dd13b90f02a296a40f8aa1b6e3269d52
ms.sourcegitcommit: 478081129d9ea8382ce08fae0bae1a08cab23893
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/20/2019
ms.locfileid: "67298292"
---
# <a name="azure-information-protection-client-administrator-guide"></a>Guida dell'amministratore del client Azure Information Protection

>*Si applica a: Active Directory Rights Management Services, [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8, Windows 7 con SP1, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2*
>
> *Istruzioni per: [Client Azure Information Protection per Windows](../faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*

Usare le informazioni di questa guida se si è responsabili del client Azure Information Protection in una rete aziendale o se sono necessarie maggiori informazioni rispetto a quelle disponibili nella [Guida per l'utente del client Azure Information Protection](client-user-guide.md). 

Ad esempio:

- Comprendere i diversi componenti di questo client e se è necessario installarlo

- Come installare il client per gli utenti, con informazioni su prerequisiti, opzioni e parametri di installazione e controlli di verifica

- Come gestire le configurazioni personalizzate che richiedono spesso la modifica del Registro di sistema

- Individuare i file e i log di utilizzo del client

- Identificare i tipi di file supportati dal client

- Configurare e usare il sito di rilevamento dei documenti per gli utenti

- Usare il client con PowerShell per il controllo dalla riga di comando

**In caso di domande su argomenti non trattati in questa documentazione**, visitare il [sito di Yammer su Azure Information Protection](https://www.yammer.com/AskIPTeam). 

## <a name="technical-overview-of-the-azure-information-protection-client"></a>Panoramica tecnica sul client Azure Information Protection

Il client Azure Information Protection include gli elementi seguenti:

- Un componente aggiuntivo di Office che installa la barra di Azure Information Protection per consentire agli utenti di selezionare le etichette di classificazione e un pulsante **Proteggi** sulla barra multifunzione per offrire altre opzioni. Per Outlook, è disponibile anche un pulsante **Non inoltrare** per la barra multifunzione.

- Esplora file, opzioni tramite clic con il pulsante destro del mouse per l'applicazione di etichette di classificazione e della protezione ai file.

- Un visualizzatore per visualizzare file protetti quando un'applicazione nativa non è in grado di aprirli.

- Un modulo di PowerShell per applicare e rimuovere etichette di classificazione e la protezione dei file. 
    
    Questo modulo include i cmdlet per installare e configurare lo [scanner Azure Information Protection](../deploy-aip-scanner.md) eseguito come servizio in Windows Server. Questo servizio consente di individuare, classificare e proteggere i file in archivi dati come le condivisioni di rete e le raccolte di SharePoint Server.

- Il client Rights Management che comunica con Azure Rights Management (Azure RMS) o Active Directory Rights Management Services (AD RMS).

Il client Azure Information Protection si integra al meglio con i servizi di Azure, Azure Information Protection e il relativo servizio di protezione dei dati, Azure Rights Management. Tuttavia, con alcune limitazioni, il client Azure Information Protection si integra anche con la versione locale di Rights Management, AD RMS. Per un confronto completo delle funzionalità supportate da Azure Information Protection e AD RMS, vedere [Confronto tra Azure Information Protection e AD RMS](../compare-on-premise.md). 

Se si usa AD RMS e si vuole passare ad Azure Information Protection, vedere [Migrazione da AD RMS ad Azure Information Protection](../migrate-from-ad-rms-to-azure-rms.md).


## <a name="should-you-deploy-the-azure-information-protection-client"></a>È consigliabile distribuire il client Azure Information Protection?

Distribuire il client Azure Information Protection se non si usa [etichette di riservatezza nel centro di conformità e sicurezza di Office 365](https://docs.microsoft.com/Office365/SecurityCompliance/sensitivity-labels) ma usando invece, le etichette di Azure Information Protection scaricati da Azure e gli eventuali di quanto segue si applica a:

- Si vuole classificare (e, facoltativamente, proteggere) documenti e messaggi di posta elettronica selezionando etichette dalle applicazioni di Office (Word, Excel, PowerPoint, Outlook).

- Si vogliono classificare (e, facoltativamente, proteggere) file tramite Esplora file, che supporta altri tipi di file rispetto a quelli supportati da Office, la selezione multipla e le cartelle.

- Si vuole eseguire script che classifichino (e, facoltativamente, proteggano) documenti tramite comandi di PowerShell.

- Si vuole eseguire un servizio che individua, classifica e, facoltativamente, protegge i file archiviati in locale.

- Si vuole visualizzare documenti protetti quando non è installata un'applicazione nativa per visualizzare i file o questa applicazione non è in grado di aprire i documenti.

- Si vuole semplicemente proteggere i file usando Esplora file o i comandi di PowerShell.

- Si vuole che utenti e amministratori siano in grado di monitorare e revocare documenti protetti.

- Si vuole rimuovere la crittografia da file e contenitori (rimozione della protezione) in blocco per scopi di ripristino dei dati.

- Si usa Office 2010 e si vuole proteggere documenti e messaggi di posta elettronica tramite il servizio Azure Rights Management.

Esempio che visualizza il componente aggiuntivo client Azure Information Protection per un'applicazione di Office con le etichette di classificazione per l'organizzazione e il nuovo pulsante **Proteggi** sulla barra multifunzione:

![Barra Azure Information Protection con criterio predefinito](../media/word2016-calloutsv2.png)

## <a name="installing-and-supporting-the-azure-information-protection-client"></a>Installazione e supporto del client Azure Information Protection

È possibile installare il client Azure Information Protection tramite un file eseguibile o un file di Windows Installer. Per altre informazioni sulle singole opzioni e per le istruzioni, vedere [Installare il client Azure Information Protection per gli utenti](client-admin-guide-install.md) nella guida dell'amministratore.  

Usare le sezioni seguenti per informazioni sull'installazione del client. 

### <a name="installation-checks-and-troubleshooting"></a>Controlli per l'installazione e risoluzione dei problemi

Dopo aver installato il client, usare l'opzione **Guida e commenti** per aprire la finestra di dialogo **Microsoft Azure Information Protection**:

- Da un'applicazione di Office: nel gruppo **Protezione** della scheda **Home** fare clic su **Proteggi** e quindi su **Guida e commenti**.

- Da Esplora file: fare clic con il pulsante destro del mouse su uno o più file o su una cartella, scegliere **Classifica e proteggi** e quindi **Guida e commenti**. 

#### <a name="help-and-feedback-section"></a>Sezione **Guida e commenti**

Il collegamento **Altre informazioni** reindirizza per impostazione predefinita al sito Web [Azure Information Protection](https://www.microsoft.com/cloud-platform/azure-information-protection), ma è possibile configurarlo con un URL personalizzato nelle [impostazioni dei criteri](../configure-policy-settings.md) di Azure Information Protection.

Il collegamento **Segnala un problema** viene visualizzato solo se si specifica un'[impostazione client avanzata](client-admin-guide-customizations.md#add-report-an-issue-for-users). Quando si configura questa impostazione, si specifica un collegamento HTTP, ad esempio l'indirizzo e-mail dell'help desk.

L'opzione **Esporta log** consente di raccogliere e allegare automaticamente i file di log relativi al client Azure Information Protection se ne è stato chiesto l'invio al supporto tecnico Microsoft. Questa opzione può essere usata anche dagli utenti finali per inviare i file di log all'help desk.

L'opzione **Ripristina le impostazioni** consente di disconnettere l'utente, eliminare i criteri di Azure Information Protection scaricati e ripristinare le impostazioni utente per il servizio Azure Rights Management.

##### <a name="more-information-about-the-reset-settings-option"></a>Altre informazioni sull'opzione Ripristina le impostazioni

- Non è necessario essere un amministratore locale per usare questa opzione e questa azione non viene registrata nel Visualizzatore eventi. 

- A meno che i file non siano bloccati, questa azione elimina tutti i file nelle posizioni seguenti. Questi file includono i certificati client, i modelli di Rights Management, i criteri di Azure Information Protection e le credenziali utente memorizzate nella cache. I file di log del client non vengono eliminati.
    
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
    
    - HKEY_CURRENT_USER\SOFTWARE\Classes\Local Settings\Software\Microsoft\MSIPC    

- L'utente connesso viene disconnesso.

#### <a name="client-status-section"></a>Sezione **Stato del client**

Usare il valore di **Connessione effettuata come** per verificare se il nome utente visualizzato identifica l'account da usare per l'autenticazione di Azure Information Protection. Questo nome utente deve corrispondere a un account usato per Office 365 o Azure Active Directory. L'account deve anche appartenere a un tenant configurato per Azure Information Protection.

Se è necessario accedere con un nome utente diverso da quello visualizzato, vedere la personalizzazione in [Accedere come utente diverso](client-admin-guide-customizations.md#sign-in-as-a-different-user).

Il valore **Ultima connessione** indica quando il client si è connesso per l'ultima volta al servizio Azure Information Protection dell'organizzazione. È possibile usare queste informazioni con l'impostazione **Il criterio di Information Protection è stato installato il giorno** per verificare la data e ora dell'installazione o dell'ultimo aggiornamento dei criteri di Azure Information Protection. Quando si connette al servizio, il client scarica automaticamente i criteri più recenti se rileva variazioni rispetto a quelli correnti e anche ogni 24 ore. Se si sono apportate modifiche ai criteri dopo l'ora visualizzata, chiudere e riaprire l'applicazione di Office.

Se viene visualizzato il messaggio **Questo client non ha la licenza per Office Professional Plus**: il client Azure Information Protection ha rilevato che l'edizione installata di Office non supporta l'applicazione della protezione di Rights Management. Quando viene effettuato questo rilevamento, le etichette che applicano la protezione non vengono visualizzate sulla barra di Azure Information Protection.

Usare le informazioni di **Versione** per verificare la versione del client installata. È possibile controllare se la versione installata è quella più recente e verificare le nuove funzionalità e le correzioni di tale versione facendo clic sul collegamento **Novità** che consente di accedere alla [cronologia delle versioni](client-version-release-history.md) del client.

## <a name="support-for-multiple-languages"></a>Supporto di altre lingue

Il client Azure Information Protection supporta le stesse lingue supportate da Office 365. Per un elenco di queste lingue, vedere la sezione **Office 365, Exchange Online Protection e Power BI** nella pagina [Disponibilità internazionale](https://products.office.com/business/international-availability) di Office.

Per queste lingue, le opzioni di menu, le finestre di dialogo e i messaggi del client Azure Information Protection vengono visualizzati nella lingua dell'utente. La lingua viene rilevata da un singolo programma di installazione, quindi non sono necessarie operazioni aggiuntive per installare il client Azure Information Protection in lingue diverse. 

Tuttavia, i nomi e le descrizioni delle etichette specificati non vengono automaticamente tradotti quando si configurano le etichette nei criteri di Azure Information Protection. A partire dal 30 agosto 2017 il [criterio predefinito](../configure-policy-default.md) corrente include il supporto per alcune lingue. Per fare in modo che gli utenti vedano le etichette nella lingua preferita, specificare le proprie traduzioni e configurare i criteri di Azure Information Protection per l'uso di tali traduzioni. Per altre informazioni, vedere [Come configurare etichette per lingue diverse in Azure Information Protection](../configure-policy-languages.md). I contrassegni visivi non vengono convertiti e non supportano più di una lingua.

## <a name="post-installation-tasks"></a>Attività post-installazione

Dopo aver installato il client Azure Information Protection, accertarsi di fornire agli utenti istruzioni per etichettare i documenti e i messaggi di posta elettronica, oltre a linee guida per le etichette da scegliere per scenari specifici. Ad esempio:

- Istruzioni per l'utente online: [Guida per l'utente di Azure Information Protection](client-user-guide.md)

- Scaricare un manuale dell'utente personalizzabile: [Azure Information Protection End User Adoption Guide](https://download.microsoft.com/download/7/1/2/712A280C-1C66-4EF9-8DC3-88EE43BEA3D4/Azure_Information_Protection_End_User_Adoption_Guide_EN_US.pdf) (Manuale d'uso di Azure Information Protection per utenti finali)

## <a name="upgrading-and-maintaining-the-azure-information-protection-client"></a>Aggiornamento e gestione del client Azure Information Protection

Il team di Azure Information Protection aggiorna regolarmente il client Azure Information Protection con correzioni e nuove funzionalità. Gli annunci vengono pubblicati nel [sito Yammer](https://www.yammer.com/AskIPTeam) del team.

Se si usa Windows Update, il client Azure Information Protection aggiorna automaticamente la versione del client disponibile a livello generale, indipendentemente dal modo in cui è stato installato il client. Le nuove versioni del client vengono pubblicate nel catalogo alcune settimane dopo il rilascio.

In alternativa, è possibile aggiornare manualmente il client scaricando la nuova versione dall'[Area download Microsoft](https://www.microsoft.com/en-us/download/details.aspx?id=53018). Installare quindi la nuova versione per aggiornare il client. È necessario usare questo metodo per aggiornare le versioni di anteprima.

Quando si esegue l'aggiornamento manuale, disinstallare prima la versione precedente solo se si sta modificando il metodo di installazione, ad esempio se si passa dalla versione eseguibile (EXE) del client alla versione di Windows Installer (MSI) del client, oppure se è necessario installare una versione precedente del client, ad esempio se è stata installata la versione di anteprima corrente per i test e ora è necessario tornare alla versione disponibile a livello generale corrente.

Fare riferimento a [cronologia delle versioni e criteri per il supporto](client-version-release-history.md) per comprendere i criteri di supporto per il client Azure Information Protection, le versioni attualmente supportate e le novità e le modifiche per le versioni supportate. 

### <a name="upgrading-the-azure-information-protection-scanner"></a>Aggiornamento dello scanner di Azure Information Protection

Usare le istruzioni seguenti per aggiornare lo scanner da una versione con disponibilità generale meno recente 1.48.204.0 alla versione corrente dello scanner.

#### <a name="to-upgrade-the-scanner-to-the-current-version"></a>Per eseguire l'aggiornamento alla versione corrente dello scanner

> [!IMPORTANT]
> Per un percorso di aggiornamento smooth, non installare il client Azure Information Protection in computer che esegue lo scanner come primo passaggio per aggiornare lo scanner. Usare invece le istruzioni di aggiornamento seguenti.

Partire dalla versione 1.48.204.0, il processo di aggiornamento da versioni precedenti automaticamente le modifiche apportate allo scanner Ottiene le impostazioni di configurazione dal portale di Azure. Viene inoltre aggiornato lo schema per il database di configurazione dello scanner e questo database viene anche rinominato da AzInfoProtection:

- Se non si specifica il proprio nome di profilo, il database di configurazione viene rinominato **AIPScanner_\<nome_computer>** . 

- Se si specifica il proprio nome di profilo, il database di configurazione viene rinominato **AIPScanner_\<nome_profilo>** .

Sebbene sia possibile aggiornare lo scanner in un ordine diverso, è consigliabile usare la procedura seguente:

1. Usare il portale di Azure per creare un nuovo profilo di scanner che include le impostazioni per lo scanner e i repository di dati con le eventuali impostazioni necessarie. Per altre informazioni su questo passaggio, vedere la [configurare lo scanner nel portale di Azure](../deploy-aip-scanner.md#configure-the-scanner-in-the-azure-portal) sezione from le istruzioni per la distribuzione dello scanner.
    
    Se il computer che esegue lo scanner è disconnesso da Internet, è comunque necessario eseguire questo passaggio. Quindi, dal portale di Azure, usare l'opzione **Esporta** per esportare il profilo dello scanner in un file.

2. Nel computer dello scanner arrestare il servizio dello scanner **Azure Information Protection Scanner**.

3. Aggiornare il client Azure Information Protection installando la versione di disponibilità generale (GA) corrente dal [Microsoft Download Center](https://www.microsoft.com/en-us/download/details.aspx?id=53018).

4. In una sessione di PowerShell eseguire il comando Update-AIPScanner con lo stesso nome di profilo specificato nel passaggio 1. ad esempio `Update-AIPScanner –Profile Europe`

5. Solo se lo scanner è in esecuzione in un computer disconnesso: A questo punto eseguire [Import-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Import-AIPScannerConfiguration) e specificare il file che contiene le impostazioni esportate.

6. Riavviare il servizio dello scanner di Azure Information Protection **Scanner Azure Information Protection**.

È ora possibile usare il resto delle istruzioni in [distribuzione dello scanner di Azure Information Protection per classificare e proteggere i file automaticamente](../deploy-aip-scanner.md), omettere il passaggio per installare lo scanner. Poiché lo scanner è già installato, non è necessario eseguire nuovamente l'installazione.

##### <a name="upgrading-in-a-different-order-to-the-recommended-steps"></a>Aggiornamento in un ordine diverso rispetto alla procedura consigliata

Se non si configura lo scanner nel portale di Azure prima di eseguire il comando Update-AIPScanner, non sarà disponibile un nome di profilo da specificare che identifica le impostazioni di configurazione dello scanner per il processo di aggiornamento. 

In questo scenario, quando si configura lo scanner nel portale di Azure, è necessario specificare esattamente lo stesso nome di profilo usato quando è stato eseguito il comando Update-AIPScanner. Se il nome non corrisponde, lo scanner non verrà configurato per le impostazioni. 

> [!TIP]
> Per identificare gli scanner con questo errore di configurazione, usare il pannello **Azure Information Protection - Nodi** nel portale di Azure.
>  
> Per gli scanner che hanno la connettività Internet, verranno inoltre visualizzati il nome del computer con il numero di versione disponibile a livello generale del client Azure Information Protection, ma nessun nome di profilo. Solo per gli scanner con numero di versione 1.41.51.0 non dovrebbe essere visualizzato il nome di profilo in questo pannello. 

Se non è stato specificato un nome di profilo quando è stato eseguito il comando Update-AIPScanner, il nome del computer viene usato per creare automaticamente il nome del profilo per lo scanner.

#### <a name="moving-the-scanner-configuration-database-to-a-different-sql-server-instance"></a>Spostamento del database di configurazione dello scanner in un'istanza diversa di SQL Server

Nella versione corrente disponibile a livello generale, è un problema noto, se si prova a spostare il database di configurazione dello scanner in una nuova istanza di SQL Server dopo aver eseguito il comando Aggiorna.

Se si sa che si desidera spostare il database di configurazione dello scanner per la versione disponibile a livello generale, eseguire le operazioni seguenti:

1. Disinstallare lo scanner tramite [Uninstall-AIPScanner](/powershell/module/azureinformationprotection/Uninstall-AIPScanner).

2. Se non sono ancora aggiornati alla versione disponibile a livello generale corrente del client Azure Information Protection, aggiornare il client a questo punto.

3. Installare lo scanner usando [Install-AIPScanner](/powershell/module/azureinformationprotection/Install-AIPScanner), specificando la nuova istanza di SQL Server e il nome del profilo.

4. Facoltativo: se non si vuole che lo scanner ripeta l'analisi di tutti i file, esportare la tabella ScannerFiles e importarla nel nuovo database.

## <a name="uninstalling-the-azure-information-protection-client"></a>Disinstallazione del client Azure Information Protection

Per disinstallare il client è possibile usare una delle opzioni seguenti:

- Usare il Pannello di controllo per disinstallare un programma: Fare clic su **Microsoft Azure Information Protection** > **Disinstalla**

- Rieseguire l'eseguibile, ad esempio **AzInfoProtection.exe**, e fare clic su **Disinstalla** nella pagina **Modifica installazione**. 

- Eseguire l'eseguibile con **/uninstall**. ad esempio `AzInfoProtection.exe /uninstall`

## <a name="next-steps"></a>Passaggi successivi
Per installare il client, vedere [Installare il client Azure Information Protection per gli utenti](client-admin-guide-install.md).

Se il client è già stato installato, vedere gli argomenti seguenti per altre informazioni che potrebbero essere necessarie per supportare il client:

- [Personalizzazioni](client-admin-guide-customizations.md)

- [File del client e registrazione dell'utilizzo](client-admin-guide-files-and-logging.md)

- [Rilevamento dei documenti](client-admin-guide-document-tracking.md)

- [Tipi di file supportati](client-admin-guide-file-types.md)

- [Comandi di PowerShell](client-admin-guide-powershell.md)
