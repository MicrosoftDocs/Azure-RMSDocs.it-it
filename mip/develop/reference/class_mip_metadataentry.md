---
title: Classe MetadataEntry
description: 'Documenta la classe metadataentry:: undefined di Microsoft Information Protection (MIP) SDK.'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 09/21/2020
ms.openlocfilehash: 026fecc8da2008a2798ca8bc44951bc97ec5455a
ms.sourcegitcommit: 3f5f9f7695b9ed3c45e9230cd8b8cb39a1c5a5ed
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/23/2020
ms.locfileid: "95566786"
---
# <a name="class-metadataentry"></a>Classe MetadataEntry 
Classe di astrazione per la voce di metadati.
  
## <a name="summary"></a>Riepilogo
 Members                        | Descrizioni                                
--------------------------------|---------------------------------------------
public MetadataEntry (const std:: String& Key, const std:: String& value, uint32_t Version)  |  Al costruttore per un'astrazione MetadataEntry.
public MetadataEntry (const std:: String& Key, const std:: String& value, const MetadataVersion& Version)  |  Al costruttore per un'astrazione MetadataEntry.
public MetadataEntry (const std:: String& Key, const std:: String& value)  |  Al costruttore per un'astrazione MetadataEntry, Version è impostato sul valore predefinito 0.
public const std:: String& GetKey () const  |  Ottenere la chiave di immissione dei metadati.
public const std:: String& GetValue () const  |  Ottiene il valore della voce di metadati.
public MetadataVersion GetVersion () const  |  Ottenere la versione di immissione dei metadati.
  
## <a name="members"></a>Members
  
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