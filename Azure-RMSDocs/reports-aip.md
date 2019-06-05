---
title: Reporting centralizzato per Azure Information Protection
description: Come usare il reporting centralizzato per monitorare l'adozione delle etichette di Azure Information Protection e trovare i file che contengono informazioni riservate
author: cabailey
ms.author: cabailey
ms.date: 06/05/2019
manager: barbkess
ms.topic: article
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: b2da2cdc-74fd-4bfb-b3c2-2a3a59a6bf2e
ms.reviewer: lilukov
ms.suite: ems
ms.openlocfilehash: 500786b518f5d95c464d4538a3d8bdefd030a3eb
ms.sourcegitcommit: 746bb029d185ac13f36482bb9a39200ab5445dbe
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/04/2019
ms.locfileid: "66507167"
---
# <a name="central-reporting-for-azure-information-protection"></a>Reporting centralizzato per Azure Information Protection

>*Si applica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*

> [!NOTE]
> Al momento questa funzionalità è disponibile in anteprima ed è soggetta a modifiche.

Usare le funzionalità di analisi di Azure Information Protection per generare report centralizzati che aiutano a tenere traccia dell'adozione delle etichette di Azure Information Protection. Inoltre:

- Monitorare documenti e messaggi di posta elettronica etichettati e protetti nell'organizzazione.

- Identificare i documenti che contengono informazioni riservate nell'organizzazione.

- Monitorare l'accesso degli utenti a documenti e messaggi di posta elettronica etichettati e tenere traccia delle modifiche alla classificazione dei documenti.

- Identificare i documenti contenenti informazioni sensibili che possono mettere a rischio l'organizzazione se non protette e attenuare il rischio seguendo le raccomandazioni.

I dati visualizzati vengono aggregati dal client Azure Information Protection e gli scanner Azure Information Protection, i computer Windows che eseguono [Microsoft Defender Advanced Threat Protection (ATP Defender Microsoft)](/windows/security/threat-protection/microsoft-defender-atp/overview)e dal [i client che supportano l'etichettatura unificata](configure-policy-migrate-labels.md#clients-and-services-that-support-unified-labeling).

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
    
    - Quali azioni di etichettatura sono state eseguite da un'applicazione specifica, ad esempio Esplora file e clic con il pulsante destro del mouse o il modulo di PowerShell AzureInformationProtection
    
    - Eseguire il drill-down dei file segnalati per visualizzare la sezione **Dettagli attività** in cui sono disponibili altre informazioni

- Nel report **Individuazione dati**:

    - Quali file sono nel repository dei dati analizzati, Windows 10 computer o i computer che eseguono il client Azure Information Protection o [i client che supportano l'etichettatura unificato](configure-policy-migrate-labels.md#clients-and-services-that-support-unified-labeling)
    
    - Quali file sono provvisti di etichetta e protetti e il percorso dei file in base alle etichette
    
    - Quali file contengono informazioni riservate per categorie note, ad esempio dati finanziari e informazioni personali e il percorso dei file in base a queste categorie

- Dal report **Raccomandazioni**:
    
    - Identificare i file non protetti che contengono un tipo noto di informazioni sensibili. Una raccomandazione consente di configurare immediatamente la condizione corrispondente a una delle etichette, per applicare l'etichettatura automatica o consigliata.
        
        Se si segue la raccomandazione: la volta successiva che i file vengono aperti da un utente o analizzati dallo scanner di Azure Information Protection, i file possono essere classificati e protetti automaticamente.
    
    - Identificare i repository dei dati che contengono file con informazioni sensibili identificate ma non analizzati da Azure Information Protection. Una raccomandazione consente di aggiungere immediatamente l'archivio dati identificato a uno dei profili dello scanner.
        
        Se si segue la raccomandazione: al ciclo successivo dello scanner, i file possono essere classificati e protetti automaticamente.

I report usano [Monitoraggio di Azure](/azure/log-analytics/log-analytics-overview) per archiviare i dati in un'area di lavoro di Log Analytics di proprietà dell'organizzazione. Se si ha familiarità con il linguaggio di query, è possibile modificare le query e creare nuovi report e dashboard di Power BI. L'esercitazione seguente può risultare utile per la comprensione del linguaggio di query: [Introduzione alle query in Monitoraggio di Azure](/azure/azure-monitor/log-query/get-started-queries).

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

- Per i documenti: Percorso e nome file dei documenti ai quali viene aggiunta l'etichetta.

- Per i messaggi di posta elettronica: Oggetto e mittente del messaggio di posta elettronica per i messaggi con etichetta. 

- Tipologie di informazioni riservate ([predefinite](https://docs.microsoft.com/office365/securitycompliance/what-the-sensitive-information-types-look-for) e personalizzate) rilevate nel contenuto.

- Versione del client di Azure Information Protection.

- Versione del sistema operativo del client.

Queste informazioni vengono archiviate in un'area di lavoro di Azure Log Analytics di proprietà dell'organizzazione e possono essere visualizzate, indipendentemente da Azure Information Protection, dagli utenti con i diritti di accesso all'area di lavoro. Per informazioni dettagliate, vedere la sezione [Autorizzazioni necessarie per la funzionalità di analisi di Azure Information Protection](#permissions-required-for-azure-information-protection-analytics). Per informazioni sulla gestione dell'accesso all'area di lavoro, vedere la sezione [Gestire l'accesso all'area di lavoro Log Analytics](https://docs.microsoft.com/azure/azure-monitor/platform/manage-access#manage-access-to-log-analytics-workspace-using-azure-permissions) nella documentazione di Azure.

Per impedire ai client di Azure Information Protection di inviare questi dati, configurare l'[impostazione dei criteri](configure-policy-settings.md) **Invia i dati di controllo a Log Analytics di Azure Information Protection** su **No**:

- Per fare in modo che la maggior parte degli utenti possa inviare questi dati e un subset di utenti non possa inviare dati di controllo: 
    - Impostare **Invia i dati di controllo a Log Analytics di Azure Information Protection** su **No** in un criterio con ambito per il subset di utenti. Questa configurazione è tipica per gli scenari di produzione.

- Per fare in modo che solo un subset di utenti possa inviare dati di controllo: 
    - Impostare **Invia i dati di controllo a Log Analytics di Azure Information Protection** su **No** nei criteri globali e su **Sì** in un criterio con ambito per il subset di utenti. Questa configurazione è tipica per gli scenari di test.

#### <a name="content-matches-for-deeper-analysis"></a>Corrispondenze di contenuto per un'analisi più approfondita 

L'area di lavoro Log Analytics di Azure per Azure Information Protection include una casella di controllo che consente di raccogliere e archiviare anche i dati identificati dai tipi di informazioni riservate o da condizioni personalizzate. Possono essere inclusi ad esempio numeri di carta di credito, numeri di previdenza sociale, numeri di passaporto e numeri di conto bancario. Se non si vogliono inviare questi dati aggiuntivi, non selezionare questa casella di controllo. Se si vuole che la maggior parte degli utenti possa inviare i dati aggiuntivi e un subset di utenti non possa inviarli, selezionare la casella di controllo e configurare un'[impostazione client avanzata](./rms-client/client-admin-guide-customizations.md#disable-sending-information-type-matches-for-a-subset-of-users) in un criterio con ambito per il subset di utenti.

Dopo la raccolta, le corrispondenze del contenuto vengono visualizzate nei report quando si esegue il drill-down nei file dai log attività, per visualizzare i **Dettagli attività**. Queste informazioni possono essere anche visualizzate e recuperate tramite query.

## <a name="prerequisites"></a>Prerequisiti
Per visualizzare i report di Azure Information Protection e creare report personalizzati, verificare che siano soddisfatti i requisiti seguenti.

|Requisito|Altre informazioni|
|---------------|--------------------|
|Una sottoscrizione di Azure che include Log Analytics ed è per lo stesso tenant di Azure Information Protection|Vedere la pagina dei [prezzi di Monitoraggio di Azure](https://azure.microsoft.com/pricing/details/log-analytics).<br /><br />Se non si dispone di un abbonamento di Azure o attualmente non si usa Azure Log Analytics, la pagina dei prezzi include un collegamento per una versione di valutazione gratuita.|
|Il client Azure Information Protection o il client di assegnazione di etichette unificato di Azure Information Protection|Se non si ha già uno di questi client, è possibile scaricare e installare dal [Microsoft Download Center](https://www.microsoft.com/en-us/download/details.aspx?id=53018). <br /><br /> Assicurarsi di avere la versione più recente per supportare [tutte le funzionalità](#features-that-require-a-minimum-version-of-the-client) per analitica di Azure Information Protection.|
|Per il report **Individuazione e rischio**: <br /><br />-Per visualizzare i dati da archivi dati locali, è stato distribuito almeno un'istanza dello scanner Azure Information Protection <br /><br />-Per visualizzare i dati dai computer Windows 10, devono essere una build minima di 1809 e si usa Microsoft Defender Advanced Threat Protection (Microsoft Defender ATP) è stata abilitata la funzionalità di integrazione di Azure Information Protection da Microsoft Defender Security Center|Per le istruzioni di installazione per lo scanner, vedere [Distribuzione dello scanner di Azure Information Protection per classificare e proteggere automaticamente i file](deploy-aip-scanner.md). <br /><br />Per informazioni sulla configurazione e Usa la funzionalità di integrazione di Azure Information Protection da Microsoft Defender Security Center, vedere [protezione delle informazioni nella panoramica di Windows](/windows/security/threat-protection/microsoft-defender-atp/information-protection-in-windows-overview).|
|Per il report **Raccomandazioni**: <br /><br />-Per aggiungere un nuovo repository dei dati dal portale di Azure come un'azione consigliata, è necessario usare la versione più recente di disponibilità a livello generale dello scanner Azure Information Protection |Per distribuire lo scanner, vedere [distribuzione dello scanner di Azure Information Protection per classificare e proteggere i file automaticamente](deploy-aip-scanner.md).|

### <a name="permissions-required-for-azure-information-protection-analytics"></a>Autorizzazioni necessarie per la funzionalità di analisi di Azure Information Protection

Specificatamente per la funzionalità di analisi di Azure Information Protection, dopo aver configurato l'area di lavoro di Azure Log Analytics, è possibile usare il ruolo di amministratore di Azure AD Ruolo con autorizzazioni di lettura per la sicurezza come alternativa ad altri ruoli di Azure AD che supportano la gestione di Azure Information Protection nel portale di Azure.

Poiché questa funzionalità usa Monitoraggio di Azure, il controllo degli accessi in base al ruolo per Azure controlla anche l'accesso all'area di lavoro. È quindi necessario un ruolo di Azure, nonché un ruolo di amministratore di Azure AD per gestire l'analisi di Azure Information Protection. Se non si ha familiarità con i ruoli di Azure, può risultare utile leggere [Differenze tra i ruoli di controllo dell'accesso in base al ruolo di Azure e i ruoli di amministratore di Azure AD](https://docs.microsoft.com/azure/role-based-access-control/rbac-and-directory-admin-roles#differences-between-azure-rbac-roles-and-azure-ad-administrator-roles).

Dettagli:

1. Uno dei [ruoli di amministratore di Azure AD](/azure/active-directory/active-directory-assign-admin-roles-azure-portal) seguenti per accedere al pannello di analisi di Azure Information Protection:
    
    - Per creare l'area di lavoro di Log Analytics o per creare query personalizzate:
    
        - **Amministratori di Azure Information Protection**
        - **Amministratore della sicurezza**
        - **Amministratore di conformità**
        - **Amministratore globale**
    
    - Dopo aver creato l'area di lavoro, è possibile usare il ruolo seguente con meno autorizzazioni per visualizzare i dati raccolti:
    
        - **Ruolo con autorizzazioni di lettura per la sicurezza**
    
    > [!NOTE] 
    > Se il tenant è stato migrato allo store unificato l'assegnazione di etichette, è possibile usare il ruolo di amministratore di Azure Information Protection. [Altre informazioni](configure-policy-migrate-labels.md#important-information-about-administrative-roles)

2. È anche necessario uno dei [ruoli di Azure Log Analytics](https://docs.microsoft.com/en-us/azure/azure-monitor/platform/manage-access#manage-access-to-log-analytics-workspace-using-azure-permissions) o dei [ruoli di Azure](https://docs.microsoft.com/azure/role-based-access-control/overview#role-assignments) standard seguenti per accedere all'area di lavoro di Azure Log Analytics:
    
    - Per creare l'area di lavoro o per creare query personalizzate, uno dei ruoli seguenti:
    
        - **Collaboratore di Log Analytics**
        - **Collaboratore**
        - **Proprietario**
    
    - Dopo aver creato l'area di lavoro, è possibile usare uno dei ruoli seguenti con meno autorizzazioni per visualizzare i dati raccolti:
    
        - **Lettore di Log Analytics**
        - **Lettore**

#### <a name="minimum-roles-to-view-the-reports"></a>Ruoli minimi per visualizzare i report

Dopo aver configurato l'area di lavoro per l'analisi di Azure Information Protection, i ruoli minimi necessari per visualizzare i report di analisi di Azure Information Protection sono i due seguenti:

- Ruolo di amministratore di Azure AD: **Ruolo con autorizzazioni di lettura per la sicurezza**
- Ruolo di Azure: **Lettore di Log Analytics**

Tuttavia, un'assegnazione di ruolo tipica per molte organizzazioni è il **ruolo con autorizzazioni di lettura per la sicurezza** di Azure AD e il ruolo **Lettore** di Azure.

### <a name="features-that-require-a-minimum-version-of-the-client"></a>Funzionalità che richiedono una versione minima del client

È possibile usare le informazioni sulla cronologia di versione per il [unificata di Azure Information Protection client l'assegnazione di etichette](./rms-client/unifiedlabelingclient-version-release-history.md) e il [client Azure Information Protection](./rms-client/client-version-release-history.md) per verificare se la versione del client supporta tutte le funzionalità di creazione di report centrale. Le versioni minime per i client:

Per Azure Information Protection unified client l'assegnazione di etichette:

- Supporto per il controllo e l'endpoint di individuazione: Versione 2.0.778.0

Per il client Azure Information Protection:

- Supporto per il controllo: Versione 1.41.51.0
- Supporto per l'individuazione di endpoint: Versione 1.48.204.0

### <a name="storage-requirements-and-data-retention"></a>Conservazione dei dati e i requisiti di archiviazione

La quantità di dati raccolti e archiviati nell'area di lavoro di Azure Information Protection varia in modo significativo per ogni tenant, a seconda di fattori, ad esempio come molti client Azure Information Protection e altri endpoint supportati sono, che tu sia la raccolta dati di individuazione di endpoint, distribuiti gli scanner e così via.

Tuttavia, come punto di partenza, è possibile trovare le stime seguenti utili:

- Per i dati di controllo generati da solo i client di Azure Information Protection: 2 GB per ogni 10.000 utenti attivi al mese.

- Per i dati di controllo generati dal client Azure Information Protection scanner e Microsoft Defender ATP: 20 GB per ogni 10.000 utenti attivi al mese.

Se si usa l'etichettatura obbligatoria o è stata configurata un'etichetta predefinita nei criteri globali, le tariffe possono risultare significativamente più elevata.

Log di monitoraggio di Azure è un **informazioni sull'utilizzo e costi stimati** funzionalità che consentono di stimare e verificare la quantità di dati archiviati in ed è anche possibile controllare il periodo di conservazione dati per l'area di lavoro di Log Analitica. Per altre informazioni, vedere [gestire i costi con i log di monitoraggio di Azure e sull'utilizzo](https://docs.microsoft.com/azure/azure-monitor/platform/manage-cost-storage).

## <a name="configure-a-log-analytics-workspace-for-the-reports"></a>Configurare un'area di lavoro di Log Analytics per i report

1. Se non già stato fatto, aprire una nuova finestra del browser e [accedere al portale di Azure](https://portal.azure.com) con un account che dispone delle [autorizzazioni necessarie per le analisi di Azure Information Protection](#permissions-required-for-azure-information-protection-analytics). Quindi passare al pannello **Azure Information Protection**. 
    
    Ad esempio, dal menu hub fare clic su **Tutti i servizi** e iniziare a digitare **Informazioni** nella casella Filtro. Selezionare **Azure Information Protection**.
    
2. Individuare le opzioni del menu **Gestisci** e selezionare **Configura le analisi (anteprima)** .

3. Nel pannello **Log Analytics di Azure Information Protection** viene visualizzato un elenco delle eventuali aree di lavoro di Log Analytics di proprietà del tenant. Eseguire una delle operazioni seguenti:
    
    - Per creare una nuova area di lavoro di Log Analytics: Selezionare **Crea nuova area di lavoro** e specificare le informazioni richieste nel pannello **Area di lavoro di Log Analytics**.
    
    - Per usare un'area di lavoro di Log Analytics già esistente: Selezionare l'area di lavoro dall'elenco.

Per assistenza nella creazione dell'area di lavoro di Log Analytics, vedere [Creare un'area di lavoro di Log Analytics nel portale di Azure](https://docs.microsoft.com/azure/log-analytics/log-analytics-quick-create-workspace).

Quando viene completata la configurazione dell'area di lavoro si è pronti per visualizzare i report.

> [!NOTE] 
> Esiste attualmente un problema noto con la visualizzazione dei dati per la prima volta nei report. Se si verifica questo problema, nei criteri globali configurare l'[impostazione dei criteri](configure-policy-settings.md) **Invia i dati di controllo a Log Analytics di Azure Information Protection** su **No** e salvare il criterio. Modificare quindi la stessa impostazione specificando **Sì** e salvare il criterio. Dopo il [download della modifica](configure-policy.md#making-changes-to-the-policy) da parte dei client, possono essere richiesti fino a 30 minuti prima che gli eventi di controllo diventino visibili nell'area di lavoro Log Analytics.

## <a name="how-to-view-the-reports"></a>Come visualizzare i report

Nel pannello Azure Information Protection trovare le opzioni del menu **Dashboard** e scegliere una delle opzioni seguenti:

- **Report di utilizzo (anteprima)** : usare questo report per vedere come vengono usate le etichette.

- **Log attività (anteprima)** : usare questo report per visualizzare le azioni di etichettatura dagli utenti e per i dispositivi e i percorsi di file.
    
    Questo report contiene un'opzione **Colonne** che consente di visualizzare più informazioni sulle attività rispetto alla visualizzazione predefinita. È anche possibile accedere ad altri dettagli su un file selezionandolo per visualizzare **Dettagli attività**.

- **Individuazione dei dati (anteprima)** : usare questo report per visualizzare informazioni sui file etichettati trovati dagli strumenti di analisi e dagli endpoint supportati.
    
    È possibile configurare un [impostazione client avanzata](./rms-client/client-admin-guide-customizations.md#enable-azure-information-protection-analytics-to-discover-sensitive-information-in-documents) per il client Azure Information Protection ai file di report contenenti informazioni riservate.
    
    Suggerimento: dalle informazioni raccolte si potrebbero individuare utenti che accedono a file contenenti informazioni riservate da posizioni di cui non si conosceva l'esistenza o che non vengono attualmente analizzate:
    
    - Se le posizioni sono in locale, è consigliabile aggiungerle come ulteriori repository di dati per lo strumento di analisi di Azure Information Protection.
    - Se le posizioni sono nel cloud, è consigliabile usare Microsoft Cloud App Security per gestirle. 
    
- **Raccomandazioni (anteprima)** : usare questo report per identificare i file che contengono informazioni sensibili e attenuare il rischio seguendo le raccomandazioni.
    
    Quando si seleziona un elemento, l'opzione **Visualizza i dati** consente di visualizzare le attività di controllo che hanno attivato la raccomandazione.


## <a name="how-to-modify-the-reports-and-create-custom-queries"></a>Come modificare i report e creare query personalizzate

Selezionare l'icona della query nel dashboard per aprire un pannello **Ricerca log**: 

![Icona di Log Analytics per personalizzare i report di Azure Information Protection](./media/log-analytics-icon.png)


I dati registrati per Azure Information Protection vengono archiviati nella tabella seguente: **InformationProtectionLogs_CL**

Per creare query personalizzate, usare i nomi di schema descrittivi implementati come funzioni **InformationProtectionEvents**. Queste funzioni sono derivate dagli attributi supportati per le query personalizzate (alcuni attributi sono solo per uso interno) e i relativi nomi non cambiano nel tempo, neanche se gli attributi sottostanti cambiano in seguito a miglioramenti o nuove funzionalità.

### <a name="friendly-schema-reference-for-event-functions"></a>Riferimenti sui nomi di schema descrittivi per le funzioni di eventi

Usare la tabella seguente per identificare il nome descrittivo delle funzioni di eventi che è possibile usare per le query personalizzate con le funzionalità di analisi di Azure Information Protection.

|Nome della colonna|Descrizione|
|-----------|-----------|
|Time|Ora dell'evento: Ora UTC nel formato AAAA-MM-ggTHH|
|Utente|Utente: Formato UPN o dominio\utente.|
|ItemPath|Oggetto del percorso o indirizzo di posta elettronica completo dell'elemento|
|ItemName|Oggetto del messaggio di posta elettronica o nome di file |
|Metodo|Etichetta assegnato metodo: Manuale, automatico, consigliato, predefinito o obbligatoria|
|Attività|Attività di controllo: DowngradeLabel, UpgradeLabel, RemoveLabel, NewLabel, individuare, accesso, RemoveCustomProtection, ChangeCustomProtection o NewCustomProtection |
|LabelName|Nome con etichetta (non localizzato)|
|LabelNameBefore |Nome dell'etichetta prima della modifica (non localizzato) |
|ProtectionType|Tipo di protezione dati [JSON] <br />{ <br />"Type": ["Template", "Custom", "DoNotForward"], <br />  "TemplateID": "GUID" <br /> } <br />|
|ProtectionBefore|Tipo di protezione dati prima della modifica di [JSON] |
|InformationTypesMatches|Matrice JSON dei [SensitiveInformation](https://docs.microsoft.com/office365/securitycompliance/what-the-sensitive-information-types-look-for) non trovati nei dati in una matrice vuota non indica nessun tipo di informazioni trovato e null significa che sono disponibili informazioni|
|MachineName |Nome di dominio completo quando è disponibile. in caso contrario, nome host|
|DeviceRisk|Punteggio di rischio di dispositivo da WDATP quando è disponibile|
|Piattaforma|Piattaforma del dispositivo (Windows, OSX, Android, iOS) |
|ApplicationName|Nome descrittivo dell'applicazione|
|AIPVersion|Versione del client Azure Information Protection che ha eseguito l'azione di controllo |
|TenantId|ID tenant di Azure AD |
|AzureApplicationId|ID (GUID) dell'applicazione registrati in Azure AD|
|ProcessName|Processo che ospita Microsoft Information Protection SDK|
|LabelId|Etichetta GUID o null|
|IsProtected|Se la protezione: Sì/No |
|ProtectionOwner |Proprietario di Rights Management in formato UPN|
|LabelIdBefore|Etichetta GUID o null prima della modifica|
|InformationTypesAbove55|Matrice JSON dei [SensitiveInformation](https://docs.microsoft.com/office365/securitycompliance/what-the-sensitive-information-types-look-for) trovati nei dati con livello di confidenza 55 o versione successiva |
|InformationTypesAbove65|Matrice JSON dei [SensitiveInformation](https://docs.microsoft.com/office365/securitycompliance/what-the-sensitive-information-types-look-for) trovati nei dati con livello di confidenza 65 o versioni successive |
|InformationTypesAbove75|Matrice JSON dei [SensitiveInformation](https://docs.microsoft.com/office365/securitycompliance/what-the-sensitive-information-types-look-for) trovati nei dati con livello di confidenza 75 o versioni successive |
|InformationTypesAbove85|Matrice JSON dei [SensitiveInformation](https://docs.microsoft.com/office365/securitycompliance/what-the-sensitive-information-types-look-for) trovati nei dati con livello di confidenza 85 o versione successiva |
|InformationTypesAbove95|Matrice JSON dei [SensitiveInformation](https://docs.microsoft.com/office365/securitycompliance/what-the-sensitive-information-types-look-for) trovati nei dati con il livello di confidenza 95 o successiva|
|DiscoveredInformationTypes |Matrice JSON dei [SensitiveInformation](https://docs.microsoft.com/office365/securitycompliance/what-the-sensitive-information-types-look-for) trovato nei dati e il loro contenuto corrispondente (se abilitati) in una matrice vuota non indica i tipi di informazioni trovati e null significa che non sono disponibili informazioni |
|ProtectedBefore|Indica se il contenuto protetto prima di modifica: Sì/No |
|ProtectionOwnerBefore|Proprietario di Rights Management prima della modifica |
|UserJustification|Giustificazione quando si effettua il downgrade o la rimozione di etichetta|
|LastModifiedBy|Utente in formato UPN che ha modificato il file. Disponibili per Office e SharePoint Online solo|
|LastModifiedDate|Ora UTC nel formato AAAA-MM-ggTHH: Disponibili per Office e SharePoint Online solo |


#### <a name="examples-using-informationprotectionevents"></a>Esempi di utilizzo di InformationProtectionEvents

Gli esempi seguenti mostrano come è possibile usare lo schema descrittivo per creare query personalizzate.

##### <a name="example-1-return-all-users-who-sent-audit-data-in-the-last-31-days"></a>Esempio 1: Restituire tutti gli utenti che hanno inviato dati di controllo negli ultimi 31 giorni 

```
InformationProtectionEvents 
| where Time > ago(31d) 
| distinct User 
```

 
##### <a name="example-2-return-the-number-of-labels-that-were-downgraded-per-day-in-the-last-31-days"></a>Esempio 2: Restituire il numero di etichette di cui è stato effettuato il downgrade ogni giorno negli ultimi 31 giorni 


```
InformationProtectionEvents 
| where Time > ago(31d) 
| where Activity == "DowngradeLabel"  
| summarize Label_Downgrades_per_Day = count(Activity) by bin(Time, 1d) 
 
```
 
##### <a name="example-3-return-the-number-of-labels-that-were-downgraded-from-confidential-by-user-in-the-last-31-days"></a>Esempio 3: Restituire il numero di etichette di cui è stato effettuato il downgrade da Confidential da User negli ultimi 31 giorni 

```

InformationProtectionEvents 
| where Time > ago(31d) 
| where Activity == "DowngradeLabel"  
| where LabelNameBefore contains "Confidential" and LabelName !contains "Confidential"  
| summarize Label_Downgrades_by_User = count(Activity) by User | sort by Label_Downgrades_by_User desc 

```

In questo esempio, un'etichetta di cui è stato effettuato il downgrade viene conteggiata solo se il nome dell'etichetta prima dell'azione conteneva il nome **Confidential** e il nome dell'etichetta dopo l'azione non conteneva il nome **Confidential**. 


## <a name="next-steps"></a>Passaggi successivi
Dopo aver esaminato le informazioni nei report, se si usa il client Azure Information Protection, è possibile decidere di apportare modifiche ai criteri di Azure Information Protection. Per istruzioni, vedere [Configurazione dei criteri di Azure Information Protection](configure-policy.md).

Se è disponibile un abbonamento a Microsoft 365, è anche possibile visualizzare l'utilizzo delle etichette nel Centro sicurezza Microsoft 365 e nel Centro conformità Microsoft 365. Per altre informazioni, vedere [Visualizzare l'utilizzo delle etichette con Analisi delle etichette](/Office365/SecurityCompliance/label-analytics).
