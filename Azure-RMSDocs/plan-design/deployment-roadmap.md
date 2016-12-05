---
title: Guida di orientamento per la distribuzione di Azure Information Protection | Azure Information Protection
description: Per preparare l&quot;ambiente e per implementare e gestire Azure Information Protection per l&quot;organizzazione, eseguire questa procedura.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 11/21/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 086600c2-c5d8-47ec-a4c0-c782e1797486
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 1fb57d2317cc632a44a87f3ce7140ce737c240e0
ms.openlocfilehash: 9cc05664480ba0e5fa090db96afbcef73c318e07


---

# <a name="azure-information-protection-deployment-roadmap"></a>Guida di orientamento per la distribuzione di Azure Information Protection

>*Si applica a: Azure Information Protection, Office 365*

Per preparare l'ambiente e per implementare e gestire Azure Information Protection per l'organizzazione, eseguire questa procedura.

Tuttavia, se si vuole provare rapidamente Azure Information Protection per conto proprio, anziché implementarlo in un ambiente di produzione, vedere [Esercitazione introduttiva di Azure Rights Management](../get-started/infoprotect-quick-start-tutorial.md).

> [!IMPORTANT]
> Prima di eseguire questa procedura, assicurarsi di aver letto [Requisiti per Azure Information Protection](../get-started/requirements-azure-rms.md).

Scegliere la guida di orientamento per la distribuzione che sia applicabile alla propria organizzazione e che corrisponda alle [caratteristiche e funzionalità della sottoscrizione](https://www.microsoft.com/en-us/cloud-platform/azure-information-protection-features) richieste:

- [Usare le funzionalità di classificazione, assegnazione di etichette e protezione](#deployment-roadmap-for-classification-labeling-and-protection)

- [Usare solo la funzionalità di protezione dei dati](#deployment-roadmap-for-data-protection-only)


## <a name="deployment-roadmap-for-classification-labeling-and-protection"></a>Guida di orientamento per la distribuzione delle funzionalità di classificazione, assegnazione di etichette e protezione

> [!NOTE]
> Se si usa già il servizio Azure Rights Management per la protezione dei dati, è possibile ignorare molti di questi passaggi e concentrare l'attenzione sui passaggi 3 e 5.1.

### <a name="step-1-confirm-your-subscription-and-assign-user-licenses"></a>Passaggio 1: Verificare la sottoscrizione e assegnare licenze utente
Esaminare le [informazioni sulle sottoscrizioni](https://www.microsoft.com/en-us/cloud-platform/azure-information-protection-pricing) e l'[elenco delle funzionalità](https://www.microsoft.com/en-us/cloud-platform/azure-information-protection-features) nel sito Azure Information Protection per verificare che l'organizzazione abbia una sottoscrizione che include le caratteristiche e le funzionalità previste. Assegnare quindi una licenza da tale sottoscrizione a ogni utente dell'organizzazione, che potrà così classificare, etichettare e proteggere documenti e messaggi di posta elettronica.

Nota: non assegnare manualmente licenze utente dalla sottoscrizione gratuita di RMS per singoli utenti e non usare questa licenza per amministrare il servizio Azure Rights Management per la propria organizzazione. Queste licenze vengono visualizzate come **Rights Management Adhoc** (Ad-hoc per Rights Manager) nell'interfaccia di amministrazione di Office 365 e come **RIGHTSMANAGEMENT_ADHOC** quando si esegue il cmdlet di PowerShell per Azure AD, [Get-MsolAccountSku](https://msdn.microsoft.com/library/azure/dn194118.aspx). Per altre informazioni sulle modalità in cui la sottoscrizione di RMS per singoli utenti viene automaticamente concessa e assegnata agli utenti, vedere [RMS per utenti singoli e Azure Information Protection](../understand-explore/rms-for-individuals.md).


### <a name="step-2-prepare-your-tenant-account-to-use-azure-information-protection"></a>Passaggio 2: Preparare l'account tenant per l'uso di Azure Information Protection
Prima di iniziare a usare Azure Information Protection, eseguire le attività di preparazione seguenti:

- Verificare di avere account utente e gruppi in Office 365 o Azure Active Directory che verranno usati da Azure Information Protection per autenticare gli utenti dell'organizzazione. Se necessario, creare questi account e gruppi o sincronizzarli dalla directory locale. Per altre informazioni, vedere [Preparazione per Azure Information Protection](prepare.md).

### <a name="step-3-configure-and-deploy-classification-and-labeling"></a>Passaggio 3: Configurare e distribuire le funzionalità di classificazione e assegnazione di etichette

Se non si è ancora definita una strategia di classificazione, esaminare i [criteri predefiniti di Azure Information Protection](../deploy-use/configure-policy-default.md) e usarli come base per decidere quali etichette di classificazione assegnare ai dati dell'organizzazione. È possibile personalizzare questi criteri in base ai requisiti aziendali. 

Riconfigurare le etichette predefinite di Azure Information Protection per apportare le modifiche necessarie per supportare le decisioni di classificazione. Configurare i criteri per l'assegnazione manuale di etichette da parte degli utenti e scrivere istruzioni per gli utenti che consentono di decidere quale etichetta applicare e in quali casi. Per altre informazioni su come configurare i criteri di Azure Information Protection, vedere [Configurazione dei criteri di Azure Information Protection](../deploy-use/configure-policy.md).

Distribuire quindi il client di Azure Information Protection per gli utenti e fornire loro istruzioni per l'uso e indicazioni per la selezione delle etichette. Per altre informazioni sull'installazione del client, vedere [Installazione del client di Azure Information Protection](../rms-client/info-protect-client.md).

Dopo un certo periodo di tempo, quando gli utenti sono in grado di assegnare etichette a documenti e messaggi di posta elettronica, introdurre configurazioni più avanzate, ad esempio:

- Applicare un'etichetta predefinita

- Richiedere agli utenti di indicare il motivo per cui hanno scelto un'etichetta con un livello di classificazione più basso

- Imporre l'assegnazione di un'etichetta a tutti i documenti e i messaggi di posta elettronica

- Personalizzare le intestazioni, i piè di pagina o le filigrane

- Definire le condizioni per il supporto delle azioni consigliate e l'assegnazione automatica di etichette

In questa fase, non selezionare l'opzione per proteggere documenti e messaggi di posta elettronica.

### <a name="step-4-prepare-for-rights-management-data-protection"></a>Passaggio 4: Preparare per la protezione dei dati di Rights Management

Quando gli utenti sono in grado di assegnare etichette ai documenti e ai messaggi di posta elettronica, si è pronti per iniziare a introdurre la protezione dei dati più sensibili. Questa fase richiede le attività di preparazione seguenti per il servizio Azure Rights Management:

1. Decidere se si desidera che Microsoft gestisca la chiave del tenant (impostazione predefinita) oppure generare e gestire personalmente la chiave del tenant. Questo servizio è noto come BYOK (Bring Your Own Key). Si noti che attualmente non è possibile usare il servizio BYOK se si usa Exchange Online. Per altre informazioni, vedere [Pianificazione e implementazione della chiave del tenant di Azure Information Protection](plan-implement-tenant-key.md).

2. Installare il modulo di Windows PowerShell per [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] in almeno un computer dotato di accesso a Internet. È possibile eseguire questo passaggio subito o più avanti. Per altre informazioni, vedere [Installazione di Windows PowerShell per il servizio Azure Rights Management](../deploy-use/install-powershell.md).

3. Se attualmente si stanno usando i servizi Rights Management locali: eseguire una migrazione per spostare le chiavi, i modelli e gli URL sul cloud. Per altre informazioni, vedere [Migrazione da AD RMS a Information Protection](migrate-from-ad-rms-to-azure-rms.md).

4. Attivare il servizio Azure Rights Management in modo che sia possibile iniziare a proteggere documenti e messaggi di posta elettronica. Se è richiesta una distribuzione graduale, configurare i controlli di selezione utenti per limitare l'utilizzo a utenti specifici. Per ulteriori informazioni, vedere l'articolo relativo all'[attivazione di Azure Rights Management](../deploy-use/activate-service.md).

Facoltativamente, considerare la possibilità di configurare quanto segue:

-   Modelli personalizzati se i modelli di criteri predefiniti per i diritti di utilizzo non sono sufficienti per l'organizzazione. È possibile eseguire questo passaggio subito o più avanti. Per altre informazioni, vedere [Configurazione di modelli personalizzati per il servizio Azure Rights Management](../deploy-use/configure-custom-templates.md).

-   Registrazione dei dati di utilizzo per monitorare le modalità con cui l'organizzazione usa Rights Management. È possibile eseguire questo passaggio subito o più avanti. Per altre informazioni, vedere [Registrazione e analisi dell'utilizzo del servizio Azure Rights Management](../deploy-use/log-analyze-usage.md).

### <a name="step-5-configure-your-azure-information-protection-policy-applications-and-services-for-rights-management-data-protection"></a>Passaggio 5: Configurare i criteri, le applicazioni e i servizi di Azure Information Protection per la protezione dei dati di Rights Management

1. Aggiornare i criteri di Azure Information Protection per applicare la protezione dei dati
    
    Modificare i criteri di Azure Information Protection in modo da usare una o più etichette per applicare la protezione di Rights Management. Per altre informazioni, vedere [Come configurare un'etichetta per applicare la protezione di Rights Management](../deploy-use/configure-policy-protection.md).
    
    Si noti che in Outlook gli utenti possono applicare etichette per attivare la protezione di Rights Management anche se Exchange non è configurato per i servizi Information Rights Management (IRM). Tuttavia, fino a quando Exchange non sarà configurato per IRM, l'organizzazione non potrà usufruire della funzionalità completa della protezione di Rights Management di Azure con Exchange. Questa configurazione aggiuntiva è inclusa nel passaggio 3 per Exchange Online e nel passaggio 6 per Exchange locale. 

2. Distribuire l'applicazione Rights Management sharing
    
    Installare l'applicazione Rights Management sharing per gli utenti affinché possano condividere in modo sicuro i documenti tramite posta elettronica, proteggere i file locali e tenere traccia dei documenti condivisi protetti. Fornire agli utenti istruzioni per l'uso di questa applicazione. Per altre informazioni, vedere [Applicazione Rights Management sharing per Windows](../rms-client/sharing-app-windows.md).

3. Configurare le applicazioni e i servizi di Office per IRM
    
    Configurare le applicazioni e i servizi di Office per le funzionalità di IRM (Information Rights Management) in SharePoint Online o Exchange Online. Per ulteriori informazioni, vedere [Configurazione delle applicazioni per Azure Rights Management](../deploy-use/configure-applications.md).

4. Configurare la funzionalità relativa agli utenti con privilegi avanzati per il ripristino dei dati
    
    Se sono presenti servizi IT che prevedono l'analisi di file che verranno protetti da Azure Rights Management, ad esempio soluzioni di prevenzione per la perdita di dati, gateway con crittografia del contenuto e prodotti antimalware, configurare gli account di tali servizi come utenti con privilegi avanzati per Azure Rights Management. Per ulteriori informazioni, vedere [Configurazione degli utenti con privilegi avanzati per Rights Management di Azure e servizi di individuazione o ripristino dei dati](../deploy-use/configure-super-users.md).

5. Proteggere i file in blocco 
    
    Per poter proteggere o rimuovere la protezione in blocco di tutti i tipi di file, installare lo strumento di protezione RMS che usa il modulo PowerShell di protezione di RMS. Per altre informazioni, vedere [Cmdlet di protezione RMS](https://msdn.microsoft.com/library/mt433195.aspx).

6. Distribuire il connettore per i server locali
    
    Se si prevede di usare servizi locali con il servizio Azure Rights Management, installare e configurare il connettore di Rights Management. Per ulteriori informazioni, vedere [Distribuzione del connettore di Azure Rights Management](../deploy-use/deploy-rms-connector.md).

### <a name="step-4-use-and-monitor-your-data-protection-solutions"></a>Passaggio 4: Usare e monitorare le soluzioni di protezione dei dati
È ora possibile proteggere i dati e registrare come viene usato Rights Management nella propria società. Per altre informazioni utili per questa fase di distribuzione, vedere [Consentire agli utenti di proteggere i file mediante il servizio Azure Rights Management](../deploy-use/help-users.md) e [Registrazione e analisi dell'utilizzo del servizio Azure Rights Management](../deploy-use/log-analyze-usage.md).

Se si vuole proteggere automaticamente i file usando Infrastruttura di classificazione file in un file server basato su Windows, vedere [Protezione RMS con Infrastruttura di classificazione file per Windows Server](../rms-client/configure-fci.md).

### <a name="step-5-administer-the-rights-management-service-for-your-tenant-account-as-needed"></a>Passaggio 5: Amministrare il servizio Rights Management per l'account tenant in base alle esigenze
Quando si inizia a usare il servizio Azure Rights Management, è possibile avvalersi di Windows PowerShell per eseguire tramite script o automatizzare le modifiche di carattere amministrativo. Per altre informazioni, vedere [Amministrazione del servizio Azure Rights Management mediante Windows PowerShell](../deploy-use/administer-powershell.md).


## <a name="deployment-roadmap-for-data-protection-only"></a>Guida di orientamento per la distribuzione della sola funzionalità di protezione

### <a name="step-1-confirm-that-you-have-a-subscription-that-includes-azure-rights-management"></a>Passaggio 1: Confermare di avere una sottoscrizione che include Azure Rights Management
Esaminare le [informazioni sulle sottoscrizioni](https://www.microsoft.com/en-us/cloud-platform/azure-information-protection-pricing) e l'[elenco delle funzionalità](https://www.microsoft.com/en-us/cloud-platform/azure-information-protection-features) nel sito Azure Information Protection per verificare che l'organizzazione abbia una sottoscrizione che include le caratteristiche e le funzionalità previste. Assegnare quindi una licenza da tale sottoscrizione a ogni utente dell'organizzazione, che potrà così proteggere documenti e messaggi di posta elettronica usando il servizio Azure Rights Management.

Nota: non assegnare manualmente licenze utente dalla sottoscrizione gratuita di RMS per singoli utenti e non usare questa licenza per amministrare il servizio Azure Rights Management per la propria organizzazione. Queste licenze vengono visualizzate come **Rights Management Adhoc** (Ad-hoc per Rights Manager) nell'interfaccia di amministrazione di Office 365 e come **RIGHTSMANAGEMENT_ADHOC** quando si esegue il cmdlet di PowerShell per Azure AD, [Get-MsolAccountSku](https://msdn.microsoft.com/library/azure/dn194118.aspx). Per altre informazioni sulle modalità in cui la sottoscrizione di RMS per singoli utenti viene automaticamente concessa e assegnata agli utenti, vedere [RMS per utenti singoli e Azure Information Protection](../understand-explore/rms-for-individuals.md).


### <a name="step-2-prepare-your-tenant-account-to-use-the-azure-rights-management-service"></a>Passaggio 2: Preparare l'account tenant per l'uso del servizio Azure Rights Management
Prima di iniziare a usare [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)], effettuare la seguente preparazione:

1.  Verificare che il tenant di Office 365 contenga gli account utente e i gruppi che verranno usati da Azure Information Protection per autenticare gli utenti dell'organizzazione. Se necessario, creare questi account e gruppi o sincronizzarli dalla directory locale. Per ulteriori informazioni, vedere [Preparazione per Azure Rights Management](prepare.md).

2. Decidere se si desidera che Microsoft gestisca la chiave del tenant (impostazione predefinita) oppure generare e gestire personalmente la chiave del tenant. Questo servizio è noto come BYOK (Bring Your Own Key). Si noti che attualmente non è possibile usare il servizio BYOK se si usa Exchange Online. Per altre informazioni, vedere [Pianificazione e implementazione della chiave del tenant di Azure Information Protection](plan-implement-tenant-key.md).

3. Installare il modulo di Windows PowerShell per [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] in almeno un computer dotato di accesso a Internet. È possibile eseguire questo passaggio subito o più avanti. Per ulteriori informazioni, vedere [Installazione di Windows PowerShell per Azure Rights Management](../deploy-use/install-powershell.md).

4. Se attualmente si stanno usando i servizi Rights Management locali: eseguire una migrazione per spostare le chiavi, i modelli e gli URL sul cloud. Per altre informazioni, vedere [Migrazione da AD RMS ad Azure Information Protection](migrate-from-ad-rms-to-azure-rms.md).

5. Attivare Rights Management in modo da poter iniziare a usare il servizio. Se è richiesta una distribuzione graduale, configurare i controlli di selezione utenti per limitare l'utilizzo a utenti specifici. Per ulteriori informazioni, vedere l'articolo relativo all'[attivazione di Azure Rights Management](../deploy-use/activate-service.md).

Facoltativamente, considerare la possibilità di configurare quanto segue:

-   Modelli personalizzati se i modelli di criteri predefiniti per i diritti di utilizzo non sono sufficienti per l'organizzazione. È possibile eseguire questo passaggio subito o più avanti. Per altre informazioni, vedere [Configurazione di modelli personalizzati per il servizio Azure Rights Management](../deploy-use/configure-custom-templates.md).

-   Registrazione dei dati di utilizzo per monitorare le modalità con cui l'organizzazione usa Rights Management. È possibile eseguire questo passaggio subito o più avanti. Per altre informazioni, vedere [Registrazione e analisi dell'utilizzo del servizio Azure Rights Management](../deploy-use/log-analyze-usage.md).

### <a name="step-3-configure-your-applications-and-services-for-rights-management"></a>Passaggio 3: Configurare le applicazioni e i servizi per Rights Management

1. Distribuire l'applicazione Rights Management sharing
    
    Installare l'applicazione Rights Management sharing per gli utenti affinché possano condividere in modo sicuro i documenti tramite posta elettronica, proteggere i file locali e tenere traccia dei documenti condivisi protetti. Fornire agli utenti istruzioni per l'uso di questa applicazione. Per altre informazioni, vedere [Applicazione Rights Management sharing per Windows](../rms-client/sharing-app-windows.md).

2. Configurare le applicazioni e i servizi di Office per IRM
    
    Configurare le applicazioni e i servizi di Office per le funzionalità di IRM (Information Rights Management) in SharePoint Online o Exchange Online. Per ulteriori informazioni, vedere [Configurazione delle applicazioni per Azure Rights Management](../deploy-use/configure-applications.md).

3. Configurare la funzionalità relativa agli utenti con privilegi avanzati per il ripristino dei dati
    
    Se sono presenti servizi IT che prevedono l'analisi di file che verranno protetti da Azure Rights Management, ad esempio soluzioni di prevenzione per la perdita di dati, gateway con crittografia del contenuto e prodotti antimalware, configurare gli account di tali servizi come utenti con privilegi avanzati per Azure Rights Management. Per ulteriori informazioni, vedere [Configurazione degli utenti con privilegi avanzati per Rights Management di Azure e servizi di individuazione o ripristino dei dati](../deploy-use/configure-super-users.md).

4. Proteggere i file in blocco 
    
    Per poter proteggere o rimuovere la protezione in blocco di tutti i tipi di file, installare lo strumento di protezione RMS che usa il modulo PowerShell di protezione di RMS. Per altre informazioni, vedere [Cmdlet di protezione RMS](https://msdn.microsoft.com/library/mt433195.aspx).

5. Distribuire il connettore per i server locali
    
    Se si prevede di usare servizi locali con il servizio Azure Rights Management, installare e configurare il connettore di Rights Management. Per ulteriori informazioni, vedere [Distribuzione del connettore di Azure Rights Management](../deploy-use/deploy-rms-connector.md).


### <a name="step-4-use-and-monitor-your-data-protection-solutions"></a>Passaggio 4: Usare e monitorare le soluzioni di protezione dei dati
È ora possibile proteggere i dati e registrare come viene usato Rights Management nella propria società. Per altre informazioni utili per questa fase di distribuzione, vedere [Consentire agli utenti di proteggere i file mediante il servizio Azure Rights Management](../deploy-use/help-users.md) e [Registrazione e analisi dell'utilizzo del servizio Azure Rights Management](../deploy-use/log-analyze-usage.md).

Se si vuole proteggere automaticamente i file usando Infrastruttura di classificazione file in un file server basato su Windows, vedere [Protezione RMS con Infrastruttura di classificazione file per Windows Server](../rms-client/configure-fci.md).

### <a name="step-5-administer-the-rights-management-service-for-your-tenant-account-as-needed"></a>Passaggio 5: Amministrare il servizio Rights Management per l'account tenant in base alle esigenze
Quando si inizia a usare il servizio Azure Rights Management, è possibile avvalersi di Windows PowerShell per eseguire tramite script o automatizzare le modifiche di carattere amministrativo. Per altre informazioni, vedere [Amministrazione del servizio Azure Rights Management mediante Windows PowerShell](../deploy-use/administer-powershell.md).





<!--HONumber=Nov16_HO4-->


