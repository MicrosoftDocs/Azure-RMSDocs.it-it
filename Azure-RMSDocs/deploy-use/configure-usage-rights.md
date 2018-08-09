---
title: Configurare diritti di utilizzo per Azure Rights Management - AIP
description: Informazioni sui diritti specifici usati quando si proteggono i file o i messaggi di posta elettronica tramite il servizio Azure Rights Management di Azure Information Protection e relativa identificazione.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 07/30/2018
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 97ddde38-b91b-42a5-8eb4-3ce6ce15393d
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 960c8070a03622407c5a4c68c90abb0e14eb7f96
ms.sourcegitcommit: 949bf02d5d12bef8e26d89ad5d6a0d5cc7826135
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/02/2018
ms.locfileid: "39474155"
---
# <a name="configuring-usage-rights-for-azure-rights-management"></a>Configurazione dei diritti di utilizzo per Azure Rights Management

>*Si applica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](http://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

Quando si imposta la protezione su file o messaggi di posta elettronica mediante il servizio Azure Rights Management di Azure Information Protection e non si usa un modello, è necessario configurare personalmente i diritti di utilizzo. Inoltre, quando si configurano dei modelli o delle etichette per la protezione di Azure Rights Management, si selezionano i diritti di utilizzo che verranno applicati automaticamente quando utenti, amministratori o servizi configurati selezionano il modello o l'etichetta. Ad esempio, nel portale di Azure è possibile selezionare ruoli che configurano un raggruppamento logico di diritti di utilizzo oppure è possibile configurare singoli diritti.

Usare le informazioni incluse in questo articolo per configurare i diritti di utilizzo desiderati per l'applicazione in uso e comprendere come tali diritti vengono interpretati dalle applicazioni.

> [!NOTE] 
> Per motivi di completezza questo articolo include valori del portale di Azure classico, che è stato ritirato l'8 gennaio 2018.
>
> Per informazioni sulla migrazione al nuovo portale, vedere [Tasks that you used to do with the Azure classic portal](migrate-portal.md) (Attività che si eseguivano con il portale di Azure classico).

## <a name="usage-rights-and-descriptions"></a>Diritti di utilizzo e relative descrizioni
Nella tabella seguente sono elencati e descritti i diritti d'uso supportati da supporta Rights Management e come vengono utilizzati e interpretati. Sono elencati in base al **nome comune**, che corrisponde in genere al modo in cui il diritto di utilizzo viene visualizzato o indicato, una versione semplificata del valore costituito da una singola parola e usato nel codice, ovvero il valore **Codifica nei criteri**. 

Il valore **Costante o valore API** e il nome dell'SDK per una chiamata API MSIPC, usato quando si scrive un'applicazione abilitata per RMS che verifica un diritto di utilizzo o aggiunge un diritto di utilizzo a un criterio.


|Diritto di utilizzo|Descrizione|Implementazione|
|-------------------------------|---------------------------|-----------------|
|Nome comune: **Modifica contenuto, Modifica** <br /><br />Codifica nei criteri: **DOCEDIT**|Consente di modificare, riorganizzare, formattare o ordinare il contenuto all'interno dell'applicazione. Non concede il diritto di salvare la copia modificata.<br /><br />In Word, a meno che non sia disponibile Office 365 ProPlus con la versione minima [1807](https://docs.microsoft.com/officeupdates/monthly-channel-2018#version-1807-july-25), questo diritto non è sufficiente per attivare o disattivare **Rileva modifiche** o per usare tutte le funzionalità di rilevamento modifiche come revisore. Per usare tutte le opzioni di rilevamento modifiche, è invece necessario il diritto **Controllo completo**. |Diritti personalizzati di Office: come parte delle opzioni **Modifica** e **Controllo completo** <br /><br />Nome nel portale di Azure classico: **Modifica contenuto**<br /><br />Nome nel portale di Azure: **Modifica contenuto, Modifica (DOCEDIT)**<br /><br />Nome nei modelli AD RMS: **Modifica** <br /><br />Valore costante o valore API: non applicabile|
|Nome comune: **Salva** <br /><br />Codifica nei criteri: **EDIT**|Consente di salvare il documento nella posizione corrente.<br /><br />Nelle applicazioni di Office questo diritto consente inoltre all'utente di modificare il documento e salvarlo con un nuovo nome in un nuovo percorso se il formato di file selezionato in modalità nativa supporta la protezione di Rights Management. La restrizione prevista per il formato del file assicura che la protezione originale non possa essere rimossa dal file.|Diritti personalizzati di Office: come parte delle opzioni **Modifica** e **Controllo completo** <br /><br />Nome nel portale di Azure classico: **Salva file**<br /><br />Nome nel portale di Azure: **Salva (EDIT)**<br /><br />Nome nei modelli AD RMS: **Salva** <br /><br />Costante o valore API: `IPC_GENERIC_WRITE L"EDIT"`|
|Nome comune: **Commenta** <br /><br />Codifica nei criteri: **COMMENT**|Consente di aggiungere annotazioni o commenti al contenuto.<br /><br />Questo diritto è disponibile nell'SDK e anche come criterio ad hoc nel modulo di protezione Azure Information Protection e RMS per Windows PowerShell. È stato inoltre implementato in alcune applicazioni di fornitori di software. Tuttavia, non è ampiamente utilizzato e non è attualmente supportato dalle applicazioni di Office.|Diritti personalizzati di Office: non implementato <br /><br />Nome nel portale di Azure classico: non implementato<br /><br />Nome nel portale di Azure: non implementato<br /><br />Nome nei modelli AD RMS: non implementato <br /><br />Costante o valore API: `IPC_GENERIC_COMMENT L"COMMENT`|
|Nome comune: **Salva con nome, Esporta** <br /><br />Codifica nei criteri: **EXPORT**|Abilita l'opzione per il salvataggio del contenuto con un nome file differente (Salva con nome). <br /><br />Per i documenti di Office e il client di Azure Information Protection, il file può essere salvato senza protezione e anche riprotetto con nuove impostazioni e autorizzazioni. Queste azioni consentite significano che un utente con questo diritto può modificare o rimuovere un'etichetta di Azure Information Protection da un documento o un messaggio di posta elettronica protetto. <br /><br />Consente di eseguire anche altre opzioni di esportazione nelle applicazioni, ad esempio **Invia a OneNote**.<br /><br /> Nota: se questo diritto non viene concesso, le applicazioni di Office consentono a un utente di salvare un documento con un nuovo nome se il formato di file selezionato in modalità nativa supporta la protezione di Rights Management.|Diritti personalizzati di Office: come parte delle opzioni **Modifica** e **Controllo completo** <br /><br />Nome nel portale di Azure classico: **Esporta contenuto (Salva con nome)** <br /><br />Nome nel portale di Azure: **Salva con nome, Esporta (EXPORT)**<br /><br />Nome nei modelli AD RMS: **Esporta (Salva con nome)** <br /><br />Costante o valore API: `IPC_GENERIC_EXPORT L"EXPORT"`|
|Nome comune: **Inoltra** <br /><br />Codifica nei criteri: **FORWARD**|Abilita l'opzione per l'inoltro di un messaggio di posta elettronica e per l'aggiunta di destinatari nelle righe **A** e **Cc** . Questo diritto non si applica ai documenti, ma solo ai messaggi di posta elettronica.<br /><br />Non consente al server d'inoltro di concedere diritti ad altri utenti come parte dell'azione di inoltro. <br /><br />Quando si concede questo diritto, concedere anche il diritto **Modifica contenuto, Modifica** (nome comune) per verificare che il messaggio di posta elettronica originale faccia parte del messaggio inoltrato e non sia un allegato. Questo diritto è richiesto anche quando si invia un messaggio di posta elettronica a un'altra organizzazione che usa il client Outlook o Outlook Web App. Oppure per gli utenti dell'organizzazione che non devono usare il servizio Azure Rights Management perché sono stati implementati i [controlli di onboarding](/powershell/module/aadrm/set-aadrmonboardingcontrolpolicy).|Diritti personalizzati di Office: negati quando si usa il criterio standard **Non inoltrare**<br /><br />Nome nel portale di Azure classico: **Inoltra**<br /><br />Nome nel portale di Azure: **Inoltra (FORWARD)**<br /><br />Nome nei modelli AD RMS: **Inoltra** <br /><br />Costante o valore API: `IPC_EMAIL_FORWARD L"FORWARD"`|
|Nome comune: **Controllo completo** <br /><br />Codifica nei criteri: **OWNER**|Concede tutti i diritti al documento. È possibile eseguire tutte le azioni disponibili.<br /><br />Include la possibilità di rimuovere la protezione e proteggere nuovamente un documento. <br /><br />Si noti che questo diritto di utilizzo non corrisponde al [proprietario di Rights Management](#rights-management-issuer-and-rights-management-owner).|Diritti personalizzati di Office: come le opzioni personalizzate **Controllo completo**.<br /><br />Nome nel portale di Azure classico: **Controllo completo**<br /><br />Nome nel portale di Azure: **Controllo completo (OWNER)**<br /><br />Nome nei modelli AD RMS: **Controllo completo** <br /><br />Costante o valore API: `IPC_GENERIC_ALL L"OWNER"`|
|Nome comune: **Stampa** <br /><br />Codifica nei criteri: **PRINT**|Abilita le opzioni per la stampa del contenuto.|Diritti personalizzati di Office: come l'opzione **Stampa contenuto** nelle autorizzazioni personalizzate. Non è un'impostazione per ogni destinatario.<br /><br />Nome nel portale di Azure classico: **Stampa**<br /><br />Nome nel portale di Azure: **Stampa (PRINT)**<br /><br />Nome nei modelli AD RMS: **Stampa** <br /><br />Costante o valore API: `IPC_GENERIC_PRINT L"PRINT"`|
|Nome comune: **Rispondi** <br /><br />Codifica nei criteri: **REPLY**|Abilita l'opzione **Rispondi** in un client di posta elettronica. Non sono consentite modifiche delle righe **A** o **Cc**.<br /><br />Quando si concede questo diritto, concedere anche il diritto **Modifica contenuto, Modifica** (nome comune) per verificare che il messaggio di posta elettronica originale faccia parte del messaggio inoltrato e non sia un allegato. Questo diritto è richiesto anche quando si invia un messaggio di posta elettronica a un'altra organizzazione che usa il client Outlook o Outlook Web App. Oppure per gli utenti dell'organizzazione che non devono usare il servizio Azure Rights Management perché sono stati implementati i [controlli di onboarding](/powershell/module/aadrm/set-aadrmonboardingcontrolpolicy).|Diritti personalizzati di Office: non applicabile<br /><br />Nome nel portale di Azure classico: **Rispondi**<br /><br />Nome nel portale di Azure classico: **Rispondi (REPLY)**<br /><br />Nome nei modelli AD RMS: **Rispondi** <br /><br />Costante o valore API: `IPC_EMAIL_REPLY`|
|Nome comune: **Rispondi a tutti** <br /><br />Codifica nei criteri: **REPLYALL**|Abilita l'opzione **Rispondi a tutti** in un client di posta elettronica, ma non consente di aggiungere destinatari nelle righe **A** o **Cc** .<br /><br />Quando si concede questo diritto, concedere anche il diritto **Modifica contenuto, Modifica** (nome comune) per verificare che il messaggio di posta elettronica originale faccia parte del messaggio inoltrato e non sia un allegato. Questo diritto è richiesto anche quando si invia un messaggio di posta elettronica a un'altra organizzazione che usa il client Outlook o Outlook Web App. Oppure per gli utenti dell'organizzazione che non devono usare il servizio Azure Rights Management perché sono stati implementati i [controlli di onboarding](/powershell/module/aadrm/set-aadrmonboardingcontrolpolicy).|Diritti personalizzati di Office: non applicabile<br /><br />Nome nel portale di Azure classico: **Rispondi a tutti**<br /><br />Nome nel portale di Azure: **Rispondi a tutti (REPLY ALL)**<br /><br />Nome nei modelli AD RMS: **Rispondi a tutti** <br /><br />Costante o valore API: `IPC_EMAIL_REPLYALL L"REPLYALL"`|
|Nome comune: **Visualizza, Apri, Leggi** <br /><br />Codifica nei criteri: **VIEW**|Consente all’utente di aprire il documento e visualizzarne il contenuto.<br /><br /> In Excel questo diritto non è sufficiente per ordinare i dati, operazione per cui è richiesto il diritto **Modifica contenuto, Modifica**. Per filtrare i dati in Excel, sono necessari i due diritti **Modifica contenuto, Modifica** e **Copia**.|Diritti personalizzati di Office: come il diritto personalizzato **Leggi**, opzione **Visualizza**.<br /><br />Nome nel portale di Azure classico: **Visualizza**<br /><br />Nome nel portale di Azure: **Visualizza, Apri, Leggi (VIEW)**<br /><br />Nome nei modelli AD RMS: **Lettura** <br /><br />Costante o valore API: `IPC_GENERIC_READ L"VIEW"`|
|Nome comune: **Copia** <br /><br />Codifica nei criteri: **EXTRACT**|Abilita le opzioni per la copia dei dati, inclusa l'acquisizione di schermate, nello stesso documento o in un altro.<br /><br />In alcune applicazioni consente anche di salvare l'intero documento in un formato non protetto.<br /><br />In Skype for Business e applicazioni di condivisione dello schermo simili, il relatore deve avere questo diritto per presentare correttamente un documento protetto. Se il relatore non ha questo diritto, i partecipanti non possono vedere il documento, che viene visualizzato come oscurato.|Diritti personalizzati di Office: come l'opzione di diritto personalizzato **Consenti agli utenti con accesso in lettura di copiare il contenuto**.<br /><br />Nome nel portale di Azure classico: **Copia ed estrai contenuto**<br /><br />Nome nel portale di Azure: **Copia (EXTRACT)**<br /><br />Nome nei modelli AD RMS: **Estrai** <br /><br />Costante o valore API: `IPC_GENERIC_EXTRACT L"EXTRACT"`|
|Nome comune: **Visualizza diritti** <br /><br />Codifica nei criteri: **VIEWRIGHTSDATA**|Consente all’utente di visualizzare i criteri applicati al documento.|Diritti personalizzati di Office: non implementato<br /><br />Nome nel portale di Azure classico: **Visualizza diritti assegnati**<br /><br />Nome nel portale di Azure: **Visualizza diritti (VIEWRIGHTSDATA)**.<br /><br />Nome nei modelli AD RMS: **Visualizza diritti** <br /><br />Costante o valore API: `IPC_READ_RIGHTS L"VIEWRIGHTSDATA"`|
|Nome comune: **Modifica diritti** <br /><br />Codifica nei criteri: **EDITRIGHTSDATA**|Consente all'utente di modificare il criterio applicato al documento. Include la rimozione della protezione.|Diritti personalizzati di Office: non implementato<br /><br />Nome nel portale di Azure classico: **Modifica diritti**<br /><br />Nome nel portale di Azure: **Modifica diritti (EDITRIGHTSDATA)**.<br /><br />Nome nei modelli AD RMS: **Modifica diritti** <br /><br />Costante o valore API: `PC_WRITE_RIGHTS L"EDITRIGHTSDATA"`|
|Nome comune: **Consenti macro** <br /><br />Codifica nei criteri: **OBJMODEL**|Abilita l'opzione per l'esecuzione di macro o per l'accesso, a livello di programmazione o in remoto, al contenuto di un documento.|Diritti personalizzati di Office: come l'opzione del criterio personalizzato **Consenti accesso a livello di programmazione**. Non è un'impostazione per ogni destinatario.<br /><br />Nome nel portale di Azure classico: **Consenti Macro**<br /><br />Nome nel portale di Azure: **Consenti macro (OBJMODEL)**<br /><br />Nome nei modelli AD RMS: **Consenti Macro** <br /><br />Valore costante o valore API: non implementato|

## <a name="rights-included-in-permissions-levels"></a>Diritti inclusi nei livelli di autorizzazioni

Alcune applicazioni raggruppano i diritti di utilizzo in livelli di autorizzazioni, per semplificare la selezione dei diritti di utilizzo che in genere vengono usati insieme. Questi livelli di autorizzazioni consentono di astrarre un livello di complessità dagli utenti, in modo che questi possano scegliere opzioni che sono basate sul ruolo.  Ad esempio, **Revisore** e **Coautore**. Anche se queste opzioni spesso mostrano agli utenti un riepilogo dei diritti, potrebbero non includere tutti i diritti elencati nella tabella precedente.

Usare la tabella seguente per un elenco di questi livelli di autorizzazioni e un elenco completo dei diritti di utilizzo che contengono. I diritti di utilizzo vengono elencati in base al relativo [nome comune](#usage-rights-and-descriptions).

|Livello di autorizzazioni|Applicazioni|Diritti di utilizzo inclusi|
|---------------------|----------------|---------------------------------|
|Visualizzatore|Portale di Azure classico <br /><br />Portale di Azure<br /><br /> Applicazione Rights Management sharing per Windows<br /><br />Client Azure Information Protection per Windows|Visualizza, Apri, Leggi; Visualizza diritti; Rispondi [[1]](#footnote-1); Rispondi a tutti [[1]](#footnote-1); Consenti macro [[2]](#footnote-2)<br /><br />Nota: per i messaggi di posta elettronica, usare Revisore anziché questo livello di autorizzazione per garantire che una risposta a un messaggio venga ricevuta come messaggio di posta elettronica e non come allegato. Revisore è richiesto anche quando si invia un messaggio di posta elettronica a un'altra organizzazione che usa il client Outlook o Outlook Web App. Oppure per gli utenti dell'organizzazione che non devono usare il servizio Azure Rights Management perché sono stati implementati i [controlli di onboarding](/powershell/module/aadrm/set-aadrmonboardingcontrolpolicy).|
|Revisore|Portale di Azure classico <br /><br />Portale di Azure<br /><br />Applicazione Rights Management sharing per Windows<br /><br />Client Azure Information Protection per Windows|Visualizza, Apri, Leggi; Salva; Modifica contenuto, Modifica; Visualizza diritti; Rispondi: Rispondi a tutti [[3]](#footnote-3); Inoltra [[3]](#footnote-3); Consenti macro[[2]](#footnote-2)|
|Coautore|Portale di Azure classico <br /><br />Portale di Azure<br /><br />Applicazione Rights Management sharing per Windows<br /><br />Client Azure Information Protection per Windows|Visualizza, Apri, Leggi; Salva; Modifica contenuto, Modifica; Copia; Visualizza diritti; Consenti macro; Salva con nome, Esporta [[4]](#footnote-4); Stampa; Rispondi [[3]](#footnote-3); Rispondi a tutti [[3]](#footnote-3); Inoltra [[3]](#footnote-3)|
|Comproprietario|Portale di Azure classico <br /><br />Portale di Azure<br /><br />Applicazione Rights Management sharing per Windows<br /><br />Client Azure Information Protection per Windows|Visualizza, Apri, Leggi; Salva; Modifica contenuto, Modifica; Copia; Visualizza diritti; Modifica diritti; Consenti macro; Salva con nome, Esporta; Stampa; Rispondi [[3]](#footnote-3); Rispondi a tutti [[3]](#footnote-3); Inoltra [[3]](#footnote-3); Controllo completo|

----

###### <a name="footnote-1"></a>Nota 1

Non incluso nel portale di Azure.

###### <a name="footnote-2"></a>Nota 2

Per il client di Azure Information Protection per Windows, questo diritto è attualmente necessario per la barra di Information Protection delle app di Office.

###### <a name="footnote-3"></a>Nota 3
Non applicabile al client Azure Information Protection per Windows o all'applicazione di condivisione Rights Management per Windows.

###### <a name="footnote-4"></a>Nota 4
Non incluso nel portale di Azure o nel client Azure Information Protection per Windows.

## <a name="rights-included-in-the-default-templates"></a>Diritti inclusi nei modelli predefiniti
Nella tabella seguente sono elencati i diritti di utilizzo inclusi quando vengono creati i modelli predefiniti. I diritti di utilizzo vengono elencati in base al relativo [nome comune](#usage-rights-and-descriptions).

Questi modelli predefiniti vengono creati al momento dell'acquisto della sottoscrizione e i nomi e i diritti di utilizzo possono essere [modificati](configure-policy-templates.md) nel portale di Azure. 

|Nome visualizzato del modello|Diritti di utilizzo dal 6 ottobre 2017 alla data corrente|Diritti di utilizzo prima del 6 ottobre 2017|
|----------------|--------------------|----------|
|\<*nome organizzazione> - Solo visualizzazione riservata* <br /><br />o<br /><br /> *Riservatezza elevata\Tutti i dipendenti*|Visualizza, Apri, Leggi; Copia; Visualizza diritti; Consenti macro; Stampa; Inoltra; Rispondi; Rispondi a tutti; Salva; Modifica contenuto, Modifica|Visualizza, Apri, Leggi|
|\<*nome organizzazione>- Riservato* <br /><br />o <br /><br />*Riservato\Tutti i dipendenti*|Visualizza, Apri, Leggi; Salva con nome, Esporta; Copia; Visualizza diritti; Modifica diritti; Consenti macro; Stampa; Inoltra; Rispondi; Rispondi a tutti; Salva; Modifica contenuto, Modifica; Controllo completo|Visualizza, Apri, Leggi; Salva con nome; Modifica contenuto, Modifica; Visualizza diritti; Consenti macro; Inoltra; Rispondi; Rispondi a tutti|

## <a name="do-not-forward-option-for-emails"></a>Opzione Non inoltrare per i messaggi di posta elettronica

I client e i servizi di Exchange, ad esempio il client Outlook, l'app Outlook Web Access e le regole del flusso di posta di Exchange, offrono un'opzione aggiuntiva per la protezione dei diritti sulle informazioni relativa ai messaggi di posta elettronica: **Non inoltrare**. 

Anche se questa opzione viene visualizzata dagli utenti e dagli amministratori di Exchange come se fosse un modello predefinito di Rights Management selezionabile, l'opzione **Non inoltrare** non è un modello. È per questo motivo che non viene visualizzata nel portale di Azure quando si visualizzano e si gestiscono i modelli di protezione. L'opzione **Non inoltrare** è invece un set di diritti di utilizzo che viene applicato in modo dinamico dagli utenti ai destinatari di posta elettronica.

Quando l'opzione **Non inoltrare** viene applicata a un messaggio di posta elettronica, il messaggio di posta elettronica viene crittografato e i destinatari devono essere autenticati. Quindi, i destinatari non possono inoltrarlo, stamparlo, copiarne il contenuto, salvarne gli allegati né salvarlo come un nome diverso. Ad esempio, nel client di Outlook, il pulsante Inoltra non è disponibile, le voci di menu **Salva con nome**, **Salva allegato** e **Stampa** non sono disponibili e non è possibile aggiungere o modificare i destinatari nei campi **A**, **Cc** o **Ccn**.

I [documenti di Office](https://support.office.com/article/bb643d33-4a3f-4ac7-9770-fd50d95f58dc#FileTypesforIRM) non protetti allegati al messaggio di posta elettronica ereditano automaticamente le stesse restrizioni. I diritti di utilizzo applicati a questi documenti sono **Modifica contenuto, Modifica**; **Salva**; **Visualizza, Apri, Leggi** e **Consenti macro**. Se si preferiscono diritti di utilizzo diversi per un allegato o se l'allegato non è un documento di Office che supporta questa protezione ereditata, proteggere il file prima di allegarlo al messaggio di posta elettronica. È quindi possibile assegnare i diritti di utilizzo specifici necessari per il file. 

### <a name="difference-between-do-not-forward-and-not-granting-the-forward-usage-right"></a>Differenza tra Non inoltrare e non concedere il diritto di utilizzo Inoltra

È importante distinguere tra l'applicazione dell'opzione **Non inoltrare** e l'applicazione di un modello che non concede il diritto di utilizzo **Inoltra** a un messaggio di posta elettronica: l'opzione **Non inoltrare** usa un elenco dinamico di utenti autorizzati in base ai destinatari scelti dall'utente del messaggio originale, mentre i diritti nel modello sono associati a un elenco statico di utenti autorizzati che l'amministratore ha specificato in precedenza. Qual è la differenza? Si consideri un esempio: 

Un utente vuole inviare per posta elettronica alcune informazioni a utenti specifici del reparto marketing, che non devono condividerle con nessun altro. Dovrà proteggere il messaggio di posta elettronica con un modello che limiti i diritti (visualizzazione, risposta e salvataggio) del reparto marketing?  Oppure dovrà scegliere l'opzione **Non inoltrare**? Entrambe le opzioni impediscono ai destinatari di inoltrare il messaggio di posta elettronica. 

- Se viene applicato il modello, i destinatari possono comunque condividere le informazioni con altri utenti del reparto marketing. Ad esempio, un destinatario potrebbe utilizzare Esplora risorse per trascinare il messaggio di posta elettronica in un percorso condiviso o in un'unità USB. Così il proprietario del messaggio di posta elettronica e tutti gli utenti del reparto marketing che hanno accesso a questo percorso potrebbero visualizzare le informazioni contenute nel messaggio di posta elettronica.
 
- Se invece si applica l'opzione **Non inoltrare**, i destinatari non possono condividere le informazioni con nessun altro utente del reparto marketing spostando il messaggio di posta elettronica in un altro percorso. In questo scenario, solo i destinatari originali e il proprietario del messaggio di posta elettronica saranno in grado di visualizzare le informazioni contenute nel messaggio di posta elettronica.

> [!NOTE] 
> Usare l'opzione **Non inoltrare** quando è importante che soltanto i destinatari selezionati dal mittente possano visualizzare le informazioni contenute nel messaggio di posta elettronica. Utilizzare un modello per i messaggi di posta elettronica per limitare i diritti di un gruppo di persone specificato prima dall'amministratore, a prescindere dai destinatari scelti dal mittente.

## <a name="encrypt-only-option-for-emails"></a>Opzione Encrypt-Only (Solo crittografia) per i messaggi di posta elettronica

Quando Exchange Online usa le nuove funzionalità per Office 365 Message Encryption, diventa disponibile una nuova opzione di posta elettronica: **Encrypt-Only (Solo crittografia)**.

Questa opzione viene distribuita ai tenant che usano Exchange Online, inizialmente solo per Outlook sul Web e come opzione di protezione dei diritti aggiuntiva per una regola del flusso di posta. Per altre informazioni, vedere l'annuncio nel post di blog seguente dal team di Office: [Encrypt only rolling out in Office 365 Message Encryption](https://aka.ms/omefeb2018) (Distribuzione di Solo crittografia per Office 365 Message Encryption).

Quando questa opzione è selezionata, il messaggio di posta elettronica viene crittografato e i destinatari devono essere autenticati. Quindi, i destinatari hanno tutti i diritti di utilizzo, a eccezione di **Salva con nome, Esporta** e **Controllo completo**. Questa combinazione di diritti di utilizzo implica che i destinatari non hanno restrizioni, ad eccezione del fatto che non possono rimuovere la protezione. Un destinatario può ad esempio, copiare dal messaggio di posta elettronica, stamparlo e inoltrarlo. 

Analogamente, i [documenti di Office](https://support.office.com/article/bb643d33-4a3f-4ac7-9770-fd50d95f58dc#FileTypesforIRM) non protetti allegati al messaggio di posta elettronica ereditano le stesse autorizzazioni per impostazione predefinita. Questi documenti vengono automaticamente protetti e quando vengono scaricati possono essere salvati, modificati, copiati e stampati dalle applicazioni di Office dai destinatari. Quando il documento viene salvato da un destinatario, può essere salvato con un nuovo nome e persino con un formato diverso. Sono tuttavia disponibili solo formati di file che supportano la protezione in modo che il documento non possa essere salvato senza la protezione originale. Se si preferiscono diritti di utilizzo diversi per un allegato o se l'allegato non è un documento di Office che supporta questa protezione ereditata, proteggere il file prima di allegarlo al messaggio di posta elettronica. È quindi possibile assegnare i diritti di utilizzo specifici necessari per il file.

In alternativa, è possibile modificare l'ereditarietà di crittografia dei documenti per i destinatari che visualizzano il documento nel browser. Prendere in considerazione questa configurazione quando non è necessario mantenere la protezione originale per il documento dopo l'autenticazione dell'utente. Per apportare questa modifica, usare il comando di PowerShell per Exchange Online: `Set-IRMConfiguration -DecryptAttachmentFromPortal $true`. Quindi, quando questi destinatari scaricano il documento, viene rimossa la protezione. Per altre informazioni, vedere il post del blog di Office [Admin control for attachments now available in Office 365 Message Encryption](https://techcommunity.microsoft.com/t5/Security-Privacy-and-Compliance/Admin-control-for-attachments-now-available-in-Office-365/ba-p/204007) (Il controllo amministrativo per gli allegati è ora disponibile in Office 365 Message Encryption). Se è necessario che il documento mantenga la protezione originale dopo il download, vedere [Proteggere la collaborazione ai documenti tramite Azure Information Protection](../secure-collaboration-documents.md).      

## <a name="rights-management-issuer-and-rights-management-owner"></a>Emittente di Rights Management e proprietario di Rights Management

Quando un documento o un messaggio di posta elettronica è protetto con il servizio Azure Rights Management, l'account che protegge il contenuto diventa automaticamente l'emittente di Rights Management per il contenuto. Questo account viene registrato come campo **issuer** nei [log di utilizzo](log-analyze-usage.md#how-to-interpret-your-azure-rights-management-usage-logs). 

All'emittente di Rights Management viene sempre concesso il diritto di utilizzo Controllo completo per il documento o il messaggio di posta elettronica e inoltre:

- Se le impostazioni di protezione includono una data di scadenza, l'emittente di Rights Management può comunque aprire e modificare il documento o il messaggio di posta elettronica dopo tale data.

- L'emittente di Rights Management può sempre accedere al documento o al messaggio di posta elettronica offline.

- L'emittente di Rights Management può comunque aprire un documento dopo che è stato revocato. 

Per impostazione predefinita, questo account è anche il **proprietario di Rights Management** per il contenuto poiché in genere l'utente che ha creato il documento o il messaggio di posta elettronica avvia la protezione. Ma esistono scenari in cui un amministratore o un servizio avvia la protezione del contenuto per conto degli utenti. Ad esempio:

- Un amministratore protegge in blocco i file di una condivisione di file: l'account amministratore di Azure AD protegge i documenti per gli utenti.

- Il connettore Rights Management protegge i documenti di Office in una cartella di Windows Server: l'account dell'entità servizio di Azure AD creato per il connettore RMS protegge i documenti per gli utenti.

In questi scenari l'emittente di Rights Management può assegnare il proprietario di Rights Management a un altro account usando gli SDK di Azure Information Protection o PowerShell. Ad esempio, quando si usa il cmdlet [Protect-RMSFile](/powershell/module/azureinformationprotection/protect-rmsfile) di PowerShell con il client di Azure Information Protection è possibile specificare il parametro **OwnerEmail** per assegnare il proprietario di Rights Management a un altro account. 

Quando l'emittente di Rights Management avvia la protezione per conto degli utenti, con l'assegnazione del proprietario di Rights Management, il proprietario originale del documento o messaggio di posta elettronica ha lo stesso livello di controllo del contenuto protetto che avrebbe se avesse avviato personalmente la protezione. 

Ad esempio, l'utente che ha creato il documento può stamparlo anche se ora è protetto da un modello che non include il diritto di utilizzo Stampa. Lo stesso utente può sempre accedere al proprio documento, indipendentemente dall'eventuale impostazione di accesso offline o data di scadenza configurata nel modello. Poiché il proprietario di Rights Management ha il diritto di utilizzo Controllo completo, tale utente può anche proteggere nuovamente il documento per concedere l'accesso ad altri utenti (a questo punto l'utente diventa l'emittente di Rights Management, nonché il proprietario di Rights Management) e persino rimuovere la protezione. Tuttavia, solo l'emittente di Rights Management può rilevare e revocare un documento.

Il proprietario di Rights Management per un documento o un messaggio di posta elettronica viene registrato come campo **owner-email** nei [log di utilizzo](log-analyze-usage.md#how-to-interpret-your-azure-rights-management-usage-logs).

Si noti che il proprietario di Rights Management è indipendente dal proprietario del file system di Windows. Spesso coincidono ma possono essere diversi, anche se non si usano gli SDK o PowerShell.

## <a name="rights-management-use-license"></a>Licenza d'uso di Rights Management

Quando un utente apre un documento o messaggio di posta elettronica protetto da Azure Rights Management, gli viene concessa una licenza d'uso di Rights Management per il contenuto. Questa licenza d'uso è un certificato che contiene i diritti di utilizzo dell'utente per il documento o messaggio di posta elettronica e la chiave di crittografia usata per crittografare il contenuto. La licenza d'uso contiene anche una data di scadenza, se è stata impostata, e il periodo di validità della licenza d'uso.

Per aprire il contenuto un utente deve avere una licenza d'uso valida oltre che un suo certificato per account con diritti, un certificato che viene concesso quando [viene inizializzato l'ambiente utente](../how-does-it-work.md#initializing-the-user-environment) e che viene rinnovato ogni 31 giorni.

Per la durata della licenza d'uso, all'utente non viene richiesto di ripetere l'autenticazione o specificare una nuova autorizzazione per il contenuto. Ciò consente all'utente di continuare ad aprire il documento o messaggio di posta elettronica protetto senza una connessione Internet. Quando scade il periodo di validità della licenza d'uso, al successivo accesso al documento o messaggio di posta elettronica protetto l'utente deve ripetere l'autenticazione o specificare una nuova autorizzazione. 

Quando i documenti e messaggi di posta elettronica sono protetti tramite un'etichetta o modello che definisce le impostazioni di protezione, è possibile modificare queste impostazioni nell'etichetta o modello senza che sia necessario proteggere nuovamente il contenuto. Se l'utente ha già accesso al contenuto, le modifiche vengono applicate dopo la scadenza del contratto di licenza. Quando tuttavia gli utenti applicano autorizzazioni personalizzate (note anche come criteri per i diritti di utilizzo ad hoc) e queste autorizzazioni devono essere modificate dopo che il documento o messaggio di posta elettronica viene protetto, il contenuto deve essere protetto nuovamente con le nuove autorizzazioni. Le autorizzazioni personalizzate per un messaggio di posta elettronica vengono implementate con l'opzione Non inoltrare.

Il valore predefinito per il periodo di validità della licenza d'uso per un tenant è di 30 giorni ed è possibile configurare questo valore tramite il cmdlet PowerShell, [Set-AadrmMaxUseLicenseValidityTime](/powershell/module/aadrm/set-aadrmmaxuselicensevaliditytime). È possibile configurare un'impostazione più restrittiva per il momento dell'applicazione della protezione tramite un'etichetta o un modello:

- Quando si configura un'etichetta o un modello nel portale di Azure, il periodo di validità della licenza d'uso assume il valore specificato nell'impostazione **Consenti l'accesso offline**. 
    
    Per altre informazioni e istruzioni per configurare questa impostazione nel portale di Azure, vedere la tabella [Informazioni sulle impostazioni di protezione](../deploy-use/configure-policy-protection.md#information-about-the-protection-settings) nell'articolo relativo a come configurare un'etichetta per la protezione di Rights Management.

- Quando si configura un modello tramite PowerShell, il periodo di validità della licenza d'uso assume il valore specificato nel parametro *LicenseValidityDuration* nei cmdlet [Set-AadrmTemplateProperty](/powershell/module/aadrm/set-aadrmtemplateproperty) e [Add-AadrmTemplate](/powershell/module/aadrm/add-aadrmtemplate).
    
    Per altre informazioni e istruzioni per configurare questa impostazione tramite PowerShell, vedere la guida relativa a ogni cmdlet.

## <a name="see-also"></a>Vedere anche
[Configurazione e gestione dei modelli per Azure Information Protection](configure-policy-templates.md)

[Configurazione degli utenti con privilegi avanzati per Azure Rights Management e servizi di individuazione o ripristino dei dati](configure-super-users.md)


