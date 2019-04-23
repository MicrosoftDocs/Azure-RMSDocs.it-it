---
title: Classe mip::LoggerDelegate
description: Documenta la classe mip::loggerdelegate di Microsoft Information Protection (MIP) SDK.
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: 511c8dabc8ff31c70c8343a80d423b76c43fa946
ms.sourcegitcommit: 682dc48cbbcbee93b26ab3872231b3fa54d3f6eb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "60184621"
---
# <a name="class-miploggerdelegate"></a>Classe mip::LoggerDelegate 
Classe che definisce l'interfaccia per il logger MIP SDK.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public void Init(const std::string& storagePath, LogLevel logLevel)  |  Inizializza il logger.
public LogLevel GetLogLevel() const  |  Ottiene il livello di log minimo che attiverà un evento di registrazione.
public void Flush()  |  Scarica il logger.
public void WriteToLog(const LogLevel level, const std::string& message, const std::string& function, const std::string& file, const int32_t line)  |  Scrive un'istruzione log in file di log.
  
## <a name="members"></a>Membri
  
### <a name="init-function"></a>Init (funzione)
Inizializza il logger.

Parametri:  
* **storagePath**: percorso della posizione in cui è possibile archiviare lo stato persistente, inclusi i log. 


* **logLevel**: livello di log minimo che attiverà un evento di registrazione.


  
### <a name="getloglevel-function"></a>GetLogLevel (funzione)
Ottiene il livello di log minimo che attiverà un evento di registrazione.

  
**Restituisce**: Il livello di registrazione più basso che attiva un evento di registrazione.
  
### <a name="flush-function"></a>Flush (funzione)
Scarica il logger.
  
### <a name="writetolog-function"></a>WriteToLog (funzione)
Scrive un'istruzione log in file di log.

Parametri:  
* **level**: livello di log per l'istruzione log. 


* **message**: messaggio per l'istruzione log. 


* **function**: nome della funzione per l'istruzione log. 


* **file**: nome file in cui è stata generata l'istruzione log. 


* **line**: numero di riga in cui è stata generata l'istruzione log.

