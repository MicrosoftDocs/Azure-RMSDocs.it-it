---
# required metadata

title: Attivazione di Azure Rights Management | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 05/16/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: f8707e01-b239-4d1a-a1ea-0d1cf9a8d214

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Attivazione di Azure Rights Management

*Si applica a: Azure Rights Management, Office 365*

Quando si attiva [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] (Azure RMS), l'organizzazione può iniziare a proteggere i dati importanti usando le applicazioni e i servizi che supportano questa soluzione di protezione delle informazioni. Gli amministratori possono inoltre gestire e monitorare i file e i messaggi di posta elettronica protetti di proprietà dell'azienda. È necessario abilitare [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] prima di poter iniziare a usare le funzionalità di Information Rights Management (IRM) in Office, SharePoint ed Exchange per proteggere eventuali file sensibili o riservati.

Per altre informazioni su Azure Rights Management prima di attivare il servizio, ad esempio sui problemi aziendali che consente di risolvere, sui casi d'uso tipici e su come funziona, vedere [Informazioni su Microsoft Azure Rights Management](../understand-explore/what-is-azure-rms.md).

> [!IMPORTANT]
> Prima di attivare [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)], assicurarsi che il piano di servizio dell'organizzazione includa i servizi [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)]. In caso contrario, non sarà possibile attivare Azure RMS.
>
> Per altre informazioni, vedere l'articolo relativo alle [sottoscrizioni cloud che supportano Azure RMS](../get-started/requirements-subscriptions.md).

Dopo l'attivazione di Azure RMS, tutti gli utenti dell'organizzazione potranno applicare la protezione delle informazioni ai propri file e tutti gli utenti potranno aprire (utilizzare) i file protetti da Azure RMS. Se si preferisce, tuttavia, è possibile limitare l'applicazione della protezione delle informazioni solo ad alcuni utenti, usando i controlli di selezione utenti per una distribuzione graduale. Per altre informazioni, vedere la sezione [Configurazione dei controlli di selezione utenti per una distribuzione graduale](#configuring-onboarding-controls-for-a-phased-deployment) di questo articolo.

Per istruzioni sull'attivazione di Rights Management dal portale di gestione, specificare se si userà l'interfaccia di amministrazione di Office 365 (versione classica o di anteprima) o il portale di gestione di Azure classico:


- [Interfaccia di amministrazione di Office 365 - versione di anteprima](activate-office365-preview.md)
- [Interfaccia di amministrazione di Office 365 - versione classica](activate-office365-classic.md)
- [Portale di Azure classico](activate-azure-classic.md)

In alternativa, è possibile usare Windows PowerShell per attivare [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)]:

1. Installare lo strumento di amministrazione di Azure Rights Management che include l'installazione del modulo di amministrazione di Azure Rights Management. Per le istruzioni, vedere [Installazione di Windows PowerShell per Microsoft Azure Rights Management](../deploy-use/install-powershell.md).

2. In una sessione di Windows PowerShell eseguire [Connect-AadrmService](https://msdn.microsoft.com/library/windowsazure/dn629415.aspx) e, quando richiesto, specificare i dati dell'account dell'amministratore globale per il tenant di Azure RMS.

3. Eseguire [Enable-Aadrm](http://msdn.microsoft.com/library/windowsazure/dn629412.aspx) che attiva il servizio Azure RMS.

## Configurazione dei controlli di selezione utenti per una distribuzione graduale
Se non si vuole permettere a tutti gli utenti di proteggere immediatamente i file usando Azure RMS, sarà possibile configurare controlli di selezione utenti usando il comando [Set-AadrmOnboardingControlPolicy](http://msdn.microsoft.com/library/azure/dn857521.aspx) di Windows PowerShell. È possibile eseguire questo comando prima o dopo l'attivazione di Azure RMS.

> [!IMPORTANT] Per usare questo comando, è necessaria almeno la versione **2.1.0.0** del [modulo di Azure RMS per Windows PowerShell](http://go.microsoft.com/fwlink/?LinkId=257721).
>
> Per verificare quale versione è installata, eseguire: **(Get-Module aadrm –ListAvailable).Version**

Se, ad esempio, inizialmente si vuole permettere solo agli amministratori del gruppo "IT department" (con ID oggetto fbb99ded-32a0-45f1-b038-38b519009503) di proteggere i contenuti per finalità di test, usare il comando seguente:

```
Set-AadrmOnboardingControlPolicy – SecurityGroupObjectId fbb99ded-32a0-45f1-b038-38b519009503
```
Si noti che per questa opzione di configurazione è necessario specificare un gruppo. Non è possibile specificare singoli utenti.

Oppure se si vuole assicurare che solo gli utenti con licenza valida per l'uso di Azure RMS possano proteggere i contenuti:

```
Set-AadrmOnboardingControlPolicy -UseRmsUserLicense $true
```
Quando si usano questi controlli di selezione utenti, tutti gli utenti dell'organizzazione potranno utilizzare sempre i contenuti protetti dal sottoinsieme di utenti, ma non potranno applicare direttamente la protezione delle informazioni da applicazioni client. Non potranno ad esempio visualizzare nei client Office i modelli predefiniti pubblicati automaticamente quando viene attivato Azure RMS oppure eventuali modelli personalizzati configurati dall'utente.  Per ottenere lo stesso risultato, le applicazioni lato server, come Exchange, possono implementare controlli specifici per i singoli utenti per l'integrazione con RMS.


## Passaggi successivi
Dopo aver attivato [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] per l'organizzazione, usare la [guida di orientamento per la distribuzione di Azure Rights Management](../plan-design/deployment-roadmap.md) per verificare se può essere necessario eseguire operazioni di configurazione aggiuntive prima di distribuire [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] a utenti e amministratori. 

Ad esempio, per usare [modelli personalizzati](configure-custom-templates.md) per semplificare l'applicazione ai file della protezione delle informazioni, connettere i server locali in modo che usino [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] installando il [connettore RMS](deploy-rms-connector.md) e distribuire l'[applicazione Rights Management sharing](../rms-client/sharing-app-windows.md) che supporta la protezione di tutti i tipi di file su tutti i dispositivi. 

I servizi di Office, ad esempio Exchange Online e SharePoint Online, richiedono operazioni di configurazione aggiuntive prima di poter usare le funzionalità di Information Rights Management (IRM). Per informazioni sul funzionamento delle applicazioni con [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)], vedere [Supporto di Azure Rights Management da parte delle applicazioni](../understand-explore/applications-support.md).



<!--HONumber=May16_HO3-->


