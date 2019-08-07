---
title: Informazioni sulle restrizioni di utilizzo | Azure RMS
description: Tutte le applicazioni abilitate per RMS devono imporre restrizioni di utilizzo.
keywords: ''
author: msmbaldwin
ms.author: mbaldwin
manager: barbkess
ms.date: 02/23/2017
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: E388B16C-ECDA-4696-A040-D457D3C96766
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
ms.custom: dev
ms.openlocfilehash: 0f94ac02b0e9d5faa42c403274d44819dad46fbd
ms.sourcegitcommit: 9968a003865ff2456c570cf552f801a816b1db07
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/05/2019
ms.locfileid: "68790749"
---
# <a name="understanding-usage-restrictions"></a>Informazioni sulle restrizioni di utilizzo

Tutte le applicazioni abilitate per RMS devono imporre restrizioni di utilizzo. Una restrizione di utilizzo è una condizione risultante da un tentativo dell'utente di eseguire un'azione, ad esempio la stampa di un documento, ma i criteri RMS per tale documento non concedono autorizzazioni o diritti per eseguire l'azione (ad esempio, il diritto di stampa).

È possibile eseguire query sulle autorizzazioni di un utente per un documento tramite la funzione [IpcAccessCheck](https://msdn.microsoft.com/library/hh535253.aspx).

## <a name="designing-with-usage-restrictions"></a>Progettazione con le restrizioni di utilizzo

-   Acquisire familiarità con i diritti standard di RMS

    Per l'insieme completo dei diritti di RMS che l'applicazione può imporre, vedere [Informazioni di riferimento sulle restrizioni di utilizzo](#usage-restriction-reference).

    Si noti che i diritti definiti dall'applicazione sono specifici della propria situazione e vanno oltre i diritti standard di RMS.

-   Identificare i punti di imposizione delle restrizione di utilizzo

    Un *punto di imposizione delle restrizioni di utilizzo* è una posizione nel flusso di controllo dell'applicazione in cui è necessario applicare una restrizione di utilizzo. L'argomento [Informazioni di riferimento sulle restrizioni di utilizzo](#usage-restriction-reference) fornisce vari esempi di punti di imposizione comuni.

    Valutare la propria applicazione per determinare quali punti di imposizione delle restrizioni di utilizzo applicare.

    È possibile che per l'applicazione non siano necessari tutti i punti di imposizione descritti in [Informazioni di riferimento sulle restrizioni di utilizzo](#usage-restriction-reference). Ad esempio, se l'applicazione non consente agli utenti di stampare il contenuto, non è necessario verificare il diritto **IPC\_GENERIC\_PRINT**.

-   Aggiornare il codice per eseguire un controllo di accesso per ogni punto di imposizione

    Per altre informazioni sull'imposizione di diritti specifici, vedere [Informazioni di riferimento sulle restrizioni di utilizzo](#usage-restriction-reference).

## <a name="usage-restriction-reference"></a>Informazioni di riferimento sulle restrizioni di utilizzo

Le restrizioni di utilizzo vengono definite dalle seguenti costanti.

Ogni diritto utente, elencato nella colonna Diritto di AD RMS, presenta una descrizione, un punto di imposizione e i metodi per l'imposizione consigliati.

| Diritto di AD RMS/descrizione | Come imporre |
|--------------------------|----------------|
|**IPC_GENERIC_ALL** <br><br> Concede tutti i diritti all'utente. <br><br> **Punti di imposizione comuni**: Nessuna |Questo diritto viene usato dal sistema e, in genere, non deve essere selezionato direttamente. <br><br> [IpcAccessCheck](https://msdn.microsoft.com/library/hh535253.aspx) usa questo diritto per determinare se concedere all'utente altri diritti come in questo esempio.<br><br> `/* fAccessGranted is set to TRUE if either the IPC_GENERIC_WRITE or the IPC_GENERIC_ALL right is granted */` <br><br> `IpcAccessCheck(hKey, IPC_GENERIC_WRITE, &fAccessGranted);`|
|**IPC_GENERIC_READ** <br><br> Il diritto di leggere il contenuto del documento. <br><br> **Punti di imposizione comuni**: Caricamento del documento|Non caricare o presentare il contenuto del documento|
|**IPC_GENERIC_WRITE** <br><br> Il diritto di modificare il contenuto del documento. <br><br> **Punti di imposizione comuni**: Modifica dei documenti|Verificare che tutti i controlli dell'interfaccia utente che possono essere usati per modificare il contenuto del documento non siano modificabili. <br><br> Disabilitare le voci del menu che attivano le modifiche al documento. Ad esempio, **Modifica** > **Taglia**, **Modifica** > **Incolla** e **Inserisci**. <br><br>Disabilitare qualsiasi voce del menu di scelta rapida che attiva le modifiche sul documento.|
|Nessun diritto di AD RMS <br><br> Nessuna descrizione <br><br> **Punti di imposizione comuni**: Salva | Disabilitare il menu **File** > **Salva**. <br><br> **Nota** Questo diritto non controlla **File** > **Salva con nome** poiché tale diritto non rappresenta una modifica al documento originale.<br><br> Disabilitare qualsiasi tasto di scelta rapida che può essere usato per avviare un salvataggio (ad esempio Ctrl+S).<br><br> **Suggerimento** Una procedura consigliata consiste nell'aggiornare il codice **File** > **Salva** principale in modo che non venga eseguito se l'utente non dispone del diritto specifico. Questa funzione agisce come rete di protezione se non è disponibile alcun meccanismo di esperienza utente che può essere usato per avviare un salvataggio. |
|**IPC_GENERIC_EXTRACT** <br><br> Il diritto di estrarre il contenuto da un formato protetto e inserirlo in un formato non protetto. <br><br> **Punti di imposizione comuni**: Copia negli Appunti | Disabilitare il menu **Modifica** > **Copia**. Disabilitare il menu **Modifica** > **Taglia**. <br><br>Disabilitare **Copia** e **Taglia** da qualsiasi menu di scelta rapida.<br><br>Disabilitare qualsiasi tasto di scelta rapida che può essere usato per avviare una copia (ad esempio Ctrl+C o Ctrl+X).<br><br>Aggiornare i gestori di messaggi della finestra perché [**WM_CUT**](https://msdn.microsoft.com/library/ms649023) blocchi la copia dei dati se l'utente non dispone di tale diritto. Se la finestra usa il gestore di messaggi predefinito fornito da Windows, rendere questa finestra una sottoclasse e fornire i propri gestori per **WM_COPY** e **WM_CUT**. |
|Nessun diritto di AD RMS <br><br> Nessuna descrizione <br><br> **Punti di imposizione comuni**: Salva con nome |Nella finestra di dialogo **Salva con nome** disabilitare qualsiasi formato di file che comporterebbe il salvataggio del documento senza protezione RMS.|
|Nessun diritto di AD RMS <br><br> Nessuna descrizione <br><br> **Punti di imposizione comuni**: Alt+PrtScn|Chiamare [IpcProtectWindow](https://msdn.microsoft.com/library/hh535268.aspx) in qualsiasi finestra che esegua il rendering del contenuto del documento.|
|**IPC_GENERIC_EXPORT** <br><br> Il diritto di estrarre il contenuto da un formato protetto e inserirlo in un formato diverso protetto da AD RMS. <br><br> **Punti di imposizione comuni**: Salva con nome|Nella finestra di dialogo **Salva con nome**, disabilitare la possibilità di salvare in altri formati di file.<br><br>**Suggerimento** Una procedura consigliata consiste nell'aggiornare il codice **File** > **Salva con nome** principale in modo che non venga eseguito se l'utente tenta di salvare il file in un formato diverso e non dispone del diritto specifico. Questa funzione agisce come rete di protezione se non è disponibile alcun meccanismo di esperienza utente che può essere usato per avviare un salvataggio con nome.|
|**IPC_GENERIC_PRINT** <br><br> Il diritto di stampare i contenuti del documento. <br><br> **Punti di imposizione comuni**: Stampa|Disabilitare il menu **File** > **Stampa**.<br><br>Disabilitare qualsiasi tasto di scelta rapida che può essere usato per avviare una stampa (ad esempio Ctrl + P).<br><br>Disabilitare le voci del menu di scelta rapida che potrebbero essere usate per avviare una stampa.<br><br>**Suggerimento** Una procedura consigliata consiste nell'aggiornare il codice **File** > **Stampa** principale in modo che non venga eseguito se l'utente non dispone del diritto specifico. Questa funzione agisce come rete di protezione se non è disponibile alcun meccanismo di esperienza utente che può essere usato per avviare una stampa.|
|**IPC_GENERIC_COMMENT** <br><br> Alcune applicazioni supportano la possibilità di aggiungere annotazioni e commenti al documento senza aggiornare il contenuto principale del documento.<br><br>Questo diritto concede all'utente l'accesso a questa funzionalità. <br><br> **Punti di imposizione comuni**: <br><br> Revisione > Inserisci commento <br><br> Revisione > Elimina commento | Disabilitare le voci del menu che consentono di modificare commenti o annotazioni sul documento. Ad esempio, **Revisione** > **Inserisci commento** e **Revisione** > **Elimina commento**. <br><br>Disabilitare qualsiasi tasto di scelta rapida che potrebbe attivare la modifica di commenti al documento.<br><br>**Nota**: un'implementazione predefinita richiede che sia **IPC_GENERIC_COMMENT** che **IPC_GENERIC_WRITE** rendano persistenti i nuovi commenti in un file. Le applicazioni possono scegliere di aggiungere il supporto per il caso in cui il diritto **IPC_GENERIC_COMMENT** venga concesso e il diritto **IPC_GENERIC_WRITE** non venga concesso. In questo caso, è consentito abilitare Salva, purché le modifiche al documento siano limitate ai commenti.|
|**IPC_VIEW_RIGHTS** <br><br> Nessuna descrizione <br><br> **Punti di imposizione comuni**: N/D|Imposti dal sistema. Il sistema non consente allo sviluppatore di eseguire query sull'[**elenco di diritti dell'utente**](https://msdn.microsoft.com/library/hh535286.aspx) da una licenza a meno che non venga concesso questo diritto.
|**IPC_EDIT_RIGHTS** <br><br> Alcune applicazioni consentono agli utenti di modificare il set di utenti e diritti per il contenuto protetto da AD RMS.<br><br>Questo diritto concede all'utente l'accesso a questa funzionalità. <br><br> **Punti di imposizione comuni**: Diritti dell'applicazione per la modifica del controllo dell'interfaccia utente|Disabilitare l'accesso utente a qualsiasi interfaccia utente che possa essere usata per modificare i criteri RMS per un documento.|


## <a name="related-topics"></a>Argomenti correlati

* [IpcAccessCheck](https://msdn.microsoft.com/library/hh535253.aspx)
