---
title: Client Azure Information Protection - criteri di supporto & Cronologia versione
description: Informazioni sugli elementi nuovi o modificati in una versione del client di Azure Information Protection per Windows e sui criteri del ciclo di vita per il supporto.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 05/31/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 4d1da800b43ecfc3fcb91881dc5462e4758ffbb7
ms.sourcegitcommit: aa13e56ae0ff0dea79e83335a6ecaf45e34e9d8c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/02/2019
ms.locfileid: "66458232"
---
# <a name="azure-information-protection-client-version-release-history-and-support-policy"></a>Client Azure Information Protection: Cronologia delle versioni e criteri per il supporto

>*Si applica a: Active Directory Rights Management Services, [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8, Windows 7 con SP1, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2*
>
> *Istruzioni per: [Client Azure Information Protection per Windows](../faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*

Il team di Azure Information Protection aggiorna regolarmente il client di Azure Information Protection con correzioni e nuove funzionalità. 

È possibile scaricare la versione disponibile a livello generale più recente e la versione di anteprima corrente (se disponibile) dall'[Area download Microsoft](https://www.microsoft.com/en-us/download/details.aspx?id=53018). 

Dopo un breve intervallo di in genere un paio di settimane, la versione di disponibilità generale più recente è anche inclusa in Microsoft Update Catalog con il nome del prodotto **Microsoft Azure Information Protection**  >  **Client di Microsoft Azure Information Protection**e la classificazione dei **aggiornamenti**. L'inserimento nel catalogo significa che è possibile aggiornare il client tramite WSUS o Configuration Manager o altri meccanismi di distribuzione del software che usano Microsoft Update.

Per altre informazioni, vedere [Aggiornamento e gestione del client Azure Information Protection](client-admin-guide.md#upgrading-and-maintaining-the-azure-information-protection-client).

> [!TIP]
> Interessati all'uso di Azure Information Protection unified imprevisto delle etichette client perché le etichette vengono pubblicate dalla protezione di Office 365 e centro conformità, Centro sicurezza di Microsoft 365 o centro conformità di Microsoft 365? Quando si scarica e quindi installare il client di assegnazione di etichette unificato da Microsoft Download Center, è possibile aggiornare il client Azure Information Protection a ciò [client unificato di assegnazione di etichette](unifiedlabelingclient-version-release-history.md).

### <a name="servicing-information-and-timelines"></a>Informazioni e tempistiche di manutenzione

Ogni versione con disponibilità generale del client di Azure Information Protection è supportata per un massimo di sei mesi dopo il rilascio della versione con disponibilità generale successiva. La documentazione non include informazioni sulle versioni non supportate del client. Le correzioni e le nuove funzionalità sono sempre valide per l'ultima versione disponibile a livello generale e non verranno applicate alle versioni precedenti.

Le versioni di anteprima non devono essere distribuite agli utenti finali nelle reti di produzione, ma è possibile usare la versione di anteprima più recente per visualizzare e provare le nuove funzionalità e correzioni che saranno disponibili nella prossima versione disponibile a livello generale. Non sono supportate le versioni di anteprima non aggiornate.

### <a name="release-history"></a>Cronologia delle versioni

Usare le informazioni seguenti per scoprire le novità o le modifiche per una versione supportata del client di Azure Information Protection per Windows. La versione più recente è elencata per prima. 

> [!NOTE]
> Dato che le correzioni di minore rilevanza non sono elencate, se si verifica un problema con il client di Azure Information Protection, è consigliabile controllare se tale problema è stato risolto con la versione disponibile a livello generale più recente. Se il problema persiste, controllare la versione di anteprima corrente (se disponibile).
>  
> Per il supporto tecnico, vedere le informazioni riportate in [Opzioni di supporto e risorse per la community](../information-support.md#support-options-and-community-resources). È anche possibile rivolgersi al team di Azure Information Protection nel [sito di Yammer](https://www.yammer.com/askipteam/).

## <a name="version-1482040"></a>Versione 1.48.204.0

**Data di rilascio**: 04/16/2019

Questa versione include MSIPC versione 1.0.3592.627 del client RMS.

**Nuove funzionalità:**

- Lo scanner Azure Information Protection è ora configurato dal portale di Azure, anziché usando PowerShell.
    
    Se si esegue l'aggiornamento da una versione disponibile a livello generare dello scanner, il processo di aggiornamento è diverso dalle versioni precedenti, quindi assicurarsi di leggere [Aggiornamento dello scanner di Azure Information Protection](client-admin-guide.md#upgrading-the-azure-information-protection-scanner).

- Lo scanner ora supporta più database di configurazione nella stessa istanza di SQL server quando si specifica un nome di profilo.

- Supporto per i tipi di informazioni sensibili seguenti, che consente di identificare la presenza di credenziali nei documenti e nei messaggi di posta elettronica:
    - Stringa di connessione del bus di servizio di Azure
    - Stringa di connessione di Azure IoT
    - Account di archiviazione di Azure
    - Stringa di connessione del database IaaS di Azure e stringa di connessione di SQL di Azure
    - Stringa di connessione di Cache Redis di Azure
    - Azure SAS
    - Stringa di connessione di SQL Server
    - Chiave di autenticazione di Azure DocumentDB
    - Password delle impostazioni di pubblicazione di Azure
    - Chiave dell'account di archiviazione di Azure (generico)

- Nuove impostazioni client avanzate che implementano messaggi popup in Outlook che possono avvisare, giustificare o bloccare l'invio di messaggi di posta elettronica. [Altre informazioni](client-admin-guide-customizations.md#implement-pop-up-messages-in-outlook-that-warn-justify-or-block-emails-being-sent)
    
    Si noti che se è stata configurata la proprietà avanzata del client di OutlookCollaborationTrustedDomains per la versione di anteprima, questa impostazione è stata sostituita da tre nuove impostazioni, in modo che i domini possono essere esenti per ogni azione: OutlookWarnTrustedDomains OutlookJustifyTrustedDomains e OutlookBlockTrustedDomains.

- Se si etichettano e proteggono i file usando il cmdlet [Set-AIPFileLabel](/powershell/azureinformationprotection/vlatest/set-aipfilelabel), è possibile usare il parametro *EnableTracking* per registrare il file nel sito di rilevamento dei documenti. [Altre informazioni](client-admin-guide-document-tracking.md#using-powershell-to-register-labeled-documents-with-the-document-tracking-site)

- Nuova impostazione client avanzata applicabile solo quando si impostano i criteri per non visualizzare le autorizzazioni personalizzate. Quando un file è protetto da autorizzazioni personalizzate, visualizzare l'opzione Autorizzazioni personalizzate in Esplora File in modo che gli utenti possano visualizzarle e modificarle. È necessario che gli utenti abbiano le autorizzazioni per modificare le impostazioni di protezione. [Altre informazioni](client-admin-guide-customizations.md#for-files-protected-with-custom-permissions-always-display-custom-permissions-to-users-in-file-explorer)

- Individuazione endpoint per [analitica di Azure Information Protection](../reports-aip.md).
    
- Due nuovi client le impostazioni avanzate per analitica, per gli scenari seguenti:
    
    - Impedire l'invio delle corrispondenze per i tipi di informazioni per un sottoinsieme di utenti quando è stata selezionata la casella di controllo per la raccolta delle corrispondenze del contenuto nel portale di Azure. [Altre informazioni](client-admin-guide-customizations.md#disable-sending-information-type-matches-for-a-subset-of-users)
    - Per il **individuazione dati** report, visualizzare se i file contengono informazioni riservate. [Altre informazioni](client-admin-guide-customizations.md#enable-azure-information-protection-analytics-to-discover-sensitive-information-in-documents)

**Correzioni**:

- Per i percorsi e i nomi di file non vengono visualizzano punti interrogativi ( **?** ) invece dei caratteri non ASCII nell'analisi di Azure Information Protection con le impostazioni locali inglesi per il sistema operativo di invio.

- vengono applicati in modo coerente nuovi contrassegni visivi quando un utente aggiunge nuove sezioni a un documento di Word e quindi etichetta di nuovo il documento.

- Il client Azure Information Protection rimuove correttamente la protezione da un documento PDF protetto dall'applicazione RMS sharing.

- Le etichette secondarie vengono applicate correttamente da PowerShell e dallo scanner quando viene configurata l'etichetta padre per le autorizzazioni definite dall'utente.

- Il client Azure Information Protection consente di visualizzare correttamente le etichette applicate dai [client che supportano l'etichettatura unificata](../configure-policy-migrate-labels.md#clients-and-services-that-support-unified-labeling).

- I documenti vengono aperti in modo corretto in Office senza un messaggio di ripristino dopo la rimozione della protezione con Esplora file e clic sul pulsante destro del mouse, PowerShell e lo scanner.

- Quando si usa l'impostazione client avanzata per impostare un'[etichetta predefinita per Outlook](client-admin-guide-customizations.md#set-a-different-default-label-for-outlook), è possibile applicare un'etichetta padre con etichette secondarie quando tutte le etichette secondarie sono disabilitate per l'utente.

- Quando si usa l'[impostazione di criteri](../configure-policy-settings.md) **Per i messaggi di posta elettronica con allegati, applicare un'etichetta corrispondente alla classificazione più elevata di questi allegati** e l'etichetta con la classificazione più elevata è configurata per le autorizzazioni definite dall'utente, accadeva che l'etichetta veniva applicata al messaggio di posta elettronica, senza che fosse applicata la protezione. Adesso:
    - Quando le autorizzazioni definite dall'utente dell'etichetta includono Outlook (Non inoltrare): si applicano tale etichetta e la protezione Non inoltrare al messaggio di posta elettronica.
    - Quando le autorizzazioni definite dall'utente dell'etichetta sono solo per Word, Excel, PowerPoint ed Esplora file: non si applica né l'etichetta né un qualsiasi tipo di protezione al messaggio di posta elettronica.

**Modifiche aggiuntive:**

- Sono i seguenti tipi di informazioni riservate [non è più supportato](../configure-policy-classification.md#sensitive-information-types-that-require-a-minimum-version-of-the-client) per la classificazione automatica o per le etichette configurate per consigliabile:
    - Numero di telefono EU
    - Coordinate GPS EU

- Poiché lo scanner di Azure Information Protection viene configurato dal portale di Azure, i cmdlet seguenti sono ora deprecati e non possono essere usati per configurare i repository di dati o l'elenco dei tipi di file:
    - Add-AIPScannerRepository
    - Add-AIPScannerScannedFileTypes
    - Get-AIPScannerRepository
    - Remove-AIPScannerRepository
    - Remove-AIPScannerScannedFileTypes
    - Set-AIPScannerRepository
    - Set-AIPScannerScannedFileTypes

- Un nuovo cmdlet di PowerShell [Import-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Import-AIPScannerConfiguration), per gli scenari in cui lo scanner di Azure Information Protection non può scaricare la configurazione dal portale di Azure.

- Lo scanner di Azure Information Protection non esclude più i file ZIP per impostazione predefinita. Per esaminare ed etichettare i file ZIP, vedere la sezione [Per esaminare i file con estensione zip](client-admin-guide-file-types.md#to-inspect-zip-files) della guida dell'amministratore.

- L'[impostazione dei criteri](../configure-policy-settings.md) **Gli utenti devono fornire una giustificazione per impostare un'etichetta di classificazione inferiore, rimuovere un'etichetta o rimuovere la protezione** non si applica più allo scanner. Lo scanner esegue queste azioni quando si imposta l'opzione **Applica una nuova etichetta ai file** su **Sì** nel profilo dello scanner.

## <a name="version-141510"></a>Versione 1.41.51.0

**Data di rilascio**: 27/11/2018

Questa versione include MSIPC versione 1.0.3592.627 del client RMS.

**Nuove funzionalità:**

- Il client Azure Information Protection protegge ora per impostazione predefinita i file PDF tramite lo standard ISO per la crittografia PDF. In precedenza, era necessario abilitare questo supporto con un'impostazione client avanzata.
    
    Se si vuole tornare alla protezione di file PDF tramite un'estensione di nome di file ppdf, usare la stessa [impostazione client avanzata](client-admin-guide-customizations.md#dont-protect-pdf-files-by-using-the-iso-standard-for-pdf-encryption), ma specificare **False**.

- Supporto per dati di controllo [reporting centralizzato](../reports-aip.md) usando analitica di Azure Information Protection, annunciate presso Microsoft Ignite 2018.

- Excel supporta ora i [contrassegni visivi](../configure-policy-markings.md) in colori diversi.

- Per le distribuzioni esistenti di S/MIME, una nuova impostazione client avanzata per configurare un'etichetta per applicare automaticamente la protezione S/MIME in Outlook. [Altre informazioni](client-admin-guide-customizations.md#configure-a-label-to-apply-smime-protection-in-outlook)

- Una nuova impostazione client avanzata, come alternativa alla modifica del Registro di sistema per evitare richieste di accesso per il servizio Azure Information Protection per i [computer disconnessi](client-admin-guide-customizations.md#support-for-disconnected-computers).

- Una nuova impostazione client avanzata per [supportare l'ordine delle etichette secondarie](client-admin-guide-customizations.md#enable-order-support-for-sublabels-on-attachments) quando si usa l'impostazione dei criteri seguente:
    - **Per i messaggi di posta elettronica con allegati, applica un'etichetta corrispondente alla classificazione più elevata di questi allegati**

**Correzioni**:

- Il client Azure Information Protection non esclude più le estensioni di nomi di file msg, rar e zip per Esplora file (clic con il pulsante destro del mouse) e i comandi di PowerShell. Tuttavia, queste estensioni rimangono escluse per impostazione predefinita per lo scanner. 

- Il client Azure Information Protection può annullare la protezione di più file (selezione multipla e una cartella che contiene i file protetti) quando si usa Esplora file, clic con il pulsante destro del mouse.

- Per Excel:
    
    - I contrassegni visivi vengono ora applicati se si salva il foglio di calcolo durante la modifica di una cella.
    
    - Excel 2010: quando si protegge un foglio di calcolo usando il [livello di autorizzazione](../configure-usage-rights.md#rights-included-in-permissions-levels) Coautore, il pulsante **Elimina etichetta** è ora disponibile quando si fa clic con il pulsante destro del mouse sul file e si sceglie **Classifica e proteggi**.

- Le impostazioni client avanzate che consentono la [rimozione di intestazioni e piè di pagina da altre soluzioni di etichettatura](client-admin-guide-customizations.md#remove-headers-and-footers-from-other-labeling-solutions) ora supportano i layout personalizzati.

**Modifiche aggiuntive:**

- Quando la pianificazione dello scanner è impostata su **Sempre**, viene ora applicato un ritardo di 30 secondi tra le analisi.

- Lo scanner non modifica più il proprietario di Rights Management per i file etichettati quando sono già protetti.

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sull'installazione e l'uso del client: 

- Per gli utenti: [Scaricare e installare il client](install-client-app.md)

- Per gli amministratori: [Guida per l'amministratore del client di Azure Information Protection](client-admin-guide.md)
