---
title: Classe mip LoggerDelegate
description: Riferimento per la classe mip LoggerDelegate
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: b25cdb177735feccfa5c4d344613e4747d18b77f
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/28/2018
ms.locfileid: "47445853"
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
  
### <a name="init"></a>Init
Inizializza il logger.

Parametri:  
* **storagePath**: percorso della posizione in cui è possibile archiviare lo stato persistente, inclusi i log. 


* **logLevel**: livello di log minimo che attiverà un evento di registrazione.


  
### <a name="loglevel"></a>LogLevel
Ottiene il livello di log minimo che attiverà un evento di registrazione.

  
**Restituisce**: livello di log minimo che attiverà un evento di registrazione.
  
### <a name="flush"></a>Svuotamento
Scarica il logger.
  
### <a name="writetolog"></a>WriteToLog
Scrive un'istruzione log in file di log.

Parametri:  
* **level**: livello di log per l'istruzione log. 


* **message**: messaggio per l'istruzione log. 


* **function**: nome della funzione per l'istruzione log. 


* **file**: nome file in cui è stata generata l'istruzione log. 


* **line**: numero di riga in cui è stata generata l'istruzione log.

