---
title: Client di Azure Information Protection&colon; cronologia delle versioni e criteri per il supporto
description: Informazioni sugli elementi nuovi o modificati in una versione del client di Azure Information Protection per Windows e sui criteri del ciclo di vita per il supporto.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 12/22/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 6ebd0ca3-1864-4b3d-bb3e-a168eee5eb1d
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 20ee380a48fa8fb303a5c71f43df17b8740b0cb4
ms.sourcegitcommit: fc9a4487e2a0bc3481a814c7c308939868d52db9
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/21/2017
---
# <a name="azure-information-protection-client-version-release-history-and-support-policy"></a>Client di Azure Information Protection: cronologia delle versioni e criteri per il supporto

>*Si applica a: Azure Information Protection*

Il team di Azure Information Protection aggiorna regolarmente il client di Azure Information Protection con correzioni e nuove funzionalità. 

È possibile scaricare la versione disponibile a livello generale più recente e la versione di anteprima corrente dall'[Area download Microsoft](https://www.microsoft.com/en-us/download/details.aspx?id=53018). Queste versioni sono incluse anche nel catalogo di Microsoft Update (categoria: **Azure Information Protection**), in modo da poter distribuire il client tramite WSUS o Configuration Manager o altri meccanismi di distribuzione di software che usano Microsoft Update.

### <a name="servicing-information-and-timelines"></a>Informazioni e tempistiche di manutenzione

Ogni versione con disponibilità generale del client di Azure Information Protection è supportata per un massimo di sei mesi dopo il rilascio della versione con disponibilità generale successiva. Le versioni del client non supportate non sono incluse in questa pagina. Le correzioni e le nuove funzionalità sono sempre valide per l'ultima versione disponibile a livello generale e non verranno applicate alle versioni precedenti.

Le versioni di anteprima non devono essere distribuite agli utenti finali nelle reti di produzione, ma è possibile usare la versione di anteprima più recente per visualizzare e provare le nuove funzionalità e correzioni che saranno disponibili nella prossima versione disponibile a livello generale. Non sono supportate le versioni di anteprima non aggiornate.

### <a name="release-history"></a>Cronologia delle versioni

Usare le informazioni seguenti per scoprire le novità o le modifiche per una versione supportata del client di Azure Information Protection per Windows. La versione più recente è elencata per prima. 

> [!NOTE]
> Dato che le correzioni di minore rilevanza non sono elencate, se si verifica un problema con il client di Azure Information Protection, è consigliabile controllare se tale problema è stato risolto con la versione disponibile a livello generale più recente. Se il problema persiste, verificare la versione di anteprima corrente.
>  
> Per il supporto tecnico, vedere le informazioni riportate in [Opzioni di supporto e risorse per la community](../get-started/information-support.md#support-options-and-community-resources). È anche possibile rivolgersi al team di Azure Information Protection nel [sito di Yammer](https://www.yammer.com/askipteam/).

## <a name="versions-later-than-110560"></a>Versioni successive alla versione 1.10.56.0

Se si usa una versione del client successiva alla versione 1.10.56.0, si tratta di una build di anteprima per scopi di testing e valutazione. 

Per informazioni sulle novità o sulle modifiche della versione di anteprima corrente dall'ultima versione di disponibilità generale del client, vedere la sezione **Dettagli** nella [pagina di download](https://www.microsoft.com/en-us/download/details.aspx?id=53018). 

## <a name="version-110560"></a>Versione 1.10.56.0

**Data di rilascio**: 18/09/2017

Questa versione include MSIPC versione 1.0.3219.0619 del client RMS.

**Nuove funzionalità**:

- Supporto per le nuove condizioni di prevenzione della perdita dei dati (DLP) di Office 365 che è possibile configurare per un'etichetta. Per altre informazioni, vedere [Configurare le condizioni per un'etichetta di Azure Information Protection](../deploy-use/configure-policy-classification.md).

- Supporto per le etichette configurate per le azioni definite dall'utente. Per Outlook, questa etichetta si applica automaticamente all'opzione Non inoltrare di Outlook. Per Word, Excel, PowerPoint ed Esplora file, questa etichetta richiede all'utente di specificare autorizzazioni personalizzate. Per altre informazioni, vedere [Configurare un'etichetta di Azure Information Protection per la protezione](../deploy-use/configure-policy-protection.md).

- Le etichette supportano più lingue. A partire da 30 agosto 2017, i [criteri predefiniti](../deploy-use/configure-policy-default.md) includono il supporto per più lingue, visualizzate agli utenti in questa versione del client. Per visualizzare le etichette nella lingua preferita dai criteri predefiniti prima di questa data e per le etichette configurate, vedere [Come configurare etichette per lingue diverse in Azure Information Protection](../deploy-use/configure-policy-languages.md).

- Le etichette vengono visualizzate dal pulsante **Proteggi** sulla barra multifunzione di Office, oltre a essere visualizzate sulla barra di Information Protection. 

- Protezione nativa per tipi di file Visio seguenti con estensione vsdm,vsdx, vssm, vssx, vstm e vstx

- Supporto per configurazioni client avanzate che è possibile configurare nel portale di Azure. Le configurazioni comprendono:
    
    - [Nascondere o visualizzare il pulsante Non inoltrare in Outlook](../rms-client/client-admin-guide-customizations.md#hide-or-show-the-do-not-forward-button-in-outlook)
    
    - [Rendere disponibili o non disponibili agli utenti le opzioni relative alle autorizzazioni personalizzate](../rms-client/client-admin-guide-customizations.md#make-the-custom-permissions-options-available-or-unavailable-to-users)
    
    - [Nascondere in modo permanente la barra di Azure Information Protection](../rms-client/client-admin-guide-customizations.md#permanently-hide-the-azure-information-protection-bar)
    
    - [Abilitare la classificazione consigliata in Outlook](../rms-client/client-admin-guide-customizations.md#enable-recommended-classification-in-outlook)

- Per PowerShell, supporto per assegnare un'etichetta ai file in modo non interattivo usando i nuovi cmdlet di PowerShell, [Set-AIPAuthentication](/powershell/module/azureinformationprotection/set-aipauthentication) e [Clear-AIPAuthentication](/powershell/module/azureinformationprotection/clear-aipauthentication). Per altre informazioni su come usare questi cmdlet, vedere la [sezione relativa a PowerShell](../rms-client/client-admin-guide-powershell.md#how-to-label-files-non-interactively-for-azure-information-protection) della guida dell'amministratore.

- Per i cmdlet di PowerShell, [Set-AIPFileLabel](/powershell/module/azureinformationprotection/set-aipfilelabel) e [Set-AIPFileClassification](/powershell/module/azureinformationprotection/set-aipfileclassification), sono disponibili nuovi parametri: **Owner** e **PreserveFileDetails**. Questi parametri consentono di specificare un indirizzo e-mail per la proprietà personalizzata Owner, lasciando invariata la data per i documenti a cui è assegnata un'etichetta.

**Correzioni**:

Correzioni per la stabilità e per scenari specifici che includono:

- Supporto per la protezione generica di file di grandi dimensioni che in precedenza potevano essere causa di danneggiamento se di dimensioni maggiori di 1 GB. Attualmente le dimensioni dei file sono limitate solo dallo spazio disponibile su disco e dalla memoria disponibile. Per altre informazioni sulle limitazioni relative alle dimensioni dei file, vedere [Dimensioni dei file supportati per la protezione](client-admin-guide-file-types.md#file-sizes-supported-for-protection) della guida dell'amministratore.

- Il visualizzatore del client Azure Information Protection consente di aprire file PDF protetti (con estensione ppdf) come file disponibili solo per la visualizzazione.

- Supporto per l'assegnazione di etichette e la protezione dei file archiviati in SharePoint Server.

- Le filigrane supportano ora più righe. Inoltre, i contrassegni visivi vengono ora applicati a un documento [solo al primo salvataggio](../deploy-use/configure-policy-markings.md#when-visual-markings-are-applied) anziché ogni volta che un documento viene salvato.

- L'opzione **Esegui diagnostica** nella finestra di dialogo **Guida e commenti** viene sostituita da **Ripristina le impostazioni**. Il comportamento per questa azione è stato modificato in modo da includere la disconnessione dell'utente e l'eliminazione dei criteri di Azure Information Protection. Per altre informazioni, vedere la sezione contenente [altre informazioni sull'opzione Ripristina le impostazioni](..\rms-client\client-admin-guide.md#more-information-about-the-reset-settings-option) della guida dell'amministratore.

- Supporto per l'autenticazione proxy.

Correzioni per una migliore esperienza utente, che includono:

- Convalida e-mail quando gli utenti specificano autorizzazioni personalizzate. Inoltre, è ora possibile specificare più indirizzi e-mail premendo INVIO.

- L'etichetta padre non viene visualizzata quando tutte le relative etichette secondarie sono configurate per la protezione e il client non dispone di un'edizione di Office che supporta la protezione. 

## <a name="version-172100"></a>Versione 1.7.210.0

**Rilasciata**: 06/06/2017

Questa versione include MSIPC versione 1.0.2217.1 del client RMS.

**Nuove funzionalità**:

- Nuovo cmdlet di PowerShell [Set-AIPFileClassification](/powershell/module/azureinformationprotection/Set-AIPFileClassification). Quando viene eseguito, questo cmdlet controlla il contenuto dei file e applica automaticamente le etichette ai file senza etichetta, in base alle condizioni specificate nei criteri di Azure Information Protection.

**Correzioni**:

- Tutti i cmdlet di classificazione e assegnazione di etichette sono ora supportati nei computer che non sono connessi a Internet ma usano criteri validi di Azure Information Protection.

- Per coerenza, un parametro di output del cmdlet [Get-AIPFileStatus](/powershell/module/azureinformationprotection/get-aipfilestatus) viene modificato da inglese britannico (**IsLabelled**) a inglese americano (**IsLabeled**). Se si usano script o processi automatizzati che cercano questo parametro, aggiornare l'ortografia del parametro.

- Correzioni generale per la stabilità che includono:

    - Per Outlook: correzioni di arresti anomali del sistema, uso elevato della memoria e problemi di visualizzazione per i menu.
    
    - Per Word, Excel e PowerPoint: correzioni di uso elevato della CPU, problemi di visualizzazione durante il salvataggio di file di Excel di grandi dimensioni o applicazioni che non rispondono. 
    
    Anche per queste applicazioni, per migliorare le prestazioni per Office 2016 con SharePoint Online e OneDrive for Business, l'assegnazione di etichette automatica e consigliata viene applicata quando si chiude il file anziché quando si salva il file (salvataggio automatico o selezionato dall'utente). Analogamente, se è abilitata l'impostazione che richiede l'**assegnazione di un'etichetta a tutti i documenti e messaggi di posta elettronica**, agli utenti non viene chiesto di selezionare un'etichetta finché il file non viene chiuso. L'eccezione è per Word 2016 ed Excel 2016 e l'utente seleziona l'opzione **Salva con nome**. Quindi, questa azione attiva i comportamenti relativi alle etichette, se sono configurati. 

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sull'installazione e l'uso del client: 

- Per utenti: [Scaricare e installare il client](install-client-app.md)

- Per amministratori: [Guida per l'amministratore del client di Azure Information Protection](client-admin-guide.md)


[!INCLUDE[Commenting house rules](../includes/houserules.md)]
