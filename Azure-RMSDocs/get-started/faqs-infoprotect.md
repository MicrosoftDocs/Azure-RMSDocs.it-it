---
title: Domande frequenti sulla classificazione e l&quot;assegnazione di etichette | Azure Information Protection
description: Questo articolo presenta alcune possibili domande su Azure Information Protection e le relative risposte.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/08/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 4b595b6a-7eb0-4438-b49a-686431f95ddd
ms.reviewer: adhall
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: fb68fc152e7f1d323cce71e3873475c78f7bbc15
ms.openlocfilehash: ad94507f4aea48172ed3c3f74f6d12e3c67cc18e


---

# <a name="frequently-asked-questions-about-classification-and-labeling-in-azure-information-protection"></a>Domande frequenti sulla classificazione e l'assegnazione di etichette in Azure Information Protection

>*Si applica a: Azure Information Protection, Office 365*

Di seguito sono riportate alcune possibili domande sulle funzionalità di classificazione e assegnazione di etichette di Azure Information Protection  e le relative risposte. 

## <a name="what-can-i-do-with-the-classification-capabilities-in-azure-information-protection"></a>Che cosa si può fare con le funzionalità di classificazione di Azure Information Protection?

Il client Azure Information Protection aggiunge alle applicazioni di Microsoft Office una barra che consente agli utenti di visualizzare e assegnare le etichette di classificazione ai messaggi di posta elettronica e ai documenti di Office.

La classificazione può essere applicata per impostazione predefinita, eseguita manualmente, consigliata o applicata automaticamente quando vengono rilevati dati sensibili. Queste etichette possono anche proteggere automaticamente i dati mediante un servizio Rights Management. Oltre ai messaggi di posta elettronica e ai documenti di Office, è possibile classificare e proteggere altri file usando Esplora file e facendo clic con il pulsante destro del mouse su un file, più file o una cartella. In alternativa, è possibile usare PowerShell dalla riga di comando, per eseguire più velocemente operazioni di classificazione e protezione in blocco.

Le etichette e il comportamento delle classificazioni vengono configurati nel portale di Azure. Per valutare molto rapidamente Azure Information Protection, è possibile usare criteri predefiniti. In alternativa, è possibile creare criteri completamente personalizzati. È possibile modificare i colori, i nomi e l'ordine delle etichette di classificazione visibili agli utenti. È anche possibile configurare descrizioni e contrassegni visivi di classificazione, ad esempio l'intestazione, il piè di pagina o una filigrana.

L'esercitazione introduttiva consente in pochi minuti di vedere queste caratteristiche in pratica: [Esercitazione introduttiva di Azure Information Protection](infoprotect-quick-start-tutorial.md).

La versione corrente presenta le limitazioni seguenti. Per sapere quando saranno disponibili altre funzionalità e nuove caratteristiche, seguire gli annunci nel [blog di Enterprise Mobility + Security](https://blogs.technet.microsoft.com/enterprisemobility/?product=azure-information-protection) e nel [sito Yammer](https://www.yammer.com/askipteam/#/threads/inGroup?type=in_group&feedId=8652489&view=all):

- I nomi e le descrizioni delle etichette sono supportati solo in una lingua.

- Manca la funzione di registrazione centralizzata per la classificazione e l'aggiunta di etichette.

- Le condizioni per la classificazione automatica devono essere frasi o motivi.

- Le app di Office per dispositivi mobili (iOS e Android) e computer Mac e le Office Web App (Office Online) non sono ancora supportati.

- Nessuna integrazione con Exchange Online o SharePoint Online.

- L'SDK per partner e sviluppatori non è disponibile.

Alcune delle limitazioni elencate in precedenza sono state risolte con la versione di febbraio del nuovo client. Per altre informazioni, vedere l'annuncio del post di blog.


## <a name="do-i-need-to-be-a-global-admin-to-try-azure-information-protection"></a>È necessario essere un amministratore globale per provare Azure Information Protection?

Per configurare i criteri di Azure Information Protection, è necessario accedere al portale di Azure come amministratore globale di Azure Active Directory.

Tuttavia, se al momento dell'installazione del [client di Azure Information Protection](https://www.microsoft.com/en-us/download/details.aspx?id=53018) si sceglie di installare i criteri demo, per provare a usare la funzionalità per l'assegnazione di etichette non è necessario accedere al portale. I criteri demo installano in locali il criterio predefinito di Azure Information Protection. È quindi possibile provare ad aggiungere etichette a documenti e a messaggi di posta elettronica, ma per modificare etichette o aggiungerne di nuove sarà necessario accedere al portale di Azure. 

## <a name="which-options-in-the-azure-portal-are-p1-or-p2"></a>Quali opzioni nel portale di Azure sono P1 o P2?

Per verificare quali sono le funzionalità incluse nella sottoscrizione di **Azure Information Protection Premium 1** (P1) rispetto alla sottoscrizione di **Azure Information Protection Premium 2** (P2), vedere l'[elenco delle funzionalità](https://www.microsoft.com/en-us/cloud-platform/azure-information-protection-features) nel sito di Azure Information Protection. Tuttavia, come guida generale, le funzionalità avanzate, ad esempio la classificazione automatica e HYOK sono specifiche della sottoscrizione di Azure Information Protection Premium 2.

## <a name="does-azure-information-protection-support-on-premises-and-hybrid-scenarios"></a>Azure Information Protection supporta scenari locali e ibridi?

Azure Information Protection è una soluzione basata sul cloud. Se si è interessati a distribuire Azure Information Protection per uno scenario ibrido, contattare il team di Information Protection inviando un messaggio di posta elettronica all'indirizzo askipteam@microsoft.com.

## <a name="how-do-computers-get-the-policy-information-from-azure-information-protection-and-how-often-is-it-refreshed"></a>In che modo i computer ottengono le informazioni relative ai criteri da Azure Information Protection e con quale frequenza le informazioni vengono aggiornate?

Ogni volta che l'utente apre un'applicazione di Office, il client di Azure Information Protection verifica la disponibilità di una versione più recente dei criteri di Azure Information Protection. Inoltre, le applicazioni di Office eseguono un controllo ogni 24 ore. Se è disponibile una versione più recente, il client la scarica tramite un collegamento HTTPS per proteggere i dati. 

Se sono caricate più istanze dell'applicazione di Office quando viene pubblicato un nuovo criterio di Azure Information Protection, è necessario chiudere tutte le istanze per ottenere la versione più recente dei criteri. Se ad esempio sono aperti due documenti di Word e si vogliono testare i criteri aggiornati di Azure Information Protection in un solo documento, chiudere entrambi i documenti di Word e riaprire quello da usare con i criteri più recenti.

## <a name="where-can-files-be-stored-to-use-azure-information-protection"></a>Dove è possibile archiviare i file da usare con Azure Information Protection? 

Azure Information Protection applica protezione ed etichette persistenti ai file e ai messaggi di posta elettronica. La posizione di archiviazione dei file non è importante.

## <a name="can-i-classify-only-new-data-or-can-i-also-classify-existing-data"></a>È possibile classificare solo nuovi dati o è possibile classificare anche i dati esistenti?

Le azioni dei criteri di Azure Information Protection vengono eseguite al momento del salvataggio dei documenti e dell'invio dei messaggi di posta elettronica, sia per il nuovo contenuto che per le modifiche apportate al contenuto esistente.

Se è installata la versione più recente del client, è anche possibile classificare rapidamente, ed eventualmente proteggere, i file esistenti da Esplora file. 

## <a name="can-i-use-azure-information-protection-for-classification-only-without-enforcing-encryption-and-restricting-usage-rights"></a>È possibile usare Azure Information Protection solo per la classificazione, senza applicare la crittografia, e limitare i diritti di utilizzo?

Sì. Se il tipo di file lo consente, è possibile configurare un criterio di Azure Information Protection che applichi solo la classificazione senza alcuna protezione. In effetti si prevede che questo sarà il caso più frequente per le reti di distribuzione in cui è necessario proteggere solo il subset dei documenti e dei messaggi di posta elettronica che richiedono una gestione dei dati particolare.

## <a name="how-does-automatic-classification-work"></a>Come funziona la classificazione automatica?

Nel portale di Azure è possibile usare motivi predefiniti, ad esempio numeri di carta di credito o codici fiscali. In alternativa, è possibile definire una stringa o un modello personalizzato come condizione per la classificazione automatica.

Un esempio di questa funzione è presente nell'[Esercitazione introduttiva di Azure Information Protection](infoprotect-quick-start-tutorial.md). 

L'accuratezza della classificazione dipende dalla configurazione della regola di classificazione, che si basa su condizioni. Attualmente le condizioni supportano motivi di testo ed espressioni regolari. Per una spiegazione delle opzioni disponibili, con alcuni esempi consigliati da provare, vedere [Come configurare le condizioni per la classificazione automatica e consigliata per Azure Information Protection](../deploy-use/configure-policy-classification.md). Il rilevamento viene eseguito quando il documento viene salvato o quando il messaggio di posta elettronica viene inviato.

Per ottenere la migliore esperienza utente e garantire la continuità aziendale, è consigliabile iniziare con azioni con consigli per gli utenti anziché con azioni completamente automatiche. In questo modo gli utenti possono accettare l'azione di aggiunta di etichette o di protezione oppure possono ignorare i suggerimenti.   

## <a name="can-azure-information-protection-prompt-users-to-classify-files-themselves-rather-than-use-automatic-classification"></a>Azure Information Protection può richiedere agli utenti di classificare i file personalmente, anziché usare la classificazione automatica? 

Sì. Tramite il portale di Azure configurare se usare la classificazione automatica o offrire consigli agli utenti. A tale scopo impostare l'opzione **Select how this label is applied: automatically or recommended to user** (Selezionare come applicare l'etichetta: automaticamente o consigliata all'utente) su **Recommended** (Consigliata).

Un esempio di questa funzione è presente nell'[Esercitazione introduttiva di Azure Information Protection](infoprotect-quick-start-tutorial.md).  

## <a name="can-i-force-all-documents-to-be-classified"></a>È possibile forzare la classificazione di tutti i documenti?

Sì. Se è necessario che gli utenti classifichino tutti i file che salvano, nel portale di Azure configurare l'impostazione dei criteri **Tutti i documenti e i messaggi di posta elettronica devono avere un'etichetta** su **On**. 

## <a name="can-i-remove-classification-from-a-file"></a>È possibile rimuovere la classificazione da un file?

Sì. Questo argomento è trattato nella guida per l'utente: [Rimuovere le etichette di classificazione e la protezione da file e messaggi di posta elettronica](../rms-client/client-remove-label-protection.md) 

## <a name="can-i-prompt-users-to-justify-why-they-are-changing-the-classification-level"></a>È possibile richiedere agli utenti di giustificare il motivo per cui stanno modificando il livello di classificazione?

Sì. Per assicurarsi che gli utenti giustifichino la modifica della classificazione, nel portale di Azure impostare l'opzione **Users must provide justification to set a lower classification label, remove a label, or remove protection** (Gli utenti devono giustificare l'abbassamento del livello di classificazione dell'etichetta) su **On** (On). Quando si esegue questa operazione, il motivo dell'azione e la giustificazione vengono registrati nel registro eventi di Windows locale: **Registri applicazioni e servizi** > **Microsoft Azure Information Protection**.

## <a name="how-can-i-automatically-protect-the-content-after-its-been-classified"></a>Come posso proteggere automaticamente il contenuto dopo che è stato classificato?

Per proteggere automaticamente il contenuto a seconda del livello di classificazione specificato, nel portale di Azure è possibile selezionare un modello di Rights Management.

Un esempio di questa funzione è presente nell'[Esercitazione introduttiva di Azure Information Protection](infoprotect-quick-start-tutorial.md). Per altre informazioni, vedere [Come configurare un'etichetta per applicare la protezione di Rights Management](../deploy-use/configure-policy-protection.md).

## <a name="can-a-file-have-more-than-one-classification"></a>Un file può avere più di una classificazione?

Poiché gli utenti possono selezionare una sola etichetta alla volta per ogni documento o messaggio di posta elettronica, la classificazione è spesso una sola. Tuttavia, se gli utenti selezionano un'etichetta secondaria, vengono effettivamente applicate due etichette contemporaneamente, ovvero un'etichetta primaria e un'etichetta secondaria. Se si usano etichette secondarie, il file può avere due classificazioni che indicano una relazione padre/figlio per un ulteriore livello di controllo.

Ad esempio, l'etichetta **Secret** può contenere le etichette secondarie **Legal** e **Finance**. È possibile applicare contrassegni visivi di classificazione e modelli di Rights Management diversi alle etichette secondarie. L'utente non potrà selezionare l'etichetta**Secret** ma solo una delle relative etichette secondarie, ad esempio **Legal**. Di conseguenza, l'etichetta impostata visualizzata dall'utente sarà **Secret\Legal**. I metadati del file includeranno una proprietà di testo personalizzato per **Secret**, una proprietà di testo personalizzato per **Legal** e un'ulteriore proprietà che contiene entrambi i valori (**Secret Legal**). 

Quando si usano etichette secondarie, non configurare contrassegni visivi, protezione e condizioni nell'etichetta principale. Quando si usano etichette secondarie, configurare queste impostazioni solo nell'etichetta secondaria. Se si configurano le impostazioni nell'etichetta principale e nella relativa etichetta secondaria, le impostazioni dell'etichetta secondaria hanno priorità.

## <a name="when-an-email-is-labeled-do-any-attachments-automatically-get-the-same-labeling"></a>Quando a un messaggio di posta elettronica viene applicata un'etichetta, eventuali allegati ottengono automaticamente la stessa etichetta?

No. Quando viene applicata un'etichetta a un messaggio di posta elettronica con allegati, tali allegati non ereditano la stessa etichetta. Gli allegati rimangono senza etichetta oppure mantengono un'etichetta applicata separatamente. Tuttavia, se l'etichetta per il messaggio di posta elettronica applica una protezione, tale protezione viene applicata agli allegati.

## <a name="how-is-azure-information-protection-classification-for-emails-different-from-exchange-message-classification"></a>Qual è la differenza tra la classificazione dei messaggi di posta elettronica di Azure Information Protection e la classificazione dei messaggi di Exchange?

La classificazione dei messaggi di Exchange è una funzionalità precedente che consente di classificare i messaggi di posta elettronica e viene implementata indipendentemente dalla classificazione di Azure Information Protection. Tuttavia, è possibile integrare le due soluzioni in modo che quando gli utenti classificano un messaggio di posta elettronica con Outlook Web App e in alcune applicazioni di posta per dispositivi mobili, vengono automaticamente aggiunti la classificazione di Azure Information Protection e i contrassegni di etichetta corrispondenti. Exchange aggiunge la classificazione e il client Azure Information Protection applica le impostazioni delle etichette corrispondenti per tale classificazione.

Sebbene Outlook Web App non supporta ancora in modo nativo la protezione e la classificazione di Azure Information Protection, è possibile adottare questa stessa tecnica per usare le etichette con questo client di posta elettronica oltre al client Outlook sul desktop.

Per ottenere questa soluzione: 

1. Usare il cmdlet [New-MessageClassification](https://technet.microsoft.com/library/bb124400) di Exchange PowerShell per creare le classificazioni dei messaggi con la proprietà Name che esegue il mapping ai nomi di etichetta nei criteri di Azure Information Protection. 

2. Creare una regola di trasporto di Exchange per ogni etichetta: applicare la regola quando le proprietà del messaggio includono la classificazione configurata e modificare le proprietà del messaggio per impostare un'intestazione del messaggio. 

    Per l'intestazione del messaggio, le informazioni da specificare sono disponibili nelle proprietà di un file Office classificato tramite l'etichetta di Azure Information Protection. Identificare la proprietà del file con il formato **MSIP_Label_<GUID>Enabled** e specificare questa stringa per l'intestazione del messaggio, quindi specificare **True** per il valore dell'intestazione. Ad esempio, l'intestazione del messaggio potrebbe essere simile a questa stringa: **MSIP_Label_132616b8-f72d-5d1e-aec1-dfd89eb8c5b2_Enabled**


Quando gli utenti usano l'app Outlook Web Access o un client del dispositivo mobile che supporta la protezione di Rights Management, si verifica quanto segue: 

- Gli utenti selezionano la classificazione dei messaggi di Exchange e inviano il messaggio di posta elettronica.

- La regola di Exchange rileva la classificazione di Exchange e di conseguenza modifica l'intestazione del messaggio per aggiungere la classificazione di Azure Information Protection.

- Quando i destinatari che eseguono il client Azure Information Protection visualizzano il messaggio di posta elettronica in Outlook, vedranno l'etichetta di Azure Information Protection assegnata e l'eventuale intestazione, piè di pagina o filigrana corrispondente del messaggio di posta elettronica. 

Se le etichette di Azure Information Protection applicano la protezione di Rights Management, aggiungerla alla configurazione della regola selezionando l'opzione per modificare la sicurezza del messaggio, applicare la protezione dei diritti, quindi selezionare il modello RMS o l'opzione Non inoltrare.

È anche possibile configurare le regole di trasporto per eseguire il mapping inverso: quando viene rilevata un'etichetta di Azure Information Protection, impostare una classificazione dei messaggi di Exchange corrispondente. A tale scopo, eseguire questa procedura:

- Per ogni etichetta di Azure Information Protection, creare una regola di trasporto da applicare quando l'intestazione **msip_labels** include il nome dell'etichetta (ad esempio, **Confidential**) e applicare una classificazione dei messaggi che esegua il mapping a questa etichetta.

## <a name="how-can-dlp-solutions-and-other-applications-integrate-with-azure-information-protection"></a>Come è possibile integrare soluzioni DLP e altre applicazioni con Azure Information Protection?

Per la classificazione, Azure Information Protection usa metadati persistenti che includono un'etichetta di testo non crittografata. Queste informazioni possono essere lette da soluzioni DLP e da altre applicazioni. Per i file, questi metadati vengono archiviati all'interno di proprietà personalizzate, per i messaggi di posta elettronica nelle intestazioni dei messaggi.

## <a name="how-does-document-tracking-and-revocation-work-for-azure-information-protection"></a>Come funzionano il rilevamento e la revoca dei documenti in Azure Information Protection?

Il rilevamento dei documenti per i file classificati e protetti tramite Azure Information Protection funziona con la versione più recente del client Azure Information Protection (versione 1.3.155.2 o successiva). 

Per altre informazioni, vedere [Tenere traccia dei documenti protetti e revocarli quando si usa Azure Information Protection](../rms-client/client-track-revoke.md).

## <a name="can-i-control-which-users-can-use-azure-information-protection-to-classify-and-protect-content"></a>È possibile avere il controllo su quali utenti possono usare Azure Information Protection per classificare e proteggere il contenuto?

È possibile limitare gli utenti che possono classificare e proteggere i dati controllando la distribuzione del client di Azure Information Protection. È possibile aggiungere nuove etichette solo per gli utenti specificati quando si configura un [criterio con ambito](../deploy-use\configure-policy-scope.md). 

I file e i messaggi di posta elettronica classificati da Azure Information Protection possono essere utilizzati o modificati da qualsiasi utente, con o senza il client di Azure Information Protection installato. 

## <a name="how-do-i-sign-in-as-a-different-user"></a>Come si accede come utente diverso?

In un ambiente di produzione, in genere non sarebbe necessario accedere come utente diverso quando si usa il client Azure Information Protection. Tuttavia, potrebbe essere necessario eseguire questa operazione se si hanno più tenant, ad esempio se si ha un tenant di prova oltre a Office 365 o un tenant di Azure usato dall'organizzazione.

È possibile verificare con quale account è stato eseguito l'accesso usando la finestra di dialogo di **Microsoft Azure Information Protection**: nell'applicazione di Office, nel gruppo **Protezione** della scheda **Home** fare clic su **Proteggi** e quindi su **Guida e commenti**. Il nome dell'account verrà visualizzato nella sezione **Stato del client**.

In particolare quando si usa un account amministratore, assicurarsi di controllare il nome di dominio dell'account di accesso che viene visualizzato. Ad esempio, se si ha un account "amministratore" in due diversi tenant, può essere facile non notare che è stato effettuato l'accesso con il nome dell'account giusto, ma con il dominio errato. Un sintomo di questo errore può essere l'impossibilità di scaricare i criteri di Azure Information Protection o di visualizzare le etichette o un comportamento previsto.

Per accedere come utente diverso, al momento è necessario modificare il Registro di sistema:

1. Usando un editor del Registro di sistema, passare a **HKEY_CURRENT_USER\SOFTWARE\Microsoft\MSIP** ed eliminare il valore **TokenCache**.

2. Riavviare tutte le applicazioni Office aperte e accedere con l'account utente diverso. Se non viene visualizzato un prompt dei comandi nell'applicazione Office per accedere al servizio Azure Information Protection, tornare alla finestra di dialogo **Microsoft Azure Information Protection** e fare clic su **Accedi** dalla sezione **Stato del client** aggiornata.

Inoltre:

- Se si vuole reinizializzare l'ambiente per il servizio Azure Rights Management (noto anche come bootstrap), è possibile farlo usando l'opzione **Reimposta** dello [strumento RMS Analyzer](https://www.microsoft.com/en-us/download/details.aspx?id=46437).

- Per eliminare i criteri di Azure Information Protection attualmente scaricati eliminare il file **Policy.msip** dalla cartella %localappdata%\Microsoft\MSIP.

## <a name="how-can-i-report-a-problem-or-send-feedback-for-azure-information-protection"></a>Come è possibile segnalare un problema o inviare commenti e suggerimenti per Azure Information Protection?

Per il supporto tecnico, usare i canali di supporto standard oppure [contattare il supporto tecnico Microsoft](information-support.md#to-contact-microsoft-support).

Per inviare feedback, ad esempio suggerimenti di possibili miglioramenti o nuove funzionalità: nel gruppo **Protezione** della scheda **Home** dell'applicazione di Office fare clic su **Proteggi** e quindi su **Guida e commenti**. Nella finestra di dialogo **Microsoft Azure Information Protection** fare clic su **Invia commenti e suggerimenti**. Verrà inviato un messaggio di posta elettronica al team di Information Protection. Al messaggio verranno allegati automaticamente i file di log del PC. 

È anche possibile rivolgersi al team di ingegneri nel [sito di Yammer per Azure Information Protection](https://www.yammer.com/askipteam/). 

[!INCLUDE[Commenting house rules](../includes/houserules.md)]


<!--HONumber=Feb17_HO2-->


