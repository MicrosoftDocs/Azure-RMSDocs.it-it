---
title: Classe ContentLabel
description: 'Documenta la classe contentlabel:: undefined di Microsoft Information Protection (MIP) SDK.'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 09/21/2020
ms.openlocfilehash: a60244b9db9b3087dde71cbdbcf63ba170cb06c3
ms.sourcegitcommit: 3f5f9f7695b9ed3c45e9230cd8b8cb39a1c5a5ed
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/23/2020
ms.locfileid: "95567195"
---
# <a name="class-contentlabel"></a>Classe ContentLabel 
Astrazione per un'etichetta di Microsoft Information Protection applicata a un contenuto, in genere un documento.
Contiene inoltre le proprietà per un'istanza specifica dell'etichetta applicata.
  
## <a name="summary"></a>Riepilogo
 Members                        | Descrizioni                                
--------------------------------|---------------------------------------------
public std:: Chrono:: time_point \<std::chrono::system_clock\> GetCreationTime () const  |  Ottiene l'ora di creazione dell'etichetta.
public AssignmentMethod GetAssignmentMethod() const  |  Ottiene il metodo di assegnazione dell'etichetta.
public const std:: Vector \<MetadataEntry\>& Getextendedpropertys () const  |  Ottiene le proprietà estese.
public bool IsProtectionAppliedFromLabel() const  |  Ottiene un valore che indica se è stata applicata o meno la protezione da parte dell'etichetta.
public std::shared_ptr\<Label\> GetLabel() const  |  Ottiene l'effettivo oggetto etichetta applicato al contenuto.
  
## <a name="members"></a>Members
  
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