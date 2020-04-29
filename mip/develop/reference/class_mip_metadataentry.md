---
title: Classe MetadataEntry
description: 'Documenta la classe metadataentry:: undefined di Microsoft Information Protection (MIP) SDK.'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 04/16/2020
ms.openlocfilehash: c9c1c8f9683ebb4be079f1817aa92a71e72005ca
ms.sourcegitcommit: f54920bf017902616589aca30baf6b64216b6913
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/22/2020
ms.locfileid: "81766508"
---
# <a name="class-metadataentry"></a>Classe MetadataEntry 
Classe di astrazione per la voce di metadati.
  
## <a name="summary"></a>Riepilogo
 Members                        | Descrizioni                                
--------------------------------|---------------------------------------------
public MetadataEntry (const std:: String& Key, const std:: String& value, unsigned int version)  |  Al costruttore per un'astrazione MetadataEntry.
public MetadataEntry (const std:: String& Key, const std:: String& value)  |  Al costruttore per un'astrazione MetadataEntry, Version è impostato sul valore predefinito 0.
public const std:: String& GetKey () const  |  Ottenere la chiave di immissione dei metadati.
public const std:: String& GetValue () const  |  Ottiene il valore della voce di metadati.
public unsigned int GetVersion () const  |  Ottenere la versione di immissione dei metadati.
  
## <a name="members"></a>Members
  
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