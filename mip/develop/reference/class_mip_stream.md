---
title: Classe mip::Stream
description: 'Documenta la classe MIP:: Stream di Microsoft Information Protection (MIP) SDK.'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 10/29/2019
ms.openlocfilehash: f1bd4220369d036c2071453412844e0691efb2ec
ms.sourcegitcommit: f5d8cf4440a35afaa1ff1a58b2a022740ed85ffd
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/04/2019
ms.locfileid: "73559967"
---
# <a name="class-mipstream"></a>Classe mip::Stream 
Classe che definisce l'interfaccia tra Microsoft Information Protection SDK e il contenuto basato su flusso.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
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
  
## <a name="members"></a>Membri
  
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
  
### <a name="seek-function"></a>Funzione Seek
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

