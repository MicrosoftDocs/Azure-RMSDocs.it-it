---
title: Classe mip ContentLabel
description: Riferimento per la classe mip ContentLabel
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: c105f620ed2cd3d6f1427f2543784ea66ce2c4d7
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/28/2018
ms.locfileid: "47446023"
---
# <a name="class-mipcontentlabel"></a>Classe mip::ContentLabel 
Astrazione per un'etichetta di Microsoft Information Protection applicata a un contenuto, in genere un documento.
Contiene inoltre le proprietà per un'istanza specifica dell'etichetta applicata.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
 public const std::string& GetCreationTime() const  |  Ottiene l'ora di creazione dell'etichetta.
 public AssignmentMethod GetAssignmentMethod() const  |  Ottiene il metodo di assegnazione dell'etichetta.
public const std::vector<std::pair<std::string, std::string>>& GetExtendedProperties() const  |  Ottiene le proprietà estese.
 public bool IsProtectionAppliedFromLabel() const  |  Ottiene un valore che indica se è stata applicata o meno la protezione da parte dell'etichetta.
public std::shared_ptr<Label> GetLabel() const  |  Ottiene l'effettivo oggetto etichetta applicato al contenuto.
  
## <a name="members"></a>Membri
  
### <a name="getcreationtime"></a>GetCreationTime
Ottiene l'ora di creazione dell'etichetta.

  
**Restituisce**: ora di creazione sotto forma di stringa GMT.
  
### <a name="getassignmentmethod"></a>GetAssignmentMethod
Ottiene il metodo di assegnazione dell'etichetta.

  
**Restituisce**: AssignmentMethod STANDARD | PRIVILEGED | AUTO. 
  
**Vedere anche**: mip::AssignmentMethod
  
### <a name="getextendedproperties"></a>GetExtendedProperties
Ottiene le proprietà estese.

  
**Restituisce**: proprietà estese.
  
### <a name="isprotectionappliedfromlabel"></a>IsProtectionAppliedFromLabel
Ottiene un valore che indica se è stata applicata o meno la protezione da parte dell'etichetta.

  
**Restituisce**: true se è disponibile la protezione dei modelli tramite questa etichetta, in caso contrario false.
  
### <a name="label"></a>Label
Ottiene l'effettivo oggetto etichetta applicato al contenuto.

  
**Restituisce**: oggetto etichetta applicato al contenuto. 
  
**Vedere anche**: [mip::Label](class_mip_label.md)