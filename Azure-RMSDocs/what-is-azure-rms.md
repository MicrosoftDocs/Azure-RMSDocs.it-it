---
title: Panoramica di Azure Rights Management Protection-AIP
description: Informazioni su Azure Rights Management (Azure RMS), la tecnologia di protezione usata da Azure Information Protection.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 07/23/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: aeeebcd7-6646-4405-addf-ee1cc74df5df
ms.subservice: azurerms
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
search.appverid:
- MET150
ms.openlocfilehash: 70ee7b3733d73ca4603bd1031931381b19d3aa08
ms.sourcegitcommit: 9968a003865ff2456c570cf552f801a816b1db07
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/05/2019
ms.locfileid: "68789762"
---
# <a name="what-is-azure-rights-management"></a>Informazioni su Microsoft Azure Rights Management

>*Si applica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*


Azure Rights Management, spesso abbreviato in Azure RMS, è la tecnologia di protezione usata da [Azure Information Protection](what-is-information-protection.md).

Questo servizio di protezione basato sul cloud usa criteri di crittografia, identità e autorizzazione per proteggere file e messaggi di posta elettronica e funziona su più dispositivi: telefoni, tablet e PC. È possibile proteggere le informazioni all'interno e all'esterno dell'organizzazione perché la protezione resta associata ai dati, anche quando supera i limiti dell'organizzazione.

Si supponga, ad esempio, che un utente invii un documento a una società partner tramite posta elettronica o che salvi il documento sull'unità cloud della società. La protezione permanente fornita da Azure RMS non solo garantisce la sicurezza dei dati aziendali, ma può anche avere valore legale per quanto riguarda la conformità normativa e la conservazione delle informazioni per fini giuridici oppure, più semplicemente, può rappresentare un esempio di procedure consigliate per la gestione delle informazioni.

In particolare, le persone e i servizi autorizzati, ad esempio la ricerca e l'indicizzazione, possono continuare a leggere ed esaminare i dati protetti. risultato non raggiunto facilmente da altre soluzioni di protezione delle informazioni che usano la crittografia peer-to-peer. Questa possibilità viene definita anche "ragionamento sui dati" e riveste un ruolo di importanza critica nel mantenimento del controllo sui dati dell'organizzazione.

La figura seguente illustra come questo servizio offra una soluzione di protezione per Office 365, oltre che per server e servizi locali. Indica inoltre che la protezione è supportata dai dispositivi degli utenti finali di uso comune che eseguono Windows, macOS, iOS e Android.


![Funzionamento di Azure RMS](./media/AzRMS_elements.png)

È possibile usare questa protezione con le sottoscrizioni di Office 365 e con quelle per Azure Information Protection. Per altre informazioni sulle sottoscrizioni disponibili e sulle funzionalità supportate, visitare il sito di [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection/).

## <a name="business-problems-solved-by-azure-rights-management"></a>Problemi aziendali risolti da Azure Rights Management

Usare la tabella seguente per identificare i requisiti o i problemi che può dover affrontare l'organizzazione in merito alla protezione di documenti e messaggi di posta elettronica e per scoprire la soluzione offerta dalla tecnologia Azure Rights Management.


|Requisito o problema|Soluzione fornita da Azure RMS|
|--------------------------|-----------------------|
|Protezione di più tipi di file|√ Nelle prime implementazioni di Rights Management era possibile proteggere, usando la protezione nativa, soltanto i file di Office. Ora, la **protezione generica**, inizialmente offerta dall'applicazione di condivisione Rights Management e ora dal client Azure Information Protection, consente il supporto per più [tipi di file](./rms-client/client-admin-guide-file-types.md).|
|Protezione dei file in qualsiasi situazione|√ Quando un file è [protetto](./rms-client/client-classify-protect.md), la protezione rimane associata al file stesso anche se questo viene salvato o copiato in un'area di archiviazione non controllata dal reparto IT, ad esempio un servizio di archiviazione cloud.|
|Condivisione sicura delle informazioni|√ Quando un file è [protetto](./rms-client/client-classify-protect.md), è possibile condividerlo con altri utenti in tutta sicurezza. Ciò accade, ad esempio, nel caso di un allegato a un messaggio di posta elettronica o un collegamento a un sito di SharePoint. Se le informazioni riservate si trovano all'interno di un messaggio di posta elettronica, è possibile proteggere il messaggio oppure semplicemente usare l'opzione Non inoltrare da Outlook. <br /><br />Il vantaggio di allegare un file protetto invece di proteggere l'intero messaggio di posta elettronica consiste nel fatto che il testo del messaggio di posta elettronica non è crittografato, quindi è possibile includere istruzioni per il primo utilizzo se il messaggio viene inviato all'esterno dell'organizzazione. Chiunque può leggere le istruzioni, ma poiché il documento allegato è protetto, solo gli utenti autorizzati potranno aprirlo, anche se il messaggio di posta elettronica o il documento viene inoltrato ad altre persone.|
|Controllo e monitoraggio|√ È possibile [controllare e monitorare l'utilizzo](log-analyze-usage.md) dei file protetti, anche all'esterno dell'organizzazione.<br /><br />Si supponga, ad esempio, di essere un dipendente della società Contoso, Ltd e di lavorare a un progetto comune con tre persone della società Fabrikam, Inc. Si invia a queste tre persone un documento protetto e impostato come di sola lettura. La funzionalità di controllo di Azure Rights Management può fornire le informazioni seguenti:<br /><br />- Se e quando le persone specificate in Fabrikam hanno aperto il documento.<br /><br />- Se altre persone che non sono state specificate hanno tentato invano di aprire il documento, forse perché questo era stato inoltrato o salvato in una posizione condivisa e accessibile da altri utenti.<br /><br />- Se una delle persone specificate ha tentato invano di stampare o modificare il documento.<br /><br />Il [sito di rilevamento dei documenti](./rms-client/client-track-revoke.md), inoltre, consente a utenti e amministratori di monitorare e, se necessario, revocare l'accesso ai documenti protetti.|
|Supporto di tutti i dispositivi di uso comune e non solo dei computer Windows|√ I  [dispositivi supportati](./requirements-client-devices.md) comprendono:<br /><br />- Computer e telefoni Windows<br /><br />- Computer Mac<br /><br />- Tablet e telefoni iOS<br /><br />- Tablet e telefoni Android|
|Supporto della collaborazione business-to-business|√ Poiché Azure Rights Management è un servizio cloud, per poter condividere contenuti protetti con altre organizzazioni non è necessario configurare esplicitamente trust con queste ultime. Se queste organizzazioni dispongono già di una directory di Office 365 o di Azure AD, la collaborazione tra organizzazioni è supportata automaticamente. In caso contrario, gli utenti possono ottenere una sottoscrizione gratuita a [RMS per utenti singoli](rms-for-individuals.md) oppure usare un account Microsoft per le [applicazioni che supportano questo tipo di autenticazione per Azure Information Protection](secure-collaboration-documents.md#supported-scenarios-for-opening-protected-documents).|
|Supporto per servizi locali e per Office 365|√ Oltre a garantire [facile integrazione con Office 365](office-apps-services-support.md), Azure Rights Management può essere usato anche con i servizi locali seguenti quando si distribuisce il [connettore RMS](deploy-rms-connector.md):<br /><br />- Exchange Server 2016<br /><br />- SharePoint Server<br /><br />- Windows Server con la funzionalità Infrastruttura di classificazione file|
|Facilità di attivazione|√ Per le nuove sottoscrizioni, l'attivazione è automatica. Per le sottoscrizione esistenti, è possibile [attivare il servizio Rights Management](activate-service.md) con solo pochi clic nel portale di gestione. In alternativa, se si preferisce il controllo della riga di comando, sono sufficienti due comandi di PowerShell.|
|Scalabilità a livello di intera organizzazione, in base alle esigenze|√ Poiché Azure Rights Management viene eseguito come servizio cloud e offre l'elasticità tipica di Azure in termini di scalabilità verticale e orizzontale, non è necessario effettuare il provisioning di server locali aggiuntivi o distribuire tali server.|
|Possibilità di creare criteri semplici e flessibili|√ I  [Modelli di protezione personalizzati](configure-policy-templates.md) forniscono agli amministratori una soluzione rapida e semplice per applicare i criteri e permettono agli utenti di usare il livello di protezione corretto per ciascun documento, nonché di limitare l'accesso al personale dell'organizzazione.<br /><br />Per condividere a livello aziendale un documento sulle strategie, ad esempio, è possibile applicare a tutti i dipendenti interni un criterio di sola lettura. Nel caso di un documento più riservato, ad esempio un report finanziario, è possibile consentire l'accesso ai soli dirigenti dell'azienda.|
|Supporto esteso per applicazioni|√ Azure Rights Management offre una stretta integrazione con applicazioni e servizi di Microsoft Office ed estende il supporto ad altre applicazioni tramite il [client Azure Information Protection](./rms-client/aip-client.md ).<br /><br />√ Gli [SDK di Azure Information Protection](./develop/developers-guide.md) forniscono agli sviluppatori interni e ai fornitori di software le API necessarie per la creazione di applicazioni personalizzate con supporto per Azure Information Protection.<br /><br />Per altre informazioni, vedere [Altre applicazioni che supportano le API di Rights Management](api-support.md).|
|Mantenimento del controllo dei dati da parte del reparto IT|√ Le organizzazioni possono scegliere di gestire la propria chiave del tenant e di usare una soluzione BYOK ("[Bring Your Own Key](plan-implement-tenant-key.md)") e archiviare la chiave del tenant in moduli di protezione hardware (HSM).<br /><br />√ Supporto per il controllo e la [registrazione dell'utilizzo](log-analyze-usage.md), per consentire agli utenti di eseguire analisi per ottenere informazioni aziendali dettagliate, monitorare i possibili abusi e, in caso di perdita di informazioni, eseguire analisi per scopi legali.<br /><br />√ L'accesso delegato mediante la [funzionalità per utenti con privilegi avanzati](configure-super-users.md) assicura agli addetti del reparto IT la possibilità di accedere sempre ai contenuti protetti, anche nel caso di documenti protetti da un utente che non fa più parte dell'organizzazione. Paragonate all'accesso delegato, le soluzioni di crittografia peer-to-peer rischiano la perdita dell'accesso ai dati aziendali.<br /><br />√ Sincronizzazione [solo degli attributi della directory richiesti da Azure RMS](/azure/active-directory/hybrid/reference-connect-sync-attributes-synchronized#azure-rms) per supportare un'identità comune per gli account Active Directory locali usando una [soluzione di identità ibrida](/azure/active-directory/hybrid/), come Azure AD Connect.<br /><br />√ Abilitazione dell'accesso Single-Sign On senza replicare le password nel cloud usando ADFS.<br /><br />√ Le organizzazioni possono sempre decidere di sospendere l'uso del servizio Azure Rights Management senza perdere l'accesso al contenuto protetto in precedenza da Azure Rights Management. Per informazioni sulle opzioni di rimozione delle autorizzazioni, vedere [Rimozione delle autorizzazioni e disattivazione di Azure Rights Management](decommission-deactivate.md). Le organizzazioni che hanno distribuito Active Directory Rights Management Services (AD RMS) possono anche [eseguire la migrazione al servizio Azure Rights Management](migrate-from-ad-rms-to-azure-rms.md) senza perdere l'accesso ai dati protetti in precedenza da AD RMS.|
> [!TIP]
> Gli utenti che hanno già acquisito familiarità con la versione locale di Rights Management, Active Directory Rights Management Services (AD RMS), possono essere interessati alla tabella comparativa disponibile in [Confronto tra Azure Rights Management e AD RMS](compare-on-premise.md).

## <a name="security-compliance-and-regulatory-requirements"></a>Requisiti di sicurezza, conformità e normativi
Azure Rights Management supporta i requisiti di sicurezza, conformità e normativi seguenti:

√ Uso di crittografia standard del settore e supporto per FIPS 140-2. Per altre informazioni, vedere [Controlli crittografici usati in Azure RMS: Algoritmi e lunghezze delle chiavi](how-does-it-work.md#cryptographic-controls-used-by-azure-rms-algorithms-and-key-lengths).

√ Supporto per il modulo di protezione hardware nCipher nShield (HSM) per archiviare la chiave del tenant in Microsoft Azure Data Center. Azure Rights Management usa ambienti di sicurezza separati per i propri data center in America del Nord, nei paesi EMEA (Europa, Medio Oriente e Africa) e in Asia, così da limitare l'uso delle chiavi all'area pertinente.

√ Certificazione per:

-   ISO/IEC 27001:2013 (include [ISO/IEC 27018](https://azure.microsoft.com/blog/2015/02/16/azure-first-cloud-computing-platform-to-conform-to-isoiec-27018-only-international-set-of-privacy-controls-in-the-cloud/))

-   Attestazioni SOC 2 SSAE 16/ISAE 3402

-   HIPAA BAA

-   EU Model Clause

-   FedRAMP come parte di Azure Active Directory nella certificazione di Office 365, FedRAMP Agency ATO (Authority to Operate) rilasciato da HHS

-   PCI DSS Livello 1

Per altre informazioni su queste certificazioni esterne, vedere il [Centro protezione Azure](https://azure.microsoft.com/support/trust-center/compliance/).

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni tecniche sul funzionamento del servizio Azure Rights Management, vedere [Funzionamento di Azure RMS](how-does-it-work.md).

