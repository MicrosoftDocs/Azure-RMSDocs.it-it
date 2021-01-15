---
title: Classe ContentLabel
description: 'Documenta la classe contentlabel:: undefined di Microsoft Information Protection (MIP) SDK.'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/13/2021
ms.openlocfilehash: 9263f9ecd926cafe4aedd578804912aed9faa128
ms.sourcegitcommit: 76926b357bbfc8772ed132ce5f2426fbea59e98b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/14/2021
ms.locfileid: "98211686"
---
# <a name="class-contentlabel"></a>Classe ContentLabel 
Astrazione per un'etichetta di Microsoft Information Protection applicata a un contenuto, in genere un documento.
Contiene inoltre le proprietà per un'istanza specifica dell'etichetta applicata.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public std:: Chrono:: time_point \<std::chrono::system_clock\> GetCreationTime () const  |  Ottiene l'ora di creazione dell'etichetta.
public AssignmentMethod GetAssignmentMethod() const  |  Ottiene il metodo di assegnazione dell'etichetta.
public const std:: Vector \<MetadataEntry\>& Getextendedpropertys () const  |  Ottiene le proprietà estese.
public bool IsProtectionAppliedFromLabel() const  |  Ottiene un valore che indica se è stata applicata o meno la protezione da parte dell'etichetta.
public std::shared_ptr\<Label\> GetLabel() const  |  Ottiene l'effettivo oggetto etichetta applicato al contenuto.
  
## <a name="members"></a>Membri
  
### <a name="getcreationtime-function"></a>GetCreationTime (funzione)
Ottiene l'ora di creazione dell'etichetta.

  
**Restituisce**: ora creazione.
  
### <a name="getassignmentmethod-function"></a>GetAssignmentMethod (funzione)
Ottiene il metodo di assegnazione dell'etichetta.

  
**Restituisce**: AssignmentMethod STANDARD | PRIVILEGED | AUTO. 
  
**Vedere anche**: mip::AssignmentMethod
  
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