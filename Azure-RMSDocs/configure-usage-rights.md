---
title: Configurare i diritti di utilizzo per Azure Information Protection
description: Comprendere e identificare i diritti specifici usati quando si proteggono i file o i messaggi di posta elettronica usando Rights Management la protezione da Azure Information Protection.
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 01/08/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 97ddde38-b91b-42a5-8eb4-3ce6ce15393d
ms.reviewer: esaggese
ms.subservice: azurerms
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 585f962f3da6fbb3cb2373a8ac3d355e1d97aef6
ms.sourcegitcommit: 551e3f5b8956da49383495561043167597a230d9
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/08/2020
ms.locfileid: "86136753"
---
# <a name="configuring-usage-rights-for-azure-information-protection"></a>Configurazione dei diritti di utilizzo per Azure Information Protection

>*Si applica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

Quando si configurano le etichette di riservatezza o i modelli di protezione per la crittografia, si selezionano i diritti di utilizzo che verranno applicati automaticamente quando l'etichetta o il modello viene selezionato da utenti, amministratori o servizi configurati. Nel portale di Azure è ad esempio possibile selezionare i ruoli che configurano un raggruppamento logico di diritti di utilizzo oppure configurare i singoli diritti. In alternativa, gli utenti potrebbero selezionare e applicare i diritti di utilizzo.

Usare questo articolo per configurare i diritti di utilizzo desiderati per l'applicazione in uso e comprendere come questi diritti sono progettati per essere interpretati dalle applicazioni. Tuttavia, le applicazioni possono variare in base alla modalità di implementazione dei diritti, in modo da consultare sempre la documentazione ed eseguire test personalizzati con le applicazioni usate dagli utenti per controllare il comportamento prima della distribuzione nell'ambiente di produzione.

> [!NOTE] 
> Per motivi di completezza, questo articolo include valori derivanti dal portale di Azure classico che è stato ritirato l'8 gennaio 2018.

## <a name="usage-rights-and-descriptions"></a>Diritti di utilizzo e descrizioni
La tabella seguente elenca e descrive i diritti di utilizzo supportati da Rights Management e illustra come vengono usati e interpretati. Sono elencati in base al **nome comune**, ovvero al nome con cui viene usato o si fa riferimento al diritto di utilizzo nella sua versione descrittiva, e non alla parola singola usata nel codice (valore in **Codifica nei criteri**). 

In questa tabella:

- Il **valore costante o valore API** è il nome dell'SDK per una chiamata API MSIPC, usato quando si scrive un'applicazione che verifica la presenza di un diritto di utilizzo o aggiunge un diritto di utilizzo a un criterio.

- L'interfaccia di **amministrazione di assegnazione di etichette** fa riferimento alla posizione in cui vengono configurate le etichette di riservatezza e può essere il centro di conformità Microsoft 365, il centro sicurezza Microsoft 365 o il centro sicurezza & conformità di Office 365.


|Diritto di utilizzo|Descrizione|Implementazione|
|-------------------------------|---------------------------|-----------------|
|Nome comune: **Modifica contenuto, Modifica** <br /><br />Codifica nei criteri: **DOCEDIT**|Consente di modificare, riorganizzare, formattare o ordinare il contenuto all'interno dell'applicazione. Non concede il diritto per il salvataggio della copia modificata.<br /><br />In Word, a meno che non sia disponibile Office 365 ProPlus con la versione minima [1807](https://docs.microsoft.com/officeupdates/monthly-channel-2018#version-1807-july-25), questo diritto non è sufficiente per attivare o disattivare **Rileva modifiche** o per usare tutte le funzionalità di rilevamento modifiche come revisore. Per usare tutte le opzioni di rilevamento modifiche, è invece necessario il diritto **Controllo completo**. |Diritti personalizzati di Office: come parte delle opzioni **Cambia** e **Controllo completo**. <br /><br />Nome nel portale di Azure classico: **Modifica contenuto**<br /><br />Nome nell'interfaccia di amministrazione di assegnazione delle etichette e portale di Azure: **modifica contenuto, modifica (DOCEDIT)**<br /><br />Nome nei modelli di AD RMS: **Modifica** <br /><br />Valore o costante API: non applicabile.|
|Nome comune: **Salva** <br /><br />Codifica nei criteri: **EDIT**|Consente di salvare il documento nella posizione corrente.<br /><br />Nelle applicazioni di Office questo diritto consente inoltre all'utente di modificare il documento e salvarlo con un nuovo nome in un nuovo percorso se il formato di file selezionato in modalità nativa supporta la protezione di Rights Management. La restrizione prevista per il formato del file assicura che la protezione originale non possa essere rimossa dal file.|Diritti personalizzati di Office: come parte delle opzioni **Cambia** e **Controllo completo**. <br /><br />Nome nel portale di Azure classico: **Salva file**<br /><br />Nome nell'interfaccia di amministrazione di assegnazione delle etichette e portale di Azure: **Salva (modifica)**<br /><br />Nome nei modelli di AD RMS: **Salva** <br /><br />Valore o costante API: `IPC_GENERIC_WRITE L"EDIT"`|
|Nome comune: **Commento** <br /><br />Codifica nei criteri: **COMMENT**|Abilita l'opzione per l'aggiunta di annotazioni o commenti al contenuto.<br /><br />Questo diritto è disponibile nell'SDK, è disponibile come criterio ad hoc nel modulo Azure Information Protection e protezione RMS per Windows PowerShell ed è stato implementato in alcune applicazioni di fornitori di software. Tuttavia, non è ampiamente utilizzato e non è supportato dalle applicazioni di Office.|Diritti personalizzati di Office: non implementato. <br /><br />Nome nel portale di Azure classico: non implementato.<br /><br />Nome nell'interfaccia di amministrazione di assegnazione delle etichette e portale di Azure: non implementato.<br /><br />Nome nei modelli di AD RMS: non implementato. <br /><br />Valore o costante API: `IPC_GENERIC_COMMENT L"COMMENT`|
|Nome comune: **Salva con nome, Esporta** <br /><br />Codifica nei criteri: **EXPORT**|Abilita l'opzione per salvare il contenuto con un nome file diverso (Salva con nome). <br /><br />Per il client Azure Information Protection, il file può essere salvato senza protezione e anche riprotetto con nuove impostazioni e autorizzazioni. Queste azioni consentite significano che un utente con questo diritto può modificare o rimuovere un'etichetta di Azure Information Protection da un documento o un messaggio di posta elettronica protetto. <br /><br />Consente di eseguire anche altre opzioni di esportazione nelle applicazioni, ad esempio **Invia a OneNote**.|Diritti personalizzati di Office: come parte dell'opzione **Controllo completo**. <br /><br />Nome nel portale di Azure classico: **Esporta contenuto (Salva con nome)** <br /><br />Nome nell'interfaccia di amministrazione di assegnazione di etichette e portale di Azure: **Salva con nome, Esporta (Export)**<br /><br />Nome nei modelli di AD RMS: **Esporta (Salva con nome)** <br /><br />Valore o costante API: `IPC_GENERIC_EXPORT L"EXPORT"`|
|Nome comune: **Inoltra** <br /><br />Codifica nei criteri: **FORWARD**|Abilita l'opzione per l'inoltro di un messaggio di posta elettronica e per l'aggiunta di destinatari nelle righe **A** e **Cc**. Questo diritto non si applica ai documenti, ma solo ai messaggi di posta elettronica.<br /><br />Non consente all'autore dell'inoltro di concedere diritti ad altri utenti come parte dell'azione di inoltro. <br /><br />Quando si concede questo diritto, concedere anche il diritto **Modifica contenuto, Modifica** (nome comune) e il diritto **Salva** (nome comune) per garantire che il messaggio di posta elettronica protetto non venga recapitato come allegato. Specificare questi diritti anche quando si invia un messaggio di posta elettronica a un'altra organizzazione che usa il client Outlook o Outlook Web App. Oppure, per gli utenti dell'organizzazione esentati dall'uso della protezione Rights Management perché sono stati implementati i [controlli di onboarding](/powershell/module/aipservice/set-aipserviceonboardingcontrolpolicy).|Diritti personalizzati di Office: negato se sono in uso i criteri standard **Non inoltrare**.<br /><br />Nome nel portale di Azure classico: **Inoltra**<br /><br />Nome nell'interfaccia di amministrazione di assegnazione delle etichette e portale di Azure: in diretta **(in poi)**<br /><br />Nome nei modelli di AD RMS: **Inoltra** <br /><br />Valore o costante API: `IPC_EMAIL_FORWARD L"FORWARD"`|
|Nome comune: **Controllo completo** <br /><br />Codifica nei criteri: **OWNER**|Concede tutti i diritti al documento ed è possibile eseguire tutte le azioni disponibili.<br /><br />Permette di rimuovere la protezione e quindi di applicarla nuovamente a un documento. <br /><br />Si noti che questo diritto di utilizzo è diverso da [Proprietario di Rights Management](#rights-management-issuer-and-rights-management-owner).|Diritti personalizzati di Office: come l'opzione personalizzata **Controllo completo**.<br /><br />Nome nel portale di Azure classico: **Controllo completo**<br /><br />Nome nell'interfaccia di amministrazione di assegnazione delle etichette e portale di Azure: **controllo completo (proprietario)**<br /><br />Nome nei modelli di AD RMS: **Controllo completo** <br /><br />Valore o costante API: `IPC_GENERIC_ALL L"OWNER"`|
|Nome comune: **Stampa** <br /><br />Codifica nei criteri: **PRINT**|Abilita le opzioni per stampare il contenuto.|Diritti personalizzati di Office: come l'opzione **Stampa contenuto** nelle autorizzazioni personalizzate. Non è un'impostazione per destinatario.<br /><br />Nome nel portale di Azure classico: **Stampa**<br /><br />Nome nell'interfaccia di amministrazione di assegnazione delle etichette e portale di Azure: **Print (Print)**<br /><br />Nome nei modelli di AD RMS: **Stampa** <br /><br />Valore o costante API: `IPC_GENERIC_PRINT L"PRINT"`|
|Nome comune: **Rispondi** <br /><br />Codifica nei criteri: **REPLY**|Abilita l'opzione **Rispondi** nel client di posta elettronica, senza consentire modifiche alle righe **A** e **Cc**.<br /><br />Quando si concede questo diritto, concedere anche il diritto **Modifica contenuto, Modifica** (nome comune) e il diritto **Salva** (nome comune) per garantire che il messaggio di posta elettronica protetto non venga recapitato come allegato. Specificare questi diritti anche quando si invia un messaggio di posta elettronica a un'altra organizzazione che usa il client Outlook o Outlook Web App. Oppure, per gli utenti dell'organizzazione esentati dall'uso della protezione Rights Management perché sono stati implementati i [controlli di onboarding](/powershell/module/aipservice/set-aipserviceonboardingcontrolpolicy).|Diritti personalizzati di Office: non applicabile.<br /><br />Nome nel portale di Azure classico: **Rispondi**<br /><br />Nome nel portale di Azure classico: **Rispondi (REPLY)**<br /><br />Nome nei modelli di AD RMS: **Rispondi** <br /><br />Valore o costante API: `IPC_EMAIL_REPLY`|
|Nome comune: **Rispondi a tutti** <br /><br />Codifica nei criteri: **REPLYALL**|Abilita l'opzione **Rispondi a tutti** in un client di posta elettronica, ma non consente di aggiungere destinatari nelle righe **A** o **Cc**.<br /><br />Quando si concede questo diritto, concedere anche il diritto **Modifica contenuto, Modifica** (nome comune) e il diritto **Salva** (nome comune) per garantire che il messaggio di posta elettronica protetto non venga recapitato come allegato. Specificare questi diritti anche quando si invia un messaggio di posta elettronica a un'altra organizzazione che usa il client Outlook o Outlook Web App. Oppure, per gli utenti dell'organizzazione esentati dall'uso della protezione Rights Management perché sono stati implementati i [controlli di onboarding](/powershell/module/aipservice/set-aipserviceonboardingcontrolpolicy).|Diritti personalizzati di Office: non applicabile.<br /><br />Nome nel portale di Azure classico: **Rispondi a tutti**<br /><br />Nome nell'interfaccia di amministrazione di assegnazione delle etichette e portale di Azure: **Rispondi a tutti (Rispondi a tutti)**<br /><br />Nome nei modelli di AD RMS: **Rispondi a tutti** <br /><br />Valore o costante API: `IPC_EMAIL_REPLYALL L"REPLYALL"`|
|Nome comune: **Visualizza, Apri, Leggi** <br /><br />Codifica nei criteri: **VIEW**|Consente all'utente di aprire il documento e visualizzare il contenuto.<br /><br /> In Excel questo diritto non è sufficiente per ordinare i dati, operazione per cui è richiesto il diritto **Modifica contenuto, Modifica**. Per filtrare i dati in Excel, sono necessari i due diritti **Modifica contenuto, Modifica** e **Copia**.|Diritti personalizzati di Office: come i criteri personalizzati **Lettura**, opzione **Visualizza**.<br /><br />Nome nel portale di Azure classico: **Visualizza**<br /><br />Nome nell'interfaccia di amministrazione di assegnazione delle etichette e portale di Azure: **Visualizza, Apri, leggi (Visualizza)**<br /><br />Nome nei modelli AD RMS: **Lettura** <br /><br />Valore o costante API: `IPC_GENERIC_READ L"VIEW"`|
|Nome comune: **Copia** <br /><br />Codifica nei criteri: **EXTRACT**|Abilita le opzioni per copiare i dati, incluse le catture di schermata, dal documento nello stesso o in un altro documento.<br /><br />In alcune applicazioni consente inoltre di salvare l'intero documento in formato non protetto.<br /><br />In Skype for Business e applicazioni di condivisione dello schermo simili, il relatore deve avere questo diritto per presentare correttamente un documento protetto. Se il relatore non ha questo diritto, i partecipanti non possono vedere il documento, che viene visualizzato come oscurato.|Diritti personalizzati di Office: come nell'opzione dei criteri personalizzati **Consenti agli utenti con accesso in lettura di copiare il contenuto**.<br /><br />Nome nel portale di Azure classico: **Copia ed estrai il contenuto**<br /><br />Nome nell'interfaccia di amministrazione per l'assegnazione di etichette e portale di Azure: **copia (Extract)**<br /><br />Nome nei modelli di AD RMS: **Estrai** <br /><br />Valore o costante API: `IPC_GENERIC_EXTRACT L"EXTRACT"`|
|Nome comune: **Visualizza diritti** <br /><br />Codifica nei criteri: **VIEWRIGHTSDATA**|Consente all'utente di visualizzare i criteri applicati al documento. <br /><br /> Non supportato dalle app di Office o dai client di Azure Information Protection.|Diritti personalizzati di Office: non implementato.<br /><br />Nome nel portale di Azure classico: **Visualizza diritti assegnati**<br /><br />Nome nell'interfaccia di amministrazione di assegnazione delle etichette e portale di Azure: **Visualizza diritti (VIEWRIGHTSDATA)**.<br /><br />Nome nei modelli di AD RMS: **Visualizza diritti** <br /><br />Valore o costante API: `IPC_READ_RIGHTS L"VIEWRIGHTSDATA"`|
|Nome comune: **Modifica diritti** <br /><br />Codifica nei criteri: **EDITRIGHTSDATA**|Consente all'utente di modificare i criteri applicati al documento. Consente di rimuovere la rimozione. <br /><br /> Non supportato dalle app di Office o dai client di Azure Information Protection.|Diritti personalizzati di Office: non implementato.<br /><br />Nome nel portale di Azure classico: **Modifica diritti**<br /><br />Nome nell'interfaccia di amministrazione di assegnazione delle etichette e portale di Azure: **Modifica diritti (EDITRIGHTSDATA)**.<br /><br />Nome nei modelli di AD RMS: **Modifica diritti** <br /><br />Valore o costante API: `PC_WRITE_RIGHTS L"EDITRIGHTSDATA"`|
|Nome comune: **Consenti macro** <br /><br />Codifica nei criteri: **OBJMODEL**|Abilita l'opzione per eseguire macro o accedere a livello di codice o in modalità remota al contenuto in un documento.|Diritti personalizzati di Office: come l'opzione dei criteri personalizzati **Consenti l'accesso a livello di programmazione**. Non è un'impostazione per destinatario.<br /><br />Nome nel portale di Azure classico: **Consenti macro**<br /><br />Nome nell'interfaccia di amministrazione di assegnazione delle etichette e portale di Azure: **Allow Macros (OBJMODEL)**<br /><br />Nome nei modelli di AD RMS: **Consenti macro** <br /><br />Valore o costante API: non implementato.|

## <a name="rights-included-in-permissions-levels"></a>Diritti inclusi nei livelli di autorizzazione

Alcune applicazioni raggruppano i diritti di utilizzo in livelli di autorizzazione, per semplificare la selezione dei diritti di utilizzo che vengono generalmente usati insieme. I livelli di autorizzazioni permettono di astrarre un livello di complessità dagli utenti, per consentire loro di scegliere opzioni basate su ruoli.  Ad esempio, **Revisore** e **Coautore**. Sebbene queste opzioni spesso mostrino agli utenti un riepilogo dei diritti, potrebbero non includere tutti i diritti elencati nella tabella precedente.

Usare la tabella seguente per un elenco dei livelli di autorizzazione e per un elenco completo dei diritti di utilizzo in essi contenuti. I diritti di utilizzo sono elencati in base al [nome comune](#usage-rights-and-descriptions).

|Livello di autorizzazioni|Applicazioni|Diritti di utilizzo inclusi|
|---------------------|----------------|---------------------------------|
|Visualizzatore|Portale di Azure classico <br /><br />Portale di Azure<br /><br />Client Azure Information Protection per Windows|Visualizza, Apri, Leggi; Visualizza diritti; Rispondi [[1]](#footnote-1); Rispondi a tutti [[1]](#footnote-1); Consenti macro [[2]](#footnote-2)<br /><br />Nota: per i messaggi di posta elettronica, usare il diritto Revisore anziché questo livello di autorizzazione per assicurarsi che la risposta venga ricevuta come messaggio di posta e non come allegato. Il diritto Revisore è necessario anche quando si invia un messaggio di posta elettronica a un'altra organizzazione che usa il client di Outlook o Outlook Web App. Oppure, per gli utenti dell'organizzazione che sono esentati dall'uso del servizio Azure Rights Management perché sono stati implementati [controlli di onboarding](/powershell/module/aipservice/set-aipserviceonboardingcontrolpolicy).|
|Revisore|Portale di Azure classico <br /><br />Portale di Azure<br /><br />Client Azure Information Protection per Windows|Visualizza, Apri, Leggi; Salva; Modifica contenuto, Modifica; Visualizza diritti; Rispondi; Rispondi a tutti [[3]](#footnote-3); Inoltra [[3]](#footnote-3); Consenti macro [[2]](#footnote-2)|
|Coautore|Portale di Azure classico <br /><br />Portale di Azure<br /><br />Client Azure Information Protection per Windows|Visualizza, Apri, Leggi; Salva; Modifica contenuto, Modifica; Copia; Visualizza diritti; Consenti macro; Salva con nome, Esporta [[4]](#footnote-4); Stampa; Rispondi [[3]](#footnote-3); Rispondi a tutti [[3]](#footnote-3); Inoltra [[3]](#footnote-3)|
|Comproprietario|Portale di Azure classico <br /><br />Portale di Azure<br /><br />Client Azure Information Protection per Windows|Visualizza, Apri, Leggi; Salva; Modifica contenuto, Modifica; Copia; Visualizza diritti; Modifica diritti; Consenti macro; Salva con nome, Esporta; Stampa; Rispondi [[3]](#footnote-3); Rispondi a tutti [[3]](#footnote-3); Inoltra [[3]](#footnote-3); Controllo completo|

----

###### <a name="footnote-1"></a>Nota 1

Non incluso nell'interfaccia di amministrazione di assegnazione di etichette o in portale di Azure.

###### <a name="footnote-2"></a>Nota 2

Per il client Azure Information Protection per Windows, questo diritto è necessario per la barra di Information Protection nelle app di Office.

###### <a name="footnote-3"></a>Nota a piè di pagina 3
Non applicabile al client Azure Information Protection per Windows.

###### <a name="footnote-4"></a>Nota a piè di pagina 4
Non incluso nell'interfaccia di amministrazione per l'assegnazione di etichette, il portale di Azure o il client di Azure Information Protection per Windows.

## <a name="rights-included-in-the-default-templates"></a>Diritti inclusi nei modelli predefiniti
La tabella seguente elenca i diritti di utilizzo inclusi quando vengono creati i modelli predefiniti. I diritti di utilizzo sono elencati in base al [nome comune](#usage-rights-and-descriptions).

Questi modelli predefiniti vengono creati al momento dell'acquisto della sottoscrizione e i nomi e i diritti di utilizzo possono essere [modificati](configure-policy-templates.md) nella portale di Azure e con [PowerShell](https://docs.microsoft.com/powershell/module/aipservice/set-aipservicetemplateproperty). 

|Nome visualizzato del modello|Diritti di utilizzo, dal 6 ottobre 2017 alla data corrente|Diritti di utilizzo prima del 6 ottobre 2017|
|----------------|--------------------|----------|
|\<*organization name>-Solo visualizzazione riservata * <br /><br />o<br /><br /> *Riservatezza elevata \ Tutti i dipendenti*|Visualizza, Apri, Leggi; Copia, Visualizza diritti; Consenti macro; Stampa; Inoltra; Rispondi; Rispondi a tutti; Salva; Modifica contenuto, Modifica|Visualizza, Apri, Leggi|
|\<*organization name>Riservate <br /><br />o <br /><br />*Riservato \ Tutti i dipendenti*|Visualizza, Apri, Leggi; Salva con nome, Esporta, Copia; Visualizza diritti; Modifica diritti; Consenti macro; Stampa; Inoltra; Rispondi; Rispondi a tutti; Salva; Modifica contenuto, Modifica; Controllo completo|Visualizza, Apri, Leggi; Salva con nome, Esporta; Modifica contenuto, Modifica; Visualizza diritti; Consenti macro; Inoltra; Rispondi; Rispondi a tutti|

## <a name="do-not-forward-option-for-emails"></a>Opzione Non inoltrare per i messaggi di posta elettronica

I client e i servizi di Exchange, ad esempio il client Outlook, Outlook sul Web, le regole del flusso di posta di Exchange e le azioni DLP per Exchange, offrono un'opzione aggiuntiva per la protezione dei diritti sulle informazioni relativa ai messaggi di posta elettronica: **Non inoltrare**. 

Sebbene questa opzione sia mostrata agli utenti e agli amministratori di Exchange come se fosse un modello di Rights Management predefinito che è possibile selezionare, **Non inoltrare** non è un modello. È per questo motivo che non viene visualizzata nel portale di Azure quando si visualizzano e si gestiscono i modelli di protezione. L'opzione **Non inoltrare** è invece un set di diritti di utilizzo che viene applicato in modo dinamico dagli utenti ai destinatari di posta elettronica.

Quando l'opzione **Non inoltrare** viene applicata a un messaggio di posta elettronica, il messaggio di posta elettronica viene crittografato e i destinatari devono essere autenticati. I destinatari quindi non possono inoltrarlo, stamparlo o copiarne il contenuto. Ad esempio, nel client di Outlook, il pulsante Inoltra non è disponibile, le voci di menu **Salva con nome** e **Stampa** non sono disponibili e non è possibile aggiungere o modificare i destinatari nei campi **A**, **Cc** o **Ccn**.

I [documenti di Office](https://support.office.com/article/bb643d33-4a3f-4ac7-9770-fd50d95f58dc#FileTypesforIRM) non protetti allegati al messaggio di posta elettronica ereditano automaticamente le stesse restrizioni. I diritti di utilizzo applicati a questi documenti sono **Modifica contenuto, Modifica**; **Salva**; **Visualizza, Apri, Leggi** e **Consenti macro**. Se si preferiscono diritti di utilizzo diversi per un allegato o se l'allegato non è un documento di Office che supporta questa protezione ereditata, proteggere il file prima di allegarlo al messaggio di posta elettronica. È quindi possibile assegnare i diritti di utilizzo specifici necessari per il file. 

### <a name="difference-between-do-not-forward-and-not-granting-the-forward-usage-right"></a>Differenza tra Non inoltrare e non concedere il diritto di utilizzo Inoltra

È importante distinguere tra l'applicazione dell'opzione **Non inoltrare** e l'applicazione di un modello che non concede il diritto di utilizzo **Inoltra** a un messaggio di posta elettronica: l'opzione **Non inoltrare** usa un elenco dinamico di utenti autorizzati in base ai destinatari scelti dall'utente del messaggio originale, mentre i diritti nel modello sono associati a un elenco statico di utenti autorizzati che l'amministratore ha specificato in precedenza. Qual è la differenza? Ecco un esempio: 

Un utente vuole inviare un messaggio di posta elettronica a destinatari specifici del reparto Marketing con informazioni che non devono essere condivise con altri utenti. Deve proteggere il messaggio tramite un modello che limita i diritti (visualizzazione, risposta e salvataggio) del reparto Marketing?  Oppure deve scegliere l'opzione **Non inoltrare**? Con entrambe le opzioni i destinatari non potranno inoltrare il messaggio di posta elettronica. 

- Se applica il modello, i destinatari possono comunque condividere le informazioni con altri utenti del reparto Marketing. Ad esempio, un destinatario può usare Esplora file per trascinare il messaggio in un percorso condiviso o su un'unità USB. Chiunque nel reparto Marketing (e il proprietario del messaggio) ha accesso a questo percorso può visualizzare le informazioni contenute nel messaggio.
 
- Applicando invece l'opzione **Non inoltrare**, i destinatari non potranno condividere le informazioni con altri del reparto Marketing spostando il messaggio in un altro percorso. In questo scenario solo i destinatari originali del messaggio (e il proprietario del messaggio) potranno visualizzare le informazioni in esso contenute.

> [!NOTE] 
> Usare l'opzione **Non inoltrare** quando è essenziale che solo i destinatari scelti dal mittente possano visualizzare le informazioni contenute nel messaggio. Usare un modello per i messaggi di posta elettronica per limitare i diritti di un gruppo di persone specificate anticipatamente dall'amministratore, indipendentemente dai destinatari scelti dal mittente.

## <a name="encrypt-only-option-for-emails"></a>Opzione Encrypt-Only (Solo crittografia) per i messaggi di posta elettronica

Quando Exchange Online usa le nuove funzionalità per Office 365 Message Encryption, diventa disponibile una nuova opzione di posta elettronica: **Encrypt-Only (Solo crittografia)**.

Questa opzione è disponibile per i tenant che usano Exchange Online e può essere selezionata in Outlook sul Web, come opzione di protezione dei diritti aggiuntiva per una regola del flusso di posta elettronica, come azione DLP di Office 365 e in Outlook (versione minima [1804](/officeupdates/monthly-channel-2018#outlook-feature-updates-4) per Office 365 ProPlus e versione minima 1805 quando sono disponibili [app di Office 365 che supportano Azure RMS](requirements-applications.md#windows-computers-for-information-rights-management-irm)). Per ulteriori informazioni sull'opzione di sola crittografia, vedere il post di Blog seguente del team di Office: [crittografare solo il rollup in office 365 Message Encryption](https://aka.ms/omefeb2018).

Quando questa opzione è selezionata, il messaggio di posta elettronica viene crittografato e i destinatari devono essere autenticati. Quindi, i destinatari hanno tutti i diritti di utilizzo, a eccezione di **Salva con nome, Esporta** e **Controllo completo**. Questa combinazione di diritti di utilizzo implica che i destinatari non hanno restrizioni, ad eccezione del fatto che non possono rimuovere la protezione. Un destinatario può ad esempio, copiare dal messaggio di posta elettronica, stamparlo e inoltrarlo. 

Analogamente, i [documenti di Office](https://support.office.com/article/bb643d33-4a3f-4ac7-9770-fd50d95f58dc#FileTypesforIRM) non protetti allegati al messaggio di posta elettronica ereditano le stesse autorizzazioni per impostazione predefinita. Questi documenti vengono automaticamente protetti e quando vengono scaricati possono essere salvati, modificati, copiati e stampati dalle applicazioni di Office dai destinatari. Quando il documento viene salvato da un destinatario, può essere salvato con un nuovo nome e persino con un formato diverso. Sono tuttavia disponibili solo formati di file che supportano la protezione in modo che il documento non possa essere salvato senza la protezione originale. Se si preferiscono diritti di utilizzo diversi per un allegato o se l'allegato non è un documento di Office che supporta questa protezione ereditata, proteggere il file prima di allegarlo al messaggio di posta elettronica. È quindi possibile assegnare i diritti di utilizzo specifici necessari per il file.

In alternativa, è possibile modificare l'ereditarietà della protezione dei documenti, specificando `Set-IRMConfiguration -DecryptAttachmentForEncryptOnly $true` con [Exchange Online PowerShell](/powershell/exchange/exchange-online/connect-to-exchange-online-powershell/connect-to-exchange-online-powershell?view=exchange-ps). Usare questa configurazione quando non è necessario mantenere la protezione originale per il documento dopo l'autenticazione dell'utente. Quando i destinatari aprono il messaggio di posta elettronica, il documento non è protetto.

Se è necessario che un documento allegato mantenga la protezione originale, vedere [Proteggere la collaborazione ai documenti tramite Azure Information Protection](secure-collaboration-documents.md).

Nota: se vengono visualizzati riferimenti a **DecryptAttachmentFromPortal**, questo parametro è ora deprecato per [Set-IRMConfiguration](/powershell/module/exchange/encryption-and-certificates/set-irmconfiguration?view=exchange-ps). A meno che non sia stato impostato in precedenza, questo parametro non è disponibile.

## <a name="automatically-encrypt-pdf-documents-with-exchange-online"></a>Crittografa automaticamente i documenti PDF con Exchange Online

Quando Exchange Online USA le nuove funzionalità per la crittografia dei messaggi di Office 365, è possibile crittografare automaticamente i documenti PDF non protetti quando sono allegati a un messaggio di posta elettronica crittografato. Il documento eredita le stesse autorizzazioni di quelle per il messaggio di posta elettronica. Per abilitare questa configurazione, impostare **EnablePdfEncryption $true** con [Set-IRMConfiguration](https://docs.microsoft.com/powershell/module/exchange/encryption-and-certificates/set-irmconfiguration?view=exchange-ps).

I destinatari che non dispongono già di un Reader installato che supporta lo standard ISO per la crittografia PDF possono installare uno dei lettori elencati nei [lettori PDF che supportano Microsoft Information Protection](./rms-client/protected-pdf-readers.md). In alternativa, i destinatari possono leggere il documento PDF protetto nel portale OME.

## <a name="rights-management-issuer-and-rights-management-owner"></a>Emittente di Rights Management e proprietario di Rights Management

Quando un documento o un messaggio di posta elettronica viene protetto tramite il servizio Azure Rights Management, l'account che protegge il contenuto diventa automaticamente l'emittente di Rights Management per il contenuto in questione. Questo account è registrato come campo **issuer** nei [log di utilizzo](log-analyze-usage.md#how-to-interpret-your-usage-logs). 

All'emittente di Rights Management è sempre concesso il diritto di utilizzo Controllo completo per il documento o il messaggio di posta elettronica e inoltre:

- Se le impostazioni di protezione includono una data di scadenza, l'emittente di Rights Management può comunque aprire e modificare il documento o il messaggio anche dopo tale data.

- L'emittente di Rights Management può sempre accedere offline al documento o al messaggio di posta elettronica.

- L'emittente di Rights Management può comunque aprire un documento anche dopo la sua revoca. 

Per impostazione predefinita, questo account è anche il **proprietario di Rights Management** per il contenuto in questione. Questo è il caso in cui l'utente che ha creato il documento o il messaggio avvia la protezione. Esistono alcuni scenari in cui un amministratore o un servizio può proteggere il contenuto per conto degli utenti. Ad esempio:

- Un amministratore protegge in blocco tutti i file in una condivisione file: l'account amministratore in Azure AD protegge i documenti per gli utenti.

- Il connettore Rights Management protegge i documenti di Office in una cartella di Windows Server: l'account dell'entità servizio in Azure AD creato per il connettore RMS protegge i documenti per gli utenti.

In questi scenari l'emittente di Rights Management può assegnare il ruolo proprietario di Rights Management a un altro account tramite gli SDK di Azure Information Protection o PowerShell. Ad esempio, quando si usa il cmdlet [Protect-RMSFile](/powershell/module/azureinformationprotection/protect-rmsfile) di PowerShell con il client Azure Information Protection è possibile specificare il parametro **OwnerEmail** per assegnare il ruolo proprietario di Rights Management a un altro account. 

Quando l'emittente di Rights Management applica la protezione per conto degli utenti, l'assegnazione del ruolo proprietario di Rights Management garantisce che il proprietario originale del documento o del messaggio di posta elettronica disponga dello stesso livello di controllo per il contenuto protetto come se avesse avviato la protezione. 

Ad esempio, l'utente che ha creato il documento può stamparlo anche se ora risulta protetto con un modello che non include il diritto di utilizzo Stampa. Lo stesso utente potrà sempre accedere al documento, indipendentemente dall'impostazione per l'accesso offline o dalla data di scadenza configurata nel modello. Inoltre, poiché il proprietario di Rights Management dispone del diritto di utilizzo Controllo completo, l'utente può proteggere di nuovo il documento per consentire l'accesso ad altri utenti, nel qual caso l'utente diventa l'emittente di Rights Management nonché il proprietario di Rights Management, e può persino rimuovere la protezione. Tuttavia, solo l'emittente di Rights Management può tracciare e revocare un documento.

Il proprietario di Rights Management per un documento o un messaggio di posta elettronica è registrato come il campo **owner-email** nei [log di utilizzo](log-analyze-usage.md#how-to-interpret-your-usage-logs).

Si noti che il proprietario di Rights Management è indipendente dal proprietario del file system di Windows. Spesso coincidono, ma possono essere diversi, anche se non si usano gli SDK o PowerShell.

## <a name="rights-management-use-license"></a>Licenza d'uso di Rights Management

Quando un utente apre un documento o un messaggio di posta elettronica protetto tramite Azure Rights Management, gli viene concessa una licenza d'uso di Rights Management per il contenuto. Questa licenza d'uso è un certificato che contiene i diritti di utilizzo dell'utente per il documento o il messaggio di posta elettronica e la chiave di crittografia usata per crittografare il documento. La licenza d'uso include anche una data di scadenza, se è stata impostata, e indica la durata di validità di tale licenza.

Per aprire il contenuto un utente deve avere una licenza d'uso valida oltre che un suo certificato per account con diritti, un certificato che viene concesso quando [viene inizializzato l'ambiente utente](how-does-it-work.md#initializing-the-user-environment) e che viene rinnovato ogni 31 giorni.

Per la durata della licenza d'uso, all'utente non viene richiesto di ripetere l'autenticazione o specificare una nuova autorizzazione per il contenuto. Ciò consente all'utente di continuare ad aprire il documento o il messaggio di posta elettronica protetto senza una connessione Internet. Quando scade il periodo di validità della licenza d'uso, al successivo accesso al documento o messaggio di posta elettronica protetto l'utente deve ripetere l'autenticazione o specificare una nuova autorizzazione. 

Quando i documenti e i messaggi di posta elettronica vengono protetti tramite un'etichetta o un modello che definisce le impostazioni di protezione, è possibile modificare queste impostazioni nell'etichetta o nel modello senza dover proteggere di nuovo il contenuto. Se l'utente ha già eseguito l'accesso al contenuto, le modifiche diventano effettive dopo la scadenza della licenza d'uso. Tuttavia, quando gli utenti applicano autorizzazioni personalizzate, note anche come criteri per i diritti ad hoc, e tali autorizzazioni devono essere modificate dopo aver protetto il documento o il messaggio di posta elettronica, è necessario proteggere di nuovo il contenuto con le nuove autorizzazioni. Le autorizzazioni personalizzate per un messaggio di posta elettronica sono implementate con l'opzione Non inoltrare.

Il periodo di validità della licenza d'uso predefinito per un tenant è di 30 giorni ed è possibile configurare questo valore tramite il cmdlet di PowerShell [set-AipServiceMaxUseLicenseValidityTime](/powershell/module/aipservice/set-aipservicemaxuselicensevaliditytime). Quando è applicata la protezione è possibile configurare un'impostazione più restrittiva usando un'etichetta o un modello:

- Quando si configura un'etichetta o un modello nel portale di Azure, il periodo di validità della licenza d'uso deriva il suo valore dall'**impostazione Consenti l'accesso offline**. 
    
    Per altre informazioni e istruzioni per configurare questa impostazione nel portale di Azure, vedere la tabella [Informazioni sulle impostazioni di protezione](configure-policy-protection.md#information-about-the-protection-settings) nell'articolo relativo a come configurare un'etichetta per la protezione di Rights Management.

- Quando si configura un modello usando PowerShell, il periodo di validità della licenza d'uso prende il valore dal parametro *LicenseValidityDuration* nei cmdlet [set-AipServiceTemplateProperty](/powershell/module/aipservice/set-aipservicetemplateproperty) e [Add-AipServiceTemplate](/powershell/module/aipservice/add-aipservicetemplate) .
    
    Per altre informazioni e indicazioni su come configurare questa impostazione con PowerShell, vedere la Guida per ogni cmdlet.

## <a name="see-also"></a>Vedere anche
[Configurazione e gestione dei modelli per Azure Information Protection](configure-policy-templates.md)

[Configurazione degli utenti con privilegi avanzati per Azure Information Protection e servizi di individuazione o ripristino dei dati](configure-super-users.md)
