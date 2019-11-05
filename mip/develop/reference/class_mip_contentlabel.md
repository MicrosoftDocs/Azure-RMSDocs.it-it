---
title: Classe mip::ContentLabel
description: 'Documenta la classe MIP:: contentlabel di Microsoft Information Protection (MIP) SDK.'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 10/29/2019
ms.openlocfilehash: a29ea5be05d928f25b9a4255416d93acedcb1c0b
ms.sourcegitcommit: f5d8cf4440a35afaa1ff1a58b2a022740ed85ffd
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/04/2019
ms.locfileid: "73558923"
---
# <a name="class-mipcontentlabel"></a>Classe mip::ContentLabel 
Astrazione per un'etichetta di Microsoft Information Protection applicata a un contenuto, in genere un documento.
Contiene inoltre le proprietà per un'istanza specifica dell'etichetta applicata.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public std:: Chrono:: time_point\<std:: Chrono:: system_clock\> GetCreationTime () const  |  Ottiene l'ora di creazione dell'etichetta.
public AssignmentMethod GetAssignmentMethod() const  |  Ottiene il metodo di assegnazione dell'etichetta.
public const std:: Vector\<std::p Air\<std:: String, std:: String\>\>& getextendedpropertys () const  |  Ottiene le proprietà estese.
public bool IsProtectionAppliedFromLabel() const  |  Ottiene un valore che indica se è stata applicata o meno la protezione da parte dell'etichetta.
public std:: shared_ptr\<label\> GetLabel () const  |  Ottiene l'effettivo oggetto etichetta applicato al contenuto.
  
## <a name="members"></a>Membri
  
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