---
title: Attivazione di Azure Rights Management - AIP
description: "È necessario attivare il servizio Azure Rights Management prima che l'organizzazione possa iniziare a proteggere i documenti e i messaggi di posta elettronica usando le applicazioni e i servizi che supportano questa soluzione di protezione delle informazioni."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 11/15/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: f8707e01-b239-4d1a-a1ea-0d1cf9a8d214
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 75c0bf83c84cb8b5d2116b05dbf2def790562b4e
ms.sourcegitcommit: fd3932ab19a00229b56efc3e301abaf9cff3f70b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/17/2017
---
# <a name="activating-azure-rights-management"></a>Attivazione di Azure Rights Management

>*Si applica a: Azure Information Protection, Office 365*

> [!NOTE]
> Le informazioni sulla configurazione sono riservate agli amministratori responsabili di un servizio applicato a tutti gli utenti all'interno di un'organizzazione. Per informazioni su come usare la funzionalità Rights Management per una specifica applicazione o aprire un file o un messaggio di posta elettronica protetto da diritti, vedere la guida e le informazioni aggiuntive fornite con l'applicazione.
>
> Ad esempio, per le applicazioni Office fare clic sull'icona della Guida e immettere i termini di ricerca, ad esempio **Rights Management** o **IRM**. Per il client Azure Information Protection per Windows, vedere la [Guida per l'utente del client Azure Information Protection](../rms-client/client-user-guide.md).
>
> Per il supporto tecnico e altre domande sul servizio, vedere le informazioni riportate in [Opzioni di supporto e risorse per la community](../get-started/information-support.md#support-options-and-community-resources).

Quando il servizio Azure Rights Management per Azure Information Protection è attivato per il tenant, l'organizzazione può iniziare a proteggere i dati importanti usando le applicazioni e i servizi che supportano questa soluzione di protezione delle informazioni. Gli amministratori possono inoltre gestire e monitorare i file e i messaggi di posta elettronica protetti di proprietà dell'azienda. È necessario abilitare questo servizio prima di poter iniziare a usare le funzionalità di Information Rights Management (IRM) in Office, SharePoint ed Exchange per proteggere eventuali file sensibili o riservati.

Per altre informazioni sul servizio Azure Rights Management prima di attivarlo, ad esempio sui problemi aziendali che consente di risolvere, sui casi d'uso tipici e su come funziona, vedere [Informazioni su Microsoft Azure Rights Management](../understand-explore/what-is-azure-rms.md).

> [!IMPORTANT]
> Non attivare il servizio Azure Rights Management se si dispone di Active Directory Rights Management Services (AD RMS) distribuito per l'organizzazione. [Altre informazioni](prepare-environment-adrms.md)

Prima di attivare [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)], assicurarsi che il piano di servizio dell'organizzazione includa la protezione dati di Azure Rights Management. In caso contrario, non sarà possibile attivare Azure Rights Management. È necessario disporre di:

- Un [piano Azure Information Protection](https://www.microsoft.com/cloud-platform/azure-information-protection-pricing) 

- Un [piano Office 365 che includa Rights Management](http://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf).

Dopo l'attivazione del servizio Azure Rights Management, tutti gli utenti dell'organizzazione potranno applicare la protezione delle informazioni ai propri file e tutti gli utenti potranno aprire (utilizzare) i file protetti da questo servizio. Se si preferisce, tuttavia, è possibile limitare l'applicazione della protezione delle informazioni solo ad alcuni utenti, usando i controlli di selezione utenti per una distribuzione graduale. Per altre informazioni, vedere la sezione [Configurazione dei controlli di selezione utenti per una distribuzione graduale](#configuring-onboarding-controls-for-a-phased-deployment) di questo articolo.

Per istruzioni sull'attivazione del servizio Rights Management dal portale di gestione, specificare se si userà l'interfaccia di amministrazione di Office 365 o il portale di Azure:

- [**Interfaccia di amministrazione di Office 365**](activate-office365.md) -richiede l'account di amministratore globale

- [**Portale di Azure**](activate-azure.md) - richiede l'account di amministratore globale o [account di amministratore della sicurezza](https://docs.microsoft.com/azure/active-directory/active-directory-assign-admin-roles)

In alternativa, è possibile usare PowerShell per attivare [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)]:

1. Installare lo strumento di amministrazione di Azure Rights Management che include l'installazione del modulo di amministrazione di Azure Rights Management. Per le istruzioni, vedere [Installazione di Windows PowerShell per Microsoft Azure Rights Management](../deploy-use/install-powershell.md).

2. In una sessione di PowerShell eseguire [Connect-AadrmService](/powershell/module/aadrm/connect-aadrmservice) e, quando richiesto, specificare i dati dell'account dell'amministratore globale per il tenant di Azure Information Protection.

3. Eseguire [Enable-Aadrm](/powershell/module/aadrm/enable-aadrm) che attiva il servizio Azure Rights Management.

## <a name="configuring-onboarding-controls-for-a-phased-deployment"></a>Configurazione dei controlli di selezione utenti per una distribuzione graduale
Se non si vuole permettere a tutti gli utenti di proteggere immediatamente i file usando Azure Rights Management, sarà possibile configurare controlli di selezione utenti usando il comando [Set-AadrmOnboardingControlPolicy](/powershell/module/aadrm/set-aadrmonboardingcontrolpolicy) di PowerShell. È possibile eseguire questo comando prima o dopo l'attivazione del servizio Azure Rights Management.

> [!IMPORTANT]
> Per usare questo comando, è necessaria almeno la versione **2.1.0.0** del [modulo di PowerShell per Azure Rights Management](https://go.microsoft.com/fwlink/?LinkId=257721).
>
> Per verificare quale versione è installata, eseguire: **(Get-Module aadrm –ListAvailable).Version**

Se, ad esempio, inizialmente si vuole permettere solo agli amministratori del gruppo "IT department" (con ID oggetto fbb99ded-32a0-45f1-b038-38b519009503) di proteggere i contenuti per finalità di test, usare il comando seguente:

```
Set-AadrmOnboardingControlPolicy -UseRmsUserLicense $False -SecurityGroupObjectId "fbb99ded-32a0-45f1-b038-38b519009503"
```

Si noti che per questa opzione di configurazione è necessario specificare un gruppo. Non è possibile specificare singoli utenti. Per ottenere l'ID oggetto per il gruppo, è possibile usare Azure AD PowerShell, ad esempio usare il comando [Get-MsolGroup](/powershell/msonline/v1/get-msolgroup) per la versione 1.0 del modulo. Oppure, è possibile copiare valore **ID oggetto** del gruppo dal portale di Azure.

In alternativa, per fare in modo che solo gli utenti con licenza valida per l'uso di Azure Information Protection possano proteggere i contenuti:

```
Set-AadrmOnboardingControlPolicy -UseRmsUserLicense $True
```

Quando i controlli di caricamento non sono più necessari, se è stata usata l'opzione di gruppo o di gestione licenze, eseguire:

```
Set-AadrmOnboardingControlPolicy -UseRmsUserLicense $False
```


Per altre informazioni su questo cmdlet ed esempi aggiuntivi, vedere la guida di [Set-AadrmOnboardingControlPolicy](/powershell/aadrm/vlatest/set-aadrmonboardingcontrolpolicy).

Quando si usano questi controlli di selezione utenti, tutti gli utenti dell'organizzazione potranno utilizzare sempre i contenuti protetti dal sottoinsieme di utenti, ma non potranno applicare direttamente la protezione delle informazioni da applicazioni client. Non potranno ad esempio visualizzare nei client di Office i modelli predefiniti pubblicati automaticamente quando viene attivato il servizio Azure Rights Management oppure eventuali modelli personalizzati configurati dall'utente.  Per ottenere lo stesso risultato, le applicazioni lato server, come Exchange, possono implementare controlli specifici per singoli utenti per l'integrazione con RMS.


## <a name="next-steps"></a>Passaggi successivi
Dopo aver attivato [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] per l'organizzazione, usare la [Guida di orientamento per la distribuzione di Azure Information Protection](../plan-design/deployment-roadmap.md) per verificare se sono necessarie altre operazioni di configurazione prima di distribuire Azure Information Protection a utenti e amministratori. 

Ad esempio, per usare dei [modelli](configure-policy-templates.md) per semplificare l'applicazione della protezione delle informazioni ai file, connettere i server locali in modo che usino [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] installando il [connettore Rights Management](deploy-rms-connector.md) e distribuire il [client Azure Information Protection](../rms-client/aip-client.md) che supporta la protezione di tutti i tipi di file su tutti i dispositivi. 

I servizi di Office, ad esempio Exchange Online e SharePoint Online, richiedono operazioni di configurazione aggiuntive prima di poter usare le funzionalità di Information Rights Management (IRM). Per informazioni sul funzionamento delle applicazioni con il servizio Rights Management, vedere [Supporto del servizio Azure Rights Management da parte delle applicazioni](../understand-explore/applications-support.md).


[!INCLUDE[Commenting house rules](../includes/houserules.md)]