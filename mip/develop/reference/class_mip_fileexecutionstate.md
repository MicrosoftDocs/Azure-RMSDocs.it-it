---
title: class mip::FileExecutionState
description: Documenta la classe mip::fileexecutionstate di Microsoft Information Protection (MIP) SDK.
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: 380e5f6732a2662d83b9bb37af5763ef30ffa3bf
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/14/2019
ms.locfileid: "56259219"
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
