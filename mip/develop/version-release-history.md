---
title: Microsoft Information Protection (MIP) SDK versione cronologia delle versioni e criteri di supporto
description: Guida introduttiva che mostra come scrivere la logica di inizializzazione per applicazioni client di Microsoft Information Protection (MIP) SDK.
author: msmbaldwin
ms.service: information-protection
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.date: 01/08/2019
ms.author: mbaldwin
manager: barbkess
ms.openlocfilehash: 9f02d682164dac8ee28ed023dd7b21b53937f4bb
ms.sourcegitcommit: fff4c155c52c9ff20bc4931d5ac20c3ea6e2ff9e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/24/2019
ms.locfileid: "60184219"
---
# <a name="microsoft-information-protection-mip-sdk-version-release-history-and-support-policy"></a>Microsoft Information Protection (MIP) SDK versione cronologia delle versioni e criteri di supporto

## <a name="servicing"></a>Per la manutenzione 

Ogni versione di disponibilità generale (GA) è supportato per sei mesi dopo la prossima versione di disponibilità generale è versione. La documentazione di potrebbe non includere informazioni sulle versioni non supportate. Correzioni e nuove funzionalità vengono applicate solo all'ultima versione disponibile a livello generale.

Le versioni di anteprima non devono essere distribuite nell'ambiente di produzione. In alternativa, usare la versione di anteprima più recente per testare nuove funzionalità e correzioni che saranno disponibili nella prossima versione disponibile a livello generale. È supportata solo la versione di anteprima più recente.

## <a name="release-history"></a>Cronologia delle versioni

Usare le informazioni seguenti per visualizzare gli elementi nuovi o modificati per una versione supportata. La versione più recente è elencata per prima. 

> [!NOTE]
> Correzioni minori non sono elencate, se si verifica un problema con il SDK, è consigliabile verificare se è impostata con l'ultima versione disponibile a livello generale. Se il problema persiste, verificare la versione di anteprima corrente.
>  
> Per il supporto tecnico, visitare il [forum di Stack Overflow Microsoft Information Protection](https://stackoverflow.com/questions/tagged/microsoft-information-protection). 

## <a name="version-110"></a>Versione 1.1.0

**Data di rilascio**: TBD

Questa versione introduce il supporto per le piattaforme seguenti:

  - .NET
  - iOS SDK (API criteri)
  - Android SDK (criterio di API e l'API di protezione)

**Nuove funzionalità:**

- Supporto ADRMS
- Le operazioni API per la protezione sono completamente asincrone (in Win32), consentendo operazioni di crittografia/decrittografia non bloccante simultanee
  - Callback dell'applicazione (AuthDelegate, HTTPDelegate e così via) può ora essere richiamato in *qualsiasi* thread in background
- Proprietà etichetta personalizzata impostate dagli amministratori IT possono ora essere letti tramite mip::Label::GetCustomSettings
- Licenza di pubblicazione serializzata ora può essere recuperato direttamente da un file senza operazioni HTTP tramite mip::FileHandler::GetSerializedPublishingLicense
- Le applicazioni ricevono una notifica se un'operazione HTTP è necessario per completare la creazione di un MIP:: fileengine/MIP:: policyengine tramite mip::FileProfile::Observer::OnAddPolicyEngineStarting / mip::PolicyProfile::Observer::OnAddEngineStarting
- Il rilevamento di eventuale contenuto protetto è una data di scadenza o non è stato semplificato con mip::ProtectionDescriptor::DoesContentExpire metodo praticità
- Classificazione:
  - Tipi di sensibilità (espressioni di espressione regolare per CC #, passport # e così via) può essere acquisita dal servizio di controllo del codice sorgente
    - Abilitare la funzionalità impostando mip::FileEngine::Settings mip::PolicyEngine::Settings flag
    - Leggere tipi tramite mip::FileEngine::ListSensitivityTypes / mip::PolicyEngine::ListSensitivityTypes
  - Risultati della classificazione dalla cartella Utility dello scanner di documento esterni possono essere inseriti in MIP per promuovere le etichette obbligatorie/consigliate basate sul contenuto del documento
    - Passare i risultati al MIP tramite mip::FileExecutionState::GetClassificationResults / mip::ExecutionState::GetClassificationResults
    - MIP::ApplyLabelAction e mip::RecommendLabelAction possono essere restituiti da mip::PolicyEngine::ComputeActions quando i risultati di classificazione corrispondono a una regola di criterio che indica le etichette necessari o consigliati

- Nuovi requisiti:
  - Imposto il popolamento di ID/nome/versione campi mip::ApplicationInfo durante la creazione di MIP:: fileprofile mip::PolicyProfile e MIP:: protectionprofile
  - Le applicazioni devono implementare nuova interfaccia mip::FileExecutionState durante la creazione di mip::FileHandlers
  
- Eccezioni aggiornate:
  - MIP::NoAuthTokenError generata se AuthDelegate dell'applicazione restituisce un token vuoto (a causa dell'annullamento)
    - Si applica alla creazione di:
      - mip::FileEngine
      - mip::FileHandler
      - mip::PolicyEngine
      - mip::ProtectionHandler
  - MIP::NoPolicyError generata se il tenant non è configurato per le etichette
    - Si applica alla creazione di:
      - mip::FileEngine
      - mip::PolicyEngine
  - MIP::ServiceDisabledError generata un'eccezione se il servizio RMS è disabilitato per un utente/dispositivo/piattaforma/tenant specifico
    - Si applica alla creazione di:
      - mip::FileHandler
      - mip::ProtectionHandler
  - MIP::NoPermissionsError generata se un utente non dispone di diritti per decrittografare un documento o il contenuto è scaduto
    - Si applica alla creazione di:
      - mip::FileHandler
      - mip::ProtectionHandler

**Correzioni**:

TBD

## <a name="next-steps"></a>Passaggi successivi

- Visualizzare [problemi e domande frequenti di MIP SDK](faqs-known-issues.md) per informazioni sulle piattaforme supportate e altro ancora.
- Visualizzare [configurazione e installazione di Microsoft Information Protection SDK](setup-configure-mip.md) per informazioni su come iniziare a usare il SDK di MIP.
