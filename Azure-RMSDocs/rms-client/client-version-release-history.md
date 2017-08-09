---
title: Client di Azure Information Protection&colon; cronologia delle versioni
description: Informazioni sugli elementi nuovi o modificati in una versione del client di Azure Information Protection per Windows.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 06/08/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 6ebd0ca3-1864-4b3d-bb3e-a168eee5eb1d
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 28b7c2f8bbd058251f4edfd93b2fee181bd4d339
ms.sourcegitcommit: ebf396cbe8eabed720b317f131884fe9f23b8691
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/29/2017
---
# <a name="azure-information-protection-client-version-release-history"></a>Client di Azure Information Protection: cronologia delle versioni

>*Si applica a: Azure Information Protection*

Il team di Azure Information Protection aggiorna regolarmente il client di Azure Information Protection con correzioni e nuove funzionalità. Il client è incluso nel Microsoft Update Catalog (categoria **Azure Information Protection**) ed è sempre possibile scaricare la versione di disponibilità generale più recente e la prossima versione (la versione di anteprima) dall'[Area download Microsoft](https://www.microsoft.com/en-us/download/details.aspx?id=53018).

Le versioni di anteprima non devono essere distribuite agli utenti finali nelle reti di produzione, ma possono essere usate per visualizzare e provare le nuove funzionalità e correzioni che saranno disponibili nella prossima versione di disponibilità generale. 

Usare le informazioni seguenti per visualizzare gli elementi nuovi o modificati di una versione di disponibilità generale. La versione più recente è elencata per prima. Per informazioni sulla versione di anteprima corrente, vedere le informazioni riportate nella pagina di download.

> [!NOTE]
> Poiché le correzioni di minore rilevanza non sono elencate, se si verifica un problema con il client di Azure Information Protection, controllare prima che tale problema non riguardi la versione di disponibilità generale più recente. In caso affermativo, verificare la versione di anteprima corrente.
>  
> Se il problema persiste, vedere le informazioni contenute in [Opzioni di supporto e risorse della community](../get-started/information-support.md#support-options-and-community-resources). È anche possibile rivolgersi al team di Azure Information Protection nel [sito di Yammer](https://www.yammer.com/askipteam/).


## <a name="version-172100"></a>Versione 1.7.210.0

**Rilasciata**: 06/06/2017

Questa versione include MSIPC versione 1.0.2217.1 del client RMS.

**Correzioni**:

- Tutti i cmdlet di classificazione e assegnazione di etichette sono ora supportati nei computer che non sono connessi a Internet ma usano criteri validi di Azure Information Protection.

- Per coerenza, un parametro di output del cmdlet [Get-AIPFileStatus](/powershell/module/azureinformationprotection/get-aipfilestatus) viene modificato da inglese britannico (**IsLabelled**) a inglese americano (**IsLabeled**). Se si usano script o processi automatizzati che cercano questo parametro, aggiornare l'ortografia del parametro.

- Correzioni generale per la stabilità che includono:

    - Per Outlook: correzioni di arresti anomali del sistema, uso elevato della memoria e problemi di visualizzazione per i menu.
    
    - Per Word, Excel e PowerPoint: correzioni di uso elevato della CPU, problemi di visualizzazione durante il salvataggio di file di Excel di grandi dimensioni o applicazioni che non rispondono. 
    
    Anche per queste applicazioni, per migliorare le prestazioni per Office 2016 con SharePoint Online e OneDrive for Business, l'assegnazione di etichette automatica e consigliata viene applicata quando si chiude il file anziché quando si salva il file (salvataggio automatico o selezionato dall'utente). Analogamente, se è abilitata l'impostazione che richiede l'assegnazione di un'**etichetta a tutti i documenti e messaggi di posta elettronica**, agli utenti non verrà chiesto di selezionare un'etichetta finché il file non viene chiuso. L'eccezione è per Word 2016 ed Excel 2016 e l'utente seleziona l'opzione **Salva con nome**. Quindi, questa azione attiva i comportamenti relativi alle etichette, se sono configurati. 

**Nuove funzionalità**:

- Nuovo cmdlet di PowerShell [Set-AIPFileClassification](/powershell/module/azureinformationprotection/Set-AIPFileClassification). Quando viene eseguito, questo cmdlet controlla il contenuto dei file e applica automaticamente le etichette ai file senza etichetta, in base alle condizioni specificate nei criteri di Azure Information Protection.


## <a name="version-14210"></a>Versione 1.4.21.0

**Data di rilascio**: 15/03/2017

**Modifica dei requisiti:**

La versione precedente ha introdotto il nuovo prerequisito di Microsoft .NET Framework 4.6.2 per il client completo. Anche se non è consigliabile, è possibile ignorare questo prerequisito con il parametro di installazione personalizzata **DowngradeDotNetRequirement**. Per altre informazioni, vedere la [sezione relativa all'installazione del client](client-admin-guide.md#how-to-install-the-azure-information-protection-client-for-users) nella Guida dell'amministratore.


**Correzioni**:

- Supporto per le unità mappate per classificare e proteggere i file.

- Supporto per file di grandi dimensioni (>250 MB) nel visualizzatore. 

- Quando è configurata la modalità HYOK, Outlook può applicare etichette configurate per l'uso di modelli di Azure Rights Management o AD RMS.


**Nuove funzionalità**:

- Possibilità di impostare autorizzazioni personalizzate dall'applicazione di Office, in modo da definire impostazioni di protezione personali, per gruppi esterni o per tutti gli utenti di un'altra organizzazione. Per altre informazioni, vedere [Impostare autorizzazioni personalizzate per un documento](client-classify-protect.md#set-custom-permissions-for-a-document) nella Guida dell'utente.
    
- I file PDF supportano ora etichette che applicano solo la classificazione.

- Per i file PDF, il visualizzatore supporta ora opzioni che consentono di eseguire varie operazioni, come la ricerca, lo zoom e la rotazione. Per usare queste opzioni, fare clic con il pulsante destro del mouse sul file quando viene aperto nel visualizzatore.


## <a name="version-131552"></a>Versione 1.3.155.2

**Data di rilascio**: 08/02/2017

**Nuovi requisiti**:

Microsoft .NET Framework

- Questa versione del client Azure Information Protection richiede Microsoft .NET Framework 4.6.2 come versione minima. Se questo non è presente, il programma di installazione prova a scaricarlo e installarlo. Al termine dell'installazione del client Azure Information Protection, potrebbe essere necessario riavviare il computer.

- Se il visualizzatore Azure Information Protection viene installato separatamente, è necessario Microsoft .NET Framework 4.5.2 come versione minima. Se questo non è presente, il programma di installazione non lo scarica e installa.

**Nuove funzionalità**:

- Nuovo client unificato che riunisce le funzionalità dell'applicazione di condivisione Rights Management per Windows e il client Azure Information Protection. Include:
    
    - Integrazione con Esplora file (clic con il pulsante destro del mouse) per l'applicazione di etichette e protezione. Supporta altri formati di file e la selezione di più file.
    - Un visualizzatore per documenti protetti (include PDF protetti per SharePoint).
    - Cmdlet di PowerShell per ottenere e impostare etichette per i file archiviati in locale o in condivisioni di rete. Questi cmdlet vengono installati con i cmdlet forniti in precedenza con lo strumento di protezione RMS (modulo RMSProtection).
    - Log di utilizzo del client che registrano informazioni, ad esempio su quale etichetta è stata applicata, come e da chi.

Questa versione del client è la [versione con disponibilità generale](https://blogs.technet.microsoft.com/enterprisemobility/2017/02/08/azure-information-protection-december-update-moves-to-general-availability/) del client in anteprima annunciato per la prima volta nel mese di dicembre 2016. Per altre informazioni su questa versione del client, vedere le guide seguenti:

- [Guida per l'amministratore del client di Azure Information Protection](client-admin-guide.md)

- [Guida per l'utente di Azure Information Protection](client-user-guide.md)


## <a name="version-1240"></a>Versione 1.2.4.0

**Data di rilascio**: 27/10/2016

**Correzioni**:

- L'installazione del client viene completata quando il servizio Windows Update è disattivato.

- In Office 2016, quando si salva un documento ed è configurata un'etichetta per un'intestazione o un piè di pagina, il cursore non passa all'intestazione o al piè di pagina.

- La classificazione automatica funziona in Word per il testo nelle caselle di testo combinate.

**Nuove funzionalità**:

- Opzione per test diagnostici e ripristino che l'utente può eseguire dall'applicazione di Office quando è installato il client di Azure Information Protection: nel gruppo **Protezione** della scheda **Home** fare clic su **Proteggi**, scegliere **Guida e commenti e suggerimenti** e quindi **Esegui diagnostica**. 

    Per altre informazioni su questa opzione, vedere la sezione [Controlli aggiuntivi e risoluzione dei problemi](client-admin-guide.md#additional-checks-and-troubleshooting) nella Guida dell'amministratore.

## <a name="version-11230"></a>Versione 1.1.23.0

**Data di rilascio**: 01/10/2016

Disponibilità generale.

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sull'installazione e l'uso del client:

- Per utenti: [Scaricare e installare il client](install-client-app.md)

- Per amministratori: [Guida per l'amministratore del client di Azure Information Protection](client-admin-guide.md)


[!INCLUDE[Commenting house rules](../includes/houserules.md)]