---
title: 'Classe FileHandler:: Observer'
description: 'Documenta la classe FileHandler:: Observer di Microsoft Information Protection (MIP) SDK.'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 09/21/2020
ms.openlocfilehash: d469271718d422216f6eaad905e60cd82e7f1244
ms.sourcegitcommit: 3f5f9f7695b9ed3c45e9230cd8b8cb39a1c5a5ed
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/23/2020
ms.locfileid: "95566952"
---
# <a name="class-filehandlerobserver"></a>Classe FileHandler:: Observer 
Interfaccia Observer per il recupero di eventi di notifica correlati al gestore di file da parte dei client.
Tutti gli errori ereditano da mip::Error. I client non devono eseguire il callback del motore sul thread che chiama l'observer.
  
## <a name="summary"></a>Riepilogo
 Members                        | Descrizioni                                
--------------------------------|---------------------------------------------
public virtual void OnCreateFileHandlerSuccess(const std::shared_ptr\<FileHandler\>& fileHandler, const std::shared_ptr\<void\>& context)  |  Viene chiamato quando il gestore è creato correttamente.
public virtual void OnCreateFileHandlerFailure(const std::exception_ptr& error, const std::shared_ptr\<void\>& context)  |  Viene chiamato quando la creazione del gestore non è riuscita.
public virtual void OnClassifySuccess (const std:: Vector \<std::shared_ptr\<Action\> \>& actions, const std:: shared_ptr \<void\>& context)  |  Chiamato quando classifica l'esito positivo.
public virtual void OnClassifyFailure (const std:: exception_ptr& Error, const std:: shared_ptr \<void\>& context)  |  Chiamato quando la classificazione non è riuscita.
public virtual void OnGetDecryptedTemporaryFileSuccess (const std:: String& decryptedFilePath, const std:: shared_ptr \<void\>& context)  |  Chiamato quando il file temporaneo decrittografato riesce.
public virtual void OnGetDecryptedTemporaryFileFailure (const std:: exception_ptr& Error, const std:: shared_ptr \<void\>& context)  |  Chiamato quando il recupero del file temporaneo decrittografato non è riuscito.
public virtual void OnGetDecryptedTemporaryStreamSuccess (const std:: shared_ptr \<Stream\>& decryptedStream, const std:: shared_ptr \<void\>& context)  |  Chiamato quando il flusso temporaneo decrittografato riesce.
public virtual void OnGetDecryptedTemporaryStreamFailure (const std:: exception_ptr& Error, const std:: shared_ptr \<void\>& context)  |  Chiamato quando il recupero del flusso temporaneo decrittografato non è riuscito.
public virtual void OnCommitSuccess(bool committed, const std::shared_ptr\<void\>& context)  |  Viene chiamato quando il commit delle modifiche al file è riuscito correttamente.
public virtual void OnCommitFailure(const std::exception_ptr& error, const std::shared_ptr\<void\>& context)  |  Viene chiamato quando il commit delle modifiche al file non è riuscito.
public virtual void OnInspectSuccess (const std:: shared_ptr \<FileInspector\>& fileinspector, const std:: shared_ptr \<void\>& context)  |  Viene chiamato quando il controllo ha esito positivo.
public virtual void OnInspectFailure (const std:: exception_ptr& Error, const std:: shared_ptr \<void\>& context)  |  Chiamato quando il controllo non è riuscito.
  
## <a name="members"></a>Members
  
### <a name="oncreatefilehandlersuccess-function"></a>OnCreateFileHandlerSuccess (funzione)
Viene chiamato quando il gestore è creato correttamente.
  
### <a name="oncreatefilehandlerfailure-function"></a>OnCreateFileHandlerFailure (funzione)
Viene chiamato quando la creazione del gestore non è riuscita.
  
### <a name="onclassifysuccess-function"></a>OnClassifySuccess (funzione)
Chiamato quando classifica l'esito positivo.
  
### <a name="onclassifyfailure-function"></a>OnClassifyFailure (funzione)
Chiamato quando la classificazione non è riuscita.
  
### <a name="ongetdecryptedtemporaryfilesuccess-function"></a>OnGetDecryptedTemporaryFileSuccess (funzione)
Chiamato quando il file temporaneo decrittografato riesce.
  
### <a name="ongetdecryptedtemporaryfilefailure-function"></a>OnGetDecryptedTemporaryFileFailure (funzione)
Chiamato quando il recupero del file temporaneo decrittografato non è riuscito.
  
### <a name="ongetdecryptedtemporarystreamsuccess-function"></a>OnGetDecryptedTemporaryStreamSuccess (funzione)
Chiamato quando il flusso temporaneo decrittografato riesce.
  
### <a name="ongetdecryptedtemporarystreamfailure-function"></a>OnGetDecryptedTemporaryStreamFailure (funzione)
Chiamato quando il recupero del flusso temporaneo decrittografato non è riuscito.
  
### <a name="oncommitsuccess-function"></a>OnCommitSuccess (funzione)
Viene chiamato quando il commit delle modifiche al file è riuscito correttamente.
  
### <a name="oncommitfailure-function"></a>OnCommitFailure (funzione)
Viene chiamato quando il commit delle modifiche al file non è riuscito.
  
### <a name="oninspectsuccess-function"></a>OnInspectSuccess (funzione)
Viene chiamato quando il controllo ha esito positivo.
  
### <a name="oninspectfailure-function"></a>OnInspectFailure (funzione)
Chiamato quando il controllo non è riuscito.