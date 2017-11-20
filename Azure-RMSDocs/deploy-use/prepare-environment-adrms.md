---
title: Preparare l'ambiente per Azure RMS e AD RMS
description: Informazioni aggiuntive per un'implementazione di Azure Rights Management con AD RMS.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 11/10/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 11ffa730-c5dc-4b6b-9c1e-c58eff8aafc2
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: b20bbc1fe0de90b9b0151098e1b77d3c7a98c431
ms.sourcegitcommit: e9a24fc5303b21f5eeebf16afed44db0d163ac77
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/11/2017
---
# <a name="preparing-the-environment-for-azure-rights-management-when-you-also-have-active-directory-rights-management-services-ad-rms"></a>Preparazione dell'ambiente per Azure Rights Management quando è presente anche Active Directory Rights Management Services (AD RMS)

>*Si applica a: Azure Information Protection, Office 365*

Indicazioni importanti da seguire se si sta già usando Active Directory Rights Management Services (AD RMS) e si verifica quanto segue:

## <a name="you-see-an-option-to-activate-protection-when-you-configure-azure-information-protection"></a>Quando si configura Azure Information Protection viene visualizzata un'opzione per attivare la protezione

Il pannello **Azure Information Protection - Attivazione della protezione** include un'opzione per attivare il servizio Azure Rights Management (Azure RMS). 

Se si usa anche Active Directory Rights Management Services (AD RMS), non selezionare **Attiva**. L'attivazione di Azure Rights Management quando è già presente AD RMS non è compatibile. Questo scenario non è supportato e restituisce risultati non prevedibili, pertanto è importante non attivare Azure Rights Management in questa fase. 

Quando i computer sono pronti per il passaggio da AD RMS al servizio Azure Rights Management è possibile avviare un processo di migrazione. Uno dei passaggi della migrazione è l'attivazione del servizio, ma questa operazione va eseguita solo dopo aver esportato le informazioni di configurazione da AD RMS al servizio Azure Rights Management. In tal modo si garantisce che sarà possibile aprire i documenti e messaggi di posta elettronica protetti in precedenza da AD RMS.

Anche quando il servizio Azure Rights Management non è attivato, è possibile usare Azure Information Protection per le etichette che applicano solo la classificazione. Viene creato un criterio predefinito speciale che non include la protezione dei dati e le opzioni di configurazione corrispondenti restano disattivate fino all'attivazione del servizio Azure Rights Management.

### <a name="step-1-configure-your-azure-information-protection-policy-for-classification-and-labeling---without-protection"></a>Passaggio 1: Configurare i criteri di Azure Information Protection per la classificazione e l'assegnazione di etichette, senza protezione

Nel pannello iniziale di **Azure Information Protection** selezionare **Criteri globali** per visualizzare e configurare i criteri globali, che non includono le opzioni per la protezione dei dati. Per altre informazioni, veder e[Configurazione dei criteri di Azure Information Protection](configure-policy.md).

### <a name="step-2-start-planning-for-migration"></a>Passaggio 2: Avviare la pianificazione della migrazione

Per informazioni sulla migrazione, vedere: [Migrazione da AD RMS ad Azure Information Protection](../plan-design/migrate-from-ad-rms-to-azure-rms.md).

### <a name="step-3-start-to-configure-labels-for-protection"></a>Passaggio 3: Iniziare a configurare le etichette per la protezione

Dopo aver attivato il servizio Azure Rights Management come parte del processo di migrazione, è possibile configurare le etichette per la protezione dati. Se tuttavia si esegue la migrazione degli utenti in batch assicurarsi che le etichette che applicano la protezione abbiano come [ambito](configure-policy-scope.md) solo gli utenti già sottoposti a migrazione.


[!INCLUDE[Commenting house rules](../includes/houserules.md)]


