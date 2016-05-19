---
# required metadata

title: Informazioni di riferimento sulle restrizioni di utilizzo | Azure RMS
description:
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 5c1b0de6-e6d6-4ec9-b810-017fd606866e

# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

﻿# Informazioni di riferimento sulle restrizioni di utilizzo

Le restrizioni di utilizzo vengono definite dalle costanti elencate in questo argomento.



Ogni diritto utente, elencato nella colonna Diritto di AD RMS, presenta una descrizione, un punto di imposizione e i metodi per l'imposizione consigliati.

| Diritto di AD RMS | Descrizione | Punti di imposizione comuni | Come imporre |
|--------------|-------------|---------------------------|----------------|
|IPC_GENERIC_ALL |Concede tutti i diritti all'utente.| Nessuno |Questo diritto viene usato dal sistema e, in genere, non deve essere selezionato direttamente. <br><br> [**IpcAccessCheck**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcaccesscheck) usa questo diritto per determinare se concedere all'utente altri diritti come in questo esempio.<br><br> `/* fAccessGranted is set to TRUE if either the IPC_GENERIC_WRITE or the IPC_GENERIC_ALL right is granted */` <br><br> `IpcAccessCheck(hKey, IPC_GENERIC_WRITE, &fAccessGranted);`
|IPC_GENERIC_READ |Il diritto di leggere il contenuto del documento.|Caricamento del documento|Non caricare o presentare il contenuto del documento|
|IPC_GENERIC_WRITE|Il diritto di modificare il contenuto del documento.|Modifica dei documenti|Verificare che tutti i controlli dell'interfaccia utente che possono essere usati per modificare il contenuto del documento non siano modificabili. <br><br> Disabilitare le voci del menu che attivano le modifiche al documento. Esempi comuni: **Modifica** > **Taglia**, **Modifica** > **Incolla** e **Inserisci**. <br><br>Disabilitare qualsiasi voce del menu di scelta rapida che attiva le modifiche sul documento.|
|Nessun diritto di AD RMS|Il chiamante non dispone di diritti AD RMS|Salva|Disabilitare il menu **File** > **Salva**. <br><br> **Nota**: questo diritto non controlla **File** > **Salva con nome** poiché non rappresenta una modifica al documento originale.<br><br> Disabilitare qualsiasi tasto di scelta rapida che può essere usato per avviare un salvataggio (ad esempio Ctrl+S).<br><br> **Suggerimento**: una procedura consigliata consiste nell'aggiornare il codice **File** > **Salva** principale perché restituisca esito negativo se l'utente non dispone di tale diritto. Questa funzione agisce come rete di protezione se non è disponibile alcun meccanismo di esperienza utente che può essere usato per avviare un salvataggio.
|IPC_GENERIC_EXTRACT|Il diritto di estrarre il contenuto da un formato protetto e inserirlo in un formato non protetto.|Copia negli Appunti|Disabilitare il menu **Modifica** > **Copia**. Disabilitare il menu **Modifica** > **Taglia**. <br><br>Disabilitare **Copia** e **Taglia** da qualsiasi menu di scelta rapida.<br><br>Disabilitare qualsiasi tasto di scelta rapida che può essere usato per avviare una copia (ad esempio Ctrl+C o Ctrl+X).<br><br>Aggiornare i gestori di messaggi della finestra perché [**WM_CUT**](https://msdn.microsoft.com/library/windows/desktop/ms649023) blocchi la copia dei dati se l'utente non dispone di tale diritto. Se la finestra usa il gestore di messaggi predefinito fornito da Windows, rendere questa finestra una sottoclasse e fornire i propri gestori per **WM_COPY** e **WM_CUT**.
|Nessun diritto di AD RMS|Il chiamante non dispone di diritti AD RMS|Salva con nome|Nella finestra di dialogo **Salva con nome** disabilitare qualsiasi formato di file che comporterebbe il salvataggio del documento senza protezione RMS.|
|Nessun diritto di AD RMS|Il chiamante non dispone di diritti AD RMS|Alt+PrtScn|Chiamare [**IpcProtectWindow**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcprotectwindow) su qualsiasi finestra che esegua il rendering del contenuto del documento.|
|IPC_GENERIC_EXPORT|Il diritto di estrarre il contenuto da un formato protetto e inserirlo in un formato diverso protetto da AD RMS.|Salva con nome|Nella finestra di dialogo **Salva con nome**, disabilitare la possibilità di salvare in altri formati di file.<br><br>**Suggerimento**: una procedura consigliata consiste nell'aggiornare il codice **File** > **Salva con nome** principale perché restituisca esito negativo se l'utente tenta di salvare il file in un formato diverso e non dispone di tale diritto. Questa funzione agisce come rete di protezione se non è disponibile alcun meccanismo di esperienza utente che può essere usato per avviare un salvataggio con nome.|
|IPC_GENERIC_PRINT|Il diritto di stampare i contenuti del documento.|Stampa|Disabilitare il menu **File** > **Stampa**.<br><br>Disabilitare qualsiasi tasto di scelta rapida che può essere usato per avviare una stampa (ad esempio Ctrl + P).<br><br>Disabilitare le voci del menu di scelta rapida che potrebbero essere usate per avviare una stampa.<br><br>**Suggerimento**: una procedura consigliata consiste nell'aggiornare il codice **File** > **Stampa** principale perché restituisca esito negativo se l'utente non dispone di tale diritto. Questa funzione agisce come rete di protezione se non è disponibile alcun meccanismo di esperienza utente che può essere usato per avviare una stampa.|
|IPC_GENERIC_COMMENT|Alcune applicazioni supportano la possibilità di aggiungere annotazioni e commenti al documento senza aggiornare il contenuto principale del documento.<br><br>Questo diritto concede all'utente l'accesso a questa funzionalità.|Revisione > Inserisci commento <br><br> Revisione > Elimina commento | Disabilitare le voci del menu che consentono di modificare commenti o annotazioni sul documento. Esempi: **Revisione** > **Inserisci commento** e **Revisione** > **Elimina commento**. <br><br>Disabilitare qualsiasi tasto di scelta rapida che potrebbe attivare la modifica di commenti al documento.<br><br>**Nota**: un'implementazione predefinita richiede che sia **IPC_GENERIC_COMMENT** che **IPC_GENERIC_WRITE** rendano persistenti i nuovi commenti in un file. Le applicazioni possono scegliere di aggiungere il supporto per il caso in cui il diritto **IPC_GENERIC_COMMENT** venga concesso e il diritto **IPC_GENERIC_WRITE** non venga concesso. In questo caso, è consentito abilitare Salva, purché le modifiche al documento siano limitate ai commenti.|
|IPC_VIEW_RIGHTS||N/D|Imposti dal sistema. Il sistema non consente allo sviluppatore di eseguire query sull'[**elenco di diritti dell'utente**](/rights-management/sdk/2.1/api/win/structures#msipc_ipc_user_rights_list) da una licenza a meno che non venga concesso questo diritto.
|IPC_EDIT_RIGHTS|Alcune applicazioni consentono agli utenti di modificare il set di utenti e diritti per il contenuto protetto da AD RMS.<br><br>Questo diritto concede all'utente l'accesso a questa funzionalità.|Diritti dell'applicazione per la modifica del controllo dell'interfaccia utente|Disabilitare l'accesso utente a qualsiasi interfaccia utente che possa essere usata per modificare i criteri RMS per un documento.|

 

 

 


<!--HONumber=Apr16_HO3-->


