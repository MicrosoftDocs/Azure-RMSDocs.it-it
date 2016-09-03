---
title: Guida di orientamento per la distribuzione di Microsoft Azure Rights Management | Azure RMS
description: 'Per preparare l''ambiente e implementare e gestire Microsoft Azure Rights Management (RMS) per l''organizzazione, eseguire la procedura seguente:'
author: cabailey
manager: mbaldwin
ms.date: 08/24/2016
ms.topic: article
ms.prod: 
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 086600c2-c5d8-47ec-a4c0-c782e1797486
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 024a29d7c7db2e4c0578a95c93e22f8e7a5b173e
ms.openlocfilehash: 13ec3a88eb1c072bf94b6c54e3e4d97e45cc8eb2


---

# Guida di orientamento per la distribuzione di Microsoft Azure Rights Management

>*Si applica a: Azure Rights Management, Office 365*

Per preparare l'ambiente e implementare e gestire Microsoft Azure Rights Management (RMS) per l'organizzazione, eseguire la procedura seguente:

Tuttavia, se si vuole provare rapidamente Azure RMS per conto proprio, anziché implementarlo in un ambiente di produzione, vedere [Esercitazione di avvio rapido per Azure Rights Management](../get-started/quick-start-tutorial.md).

Per un elenco di scenari specifici con relativi passaggi di configurazione e documentazione dell'utente finale, vedere [Guida alla distribuzione rapida di Azure Rights Management](../get-started/rapid-deployment-guide.md).

> [!IMPORTANT]
> Prima di eseguire i seguenti passaggi, leggere assicurarsi di aver letto [Requisiti di Azure Rights Management](../get-started/requirements-azure-rms.md).

## Passaggio 1: Confermare di avere una sottoscrizione che include Azure Rights Management
Sono disponibili più tipi di sottoscrizione che includono [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)]. Vedere [Sottoscrizioni cloud che supportano Azure RMS](../get-started/requirements-subscriptions.md) e verificare che la sottoscrizione includa la funzionalità che si vuole usare nell'organizzazione facendo riferimento alla tabella in [Offerte di Rights Management Services (RMS) a confronto](https://technet.microsoft.com/dn858608). È necessario assegnare una licenza di sottoscrizione a ogni utente dell'organizzazione in modo da proteggere i file e messaggi di posta elettronica tramite Azure RMS.

## Passaggio 2: preparare l'account tenant per l'utilizzo di Rights Management
Prima di iniziare a usare [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)], effettuare la seguente preparazione:

1.  Verificare che il tenant di Azure o Office 365 contenga gli account utente e i gruppi che verranno usati da Azure RMS per autenticare gli utenti dell'organizzazione. Se necessario, creare questi account e gruppi o sincronizzarli dalla directory locale. Per ulteriori informazioni, vedere [Preparazione per Azure Rights Management](prepare.md).

2.  Decidere se si desidera che Microsoft gestisca la chiave del tenant (impostazione predefinita) oppure generare e gestire personalmente la chiave del tenant. Questo servizio è noto come BYOK (Bring Your Own Key). Si noti che attualmente non è possibile usare il servizio BYOK se si usa Exchange Online. Per ulteriori informazioni, vedere [Pianificazione e implementazione della chiave del tenant di Azure Rights Management](plan-implement-tenant-key.md).

3.  Installare il modulo di Windows PowerShell per [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] in almeno un computer dotato di accesso a Internet. È possibile eseguire questo passaggio subito o più avanti. Per ulteriori informazioni, vedere [Installazione di Windows PowerShell per Azure Rights Management](../deploy-use/install-powershell.md).

4.  Se attualmente si stanno usando i servizi Rights Management locali: eseguire una migrazione per spostare le chiavi, i modelli e gli URL sul cloud. Per ulteriori informazioni, vedere [Migrazione da AD RMS ad Azure Rights Management](migrate-from-ad-rms-to-azure-rms.md).

5.  Attivare Rights Management in modo da poter iniziare a usare il servizio. Se è richiesta una distribuzione graduale, configurare i controlli di selezione utenti per limitare l'utilizzo a utenti specifici. Per ulteriori informazioni, vedere l'articolo relativo all'[attivazione di Azure Rights Management](../deploy-use/activate-service.md).

Facoltativamente, considerare la possibilità di configurare quanto segue:

-   Modelli personalizzati se i modelli di criteri predefiniti per i diritti di utilizzo non sono sufficienti per l'organizzazione. È possibile eseguire questo passaggio subito o più avanti. Per altre informazioni, vedere [Configurazione di modelli personalizzati per Azure Rights Management](../deploy-use/configure-custom-templates.md).

-   Registrazione dei dati di utilizzo per monitorare le modalità con cui l'organizzazione usa Rights Management. È possibile eseguire questo passaggio subito o più avanti. Per ulteriori informazioni, vedere [Registrazione e analisi dell'utilizzo di Azure Rights Management](../deploy-use/log-analyze-usage.md).

## Passaggio 3: Configurare le applicazioni e i servizi per Rights Management
La configurazione delle applicazione e dei servizi può includere l'installazione dell'applicazione di condivisione Rights Management e l'abilitazione del supporto per le funzionalità IRM (Information Rights Management) in SharePoint Online o Exchange Online. Per ulteriori informazioni, vedere [Configurazione delle applicazioni per Azure Rights Management](../deploy-use/configure-applications.md).

Se sono disponibili servizi IT esistenti che devono esaminare i file che verranno protetti da Azure RMS, ad esempio soluzioni di prevenzione per la perdita di dati, gateway con crittografia del contenuto e prodotti antimalware, configurare gli account del servizio per utenti con privilegi avanzati per Azure RMS. Per ulteriori informazioni, vedere [Configurazione degli utenti con privilegi avanzati per Rights Management di Azure e servizi di individuazione o ripristino dei dati](../deploy-use/configure-super-users.md).

Per poter proteggere o rimuovere la protezione in blocco di tutti i tipi di file, installare lo strumento di protezione RMS che usa il modulo PowerShell di protezione di RMS. Per altre informazioni, vedere [Azure Rights Management Protection Cmdlets](https://msdn.microsoft.com/library/mt433195.aspx) (Cmdlet di protezione di Azure Rights Management).

Se si dispone di servizi locali da usare con Microsoft Azure Rights Management, installare e configurare il relativo connettore. Per ulteriori informazioni, vedere [Distribuzione del connettore di Azure Rights Management](../deploy-use/deploy-rms-connector.md).

## Passaggio 4: Pubblicare e utilizzare il contenuto protetto da diritti
È possibile pubblicare e utilizzare il contenuto protetto e registrare come la società usa Rights Management. Per ulteriori informazioni, vedere [Consentire agli utenti di proteggere i file mediante Azure Rights Management](../deploy-use/help-users.md) e [Registrazione e analisi dell'uso di Rights Management di Windows Azure](../deploy-use/log-analyze-usage.md).

Se si vuole proteggere automaticamente i file usando l'infrastruttura di classificazione file in un file server basato su Windows, vedere [Protezione RMS con l'infrastruttura di classificazione file (FCI, File Classification Infrastructure) per Windows Server](../rms-client/configure-fci.md).

## Passaggio 5: Amministrare Rights Management per l'account tenant in base alle esigenze
Quando si inizia a usare [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)], è possibile avvalersi del modulo [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] per Windows PowerShell per eseguire tramite script o automatizzare le modifiche di carattere amministrativo. Per ulteriori informazioni, vedere [Amministrazione di Microsoft Azure Rights Management mediante Windows PowerShell](../deploy-use/administer-powershell.md).





<!--HONumber=Aug16_HO4-->


