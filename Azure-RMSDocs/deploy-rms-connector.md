---
title: Distribuire il connettore di Rights Management - AIP
description: Istruzioni per distribuire il connettore RMS, che fornisce il servizio di protezione dei dati per le distribuzioni locali esistenti che usano Exchange Server, SharePoint Server o Windows Server e Infrastruttura di classificazione file.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 11/09/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 90e7e33f-9ecc-497b-89c5-09205ffc5066
ms.subservice: connector
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 894f2cd0b2cfc2a8cf15278b46bf508314ebaf71
ms.sourcegitcommit: 2917e822a5d1b21bf465f2cb93cfe46937b1faa7
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/15/2020
ms.locfileid: "79404352"
---
# <a name="deploying-the-azure-rights-management-connector"></a>Distribuzione del connettore di Azure Rights Management

>*Si applica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), windows server 2016, windows Server 2012 R2, windows Server 2012*

Usare queste informazioni per comprendere il funzionamento del connettore di Azure Rights Management e come distribuirlo correttamente per l'organizzazione. Questo connettore garantisce la protezione dei dati per le distribuzioni locali esistenti che usano Microsoft **Exchange Server**, **SharePoint Server** o file server che eseguono Windows Server e **Infrastruttura di classificazione file** (FCI, File Classification Infrastructure).


## <a name="overview-of-the-microsoft-rights-management-connector"></a>Panoramica del connettore Microsoft Rights Management
Il connettore Microsoft Rights Management (RMS) consente di abilitare rapidamente server in locale esistenti in modo che usino la funzionalità Information Rights Management (IRM) con il servizio Microsoft Rights Management (Azure RMS) basati su cloud. Con questa funzionalità, il reparto IT e gli utenti possono proteggere facilmente documenti e immagini sia all'interno sia all'esterno dell'organizzazione, senza necessità di installare un'infrastruttura aggiuntiva o di stabilire relazioni di trust con altre organizzazioni. 

Il connettore RMS è un servizio con footprint ridotto installato in locale, nei server che eseguono Windows Server 2016, Windows Server 2012 R2, Windows Server 2012. Oltre a eseguire il connettore in computer fisici, è possibile anche eseguirlo nelle macchine virtuali, incluse le VM IaaS di Azure. Una volta distribuito, il connettore opera come interfaccia di comunicazione (inoltro) tra i server locali e il servizio cloud come illustrato nell'immagine seguente. Le frecce indicano la direzione in cui vengono avviate le connessioni di rete.

![Panoramica dell'architettura del connettore RMS](./media/RMS_connector.png)


### <a name="on-premises-servers-supported"></a>Server locali supportati

Il connettore RMS supporta i server locali seguenti: Exchange Server, SharePoint Server e i file server che eseguono Windows Server e usano la funzionalità Infrastruttura di classificazione file per classificare e applicare criteri ai documenti Office presenti in una cartella. 

> [!NOTE]
> Se si vuole proteggere più tipi di file (non solo i documenti di Office) usando Infrastruttura di classificazione file, non usare il connettore RMS, ma i [cmdlet di AzureInformationProtection](/powershell/azureinformationprotection/vlatest/aip).

Per informazioni sulle versioni dei server locali supportate dal connettore RMS, vedere [Server locali che supportano Azure RMS](requirements-servers.md).


### <a name="support-for-hybrid-scenarios"></a>Supporto per gli scenari ibridi

È possibile usare il connettore RMS anche se alcuni utenti si connettono ai servizi online, in uno scenario ibrido. Ad esempio, le caselle postali di alcuni utenti utilizzano Exchange Online e le caselle postali di alcuni utenti utilizzano Exchange Server. Dopo aver installato il connettore RMS, tutti gli utenti possono proteggere e utilizzare messaggi di posta elettronica e allegati tramite Azure RMS e la protezione delle informazioni funziona in modo uniforme nelle due configurazioni di distribuzione.

### <a name="support-for-customer-managed-keys-byok"></a>Supporto per le chiavi gestite dal cliente (BYOK)

Se si gestisce la propria chiave del tenant per Azure RMS (scenario BYOK, Bring Your Own Key), il connettore RMS e i server locali che usano tale chiave non accedono al modulo di protezione hardware (HSM) in cui è contenuta. Questo perché tutte le operazioni di crittografia che usano la chiave del tenant vengono eseguite in Azure RMS e non in locale.

Per altre informazioni su questo scenario per la gestione della chiave del tenant, vedere [Pianificazione e implementazione della chiave del tenant di Azure Information Protection](plan-implement-tenant-key.md).

## <a name="prerequisites-for-the-rms-connector"></a>Prerequisiti per l'installazione del connettore RMS
Prima di installare il connettore RMS, accertarsi che i requisiti seguenti siano soddisfatti.

|Requisito|Altre informazioni|
|---------------|--------------------|
|Il servizio di protezione è attivato|[Attivazione del servizio di protezione da Azure Information Protection](activate-service.md)|
|Sincronizzazione delle directory tra le foreste locali di Active Directory e Azure Active Directory|Dopo l'attivazione di RMS, configurare Azure Active Directory per l'uso da parte di utenti e gruppi nel database di Active Directory.<br /><br />**Importante**: è necessario eseguire il passaggio di sincronizzazione della directory in modo che il connettore RMS possa funzionare, anche per una rete di test. Sebbene sia possibile usare Office 365 e Azure Active Directory con account creati manualmente in Azure Active Directory, per usare il connettore è necessario che gli account di Azure Active Directory siano sincronizzati con Servizi di dominio Active Directory. La sincronizzazione manuale della password non è sufficiente.<br /><br />Per ulteriori informazioni, vedere le seguenti risorse:<br /><br />- [Integrare i domini Active Directory locali con Azure Active Directory](/azure/architecture/reference-architectures/identity/azure-ad)<br /><br />- [Confronto degli strumenti di integrazione di directory di identità ibride](/azure/active-directory/hybrid/plan-hybrid-identity-design-considerations-tools-comparison)|
|Almeno due computer membri su cui installare il connettore RMS:<br /><br />-Un computer fisico o virtuale a 64 bit che esegue uno dei sistemi operativi seguenti: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012.<br /><br />- Almeno 1 GB di RAM.<br /><br />- Almeno 64 GB di spazio su disco.<br /><br />- Almeno un'interfaccia di rete.<br /><br />-Accesso a Internet tramite un firewall o un proxy Web che non richiede l'autenticazione.<br /><br />- Ubicazione in una foresta o in un dominio che considera attendibile altre foreste dell'organizzazione contenenti installazioni di server di Exchange o di SharePoint da usare con il connettore RMS.|Per ottenere elevati livelli di tolleranza di errore e disponibilità, è necessario installare il connettore RMS in almeno due computer.<br /><br />**Suggerimento**: se si esegue Outlook Web Access o si usano dispositivi mobili con Exchange ActiveSync IRM ed è fondamentale mantenere l'accesso ai messaggi di posta elettronica e agli allegati protetti da Azure RMS, è consigliabile distribuire un gruppo con carico bilanciato di server del connettore per garantire una disponibilità elevata.<br /><br />Per l'esecuzione del connettore non sono necessari server dedicati. È invece necessario installare il connettore in un computer separato dai server che lo usano.<br /><br />**Importante**: non installare il connettore in un computer che esegue Exchange Server, SharePoint Server o un file server configurato per la funzionalità Infrastruttura di classificazione file, se si desidera usare tale funzionalità da questi servizi con Azure RMS. Inoltre, non installare il connettore in un controller di dominio.<br /><br />In presenza di carichi di lavoro server che si vuole usare con il connettore RMS, con server inclusi in domini non considerati attendibili dal dominio da cui si esegue il connettore, è possibile installare server del connettore RMS aggiuntivi in questi domini non attendibili o in altri domini nelle rispettive foreste. <br /><br />Non sono previsti limiti per il numero di server del connettore che è possibile eseguire per l'organizzazione e tutti i server del connettore installati in un'organizzazione condividono la stessa configurazione. Tuttavia, per configurare il connettore per autorizzare i server, è necessario essere in grado di visualizzare gli account del servizio o del server da autorizzare e questo significa dover eseguire lo strumento di amministrazione di RMS in una foresta da cui è possibile visualizzare tali account.|


## <a name="steps-to-deploy-the-rms-connector"></a>Passaggi per distribuire il connettore RMS

Il connettore non verifica automaticamente tutti i [prerequisiti](deploy-rms-connector.md#prerequisites-for-the-rms-connector) necessari per una corretta distribuzione, quindi assicurarsi che questi siano soddisfatti prima di iniziare. Per la distribuzione è necessario installare il connettore, configurarlo e quindi configurare i server che devono usare il connettore. 

-   **Passaggio 1:**  [installazione del connettore RMS](install-configure-rms-connector.md#installing-the-rms-connector)

-   **Passaggio 2:**  [immissione delle credenziali](install-configure-rms-connector.md#entering-credentials)

-   **Passaggio 3:**  [autorizzazione dei server all'uso del connettore RMS](install-configure-rms-connector.md#authorizing-servers-to-use-the-rms-connector)

-   **Passaggio 4:**  [configurazione del bilanciamento del carico e disponibilità elevata](install-configure-rms-connector.md#configuring-load-balancing-and-high-availability)

-   Facoltativo: [Configurazione del connettore RMS per l'uso di HTTPS](install-configure-rms-connector.md#configuring-the-rms-connector-to-use-https)

-   Facoltativo: [Configurazione del connettore RMS per un server proxy Web](install-configure-rms-connector.md#configuring-the-rms-connector-for-a-web-proxy-server)

-   Facoltativo: [Installazione dello strumento di amministrazione di connettore RMS su computer amministrativi](install-configure-rms-connector.md#installing-the-rms-connector-administration-tool-on-administrative-computers)

-   **Passaggio 5:**  [configurazione dei server per l'uso del connettore RMS](configure-servers-rms-connector.md)

    -   [Configurazione di un server di Exchange per l'uso del connettore](configure-servers-rms-connector.md#configuring-an-exchange-server-to-use-the-connector)

    -   [Configurazione di un server di SharePoint per l'uso del connettore](configure-servers-rms-connector.md#configuring-a-sharepoint-server-to-use-the-connector)

    -   [Configurazione di un file server per consentire l'uso del connettore alla funzionalità Infrastruttura di classificazione file](configure-servers-rms-connector.md#configuring-a-file-server-for-file-classification-infrastructure-to-use-the-connector)


## <a name="next-steps"></a>Passaggi successivi

Procedere al Passaggio 1: [Installazione e configurazione del connettore di Azure Rights Management](install-configure-rms-connector.md).
