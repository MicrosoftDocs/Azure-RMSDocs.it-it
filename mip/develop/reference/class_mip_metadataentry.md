---
title: Classe MetadataEntry
description: 'Documenta la classe metadataentry:: undefined di Microsoft Information Protection (MIP) SDK.'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/13/2021
ms.openlocfilehash: dd758d49d0c207fe5e4c5eeb04bb63ba91174fcc
ms.sourcegitcommit: 76926b357bbfc8772ed132ce5f2426fbea59e98b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/14/2021
ms.locfileid: "98215188"
---
# <a name="class-metadataentry"></a>Classe MetadataEntry 
Classe di astrazione per la voce di metadati.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public MetadataEntry (const std:: String& Key, const std:: String& value, uint32_t Version)  |  Al costruttore per un'astrazione MetadataEntry.
public MetadataEntry (const std:: String& Key, const std:: String& value, const MetadataVersion& Version)  |  Al costruttore per un'astrazione MetadataEntry.
public MetadataEntry (const std:: String& Key, const std:: String& value)  |  Al costruttore per un'astrazione MetadataEntry, Version è impostato sul valore predefinito 0.
public const std:: String& GetKey () const  |  Ottenere la chiave di immissione dei metadati.
public const std:: String& GetValue () const  |  Ottiene il valore della voce di metadati.
public MetadataVersion GetVersion () const  |  Ottenere la versione di immissione dei metadati.
  
## <a name="members"></a>Membri
  
### <a name="metadataentry-function"></a>MetadataEntry (funzione)
Al costruttore per un'astrazione MetadataEntry.

Parametri  
* **chiave**: voce della chiave dei metadati. 


* **valore**: immissione del valore dei metadati 


* **versione**: valore della versione dei metadati


  
### <a name="metadataentry-function"></a>MetadataEntry (funzione)
Al costruttore per un'astrazione MetadataEntry.

Parametri  
* **chiave**: voce della chiave dei metadati. 


* **valore**: immissione del valore dei metadati 


* **versione**: valore della versione dei metadati


  
### <a name="metadataentry-function"></a>MetadataEntry (funzione)
Al costruttore per un'astrazione MetadataEntry, Version è impostato sul valore predefinito 0.

Parametri  
* **chiave**: voce della chiave dei metadati. 


* **valore**: immissione del valore dei metadati


  
### <a name="getkey-function"></a>GetKey (funzione)
Ottenere la chiave di immissione dei metadati.

  
**Restituisce**: chiave di immissione dei metadati.
  
### <a name="getvalue-function"></a>Funzione GetValue
Ottiene il valore della voce di metadati.

  
**Restituisce**: valore di immissione dei metadati.
  
### <a name="getversion-function"></a>GetVersion (funzione)
Ottenere la versione di immissione dei metadati.

  
**Restituisce**: versione di immissione dei metadati.