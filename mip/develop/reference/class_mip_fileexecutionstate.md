---
title: class mip::FileExecutionState
description: Documenta la classe mip::fileexecutionstate di Microsoft Information Protection (MIP) SDK.
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: 9433ca2f47496e0d28d46c68b3100b53cd25c3f3
ms.sourcegitcommit: 471b3683367d93f0673c1cf276a15f83572aa80e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/05/2019
ms.locfileid: "57333687"
---
# <a name="class-mipfileexecutionstate"></a>class mip::FileExecutionState 
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
Public std:: Map virtual\<std:: String, std:: shared_ptr\<ClassificationResult\> \> GetClassificationResults (const std:: shared_ptr\<FileHandler\> &, const std :: vector\<std:: shared_ptr\<ClassificationRequest\> \> &) const  |  Restituisce una mappa dei risultati della classificazione.
Public std:: Vector virtual\<uint8_t\> GetSerializedProtectionInfo() const  |  Restituisce un buffer con il PL. serializzato
  
## <a name="members"></a>Membri
  
### <a name="getclassificationresults-function"></a>GetClassificationResults (funzione)
Restituisce una mappa dei risultati della classificazione.

Parametri:  
* **fileHandler**:-il gestore di file del file usato 


* **classificationIds**: un elenco di ID di classificazione. 



  
**Restituisce**: Elenco di risultati di classificazione.
  
### <a name="getserializedprotectioninfo-function"></a>GetSerializedProtectionInfo function
Restituisce un buffer con il PL. serializzato

  
**Restituisce**: Un buffer con il PL. serializzato
