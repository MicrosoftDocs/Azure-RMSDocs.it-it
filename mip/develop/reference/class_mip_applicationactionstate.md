---
title: Classe ApplicationActionState
description: 'Documenta la classe applicationactionstate:: undefined di Microsoft Information Protection (MIP) SDK.'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/13/2021
ms.openlocfilehash: ef62674d4586b967a822ccfb25612a491d157bf4
ms.sourcegitcommit: 76926b357bbfc8772ed132ce5f2426fbea59e98b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/14/2021
ms.locfileid: "98212281"
---
# <a name="class-applicationactionstate"></a>Classe ApplicationActionState 
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public LabelState GetNewLabelState () const  |  Ottiene il nuovo stato dell'etichetta.
public std:: shared_ptr \<Label\> GetNewLabel () const  |  Ottiene l'ID dell'etichetta di riservatezza da applicare al documento.
STD pubblico::p aria \<bool, std::string\> IsDowngradeJustified () const  |  L'implementazione dovrebbe restituire un valore che indica se è stata fornita una giustificazione per effettuare il downgrade di un'etichetta esistente.
public AssignmentMethod GetNewLabelAssignmentMethod() const  |  Ottiene il metodo di assegnazione della nuova etichetta.
public virtual std:: Vector \<std::pair\<std::string, std::string\> \> GetNewLabelExtendedProperties () const  |  Restituisce le proprietà estese della nuova etichetta.
public ActionType GetSupportedActions() const  |  Ottiene un'enumerazione mascherata che descrive tutti i tipi di azioni supportati.
public bool IsRecommendationEnabled () const  |  Ottenere un valore bool che indica che l'azione consigliata restituirà. per impostazione predefinita deve essere true, a meno che l'utente non specifichi else.
  
## <a name="members"></a>Membri
  
### <a name="getnewlabelstate-function"></a>GetNewLabelState (funzione)
Ottiene il nuovo stato dell'etichetta.

  
**Returns**: nuovo stato dell'etichetta. 
  
**Vedere anche**: MIP:: LabelState
  
### <a name="getnewlabel-function"></a>GetNewLabel (funzione)
Ottiene l'ID dell'etichetta di riservatezza da applicare al documento.

  
**Restituisce**: ID dell'etichetta di riservatezza da applicare al contenuto se esistente, in caso contrario una stringa vuota per rimuovere l'etichetta.
  
### <a name="isdowngradejustified-function"></a>IsDowngradeJustified (funzione)
L'implementazione dovrebbe restituire un valore che indica se è stata fornita una giustificazione per effettuare il downgrade di un'etichetta esistente.

  
**Restituisce**: true se è stata fornita una giustificazione per il downgrade insieme al messaggio di giustificazione, in caso contrario false 
  
**Vedere anche**: MIP:: JustifyAction
  
### <a name="getnewlabelassignmentmethod-function"></a>GetNewLabelAssignmentMethod (funzione)
Ottiene il metodo di assegnazione della nuova etichetta.

  
**Restituisce**: metodo di assegnazione STANDARD, PRIVILEGED, AUTO. 
  
**Vedere anche**: mip::AssignmentMethod
  
### <a name="getnewlabelextendedproperties-function"></a>GetNewLabelExtendedProperties (funzione)
Restituisce le proprietà estese della nuova etichetta.

  
**Restituisce**: proprietà estese applicate al contenuto.
  
### <a name="getsupportedactions-function"></a>GetSupportedActions (funzione)
Ottiene un'enumerazione mascherata che descrive tutti i tipi di azioni supportati.

  
**Restituisce**: enumerazione mascherata che descrive tutti i tipi di azioni supportati.
ActionType::Justify deve essere supportato. Quando una modifica dei criteri e dell'etichetta richiede una giustificazione, verrà restituita sempre un'azione di giustificazione.
  
### <a name="isrecommendationenabled-function"></a>IsRecommendationEnabled (funzione)
Ottenere un valore bool che indica che l'azione consigliata restituirà. per impostazione predefinita deve essere true, a meno che l'utente non specifichi else.

  
**Restituisce**: un bool che significa che l'azione consigliata restituirà.
ActionType:: RecommendLabel deve essere abilitato affinché questo campo abbia un effetto.