---
title: Reporting centralizzato per Azure Information Protection
description: Come usare il reporting centralizzato per monitorare l'adozione delle etichette di Azure Information Protection e trovare i file che contengono informazioni riservate
author: cabailey
ms.author: cabailey
ms.date: 04/02/2019
manager: barbkess
ms.topic: article
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: b2da2cdc-74fd-4bfb-b3c2-2a3a59a6bf2e
ms.reviewer: lilukov
ms.suite: ems
ms.openlocfilehash: e24b143c64957fb4336effc4cac6666b374f3a15
ms.sourcegitcommit: 8da0aa8f9bb9f91375580a703682d23a81a441bf
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/02/2019
ms.locfileid: "58809965"
---
# <a name="central-reporting-for-azure-information-protection"></a>Reporting centralizzato per Azure Information Protection

>*Si applica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*

> [!NOTE]
> Al momento questa funzionalità è disponibile in anteprima ed è soggetta a modifiche.

Usare le funzionalità di analisi di Azure Information Protection per generare report centralizzati per tenere traccia dell'adozione delle etichette di Azure Information Protection. Inoltre:

- Monitorare l'accesso utente a documenti e messaggi di posta elettronica etichettati ed eventuali modifiche alla relativa classificazione. 

- Identificare i documenti contenenti informazioni sensibili che possono mettere a rischio l'organizzazione se non protette e attenuare il rischio seguendo le raccomandazioni.

Attualmente, i dati visualizzati vengono aggregati dai client Azure Information Protection, dagli scanner Azure Information Protection e dai computer Windows che eseguono [Windows Defender Advanced Threat Protection (Windows Defender ATP)](/windows/security/threat-protection/windows-defender-atp/overview).

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

- Nel report **Individuazione dati**:

    - Quali sono i file nei repository dei dati analizzati o i computer Windows 10
    
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

- [Discover and protect sensitive data through Azure Information Protection and Windows Defender ATP](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/Discover-and-protect-sensitive-data-through-Azure-Information/ba-p/297292) (Individuare e proteggere i dati sensibili con Azure Information Protection e Windows Defender ATP)

### <a name="information-collected-and-sent-to-microsoft"></a>Informazioni raccolte e inviate a Microsoft

Per generare questi report gli endpoint inviano i seguenti tipi di informazioni a Microsoft:

- Azione per l'etichetta. Ad esempio impostazione o modifica di un'etichetta, aggiunta o rimozione della protezione, etichette automatiche e consigliate.

- Nome dell'etichetta prima e dopo l'azione dell'etichetta.

- ID del tenant dell'organizzazione.

- ID utente (indirizzo di posta elettronica o UPN).

- Nome del dispositivo dell'utente.

- Per i documenti: Percorso e nome file dei documenti ai quali viene aggiunta l'etichetta.

- Per i messaggi di posta elettronica: Oggetto, mittente e destinatari del messaggio di posta elettronica per i messaggi con etichetta. 

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

## <a name="prerequisites-for-azure-information-protection-analytics"></a>Prerequisiti per l'analitica di Azure Information Protection
Per visualizzare i report di Azure Information Protection e creare report personalizzati, verificare che siano soddisfatti i requisiti seguenti.

|Requisito|Altre informazioni|
|---------------|--------------------|
|Un abbonamento di Azure che include Log Analytics|Vedere la pagina dei [prezzi di Monitoraggio di Azure](https://azure.microsoft.com/pricing/details/log-analytics).<br /><br />Se non si dispone di un abbonamento di Azure o attualmente non si usa Azure Log Analytics, la pagina dei prezzi include un collegamento per una versione di valutazione gratuita.|
|Client Azure Information Protection (versione attualmente disponibile a livello generale o versione di anteprima) o versione di anteprima del client per l'etichettatura unificata Azure Information Protection|Se non è ancora stata installata una di queste versioni del client, è possibile scaricarle e installarle dall'Area download Microsoft:<br /> - [Client Azure Information Protection](https://www.microsoft.com/en-us/download/details.aspx?id=53018) <br /> - [Client per l'etichettatura unificata Azure Information Protection](https://www.microsoft.com/en-us/download/details.aspx?id=57440)|
|Per il report **Individuazione e rischio**: <br /><br />- Per visualizzare i dati da archivi dati locali, è stata distribuita almeno un'istanza dello scanner di Azure Information Protection (versione attualmente disponibile a livello generale o versione di anteprima) <br /><br />- Per visualizzare i dati dai computer Windows 10, tali computer devono disporre come minimo della build 1809 ed è necessario usare Windows Defender Advanced Threat Protection (Windows Defender ATP) e aver abilitato la funzionalità di integrazione di Azure Information Protection da Windows Defender Security Center|Per le istruzioni di installazione per lo scanner, vedere [Distribuzione dello scanner di Azure Information Protection per classificare e proteggere automaticamente i file](deploy-aip-scanner.md). <br /><br />Per informazioni sulla configurazione e l'uso della funzionalità di integrazione di Azure Information Protection da Windows Defender Security Center, vedere [Panoramica della protezione delle informazioni in Windows](/windows/security/threat-protection/windows-defender-atp/information-protection-in-windows-overview).|
|Per il report **Raccomandazioni**: <br /><br />- Per aggiungere un nuovo repository dei dati dal portale di Azure come azione consigliata, è necessario usare la versione di anteprima corrente dello scanner di Azure Information Protection |Per distribuire la versione di anteprima dello scanner, vedere [Distribuzione della versione di anteprima dello scanner di Azure Information Protection per classificare e proteggere automaticamente i file](deploy-aip-scanner-preview.md).|

### <a name="permissions-required-for-azure-information-protection-analytics"></a>Autorizzazioni necessarie per la funzionalità di analisi di Azure Information Protection

Specificatamente per la funzionalità di analisi di Azure Information Protection, dopo aver configurato l'area di lavoro di Azure Log Analytics, è possibile usare il ruolo di amministratore di Azure AD Ruolo con autorizzazioni di lettura per la sicurezza come alternativa ad altri ruoli di Azure AD che supportano la gestione di Azure Information Protection nel portale di Azure.

Poiché questa funzionalità usa Monitoraggio di Azure, il controllo degli accessi in base al ruolo per Azure controlla anche l'accesso all'area di lavoro. È quindi necessario un ruolo di Azure, nonché un ruolo di amministratore di Azure AD per gestire l'analisi di Azure Information Protection. Se non si ha familiarità con i ruoli di Azure, può risultare utile leggere [Differenze tra i ruoli di controllo dell'accesso in base al ruolo di Azure e i ruoli di amministratore di Azure AD](https://docs.microsoft.com/azure/role-based-access-control/rbac-and-directory-admin-roles#differences-between-azure-rbac-roles-and-azure-ad-administrator-roles).

Dettagli:

1. Uno dei [ruoli di amministratore di Azure AD](/azure/active-directory/active-directory-assign-admin-roles-azure-portal) seguenti per accedere al pannello di analisi di Azure Information Protection:
    
    - Per creare l'area di lavoro di Log Analytics o per creare query personalizzate:
    
        - **Amministratore di Information Protection**
        - **Amministratore della sicurezza**
        - **Amministratore globale**
    
    - Dopo aver creato l'area di lavoro, è possibile usare il ruolo seguente con meno autorizzazioni per visualizzare i dati raccolti:
    
        - **Ruolo con autorizzazioni di lettura per la sicurezza**
    
    > [!NOTE] 
    > Se è stata eseguita la migrazione del tenant all'archivio di etichettatura unificata, l'account deve essere un amministratore globale o uno dei ruoli elencati ed essere autorizzato ad accedere al Centro sicurezza e conformità di Office 365. [Altre informazioni](configure-policy-migrate-labels.md#important-information-about-administrative-roles)

2. È anche necessario uno dei [ruoli di Azure Log Analytics](https://docs.microsoft.com/azure/azure-monitor/platform/manage-access#managing-access-to-log-analytics-using-azure-permissions) o dei [ruoli di Azure](https://docs.microsoft.com/azure/role-based-access-control/overview#role-assignments) standard seguenti per accedere all'area di lavoro di Azure Log Analytics:
    
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

## <a name="configure-a-log-analytics-workspace-for-the-reports"></a>Configurare un'area di lavoro di Log Analytics per i report

1. Se non già stato fatto, aprire una nuova finestra del browser e [accedere al portale di Azure](https://portal.azure.com) con un account che dispone delle [autorizzazioni necessarie per le analisi di Azure Information Protection](#permissions-required-for-azure-information-protection-analytics). Quindi passare al pannello **Azure Information Protection**. 
    
    Ad esempio, dal menu hub fare clic su **Tutti i servizi** e iniziare a digitare **Informazioni** nella casella Filtro. Selezionare **Azure Information Protection**.
    
2. Individuare le opzioni del menu **Gestisci** e selezionare **Configura le analisi (anteprima)**.

3. Nel pannello **Log Analytics di Azure Information Protection** viene visualizzato un elenco delle eventuali aree di lavoro di Log Analytics di proprietà del tenant. Eseguire una delle operazioni seguenti:
    
    - Per creare una nuova area di lavoro di Log Analytics: Selezionare **Crea nuova area di lavoro** e specificare le informazioni richieste nel pannello **Area di lavoro di Log Analytics**.
    
    - Per usare un'area di lavoro di Log Analytics già esistente: Selezionare l'area di lavoro dall'elenco.

Per assistenza nella creazione dell'area di lavoro di Log Analytics, vedere [Creare un'area di lavoro di Log Analytics nel portale di Azure](https://docs.microsoft.com/azure/log-analytics/log-analytics-quick-create-workspace).

Quando viene completata la configurazione dell'area di lavoro si è pronti per visualizzare i report.

> [!NOTE]
> Esiste attualmente un problema noto con la visualizzazione dei dati per la prima volta nei report. Se si verifica questo problema, nei criteri globali configurare l'[impostazione dei criteri](configure-policy-settings.md) **Invia i dati di controllo a Log Analytics di Azure Information Protection** su **No** e salvare il criterio. Modificare quindi la stessa impostazione specificando **Sì** e salvare il criterio. Dopo il [download della modifica](configure-policy.md#making-changes-to-the-policy) da parte dei client, possono essere richiesti fino a 30 minuti prima che gli eventi di controllo diventino visibili nell'area di lavoro Log Analytics.

## <a name="how-to-view-the-reports"></a>Come visualizzare i report

Nel pannello Azure Information Protection trovare le opzioni del menu **Dashboard** e scegliere una delle opzioni seguenti:

- **Report di utilizzo (anteprima)**: usare questo report per vedere come vengono usate le etichette. 

- **Log attività (anteprima)**: usare questo report per visualizzare le azioni di etichettatura dagli utenti e per i dispositivi e i percorsi di file.
    
    Questo report contiene un'opzione **Colonne** che consente di visualizzare ulteriori informazioni sulle attività rispetto alla visualizzazione predefinita.

- **Individuazione dei dati (anteprima)**: usare questo report per visualizzare informazioni sui file trovati dagli scanner o da Windows Defender ATP.

- **Raccomandazioni (anteprima)**: usare questo report per identificare i file che contengono informazioni sensibili e attenuare il rischio seguendo le raccomandazioni.
    
    La distribuzione di questo report ai tenant è in corso, pertanto, se non è visibile, riprovare tra qualche giorno.
    
    Quando si seleziona un elemento, l'opzione **Visualizza i dati** consente di visualizzare le attività di controllo che hanno attivato la raccomandazione.

> [!NOTE]
> È presente un problema noto per cui nei percorsi e nomi di file la visualizzazione di caratteri non ASCII viene sostituita da punti interrogativi (**?**) quando le impostazioni locali del sistema operativo di invio corrispondono all'inglese.

## <a name="how-to-modify-the-reports"></a>Come modificare i report

Selezionare l'icona della query nel dashboard per aprire un pannello **Ricerca log**: 

![Icona di Log Analytics per personalizzare i report di Azure Information Protection](./media/log-analytics-icon.png)


I dati registrati per Azure Information Protection vengono archiviati nella tabella seguente: **InformationProtectionLogs_CL**

## <a name="next-steps"></a>Passaggi successivi
Dopo aver esaminato le informazioni nei report, si potrebbe decidere di apportare modifiche ai criteri di Azure Information Protection. Per istruzioni, vedere [Configurazione dei criteri di Azure Information Protection](configure-policy.md).

Se è disponibile un abbonamento a Microsoft 365, è anche possibile visualizzare l'utilizzo delle etichette nel Centro sicurezza Microsoft 365 e nel Centro conformità Microsoft 365. Per altre informazioni, vedere [Visualizzare l'utilizzo delle etichette con Analisi delle etichette](/Office365/SecurityCompliance/label-analytics).
