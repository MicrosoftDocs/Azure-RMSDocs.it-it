---
title: Classe mip::ContentLabel
description: 'Documenta la classe MIP:: contentlabel di Microsoft Information Protection (MIP) SDK.'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 07/16/2019
ms.openlocfilehash: 27f8adba3e65647a3804256e0b429e1457003085
ms.sourcegitcommit: fcde8b31f8685023f002044d3a1d1903e548d207
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/21/2019
ms.locfileid: "69884406"
---
# <a name="class-mipcontentlabel"></a>Classe mip::ContentLabel 
Astrazione per un'etichetta di Microsoft Information Protection applicata a un contenuto, in genere un documento.
Contiene inoltre le proprietà per un'istanza specifica dell'etichetta applicata.
  
## <a name="summary"></a>Riepilogo
 Members                        | Descrizioni                                
--------------------------------|---------------------------------------------
public std:: Chrono:: time_point\<std:: Chrono:: system_clock\> GetCreationTime () const  |  Ottiene l'ora di creazione dell'etichetta.
public AssignmentMethod GetAssignmentMethod() const  |  Ottiene il metodo di assegnazione dell'etichetta.
public const std::\<vector std::p\<aria std:: String, std::\>String\>& getextendedproperties () const  |  Ottiene le proprietà estese.
public bool IsProtectionAppliedFromLabel() const  |  Ottiene un valore che indica se è stata applicata o meno la protezione da parte dell'etichetta.
public std:: shared_ptr\<label\> GetLabel () const  |  Ottiene l'effettivo oggetto etichetta applicato al contenuto.
  
## <a name="members"></a>Members
  
### <a name="getcreationtime-function"></a>GetCreationTime (funzione)
Ottiene l'ora di creazione dell'etichetta.

  
**Restituisce**: Ora di creazione.
  
### <a name="getassignmentmethod-function"></a>GetAssignmentMethod (funzione)
Ottiene il metodo di assegnazione dell'etichetta.

  
**Restituisce**: AssignmentMethod STANDARD, PRIVILEGED, AUTO. 
  
**Vedere anche**: [MIP:: AssignmentMethod](mip-enums-and-structs.md#assignmentmethod-enum)
  
### <a name="getextendedproperties-function"></a>Funzione getextendedproperties
Ottiene le proprietà estese.

  
**Restituisce**: Proprietà estese.
  
### <a name="isprotectionappliedfromlabel-function"></a>IsProtectionAppliedFromLabel (funzione)
Ottiene un valore che indica se è stata applicata o meno la protezione da parte dell'etichetta.

  
**Restituisce**: True se è presente la protezione modello ed è stata da questa etichetta; in caso contrario, false.
  
### <a name="getlabel-function"></a>Funzione GetLabel
Ottiene l'effettivo oggetto etichetta applicato al contenuto.

  
**Restituisce**: Oggetto Label applicato al contenuto. 
  
**Vedere anche**: [mip::Label](class_mip_label.md)