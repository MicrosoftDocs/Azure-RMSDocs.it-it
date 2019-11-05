---
title: Classe mip::Label
description: "Documenta la classe MIP:: label dell'SDK Microsoft Information Protection (MIP)."
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 10/29/2019
ms.openlocfilehash: 5bdc88746a8921f306d9d52dbe75f3c2b826a5b6
ms.sourcegitcommit: f5d8cf4440a35afaa1ff1a58b2a022740ed85ffd
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/04/2019
ms.locfileid: "73560146"
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
public const std:: String & GetAutoTooltip () const  |  Ottenere la descrizione della descrizione comando della classificazione che determina l'applicazione di questa etichetta.
public bool IsActive() const  |  Ottiene un valore booleano che indica se l'etichetta è attiva.
public std:: weak_ptr\<label\> GetParent () const  |  Ottiene l'etichetta padre.
public const std:: Vector\<std:: shared_ptr\<label\>\>& GetChildren () const  |  Ottiene le etichette figlio dell'etichetta corrente.
public const std:: Vector\<std::p Air\<std:: String, std:: String\>\>& GetCustomSettings () const  |  Ottiene le impostazioni personalizzate di un'etichetta.
public ActionSource GetActionSource() const  |  Ottiene l'origine dell'azione dell'etichetta.
  
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

  
**Restituisce**un vettore di coppie chiave-valore che rappresenta le impostazioni personalizzate.
  
### <a name="getactionsource-function"></a>GetActionSource (funzione)
Ottiene l'origine dell'azione dell'etichetta.

  
**Restituisce**: origine azione