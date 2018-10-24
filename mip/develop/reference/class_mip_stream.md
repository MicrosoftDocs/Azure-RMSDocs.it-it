---
title: Classe mip Stream
description: Riferimento per la classe mip Stream
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: e6296c5e15590741e008979dcf12373ff5fcdf00
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/28/2018
ms.locfileid: "47445224"
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
  
### <a name="read"></a>Lettura
Legge in un buffer dal flusso.

Parametri:  
* **buffer**: puntatore a un buffer 


* **bufferLength**: dimensioni del buffer. 



  
**Restituisce**: numero di byte letti.
  
### <a name="write"></a>Monitoraggio
Scrive nel flusso da un buffer.

Parametri:  
* **buffer**: puntatore a un buffer 


* **bufferLength**: dimensioni del buffer. 



  
**Restituisce**: numero di byte scritti.
  
### <a name="flush"></a>Svuotamento
Scarica il flusso.

  
**Restituisce**: true se l'operazione ha esito positivo, in caso contrario false.
  
### <a name="seek"></a>Seek
Cerca una posizione all'interno del flusso.

Parametri:  
* **position**: posizione da cercare nel flusso.


  
### <a name="canread"></a>CanRead
Verifica se il flusso può essere letto.

  
**Restituisce**: true se è leggibile, in caso contrario false.
  
### <a name="canwrite"></a>CanWrite
Verifica se il flusso può essere scritto.

  
**Restituisce**: true se è scrivibile, in caso contrario false.
  
### <a name="position"></a>Posizione
Ottiene la posizione corrente all'interno del flusso.

  
**Restituisce**: posizione all'interno del flusso.
  
### <a name="size"></a>Dimensioni
Ottiene le dimensioni del contenuto all'interno del flusso.

  
**Restituisce**: dimensioni del flusso.
  
### <a name="size"></a>Dimensioni
Imposta le dimensioni del flusso.

Parametri:  
* **stream**: dimensioni.

