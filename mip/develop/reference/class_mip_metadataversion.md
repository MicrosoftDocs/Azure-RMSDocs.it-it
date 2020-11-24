---
title: Classe MetadataVersion
description: 'Documenta la classe metadataversion:: undefined di Microsoft Information Protection (MIP) SDK.'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 09/21/2020
ms.openlocfilehash: 05154ec7777fb94478c2065f6e637dea47d58d28
ms.sourcegitcommit: 3f5f9f7695b9ed3c45e9230cd8b8cb39a1c5a5ed
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/23/2020
ms.locfileid: "95566768"
---
# <a name="class-metadataversion"></a>Classe MetadataVersion 
Interfaccia per un MetadataVersion. MetadataVersion determina quali metadati sono attivi e come vengono elaborati.
  
## <a name="summary"></a>Riepilogo
 Members                        | Descrizioni                                
--------------------------------|---------------------------------------------
public MetadataVersion (versione uint32_t, flag MetadataVersionFormat)  |  Costruttore MetadataVersion.
public virtual uint32_t GetValue () const  |  Ottenere la versione numerica.
public virtual bool HasFlag (flag MetadataVersionFormat) const  |  Ottiene un valore che indica se è impostato un flag specifico.
public virtual MetadataVersionFormat GetFlags () const  |  Ottenere i flag che definiscono la modalità di elaborazione dei metadati per una determinata versione.
  
## <a name="members"></a>Members
  
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