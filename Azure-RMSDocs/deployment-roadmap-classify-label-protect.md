---
title: Distribuire Azure Information Protection (AIP) per la classificazione, l'assegnazione di etichette e la protezione
description: Usare questa procedura per preparare, implementare e gestire Azure Information Protection (AIP) per l'organizzazione, quando si vuole classificare, etichettare e proteggere i dati.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 11/11/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 086600c2-c5d8-47ec-a4c0-c782e1797486
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 6612500a86f8a84c5f5762e91933c3f9cf743678
ms.sourcegitcommit: f6d536b6a3b5e14e24f0b9e58d17a3136810213b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/26/2021
ms.locfileid: "98809532"
---
# <a name="aip-deployment-roadmap-for-classification-labeling-and-protection"></a>Roadmap per la distribuzione di AIP per la classificazione, l'assegnazione di etichette e la protezione

>***Si applica a**: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*
>
>***Rilevante per**: [Client di etichettatura unificata e client classico di AIP](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

>[!NOTE] 
> Per offrire un'esperienza per i clienti unificata e semplificata, il **client classico di Azure Information Protection** e **Gestione etichette** nel portale di Azure saranno **deprecati** a partire dal **31 marzo 2021**. In questo intervallo di tempo tutti i clienti correnti di Azure Information Protection possono passare alla soluzione di etichettatura unificata usando la piattaforma di etichettatura unificata di Microsoft Information Protection. Altre informazioni nell'[avviso ufficiale sulla deprecazione](https://aka.ms/aipclassicsunset).

Usare i passaggi seguenti come consigli per la preparazione, l'implementazione e la gestione di Azure Information Protection per la propria organizzazione, quando si vogliono classificare, etichettare e proteggere i dati.

Questa roadmap è consigliata per tutti i clienti con una sottoscrizione di supporto. Funzionalità aggiuntive includono l'individuazione di informazioni riservate e l'assegnazione di etichette a documenti e messaggi di posta elettronica per la classificazione 

Le etichette possono anche applicare la protezione, semplificando questo passaggio per gli utenti. 

> [!TIP]
> In alternativa, è possibile cercare uno degli articoli seguenti:
> - [Guida di orientamento per AIP solo per la protezione dei dati](deployment-roadmap-protect-only.md)
> - [Guide pratiche per scenari comuni che usano Azure Information Protection](how-to-guides.md)
> - [Roadmap della versione Azure Information Protection](information-support.md#information-about-new-releases-and-updates)

## <a name="deployment-process"></a>Processo di distribuzione

Eseguire la procedura seguente:

1. [Verificare la sottoscrizione e assegnare licenze utente](#confirm-your-subscription-and-assign-user-licenses)
1. [Preparare il tenant per l'uso di Azure Information Protection](#prepare-your-tenant-to-use-azure-information-protection)
1. [Configurare e distribuire le funzionalità di classificazione e assegnazione di etichette](#configure-and-deploy-classification-and-labeling)
1. [Prepararsi per la protezione dei dati](#prepare-for-data-protection)
1. [Configurare etichette e impostazioni, applicazioni e servizi per la protezione dei dati](#configure-labels-and-settings-applications-and-services-for-data-protection)
1. [Usare e monitorare le soluzioni di protezione dei dati](#use-and-monitor-your-data-protection-solutions)
1. [Amministrare il servizio di protezione per l'account tenant in base alle esigenze](#administer-the-protection-service-for-your-tenant-account-as-needed)

> [!TIP]
> Se si usano già le funzionalità di Azure Information Protection, È possibile ignorare molti di questi passaggi e concentrarsi sui passaggi [3](#configure-and-deploy-classification-and-labeling) e [5,1](#configure-labels-and-settings-applications-and-services-for-data-protection).

## <a name="confirm-your-subscription-and-assign-user-licenses"></a>Verificare la sottoscrizione e assegnare licenze utente

Verificare che l'organizzazione disponga di una sottoscrizione che includa le funzionalità e le funzionalità che si prevede. Questi dettagli sono disponibili nella pagina relativa ai [prezzi Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection) .

Assegnare quindi le licenze da tale sottoscrizione a ogni utente dell'organizzazione, che potrà così classificare, etichettare e proteggere documenti e messaggi di posta elettronica.

> [!IMPORTANT]
> Non assegnare manualmente le licenze utente dalla sottoscrizione gratuita di RMS per utenti singoli e non usare questa licenza per amministrare il servizio Rights Management di Azure per l'organizzazione. 
>
> Queste licenze vengono visualizzate come **Rights Management Adhoc** (Ad-hoc per Rights Manager) nell'interfaccia di amministrazione di Microsoft 365 e come **RIGHTSMANAGEMENT_ADHOC** quando si esegue il cmdlet di PowerShell per Azure AD, [Get-MsolAccountSku](/previous-versions/azure/dn194118(v=azure.100)). 
>
> Per ulteriori informazioni, vedere [RMS per utenti singoli e Azure Information Protection](./rms-for-individuals.md).
> 
## <a name="prepare-your-tenant-to-use-azure-information-protection"></a>Preparare il tenant per l'uso di Azure Information Protection

Prima di iniziare a usare Azure Information Protection, assicurarsi di disporre di account utente e gruppi in Microsoft 365 o Azure Active Directory che AIP possa usare per autenticare e autorizzare gli utenti.

Se necessario, creare questi account e gruppi o sincronizzarli dalla directory locale. 

Per altre informazioni, vedere [Preparazione di utenti e gruppi per Azure Information Protection](prepare.md).

## <a name="configure-and-deploy-classification-and-labeling"></a>Configurare e distribuire le funzionalità di classificazione e assegnazione di etichette

Eseguire la procedura seguente:

1. **Analizza i file (facoltativo ma consigliato)**

    [Distribuire il client di Azure Information Protection](quickstart-deploy-client.md), quindi [installare](tutorial-install-scanner.md) ed [eseguire lo scanner](tutorial-scan-networks-and-content.md) per individuare le informazioni riservate presenti negli archivi dati locali. 

    Le informazioni trovate dallo scanner possono semplificare la tassonomia di classificazione, oltre a fornire informazioni utili sulle etichette richieste e sui file che necessitano di protezione.

    La modalità di **individuazione** dello scanner non richiede alcuna configurazione di etichetta o tassonomia ed è quindi adatta in questa fase iniziale della distribuzione. È anche possibile usare questa configurazione dello scanner in parallelo con i passaggi di distribuzione seguenti, fino a quando non si configurano le etichette consigliate o automatiche.

1. **Personalizzare i criteri di AIP predefiniti**.

    Se non si dispone ancora di una strategia di classificazione, usare un criterio predefinito come base per determinare quali etichette saranno necessarie per i dati. Personalizzare queste etichette secondo necessità per soddisfare le proprie esigenze.

    Ad esempio, è possibile riconfigurare le etichette con i dettagli seguenti:

    - Assicurarsi che le etichette siano in grado di supportare le decisioni di classificazione.
    - Configurare i criteri per l'etichettatura manuale da parte degli utenti
    - Scrivere le linee guida per gli utenti per spiegare quale etichetta applicare a ogni scenario.
    - Se il criterio predefinito è stato creato con etichette che applicano automaticamente la protezione, potrebbe essere necessario rimuovere temporaneamente le impostazioni di protezione o disabilitare l'etichetta durante il test delle impostazioni. 

    Le etichette di riservatezza e i criteri di etichettatura per il client di etichetta unificata sono configurati nel centro sicurezza Microsoft 365, nel centro di conformità Microsoft 365 o nel Microsoft 365 Security & Compliance Center. Per ulteriori informazioni, vedere informazioni [sulle etichette di riservatezza](/microsoft-365/compliance/sensitivity-labels).

1. **Distribuire il client per gli utenti**

    Una volta configurati i criteri, distribuire il client Azure Information Protection per gli utenti. Fornire formazione per gli utenti e istruzioni specifiche per la selezione delle etichette. 

    Per ulteriori informazioni, vedere la [Guida dell'amministratore client Unified Labeling](./rms-client/clientv2-admin-guide.md).

1. **Introduzione a configurazioni più avanzate**

    Attendere che gli utenti diventino più comodi con le etichette sui documenti e i messaggi di posta elettronica. Quando si è pronti, introdurre configurazioni avanzate, ad esempio:

    - Applicazione delle etichette predefinite
    - Chiedere agli utenti di giustificare se hanno scelto un'etichetta con un livello di classificazione inferiore o rimuovere un'etichetta
    - Invio di un'etichetta a tutti i documenti e i messaggi di posta elettronica
    - Personalizzazione di intestazioni, piè di pagina o filigrane
    - Etichettatura consigliata e automatica

    Per altre informazioni, vedere [Guida dell'amministratore: configurazioni personalizzate](rms-client/client-admin-guide-customizations.md).
     
    > [!TIP]
    > Se sono state configurate etichette per l'etichettatura automatica, eseguire di nuovo lo [scanner di Azure Information Protection](deploy-aip-scanner-manage.md) negli archivi dati locali in modalità di individuazione e in base ai criteri. 
    > 
    > L'esecuzione dello scanner in modalità di individuazione indica le etichette da applicare ai file, che consente di ottimizzare la configurazione dell'etichetta e prepara la classificazione e la protezione dei file in blocco. 
    > 

## <a name="prepare-for-data-protection"></a>Prepararsi per la protezione dei dati

Introduce la protezione dei dati più sensibili quando gli utenti diventano i documenti e i messaggi di posta elettronica.

Per preparare la protezione dei dati, seguire questa procedura:

1. **Determinare come si vuole gestire la chiave del tenant**.

    Decidere se si desidera che Microsoft gestisca la chiave del tenant (impostazione predefinita) oppure generare e gestire personalmente la chiave del tenant. Questo servizio è noto come BYOK (Bring Your Own Key). 
 
    Per altre informazioni e opzioni per la protezione locale aggiuntiva, vedere [pianificazione e implementazione della chiave del tenant Azure Information Protection](plan-implement-tenant-key.md).

1. **Installare PowerShell per AIP**.

    Installare il modulo PowerShell per **AIPService** in almeno un computer dotato di accesso a Internet. È possibile eseguire questo passaggio subito o più avanti. 

    Per altre informazioni, vedere [installazione del modulo PowerShell AIPService](./install-powershell.md).

1. **Solo ad RMS**: eseguire la migrazione delle chiavi, dei modelli e degli URL nel cloud.

    Se attualmente si usa AD RMS, eseguire una migrazione per spostare le chiavi, i modelli e gli URL nel cloud. 
    
    Per altre informazioni, vedere [Migrazione da AD RMS a Information Protection](migrate-from-ad-rms-to-azure-rms.md).

1. **Attivare la protezione**.

    Verificare che il servizio di protezione sia attivato in modo che sia possibile iniziare a proteggere documenti e messaggi di posta elettronica. Se si esegue la distribuzione in più fasi, configurare i controlli di onboarding degli utenti per limitare la capacità degli utenti di applicare la protezione. 

    Per altre informazioni, vedere [Attivazione del servizio di protezione da Azure Information Protection](./activate-service.md).

1. **Prendere in considerazione la registrazione dell'utilizzo (facoltativo)**.

    Prendere in considerazione la registrazione dell'utilizzo per monitorare il modo in cui l'organizzazione usa il servizio di protezione. È possibile eseguire questo passaggio subito o più avanti. 

    Per ulteriori informazioni, vedere [registrazione e analisi dell'utilizzo della protezione da Azure Information Protection](./log-analyze-usage.md).

## <a name="configure-labels-and-settings-applications-and-services-for-data-protection"></a>Configurare etichette e impostazioni, applicazioni e servizi per la protezione dei dati

Eseguire la procedura seguente:

1. **Aggiornare le etichette per applicare la protezione**
    
    Per altre informazioni, vedere [Limitare l'accesso al contenuto usando la crittografia nelle etichette di riservatezza](/microsoft-365/compliance/encryption-sensitivity-labels).

    > [!IMPORTANT]
    > Gli utenti possono applicare le etichette in Outlook che applicano la protezione Rights Management anche se Exchange non è configurato per Information Rights Management (IRM). 
    > 
    > Tuttavia, fino a quando Exchange non viene configurato per IRM o [Microsoft 365 crittografia dei messaggi con nuove funzionalità](https://support.office.com/article/7ff0c040-b25c-4378-9904-b1b50210d00e), l'organizzazione non otterrà la funzionalità completa dell'uso della protezione Rights Management di Azure con Exchange. Questa configurazione aggiuntiva è inclusa nell'elenco seguente, 2 per Exchange Online e 5 per Exchange locale. 
    > 
    
1. **Configurare le applicazioni e i servizi di Office**
    
    Configurare le applicazioni e i servizi di Office per le funzionalità IRM (Information Rights Management) in Microsoft SharePoint o Exchange Online. 

    Per altre informazioni, vedere [configurazione di applicazioni per Azure Rights Management](configure-applications.md).

1. **Configurare la funzionalità relativa agli utenti con privilegi avanzati per il ripristino dei dati**
    
    Se sono presenti servizi IT che prevedono l'analisi dei file che verranno protetti da Azure Information Protection, ad esempio soluzioni di prevenzione della perdita di dati, gateway con crittografia del contenuto e prodotti antimalware, configurare gli account di tali servizi come utenti con privilegi avanzati per Azure Rights Management. 

    Per ulteriori informazioni, vedere [configurazione degli utenti con privilegi avanzati per Azure Information Protection e servizi di individuazione o ripristino dei dati](./configure-super-users.md).

1. **Classificare e proteggere i file esistenti in blocco**
    
    Per gli archivi dati locali, eseguire ora lo [scanner di Azure Information Protection](deploy-aip-scanner.md) in modalità di imposizione in modo che i file vengano etichettati automaticamente.
    
    Per i file nei PC, usare i cmdlet di PowerShell per classificare e proteggere i file. Per altre informazioni, vedere [uso di PowerShell con Azure Information Protection Unified Labeling client](./rms-client/clientv2-admin-guide-powershell.md).

    Per gli archivi dati basati su cloud, usare [Azure Cloud App Security](/cloud-app-security). 

    > [!TIP]
    > Sebbene la classificazione e la protezione dei file esistenti in blocco non sia uno dei principali casi d'uso per cloud app Security, le [soluzioni alternative documentate](/cloud-app-security/azip-integration#enable-azure-information-protection) possono aiutare a ottenere i file classificati e protetti.

6. **Distribuire il connettore per le raccolte protette con IRM in SharePoint Server e i messaggi protetti con IRM per Exchange locale**
    
    Se si dispone di SharePoint ed Exchange locale e si vogliono usare le funzionalità di Information Rights Management (IRM), installare e configurare il connettore di Rights Management. 

    Per ulteriori informazioni, vedere [Distribuzione del connettore di Azure Rights Management](./deploy-rms-connector.md).

## <a name="use-and-monitor-your-data-protection-solutions"></a>Usare e monitorare le soluzioni di protezione dei dati

A questo punto è possibile monitorare il modo in cui l'organizzazione usa le etichette configurate e confermare che si stanno proteggendo le informazioni riservate. 

Per ulteriori informazioni, vedere i seguenti argomenti:

- [Reporting centrale per Azure Information Protection](reports-aip.md) al momento in anteprima
- [Registrazione e analisi dell'utilizzo della protezione da Azure Information Protection](./log-analyze-usage.md)

## <a name="administer-the-protection-service-for-your-tenant-account-as-needed"></a>Amministrare il servizio di protezione per l'account tenant in base alle esigenze

Quando si inizia a usare il servizio di protezione, PowerShell può essere utile per facilitare l'esecuzione di script o l'automazione di modifiche di carattere amministrativo. Per alcune delle configurazioni avanzate potrebbe essere richiesto anche PowerShell. 

Per altre informazioni, vedere [amministrazione della protezione da Azure Information Protection tramite PowerShell](./administer-powershell.md).

## <a name="references-for-classic-client-environments"></a>Riferimenti per ambienti client classici

**Pertinente per**: solo client di AIP classico

Se si usa il client classico, usare i riferimenti seguenti anziché quelli collegati sopra:

- **Distribuire ed eseguire lo scanner** fornito con il client classico. Per altre informazioni, vedere [che cos'è il Azure Information Protection scanner classico?](deploy-aip-scanner-classic.md)

- **Configurare i criteri nell'portale di Azure.** Per ulteriori informazioni, vedere [Configuring Azure Information Protection Policy](./configure-policy.md) e [How to Configure an Label for Rights Management Protection](./configure-policy-protection.md).

- **Distribuire il client per gli utenti** usando la [Guida dell'amministratore client classico](./rms-client/client-admin-guide.md) e le [istruzioni di configurazione personalizzate per il client classico](rms-client/client-admin-guide-customizations.md).

- **Istruzioni di PowerShell**: [uso di PowerShell con il client di Azure Information Protection](./rms-client/client-admin-guide-powershell.md)

- **Monitoraggio locale**: [registrazione dell'utilizzo locale con monitoraggio eventi di Windows](./rms-client/client-admin-guide-files-and-logging.md#usage-logging-for-the-azure-information-protection-classic-client)

> [!TIP]
> Potrebbe anche essere interessante la Guida di [orientamento per la distribuzione di Azure Information Protection solo per la protezione](deployment-roadmap-protect-only.md), supportata solo per il client classico.

## <a name="next-steps"></a>Passaggi successivi

Quando si distribuisce Azure Information Protection, potrebbe risultare utile consultare le [domande frequenti](faqs.md), i [problemi noti](known-issues.md)e la pagina [informazioni e supporto](information-support.md) per ulteriori risorse.