---
title: Classe mip::Label
description: 'Classe MIP:: Label di Microsoft Information Protection (MIP) SDK vengono documentate.'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: 5a2444ab0abd944418a8d55eae35c5f6023282f7
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/14/2019
ms.locfileid: "56253234"
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
pubblica std::weak_ptr\<etichetta\> GetParent const  |  Ottiene l'etichetta padre.
public const std::vector\<std::shared_ptr\<Label\>\>& GetChildren() const  |  Ottiene le etichette figlio dell'etichetta corrente.
Public std:: Vector const\<std:: Pair\<std:: String, std:: String\>\>& GetCustomSettings() const  |  Ottiene le impostazioni di un'etichetta personalizzate.
  
## <a name="members"></a>Membri
  
### <a name="getid-function"></a>GetId (funzione)
Ottiene l'ID dell'etichetta.

  
**Restituisce**: L'ID etichetta.
  
### <a name="getname-function"></a>GetName (funzione)
Ottiene il nome dell'etichetta.

  
**Restituisce**: Il nome dell'etichetta.
  
### <a name="getdescription-function"></a>GetDescription (funzione)
Ottiene la descrizione dell'etichetta.

  
**Restituisce**: La descrizione dell'etichetta.
  
### <a name="getcolor-function"></a>GetColor (funzione)
Ottiene il colore in cui deve essere visualizzata l'etichetta.

  
**Restituisce**: Valore di colore, il formato della stringa. "#RRGGBB", dove RR, GG, BB sono valori esadecimali di due cifre compresi nell'intervallo 0-F.
  
### <a name="getsensitivity-function"></a>GetSensitivity (funzione)
Ottiene la riservatezza dell'etichetta.

  
**Restituisce**: Un valore numerico. A un valore più alto corrisponde una riservatezza più elevata.
  
### <a name="gettooltip-function"></a>GetTooltip (funzione)
Ottiene la descrizione comando dell'etichetta.

  
**Restituisce**: Una stringa di descrizione comando.
  
### <a name="isactive-function"></a>IsActive (funzione)
Ottiene un valore booleano che indica se l'etichetta è attiva.
Possono essere applicate solo le etichette attive. Le etichette inattive non possono essere applicate e sono usate solo a scopo di visualizzazione. 

  
**Restituisce**: True se l'etichetta è attiva, in caso contrario, false.
  
### <a name="getparent-function"></a>GetParent (funzione)
Ottiene l'etichetta padre.

  
**Restituisce**: Puntatore debole all'elemento padre di assegnare un'etichetta se esistente in caso contrario un puntatore vuoto.
  
### <a name="getchildren-function"></a>GetChildren (funzione)
Ottiene le etichette figlio dell'etichetta corrente.

  
**Restituisce**: Vettore di puntatori condivisi a etichette.
  
### <a name="getcustomsettings-function"></a>GetCustomSettings (funzione)
Ottiene le impostazioni di un'etichetta personalizzate.

  
**Restituisce**: Vettore di coppie chiave-valore che rappresenta le impostazioni personalizzate.
