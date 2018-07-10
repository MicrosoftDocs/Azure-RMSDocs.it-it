---
title: Attivazione di Azure Rights Management - AIP
description: È necessario attivare il servizio Azure Rights Management prima che l'organizzazione possa iniziare a proteggere i documenti e i messaggi di posta elettronica usando le applicazioni e i servizi che supportano questa soluzione di protezione delle informazioni.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 06/29/2018
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: f8707e01-b239-4d1a-a1ea-0d1cf9a8d214
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 8e8a5062efe3b14f1867cf8440dc91c368a810f5
ms.sourcegitcommit: 6bdc1e5c328ad3b63aeb6f60ba9905551261a7a1
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/30/2018
ms.locfileid: "37137781"
---
# <a name="activating-azure-rights-management"></a>Attivazione di Azure Rights Management

>*Si applica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](http://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

> [!NOTE]
> Le informazioni sulla configurazione sono riservate agli amministratori responsabili di un servizio applicato a tutti gli utenti all'interno di un'organizzazione. Per informazioni su come usare la funzionalità Rights Management per una specifica applicazione o aprire un file o un messaggio di posta elettronica protetto da diritti, vedere la guida e le informazioni aggiuntive fornite con l'applicazione.
>
> Ad esempio, per le applicazioni Office fare clic sull'icona della Guida e immettere i termini di ricerca, ad esempio **Rights Management** o **IRM**. Per il client Azure Information Protection per Windows, vedere la [Guida per l'utente del client Azure Information Protection](../rms-client/client-user-guide.md).
>
> Per il supporto tecnico e altre domande sul servizio, vedere le informazioni riportate in [Opzioni di supporto e risorse per la community](../get-started/information-support.md#support-options-and-community-resources).

Quando il servizio Azure Rights Management per Azure Information Protection è attivato per l'organizzazione, gli amministratori e gli utenti possono iniziare a proteggere i dati importanti usando le applicazioni e i servizi che supportano questa soluzione di protezione delle informazioni. Gli amministratori possono anche gestire e monitorare i documenti e i messaggi di posta elettronica protetti di proprietà dell'azienda. 


## <a name="do-you-need-to-activate-azure-rights-management"></a>Attivare il servizio Azure Rights Management

Quanto Azure Rights Management è incluso in un piano di servizio, non è necessario attivare il servizio:

- **Se la sottoscrizione che include Azure Rights Management o Azure Information Protection risale alla fine di febbraio 2018 o a un periodo successivo:** il servizio viene attivato automaticamente. Non è necessario attivare il servizio, a meno che Azure Rights Management sia stato disattivato dall'utente o da un altro amministratore globale.

- **Se la sottoscrizione che include Azure Rights Management o Azure Information Protection risale a febbraio 2018 o prima:** Microsoft sta iniziando ad attivare il servizio Azure Rights Management per queste sottoscrizioni se il tenant usa Exchange Online. Per queste sottoscrizioni, l'implementazione dell'attivazione automatica inizierà l'1 agosto 2018 quando il servizio verrà automaticamente attivato a meno che **AutomaticServiceUpdateEnabled** non risulti impostato su **false** quando si esegue [Get-IRMConfiguration](/powershell/module/exchange/encryption-and-certificates/get-irmconfiguration?view=exchange-ps). 

Se nessuno degli scenari successivi è applicabile, è necessario attivare manualmente il servizio di protezione. 

Dopo l'attivazione del servizio, tutti gli utenti dell'organizzazione potranno applicare la protezione delle informazioni ai propri documenti e messaggi di posta elettronica e tutti gli utenti potranno aprire (utilizzare) i documenti e i messaggi di posta elettronica protetti da questo servizio. Se si preferisce, tuttavia, è possibile limitare l'applicazione della protezione delle informazioni solo ad alcuni utenti, usando i controlli di selezione utenti per una distribuzione graduale. Per altre informazioni, vedere la sezione [Configurazione dei controlli di selezione utenti per una distribuzione graduale](#configuring-onboarding-controls-for-a-phased-deployment) di questo articolo.

## <a name="how-to-activate-or-confirm-the-status-of-the-azure-rights-management-service"></a>Come attivare o confermare lo stato del servizio Azure Rights Management 

> [!IMPORTANT]
> Non attivare il servizio Azure Rights Management se si dispone di Active Directory Rights Management Services (AD RMS) distribuito per l'organizzazione. [Altre informazioni](prepare-environment-adrms.md)

Per usare questa soluzione di protezione dati, l'organizzazione deve essere in possesso di un piano di servizio che include il servizio Azure Rights Management di Azure Information Protection. Senza questo piano, il servizio Azure Rights Management non può essere attivato. È necessario disporre di:

- Un [piano Azure Information Protection](https://www.microsoft.com/cloud-platform/azure-information-protection-pricing) 

- Un [piano Office 365 che includa Rights Management](http://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf).

Dopo l'attivazione del servizio Azure Rights Management, tutti gli utenti dell'organizzazione potranno applicare la protezione delle informazioni ai propri documenti e messaggi di posta elettronica e tutti gli utenti potranno aprire (utilizzare) i documenti e i messaggi di posta elettronica protetti da questo servizio. Se si preferisce, tuttavia, è possibile limitare l'applicazione della protezione delle informazioni solo ad alcuni utenti, usando i controlli di selezione utenti per una distribuzione graduale. Per altre informazioni, vedere la sezione [Configurazione dei controlli di selezione utenti per una distribuzione graduale](#configuring-onboarding-controls-for-a-phased-deployment) di questo articolo.

## <a name="choosing-your-activation-method"></a>Scelta del metodo di attivazione

Per istruzioni sull'attivazione del servizio Rights Management dal portale di gestione, specificare se si userà l'interfaccia di amministrazione di Office 365 o il portale di Azure:

- [Interfaccia di amministrazione di Office 365](activate-office365.md) - richiede l'account di amministratore globale

- [Portale di Azure](activate-azure.md) - non richiede l'account di amministratore globale

In alternativa, è possibile usare i comandi PowerShell seguenti:

1. Installare il modulo AADRM per configurare e gestire il servizio di protezione. Per le istruzioni, vedere [Installazione del modulo PowerShell AADRM](../deploy-use/install-powershell.md).

2. In una sessione di PowerShell eseguire [Connect-AadrmService](/powershell/module/aadrm/connect-aadrmservice) e, quando richiesto, specificare i dati dell'account dell'amministratore globale per il tenant di Azure Information Protection.

3. Eseguire [Get-Aadrm](/powershell/aadrm/vlatest/get-aadrm) per confermare se il servizio Azure Rights Management è attivato. Lo stato **Abilitato** ne conferma l'attivazione; lo stato **Disabilitato** indica che il servizio è disattivato.

4. Per attivare il servizio, eseguire [Enable-Aadrm](/powershell/aadrm/vlatest/enable-aadrm).

## <a name="configuring-onboarding-controls-for-a-phased-deployment"></a>Configurazione dei controlli di selezione utenti per una distribuzione graduale
Se non si vuole permettere a tutti gli utenti di proteggere immediatamente i documenti e i messaggi di posta elettronica usando Azure Rights Management, sarà possibile configurare controlli di selezione utenti usando il comando [Set-AadrmOnboardingControlPolicy](/powershell/module/aadrm/set-aadrmonboardingcontrolpolicy) di PowerShell. È possibile eseguire questo comando prima o dopo l'attivazione del servizio Azure Rights Management.

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

Quando si usano questi controlli di selezione utenti, tutti gli utenti dell'organizzazione potranno utilizzare sempre i contenuti protetti dal sottoinsieme di utenti, ma non potranno applicare direttamente la protezione delle informazioni da applicazioni client. Non potranno ad esempio visualizzare nei client di Office i modelli predefiniti pubblicati automaticamente quando viene attivato il servizio Azure Rights Management oppure eventuali modelli personalizzati configurati dall'utente. Per ottenere lo stesso risultato, le applicazioni lato server, come Exchange, possono implementare controlli specifici per singoli utenti per l'integrazione con RMS.


## <a name="next-steps"></a>Passaggi successivi
Quanto il servizio Azure Rights Management è attivato per l'organizzazione, usare la [Guida di orientamento per la distribuzione di Azure Information Protection](../plan-design/deployment-roadmap.md) per verificare se sono necessari altri passaggi di configurazione prima di implementare Azure Information Protection a utenti e amministratori. 

Ad esempio, per usare dei [modelli](configure-policy-templates.md) per semplificare l'applicazione della protezione delle informazioni ai file, connettere i server locali in modo che usino [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] installando il [connettore Rights Management](deploy-rms-connector.md) e distribuire il [client Azure Information Protection](../rms-client/aip-client.md) che supporta la protezione di tutti i tipi di file su tutti i dispositivi. 

I servizi di Office, ad esempio Exchange Online e SharePoint Online, richiedono operazioni di configurazione aggiuntive prima di poter usare le funzionalità di Information Rights Management (IRM). Per informazioni sul funzionamento delle applicazioni con il servizio Rights Management, vedere [Supporto del servizio Azure Rights Management da parte delle applicazioni](../understand-explore/applications-support.md).


[!INCLUDE[Commenting house rules](../includes/houserules.md)]
