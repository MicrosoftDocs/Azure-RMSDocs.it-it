---
title: Rilevare e revocare l'accesso Azure Information Protection
description: Viene descritto come gli amministratori possono tenere traccia dell'accesso ai documenti per i documenti protetti, nonché revocare l'accesso, se necessario.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 01/07/2021
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 643c762e-23ca-4b02-bc39-4e3eeb657a1d
ms.subservice: doctrack
ms.reviewer: esaggese
ms.suite: ems
ms.custom: user
ms.openlocfilehash: 7b60438ad3d1e8a971c58a7f29b2f8b41dd84c91
ms.sourcegitcommit: 78c7ab80be7c292ea4bc62954a4e29c449e97439
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/13/2021
ms.locfileid: "98163740"
---
# <a name="administrator-guide-track-and-revoke-document-access-with-azure-information-protection-public-preview"></a>Guida dell'amministratore: rilevare e revocare l'accesso ai documenti con Azure Information Protection (anteprima pubblica)

>***Si applica a**: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8 *
>
>***Pertinente per**: [AIP Unified Labeling client only](../faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients). Per il client classico, vedere [Guida dell'amministratore: configurazione e uso del rilevamento dei documenti per AIP usando il client classico](client-admin-guide-document-tracking.md). *

Se è stato eseguito l'aggiornamento alla [versione 2.9.111.0](unifiedlabelingclient-version-release-history.md#version-291110) o successiva, eventuali documenti protetti non ancora registrati per il rilevamento vengono registrati automaticamente alla successiva apertura tramite il client di assegnazione unificata di AIP. I documenti protetti sono supportati per Track and Revoke, anche se non sono etichettati.

La registrazione di un documento per il rilevamento consente [Microsoft 365 agli amministratori globali](/microsoft-365/admin/add-users/about-admin-roles#commonly-used-microsoft-365-admin-center-roles) di tenere traccia dei dettagli di accesso, inclusi gli eventi di accesso riusciti e i tentativi negati, nonché di revocare l'accesso, se necessario. 

Le funzionalità rileva e revoca per il client Unified Labeling sono attualmente in anteprima. Le [condizioni aggiuntive per l'anteprima di Azure](https://azure.microsoft.com/support/legal/preview-supplemental-terms/) includono termini legali aggiuntivi che si applicano a funzionalità di Azure in versione beta, anteprima o diversamente non ancora disponibili a livello generale. 

## <a name="track-document-access"></a>Tenere traccia dell'accesso ai documenti

Gli amministratori globali possono tenere traccia dell'accesso per i documenti protetti tramite PowerShell usando il **ContentID** generato per il documento protetto durante la registrazione.

**Per visualizzare i dettagli di accesso ai documenti**:

Usare i cmdlet seguenti per trovare i dettagli del documento di cui si vuole tenere traccia:

1. Trovare il valore **ContentID** per il documento di cui si vuole tenere traccia.
    
    Usare [Get-AipServiceDocumentLog](/powershell/module/aipservice/get-aipservicedocumentlog) per cercare un documento usando il nome file e/o l'indirizzo di posta elettronica dell'utente che ha applicato la protezione.
    
    ad esempio:
        
    ```PowerShell
    Get-AipServiceDocumentLog -ContentName "test.docx" -Owner “alice@contoso.com” -FromTime "12/01/2020 00:00:00" -ToTime "12/31/2020 23:59:59"
    ```
 
    Questo comando restituisce **ContentID** per tutti i documenti protetti corrispondenti, registrati per il rilevamento.

    > [!NOTE]
    > I documenti protetti vengono registrati per il rilevamento quando vengono aperti per la prima volta in un computer in cui è installato il client di etichettatura unificata. Se questo comando non restituisce il ContentID per il file protetto, aprirlo in un computer in cui è installato il client di etichettatura unificato per registrare il documento per il rilevamento.

1. Usare il cmdlet [Get-AipServiceTrackingLog](/powershell/module/aipservice/get-aipservicetrackinglog) con il **ContentID** del documento per restituire i dati di rilevamento.

    Ad esempio:
    
    ```PowerShell
    Get-AipServiceTrackingLog -ContentId c03bf90c-6e40-4f3f-9ba0-2bcd77524b87
    ```

    Vengono restituiti i dati di rilevamento, inclusi i messaggi di posta elettronica degli utenti che hanno tentato di accedere, la concessione o la negazione dell'accesso, l'ora e la data del tentativo e il dominio e la posizione in cui ha avuto origine il tentativo di accesso.

## <a name="revoke-document-access-from-powershell"></a>Revocare l'accesso ai documenti da PowerShell

Gli amministratori globali possono revocare l'accesso per qualsiasi documento protetto archiviato nelle rispettive condivisioni di contenuto locali, usando il cmdlet [set-AIPServiceDocumentRevoked](/powershell/module/aipservice/set-aipservicedocumentrevoked) .

1. Individuare il valore **ContentID** per il documento per cui si desidera revocare l'accesso.
    
    Usare [Get-AipServiceDocumentLog](/powershell/module/aipservice/get-aipservicedocumentlog) per cercare un documento usando il nome file e/o l'indirizzo di posta elettronica dell'utente che ha applicato la protezione.
    
    Ad esempio:
        
    ```PowerShell
    Get-AipServiceDocumentLog -ContentName "test.docx" -Owner “alice@contoso.com” -FromTime "12/01/2020 00:00:00" -ToTime "12/31/2020 23:59:59"
    ```

    I dati restituiti includono il valore ContentID per il documento.

    > [!TIP]
    > Solo i documenti che sono stati protetti e registrati per il rilevamento hanno un valore **ContentID** . 
    >
    > Se il documento non contiene **ContentID**, aprirlo in un computer in cui è installato il client di etichettatura unificato per registrare il file per il rilevamento.

1. Usare [set-AIPServiceDocumentRevoked](/powershell/module/aipservice/set-aipservicedocumentrevoked) con il ContentId del documento per revocare l'accesso.

    Ad esempio:

    ```PowerShell
    Set-AipServiceDocumentRevoked -ContentId 0e421e6d-ea17-4fdb-8f01-93a3e71333b8 -IssuerName testIssuer
    ```

> [!NOTE]
> Se è consentito l' [accesso offline](/microsoft-365/compliance/encryption-sensitivity-labels#assign-permissions-now) , gli utenti continueranno a essere in grado di accedere ai documenti revocati fino alla scadenza del periodo di criteri offline. 
> 

> [!TIP]
> Gli utenti possono anche revocare l'accesso per tutti i documenti in cui è stata applicata la protezione direttamente dal menu di **riservatezza** nelle app di Office. Per altre informazioni, vedere [Guida dell'utente: revocare l'accesso ai documenti con Azure Information Protection](revoke-access-user.md)

### <a name="un-revoke-access"></a>Annulla revoca accesso

Se è stato revocato accidentalmente l'accesso a un documento specifico, usare lo stesso valore di **ContentID** con il cmdlet [Clear-AipServiceDocumentRevoke](/powershell/module/aipservice/clear-aipservicedocumentrevoke) per annullare la revoca dell'accesso. 

Ad esempio:

```PowerShell
Clear-AipServiceDocumentRevoke -ContentId   0e421e6d-ea17-4fdb-8f01-93a3e71333b8 -IssuerName testIssuer
```

L'accesso ai documenti viene concesso all'utente definito nel parametro **IssuerName** .

## <a name="turn-off-track-and-revoke-features-for-your-tenant"></a>Disattivare le funzionalità di rilevamento e revoca per il tenant

Se è necessario disattivare le funzionalità di rilevamento e revoca per il tenant, ad esempio per i requisiti di privacy nell'organizzazione o nell'area, eseguire entrambi i passaggi seguenti:

1. Eseguire il cmdlet [Disable-AipServiceDocumentTrackingFeature](/powershell/module/aipservice/disable-aipservicedocumenttrackingfeature) .

1. Impostare l'impostazione client avanzata [EnableTrackAndRevoke](clientv2-admin-guide-customizations.md#turn-off-document-tracking-features-public-preview) su **false**. 

Il rilevamento dei documenti e le opzioni per revocare l'accesso sono disattivati per il tenant:

- L'apertura di documenti protetti con il client AIP Unified Labeling non registra più i documenti per Track and Revoke.
- I log di accesso non vengono archiviati quando vengono aperti i documenti protetti che sono già registrati. I log di accesso archiviati prima della disattivazione di queste funzionalità sono ancora disponibili. 
- Gli amministratori non saranno in grado di rilevare o revocare l'accesso tramite PowerShell e gli utenti finali non visualizzeranno più l'opzione di menu [**Revoke**](revoke-access-user.md#revoke-access-from-microsoft-office-apps) nelle app di Office.

> [!NOTE]
> Per attivare di nuovo Tracking e REVOKE, impostare [EnableTrackAndRevoke](clientv2-admin-guide-customizations.md#turn-off-document-tracking-features-public-preview) su **true** ed eseguire anche il cmdlet [Enable-AipServiceDocumentTrackingFeature](/powershell/module/aipservice/enable-aipservicedocumenttrackingfeature) .
>
## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni, vedere:

- [Guida dell'utente del client per l'assegnazione unificata di AIP](clientv2-user-guide.md)
- [Guida dell'amministratore client per l'assegnazione unificata di AIP](clientv2-admin-guide.md)
- [Problemi noti per le funzionalità di rilevamento e revoca](../known-issues.md#known-issues-for-track-and-revoke-features-public-preview)
