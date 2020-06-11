---
title: Guida di orientamento per la distribuzione di Azure Information Protection
description: Per preparare l'ambiente e per implementare e gestire Azure Information Protection per l'organizzazione, eseguire questa procedura.
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 06/10/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 086600c2-c5d8-47ec-a4c0-c782e1797486
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 9852c792e732a0d84326e7dfc6f8b291af56fcad
ms.sourcegitcommit: f32928f7dcc03111fc72d958cda9933d15065a2b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/10/2020
ms.locfileid: "84665861"
---
# <a name="azure-information-protection-deployment-roadmap"></a>Guida di orientamento per la distribuzione di Azure Information Protection

>*Si applica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

>[!NOTE] 
> Per offrire un'esperienza per i clienti unificata e semplificata, il **client di Azure Information Protection client (versione classica)** e la **Gestione etichette** nel portale di Azure vengono **deprecati** a partire dal **31 marzo 2021**. In questo intervallo di tempo tutti i clienti correnti di Azure Information Protection possono passare alla soluzione di etichettatura unificata usando la piattaforma di etichettatura unificata di Microsoft Information Protection. Altre informazioni nell'[avviso ufficiale sulla deprecazione](https://aka.ms/aipclassicsunset).

Usare le indicazioni della procedura che segue per preparare l'ambiente e per implementare e gestire Azure Information Protection per l'organizzazione.

In alternativa: 

- Cerchi istruzioni basate sullo scenario per Azure Information Protection? Vedere le [guide alle procedure per scenari comuni che usano Azure Information Protection](how-to-guides.md).

- Cerchi la roadmap per la versione Azure Information Protection? Vedere [informazioni sulle nuove versioni e sugli aggiornamenti](information-support.md#information-about-new-releases-and-updates).

### <a name="identify-your-deployment-roadmap"></a>Identificare la guida di orientamento per la distribuzione

Prima di eseguire questa procedura per distribuire Azure Information Protection, assicurarsi di aver letto [Requisiti per Azure Information Protection](./requirements.md).

Scegliere quindi la guida di orientamento per la distribuzione che sia applicabile alla propria organizzazione e che corrisponda alle [caratteristiche e funzionalità della sottoscrizione](https://azure.microsoft.com/pricing/details/information-protection/) richieste:

- [Usare le funzionalità di classificazione, assegnazione di etichette e protezione](#deployment-roadmap-for-classification-labeling-and-protection)
    
    Il percorso consigliato quando si dispone di una sottoscrizione di supporto perché le funzionalità aggiuntive supportano l'individuazione di informazioni riservate e l'assegnazione di etichette a documenti e messaggi di posta elettronica per la classificazione. Le etichette possono anche applicare la protezione, astrarre questa complessità dagli utenti.
    
    La procedura di distribuzione è adatta per le etichette di Azure Information Protection e le etichette di riservatezza che usano la [piattaforma di assegnazione di etichette unificata](faqs.md#how-can-i-determine-if-my-tenant-is-on-the-unified-labeling-platform).

- [Usare solo la funzionalità di protezione dei dati](#deployment-roadmap-for-data-protection-only)
    
    Percorso da usare quando non si dispone di una sottoscrizione che supporta la classificazione e le etichette, ma supporta la protezione senza etichette.

## <a name="deployment-roadmap-for-classification-labeling-and-protection"></a>Guida di orientamento per la distribuzione delle funzionalità di classificazione, assegnazione di etichette e protezione

> [!NOTE]
> Se si usano già le funzionalità di Azure Information Protection, è possibile ignorare molti di questi passaggi e concentrare l'attenzione sui passaggi 3 e 5.1.

### <a name="step-1-confirm-your-subscription-and-assign-user-licenses"></a>Passaggio 1: Verificare la sottoscrizione e assegnare licenze utente
Esaminare le informazioni sulla sottoscrizione e l'elenco delle funzionalità nella pagina [Prezzi di Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection) per verificare che l'organizzazione abbia una sottoscrizione che include le caratteristiche e le funzionalità previste. Assegnare quindi le licenze da tale sottoscrizione a ogni utente dell'organizzazione, che potrà così classificare, etichettare e proteggere documenti e messaggi di posta elettronica.

Nota: non assegnare manualmente licenze utente dalla sottoscrizione gratuita di RMS per singoli utenti e non usare questa licenza per amministrare il servizio Azure Rights Management per la propria organizzazione. Queste licenze vengono visualizzate come **Rights Management Adhoc** (Ad-hoc per Rights Manager) nell'interfaccia di amministrazione di Microsoft 365 e come **RIGHTSMANAGEMENT_ADHOC** quando si esegue il cmdlet di PowerShell per Azure AD, [Get-MsolAccountSku](https://msdn.microsoft.com/library/azure/dn194118.aspx). Per altre informazioni sulle modalità in cui la sottoscrizione di RMS per singoli utenti viene automaticamente concessa e assegnata agli utenti, vedere [RMS per utenti singoli e Azure Information Protection](./rms-for-individuals.md).

### <a name="step-2-prepare-your-tenant-to-use-azure-information-protection"></a>Passaggio 2: Preparare il tenant per l'uso di Azure Information Protection

Prima di iniziare a usare Azure Information Protection, verificare di avere account utente e gruppi in Office 365 o Azure Active Directory. Questi account utente e gruppi verranno usati da Azure Information Protection per autenticare e autorizzare gli utenti dell'organizzazione. Se necessario, creare questi account e gruppi o sincronizzarli dalla directory locale. 

Per altre informazioni, vedere [Preparazione di utenti e gruppi per Azure Information Protection](prepare.md).

### <a name="step-3-configure-and-deploy-classification-and-labeling"></a>Passaggio 3: Configurare e distribuire le funzionalità di classificazione e assegnazione di etichette

Prima di configurare le etichette e le impostazioni dei criteri, decidere quale client di Azure Information Protection si utilizzerà: il client classico o il client di etichetta unificata. In alternativa, potrebbero essere necessari entrambi i client. Questa decisione client è ora necessaria, quindi si conosce il portale di gestione da usare per configurare le etichette e le impostazioni dei criteri. Per altre informazioni e per semplificare questa decisione, vedere scegliere il [client Azure Information Protection da usare](./rms-client/use-client.md#choose-which-labeling-client-to-use-for-windows-computers).

> [!TIP]
> **Facoltativo ma consigliato**: provare a usare la [Guida introduttiva dello scanner](quickstart-findsensitiveinfo.md) per individuare le informazioni riservate presenti negli archivi dati locali. Le informazioni trovate dallo scanner possono semplificare la tassonomia di classificazione, oltre a fornire informazioni utili sulle etichette richieste e sui file che necessitano di protezione.
> 
> Poiché la modalità di individuazione dello scanner non richiede la configurazione di etichette o se è stata definita la tassonomia della classificazione, l'esecuzione dello scanner in questo modo è adatta per questa fase iniziale della distribuzione. È anche possibile usare questa configurazione dello scanner in parallelo con i passaggi di distribuzione seguenti, fino a quando non si configurano le etichette consigliate o automatiche.

Se non si dispone già di una strategia di classificazione, esaminare i [criteri predefiniti Azure Information Protection](./configure-policy-default.md) e usarli come base per decidere quali etichette di classificazione assegnare ai dati dell'organizzazione. È possibile personalizzare questi criteri in base ai requisiti aziendali.

Riconfigurare le etichette per apportare le modifiche necessarie per supportare le decisioni di classificazione. Configurare i criteri per l'assegnazione manuale di etichette da parte degli utenti e scrivere istruzioni per gli utenti che consentono di decidere quale etichetta applicare e in quali casi. Se i criteri predefiniti sono stati creati con etichette che applicano la protezione automaticamente, rimuovere temporaneamente le impostazioni di protezione o disabilitare le etichette. Per ulteriori informazioni sulla configurazione delle etichette e delle impostazioni dei criteri, vedere la documentazione seguente:

- Etichette di Azure Information Protection per il client classico: [configurazione dei criteri di Azure Information Protection](./configure-policy.md)

- Etichette di riservatezza per il client Unified Labeling: [informazioni sulle etichette di riservatezza](https://docs.microsoft.com/microsoft-365/compliance/sensitivity-labels)

Distribuire quindi il client di Azure Information Protection (versione classica) o il client per l'assegnazione di etichette unificata Azure Information Protection per gli utenti. Fornire formazione per gli utenti e istruzioni specifiche per la selezione delle etichette. Per ulteriori informazioni sull'installazione e sul supporto dei client, vedere le guide di amministrazione:

- [Guida per l'amministratore del client di Azure Information Protection](./rms-client/client-admin-guide.md)

- [Guida dell'amministratore client per l'assegnazione di etichette unificata Azure Information Protection](./rms-client/clientv2-admin-guide.md)

Dopo un certo periodo di tempo, quando gli utenti sono in grado di assegnare etichette a documenti e messaggi di posta elettronica, introdurre configurazioni più avanzate, Ecco alcuni esempi:

- Applicare un'etichetta predefinita

- Richiedere agli utenti di indicare il motivo per cui hanno scelto un'etichetta con un livello di classificazione più basso o hanno rimosso un'etichetta

- Imporre l'assegnazione di un'etichetta a tutti i documenti e i messaggi di posta elettronica

- Personalizzare le intestazioni, i piè di pagina o le filigrane

- Etichettatura consigliata e automatica

In questa fase, non selezionare l'opzione per proteggere documenti e messaggi di posta elettronica. Tuttavia, dopo avere configurato le etichette per l'assegnazione automatica, eseguire lo [scanner di Azure Information Protection](deploy-aip-scanner.md) sugli archivi dati locali in modalità di individuazione e in modo da soddisfare i criteri. L'esecuzione dello scanner con questa configurazione indica quali etichette verranno applicate ai file. Queste informazioni consentono di ottimizzare la configurazione delle etichette e di prepararsi per la classificazione e la protezione dei file in blocco. 

### <a name="step-4-prepare-for-data-protection"></a>Passaggio 4: Prepararsi per la protezione dei dati

Quando gli utenti sono in grado di assegnare etichette ai documenti e ai messaggi di posta elettronica, si è pronti per iniziare a introdurre la protezione dei dati più sensibili. Questa fase richiede la preparazione seguente:

1. Decidere se si desidera che Microsoft gestisca la chiave del tenant (impostazione predefinita) oppure generare e gestire personalmente la chiave del tenant. Questo servizio è noto come BYOK (Bring Your Own Key). Per altre informazioni, vedere [Planning and implementing your Azure Information Protection tenant key](plan-implement-tenant-key.md) (Pianificazione e implementazione della chiave del tenant Azure Information Protection).

2. Installare il modulo PowerShell per AIPService in almeno un computer dotato di accesso a Internet. È possibile eseguire questo passaggio subito o più avanti. Per altre informazioni, vedere [installazione del modulo PowerShell AIPService](./install-powershell.md).

3. Se attualmente si usa AD RMS, eseguire una migrazione per spostare le chiavi, i modelli e gli URL nel cloud. Per altre informazioni, vedere [Migrazione da AD RMS a Information Protection](migrate-from-ad-rms-to-azure-rms.md).

4. Verificare che il servizio di protezione sia attivato in modo che sia possibile iniziare a proteggere documenti e messaggi di posta elettronica. Se è richiesta una distribuzione in più fasi, configurare i controlli di selezione utenti per limitare la capacità degli utenti di applicare la protezione. Per altre informazioni, vedere [Attivazione del servizio di protezione da Azure Information Protection](./activate-service.md).

Facoltativamente, considerare la possibilità di configurare quanto segue:

- Registrazione dei dati di utilizzo per monitorare le modalità con cui l'organizzazione usa il servizio di protezione. È possibile eseguire questo passaggio subito o più avanti. Per ulteriori informazioni, vedere [registrazione e analisi dell'utilizzo della protezione da Azure Information Protection](./log-analyze-usage.md).

### <a name="step-5-configure-labels-and-settings-applications-and-services-for-data-protection"></a>Passaggio 5: configurare le etichette e le impostazioni, le applicazioni e i servizi per la protezione dei dati

1. Aggiornare le etichette per applicare la protezione
    
    Per il client di Azure Information Protection (classico), vedere [How to Configure an Label for Rights Management Protection](./configure-policy-protection.md).
    
    Per il client di etichettatura unificata di Azure Information Protection, vedere [limitare l'accesso al contenuto usando la crittografia in etichette di riservatezza](https://docs.microsoft.com/microsoft-365/compliance/encryption-sensitivity-labels).
    
    Si noti che in Outlook gli utenti possono applicare etichette per attivare la protezione di Rights Management anche se Exchange non è configurato per i servizi Information Rights Management (IRM). Tuttavia, finché Exchange non sarà configurato per IRM o per [Office 365 Message Encryption con nuove funzionalità](https://support.office.com/article/7ff0c040-b25c-4378-9904-b1b50210d00e), l'organizzazione non potrà usufruire in modo completo della protezione di Azure Rights Management con Exchange. Questa configurazione aggiuntiva è inclusa nell'elenco seguente, 2 per Exchange Online e 5 per Exchange locale. 

2. Configurare le applicazioni e i servizi di Office
    
    Configurare le applicazioni e i servizi di Office per le funzionalità IRM (Information Rights Management) in Microsoft SharePoint o Exchange Online. Per altre informazioni, vedere [configurazione di applicazioni per Azure Rights Management](configure-applications.md).

3. Configurare la funzionalità relativa agli utenti con privilegi avanzati per il ripristino dei dati
    
    Se sono presenti servizi IT che prevedono l'analisi dei file che verranno protetti da Azure Information Protection, ad esempio soluzioni di prevenzione della perdita di dati, gateway con crittografia del contenuto e prodotti anti-malware, configurare gli account di questi servizi come utenti con privilegi avanzati per Azure Rights Management. Per ulteriori informazioni, vedere [configurazione degli utenti con privilegi avanzati per Azure Information Protection e servizi di individuazione o ripristino dei dati](./configure-super-users.md).

4. Classificare e proteggere i file esistenti in blocco
    
    Per gli archivi dati locali, eseguire ora lo [scanner di Azure Information Protection](deploy-aip-scanner.md) in modalità di imposizione in modo che i file vengano etichettati automaticamente. Per gli archivi dati basati su cloud, usare [Azure Cloud App Security](https://docs.microsoft.com/cloud-app-security).
    
    Per i file nei PC, è possibile usare i cmdlet di PowerShell per classificare e proteggere i file. Per ulteriori informazioni, vedere le guide di amministrazione seguenti:
    
    - Client di Azure Information Protection (classico): [uso di PowerShell con il client di Azure Information Protection](./rms-client/client-admin-guide-powershell.md)
    
    - Azure Information Protection client per l'assegnazione di etichette unificata: [uso di PowerShell con il client di Azure Information Protection Unified Labeling](./rms-client/clientv2-admin-guide-powershell.md)

6. Distribuire il connettore per le raccolte protette con IRM in SharePoint Server e i messaggi protetti con IRM per Exchange locale
    
    Se si dispone di SharePoint ed Exchange locale e si vogliono usare le funzionalità di Information Rights Management (IRM), installare e configurare il connettore di Rights Management. Per altre informazioni, vedere [Deploying the Azure Rights Management Connector](./deploy-rms-connector.md).

### <a name="step-6-use-and-monitor-your-data-protection-solutions"></a>Passaggio 6: Usare e monitorare le soluzioni di protezione dei dati
A questo punto è possibile monitorare il modo in cui l'organizzazione usa le etichette configurate e confermare che si stanno proteggendo le informazioni riservate. Per altre informazioni a supporto di questa fase di distribuzione, vedere gli argomenti seguenti:

- [Reporting centrale per Azure Information Protection](reports-aip.md) al momento in anteprima

- [Registrazione dell'utilizzo locale con monitoraggio eventi di Windows](./rms-client/client-admin-guide-files-and-logging.md#usage-logging-for-the-azure-information-protection-client) per il client di Azure Information Protection (versione classica)

- [Registrazione e analisi dell'utilizzo della protezione da Azure Information Protection](./log-analyze-usage.md)

### <a name="step-7-administer-the-protection-service-for-your-tenant-account-as-needed"></a>Passaggio 7: Amministrare il servizio di protezione per l'account tenant in base alle esigenze

Quando si inizia a usare il servizio di protezione, PowerShell può essere utile per facilitare l'esecuzione di script o l'automazione di modifiche di carattere amministrativo. Per alcune delle configurazioni avanzate potrebbe essere richiesto anche PowerShell. 

Per altre informazioni, vedere [amministrazione della protezione da Azure Information Protection tramite PowerShell](./administer-powershell.md).


## <a name="deployment-roadmap-for-data-protection-only"></a>Guida di orientamento per la distribuzione della sola funzionalità di protezione

### <a name="step-1-confirm-that-you-have-a-subscription-that-includes-the-protection-service-from-azure-information-protection"></a>Passaggio 1: Verificare di avere una sottoscrizione che includa il servizio di protezione di Azure Information Protection

Esaminare le informazioni sulla sottoscrizione e l'elenco delle funzionalità nella pagina [Prezzi di Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection) per verificare che l'organizzazione abbia una sottoscrizione che include le caratteristiche e le funzionalità previste. Assegnare quindi una licenza da tale sottoscrizione a ogni utente dell'organizzazione, che potrà così proteggere documenti e messaggi di posta elettronica.

Nota: non assegnare manualmente licenze utente dalla sottoscrizione gratuita di RMS per singoli utenti e non usare questa licenza per amministrare il servizio Azure Rights Management per la propria organizzazione. Queste licenze vengono visualizzate come **Rights Management Adhoc** (Ad-hoc per Rights Manager) nell'interfaccia di amministrazione di Microsoft 365 e come **RIGHTSMANAGEMENT_ADHOC** quando si esegue il cmdlet di PowerShell per Azure AD, [Get-MsolAccountSku](https://msdn.microsoft.com/library/azure/dn194118.aspx). Per altre informazioni sulle modalità in cui la sottoscrizione di RMS per singoli utenti viene automaticamente concessa e assegnata agli utenti, vedere [RMS per utenti singoli e Azure Information Protection](./rms-for-individuals.md).


### <a name="step-2-prepare-your-tenant-to-use-azure-information-protection"></a>Passaggio 2: Preparare il tenant per l'uso di Azure Information Protection

Prima di iniziare a usare il servizio di protezione di Azure Information Protection, eseguire le attività di preparazione seguenti:

1. Verificare che il tenant di Office 365 contenga gli account utente e i gruppi che Azure Information Protection dovrà usare per autenticare gli utenti dell'organizzazione. Se necessario, creare questi account e gruppi o sincronizzarli dalla directory locale. Per altre informazioni, vedere [Preparazione di utenti e gruppi per Azure Information Protection](prepare.md).

2. Decidere se si desidera che Microsoft gestisca la chiave del tenant (impostazione predefinita) oppure generare e gestire personalmente la chiave del tenant. Questo servizio è noto come BYOK (Bring Your Own Key). Per altre informazioni, vedere [Planning and implementing your Azure Information Protection tenant key](plan-implement-tenant-key.md) (Pianificazione e implementazione della chiave del tenant Azure Information Protection).

3. Installare il modulo PowerShell per AIPService in almeno un computer dotato di accesso a Internet. È possibile eseguire questo passaggio subito o più avanti. Per altre informazioni, vedere [installazione del modulo PowerShell AIPService](./install-powershell.md).

4. Se attualmente si usa AD RMS, eseguire una migrazione per spostare le chiavi, i modelli e gli URL nel cloud. Per altre informazioni, vedere [Migrazione da AD RMS ad Azure Information Protection](migrate-from-ad-rms-to-azure-rms.md).

5. Verificare che il servizio di protezione sia attivato in modo che sia possibile iniziare a proteggere documenti e messaggi di posta elettronica. Se è richiesta una distribuzione in più fasi, configurare i controlli di selezione utenti per limitare la capacità degli utenti di applicare la protezione. Per altre informazioni, vedere [Attivazione del servizio di protezione da Azure Information Protection](./activate-service.md).

Facoltativamente, considerare la possibilità di configurare quanto segue:

- Modelli personalizzati per impostazioni di protezione se i modelli predefiniti non sono sufficienti per l'organizzazione. È possibile eseguire questo passaggio subito o più avanti. Per altre informazioni, vedere [Configurazione e gestione dei modelli per Azure Information Protection](./configure-policy-templates.md).

- Registrazione dei dati di utilizzo per monitorare le modalità con cui l'organizzazione usa il servizio di protezione. È possibile eseguire questo passaggio subito o più avanti. Per ulteriori informazioni, vedere [registrazione e analisi dell'utilizzo della protezione da Azure Information Protection](./log-analyze-usage.md).

### <a name="step-3-install-the-azure-information-protection-client-classic-and-configure-applications-and-services-for-rights-management"></a>Passaggio 3: installare il client di Azure Information Protection (versione classica) e configurare le applicazioni e i servizi per Rights Management

1. Distribuire il client di Azure Information Protection (versione classica)
    
    Installare il client classico affinché gli utenti supportino Office 2010, per proteggere i file diversi da documenti e messaggi di posta elettronica di Office e per tenere traccia dei documenti protetti. Fornire agli utenti istruzioni per l'uso di questo client. Per altre informazioni, vedere [Client Azure Information Protection per Windows](./rms-client/aip-client.md).

2. Configurare le applicazioni e i servizi di Office
    
    Configurare le applicazioni e i servizi di Office per le funzionalità IRM (Information Rights Management) in SharePoint o in Exchange Online. Per altre informazioni, vedere [configurazione di applicazioni per Azure Rights Management](./configure-applications.md).

3. Configurare la funzionalità relativa agli utenti con privilegi avanzati per il ripristino dei dati
    
    Se sono presenti servizi IT che prevedono l'analisi dei file che verranno protetti da Azure Information Protection, ad esempio soluzioni di prevenzione della perdita di dati, gateway con crittografia del contenuto e prodotti anti-malware, configurare gli account di questi servizi come utenti con privilegi avanzati per Azure Rights Management. Per ulteriori informazioni, vedere [configurazione degli utenti con privilegi avanzati per Azure Information Protection e servizi di individuazione o ripristino dei dati](./configure-super-users.md).

4. Proteggere i file esistenti in blocco 
    
    È possibile usare i cmdlet di PowerShell per proteggere o rimuovere la protezione per più tipi di file in blocco. Per altre informazioni, vedere [uso di PowerShell con il client Azure Information Protection](./rms-client/client-admin-guide-powershell.md) dalla guida dell'amministratore.
    
    Per i file nei file server basati su Windows, è possibile usare questi cmdlet con uno script e Infrastruttura di classificazione file per Windows Server. Per altre informazioni, vedere [Protezione RMS con Infrastruttura di classificazione file per Windows Server](./rms-client/configure-fci.md).

5. Distribuire il connettore per i server locali
    
    Se si prevede di usare servizi locali con il servizio di protezione, installare e configurare il connettore di Rights Management. Per altre informazioni, vedere [Deploying the Azure Rights Management Connector](./deploy-rms-connector.md).

### <a name="step-4-use-and-monitor-your-data-protection-solutions"></a>Passaggio 4: Usare e monitorare le soluzioni di protezione dei dati

A questo punto è possibile proteggere i dati e registrare il modo in cui l'azienda usa il servizio di protezione. Per informazioni aggiuntive per il supporto di questa fase di distribuzione, vedere [consentire agli utenti di proteggere i file tramite il servizio Rights Management di Azure](./help-users.md) e [registrazione e analisi dell'utilizzo della protezione da Azure Information Protection](./log-analyze-usage.md).

### <a name="step-5-administer-the-protection-service-for-your-tenant-account-as-needed"></a>Passaggio 5: Amministrare il servizio di protezione per l'account tenant in base alle esigenze

Quando si inizia a usare il servizio di protezione, PowerShell può essere utile per facilitare l'esecuzione di script o l'automazione di modifiche di carattere amministrativo. Per alcune delle configurazioni avanzate potrebbe essere richiesto anche PowerShell. 

Per altre informazioni, vedere [amministrazione della protezione da Azure Information Protection tramite PowerShell](./administer-powershell.md).

## <a name="next-steps"></a>Passaggi successivi

Quando si distribuisce Azure Information Protection, potrebbe essere utile consultare le [domande frequenti](faqs.md)e la pagina [informazioni e supporto](information-support.md) per ulteriori risorse.