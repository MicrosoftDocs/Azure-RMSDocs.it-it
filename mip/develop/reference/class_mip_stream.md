---
title: Classe mip::Stream
description: 'Documenta la classe MIP:: Stream di Microsoft Information Protection (MIP) SDK.'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 02/14/2020
ms.openlocfilehash: 65e50fc9751b2ac38e2dae216e3e81cacba5c832
ms.sourcegitcommit: 2d3c638fb576f3f074330a33d077db0cf0e7d4e7
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/20/2020
ms.locfileid: "77489402"
---
# <a name="class-mipstream"></a>Classe mip::Stream 
Classe che definisce l'interfaccia tra Microsoft Information Protection SDK e il contenuto basato su flusso.
  
## <a name="summary"></a>Riepilogo
 Members                        | Descrizioni                                
--------------------------------|---------------------------------------------
public int64_t Read(uint8_t* buffer, int64_t bufferLength)  |  Legge in un buffer dal flusso.
public int64_t Write(const uint8_t* buffer, int64_t bufferLength)  |  Scrive nel flusso da un buffer.
public bool Flush()  |  Scarica il flusso.
public void Seek(int64_t position)  |  Cerca una posizione all'interno del flusso.
public bool CanRead() const  |  Verifica se il flusso può essere letto.
public bool CanWrite() const  |  Verifica se il flusso può essere scritto.
public int64_t Position()  |  Ottiene la posizione corrente all'interno del flusso.
public int64_t Size()  |  Ottiene le dimensioni del contenuto all'interno del flusso.
public void Size(int64_t value)  |  Imposta le dimensioni del flusso.
  
## <a name="members"></a>Members
  
### <a name="read-function"></a>Read (funzione)
Legge in un buffer dal flusso.

Parametri:  
* **buffer**: puntatore a un buffer 


* **bufferLength**: dimensioni del buffer. 



  
**Restituisce**: numero di byte letti.
  
### <a name="write-function"></a>Write (funzione)
Scrive nel flusso da un buffer.

Parametri:  
* **buffer**: puntatore a un buffer 


* **bufferLength**: dimensioni del buffer. 



  
**Restituisce**: numero di byte scritti.
  
### <a name="flush-function"></a>Flush (funzione)
Scarica il flusso.

  
**Restituisce**: true se l'operazione ha esito positivo, in caso contrario false.
  
### <a name="seek-function"></a>Seek (funzione)
Cerca una posizione all'interno del flusso.

Parametri:  
* **position**: posizione da cercare nel flusso.


  
### <a name="canread-function"></a>Funzione CanRead
Verifica se il flusso può essere letto.

  
**Restituisce**: true se è leggibile, in caso contrario false.
  
### <a name="canwrite-function"></a>CanWrite (funzione)
Verifica se il flusso può essere scritto.

  
**Restituisce**: true se è scrivibile, in caso contrario false.
  
### <a name="position-function"></a>Position (funzione)
Ottiene la posizione corrente all'interno del flusso.

  
**Restituisce**: posizione all'interno del flusso.
  
### <a name="size-function"></a>Size (funzione)
Ottiene le dimensioni del contenuto all'interno del flusso.

  
**Restituisce**: dimensioni del flusso.
  
### <a name="size-function"></a>Size (funzione)
Imposta le dimensioni del flusso.

Parametri:  
* **stream**: dimensioni.

