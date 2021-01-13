---
title: Guida di orientamento per la distribuzione di Azure Information Protection (AIP) per la protezione
description: Usare questa procedura per preparare, implementare e gestire Azure Information Protection (AIP) per l'organizzazione, quando si vuole implementare solo la protezione.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 07/23/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 086600c2-c5d8-47ec-a4c0-c782e1797486
ROBOTS: NOINDEX
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 293ed29ba70ae5f4adff5530d782ecb661a6f9dd
ms.sourcegitcommit: 78c7ab80be7c292ea4bc62954a4e29c449e97439
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/13/2021
ms.locfileid: "98164114"
---
# <a name="azure-information-protection-deployment-roadmap-for-protection-only"></a>Guida di orientamento per la distribuzione di Azure Information Protection solo per la protezione

>***Si applica a**: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*
>
>***Pertinente per**: [Azure Information Protection client classico per Windows](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients). Per il client Unified Labeling, vedere la Guida [di orientamento per la distribuzione di AIP per la classificazione, l'assegnazione di etichette e la protezione](deployment-roadmap-classify-label-protect.md). *

> [!NOTE] 
> Per offrire un'esperienza per i clienti unificata e semplificata, il **client classico di Azure Information Protection** e **Gestione etichette** nel portale di Azure saranno **deprecati** a partire dal **31 marzo 2021**. In questo intervallo di tempo tutti i clienti correnti di Azure Information Protection possono passare alla soluzione di etichettatura unificata usando la piattaforma di etichettatura unificata di Microsoft Information Protection. Altre informazioni nell'[avviso ufficiale sulla deprecazione](https://aka.ms/aipclassicsunset).

> [!TIP]
> In alternativa, è possibile cercare uno degli articoli seguenti:
> - [Roadmap per la distribuzione di AIP per la classificazione, l'assegnazione di etichette e la protezione](deployment-roadmap-classify-label-protect.md)
> - [Guide pratiche per scenari comuni che usano Azure Information Protection](how-to-guides.md)
> - [Roadmap della versione Azure Information Protection](information-support.md#information-about-new-releases-and-updates)

Usare i passaggi seguenti come consigli per la preparazione, l'implementazione e la gestione di Azure Information Protection per l'organizzazione, quando si vuole implementare solo la protezione dei dati.

Questa roadmap è consigliata per i clienti con una sottoscrizione che non supporta la classificazione e le etichette, ma supporta la protezione senza etichette. È necessario che sia installato il client AIP classico. 

## <a name="deployment-process"></a>Processo di distribuzione

Eseguire la procedura seguente:

1. [Verificare di disporre di una sottoscrizione che includa il servizio di protezione AIP](#confirm-that-you-have-a-subscription-that-includes-the-aip-protection-service) 
1. [Preparare il tenant per l'uso di Azure Information Protection](#prepare-your-tenant-to-use-azure-information-protection)
1. [Installare le applicazioni e i servizi di Azure Information Protection classico e client per Rights Management](#install-the-azure-information-protection-classic-and-client-configure-applications-and-services-for-rights-management)
1. [Usare e monitorare le soluzioni di protezione dei dati](#use-and-monitor-your-data-protection-solutions)
1. [Amministrare il servizio di protezione per l'account tenant in base alle esigenze](#administer-the-protection-service-for-your-tenant-account-as-needed)

## <a name="confirm-that-you-have-a-subscription-that-includes-the-aip-protection-service"></a>Verificare di disporre di una sottoscrizione che includa il servizio di protezione AIP

Verificare che l'organizzazione disponga di una sottoscrizione che includa le funzionalità e le funzionalità che si prevede. È possibile utilizzare le informazioni sulla sottoscrizione e l'elenco delle funzionalità nella pagina dei [prezzi Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection) .

Assegnare una licenza da questa sottoscrizione a ogni utente dell'organizzazione che proteggerà documenti e messaggi di posta elettronica.

> [!IMPORTANT]
> non assegnare manualmente licenze utente dalla sottoscrizione gratuita di RMS per singoli utenti e non usare questa licenza per amministrare il servizio Azure Rights Management per la propria organizzazione. 
>
> Queste licenze vengono visualizzate come **Rights Management Adhoc** (Ad-hoc per Rights Manager) nell'interfaccia di amministrazione di Microsoft 365 e come **RIGHTSMANAGEMENT_ADHOC** quando si esegue il cmdlet di PowerShell per Azure AD, [Get-MsolAccountSku](/previous-versions/azure/dn194118(v=azure.100)). 
>
> Per altre informazioni sulle modalità in cui la sottoscrizione di RMS per singoli utenti viene automaticamente concessa e assegnata agli utenti, vedere [RMS per utenti singoli e Azure Information Protection](./rms-for-individuals.md).

## <a name="prepare-your-tenant-to-use-azure-information-protection"></a>Preparare il tenant per l'uso di Azure Information Protection

Prima di iniziare a usare il servizio di protezione di Azure Information Protection, eseguire le attività di preparazione seguenti:

1. **Configurare gli account utente e i gruppi per AIP**

    Verificare che il tenant di Microsoft 365 contenga gli account utente e i gruppi che verranno usati da Azure Information Protection per autenticare e autorizzare gli utenti dell'organizzazione. Se necessario, creare questi account e gruppi o sincronizzarli dalla directory locale. 

    Per altre informazioni, vedere [Preparazione di utenti e gruppi per Azure Information Protection](prepare.md).

1. **Decidere come si vuole gestire la chiave del tenant**

    Decidere se si desidera che Microsoft gestisca la chiave del tenant (impostazione predefinita) oppure generare e gestire personalmente la chiave del tenant. Questo servizio è noto come BYOK (Bring Your Own Key). Per una maggiore sicurezza, implementare la protezione HYOK ("Mantieni la propria chiave"). 

    Per altre informazioni, vedere [Planning and implementing your Azure Information Protection tenant key](plan-implement-tenant-key.md) (Pianificazione e implementazione della chiave del tenant Azure Information Protection).

1. **Installare PowerShell per AIP**

    Installare il modulo PowerShell per AIPService in almeno un computer dotato di accesso a Internet. È possibile eseguire questo passaggio subito o più avanti. 

    Per altre informazioni, vedere [installazione del modulo PowerShell AIPService](./install-powershell.md).

1. **Solo AD RMS: eseguire la migrazione dei dati nel cloud**

    Se attualmente si usa AD RMS, eseguire una migrazione per spostare le chiavi, i modelli e gli URL nel cloud. 

    Per altre informazioni, vedere [Migrazione da AD RMS ad Azure Information Protection](migrate-from-ad-rms-to-azure-rms.md).

1. **Attiva protezione**

    Verificare che il servizio di protezione sia attivato in modo che sia possibile iniziare a proteggere documenti e messaggi di posta elettronica. Se si esegue la distribuzione in fasi, configurare i controlli di onboarding degli utenti per limitare la capacità degli utenti di applicare la protezione. 

    Per altre informazioni, vedere [Attivazione del servizio di protezione da Azure Information Protection](./activate-service.md).

1. **Configurare le funzionalità facoltative in base alle esigenze**

    Considerare la possibilità di configurare una delle funzionalità seguenti, ora o versione successiva.
    
    |Funzionalità  |Description  |
    |---------|---------|
    |**Modelli personalizzati per le impostazioni di protezione**     |  Se i modelli predefiniti non sono sufficienti per l'organizzazione, configurare i modelli personalizzati. </br>Per altre informazioni, vedere [Configurazione e gestione dei modelli per Azure Information Protection](./configure-policy-templates.md).       |
    |**Registrazione dell'utilizzo**     | Configurare la registrazione dell'utilizzo per monitorare il modo in cui l'organizzazione usa il servizio di protezione. </br>Per ulteriori informazioni, vedere [registrazione e analisi dell'utilizzo della protezione da Azure Information Protection](./log-analyze-usage.md).        |
    | | |

## <a name="install-the-azure-information-protection-classic-and-client-configure-applications-and-services-for-rights-management"></a>Installare le applicazioni e i servizi di Azure Information Protection classico e client per Rights Management

Eseguire la procedura seguente:

1. **Distribuire il client di Azure Information Protection classico**
    
    Installare il client classico affinché gli utenti supportino Office 2010, per proteggere i file diversi da documenti e messaggi di posta elettronica di Office e per tenere traccia dei documenti protetti e fornire la formazione degli utenti per questo client. 

    Per ulteriori informazioni, vedere [Azure Information Protection client classico per Windows](./rms-client/aip-client.md) e [AIP per le versioni di Windows e Office nel supporto esteso](known-issues.md#aip-for-windows-and-office-versions-in-extended-support).

2. **Configurare le applicazioni e i servizi di Office**
    
    Configurare le applicazioni e i servizi di Office per le funzionalità IRM (Information Rights Management) in SharePoint o in Exchange Online. 

    Per altre informazioni, vedere [configurazione di applicazioni per Azure Rights Management](./configure-applications.md).

3. **Configurare la funzionalità relativa agli utenti con privilegi avanzati per il ripristino dei dati**
    
    Se sono presenti servizi IT che prevedono l'analisi dei file che verranno protetti da Azure Information Protection, ad esempio soluzioni di prevenzione della perdita di dati, gateway con crittografia del contenuto e prodotti antimalware, configurare gli account di tali servizi come utenti con privilegi avanzati per Azure Rights Management. 

    Per ulteriori informazioni, vedere [configurazione degli utenti con privilegi avanzati per Azure Information Protection e servizi di individuazione o ripristino dei dati](./configure-super-users.md).

4. **Proteggere i file esistenti in blocco** 
    
    È possibile usare i cmdlet di PowerShell per proteggere o rimuovere la protezione per più tipi di file in blocco. 

    Per altre informazioni, vedere [uso di PowerShell con il client Azure Information Protection](./rms-client/client-admin-guide-powershell.md) dalla guida dell'amministratore.
    
    Per i file nei file server basati su Windows, è possibile usare questi cmdlet con uno script e Infrastruttura di classificazione file per Windows Server. Per altre informazioni, vedere [Protezione RMS con Infrastruttura di classificazione file per Windows Server](./rms-client/configure-fci.md).

5. **Distribuire il connettore per i server locali**
    
    Se si prevede di usare servizi locali con il servizio di protezione, installare e configurare il connettore di Rights Management. 

    Per ulteriori informazioni, vedere [Distribuzione del connettore di Azure Rights Management](./deploy-rms-connector.md).

## <a name="use-and-monitor-your-data-protection-solutions"></a>Usare e monitorare le soluzioni di protezione dei dati

A questo punto è possibile proteggere i dati e registrare il modo in cui l'azienda usa il servizio di protezione. 

Per altre informazioni, vedere:

- [Consentire agli utenti di proteggere i file mediante il servizio Azure Rights Management](./help-users.md)
- [Registrazione e analisi dell'utilizzo della protezione da Azure Information Protection](./log-analyze-usage.md)

## <a name="administer-the-protection-service-for-your-tenant-account-as-needed"></a>Amministrare il servizio di protezione per l'account tenant in base alle esigenze

Quando si inizia a usare il servizio di protezione, PowerShell può essere utile per facilitare l'esecuzione di script o l'automazione di modifiche di carattere amministrativo. Per alcune delle configurazioni avanzate potrebbe essere richiesto anche PowerShell. 

Per altre informazioni, vedere [amministrazione della protezione da Azure Information Protection tramite PowerShell](./administer-powershell.md).

## <a name="next-steps"></a>Passaggi successivi

Quando si distribuisce Azure Information Protection, potrebbe essere utile consultare le [domande frequenti](faqs.md)e la pagina [informazioni e supporto](information-support.md) per ulteriori risorse.