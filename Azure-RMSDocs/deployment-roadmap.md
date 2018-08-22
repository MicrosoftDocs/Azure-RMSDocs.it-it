---
title: Guida di orientamento per la distribuzione di Azure Information Protection
description: Per preparare l'ambiente e per implementare e gestire Azure Information Protection per l'organizzazione, eseguire questa procedura.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 03/05/2018
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 086600c2-c5d8-47ec-a4c0-c782e1797486
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 7107b98dabd31e1b4c8c9afc8a7ed26524d0c778
ms.sourcegitcommit: 5fdf013fe05b65517b56245e1807875d80be6e70
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2018
ms.locfileid: "39490374"
---
# <a name="azure-information-protection-deployment-roadmap"></a>Guida di orientamento per la distribuzione di Azure Information Protection

>*Si applica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](http://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

Usare le indicazioni della procedura che segue per preparare l'ambiente e per implementare e gestire Azure Information Protection per l'organizzazione.

Tuttavia, se si vuole provare rapidamente Azure Information Protection per conto proprio, anziché implementarlo in un ambiente di produzione, vedere [Esercitazione introduttiva di Azure Rights Management](./infoprotect-quick-start-tutorial.md).

> [!IMPORTANT]
> Prima di eseguire questa procedura, assicurarsi di aver letto [Requisiti per Azure Information Protection](./requirements.md).

Scegliere la guida di orientamento per la distribuzione che sia applicabile alla propria organizzazione e che corrisponda alle [caratteristiche e funzionalità della sottoscrizione](https://azure.microsoft.com/pricing/details/information-protection/) richieste:

- [Usare le funzionalità di classificazione, assegnazione di etichette e protezione](#deployment-roadmap-for-classification-labeling-and-protection)

- [Usare solo la funzionalità di protezione dei dati](#deployment-roadmap-for-data-protection-only)


## <a name="deployment-roadmap-for-classification-labeling-and-protection"></a>Guida di orientamento per la distribuzione delle funzionalità di classificazione, assegnazione di etichette e protezione

> [!NOTE]
> Se si usano già le funzionalità di Azure Information Protection, è possibile ignorare molti di questi passaggi e concentrare l'attenzione sui passaggi 3 e 5.1.

### <a name="step-1-confirm-your-subscription-and-assign-user-licenses"></a>Passaggio 1: Verificare la sottoscrizione e assegnare licenze utente
Esaminare le informazioni sulla sottoscrizione e l'elenco delle funzionalità nella pagina [Prezzi di Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection) per verificare che l'organizzazione abbia una sottoscrizione che include le caratteristiche e le funzionalità previste. Assegnare quindi una licenza da tale sottoscrizione a ogni utente dell'organizzazione, che potrà così classificare, etichettare e proteggere documenti e messaggi di posta elettronica.

Nota: non assegnare manualmente licenze utente dalla sottoscrizione gratuita di RMS per singoli utenti e non usare questa licenza per amministrare il servizio Azure Rights Management per la propria organizzazione. Queste licenze vengono visualizzate come **Rights Management Adhoc** (Ad-hoc per Rights Manager) nell'interfaccia di amministrazione di Office 365 e come **RIGHTSMANAGEMENT_ADHOC** quando si esegue il cmdlet di PowerShell per Azure AD, [Get-MsolAccountSku](https://msdn.microsoft.com/library/azure/dn194118.aspx). Per altre informazioni sulle modalità in cui la sottoscrizione di RMS per singoli utenti viene automaticamente concessa e assegnata agli utenti, vedere [RMS per utenti singoli e Azure Information Protection](./rms-for-individuals.md).


### <a name="step-2-prepare-your-tenant-to-use-azure-information-protection"></a>Passaggio 2: Preparare il tenant per l'uso di Azure Information Protection
Prima di iniziare a usare Azure Information Protection, eseguire le attività di preparazione seguenti:

- In Office 365 o in Azure Active Directory verificare che siano presenti account utente e gruppi utilizzabili da Azure Information Protection per l'autenticazione e l'autorizzazione degli utenti dell'organizzazione. Se necessario, creare questi account e gruppi o sincronizzarli dalla directory locale. Per altre informazioni, vedere [Preparazione di utenti e gruppi per Azure Information Protection](prepare.md).

### <a name="step-3-configure-and-deploy-classification-and-labeling"></a>Passaggio 3: Configurare e distribuire le funzionalità di classificazione e assegnazione di etichette

Se non si è ancora definita una strategia di classificazione, esaminare i [criteri predefiniti di Azure Information Protection](./configure-policy-default.md) e usarli come base per decidere quali etichette di classificazione assegnare ai dati dell'organizzazione. È possibile personalizzare questi criteri in base ai requisiti aziendali. 

Riconfigurare le etichette predefinite di Azure Information Protection per apportare le modifiche necessarie per supportare le decisioni di classificazione. Configurare i criteri per l'assegnazione manuale di etichette da parte degli utenti e scrivere istruzioni per gli utenti che consentono di decidere quale etichetta applicare e in quali casi. Se i criteri predefiniti sono stati creati con etichette che applicano la protezione automaticamente, rimuovere le impostazioni di protezione o disabilitare le etichette. Per altre informazioni su come configurare i criteri di Azure Information Protection, vedere [Configurazione dei criteri di Azure Information Protection](./configure-policy.md).

Distribuire quindi il client di Azure Information Protection per gli utenti e fornire loro istruzioni per l'uso e indicazioni per la selezione delle etichette. Per altre informazioni sull'installazione e il supporto del client, vedere la [Guida dell'amministratore del client Azure Information Protection](./rms-client/client-admin-guide.md).

Dopo un certo periodo di tempo, quando gli utenti sono in grado di assegnare etichette a documenti e messaggi di posta elettronica, introdurre configurazioni più avanzate, ad esempio:

- Applicare un'etichetta predefinita

- Richiedere agli utenti di indicare il motivo per cui hanno scelto un'etichetta con un livello di classificazione più basso

- Imporre l'assegnazione di un'etichetta a tutti i documenti e i messaggi di posta elettronica

- Personalizzare le intestazioni, i piè di pagina o le filigrane

- Definire le condizioni per il supporto delle azioni consigliate e l'assegnazione automatica di etichette

In questa fase, non selezionare l'opzione per proteggere documenti e messaggi di posta elettronica.

### <a name="step-4-prepare-for-data-protection"></a>Passaggio 4: Prepararsi per la protezione dei dati

Quando gli utenti sono in grado di assegnare etichette ai documenti e ai messaggi di posta elettronica, si è pronti per iniziare a introdurre la protezione dei dati più sensibili. Questa fase richiede la preparazione seguente:

1. Decidere se si desidera che Microsoft gestisca la chiave del tenant (impostazione predefinita) oppure generare e gestire personalmente la chiave del tenant. Questo servizio è noto come BYOK (Bring Your Own Key). Per altre informazioni, vedere [Pianificazione e implementazione della chiave del tenant di Azure Information Protection](plan-implement-tenant-key.md).

2. Installare il modulo di PowerShell per AADRM in almeno un computer dotato di accesso a Internet. È possibile eseguire questo passaggio subito o più avanti. Per altre informazioni, vedere [Installazione del modulo PowerShell AADRM](./install-powershell.md).

3. Se attualmente si usa AD RMS, eseguire una migrazione per spostare le chiavi, i modelli e gli URL nel cloud. Per altre informazioni, vedere [Migrazione da AD RMS a Information Protection](migrate-from-ad-rms-to-azure-rms.md).

4. Verificare che il servizio di protezione sia attivato in modo che sia possibile iniziare a proteggere documenti e messaggi di posta elettronica. Se è richiesta una distribuzione graduale, configurare i controlli di selezione utenti per limitare l'utilizzo a utenti specifici. Per ulteriori informazioni, vedere l'articolo relativo all'[attivazione di Azure Rights Management](./activate-service.md).

Facoltativamente, considerare la possibilità di configurare quanto segue:

-   Modelli personalizzati per impostazioni di protezione se i modelli predefiniti non sono sufficienti per l'organizzazione. È possibile eseguire questo passaggio subito o più avanti. Per altre informazioni, vedere [Configurazione e gestione dei modelli per Azure Information Protection](./configure-policy-templates.md).

-   Registrazione dei dati di utilizzo per monitorare le modalità con cui l'organizzazione usa il servizio di protezione. È possibile eseguire questo passaggio subito o più avanti. Per altre informazioni, vedere [Registrazione e analisi dell'utilizzo del servizio Azure Rights Management](./log-analyze-usage.md).

### <a name="step-5-configure-your-azure-information-protection-policy-applications-and-services-for-data-protection"></a>Passaggio 5: Configurare i criteri di Azure Information Protection, le applicazioni e i servizi per la protezione dei dati

1. Aggiornare i criteri di Azure Information Protection per applicare la protezione dei dati
    
    Modificare i criteri di Azure Information Protection in modo da usare una o più etichette per applicare la protezione. Per altre informazioni, vedere [Come configurare un'etichetta per la protezione di Rights Management](./configure-policy-protection.md).
    
    Si noti che in Outlook gli utenti possono applicare etichette per attivare la protezione di Rights Management anche se Exchange non è configurato per i servizi Information Rights Management (IRM). Tuttavia, finché Exchange non sarà configurato per IRM o per [Office 365 Message Encryption con nuove funzionalità](https://support.office.com/article/7ff0c040-b25c-4378-9904-b1b50210d00e), l'organizzazione non potrà usufruire in modo completo della protezione di Azure Rights Management con Exchange. Questa configurazione aggiuntiva è inclusa nell'elenco seguente, 2 per Exchange Online e 5 per Exchange locale. 

2. Configurare le applicazioni e i servizi di Office
    
    Configurare le applicazioni e i servizi di Office per le funzionalità di IRM (Information Rights Management) in SharePoint Online o Exchange Online. Per ulteriori informazioni, vedere [Configurazione delle applicazioni per Azure Rights Management](./configure-applications.md).

3. Configurare la funzionalità relativa agli utenti con privilegi avanzati per il ripristino dei dati
    
    Se sono presenti servizi IT che prevedono l'analisi dei file che verranno protetti da Azure Information Protection, ad esempio soluzioni di prevenzione della perdita di dati, gateway con crittografia del contenuto e prodotti antimalware, configurare gli account di tali servizi come utenti con privilegi avanzati per Azure Rights Management. Per ulteriori informazioni, vedere [Configurazione degli utenti con privilegi avanzati per Rights Management di Azure e servizi di individuazione o ripristino dei dati](./configure-super-users.md).

4. Classificare e proteggere file in blocco in base alle esigenze
    
    I cmdlet di PowerShell che consentono di classificare e proteggere i file, oltre che di rimuovere la classificazione e la protezione, vengono installati automaticamente con il client Azure Information Protection. Per altre informazioni, vedere [Uso di PowerShell con il client Azure Information Protection](./rms-client/client-admin-guide-powershell.md) nella guida dell'amministratore.

6. Distribuire il connettore per i server locali
    
    Se si prevede di usare servizi locali con il servizio di protezione, installare e configurare il connettore di Rights Management. Per ulteriori informazioni, vedere [Distribuzione del connettore di Azure Rights Management](./deploy-rms-connector.md).

### <a name="step-6-use-and-monitor-your-data-protection-solutions"></a>Passaggio 6: Usare e monitorare le soluzioni di protezione dei dati
È ora possibile proteggere i dati e registrare come vengono usate le etichette configurate e la protezione dei dati all'interno della società. Per altre informazioni a supporto di questa fase di distribuzione, vedere gli argomenti seguenti:

- [Consentire agli utenti di proteggere i file mediante il servizio Azure Rights Management](./help-users.md)

-  [Registrazione e analisi dell'utilizzo del servizio Azure Rights Management](./log-analyze-usage.md)

- [File del client e registrazione dell'utilizzo](./rms-client/client-admin-guide-files-and-logging.md)

Se si vuole proteggere automaticamente i file usando Infrastruttura di classificazione file in un file server basato su Windows, vedere [Protezione RMS con Infrastruttura di classificazione file per Windows Server](./rms-client/configure-fci.md).

### <a name="step-7-administer-the-protection-service-for-your-tenant-account-as-needed"></a>Passaggio 7: Amministrare il servizio di protezione per l'account tenant in base alle esigenze
Quando si inizia a usare il servizio di protezione, PowerShell può essere utile per facilitare l'esecuzione di script o l'automazione di modifiche di carattere amministrativo. Per altre informazioni, vedere [Amministrazione del servizio Azure Rights Management mediante Windows PowerShell](./administer-powershell.md).


## <a name="deployment-roadmap-for-data-protection-only"></a>Guida di orientamento per la distribuzione della sola funzionalità di protezione

### <a name="step-1-confirm-that-you-have-a-subscription-that-includes-the-protection-service-from-azure-information-protection"></a>Passaggio 1: Verificare di avere una sottoscrizione che includa il servizio di protezione di Azure Information Protection
Esaminare le informazioni sulla sottoscrizione e l'elenco delle funzionalità nella pagina [Prezzi di Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection) per verificare che l'organizzazione abbia una sottoscrizione che include le caratteristiche e le funzionalità previste. Assegnare quindi una licenza da tale sottoscrizione a ogni utente dell'organizzazione, che potrà così proteggere documenti e messaggi di posta elettronica.

Nota: non assegnare manualmente licenze utente dalla sottoscrizione gratuita di RMS per singoli utenti e non usare questa licenza per amministrare il servizio Azure Rights Management per la propria organizzazione. Queste licenze vengono visualizzate come **Rights Management Adhoc** (Ad-hoc per Rights Manager) nell'interfaccia di amministrazione di Office 365 e come **RIGHTSMANAGEMENT_ADHOC** quando si esegue il cmdlet di PowerShell per Azure AD, [Get-MsolAccountSku](https://msdn.microsoft.com/library/azure/dn194118.aspx). Per altre informazioni sulle modalità in cui la sottoscrizione di RMS per singoli utenti viene automaticamente concessa e assegnata agli utenti, vedere [RMS per utenti singoli e Azure Information Protection](./rms-for-individuals.md).


### <a name="step-2-prepare-your-tenant-to-use-azure-information-protection"></a>Passaggio 2: Preparare il tenant per l'uso di Azure Information Protection
Prima di iniziare a usare il servizio di protezione di Azure Information Protection, eseguire le attività di preparazione seguenti:

1.  Verificare che il tenant di Office 365 contenga gli account utente e i gruppi che Azure Information Protection dovrà usare per autenticare gli utenti dell'organizzazione. Se necessario, creare questi account e gruppi o sincronizzarli dalla directory locale. Per altre informazioni, vedere [Preparazione di utenti e gruppi per Azure Information Protection](prepare.md).

2. Decidere se si desidera che Microsoft gestisca la chiave del tenant (impostazione predefinita) oppure generare e gestire personalmente la chiave del tenant. Questo servizio è noto come BYOK (Bring Your Own Key). Per altre informazioni, vedere [Pianificazione e implementazione della chiave del tenant di Azure Information Protection](plan-implement-tenant-key.md).

3. Installare il modulo di PowerShell per AADRM in almeno un computer dotato di accesso a Internet. È possibile eseguire questo passaggio subito o più avanti. Per altre informazioni, vedere [Installazione del modulo PowerShell AADRM](./install-powershell.md).

4. Se attualmente si usa AD RMS, eseguire una migrazione per spostare le chiavi, i modelli e gli URL nel cloud. Per altre informazioni, vedere [Migrazione da AD RMS ad Azure Information Protection](migrate-from-ad-rms-to-azure-rms.md).

5. Verificare che il servizio di protezione sia attivato in modo che sia possibile iniziare a proteggere documenti e messaggi di posta elettronica. Se è richiesta una distribuzione graduale, configurare i controlli di selezione utenti per limitare l'utilizzo a utenti specifici. Per ulteriori informazioni, vedere l'articolo relativo all'[attivazione di Azure Rights Management](./activate-service.md).

Facoltativamente, considerare la possibilità di configurare quanto segue:

-   Modelli personalizzati per impostazioni di protezione se i modelli predefiniti non sono sufficienti per l'organizzazione. È possibile eseguire questo passaggio subito o più avanti. Per altre informazioni, vedere [Configurazione e gestione dei modelli per Azure Information Protection](./configure-policy-templates.md).

- Registrazione dei dati di utilizzo per monitorare le modalità con cui l'organizzazione usa il servizio di protezione. È possibile eseguire questo passaggio subito o più avanti. Per altre informazioni, vedere [Registrazione e analisi dell'utilizzo del servizio Azure Rights Management](./log-analyze-usage.md).

### <a name="step-3-install-the-client-and-configure-applications-and-services-for-rights-management"></a>Passaggio 3: Installare il client e configurare le applicazioni e i servizi per Rights Management

1. Distribuire il client Azure Information Protection
    
    Installare Azure Information Protection per gli utenti, per supportare Office 2010, per proteggere file diversi dai messaggi di posta elettronica e dai documenti di Office e per tenere traccia dei documenti protetti. Fornire agli utenti istruzioni per l'uso di questo client. Per altre informazioni, vedere [Client Azure Information Protection per Windows](./rms-client/aip-client.md).

2. Configurare le applicazioni e i servizi di Office
    
    Configurare le applicazioni e i servizi di Office per le funzionalità di IRM (Information Rights Management) in SharePoint Online o Exchange Online. Per ulteriori informazioni, vedere [Configurazione delle applicazioni per Azure Rights Management](./configure-applications.md).

3. Configurare la funzionalità relativa agli utenti con privilegi avanzati per il ripristino dei dati
    
    Se sono presenti servizi IT che prevedono l'analisi dei file che verranno protetti da Azure Information Protection, ad esempio soluzioni di prevenzione della perdita di dati, gateway con crittografia del contenuto e prodotti antimalware, configurare gli account di tali servizi come utenti con privilegi avanzati per Azure Rights Management. Per ulteriori informazioni, vedere [Configurazione degli utenti con privilegi avanzati per Rights Management di Azure e servizi di individuazione o ripristino dei dati](./configure-super-users.md).

4. Proteggere file in blocco in base alle esigenze 
    
    I cmdlet di PowerShell che consentono di proteggere più tipi di file in blocco, oltre che di annullare la protezione, vengono installati automaticamente con il client Azure Information Protection. Per altre informazioni, vedere [Uso di PowerShell con il client Azure Information Protection](./rms-client/client-admin-guide-powershell.md) nella guida dell'amministratore.

5. Distribuire il connettore per i server locali
    
    Se si prevede di usare servizi locali con il servizio di protezione, installare e configurare il connettore di Rights Management. Per ulteriori informazioni, vedere [Distribuzione del connettore di Azure Rights Management](./deploy-rms-connector.md).


### <a name="step-4-use-and-monitor-your-data-protection-solutions"></a>Passaggio 4: Usare e monitorare le soluzioni di protezione dei dati
È ora possibile proteggere i dati e registrare come viene usato il servizio di protezione all'interno della società. Per altre informazioni utili per questa fase di distribuzione, vedere [Consentire agli utenti di proteggere i file mediante il servizio Azure Rights Management](./help-users.md) e [Registrazione e analisi dell'utilizzo del servizio Azure Rights Management](./log-analyze-usage.md).

Se si vuole proteggere automaticamente i file usando Infrastruttura di classificazione file in un file server basato su Windows, vedere [Protezione RMS con Infrastruttura di classificazione file per Windows Server](./rms-client/configure-fci.md).

### <a name="step-5-administer-the-protection-service-for-your-tenant-account-as-needed"></a>Passaggio 5: Amministrare il servizio di protezione per l'account tenant in base alle esigenze
Quando si inizia a usare il servizio di protezione, PowerShell può essere utile per facilitare l'esecuzione di script o l'automazione di modifiche di carattere amministrativo. Per altre informazioni, vedere [Amministrazione del servizio Azure Rights Management mediante Windows PowerShell](./administer-powershell.md).
