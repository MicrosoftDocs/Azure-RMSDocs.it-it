---
title: Domande frequenti per Azure Information Protection (anteprima) | Azure Information Protection
description: Domande sulla versione di anteprima di Azure Information Protection e relative risposte.
author: cabailey
manager: mbaldwin
ms.date: 08/22/2016
ms.topic: article
ms.prod: 
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 4b595b6a-7eb0-4438-b49a-686431f95ddd
ms.reviewer: adhall
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: c9f9211e7c1dcf293caf81475515114b5433d6a7
ms.openlocfilehash: 55d56786150d38b36ae8185c4a7ac4c8a5c51ba4


---

# Domande frequenti per Azure Information Protection (anteprima)

>*Si applica a: Azure Information Protection (anteprima)*

**[ Informazioni preliminari soggette a modifiche. ]**

Domande sulla versione di anteprima di Azure Information Protection  e relative risposte. 

Si prevede che questo elenco verrà aggiornato frequentemente, con lo spostamento di alcune informazioni all'interno della documentazione principale e l'inserimento di nuove domande dei clienti. 

## Cosa è possibile fare con la versione di anteprima di Azure Information Protection e quali sono le limitazioni attuali?

Questa versione di anteprima aggiunge alle applicazioni di Microsoft Office la barra di Information Protection, che consente di visualizzare e modificare le etichette di classificazione assegnate ai dati. La classificazione può essere eseguita manualmente o, scelta consigliata, applicata automaticamente. I dati corrispondenti alle classificazioni specificate possono essere protetti tramite un modello di Azure Rights Management.  

Le etichette e il comportamento delle classificazioni vengono configurati nel portale di Azure. È possibile usare criteri predefiniti per valutare molto rapidamente Azure Information Protection. In alternativa, è possibile creare criteri completamente personalizzati. È possibile modificare i colori, i nomi e l'ordine delle etichette di classificazione visibili agli utenti. È anche possibile configurare descrizioni e contrassegni visivi di classificazione, ad esempio l'intestazione, il piè di pagina o una filigrana.

L'esercitazione introduttiva consente in pochi minuti di vedere queste caratteristiche in pratica: [Esercitazione introduttiva di Azure Information Protection](infoprotect-quick-start-tutorial.md).

Si noti che l'anteprima consente di provare il nuovo **piano di servizio Premium P2** e che alcune funzionalità avanzate, ad esempio l'aggiunta automatica di etichette e l'aggiunta di etichette consigliate, potrebbero non essere disponibili nel piano corrente al momento della disponibilità generale. Per informazioni sui diversi piani di servizio (Azure Information Protection Premium P1 e Azure Information Protection Premium P2), vedere il post di blog seguente: [Introducing Enterprise Mobility + Security](https://blogs.technet.microsoft.com/enterprisemobility/2016/07/07/introducing-enterprise-mobility-security/) (Introduzione alla mobilità aziendale + sicurezza).

Questa versione di anteprima presenta le limitazioni seguenti. Per sapere quando saranno disponibili altre funzionalità e nuove caratteristiche, seguire gli annunci in [Enterprise Mobility and Security Blog](https://blogs.technet.microsoft.com/enterprisemobility/?product=azure-information-protection) (blog sulla mobilità e la sicurezza aziendale) e nel [sito Yammer](https://www.yammer.com/askipteam/#/threads/inGroup?type=in_group&feedId=8652489&view=all):

- Manca la funzione di registrazione centralizzata per la classificazione e l'aggiunta di etichette.

- I nomi e le descrizioni delle etichette sono supportati solo in una lingua.

- Le condizioni per la classificazione automatica devono essere frasi o motivi.

- Non è possibile classificare i file da Esplora File di Windows.

- Le app di Office per dispositivi mobili (iOS e Android) e computer Mac e le Office Web App (Office Online) non sono ancora supportati.

- Nessuna integrazione con Exchange Online o SharePoint Online.

- L'SDK per partner e sviluppatori non è disponibile.

## Quale sottoscrizione mi serve per provare Azure Information Protection?

Per la versione di anteprima, è possibile usare qualsiasi sottoscrizione di Office 365 che include la protezione di documenti e messaggi di posta elettronica di Office mediante Azure Rights Management. Azure Information Protection è disponibile in tutte le aree. Per altre informazioni sulle opzioni di sottoscrizione disponibili e sui collegamenti alle versioni di valutazione gratuite, vedere la sezione relativa alla [sottoscrizione di Office 365](../get-started/requirements-subscriptions.md#office-365-subscription) nella documentazione sui requisiti per Azure RMS.

Per configurare i criteri di Azure Information Protection nel portale di Azure è necessaria una sottoscrizione di Azure. Se l'organizzazione non ha una sottoscrizione di Azure, è possibile ottenerne una registrandosi per una versione di valutazione gratuita: andare alla pagina [Microsoft Azure - Introduzione](https://account.windowsazure.com/organization) e seguire le istruzioni.

Qualsiasi modifica ai requisiti di sottoscrizione verrà annunciata in [Enterprise Mobility and Security Blog](https://blogs.technet.microsoft.com/enterprisemobility/?product=azure-information-protection) (blog sulla mobilità e la sicurezza aziendale).

## Devo essere un amministratore globale per provare l'anteprima di Azure Information Protection?

Per la sola versione di anteprima, qualsiasi utente autenticato da Azure può visualizzare e configurare i criteri di Azure Information Protection del tenant per la classificazione e l'aggiunta di etichette nel portale di Azure. Tuttavia, per configurare un'etichetta da applicare a un modello di Azure Rights Management, è necessario accedere come amministratore globale di Azure Active Directory.

Se al momento dell'installazione del [client di Azure Information Protection](https://www.microsoft.com/en-us/download/details.aspx?id=53018) si sceglie di installare i criteri demo, per provare l'anteprima non è neanche necessario accedere al portale. I criteri demo installano in locali il criterio predefinito di Azure Information Protection. È quindi possibile provare ad aggiungere etichette a documenti e a messaggi di posta elettronica, ma per modificare etichette o aggiungerne di nuove sarà necessario accedere al portale di Azure. 

Se si vogliono proteggere i documenti e i messaggi di posta elettronica classificati e con etichette e Azure Rights Management non è stato ancora attivato, il processo di attivazione richiede autorizzazioni di amministratore speciali. Per altre informazioni, vedere [È necessario essere un amministratore globale per configurare Azure RMS oppure tale configurazione può essere delegata ad altri amministratori?](../get-started/faqs.md#do-you-need-to-be-a-global-admin-to-configure-azure-rms-or-can-i-delegate-to-other-administrators)


## Azure Information Protection supporta scenari locali e ibridi?

Azure Information Protection è una soluzione basata sul cloud. Se si è interessati a distribuire Azure Information Protection per uno scenario ibrido, contattare il team di Information Protection inviando un messaggio di posta elettronica all'indirizzo askipteam@microsoft.com.

## Quali piattaforme e applicazioni client sono supportate da Azure Information Protection?

Questa informazione è ora documentata e verrà aggiornata in [Requisiti per Azure Information Protection](requirements-azure-infoprotect.md).


## In che modo i computer ottengono le informazioni relative ai criteri da Azure Information Protection e con quale frequenza le informazioni vengono aggiornate?

Ogni volta che l'utente apre un'applicazione di Office, il client di Azure Information Protection verifica la disponibilità di una versione più recente dei criteri di Azure Information Protection. Se è disponibile una versione più recente, il client la scarica tramite un collegamento HTTPS per proteggere i dati. 

Se sono caricate più istanze dell'applicazione di Office quando viene pubblicato un nuovo criterio di Azure Information Protection, è necessario chiudere tutte le istanze per ottenere la versione più recente dei criteri. Se ad esempio sono aperti due documenti di Word e si vogliono testare i criteri aggiornati di Azure Information Protection in un solo documento, chiudere entrambi i documenti di Word e riaprire quello da usare con i criteri più recenti.

## Dove è possibile archiviare i file da usare con Azure Information Protection? 

Azure Information Protection applica protezione ed etichette persistenti ai file e ai messaggi di posta elettronica. La posizione di archiviazione dei file non è importante.

## È possibile classificare solo nuovi dati o è possibile classificare anche i dati esistenti?

Le azioni dei criteri di Azure Information Protection vengono eseguite al momento del salvataggio dei documenti e dell'invio dei messaggi di posta elettronica, sia per il nuovo contenuto che per le modifiche apportate al contenuto esistente. 

Se i file che si vogliono classificare sono stati salvati, è sufficiente aprirli e salvarli in un'applicazione di Office. 

Attualmente non è possibile eseguire l'analisi e applicare la classificazione in blocco, ma è necessario aprire e salvare ogni documento nell'applicazione di Office. 

## È possibile usare Azure Information Protection solo per la classificazione, senza applicare la crittografia, e limitare i diritti di utilizzo?

Sì. È possibile configurare un criterio di Azure Information Protection che si limiti ad applicare un'etichetta. In effetti si prevede che questo sarà il caso più frequente per le reti di distribuzione in cui è necessario proteggere solo il subset dei documenti e dei messaggi di posta elettronica che richiedono una gestione dei dati particolare.

## Come funziona la classificazione automatica?

Nel portale di Azure è possibile usare motivi predefiniti, ad esempio numeri di carta di credito o codici fiscali. In alternativa, è possibile definire una stringa o un modello personalizzato come condizione per la classificazione automatica.

Un esempio di questa funzione è presente nell'[Esercitazione introduttiva di Azure Information Protection](infoprotect-quick-start-tutorial.md). 

L'accuratezza della classificazione dipende dalla configurazione della regola di classificazione, che si basa su condizioni. Attualmente le condizioni supportano motivi di testo ed espressioni regolari. Per una spiegazione delle opzioni disponibili durante l'anteprima, con alcuni esempi consigliati da provare, vedere [Come configurare le condizioni per la classificazione automatica e consigliata per Azure Information Protection](configure-policy-classification.md). Il rilevamento viene eseguito quando il documento viene salvato o quando il messaggio di posta elettronica viene inviato.

Per ottenere la migliore esperienza utente e garantire la continuità aziendale, è consigliabile iniziare con azioni con consigli per gli utenti anziché con azioni completamente automatiche. In questo modo gli utenti possono accettare l'azione di aggiunta di etichette o di protezione oppure possono ignorare i suggerimenti.   

## Azure Information Protection può richiedere agli utenti di classificare i file personalmente, anziché usare la classificazione automatica? 

Sì. Tramite il portale di Azure configurare se usare la classificazione automatica o offrire consigli agli utenti. A tale scopo impostare l'opzione **Select how this label is applied: automatically or recommended to user** (Selezionare come applicare l'etichetta: automaticamente o consigliata all'utente) su **Recommended** (Consigliata).

Un esempio di questa funzione è presente nell'[Esercitazione introduttiva di Azure Information Protection](infoprotect-quick-start-tutorial.md).  

## È possibile forzare la classificazione di tutti i documenti?

Sì. Se è necessario che gli utenti classifichino tutti i file che salvano, nel portale di Azure impostare l'opzione **All documents and emails must have a label** (Tutti i documenti e i messaggi di posta elettronica devono avere un'etichetta) su **On**. 

## È possibile rimuovere la classificazione da un file?

Sì. Per rimuovere la classificazione da un file, aprire il file nell'applicazione di Office, fare clic sull'icona **Modifica etichetta** sulla barra Information Protection, fare clic sull'icona **Rimuovi etichetta** e quindi fare clic su **OK** per confermare l'azione. 


## È possibile richiedere agli utenti di giustificare il motivo per cui stanno modificando il livello di classificazione?

Sì. Per assicurarsi che gli utenti giustifichino la modifica della classificazione, nel portale di Azure impostare l'opzione **Users must provide justification when lowering the sensitivity level** (Gli utenti devono giustificare l'abbassamento del livello di riservatezza) su **On**. Quando si esegue questa operazione, il motivo dell'azione e la giustificazione vengono registrati nel registro eventi di Windows locale: **Application** > **Microsoft Azure Information Protection**.

## Come posso proteggere automaticamente il contenuto dopo che è stato classificato?

Per proteggere automaticamente il contenuto a seconda del livello di classificazione specificato, nel portale di Azure è possibile selezionare un modello di Azure Rights Management.

Un esempio di questa funzione è presente nell'[Esercitazione introduttiva di Azure Information Protection](infoprotect-quick-start-tutorial.md). Per altre informazioni, vedere [Come configurare un'etichetta per applicare la protezione di Rights Management](configure-policy-protection.md).

## È possibile assegnare a un file due classificazioni diverse?

Se necessario, è possibile creare etichette secondarie per descrivere meglio le sottocategorie per un'etichetta di riservatezza specifica. Ad esempio, l'etichetta principale **Secret** (Segreto) può contenere etichette secondarie quali **Secret – Legal** (Segreto: legale) e **Secret – Finance** (Segreto: finanziario). È quindi possibile applicare contrassegni visivi di classificazione diversi e modelli di Rights Management diversi a etichette secondarie diverse.

Anche se è attualmente possibile impostare contrassegni visivi, protezione e condizioni a entrambi i livelli, quando si usano sottolivelli è necessario configurare queste impostazioni solo in corrispondenza del livello secondario. Se si configurano le stesse impostazioni per l'etichetta padre e per il sottolivello corrispondente, le impostazioni di quest'ultimo hanno la precedenza.

## Come è possibile integrare soluzioni DLP e altre applicazioni con Azure Information Protection?

Per la classificazione, Azure Information Protection usa metadati persistenti che includono un'etichetta di testo non crittografata. Queste informazioni possono essere lette da soluzioni DLP e da altre applicazioni. Per i file, questi metadati vengono archiviati all'interno di proprietà personalizzate, per i messaggi di posta elettronica nelle intestazioni dei messaggi.

## Come funzionano il rilevamento e la revoca dei documenti in Azure Information Protection?

Il rilevamento dei documenti per i file classificati e protetti tramite Azure Information Protection funziona allo stesso modo che in Azure Rights Management e nell'applicazione RMS sharing. È inoltre possibile accedere al sito di rilevamento dei documenti tramite il client di Azure Information Protection versione 1.0.233 o successiva: 

- In un'applicazione di Office, nel gruppo **Protezione** della scheda **Home** fare clic su **Proteggi** > **Rileva utilizzo**. 

Per altre informazioni, vedere [Rilevare e revocare i documenti quando si usa l'applicazione di condivisione RMS](../rms-client/sharing-app-track-revoke.md).

## In che modo Azure Information Protection applica i criteri configurati dall'utente?

Quando un documento è protetto da un modello di Azure Rights Management, viene prima eseguita l'autenticazione dell'utente per verificare che disponga dei diritti necessari per il documento, quindi l'applicazione applica i criteri dei diritti di utilizzo. 

## In che modo Azure Information Protection usa Azure Active Directory?

Azure Information Protection usa Azure Active Directory per eseguire l'autenticazione utente.

## È possibile avere il controllo su quali utenti possono usare Azure Information Protection per classificare e proteggere il contenuto?

È possibile limitare gli utenti che possono classificare e proteggere i dati controllando la distribuzione del client di Azure Information Protection. 

I file e i messaggi di posta elettronica classificati da Azure Information Protection possono essere usati o modificati da qualsiasi utente, con o senza client Azure Information Protection installato. 

## Come posso segnalare un problema o inviare commenti e suggerimenti per questa versione di anteprima?

Se si individua un problema durante l'uso di questa versione di anteprima, nel gruppo **Protezione** della scheda **Home** dell'applicazione di Office fare clic su **Proteggi** e quindi fare clic su **Guida e commenti e suggerimenti**. Nella finestra di dialogo **Microsoft Azure Information Protection** fare clic su **Invia commenti e suggerimenti**. Verrà inviato un messaggio di posta elettronica al team di Information Protection. Al messaggio verranno allegati automaticamente i file di log del PC per consentire la diagnosi del problema. 

Per eventuali domande o commenti, usare il [sito Azure Information Protection in Yammer](https://www.yammer.com/askipteam/#/threads/inGroup?type=in_group&feedId=8652489&view=all). 

## Cosa fare se la domanda non è presente?

Prima verificare che la domanda non sia inclusa nell'[annuncio di Azure Information Protection (anteprima)](https://blogs.technet.microsoft.com/enterprisemobility/2016/07/12/azure-information-protection-public-preview-available-now/), in Enterprise Mobility and Security Blog (blog sulla mobilità e la sicurezza aziendale).

Quindi, visitare il nostro [sito Yammer](https://www.yammer.com/askipteam/#/threads/inGroup?type=in_group&feedId=8652489&view=all) per vedere se qualcun altro ha posto la stessa domanda. In caso negativo, pubblicare la domanda qui.







<!--HONumber=Aug16_HO4-->


