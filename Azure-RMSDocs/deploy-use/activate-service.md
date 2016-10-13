---
title: Attivazione di Azure Rights Management | Azure Information Protection
description: "È necessario attivare il servizio Azure Rights Management prima che l'organizzazione possa iniziare a proteggere i documenti e i messaggi di posta elettronica usando le applicazioni e i servizi che supportano questa soluzione di protezione delle informazioni."
author: cabailey
manager: mbaldwin
ms.date: 10/05/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: f8707e01-b239-4d1a-a1ea-0d1cf9a8d214
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 78b975c2babad347fc5be7956d504c7283508962
ms.openlocfilehash: 06c71229427743e9669baee1fdbb41f175180b0f


---

# Attivazione di Azure Rights Management

>*Si applica a: Azure Information Protection, Office 365*

Quando il servizio Azure Rights Management per Azure Information Protection è attivato, l'organizzazione può iniziare a proteggere i dati importanti usando le applicazioni e i servizi che supportano questa soluzione di protezione delle informazioni. Gli amministratori possono inoltre gestire e monitorare i file e i messaggi di posta elettronica protetti di proprietà dell'azienda. È necessario abilitare questo servizio prima di poter iniziare a usare le funzionalità di Information Rights Management (IRM) in Office, SharePoint ed Exchange per proteggere eventuali file sensibili o riservati.

Per altre informazioni sul servizio Azure Rights Management prima di attivarlo, ad esempio sui problemi aziendali che consente di risolvere, sui casi d'uso tipici e su come funziona, vedere [Informazioni su Microsoft Azure Rights Management](../understand-explore/what-is-azure-rms.md).

> [!IMPORTANT]
> Prima di attivare [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)], assicurarsi che il piano di servizio dell'organizzazione includa la protezione dati di Azure Rights Management. In caso contrario, non sarà possibile attivare Azure Rights Management.
>
> È necessario un [piano Azure Information Protection Premium](https://www.microsoft.com/en-us/cloud-platform/azure-information-protection-pricing) o un [piano di Office 365 che include Rights Management](http://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf).

Dopo l'attivazione del servizio Azure Rights Management, tutti gli utenti dell'organizzazione potranno applicare la protezione delle informazioni ai propri file e tutti gli utenti potranno aprire (utilizzare) i file protetti da questo servizio. Se si preferisce, tuttavia, è possibile limitare l'applicazione della protezione delle informazioni solo ad alcuni utenti, usando i controlli di selezione utenti per una distribuzione graduale. Per altre informazioni, vedere la sezione [Configurazione dei controlli di selezione utenti per una distribuzione graduale](#configuring-onboarding-controls-for-a-phased-deployment) di questo articolo.

Per istruzioni sull'attivazione del servizio Rights Management dal portale di gestione, specificare se si userà l'interfaccia di amministrazione di Office 365 (versione classica o di anteprima) o il portale di gestione di Azure classico:


- [Interfaccia di amministrazione di Office 365 - versione di anteprima](activate-office365-preview.md)
- [Interfaccia di amministrazione di Office 365 - versione classica](activate-office365-classic.md)
- [Portale di Azure classico](activate-azure-classic.md)

In alternativa, è possibile usare Windows PowerShell per attivare [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)]:

1. Installare lo strumento di amministrazione di Azure Rights Management che include l'installazione del modulo di amministrazione di Azure Rights Management. Per le istruzioni, vedere [Installazione di Windows PowerShell per Microsoft Azure Rights Management](../deploy-use/install-powershell.md).

2. In una sessione di Windows PowerShell eseguire [Connect-AadrmService](https://msdn.microsoft.com/library/windowsazure/dn629415.aspx) e, quando richiesto, specificare i dati dell'account dell'amministratore globale per il tenant di Azure Information Protection.

3. Eseguire [Enable-Aadrm](http://msdn.microsoft.com/library/windowsazure/dn629412.aspx) che attiva il servizio Azure Rights Management.

## Configurazione dei controlli di selezione utenti per una distribuzione graduale
Se non si vuole permettere a tutti gli utenti di proteggere immediatamente i file usando Azure Rights Management, sarà possibile configurare controlli di selezione utenti usando il comando [Set-AadrmOnboardingControlPolicy](http://msdn.microsoft.com/library/azure/dn857521.aspx) di Windows PowerShell. È possibile eseguire questo comando prima o dopo l'attivazione del servizio Azure Rights Management.

> [!IMPORTANT]
> Per usare questo comando, è necessaria almeno la versione **2.1.0.0** del [modulo di Windows PowerShell per Azure Rights Management](http://go.microsoft.com/fwlink/?LinkId=257721).
>
> Per verificare quale versione è installata, eseguire: **(Get-Module aadrm –ListAvailable).Version**

Se, ad esempio, inizialmente si vuole permettere solo agli amministratori del gruppo "IT department" (con ID oggetto fbb99ded-32a0-45f1-b038-38b519009503) di proteggere i contenuti per finalità di test, usare il comando seguente:

```
Set-AadrmOnboardingControlPolicy – SecurityGroupObjectId fbb99ded-32a0-45f1-b038-38b519009503
```
Si noti che per questa opzione di configurazione è necessario specificare un gruppo. Non è possibile specificare singoli utenti.

In alternativa, se si vuole assicurare che solo gli utenti con licenza valida per l'uso di Azure Information Protection possano proteggere i contenuti:

```
Set-AadrmOnboardingControlPolicy -UseRmsUserLicense $true
```
Quando si usano questi controlli di selezione utenti, tutti gli utenti dell'organizzazione potranno utilizzare sempre i contenuti protetti dal sottoinsieme di utenti, ma non potranno applicare direttamente la protezione delle informazioni da applicazioni client. Non potranno ad esempio visualizzare nei client di Office i modelli predefiniti pubblicati automaticamente quando viene attivato il servizio Azure Rights Management oppure eventuali modelli personalizzati configurati dall'utente.  Per ottenere lo stesso risultato, le applicazioni lato server, come Exchange, possono implementare controlli specifici per singoli utenti per l'integrazione con RMS.


## Passaggi successivi
Dopo aver attivato [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] per l'organizzazione, usare la [Guida di orientamento per la distribuzione di Azure Information Protection](../plan-design/deployment-roadmap.md) per verificare se sono necessarie altre operazioni di configurazione prima di distribuire Azure Information Protection a utenti e amministratori. 

Ad esempio, per usare [modelli personalizzati](configure-custom-templates.md) per semplificare l'applicazione della protezione delle informazioni ai file, connettere i server locali in modo che usino [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] installando il [connettore di Rights Management](deploy-rms-connector.md) e distribuire l'[applicazione Rights Management sharing](../rms-client/sharing-app-windows.md) che supporta la protezione di tutti i tipi di file su tutti i dispositivi. 

I servizi di Office, ad esempio Exchange Online e SharePoint Online, richiedono operazioni di configurazione aggiuntive prima di poter usare le funzionalità di Information Rights Management (IRM). Per informazioni sul funzionamento delle applicazioni con il servizio Rights Management, vedere [Supporto del servizio Azure Rights Management da parte delle applicazioni](../understand-explore/applications-support.md).




<!--HONumber=Oct16_HO1-->


