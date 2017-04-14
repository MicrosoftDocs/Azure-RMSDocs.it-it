---
title: Rilevamento dei documenti per Azure Information Protection
description: Istruzioni e informazioni per amministratori per configurare e usare il rilevamento dei documenti per Azure Information Protection.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/08/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 983ecdc9-5631-48b8-8777-f4cbbb4934e8
ms.reviewer: eymanor
ms.suite: ems
ms.openlocfilehash: dad69e37e2908d155fd1be370d190fd91d5739a3
ms.sourcegitcommit: 7b773ca5bf1abf30e527c34717ecb2dc96f88033
translationtype: HT
---
# <a name="configuring-and-using-document-tracking-for-azure-information-protection"></a>Configurazione e uso del rilevamento dei documenti per Azure Information Protection

>*Si applica a: Active Directory Rights Management Services, Azure Information Protection, Windows 10, Windows 8.1, Windows 8, Windows 7 con SP1*

Se si dispone di una [sottoscrizione che supporta il rilevamento dei documenti](https://www.microsoft.com/cloud-platform/azure-information-protection-features), il sito di rilevamento dei documenti è abilitato per impostazione predefinita per tutti gli utenti dell'organizzazione. Il rilevamento dei documenti mostra informazioni quali indirizzi di posta elettronica delle persone che hanno tentato di accedere ai documenti protetti condivisi dagli utenti, nel momento in cui queste persone hanno tentato di accedere, e la loro posizione. Se la visualizzazione di queste informazioni non è consentita all'interno dell'organizzazione a causa dei requisiti sulla privacy, è possibile disabilitare l'accesso al sito di rilevamento dei documenti tramite il cmdlet [Disable-AadrmDocumentTrackingFeature](http://go.microsoft.com/fwlink/?LinkId=623032). È possibile riabilitare l'accesso al sito in qualsiasi momento utilizzando [Enable-AadrmDocumentTrackingFeature](http://go.microsoft.com/fwlink/?LinkId=623037), ed è possibile verificare se l'accesso è attualmente abilitato o disabilitato utilizzando [Get-AadrmDocumentTrackingFeature](http://go.microsoft.com/fwlink/?LinkId=623037).

Per eseguire questi cmdlet, è necessario disporre almeno della versione **2.3.0.0** del modulo Azure Rights Management per Windows PowerShell. Per istruzioni di installazione, vedere [Installazione di Windows PowerShell per Azure Rights Management](../deploy-use/install-powershell.md).

> [!TIP]
> Se il modulo è stato scaricato e installato in precedenza, verificarne il numero di versione eseguendo: `(Get-Module aadrm –ListAvailable).Version`

Gli URL seguenti vengono utilizzati per il rilevamento dei documenti e devono essere consentiti (ad esempio, aggiungerli ai siti attendibili se si utilizza Internet Explorer con protezione avanzata):

-   https://&#42;.azurerms.com

-   https://ecn.dev.virtualearth.net

    > [!NOTE]
    > questo URL è per Bing maps.

-   https://&#42;.microsoftonline.com

-   https://&#42;.microsoftonline-p.com

## <a name="tracking-and-revoking-documents-for-users"></a>Rilevamento e revoca dei documenti per gli utenti

Quando gli utenti accedono al sito di rilevamento dei documenti, possono rilevare e revocare i documenti protetti tramite il client Azure Information Protection o condivisi tramite l'applicazione di condivisione Rights Management. Quando si accede come amministratore di Azure Information Protection (amministratore globale), è possibile fare clic sull'icona di amministrazione per passare alla modalità amministratore in modo da visualizzare i documenti che sono stati condivisi dagli utenti dell'organizzazione:

![Icona di amministrazione nel sito di rilevamento dei documenti](../media/tracking-site-admin-icon.png)

Le azioni intraprese in modalità amministratore vengono controllate e registrate nei file di log dei dati di utilizzo e, per continuare, è necessario confermare. Per altre informazioni su questa registrazione, vedere la sezione seguente.

Quando si è in modalità amministratore, è quindi possibile eseguire la ricerca in base all'utente o al documento. Se si esegue la ricerca in base all'utente, si visualizzeranno tutti i documenti che l'utente specificato ha condiviso. Se si esegue la ricerca in base al documento, si visualizzeranno tutti gli utenti dell'organizzazione che hanno condiviso tale documento. È quindi possibile analizzare i risultati della ricerca per rilevare i documenti che gli utenti hanno condiviso e, se necessario, revocarli. 

Per uscire dalla modalità amministratore, fare clic su **X** accanto a **Esci dalla modalità amministratore**:

![Opzione Esci dalla modalità amministratore nel sito di rilevamento dei documenti](../media/tracking-site-exit-admin-icon.png)

Per istruzioni su come usare il sito di rilevamento dei documenti, vedere [Tenere traccia dei documenti e revocarli](client-track-revoke.md) nella Guida dell'utente.

## <a name="usage-logging-for-the-document-tracking-site"></a>Registrazione dei dati di utilizzo per il sito di rilevamento dei documenti

Nei file di log dei dati di utilizzo sono presenti due campi applicabili al rilevamento dei documenti: **AdminAction** e **ActingAsUser**.

**AdminAction**: questo campo ha un valore true quando un amministratore usa il sito di rilevamento dei documenti in modalità amministratore, ad esempio, per revocare un documento per conto dell'utente o per visualizzare quando il documento è stato condiviso. Questo campo è vuoto quando l'accesso al sito di rilevamento dei documenti viene eseguito dall'utente.

**ActingAsUser**: quando il campo AdminAction è true, questo campo contiene il nome utente per conto del quale agisce l'amministratore per eseguire la ricerca di un utente o del proprietario di un documento. Questo campo è vuoto quando l'accesso al sito di rilevamento dei documenti viene eseguito dall'utente. 

Sono inoltre disponibili tipi di richieste che registrano la modalità in cui utenti e amministratori stanno usando il sito di rilevamento dei documenti. **RevokeAccess**, ad esempio, è il tipo di richiesta usato quando un utente, o un amministratore che agisce per conto dell'utente, revoca un documento nel sito di rilevamento dei documenti. Usare questo tipo di richiesta in combinazione con il campo AdminAction per determinare se il documento è stato revocato dal relativo utente (il campo AdminAction è vuoto) o se un amministratore ha revocato un documento per conto di un utente (il campo AdminAction è true).


Per altre informazioni sulla registrazione dell'utilizzo, vedere [Registrazione e analisi dell'utilizzo del servizio Azure Rights Management](../deploy-use/log-analyze-usage.md)



## <a name="next-steps"></a>Passaggi successivi
Dopo aver configurato il sito di rilevamento dei documenti per il client Azure Information Protection, vedere gli argomenti seguenti per altre informazioni che potrebbero essere necessarie per supportare il client:

- [File del client e registrazione dell'utilizzo](client-admin-guide-files-and-logging.md)

- [Tipi di file supportati](client-admin-guide-file-types.md)

- [Comandi di PowerShell](client-admin-guide-powershell.md)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
