---
title: 'Classe MIP:: FileExecutionState'
description: 'Documenta la classe MIP:: fileexecutionstate di Microsoft Information Protection (MIP) SDK.'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 02/14/2020
ms.openlocfilehash: a55ad7b5d28a3115ea4f17f36a846011e82d7827
ms.sourcegitcommit: 2d3c638fb576f3f074330a33d077db0cf0e7d4e7
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/20/2020
ms.locfileid: "77490048"
---
# <a name="class-mipfileexecutionstate"></a>Classe MIP:: FileExecutionState 
  
## <a name="summary"></a>Riepilogo
 Members                        | Descrizioni                                
--------------------------------|---------------------------------------------
public virtual DataState GetDataState () const  |  Ottiene lo stato del contenuto mentre l'applicazione interagisce con esso.
public virtual std:: shared_ptr\<ClassificationResults\> GetClassificationResults (const std:: shared_ptr\<FileHandler\> &, const std:: Vector\<std:: shared_ptr\<ClassificationRequest\>\> &) const  |  Restituisce una mappa dei risultati della classificazione.
public virtual std:: Map\<std:: String, std:: String\> GetAuditMetadata () const  |  Restituisce una mappa delle coppie chiave-valore di controllo specifiche dell'applicazione.
  
## <a name="members"></a>Members
  
### <a name="getdatastate-function"></a>GetDataState (funzione)
Ottiene lo stato del contenuto mentre l'applicazione interagisce con esso.

  
**Restituisce**: stato dei dati del contenuto
  
### <a name="getclassificationresults-function"></a>GetClassificationResults (funzione)
Restituisce una mappa dei risultati della classificazione.

Parametri:  
* **FileHandler**: il gestore di file del file usato 


* **classificationIds**: elenco di ID di classificazione. 



  
**Restituisce**: un elenco di risultati della classificazione.
  
### <a name="getauditmetadata-function"></a>GetAuditMetadata (funzione)
Restituisce una mappa delle coppie chiave-valore di controllo specifiche dell'applicazione.

  
**Returns**: elenco della chiave registrata dei metadati di controllo specifici dell'applicazione: coppie valore mittente: ID di posta elettronica per i destinatari del mittente: rappresenta una matrice JSON di destinatari per un messaggio di posta elettronica LastModifiedBy: ID di posta elettronica per l'utente che ha apportato l'ultima modifica al contenuto LastModifiedDate: data dell'Ultima modifica del contenuto