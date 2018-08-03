---
title: Problemi risolti da Azure Rights Management - AIP
description: Identificare i requisiti o i possibili problemi dell'organizzazione e scoprire la soluzione offerta dalla tecnologia Azure RMS.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 05/21/2018
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: b551c62d-5ac6-4359-85b3-90693e77b37f
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 8f57c33f023cd45fd2538244520b77a89f944db1
ms.sourcegitcommit: 949bf02d5d12bef8e26d89ad5d6a0d5cc7826135
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/02/2018
ms.locfileid: "39474728"
---
# <a name="what-problems-does-azure-rms-solve"></a>Problemi risolti da Azure RMS

>*Si applica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](http://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

Usare la tabella seguente per identificare i requisiti aziendali o i possibili problemi che può incontrare l'organizzazione per quanto riguarda la protezione di documenti e messaggi di posta elettronica e per scoprire la soluzione offerta dalla tecnologia Azure Rights Management (Azure RMS).

Azure RMS è la tecnologia di protezione usata da [Azure Information Protection](what-is-information-protection.md).

|Requisito o problema|Soluzione fornita da Azure RMS|
|--------------------------|-----------------------|
|Protezione di più tipi di file|√ Nelle prime implementazioni di Rights Management era possibile proteggere, usando la protezione nativa, soltanto i file di Office. Ora, la **protezione generica**, inizialmente offerta dall'applicazione di condivisione Rights Management e ora dal client Azure Information Protection, consente il supporto per più [tipi di file](./rms-client/client-admin-guide-file-types.md).|
|Protezione dei file in qualsiasi situazione|√ Quando un file è [protetto](./rms-client/client-classify-protect.md), la protezione rimane associata al file stesso anche se questo viene salvato o copiato in un'area di archiviazione non controllata dal reparto IT, ad esempio un servizio di archiviazione cloud.|
|Condivisione sicura delle informazioni|√ Quando un file è [protetto](./rms-client/client-classify-protect.md), è possibile condividerlo con altri utenti in tutta sicurezza. Ciò accade, ad esempio, nel caso di un allegato a un messaggio di posta elettronica o un collegamento a un sito di SharePoint. Se le informazioni riservate si trovano all'interno di un messaggio di posta elettronica, è possibile proteggere il messaggio oppure semplicemente usare l'opzione Non inoltrare da Outlook. <br /><br />Il vantaggio di allegare un file protetto invece di proteggere l'intero messaggio di posta elettronica consiste nel fatto che il testo del messaggio di posta elettronica non è crittografato, quindi è possibile includere istruzioni per il primo utilizzo se il messaggio viene inviato all'esterno dell'organizzazione. Chiunque può leggere le istruzioni, ma poiché il documento allegato è protetto, solo gli utenti autorizzati potranno aprirlo, anche se il messaggio di posta elettronica o il documento viene inoltrato ad altre persone.|
|Controllo e monitoraggio|√ È possibile [controllare e monitorare l'utilizzo](./deploy-use/log-analyze-usage.md) dei file protetti, anche all'esterno dell'organizzazione.<br /><br />Si supponga, ad esempio, di essere un dipendente della società Contoso, Ltd e di lavorare a un progetto comune con tre persone della società Fabrikam, Inc. Si invia a queste tre persone un documento protetto e impostato come di sola lettura. La funzionalità di controllo di Azure Rights Management può fornire le informazioni seguenti:<br /><br />- Se e quando le persone specificate in Fabrikam hanno aperto il documento.<br /><br />- Se altre persone che non sono state specificate hanno tentato invano di aprire il documento, forse perché questo era stato inoltrato o salvato in una posizione condivisa e accessibile da altri utenti.<br /><br />- Se una delle persone specificate ha tentato invano di stampare o modificare il documento.<br /><br />Il [sito di rilevamento dei documenti](./rms-client/client-track-revoke.md), inoltre, consente a utenti e amministratori di monitorare e, se necessario, revocare l'accesso ai documenti protetti.|
|Supporto di tutti i dispositivi di uso comune e non solo dei computer Windows|√ I [dispositivi supportati](./requirements-client-devices.md) includono:<br /><br />- Computer e telefoni Windows<br /><br />- Computer Mac<br /><br />- Tablet e telefoni iOS<br /><br />- Tablet e telefoni Android|
|Supporto della collaborazione business-to-business|√ Poiché Azure Rights Management è un servizio cloud, per poter condividere contenuti protetti con altre organizzazioni non è necessario configurare esplicitamente trust con queste ultime. Se queste organizzazioni dispongono già di una directory di Office 365 o di Azure AD, la collaborazione tra organizzazioni è supportata automaticamente. In caso contrario, gli utenti possono ottenere una sottoscrizione gratuita a [RMS per utenti singoli](rms-for-individuals.md) oppure usare un account Microsoft per le [applicazioni che supportano questo tipo di autenticazione per Azure Information Protection](secure-collaboration-documents.md#supported-scenarios-for-opening-protected-documents).|
|Supporto per servizi locali e per Office 365|√ Oltre a garantire [facile integrazione con Office 365](office-apps-services-support.md), Azure Rights Management può essere usato anche con i servizi locali seguenti quando si distribuisce il [connettore RMS](./deploy-use/deploy-rms-connector.md):<br /><br />- Exchange Server 2016<br /><br />- SharePoint Server<br /><br />- Windows Server con la funzionalità Infrastruttura di classificazione file|
|Facilità di attivazione|√ Per le nuove sottoscrizioni, l'attivazione è automatica. Per le sottoscrizione esistenti, è possibile [attivare il servizio Rights Management](./deploy-use/activate-service.md) con solo pochi clic nel portale di gestione. In alternativa, se si preferisce il controllo della riga di comando, sono sufficienti due comandi di PowerShell.|
|Scalabilità a livello di intera organizzazione, in base alle esigenze|√ Poiché Azure Rights Management viene eseguito come servizio cloud e offre l'elasticità tipica di Azure in termini di scalabilità verticale e orizzontale, non è necessario effettuare il provisioning di server locali aggiuntivi o distribuire tali server.|
|Possibilità di creare criteri semplici e flessibili|√ I [Modelli di protezione personalizzati](./deploy-use/configure-policy-templates.md) forniscono agli amministratori una soluzione rapida e semplice per applicare i criteri e permettono agli utenti di usare il livello di protezione corretto per ciascun documento, nonché di limitare l'accesso al personale dell'organizzazione.<br /><br />Per condividere a livello aziendale un documento sulle strategie, ad esempio, è possibile applicare a tutti i dipendenti interni un criterio di sola lettura. Nel caso di un documento più riservato, ad esempio un report finanziario, è possibile consentire l'accesso ai soli dirigenti dell'azienda.|
|Supporto esteso per applicazioni|√ Azure Rights Management offre una stretta integrazione con applicazioni e servizi di Microsoft Office ed estende il supporto ad altre applicazioni tramite il [client Azure Information Protection](./rms-client/aip-client.md ).<br /><br />√ Gli [SDK di Azure Information Protection](./develop/developers-guide.md) forniscono agli sviluppatori interni e ai fornitori di software le API necessarie per la creazione di applicazioni personalizzate con supporto per Azure Information Protection.<br /><br />Per altre informazioni, vedere [Altre applicazioni che supportano le API di Rights Management](api-support.md).|
|Mantenimento del controllo dei dati da parte del reparto IT|√ Le organizzazioni possono scegliere di gestire la propria chiave del tenant e di usare una soluzione BYOK ("[Bring Your Own Key](./plan-design/plan-implement-tenant-key.md)") e archiviare la chiave del tenant in moduli di protezione hardware (HSM).<br /><br />√ Supporto per il controllo e la [registrazione dell'utilizzo](./deploy-use/log-analyze-usage.md), per consentire agli utenti di eseguire analisi per ottenere informazioni aziendali dettagliate, monitorare i possibili abusi e, in caso di perdita di informazioni, eseguire analisi per scopi legali.<br /><br />√ L'accesso delegato mediante la [funzionalità per utenti con privilegi avanzati](./deploy-use/configure-super-users.md) assicura agli addetti del reparto IT la possibilità di accedere sempre ai contenuti protetti, anche nel caso di documenti protetti da un utente che non fa più parte dell'organizzazione. Paragonate all'accesso delegato, le soluzioni di crittografia peer-to-peer rischiano la perdita dell'accesso ai dati aziendali.<br /><br />√ Sincronizzazione [solo degli attributi della directory richiesti da Azure RMS](/active-directory/active-directory-aadconnectsync-attributes-synchronized#azure-rms) per supportare un'identità comune per gli account Active Directory locali usando uno [strumento di sincronizzazione della directory](/active-directory/active-directory-hybrid-identity-design-considerations-tools-comparison), come Azure AD Connect.<br /><br />√ Abilitazione dell'accesso Single-Sign On senza replicare le password nel cloud usando AD FS.<br /><br />√ Le organizzazioni possono sempre decidere di sospendere l'uso del servizio Azure Rights Management senza perdere l'accesso al contenuto protetto in precedenza da Azure Rights Management. Per informazioni sulle opzioni di rimozione delle autorizzazioni, vedere [Rimozione delle autorizzazioni e disattivazione di Azure Rights Management](./deploy-use/decommission-deactivate.md). Le organizzazioni che hanno distribuito Active Directory Rights Management Services (AD RMS) possono anche [eseguire la migrazione al servizio Azure Rights Management](./plan-design/migrate-from-ad-rms-to-azure-rms.md) senza perdere l'accesso ai dati protetti in precedenza da AD RMS.|
> [!TIP]
> Gli utenti che hanno già acquisito familiarità con la versione locale di Rights Management, Active Directory Rights Management Services (AD RMS), possono essere interessati alla tabella comparativa disponibile in [Confronto tra Azure Rights Management e AD RMS](compare-on-premise.md).

## <a name="security-compliance-and-regulatory-requirements"></a>Requisiti di sicurezza, conformità e normativi
Azure Rights Management supporta i requisiti di sicurezza, conformità e normativi seguenti:

√ Uso di crittografia standard del settore e supporto per FIPS 140-2. Per altre informazioni, vedere [Controlli crittografici usati in Azure RMS: algoritmi e lunghezze delle chiavi](how-does-it-work.md#cryptographic-controls-used-by-azure-rms-algorithms-and-key-lengths).

√ Supporto per moduli di protezione hardware (HSM) Thales per archiviare la chiave del tenant in data center di Microsoft Azure. Azure Rights Management usa ambienti di sicurezza separati per i propri data center in America del Nord, nei paesi EMEA (Europa, Medio Oriente e Africa) e in Asia, così da limitare l'uso delle chiavi all'area pertinente.

√ Certificazione per:

-   ISO/IEC 27001:2013 (include [ISO/IEC 27018](http://azure.microsoft.com/blog/2015/02/16/azure-first-cloud-computing-platform-to-conform-to-isoiec-27018-only-international-set-of-privacy-controls-in-the-cloud/))

-   Attestazioni SOC 2 SSAE 16/ISAE 3402

-   HIPAA BAA

-   EU Model Clause

-   FedRAMP come parte di Azure Active Directory nella certificazione di Office 365, FedRAMP Agency ATO (Authority to Operate) rilasciato da HHS

-   PCI DSS Livello 1

Per altre informazioni su queste certificazioni esterne, vedere il [Centro protezione Azure](http://azure.microsoft.com/support/trust-center/compliance/).

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni tecniche sul funzionamento del servizio Azure Rights Management, vedere [Funzionamento di Azure RMS](how-does-it-work.md).
