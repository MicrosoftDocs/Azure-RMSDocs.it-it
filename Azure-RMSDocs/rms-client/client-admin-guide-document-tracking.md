---
title: Rilevamento dei documenti per Azure Information Protection
description: Istruzioni e informazioni per gli amministratori sulla configurazione e l'uso del rilevamento dei documenti per Azure Information Protection.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 01/29/2018
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 983ecdc9-5631-48b8-8777-f4cbbb4934e8
ms.reviewer: eymanor
ms.suite: ems
ms.openlocfilehash: bbbc9a274ea815577109276bceb0b08617f03809
ms.sourcegitcommit: 972acdb468ac32a28e3e24c90694aff4b75206fc
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/29/2018
---
# <a name="admin-guide-configuring-and-using-document-tracking-for-azure-information-protection"></a>Guida dell'amministratore: configurazione e uso del rilevamento dei documenti per Azure Information Protection

>*Si applica a: Active Directory Rights Management Services, Azure Information Protection, Windows 10, Windows 8.1, Windows 8, Windows 7 con SP1, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2*

Se dispone di una [sottoscrizione che supporta il rilevamento dei documenti](https://www.microsoft.com/en-us/cloud-platform/azure-information-protection-features), il sito di rilevamento dei documenti è abilitato per impostazione predefinita per tutti gli utenti dell'organizzazione. Il rilevamento dei documenti fornisce informazioni, per utenti e amministratori, su quando si è verificato l'accesso a un documento protetto; se necessario, è possibile revocare un documento rilevato.

## <a name="privacy-controls-for-your-document-tracking-site"></a>Controlli sulla privacy per il sito di rilevamento dei documenti

Se la visualizzazione di tutte le informazioni di rilevamento dei documenti non è consentita all'interno dell'organizzazione a causa dei requisiti sulla privacy, è possibile disabilitare il rilevamento dei documenti tramite il cmdlet [Disable-AadrmDocumentTrackingFeature](/powershell/module/aadrm/disable-aadrmdocumenttrackingfeature). 

Questo cmdlet disabilita l'accesso al sito di rilevamento dei documenti impedendo a tutti gli utenti dell'organizzazione di rilevare o revocare l'accesso ai documenti protetti. È possibile riabilitare il rilevamento dei documenti in qualsiasi momento, tramite il cmdlet [Enable-AadrmDocumentTrackingFeature](/powershell/module/aadrm/enable-aadrmdocumenttrackingfeature) e si può verificare se il rilevamento dei documenti è attualmente abilitato o disabilitato usando [Get-AadrmDocumentTrackingFeature](/powershell/module/aadrm/get-aadrmdocumenttrackingfeature). Per eseguire questi cmdlet è necessario disporre almeno della versione **2.3.0.0** del modulo Azure Rights Management (AADRM) per PowerShell. 

Quando il sito di rilevamento dei documenti è abilitato, per impostazione predefinita vengono visualizzate informazioni quali gli indirizzi di posta elettronica delle persone che hanno tentato di accedere a documenti protetti, quando hanno tentato l'accesso e la loro posizione. Questo livello di informazioni può essere utile per determinare come vengono usati i documenti condivisi e se debbano essere revocati in caso di attività sospetta. Tuttavia, per motivi di privacy, potrebbe essere necessario disabilitare queste informazioni relative ad alcuni o tutti gli utenti. 

Se sono presenti utenti le cui attività non devono essere rilevate da altri utenti, aggiungerli a un gruppo archiviato in Azure AD e specificare il gruppo con il cmdlet [Set-AadrmDoNotTrackUserGroup](/powershell/module/aadrm/Set-AadrmDoNotTrackUserGroup). Quando si esegue questo cmdlet è necessario specificare un singolo gruppo, ma esso può contenere gruppi annidati. 

Gli utenti non possono vedere le attività dei membri di questo gruppo nel sito di rilevamento, quando queste attività sono correlate a documenti che hanno condiviso con loro. Inoltre non vengono inviate notifiche tramite posta elettronica all'utente che ha condiviso il documento.

Con questa configurazione tutti gli utenti possono comunque usare il sito di rilevamento dei documenti e revocare l'accesso ai documenti protetti, tuttavia non vedranno le attività degli utenti che sono stati specificati con il cmdlet Set-AadrmDoNotTrackUserGroup.

Questa impostazione influisce solo sugli utenti finali. Gli amministratori di Azure Information Protection possono sempre rilevare le attività di tutti gli utenti, anche quando sono stati specificati con Set-AadrmDoNotTrackUserGroup. Per altre informazioni su come gli amministratori possono rilevare i documenti per gli utenti, vedere la sezione [Rilevamento e revoca dei documenti per gli utenti](#tracking-and-revoking-documents-for-users).

Quando questa opzione non è più necessaria, si può usare il cmdlet [Clear-AadrmDoNotTrackUserGroup](/powershell/module/aadrm/Clear-AadrmDoNotTrackUserGroup). È possibile rimuovere in modo selettivo gli utenti eliminandoli dal gruppo, ma bisogna tenere in considerazione la [memorizzazione di gruppo nella cache](../plan-design/prepare.md#group-membership-caching-by-azure-information-protection). Si può controllare se questa opzione è attualmente in uso tramite [Get-AadrmDoNotTrackUserGroup](/powershell/module/aadrm/get-AadrmDoNotTrackUserGroup). Per eseguire i cmdlet per questa configurazione di gruppo è necessario disporre almeno della versione **2.10.0.0** del modulo Azure Rights Management (AADRM) per PowerShell.

Per altre informazioni su ciascuno di questi cmdlet, usare i collegamenti forniti. Per le istruzioni di installazione del modulo PowerShell, vedere [Installazione di Windows PowerShell per Azure Rights Management](../deploy-use/install-powershell.md). Se il modulo è già stato scaricato e installato, controllare il numero di versione eseguendo: `(Get-Module aadrm –ListAvailable).Version`


## <a name="destination-urls-used-by-the-document-tracking-site"></a>URL di destinazione utilizzati dal sito di rilevamento dei documenti

Gli URL seguenti vengono usati per il rilevamento dei documenti e devono essere consentiti su tutti i dispositivi e servizi tra i client che eseguono il client Azure Information Protection e Internet. Ad esempio, aggiungere gli URL ai firewall o ai siti attendibili se si usa Internet Explorer con protezione avanzata.

-  `https://*.azurerms.com`

- `https://*.microsoftonline.com`

- `https://*.microsoftonline-p.com`

- `https://ecn.dev.virtualearth.net`

Questi URL sono standard per il servizio Azure Rights Management, eccetto l'URL virtualearth.net utilizzato per le mappe Bing per mostrare la posizione dell'utente.

## <a name="tracking-and-revoking-documents-for-users"></a>Rilevamento e revoca dei documenti per gli utenti

Quando l'utente accede al sito di rilevamento dei documenti può rilevare e revocare i documenti che ha protetto tramite il client Azure Information Protection o condiviso tramite l'applicazione di condivisione di Rights Management. Quando si accede come amministratore di Azure Information Protection (amministratore globale), è possibile fare clic sull'icona di amministrazione per passare alla modalità di amministratore. Questa modalità consente di visualizzare i documenti che gli utenti dell'organizzazione hanno selezionato per il rilevamento mediante il client Azure Information Protection o condiviso tramite l'applicazione di condivisione di Rights Management:

![Icona di amministrazione nel sito di rilevamento dei documenti](../media/tracking-site-admin-icon.png)

> [!NOTE] 
> Se questa icona non compare per un amministratore globale, è perché l'amministratore non ha ancora condiviso documenti. In questo caso usare il seguente URL per accedere al sito di rilevamento dei documenti: https://portal.azurerms.com/#/admin

Le azioni eseguite in modalità amministratore vengono controllate e registrate nei file di log di utilizzo e per continuare è necessario confermare. Per altre informazioni su questa registrazione, vedere la sezione successiva.

Quando si è in modalità amministratore è possibile eseguire ricerche per utente o per documento. Se si esegue una ricerca per utente, si vedono tutti i documenti che l'utente ha selezionato per il rilevamento mediante il client Azure Information Protection o condiviso tramite l'applicazione di condivisione di Rights Management. 

Se si esegue una ricerca per documento, si vedono tutti gli utenti dell'organizzazione che hanno rilevato il documento mediante il client Azure Information Protection o l'hanno condiviso tramite l'applicazione di condivisione di Rights Management. È quindi possibile esaminare i risultati della ricerca per rilevare i documenti che gli utenti hanno protetto e revocare tali documenti se necessario. 

Per uscire dalla modalità amministratore, fare clic sulla **X** accanto a **Esci dalla modalità amministratore**:

![Uscire dalla modalità amministratore nel sito di rilevamento dei documenti](../media/tracking-site-exit-admin-icon.png)

Per istruzioni su come usare il sito di rilevamento dei documenti, vedere [Rilevare e revocare i documenti](client-track-revoke.md) nella Guida dell'utente.

## <a name="usage-logging-for-the-document-tracking-site"></a>Registrazione dell'utilizzo per il sito di rilevamento dei documenti

Due campi nei file di log di utilizzo riguardano il rilevamento dei documenti: **AdminAction** e **ActingAsUser**.

**AdminAction**: questo campo ha il valore true quando un amministratore usa il sito di rilevamento dei documenti in modalità amministratore, ad esempio per revocare un documento per conto di un utente o per vedere quando è stato condiviso. Il campo è vuoto quando l'utente accede al sito di rilevamento dei documenti.

**ActingAsUser**: quando il campo AdminAction è true, questo campo contiene il nome utente per conto del quale l'amministratore opera, ad esempio l'utente cercato o il proprietario del documento. Il campo è vuoto quando l'utente accede al sito di rilevamento dei documenti. 

Sono inoltre disponibili tipi di richiesta che registrano nel log informazioni su come utenti e amministratori usano il sito di rilevamento dei documenti. Ad esempio, **RevokeAccess** è il tipo di richiesta quando un utente o un amministratore per conto di un utente ha revocato un documento nel sito di rilevamento dei documenti. Usare questo tipo di richiesta in combinazione con il campo AdminAction per determinare se l'utente ha revocato un proprio documento (il campo AdminAction è vuoto) o un amministratore ha revocato un documento per conto dell'utente (il campo AdminAction è true).


Per altre informazioni sulla registrazione dell'utilizzo, vedere [Registrazione e analisi dell'utilizzo del servizio Azure Rights Management](../deploy-use/log-analyze-usage.md)



## <a name="next-steps"></a>Passaggi successivi
Dopo aver configurato il sito di rilevamento dei documenti per il client Azure Information Protection, vedere gli argomenti seguenti per altre informazioni che potrebbero essere necessarie per il supporto di questo client:

- [Personalizzazioni](client-admin-guide-customizations.md)

- [File client e registrazione dell'utilizzo](client-admin-guide-files-and-logging.md)

- [Tipi di file supportati](client-admin-guide-file-types.md)

- [Comandi di PowerShell](client-admin-guide-powershell.md)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
