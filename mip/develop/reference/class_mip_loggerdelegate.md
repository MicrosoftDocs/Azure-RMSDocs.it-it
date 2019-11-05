---
title: Classe mip::LoggerDelegate
description: 'Documenta la classe MIP:: loggerdelegate di Microsoft Information Protection (MIP) SDK.'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 10/29/2019
ms.openlocfilehash: f1726c53afb7e398f8921e1cb8fc67e3166fffe8
ms.sourcegitcommit: f5d8cf4440a35afaa1ff1a58b2a022740ed85ffd
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/04/2019
ms.locfileid: "73561053"
---
# <a name="class-miploggerdelegate"></a>Classe mip::LoggerDelegate 
Classe che definisce l'interfaccia per il logger MIP SDK.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public void Init(const std::string& storagePath)  |  Inizializza il logger.
public void Flush()  |  Scarica il logger.
public void WriteToLog(const LogLevel level, const std::string& message, const std::string& function, const std::string& file, const int32_t line)  |  Scrive un'istruzione log in file di log.
  
## <a name="members"></a>Membri
  
### <a name="init-function"></a>Funzione init
Inizializza il logger.

Parametri:  
* **storagePath**: percorso della posizione in cui è possibile archiviare lo stato persistente, inclusi i log.


  
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

