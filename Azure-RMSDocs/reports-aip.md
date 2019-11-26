---
title: Reporting centralizzato per Azure Information Protection
description: Come usare il reporting centralizzato per monitorare l'adozione delle etichette di Azure Information Protection e trovare i file che contengono informazioni riservate
author: cabailey
ms.author: cabailey
ms.date: 11/25/2019
manager: rkarlin
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: b2da2cdc-74fd-4bfb-b3c2-2a3a59a6bf2e
ms.subservice: analytics
ms.reviewer: lilukov
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 7c310122ac72bc7312fe0bd8d41bd3dc80715d76
ms.sourcegitcommit: fed1df1858f8316f7dd45e751c6910b444651a87
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/25/2019
ms.locfileid: "74474285"
---
# <a name="central-reporting-for-azure-information-protection"></a>Reporting centralizzato per Azure Information Protection

>*Si applica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*

> [!NOTE]
> Al momento questa funzionalità è disponibile in anteprima ed è soggetta a modifiche.

Use Azure Information Protection analytics for central reporting to help you track the adoption of your labels that classify and protect your organization's data. Inoltre:

- Monitorare documenti e messaggi di posta elettronica etichettati e protetti nell'organizzazione.

- Identificare i documenti che contengono informazioni riservate nell'organizzazione.

- Monitorare l'accesso degli utenti a documenti e messaggi di posta elettronica etichettati e tenere traccia delle modifiche alla classificazione dei documenti.

- Identificare i documenti contenenti informazioni sensibili che possono mettere a rischio l'organizzazione se non protette e attenuare il rischio seguendo le raccomandazioni.

- Identify when protected documents are accessed by internal or external users from Windows computers, and whether access was granted or denied.

The data that you see is aggregated from your Azure Information Protection clients and scanners, from Microsoft Cloud App Security, from Windows 10 computers using Microsoft Defender Advanced Threat Protection, and from [protection usage logs](log-analyze-usage.md).

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
    
    - What labeling actions were performed by a specific application, such File Explorer and right-click, PowerShell, the scanner, or Microsoft Cloud App Security
    
    - Which protected documents were accessed successfully by users or denied access to users, even if those users don't have the Azure Information Protection client installed or are outside your organization

    - Eseguire il drill-down dei file segnalati per visualizzare la sezione **Dettagli attività** in cui sono disponibili altre informazioni

- Nel report **Individuazione dati**:

    - What files are on your scanned data repositories, Windows 10 computers, or computers running the Azure Information Protection clients
    
    - Quali file sono provvisti di etichetta e protetti e il percorso dei file in base alle etichette
    
    - Quali file contengono informazioni riservate per categorie note, ad esempio dati finanziari e informazioni personali e il percorso dei file in base a queste categorie

- Dal report **Raccomandazioni**:
    
    - Identificare i file non protetti che contengono un tipo noto di informazioni sensibili. Una raccomandazione consente di configurare immediatamente la condizione corrispondente a una delle etichette, per applicare l'etichettatura automatica o consigliata.
        
        If you follow the recommendation: The next time the files are opened by a user or scanned by the Azure Information Protection scanner, the files can be automatically classified and protected.
    
    - Identificare i repository dei dati che contengono file con informazioni sensibili identificate ma non analizzati da Azure Information Protection. Una raccomandazione consente di aggiungere immediatamente l'archivio dati identificato a uno dei profili dello scanner.
        
        If you follow the recommendation: On the next scanner cycle, the files can be automatically classified and protected.

I report usano [Monitoraggio di Azure](/azure/log-analytics/log-analytics-overview) per archiviare i dati in un'area di lavoro di Log Analytics di proprietà dell'organizzazione. Se si ha familiarità con il linguaggio di query, è possibile modificare le query e creare nuovi report e dashboard di Power BI. You might find the following tutorial helpful to understand the query language: [Get started with Azure Monitor log queries](/azure/azure-monitor/log-query/get-started-queries).

Per altre informazioni, vedere i seguenti post di blog: 
- [Data discovery, reporting and analytics for all your data with Microsoft Information Protection](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/Data-discovery-reporting-and-analytics-for-all-your-data-with/ba-p/253854) (Individuazione, report e analisi per tutti i dati utente con Microsoft Information Protection).

- [Discover and protect sensitive data through Azure Information Protection and Microsoft Defender ATP](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/Discover-and-protect-sensitive-data-through-Azure-Information/ba-p/297292)

### <a name="information-collected-and-sent-to-microsoft"></a>Informazioni raccolte e inviate a Microsoft

Per generare questi report, gli endpoint inviano i seguenti tipi di informazioni a Microsoft:

- Azione per l'etichetta. Ad esempio impostazione o modifica di un'etichetta, aggiunta o rimozione della protezione, etichette automatiche e consigliate.

- Nome dell'etichetta prima e dopo l'azione dell'etichetta.

- ID del tenant dell'organizzazione.

- ID utente (indirizzo di posta elettronica o UPN).

- Nome del dispositivo dell'utente.

- Per i documenti: percorso e nome file dei documenti ai quali viene aggiunta l'etichetta.

- For emails: The email subject and email sender  for emails that are labeled. 

- Tipologie di informazioni riservate ([predefinite](https://docs.microsoft.com/office365/securitycompliance/what-the-sensitive-information-types-look-for) e personalizzate) rilevate nel contenuto.

- Versione del client di Azure Information Protection.

- Versione del sistema operativo del client.

Queste informazioni vengono archiviate in un'area di lavoro di Azure Log Analytics di proprietà dell'organizzazione e possono essere visualizzate, indipendentemente da Azure Information Protection, dagli utenti con i diritti di accesso all'area di lavoro. Per informazioni dettagliate, vedere la sezione [Autorizzazioni necessarie per la funzionalità di analisi di Azure Information Protection](#permissions-required-for-azure-information-protection-analytics). Per informazioni sulla gestione dell'accesso all'area di lavoro, vedere la sezione [Gestire l'accesso all'area di lavoro Log Analytics](https://docs.microsoft.com/azure/azure-monitor/platform/manage-access#manage-access-using-azure-permissions) nella documentazione di Azure.

To prevent Azure Information Protection clients (classic) from sending this data, set the [policy setting](configure-policy-settings.md) of **Send audit data to Azure Information Protection analytics** to **Off**:

- Per fare in modo che la maggior parte degli utenti possa inviare questi dati e un subset di utenti non possa inviare dati di controllo: 
    - Set **Send audit data to Azure Information Protection analytics** to **Off** in a scoped policy for the subset of users. Questa configurazione è tipica per gli scenari di produzione.

- Per fare in modo che solo un subset di utenti possa inviare dati di controllo: 
    - Set **Send audit data to Azure Information Protection analytics** to **Off** in the global policy, and **On** in a scoped policy for the subset of users. Questa configurazione è tipica per gli scenari di test.

To prevent Azure Information Protection unified clients from sending this data, configure a label policy [advanced setting](./rms-client/clientv2-admin-guide-customizations.md#disable-sending-audit-data-to-azure-information-protection-analytics).

#### <a name="content-matches-for-deeper-analysis"></a>Corrispondenze di contenuto per un'analisi più approfondita

Azure Information Protection lets you collect and store the actual data that's identified as being a sensitive information type (predefined or custom). Possono essere inclusi ad esempio numeri di carta di credito, numeri di previdenza sociale, numeri di passaporto e numeri di conto bancario. The content matches are displayed when you select an entry from **Activity logs**, and view the **Activity Details**. 

By default, Azure Information Protection clients don't send content matches. To change this behavior so that content matches are sent:

- For the classic client, select a checkbox as part of the [configuration](#configure-a-log-analytics-workspace-for-the-reports) for Azure Information Protection analytics. The checkbox is named **Enable deeper analytics into your sensitive data**.
    
    If you want most users who are using this client to send content matches but a subset of users cannot send content matches, select the checkbox and then configure an [advanced client setting](./rms-client/client-admin-guide-customizations.md#disable-sending-information-type-matches-for-a-subset-of-users) in a scoped policy for the subset of users.

- For the unified labeling client, configure an [advanced setting](./rms-client/clientv2-admin-guide-customizations.md#send-information-type-matches-to-azure-information-protection-analytics) in a label policy.

## <a name="prerequisites"></a>Prerequisiti
Per visualizzare i report di Azure Information Protection e creare report personalizzati, verificare che siano soddisfatti i requisiti seguenti.

|Requisito|Ulteriori informazioni|
|---------------|--------------------|
|Una sottoscrizione di Azure che include Log Analytics ed è per lo stesso tenant di Azure Information Protection|Vedere la pagina dei [prezzi di Monitoraggio di Azure](https://azure.microsoft.com/pricing/details/log-analytics).<br /><br />Se non si dispone di un abbonamento di Azure o attualmente non si usa Azure Log Analytics, la pagina dei prezzi include un collegamento per una versione di valutazione gratuita.|
|For reporting information from labeling clients: <br /><br />- Azure Information Protection clients|Both the unified labeling client and the classic client are supported. <br /><br />If not already installed, you can download and install these clients from the [Microsoft Download Center](https://www.microsoft.com/en-us/download/details.aspx?id=53018).|
|For reporting information from cloud-based data stores: <br /><br />- Microsoft Cloud App Security |To display information from Microsoft Cloud App Security, configure [Azure Information Protection integration](https://docs.microsoft.com/cloud-app-security/azip-integration).|
|For reporting information from on-premises data stores: <br /><br />- Azure Information Protection scanner |Per le istruzioni di installazione per lo scanner, vedere [Distribuzione dello scanner di Azure Information Protection per classificare e proteggere automaticamente i file](deploy-aip-scanner.md). |
|For reporting information from Windows 10 computers:  <br /><br />- Minimum build of 1809 with Microsoft Defender Advanced Threat Protection (Microsoft Defender ATP)|You must enable the Azure Information Protection integration feature from Microsoft Defender Security Center. For more information, see [Information protection in Windows overview](/windows/security/threat-protection/microsoft-defender-atp/information-protection-in-windows-overview).|

### <a name="permissions-required-for-azure-information-protection-analytics"></a>Autorizzazioni necessarie per la funzionalità di analisi di Azure Information Protection

Specificatamente per la funzionalità di analisi di Azure Information Protection, dopo aver configurato l'area di lavoro di Azure Log Analytics, è possibile usare il ruolo di amministratore di Azure AD Ruolo con autorizzazioni di lettura per la sicurezza come alternativa ad altri ruoli di Azure AD che supportano la gestione di Azure Information Protection nel portale di Azure. This additional role is supported only if your tenant isn't on the [unified labeling platform](faqs.md#how-can-i-determine-if-my-tenant-is-on-the-unified-labeling-platform).

Because Azure Information Protection analytics uses Azure Monitoring, role-based access control (RBAC) for Azure also controls access to your workspace. È quindi necessario un ruolo di Azure, nonché un ruolo di amministratore di Azure AD per gestire l'analisi di Azure Information Protection. Se non si ha familiarità con i ruoli di Azure, può risultare utile leggere [Differenze tra i ruoli di controllo dell'accesso in base al ruolo di Azure e i ruoli di amministratore di Azure AD](https://docs.microsoft.com/azure/role-based-access-control/rbac-and-directory-admin-roles#differences-between-azure-rbac-roles-and-azure-ad-administrator-roles).

Dettagli:

1. One of the following [Azure AD administrator roles](/azure/active-directory/active-directory-assign-admin-roles-azure-portal) to access the Azure Information Protection analytics pane:
    
    - Per creare l'area di lavoro di Log Analytics o per creare query personalizzate:
    
        - **Azure Information Protection administrator**
        - **Amministratore della sicurezza**
        - **Amministratore di conformità**
        - **Compliance data administrator**
        - **Amministratore globale**
    
    - After the workspace has been created, you can then use the following roles with fewer permissions to view the data collected:
    
        - **Ruolo con autorizzazioni di lettura per la sicurezza**
        - **Global reader**
    
    > [!NOTE] 
    > You cannot use the Azure Information Protection administrator role, the Security reader role, or the Global reader role if your tenant is on the [unified labeling platform](faqs.md#how-can-i-determine-if-my-tenant-is-on-the-unified-labeling-platform).

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

- Azure AD administrator role: **Security reader**
- Azure role: **Log Analytics Reader**

Tuttavia, un'assegnazione di ruolo tipica per molte organizzazioni è il **ruolo con autorizzazioni di lettura per la sicurezza** di Azure AD e il ruolo **Lettore** di Azure.

### <a name="storage-requirements-and-data-retention"></a>Storage requirements and data retention

The amount of data collected and stored in your Azure Information Protection workspace will vary significantly for each tenant, depending on factors such as how many Azure Information Protection clients and other supported endpoints you have, whether you're collecting endpoint discovery data, you've deployed scanners, the number of protected documents that are accessed, and so on.

However, as a starting point, you might find the following estimates useful:

- For audit data generated by Azure Information Protection clients only: 2 GB per 10,000 active users per month.

- For audit data generated by Azure Information Protection clients, scanners, and Microsoft Defender ATP: 20 GB per 10,000 active users per month.

If you use mandatory labeling or you've configured a default label for most users, your rates are likely to be significantly higher.

Azure Monitor Logs has a **Usage and estimated costs** feature to help you estimate and review the amount of data stored, and you can also control the data retention period for your Log Analytics workspace. For more information, see [Manage usage and costs with Azure Monitor Logs](https://docs.microsoft.com/azure/azure-monitor/platform/manage-cost-storage).

## <a name="configure-a-log-analytics-workspace-for-the-reports"></a>Configurare un'area di lavoro di Log Analytics per i report

1. Se non già stato fatto, aprire una nuova finestra del browser e [accedere al portale di Azure](https://portal.azure.com) con un account che dispone delle [autorizzazioni necessarie per le analisi di Azure Information Protection](#permissions-required-for-azure-information-protection-analytics). Passare quindi al riquadro **Azure Information Protection**. 
    
    For example, in the search box for resources, services, and docs: Start typing **Information** and select **Azure Information Protection**.
    
2. Individuare le opzioni del menu **Gestisci** e selezionare **Configura le analisi (anteprima)** .

3. On the **Azure Information Protection log analytics** pane, you see a list of any Log Analytics workspaces that are owned by your tenant. Effettuare una delle operazioni seguenti:
    
    - To create a new Log Analytics workspace: Select **Create new workspace**, and on the **Log analytics workspace** pane, supply the requested information.
    
    - Per usare un'area di lavoro di Log Analytics esistente, selezionare l'area di lavoro dall'elenco.
    
    Per assistenza nella creazione dell'area di lavoro di Log Analytics, vedere [Creare un'area di lavoro di Log Analytics nel portale di Azure](https://docs.microsoft.com/azure/log-analytics/log-analytics-quick-create-workspace).

4. If you have Azure Information Protection clients (classic), select the checkbox **Enable deeper analytics into your sensitive data** if you want to store the actual data that's identified as being a sensitive information type. For more information about this setting, see the [Content matches for deeper analysis](#content-matches-for-deeper-analysis) section on this page.

5. Selezionare **OK**.

You're now ready to view the reports.

## <a name="how-to-view-the-reports"></a>Come visualizzare i report

From the Azure Information Protection pane, locate the **Dashboards** menu options, and select one of the following options:

- **Report di utilizzo (anteprima)** : usare questo report per vedere come vengono usate le etichette.

- **Log attività (anteprima)** : usare questo report per visualizzare le azioni di etichettatura dagli utenti e per i dispositivi e i percorsi di file. In addition, for protected documents, you can see access attempts (successful or denied) for users both inside and outside your organization, even if they don't have the Azure Information Protection client installed
    
    Questo report contiene un'opzione **Colonne** che consente di visualizzare più informazioni sulle attività rispetto alla visualizzazione predefinita. È anche possibile accedere ad altri dettagli su un file selezionandolo per visualizzare **Dettagli attività**.

- **Data discovery (Preview)** : Use this report to see information about labeled files found by scanners and supported endpoints.
    
    Tip: From the information collected, you might find users accessing files that contain sensitive information from location that you didn't know about or aren't currently scanning:
    
    - Se le posizioni sono in locale, è consigliabile aggiungerle come ulteriori repository di dati per lo strumento di analisi di Azure Information Protection.
    - Se le posizioni sono nel cloud, è consigliabile usare Microsoft Cloud App Security per gestirle. 
    
- **Recommendations (Preview)** : Use this report to identify files that have sensitive information and mitigate your risk by following the recommendations.
    
    Quando si seleziona un elemento, l'opzione **Visualizza i dati** consente di visualizzare le attività di controllo che hanno attivato la raccomandazione.


## <a name="how-to-modify-the-reports-and-create-custom-queries"></a>Come modificare i report e creare query personalizzate

Select the query icon in the dashboard to open a **Log Search** pane: 

![Icona di Log Analytics per personalizzare i report di Azure Information Protection](./media/log-analytics-icon.png)


I dati registrati per Azure Information Protection vengono archiviati nella tabella seguente: **InformationProtectionLogs_CL**

Per creare query personalizzate, usare i nomi di schema descrittivi implementati come funzioni **InformationProtectionEvents**. Queste funzioni sono derivate dagli attributi supportati per le query personalizzate (alcuni attributi sono solo per uso interno) e i relativi nomi non cambiano nel tempo, neanche se gli attributi sottostanti cambiano in seguito a miglioramenti o nuove funzionalità.

### <a name="friendly-schema-reference-for-event-functions"></a>Riferimenti sui nomi di schema descrittivi per le funzioni di eventi

Usare la tabella seguente per identificare il nome descrittivo delle funzioni di eventi che è possibile usare per le query personalizzate con le funzionalità di analisi di Azure Information Protection.

|Nome della colonna|Description|
|-----------|-----------|
|Ora|Event time: UTC in format YYYY-MM-DDTHH:MM:SS|
|Utente|User: Format UPN or DOMAIN\USER|
|ItemPath|Full item path or email subject|
|ItemName|File name or email subject |
|Metodo|Label assigned method: Manual, Automatic, Recommended, Default, or Mandatory|
|Attività|Audit activity: DowngradeLabel, UpgradeLabel, RemoveLabel, NewLabel, Discover, Access, RemoveCustomProtection, ChangeCustomProtection, or NewCustomProtection |
|LabelName|Label name (not localized)|
|LabelNameBefore |Label name before change (not localized) |
|ProtectionType|Protection type [JSON] <br />{ <br />"Type": ["Template", "Custom", "DoNotForward"], <br />  "TemplateID": "GUID" <br /> } <br />|
|ProtectionBefore|Protection type before change [JSON] |
|MachineName |FQDN when available; otherwise host name|
|DeviceRisk|Device risk score from WDATP when available|
|Piattaforma|Device platform (Win, OSX, Android, iOS) |
|ApplicationName|Application friendly name|
|AIPVersion|Version of the Azure Information Protection client that performed the audit action |
|TenantId|ID tenant di Azure AD |
|AzureApplicationId|Azure AD registered application ID (GUID)|
|ProcessName|Process that hosts MIP SDK|
|LabelId|Label GUID or null|
|IsProtected|Whether protected: Yes/No |
|ProtectionOwner |Rights Management owner in UPN format|
|LabelIdBefore|Label GUID or null before change|
|InformationTypesAbove55|JSON array of [SensitiveInformation](https://docs.microsoft.com/microsoft-365/compliance/what-the-sensitive-information-types-look-for) found in data with confidence level 55 or above |
|InformationTypesAbove65|JSON array of [SensitiveInformation](https://docs.microsoft.com/microsoft-365/compliance/what-the-sensitive-information-types-look-for) found in data with confidence level 65 or above |
|InformationTypesAbove75|JSON array of [SensitiveInformation](https://docs.microsoft.com/microsoft-365/compliance/what-the-sensitive-information-types-look-for) found in data with confidence level 75 or above |
|InformationTypesAbove85|JSON array of [SensitiveInformation](https://docs.microsoft.com/microsoft-365/compliance/what-the-sensitive-information-types-look-for) found in data with confidence level 85 or above |
|InformationTypesAbove95|JSON array of [SensitiveInformation](https://docs.microsoft.com/microsoft-365/compliance/what-the-sensitive-information-types-look-for) found in data with confidence level 95 or above|
|DiscoveredInformationTypes |JSON array of [SensitiveInformation](https://docs.microsoft.com/microsoft-365/compliance/what-the-sensitive-information-types-look-for) found in data and their matched content (if enabled) where an empty array means no information types found, and null means no information available |
|ProtectedBefore|Whether the content was protected before change: Yes/No |
|ProtectionOwnerBefore|Rights Management owner before change |
|UserJustification|Justification when downgrading or removing label|
|LastModifiedBy|User in UPN format who last modified the file. Available for Office and SharePoint Online only|
|LastModifiedDate|UTC in format YYYY-MM-DDTHH:MM:SS: Available for Office & SharePoint Online only |


#### <a name="examples-using-informationprotectionevents"></a>Esempi di utilizzo di InformationProtectionEvents

Gli esempi seguenti mostrano come è possibile usare lo schema descrittivo per creare query personalizzate.

##### <a name="example-1-return-all-users-who-sent-audit-data-in-the-last-31-days"></a>Example 1: Return all users who sent audit data in the last 31 days 

```
InformationProtectionEvents 
| where Time > ago(31d) 
| distinct User 
```

 
##### <a name="example-2-return-the-number-of-labels-that-were-downgraded-per-day-in-the-last-31-days"></a>Example 2: Return the number of labels that were downgraded per day in the last 31 days 


```
InformationProtectionEvents 
| where Time > ago(31d) 
| where Activity == "DowngradeLabel"  
| summarize Label_Downgrades_per_Day = count(Activity) by bin(Time, 1d) 
 
```
 
##### <a name="example-3-return-the-number-of-labels-that-were-downgraded-from-confidential-by-user-in-the-last-31-days"></a>Example 3: Return the number of labels that were downgraded from Confidential by user, in the last 31 days 

```

InformationProtectionEvents 
| where Time > ago(31d) 
| where Activity == "DowngradeLabel"  
| where LabelNameBefore contains "Confidential" and LabelName !contains "Confidential"  
| summarize Label_Downgrades_by_User = count(Activity) by User | sort by Label_Downgrades_by_User desc 

```

In questo esempio, un'etichetta di cui è stato effettuato il downgrade viene conteggiata solo se il nome dell'etichetta prima dell'azione conteneva il nome **Confidential** e il nome dell'etichetta dopo l'azione non conteneva il nome **Confidential**. 


## <a name="next-steps"></a>Passaggi successivi
After reviewing the information in the reports, if you are using the Azure Information Protection client, you might decide to make changes to your Azure Information Protection policy. Per istruzioni, vedere [Configurazione dei criteri di Azure Information Protection](configure-policy.md).

Se è disponibile un abbonamento a Microsoft 365, è anche possibile visualizzare l'utilizzo delle etichette nel Centro sicurezza Microsoft 365 e nel Centro conformità Microsoft 365. Per altre informazioni, vedere [Visualizzare l'utilizzo delle etichette con Analisi delle etichette](/microsoft-365/compliance/label-analytics).
