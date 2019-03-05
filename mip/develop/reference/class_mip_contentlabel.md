---
title: Classe mip::ContentLabel
description: 'Classe MIP:: contentlabel di Microsoft Information Protection (MIP) SDK vengono documentate.'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: 34e4395858713219361e4e2ccf8308d89bc5f29d
ms.sourcegitcommit: 471b3683367d93f0673c1cf276a15f83572aa80e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/05/2019
ms.locfileid: "57330492"
---
# <a name="class-mipcontentlabel"></a>Classe mip::ContentLabel 
Astrazione per un'etichetta di Microsoft Information Protection applicata a un contenuto, in genere un documento.
Contiene inoltre le proprietà per un'istanza specifica dell'etichetta applicata.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public const std::string& GetCreationTime() const  |  Ottiene l'ora di creazione dell'etichetta.
public AssignmentMethod GetAssignmentMethod() const  |  Ottiene il metodo di assegnazione dell'etichetta.
Public std:: Vector const\<std:: Pair\<std:: String, std:: String\>\>& GetExtendedProperties() const  |  Ottiene le proprietà estese.
public bool IsProtectionAppliedFromLabel() const  |  Ottiene un valore che indica se è stata applicata o meno la protezione da parte dell'etichetta.
Public std:: shared_ptr\<etichetta\> GetLabel() const  |  Ottiene l'effettivo oggetto etichetta applicato al contenuto.
  
## <a name="members"></a>Membri
  
### <a name="getcreationtime-function"></a>GetCreationTime (funzione)
Ottiene l'ora di creazione dell'etichetta.

  
**Restituisce**: Ora di creazione sotto forma di stringa GMT.
  
### <a name="getassignmentmethod-function"></a>GetAssignmentMethod (funzione)
Ottiene il metodo di assegnazione dell'etichetta.

  
**Restituisce**: AssignmentMethod STANDARD, PRIVILEGED, AUTO. 
  
**Vedere anche**: [assignmentmethod](mip-enums-and-structs.md#assignmentmethod-enum)
  
### <a name="getextendedproperties-function"></a>GetExtendedProperties (funzione)
Ottiene le proprietà estese.

  
**Restituisce**: Proprietà estese.
  
### <a name="isprotectionappliedfromlabel-function"></a>IsProtectionAppliedFromLabel (funzione)
Ottiene un valore che indica se è stata applicata o meno la protezione da parte dell'etichetta.

  
**Restituisce**: True se è presente della protezione dei modelli ed era da questa etichetta, altrimenti false.
  
### <a name="getlabel-function"></a>GetLabel (funzione)
Ottiene l'effettivo oggetto etichetta applicato al contenuto.

  
**Restituisce**: Oggetto etichetta applicato al contenuto. 
  
**Vedere anche**: [mip::Label](class_mip_label.md)
