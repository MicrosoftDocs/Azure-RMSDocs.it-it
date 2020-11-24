---
title: Classe FileExecutionState
description: 'Documenta la classe fileexecutionstate:: undefined di Microsoft Information Protection (MIP) SDK.'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 09/21/2020
ms.openlocfilehash: c84f7aa81fd628a8af9598653f0895dc0dd934d2
ms.sourcegitcommit: 3f5f9f7695b9ed3c45e9230cd8b8cb39a1c5a5ed
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/23/2020
ms.locfileid: "95566971"
---
# <a name="class-fileexecutionstate"></a>Classe FileExecutionState 
  
## <a name="summary"></a>Riepilogo
 Members                        | Descrizioni                                
--------------------------------|---------------------------------------------
public virtual DataState GetDataState () const  |  Ottiene lo stato del contenuto mentre l'applicazione interagisce con esso.
public virtual std:: shared_ptr \<ClassificationResults\> GetClassificationResults (const std:: shared_ptr \<FileHandler\> &, const std:: Vector \<std::shared_ptr\<ClassificationRequest\> \> &) const  |  Restituisce una mappa dei risultati della classificazione.
public virtual std:: Map \<std::string, std::string\> GetAuditMetadata () const  |  Restituisce una mappa delle coppie chiave-valore di controllo specifiche dell'applicazione.
  
## <a name="members"></a>Members
  
### <a name="getdatastate-function"></a>GetDataState (funzione)
Ottiene lo stato del contenuto mentre l'applicazione interagisce con esso.

  
**Restituisce**: stato dei dati del contenuto
  
### <a name="getclassificationresults-function"></a>GetClassificationResults (funzione)
Restituisce una mappa dei risultati della classificazione.

Parametri  
* **FileHandler**: il gestore di file del file usato 


* **classificationIds**: elenco di ID di classificazione. 



  
**Restituisce**: un elenco di risultati della classificazione.
  
### <a name="getauditmetadata-function"></a>GetAuditMetadata (funzione)
Restituisce una mappa delle coppie chiave-valore di controllo specifiche dell'applicazione.

  
**Returns**: elenco della chiave registrata dei metadati di controllo specifici dell'applicazione: coppie valore mittente: ID di posta elettronica per i destinatari del mittente: rappresenta una matrice JSON di destinatari per un messaggio di posta elettronica LastModifiedBy: ID di posta elettronica per l'utente che ha apportato l'ultima modifica al contenuto LastModifiedDate: data dell'Ultima modifica del contenuto