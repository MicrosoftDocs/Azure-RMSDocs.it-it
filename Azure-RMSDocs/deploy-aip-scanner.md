---
title: Distribuire lo scanner Azure Information Protection - AIP
description: Istruzioni per installare, configurare ed eseguire la versione di disponibilità generale corrente dello scanner Azure Information Protection per individuare, classificare e proteggere i file negli archivi dati.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 04/24/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.reviewer: demizets
ms.suite: ems
ms.openlocfilehash: 75ea97484b226617c33f985a40035e3b641434c5
ms.sourcegitcommit: fff4c155c52c9ff20bc4931d5ac20c3ea6e2ff9e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/24/2019
ms.locfileid: "62773702"
---
# <a name="deploying-the-azure-information-protection-scanner-to-automatically-classify-and-protect-files"></a>Distribuzione dello scanner di Azure Information Protection per classificare e proteggere automaticamente i file

>*Si applica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows Server 2016, Windows Server 2012 R2*
>
> *Istruzioni per: [Client Azure Information Protection per Windows](faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*

> [!NOTE]
> Questo articolo riguarda la versione disponibile a livello generale corrente dello scanner di Azure Information Protection.
> 
> Per eseguire l'aggiornamento da una versione con disponibilità generale dello scanner antecedente 1.48.204.0, vedere [l'aggiornamento lo scanner Azure Information Protection](./rms-client/client-admin-guide.md#upgrading-the-azure-information-protection-scanner). È quindi possibile usare le istruzioni riportate in questa pagina, omettendo il passaggio per installare lo scanner.
> 
> Se non si è pronti per eseguire l'aggiornamento da una versione precedente, vedere [distribuzione di versioni precedenti dello scanner Azure Information Protection per classificare e proteggere i file automaticamente](deploy-aip-scanner-previousversions.md).


Di seguito vengono illustrate le caratteristiche dello scanner di Azure Information Protection e le relative procedure per installarlo, configurarlo ed eseguirlo.

Questo scanner viene eseguito come servizio in Windows Server e consente di individuare, classificare e proteggere i file negli archivi dati seguenti:

- Cartelle locali nel computer Windows Server che esegue lo scanner.

- Percorsi UNC delle condivisioni di rete che usano il protocollo SMB (Server Message Block).

- Siti e librerie per SharePoint Server 2016 e SharePoint Server 2013. SharePoint 2010 è supportato anche per i clienti che dispongono del [supporto "Extended" per la versione corrente di SharePoint](https://support.microsoft.com/lifecycle/search?alpha=SharePoint%20Server%202010).

Per analizzare ed etichettare i file nei repository cloud, usare [Cloud App Security](https://docs.microsoft.com/cloud-app-security/) invece dello scanner.

## <a name="overview-of-the-azure-information-protection-scanner"></a>Panoramica dello scanner di Azure Information Protection

Dopo aver configurato i [criteri di Azure Information Protection](configure-policy.md) per le etichette che applicano la classificazione automatica, è possibile etichettare i file rilevati dallo scanner. Le etichette applicano la classificazione e, facoltativamente, applicano o rimuovono la protezione:

![Panoramica dell'architettura dello scanner di Azure Information Protection](./media/infoprotect-scanner.png)

Lo scanner può controllare tutti i file indicizzabili da Windows, tramite IFilter installati nel computer. In seguito, per stabilire se i file devono essere etichettati, lo scanner usa il rilevamento di modelli e di tipi di dati sensibili della prevenzione della perdita di dati (DLP) predefiniti in Office 365 o i modelli regex di Office 365. Poiché usa il client di Azure Information Protection, lo scanner è in grado di classificare e proteggere gli stessi [tipi di file](./rms-client/client-admin-guide-file-types.md).

È possibile eseguire lo scanner solo in modalità di individuazione, in cui si usano i report per verificare che cosa accadrebbe se i file fossero etichettati. Oppure è possibile eseguire lo scanner per applicare automaticamente le etichette. È anche possibile eseguire lo scanner per individuare i file che contengono tipi di informazioni riservate, senza configurare le etichette per le condizioni per l'applicazione della classificazione automatica.

Si noti che lo scanner non individua e non applica etichette in tempo reale. Effettua sistematicamente una ricerca per indicizzazione nei file presenti negli archivi dati specificati ed è possibile configurare questo ciclo in modo da eseguirlo una o più volte.

È possibile specificare quali tipi di file analizzare o escludere dall'analisi, definendo un elenco di tipi di file come parte della configurazione dello scanner.


## <a name="prerequisites-for-the-azure-information-protection-scanner"></a>Prerequisiti per lo scanner di Azure Information Protection
Prima di installare lo scanner di Azure Information Protection, verificare che i requisiti seguenti siano soddisfatti.

|Requisito|Altre informazioni|
|---------------|--------------------|
|Computer Windows Server per eseguire il servizio scanner:<br /><br />- 4 processori core<br /><br />- 8 GB di RAM<br /><br />- 10 GB di spazio libero (media) per i file temporanei|Windows Server 2016 o Windows Server 2012 R2. <br /><br />Nota: per scopi di test o valutazione in un ambiente non di produzione, è possibile usare un sistema operativo client Windows [supportato dal client di Azure Information Protection](requirements.md#client-devices).<br /><br />Il computer può essere un computer fisico o virtuale con una connessione di rete veloce e affidabile agli archivi dati da analizzare.<br /><br /> Lo scanner richiede spazio su disco sufficiente a creare i file temporanei per ogni file analizzato, quattro file per core. Lo spazio su disco consigliato di 10 GB consente a 4 processori core di analizzare 16 file, ognuno con una dimensione di 625 MB. <br /><br />Se la connettività Internet non è possibile a causa dei criteri dell'organizzazione, vedere la sezione [Distribuzione dello scanner con configurazioni alternative](#deploying-the-scanner-with-alternative-configurations). In caso contrario, assicurarsi che il computer abbia la connettività Internet che consente gli URL seguenti tramite HTTPS (porta 443):<br /> \*.aadrm.com <br /> \*.azurerms.com<br /> \*.informationprotection.azure.com <br /> informationprotection.hosting.portal.azure.net <br /> \*.aria.microsoft.com|
|Account del servizio per eseguire il servizio scanner|Oltre a eseguire il servizio scanner nel computer Windows Server, questo account di Windows esegue l'autenticazione in Azure AD e scarica i criteri di Azure Information Protection. Questo account deve essere un account Active Directory ed essere sincronizzato con Azure AD. Se non è possibile sincronizzare questo account a causa dei criteri dell'organizzazione, vedere la sezione [Distribuzione dello scanner con configurazioni alternative](#deploying-the-scanner-with-alternative-configurations).<br /><br />I requisiti di questo account del servizio sono i seguenti:<br /><br />Assegnazione dei diritti utente per l'- **accesso locale**. Questo diritto è richiesto per l'installazione e la configurazione dello scanner, ma non per il funzionamento. È necessario concedere questo diritto all'account del servizio, ma è possibile rimuoverlo dopo avere verificato che lo scanner è in grado di individuare, classificare e proteggere i file. Se non è possibile concedere questo diritto neppure per un breve periodo a causa dei criteri dell'organizzazione, vedere la sezione [Distribuzione dello scanner con configurazioni alternative](#deploying-the-scanner-with-alternative-configurations).<br /><br />Assegnazione dei diritti utente per l'- **accesso come servizio**. Questo diritto viene concesso automaticamente all'account del servizio durante l'installazione dello scanner ed è richiesto per l'installazione, la configurazione e il funzionamento dello scanner. <br /><br />- Autorizzazioni per i repository di dati: è necessario concedere le autorizzazioni per la **lettura** e la **scrittura** per analizzare i file e quindi applicare la classificazione e la protezione ai file che soddisfano le condizioni indicate nei criteri di Azure Information Protection. Per eseguire lo scanner solo in modalità di individuazione, è sufficiente l'autorizzazione per la **lettura**.<br /><br />- Per le etichette che riproteggono o rimuovono la protezione: per garantire che lo scanner abbia sempre accesso ai file protetti, trasformare l'account in un [utente con privilegi avanzati](configure-super-users.md) per il servizio Azure Rights Management e verificare che sia abilitata la funzionalità per utenti con privilegi avanzati. Per altre informazioni sui requisiti dell'account per l'applicazione della protezione, vedere [Preparazione di utenti e gruppi per Azure Information Protection](prepare.md). Se inoltre sono stati implementati i [controlli di onboarding](activate-service.md#configuring-onboarding-controls-for-a-phased-deployment) per una distribuzione a fasi, verificare che questo account sia incluso nei controlli di onboarding configurati.|
|SQL Server per archiviare la configurazione dello scanner:<br /><br />- Istanza locale o remota<br /><br />- Ruolo Sysadmin per installare lo scanner|SQL Server 2012 è la versione minima per le edizioni seguenti:<br /><br />- SQL Server Enterprise<br /><br />- SQL Server Standard<br /><br />- SQL Server Express<br /><br />Lo scanner di Azure Information Protection supporta più database di configurazione nella stessa istanza di SQL Server quando si specifica un nome di profilo personalizzato per lo scanner.<br /><br />Quando si installa lo scanner e l'account ha il ruolo Sysadmin, il processo di installazione crea automaticamente il database di configurazione dello scanner e concede il ruolo db_owner necessario all'account del servizio che esegue lo scanner. Se non è possibile ricevere il ruolo Sysadmin o se l'organizzazione richiede che i database vengano creati e configurati manualmente, vedere la sezione [Distribuzione dello scanner con configurazioni alternative](#deploying-the-scanner-with-alternative-configurations).<br /><br />Le dimensioni del database di configurazione varieranno per ogni distribuzione, ma è consigliabile allocare 500 MB ogni 1.000.000 file da analizzare. |
|Il client di Azure Information Protection è installato nel computer Windows Server|È necessario installare il client completo per lo scanner. Non installare solo il modulo PowerShell del client.<br /><br />Per istruzioni sull'installazione del client, vedere la [guida per l'amministratore](./rms-client/client-admin-guide.md). Se lo scanner è stato installato in precedenza e ora è necessario aggiornarlo a una versione più recente, vedere [Aggiornamento dello scanner di Azure Information Protection](./rms-client/client-admin-guide.md#upgrading-the-azure-information-protection-scanner).|
|Etichette configurate che applicano la classificazione automatica e, facoltativamente, la protezione|Per altre informazioni su come configurare un'etichetta per le condizioni e applicare la protezione:<br /> - [Come configurare le condizioni per la classificazione automatica e consigliata](configure-policy-classification.md)<br /> - [Come configurare un'etichetta per la protezione di Rights Management](configure-policy-protection.md) <br /><br />Suggerimento: è possibile usare le istruzioni in questa [esercitazione](infoprotect-quick-start-tutorial.md) per testare lo scanner con un'etichetta che esegue la ricerca di numeri di carta di credito in un documento di Word preparato. Tuttavia, sarà necessario modificare la configurazione dell'etichetta in modo che l'opzione **Specificare se l'etichetta viene applicata automaticamente o se viene consigliata all'utente** sia impostata su **Automatico** anziché su **Consigliato**. Rimuovere quindi l'etichetta dal documento (se applicata) e copiare il file in un repository di dati per lo scanner. Per eseguire test velocemente, è possibile copiare il file in una cartella locale nel computer dello scanner.<br /><br /> nonostante sia possibile eseguire lo scanner anche se non sono state configurate etichette che applicano la classificazione automatica, questo scenario non è illustrato in queste istruzioni. [Altre informazioni](#using-the-scanner-with-alternative-configurations)|
|Per i siti e le raccolte di SharePoint da analizzare:<br /><br />- SharePoint 2016<br /><br />- SharePoint 2013<br /><br />- SharePoint 2010|Altre versioni di SharePoint non sono supportate per lo scanner.<br /><br />Per le farm SharePoint di grandi dimensioni, controllare se è necessario aumentare la soglia della visualizzazione elenco (per impostazione predefinita, 5.000) per lo scanner al fine di accedere a tutti i file. Per altre informazioni, vedere la documentazione di SharePoint seguente: [Gestire elenchi e raccolte di grandi dimensioni in SharePoint](https://support.office.com/article/manage-large-lists-and-libraries-in-sharepoint-b8588dae-9387-48c2-9248-c24122f07c59#__bkmkchangelimit&ID0EAABAAA=Server)|
|Per i documenti di Office da analizzare:<br /><br />- Formati di file 97-2003 e formati Office Open XML per Word, Excel e PowerPoint|Per altre informazioni sui tipi di file supportati dallo scanner per questi formati di file, vedere [Tipi di file supportati dal client Azure Information Protection](./rms-client/client-admin-guide-file-types.md)|
|Per i percorsi lunghi:<br /><br />- Massimo 260 caratteri, salvo se lo scanner è installato in Windows 2016 e il computer è configurato per il supporto dei percorsi lunghi|Windows 10 e Windows Server 2016 supportano i percorsi di lunghezza superiore a 260 caratteri mediante l'[impostazione di Criteri di gruppo](https://blogs.msdn.microsoft.com/jeremykuhne/2016/07/30/net-4-6-2-and-long-paths-on-windows-10/) seguente: **Criteri Computer locale** > **Configurazione computer** > **Modelli amministrativi** > **Tutte le impostazioni** > **NTFS** > **Abilita percorsi lunghi Win32**<br /><br /> Per altre informazioni sul supporto dei percorsi di file lunghi, vedere la sezione [Maximum Path Length Limitation](https://docs.microsoft.com/windows/desktop/FileIO/naming-a-file#maximum-path-length-limitation) (Limite massimo lunghezza del percorso) nella documentazione per sviluppatori di Windows 10.

Se non è possibile soddisfare tutti i requisiti indicati nella tabella perché non sono consentiti dai criteri dell'organizzazione, vedere la sezione successiva per conoscere le alternative.

Se vengono soddisfatti tutti i requisiti, passare direttamente alla [sezione sulla configurazione dello scanner](#configure-the-scanner-in-the-azure-portal).

### <a name="deploying-the-scanner-with-alternative-configurations"></a>Distribuzione dello scanner con configurazioni alternative

I prerequisiti elencati nella tabella sono i requisiti predefiniti per lo scanner e sono consigliati perché costituiscono la configurazione più semplice per la distribuzione dello scanner. Sono appropriati per il test iniziale, per poter controllare le funzionalità dello scanner. In un ambiente di produzione, tuttavia, i criteri dell'organizzazione potrebbero non consentire questi requisiti predefiniti a causa di una o più delle restrizioni seguenti:

- La connettività Internet non è consentita per i server

- Non è possibile concedere all'utente il ruolo Sysadmin o i database devono essere creati e configurati manualmente

- Agli account del servizio non può essere concesso il diritto **Log on locally** (Accesso locale)

- Gli account del servizio non possono essere sincronizzati con Azure Active Directory, ma i server hanno la connettività Internet

Lo scanner può soddisfare queste restrizioni, che tuttavia richiedono una configurazione aggiuntiva.


#### <a name="restriction-the-scanner-server-cannot-have-internet-connectivity"></a>Restrizione: il server dello scanner non può avere la connettività Internet

Seguire le istruzioni per un [computer disconnesso](./rms-client/client-admin-guide-customizations.md#support-for-disconnected-computers). A tale scopo, effettuare le operazioni seguenti:

1. Configurare lo scanner nel portale di Azure, creando un profilo dello scanner. Se occorre assistenza per questo passaggio, vedere [Configurare lo scanner nel portale di Azure](#configure-the-scanner-in-the-azure-portal).

2. Esportare il profilo dello scanner dal pannello **Azure Information Protection - Profili (anteprima)** tramite l'opzione **Esporta**.

3. Infine, in una sessione di PowerShell, eseguire [Import-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Import-AIPScannerConfiguration) e specificare il file che contiene le impostazioni esportate.

Si noti che in questa configurazione lo scanner non può applicare la protezione (o rimuovere la protezione) usando la chiave basata sul cloud dell'organizzazione. Lo scanner può invece usare esclusivamente le etichette che applicano solo la classificazione o la protezione che usa [HYOK](configure-adrms-restrictions.md). 

#### <a name="restriction-you-cannot-be-granted-sysadmin-or-databases-must-be-created-and-configured-manually"></a>Restrizione: Non è possibile concedere all'utente il ruolo Sysadmin o i database devono essere creati e configurati manualmente

Se è possibile concedere temporaneamente all'utente il ruolo Sysadmin per installare lo scanner, è possibile rimuovere questo ruolo al termine dell'installazione dello scanner. Quando si usa questa configurazione, il database viene creato automaticamente e all'account del servizio per lo scanner vengono concesse automaticamente le autorizzazioni necessarie. L'account utente che configura lo scanner richiede tuttavia il ruolo db_owner per il database di configurazione dello scanner ed è necessario concedere manualmente questo ruolo all'account utente.

Se non è possibile concedere il ruolo Sysadmin all'utente anche solo temporaneamente, è necessario creare manualmente un database prima di installare lo scanner. Quando si usa questa configurazione, assegnare i ruoli seguenti:
    
|Account|Ruolo a livello database|
|--------------------------------|---------------------|
|Account del servizio per lo scanner|db_owner|
|Account utente per l'installazione dello scanner|db_owner|
|Account utente per la configurazione dello scanner |db_owner|

In genere, si usa lo stesso account utente per installare e configurare lo scanner, ma, se si usano account diversi, entrambi richiedono il ruolo db_owner per il database di configurazione dello scanner:

- Se non si specifica il proprio nome di profilo per lo scanner, il database di configurazione viene denominato **AIPScanner_\<nome_computer>**. 

- Se si specifica il proprio nome di profilo, il database di configurazione viene denominato **AIPScanner_\<nome_profilo>**.

#### <a name="restriction-the-service-account-for-the-scanner-cannot-be-granted-the-log-on-locally-right"></a>Restrizione: all'account del servizio scanner non può essere concesso il diritto di **accesso locale**

Se i criteri dell'organizzazione non consentono il diritto **Log on locally** (Accesso locale) per gli account del servizio, ma consentono il diritto **Accesso come processo batch**, seguire le istruzioni per [specificare e usare il parametro Token per Set-AIPAuthentication](./rms-client/client-admin-guide-powershell.md#specify-and-use-the-token-parameter-for-set-aipauthentication) della Guida dell'amministratore.

#### <a name="restriction-the-scanner-service-account-cannot-be-synchronized-to-azure-active-directory-but-the-server-has-internet-connectivity"></a>Restrizione: l'account del servizio scanner non può essere sincronizzato con Azure Active Directory, ma il server ha la connettività Internet

È possibile usare un account per eseguire il servizio dello scanner e un altro per l'autenticazione in Azure Active Directory:

- Per l'account del servizio dello scanner, è possibile usare un account Windows locale o un account Active Directory.

- Per l'account Azure Active Directory, seguire le istruzioni per [specificare e usare il parametro Token per Set-AIPAuthentication](./rms-client/client-admin-guide-powershell.md#specify-and-use-the-token-parameter-for-set-aipauthentication) nella Guida dell'amministratore.


## <a name="configure-the-scanner-in-the-azure-portal"></a>Configurare lo scanner nel portale di Azure

Prima di installare lo scanner o di eseguire l'aggiornamento dalla versione disponibile a livello generale dello scanner, creare un profilo per lo scanner nel portale di Azure. Si configura il profilo per le impostazioni dello scanner e per i repository di dati da analizzare.

1. Se non è già stato fatto, aprire una nuova finestra del browser e [accedere al portale di Azure](configure-policy.md#signing-in-to-the-azure-portal). Quindi passare al pannello **Azure Information Protection**. 
    
    Ad esempio, dal menu hub fare clic su **Tutti i servizi** e iniziare a digitare **Informazioni** nella casella Filtro. Selezionare **Azure Information Protection**.
    
2. Individuare il **Scanner** le opzioni di menu e selezionare **profili**.

3. Nel **Azure Information Protection - profili** blade, selezionare **Add**:
    
    ![Aggiungere il profilo per lo scanner di Azure Information Protection](./media/scanner-add-profile.png)

4. Nel pannello **Aggiungi un nuovo profilo** specificare un nome per lo scanner, usato per identificare le impostazioni di configurazione e i repository di dati da analizzare corrispondenti. Ad esempio, è possibile specificare **Europa** per identificare la posizione geografica dei repository di dati che verranno analizzati dallo scanner. Quando in un secondo momento si installa o si aggiorna lo scanner, sarà necessario specificare lo stesso nome di profilo.
    
    Facoltativamente, specificare una descrizione per scopi amministrativi, per facilitare l'identificazione del nome di profilo dello scanner.

5. Per questa configurazione iniziale, configurare le impostazioni seguenti e quindi selezionare **Salva** ma non chiudere il pannello:
    
    - **Pianificazione**: mantenere l'impostazione predefinita **Manuale**
    - **Tipi di informazioni da individuare**: impostare su **Solo criteri**
    - **Configura i repository**: non configurare in questo momento perché il profilo deve essere prima salvato.
    - **Imponi**: selezionare **No**
    - **Etichetta i file in base al contenuto**: mantenere l'impostazione predefinita **Sì**
    - **Etichetta predefinita**: mantenere l'impostazione predefinita **Impostazione predefinita dei criteri**
    - **Applica una nuova etichetta ai file**: mantenere l'impostazione predefinita **No**
    - **Mantieni "Data ultima modifica", "Ultima modifica" e "Modificato da"**: mantenere l'impostazione predefinita **Sì**
    - **Tipi di file da analizzare**: mantenere i tipi di file predefiniti per **Escludi**
    - **Proprietario predefinito**: mantenere l'impostazione predefinita **Account scanner**

6. Dopo aver creato e salvato il profilo, si è pronti per tornare all'opzione **Configura i repository** per specificare gli archivi dati da analizzare. È possibile specificare cartelle locali, percorsi UNC e URL di SharePoint Server per siti e librerie locali di SharePoint. 
    
    Per SharePoint sono supportate le versioni SharePoint Server 2016 e SharePoint Server 2013. Anche SharePoint Server 2010 è supportato quando è disponibile il [supporto "Extended" per questa versione di SharePoint](https://support.microsoft.com/lifecycle/search?alpha=SharePoint%20Server%202010).
    
    Per aggiungere il primo archivio dati, sempre nel pannello **Aggiungi un nuovo profilo**, selezionare **Configura i repository** per aprire il pannello **Repository**:
    
    ![Configurare i repository di dati per lo scanner di Azure Information Protection](./media/scanner-repositories-bar.png)

7. Nel pannello **Repository** selezionare **Aggiungi**:
    
    ![Aggiungere il repository di dati per lo scanner di Azure Information Protection](./media/scanner-repository-add.png)

8. Nel pannello **Repository** specificare il percorso per il repository dei dati. 
    
    I caratteri jolly e i percorsi WebDav non sono supportati.
    
    Esempi:
    
    Per un percorso locale: `C:\Folder`
    
    Per una condivisione di rete: `C:\Folder\Filename`
    
    Per un percorso UNC: `\\Server\Folder`
    
    Per una raccolta di SharePoint: `http://sharepoint.contoso.com/Shared%20Documents/Folder`
    
    > [!TIP]
    > Se si aggiunge un percorso di SharePoint per "Documenti condivisi":
    >
     >- Specificare **Documenti condivisi** nel percorso quando si vogliono analizzare tutti i documenti e tutte le cartelle da Documenti condivisi. ad esempio `http://sp2013/Shared Documents`
     >
     >- Specificare **Documenti** nel percorso quando si vogliono analizzare tutti i documenti e tutte le cartelle da una sottocartella in Documenti condivisi. ad esempio `http://sp2013/Documents/Sales Reports`
    
    Non modificare le altre impostazioni in questo pannello per questa configurazione iniziale, ma mantenere **Impostazione predefinita del profilo**. Questo significa che il repository dei dati eredita le impostazioni dal profilo dello scanner. 
    
    Selezionare **Salva**.

9. Se si vuole aggiungere un altro repository, ripetere i passaggi 7 e 8.

10. È ora possibile chiudere il **aggiungere un nuovo profilo** pannello e verrà visualizzato il nome del profilo visualizzato nei **Azure Information Protection - profili** pannello, insieme al **pianificazione** che Mostra colonne **manuali** e il **IMPONI** colonna è vuota.

A questo punto si è pronti per installare lo scanner con il profilo di scanner appena creato.

## <a name="install-the-scanner"></a>Installare lo scanner

1. Accedere al computer Windows Server che eseguirà lo scanner. Usare un account con diritti di amministratore locale e con le autorizzazioni per scrivere nel database master di SQL Server.

2. Aprire una sessione di Windows PowerShell con l'opzione **Esegui come amministratore**.

3. Eseguire il cmdlet [Install-AIPScanner](/powershell/module/azureinformationprotection/Install-AIPScanner), che specifica l'istanza di SQL Server in cui creare un database per lo scanner di Azure Information Protection e il nome del profilo di scanner specificato nella sezione precedente: 
    
    ```
    Install-AIPScanner -SqlServerInstance <name> -Profile <profile name>
    ```
    
    Esempi, usando il nome di profilo **Europe**:
    
    Per un'istanza predefinita: `Install-AIPScanner -SqlServerInstance SQLSERVER1 -Profile Europe`
    
    Per un'istanza denominata: `Install-AIPScanner -SqlServerInstance SQLSERVER1\AIPSCANNER -Profile Europe`
    
    Per SQL Server Express: `Install-AIPScanner -SqlServerInstance SQLSERVER1\SQLEXPRESS -Profile Europe`
    
    Quando richiesto, specificare le credenziali per l'account del servizio scanner (\<dominio\nome utente>) e la password.

4. Verificare che il servizio è ora installato usando **Strumenti di amministrazione** > **Servizi**. 
    
    Il servizio installato è denominato **Azure Information Protection Scanner** ed è configurato per essere eseguito usando l'account del servizio scanner creato.

Ora che è stato installato lo scanner, è necessario ottenere un token di Azure AD per l'account del servizio scanner da autenticare, in modo che lo scanner possa essere eseguito automaticamente. 

## <a name="get-an-azure-ad-token-for-the-scanner"></a>Ottenere un token di Azure AD per lo scanner

Il token di Azure AD consente all'account del servizio scanner di eseguire l'autenticazione per il servizio Azure Information Protection.

1. Tornare al portale di Azure per creare due applicazioni di Azure AD necessarie per specificare un token di accesso per l'autenticazione. Dopo un accesso interattivo iniziale, questo token consente di eseguire lo scanner in modo non interattivo.
    
    Per creare queste applicazioni, seguire le istruzioni della sezione [Come assegnare un'etichetta ai file in modo non interattivo per Azure Information Protection](./rms-client/client-admin-guide-powershell.md#how-to-label-files-non-interactively-for-azure-information-protection) della guida per l'amministratore.

2. Dal computer Windows Server, se all'account del servizio scanner è stato concesso il diritto di **accesso locale** per l'installazione: accedere con questo account e avviare una sessione di PowerShell. Eseguire [Set-AIPAuthentication](/powershell/module/azureinformationprotection/set-aipauthentication) specificando i valori copiati nel passaggio precedente:
    
    ```
    Set-AIPAuthentication -webAppId <ID of the "Web app / API" application> -webAppKey <key value generated in the "Web app / API" application> -nativeAppId <ID of the "Native" application>
    ```
    
    Quando richiesto, specificare la password per le credenziali dell'account del servizio per Azure AD e quindi fare clic su **Accetto**.
    
    Se all'account del servizio scanner non può essere concesso il diritto di **accesso locale**: seguire le istruzioni riportate nella sezione [Specificare e usare il parametro Token per Set-AIPAuthentication](./rms-client/client-admin-guide-powershell.md#specify-and-use-the-token-parameter-for-set-aipauthentication) della Guida dell'amministratore. 

Lo scanner ora ha un token per l'autenticazione ad Azure AD, che può essere valido per un anno, due anni, o senza scadenza, in base alla configurazione dell'**app Web/API** in Azure AD. Quando il token scade, è necessario ripetere i passaggi 1 e 2.

Si è ora pronti per eseguire la prima analisi in modalità di individuazione.

## <a name="run-a-discovery-cycle-and-view-reports-for-the-scanner"></a>Eseguire un ciclo di individuazione e visualizzare i report per lo scanner

1. Nel portale di Azure tornare ad Azure Information Protection per avviare lo scanner. Dall'opzione di menu **Scanner** selezionare **Nodi**. Selezionare il nodo dello scanner e quindi l'opzione **Avvia analisi**:
    
    ![Avviare l'analisi per lo scanner di Azure Information Protection](./media/scanner-scan-now.png)
    
    In alternativa, nella sessione di PowerShell, eseguire il comando seguente:
    
        Start-AIPScan

2. Attendere che lo scanner completi il proprio ciclo. Quando lo scanner ha completato l'analisi per tutti i file negli archivi dati specificati, lo scanner viene arrestato anche se il servizio scanner rimane in esecuzione:
    
    - Nel pannello **Azure Information Protection - Nodi** il valore della colonna **STATO** passa da **Analisi in corso** a **Inattivo**.
    
    - Usando PowerShell è possibile eseguire `Get-AIPScannerStatus` per monitorare la modifica dello stato.
    
    - Controllare il registro eventi locale **Applicazioni e servizi** di Windows, **Azure Information Protection**. Questo registro indica anche quando lo scanner ha completato l'analisi, con un riepilogo dei risultati. Cercare l'ID evento informativo **911**.

3. Esaminare i report archiviati in %*localappdata*%\Microsoft\MSIP\Scanner\Reports. I file summary.txt includono il tempo impiegato per l'analisi, il numero di file analizzati e il numero di file con una corrispondenza per i tipi di informazioni. I file con estensione csv includono ulteriori dettagli per ogni file. In questa cartella vengono archiviati fino a 60 report per ogni ciclo di analisi e tutti i report tranne l'ultimo vengono compressi per ridurre al minimo lo spazio su disco necessario.
    
    > [!NOTE]
    > È possibile modificare il livello di registrazione usando il parametro *ReportLevel* con [Set-AIPScannerConfiguration](/powershell/module/azureinformationprotection/set-aipscannerconfiguration), ma non è possibile modificare il percorso della cartella o il nome del report. Valutare la possibilità di usare una giunzione di directory per la cartella, se si vogliono archiviare i report in un volume o una partizione diversi.
    >
    > Ad esempio, usando il comando [Mklink](/windows-server/administration/windows-commands/mklink): `mklink /j D:\Scanner_reports C:\Users\aipscannersvc\AppData\Local\Microsoft\MSIP\Scanner\Reports`
    
    Con l'impostazione **Solo criteri** per **Tipi di informazioni da individuare**, solo i file che soddisfano le condizioni configurate per la classificazione automatica vengono inclusi nei report dettagliati. Se non si vedono etichette applicate, controllare che la configurazione delle etichette includa la classificazione automatica anziché consigliata.
    
    > [!TIP]
    > Gli scanner inviano queste informazioni ad Azure Information Protection ogni cinque minuti, in modo che sia possibile visualizzare i risultati quasi in tempo reale dal portale di Azure. Per altre informazioni, vedere [Reporting per Azure Information Protection](reports-aip.md). 
        
    Se i risultati non sono quelli previsti, potrebbe essere necessario riconfigurare le condizioni specificate per le etichette nei criteri di Azure Information Protection. In questo caso, ripetere i passaggi da 1 a 3 finché non si è pronti a modificare la configurazione per applicare la classificazione e, facoltativamente, la protezione. 

Il portale di Azure visualizza solo le informazioni sull'ultima analisi. Se è necessario visualizzare i risultati delle analisi precedenti, tornare ai report archiviati nel computer dello scanner, nella cartella %*localappdata*%\Microsoft\MSIP\Scanner\Reports.

Quando si è pronti ad etichettare automaticamente i file individuati dallo scanner, passare alla procedura successiva. 

## <a name="configure-the-scanner-to-apply-classification-and-protection"></a>Configurare lo scanner per applicare la classificazione e la protezione

Se si seguono queste istruzioni, lo scanner viene eseguito una volta e solo ai fini della creazione di report. Per modificare queste impostazioni, modificare il profilo dello scanner:

1. Nella **Azure Information Protection - profili** pannello, selezionare il profilo scanner per modificarlo.

2. Nel pannello \<**nome profilo**> modificare le due impostazioni seguenti e quindi selezionare **Salva**:
    
   - **Pianificazione**: impostare su **Sempre**
   - **Imponi**: selezionare **Sì**
    
     Esistono altre impostazioni di configurazione che è opportuno modificare. Indicare ad esempio se gli attributi dei file vengono modificati e se lo scanner può rietichettare i file. Usare la Guida con informazioni popup per altre informazioni sulle singole impostazioni di configurazione.

3. Prendere nota dell'ora corrente e avviare di nuovo lo scanner dal pannello **Azure Information Protection - Nodi**:
    
    ![Avviare l'analisi per lo scanner di Azure Information Protection](./media/scanner-scan-now.png)
    
    In alternativa, è possibile eseguire il comando seguente nella sessione di PowerShell:
    
        Start-AIPScan

4. Monitorare di nuovo il tipo di evento informativo **911** nel registro eventi, con un timestamp successivo all'avvio dell'analisi nel passaggio precedente. 
    
    Controllare quindi i report per visualizzare i dettagli dei file etichettati, la classificazione applicata a ogni file e se la protezione è stata applicata. In alternativa, usare il portale di Azure per visualizzare più facilmente queste informazioni.

Poiché la pianificazione è stata configurata in modo da essere eseguita continuamente, quando lo scanner ha completato l'analisi di tutti i file, avvia un nuovo ciclo automaticamente per individuare eventuali file nuovi e modificati.


## <a name="how-files-are-scanned"></a>Modalità di analisi dei file

Lo scanner esegue i processi seguenti per l'analisi di file.

### <a name="1-determine-whether-files-are-included-or-excluded-for-scanning"></a>1. Determinare se i file sono esclusi o inclusi nell'analisi 
Lo scanner ignora automaticamente i file [esclusi dalla classificazione e dalla protezione](./rms-client/client-admin-guide-file-types.md#file-types-that-are-excluded-from-classification-and-protection), ad esempio file eseguibili e file di sistema.

È possibile modificare questo comportamento definendo un elenco di tipi di file da includere o escludere dall'analisi. È possibile specificare questo elenco da applicare a tutti i repository di dati per impostazione predefinita ed è possibile specificare un elenco per ogni repository dei dati. Per specificare questo elenco, usare l'impostazione **Tipi di file da analizzare** nel profilo dello scanner:

![Configurare i tipi di file da analizzare per lo scanner di Azure Information Protection](./media/scanner-file-types.png)

### <a name="2-inspect-and-label-files"></a>2. Esaminare e assegnare etichette ai file

Lo scanner usa quindi i filtri per l'analisi dei tipi di file supportati. Gli stessi filtri vengono usati dal sistema operativo per Windows Search e per l'indicizzazione. Windows IFilter viene usato senza alcuna configurazione aggiuntiva per l'analisi di file usati da Word, Excel e PowerPoint, nonché di documenti PDF e file di testo.

Per l'elenco completo dei tipi di file supportati per impostazione predefinita e per informazioni aggiuntive su come configurare filtri esistenti che includono i file con estensione zip e tiff, vedere [Tipi di file supportati per il controllo](./rms-client/client-admin-guide-file-types.md#file-types-supported-for-inspection).

Dopo il controllo è possibile contrassegnare questi file mediante le condizioni specificate per le etichette. In alternativa, se si usa la modalità di individuazione, i file possono essere segnalati se contengono le condizioni specificate per le etichette o tutti i tipi di informazioni riservate noti. 

Tuttavia lo scanner non è in grado di contrassegnare i file nelle circostanze seguenti:

- Se l'etichetta applica classificazione ma non protezione e il tipo di file non [supporta solo la classificazione](./rms-client/client-admin-guide-file-types.md#file-types-supported-for-classification-only).

- Se l'etichetta applica classificazione e protezione, ma lo scanner non protegge il tipo di file.
    
    Per impostazione predefinita lo scanner protegge solo i tipi di file di Office e i file PDF se questi sono protetti usando lo standard ISO per la crittografia dei file PDF. È possibile impostare la protezione di altri tipi di file quando si [modifica il Registro di sistema](#editing-the-registry-for-the-scanner), come descritto in una delle sezioni seguenti.

Ad esempio, dopo il controllo di file con estensione txt, lo scanner non può applicare un'etichetta configurata per la classificazione ma non per la protezione, perché il tipo di file con estensione txt non supporta la sola classificazione. Se l'etichetta è configurata per la classificazione e la protezione dati e il Registro di sistema viene modificato per il tipo di file con estensione txt, lo scanner può applicare un'etichetta al file. 

> [!TIP]
> Durante questo processo, se lo scanner si arresta e non completa l'analisi di un numero elevato di file in un repository:
> 
> - Potrebbe essere necessario aumentare il numero di porte dinamiche per il sistema operativo che ospita i file. Uno dei motivi per cui lo scanner supera il numero di connessioni di rete consentite e pertanto si arresta può essere la protezione avanzata dei server per SharePoint.
>     
>     Per verificare se questa è la causa dell'arresto dello scanner, verificare se il messaggio di errore seguente viene registrato per lo scanner in %*localappdata*%\Microsoft\MSIP\Logs\MSIPScanner.iplog (compresso come file zip se sono presenti più log): **Non è possibile connettersi al server remoto ---> System.Net.Sockets.SocketException: Di norma è consentito un solo uso di ogni indirizzo di socket (protocollo/indirizzo di rete/porta) IP:porta**
>    
>     Per altre informazioni su come visualizzare l'intervallo di porte corrente e aumentarlo, vedere [Impostazioni che possono essere modificate per migliorare le prestazioni di rete](https://docs.microsoft.com/biztalk/technical-guides/settings-that-can-be-modified-to-improve-network-performance).
> 
> - Per le farm SharePoint di grandi dimensioni, potrebbe essere necessario aumentare la soglia della visualizzazione elenco (per impostazione predefinita, 5.000). Per altre informazioni, vedere la documentazione di SharePoint seguente: [Gestire elenchi e raccolte di grandi dimensioni in SharePoint](https://support.office.com/article/manage-large-lists-and-libraries-in-sharepoint-b8588dae-9387-48c2-9248-c24122f07c59#__bkmkchangelimit&ID0EAABAAA=Server).

### <a name="3-label-files-that-cant-be-inspected"></a>3. Assegnare etichette ai file che non possono essere controllati
Per i tipi di file che non possono essere controllati, lo scanner applica l'etichetta predefinita nei criteri di Azure Information Protection oppure l'etichetta predefinita configurata per lo scanner.

Come nel passaggio precedente, lo scanner non è in grado di contrassegnare i file nelle circostanze seguenti:

- Se l'etichetta applica classificazione ma non protezione e il tipo di file non [supporta solo la classificazione](./rms-client/client-admin-guide-file-types.md#file-types-supported-for-classification-only).

- Se l'etichetta applica classificazione e protezione, ma lo scanner non protegge il tipo di file.
    
    Per impostazione predefinita lo scanner protegge solo i tipi di file di Office e i file PDF se questi sono protetti usando lo standard ISO per la crittografia dei file PDF. È possibile impostare la protezione di altri tipi di file quando si [modifica il Registro di sistema](#editing-the-registry-for-the-scanner), come descritto di seguito.


### <a name="editing-the-registry-for-the-scanner"></a>Modifica del Registro di sistema per lo scanner

Per modificare il comportamento predefinito dello scanner per la protezione di tipi di file diversi dai file di Office e i file PDF, è necessario modificare manualmente il Registro di sistema e specificare i tipi di file aggiuntivi da proteggere e il tipo di protezione (nativa o generica). Per informazioni, vedere [Configurazione dell'API file](develop/file-api-configuration.md) nelle linee guida per sviluppatori. Per fare riferimento alla protezione generica, questa documentazione per sviluppatori usa il termine "PFile". Inoltre, specificatamente per lo scanner:

- Lo scanner ha un proprio comportamento predefinito: solo i formati di file di Office e i documenti PDF sono protetti per impostazione predefinita. Se il Registro di sistema non viene modificato, tutti gli altri tipi di file non verranno etichettati né protetti dallo scanner.

- Se si vuole lo stesso comportamento di protezione predefinito del client Azure Information Protection, in cui tutti i file vengono automaticamente protetti con la protezione nativa o generica: specificare il carattere jolly `*` come chiave del Registro di sistema e `Default` come dati valore.

Quando si modifica il Registro di sistema, creare manualmente la chiave **MSIPC** e la chiave **FileProtection** se non esistono, nonché una chiave per ogni estensione del nome file.

Ad esempio, per fare in modo che lo scanner protegga le immagini TIFF oltre ai file di Office e ai file PDF, il Registro di sistema dopo la modifica avrà un aspetto simile all'immagine seguente. Dato che sono file immagine, i file con estensione tiff supportano la protezione nativa e l'estensione di file risultante è ptiff.

![Modifica del Registro di sistema per l'applicazione della protezione con lo scanner](./media/editregistry-scanner.png)

Per un elenco di file di testo e file immagine che supportano la protezione nativa ma vanno specificati nel Registro di sistema, vedere [Tipi di file supportati per la classificazione e la protezione](./rms-client/client-admin-guide-file-types.md#file-types-supported-for-protection) nella Guida dell'amministratore.

Per i file che non supportano la protezione nativa, specificare l'estensione del nome file come nuova chiave e **PFile** per la protezione generica. L'estensione del nome file risultante per il file protetto è pfile.


## <a name="when-files-are-rescanned"></a>Ripetizione dell'analisi dei file

Per il primo ciclo di analisi, lo scanner analizza tutti i file negli archivi dati configurati e quindi per le analisi successive, vengono controllati solo i file nuovi o modificati. 

È possibile imporre allo scanner di esaminare di nuovo tutti i file dal pannello **Azure Information Protection - Nodi** nel portale di Azure. Selezionare lo scanner nell'elenco e quindi selezionare l'opzione **Ripeti l'analisi di tutti i file**:

![Avviare un'altra analisi per lo scanner di Azure Information Protection](./media/scanner-rescan-files.png)

È utile verificare nuovamente i file quando si vuole che i report includano tutti i file e questa configurazione viene in genere usata quando lo scanner viene eseguito in modalità di individuazione. Al termine di un'analisi completa, il tipo di analisi diventa automaticamente incrementale in modo che per le analisi successive vengono analizzati solo i file nuovi o modificati.

Inoltre, tutti i file vengono controllati quando lo scanner scarica un criterio di Azure Information Protection con condizioni nuove o modificate. Lo scanner aggiorna i criteri ogni ora, all'avvio del servizio e quando risalgono a più di un'ora prima.  

> [!TIP]
> Se è necessario aggiornare i criteri prima di questo intervallo di un'ora, ad esempio, durante un periodo di test: Eliminare manualmente il file dei criteri **Policy.msip** sia da **%LocalAppData%\Microsoft\MSIP\Policy.msip** che da **%LocalAppData%\Microsoft\MSIP\Scanner**. Riavviare il servizio scanner di Azure Information Protection.
> 
> Se sono state modificate le impostazioni di protezione dei criteri, attendere 15 minuti dal salvataggio delle impostazioni di protezione prima di riavviare il servizio.

Se lo scanner ha scaricato criteri per cui non sono state configurate condizioni automatiche, la copia del file dei criteri nella cartella dello scanner non viene aggiornata. In questo scenario, è necessario eliminare il file di criteri **Policy.msip** sia da **%LocalAppData%\Microsoft\MSIP\Policy.msip** che da **%LocalAppData%\Microsoft\MSIP\Scanner** prima che lo scanner possa usare un nuovo file dei criteri scaricato con etichette calcolate correttamente per le condizioni automatiche.

## <a name="editing-in-bulk-for-the-data-repository-settings"></a>Modifica in blocco per le impostazioni dei repository di dati

Per i repository di dati aggiunti a un profilo dello scanner, è possibile usare le opzioni **Esporta** e **Importa** per modificare velocemente le impostazioni. Si supponga, ad esempio di volere aggiungere un nuovo tipo di file da escludere dall'analisi per i repository di dati di SharePoint.

Invece di modificare ogni repository di dati nel portale di Azure, usare l'opzione **Esporta** dal pannello **Repository**:

![Esportazione delle impostazioni del repository dei dati per lo scanner](./media/export-scanner-repositories.png)

Modificare manualmente il file per apportare la modifica e quindi usare l'opzione **Importa** nello stesso pannello.

## <a name="using-the-scanner-with-alternative-configurations"></a>Uso dello scanner con configurazioni alternative

Lo scanner di Azure Information Protection supporta due scenari alternativi in cui non è necessario configurare le etichette per le condizioni: 

- Applicare un'etichetta predefinita a tutti i file in un repository di dati.
    
    Per questa configurazione, impostare **Etichetta predefinita** su **Personalizzata** e selezionare l'etichetta da usare.
    
    Il contenuto dei file non viene analizzato e tutti i file nel repository di dati vengono etichettati in base all'etichetta predefinita specificata per il repository di dati o il profilo dello scanner.
    

- Identificare tutte le condizioni personalizzate e i tipi di informazioni riservate noti.
    
    Per questa configurazione, impostare **Tipi di informazioni da individuare** su **Tutti**.
    
    Lo scanner usa eventuali condizioni personalizzate specificate per le etichette nei criteri di Azure Information Protection e l'elenco di tipi di informazioni che è possibile specificare per le etichette nei criteri di Azure Information Protection. Questa impostazione consente di trovare le informazioni sensibili di cui si potrebbe non essere a conoscenza, a scapito però della velocità di analisi per lo scanner.
    
    Nell'articolo di avvio rapido seguente per la versione disponibile a livello generale dello scanner viene usata questa configurazione: [Avvio rapido: Trovare le informazioni riservate disponibili](quickstart-findsensitiveinfo.md).

## <a name="optimizing-the-performance-of-the-scanner"></a>Ottimizzazione delle prestazioni dello scanner

Usare le linee guida seguenti per ottimizzare le prestazioni dello scanner. Se tuttavia la priorità è la velocità di risposta del computer dello scanner più che le prestazioni dello scanner, è possibile usare un'impostazione client avanzata per limitare il numero di thread usati dallo scanner.

Per ottimizzare le prestazioni dello scanner:

- **Disporre di una connessione di rete ad alta velocità e affidabile tra il computer dello scanner e l'archivio dei dati analizzati**
    
    Ad esempio, inserire il computer dello scanner nella stessa rete LAN o (scelta consigliata) nello stesso segmento di rete dell'archivio dei dati analizzati.
    
    La qualità della connessione di rete influisce sulle prestazioni dello scanner perché per controllare i file lo scanner trasferisce il contenuto dei file nel computer che esegue il servizio di analisi. Quando si riduce o si elimina il numero di hop di rete per i dati, si riduce anche il carico sulla rete. 

- **Verificare che il computer dello scanner abbia risorse del processore disponibili**
    
    La ricerca di una corrispondenza nel contenuto dei file e la crittografia e la decrittografia dei file sono operazioni che richiedono un uso intensivo del processore. Monitorare i cicli di analisi tipici degli archivi dati specificati per identificare se una mancanza di risorse del processore influisce negativamente sulle prestazioni dello scanner.
    
- **Non eseguire l'analisi delle cartelle locali nel computer che esegue il servizio di analisi**
    
    Se sono presenti cartelle da analizzare in un server di Windows, installare lo scanner in un computer diverso e configurare le cartelle come condivisioni di rete da analizzare. La separazione delle due funzioni di hosting dei file e di analisi dei file fa in modo che le risorse di elaborazione di questi servizi non siano in competizione tra loro.

Se necessario, installare più istanze dello scanner. Lo scanner di Azure Information Protection supporta più database di configurazione nella stessa istanza di SQL Server quando si specifica un nome di profilo personalizzato per lo scanner.

Altri fattori che influenzano le prestazioni dello scanner:

- Carico corrente e tempi di risposta degli archivi dati che contengono i file da analizzare

- Esecuzione dello scanner in modalità di individuazione o applicazione
    
    La modalità di individuazione ha in genere una velocità di analisi maggiore rispetto alla modalità di applicazione poiché l'individuazione richiede una sola azione di lettura dei file, mentre la modalità di applicazione richiede azioni di lettura e scrittura.

- Modifica delle condizioni in Azure Information Protection
    
    Il primo ciclo di analisi nel quale lo scanner deve analizzare ogni file richiede più tempo rispetto ai cicli di analisi successivi in cui, per impostazione predefinita, vengono analizzati solo i file nuovi e modificati. Tuttavia, se si modificano le condizioni nei criteri di Azure Information Protection, tutti i file vengono analizzati nuovamente come descritto nella [sezione precedente](#when-files-are-rescanned).

- La costruzione di espressioni regex per condizioni personalizzate
    
    Per evitare un consumo intenso di memoria e il rischio di timeout (15 minuti per ogni file), rivedere le espressioni regex per assicurarsi che usino criteri di ricerca efficienti. Ad esempio:
    
    - Evitare [quantificatori greedy](https://docs.microsoft.com/dotnet/standard/base-types/quantifiers-in-regular-expressions)
    
    - Usare gruppi di non acquisizione, ad esempio `(?:expression)` invece di `(expression)`

- Livello di registrazione selezionato
    
    È possibile scegliere tra **Debug**, **Info** (Informazioni), **Error** (Errore) e **Off** (Disattivato) per i report dello scanner. **Off** (Disattivato) offre le prestazioni migliori; **Debug** rallenta considerevolmente lo scanner ed è consigliabile usarlo solo per la ricerca e la risoluzione dei problemi. Per altre informazioni, vedere il parametro *ReportLevel* del cmdlet [Set-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Set-AIPScannerConfiguration).

- File:
    
    - I file di Office vengono analizzati più rapidamente rispetto ai file PDF.
    
    - I file non protetti sono più veloci da analizzare rispetto ai file protetti.
    
    - I file di grandi dimensioni richiedono più tempo per l'analisi rispetto ai file di piccole dimensioni.

- Inoltre:
    
    - Verificare che l'account del servizio che esegue lo scanner abbia solo i diritti indicati nella sezione relativa ai [prerequisiti dello scanner](#prerequisites-for-the-azure-information-protection-scanner) e quindi configurare la [proprietà avanzata del client](./rms-client/client-admin-guide-customizations.md#disable-the-low-integrity-level-for-the-scanner) per disabilitare il livello di integrità basso per lo scanner.
    
    - L'esecuzione dello scanner è più rapida quando si usa la [configurazione alternativa](#using-the-scanner-with-alternative-configurations) per applicare un'etichetta predefinita a tutti i file in quanto lo scanner non esamina i contenuti del file.
    
    - L'esecuzione dello scanner è più lenta quando si usa la [configurazione alternativa](#using-the-scanner-with-alternative-configurations) per identificare tutte le condizioni personalizzate e i tipi di informazioni riservate noti.
    

## <a name="list-of-cmdlets-for-the-scanner"></a>Elenco dei cmdlet per lo scanner

Dato che è ora possibile configurare lo scanner dal portale di Azure, i cmdlet di versioni precedenti usati per la configurazione dei repository di dati e l'elenco dei tipi di file analizzati sono deprecati. 

I cmdlet rimanenti includono i cmdlet per installare e aggiornare lo scanner, modificare il database di configurazione dello scanner e il profilo, modificare il livello di report locale e importare le impostazioni di configurazione per un computer disconnesso. 

L'elenco completo dei cmdlet che supporta la versione corrente dello scanner: 

- [Get-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Get-AIPScannerConfiguration)

- [Get-AIPScannerStatus](/powershell/module/azureinformationprotection/Get-AIPScannerStatus)

- [Install-AIPScanner](/powershell/module/azureinformationprotection/Install-AIPScanner)

- [Set-AIPScanner](/powershell/module/azureinformationprotection/Set-AIPScanner)

- [Set-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Set-AIPScannerConfiguration)

- [Start-AIPScan](/powershell/module/azureinformationprotection/Start-AIPScan)

- [Uninstall-AIPScanner](/powershell/module/azureinformationprotection/Uninstall-AIPScanner)

- [Update-AIPScanner](/powershell/module/azureinformationprotection/Update-AIPScanner)


## <a name="event-log-ids-and-descriptions-for-the-scanner"></a>ID registro eventi e descrizioni per lo scanner

Usare le sezioni seguenti per identificare gli ID evento e le descrizioni possibili per lo scanner. Gli eventi vengono registrati nel server su cui viene seguito il servizio scanner, nel registro eventi di **applicazioni e servizi** di Windows, **Azure Information Protection**.

-----

Informazione **910**

**Ciclo dello scanner avviato.**

Questo evento viene registrato quando il servizio scanner viene avviato e inizia a cercare i file negli archivi dati specificati.

----

Informazione **911**

**Ciclo dello scanner completato.**

Questo evento viene registrato quando lo scanner ha completato un'analisi manuale o un ciclo in caso di pianificazione continua.

Se lo scanner è stato configurato per l'esecuzione manuale anziché continuativa, per analizzare di nuovo i file impostare **Pianificazione** su **Manuale** o **Sempre** nel profilo dello scanner e quindi riavviare il servizio.

----

## <a name="next-steps"></a>Passaggi successivi

Se si è interessati a scoprire come è stato implementato questo scanner dai team Microsoft Core Services Engineering e Operations,  Leggere il case study tecnico: [Automating data protection with Azure Information Protection scanner](https://www.microsoft.com/itshowcase/Article/Content/1070/Automating-data-protection-with-Azure-Information-Protection-scanner) (Automazione della protezione dei dati con lo scanner di Azure Information Protection).

Può sorgere questa domanda: [Qual è la differenza tra l'infrastruttura di classificazione file di Windows Server e lo scanner di Azure Information Protection?](faqs.md#whats-the-difference-between-windows-server-fci-and-the-azure-information-protection-scanner)

È anche possibile usare PowerShell per classificare e proteggere in modo interattivo i file dal computer desktop. Per altre informazioni su questo e altri scenari che usano PowerShell, vedere [Uso di PowerShell con il client Azure Information Protection](./rms-client/client-admin-guide-powershell.md).

