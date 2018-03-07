---
title: Preparare l'ambiente per Azure RMS e AD RMS
description: Informazioni aggiuntive per un'implementazione di Azure Rights Management con AD RMS.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/21/2018
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 11ffa730-c5dc-4b6b-9c1e-c58eff8aafc2
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: de42f0d87f42c304c2df906fe037816be7f2ba25
ms.sourcegitcommit: 23d98a405057d61a737313c8dfef042996131d3e
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/27/2018
---
# <a name="preparing-the-environment-for-azure-rights-management-when-you-also-have-active-directory-rights-management-services-ad-rms"></a>Preparazione dell'ambiente per Azure Rights Management quando è presente anche Active Directory Rights Management Services (AD RMS)

>*Si applica a: Azure Information Protection, Office 365*

Indicazioni importanti da seguire se si usa già Active Directory Rights Management Services (AD RMS) e in presenza di uno degli scenari seguenti:

- [La sottoscrizione che include Azure Rights Management è stata acquistata durante il mese di febbraio 2018 o successivamente](#your-subscription-was-purchased-during-or-after-february-2018).

- [Quando si configura il criterio di Azure Information Protection nel portale di Azure, viene visualizzata un'opzione che consente di attivare la protezione](#you-see-an-option-to activate-azure-rights-management-when-you-configure-azure-information-protection)

## <a name="your-subscription-was-purchased-during-or-after-february-2018"></a>La sottoscrizione è stata acquistata nel mese di febbraio 2018 o successivamente

Verso la fine di febbraio 2018, le nuove sottoscrizioni che includono Azure Information Protection attivano il servizio di Azure Rights Management per impostazione predefinita. Se il servizio viene attivato automaticamente e si usa anche Active Directory Rights Management Services (AD RMS), questa combinazione non è compatibile. Se non vengono eseguiti altri passaggi, è possibile che all'avvio alcuni computer usino automaticamente il servizio Azure Rights Management e si connettano anche al cluster AD RMS. Questo scenario non è supportato e restituisce risultati non prevedibili, pertanto è importante disattivare Azure Rights Management appena possibile. 

Quando i computer sono pronti per il passaggio da AD RMS al servizio Azure Rights Management, è possibile avviare un processo di migrazione. Uno dei passaggi della migrazione è la riattivazione del servizio, ma questa operazione viene eseguita solo dopo aver esportato le informazioni di configurazione da AD RMS nel servizio Azure Rights Management. In tal modo si garantisce che sia possibile aprire i documenti e messaggi di posta elettronica protetti in precedenza da AD RMS.

Il primo passaggio prevede la disattivazione del servizio Azure Rights Management.

### <a name="step-1-deactivate-azure-rights-management"></a>Passaggio 1: Disattivare Azure Rights Management
Per disattivare [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)], usare una delle procedure descritte di seguito.

> [!TIP]
> È inoltre possibile usare il cmdlet di Windows PowerShell [Disable-Aadrm](http://msdn.microsoft.com/library/windowsazure/dn629422.aspx) per disattivare [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)].

#### <a name="to-deactivate-rights-management-from-the-office-365-admin-center"></a>Per disattivare Rights Management mediante l'interfaccia di amministrazione di Office 365

1. Accedere alla [pagina Rights Management](https://account.activedirectory.windowsazure.com/RmsOnline/Manage.aspx) per gli amministratori di Office 365.
    
    Se viene chiesto di effettuare l'accesso, usare un account di amministratore globale di Office 365.

2. Nella pagina **rights management** fare clic su **disattiva**.

3.  Quando viene visualizzata la richiesta **Disattivare Rights Management?** fare clic su **Disattiva**.

Verrà visualizzato il messaggio che indica che **Rights Management non è attivato** con l'opzione per l'attivazione.

#### <a name="to-deactivate-rights-management-from-the-azure-portal"></a>Per disattivare Rights Management dal portale di Azure

1. Se non è già stato fatto, aprire una nuova finestra del browser e [accedere al portale di Azure](configure-policy.md#signing-in-to-the-azure-portal). Quindi passare al pannello **Azure Information Protection**.
    
    Ad esempio, dal menu hub fare clic su **Tutti i servizi** e iniziare a digitare **Informazioni** nella casella Filtro. Selezionare **Azure Information Protection**.
    
    Se non si è ancora eseguito l'accesso al pannello Azure Information Protection, vedere i [passaggi aggiuntivi](configure-policy.md#to-access-the-azure-information-protection-blade-for-the-first-time) che è necessario eseguire una sola volta per aggiungere questo pannello al portale.

2. Nel pannello iniziale di **Azure Information Protection** selezionare **Protection activation** (Attivazione protezione). 

3.  Nel pannello **Azure Information Protection - Protection activation** (Azure Information Protection - Attivazione protezione) selezionare **Disattiva**. Selezionare **Sì** per confermare la scelta.

Sulla barra delle informazioni verrà visualizzato **Disattivazione completata** mentre **Disattiva** è stato sostituito da **Attiva**. 

### <a name="step-2-start-planning-for-migration"></a>Passaggio 2: Avviare la pianificazione della migrazione

Per informazioni vedere la guida sulla migrazione: [Migrazione da AD RMS ad Azure Information Protection](../plan-design/migrate-from-ad-rms-to-azure-rms.md).

## <a name="you-see-an-option-to-activate-protection-when-you-configure-azure-information-protection"></a>Quando si configura Azure Information Protection viene visualizzata un'opzione per attivare la protezione

Il pannello **Azure Information Protection - Attivazione della protezione** include un'opzione per attivare il servizio Azure Rights Management (Azure RMS).  

Se si usa anche Active Directory Rights Management Services (AD RMS), non selezionare **Attiva**. L'attivazione di Azure Rights Management quando è già presente AD RMS non è compatibile. Questo scenario non è supportato e restituisce risultati non prevedibili, pertanto è importante non attivare Azure Rights Management in questa fase.  

Quando i computer sono pronti per il passaggio da AD RMS al servizio Azure Rights Management è possibile avviare un processo di migrazione. Uno dei passaggi della migrazione è l'attivazione del servizio, ma questa operazione va eseguita solo dopo aver esportato le informazioni di configurazione da AD RMS al servizio Azure Rights Management. In tal modo si garantisce che sarà possibile aprire i documenti e messaggi di posta elettronica protetti in precedenza da AD RMS. 

Anche quando il servizio Azure Rights Management non è attivato, è possibile usare Azure Information Protection per le etichette che applicano solo la classificazione. Viene creato un criterio predefinito speciale che non include la protezione dei dati e le opzioni di configurazione corrispondenti restano disattivate fino all'attivazione del servizio Azure Rights Management.

### <a name="step-1-configure-your-azure-information-protection-policy-for-classification-and-labeling---without-protection"></a>Passaggio 1: Configurare i criteri di Azure Information Protection per la classificazione e l'assegnazione di etichette, senza protezione

Nel pannello iniziale di **Azure Information Protection** selezionare **Criteri globali** per visualizzare e configurare i criteri globali, che non includono le opzioni per la protezione dei dati. Per altre informazioni, veder e[Configurazione dei criteri di Azure Information Protection](configure-policy.md).

### <a name="step-2-start-planning-for-migration"></a>Passaggio 2: Avviare la pianificazione della migrazione

Per informazioni vedere la guida sulla migrazione: [Migrazione da AD RMS ad Azure Information Protection](../plan-design/migrate-from-ad-rms-to-azure-rms.md).

### <a name="step-3-start-to-configure-labels-for-protection"></a>Passaggio 3: Iniziare a configurare le etichette per la protezione

Dopo aver attivato il servizio Azure Rights Management come parte del processo di migrazione, è possibile configurare le etichette per la protezione dati. Se tuttavia si esegue la migrazione degli utenti in batch assicurarsi che le etichette che applicano la protezione abbiano come ambito gli utenti sottoposti a migrazione.

[!INCLUDE[Commenting house rules](../includes/houserules.md)]

