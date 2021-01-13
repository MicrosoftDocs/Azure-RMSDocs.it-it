---
title: Rilevamento dei documenti per Azure Information Protection
description: Istruzioni e informazioni per gli amministratori sulla configurazione e l'uso del rilevamento dei documenti per Azure Information Protection.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 03/16/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 983ecdc9-5631-48b8-8777-f4cbbb4934e8
ROBOTS: NOINDEX
ms.subservice: doctrack
ms.reviewer: eymanor
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: c8516ec14b5927eb21ad217a6c28d85eaa03b0b5
ms.sourcegitcommit: 78c7ab80be7c292ea4bc62954a4e29c449e97439
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/13/2021
ms.locfileid: "98164590"
---
# <a name="admin-guide-configuring-and-using-document-tracking-for-azure-information-protection-using-the-classic-client"></a>Guida dell'amministratore: configurazione e uso del rilevamento dei documenti per Azure Information Protection usando il client classico

>***Si applica a**: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8, Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012 *
>
>***Pertinente per**: [Azure Information Protection client classico per Windows](../faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients). Per il client di etichettatura unificata, vedere la [Guida dell'amministratore del client Unified Labeling](track-and-revoke-admin.md). *

> [!NOTE] 
> Per offrire un'esperienza per i clienti unificata e semplificata, il **client classico di Azure Information Protection** e **Gestione etichette** nel portale di Azure saranno **deprecati** a partire dal **31 marzo 2021**. In questo intervallo di tempo tutti i clienti correnti di Azure Information Protection possono passare alla soluzione di etichettatura unificata usando la piattaforma di etichettatura unificata di Microsoft Information Protection. Altre informazioni nell'[avviso ufficiale sulla deprecazione](https://aka.ms/aipclassicsunset).

Se si dispone di una [sottoscrizione che supporta il rilevamento dei documenti](https://www.microsoft.com/cloud-platform/azure-information-protection-features) e il client AIP classico, il sito di rilevamento dei documenti è abilitato per impostazione predefinita per tutti gli utenti dell'organizzazione. Il rilevamento dei documenti fornisce informazioni, per utenti e amministratori, su quando si è verificato l'accesso a un documento protetto; se necessario, è possibile revocare un documento rilevato.

## <a name="using-powershell-to-manage-the-document-tracking-site"></a>Uso di PowerShell per gestire il sito di rilevamento dei documenti

Le sezioni seguenti contengono informazioni su come gestire il sito di rilevamento dei documenti tramite PowerShell. Per le istruzioni di installazione per il modulo PowerShell, vedere [installazione del modulo PowerShell AIPService](../install-powershell.md).

Per altre informazioni su ognuno dei cmdlet, usare i relativi collegamenti.

### <a name="privacy-controls-for-your-document-tracking-site"></a>Controlli sulla privacy per il sito di rilevamento dei documenti

Se la visualizzazione di tutte le informazioni di rilevamento dei documenti non è consentita nell'organizzazione a causa dei requisiti sulla privacy, è possibile disabilitare il rilevamento dei documenti tramite il cmdlet [Disable-AipServiceDocumentTrackingFeature](/powershell/module/aipservice/disable-aipservicedocumenttrackingfeature) . 

Questo cmdlet disabilita l'accesso al sito di rilevamento dei documenti impedendo a tutti gli utenti dell'organizzazione di rilevare o revocare l'accesso ai documenti protetti. È possibile riabilitare il rilevamento dei documenti in qualsiasi momento usando [Enable-AipServiceDocumentTrackingFeature](/powershell/module/aipservice/enable-aipservicedocumenttrackingfeature)ed è possibile verificare se il rilevamento dei documenti è attualmente abilitato o disabilitato usando [Get-AipServiceDocumentTrackingFeature](/powershell/module/aipservice/get-aipservicedocumenttrackingfeature). 

Quando il sito di rilevamento dei documenti è abilitato, per impostazione predefinita vengono visualizzate informazioni quali gli indirizzi di posta elettronica delle persone che hanno tentato di accedere a documenti protetti, quando hanno tentato l'accesso e la loro posizione. Questo livello di informazioni può essere utile per determinare come vengono usati i documenti condivisi e se debbano essere revocati in caso di attività sospetta. Tuttavia, per motivi di privacy, potrebbe essere necessario disabilitare queste informazioni relative ad alcuni o tutti gli utenti. 

Se sono presenti utenti che non devono avere questa attività rilevata da altri utenti, aggiungerli a un gruppo archiviato in Azure AD e specificare il gruppo con il cmdlet [set-AipServiceDoNotTrackUserGroup](/powershell/module/aipservice/Set-AipServiceDoNotTrackUserGroup) . Quando si esegue questo cmdlet è necessario specificare un singolo gruppo, ma esso può contenere gruppi annidati. 

Gli utenti non possono vedere le attività dei membri di questo gruppo nel sito di rilevamento, quando queste attività sono correlate a documenti che hanno condiviso con loro. Inoltre non vengono inviate notifiche tramite posta elettronica all'utente che ha condiviso il documento.

Con questa configurazione tutti gli utenti possono comunque usare il sito di rilevamento dei documenti e revocare l'accesso ai documenti protetti, Tuttavia, non visualizzano l'attività per gli utenti specificati tramite il cmdlet Set-AipServiceDoNotTrackUserGroup.

Questa impostazione influisce solo sugli utenti finali. Gli amministratori di Azure Information Protection possono sempre tenere traccia delle attività di tutti gli utenti, anche quando tali utenti vengono specificati tramite set-AipServiceDoNotTrackUserGroup. Per altre informazioni su come gli amministratori possono rilevare i documenti per gli utenti, vedere la sezione [Rilevamento e revoca dei documenti per gli utenti](#tracking-and-revoking-documents-for-users).


### <a name="logging-information-from-the-document-tracking-site"></a>Informazioni di registrazione dal sito di rilevamento dei documenti

È possibile utilizzare i cmdlet seguenti per scaricare le informazioni di registrazione dal sito di rilevamento dei documenti:

- [Get-AipServiceTrackingLog](/powershell/module/aipservice/Get-AipServiceTrackingLog)
    
    Questo cmdlet restituisce informazioni di rilevamento sui documenti protetti per un utente specificato che ha protetto i documenti (emittente di Rights Management) o ha avuto accesso a documenti protetti. Usare questo cmdlet per rispondere alla domanda "A quali documenti protetti ha eseguito l'accesso un utente specificato o quali documenti protetti ha rilevato?"

- [Get-AipServiceDocumentLog](/powershell/module/aipservice/Get-AipServiceDocumentLog)
    
    Questo cmdlet restituisce informazioni di protezione sui documenti rilevati per un utente specificato se tale utente ha protetto documenti (emittente di Rights Management) o era proprietario di Rights Management per i documenti oppure se i documenti protetti erano configurati per consentire l'accesso direttamente all'utente. Usare questo cmdlet per rispondere alla domanda "In che modo sono protetti i documenti per un utente specificato?"

## <a name="destination-urls-used-by-the-document-tracking-site"></a>URL di destinazione utilizzati dal sito di rilevamento dei documenti

Gli URL seguenti vengono usati per il rilevamento dei documenti e devono essere consentiti su tutti i dispositivi e i servizi tra i client che eseguono il client Azure Information Protection e Internet. Ad esempio, aggiungere gli URL ai firewall o ai siti attendibili se si usa Internet Explorer con protezione avanzata.

-  `https://*.azurerms.com`

- `https://*.microsoftonline.com`

- `https://*.microsoftonline-p.com`

- `https://ecn.dev.virtualearth.net`

Questi URL sono standard per il servizio Azure Rights Management, eccetto l'URL virtualearth.net utilizzato per le mappe Bing per mostrare la posizione dell'utente.

## <a name="tracking-and-revoking-documents-for-users"></a>Rilevamento e revoca dei documenti per gli utenti

Quando gli utenti accedono al sito di rilevamento dei documenti, possono rilevare e revocare i documenti protetti tramite il client Azure Information Protection. Quando si accede come amministratore di globale di Azure AD per il tenant, è possibile fare clic sull'icona di amministrazione per passare alla modalità amministratore. Gli altri ruoli di amministratore non supportano questa modalità per il sito di rilevamento dei documenti. 

![Icona di amministrazione nel sito di rilevamento dei documenti](../media/tracking-site-admin-icon.png)

La modalità amministratore consente di visualizzare i documenti che gli utenti dell'organizzazione hanno selezionato per tenerne traccia con il client Azure Information Protection.

> [!NOTE] 
> Se si è un amministratore globale e l'icona non è visibile, significa che non sono stati ancora condivisi documenti. In questo caso, usare l'URL seguente per accedere al sito di rilevamento dei documenti: https://portal.azurerms.com/#/admin

Le azioni eseguite in modalità amministratore vengono controllate e registrate nei file di log di utilizzo e per continuare è necessario confermare. Per altre informazioni su questa registrazione, vedere la sezione successiva.

Quando si è in modalità amministratore è possibile eseguire ricerche per utente o per documento. Se si esegue la ricerca per utente, vengono visualizzati tutti i documenti che l'utente specificato ha selezionato per tenerne traccia con il client Azure Information Protection. 

Se si esegue la ricerca per documento, vengono visualizzati tutti gli utenti dell'organizzazione che hanno tenuto traccia del documento con il client Azure Information Protection. È quindi possibile esaminare i risultati della ricerca per rilevare i documenti che gli utenti hanno protetto e revocare tali documenti se necessario. 

Per uscire dalla modalità amministratore, fare clic sulla **X** accanto a **Esci dalla modalità amministratore**:

![Uscire dalla modalità amministratore nel sito di rilevamento dei documenti](../media/tracking-site-exit-admin-icon.png)

Per istruzioni su come usare il sito di rilevamento dei documenti, vedere [Rilevare e revocare i documenti](client-track-revoke.md) nella Guida dell'utente.

### <a name="using-powershell-to-register-labeled-documents-with-the-document-tracking-site"></a>Uso di PowerShell per registrare i documenti etichettati nel sito di rilevamento dei documenti

Per poter rilevare e revocare un documento, è prima necessario registrarlo nel sito di rilevamento dei documenti. Questa azione si verifica quando gli utenti selezionano l'opzione **Rileva e revoca** da Esplora file o dalle app di Office quando usano il client Azure Information Protection.

Se si etichettano e proteggono i file per gli utenti usando il cmdlet [Set-AIPFileLabel](/powershell/azureinformationprotection/vlatest/set-aipfilelabel), è possibile usare il parametro *EnableTracking* per registrare il file nel sito di rilevamento dei documenti. Ad esempio:

```ps
Set-AIPFileLabel -Path C:\Projects\ -LabelId ade72bf1-4714-4714-4714-a325f824c55a -EnableTracking
```

## <a name="usage-logging-for-the-document-tracking-site"></a>Registrazione dell'utilizzo per il sito di rilevamento dei documenti

Due campi nei file di log di utilizzo riguardano il rilevamento dei documenti: **AdminAction** e **ActingAsUser**.

**AdminAction**: questo campo ha il valore true quando un amministratore usa il sito di rilevamento dei documenti in modalità amministratore, ad esempio per revocare un documento per conto di un utente o per vedere quando è stato condiviso. Il campo è vuoto quando l'utente accede al sito di rilevamento dei documenti.

**ActingAsUser**: quando il campo AdminAction è true, questo campo contiene il nome utente per conto del quale l'amministratore opera, ad esempio l'utente cercato o il proprietario del documento. Il campo è vuoto quando l'utente accede al sito di rilevamento dei documenti. 

Sono inoltre disponibili tipi di richiesta che registrano nel log informazioni su come utenti e amministratori usano il sito di rilevamento dei documenti. Ad esempio, **RevokeAccess** è il tipo di richiesta quando un utente o un amministratore per conto di un utente ha revocato un documento nel sito di rilevamento dei documenti. Usare questo tipo di richiesta in combinazione con il campo AdminAction per determinare se l'utente ha revocato un proprio documento (il campo AdminAction è vuoto) o un amministratore ha revocato un documento per conto dell'utente (il campo AdminAction è true).

Per ulteriori informazioni sulla registrazione dell'utilizzo, vedere [registrazione e analisi dell'utilizzo della protezione da Azure Information Protection](../log-analyze-usage.md)

## <a name="next-steps"></a>Passaggi successivi
Dopo aver configurato il sito di rilevamento dei documenti per il client Azure Information Protection, vedere gli argomenti seguenti per altre informazioni che potrebbero essere necessarie per il supporto di questo client:

- [Personalizzazioni](client-admin-guide-customizations.md)

- [File del client e registrazione dell'utilizzo](client-admin-guide-files-and-logging.md)

- [Tipi di file supportati](client-admin-guide-file-types.md)

- [Comandi di PowerShell](client-admin-guide-powershell.md)

