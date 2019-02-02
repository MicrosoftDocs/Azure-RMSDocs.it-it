---
title: class mip::FileExecutionState
description: Documenta la classe mip::fileexecutionstate di Microsoft Information Protection (MIP) SDK.
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: 08a9064645f0ffb3ffbaa72f00db26c5b29d3643
ms.sourcegitcommit: be05adc7750e22c110b261882de0389b9dfb2726
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/02/2019
ms.locfileid: "55652337"
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