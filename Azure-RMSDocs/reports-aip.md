---
title: Reporting centralizzato per Azure Information Protection
description: Come usare il reporting centralizzato per monitorare l'adozione delle etichette di Azure Information Protection e trovare i file che contengono informazioni riservate
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 11/13/2018
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.assetid: b2da2cdc-74fd-4bfb-b3c2-2a3a59a6bf2e
ms.reviewer: lilukov
ms.suite: ems
ms.openlocfilehash: 85ca097a1808c2940ce534c7ce3d0542aaf3f27a
ms.sourcegitcommit: 0f9e2ba05b61f8db08387576a697b8deff45fd36
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/13/2018
ms.locfileid: "51611421"
---
# <a name="central-reporting-for-azure-information-protection"></a>Reporting centralizzato per Azure Information Protection

>*Si applica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*

> [!NOTE]
> Al momento questa funzionalità è disponibile in anteprima ed è soggetta a modifiche. I dati raccolti durante questo periodo di anteprima potrebbero non essere supportati quando la funzionalità passa alla disponibilità di carattere generale.


Usare le analitiche di reporting centralizzato di Azure Information Protection per tenere traccia dell'adozione delle etichette di Azure Information Protection e per monitorare l'accesso utente a documenti e messaggi di posta elettronica provvisti di etichetta e le eventuali modifiche alla classificazione di tali elementi. È anche possibile identificare documenti che contengono informazioni riservate e devono essere protetti.

Attualmente, i dati visualizzati sono aggregati dai client Azure Information Protection e dagli scanner Azure Information Protection.

Ad esempio è possibile visualizzare quanto segue:

- Nel **Report di utilizzo**, in cui è possibile selezionare un periodo di tempo:
    
    - Quali etichette vengono applicate
    
    - Quanti documenti e messaggi di posta elettronica vengono corredati di etichetta
    
    - Quanti documenti e messaggi di posta elettronica vengono protetti
    
    - Quanti utenti e dispositivi applicano etichette a documenti e messaggi di posta elettronica
    
    - Quali applicazioni vengono usate per l'assegnazione di etichette

- Nel report **Individuazione dati**:

    - Quali file si trovano nei repository dei dati analizzati
    
    - Quali file sono provvisti di etichetta e protetti e il percorso dei file in base alle etichette
    
    - Quali file contengono informazioni riservate per categorie note, ad esempio dati finanziari e informazioni personali e il percorso dei file in base a queste categorie
    
I report usano [Azure Log Analytics](/azure/log-analytics/log-analytics-overview) per archiviare i dati in un'area di lavoro di proprietà dell'utente. Se si ha familiarità con il linguaggio di query, è possibile modificare le query e creare nuovi report e dashboard di Power BI. L'esercitazione seguente può risultare utile per la comprensione del linguaggio di query: [Getting Started with the Analytics Portal](https://docs.loganalytics.io/docs/Learn/Getting-Started/Getting-started-with-the-Analytics-portal) (Introduzione al portale Analytics). 

Per altre informazioni, vedere il post di blog [Data discovery, reporting and analytics for all your data with Microsoft Information Protection](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/Data-discovery-reporting-and-analytics-for-all-your-data-with/ba-p/253854) (Rilevamento, report e analitica per tutti i dati utente con Microsoft Information Protection).

### <a name="information-collected-and-sent-to-microsoft"></a>Informazioni raccolte e inviate a Microsoft

Per generare questi report gli endpoint inviano i seguenti tipi di informazioni a Microsoft:

- Azione per l'etichetta. Ad esempio impostazione o modifica di un'etichetta, aggiunta o rimozione della protezione, etichette automatiche e consigliate.

- Nome dell'etichetta prima e dopo l'azione dell'etichetta.

- ID del tenant dell'organizzazione.

- ID utente (indirizzo di posta elettronica o UPN).

- Nome del dispositivo dell'utente.

- Per i documenti: percorso e nome file dei documenti ai quali viene aggiunta l'etichetta.

- Per i messaggi di posta elettronica: oggetto, mittente e destinatari del messaggio di posta elettronica per i messaggi con etichetta. 

- Tipologie di informazioni riservate ([predefinite](https://docs.microsoft.com/office365/securitycompliance/what-the-sensitive-information-types-look-for) e personalizzate) rilevate nel contenuto.

- Versione del client di Azure Information Protection.

- Versione del sistema operativo del client.

Queste informazioni vengono archiviate in un'area di lavoro di Azure Log Analytics di cui si è proprietari e possono essere visualizzate solo dagli utenti che dispongono dei diritti di accesso all'area di lavoro. Per informazioni sulla configurazione dell'accesso all'area di lavoro, vedere la sezione [Gestire utenti e account](/azure/log-analytics/log-analytics-manage-access?toc=/azure/azure-monitor#manage-accounts-and-users) nella documentazione di Azure.

## <a name="prerequisites-for-azure-information-protection-analytics"></a>Prerequisiti per l'analitica di Azure Information Protection
Per visualizzare i report di Azure Information Protection e creare report personalizzati, verificare che siano soddisfatti i requisiti seguenti.

|Requisito|Altre informazioni|
|---------------|--------------------|
|Un abbonamento di Azure che include Log Analytics|Vedere la pagina [Prezzi di Log Analytics](https://azure.microsoft.com/pricing/details/log-analytics).<br /><br />Se non si dispone di un abbonamento di Azure o attualmente non si usa Azure Log Analytics, la pagina dei prezzi include un collegamento per una versione di valutazione gratuita.|
|La versione di anteprima corrente del client di Azure Information Protection.|Se non è ancora stata installata la versione di anteprima corrente del client, è possibile scaricarla e installarla dall'[Area download Microsoft](https://www.microsoft.com/en-us/download/details.aspx?id=53018).|
|Per il report **Individuazione e rischio**: <br /><br />- Deve essere stata distribuita almeno un'istanza dello scanner Azure Information Protection (versione di anteprima corrente)|Per le istruzioni di installazione, vedere [Distribuzione dello scanner di Azure Information Protection per classificare e proteggere automaticamente i file](deploy-aip-scanner.md). <br /><br />Se si esegue l'aggiornamento da una versione precedente dello scanner, vedere [Aggiornamento dello scanner di Azure Information Protection](./rms-client/client-admin-guide.md#upgrading-the-azure-information-protection-scanner).|


## <a name="configure-a-log-analytics-workspace-for-the-reports"></a>Configurare un'area di lavoro di Log Analytics per i report

1. Se non è già stato fatto, aprire una nuova finestra del browser e [accedere al portale di Azure](configure-policy.md#signing-in-to-the-azure-portal). Quindi passare al pannello **Azure Information Protection**. 
    
    Ad esempio, dal menu hub fare clic su **Tutti i servizi** e iniziare a digitare **Informazioni** nella casella Filtro. Selezionare **Azure Information Protection**.
    
2. Individuare le opzioni del menu **Gestisci** e selezionare **Configura le analisi (anteprima)**.

3. Nel pannello **Log Analytics di Azure Information Protection** viene visualizzato un elenco delle eventuali aree di lavoro di Log Analytics di proprietà del tenant. Eseguire una delle operazioni seguenti:
    
    - Per creare una nuova area di lavoro di Log Analytics: selezionare **Crea nuova area di lavoro**, quindi nel pannello **Area di lavoro di Log Analytics** specificare le informazioni richieste.
    
    - Per usare un'area di lavoro di Log Analytics esistente, selezionare l'area di lavoro dall'elenco.

Per assistenza nella creazione dell'area di lavoro di Log Analytics, vedere [Creare un'area di lavoro di Log Analytics nel portale di Azure](https://docs.microsoft.com/azure/log-analytics/log-analytics-quick-create-workspace).

Quando viene completata la configurazione dell'area di lavoro si è pronti per visualizzare i report.

## <a name="how-to-view-the-reports"></a>Come visualizzare i report

Nel pannello Azure Information Protection trovare le opzioni del menu **Dashboard** e scegliere una delle opzioni seguenti:

- **Report di utilizzo (anteprima)**: usare questo report per vedere come vengono usate le etichette. 

- **Individuazione dati (anteprima)**: usare questo report per visualizzare informazioni sui file rilevati dagli scanner.

## <a name="how-to-modify-the-reports"></a>Come modificare i report

Selezionare l'icona della query nel dashboard per aprire un pannello **Ricerca log**: 

![Icona di Log Analytics per personalizzare i report di Azure Information Protection](./media/log-analytics-icon.png)


I dati registrati per Azure Information Protection vengono archiviati nella tabella seguente: **InformationProtectionLogs_CL**

## <a name="next-steps"></a>Passaggi successivi
Dopo aver esaminato le informazioni nei report, si potrebbe decidere di apportare modifiche ai criteri di Azure Information Protection. Per istruzioni, vedere [Configurazione dei criteri di Azure Information Protection](configure-policy.md).