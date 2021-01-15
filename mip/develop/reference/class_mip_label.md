---
title: Etichetta classe
description: 'Documents the label:: undefined Class of the Microsoft Information Protection (MIP) SDK.'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/13/2021
ms.openlocfilehash: 726c61d1b73389bfdc10afb961177659e5a137d4
ms.sourcegitcommit: 76926b357bbfc8772ed132ce5f2426fbea59e98b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/14/2021
ms.locfileid: "98213896"
---
# <a name="class-label"></a>Etichetta classe 
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
public const std:: String& GetAutoTooltip () const  |  Ottenere la descrizione della descrizione comando della classificazione che determina l'applicazione di questa etichetta.
public bool IsActive() const  |  Ottiene un valore booleano che indica se l'etichetta è attiva.
public std::weak_ptr\<Label\> GetParent() const  |  Ottiene l'etichetta padre.
public const std:: Vector \<std::shared_ptr\<Label\> \>& GetChildren () const  |  Ottiene le etichette figlio dell'etichetta corrente.
public const std:: Vector \<std::pair\<std::string, std::string\> \>& GetCustomSettings () const  |  Ottiene le impostazioni personalizzate di un'etichetta.
public ActionSource GetActionSource() const  |  Ottiene l'origine dell'azione dell'etichetta.
public const std:: Vector \<std::string\>& GetContentFormats () const  |  Ottiene i tipi di contenuto.
  
## <a name="members"></a>Membri
  
### <a name="getid-function"></a>GetId (funzione)
Ottiene l'ID dell'etichetta.

  
**Restituisce**: ID dell'etichetta.
  
### <a name="getname-function"></a>GetName (funzione)
Ottiene il nome dell'etichetta.

  
**Restituisce**: nome dell'etichetta.
  
### <a name="getdescription-function"></a>Funzione GetDescription
Ottiene la descrizione dell'etichetta.

  
**Restituisce**: descrizione dell'etichetta.
  
### <a name="getcolor-function"></a>Funzione GetColor
Ottiene il colore in cui deve essere visualizzata l'etichetta.

  
**Restituisce**: valore del colore in formato stringa. "#RRGGBB", dove RR, GG, BB sono valori esadecimali di due cifre compresi nell'intervallo 0-F.
  
### <a name="getsensitivity-function"></a>Funzione getsensitivity
Ottiene la riservatezza dell'etichetta.

  
**Restituisce**: valore numerico. A un valore più alto corrisponde una riservatezza più elevata.
  
### <a name="gettooltip-function"></a>Funzione GetToolTip
Ottiene la descrizione comando dell'etichetta.

  
**Restituisce**: stringa di descrizione comando.
  
### <a name="getautotooltip-function"></a>GetAutoTooltip (funzione)
Ottenere la descrizione della descrizione comando della classificazione che determina l'applicazione di questa etichetta.

  
**Restituisce**: stringa di descrizione comando.
  
### <a name="isactive-function"></a>Funzione Active
Ottiene un valore booleano che indica se l'etichetta è attiva.
Possono essere applicate solo le etichette attive. Le etichette inattive non possono essere applicate e sono usate solo a scopo di visualizzazione. 

  
**Restituisce**: true se l'etichetta è attiva, in caso contrario false.
  
### <a name="getparent-function"></a>Funzione GetParent
Ottiene l'etichetta padre.

  
**Restituisce**: puntatore debole all'etichetta padre se esistente, in caso contrario un puntatore vuoto.
  
### <a name="getchildren-function"></a>GetChildren (funzione)
Ottiene le etichette figlio dell'etichetta corrente.

  
**Restituisce**: vettore di puntatori condivisi a etichette.
  
### <a name="getcustomsettings-function"></a>GetCustomSettings (funzione)
Ottiene le impostazioni personalizzate di un'etichetta.

  
**Restituisce** un vettore di coppie chiave-valore che rappresenta le impostazioni personalizzate.
  
### <a name="getactionsource-function"></a>GetActionSource (funzione)
Ottiene l'origine dell'azione dell'etichetta.

  
**Restituisce**: origine azione
  
### <a name="getcontentformats-function"></a>GetContentFormats (funzione)
Ottiene i tipi di contenuto.

  
<Returns>