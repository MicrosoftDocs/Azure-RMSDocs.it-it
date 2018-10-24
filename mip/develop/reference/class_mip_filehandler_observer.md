---
title: Classe mip FileHandler Observer
description: Riferimento per la classe mip FileHandler Observer
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: a587107afc2b8963d64c31ad47af81761bf2b9f8
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/28/2018
ms.locfileid: "47446175"
---
# <a name="class-mipfilehandlerobserver"></a>Classe mip::FileHandler::Observer 
Interfaccia [Observer](class_mip_filehandler_observer.md) per il recupero di eventi di notifica correlati al gestore di file da parte dei client.
Tutti gli errori ereditano da [mip::Error](class_mip_error.md). I client non devono eseguire il callback del motore sul thread che chiama l'observer.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public virtual void OnCreateFileHandlerSuccess(const std::shared_ptr<FileHandler>& fileHandler, const std::shared_ptr<void>& context)  |  Viene chiamato quando il gestore è creato correttamente.
public virtual void OnCreateFileHandlerFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context)  |  Viene chiamato quando la creazione del gestore non è riuscita.
public virtual void OnGetLabelSuccess(const std::shared_ptr<ContentLabel>& label, const std::shared_ptr<void>& context)  |  Viene chiamato quando l'etichetta viene recuperata correttamente.
public virtual void OnGetLabelFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context)  |  Viene chiamato quando il recupero dell'etichetta non è riuscito.
public virtual void OnGetProtectionSuccess(const std::shared_ptr<ProtectionHandler>& protectionHandler, const std::shared_ptr<void>& context)  |  Viene chiamato quando i criteri di protezione vengono recuperati correttamente.
public virtual void OnGetProtectionFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context)  |  Viene chiamato quando il recupero dei criteri di protezione non è riuscito.
public virtual void OnCommitSuccess(bool committed, const std::shared_ptr<void>& context)  |  Viene chiamato quando il commit delle modifiche al file è riuscito correttamente.
public virtual void OnCommitFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context)  |  Viene chiamato quando il commit delle modifiche al file non è riuscito.
  
## <a name="members"></a>Membri
  
### <a name="oncreatefilehandlersuccess"></a>OnCreateFileHandlerSuccess
Viene chiamato quando il gestore è creato correttamente.
  
### <a name="oncreatefilehandlerfailure"></a>OnCreateFileHandlerFailure
Viene chiamato quando la creazione del gestore non è riuscita.
  
### <a name="ongetlabelsuccess"></a>OnGetLabelSuccess
Viene chiamato quando l'etichetta viene recuperata correttamente.
  
### <a name="ongetlabelfailure"></a>OnGetLabelFailure
Viene chiamato quando il recupero dell'etichetta non è riuscito.
  
### <a name="ongetprotectionsuccess"></a>OnGetProtectionSuccess
Viene chiamato quando i criteri di protezione vengono recuperati correttamente.
  
### <a name="ongetprotectionfailure"></a>OnGetProtectionFailure
Viene chiamato quando il recupero dei criteri di protezione non è riuscito.
  
### <a name="oncommitsuccess"></a>OnCommitSuccess
Viene chiamato quando il commit delle modifiche al file è riuscito correttamente.
  
### <a name="oncommitfailure"></a>OnCommitFailure
Viene chiamato quando il commit delle modifiche al file non è riuscito.