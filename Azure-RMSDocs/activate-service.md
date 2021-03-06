---
title: Attivazione del servizio di protezione da Azure Information Protection (AIP)
description: Informazioni su come attivare il servizio Azure Rights Management Protection per proteggere documenti e messaggi di posta elettronica.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 11/30/2019
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: f8707e01-b239-4d1a-a1ea-0d1cf9a8d214
ms.subservice: azurerms
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: e3089134dc3b289d024c507aec886d622e4d6e16
ms.sourcegitcommit: 74b8d03d1ede3da12842b84546417e63897778bb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/07/2021
ms.locfileid: "102414770"
---
# <a name="activating-the-protection-service-from-azure-information-protection"></a>Attivazione del servizio di protezione da Azure Information Protection

>***Si applica a**: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*
>
>***Rilevante per**: [Client di etichettatura unificata e client classico di AIP](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

Questo articolo descrive come gli amministratori possono attivare il servizio Azure Rights Management Protection per Azure Information Protection (AIP). Quando il servizio di protezione viene attivato per l'organizzazione, gli amministratori e gli utenti possono iniziare a proteggere i dati importanti usando le applicazioni e i servizi che supportano questa soluzione di protezione delle informazioni. Gli amministratori possono anche gestire e monitorare i documenti e i messaggi di posta elettronica protetti di proprietà dell'azienda.

> [!NOTE]
> Le informazioni sulla configurazione sono riservate agli amministratori responsabili di un servizio applicato a tutti gli utenti all'interno di un'organizzazione. Per informazioni su come usare la funzionalità Rights Management per una specifica applicazione o aprire un file o un messaggio di posta elettronica protetto da diritti, vedere la guida e le informazioni aggiuntive fornite con l'applicazione.
>
> Ad esempio, per le applicazioni Office fare clic sull'icona della Guida e immettere i termini di ricerca, ad esempio **Rights Management** o **IRM**. Per il client Azure Information Protection per Windows, vedere la [Guida per l'utente del client Azure Information Protection](./rms-client/clientv2-user-guide.md).
>
> Per il supporto tecnico e altre domande sul servizio, vedere le informazioni riportate in [Opzioni di supporto e risorse per la community](information-support.md#support-options-and-community-resources).

## <a name="automatic-activation-for-azure-rights-management"></a>Attivazione automatica per Azure Rights Management

Quando si dispone di un piano di servizio che include Rights Management di Azure, potrebbe non essere necessario attivare il servizio:

- **Se la sottoscrizione che include Azure Rights Management o Azure Information Protection è stata ottenuta fino alla fine del 2018 febbraio o versione successiva**, il servizio viene attivato automaticamente. Non è necessario attivare il servizio, a meno che Azure Rights Management sia stato disattivato dall'utente o da un altro amministratore globale.

- **Se la sottoscrizione che include Azure Rights Management o Azure Information Protection è stata ottenuta prima o durante il 2018 febbraio**: Microsoft attiva il servizio Azure Rights Management per queste sottoscrizioni se il tenant usa Exchange Online. Per queste sottoscrizioni, il servizio verrà attivato a meno che non si veda che **AutomaticServiceUpdateEnabled** è impostato su **false** quando si esegue [Get-IRMConfiguration](/powershell/module/exchange/encryption-and-certificates/get-irmconfiguration). 

Se nessuno degli scenari elencati si applica, è necessario attivare manualmente il servizio di protezione. 

Dopo l'attivazione del servizio, tutti gli utenti dell'organizzazione potranno applicare la protezione delle informazioni ai propri documenti e messaggi di posta elettronica e tutti gli utenti potranno aprire (utilizzare) i documenti e i messaggi di posta elettronica protetti da questo servizio. Se si preferisce, tuttavia, è possibile limitare l'applicazione della protezione delle informazioni solo ad alcuni utenti, usando i controlli di selezione utenti per una distribuzione graduale. Per altre informazioni, vedere la sezione [Configurazione dei controlli di selezione utenti per una distribuzione graduale](#configuring-onboarding-controls-for-a-phased-deployment) di questo articolo.

## <a name="how-to-activate-or-confirm-the-status-of-the-protection-service"></a>Come attivare o confermare lo stato del servizio di protezione 

> [!IMPORTANT]
> Non attivare il servizio di protezione se è stato distribuito Active Directory Rights Management Services (AD RMS) per l'organizzazione. [Altre informazioni](prepare-environment-adrms.md)

Per usare questa soluzione di protezione dati, l'organizzazione deve essere in possesso di un piano di servizio che include il servizio Azure Rights Management di Azure Information Protection. Senza questo, il servizio di protezione non può essere attivato. È necessario disporre di:

- [Piano di Azure Information Protection](https://www.microsoft.com/cloud-platform/azure-information-protection-pricing) 

- Un [piano Office 365 che includa Rights Management](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf).

Quando il servizio di protezione viene attivato, tutti gli utenti dell'organizzazione possono applicare la protezione delle informazioni ai documenti e ai messaggi di posta elettronica e tutti gli utenti possono aprire (utilizzare) documenti e messaggi di posta elettronica protetti da questo servizio. Se si preferisce, tuttavia, è possibile limitare l'applicazione della protezione delle informazioni solo ad alcuni utenti, usando i controlli di selezione utenti per una distribuzione graduale. Per altre informazioni, vedere la sezione [Configurazione dei controlli di selezione utenti per una distribuzione graduale](#configuring-onboarding-controls-for-a-phased-deployment) di questo articolo.

## <a name="supported-activation-methods"></a>Metodi di attivazione supportati

Per istruzioni su come attivare il servizio di protezione dati dal portale di gestione, scegliere se usare l'interfaccia di amministrazione di Microsoft 365 o il portale di Azure:

- [Interfaccia di amministrazione di Microsoft 365](activate-office365.md) - richiede l'account di amministratore globale

- [Portale di Azure](activate-azure.md) - non richiede l'account di amministratore globale

In alternativa, è possibile usare i comandi PowerShell seguenti:

1. Installare il modulo AIPService per configurare e gestire il servizio di protezione. Per istruzioni, vedere [installazione del modulo PowerShell AIPService](install-powershell.md).

2. Da una sessione di PowerShell eseguire [Connect-AipService](/powershell/module/aipservice/connect-aipservice)e, quando richiesto, specificare i dettagli dell'account amministratore globale per il tenant di Azure Information Protection.

3. Eseguire [Get-AipService](/powershell/module/aipservice/get-aipservice) per verificare se il servizio di protezione è attivato. Lo stato **Abilitato** ne conferma l'attivazione; lo stato **Disabilitato** indica che il servizio è disattivato.

4. Per attivare il servizio, eseguire [Enable-AipService](/powershell/module/aipservice/enable-aipservice).

## <a name="configuring-onboarding-controls-for-a-phased-deployment"></a>Configurazione dei controlli di selezione utenti per una distribuzione graduale
Se non si vuole che tutti gli utenti siano in grado di proteggere i documenti e i messaggi di posta elettronica immediatamente usando Azure Information Protection, è possibile configurare i controlli di onboarding degli utenti usando il comando di PowerShell [set-AipServiceOnboardingControlPolicy](/powershell/module/aipservice/set-aipserviceonboardingcontrolpolicy) . È possibile eseguire questo comando prima o dopo l'attivazione del servizio Azure Rights Management.

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

Per ulteriori informazioni su questo cmdlet ed esempi aggiuntivi, vedere la Guida di [set-AipServiceOnboardingControlPolicy](/powershell/module/aipservice/set-aipserviceonboardingcontrolpolicy) .

Quando si usano questi controlli di selezione utenti, tutti gli utenti dell'organizzazione potranno utilizzare sempre i contenuti protetti dal sottoinsieme di utenti, ma non potranno applicare direttamente la protezione delle informazioni da applicazioni client. Ad esempio, non vedranno nelle app di Office i modelli di protezione predefiniti che vengono pubblicati automaticamente quando viene attivato il servizio di protezione o modelli personalizzati che è possibile configurare. Le applicazioni lato server, come Exchange, possono implementare i propri controlli per utente per ottenere lo stesso risultato. Ad esempio, per impedire agli utenti di proteggere messaggi di posta elettronica in Outlook sul Web, usare [Set-OwaMailboxPolicy](/powershell/module/exchange/client-access/set-owamailboxpolicy) per impostare il parametro *IRMEnabled* su *$false*.


## <a name="next-steps"></a>Passaggi successivi
Quando il servizio di protezione viene attivato per l'organizzazione, usare la Guida di orientamento per la [distribuzione Azure Information Protection](deployment-roadmap.md) per verificare se è necessario eseguire altri passaggi di configurazione prima di distribuire Azure Information Protection a utenti e amministratori. 

Ad esempio, è possibile usare i [modelli](configure-policy-templates.md) per semplificare l'applicazione della protezione ai file da parte degli utenti, connettere i server locali per usare il servizio di protezione installando il [connettore Rights Management](deploy-rms-connector.md)e distribuire il client di [Azure Information Protection](./rms-client/aip-client.md) che supporta la protezione di tutti i tipi di file in tutti i dispositivi. 

Per poter utilizzare le funzionalità IRM (Information Rights Management), i servizi Office, ad esempio Exchange Online e Microsoft SharePoint, richiedono una configurazione aggiuntiva. Per informazioni sul funzionamento delle applicazioni con il servizio di protezione, Azure Rights Management, vedere [come le applicazioni supportano il servizio azure Rights Management](applications-support.md).

