---
title: Classe mip::ContentLabel
description: 'Classe MIP:: contentlabel di Microsoft Information Protection (MIP) SDK vengono documentate.'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: 96f8cca48f385a21685e93eb5bc57abac571975c
ms.sourcegitcommit: ea76aade54134afaf5023145fcb755e40c7b84b7
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/15/2019
ms.locfileid: "59573013"
---
# <a name="class-mipcontentlabel"></a>Classe mip::ContentLabel 
Astrazione per un'etichetta di Microsoft Information Protection applicata a un contenuto, in genere un documento.
Contiene inoltre le proprietà per un'istanza specifica dell'etichetta applicata.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
pubblica std::chrono::time_point\<std\> GetCreationTime() const  |  Ottiene l'ora di creazione dell'etichetta.
public AssignmentMethod GetAssignmentMethod() const  |  Ottiene il metodo di assegnazione dell'etichetta.
Public std:: Vector const\<std:: Pair\<std:: String, std:: String\>\>& GetExtendedProperties() const  |  Ottiene le proprietà estese.
public bool IsProtectionAppliedFromLabel() const  |  Ottiene un valore che indica se è stata applicata o meno la protezione da parte dell'etichetta.
Public std:: shared_ptr\<etichetta\> GetLabel() const  |  Ottiene l'effettivo oggetto etichetta applicato al contenuto.
  
## <a name="members"></a>Membri
  
### <a name="getcreationtime-function"></a>GetCreationTime (funzione)
Ottiene l'ora di creazione dell'etichetta.

  
**Restituisce**: Ora di creazione.
  
### <a name="getassignmentmethod-function"></a>GetAssignmentMethod (funzione)
Ottiene il metodo di assegnazione dell'etichetta.

  
**Restituisce**: AssignmentMethod STANDARD, PRIVILEGED, AUTO. 
  
**Vedere anche**: [assignmentmethod](mip-enums-and-structs.md#assignmentmethod)
  
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