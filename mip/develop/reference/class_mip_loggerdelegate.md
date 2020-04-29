---
title: Classe LoggerDelegate
description: 'Documenta la classe loggerdelegate:: undefined di Microsoft Information Protection (MIP) SDK.'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 04/16/2020
ms.openlocfilehash: e213f243a0e46bb804b224c7a0752a0b9b270103
ms.sourcegitcommit: f54920bf017902616589aca30baf6b64216b6913
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/22/2020
ms.locfileid: "81761826"
---
# <a name="class-loggerdelegate"></a>Classe LoggerDelegate 
Classe che definisce l'interfaccia per il logger MIP SDK.
  
## <a name="summary"></a>Riepilogo
 Members                        | Descrizioni                                
--------------------------------|---------------------------------------------
public void Init(const std::string& storagePath)  |  Inizializza il logger.
public void Flush()  |  Scarica il logger.
public void WriteToLog(const LogLevel level, const std::string& message, const std::string& function, const std::string& file, const int32_t line)  |  Scrive un'istruzione log in file di log.
  
## <a name="members"></a>Members
  
### <a name="init-function"></a>Funzione init
Inizializza il logger.

Parametri  
* **storagePath**: percorso della posizione in cui è possibile archiviare lo stato persistente, inclusi i log.


  
### <a name="flush-function"></a>Flush (funzione)
Scarica il logger.
  
### <a name="writetolog-function"></a>WriteToLog (funzione)
Scrive un'istruzione log in file di log.

Parametri  
* **level**: livello di log per l'istruzione log. 


* **message**: messaggio per l'istruzione log. 


* **function**: nome della funzione per l'istruzione log. 


* **file**: nome file in cui è stata generata l'istruzione log. 


* **line**: numero di riga in cui è stata generata l'istruzione log.

