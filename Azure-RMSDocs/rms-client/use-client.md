---
title: Il client per Azure Information Protection - AIP
description: Microsoft Azure Information Protection offre una soluzione client-server che consente di proteggere i dati di un'organizzazione. Il client (di Azure Information Protection o di Rights Management) si integra con le applicazioni che vengono eseguite su computer e dispositivi mobili.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 06/23/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.suite: ems
ms.openlocfilehash: b51ebdb55212e2a29b6a8ce950bd69d578e98ed9
ms.sourcegitcommit: b92f60a87f824fc2da1e599f526898e3a0c919c3
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/24/2019
ms.locfileid: "67343684"
---
# <a name="the-client-side-of-azure-information-protection"></a>Lato client di Azure Information Protection

>*Si applica a: Active Directory Rights Management Services, [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8, Windows 7 con SP1, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2*

Azure Information Protection offre una soluzione client-server che consente di proteggere i documenti e i messaggi di posta elettronica di un'organizzazione:

- Il client può essere il client Azure Information Protection (versione classico), il client di assegnazione di etichette unificato di Azure Information Protection o il client Rights Management. A seconda di quale di questi client usate, si integra con le applicazioni che vengono eseguite su computer e dispositivi mobili. 
- Il servizio risiede nel cloud (Azure Information Protection, che usa il servizio Azure Rights Management per la protezione dei dati) o in locale (Active Directory Rights Management Services, più comunemente noto come AD RMS). 

Il client Azure Information Protection (versione classico) e il client di assegnazione di etichette unificato di Azure Information Protection supporta classificazione e protezione con l'assegnazione di etichette. Il client classico supporta anche la protezione senza l'assegnazione di etichette. Entrambi i client si integrano con le applicazioni di Office e devono essere installati separatamente.

Il client Rights Management (RMS) viene installato automaticamente con alcune applicazioni, ad esempio le applicazioni di Office, il client Azure Information Protection (versione classica) e client di assegnazione di etichette unificata di Azure Information Protection e applicazioni abilitate per RMS fornitori di software. Tuttavia può essere anche [installato da solo](https://www.microsoft.com/en-us/download/details.aspx?id=38396), per supportare la [sincronizzazione dei file tra le librerie protette da IRM e OneDrive for Business](https://support.office.com/article/Deploy-the-new-OneDrive-sync-client-in-an-enterprise-environment-3f3a511c-30c6-404a-98bf-76f95c519668) e per gli sviluppatori che vogliono integrare la protezione di Rights Management nelle applicazioni line-of-business.

## <a name="choose-which-azure-information-protection-client-to-use"></a>Scegliere il client Azure Information Protection da usare

Il **client Azure Information Protection (versione classica)** Scarica le etichette e le impostazioni dei criteri dal portale di Azure. Per altre informazioni su questo client, vedere il [client Azure Information Protection: Cronologia delle versioni e criteri per il supporto](client-version-release-history.md).

Il **client per l'etichettatura unificata Azure Information Protection** scarica le etichette e le impostazioni dei criteri dai centri di amministrazione: Centro sicurezza e conformità di Office 365, Centro sicurezza Microsoft 365 e Centro conformità Microsoft 365. Per altre informazioni su questo client, vedere il [unificata di Azure Information Protection client l'assegnazione di etichette: informazioni di rilascio versione](unifiedlabelingclient-version-release-history.md).

Quale client è opportuno installare?

- Installare la versione di disponibilità corrente del client l'assegnazione di etichette unificata di Azure Information Protection per etichette che possono anche essere usato da MacOS, iOS e Android e se non sono necessarie funzionalità avanzate, ad esempio advanced impostazioni client, le autorizzazioni definite dall'utente, una chiave in locale (HYOK) o lo scanner per gli archivi dati locali.
    
    La versione di anteprima del client di assegnazione di etichette unificata di Azure Information Protection supporta le impostazioni del client avanzato e le autorizzazioni definite dall'utente, ma non una chiave in locale (HYOK) o lo scanner per i dati in locale vengono archiviati.

- Installare il client Azure Information Protection (versione classica) se è necessaria una versione del client che è a livello generale con funzionalità avanzate che non sono ancora disponibili nel client di assegnazione di etichette unificato di disponibilità generale corrente. Il compromesso è che le etichette possono essere utilizzate in altre piattaforme client.

Il client classico e il client di assegnazione di etichette unificato non sono attualmente parità per le relative funzionalità. Tuttavia, con la versione di anteprima corrente, questo divario e sarà possibile nuove funzionalità per essere aggiunto solo a client unificato imprevisto delle etichette. Per questo motivo, è consigliabile che distribuire il client di assegnazione di etichette unificato se set di funzionalità correnti e le funzionalità di soddisfare i requisiti aziendali. In caso contrario, o se è stato configurato le etichette nel portale di Azure che non si è ancora [migrate nell'archivio di assegnazione di etichette unificata](../configure-policy-migrate-labels.md), usare il client di classico.

È anche possibile installare entrambi i client nello stesso ambiente per supportare differenti requisiti aziendali, come illustrato nell'esempio seguente. Per questo scenario, si consiglia di che migrare le etichette nel portale di Azure in modo che entrambi i set di client di condividono lo stesso set di etichette per facilitare l'amministrazione.

##### <a name="example-deployment-strategy"></a>Strategia di distribuzione di esempio:

- Per la maggior parte degli utenti, si distribuisce il client di assegnazione di etichette unificato di Azure Information Protection perché la maggior parte degli utenti non richiedono funzionalità che sono disponibili solo con il client Azure Information Protection (versione classica). 
    
    Per questi utenti, l'esperienza di assegnazione di etichette è molto simile se dispongono anche i dispositivi che eseguono MacOS, iOS e Android, e questi dispositivi hanno una versione di Office che supporta le etichette di riservatezza.

- Per usufruire installare la versione di anteprima del client unificato imprevisto delle etichette per testare le nuove funzionalità che includono le autorizzazioni definite dall'utente e impostazioni client avanzate.

- Per un subset di utenti, si distribuisce il client classico perché gli utenti richiedono le etichette che applicano tenere premuto il proprio protezione con chiave (HYOK) o un prompt dei comandi per le autorizzazioni definite dall'utente.
    
    Per i quali dispongono di funzionalità e caratteristiche aggiuntive, ma un'esperienza leggermente diversa se dispongono anche i dispositivi che eseguono MacOS, iOS e Android e questi dispositivi è installata una versione di Office che supporta le etichette di riservatezza. Ad esempio, viene visualizzato un **Protect** pulsante anziché un **sensibilità** pulsante sulla barra multifunzione di Office e la barra di Information Protection può essere visualizzato per impostazione predefinita.

- Si dispone di archivi dati locali con i documenti che devono essere analizzati alla ricerca di informazioni riservate, o classificati e protetti. Distribuire il client nei server classico per eseguire lo scanner Azure Information Protection.

### <a name="compare-the-clients"></a>Confrontare i client

Usare la tabella seguente per poter confrontare le funzionalità supportate dai due client Azure Information Protection.

|Funzionalità|Client classico|client unificato di assegnazione di etichette|
|-------|-----------------------------------|----------------------------------------------------|
|Azioni di assegnazione di etichette: manuali, consigliate, automatiche| Yes | Yes |
|Creazione di report centrale (analisi):| Yes | Sì, con limitazioni:<br /><br /> -Nessun supporto per [corrispondenze nel contenuto](../reports-aip.md#content-matches-for-deeper-analysis) |
|Reimpostazione delle impostazioni ed esportazione dei log:| Yes | Yes |
|Autorizzazioni definite dall'utente:| Yes | Sì, con limitazioni: <br /><br />-Per Outlook solo (Do Not Forward): Supportato<br /><br />-Per Word, Excel, PowerPoint e File Explorer: Con il client di anteprima è supportata quando si configura l'etichetta nel portale di Azure |
|Autorizzazioni personalizzate:| Yes | Esplora file e PowerShell (versione di anteprima) <br /><br /> In alternativa, nelle app Office gli utenti possono selezionare **Info sul file** > **Proteggi documento** > **Limita accesso** |
|Barra di Information Protection nelle app Office:| Yes | Sì, con limitazioni:<br /><br /> - Nessun titolo o descrizione comando personalizzabile<br /><br /> - Colore dell'etichetta non visualizzato per l'etichetta applicata|
|Le etichette permettono di applicare contrassegni visivi (intestazione, piè di pagina, filigrana):| Yes | Sì, con limitazioni:<br /><br /> - Le intestazioni e i piè di pagina non supportano le variabili per i valori dinamici <br /><br /> - Nessun supporto per l’impostazione di contrassegni visivi diversi per Word, Excel, PowerPoint e Outlook|
|Esplora file, azioni con il pulsante destro del mouse:| Yes | Sì, con limitazioni:<br /><br /> - Non è possibile proteggere i documenti PDF in formato ppdf <br /><br />  - Nessun supporto per la modalità di sola protezione|
|Visualizzatore per i file protetti:| Yes | Sì, con limitazioni:<br /><br /> -Per i file protetti in modo generico (. pfile), a differenza di Visualizzatore dal client classico, non è possibile salvare le modifiche apportate al file aperto originariamente.|
|Comandi di PowerShell:| Yes | Sì, con limitazioni:<br /><br />- Cmdlet inclusi: [Get-AIPFileStatus](/powershell/module/azureinformationprotection/get-aipfilestatus), [New-AIPCustomPermissions](/powershell/module/azureinformationprotection/New-AIPCustomPermissions) (client di anteprima) [Set-AIPFileClassification](/powershell/module/azureinformationprotection/set-aipfileclassification), [Set-AIPFileLabel](/powershell/module/azureinformationprotection/set-aipfilelabel), [ Set-AIPAuthentication](/powershell/module/azureinformationprotection/set-aipauthentication) <br /><br />-Attualmente, non è possibile rimuovere la protezione dai file contenitore (con estensione zip, RAR, 7z,. MSG e pst)|
|Supporto offline per le azioni di protezione:| Yes | Sì, con limitazioni: <br /><br />- Per i comandi di Esplora File e PowerShell, l'utente deve essere connesso a Internet per proteggere i file. |
|Supporto per i computer disconnessi con gestione manuale dei file di criteri:| Yes |No |
|Supporto HYOK:| Yes | No<br /><br /> Le etichette di cui si esegue la migrazione dal portale di Azure e che sono configurate per la protezione HYOK vengono visualizzate dal client per l'etichettatura unificata Azure Information Protection, ma non applicano la protezione. |
|Registrazione dell'utilizzo nel Visualizzatore eventi:| Yes | No|
|Ereditarietà delle etichette dagli allegati di posta elettronica:| Yes | Sì (solo client di anteprima) |
|Visualizzazione del pulsante Non inoltrare in Outlook| Yes | No |
|[Personalizzazioni](client-admin-guide-customizations.md#available-advanced-client-settings) che includono:<br />- Etichetta predefinita per la posta elettronica<br />- Abilitazione delle autorizzazioni personalizzate <br />- Supporto S/MIME<br />- Opzione Segnala un problema| Yes | Sì, usando [PowerShell](clientv2-admin-guide-customizations.md#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell) (solo client di anteprima) |
|Scanner per gli archivi dati locali:| Yes | No |
|Tenere traccia e revocare:| Yes | No |
|Modalità di sola protezione modalità (senza etichette) usando i modelli:| Yes | No |
|Supporto multilingue:| Yes | No |
|Supporto per AD RMS:| Yes | È supportata solo l'azione seguente:<br /><br /> - Il visualizzatore può aprire i documenti protetti se si distribuisce l'[estensione per dispositivi mobili di Active Directory Rights Management Services](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn673574\(v=ws.11\))|

#### <a name="detailed-comparisons-for-the-clients"></a>Confronti dettagliati per i client

Quando entrambi i client supportano la funzionalità stessa, usare la tabella seguente per identificare alcune differenze funzionali tra i due client.

|Funzionalità |Client classico|client unificato di assegnazione di etichette|
|--------------|-----------------------------------|-----------------------------------------------------------|
|Configurazione:| Opzione per installare i criteri demo locali | Nessun criterio demo locale|
|Selezione e visualizzazione di etichette se applicate nelle app Office:|Dal pulsante **Proteggi** nella barra multifunzione <br /><br /> Dalla barra di Information Protection (barra orizzontale sotto la barra multifunzione)|Dal pulsante **Riservatezza** sulla barra multifunzione<br /><br /> Dalla barra di Information Protection (barra orizzontale sotto la barra multifunzione)|
|Gestione della barra di Information Protection nelle app Office:|Per gli utenti: <br /><br />- Opzione per visualizzare o nascondere la barra dal pulsante **Proteggi** sulla barra multifunzione<br /><br />- Quando un utente seleziona l'opzione per nascondere la barra, per impostazione predefinita, la barra viene nascosta in tale app, ma continua a essere automaticamente visualizzata nelle app appena aperte <br /><br /> Per gli amministratori: <br /><br />- Impostazioni dei criteri per visualizzare o nascondere automaticamente la barra quando un'app viene aperta per la prima volta e per controllare se la barra rimane automaticamente nascosta per le app appena aperte dopo che un utente ha selezionato l'opzione per nascondere la barra|Per gli utenti: <br /><br />- Opzione per visualizzare o nascondere la barra dal pulsante **Riservatezza** sulla barra multifunzione<br /><br />- Quando un utente seleziona l'opzione per nascondere la barra, la barra viene nascosta in tale app e anche nelle app appena aperte <br /><br />Per gli amministratori: <br /><br />-Impostazione PowerShell per gestire la barra (solo client di anteprima)|
|Colore dell'etichetta: | Configurazione nel portale di Azure | Mantenuti dopo la migrazione di etichette di Office 365 e possono essere configurate con PowerShell <br /><br /> Nuove etichette create le interfacce di amministrazione non è un colore, ma i colori possono essere configurati tramite [PowerShell](clientv2-admin-guide-customizations.md#specify-a-color-for-the-label)|
|Aggiornamento criteri: | Quando si apre un'app Office <br /><br /> Quando si fa clic con il pulsante destro del mouse per classificare e proteggere un file o una cartella <br /><br />Quando si eseguono i cmdlet di PowerShell per l'assegnazione di etichette e la protezione<br /><br />Ogni 24 ore | Quando si apre un'app Office <br /><br /> Quando si fa clic con il pulsante destro del mouse per classificare e proteggere un file o una cartella <br /><br />Quando si eseguono i cmdlet di PowerShell per l'assegnazione di etichette e la protezione<br /><br />Ogni 4 ore|
|Formati supportati per PDF:| Protezione: <br /><br /> - Standard ISO per la crittografia dei file PDF (impostazione predefinita) <br /><br /> - Estensione ppdf <br /><br /> Consumo: <br /><br /> - Standard ISO per la crittografia dei file PDF <br /><br />- Estensione ppdf<br /><br />- Protezione IRM SharePoint| Protezione: <br /><br /> - Standard ISO per la crittografia dei file PDF <br /><br /> <br /><br /> Consumo: <br /><br /> - Standard ISO per la crittografia dei file PDF <br /><br />- Estensione ppdf<br /><br />- Protezione IRM SharePoint|
|Cmdlet supportati:| Tutti i cmdlet documentati per [AzureInformatioProtection](/powershell/module/azureinformationprotection) | Set-AIPAuthentication supporta le sessioni non interattive usando solo il client di anteprima <br /><br /> Set-AIPFileClassification e Set-AIPFileLabel non supportano il parametro *Owner* o le librerie di SharePoint Server <br /><br /> È inoltre presente un singolo commento "No label to apply" per tutti gli scenari in cui non viene applicata un'etichetta <br /><br /> Set-AIPFileClassification nel client di anteprima supporta il *WhatIf* parametro, pertanto può essere eseguito in modalità di individuazione <br /><br /> Set-AIPFileLabel non supporta il parametro *EnableTracking* <br /><br /> Get-AIPFileStatus non restituisce informazioni sulle etichette da altri tenant e non visualizza il parametro *RMSIssuedTime*<br /><br />Inoltre, il *LabelingMethod* parametro per Get-AIPFileStatus Visualizza **con privilegi** o **Standard** anziché **manuale** o **Automatica**. Per altre informazioni, vedere la [documentazione online](/powershell/module/azureinformationprotection/get-aipfilestatus).|
|Richieste di giustificazione (se configurate) per ogni azione in Office: | Frequenza: per ogni file <br /><br /> Riduzione del livello di riservatezza <br /><br /> Rimozione di un'etichetta<br /><br /> Rimozione della protezione | Frequenza: per ogni sessione <br /><br /> Riduzione del livello di riservatezza<br /><br /> Rimozione di un'etichetta|
|Azioni di rimozione di etichette applicate: | Viene chiesta conferma all'utente <br /><br />L'etichetta predefinita o l'etichetta automatica (se configurata) non viene applicata automaticamente alla successiva apertura del file nell'app Office  <br /><br />| Non viene chiesta conferma all'utente<br /><br /> L'etichetta predefinita o l'etichetta automatica (se configurata) viene applicata automaticamente alla successiva apertura del file nell'app Office|
|Etichette automatiche e consigliate: | Configurata come [condizioni per le etichette](../configure-policy-classification.md) nel portale di Azure con i tipi di informazioni predefiniti e le condizioni personalizzate che usano frasi o espressioni regolari <br /><br />Le opzioni di configurazione possibili sono: <br /><br />- Conteggio univoco/non univoco <br /><br /> - Conteggio minimo| Configurata nei centri di amministrazione con i tipi di informazioni riservate predefiniti e i [tipi di informazioni personalizzati](https://docs.microsoft.com/office365/securitycompliance/create-a-custom-sensitive-information-type)<br /><br />Le opzioni di configurazione possibili sono:  <br /><br />- Solo conteggio univoco <br /><br />- Conteggio minimo e massimo <br /><br />- Supporto di AND e OR con i tipi di informazioni <br /><br />- Dizionario di parole chiave<br /><br />- Livello di attendibilità e prossimità dei caratteri personalizzabili|
|Suggerimento per i criteri personalizzabili per le etichette automatiche e consigliate: | Yes <br /><br />Usare il portale di Azure per sostituire il messaggio predefinito per gli utenti | No <br /><br /> Anche se le interfacce di amministrazione hanno un'opzione per fornire un suggerimento per i criteri personalizzati, questa opzione non è attualmente supportata dal client di assegnazione di etichette unificato|
|Modificare il livello di protezione predefinito dei file: | Yes <br /><br />È possibile usare [il Registro di sistema](client-admin-guide-file-types.md#changing-the-default-protection-level-of-files) sostituire i valori predefiniti di protezione nativa e generica | No |

Per un confronto dettagliato delle differenze di comportamento per le impostazioni di protezione dati specifico, vedere [confronto tra il comportamento delle impostazioni di protezione per un'etichetta](../configure-policy-migrate-labels.md#comparing-the-behavior-of-protection-settings-for-a-label).

#### <a name="features-not-planned-to-be-in-the-azure-information-protection-unified-labeling-client"></a>Funzionalità non è prevista la nel client per l'assegnazione di etichette unificato di Azure Information Protection

Anche se il client di assegnazione di etichette unificato di Azure Information Protection è ancora in fase di sviluppo, le seguenti funzionalità e differenze di comportamento del client classico non sono attualmente previsti siano disponibili nelle versioni future del client di assegnazione di etichette unificata: 

- Autorizzazioni personalizzate nelle app di Office: Word, Excel e PowerPoint

- Rilevamento e revoca da app di Office ed Esplora file

- Titolo e descrizione comando della barra di Information Protection

- Modalità di sola protezione modalità (senza etichette) usando i modelli

- Protezione del documento PDF come formato ppdf

- Visualizzazione del pulsante Non inoltrare in Outlook

- Criteri demo

- Giustificazione per la rimozione della protezione

- Richiesta di conferma **si desidera eliminare questa etichetta?** per gli utenti quando non si usa l'impostazione di criteri per la giustificazione

- Assegnazione di un'etichetta a un documento di Office tramite una proprietà personalizzata esistente (impostazioni client avanzate SyncPropertyName e SyncPropertyState)

- Separazione dei cmdlet PowerShell per la connessione a un servizio Rights Management


#### <a name="parent-labels-and-their-sublabels"></a>Etichette padre ed etichette secondarie 

Il client Azure Information Protection (versione classico) non supporta le configurazioni che specificano un'etichetta padre con etichette secondarie. Queste configurazioni includono la specifica di un'etichetta predefinita e un'etichetta per la classificazione consigliata o automatica. Quando un'etichetta ha etichette secondarie, è possibile specificare una delle etichette secondarie, ma non l'etichetta padre.

Per motivi di parità, nemmeno il client per l'etichettatura unificata di Azure Information Protection supporta l'applicazione di etichette padre con etichette secondarie, anche se è possibile selezionare queste etichette nei centri di amministrazione. In questo scenario il client di etichettatura unificata Azure Information Protection non applicherà l'etichetta padre.

## <a name="see-also"></a>Vedere anche
Quando sono necessarie altre informazioni su come distribuire e usare questi client, usare la documentazione seguente:

- [Client di Azure Information Protection](AIP-client.md)

- [Client per l'etichettatura unificata Azure Information Protection](unifiedlabelingclient-version-release-history.md)

- [Note sulla distribuzione del client RMS](client-deployment-notes.md)

Anche se il client Azure Information Protection (versione classico) può essere usato con AD RMS, questo client è ideale per lavorare con i servizi di Azure; Azure Information Protection e il relativo servizio di protezione dati, Azure Rights Management. Per un confronto del lato servizio per Azure Information Protection, vedere [Confronto tra Azure Information Protection e AD RMS](../compare-on-premise.md).
