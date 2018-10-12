---
title: Classe mip Label
description: Riferimento per la classe mip Label
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: 2a80748430df83a16a4d5ee716344d17ce7deee4
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/28/2018
ms.locfileid: "47446278"
---
# <a name="class-miplabel"></a>Classe mip::Label 
Astrazione per una singola etichetta di Microsoft Information Protection.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
 public const std::string& GetId() const  |  Ottiene l'ID dell'etichetta.
 public const std::string& GetName() const  |  Ottiene il nome dell'etichetta.
 public const std::string& GetDescription() const  |  Ottiene la descrizione dell'etichetta.
 public const std::string& GetColor() const  |  Ottiene il colore in cui deve essere visualizzata l'etichetta.
 public int GetSensitivity() const  |  Ottiene la riservatezza dell'etichetta.
 public const std::string& GetTooltip() const  |  Ottiene la descrizione comando dell'etichetta.
 public bool IsActive() const  |  Ottiene un valore booleano che indica se l'etichetta è attiva.
public std::weak_ptr<Label> GetParent() const  |  Ottiene l'etichetta padre.
public const std::vector<std::shared_ptr<Label>>& GetChildren() const  |  Ottiene le etichette figlio dell'etichetta corrente.
  
## <a name="members"></a>Membri
  
### <a name="getid"></a>GetId
Ottiene l'ID dell'etichetta.

  
**Restituisce**: ID dell'etichetta.
  
### <a name="getname"></a>GetName
Ottiene il nome dell'etichetta.

  
**Restituisce**: nome dell'etichetta.
  
### <a name="getdescription"></a>GetDescription
Ottiene la descrizione dell'etichetta.

  
**Restituisce**: descrizione dell'etichetta.
  
### <a name="getcolor"></a>GetColor
Ottiene il colore in cui deve essere visualizzata l'etichetta.

  
**Restituisce**: valore del colore in formato stringa. "#RRGGBB", dove RR, GG, BB sono valori esadecimali di due cifre compresi nell'intervallo 0-F.
  
### <a name="getsensitivity"></a>GetSensitivity
Ottiene la riservatezza dell'etichetta.

  
**Restituisce**: valore numerico. A un valore più alto corrisponde una riservatezza più elevata.
  
### <a name="gettooltip"></a>GetTooltip
Ottiene la descrizione comando dell'etichetta.

  
**Restituisce**: stringa di descrizione comando.
  
### <a name="isactive"></a>IsActive
Ottiene un valore booleano che indica se l'etichetta è attiva.
Possono essere applicate solo le etichette attive. Le etichette inattive non possono essere applicate e sono usate solo a scopo di visualizzazione. 

  
**Restituisce**: true se l'etichetta è attiva, in caso contrario false.
  
### <a name="label"></a>Label
Ottiene l'etichetta padre.

  
**Restituisce**: puntatore debole all'etichetta padre se esistente, in caso contrario un puntatore vuoto.
  
### <a name="label"></a>Label
Ottiene le etichette figlio dell'etichetta corrente.

  
**Restituisce**: vettore di puntatori condivisi a etichette.