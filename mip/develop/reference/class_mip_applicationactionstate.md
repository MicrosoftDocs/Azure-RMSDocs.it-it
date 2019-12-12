---
title: 'Classe MIP:: ApplicationActionState'
description: 'Documenta la classe MIP:: applicationactionstate di Microsoft Information Protection (MIP) SDK.'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 10/29/2019
ms.openlocfilehash: a3a5bde734c62859d2f2a03967a61d9ec14a2056
ms.sourcegitcommit: 474cd033de025bab280cb7a9721ac7ffc2d60b55
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/05/2019
ms.locfileid: "73559439"
---
# <a name="class-mipapplicationactionstate"></a>Classe MIP:: ApplicationActionState 
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public LabelState GetNewLabelState () const  |  Ottiene il nuovo stato dell'etichetta.
public std:: shared_ptr\<label\> GetNewLabel () const  |  Ottiene l'ID dell'etichetta di riservatezza da applicare al documento.
public std::p Air\<bool, std:: String\> IsDowngradeJustified () const  |  L'implementazione dovrebbe restituire un valore che indica se è stata fornita una giustificazione per effettuare il downgrade di un'etichetta esistente.
public AssignmentMethod GetNewLabelAssignmentMethod() const  |  Ottiene il metodo di assegnazione della nuova etichetta.
public virtual std:: Vector\<std::p Air\<std:: String, std:: String\>\> GetNewLabelExtendedProperties () const  |  Restituisce le proprietà estese della nuova etichetta.
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