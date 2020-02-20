---
title: 'Classe MIP:: ApplicationActionState'
description: 'Documenta la classe MIP:: applicationactionstate di Microsoft Information Protection (MIP) SDK.'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 02/14/2020
ms.openlocfilehash: 70128f67f758145be2b03954d3385a8428d63fe9
ms.sourcegitcommit: 2d3c638fb576f3f074330a33d077db0cf0e7d4e7
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/20/2020
ms.locfileid: "77490643"
---
# <a name="class-mipapplicationactionstate"></a>Classe MIP:: ApplicationActionState 
  
## <a name="summary"></a>Riepilogo
 Members                        | Descrizioni                                
--------------------------------|---------------------------------------------
public LabelState GetNewLabelState () const  |  Ottiene il nuovo stato dell'etichetta.
public std:: shared_ptr\<label\> GetNewLabel () const  |  Ottiene l'ID dell'etichetta di riservatezza da applicare al documento.
public std::p Air\<bool, std:: String\> IsDowngradeJustified () const  |  L'implementazione dovrebbe restituire un valore che indica se è stata fornita una giustificazione per effettuare il downgrade di un'etichetta esistente.
public AssignmentMethod GetNewLabelAssignmentMethod() const  |  Ottiene il metodo di assegnazione della nuova etichetta.
public virtual std:: Vector\<std::p Air\<std:: String, std:: String\>\> GetNewLabelExtendedProperties () const  |  Restituisce le proprietà estese della nuova etichetta.
public ActionType GetSupportedActions() const  |  Ottiene un'enumerazione mascherata che descrive tutti i tipi di azioni supportati.
public bool IsRecommendationEnabled () const  |  Ottenere un valore bool che indica che l'azione consigliata restituirà. per impostazione predefinita deve essere true, a meno che l'utente non specifichi else.
  
## <a name="members"></a>Members
  
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
  
**Vedere anche**: [MIP:: AssignmentMethod](mip-enums-and-structs.md#assignmentmethod-enum)
  
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