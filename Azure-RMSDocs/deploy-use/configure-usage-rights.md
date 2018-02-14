---
title: Configurare i diritti di utilizzo per Azure Rights Management - Azure Information Protection
description: Informazioni su come identificare i diritti specifici che vengono usati per la protezione di file o messaggi di posta elettronica tramite il servizio Azure Rights Management di Azure Information Protection.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 01/29/2018
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 97ddde38-b91b-42a5-8eb4-3ce6ce15393d
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: ceada043abfa1bee18c6407b3804815d95e89453
ms.sourcegitcommit: 972acdb468ac32a28e3e24c90694aff4b75206fc
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/29/2018
---
# <a name="configuring-usage-rights-for-azure-rights-management"></a>Configurazione dei diritti di utilizzo per Azure Rights Management

>*Si applica a: Azure Information Protection, Office 365*

Quando si imposta la protezione su file o messaggi di posta elettronica tramite il servizio Azure Rights Management di Azure Information Protection e non si usa un modello, è necessario configurare i diritti di utilizzo manualmente. Inoltre, quando si configurano modelli o etichette per la protezione di Azure Rights Management, si selezionano i diritti di utilizzo che verranno applicati automaticamente quando il modello o l'etichetta è selezionata dagli utenti, dagli amministratori o dai servizi configurati. Nel portale di Azure è ad esempio possibile selezionare i ruoli che configurano un raggruppamento logico di diritti di utilizzo oppure configurare i singoli diritti.

Usare questo articolo per ottenere informazioni su come configurare i diritti di utilizzo desiderati per l'applicazione in uso e comprendere in che modo tali diritti vengono interpretati dalle applicazioni.

> [!NOTE] 
> Per motivi di completezza, questo articolo include valori derivanti dal portale di Azure classico che è stato ritirato l'8 gennaio 2018.
>
> Per informazioni sulla migrazione al nuovo portale, vedere [Attività che precedentemente venivano eseguite con il portale di Azure classico](migrate-portal.md).

## <a name="usage-rights-and-descriptions"></a>Diritti di utilizzo e descrizioni
La tabella seguente elenca e descrive i diritti di utilizzo supportati da Rights Management e illustra come vengono usati e interpretati. Sono elencati in base al **nome comune**, ovvero al nome con cui viene usato o si fa riferimento al diritto di utilizzo nella sua versione descrittiva, e non alla parola singola usata nel codice (valore in **Codifica nei criteri**). 

Il **valore o costante API** è il nome dell'SDK per una chiamata all'API MSIPC, usata durante la scrittura di un'applicazione abilitata per RMS che verifica un diritto di utilizzo o ne aggiunge uno ai criteri.


|Diritto di utilizzo|Description|Implementazione|
|-------------------------------|---------------------------|-----------------|
|Nome comune: **Modifica contenuto, Modifica** <br /><br />Codifica nei criteri: **DOCEDIT**|Consente all'utente di modificare, ridisporre, formattare o filtrare il contenuto all'interno di un'applicazione. Non concede il diritto per il salvataggio della copia modificata.|Diritti personalizzati di Office: come parte delle opzioni **Cambia** e **Controllo completo**. <br /><br />Nome nel portale di Azure classico: **Modifica contenuto**<br /><br />Nome nel portale di Azure: **Modifica contenuto, Modifica (DOCEDIT)**<br /><br />Nome nei modelli di AD RMS: **Modifica** <br /><br />Valore o costante API: non applicabile.|
|Nome comune: **Salva** <br /><br />Codifica nei criteri: **EDIT**|Consente all'utente di salvare il documento nella posizione corrente.<br /><br />Nelle applicazioni di Office questo diritto consente inoltre all'utente di modificare il documento.|Diritti personalizzati di Office: come parte delle opzioni **Cambia** e **Controllo completo**. <br /><br />Nome nel portale di Azure classico: **Salva file**<br /><br />Nome nel portale di Azure: **Salva (EDIT)**<br /><br />Nome nei modelli di AD RMS: **Salva** <br /><br />Valore o costante API: `IPC_GENERIC_WRITE L"EDIT"`|
|Nome comune: **Commento** <br /><br />Codifica nei criteri: **COMMENT**|Abilita l'opzione per l'aggiunta di annotazioni o commenti al contenuto.<br /><br />Questo diritto è disponibile nell'SDK, è disponibile come criterio ad hoc nel modulo Azure Information Protection e protezione RMS per Windows PowerShell ed è stato implementato in alcune applicazioni di fornitori di software. Tuttavia, non è ampiamente usato e non è attualmente supportato dalle applicazioni di Office.|Diritti personalizzati di Office: non implementato. <br /><br />Nome nel portale di Azure classico: non implementato.<br /><br />Nome nel portale di Azure: non implementato.<br /><br />Nome nei modelli di AD RMS: non implementato. <br /><br />Valore o costante API: `IPC_GENERIC_COMMENT L"COMMENT`|
|Nome comune: **Salva con nome, Esporta** <br /><br />Codifica nei criteri: **EXPORT**|Abilita l'opzione per salvare il contenuto con un nome file diverso (Salva con nome). Per i documenti di Office e il client Azure Information Protection, il file può essere salvato senza protezione.<br /><br />Questo diritto consente inoltre all'utente di eseguire altre opzioni di esportazione nelle applicazioni, come l'operazione **Invia a OneNote**.<br /><br /> Nota: se questo diritto non è concesso, le applicazioni di Office consentono a un utente di salvare un documento con un nuovo nome se il formato di file selezionato supporta la protezione Rights Management in modo nativo.|Diritti personalizzati di Office: come parte delle opzioni **Cambia** e **Controllo completo**. <br /><br />Nome nel portale di Azure classico: **Esporta contenuto (Salva con nome)** <br /><br />Nome nel portale di Azure: **Salva con nome, Esporta (EXPORT)**<br /><br />Nome nei modelli di AD RMS: **Esporta (Salva con nome)** <br /><br />Valore o costante API: `IPC_GENERIC_EXPORT L"EXPORT"`|
|Nome comune: **Inoltra** <br /><br />Codifica nei criteri: **FORWARD**|Abilita l'opzione per inoltrare un messaggio di posta elettronica e per aggiungere i destinatari nelle righe **A** e **Cc**. Questo diritto non si applica ai documenti, ma solo ai messaggi di posta elettronica.<br /><br />Non consente all'autore dell'inoltro di concedere diritti ad altri utenti come parte dell'azione di inoltro. <br /><br />Quando si concede questo diritto, viene anche concesso il diritto **Modifica contenuto, Modifica** (nome comune) per garantire che il messaggio di posta elettronica originale sia parte del messaggio inoltrato e non allegato. Questo diritto è necessario anche quando si invia un messaggio di posta elettronica a un'altra organizzazione che usa il client di Outlook o Outlook Web App. Oppure, per gli utenti dell'organizzazione che sono esentati dall'uso del servizio Azure Rights Management perché sono stati implementati [controlli di onboarding](/powershell/module/aadrm/set-aadrmonboardingcontrolpolicy).|Diritti personalizzati di Office: negato se sono in uso i criteri standard **Non inoltrare**.<br /><br />Nome nel portale di Azure classico: **Inoltra**<br /><br />Nome nel portale di Azure: **Inoltra (FORWARD)**<br /><br />Nome nei modelli di AD RMS: **Inoltra** <br /><br />Valore o costante API: `IPC_EMAIL_FORWARD L"FORWARD"`|
|Nome comune: **Controllo completo** <br /><br />Codifica nei criteri: **OWNER**|Concede tutti i diritti al documento ed è possibile eseguire tutte le azioni disponibili.<br /><br />Permette di rimuovere la protezione e quindi di applicarla nuovamente a un documento. <br /><br />Si noti che questo diritto di utilizzo è diverso da [Proprietario di Rights Management](#rights-management-issuer-and-rights-management-owner).|Diritti personalizzati di Office: come l'opzione personalizzata **Controllo completo**.<br /><br />Nome nel portale di Azure classico: **Controllo completo**<br /><br />Nome nel portale di Azure: **Controllo completo (OWNER)**<br /><br />Nome nei modelli di AD RMS: **Controllo completo** <br /><br />Valore o costante API: `IPC_GENERIC_ALL L"OWNER"`|
|Nome comune: **Stampa** <br /><br />Codifica nei criteri: **PRINT**|Abilita le opzioni per stampare il contenuto.|Diritti personalizzati di Office: come l'opzione **Stampa contenuto** nelle autorizzazioni personalizzate. Non è un'impostazione per destinatario.<br /><br />Nome nel portale di Azure classico: **Stampa**<br /><br />Nome nel portale di Azure: **Stampa (PRINT)**<br /><br />Nome nei modelli di AD RMS: **Stampa** <br /><br />Valore o costante API: `IPC_GENERIC_PRINT L"PRINT"`|
|Nome comune: **Rispondi** <br /><br />Codifica nei criteri: **REPLY**|Abilita l'opzione **Rispondi** nel client di posta elettronica, senza consentire modifiche alle righe **A** e **Cc**.<br /><br />Quando si concede questo diritto, viene anche concesso il diritto **Modifica contenuto, Modifica** (nome comune) per garantire che il messaggio di posta elettronica originale sia parte del messaggio inoltrato e non allegato. Questo diritto è necessario anche quando si invia un messaggio di posta elettronica a un'altra organizzazione che usa il client di Outlook o Outlook Web App. Oppure, per gli utenti dell'organizzazione che sono esentati dall'uso del servizio Azure Rights Management perché sono stati implementati [controlli di onboarding](/powershell/module/aadrm/set-aadrmonboardingcontrolpolicy).|Diritti personalizzati di Office: non applicabile.<br /><br />Nome nel portale di Azure classico: **Rispondi**<br /><br />Nome nel portale di Azure classico: **Rispondi (REPLY)**<br /><br />Nome nei modelli di AD RMS: **Rispondi** <br /><br />Valore o costante API: `IPC_EMAIL_REPLY`|
|Nome comune: **Rispondi a tutti** <br /><br />Codifica nei criteri: **REPLYALL**|Abilita l'opzione **Rispondi a tutti** nel client di posta elettronica, ma non consente all'utente di aggiungere destinatari nelle righe **A** o **Cc**.<br /><br />Quando si concede questo diritto, viene anche concesso il diritto **Modifica contenuto, Modifica** (nome comune) per garantire che il messaggio di posta elettronica originale sia parte del messaggio inoltrato e non allegato. Questo diritto è necessario anche quando si invia un messaggio di posta elettronica a un'altra organizzazione che usa il client di Outlook o Outlook Web App. Oppure, per gli utenti dell'organizzazione che sono esentati dall'uso del servizio Azure Rights Management perché sono stati implementati [controlli di onboarding](/powershell/module/aadrm/set-aadrmonboardingcontrolpolicy).|Diritti personalizzati di Office: non applicabile.<br /><br />Nome nel portale di Azure classico: **Rispondi a tutti**<br /><br />Nome nel portale di Azure: **Rispondi a tutti (REPLY ALL)**<br /><br />Nome nei modelli di AD RMS: **Rispondi a tutti** <br /><br />Valore o costante API: `IPC_EMAIL_REPLYALL L"REPLYALL"`|
|Nome comune: **Visualizza, Apri, Leggi** <br /><br />Codifica nei criteri: **VIEW**|Consente all'utente di aprire il documento e visualizzare il contenuto.|Diritti personalizzati di Office: come i criteri personalizzati **Lettura**, opzione **Visualizza**.<br /><br />Nome nel portale di Azure classico: **Visualizza**<br /><br />Nome nel portale di Azure: **Visualizza, Apri, Leggi (VIEW)**<br /><br />Nome nei modelli di AD RMS: **Rispondi a tutti** <br /><br />Valore o costante API: `IPC_GENERIC_READ L"VIEW"`|
|Nome comune: **Copia** <br /><br />Codifica nei criteri: **EXTRACT**|Abilita le opzioni per copiare i dati, incluse le catture di schermata, dal documento nello stesso o in un altro documento.<br /><br />In alcune applicazioni consente inoltre di salvare l'intero documento in formato non protetto.|Diritti personalizzati di Office: come nell'opzione dei criteri personalizzati **Consenti agli utenti con accesso in lettura di copiare il contenuto**.<br /><br />Nome nel portale di Azure classico: **Copia ed estrai il contenuto**<br /><br />Nome nel portale di Azure: **Copia (EXTRACT)**<br /><br />Nome nei modelli di AD RMS: **Estrai** <br /><br />Valore o costante API: `IPC_GENERIC_EXTRACT L"EXTRACT"`|
|Nome comune: **Visualizza diritti** <br /><br />Codifica nei criteri: **VIEWRIGHTSDATA**|Consente all'utente di visualizzare i criteri applicati al documento.|Diritti personalizzati di Office: non implementato.<br /><br />Nome nel portale di Azure classico: **Visualizza diritti assegnati**<br /><br />Nome nel portale di Azure: **Visualizza diritti (VIEWRIGHTSDATA)**.<br /><br />Nome nei modelli di AD RMS: **Visualizza diritti** <br /><br />Valore o costante API: `IPC_READ_RIGHTS L"VIEWRIGHTSDATA"`|
|Nome comune: **Modifica diritti** <br /><br />Codifica nei criteri: **EDITRIGHTSDATA**|Consente all'utente di modificare i criteri applicati al documento. Consente di rimuovere la rimozione.|Diritti personalizzati di Office: non implementato.<br /><br />Nome nel portale di Azure classico: **Modifica diritti**<br /><br />Nome nel portale di Azure: **Modifica diritti (VIEWRIGHTSDATA)**.<br /><br />Nome nei modelli di AD RMS: **Modifica diritti** <br /><br />Valore o costante API: `PC_WRITE_RIGHTS L"EDITRIGHTSDATA"`|
|Nome comune: **Consenti macro** <br /><br />Codifica nei criteri: **OBJMODEL**|Abilita l'opzione per eseguire macro o accedere a livello di codice o in modalità remota al contenuto in un documento.|Diritti personalizzati di Office: come l'opzione dei criteri personalizzati **Consenti l'accesso a livello di programmazione**. Non è un'impostazione per destinatario.<br /><br />Nome nel portale di Azure classico: **Consenti macro**<br /><br />Nome nel portale di Azure: **Consenti macro (OBJMODEL)**<br /><br />Nome nei modelli di AD RMS: **Consenti macro** <br /><br />Valore o costante API: non implementato.|

## <a name="rights-included-in-permissions-levels"></a>Diritti inclusi nei livelli di autorizzazione

Alcune applicazioni raggruppano i diritti di utilizzo in livelli di autorizzazione, per semplificare la selezione dei diritti di utilizzo che vengono generalmente usati insieme. I livelli di autorizzazioni permettono di astrarre un livello di complessità dagli utenti, per consentire loro di scegliere opzioni basate su ruoli.  Ad esempio: **Revisore** e **Coautore**. Sebbene queste opzioni spesso mostrino agli utenti un riepilogo dei diritti, potrebbero non includere tutti i diritti elencati nella tabella precedente.

Usare la tabella seguente per un elenco dei livelli di autorizzazione e per un elenco completo dei diritti di utilizzo in essi contenuti. I diritti di utilizzo sono elencati in base al [nome comune](#usage-rights-and-descriptions).

|Livello di autorizzazioni|Applicazioni|Diritti di utilizzo inclusi|
|---------------------|----------------|---------------------------------|
|Visualizzatore|Portale di Azure classico <br /><br />portale di Azure<br /><br /> Applicazione di condivisione Rights Management per Windows<br /><br />Client Azure Information Protection per Windows|Visualizza, Apri, Leggi; Visualizza diritti; Rispondi [[1]](#footnote-1); Rispondi a tutti [[1]](#footnote-1); Consenti macro [[2]](#footnote-2)<br /><br />Nota: per i messaggi di posta elettronica, usare il diritto Revisore anziché questo livello di autorizzazione per assicurarsi che la risposta venga ricevuta come messaggio di posta e non come allegato. Il diritto Revisore è necessario anche quando si invia un messaggio di posta elettronica a un'altra organizzazione che usa il client di Outlook o Outlook Web App. Oppure, per gli utenti dell'organizzazione che sono esentati dall'uso del servizio Azure Rights Management perché sono stati implementati [controlli di onboarding](/powershell/module/aadrm/set-aadrmonboardingcontrolpolicy).|
|Revisore|Portale di Azure classico <br /><br />portale di Azure<br /><br />Applicazione di condivisione Rights Management per Windows<br /><br />Client Azure Information Protection per Windows|Visualizza, Apri, Leggi; Salva; Modifica contenuto, Modifica; Visualizza diritti; Rispondi; Rispondi a tutti [[3]](#footnote-3); Inoltra [[3]](#footnote-3); Consenti macro [[2]](#footnote-2)|
|Coautore|Portale di Azure classico <br /><br />portale di Azure<br /><br />Applicazione di condivisione Rights Management per Windows<br /><br />Client Azure Information Protection per Windows|Visualizza, Apri, Leggi; Salva; Modifica contenuto, Modifica; Copia; Visualizza diritti; Consenti macro; Salva con nome, Esporta [[4]](#footnote-4); Stampa; Rispondi [[3]](#footnote-3); Rispondi a tutti [[3]](#footnote-3); Inoltra [[3]](#footnote-3)|
|Comproprietario|Portale di Azure classico <br /><br />portale di Azure<br /><br />Applicazione di condivisione Rights Management per Windows<br /><br />Client Azure Information Protection per Windows|Visualizza, Apri, Leggi; Salva; Modifica contenuto, Modifica; Copia; Visualizza diritti; Modifica diritti; Consenti macro; Salva con nome, Esporta; Stampa; Rispondi [[3]](#footnote-3); Rispondi a tutti [[3]](#footnote-3); Inoltra [[3]](#footnote-3); Controllo completo|

----

###### <a name="footnote-1"></a>Nota a piè di pagina 1

Non incluso nel portale di Azure.

###### <a name="footnote-2"></a>Nota a piè di pagina 2

Per il client Azure Information Protection per Windows, questo diritto è necessario per la barra di Information Protection nelle app di Office.

###### <a name="footnote-3"></a>Nota a piè di pagina 3
Non applicabile al client Azure Information Protection per Windows o all'applicazione di condivisione Rights Management per Windows.

###### <a name="footnote-4"></a>Nota a piè di pagina 4
Non incluso nel portale di Azure o nel client Azure Information Protection per Windows.

## <a name="rights-included-in-the-default-templates"></a>Diritti inclusi nei modelli predefiniti
La tabella seguente elenca i diritti di utilizzo inclusi quando vengono creati i modelli predefiniti. I diritti di utilizzo sono elencati in base al [nome comune](#usage-rights-and-descriptions).

Questi modelli predefiniti vengono creati al momento dell'acquisto della sottoscrizione. I nomi e i diritti di utilizzo possono essere stati [modificati](configure-policy-templates.md) nel portale di Azure. 

|Nome visualizzato del modello|Diritti di utilizzo, dal 6 ottobre 2017 alla data corrente|Diritti di utilizzo prima del 6 ottobre 2017|
|----------------|--------------------|----------|
|\<*nome organizzazione> - Solo visione riservata* <br /><br />o Gestione configurazione<br /><br /> *Riservatezza elevata \ Tutti i dipendenti*|Visualizza, Apri, Leggi; Copia, Visualizza diritti; Consenti macro; Stampa; Inoltra; Rispondi; Rispondi a tutti; Salva; Modifica contenuto, Modifica|Visualizza, Apri, Leggi|
|\<*nome organizzazione>- Riservato* <br /><br />o Gestione configurazione <br /><br />*Riservato \ Tutti i dipendenti*|Visualizza, Apri, Leggi; Salva con nome, Esporta, Copia; Visualizza diritti; Modifica diritti; Consenti macro; Stampa; Inoltra; Rispondi; Rispondi a tutti; Salva; Modifica contenuto, Modifica; Controllo completo|Visualizza, Apri, Leggi; Salva con nome, Esporta; Modifica contenuto, Modifica; Visualizza diritti; Consenti macro; Inoltra; Rispondi; Rispondi a tutti|

## <a name="do-not-forward-option-for-emails"></a>Opzione Non inoltrare per i messaggi di posta elettronica

I servizi e i client di Exchange, ad esempio il client di Outlook, l'app Outlook Web Access e le regole di trasporto di Exchange, hanno un'opzione aggiuntiva per la protezione dei diritti delle informazioni per i messaggi di posta elettronica: **Non inoltrare**. 

Sebbene questa opzione sia mostrata agli utenti e agli amministratori di Exchange come se fosse un modello di Rights Management predefinito che è possibile selezionare, **Non inoltrare** non è un modello. Questo spiega perché non è disponibile nel portale di Azure quando si visualizzano e gestiscono i modelli per Azure Rights Management. Le opzioni **Non inoltrare** sono un set di diritti applicati in modo dinamico dagli utenti ai relativi destinatari di posta elettronica.

Quando l'opzione **Non inoltrare** viene applicata a un messaggio di posta elettronica, i destinatari non possono inoltrarlo, stamparlo, copiarne il contenuto, salvare gli allegati o salvarlo con un altro nome. Ad esempio, nel client di Outlook il pulsante Inoltra non è disponibile, le opzioni di menu **Salva con nome**, **Salva allegato** e **Stampa** non sono disponibili e non è possibile aggiungere o modificare i destinatari nelle caselle **A**, **Cc** e **Ccn**.

Esiste una differenza importante tra l'applicazione dell'opzione **Non inoltrare** e l'applicazione di un modello che non concede il diritto di inoltro a un messaggio di posta elettronica: l'opzione **Non inoltrare** usa un elenco dinamico di utenti autorizzati basato sui destinatari dell'utente selezionati nel messaggio di posta elettronica originale, mentre i diritti nel modello prevedono un elenco statico di utenti autorizzati specificati in precedenza dall'amministratore. Qual è la differenza? Ecco un esempio: 

Un utente vuole inviare un messaggio di posta elettronica a destinatari specifici del reparto Marketing con informazioni che non devono essere condivise con altri utenti. Deve proteggere il messaggio tramite un modello che limita i diritti (visualizzazione, risposta e salvataggio) del reparto Marketing?  Oppure deve scegliere l'opzione **Non inoltrare**? Con entrambe le opzioni i destinatari non potranno inoltrare il messaggio di posta elettronica. 

- Se applica il modello, i destinatari possono comunque condividere le informazioni con altri utenti del reparto Marketing. Ad esempio, un destinatario può usare Esplora file per trascinare il messaggio in un percorso condiviso o su un'unità USB. Chiunque nel reparto Marketing (e il proprietario del messaggio) ha accesso a questo percorso può visualizzare le informazioni contenute nel messaggio.
 
- Applicando invece l'opzione **Non inoltrare**, i destinatari non potranno condividere le informazioni con altri del reparto Marketing spostando il messaggio in un altro percorso. In questo scenario solo i destinatari originali del messaggio (e il proprietario del messaggio) potranno visualizzare le informazioni in esso contenute.

> [!NOTE] 
> Usare l'opzione **Non inoltrare** quando è essenziale che solo i destinatari scelti dal mittente possano visualizzare le informazioni contenute nel messaggio. Usare un modello per i messaggi di posta elettronica per limitare i diritti di un gruppo di persone specificate anticipatamente dall'amministratore, indipendentemente dai destinatari scelti dal mittente.

## <a name="rights-management-issuer-and-rights-management-owner"></a>Emittente di Rights Management e proprietario di Rights Management

Quando un documento o un messaggio di posta elettronica viene protetto tramite il servizio Azure Rights Management, l'account che protegge il contenuto diventa automaticamente l'emittente di Rights Management per il contenuto in questione. Questo account è registrato come campo **issuer** nei [log di utilizzo](log-analyze-usage.md#how-to-interpret-your-azure-rights-management-usage-logs). 

All'emittente di Rights Management è sempre concesso il diritto di utilizzo Controllo completo per il documento o il messaggio di posta elettronica e inoltre:

- Se le impostazioni di protezione includono una data di scadenza, l'emittente di Rights Management può comunque aprire e modificare il documento o il messaggio anche dopo tale data.

- L'emittente di Rights Management può sempre accedere offline al documento o al messaggio di posta elettronica.

- L'emittente di Rights Management può comunque aprire un documento anche dopo la sua revoca. 

Per impostazione predefinita, questo account è anche il **proprietario di Rights Management** per il contenuto in questione. Questo è il caso in cui l'utente che ha creato il documento o il messaggio avvia la protezione. Esistono alcuni scenari in cui un amministratore o un servizio può proteggere il contenuto per conto degli utenti. Ad esempio

- Un amministratore protegge in blocco tutti i file in una condivisione file: l'account amministratore in Azure AD protegge i documenti per gli utenti.

- Il connettore Rights Management protegge i documenti di Office in una cartella di Windows Server: l'account dell'entità servizio in Azure AD creato per il connettore RMS protegge i documenti per gli utenti.

In questi scenari l'emittente di Rights Management può assegnare il ruolo proprietario di Rights Management a un altro account tramite gli SDK di Azure Information Protection o PowerShell. Ad esempio, quando si usa il cmdlet [Protect-RMSFile](/powershell/module/azureinformationprotection/protect-rmsfile) di PowerShell con il client Azure Information Protection è possibile specificare il parametro **OwnerEmail** per assegnare il ruolo proprietario di Rights Management a un altro account. 

Quando l'emittente di Rights Management applica la protezione per conto degli utenti, l'assegnazione del ruolo proprietario di Rights Management garantisce che il proprietario originale del documento o del messaggio di posta elettronica disponga dello stesso livello di controllo per il contenuto protetto come se avesse avviato la protezione. 

Ad esempio, l'utente che ha creato il documento può stamparlo anche se ora risulta protetto con un modello che non include il diritto di utilizzo Stampa. Lo stesso utente potrà sempre accedere al documento, indipendentemente dall'impostazione per l'accesso offline o dalla data di scadenza configurata nel modello. Inoltre, poiché il proprietario di Rights Management dispone del diritto di utilizzo Controllo completo, l'utente può proteggere di nuovo il documento per consentire l'accesso ad altri utenti, nel qual caso l'utente diventa l'emittente di Rights Management nonché il proprietario di Rights Management, e può persino rimuovere la protezione. Tuttavia, solo l'emittente di Rights Management può tracciare e revocare un documento.

Il proprietario di Rights Management per un documento o un messaggio di posta elettronica è registrato come il campo **owner-email** nei [log di utilizzo](log-analyze-usage.md#how-to-interpret-your-azure-rights-management-usage-logs).

Si noti che il proprietario di Rights Management è indipendente dal proprietario del file system di Windows. Spesso coincidono, ma possono essere diversi, anche se non si usano gli SDK o PowerShell.

## <a name="rights-management-use-license"></a>Licenza d'uso di Rights Management

Quando un utente apre un documento o un messaggio di posta elettronica protetto tramite Azure Rights Management, gli viene concessa una licenza d'uso di Rights Management per il contenuto. Questa licenza d'uso è un certificato che contiene i diritti di utilizzo dell'utente per il documento o il messaggio di posta elettronica e la chiave di crittografia usata per crittografare il documento. La licenza d'uso include anche una data di scadenza, se è stata impostata, e indica la durata di validità di tale licenza.

Per la durata della licenza d'uso, l'utente non verrà autenticato né autorizzato nuovamente. In questo modo, l'utente potrà continuare ad aprire il documento o il messaggio di posta elettronica protetto senza una connessione Internet. Dopo la scadenza del periodo di validità della licenza d'uso, quando l'utente accede al documento o al messaggio di posta elettronica protetto, deve essere autenticato e autorizzato nuovamente. 

Quando i documenti e i messaggi di posta elettronica vengono protetti tramite un'etichetta o un modello che definisce le impostazioni di protezione, è possibile modificare queste impostazioni nell'etichetta o nel modello senza dover proteggere di nuovo il contenuto. Se l'utente ha già eseguito l'accesso al contenuto, le modifiche diventano effettive dopo la scadenza della licenza d'uso. Tuttavia, quando gli utenti applicano autorizzazioni personalizzate, note anche come criteri per i diritti ad hoc, e tali autorizzazioni devono essere modificate dopo aver protetto il documento o il messaggio di posta elettronica, è necessario proteggere di nuovo il contenuto con le nuove autorizzazioni. Le autorizzazioni personalizzate per un messaggio di posta elettronica sono implementate con l'opzione Non inoltrare.

Il periodo di validità predefinito della licenza d'uso per un tenant è 30 giorni ed è possibile configurare questo valore con il cmdlet di PowerShell [Set-AadrmMaxUseLicenseValidityTime](/powershell/module/aadrm/set-aadrmmaxuselicensevaliditytime). Quando è applicata la protezione è possibile configurare un'impostazione più restrittiva usando un'etichetta o un modello:

- Quando si configura un'etichetta o un modello nel portale di Azure, il periodo di validità della licenza d'uso deriva il suo valore dall'**impostazione Consenti l'accesso offline**. 
    
    Per altre informazioni e indicazioni su come configurare questa impostazione nel portale di Azure, vedere la tabella nel passaggio 9 di [Come configurare un'etichetta per la protezione di Rights Management](configure-policy-protection.md).

- Quando si configura un modello con PowerShell, il periodo di validità della licenza d'uso deriva il suo valore dal parametro *LicenseValidityDuration* nei cmdlet [Set-AadrmTemplateProperty](/powershell/module/aadrm/set-aadrmtemplateproperty) e [Add-AadrmTemplate](/powershell/module/aadrm/add-aadrmtemplate).
    
    Per altre informazioni e indicazioni su come configurare questa impostazione con PowerShell, vedere la Guida per ogni cmdlet.


## <a name="see-also"></a>Vedere anche
[Configurazione e gestione dei modelli per Azure Information Protection](configure-policy-templates.md)

[Configurazione degli utenti con privilegi avanzati per Azure Rights Management e servizi di individuazione o ripristino dei dati](configure-super-users.md)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]

