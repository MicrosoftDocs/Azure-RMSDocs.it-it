---
title: Reporting centralizzato per Azure Information Protection
description: Come usare il reporting centralizzato per monitorare l'adozione delle etichette di Azure Information Protection e trovare i file che contengono informazioni riservate
author: batamig
ms.author: bagol
ms.date: 03/01/2021
manager: rkarlin
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: b2da2cdc-74fd-4bfb-b3c2-2a3a59a6bf2e
ms.subservice: analytics
ms.reviewer: lilukov
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 4c42dccc21235fe403f3c491491e0a03e015c890
ms.sourcegitcommit: 7420cf0200c90687996124424a254c289b11a26f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/04/2021
ms.locfileid: "101844337"
---
# <a name="central-reporting-for-azure-information-protection-public-preview"></a>Reporting centrale per Azure Information Protection (anteprima pubblica)

>***Si applica a**: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*
>
>***Rilevante per**: [Client di etichettatura unificata e client classico di AIP](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

>[!NOTE] 
> Per offrire un'esperienza per i clienti unificata e semplificata, il **client classico di Azure Information Protection** e **Gestione etichette** nel portale di Azure saranno **deprecati** a partire dal **31 marzo 2021**. In questo intervallo di tempo tutti i clienti correnti di Azure Information Protection possono passare alla soluzione di etichettatura unificata usando la piattaforma di etichettatura unificata di Microsoft Information Protection. Altre informazioni nell'[avviso ufficiale sulla deprecazione](https://aka.ms/aipclassicsunset).

Usare Azure Information Protection Analytics per la creazione di report centrali che consentono di tenere traccia dell'adozione delle etichette che classificano e proteggono i dati dell'organizzazione. Inoltre:

- Monitorare documenti e messaggi di posta elettronica etichettati e protetti nell'organizzazione.

- Identificare i documenti che contengono informazioni riservate nell'organizzazione.

- Monitorare l'accesso degli utenti a documenti e messaggi di posta elettronica etichettati e tenere traccia delle modifiche alla classificazione dei documenti.

- Identificare i documenti contenenti informazioni sensibili che possono mettere a rischio l'organizzazione se non protette e attenuare il rischio seguendo le raccomandazioni.

- Individuare i casi in cui l'accesso ai documenti protetti viene eseguito da utenti interni o esterni da computer Windows e se l'accesso è stato concesso o negato.

I dati visualizzati sono aggregati da client e scanner di Azure Information Protection, da Microsoft Cloud App Security, da computer Windows 10 che usano Microsoft Defender Advanced Threat Protection e dai [log di utilizzo della protezione](log-analyze-usage.md). 

Azure Information Protection Analytics per la creazione di report centrali è attualmente in fase di anteprima. Le [condizioni aggiuntive per l'anteprima di Azure](https://azure.microsoft.com/support/legal/preview-supplemental-terms/) includono termini legali aggiuntivi che si applicano a funzionalità di Azure in versione beta, anteprima o diversamente non ancora disponibili a livello generale. 


## <a name="aip-reporting-data"></a>Dati di report AIP

Ad esempio, il Azure Information Protection Analytics per Reporting centrale Visualizza i dati seguenti:

|Report  |Dati di esempio visualizzati |
|---------|---------|
|**Report Uso**     |  Selezionare un periodo di tempo per mostrare uno dei seguenti elementi: <br /><br />     -Quali etichette vengono applicate <br /><br />-Quanti documenti e messaggi di posta elettronica vengono etichettati <br /><br />-Il numero di documenti e messaggi di posta elettronica protetti <br /><br />-Quanti utenti e quanti dispositivi sono contrassegnati da documenti e messaggi di posta elettronica <br /><br />-Quali applicazioni vengono utilizzate per l'assegnazione di etichette     |
|**Log attività**     | Selezionare un periodo di tempo per mostrare uno dei seguenti elementi: <br /><br />      -Quali file individuati in precedenza dallo scanner sono stati eliminati dal repository analizzato <br /> <br /> -Quali azioni di etichettatura sono state eseguite da un utente specifico <br /><br /> -Quali azioni di etichettatura sono state eseguite da un dispositivo specifico<br /> <br />    -Quali utenti hanno eseguito l'accesso a un documento con etichetta specifico<br /> <br />-Quali azioni di etichettatura sono state eseguite per un percorso di file specifico<br /> <br />-Quali azioni di etichettatura sono state eseguite da un'applicazione specifica, ad esempio Esplora file e con il pulsante destro del mouse, PowerShell, lo scanner o Microsoft Cloud App Security <br /> <br />-I documenti protetti a cui è stato effettuato l'accesso dagli utenti o hanno negato l'accesso agli utenti, anche se tali utenti non hanno il client di Azure Information Protection installato o non sono all'interno dell'organizzazione <br /> <br />-Eseguire il drill-down nei file segnalati per visualizzare **i dettagli dell'attività** per altre informazioni      |
|**Report di individuazione dati**     |      -Quali file si trovano nei repository di dati scansionati, nei computer Windows 10 o nei computer che eseguono i client di Azure Information Protection <br /><br />-Quali file sono contrassegnati e protetti e il percorso dei file in base alle etichette <br /><br />-Quali file contengono informazioni riservate per le categorie note, ad esempio dati finanziari e informazioni personali, nonché la posizione dei file in base a queste categorie       |
|**Report raccomandazioni**     | -Identificare i file non protetti che contengono un tipo di informazioni riservate noto. Una raccomandazione consente di configurare immediatamente la condizione corrispondente a una delle etichette, per applicare l'etichettatura automatica o consigliata. **<br /> Se si segue la raccomandazione**: la volta successiva che i file vengono aperti da un utente o analizzati dal Azure Information Protection scanner, i file possono essere classificati e protetti automaticamente. <br /><br /> : I repository di dati hanno file con informazioni riservate identificate, ma non vengono analizzati dal Azure Information Protection. Una raccomandazione consente di aggiungere immediatamente l'archivio dati identificato a uno dei profili dello scanner. <br />   **Se si segue la raccomandazione**: al successivo ciclo dello scanner, i file possono essere classificati e protetti automaticamente.        |
| | |

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

- Indirizzo IP del dispositivo dell'utente. 

- Nome del processo pertinente, ad esempio **Outlook** o **MSIP. app**.

- Nome dell'applicazione che ha eseguito l'assegnazione di etichette, ad esempio **Outlook** o **Esplora file**

- Per i documenti: percorso e nome file dei documenti ai quali viene aggiunta l'etichetta.

- Per i messaggi di posta elettronica: l'oggetto e il mittente di posta elettronica per i messaggi di posta elettronica contrassegnati. 

- Tipologie di informazioni riservate ([predefinite](/office365/securitycompliance/what-the-sensitive-information-types-look-for) e personalizzate) rilevate nel contenuto.

- Versione del client di Azure Information Protection.

- Versione del sistema operativo del client.

Queste informazioni vengono archiviate in un'area di lavoro di Azure Log Analytics di proprietà dell'organizzazione e possono essere visualizzate, indipendentemente da Azure Information Protection, dagli utenti con i diritti di accesso all'area di lavoro. 

Per informazioni dettagliate, vedere:

- [Autorizzazioni necessarie per la funzionalità di analisi di Azure Information Protection](#permissions-required-for-azure-information-protection-analytics)
- [Gestire l'accesso all'area di lavoro Log Analytics usando le autorizzazioni di Azure](/azure/azure-monitor/platform/manage-access#manage-access-using-azure-permissions)
- [Riferimento al log di controllo Azure Information Protection](audit-logs.md)

#### <a name="prevent-the-aip-clients-from-sending-auditing-data"></a>Impedisci ai client AIP di inviare dati di controllo

**Client per l'etichettatura unificata** 

Per impedire che il client con etichetta unificata di Azure Information Protection invii i dati di controllo, configurare un' [impostazione avanzata](./rms-client/clientv2-admin-guide-customizations.md#disable-sending-audit-data-to-azure-information-protection-analytics)dei criteri di etichetta.

**Client classico**

Per impedire che il client di Azure Information Protection classico invii questi dati, impostare l' [impostazione dei criteri](configure-policy-settings.md) di **Invia dati di controllo su Azure Information Protection Analytics** su **disattivato**:

|Requisito  |Istruzioni  |
|---------|---------|
|**Per configurare la maggior parte degli utenti per l'invio di dati, con un subset di utenti che non possono inviare dati**     |  Impostare **Invia dati di controllo a Azure Information Protection Analytics** su **disattivato** in un criterio con ambito per il subset di utenti. <br><br> Questa configurazione è tipica per gli scenari di produzione.     |
|**Per configurare solo un subset di utenti che inviano dati**     |  Impostare **Invia dati di controllo a Azure Information Protection Analytics** su **disattivato** nei criteri **globali e in** in un criterio con ambito per il subset di utenti. <br><br>Questa configurazione è tipica per gli scenari di test.       |
| | |

#### <a name="content-matches-for-deeper-analysis"></a>Corrispondenze di contenuto per un'analisi più approfondita

Azure Information Protection consente di raccogliere e archiviare i dati effettivi identificati come un tipo di informazioni riservate (predefinito o personalizzato). Possono essere inclusi ad esempio numeri di carta di credito, numeri di previdenza sociale, numeri di passaporto e numeri di conto bancario. Le corrispondenze contenuto vengono visualizzate quando si seleziona una voce dai **log attività** e si visualizzano i **Dettagli dell'attività**. 

Per impostazione predefinita, i client di Azure Information Protection non inviano corrispondenze di contenuto. Per modificare questo comportamento in modo che vengano inviate le corrispondenze del contenuto:

|Client  |Istruzioni  |
|---------|---------|
|**Client per l'etichettatura unificata**      |  Configurare un' [impostazione avanzata](./rms-client/clientv2-admin-guide-customizations.md#send-information-type-matches-to-azure-information-protection-analytics) in un criterio di etichetta.       |
|**Client classico**      |   Selezionare una casella di controllo come parte della [configurazione](#configure-a-log-analytics-workspace-for-the-reports) per Azure Information Protection Analytics. La casella di controllo è denominata **Abilita analisi più approfondita nei dati sensibili**. <br><br> Se si vuole che la maggior parte degli utenti che usano questo client per inviare corrispondenze di contenuto, ma un subset di utenti non può inviare corrispondenze di contenuto, selezionare la casella di controllo e quindi configurare un' [impostazione client avanzata](./rms-client/client-admin-guide-customizations.md#disable-sending-information-type-matches-for-a-subset-of-users) in un criterio con ambito per il subset di utenti.     |
|     |         |


## <a name="prerequisites"></a>Prerequisiti
Per visualizzare i report di Azure Information Protection e creare report personalizzati, verificare che siano soddisfatti i requisiti seguenti.

|Requisito|Altre informazioni|
|---------------|--------------------|
|Una sottoscrizione di Azure che include Log Analytics ed è per lo stesso tenant di Azure Information Protection|Vedere la pagina dei [prezzi di Monitoraggio di Azure](https://azure.microsoft.com/pricing/details/log-analytics).<br /><br />Se non si dispone di un abbonamento di Azure o attualmente non si usa Azure Log Analytics, la pagina dei prezzi include un collegamento per una versione di valutazione gratuita.|
|Per informazioni sulla creazione di report per l'assegnazione di etichette ai client: <br /><br />-Client Azure Information Protection|Sono supportati sia il client Unified labeling che il client classico. <br /><br />Se non è già installato, è possibile scaricare e installare il client di etichettatura unificata dall' [area download Microsoft](https://www.microsoft.com/download/details.aspx?id=53018). Per distribuire il client classico AIP, aprire un ticket di supporto per ottenere l'accesso al download.|
|Per informazioni sulla creazione di report da archivi dati basati sul cloud: <br /><br />-Microsoft Cloud App Security |Per visualizzare le informazioni da Microsoft Cloud App Security, configurare l' [integrazione di Azure Information Protection](/cloud-app-security/azip-integration).|
|Per informazioni sulla creazione di report da archivi dati locali: <br /><br />-Azure Information Protection scanner |Per le istruzioni di installazione per lo scanner, vedere [Distribuzione dello scanner di Azure Information Protection per classificare e proteggere automaticamente i file](deploy-aip-scanner.md). |
|Per informazioni sulla creazione di report da computer Windows 10:  <br /><br />-Compilazione minima di 1809 con Microsoft Defender Advanced Threat Protection (Microsoft Defender ATP)|È necessario abilitare la funzionalità di integrazione Azure Information Protection da Microsoft Defender Security Center. Per altre informazioni, vedere [Panoramica di Information Protection in Windows](/windows/security/threat-protection/microsoft-defender-atp/information-protection-in-windows-overview).|
| | |

### <a name="permissions-required-for-azure-information-protection-analytics"></a>Autorizzazioni necessarie per la funzionalità di analisi di Azure Information Protection

Specificatamente per la funzionalità di analisi di Azure Information Protection, dopo aver configurato l'area di lavoro di Azure Log Analytics, è possibile usare il ruolo di amministratore di Azure AD Ruolo con autorizzazioni di lettura per la sicurezza come alternativa ad altri ruoli di Azure AD che supportano la gestione di Azure Information Protection nel portale di Azure. Questo ruolo aggiuntivo è supportato solo se il tenant non è nella [piattaforma di etichettatura unificata](faqs.md#how-can-i-determine-if-my-tenant-is-on-the-unified-labeling-platform).

Poiché Azure Information Protection Analytics usa il monitoraggio di Azure, il controllo degli accessi in base al ruolo (RBAC) per Azure controlla anche l'accesso all'area di lavoro. È quindi necessario un ruolo di Azure, nonché un ruolo di amministratore di Azure AD per gestire l'analisi di Azure Information Protection. Se non si ha familiarità con i ruoli di Azure, può risultare utile leggere [Differenze tra i ruoli di controllo dell'accesso in base al ruolo di Azure e i ruoli di amministratore di Azure AD](/azure/role-based-access-control/rbac-and-directory-admin-roles#differences-between-azure-rbac-roles-and-azure-ad-administrator-roles).

Per altre informazioni, vedere:

- [Ruoli di amministratore Azure AD obbligatori](#required-azure-ad-administrator-roles)
- [Ruoli di Log Analytics di Azure richiesti](#required-azure-log-analytics-roles)
- [Ruoli minimi per visualizzare i report](#minimum-roles-to-view-the-reports)

#### <a name="required-azure-ad-administrator-roles"></a>Ruoli di amministratore Azure AD obbligatori

Per accedere al riquadro analisi Azure Information Protection, è necessario disporre di uno dei seguenti [ruoli di amministratore Azure ad](/azure/active-directory/active-directory-assign-admin-roles-azure-portal) :

- Per creare l'area di lavoro di Log Analytics o per creare query personalizzate:
    
    - **Amministratore Azure Information Protection**
    - **Amministratore della sicurezza**
    - **Amministratore di conformità**
    - **Amministratore dati di conformità**
    - **Amministratore globale**
    
- Dopo aver creato l'area di lavoro, è possibile usare i ruoli seguenti con un minor numero di autorizzazioni per visualizzare i dati raccolti:
    
    - **Ruolo con autorizzazioni di lettura per la sicurezza**
    - **Lettore globale**

#### <a name="required-azure-log-analytics-roles"></a>Ruoli di Log Analytics di Azure richiesti

Per accedere all'area di lavoro di Azure Log Analytics, è necessario disporre di uno dei seguenti ruoli di Azure [log Analytics](/azure/azure-monitor/platform/manage-access#manage-access-using-azure-permissions) o dei ruoli standard di [Azure](/azure/role-based-access-control/rbac-and-directory-admin-roles#azure-rbac-roles) :
    
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

La quantità di dati raccolti e archiviati nell'area di lavoro di Azure Information Protection varierà in modo significativo per ogni tenant, a seconda di fattori quali il numero di Azure Information Protection client e altri endpoint supportati, sia che si stiano raccogliendo i dati di individuazione degli endpoint, che siano stati distribuiti scanner, il numero di documenti protetti a cui si accede e così via.

Tuttavia, come punto di partenza, le stime seguenti potrebbero risultare utili:

- Per i dati di controllo generati solo da client Azure Information Protection: 2 GB per 10.000 utenti attivi al mese.

- Per i dati di controllo generati da client Azure Information Protection, scanner e Microsoft Defender ATP: 20 GB per 10.000 utenti attivi al mese.

Se si usa l'etichettatura obbligatoria o si è configurata un'etichetta predefinita per la maggior parte degli utenti, è probabile che le tariffe siano significativamente più elevate.

I log di monitoraggio di Azure hanno una funzionalità di **utilizzo e costi stimati** che consentono di stimare e controllare la quantità di dati archiviati ed è inoltre possibile controllare il periodo di conservazione dei dati per l'area di lavoro log Analytics. Per altre informazioni, vedere [gestire l'utilizzo e i costi con i log di monitoraggio di Azure](/azure/azure-monitor/platform/manage-cost-storage).

## <a name="configure-a-log-analytics-workspace-for-the-reports"></a>Configurare un'area di lavoro di Log Analytics per i report

1. Se non già stato fatto, aprire una nuova finestra del browser e [accedere al portale di Azure](https://portal.azure.com) con un account che dispone delle [autorizzazioni necessarie per le analisi di Azure Information Protection](#permissions-required-for-azure-information-protection-analytics). Quindi passare al riquadro **Azure Information Protection**. 
    
    Ad esempio, nella casella di ricerca di risorse, servizi e documentazione: iniziare a digitare **Informazioni** e selezionare **Azure Information Protection**.
    
1. Individuare le opzioni del menu **Gestisci** e selezionare **Configura le analisi (anteprima)**.

1. Nel riquadro **Azure Information Protection log Analytics** viene visualizzato un elenco di tutte le aree di lavoro log Analytics di proprietà del tenant. Eseguire una delle operazioni seguenti:
    
    - **Per creare una nuova area di lavoro log Analytics**: selezionare **Crea nuova area di lavoro** e nel riquadro **area di lavoro di log Analytics** fornire le informazioni richieste.
    
    - **Per usare un'area di lavoro log Analytics esistente**: selezionare l'area di lavoro nell'elenco.
    
    Per assistenza nella creazione dell'area di lavoro di Log Analytics, vedere [Creare un'area di lavoro di Log Analytics nel portale di Azure](/azure/log-analytics/log-analytics-quick-create-workspace).

1. **Solo client classico AIP**: selezionare la casella di controllo **Abilita analisi più approfondita nei dati sensibili** se si desidera archiviare i dati effettivi identificati come tipo di informazioni riservate. 

    Per ulteriori informazioni su questa impostazione, vedere la sezione [corrispondenze di contenuto per l'analisi più approfondita](#content-matches-for-deeper-analysis) in questa pagina.

1. Selezionare **OK**.

A questo punto si è pronti per visualizzare i report.

## <a name="how-to-view-the-reports"></a>Come visualizzare i report

Dal riquadro Azure Information Protection individuare le opzioni del menu **Dashboard** e selezionare una delle opzioni seguenti:

|Report  |Descrizione  |
|---------|---------|
|**Report sull'utilizzo (anteprima)**     |  usare questo report per vedere come vengono usate le etichette.       |
|**Log attività (anteprima)**     |  usare questo report per visualizzare le azioni di etichettatura dagli utenti e per i dispositivi e i percorsi di file. Per i documenti protetti, inoltre, è possibile visualizzare i tentativi di accesso (esito positivo o negativo) per gli utenti all'interno e all'esterno dell'organizzazione, anche se non hanno installato il client di Azure Information Protection. <br><br>  Questo report contiene un'opzione **Colonne** che consente di visualizzare più informazioni sulle attività rispetto alla visualizzazione predefinita. È anche possibile accedere ad altri dettagli su un file selezionandolo per visualizzare **Dettagli attività**.     |
|**Individuazione dati (anteprima)**     |    usare questo report per visualizzare informazioni sui file etichettati trovati dagli strumenti di analisi e dagli endpoint supportati.  <br><br>**Suggerimento**: dalle informazioni raccolte, è possibile che gli utenti accedano a file che contengono informazioni riservate dal percorso di cui non si è a conoscenza o che non sono in corso di analisi: <br><br>-Se i percorsi sono locali, è consigliabile aggiungere i percorsi come repository di dati aggiuntivi per lo scanner Azure Information Protection. <br>  -Se i percorsi si trovano nel cloud, provare a usare Microsoft Cloud App Security per gestirli.    |
|**Raccomandazioni (anteprima)**     | usare questo report per identificare i file che contengono informazioni sensibili e attenuare il rischio seguendo le raccomandazioni.  <br><br> Quando si seleziona un elemento, l'opzione **Visualizza i dati** consente di visualizzare le attività di controllo che hanno attivato la raccomandazione.     |
|     |         |


## <a name="how-to-modify-the-reports-and-create-custom-queries"></a>Come modificare i report e creare query personalizzate

Selezionare l'icona della query nel dashboard per aprire un riquadro **Ricerca log** : 

![Icona di Log Analytics per personalizzare i report di Azure Information Protection](./media/log-analytics-icon.png)


I dati registrati per Azure Information Protection vengono archiviati nella tabella seguente: **InformationProtectionLogs_CL**

Per creare query personalizzate, usare i nomi di schema descrittivi implementati come funzioni **InformationProtectionEvents**. Queste funzioni sono derivate dagli attributi supportati per le query personalizzate (alcuni attributi sono solo per uso interno) e i relativi nomi non cambiano nel tempo, neanche se gli attributi sottostanti cambiano in seguito a miglioramenti o nuove funzionalità.

### <a name="friendly-schema-reference-for-event-functions"></a>Riferimenti sui nomi di schema descrittivi per le funzioni di eventi

Usare la tabella seguente per identificare il nome descrittivo delle funzioni di eventi che è possibile usare per le query personalizzate con le funzionalità di analisi di Azure Information Protection.

|Nome colonna|Descrizione|
|-----------|-----------|
|**Time**|Ora dell'evento: UTC nel formato AAAA-MM-GGThh: MM: SS|
|**Utente**|Utente: Format UPN o dominio\utente|
|**ItemPath**|Percorso dell'elemento completo o oggetto di posta elettronica|
|**ItemName**|Nome file o oggetto posta elettronica |
|**Metodo**|Metodo assegnato etichetta: manuale, automatico, consigliato, predefinito o obbligatorio|
|**Attività**|Attività di controllo: DowngradeLabel, UpgradeLabel, RemoveLabel, NewLabel, Discover, Access, RemoveCustomProtection, ChangeCustomProtection, NewCustomProtection o FileRemoved |
|**ResultStatus**|Stato risultato dell'azione:<br /><br /> Succeeded o failed (segnalato solo dallo scanner AIP)|
|**ErrorMessage_s**|Include i dettagli del messaggio di errore se ResultStatus = failed. Segnalato solo dallo scanner AIP|
|**Nomeetichetta**|Nome etichetta (non localizzato)|
|**LabelNameBefore** |Nome etichetta prima della modifica (non localizzato) |
|**ProtectionType**|Tipo di protezione [JSON] <br />{ <br />"Type": ["Template", "Custom", "DoNotForward"], <br />  "TemplateID": "GUID" <br /> } <br />|
|**ProtectionBefore**|Tipo di protezione prima della modifica [JSON] |
|**MachineName** |FQDN quando disponibile; nome host in caso contrario|
|**DeviceRisk**|Punteggio di rischio del dispositivo da WDATP quando disponibile|
|**Piattaforma**|Piattaforma del dispositivo (Win, OSX, Android, iOS) |
|**ApplicationName**|Nome descrittivo dell'applicazione|
|**AIPVersion**|Versione del client di Azure Information Protection che ha eseguito l'azione di controllo |
|**TenantId**|ID tenant di Azure AD |
|**AzureApplicationId**|ID applicazione registrato Azure AD (GUID)|
|**ProcessName**|Processo che ospita MIP SDK|
|**LabelId**|GUID etichetta o null|
|**IsProtected**|Se protetto: Sì/No |
|**ProtectionOwner** |Proprietario Rights Management in formato UPN|
|**LabelIdBefore**|GUID etichetta o null prima della modifica|
|**InformationTypesAbove55**|Matrice JSON di [SensitiveInformation](/microsoft-365/compliance/what-the-sensitive-information-types-look-for) trovata nei dati con livello di confidenza 55 o superiore |
|**InformationTypesAbove65**|Matrice JSON di [SensitiveInformation](/microsoft-365/compliance/what-the-sensitive-information-types-look-for) trovata nei dati con livello di confidenza 65 o superiore |
|**InformationTypesAbove75**|Matrice JSON di [SensitiveInformation](/microsoft-365/compliance/what-the-sensitive-information-types-look-for) trovata nei dati con livello di confidenza 75 o superiore |
|**InformationTypesAbove85**|Matrice JSON di [SensitiveInformation](/microsoft-365/compliance/what-the-sensitive-information-types-look-for) trovata nei dati con livello di confidenza 85 o superiore |
|**InformationTypesAbove95**|Matrice JSON di [SensitiveInformation](/microsoft-365/compliance/what-the-sensitive-information-types-look-for) trovata nei dati con livello di confidenza 95 o superiore|
|**DiscoveredInformationTypes** |Matrice JSON di [SensitiveInformation](/microsoft-365/compliance/what-the-sensitive-information-types-look-for) trovata nei dati e il relativo contenuto corrispondente (se abilitato) in cui una matrice vuota indica che non sono stati trovati tipi di informazioni e null indica che non sono disponibili informazioni |
|**ProtectedBefore**|Se il contenuto è stato protetto prima della modifica: Sì/No |
|**ProtectionOwnerBefore**|Proprietario Rights Management prima della modifica |
|**UserJustification**|Giustificazione durante il downgrade o la rimozione dell'etichetta|
|**LastModifiedBy**|Utente in formato UPN che ha eseguito l'ultima modifica al file. Disponibile solo per Office e SharePoint|
|**LastModifiedDate**|UTC nel formato AAAA-MM-GGThh: MM: SS: disponibile solo per Office e SharePoint |
| | |
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
Dopo aver esaminato le informazioni nei report, se si usa il client di Azure Information Protection, è possibile decidere di apportare modifiche ai criteri di etichettatura. 

- **Client per l'assegnazione di etichette unificata**: apportare modifiche ai criteri di etichettatura nell'interfaccia di amministrazione di assegnazione di etichette, tra cui il centro sicurezza Microsoft 365, il centro di conformità Microsoft 365 o il Microsoft 365 Security & Compliance Center. Per altre informazioni, vedere la [documentazione di Microsoft 365](/microsoft-365/compliance/sensitivity-labels).

- **Client classico**: apportare modifiche ai criteri nel portale di Azure. Per ulteriori informazioni, vedere [Configuring the Azure Information Protection Policy](configure-policy.md).

Se è disponibile un abbonamento a Microsoft 365, è anche possibile visualizzare l'utilizzo delle etichette nel Centro sicurezza Microsoft 365 e nel Centro conformità Microsoft 365. Per altre informazioni, vedere [Visualizzare l'utilizzo delle etichette con Analisi delle etichette](/microsoft-365/compliance/label-analytics).

I log di controllo AIP vengono inviati anche a Microsoft 365 Activity Explorer, dove possono essere visualizzati con nomi diversi. Per altre informazioni, vedere:

- [Anteprima pubblica: log di controllo AIP in Esplora attività](https://www.yammer.com/askipteam/#/Threads/show?threadId=1085834054254592)
- [Introduzione ad Esplora attività](/microsoft-365/compliance/data-classification-activity-explorer).