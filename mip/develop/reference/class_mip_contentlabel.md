---
title: Classe mip::ContentLabel
description: 'Documenta la classe MIP:: contentlabel di Microsoft Information Protection (MIP) SDK.'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 02/14/2020
ms.openlocfilehash: f131885572ab5ad3a2664a6b50162a011529bfbb
ms.sourcegitcommit: 2d3c638fb576f3f074330a33d077db0cf0e7d4e7
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/20/2020
ms.locfileid: "77490337"
---
# <a name="class-mipcontentlabel"></a>Classe mip::ContentLabel 
Astrazione per un'etichetta di Microsoft Information Protection applicata a un contenuto, in genere un documento.
Contiene inoltre le proprietà per un'istanza specifica dell'etichetta applicata.
  
## <a name="summary"></a>Riepilogo
 Members                        | Descrizioni                                
--------------------------------|---------------------------------------------
public std:: Chrono:: time_point\<std:: Chrono:: system_clock\> GetCreationTime () const  |  Ottiene l'ora di creazione dell'etichetta.
public AssignmentMethod GetAssignmentMethod() const  |  Ottiene il metodo di assegnazione dell'etichetta.
public const std:: Vector\<std::p Air\<std:: String, std:: String\>\>& getextendedpropertys () const  |  Ottiene le proprietà estese.
public bool IsProtectionAppliedFromLabel() const  |  Ottiene un valore che indica se è stata applicata o meno la protezione da parte dell'etichetta.
public std:: shared_ptr\<label\> GetLabel () const  |  Ottiene l'effettivo oggetto etichetta applicato al contenuto.
  
## <a name="members"></a>Members
  
### <a name="getcreationtime-function"></a>GetCreationTime (funzione)
Ottiene l'ora di creazione dell'etichetta.

  
**Restituisce**: ora creazione.
  
### <a name="getassignmentmethod-function"></a>GetAssignmentMethod (funzione)
Ottiene il metodo di assegnazione dell'etichetta.

  
**Restituisce**: AssignmentMethod STANDARD | PRIVILEGED | AUTO. 
  
**Vedere anche**: [MIP:: AssignmentMethod](mip-enums-and-structs.md#assignmentmethod-enum)
  
### <a name="getextendedproperties-function"></a>Funzione getextendedproperties
Ottiene le proprietà estese.

  
**Restituisce**: proprietà estese.
  
### <a name="isprotectionappliedfromlabel-function"></a>IsProtectionAppliedFromLabel (funzione)
Ottiene un valore che indica se è stata applicata o meno la protezione da parte dell'etichetta.

  
**Restituisce**: true se è disponibile la protezione dei modelli tramite questa etichetta, in caso contrario false.
  
### <a name="getlabel-function"></a>Funzione GetLabel
Ottiene l'effettivo oggetto etichetta applicato al contenuto.

  
**Restituisce**: oggetto etichetta applicato al contenuto. 
  
**Vedere anche**: MIP:: Label