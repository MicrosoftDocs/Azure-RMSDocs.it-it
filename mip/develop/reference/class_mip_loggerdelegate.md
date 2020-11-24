---
title: Classe LoggerDelegate
description: 'Documenta la classe loggerdelegate:: undefined di Microsoft Information Protection (MIP) SDK.'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 09/21/2020
ms.openlocfilehash: 48b01649d3c9b3e8089294d0012fa6393362e98e
ms.sourcegitcommit: 3f5f9f7695b9ed3c45e9230cd8b8cb39a1c5a5ed
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/23/2020
ms.locfileid: "95566792"
---
# <a name="class-loggerdelegate"></a>Classe LoggerDelegate 
Classe che definisce l'interfaccia per il logger MIP SDK.
  
## <a name="summary"></a>Riepilogo
 Members                        | Descrizioni                                
--------------------------------|---------------------------------------------
public void Init(const std::string& storagePath)  |  Inizializzare il logger.
public void Flush()  |  Scarica il logger.
public void WriteToLog(const LogLevel level, const std::string& message, const std::string& function, const std::string& file, const int32_t line)  |  Scrive un'istruzione log in file di log.
  
## <a name="members"></a>Members
  
### <a name="init-function"></a>Funzione init
Inizializzare il logger.

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

