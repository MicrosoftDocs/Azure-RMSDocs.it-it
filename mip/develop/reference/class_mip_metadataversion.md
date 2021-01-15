---
title: Classe MetadataVersion
description: 'Documenta la classe metadataversion:: undefined di Microsoft Information Protection (MIP) SDK.'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/13/2021
ms.openlocfilehash: 35ed3ef28cd4a1a822c11f64b422a474edcd4b53
ms.sourcegitcommit: 76926b357bbfc8772ed132ce5f2426fbea59e98b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/14/2021
ms.locfileid: "98213607"
---
# <a name="class-metadataversion"></a>Classe MetadataVersion 
Interfaccia per un MetadataVersion. MetadataVersion determina quali metadati sono attivi e come vengono elaborati.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public MetadataVersion (versione uint32_t, flag MetadataVersionFormat)  |  Costruttore MetadataVersion.
public virtual uint32_t GetValue () const  |  Ottenere la versione numerica.
public virtual bool HasFlag (flag MetadataVersionFormat) const  |  Ottiene un valore che indica se è impostato un flag specifico.
public virtual MetadataVersionFormat GetFlags () const  |  Ottenere i flag che definiscono la modalità di elaborazione dei metadati per una determinata versione.
  
## <a name="members"></a>Membri
  
### <a name="metadataversion-function"></a>MetadataVersion (funzione)
Costruttore MetadataVersion.

Parametri  
* **versione**: versione numerica da usare per le azioni dei metadati 


* **Flags**: Flags per specificare la modalità di utilizzo della versione per il calcolo delle azioni dei metadati


  
### <a name="getvalue-function"></a>Funzione GetValue
Ottenere la versione numerica.

  
**Restituisce**: la versione numerica.
  
### <a name="hasflag-function"></a>HasFlag (funzione)
Ottiene un valore che indica se è impostato un flag specifico.

  
**Restituisce**: true se il flag è impostato.
  
### <a name="getflags-function"></a>Funzione GetFlags
Ottenere i flag che definiscono la modalità di elaborazione dei metadati per una determinata versione.

  
**Restituisce**: i flag che specificano la modalità di elaborazione dei metadati.