---
# required metadata

title: Distribuzione del connettore di Azure Rights Management | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 05/20/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 90e7e33f-9ecc-497b-89c5-09205ffc5066

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Distribuzione del connettore di Azure Rights Management

*Si applica a: Azure Rights Management, Windows Server 2012, Windows Server 2012 R2*

In questo articolo vengono fornite informazioni sul connettore Azure Rights Management (RMS) e su come è possibile usarlo per garantire la protezione delle informazioni nelle distribuzioni locali esistenti che usano Microsoft Exchange Server, Microsoft SharePoint Server o file server che eseguono Windows Server e usano la funzionalità Infrastruttura di classificazione file di Gestione risorse file server.

> [!TIP] Per uno scenario di esempio generale con screenshot, vedere la sezione [Protezione automatica dei file su file server che eseguono Windows Server e Infrastruttura di classificazione file](../understand-explore/what-admins-users-see.md#automatically-protecting-files-on-file-servers-running-windows-server-and-file-classification-infrastructure) nell'articolo [Azure RMS in azione](../understand-explore/what-admins-users-see.md).

## Panoramica del connettore Microsoft Rights Management
Il connettore Microsoft Rights Management (RMS) consente di abilitare rapidamente server in locale esistenti in modo che usino la funzionalità Information Rights Management (IRM) con il servizio Microsoft Rights Management (Azure RMS) basati su cloud. Con questa funzionalità, il reparto IT e gli utenti possono proteggere facilmente documenti e immagini sia all'interno sia all'esterno dell'organizzazione, senza necessità di installare un'infrastruttura aggiuntiva o di stabilire relazioni di trust con altre organizzazioni. È possibile utilizzare questo connettore anche se alcuni utenti si connettono ai servizi online, in uno scenario ibrido. Ad esempio, le caselle postali di alcuni utenti utilizzano Exchange Online e le caselle postali di alcuni utenti utilizzano Exchange Server. Dopo aver installato il connettore RMS, tutti gli utenti possono proteggere e utilizzare messaggi di posta elettronica e allegati tramite Azure RMS e la protezione delle informazioni funziona in modo uniforme nelle due configurazioni di distribuzione.

Il connettore RMS è un servizio di piccole dimensioni installato localmente su server che eseguono Windows Server 2012 R2, Windows Server 2012 o Windows Server 2008 R2. Oltre a eseguire il connettore in computer fisici, è possibile anche eseguirlo nelle macchine virtuali, incluse le VM IaaS di Azure. Una volta installato e configurato, il connettore opera come interfaccia di comunicazione (inoltro) tra i server locali e il servizio cloud.

Se si gestisce la propria chiave del tenant per Azure RMS (scenario BYOK, Bring Your Own Key), il connettore RMS e i server locali che usano tale chiave non accedono al modulo di protezione hardware (HSM) in cui è contenuta. Questo perché tutte le operazioni di crittografia che usano la chiave del tenant vengono eseguite in Azure RMS e non in locale.

![Panoramica dell'architettura del connettore RMS](../media/RMS_connector.png)

Il connettore RMS supporta i server locali seguenti: Exchange Server, SharePoint Server e i file server che eseguono Windows Server e usano la funzionalità Infrastruttura di classificazione file per classificare e applicare criteri ai documenti Office presenti in una cartella. Se si desidera proteggere tutti i tipi di file utilizzano la classificazione dei file, non utilizzare il connettore RMS, ma utilizzare invece i [cmdlet di protezione di RMS](https://msdn.microsoft.com/library/azure/mt433195.aspx).

> [!NOTE] Per le versioni supportate di questi server locali, vedere [Server locali che supportano Azure RMS](..\get-started\requirements-servers.md).

Nelle sezioni seguenti vengono fornite informazioni sulla pianificazione, installazione e configurazione del connettore RMS. In seguito, è necessario eseguire alcune attività di configurazione post-installazione per consentire ai server dell'organizzazione di usare il connettore.

-   [Prerequisiti per l'installazione del connettore RMS](deploy-rms-connector.md#prerequisites-for-the-rms-connector)

-   **Passaggio 1:** [Installazione del connettore RMS](install-configure-rms-connector.md#installing-the-rms-connector)

-   **Passaggio 2:** [Immissione delle credenziali](install-configure-rms-connector.md#entering-credentials)

-   **Passaggio 3:** [Autorizzazione dei server all'uso del connettore RMS](install-configure-rms-connector.md#authorizing-servers-to-use-the-rms-connector)

-   **Passaggio 4:** [Configurazione del bilanciamento del carico per elevati livelli di disponibilità](install-configure-rms-connector.md#configuring-load-balancing-and-high-availability)

-   Facoltativo: [Configurazione del connettore RMS per l'uso di HTTPS](install-configure-rms-connector.md#configuring-the-rms-connector-to-use-https)

-   Facoltativo: [Configurazione del connettore RMS per un server proxy Web](install-configure-rms-connector.md#configuring-the-rms-connector-for-a-web-proxy-server)

-   Facoltativo: [Installazione dello strumento di amministrazione di connettore RMS su computer amministrativi](install-configure-rms-connector.md#installing-the-rms-connector-administration-tool-on-administrative-computers)

-   **Passaggio 5:** [Configurazione dei server per l'uso del connettore RMS](configure-servers-rms-connector.md)

    -   [Configurazione di un server di Exchange per l'uso del connettore](configure-servers-rms-connector.md#configuring-an-exchange-server-to-use-the-connector)

    -   [Configurazione di un server di SharePoint per l'uso del connettore](configure-servers-rms-connector.md#configuring-a-sharepoint-server-to-use-the-connector)

    -   [Configurazione di un file server per consentire l'uso del connettore alla funzionalità Infrastruttura di classificazione file](configure-servers-rms-connector.md#configuring-a-file-server-for-file-classification-infrastructure-to-use-the-connector)


## Prerequisiti per l'installazione del connettore RMS
Prima di installare il connettore RMS, accertarsi che i requisiti seguenti siano soddisfatti.

|Requisito|Altre informazioni|
|---------------|--------------------|
|È necessario che il servizio Rights Management (RMS) sia attivato|[Attivazione di Azure Rights Management](activate-service.md)|
|Sincronizzazione delle directory tra le foreste locali di Active Directory e Azure Active Directory|Dopo l'attivazione di RMS, configurare Azure Active Directory per l'uso da parte di utenti e gruppi nel database di Active Directory.<br /><br />**Importante**: è necessario eseguire il passaggio di sincronizzazione della directory in modo che il connettore RMS possa funzionare, anche per una rete di test. Sebbene sia possibile usare Office 365 e Azure Active Directory con account creati manualmente in Azure Active Directory, per usare il connettore è necessario che gli account di Azure Active Directory siano sincronizzati con Servizi di dominio Active Directory. La sincronizzazione manuale della password non è sufficiente.<br /><br />Per altre informazioni, vedere le risorse seguenti:<br /><br />[Integrazione delle identità locali con Azure Active Directory](/active-directory/active-directory-aadconnect)<br /><br />[Confronto degli strumenti di integrazione di directory di identità ibride](/active-directory/active-directory-hybrid-identity-design-considerations-tools-comparison)|
|Facoltativo ma consigliato:<br /><br />Abilitare la federazione tra Active Directory locale e Azure Active Directory|È possibile abilitare la federazione delle identità tra la directory locale e Azure Active Directory. Questa configurazione assicura agli utenti maggiore semplicità, grazie alla possibilità di accedere al servizio RMS mediante Single Sign-On. Senza l'accesso Single Sign-On, per poter usare contenuto protetto gli utenti devono immettere le proprie credenziali.<br /><br />Per istruzioni sulla configurazione della federazione tra Servizi di Dominio Active Directory e Azure Active Directory usando ADFS (Active Directory Federation Services), vedere [Elenco di controllo: Uso di ADFS per implementare e gestire Single Sign-On](http://technet.microsoft.com/library/jj205462.aspx) nella libreria di Windows Server.|
|Almeno due computer membri su cui installare il connettore RMS:<br /><br />- Un computer fisico o virtuale a 64 bit che esegue uno dei sistemi operativi seguenti: Windows Server 2012 R2,  Windows Server 2012 o Windows Server 2008 R2.<br /><br />- Almeno 1 GB di RAM.<br /><br />- Almeno 64 GB di spazio su disco.<br /><br />- Almeno un'interfaccia di rete.<br /><br />- Accesso a Internet tramite un firewall o un proxy Web che non richiede l'autenticazione.<br /><br />- Ubicazione in una foresta o in un dominio che considera attendibile altre foreste dell'organizzazione contenenti installazioni di server di Exchange o di SharePoint da usare con il connettore RMS.|Per ottenere elevati livelli di tolleranza di errore e disponibilità, è necessario installare il connettore RMS in almeno due computer.<br /><br />**Suggerimento**: se si esegue Outlook Web Access o si usano dispositivi mobili con Exchange ActiveSync IRM ed è fondamentale mantenere l'accesso ai messaggi di posta elettronica e agli allegati protetti da Azure RMS, è consigliabile distribuire un gruppo con carico bilanciato di server del connettore per garantire una disponibilità elevata.<br /><br />Per l'esecuzione del connettore non sono necessari server dedicati. È invece necessario installare il connettore in un computer separato dai server che lo usano.<br /><br />**Importante**: non installare il connettore in un computer che esegue Exchange Server, SharePoint Server o un file server configurato per la funzionalità Infrastruttura di classificazione file, se si desidera usare tale funzionalità da questi servizi con Azure RMS. Inoltre, non installare il connettore in un controller di dominio.|

## Passaggi successivi

Passare a [Installazione e configurazione del connettore di Azure Rights Management](install-configure-rms-connector.md).

<!--HONumber=May16_HO3-->


