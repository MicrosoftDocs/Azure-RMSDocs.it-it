---
title: Reporting centralizzato per Azure Information Protection
description: Come usare il reporting centralizzato per monitorare l'adozione delle etichette di Azure Information Protection e trovare i file che contengono informazioni riservate
author: cabailey
ms.author: cabailey
ms.date: 02/26/2019
manager: barbkess
ms.topic: article
ms.collection: M365-security-compliance
ms.prod: ''
ms.service: information-protection
ms.assetid: b2da2cdc-74fd-4bfb-b3c2-2a3a59a6bf2e
ms.reviewer: lilukov
ms.suite: ems
ms.openlocfilehash: 319365dd5dfa7c9c5cb82532faa179334c8f0b0f
ms.sourcegitcommit: dde803603371dc30d40ca7225f330163bcc7c103
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/26/2019
ms.locfileid: "56825969"
---
# <a name="central-reporting-for-azure-information-protection"></a>Reporting centralizzato per Azure Information Protection

>*Si applica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*

> [!NOTE]
> Al momento questa funzionalità è disponibile in anteprima ed è soggetta a modifiche.

Usare le funzionalità di analisi di Azure Information Protection per generare report centralizzati per tenere traccia dell'adozione delle etichette di Azure Information Protection. Inoltre:

- Monitorare l'accesso utente a documenti e messaggi di posta elettronica etichettati ed eventuali modifiche alla relativa classificazione. 

- Identificare i documenti che contengono informazioni riservate e devono essere protetti.

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

Queste informazioni vengono archiviate in un'area di lavoro di Azure Log Analytics di proprietà dell'organizzazione e possono essere visualizzate, indipendentemente da Azure Information Protection, dagli utenti con i diritti di accesso all'area di lavoro. Per informazioni dettagliate, vedere la sezione [Autorizzazioni necessarie per la funzionalità di analisi di Azure Information Protection](#permissions-required-for-azure-information-protection-analytics). Per informazioni sulla gestione dell'accesso all'area di lavoro, vedere la sezione [Gestire utenti e account](/azure/azure-monitor/platform/manage-access#manage-accounts-and-users) nella documentazione di Azure.

> [!NOTE]
> L'area di lavoro di Azure Log Analytics per Azure Information Protection include una casella di controllo per le corrispondenze di contenuto del documento. Quando si seleziona questa casella di controllo vengono raccolti anche i dati effettivi identificati da tipi di informazioni riservate o dalle condizioni personalizzate. Possono essere inclusi ad esempio numeri di carta di credito, numeri di previdenza sociale, numeri di passaporto e numeri di conto bancario. Se non si vuole raccogliere questi dati, non selezionare la casella di controllo.
>
> Attualmente queste informazioni non vengono visualizzate nei report, ma possono essere visualizzate e recuperate tramite query.

## <a name="prerequisites-for-azure-information-protection-analytics"></a>Prerequisiti per l'analitica di Azure Information Protection
Per visualizzare i report di Azure Information Protection e creare report personalizzati, verificare che siano soddisfatti i requisiti seguenti.

|Requisito|Altre informazioni|
|---------------|--------------------|
|Un abbonamento di Azure che include Log Analytics|Vedere la pagina dei [prezzi di Monitoraggio di Azure](https://azure.microsoft.com/pricing/details/log-analytics).<br /><br />Se non si dispone di un abbonamento di Azure o attualmente non si usa Azure Log Analytics, la pagina dei prezzi include un collegamento per una versione di valutazione gratuita.|
|Client Azure Information Protection (versione disponibile a livello generale corrente o versione di anteprima) o versione di anteprima del client per l'etichettatura unificata Azure Information Protection|Se non è ancora stata installata una di queste versioni del client, è possibile scaricarle e installarle dall'Area download Microsoft:<br /> - [Client Azure Information Protection](https://www.microsoft.com/en-us/download/details.aspx?id=53018) <br /> - [Client per l'etichettatura unificata Azure Information Protection](https://www.microsoft.com/en-us/download/details.aspx?id=57440)|
|Per il report **Individuazione e rischio**: <br /><br />- Per visualizzare i dati da archivi dati locali, è stata distribuita almeno un'istanza dello scanner di Azure Information Protection (attualmente disponibile a livello generale o in versione di anteprima) <br /><br />- Per visualizzare i dati dai computer Windows 10, tali computer devono disporre come minimo della build 1809 ed è necessario usare Windows Defender Advanced Threat Protection (Windows Defender ATP) e aver abilitato la funzionalità di integrazione di Azure Information Protection da Windows Defender Security Center|Per le istruzioni di installazione per lo scanner, vedere [Distribuzione dello scanner di Azure Information Protection per classificare e proteggere automaticamente i file](deploy-aip-scanner.md). Se si esegue l'aggiornamento da una versione precedente dello scanner, vedere [Aggiornamento dello scanner di Azure Information Protection](./rms-client/client-admin-guide.md#upgrading-the-azure-information-protection-scanner).<br /><br />Per informazioni sulla configurazione e l'uso della funzionalità di integrazione di Azure Information Protection da Windows Defender Security Center, vedere [Panoramica della protezione delle informazioni in Windows](/windows/security/threat-protection/windows-defender-atp/information-protection-in-windows-overview).|

### <a name="permissions-required-for-azure-information-protection-analytics"></a>Autorizzazioni necessarie per la funzionalità di analisi di Azure Information Protection

Specificatamente per la funzionalità di analisi di Azure Information Protection, dopo aver configurato l'area di lavoro di Azure Log Analytics, è possibile usare il ruolo di amministratore di Azure AD Ruolo con autorizzazioni di lettura per la sicurezza come alternativa ad altri ruoli di Azure AD che supportano la gestione di Azure Information Protection nel portale di Azure.

Poiché questa funzionalità usa Monitoraggio di Azure, il controllo degli accessi in base al ruolo per Azure controlla anche l'accesso all'area di lavoro. È quindi necessario un ruolo di Azure, nonché un ruolo di amministratore di Azure AD per gestire l'analisi di Azure Information Protection. Se non si ha familiarità con i ruoli di Azure, può risultare utile leggere [Differenze tra i ruoli di controllo dell'accesso in base al ruolo di Azure e i ruoli di amministratore di Azure AD](https://docs.microsoft.com/azure/role-based-access-control/rbac-and-directory-admin-roles#differences-between-azure-rbac-roles-and-azure-ad-administrator-roles).

Dettagli:

1. Per accedere al pannello della funzionalità di analisi di Azure Information Protection nel portale di Azure, è necessario disporre di uno dei [ruoli di amministratore di Azure AD](/azure/active-directory/active-directory-assign-admin-roles-azure-portal) seguenti:
    
    - Per creare l'area di lavoro di Log Analytics o per creare query personalizzate, è necessario uno dei ruoli seguenti:
    
        - **Amministratore di Information Protection**
        - **Amministratore della sicurezza**
        - **Amministratore globale**
    
    - Per visualizzare i dati dopo la creazione dell'area di lavoro di Log Analytics, è necessario uno dei ruoli seguenti:
    
        - **Ruolo con autorizzazioni di lettura per la sicurezza**
        - **Amministratore di Information Protection**
        - **Amministratore della sicurezza**
        - **Amministratore globale**
    
    > [!NOTE] 
    > Se è stata eseguita la migrazione del tenant all'archivio di etichettatura unificata, l'account deve essere un amministratore globale o uno dei ruoli elencati ed essere autorizzato ad accedere al Centro sicurezza e conformità di Office 365. [Altre informazioni](configure-policy-migrate-labels.md#important-information-about-administrative-roles)

2. Per accedere all'area di lavoro di Azure Log Analytics, è necessario uno dei [ruoli di Azure Log Analytics](https://docs.microsoft.com/azure/azure-monitor/platform/manage-access#managing-access-to-log-analytics-using-azure-permissions) o dei [ruoli di Azure](https://docs.microsoft.com/azure/role-based-access-control/overview#role-assignments) standard seguenti:
    
    - Per creare un'area di lavoro di Log Analytics o per creare query personalizzate, uno dei ruoli seguenti:
    
        - **Collaboratore di Log Analytics**
        - Ruolo di Azure: **Proprietario** o **Collaboratore**
    
    - Per visualizzare i dati in un'area di lavoro di Log Analytics dopo la creazione dell'area di lavoro, è necessario uno dei ruoli seguenti:
    
        - **Lettore di Log Analytics**
        - Ruolo di Azure: **Lettore**

#### <a name="minimum-roles-to-view-the-reports"></a>Ruoli minimi per visualizzare i report

Dopo aver configurato l'area di lavoro per l'analisi di Azure Information Protection, i ruoli minimi necessari per visualizzare i report sono i due seguenti:

- Ruolo di amministratore di Azure AD: **Ruolo con autorizzazioni di lettura per la sicurezza**
- Ruolo di Azure: **Lettore di Log Analytics**

## <a name="configure-a-log-analytics-workspace-for-the-reports"></a>Configurare un'area di lavoro di Log Analytics per i report

1. Se non già stato fatto, aprire una nuova finestra del browser e [accedere al portale di Azure](https://portal.azure.com) con un account che dispone delle [autorizzazioni necessarie per le analisi di Azure Information Protection](#permissions-required-for-azure-information-protection-analytics). Quindi passare al pannello **Azure Information Protection**. 
    
    Ad esempio, dal menu hub fare clic su **Tutti i servizi** e iniziare a digitare **Informazioni** nella casella Filtro. Selezionare **Azure Information Protection**.
    
2. Individuare le opzioni del menu **Gestisci** e selezionare **Configura le analisi (anteprima)**.

3. Nel pannello **Log Analytics di Azure Information Protection** viene visualizzato un elenco delle eventuali aree di lavoro di Log Analytics di proprietà del tenant. Eseguire una delle operazioni seguenti:
    
    - Per creare una nuova area di lavoro di Log Analytics: Selezionare **Crea nuova area di lavoro** e specificare le informazioni richieste nel pannello **Area di lavoro di Log Analytics**.
    
    - Per usare un'area di lavoro di Log Analytics già esistente: Selezionare l'area di lavoro dall'elenco.

Per assistenza nella creazione dell'area di lavoro di Log Analytics, vedere [Creare un'area di lavoro di Log Analytics nel portale di Azure](https://docs.microsoft.com/azure/log-analytics/log-analytics-quick-create-workspace).

Quando viene completata la configurazione dell'area di lavoro si è pronti per visualizzare i report.

## <a name="how-to-view-the-reports"></a>Come visualizzare i report

Nel pannello Azure Information Protection trovare le opzioni del menu **Dashboard** e scegliere una delle opzioni seguenti:

- **Report di utilizzo (anteprima)**: usare questo report per vedere come vengono usate le etichette. 

- **Log attività (anteprima)**: usare questo report per visualizzare le azioni di etichettatura dagli utenti e per i dispositivi e i percorsi di file.
    
    Questo report contiene un'opzione **Colonne** che consente di visualizzare ulteriori informazioni sulle attività rispetto alla visualizzazione predefinita.

- **Individuazione dei dati (anteprima)**: usare questo report per visualizzare informazioni sui file trovati dagli scanner o da Windows Defender ATP.

> [!NOTE]
> È presente un problema noto per cui nei percorsi e nomi di file la visualizzazione di caratteri non ASCII viene sostituita da punti interrogativi (**?**) quando le impostazioni locali del sistema operativo di invio corrispondono all'inglese.

## <a name="how-to-modify-the-reports"></a>Come modificare i report

Selezionare l'icona della query nel dashboard per aprire un pannello **Ricerca log**: 

![Icona di Log Analytics per personalizzare i report di Azure Information Protection](./media/log-analytics-icon.png)


I dati registrati per Azure Information Protection vengono archiviati nella tabella seguente: **InformationProtectionLogs_CL**

## <a name="next-steps"></a>Passaggi successivi
Dopo aver esaminato le informazioni nei report, si potrebbe decidere di apportare modifiche ai criteri di Azure Information Protection. Per istruzioni, vedere [Configurazione dei criteri di Azure Information Protection](configure-policy.md).
