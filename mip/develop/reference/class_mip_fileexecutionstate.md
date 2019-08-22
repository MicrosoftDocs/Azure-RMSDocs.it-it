---
title: 'Classe MIP:: FileExecutionState'
description: 'Documenta la classe MIP:: fileexecutionstate di Microsoft Information Protection (MIP) SDK.'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 07/16/2019
ms.openlocfilehash: 24750ea7c719545889cb833aa4c685fdcd1e9e3d
ms.sourcegitcommit: fcde8b31f8685023f002044d3a1d1903e548d207
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/21/2019
ms.locfileid: "69885727"
---
# <a name="class-mipfileexecutionstate"></a>Classe MIP:: FileExecutionState 
  
## <a name="summary"></a>Riepilogo
 Members                        | Descrizioni                                
--------------------------------|---------------------------------------------
public virtual DataState GetDataState () const  |  Ottiene lo stato del contenuto mentre l'applicazione interagisce con esso.
public virtual std:: shared_ptr\<ClassificationResults\> GetClassificationResults (const std:\> :\<shared_ptr FileHandler &, const std:\<: vector std:: shared_ptr\<ClassificationRequest\>&)const \>  |  Restituisce una mappa dei risultati della classificazione.
public virtual std:: Map\<std:: String, std:: String\> GetAuditMetadata () const  |  Restituisce una mappa delle coppie chiave-valore di controllo specifiche dell'applicazione.
  
## <a name="members"></a>Members
  
### <a name="getdatastate-function"></a>GetDataState (funzione)
Ottiene lo stato del contenuto mentre l'applicazione interagisce con esso.

  
**Restituisce**: Stato dei dati di contenuto
  
### <a name="getclassificationresults-function"></a>GetClassificationResults (funzione)
Restituisce una mappa dei risultati della classificazione.

Parametri:  
* FileHandler: il gestore di file del file usato 


* **classificationIds**: elenco di ID di classificazione. 



  
**Restituisce**: Elenco di risultati della classificazione.
  
### <a name="getauditmetadata-function"></a>GetAuditMetadata (funzione)
Restituisce una mappa delle coppie chiave-valore di controllo specifiche dell'applicazione.

  
**Restituisce**: Elenco dei metadati di controllo specifici dell'applicazione chiave registrata: coppie valore mittente: ID di posta elettronica per i destinatari del mittente: Rappresenta una matrice JSON di destinatari per un LastModifiedBy di posta elettronica: ID di posta elettronica per l'utente che ha apportato l'ultima modifica al contenuto LastModifiedDate: Data dell'Ultima modifica apportata al contenuto