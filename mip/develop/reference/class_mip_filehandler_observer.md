---
title: Classe mip::FileHandler::Observer
description: 'Classe MIP:: FileHandler di Microsoft Information Protection (MIP) SDK vengono documentate.'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: 4204bd17abe756c42c672a1cda17706b59600795
ms.sourcegitcommit: ea76aade54134afaf5023145fcb755e40c7b84b7
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/15/2019
ms.locfileid: "59573668"
---
# <a name="class-mipfilehandlerobserver"></a>Classe mip::FileHandler::Observer 
Interfaccia [Observer](class_mip_filehandler_observer.md) per il recupero di eventi di notifica correlati al gestore di file da parte dei client.
Tutti gli errori ereditano da [mip::Error](class_mip_error.md). I client non devono eseguire il callback del motore sul thread che chiama l'observer.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
OnCreateFileHandlerSuccess void virtuale pubblico (const std:: shared_ptr\<FileHandler\>& fileHandler, const std:: shared_ptr\<void\>& contesto)  |  Viene chiamato quando il gestore è creato correttamente.
OnCreateFileHandlerFailure void virtuale pubblico (std::exception_ptr const & errore, const std:: shared_ptr\<void\>& contesto)  |  Viene chiamato quando la creazione del gestore non è riuscita.
OnClassifySuccess void virtuale pubblico (const std:: Vector\<std:: shared_ptr\<azione\>\>& azioni, const std:: shared_ptr\<void\>& contesto)  |  Chiamato quando la classificazione di esito positivo.
public virtual void OnClassifyFailure(const std::exception_ptr& error, const std::shared_ptr\<void\>& context)  |  Chiamato quando la classificazione non è riuscita.
OnGetDecryptedTemporaryFileSuccess void virtuale pubblico (const std:: String & decryptedFilePath, const std:: shared_ptr\<void\>& contesto)  |  Chiamato quando si recupera il successo di file temporanei decrittografato.
public virtual void OnGetDecryptedTemporaryFileFailure(const std::exception_ptr& error, const std::shared_ptr\<void\>& context)  |  Chiamato quando si recupera il file temporaneo decrittografato non è riuscito.
OnCommitSuccess void virtuale pubblico (bool esegue il commit, const std:: shared_ptr\<void\>& contesto)  |  Viene chiamato quando il commit delle modifiche al file è riuscito correttamente.
OnCommitFailure void virtuale pubblico (std::exception_ptr const & errore, const std:: shared_ptr\<void\>& contesto)  |  Viene chiamato quando il commit delle modifiche al file non è riuscito.
  
## <a name="members"></a>Membri
  
### <a name="oncreatefilehandlersuccess-function"></a>OnCreateFileHandlerSuccess (funzione)
Viene chiamato quando il gestore è creato correttamente.
  
### <a name="oncreatefilehandlerfailure-function"></a>OnCreateFileHandlerFailure (funzione)
Viene chiamato quando la creazione del gestore non è riuscita.
  
### <a name="onclassifysuccess-function"></a>OnClassifySuccess (funzione)
Chiamato quando la classificazione di esito positivo.
  
### <a name="onclassifyfailure-function"></a>OnClassifyFailure (funzione)
Chiamato quando la classificazione non è riuscita.
  
### <a name="ongetdecryptedtemporaryfilesuccess-function"></a>OnGetDecryptedTemporaryFileSuccess (funzione)
Chiamato quando si recupera il successo di file temporanei decrittografato.
  
### <a name="ongetdecryptedtemporaryfilefailure-function"></a>OnGetDecryptedTemporaryFileFailure (funzione)
Chiamato quando si recupera il file temporaneo decrittografato non è riuscito.
  
### <a name="oncommitsuccess-function"></a>OnCommitSuccess (funzione)
Viene chiamato quando il commit delle modifiche al file è riuscito correttamente.
  
### <a name="oncommitfailure-function"></a>OnCommitFailure (funzione)
Viene chiamato quando il commit delle modifiche al file non è riuscito.