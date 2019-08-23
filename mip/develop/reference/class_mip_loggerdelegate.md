---
title: Classe mip::LoggerDelegate
description: 'Documenta la classe MIP:: loggerdelegate di Microsoft Information Protection (MIP) SDK.'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 07/16/2019
ms.openlocfilehash: effba9bc41907c477cea7e3cf6a8688187538068
ms.sourcegitcommit: fcde8b31f8685023f002044d3a1d1903e548d207
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/21/2019
ms.locfileid: "69883916"
---
# <a name="class-miploggerdelegate"></a>Classe mip::LoggerDelegate 
Classe che definisce l'interfaccia per il logger MIP SDK.
  
## <a name="summary"></a>Riepilogo
 Members                        | Descrizioni                                
--------------------------------|---------------------------------------------
public void Init(const std::string& storagePath, LogLevel logLevel)  |  Inizializza il logger.
public LogLevel GetLogLevel() const  |  Ottiene il livello di log minimo che attiverà un evento di registrazione.
public void Flush()  |  Scarica il logger.
public void WriteToLog(const LogLevel level, const std::string& message, const std::string& function, const std::string& file, const int32_t line)  |  Scrive un'istruzione log in file di log.
  
## <a name="members"></a>Members
  
### <a name="init-function"></a>Funzione init
Inizializza il logger.

Parametri:  
* **storagePath**: percorso della posizione in cui è possibile archiviare lo stato persistente, inclusi i log. 


* **logLevel**: livello di log minimo che attiverà un evento di registrazione.


  
### <a name="getloglevel-function"></a>GetLogLevel (funzione)
Ottiene il livello di log minimo che attiverà un evento di registrazione.

  
**Restituisce**: Livello di log più basso che attiverà un evento di registrazione.
  
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

