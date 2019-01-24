---
title: 'Client di Azure Information Protection: cronologia delle versioni e criteri per il supporto'
description: Informazioni sugli elementi nuovi o modificati in una versione del client di Azure Information Protection per Windows e sui criteri del ciclo di vita per il supporto.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 01/16/2019
ms.topic: conceptual
ms.service: information-protection
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: d120c9dea8ac49c48d7b47d4ee0a0b317ab8c5d6
ms.sourcegitcommit: 2c90f5bf11ec34ab94824a39ccab75bde71fc3aa
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/15/2019
ms.locfileid: "54314952"
---
# <a name="azure-information-protection-client-version-release-history-and-support-policy"></a>Client Azure Information Protection: Cronologia delle versioni e criteri per il supporto

>*Si applica a: Active Directory Rights Management Services, [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8, Windows 7 con SP1, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2*

Il team di Azure Information Protection aggiorna regolarmente il client di Azure Information Protection con correzioni e nuove funzionalità. 

È possibile scaricare la versione disponibile a livello generale più recente e la versione di anteprima corrente (se disponibile) dall'[Area download Microsoft](https://www.microsoft.com/en-us/download/details.aspx?id=53018). Dopo un breve periodo solitamente di un paio di settimane, la versione disponibile a livello generale più recente viene inclusa anche in Microsoft Update Catalog (categoria: **Azure Information Protection**). L'inserimento nel catalogo significa che è possibile aggiornare il client tramite WSUS o Configuration Manager o altri meccanismi di distribuzione del software che usano Microsoft Update.

Per altre informazioni, vedere [Aggiornamento e gestione del client Azure Information Protection](client-admin-guide.md#upgrading-and-maintaining-the-azure-information-protection-client).

### <a name="servicing-information-and-timelines"></a>Informazioni e tempistiche di manutenzione

Ogni versione con disponibilità generale del client di Azure Information Protection è supportata per un massimo di sei mesi dopo il rilascio della versione con disponibilità generale successiva. La documentazione non include informazioni sulle versioni non supportate del client. Le correzioni e le nuove funzionalità sono sempre valide per l'ultima versione disponibile a livello generale e non verranno applicate alle versioni precedenti.

Le versioni di anteprima non devono essere distribuite agli utenti finali nelle reti di produzione, ma è possibile usare la versione di anteprima più recente per visualizzare e provare le nuove funzionalità e correzioni che saranno disponibili nella prossima versione disponibile a livello generale. Non sono supportate le versioni di anteprima non aggiornate.

### <a name="release-history"></a>Cronologia delle versioni

Usare le informazioni seguenti per scoprire le novità o le modifiche per una versione supportata del client di Azure Information Protection per Windows. La versione più recente è elencata per prima. 

> [!NOTE]
> Dato che le correzioni di minore rilevanza non sono elencate, se si verifica un problema con il client di Azure Information Protection, è consigliabile controllare se tale problema è stato risolto con la versione disponibile a livello generale più recente. Se il problema persiste, verificare la versione di anteprima corrente.
>  
> Per il supporto tecnico, vedere le informazioni riportate in [Opzioni di supporto e risorse per la community](../information-support.md#support-options-and-community-resources). È anche possibile rivolgersi al team di Azure Information Protection nel [sito di Yammer](https://www.yammer.com/askipteam/).

## <a name="versions-later-than-141510"></a>Versioni successive alla versione 1.41.51.0

Se la versione 1 del client usata è successiva alla 1.41.51.0, si tratta di una build di anteprima per scopi di test e valutazione.  

> [!TIP]
> Se si è interessati alla valutazione del client di etichettatura unificato Azure Information Protection perché si pubblicano le etichette dal Centro sicurezza e conformità di Office 365, Vedere [Client per l'etichettatura unificata di Azure Information Protection: informazioni di rilascio versione](unifiedlabelingclient-version-release-history.md).

**Data di rilascio**: 15/01/2019

Questa versione include MSIPC versione 1.0.3592.627 del client RMS.

**Nuove funzionalità:**

- Lo scanner di Azure Information Protection può essere ora configurato dal portale di Azure, anziché usando PowerShell:
    
    - Se si esegue l'aggiornamento da una versione disponibile a livello generare dello scanner, il processo di aggiornamento è diverso dalle versioni precedenti, quindi assicurarsi di leggere [Aggiornamento dello scanner di Azure Information Protection](client-admin-guide.md#upgrading-the-azure-information-protection-scanner).
    
    - Per la prima installazione dello scanner, vedere invece [Distribuzione dello scanner di Azure Information Protection per classificare e proteggere automaticamente i file](../deploy-aip-scanner-preview.md).

- Se si etichettano e proteggono i file usando il cmdlet [Set-AIPFileLabel](/powershell/azureinformationprotection/vlatest/set-aipfilelabel), è possibile usare il parametro *EnableTracking* per registrare il file nel sito di rilevamento dei documenti. [Altre informazioni](client-admin-guide-document-tracking.md#using-powershell-to-register-labeled-documents-with-the-document-tracking-site)

- Lo scanner di Azure Information Protection supporta ora più database di configurazione nella stessa istanza di SQL server quando si specifica un nome di profilo.

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

**Correzioni**:

- vengono applicati in modo coerente nuovi contrassegni visivi quando un utente aggiunge nuove sezioni a un documento di Word e quindi etichetta di nuovo il documento.

- Il client Azure Information Protection rimuove correttamente la protezione da un documento PDF protetto dall'applicazione RMS sharing.

- Per i percorsi e i nomi di file non vengono visualizzano punti interrogativi (**?**) anziché caratteri non ASCII nell'analisi di Azure Information Protection con le impostazioni locali inglesi per il sistema operativo di invio.

- Le etichette secondarie vengono applicate correttamente da PowerShell e dallo scanner quando viene configurata l'etichetta padre per le autorizzazioni definite dall'utente.

- Il client Azure Information Protection consente di visualizzare correttamente le etichette applicate dai [client che supportano l'etichettatura unificata](../configure-policy-migrate-labels.md#clients-that-support-unified-labeling).

- I documenti vengono aperti in modo corretto in Office senza un messaggio di ripristino dopo la rimozione della protezione con Esplora file e clic sul pulsante destro del mouse, PowerShell e lo scanner.

**Modifiche aggiuntive:**

- non sono più supportati i tipi di informazioni sensibili seguenti per le etichette configurate per la classificazione consigliata o automatica:
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

- Supporto del [reporting centralizzato](../reports-aip.md) per la funzionalità di analisi di Azure Information Protection annunciata in Microsoft Ignite.

- Excel supporta ora i [contrassegni visivi](../configure-policy-markings.md) in colori diversi.

- Per le distribuzioni esistenti di S/MIME, una nuova impostazione client avanzata (in anteprima) per configurare un'etichetta per applicare automaticamente la protezione S/MIME in Outlook. [Altre informazioni](client-admin-guide-customizations.md#configure-a-label-to-apply-smime-protection-in-outlook)

- Una nuova impostazione client avanzata, come alternativa alla modifica del Registro di sistema per evitare richieste di accesso per il servizio Azure Information Protection per i [computer disconnessi](client-admin-guide-customizations.md#support-for-disconnected-computers).

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

## <a name="version-137190"></a>Versione 1.37.19.0

**Data di rilascio**: 17/09/2018

Questa versione include MSIPC versione 1.0.3592.627 del client RMS.

**Nuove funzionalità**: 

- Supporto dello standard ISO per la crittografia dei file PDF mediante la definizione di una nuova [configurazione del client avanzata](client-admin-guide-customizations.md#dont-protect-pdf-files-by-using-the-iso-standard-for-pdf-encryption). Quando questa opzione è impostata su **True**, i documenti PDF protetti mantengono l'estensione pdf (anziché adottare l'estensione ppdf) e possono essere aperti da lettori PDF che supportano questo standard ISO. Attualmente, è necessario indicare agli utenti di aprire questi file PDF protetti manualmente con il Visualizzatore Azure Information Protection. Per consentire agli utenti di eseguire questa operazione, quando aprono uno di questi file PDF protetti, viene visualizzata una pagina con le icone da selezionare per il sistema operativo usato.

- Supporto dei nuovi tipi di informazioni sensibili che consentono di classificare i documenti contenenti informazioni personali. [Altre informazioni](../configure-policy-classification.md#sensitive-information-types-that-require-a-minimum-version-of-the-client) 

- Le etichette che applicano la protezione ora vengono visualizzate nelle app di Office 2016 (versione minima 1805, build 9330.2078) quando all'utente viene assegnata una licenza per Azure Rights Management (noto anche come Azure Information Protection per Office 365).

- Supporto di assegnazione etichette per il formato **Strict Open XML Document** in file di Word, Excel e PowerPoint. Per altre informazioni sui formati Open XML, vedere il post del blog di Office [New file format options in the new Office](https://www.microsoft.com/en-us/microsoft-365/blog/2012/08/13/new-file-format-options-in-the-new-office/) (Nuove opzioni per i formati di file nel nuovo Office). 

- Supporto dei file protetti con Secure Islands e diversi da file PDF e documenti di Office. Ad esempio file di testo e file immagine protetti. Oppure file con estensione pfile. Questo supporto attiva nuovi scenari. Ad esempio lo scanner Azure Information Protection può verificare la presenza di informazioni riservate in questi file e rietichettarli automaticamente per Azure Information Protection. [Altre informazioni](client-admin-guide-customizations.md#support-for-files-protected-by-secure-islands)

- Nuove impostazioni client avanzate per rimuovere le intestazioni e i piè di pagina applicati ai documenti da altre soluzioni di assegnazione etichette. [Altre informazioni](client-admin-guide-customizations.md#remove-headers-and-footers-from-other-labeling-solutions)

- Per lo scanner di Azure Information Protection:

    - Nuovo cmdlet, [Update-AIPScanner](/powershell/module/azureinformationprotection/Update-AIPScanner): deve essere eseguito una sola volta dopo l'aggiornamento dalla versione di disponibilità a livello generale precedente (1.29.5.0) o versioni precedenti.
    
    - Nuovo cmdlet, [Get-AIPScannerStatus](/powershell/module/azureinformationprotection/Get-AIPScannerStatus): ottiene lo stato corrente del servizio per lo scanner.  
    
    - Nuovo cmdlet [Start-AIPScan](/powershell/module/azureinformationprotection/Start-AIPScan): richiede allo scanner di avviare un ciclo di analisi unico quando la pianificazione è impostata su manuale.
    
    - Quando si usa lo standard ISO per la crittografia dei file PDF, i documenti PDF sono ora protetti per impostazione predefinita.
    
    - SharePoint Server 2010 è supportato per i clienti che dispongono del [supporto "Extended" per la versione corrente di SharePoint](https://support.microsoft.com/lifecycle/search?alpha=SharePoint%20Server%202010).
    
- Supporto del nuovo pannello **Azure Information Protection - Nodi (anteprima)** nel portale di Azure, che consente di gestire gli scanner da una posizione centrale. Le informazioni dagli scanner distribuiti con connettività ad Azure vengono aggiornate ogni cinque minuti. Da questo pannello è possibile avviare lo scanner per una singola analisi, rianalizzare tutti i file, controllare lo stato di uno scanner e visualizzare la velocità di scansione.

**Correzioni**

- Per lo scanner di Azure Information Protection:
    
    - Per i documenti protetti nelle raccolte di SharePoint, se il parametro *DefaultOwner* non viene usato per il repository dei dati, il valore Editor di SharePoint viene ora usato come valore predefinito invece del valore Autore.
    
    - I report dello scanner includono "Autore ultima modifica" per i documenti di Office.
    
    - Ora è possibile proteggere tutti i tipi di file usando il carattere jolly `*` quando si modifica il Registro di sistema come descritto nella sezione [Modifica del Registro di sistema per lo scanner](../deploy-aip-scanner.md#editing-the-registry-for-the-scanner).

- La visualizzazione di messaggi di posta elettronica mediante le icone freccia elemento successivo ed elemento precedente nella barra di accesso rapido visualizza l'etichetta appropriata per ogni messaggio.

- Quando si applica la classificazione e la protezione mediante Esplora file, PowerShell o lo scanner, i metadati del documento di Office non vengono rimossi o crittografati.

- Le autorizzazioni personalizzate supportano gli indirizzi di posta elettronica di destinatari contenenti un apostrofo.

- L'ambiente del computer viene inizializzato correttamente (bootstrap) quando questa operazione viene avviata mediante l'apertura di un documento protetto archiviato in SharePoint Online.

- Quando si fa clic con il pulsante destro del mouse in Esplora file, in PowerShell o nello scanner dal client, l'assegnazione delle etichette è bloccata per i file nei percorsi WebDav poiché si tratta di uno scenario non supportato.

- L'icona Elimina l'etichetta non viene visualizzata nelle app client (Word, Excel, PowerPoint e Outlook) quando si configura l'[impostazione di criteri](../configure-policy-settings.md) di **Tutti i documenti e i messaggi di posta elettronica devono avere un'etichetta**.

**Modifiche aggiuntive**:

- Per [Set-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Set-AIPScannerConfiguration):
    
    - I valori del parametro *Schedule* non sono più **OneTime**, **Continuous** e **Never**, ma **Manual** e **Always**.
        
    - Il parametro *Type* è stato rimosso e pertanto viene rimosso anche dall'output quando si esegue [Get-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Get-AIPScannerConfiguration). Per impostazione predefinita, solo i file nuovi o modificati vengono controllati dopo il primo ciclo di analisi. Se il parametro *Type* è stato impostato su **Full** in precedenza per ripetere l'analisi di tutti i file, eseguire ora [Start-AIPScan](/powershell/module/azureinformationprotection/Start-AIPScan) con il parametro *Reset*. Lo scanner deve essere anche configurato per una pianificazione manuale, che richiede l'impostazione del parametro *Schedule* su **Manual** con [Set-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Set-AIPScannerConfiguration).
    
- L'elenco di esclusione predefinito per il client e lo scanner ora include i file con estensione msg, rar e zip. Lo scanner esclude anche i file con estensione rtf. [Altre informazioni](client-admin-guide-file-types.md#file-types-that-are-excluded-from-classification-and-protection)

- La versione dei criteri è ora la 1.4. L'identificazione del numero di versione è necessaria per la [configurazione dei computer disconnessi](client-admin-guide-customizations.md#support-for-disconnected-computers).

- Il collegamento **Invia commenti e suggerimenti** nella finestra di dialogo **Guida e commenti** è stato rimosso. È stato temporaneamente sostituito da **Segnala un problema** che per impostazione predefinita inviava un messaggio di posta elettronica a Microsoft. A partire da dicembre 2018 l'opzione **Segnala un problema** non viene visualizzata per impostazione predefinita ma può essere aggiunta con un'[impostazione client avanzata](client-admin-guide-customizations.md#add-report-an-issue-for-users) in cui si specifica una stringa HTTP per il collegamento. Ad esempio, una pagina Web personalizzata in cui gli utenti possono segnalare i problemi o un indirizzo di posta elettronica che rimanda all'help desk. 

## <a name="version-12950"></a>Versione 1.29.5.0 

**Data di rilascio**: 26/06/2018

Questa versione include MSIPC versione 1.0.3403.1224 del client RMS.

**Correzioni**:

- Per le versioni di Outlook 16.0.9324.1000 e successive (A portata di clic), la barra di Azure Information Protection supporta le opzioni di visualizzazione dello schermo più recenti per risolvere il problema della barra visualizzata all'esterno dell'applicazione Outlook.

- I contrassegni visivi configurati [per ogni tipo di applicazione di Office](../configure-policy-markings.md#setting-different-visual-markings-for-word-excel-powerpoint-and-outlook) ora sostituiscono un'intestazione o un piè di pagina applicato in precedenza da un'etichetta di Azure Information Protection.

- Quando un file di Excel è già etichettato e l'etichetta applica contrassegni visivi, ora i contrassegni visivi dell'etichetta vengono applicati a un nuovo foglio.

- Quando si usa l'impostazione client avanzata per [etichettare un documento di Office usando una proprietà personalizzata esistente](client-admin-guide-customizations.md#label-an-office-document-by-using-an-existing-custom-property), l'assegnazione automatica dell'etichetta non esegue l'override di quella manuale.

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sull'installazione e l'uso del client: 

- Per gli utenti: [Scaricare e installare il client](install-client-app.md)

- Per gli amministratori: [Guida per l'amministratore del client di Azure Information Protection](client-admin-guide.md)
