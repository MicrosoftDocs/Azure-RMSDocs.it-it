---
# required metadata

title: Processo FastTrack Center Benefit per Enterprise Mobility Suite: requisiti dell'ambiente di origine
description:
keywords:
author: staciebarker
manager: jeffgilb
ms.date: 04/28/2016
ms.topic: article
ms.prod:
ms.service:
ms.technology:
ms.assetid: 9048f3e5-cc28-4744-bb5e-36f974abb261

# optional metadata

ROBOTS: noindex
#audience:
#ms.devlang:
ms.reviewer: 
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---


# Processo FastTrack Center Benefit per Enterprise Mobility Suite: requisiti dell'ambiente di origine
Se si usa [FastTrack Center Benefit per Enterprise Mobility Suite (EMS)](fasttrack-center-benefit-for-enterprise-mobility-suite-ems.md) per ottenere Azure Active Directory Premium, Microsoft Intune e/o Azure Rights Management pronti all'uso, è necessario che l'ambiente soddisfi i requisiti descritti nelle sezioni seguenti.

Per altre informazioni sul processo di caricamento FastTrack, vedere [Processo FastTrack Center Benefit per Enterprise Mobility Suite (EMS)](fasttrack-center-benefit-process-for-enterprise-mobility-suite-ems.md).

Se Microsoft Active Directory locale è già presente nell'ambiente corrente, è possibile integrarlo con EMS o qualsiasi altro suo singolo servizio per sfruttare le funzionalità complete di gestione delle identità da una singola console. FastTrack Center Benefit prevede assistenza durante il processo d'integrazione di Microsoft Azure Active Directory Premium con l'implementazione locale esistente. Se l'integrazione è necessaria, l'ambiente di origine deve essere a un livello minimo per tale applicazione.

La tabella seguente illustra le previsioni nell'ambiente di origine esistente per l'onboarding.

|Attività|Previsione per l’ambiente di origine|
|------------|----------------------------------|
|Onboarding di base|Foreste di Active Directory con il livello di foresta funzionale impostato su Windows Server 2008 o versione successiva, con la configurazione di foresta seguente:<br /><br />-   Foresta singola di Active Directory<br />-   Più foreste di Active Directory </br></br>**Nota**: per tutte le configurazioni a più foreste, la distribuzione di AD FS è esterna all'ambito di FastTrack Center Benefit.|
|Caricamento di Microsoft Azure Active Directory Premium|Active Directory e l'ambiente locali sono stati preparati per Azure Active Directory Premium. Quest'ultimo include la correzione dei problemi identificati che impediscono l'integrazione con le funzionalità di Azure Active Directory e Azure Active Directory Premium.|
|Caricamento di Microsoft Intune, solo cloud o integrato con System Center Configuration Manager|Per la gestione di dispositivi con System Center Configuration Manager 2012 R2 o versione successiva connessi a Microsoft Intune, gli amministratori IT dovranno seguire l' [Elenco di controllo amministratore: Configurazione di Configuration Manager per la gestione di dispositivi mobili mediante Microsoft Intune](https://technet.microsoft.com/library/jj943763.aspx).</br></br> **Nota**: i vantaggi del servizio non includono l'assistenza durante la configurazione di System Center Configuration Manager o il suo aggiornamento ai requisiti minimi necessari per integrare Microsoft Intune con System Center Configuration Manager.|

Leggere la parte successiva del processo di caricamento di FastTrack: [Processo FastTrack Center Benefit per Enterprise Mobility Suite: fasi](fasttrack-center-benefit-process-for-ems-phases.md)

### Altre informazioni
Vedere [Enterprise Mobility Suite](https://www.microsoft.com/en-us/server-cloud/enterprise-mobility/overview.aspx).



<!--HONumber=Jun16_HO1-->


