---
title: class mip::FileExecutionState
description: Documenta la classe mip::fileexecutionstate di Microsoft Information Protection (MIP) SDK.
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: bdf0814e56d64bd16918a6f4d269a057620f92f5
ms.sourcegitcommit: fff4c155c52c9ff20bc4931d5ac20c3ea6e2ff9e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/24/2019
ms.locfileid: "60184672"
---
# <a name="class-mipfileexecutionstate"></a>class mip::FileExecutionState 
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public virtual DataState GetDataState() const  |  Ottiene lo stato del contenuto mentre l'applicazione interagisce con esso.
Public std:: shared_ptr virtual\<ClassificationResults\> GetClassificationResults (const std:: shared_ptr\<FileHandler\> &, const std:: Vector\<std::shared_ptr\<ClassificationRequest\> \> &) const  |  Restituisce una mappa dei risultati della classificazione.
Public std:: Vector virtual\<uint8_t\> GetSerializedProtectionInfo() const  |  Restituisce un buffer con il PL. serializzato
public virtual std::map\<std::string, std::string\> GetAuditMetadata() const  |  Restituisce una mappa di coppie chiave-valore di controllo specifico dell'applicazione.
  
## <a name="members"></a>Membri
  
### <a name="getdatastate-function"></a>GetDataState (funzione)
Ottiene lo stato del contenuto mentre l'applicazione interagisce con esso.

  
**Restituisce**: Stato dei dati del contenuto
  
### <a name="getclassificationresults-function"></a>GetClassificationResults (funzione)
Restituisce una mappa dei risultati della classificazione.

Parametri:  
* **fileHandler**:-il gestore di file del file usato 


* **classificationIds**: un elenco di ID di classificazione. 



  
**Restituisce**: Un elenco dei risultati di classificazione.
  
### <a name="getserializedprotectioninfo-function"></a>GetSerializedProtectionInfo function
Restituisce un buffer con il PL. serializzato

  
**Restituisce**: Un buffer con il PL. serializzato
  
### <a name="getauditmetadata-function"></a>GetAuditMetadata (funzione)
Restituisce una mappa di coppie chiave-valore di controllo specifico dell'applicazione.

  
**Restituisce**: Un elenco di coppie chiave: valore registrato di metadati controllo specifico dell'applicazione mittente: Id di posta elettronica del mittente, destinatari: Rappresenta una matrice JSON dei destinatari del messaggio di posta elettronica LastModifiedBy: Id di posta elettronica per l'utente che ha modificato il LastModifiedDate & lt; contenuto: Data che ultima modifica del contenuto