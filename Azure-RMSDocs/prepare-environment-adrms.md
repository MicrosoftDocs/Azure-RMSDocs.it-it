---
title: Preparare l'ambiente per Azure RMS e AD RMS
description: Linee guida per gli amministratori se Azure Rights Management con AD RMS distribuito.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 11/30/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 11ffa730-c5dc-4b6b-9c1e-c58eff8aafc2
ms.subservice: azurerms
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 45423a4ac7fa81d5171e260d14170bae07428ad9
ms.sourcegitcommit: 8a141858e494dd1d3e48831e6cd5a5be48ac00d2
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2020
ms.locfileid: "97386373"
---
# <a name="prepare-the-environment-for-azure-rights-management-when-you-have-ad-rms"></a>Preparare l'ambiente per Azure Rights Management quando si dispone di AD RMS

>***Si applica a**: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*
>
>***Pertinente per**: [Azure Information Protection Unified Labeling client e il client classico per Windows](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

> [!IMPORTANT]
> Linee guida per l'uso di Active Directory Rights Management Services (AD RMS)

Se il servizio Active Rights Management è attivato e si usa anche AD RMS, la combinazione dei due servizi non è compatibile. Se non vengono eseguiti altri passaggi, è possibile che all'avvio alcuni computer usino automaticamente il servizio Azure Rights Management e si connettano anche al cluster AD RMS. Questo scenario non è supportato e restituisce risultati non prevedibili, quindi è importante eseguire alcuni passaggi aggiuntivi. 

**Per verificare se sono state distribuite ad RMS**:

1. Nonostante sia facoltativo, la maggior parte delle distribuzioni di AD RMS pubblica il punto di connessione del servizio in Active Directory in modo che i computer del dominio possano individuare il cluster AD RMS. 
    
    Usare ADSI Edit per verificare se è stato pubblicato un punto di connessione del servizio in Active Directory: `CN=Configuration [server name], CN=Services, CN=RightsManagementServices, CN=SCP`

2. Se non si usa un punto di connessione del servizio, i computer Windows che si connettono a un cluster AD RMS devono essere configurati per l'individuazione del servizio lato client o il reindirizzamento delle licenze usando il Registro di sistema di Windows: `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSIPC\ServiceLocation` o `HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\MSIPC\ServiceLocation`
    
    Per altre informazioni su queste configurazioni del Registro di sistema, vedere [Abilitazione dell'individuazione del servizio sul lato client usando il Registro di sistema di Windows](./rms-client/client-deployment-notes.md#enabling-client-side-service-discovery-by-using-the-windows-registry) e [Reindirizzamento del traffico del server delle licenze](./rms-client/client-deployment-notes.md#redirecting-licensing-server-traffic).   

Se AD RMS viene distribuito per l'organizzazione, considerare se è possibile eseguire la migrazione ad Azure Information Protection. Azure Information Protection presenta numerosi vantaggi rispetto ad AD RMS, Ad esempio, un migliore supporto per i dispositivi mobili e l'integrazione con Microsoft 365 Services, nonché con Exchange Server e SharePoint Server. Per altre informazioni, vedere [Confronto tra Azure Information Protection e AD RMS](compare-on-premise.md).

Quando si esegue la migrazione a Azure Information Protection, non si perderà l'accesso al contenuto protetto in precedenza e non sarà necessario rimuovere o riproteggere il contenuto. I documenti e i messaggi di posta elettronica protetti da AD RMS possono comunque essere aperti anche dopo aver effettuato il deprovisioning AD RMS.

Che si decida di eseguire la migrazione ad Azure Information Protection o di accettare le limitazioni nell'uso della distribuzione corrente di AD RMS, è prima di tutto necessario assicurarsi che il servizio Azure Rights Management sia disattivato. Per istruzioni, seguire i passaggi per lo scenario appropriato:

- [La sottoscrizione che include Azure Rights Management è stata acquistata durante il mese di febbraio 2018 o successivamente](#your-subscription-was-purchased-during-or-after-february-2018)

- [La sottoscrizione è stata acquistata prima o durante il mese di febbraio 2018 ed è disponibile Exchange Online](#your-subscription-was-purchased-before-or-during-february-2018-and-you-have-exchange-online)

- [Quando si configura il criterio di Azure Information Protection nel portale di Azure, viene visualizzata un'opzione che consente di attivare la protezione](#you-see-an-option-to-activate-protection-when-you-configure-azure-information-protection)


## <a name="your-subscription-was-purchased-during-or-after-february-2018"></a>La sottoscrizione è stata acquistata nel mese di febbraio 2018 o successivamente

Verso la fine di febbraio 2018, le nuove sottoscrizioni che includono Azure Information Protection attivano il servizio di Azure Rights Management per impostazione predefinita. Se il servizio viene attivato automaticamente e si usa anche Active Directory Rights Management Services (AD RMS), questa combinazione non è compatibile, quindi è importante disattivare il servizio Azure Rights Management quanto prima. 

### <a name="step-1-deactivate-azure-rights-management"></a>Passaggio 1: Disattivare Azure Rights Management
Per disattivare Azure Rights Management, usare una delle procedure descritte di seguito.

> [!TIP]
> Per disattivare il servizio Rights Management di Azure, è anche possibile usare il cmdlet di Windows PowerShell [Disable-AipService](/powershell/module/aipservice/disable-aipservice).

#### <a name="to-deactivate-rights-management-from-the-microsoft-365-admin-center"></a>Per disattivare Rights Management dall'interfaccia di amministrazione di Microsoft 365

1. Passare alla [pagina Rights Management](https://account.activedirectory.windowsazure.com/RmsOnline/Manage.aspx) per Microsoft 365 Administrators.
    
    Se viene richiesto di eseguire l'accesso, usare un account che sia un amministratore globale per Microsoft 365.

2. Nella pagina **rights management** fare clic su **disattiva**.

3.  Quando viene visualizzata la richiesta **Disattivare Rights Management?** fare clic su **Disattiva**.

Verrà visualizzato il messaggio che indica che **Rights Management non è attivato** con l'opzione per l'attivazione.

#### <a name="to-deactivate-rights-management-from-the-azure-portal"></a>Per disattivare Rights Management dal portale di Azure

1. Aprire una nuova finestra del browser e accedere al [portale di Azure](configure-policy.md#signing-in-to-the-azure-portal), se questa operazione non è già stata eseguita. Quindi passare al riquadro **Azure Information Protection**.
    
    Ad esempio, nella casella di ricerca di risorse, servizi e documentazione: iniziare a digitare **Informazioni** e selezionare **Azure Information Protection**.
    
    Se non è stato eseguito l'accesso al riquadro Azure Information Protection prima, vedere i [passaggi aggiuntivi](configure-policy.md#to-access-the-azure-information-protection-pane-for-the-first-time) monouso per aggiungere questo riquadro al portale.

2. Scegliere **Attivazione della protezione** dalle opzioni del menu. 

3.  Nel riquadro **attivazione protezione Azure Information Protection** selezionare **Disattiva**. Selezionare **Sì** per confermare la scelta.

Sulla barra delle informazioni verrà visualizzato **Disattivazione completata** mentre **Disattiva** è stato sostituito da **Attiva**. 

### <a name="step-2-start-planning-for-migration"></a>Passaggio 2: Iniziare la pianificazione della migrazione

Per informazioni, vedere la guida alla migrazione: [Migrazione da AD RMS ad Azure Information Protection](migrate-from-ad-rms-to-azure-rms.md)


## <a name="your-subscription-was-purchased-before-or-during-february-2018-and-you-have-exchange-online"></a>La sottoscrizione è stata acquistata prima o durante il mese di febbraio 2018 ed è disponibile Exchange Online

Microsoft sta iniziando ad attivare il servizio Azure Rights Management per le sottoscrizioni che includono Azure Rights Management o Azure Information Protection e i tenant che usano Exchange Online. Per questi tenant, l'implementazione dell'attivazione automatica inizierà l'1 agosto 2018.

Se il servizio viene attivato automaticamente e si usa anche AD RMS, questa combinazione non è compatibile, quindi è importante che il tenant venga rifiutato esplicitamente dall'aggiornamento automatico del servizio. 

### <a name="step-1-opt-out-from-the-automatic-service-update"></a>Passaggio 1: Rifiutare esplicitamente l'aggiornamento automatico del servizio

Usare il comando di PowerShell per Exchange Online [Set-IRMConfiguration](/powershell/module/exchange/encryption-and-certificates/set-irmconfiguration) seguente:`Set-IRMConfiguration -AutomaticServiceUpdateEnabled $false`

[Altre informazioni](https://support.office.com/article/protection-features-in-azure-information-protection-rolling-out-to-existing-office-365-tenants-7ad6f58e-65d7-4c82-8e65-0b773666634d) 

### <a name="step-2-start-planning-for-migration"></a>Passaggio 2: Iniziare la pianificazione della migrazione

Per informazioni, vedere la guida alla migrazione: [Migrazione da AD RMS ad Azure Information Protection](migrate-from-ad-rms-to-azure-rms.md)


## <a name="you-see-an-option-to-activate-protection-when-you-configure-azure-information-protection"></a>Viene visualizzata un'opzione per attivare la protezione quando si configura Azure Information Protection

Il riquadro **attivazione protezione Azure Information Protection** ha un'opzione per attivare il servizio Azure Rights Management.  

Se si usa anche AD RMS, non selezionare l'opzione **Attiva**. Quando il servizio Azure Rights Management non è attivato, è comunque possibile usare Azure Information Protection per etichette che applicano solo una classificazione. Vengono creati criteri predefiniti speciali che non includono la protezione dati e le opzioni di configurazione rimangono non disponibili fino a quando il servizio Azure Rights Management è attivato.

### <a name="step-1-configure-your-azure-information-protection-policy-for-classification-and-labeling---without-protection"></a>Passaggio 1: Configurare i criteri di Azure Information Protection per la classificazione e l'assegnazione di etichette, senza protezione

Dal riquadro **Azure Information Protection-labels** visualizzare e configurare le etichette che non includono opzioni per la protezione dei dati. Per altre informazioni su come configurare le etichette e le impostazioni dei criteri, vedere [Configurazione dei criteri di Azure Information Protection](configure-policy.md).

### <a name="step-2-start-planning-for-migration"></a>Passaggio 2: Iniziare la pianificazione della migrazione

Per informazioni, vedere la guida alla migrazione: [Migrazione da AD RMS ad Azure Information Protection](migrate-from-ad-rms-to-azure-rms.md)

### <a name="step-3-configure-labels-for-protection"></a>Passaggio 3: Configurare le etichette per la protezione

Dopo aver attivato il servizio Azure Rights Management come parte del processo di migrazione, è possibile configurare le etichette per la protezione dati. Se tuttavia si esegue la migrazione degli utenti in batch assicurarsi che le etichette che applicano la protezione abbiano come ambito gli utenti sottoposti a migrazione.


