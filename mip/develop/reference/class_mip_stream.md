---
title: Classe mip::Stream
description: 'Classe MIP:: Stream di Microsoft Information Protection (MIP) SDK vengono documentate.'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: 4289b39ba454b19c6836a7eaccb6333cbb9000b4
ms.sourcegitcommit: be05adc7750e22c110b261882de0389b9dfb2726
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/02/2019
ms.locfileid: "55651701"
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



  
**Restituisce**: Numero di byte letti.
  
### <a name="write-function"></a>Scrivere una funzione
Scrive nel flusso da un buffer.

Parametri:  
* **buffer**: puntatore a un buffer 


* **bufferLength**: dimensioni del buffer. 



  
**Restituisce**: Numero di byte scritti.
  
### <a name="flush-function"></a>Flush (funzione)
Scarica il flusso.

  
**Restituisce**: True se ha esito positivo in caso contrario false.
  
### <a name="seek-function"></a>Seek (funzione)
Cerca una posizione all'interno del flusso.

Parametri:  
* **position**: posizione da cercare nel flusso.


  
### <a name="canread-function"></a>Proprietà CanRead (funzione)
Verifica se il flusso può essere letto.

  
**Restituisce**: True se leggibili in caso contrario false.
  
### <a name="canwrite-function"></a>CanWrite (funzione)
Verifica se il flusso può essere scritto.

  
**Restituisce**: True se è scrivibile in caso contrario false.
  
### <a name="position-function"></a>Position-funzione
Ottiene la posizione corrente all'interno del flusso.

  
**Restituisce**: Posizione all'interno del flusso.
  
### <a name="size-function"></a>Funzione Size
Ottiene le dimensioni del contenuto all'interno del flusso.

  
**Restituisce**: Le dimensioni del flusso.
  
### <a name="size-function"></a>Funzione Size
Imposta le dimensioni del flusso.

Parametri:  
* **stream**: dimensioni.

