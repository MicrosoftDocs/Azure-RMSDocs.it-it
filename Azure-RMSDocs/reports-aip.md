---
title: Reporting centralizzato per Azure Information Protection
description: Come usare il reporting centralizzato per monitorare l'adozione delle etichette di Azure Information Protection e trovare i file che contengono informazioni riservate
author: cabailey
ms.author: cabailey
ms.date: 10/14/2019
manager: rkarlin
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: b2da2cdc-74fd-4bfb-b3c2-2a3a59a6bf2e
ms.subservice: analytics
ms.reviewer: lilukov
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 8b7884de10999518d0c6cf9806b546181277a113
ms.sourcegitcommit: 07ae7007c79c998bbf3b8cf37808daf0eec68ad1
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/16/2019
ms.locfileid: "72447841"
---
# <a name="central-reporting-for-azure-information-protection"></a>Reporting centralizzato per Azure Information Protection

>*Si applica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*

> [!NOTE]
> Al momento questa funzionalità è disponibile in anteprima ed è soggetta a modifiche.

Usare Azure Information Protection Analytics per la creazione di report centrali che consentono di tenere traccia dell'adozione delle etichette che classificano e proteggono i dati dell'organizzazione. Inoltre:

- Monitorare documenti e messaggi di posta elettronica etichettati e protetti nell'organizzazione.

- Identificare i documenti che contengono informazioni riservate nell'organizzazione.

- Monitorare l'accesso degli utenti a documenti e messaggi di posta elettronica etichettati e tenere traccia delle modifiche alla classificazione dei documenti.

- Identificare i documenti contenenti informazioni sensibili che possono mettere a rischio l'organizzazione se non protette e attenuare il rischio seguendo le raccomandazioni.

- Individuare i casi in cui l'accesso ai documenti protetti viene eseguito da utenti interni o esterni da computer Windows e se l'accesso è stato concesso o negato.

I dati visualizzati sono aggregati da client e scanner di Azure Information Protection, da [client e servizi che supportano l'assegnazione di etichette unificata](configure-policy-migrate-labels.md#clients-and-services-that-support-unified-labeling)e dai log di [utilizzo della protezione](log-analyze-usage.md).

> [!NOTE]
> Attualmente, fatta eccezione per la versione di anteprima del client Unified Labeling, Azure Information Protection Analytics non include i tipi di informazioni personalizzate per i client e i servizi che supportano l'assegnazione di etichette unificata.

Ad esempio è possibile visualizzare quanto segue:

- Nel **Report di utilizzo**, in cui è possibile selezionare un periodo di tempo:
    
    - Quali etichette vengono applicate
    
    - Quanti documenti e messaggi di posta elettronica vengono corredati di etichetta
    
    - Quanti documenti e messaggi di posta elettronica vengono protetti
    
    - Quanti utenti e dispositivi applicano etichette a documenti e messaggi di posta elettronica
    
    - Quali applicazioni vengono usate per l'assegnazione di etichette

- Dai **log attività**, in cui è possibile selezionare un periodo di tempo:
    
    - Quali azioni di etichettatura sono state eseguite da un utente specifico
    
    - Quali azioni di etichettatura sono state eseguite da un dispositivo specifico
    
    - Quali utenti hanno avuto accesso a un documento etichettato specifico
    
    - Quali azioni di etichettatura sono state eseguite da un percorso di file specifico
    
    - Quali azioni di assegnazione di etichette sono state eseguite da un'applicazione specifica, ad esempio Esplora file e con il pulsante destro del mouse, PowerShell, lo scanner o Microsoft Cloud App Security
    
    - A quali documenti protetti è stato eseguito l'accesso da parte degli utenti o negato l'accesso agli utenti, anche se tali utenti non hanno il client di Azure Information Protection installato o non sono all'interno dell'organizzazione

    - Eseguire il drill-down dei file segnalati per visualizzare la sezione **Dettagli attività** in cui sono disponibili altre informazioni

- Nel report **Individuazione dati**:

    - Quali file si trovano nei repository di dati scansionati, nei computer Windows 10 o nei computer che eseguono il client Azure Information Protection o i [client che supportano l'assegnazione di etichette unificata](configure-policy-migrate-labels.md#clients-and-services-that-support-unified-labeling)
    
    - Quali file sono provvisti di etichetta e protetti e il percorso dei file in base alle etichette
    
    - Quali file contengono informazioni riservate per categorie note, ad esempio dati finanziari e informazioni personali e il percorso dei file in base a queste categorie

- Dal report **Raccomandazioni**:
    
    - Identificare i file non protetti che contengono un tipo noto di informazioni sensibili. Una raccomandazione consente di configurare immediatamente la condizione corrispondente a una delle etichette, per applicare l'etichettatura automatica o consigliata.
        
        Se si segue la Raccomandazione: la volta successiva che i file vengono aperti da un utente o analizzati dal Azure Information Protection scanner, i file possono essere classificati e protetti automaticamente.
    
    - Identificare i repository dei dati che contengono file con informazioni sensibili identificate ma non analizzati da Azure Information Protection. Una raccomandazione consente di aggiungere immediatamente l'archivio dati identificato a uno dei profili dello scanner.
        
        Se si segue la Raccomandazione: al successivo ciclo dello scanner, i file possono essere classificati e protetti automaticamente.

I report usano [Monitoraggio di Azure](/azure/log-analytics/log-analytics-overview) per archiviare i dati in un'area di lavoro di Log Analytics di proprietà dell'organizzazione. Se si ha familiarità con il linguaggio di query, è possibile modificare le query e creare nuovi report e dashboard di Power BI. L'esercitazione seguente può essere utile per comprendere il linguaggio di query: [Introduzione alle query di log di monitoraggio di Azure](/azure/azure-monitor/log-query/get-started-queries).

Per altre informazioni, vedere i seguenti post di blog: 
- [Data discovery, reporting and analytics for all your data with Microsoft Information Protection](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/Data-discovery-reporting-and-analytics-for-all-your-data-with/ba-p/253854) (Individuazione, report e analisi per tutti i dati utente con Microsoft Information Protection).

- [Individuare e proteggere i dati sensibili tramite Azure Information Protection e Microsoft Defender ATP](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/Discover-and-protect-sensitive-data-through-Azure-Information/ba-p/297292)

### <a name="information-collected-and-sent-to-microsoft"></a>Informazioni raccolte e inviate a Microsoft

Per generare questi report, gli endpoint inviano i seguenti tipi di informazioni a Microsoft:

- Azione per l'etichetta. Ad esempio impostazione o modifica di un'etichetta, aggiunta o rimozione della protezione, etichette automatiche e consigliate.

- Nome dell'etichetta prima e dopo l'azione dell'etichetta.

- ID del tenant dell'organizzazione.

- ID utente (indirizzo di posta elettronica o UPN).

- Nome del dispositivo dell'utente.

- Per i documenti: percorso e nome file dei documenti ai quali viene aggiunta l'etichetta.

- Per i messaggi di posta elettronica: l'oggetto e il mittente di posta elettronica per i messaggi di posta elettronica contrassegnati. 

- [Tipi di informazioni riservate predefinite](https://docs.microsoft.com/microsoft-365/compliance/what-the-sensitive-information-types-look-for) rilevati nel contenuto.
    
    Se si usano Azure Information Protection etichette con condizioni personalizzate, vengono inviati anche i nomi dei tipi di informazioni personalizzate. Fatta eccezione per la versione di anteprima del client Unified Labeling, i tipi di informazioni riservate personalizzate create nel centro di etichette non vengono inviati.

- Versione del client di Azure Information Protection.

- Versione del sistema operativo del client.

Queste informazioni vengono archiviate in un'area di lavoro di Azure Log Analytics di proprietà dell'organizzazione e possono essere visualizzate, indipendentemente da Azure Information Protection, dagli utenti con i diritti di accesso all'area di lavoro. Per informazioni dettagliate, vedere la sezione [Autorizzazioni necessarie per la funzionalità di analisi di Azure Information Protection](#permissions-required-for-azure-information-protection-analytics). Per informazioni sulla gestione dell'accesso all'area di lavoro, vedere la sezione [Gestire l'accesso all'area di lavoro Log Analytics](https://docs.microsoft.com/azure/azure-monitor/platform/manage-access#manage-access-to-log-analytics-workspace-using-azure-permissions) nella documentazione di Azure.

Per impedire ai client di Azure Information Protection (versione classica) di inviare questi dati, impostare l' [impostazione dei criteri](configure-policy-settings.md) **Invia dati di controllo su Azure Information Protection Analytics** su **disattivato**:

- Per fare in modo che la maggior parte degli utenti possa inviare questi dati e un subset di utenti non possa inviare dati di controllo: 
    - Impostare **Invia dati di controllo a Azure Information Protection Analytics** su **disattivato** in un criterio con ambito per il subset di utenti. Questa configurazione è tipica per gli scenari di produzione.

- Per fare in modo che solo un subset di utenti possa inviare dati di controllo: 
    - Impostare **Invia dati di controllo a Azure Information Protection Analytics** su **disattivato** nei criteri **globali e in** in un criterio con ambito per il subset di utenti. Questa configurazione è tipica per gli scenari di test.

Per evitare che Azure Information Protection client unificati invii questi dati, configurare un' [impostazione avanzata](./rms-client/clientv2-admin-guide-customizations.md#disable-sending-audit-data-to-azure-information-protection-analytics)dei criteri di etichetta.

#### <a name="content-matches-for-deeper-analysis"></a>Corrispondenze di contenuto per un'analisi più approfondita

Azure Information Protection consente di raccogliere e archiviare i dati effettivi identificati come un tipo di informazioni riservate (predefinito o personalizzato). Possono essere inclusi ad esempio numeri di carta di credito, numeri di previdenza sociale, numeri di passaporto e numeri di conto bancario. Le corrispondenze contenuto vengono visualizzate quando si seleziona una voce dai **log attività**e si visualizzano i **Dettagli dell'attività**. 

Per impostazione predefinita, i client di Azure Information Protection non inviano corrispondenze di contenuto. Per modificare questo comportamento in modo che vengano inviate le corrispondenze del contenuto:

- Per il client classico, selezionare una casella di controllo come parte della [configurazione](#configure-a-log-analytics-workspace-for-the-reports) per Azure Information Protection Analytics. La casella di controllo è denominata **Abilita analisi più approfondita nei dati sensibili**.
    
    Se si vuole che la maggior parte degli utenti che usano questo client per inviare corrispondenze di contenuto, ma un subset di utenti non può inviare corrispondenze di contenuto, selezionare la casella di controllo e quindi configurare un' [impostazione client avanzata](./rms-client/client-admin-guide-customizations.md#disable-sending-information-type-matches-for-a-subset-of-users) in un criterio con ambito per il subset di utenti.

- Per il client Unified Labeling, configurare un' [impostazione avanzata](./rms-client/clientv2-admin-guide-customizations.md#send-information-type-matches-to-azure-information-protection-analytics) in un criterio di etichetta.

## <a name="prerequisites"></a>Prerequisiti
Per visualizzare i report di Azure Information Protection e creare report personalizzati, verificare che siano soddisfatti i requisiti seguenti.

|Requisito|Ulteriori informazioni|
|---------------|--------------------|
|Una sottoscrizione di Azure che include Log Analytics ed è per lo stesso tenant di Azure Information Protection|Vedere la pagina dei [prezzi di Monitoraggio di Azure](https://azure.microsoft.com/pricing/details/log-analytics).<br /><br />Se non si dispone di un abbonamento di Azure o attualmente non si usa Azure Log Analytics, la pagina dei prezzi include un collegamento per una versione di valutazione gratuita.|
|Per informazioni sulla creazione di report per l'assegnazione di etichette ai client: <br /><br />-Client Azure Information Protection|Sono supportati sia il client Unified labeling che il client classico. <br /><br />Se non è già installato, è possibile scaricare e installare questi client dall' [area download Microsoft](https://www.microsoft.com/en-us/download/details.aspx?id=53018).|
|Per informazioni sulla creazione di report da archivi dati basati sul cloud: <br /><br />-Microsoft Cloud App Security |Per visualizzare le informazioni da Microsoft Cloud App Security, configurare l' [integrazione di Azure Information Protection](https://docs.microsoft.com/cloud-app-security/azip-integration).|
|Per informazioni sulla creazione di report da archivi dati locali: <br /><br />-Azure Information Protection scanner |Per le istruzioni di installazione per lo scanner, vedere [Distribuzione dello scanner di Azure Information Protection per classificare e proteggere automaticamente i file](deploy-aip-scanner.md). |
|Per informazioni sulla creazione di report da computer Windows 10:  <br /><br />-Compilazione minima di 1809 con Microsoft Defender Advanced Threat Protection (Microsoft Defender ATP)|È necessario abilitare la funzionalità di integrazione Azure Information Protection da Microsoft Defender Security Center. Per altre informazioni, vedere [Panoramica di Information Protection in Windows](/windows/security/threat-protection/microsoft-defender-atp/information-protection-in-windows-overview).|

### <a name="permissions-required-for-azure-information-protection-analytics"></a>Autorizzazioni necessarie per la funzionalità di analisi di Azure Information Protection

Specificatamente per la funzionalità di analisi di Azure Information Protection, dopo aver configurato l'area di lavoro di Azure Log Analytics, è possibile usare il ruolo di amministratore di Azure AD Ruolo con autorizzazioni di lettura per la sicurezza come alternativa ad altri ruoli di Azure AD che supportano la gestione di Azure Information Protection nel portale di Azure.

Poiché questa funzionalità usa Monitoraggio di Azure, il controllo degli accessi in base al ruolo per Azure controlla anche l'accesso all'area di lavoro. È quindi necessario un ruolo di Azure, nonché un ruolo di amministratore di Azure AD per gestire l'analisi di Azure Information Protection. Se non si ha familiarità con i ruoli di Azure, può risultare utile leggere [Differenze tra i ruoli di controllo dell'accesso in base al ruolo di Azure e i ruoli di amministratore di Azure AD](https://docs.microsoft.com/azure/role-based-access-control/rbac-and-directory-admin-roles#differences-between-azure-rbac-roles-and-azure-ad-administrator-roles).

Dettagli:

1. Uno dei [ruoli di amministratore di Azure AD](/azure/active-directory/active-directory-assign-admin-roles-azure-portal) seguenti per accedere al pannello di analisi di Azure Information Protection:
    
    - Per creare l'area di lavoro di Log Analytics o per creare query personalizzate:
    
        - **Amministratore Azure Information Protection**
        - **Amministratore della sicurezza**
        - **Amministratore di conformità**
        - **Amministratore dati di conformità**
        - **Amministratore globale**
    
    - Dopo aver creato l'area di lavoro, è possibile usare i ruoli seguenti con un minor numero di autorizzazioni per visualizzare i dati raccolti:
    
        - **Ruolo con autorizzazioni di lettura per la sicurezza**
        - **Lettore globale**
    
    > [!NOTE] 
    > Non è possibile usare il ruolo di amministratore di Azure Information Protection o il ruolo di lettore globale se il tenant si trova nella [piattaforma di etichettatura unificata](faqs.md#how-can-i-determine-if-my-tenant-is-on-the-unified-labeling-platform).

2. È anche necessario uno dei [ruoli di Azure Log Analytics](https://docs.microsoft.com/azure/azure-monitor/platform/manage-access#manage-access-using-azure-permissions) o dei [ruoli di Azure](https://docs.microsoft.com/azure/role-based-access-control/rbac-and-directory-admin-roles#azure-rbac-roles) standard seguenti per accedere all'area di lavoro di Azure Log Analytics:
    
    - Per creare l'area di lavoro o per creare query personalizzate, uno dei ruoli seguenti:
    
        - **Collaboratore di Log Analytics**
        - **Collaboratore**
        - **Proprietario**
    
    - Dopo aver creato l'area di lavoro, è possibile usare uno dei ruoli seguenti con meno autorizzazioni per visualizzare i dati raccolti:
    
        - **Lettore di Log Analytics**
        - **Lettore**

#### <a name="minimum-roles-to-view-the-reports"></a>Ruoli minimi per visualizzare i report

Dopo aver configurato l'area di lavoro per l'analisi di Azure Information Protection, i ruoli minimi necessari per visualizzare i report di analisi di Azure Information Protection sono i due seguenti:

- Ruolo di amministratore di Azure AD: **Reader di sicurezza**
- Ruolo di Azure: **Reader log Analytics**

Tuttavia, un'assegnazione di ruolo tipica per molte organizzazioni è il **ruolo con autorizzazioni di lettura per la sicurezza** di Azure AD e il ruolo **Lettore** di Azure.

### <a name="storage-requirements-and-data-retention"></a>Requisiti di archiviazione e conservazione dei dati

La quantità di dati raccolti e archiviati nell'area di lavoro di Azure Information Protection varierà in modo significativo per ogni tenant, a seconda di fattori quali il numero di Azure Information Protection client e altri endpoint supportati, indipendentemente dal fatto che si tratti di raccolta dei dati di individuazione degli endpoint, sono stati distribuiti scanner, il numero di documenti protetti a cui si accede e così via.

Tuttavia, come punto di partenza, le stime seguenti potrebbero risultare utili:

- Per i dati di controllo generati solo da client Azure Information Protection: 2 GB per 10.000 utenti attivi al mese.

- Per i dati di controllo generati da client Azure Information Protection, scanner e Microsoft Defender ATP: 20 GB per 10.000 utenti attivi al mese.

Se si usa l'etichettatura obbligatoria o si è configurata un'etichetta predefinita per la maggior parte degli utenti, è probabile che le tariffe siano significativamente più elevate.

I log di monitoraggio di Azure hanno una funzionalità di **utilizzo e costi stimati** che consentono di stimare e controllare la quantità di dati archiviati ed è inoltre possibile controllare il periodo di conservazione dei dati per l'area di lavoro log Analytics. Per altre informazioni, vedere [gestire l'utilizzo e i costi con i log di monitoraggio di Azure](https://docs.microsoft.com/azure/azure-monitor/platform/manage-cost-storage).

## <a name="configure-a-log-analytics-workspace-for-the-reports"></a>Configurare un'area di lavoro di Log Analytics per i report

1. Se non già stato fatto, aprire una nuova finestra del browser e [accedere al portale di Azure](https://portal.azure.com) con un account che dispone delle [autorizzazioni necessarie per le analisi di Azure Information Protection](#permissions-required-for-azure-information-protection-analytics). Quindi passare al pannello **Azure Information Protection**. 
    
    Ad esempio, dal menu hub fare clic su **Tutti i servizi** e iniziare a digitare **Informazioni** nella casella Filtro. Selezionare **Azure Information Protection**.
    
2. Individuare le opzioni del menu **Gestisci** e selezionare **Configura le analisi (anteprima)** .

3. Nel pannello **Log Analytics di Azure Information Protection** viene visualizzato un elenco delle eventuali aree di lavoro di Log Analytics di proprietà del tenant. Effettuare una delle operazioni seguenti:
    
    - Per creare una nuova area di lavoro di Log Analytics: selezionare **Crea nuova area di lavoro**, quindi nel pannello **Area di lavoro di Log Analytics** specificare le informazioni richieste.
    
    - Per usare un'area di lavoro di Log Analytics esistente, selezionare l'area di lavoro dall'elenco.
    
    Per assistenza nella creazione dell'area di lavoro di Log Analytics, vedere [Creare un'area di lavoro di Log Analytics nel portale di Azure](https://docs.microsoft.com/azure/log-analytics/log-analytics-quick-create-workspace).

4. Se si dispone di Azure Information Protection client (versione classica), selezionare la casella di controllo **Abilita analisi più approfondita nei dati sensibili** se si desidera archiviare i dati effettivi identificati come tipo di informazioni riservate. Per ulteriori informazioni su questa impostazione, vedere la sezione [corrispondenze di contenuto per l'analisi più approfondita](#content-matches-for-deeper-analysis) in questa pagina.

5. Selezionare **OK**.

Dopo aver configurato l'area di lavoro, eseguire le operazioni seguenti se si pubblicano le etichette di riservatezza in uno dei seguenti centri di gestione: Office 365 Centro sicurezza e conformità, Centro sicurezza Microsoft 365, Microsoft 365 conformità Center:

- Nella portale di Azure passare a **Azure Information Protection** > **Gestisci**l'**etichetta unificata** >  e selezionare **pubblica**.
    
    Selezionare questa opzione di **pubblicazione** ogni volta che si crea una modifica dell'etichetta (crea, modifica, Elimina) nel centro di etichette. 

A questo punto si è pronti per visualizzare i report.

## <a name="how-to-view-the-reports"></a>Come visualizzare i report

Nel pannello Azure Information Protection trovare le opzioni del menu **Dashboard** e scegliere una delle opzioni seguenti:

- **Report di utilizzo (anteprima)** : usare questo report per vedere come vengono usate le etichette.

- **Log attività (anteprima)** : usare questo report per visualizzare le azioni di etichettatura dagli utenti e per i dispositivi e i percorsi di file. Per i documenti protetti, inoltre, è possibile visualizzare i tentativi di accesso (esito positivo o negativo) per gli utenti all'interno e all'esterno dell'organizzazione, anche se non hanno installato il client di Azure Information Protection
    
    Questo report contiene un'opzione **Colonne** che consente di visualizzare più informazioni sulle attività rispetto alla visualizzazione predefinita. È anche possibile accedere ad altri dettagli su un file selezionandolo per visualizzare **Dettagli attività**.

- **Individuazione dati (anteprima)** : usare questo report per visualizzare le informazioni sui file con etichetta trovati dagli scanner e dagli endpoint supportati.
    
    Suggerimento: dalle informazioni raccolte, è possibile che gli utenti accedano a file che contengono informazioni riservate dal percorso di cui non si è a conoscenza o che non sono in corso di analisi:
    
    - Se le posizioni sono in locale, è consigliabile aggiungerle come ulteriori repository di dati per lo strumento di analisi di Azure Information Protection.
    - Se le posizioni sono nel cloud, è consigliabile usare Microsoft Cloud App Security per gestirle. 
    
- **Raccomandazioni (anteprima)** : usare questo report per identificare i file che contengono informazioni riservate e mitigare il rischio seguendo le raccomandazioni.
    
    Quando si seleziona un elemento, l'opzione **Visualizza i dati** consente di visualizzare le attività di controllo che hanno attivato la raccomandazione.


## <a name="how-to-modify-the-reports-and-create-custom-queries"></a>Come modificare i report e creare query personalizzate

Selezionare l'icona della query nel dashboard per aprire un pannello **Ricerca log**: 

![Icona di Log Analytics per personalizzare i report di Azure Information Protection](./media/log-analytics-icon.png)


I dati registrati per Azure Information Protection vengono archiviati nella tabella seguente: **InformationProtectionLogs_CL**

Per creare query personalizzate, usare i nomi di schema descrittivi implementati come funzioni **InformationProtectionEvents**. Queste funzioni sono derivate dagli attributi supportati per le query personalizzate (alcuni attributi sono solo per uso interno) e i relativi nomi non cambiano nel tempo, neanche se gli attributi sottostanti cambiano in seguito a miglioramenti o nuove funzionalità.

### <a name="friendly-schema-reference-for-event-functions"></a>Riferimenti sui nomi di schema descrittivi per le funzioni di eventi

Usare la tabella seguente per identificare il nome descrittivo delle funzioni di eventi che è possibile usare per le query personalizzate con le funzionalità di analisi di Azure Information Protection.

|Nome della colonna|Description|
|-----------|-----------|
|Accesso|Un documento protetto è stato aperto, identificato dal nome file se è stato rilevato, oppure con ID se non è stato rilevato.|
|AccessDenied|A un documento protetto è stato negato l'accesso, identificato dal nome file, se viene rilevato, oppure con ID se non è stato rilevato.|
|Ora|Ora dell'evento: UTC nel formato AAAA-MM-GGThh: MM: SS|
|Utente|Utente: Format UPN o dominio\utente|
|ItemPath|Percorso dell'elemento completo o oggetto di posta elettronica|
|ItemName|Nome file o oggetto posta elettronica |
|Metodo|Metodo assegnato etichetta: manuale, automatico, consigliato, predefinito o obbligatorio|
|Attività|Attività di controllo: DowngradeLabel, UpgradeLabel, RemoveLabel, NewLabel, Discover, Access, RemoveCustomProtection, ChangeCustomProtection o NewCustomProtection |
|Nomeetichetta|Nome etichetta (non localizzato)|
|LabelNameBefore |Nome etichetta prima della modifica (non localizzato) |
|ProtectionType|Tipo di protezione [JSON] <br />{ <br />"Type": ["Template", "Custom", "DoNotForward"], <br />  "TemplateID": "GUID" <br /> } <br />|
|ProtectionBefore|Tipo di protezione prima della modifica [JSON] |
|InformationTypesMatches|Matrice JSON di [SensitiveInformation](https://docs.microsoft.com/microsoft-365/compliance/what-the-sensitive-information-types-look-for) trovata nei dati in cui una matrice vuota indica che non sono stati trovati tipi di informazioni e null indica che non sono disponibili informazioni|
|MachineName |FQDN quando disponibile; nome host in caso contrario|
|DeviceRisk|Punteggio di rischio del dispositivo da WDATP quando disponibile|
|Piattaforma|Piattaforma del dispositivo (Win, OSX, Android, iOS) |
|ApplicationName|Nome descrittivo dell'applicazione|
|AIPVersion|Versione del client di Azure Information Protection che ha eseguito l'azione di controllo |
|TenantId|ID tenant di Azure AD |
|AzureApplicationId|ID applicazione registrato Azure AD (GUID)|
|ProcessName|Processo che ospita MIP SDK|
|LabelId|GUID etichetta o null|
|IsProtected|Se protetto: Sì/No |
|ProtectionOwner |Proprietario Rights Management in formato UPN|
|LabelIdBefore|GUID etichetta o null prima della modifica|
|InformationTypesAbove55|Matrice JSON di [SensitiveInformation](https://docs.microsoft.com/microsoft-365/compliance/what-the-sensitive-information-types-look-for) trovata nei dati con livello di confidenza 55 o superiore |
|InformationTypesAbove65|Matrice JSON di [SensitiveInformation](https://docs.microsoft.com/microsoft-365/compliance/what-the-sensitive-information-types-look-for) trovata nei dati con livello di confidenza 65 o superiore |
|InformationTypesAbove75|Matrice JSON di [SensitiveInformation](https://docs.microsoft.com/microsoft-365/compliance/what-the-sensitive-information-types-look-for) trovata nei dati con livello di confidenza 75 o superiore |
|InformationTypesAbove85|Matrice JSON di [SensitiveInformation](https://docs.microsoft.com/microsoft-365/compliance/what-the-sensitive-information-types-look-for) trovata nei dati con livello di confidenza 85 o superiore |
|InformationTypesAbove95|Matrice JSON di [SensitiveInformation](https://docs.microsoft.com/microsoft-365/compliance/what-the-sensitive-information-types-look-for) trovata nei dati con livello di confidenza 95 o superiore|
|DiscoveredInformationTypes |Matrice JSON di [SensitiveInformation](https://docs.microsoft.com/microsoft-365/compliance/what-the-sensitive-information-types-look-for) trovata nei dati e il relativo contenuto corrispondente (se abilitato) in cui una matrice vuota indica che non sono stati trovati tipi di informazioni e null indica che non sono disponibili informazioni |
|ProtectedBefore|Se il contenuto è stato protetto prima della modifica: Sì/No |
|ProtectionOwnerBefore|Proprietario Rights Management prima della modifica |
|UserJustification|Giustificazione durante il downgrade o la rimozione dell'etichetta|
|LastModifiedBy|Utente in formato UPN che ha eseguito l'ultima modifica al file. Disponibile solo per Office e SharePoint Online|
|LastModifiedDate|UTC nel formato AAAA-MM-GGThh: MM: SS: disponibile solo per Office & SharePoint Online |


#### <a name="examples-using-informationprotectionevents"></a>Esempi di utilizzo di InformationProtectionEvents

Gli esempi seguenti mostrano come è possibile usare lo schema descrittivo per creare query personalizzate.

##### <a name="example-1-return-all-users-who-sent-audit-data-in-the-last-31-days"></a>Esempio 1: restituire tutti gli utenti che hanno inviato i dati di controllo negli ultimi 31 giorni 

```
InformationProtectionEvents 
| where Time > ago(31d) 
| distinct User 
```

 
##### <a name="example-2-return-the-number-of-labels-that-were-downgraded-per-day-in-the-last-31-days"></a>Esempio 2: restituire il numero di etichette di cui è stato effettuato il downgrade al giorno negli ultimi 31 giorni 


```
InformationProtectionEvents 
| where Time > ago(31d) 
| where Activity == "DowngradeLabel"  
| summarize Label_Downgrades_per_Day = count(Activity) by bin(Time, 1d) 
 
```
 
##### <a name="example-3-return-the-number-of-labels-that-were-downgraded-from-confidential-by-user-in-the-last-31-days"></a>Esempio 3: restituire il numero di etichette di cui è stato effettuato il downgrade da Confidential by User negli ultimi 31 giorni 

```

InformationProtectionEvents 
| where Time > ago(31d) 
| where Activity == "DowngradeLabel"  
| where LabelNameBefore contains "Confidential" and LabelName !contains "Confidential"  
| summarize Label_Downgrades_by_User = count(Activity) by User | sort by Label_Downgrades_by_User desc 

```

In questo esempio, un'etichetta di cui è stato effettuato il downgrade viene conteggiata solo se il nome dell'etichetta prima dell'azione conteneva il nome **Confidential** e il nome dell'etichetta dopo l'azione non conteneva il nome **Confidential**. 


## <a name="next-steps"></a>Passaggi successivi
Una volta esaminate le informazioni nei report, se si utilizza il client di Azure Information Protection, è possibile decidere di apportare modifiche ai criteri di Azure Information Protection. Per istruzioni, vedere [Configurazione dei criteri di Azure Information Protection](configure-policy.md).

Se è disponibile un abbonamento a Microsoft 365, è anche possibile visualizzare l'utilizzo delle etichette nel Centro sicurezza Microsoft 365 e nel Centro conformità Microsoft 365. Per altre informazioni, vedere [Visualizzare l'utilizzo delle etichette con Analisi delle etichette](/microsoft-365/compliance/label-analytics).
