---
title: Il client per Azure Information Protection-AIP
description: Microsoft Azure Information Protection offre una soluzione client-server che consente di proteggere i dati di un'organizzazione. Il client (di Azure Information Protection o di Rights Management) si integra con le applicazioni che vengono eseguite su computer e dispositivi mobili.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 09/26/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.suite: ems
ms.custom: admin
search.appverid:
- MET150
ms.openlocfilehash: 63220621a6c3bbf7ad84ba4c76c38353b56c256d
ms.sourcegitcommit: a091cabd5ad24b4534b5f69f029843037c7872d3
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/26/2019
ms.locfileid: "71313989"
---
# <a name="the-client-side-of-azure-information-protection"></a>Lato client di Azure Information Protection

>*Si applica a: Active Directory Rights Management Services, [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8, Windows 7 con SP1, windows server 2019, windows server 2016, windows Server 2012 R2, windows Server 2012, windows Server 2008 R2*

Azure Information Protection offre una soluzione client-server che consente di proteggere i documenti e i messaggi di posta elettronica di un'organizzazione:

- Il client può essere il client di Azure Information Protection (classico), il client Azure Information Protection Unified Labeling o il client di Rights Management. Indipendentemente dai client usati, si integra con le applicazioni eseguite su computer e dispositivi mobili. 
- Il servizio risiede nel cloud (Azure Information Protection, che usa il servizio Azure Rights Management per la protezione dei dati) o in locale (Active Directory Rights Management Services, più comunemente noto come AD RMS). 

Il client Azure Information Protection (classico) e il client di Azure Information Protection Unified Labeling supportano la classificazione e la protezione con l'assegnazione di etichette. Il client classico supporta inoltre la protezione senza l'assegnazione di etichette. Entrambi i client si integrano con le applicazioni di Office e devono essere installati separatamente.

Il client di Rights Management (RMS) viene installato automaticamente con alcune applicazioni, ad esempio le applicazioni di Office, il client di Azure Information Protection (classico) e il client di assegnazione di etichette unificato Azure Information Protection e le applicazioni abilitate per RMS da fornitori di software. Tuttavia può essere anche [installato da solo](https://www.microsoft.com/en-us/download/details.aspx?id=38396), per supportare la [sincronizzazione dei file tra le librerie protette da IRM e OneDrive for Business](https://support.office.com/article/Deploy-the-new-OneDrive-sync-client-in-an-enterprise-environment-3f3a511c-30c6-404a-98bf-76f95c519668) e per gli sviluppatori che vogliono integrare la protezione di Rights Management nelle applicazioni line-of-business.

## <a name="choose-which-azure-information-protection-client-to-use"></a>Scegliere il client Azure Information Protection da usare

Il **client di Azure Information Protection (versione classica)** Scarica le etichette e le impostazioni dei criteri dall'portale di Azure. Per ulteriori informazioni su questo client, vedere il [client Azure Information Protection: Cronologia delle versioni e criteri per il supporto](client-version-release-history.md).

Il **client per l'etichettatura unificata Azure Information Protection** scarica le etichette e le impostazioni dei criteri dai centri di amministrazione: Centro sicurezza e conformità di Office 365, Centro sicurezza Microsoft 365 e Centro conformità Microsoft 365. Per ulteriori informazioni su questo client, vedere il [Azure Information Protection client Unified Labeling: informazioni di rilascio versione](unifiedlabelingclient-version-release-history.md).

Quale client è opportuno installare?

- Installare il client di etichettatura unificato Azure Information Protection per le etichette che possono essere usate anche da MacOS, iOS e Android e, se non sono necessarie le poche funzionalità che non sono ancora supportate. Queste funzionalità includono la protezione del contenuto con una chiave locale (HYOK) e una versione di disponibilità generale dello scanner per gli archivi dati locali.

- Installare il client di Azure Information Protection (classico) se è necessaria una versione del client con funzionalità che non sono ancora disponibili con il client di etichettatura unificata. Il compromesso è che non è possibile usare le etichette su altre piattaforme client e sull'amministrazione usando un altro portale di gestione.

La versione di disponibilità generale più recente del client Unified Labeling consente di chiudere la parità nelle funzionalità con il client classico. Quando questo gap si chiude, è possibile aspettarsi che vengano aggiunte nuove funzionalità solo al client di etichettatura unificata. Per questo motivo, è consigliabile distribuire il client di etichettatura unificata se il set di funzionalità e le funzionalità correnti soddisfano i requisiti aziendali. In caso contrario, o se sono state configurate etichette nel portale di Azure di cui non è ancora stata [eseguita la migrazione nell'archivio Unified Labeling](../configure-policy-migrate-labels.md), usare il client classico.

È anche possibile installare entrambi i client nello stesso ambiente per supportare requisiti aziendali diversi, come illustrato nell'esempio seguente. Per questo scenario, è consigliabile eseguire la migrazione delle etichette nel portale di Azure in modo che entrambi i set di client condividano lo stesso set di etichette per semplificare l'amministrazione.

##### <a name="example-deployment-strategy"></a>Strategia di distribuzione di esempio:

- Per la maggior parte degli utenti, si distribuisce il Azure Information Protection client Unified Labeling perché questo client soddisfa le esigenze aziendali per questi utenti. 
    
    Per questi utenti, la loro esperienza di etichettatura è molto simile in Windows, Mac, iOS e Android, perché hanno le stesse etichette pubblicate e le stesse impostazioni dei criteri. In qualità di amministratore, le etichette e le impostazioni dei criteri vengono gestite nello stesso centro di gestione.

- Si installa anche il client di assegnazione di etichette unificato per testare la versione di anteprima dello scanner Azure Information Protection e le nuove funzionalità client.

- Per un subset di utenti, si distribuisce il client classico perché questi utenti richiedono etichette che applicano la protezione HYOK (Holding your own key).
    
    Per questi utenti hanno un'esperienza di etichettatura leggermente diversa quando usano questo client. Ad esempio, viene visualizzato un pulsante Proteggi anziché un pulsante di **riservatezza** nelle app di Office. In qualità di amministratore, è necessario gestire le etichette per le impostazioni di HYOK e le impostazioni dei criteri in un centro di gestione diverso per le etichette e le impostazioni per le altre piattaforme client.

- Sono presenti archivi dati locali con documenti che devono essere analizzati per ottenere informazioni riservate oppure classificati e protetti. Per l'uso in produzione, si distribuisce il client classico nei server per eseguire lo scanner Azure Information Protection.

### <a name="compare-the-clients"></a>Confrontare i client

Usare la tabella seguente per confrontare le funzionalità supportate dai due client Azure Information Protection.

|Funzionalità|Client classico|Client di etichetta unificato|
|-------|-----------------------------------|----------------------------------------------------|
|Azioni di assegnazione di etichette: manuali, consigliate, automatiche| Yes | Yes |
|Creazione di report centrale (analisi):| Yes | Sì, con limitazioni:<br /><br /> -I tipi di informazioni riservate personalizzate sono supportati con la versione di anteprima |
|Un visualizzatore per i file protetti (testo, immagini, PDF, Pfile):| Yes | Yes |
|Supporto multilingue per le etichette:| Yes | Yes |
|Ereditarietà delle etichette dagli allegati di posta elettronica:| Yes | Yes  |
|Personalizzazioni che includono:<br />- Etichetta predefinita per la posta elettronica<br />-Messaggi popup in Outlook <br />- Supporto S/MIME<br />- Opzione Segnala un problema| Yes <br /><br /> Supportato come [Impostazioni client avanzate che è possibile configurare nella portale di Azure](client-admin-guide-customizations.md#how-to-configure-advanced-client-configuration-settings-in-the-portal)| Yes <br /><br /> Supportato come [Impostazioni avanzate configurate con PowerShell](clientv2-admin-guide-customizations.md#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell) |
|Autorizzazioni definite dall'utente:| Yes | Yes |
|Scanner per gli archivi dati locali:| Yes | Sì-versione di anteprima |
|Autorizzazioni personalizzate:| Yes | Esplora file e PowerShell <br /><br /> Nelle app di Office, in alternativa, gli utenti possono selezionare **file info** > Proteggi il**documento** > **limitare l'accesso** o gli amministratori possono configurare un'etichetta per le autorizzazioni definite dall'utente|
|Barra di Information Protection nelle app Office:| Yes | Sì, con limitazioni:<br /><br /> - Nessun titolo o descrizione comando personalizzabile<br /><br /> -Il colore dell'etichetta non viene visualizzato per l'etichetta applicata a meno che non si usi la versione di anteprima|
|Le etichette permettono di applicare contrassegni visivi (intestazione, piè di pagina, filigrana):| Yes | Sì, con limitazioni:<br /><br /> - Le intestazioni e i piè di pagina non supportano le variabili per i valori dinamici <br /><br /> - Nessun supporto per l’impostazione di contrassegni visivi diversi per Word, Excel, PowerPoint e Outlook|
|Esplora file, azioni con il pulsante destro del mouse:| Yes | Sì, con limitazioni:<br /><br /> -Non è possibile proteggere i documenti PDF per il formato Ppdf precedente <br /><br />  - Nessun supporto per la modalità di sola protezione|
|Comandi di PowerShell:| Yes | Sì, con limitazioni:<br /><br />-Non è possibile rimuovere la protezione dai file contenitore (zip,. rar,. 7z,. msg e. pst)|
|Supporto offline per le azioni di protezione:| Yes | Sì, con limitazioni: <br /><br />- Per i comandi di Esplora File e PowerShell, l'utente deve essere connesso a Internet per proteggere i file. |
|Supporto per i computer disconnessi con gestione manuale dei file di criteri:| Yes |No |
|Supporto HYOK:| Yes | No <br /><br /> Le etichette di cui si esegue la migrazione dal portale di Azure e che sono configurate per la protezione HYOK vengono visualizzate dal client per l'etichettatura unificata Azure Information Protection, ma non applicano la protezione. |
|Registrazione dell'utilizzo nel Visualizzatore eventi:| Yes | No|
|Visualizzare il pulsante Non inoltrare in Outlook| Yes | No |
|Tenere traccia e revocare:| Yes | No |
|Modalità di sola protezione (nessuna etichetta) tramite i modelli:| Yes | No |
|Supporto per AD RMS:| Yes | È supportata solo l'azione seguente:<br /><br /> - Il visualizzatore può aprire i documenti protetti se si distribuisce l'[estensione per dispositivi mobili di Active Directory Rights Management Services](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn673574\(v=ws.11\))|

#### <a name="detailed-comparisons-for-the-clients"></a>Confronti dettagliati per i client

Quando entrambi i client supportano la stessa funzionalità, usare la tabella seguente per identificare alcune differenze funzionali tra i due client.

|Funzionalità |Client classico|Client di etichetta unificato|
|--------------|-----------------------------------|-----------------------------------------------------------|
|Configurazione:| Opzione per installare i criteri demo locali | Nessun criterio demo locale|
|Selezione e visualizzazione di etichette se applicate nelle app Office:|Dal pulsante **Proteggi** nella barra multifunzione <br /><br /> Dalla barra di Information Protection (barra orizzontale sotto la barra multifunzione)|Dal pulsante **Riservatezza** sulla barra multifunzione<br /><br /> Dalla barra di Information Protection (barra orizzontale sotto la barra multifunzione)|
|Gestione della barra di Information Protection nelle app Office:|Per gli utenti: <br /><br />- Opzione per visualizzare o nascondere la barra dal pulsante **Proteggi** sulla barra multifunzione<br /><br />- Quando un utente seleziona l'opzione per nascondere la barra, per impostazione predefinita, la barra viene nascosta in tale app, ma continua a essere automaticamente visualizzata nelle app appena aperte <br /><br /> Per gli amministratori: <br /><br />- Impostazioni dei criteri per visualizzare o nascondere automaticamente la barra quando un'app viene aperta per la prima volta e per controllare se la barra rimane automaticamente nascosta per le app appena aperte dopo che un utente ha selezionato l'opzione per nascondere la barra|Per gli utenti: <br /><br />- Opzione per visualizzare o nascondere la barra dal pulsante **Riservatezza** sulla barra multifunzione<br /><br />- Quando un utente seleziona l'opzione per nascondere la barra, la barra viene nascosta in tale app e anche nelle app appena aperte <br /><br />Per gli amministratori: <br /><br />-Impostazione di PowerShell per gestire la barra |
|Colore dell'etichetta: | Configurazione nel portale di Azure | Conservati dopo la migrazione dell'etichetta a Office 365 e configurabili con PowerShell <br /><br /> I colori possono essere configurati tramite [PowerShell](clientv2-admin-guide-customizations.md#specify-a-color-for-the-label)|
|Le etichette supportano lingue diverse:| Configurazione nel portale di Azure | Configurare usando Office 365 Sicurezza e conformità PowerShell e il parametro *LocaleSettings* per [New-Label](https://docs.microsoft.com/powershell/module/exchange/policy-and-compliance/new-label?view=exchange-ps) e [set-label](https://docs.microsoft.com/powershell/module/exchange/policy-and-compliance/set-label?view=exchange-ps)|
|Aggiornamento criteri: | Quando si apre un'app Office <br /><br /> Quando si fa clic con il pulsante destro del mouse per classificare e proteggere un file o una cartella <br /><br />Quando si eseguono i cmdlet di PowerShell per l'assegnazione di etichette e la protezione<br /><br />Ogni 24 ore | Quando si apre un'app Office <br /><br /> Quando si fa clic con il pulsante destro del mouse per classificare e proteggere un file o una cartella <br /><br />Quando si eseguono i cmdlet di PowerShell per l'assegnazione di etichette e la protezione<br /><br />Ogni 4 ore|
|Formati supportati per PDF:| Protezione: <br /><br /> - Standard ISO per la crittografia dei file PDF (impostazione predefinita) <br /><br /> - Estensione ppdf <br /><br /> Consumo: <br /><br /> - Standard ISO per la crittografia dei file PDF <br /><br />- Estensione ppdf<br /><br />- Protezione IRM SharePoint| Protezione: <br /><br /> - Standard ISO per la crittografia dei file PDF <br /><br /> <br /><br /> Consumo: <br /><br /> - Standard ISO per la crittografia dei file PDF <br /><br />- Estensione ppdf<br /><br />- Protezione IRM SharePoint|
|File protetti in modo generico (con estensione Pfile) aperti con il Visualizzatore:| Il file viene aperto nell'app originale, dove può essere visualizzato, modificato e salvato senza protezione | Il file viene aperto nell'app originale, dove può essere visualizzato e modificato, ma non salvato|
|Cmdlet supportati:| Cmdlet per l'assegnazione di etichette e i cmdlet per la sola protezione | Cmdlet per l'assegnazione di etichette:<br /><br />Set-AIPFileClassification, set-AIPFileLabel e Get-AIPFileStatus non supportano i percorsi di SharePoint a meno che non si usi la versione di anteprima <br /><br /> Set-AIPFileClassification e set-AIPFileLabel non supportano il parametro *owner* <br /><br /> È inoltre presente un singolo commento "No label to apply" per tutti gli scenari in cui non viene applicata un'etichetta <br /><br /> Set-AIPFileClassification supporta il parametro *whatIf* , in modo che possa essere eseguito in modalità di individuazione <br /><br /> Set-AIPFileLabel non supporta il parametro *EnableTracking* <br /><br /> Get-AIPFileStatus non restituisce informazioni sulle etichette da altri tenant e non visualizza il parametro *RMSIssuedTime*<br /><br />Inoltre, il parametro *LabelingMethod* per Get-AIPFileStatus Visualizza **Privileged** o **standard** anziché **Manual** o **Automatic**. Per altre informazioni, vedere la [documentazione online](/powershell/module/azureinformationprotection/get-aipfilestatus).|
|Richieste di giustificazione (se configurate) per ogni azione in Office: | Frequenza: per ogni file <br /><br /> Riduzione del livello di riservatezza <br /><br /> Rimozione di un'etichetta<br /><br /> Rimozione della protezione | Frequenza: per ogni sessione <br /><br /> Riduzione del livello di riservatezza<br /><br /> Rimozione di un'etichetta|
|Azioni di rimozione di etichette applicate: | Viene chiesta conferma all'utente <br /><br />L'etichetta predefinita o l'etichetta automatica (se configurata) non viene applicata automaticamente alla successiva apertura del file nell'app Office  <br /><br />| Non viene chiesta conferma all'utente<br /><br /> L'etichetta predefinita o l'etichetta automatica (se configurata) viene applicata automaticamente alla successiva apertura del file nell'app Office|
|Etichette automatiche e consigliate: | Configurata come [condizioni per le etichette](../configure-policy-classification.md) nel portale di Azure con i tipi di informazioni predefiniti e le condizioni personalizzate che usano frasi o espressioni regolari <br /><br />Le opzioni di configurazione possibili sono: <br /><br />- Conteggio univoco/non univoco <br /><br /> - Conteggio minimo| Configurata nei centri di amministrazione con i tipi di informazioni riservate predefiniti e i [tipi di informazioni personalizzati](https://docs.microsoft.com/office365/securitycompliance/create-a-custom-sensitive-information-type)<br /><br />Le opzioni di configurazione possibili sono:  <br /><br />- Solo conteggio univoco <br /><br />- Conteggio minimo e massimo <br /><br />- Supporto di AND e OR con i tipi di informazioni <br /><br />- Dizionario di parole chiave<br /><br />- Livello di attendibilità e prossimità dei caratteri personalizzabili|
|Suggerimento per i criteri personalizzabili per le etichette automatiche e consigliate: | Yes <br /><br />Usare il portale di Azure per sostituire il messaggio predefinito con gli utenti | No <br /><br /> Sebbene i centri di amministrazione dispongano di un'opzione per fornire un suggerimento personalizzato, questa opzione non è attualmente supportata dal client Unified Labeling|
|Modificare il livello di protezione predefinito dei file: | Yes <br /><br />È possibile utilizzare le [modifiche del registro di sistema](client-admin-guide-file-types.md#changing-the-default-protection-level-of-files) per eseguire l'override delle impostazioni predefinite di protezione nativa e generica | No |

Per un confronto dettagliato delle differenze di comportamento per specifiche impostazioni di protezione, vedere [confronto tra il comportamento delle impostazioni di protezione per un'etichetta](../configure-policy-migrate-labels.md#comparing-the-behavior-of-protection-settings-for-a-label).

#### <a name="features-not-planned-to-be-in-the-azure-information-protection-unified-labeling-client"></a>Funzionalità non previste nel client di Azure Information Protection Unified Labeling

Anche se il Azure Information Protection client di assegnazione unificata di etichette è ancora in fase di sviluppo, le seguenti funzionalità e differenze di comportamento rispetto al client classico non sono attualmente pianificate per essere disponibili nelle versioni future per il client Unified Labeling: 

- Supportare le app di Office per computer disconnessi con la gestione manuale dei file di criteri

- Autorizzazioni personalizzate come opzione separata che gli utenti possono selezionare nelle app di Office: Word, Excel e PowerPoint

- Rilevamento e revoca da app di Office ed Esplora file

- Titolo e descrizione comando della barra di Information Protection

- Modalità di sola protezione (nessuna etichetta) tramite i modelli

- Protezione del documento PDF come formato ppdf

- Visualizzazione del pulsante Non inoltrare in Outlook

- Criteri demo

- Giustificazione per la rimozione della protezione

- Richiesta **di conferma eliminare questa etichetta?** per gli utenti se non si usa l'impostazione dei criteri per la giustificazione

- Assegnazione di un'etichetta a un documento di Office tramite una proprietà personalizzata esistente (impostazioni client avanzate SyncPropertyName e SyncPropertyState)

- Separazione dei cmdlet PowerShell per la connessione a un servizio Rights Management


#### <a name="parent-labels-and-their-sublabels"></a>Etichette padre ed etichette secondarie 

Il client Azure Information Protection (classico) non supporta le configurazioni che specificano un'etichetta padre con etichette secondarie. Queste configurazioni includono la specifica di un'etichetta predefinita e un'etichetta per la classificazione consigliata o automatica. Quando un'etichetta ha etichette secondarie, è possibile specificare una delle etichette secondarie, ma non l'etichetta padre.

Per motivi di parità, nemmeno il client per l'etichettatura unificata di Azure Information Protection supporta l'applicazione di etichette padre con etichette secondarie, anche se è possibile selezionare queste etichette nei centri di amministrazione. In questo scenario il client di etichettatura unificata Azure Information Protection non applicherà l'etichetta padre.

## <a name="see-also"></a>Vedere anche
Quando sono necessarie altre informazioni su come distribuire e usare questi client, usare la documentazione seguente:

- [Client di Azure Information Protection](AIP-client.md)

- [Client per l'etichettatura unificata Azure Information Protection](unifiedlabelingclient-version-release-history.md)

- [Note sulla distribuzione del client RMS](client-deployment-notes.md)

Sebbene il client di Azure Information Protection (classico) possa essere usato con AD RMS, questo client è più adatto per lavorare con i servizi di Azure. Azure Information Protection e il servizio di protezione, Azure Rights Management. Per un confronto del lato servizio per Azure Information Protection, vedere [Confronto tra Azure Information Protection e AD RMS](../compare-on-premise.md).
