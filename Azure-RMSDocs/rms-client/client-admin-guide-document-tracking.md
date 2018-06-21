---
title: Rilevamento dei documenti per Azure Information Protection
description: Istruzioni e informazioni per amministratori per configurare e usare il rilevamento dei documenti per Azure Information Protection.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 04/13/2018
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 983ecdc9-5631-48b8-8777-f4cbbb4934e8
ms.reviewer: eymanor
ms.suite: ems
ms.openlocfilehash: e24d91f04dc3186a9451546c8a962c49129f326b
ms.sourcegitcommit: affda7572064edaf9e3b63d88f4a18d0d6932b13
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/16/2018
ms.locfileid: "31008982"
---
# <a name="admin-guide-configuring-and-using-document-tracking-for-azure-information-protection"></a>Guida dell'amministratore: Configurazione e uso del rilevamento dei documenti per Azure Information Protection

>*Si applica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8, Windows 7 con SP1, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2*

Se si dispone di una [sottoscrizione che supporta il rilevamento dei documenti](https://www.microsoft.com/en-us/cloud-platform/azure-information-protection-features), il sito di rilevamento dei documenti è abilitato per impostazione predefinita per tutti gli utenti dell'organizzazione. Il rilevamento dei documenti consente di indicare a utenti e amministratori quando è stato eseguito l'accesso a un documento protetto e, se necessario, se è possibile revocare un documento rilevato.

## <a name="using-powershell-to-manage-the-document-tracking-site"></a>Uso di PowerShell per gestire il sito di rilevamento dei documenti

Le sezioni seguenti contengono informazioni su come gestire il sito di rilevamento dei documenti tramite PowerShell. Per le istruzioni di installazione del modulo PowerShell, vedere [Installazione del modulo PowerShell AADRM](../deploy-use/install-powershell.md). Se il modulo è stato scaricato e installato in precedenza, verificarne il numero di versione eseguendo: `(Get-Module aadrm –ListAvailable).Version`

Per altre informazioni su ognuno dei cmdlet, usare i relativi collegamenti.

### <a name="privacy-controls-for-your-document-tracking-site"></a>Controlli sulla privacy per il sito di rilevamento dei documenti

Se la visualizzazione di tutte le informazioni sul rilevamento dei documenti non è consentita nell'organizzazione a causa dei requisiti di privacy, è possibile disabilitare il rilevamento dei documenti usando il cmdlet [Disable-AadrmDocumentTrackingFeature](/powershell/module/aadrm/disable-aadrmdocumenttrackingfeature). 

Il cmdlet disabilita l'accesso al sito di rilevamento dei documenti in modo che tutti gli utenti dell'organizzazione non possano rilevare o revocare l'accesso ai documenti che hanno protetto. È possibile riabilitare il rilevamento dei documenti in qualsiasi momento usando [Enable-AadrmDocumentTrackingFeature](/powershell/module/aadrm/enable-aadrmdocumenttrackingfeature) e verificare se il rilevamento dei documenti è attualmente abilitato o disabilitato usando [Get-AadrmDocumentTrackingFeature](/powershell/module/aadrm/get-aadrmdocumenttrackingfeature). Per eseguire questi cmdlet, è necessario avere almeno la versione **2.3.0.0** del modulo AADRM per PowerShell. 

Quando è abilitato, il sito di rilevamento dei documenti visualizza, per impostazione predefinita, informazioni quali gli indirizzi di posta elettronica delle persone che hanno tentato di accedere ai documenti protetti, quando queste persone hanno tentato di accedere e la relativa posizione. Questo livello di informazioni può essere molto utile per determinare come vengono usati i documenti condivisi e se tali documenti devono essere revocati quando si rileva un'attività sospetta. Tuttavia, per motivi di privacy, può essere necessario disabilitare queste informazioni per alcuni o tutti gli utenti. 

Se per alcuni utenti questa attività non deve essere rilevata da altri, aggiungerli a un gruppo archiviato in Azure AD e specificare il gruppo con il cmdlet [Set-AadrmDoNotTrackUserGroup](/powershell/module/aadrm/Set-AadrmDoNotTrackUserGroup). Quando si esegue questo cmdlet è necessario specificare un singolo gruppo. Tuttavia, il gruppo può contenere gruppi nidificati. 

Per questi membri del gruppo, gli utenti non possono visualizzare attività nel sito di rilevamento dei documenti se queste ultime sono legate a documenti condivisi con loro. Inoltre, non vengono inviate notifiche di posta elettronica all'utente che ha condiviso il documento.

Quando si usa questa configurazione, tutti gli utenti possono comunque usare il sito di rilevamento dei documenti e revocare l'accesso ai documenti protetti. Tuttavia non visualizzano l'attività per gli utenti specificati usando il cmdlet Set-AadrmDoNotTrackUserGroup.

Questa impostazione si applica solo agli utenti finali. Gli amministratori di Azure Information Protection possono sempre tenere traccia delle attività di tutti gli utenti, anche quando vengono specificati usando Set-AadrmDoNotTrackUserGroup. Per altre informazioni su come gli amministratori possono tenere traccia dei per gli utenti, vedere la sezione [Rilevamento e revoca dei documenti per gli utenti](#tracking-and-revoking-documents-for-users).


### <a name="logging-information-from-the-document-tracking-site"></a>Informazioni di registrazione dal sito di rilevamento dei documenti

Quando si dispone almeno della versione **2.13.0.0** del modulo AADRM, è possibile usare i cmdlet seguenti per scaricare le informazioni di registrazione dal sito di rilevamento dei documenti:

- [Get-AadrmTrackingLog](/powershell/module/aadrm/Get-AadrmTrackingLog)
    
    Questo cmdlet restituisce informazioni di rilevamento sui documenti protetti per un utente specificato che ha protetto i documenti (emittente di Rights Management) o ha avuto accesso a documenti protetti. Usare questo cmdlet per rispondere alla domanda "A quali documenti protetti ha eseguito l'accesso un utente specificato o quali documenti protetti ha rilevato?"

- [Get-AadrmDocumentLog](/powershell/module/aadrm/Get-AadrmDocumentLog)
    
    Questo cmdlet restituisce informazioni di protezione sui documenti rilevati per un utente specificato se tale utente ha protetto documenti (emittente di Rights Management) o era proprietario di Rights Management per i documenti oppure se i documenti protetti erano configurati per consentire l'accesso direttamente all'utente. Usare questo cmdlet per rispondere alla domanda "In che modo sono protetti i documenti per un utente specificato?"
 
## <a name="destination-urls-used-by-the-document-tracking-site"></a>URL di destinazione usati dal sito di rilevamento dei documenti

Gli URL seguenti vengono usati per il rilevamento dei documenti e devono essere consentiti su tutti i dispositivi e servizi tra i client che eseguono il client Azure Information Protection e Internet. Ad esempio, aggiungere gli URL ai firewall o ai siti attendibili se si usa Internet Explorer con protezione avanzata.

-  `https://*.azurerms.com`

- `https://*.microsoftonline.com`

- `https://*.microsoftonline-p.com`

- `https://ecn.dev.virtualearth.net`

Questi URL sono standard per il servizio Azure Rights Management, ad eccezione dell'URL virtualearth.net usato nelle mappe di Bing per visualizzare la posizione dell'utente.

## <a name="tracking-and-revoking-documents-for-users"></a>Rilevamento e revoca dei documenti per gli utenti

Quando gli utenti accedono al sito di rilevamento dei documenti, possono rilevare e revocare i documenti protetti tramite il client Azure Information Protection o condivisi tramite l'applicazione di condivisione Rights Management. Quando si accede come amministratore di Azure Information Protection (amministratore globale), è possibile fare clic sull'icona di amministrazione per passare alla modalità amministratore. Questa modalità consente di visualizzare i documenti che gli utenti dell'organizzazione hanno selezionato per tenerne traccia con il client Azure Information Protection o per condividerli con l'applicazione di condivisione Rights Management:

![Icona di amministrazione nel sito di rilevamento dei documenti](../media/tracking-site-admin-icon.png)

> [!NOTE] 
> Se si è un amministratore globale e l'icona non è visibile, significa che non sono stati ancora condivisi documenti. In questo caso, usare l'URL seguente per accedere al sito di rilevamento dei documenti: https://portal.azurerms.com/#/admin

Le azioni intraprese in modalità amministratore vengono controllate e registrate nei file di log dei dati di utilizzo e, per continuare, è necessario confermare. Per altre informazioni su questa registrazione, vedere la sezione seguente.

Quando si è in modalità amministratore, è quindi possibile eseguire la ricerca in base all'utente o al documento. Se si esegue la ricerca per utente, è possibile visualizzare tutti i documenti che l'utente specificato ha selezionato per tenerne traccia con il client Azure Information Protection o per condividerli con l'applicazione di condivisione Rights Management. 

Se si esegue la ricerca per documento è possibile visualizzare tutti gli utenti dell'organizzazione che hanno tenuto traccia del documento con il client Azure Information Protection o che l'hanno condiviso con l'applicazione di condivisione Rights Management. È quindi possibile analizzare i risultati della ricerca per rilevare i documenti che gli utenti hanno protetto e revocarli se necessario. 

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

- [Personalizzazioni](client-admin-guide-customizations.md)

- [File del client e registrazione dell'utilizzo](client-admin-guide-files-and-logging.md)

- [Tipi di file supportati](client-admin-guide-file-types.md)

- [Comandi di PowerShell](client-admin-guide-powershell.md)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
