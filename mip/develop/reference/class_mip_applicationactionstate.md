---
title: 'Classe MIP:: ApplicationActionState'
description: 'Documenta la classe MIP:: applicationactionstate di Microsoft Information Protection (MIP) SDK.'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 07/16/2019
ms.openlocfilehash: 308918e57cf5495e3da2102ee8caca910c11f670
ms.sourcegitcommit: fcde8b31f8685023f002044d3a1d1903e548d207
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/21/2019
ms.locfileid: "69893617"
---
# <a name="class-mipapplicationactionstate"></a>Classe MIP:: ApplicationActionState 
  
## <a name="summary"></a>Riepilogo
 Members                        | Descrizioni                                
--------------------------------|---------------------------------------------
public LabelState GetNewLabelState () const  |  Ottiene il nuovo stato dell'etichetta.
public std:: shared_ptr\<label\> GetNewLabel () const  |  Ottiene l'ID dell'etichetta di riservatezza da applicare al documento.
public std::p aria\<bool, std:: String\> IsDowngradeJustified () const  |  L'implementazione dovrebbe restituire un valore che indica se è stata fornita una giustificazione per effettuare il downgrade di un'etichetta esistente.
public AssignmentMethod GetNewLabelAssignmentMethod() const  |  Ottiene il metodo di assegnazione della nuova etichetta.
public virtual std:: Vector\<std::p Air\<std:: String, std:: String\> \> GetNewLabelExtendedProperties () const  |  Restituisce le proprietà estese della nuova etichetta.
public ActionType GetSupportedActions() const  |  Ottiene un'enumerazione mascherata che descrive tutti i tipi di azioni supportati.
public bool IsRecommendationEnabled () const  |  Ottenere un valore bool che indica che l'azione consigliata restituirà. per impostazione predefinita deve essere true, a meno che l'utente non specifichi else.
  
## <a name="members"></a>Members
  
### <a name="getnewlabelstate-function"></a>GetNewLabelState (funzione)
Ottiene il nuovo stato dell'etichetta.

  
**Restituisce**: Nuovo stato dell'etichetta. 
  
**Vedere anche**: MIP:: LabelState
  
### <a name="getnewlabel-function"></a>GetNewLabel (funzione)
Ottiene l'ID dell'etichetta di riservatezza da applicare al documento.

  
**Restituisce**: ID dell'etichetta di riservatezza da applicare al contenuto se esistente altrimenti vuoto per rimuovere l'etichetta.
  
### <a name="isdowngradejustified-function"></a>IsDowngradeJustified (funzione)
L'implementazione dovrebbe restituire un valore che indica se è stata fornita una giustificazione per effettuare il downgrade di un'etichetta esistente.

  
**Restituisce**: True se il downgrade è justifiedalong con la giustificazione messageelse false 
  
**Vedere anche**: [mip::JustifyAction](class_mip_justifyaction.md)
  
### <a name="getnewlabelassignmentmethod-function"></a>GetNewLabelAssignmentMethod (funzione)
Ottiene il metodo di assegnazione della nuova etichetta.

  
**Restituisce**: Metodo di assegnazione STANDARD, PRIVILEGed, AUTO. 
  
**Vedere anche**: [MIP:: AssignmentMethod](mip-enums-and-structs.md#assignmentmethod-enum)
  
### <a name="getnewlabelextendedproperties-function"></a>GetNewLabelExtendedProperties (funzione)
Restituisce le proprietà estese della nuova etichetta.

  
**Restituisce**: Proprietà estese applicate al contenuto.
  
### <a name="getsupportedactions-function"></a>GetSupportedActions (funzione)
Ottiene un'enumerazione mascherata che descrive tutti i tipi di azioni supportati.

  
**Restituisce**: Enumerazione mascherata che descrive tutti i tipi di azione supportati.
ActionType::Justify deve essere supportato. Quando una modifica dei criteri e dell'etichetta richiede una giustificazione, verrà restituita sempre un'azione di giustificazione.
  
### <a name="isrecommendationenabled-function"></a>IsRecommendationEnabled (funzione)
Ottenere un valore bool che indica che l'azione consigliata restituirà. per impostazione predefinita deve essere true, a meno che l'utente non specifichi else.

  
**Restituisce**: Un bool che significa che l'azione consigliata restituirà.
ActionType:: RecommendLabel deve essere abilitato affinché questo campo abbia un effetto.