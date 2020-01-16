---
title: Rilevamento dei documenti per Azure Information Protection
description: Istruzioni e informazioni per amministratori per configurare e usare il rilevamento dei documenti per Azure Information Protection.
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 1/06/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 983ecdc9-5631-48b8-8777-f4cbbb4934e8
ms.subservice: doctrack
ms.reviewer: eymanor
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 57d0fd6e2377a4ba6daaef65f8a64767eccbbd46
ms.sourcegitcommit: 03dc2eb973b20897b30659c2ac6cb43ce0a40e71
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/15/2020
ms.locfileid: "75960630"
---
# <a name="admin-guide-configuring-and-using-document-tracking-for-azure-information-protection"></a>Guida dell'amministratore: Configurazione e uso del rilevamento dei documenti per Azure Information Protection

>*Si applica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8, windows server 2019, windows server 2016, windows Server 2012 R2, windows Server 2012, windows Server 2008 R2*
>
> *Istruzioni per: [client di Azure Information Protection per Windows](../faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*


Se si dispone di una [sottoscrizione che supporta il rilevamento dei documenti](https://www.microsoft.com/en-us/cloud-platform/azure-information-protection-features), il sito di rilevamento dei documenti è abilitato per impostazione predefinita per tutti gli utenti dell'organizzazione. Il rilevamento dei documenti consente di indicare a utenti e amministratori quando è stato eseguito l'accesso a un documento protetto e, se necessario, se è possibile revocare un documento rilevato.

## <a name="using-powershell-to-manage-the-document-tracking-site"></a>Uso di PowerShell per gestire il sito di rilevamento dei documenti

Le sezioni seguenti contengono informazioni su come gestire il sito di rilevamento dei documenti tramite PowerShell. Per le istruzioni di installazione per il modulo PowerShell, vedere [installazione del modulo PowerShell AIPService](../install-powershell.md).

Per altre informazioni su ognuno dei cmdlet, usare i relativi collegamenti.

### <a name="privacy-controls-for-your-document-tracking-site"></a>Controlli sulla privacy per il sito di rilevamento dei documenti

Se la visualizzazione di tutte le informazioni di rilevamento dei documenti non è consentita nell'organizzazione a causa dei requisiti sulla privacy, è possibile disabilitare il rilevamento dei documenti tramite il cmdlet [Disable-AipServiceDocumentTrackingFeature](/powershell/module/aipservice/disable-aipservicedocumenttrackingfeature) . 

Il cmdlet disabilita l'accesso al sito di rilevamento dei documenti in modo che tutti gli utenti dell'organizzazione non possano rilevare o revocare l'accesso ai documenti che hanno protetto. È possibile riabilitare il rilevamento dei documenti in qualsiasi momento usando [Enable-AipServiceDocumentTrackingFeature](/powershell/module/aipservice/enable-aipservicedocumenttrackingfeature)ed è possibile verificare se il rilevamento dei documenti è attualmente abilitato o disabilitato usando [Get-AipServiceDocumentTrackingFeature](/powershell/module/aipservice/get-aipservicedocumenttrackingfeature). 

Quando è abilitato, il sito di rilevamento dei documenti visualizza, per impostazione predefinita, informazioni quali gli indirizzi di posta elettronica delle persone che hanno tentato di accedere ai documenti protetti, quando queste persone hanno tentato di accedere e la relativa posizione. Questo livello di informazioni può essere molto utile per determinare come vengono usati i documenti condivisi e se tali documenti devono essere revocati quando si rileva un'attività sospetta. Tuttavia, per motivi di privacy, può essere necessario disabilitare queste informazioni per alcuni o tutti gli utenti. 

Se sono presenti utenti che non devono avere questa attività rilevata da altri utenti, aggiungerli a un gruppo archiviato in Azure AD e specificare il gruppo con il cmdlet [set-AipServiceDoNotTrackUserGroup](/powershell/module/aipservice/Set-AipServiceDoNotTrackUserGroup) . Quando si esegue questo cmdlet è necessario specificare un singolo gruppo. Tuttavia, il gruppo può contenere gruppi nidificati. 

Per questi membri del gruppo, gli utenti non possono visualizzare attività nel sito di rilevamento dei documenti se queste ultime sono legate a documenti condivisi con loro. Inoltre, non vengono inviate notifiche di posta elettronica all'utente che ha condiviso il documento.

Quando si usa questa configurazione, tutti gli utenti possono comunque usare il sito di rilevamento dei documenti e revocare l'accesso ai documenti protetti. Tuttavia, non visualizzano l'attività per gli utenti specificati usando il cmdlet Set-AipServiceDoNotTrackUserGroup.

Questa impostazione si applica solo agli utenti finali. Gli amministratori di Azure Information Protection possono sempre tenere traccia delle attività di tutti gli utenti, anche quando tali utenti vengono specificati tramite set-AipServiceDoNotTrackUserGroup. Per altre informazioni su come gli amministratori possono tenere traccia dei per gli utenti, vedere la sezione [Rilevamento e revoca dei documenti per gli utenti](#tracking-and-revoking-documents-for-users).


### <a name="logging-information-from-the-document-tracking-site"></a>Informazioni di registrazione dal sito di rilevamento dei documenti

È possibile utilizzare i cmdlet seguenti per scaricare le informazioni di registrazione dal sito di rilevamento dei documenti:

- [Get-AipServiceTrackingLog](/powershell/module/aipservice/Get-AipServiceTrackingLog)
    
    Questo cmdlet restituisce informazioni di rilevamento sui documenti protetti per un utente specificato che ha protetto i documenti (emittente di Rights Management) o ha avuto accesso a documenti protetti. Usare questo cmdlet per rispondere alla domanda "A quali documenti protetti ha eseguito l'accesso un utente specificato o quali documenti protetti ha rilevato?"

- [Get-AipServiceDocumentLog](/powershell/module/aipservice/Get-AipServiceDocumentLog)
    
    Questo cmdlet restituisce informazioni di protezione sui documenti rilevati per un utente specificato se tale utente ha protetto documenti (emittente di Rights Management) o era proprietario di Rights Management per i documenti oppure se i documenti protetti erano configurati per consentire l'accesso direttamente all'utente. Usare questo cmdlet per rispondere alla domanda "In che modo sono protetti i documenti per un utente specificato?"

## <a name="destination-urls-used-by-the-document-tracking-site"></a>URL di destinazione usati dal sito di rilevamento dei documenti

Gli URL seguenti vengono usati per il rilevamento dei documenti e devono essere consentiti su tutti i dispositivi e i servizi tra i client che eseguono il client Azure Information Protection e Internet. Ad esempio, aggiungere gli URL ai firewall o ai siti attendibili se si usa Internet Explorer con protezione avanzata.

-  `https://*.azurerms.com`

- `https://*.microsoftonline.com`

- `https://*.microsoftonline-p.com`

- `https://ecn.dev.virtualearth.net`

Questi URL sono standard per il servizio Azure Rights Management, ad eccezione dell'URL virtualearth.net usato nelle mappe di Bing per visualizzare la posizione dell'utente.

## <a name="tracking-and-revoking-documents-for-users"></a>Rilevamento e revoca dei documenti per gli utenti

Quando gli utenti accedono al sito di rilevamento dei documenti, possono rilevare e revocare i documenti protetti tramite il client Azure Information Protection. Quando si accede come amministratore di globale di Azure AD per il tenant, è possibile fare clic sull'icona di amministrazione per passare alla modalità amministratore. Gli altri ruoli di amministratore non supportano questa modalità per il sito di rilevamento dei documenti. 

![Icona di amministrazione nel sito di rilevamento dei documenti](../media/tracking-site-admin-icon.png)

La modalità amministratore consente di visualizzare i documenti che gli utenti dell'organizzazione hanno selezionato per tenerne traccia con il client Azure Information Protection.

> [!NOTE] 
> Se si è un amministratore globale e l'icona non è visibile, significa che non sono stati ancora condivisi documenti. In questo caso, usare l'URL seguente per accedere al sito di rilevamento dei documenti: https://portal.azurerms.com/#/admin

Le azioni intraprese in modalità amministratore vengono controllate e registrate nei file di log dei dati di utilizzo e, per continuare, è necessario confermare. Per altre informazioni su questa registrazione, vedere la sezione seguente.

Quando si è in modalità amministratore, è quindi possibile eseguire la ricerca in base all'utente o al documento. Se si esegue la ricerca per utente, vengono visualizzati tutti i documenti che l'utente specificato ha selezionato per tenerne traccia con il client Azure Information Protection. 

Se si esegue la ricerca per documento, vengono visualizzati tutti gli utenti dell'organizzazione che hanno tenuto traccia del documento con il client Azure Information Protection. È quindi possibile analizzare i risultati della ricerca per rilevare i documenti che gli utenti hanno protetto e revocarli se necessario. 

Per uscire dalla modalità amministratore, fare clic su **X** accanto a **Esci dalla modalità amministratore**:

![Opzione Esci dalla modalità amministratore nel sito di rilevamento dei documenti](../media/tracking-site-exit-admin-icon.png)

Per istruzioni su come usare il sito di rilevamento dei documenti, vedere [Tenere traccia dei documenti e revocarli](client-track-revoke.md) nella Guida dell'utente.

### <a name="using-powershell-to-register-labeled-documents-with-the-document-tracking-site"></a>Uso di PowerShell per registrare i documenti etichettati nel sito di rilevamento dei documenti

Per poter rilevare e revocare un documento, è prima necessario registrarlo nel sito di rilevamento dei documenti. Questa azione si verifica quando gli utenti selezionano l'opzione **Rileva e revoca** da Esplora file o dalle app di Office quando usano il client Azure Information Protection.

Se si etichettano e proteggono i file per gli utenti usando il cmdlet [Set-AIPFileLabel](/powershell/azureinformationprotection/vlatest/set-aipfilelabel), è possibile usare il parametro *EnableTracking* per registrare il file nel sito di rilevamento dei documenti. Ad esempio:

    Set-AIPFileLabel -Path C:\Projects\ -LabelId ade72bf1-4714-4714-4714-a325f824c55a -EnableTracking

## <a name="usage-logging-for-the-document-tracking-site"></a>Registrazione dei dati di utilizzo per il sito di rilevamento dei documenti

Nei file di log dei dati di utilizzo sono presenti due campi applicabili al rilevamento dei documenti: **AdminAction** e **ActingAsUser**.

**AdminAction**: questo campo ha un valore true quando un amministratore usa il sito di rilevamento dei documenti in modalità amministratore, ad esempio, per revocare un documento per conto dell'utente o per visualizzare quando il documento è stato condiviso. Questo campo è vuoto quando l'accesso al sito di rilevamento dei documenti viene eseguito dall'utente.

**ActingAsUser**: quando il campo AdminAction è true, questo campo contiene il nome utente per conto del quale agisce l'amministratore per eseguire la ricerca di un utente o del proprietario di un documento. Questo campo è vuoto quando l'accesso al sito di rilevamento dei documenti viene eseguito dall'utente. 

Sono inoltre disponibili tipi di richieste che registrano la modalità in cui utenti e amministratori stanno usando il sito di rilevamento dei documenti. **RevokeAccess**, ad esempio, è il tipo di richiesta usato quando un utente, o un amministratore che agisce per conto dell'utente, revoca un documento nel sito di rilevamento dei documenti. Usare questo tipo di richiesta in combinazione con il campo AdminAction per determinare se il documento è stato revocato dal relativo utente (il campo AdminAction è vuoto) o se un amministratore ha revocato un documento per conto di un utente (il campo AdminAction è true).

Per ulteriori informazioni sulla registrazione dell'utilizzo, vedere [registrazione e analisi dell'utilizzo della protezione da Azure Information Protection](../log-analyze-usage.md)

## <a name="next-steps"></a>Passaggi successivi
Dopo aver configurato il sito di rilevamento dei documenti per il client Azure Information Protection, vedere gli argomenti seguenti per altre informazioni che potrebbero essere necessarie per supportare il client:

- [Personalizzazioni](client-admin-guide-customizations.md)

- [File del client e registrazione dell'utilizzo](client-admin-guide-files-and-logging.md)

- [Tipi di file supportati](client-admin-guide-file-types.md)

- [Comandi di PowerShell](client-admin-guide-powershell.md)

