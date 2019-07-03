---
title: Attivazione del servizio di protezione di Azure Information Protection
description: Il servizio di protezione Azure Rights Management, deve essere attivato prima che l'organizzazione possa iniziare a proteggere documenti e messaggi di posta elettronica usando le applicazioni e servizi che supportano questa soluzione di protezione delle informazioni.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 07/03/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: f8707e01-b239-4d1a-a1ea-0d1cf9a8d214
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 16c3ded1ea8f5d7c2191b994ec63132bd5f9bf1e
ms.sourcegitcommit: a5f595f8a453f220756fdc11fd5d466c71d51963
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/02/2019
ms.locfileid: "67520310"
---
# <a name="activating-the-protection-service-from-azure-information-protection"></a>Attivazione del servizio di protezione di Azure Information Protection

>*Si applica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

> [!NOTE]
> Le informazioni sulla configurazione sono riservate agli amministratori responsabili di un servizio applicato a tutti gli utenti all'interno di un'organizzazione. Per informazioni su come usare la funzionalità Rights Management per una specifica applicazione o aprire un file o un messaggio di posta elettronica protetto da diritti, vedere la guida e le informazioni aggiuntive fornite con l'applicazione.
>
> Ad esempio, per le applicazioni Office fare clic sull'icona della Guida e immettere i termini di ricerca, ad esempio **Rights Management** o **IRM**. Per il client Azure Information Protection per Windows, vedere la [Guida per l'utente del client Azure Information Protection](./rms-client/client-user-guide.md).
>
> Per il supporto tecnico e altre domande sul servizio, vedere le informazioni riportate in [Opzioni di supporto e risorse per la community](information-support.md#support-options-and-community-resources).

Quando il servizio di protezione per Azure Information Protection è attivato per l'organizzazione, gli amministratori e gli utenti possono iniziare a proteggere i dati importanti usando le applicazioni e servizi che supportano questa soluzione di protezione delle informazioni. Gli amministratori possono anche gestire e monitorare i documenti e i messaggi di posta elettronica protetti di proprietà dell'azienda. 


## <a name="do-you-need-to-activate-the-protection-service-azure-rights-management"></a>È necessario attivare il servizio di protezione Azure Rights Management?

Quanto Azure Rights Management è incluso in un piano di servizio, non è necessario attivare il servizio:

- **Se la sottoscrizione che include Azure Rights Management o Azure Information Protection risale alla fine di febbraio 2018 o a un periodo successivo:** il servizio viene attivato automaticamente. Non è necessario attivare il servizio, a meno che Azure Rights Management sia stato disattivato dall'utente o da un altro amministratore globale.

- **Se la sottoscrizione che include Azure Rights Management o Azure Information Protection risale a febbraio 2018 o a un periodo precedente:** Microsoft sta iniziando ad attivare il servizio Azure Rights Management per le sottoscrizioni se il tenant usa Exchange Online. Per queste sottoscrizioni, l'implementazione dell'attivazione automatica inizierà l'1 agosto 2018 quando il servizio verrà automaticamente attivato a meno che **AutomaticServiceUpdateEnabled** non risulti impostato su **false** quando si esegue [Get-IRMConfiguration](/powershell/module/exchange/encryption-and-certificates/get-irmconfiguration?view=exchange-ps). 

Se nessuno degli scenari successivi è applicabile, è necessario attivare manualmente il servizio di protezione. 

Dopo l'attivazione del servizio, tutti gli utenti dell'organizzazione potranno applicare la protezione delle informazioni ai propri documenti e messaggi di posta elettronica e tutti gli utenti potranno aprire (utilizzare) i documenti e i messaggi di posta elettronica protetti da questo servizio. Se si preferisce, tuttavia, è possibile limitare l'applicazione della protezione delle informazioni solo ad alcuni utenti, usando i controlli di selezione utenti per una distribuzione graduale. Per altre informazioni, vedere la sezione [Configurazione dei controlli di selezione utenti per una distribuzione graduale](#configuring-onboarding-controls-for-a-phased-deployment) di questo articolo.

## <a name="how-to-activate-or-confirm-the-status-of-the-protection-service"></a>Come attivare o confermare lo stato del servizio di protezione 

> [!IMPORTANT]
> Non attivare il servizio di protezione se si dispone di Active Directory Rights Management Services (AD RMS) distribuito per l'organizzazione. [Altre informazioni](prepare-environment-adrms.md)

Per usare questa soluzione di protezione dati, l'organizzazione deve essere in possesso di un piano di servizio che include il servizio Azure Rights Management di Azure Information Protection. In caso contrario, il servizio di protezione non può essere attivato. È necessario disporre di:

- Un [piano Azure Information Protection](https://www.microsoft.com/cloud-platform/azure-information-protection-pricing) 

- Un [piano Office 365 che includa Rights Management](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf).

Quando viene attivato il servizio di protezione, tutti gli utenti nell'organizzazione possono applicare la protezione delle informazioni ai propri documenti e messaggi di posta elettronica e tutti gli utenti potranno aprire (utilizzare) i documenti e messaggi di posta elettronica che sono stati protetti da questo servizio. Se si preferisce, tuttavia, è possibile limitare l'applicazione della protezione delle informazioni solo ad alcuni utenti, usando i controlli di selezione utenti per una distribuzione graduale. Per altre informazioni, vedere la sezione [Configurazione dei controlli di selezione utenti per una distribuzione graduale](#configuring-onboarding-controls-for-a-phased-deployment) di questo articolo.

## <a name="choosing-your-activation-method"></a>Scelta del metodo di attivazione

Per istruzioni su come attivare il servizio di protezione dal portale di gestione, selezionare se usare l'interfaccia di amministrazione di Microsoft 365 o il portale di Azure:

- [Interfaccia di amministrazione di Microsoft 365](activate-office365.md) - richiede l'account di amministratore globale

- [Portale di Azure](activate-azure.md) - non richiede l'account di amministratore globale

In alternativa, è possibile usare i comandi PowerShell seguenti:

1. Installare il modulo AIPService, per configurare e gestire il servizio di protezione. Per istruzioni, vedere [installazione del modulo AIPService PowerShell](install-powershell.md).

2. Da una sessione di PowerShell, eseguire [Connect-AipService](/powershell/module/aipservice/connect-aipservice)e quando richiesto, specificare i dettagli dell'account amministratore globale per il tenant di Azure Information Protection.

3. Eseguire [Get-AipService](/powershell/module/aipservice/get-aipservice) per verificare se è attivato il servizio di protezione. Lo stato **Abilitato** ne conferma l'attivazione; lo stato **Disabilitato** indica che il servizio è disattivato.

4. Per attivare il servizio, eseguire [Enable-AipService](/powershell/module/aipservice/enable-aipservice).

## <a name="configuring-onboarding-controls-for-a-phased-deployment"></a>Configurazione dei controlli di selezione utenti per una distribuzione graduale
Se non si desidera tutti gli utenti siano in grado di proteggere immediatamente i documenti e messaggi di posta elettronica tramite Azure Information Protection, è possibile configurare controlli di selezione utenti usando il [Set-AipServiceOnboardingControlPolicy](/powershell/module/aipservice/set-aipserviceonboardingcontrolpolicy) PowerShell comando. È possibile eseguire questo comando prima o dopo l'attivazione del servizio Azure Rights Management.

Se, ad esempio, inizialmente si vuole permettere solo agli amministratori del gruppo "IT department" (con ID oggetto fbb99ded-32a0-45f1-b038-38b519009503) di proteggere i contenuti per finalità di test, usare il comando seguente:

```
Set-AipServiceOnboardingControlPolicy -UseRmsUserLicense $False -SecurityGroupObjectId "fbb99ded-32a0-45f1-b038-38b519009503"
```

Si noti che per questa opzione di configurazione è necessario specificare un gruppo. Non è possibile specificare singoli utenti. Per ottenere l'ID oggetto per il gruppo, è possibile usare Azure AD PowerShell, ad esempio usare il comando [Get-MsolGroup](/powershell/msonline/v1/get-msolgroup) per la versione 1.0 del modulo. Oppure, è possibile copiare valore **ID oggetto** del gruppo dal portale di Azure.

In alternativa, per fare in modo che solo gli utenti con licenza valida per l'uso di Azure Information Protection possano proteggere i contenuti:

```
Set-AipServiceOnboardingControlPolicy -UseRmsUserLicense $True
```

Quando i controlli di caricamento non sono più necessari, se è stata usata l'opzione di gruppo o di gestione licenze, eseguire:

```
Set-AipServiceOnboardingControlPolicy -UseRmsUserLicense $False
```

Per altre informazioni su questo cmdlet ed esempi aggiuntivi, vedere la [Set-AipServiceOnboardingControlPolicy](/powershell/module/aipservice/set-aipserviceonboardingcontrolpolicy) Guida in linea.

Quando si usano questi controlli di selezione utenti, tutti gli utenti dell'organizzazione potranno utilizzare sempre i contenuti protetti dal sottoinsieme di utenti, ma non potranno applicare direttamente la protezione delle informazioni da applicazioni client. Ad esempio, non potranno visualizzare nelle proprie app di Office i modelli di protezione predefiniti pubblicati automaticamente quando viene attivato il servizio di protezione o i modelli personalizzati che è possibile configurare. Le applicazioni sul lato server, come Exchange, possono implementare controlli propri per utente per ottenere lo stesso risultato. Ad esempio, per impedire agli utenti di proteggere messaggi di posta elettronica in Outlook sul Web, usare [Set-OwaMailboxPolicy](/powershell/module/exchange/client-access/set-owamailboxpolicy?view=exchange-ps) per impostare il parametro *IRMEnabled* su *$false*.


## <a name="next-steps"></a>Passaggi successivi
Quando il servizio di protezione è attivato per l'organizzazione, usare il [Guida alla distribuzione di Azure Information Protection](deployment-roadmap.md) per verificare se sono presenti altri passaggi di configurazione che potrebbe essere necessario eseguire prima di distribuire Azure Information Protection a utenti e amministratori. 

Potrebbe ad esempio, si desidera utilizzare [modelli](configure-policy-templates.md) per renderne più semplice per gli utenti applicare la protezione ai file, connettere i server locali per usare il servizio di protezione dati tramite l'installazione il [connettorediRightsManagement](deploy-rms-connector.md)e distribuire le [client Azure Information Protection](./rms-client/aip-client.md) che supporta la protezione di tutti i tipi di file su tutti i dispositivi. 

I servizi di Office, ad esempio Exchange Online e SharePoint Online, richiedono operazioni di configurazione aggiuntive prima di poter usare le funzionalità di Information Rights Management (IRM). Per informazioni sul funzionano delle applicazioni con il servizio di protezione Azure Rights Management, vedere [modo in cui le applicazioni supportano il servizio Azure Rights Management](applications-support.md).

