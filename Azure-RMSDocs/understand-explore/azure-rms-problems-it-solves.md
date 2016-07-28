---
title: Problemi risolti da Azure RMS | Azure RMS
description: 
keywords: 
author: cabailey
manager: mbaldwin
ms.date: 07/13/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: b551c62d-5ac6-4359-85b3-90693e77b37f
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 06f615c993d54ab1e8e4a94d7414302481d919b4
ms.openlocfilehash: 17756d4e641c10c0522f7a849634ae67630b363b


---


# Problemi risolti da Azure RMS

*Si applica a: Azure Rights Management, Office 365*

Usare la seguente tabella per identificare i requisiti aziendali e i possibili problemi dell'organizzazione e per scoprire la soluzione fornita da Azure RMS.

|Requisito o problema|Soluzione fornita da Azure RMS|
|--------------------------|-----------------------|
|Protezione di tutti i tipi di file|√ Nella precedente implementazione di Rights Management era possibile proteggere, usando la protezione nativa, soltanto i file di Office. Per [protezione generica](../rms-client/sharing-app-dialog-box.md#what-s-the-difference-between-generic-protection-and-built-in-native-protection) si intende che sono supportati tutti i tipi di file.|
|Protezione dei file in qualsiasi situazione|√ Quando un file viene salvato in un percorso ([protezione sul posto](../rms-client/sharing-app-protect-in-place.md)), i criteri di protezione rimangono associati al file stesso anche se questo viene copiato in un'area di archiviazione non controllata dal reparto IT, ad esempio un servizio di archiviazione cloud.|
|Condivisione sicura dei file tramite posta elettronica|√ Quando un file viene condiviso tramite posta elettronica ([condivisione file protetto](../rms-client/sharing-app-protect-by-email.md)), viene protetto come un allegato a un messaggio di posta elettronica, con istruzioni per l'apertura. Il testo del messaggio di posta non viene crittografato, in modo che il destinatario possa sempre leggere le istruzioni. Il documento allegato, tuttavia, è protetto e può essere aperto solo dagli utenti autorizzati, anche se il messaggio di posta elettronica o il documento viene inoltrato ad altre persone.|
|Controllo e monitoraggio|√ È possibile [controllare e monitorare l'utilizzo](../deploy-use/log-analyze-usage.md) dei file protetti, anche all'esterno dell'organizzazione.<br /><br />Si supponga, ad esempio, di essere un dipendente della società Contoso, Ltd e di lavorare a un progetto comune con tre persone della società Fabrikam, Inc. Si supponga quindi di inviare a queste tre persone un documento protetto e di sola lettura. La funzionalità di controllo di Azure RMS può fornire le seguenti informazioni:<br /><br />- Se e quando le persone specificate in Fabrikam hanno aperto il documento.<br /><br />- Se altre persone che non sono state specificate hanno tentato invano di aprire il documento, forse perché questo era stato inoltrato o salvato in una posizione condivisa e accessibile da altri utenti.<br /><br />- Se una delle persone specificate ha tentato invano di stampare o modificare il documento.|
|Supporto per tutti i dispositivi di uso comune, non solo dei computer Windows|√ I [dispositivi supportati](../get-started/requirements-client-devices.md) includono:<br /><br />- Computer e telefoni Windows<br /><br />- Computer Mac<br /><br />- Tablet e telefoni iOS<br /><br />- Tablet e telefoni Android|
|Supporto della collaborazione business-to-business|√ Poiché Azure RMS è un servizio cloud, per poter condividere contenuti protetti con altre organizzazioni non è necessario configurare esplicitamente dei trust con queste ultime. Se queste organizzazioni dispongono già di una directory di Office 365 o di Azure AD, la collaborazione tra organizzazioni è supportata automaticamente. In caso contrario, gli utenti possono registrarsi per ottenere una sottoscrizione gratuita a [RMS per utenti singoli](rms-for-individuals.md).|
|Supporto per servizi locali e per Office 365|√ Oltre a garantire [facile integrazione con Office 365](office-apps-services-support.md), Azure RMS può essere usato anche con i servizi locali seguenti quando si distribuisce il [connettore RMS](../deploy-use/deploy-rms-connector.md):<br /><br />- Exchange Server 2016<br /><br />- SharePoint Server<br /><br />- Windows Server con la funzionalità Infrastruttura di classificazione file|
|Facilità di attivazione|√ L'[attivazione del servizio Rights Management](../deploy-use/activate-service.md) per gli utenti richiede solo pochi clic nel portale di Azure classico.|
|Scalabilità a livello di intera organizzazione, in base alle esigenze|√ Poiché Azure RMS viene eseguito come servizio cloud e offre l'elasticità tipica di Azure in termini di scalabilità verticale e orizzontale, non è necessario effettuare il provisioning di server locali aggiuntivi o distribuire tali server.|
|Possibilità di creare criteri semplici e flessibili|√ I [modelli di criteri per i diritti personalizzati](../deploy-use/configure-custom-templates.md) forniscono agli amministratori una soluzione rapida e semplice per applicare i criteri e permettono agli utenti di usare il livello di protezione corretto per ciascun documento, nonché di limitare l'accesso al personale dell'organizzazione.<br /><br />Per condividere a livello aziendale un documento sulle strategie, ad esempio, è possibile applicare a tutti i dipendenti interni un criterio di sola lettura. Nel caso di un documento più riservato, ad esempio un report finanziario, è possibile consentire l'accesso ai soli dirigenti dell'azienda.|
|Supporto esteso per applicazioni|√ Azure RMS è caratterizzato da una stretta integrazione con applicazioni e servizi di Microsoft Office ed estende il supporto ad altre applicazioni usando l'applicazione RMS sharing.√ Azure RMS è caratterizzato da una stretta integrazione con applicazioni e servizi di Microsoft Office ed estende il supporto ad altre applicazioni usando l'applicazione RMS sharing.<br /><br />√ [Microsoft Rights Management SDK](../develop/developers-guide.md#software-development-kits) fornisce agli sviluppatori interni e ai fornitori di software le API necessarie per la creazione di applicazioni personalizzate con supporto per Azure RMS.<br /><br />Per altre informazioni, vedere [Altre applicazioni che supportano le API RMS](api-support.md).|
|Mantenimento del controllo dei dati da parte del reparto IT|√ Le organizzazioni possono scegliere di gestire la propria chiave del tenant e di usare una soluzione BYOK ("[Bring Your Own Key](../plan-design/plan-implement-tenant-key.md)") e archiviare la chiave del tenant in moduli di protezione hardware (HSM).<br /><br />√ Supporto per il controllo e la [registrazione dell'utilizzo](../deploy-use/log-analyze-usage.md), per consentire agli utenti di eseguire analisi per ottenere informazioni aziendali dettagliate, monitorare i possibili abusi e, in caso di perdita di informazioni, eseguire analisi per scopi legali.<br /><br />√ L'accesso delegato mediante la [funzionalità per utenti con privilegi avanzati](../deploy-use/configure-super-users.md) assicura agli addetti del reparto IT la possibilità di accedere sempre ai contenuti protetti, anche nel caso di documenti protetti da un utente che non fa più parte dell'organizzazione. Paragonate all'accesso delegato, le soluzioni di crittografia peer-to-peer rischiano la perdita dell'accesso ai dati aziendali.<br /><br />√ Sincronizzazione [solo degli attributi della directory richiesti da Azure RMS](/active-directory/active-directory-aadconnectsync-attributes-synchronized#azure-rms) per supportare un'identità comune per gli account Active Directory locali usando uno [strumento di sincronizzazione della directory](/active-directory/active-directory-hybrid-identity-design-considerations-tools-comparison), come Azure AD Connect.<br /><br />√ Abilitazione dell'accesso Single-Sign On senza replicare le password nel cloud usando AD FS.<br /><br />√ Le organizzazioni possono sempre decidere di sospendere l'uso di Azure RMS, senza perdere l'accesso al contenuto protetto in precedenza da Azure RMS. Per informazioni sulle opzioni di rimozione delle autorizzazioni, vedere [Rimozione delle autorizzazioni e disattivazione di Azure Rights Management](../deploy-use/decommission-deactivate.md). Le organizzazioni che hanno distribuito Active Directory Rights Management Services (AD RMS), possono anche [eseguire la migrazione ad Azure RMS](../plan-design/migrate-from-ad-rms-to-azure-rms.md) senza perdere l'accesso ai dati protetti in precedenza da AD RMS.|
> [!TIP]
> Gli utenti che hanno già acquisito familiarità con la versione locale di Rights Management, Active Directory Rights Management Services (AD RMS), possono essere interessati alla tabella comparativa disponibile in [Confronto tra Azure Rights Management e AD RMS](compare-azure-rms-ad-rms.md).

## Requisiti di sicurezza, conformità e normativi
Azure RMS supporta i requisiti di sicurezza, conformità e normativi seguenti:

√ Uso di crittografia standard del settore e supporto per FIPS 140-2. Per altre informazioni, vedere [Controlli crittografici usati in Azure RMS: algoritmi e lunghezze delle chiavi](how-does-it-work.md#cryptographic-controls-used-by-azure-rms-algorithms-and-key-lengths).

√ Supporto per moduli di protezione hardware (HSM) Thales per archiviare la chiave del tenant in data center di Microsoft Azure. Azure RMS usa ambienti di sicurezza separati per i propri data center in America del Nord, nei paesi EMEA (Europa, Medio Oriente e Africa) e in Asia, così da limitare l'uso della chiave del tenant al Paese in cui ha sede il data center.

√ Certificazione per:

-   ISO/IEC 27001:2013 (include [ISO/IEC 27018](http://azure.microsoft.com/blog/2015/02/16/azure-first-cloud-computing-platform-to-conform-to-isoiec-27018-only-international-set-of-privacy-controls-in-the-cloud/))

-   Attestazioni SOC 2 SSAE 16/ISAE 3402

-   HIPAA BAA

-   EU Model Clause

-   FedRAMP come parte di Azure Active Directory nella certificazione di Office 365, FedRAMP Agency ATO (Authority to Operate) rilasciato da HHS

-   PCI DSS Livello 1

Per altre informazioni su queste certificazioni esterne, vedere il [Centro protezione Azure](http://azure.microsoft.com/support/trust-center/compliance/).

## Passaggi successivi

Per informazioni sul funzionamento di Azure RMS per gli amministratori e gli utenti, vedere [Azure RMS in azione](what-admins-users-see.md).

Se si è interessati ad altre informazioni tecniche sul funzionamento di Azure RMS, vedere [Funzionamento di Azure RMS](how-does-it-work.md). 


<!--HONumber=Jul16_HO3-->


