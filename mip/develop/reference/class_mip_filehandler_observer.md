---
title: Classe mip::FileHandler::Observer
description: "Documenta la classe MIP:: FileHandler dell'SDK Microsoft Information Protection (MIP)."
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 08/27/2019
ms.openlocfilehash: bcaf01e24ed01819e973576a70258e00e900ad28
ms.sourcegitcommit: 1499790746145d40d667d138baa6e18598421f0e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/27/2019
ms.locfileid: "70054975"
---
# <a name="class-mipfilehandlerobserver"></a>Classe mip::FileHandler::Observer 
Interfaccia [Observer](class_mip_filehandler_observer.md) per il recupero di eventi di notifica correlati al gestore di file da parte dei client.
Tutti gli errori ereditano da [mip::Error](class_mip_error.md). I client non devono eseguire il callback del motore sul thread che chiama l'observer.
  
## <a name="summary"></a>Riepilogo
 Members                        | Descrizioni                                
--------------------------------|---------------------------------------------
public virtual void OnCreateFileHandlerSuccess (const std::\<shared_ptr\>FileHandler & FileHandler, const std::\<shared_ptr\>void & context)  |  Viene chiamato quando il gestore è creato correttamente.
public virtual void OnCreateFileHandlerFailure (const std:: exception_ptr & Error, const std:\<:\>shared_ptr void & context)  |  Viene chiamato quando la creazione del gestore non è riuscita.
public virtual void OnClassifySuccess (const std::\<vector std::\<shared_ptr\>azione & Actions\>, const std\<:\>: shared_ptr void & context)  |  Chiamato quando classifica l'esito positivo.
public virtual void OnClassifyFailure (const std:: exception_ptr & Error, const std:\<:\>shared_ptr void & context)  |  Chiamato quando la classificazione non è riuscita.
public virtual void OnGetDecryptedTemporaryFileSuccess (const std:: String & decryptedFilePath, const std:\<:\>shared_ptr void & context)  |  Chiamato quando il file temporaneo decrittografato riesce.
public virtual void OnGetDecryptedTemporaryFileFailure (const std:: exception_ptr & Error, const std:\<:\>shared_ptr void & context)  |  Chiamato quando il recupero del file temporaneo decrittografato non è riuscito.
public virtual void OnGetDecryptedTemporaryStreamSuccess (const std::\<shared_ptr\>Stream & decryptedStream, const std:\<:\>shared_ptr void & context)  |  Chiamato quando il flusso temporaneo decrittografato riesce.
public virtual void OnGetDecryptedTemporaryStreamFailure (const std:: exception_ptr & Error, const std:\<:\>shared_ptr void & context)  |  Chiamato quando il recupero del flusso temporaneo decrittografato non è riuscito.
public virtual void OnCommitSuccess (bool committed, const std::\<shared_ptr\>void & context)  |  Viene chiamato quando il commit delle modifiche al file è riuscito correttamente.
public virtual void OnCommitFailure (const std:: exception_ptr & Error, const std:\<:\>shared_ptr void & context)  |  Viene chiamato quando il commit delle modifiche al file non è riuscito.
public virtual void OnInspectSuccess (const std::\<shared_ptr fileinspector\>& fileinspector, const std:\<:\>shared_ptr void & context)  |  Viene chiamato quando il controllo ha esito positivo.
public virtual void OnInspectFailure (const std:: exception_ptr & Error, const std:\<:\>shared_ptr void & context)  |  Chiamato quando il controllo non è riuscito.
  
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