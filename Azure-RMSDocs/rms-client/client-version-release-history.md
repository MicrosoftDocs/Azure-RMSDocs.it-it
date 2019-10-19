---
title: Azure Information Protection & i criteri di supporto per la cronologia delle versioni client
description: Informazioni sugli elementi nuovi o modificati in una versione del client di Azure Information Protection per Windows e sui criteri del ciclo di vita per il supporto.
author: cabailey
ms.author: cabailey
manager: rkarlin
ms.date: 10/17/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: v1client
ms.reviewer: elkamins
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 98861fcabfb6e00edbc0206f3c80a45d6287f70f
ms.sourcegitcommit: e007bffd33c959124baa5719236981c93947a3e4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/17/2019
ms.locfileid: "72535346"
---
# <a name="azure-information-protection-client-version-release-history-and-support-policy"></a>Client di Azure Information Protection: cronologia delle versioni e criteri per il supporto

>*Si applica a: Active Directory Rights Management Services, [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8, Windows 7 con SP1, windows server 2019, windows server 2016, windows Server 2012 R2, windows Server 2012, windows Server 2008 R2*
>
> *Istruzioni per: [client di Azure Information Protection per Windows](../faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*

Il team di Azure Information Protection aggiorna regolarmente il client di Azure Information Protection con correzioni e nuove funzionalità. 

È possibile scaricare la versione disponibile a livello generale più recente e la versione di anteprima corrente (se disponibile) dall'[Area download Microsoft](https://www.microsoft.com/en-us/download/details.aspx?id=53018). 

Dopo un breve ritardo di genere in un paio di settimane, la versione di disponibilità generale più recente è inclusa anche nel catalogo di Microsoft Update con il nome del prodotto **Microsoft Azure Information Protection**  > **Microsoft Azure informazioni Client di protezione**e classificazione degli **aggiornamenti**. L'inserimento nel catalogo significa che è possibile aggiornare il client tramite WSUS o Configuration Manager o altri meccanismi di distribuzione del software che usano Microsoft Update.

Per altre informazioni, vedere [Aggiornamento e gestione del client Azure Information Protection](client-admin-guide.md#upgrading-and-maintaining-the-azure-information-protection-client).

> [!TIP]
> Si è interessati all'uso del client Azure Information Protection Unified Labeling perché le etichette vengono pubblicate dalla Centro sicurezza e conformità di Office 365, dal centro sicurezza Microsoft 365 o da Microsoft 365 Compliance Center? Quando si scarica e si installa il client di etichettatura unificata dall'area download Microsoft, è possibile aggiornare il client di Azure Information Protection a questo [client di etichetta unificata](unifiedlabelingclient-version-release-history.md).

### <a name="servicing-information-and-timelines"></a>Informazioni e tempistiche di manutenzione

Ogni versione con disponibilità generale del client di Azure Information Protection è supportata per un massimo di sei mesi dopo il rilascio della versione con disponibilità generale successiva. Fatta eccezione per questa sezione, nella documentazione non sono incluse informazioni sulle versioni non supportate del client. Le correzioni e le nuove funzionalità sono sempre valide per l'ultima versione disponibile a livello generale e non verranno applicate alle versioni precedenti.

Le versioni di anteprima non devono essere distribuite agli utenti finali nelle reti di produzione, ma è possibile usare la versione di anteprima più recente per visualizzare e provare le nuove funzionalità e correzioni che saranno disponibili nella prossima versione disponibile a livello generale. Non sono supportate le versioni di anteprima non aggiornate.

##### <a name="general-availability-versions-that-are-no-longer-supported"></a>Versioni di disponibilità generale non più supportate:

|Versione client|Data di rilascio|
|--------------|-------------|
|1.41.51.0|27/11/2018|
|1.37.19.0|17/09/2018|
|1.29.5.0|26/06/2018|
|1.27.48.0|30/05/2018|
|1.26.6.0|04/17/2018|
|1.10.56.0|09/18/2017|
|1.7.210.0|06/06/2017|
|1.4.21.0|03/15/2017|
|1.3.155.2|02/08/2017|
|1.2.4.0.0|10/27/2016|
|1.1.23.0|10/01/2016|

Il formato della data usato in questa pagina è *mese/giorno/anno*.

A partire da 6/2/2019, il servizio di assegnazione di etichette per Azure Information Protection richiede connessioni che usano TLS 1,2.

Tutte le versioni client di 1.4.21.0 rilasciate 03/15/2017 supportano TLS 1,2. Le versioni client **1.3.155.2**, **1.2.4.0**e **1.1.23.0** non usano TLS 1,2 e pertanto non possono più scaricare i criteri di Azure Information Protection.

### <a name="release-history"></a>Cronologia delle versioni

Usare le informazioni seguenti per scoprire le novità o le modifiche per una versione supportata del client di Azure Information Protection per Windows. La versione più recente è elencata per prima.

> [!NOTE]
> Dato che le correzioni di minore rilevanza non sono elencate, se si verifica un problema con il client di Azure Information Protection, è consigliabile controllare se tale problema è stato risolto con la versione disponibile a livello generale più recente. Se il problema persiste, controllare la versione di anteprima corrente (se disponibile).
>  
> Per il supporto tecnico, vedere le informazioni riportate in [Opzioni di supporto e risorse per la community](../information-support.md#support-options-and-community-resources). È anche possibile rivolgersi al team di Azure Information Protection nel [sito di Yammer](https://www.yammer.com/askipteam/).

## <a name="version-153100"></a>Versione 1.53.10.0

**Rilasciata**: 07/15/2019

Questa versione include MSIPC versione 1.0.3889.0419 del client RMS.

**Nuove funzionalità:**

- Nuova impostazione client avanzata per esentare i messaggi di Outlook dall'impostazione dei criteri **tutti i documenti e i messaggi di posta elettronica devono avere un'etichetta**. [Altre informazioni](client-admin-guide-customizations.md#exempt-outlook-messages-from-mandatory-labeling)

- Nuova impostazione client avanzata per personalizzare ulteriormente le impostazioni che implementano messaggi popup in Outlook che avvisano, giustificano o bloccano l'invio di messaggi di posta elettronica. Con questa nuova impostazione avanzata, è possibile impostare un'azione diversa per i messaggi di posta elettronica senza allegati. [Altre informazioni](client-admin-guide-customizations.md#to-specify-a-different-action-for-email-messages-without-attachments)

**Correzioni**:

- Quando si usa Esplora file, fare clic con il pulsante destro del mouse per etichettare un file con protezione applicata indipendentemente da un'etichetta. tale protezione viene mantenuta. Un utente, ad esempio, ha applicato autorizzazioni personalizzate a un file.

- Quando si sostituisce l'opzione non eseguire l'invio in un thread di posta elettronica con un'etichetta configurata per le autorizzazioni definite dall'utente e non in avanti, i destinatari originali possono comunque aprire il messaggio di posta elettronica.

- Nello scenario seguente un utente non vede più nella descrizione comando dell'etichetta che l'etichetta è stata impostata automaticamente: un utente riceve un messaggio di posta elettronica protetto con un documento collegato che non è etichettato, ma protetto automaticamente. Quando l'utente della stessa organizzazione del mittente apre il documento, al documento viene applicata l'etichetta corrispondente per le impostazioni di protezione.

- Il [diritto di utilizzo](../configure-usage-rights.md#usage-rights-and-descriptions) minimo per eseguire il cmdlet [Unprotect-RMSFile](/powershell/module/azureinformationprotection/unprotect-rmsfile) è ora **Salva con nome, Esporta** (esportazione) anziché **copia** (estrazione).

## <a name="version-1482040"></a>Versione 1.48.204.0

**Rilasciata**: 04/16/2019

Supportato tramite 01/15/2020

Questa versione include MSIPC versione 1.0.3592.627 del client RMS.

**Nuove funzionalità:**

- Il Azure Information Protection scanner è ora configurato dal portale di Azure, anziché tramite PowerShell.
    
    Se si esegue l'aggiornamento da una versione disponibile a livello generare dello scanner, il processo di aggiornamento è diverso dalle versioni precedenti, quindi assicurarsi di leggere [Aggiornamento dello scanner di Azure Information Protection](client-admin-guide.md#upgrading-the-azure-information-protection-scanner).

- Lo scanner supporta ora più database di configurazione nella stessa istanza di SQL Server quando si specifica un nome di profilo.

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

- Supporto per l'individuazione di endpoint per [Azure Information Protection Analytics](../reports-aip.md), per segnalare le informazioni riservate trovate quando gli utenti salvano per la prima volta un documento di Office (usando le app desktop per Word, Excel e PowerPoint):
    - Per individuare queste informazioni, non è necessario etichettare i documenti.
    - Le informazioni riservate sono identificate da tipi di informazioni predefiniti e personalizzati.
    - Se non si desidera che i tipi di informazioni riservate vengano inviati a Azure Information Protection Analytics, è possibile disabilitare l'individuazione degli endpoint con un' [impostazione client avanzata](client-admin-guide-customizations.md#disable-sending-discovered-sensitive-information-in-documents-to-azure-information-protection-analytics).

- Nuove impostazioni client avanzate che implementano messaggi popup in Outlook che possono avvisare, giustificare o bloccare l'invio di messaggi di posta elettronica. [Altre informazioni](client-admin-guide-customizations.md#implement-pop-up-messages-in-outlook-that-warn-justify-or-block-emails-being-sent)
    
    Si noti che se è stata configurata la proprietà Advanced client di OutlookCollaborationTrustedDomains per la versione di anteprima, questa impostazione viene ora sostituita da tre nuove impostazioni, in modo che i domini possano essere esentati per azione: OutlookWarnTrustedDomains, OutlookJustifyTrustedDomains e OutlookBlockTrustedDomains.

- Se si etichettano e proteggono i file usando il cmdlet [Set-AIPFileLabel](/powershell/azureinformationprotection/vlatest/set-aipfilelabel), è possibile usare il parametro *EnableTracking* per registrare il file nel sito di rilevamento dei documenti. [Altre informazioni](client-admin-guide-document-tracking.md#using-powershell-to-register-labeled-documents-with-the-document-tracking-site)

- Una nuova impostazione client avanzata per [Azure Information Protection Analytics](../reports-aip.md), per impedire l'invio di corrispondenze dei tipi di informazioni per un subset di utenti dopo aver selezionato la casella di controllo nella portale di Azure che consente di ottenere analisi più approfondite nei dati sensibili. Questa impostazione è applicabile per il client e lo scanner. [Altre informazioni](client-admin-guide-customizations.md#disable-sending-information-type-matches-for-a-subset-of-users)

- Nuova impostazione client avanzata applicabile solo quando si configura l'impostazione dei criteri in modo da non visualizzare autorizzazioni personalizzate: quando è presente un file protetto con autorizzazioni personalizzate, visualizzare l'opzione autorizzazioni personalizzate in Esplora file in modo che gli utenti possano vedere e modificarle (se dispongono delle autorizzazioni per modificare le impostazioni di protezione). [Altre informazioni](client-admin-guide-customizations.md#for-files-protected-with-custom-permissions-always-display-custom-permissions-to-users-in-file-explorer)


**Correzioni**:

- Per i percorsi e i nomi di file non vengono visualizzano punti interrogativi ( **?** ) invece dei caratteri non ASCII nell'analisi di Azure Information Protection con le impostazioni locali inglesi per il sistema operativo di invio.

- vengono applicati in modo coerente nuovi contrassegni visivi quando un utente aggiunge nuove sezioni a un documento di Word e quindi etichetta di nuovo il documento.

- Il client Azure Information Protection rimuove correttamente la protezione da un documento PDF protetto dall'applicazione RMS sharing.

- Le etichette secondarie vengono applicate correttamente da PowerShell e dallo scanner quando viene configurata l'etichetta padre per le autorizzazioni definite dall'utente.

- Il client Azure Information Protection consente di visualizzare correttamente le etichette applicate dai [client che supportano l'etichettatura unificata](../configure-policy-migrate-labels.md#clients-and-services-that-support-unified-labeling).

- I documenti vengono aperti in modo corretto in Office senza un messaggio di ripristino dopo la rimozione della protezione con Esplora file e clic sul pulsante destro del mouse, PowerShell e lo scanner.

- Quando si usa l'impostazione client avanzata per impostare un'[etichetta predefinita per Outlook](client-admin-guide-customizations.md#set-a-different-default-label-for-outlook), è possibile applicare un'etichetta padre con etichette secondarie quando tutte le etichette secondarie sono disabilitate per l'utente.

- Quando si usa l'[impostazione di criteri](../configure-policy-settings.md) **Per i messaggi di posta elettronica con allegati, applicare un'etichetta corrispondente alla classificazione più elevata di questi allegati** e l'etichetta con la classificazione più elevata è configurata per le autorizzazioni definite dall'utente, accadeva che l'etichetta veniva applicata al messaggio di posta elettronica, senza che fosse applicata la protezione. Adesso:
    - Quando le autorizzazioni definite dall'utente dell'etichetta includono Outlook (non inoltrare): applicare tale etichetta e la relativa protezione non inoltrare al messaggio di posta elettronica.
    - Quando le autorizzazioni definite dall'utente dell'etichetta sono destinate solo a Word, Excel, PowerPoint ed Esplora file: non applicare l'etichetta né applicare alcuna protezione al messaggio di posta elettronica.

**Modifiche aggiuntive:**

- I tipi di informazioni sensibili seguenti [non sono più supportati](../configure-policy-classification.md#sensitive-information-types-that-require-a-minimum-version-of-the-client) per le etichette configurate per la classificazione automatica o consigliata:
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

- L'[impostazione dei criteri](../configure-policy-settings.md) **Gli utenti devono fornire una giustificazione per impostare un'etichetta di classificazione inferiore, rimuovere un'etichetta o rimuovere la protezione** non si applica più allo scanner. Lo scanner esegue queste azioni quando si configura l'impostazione modifica **etichette file** **su** in nel profilo scanner, quindi selezionare la casella di controllo **Consenti downgrade etichetta** .

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sull'installazione e l'uso del client: 

- Per utenti: [Scaricare e installare il client](install-client-app.md)

- Per amministratori: [Guida per l'amministratore del client di Azure Information Protection](client-admin-guide.md)
