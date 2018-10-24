---
title: Classe mip ExecutionState
description: Riferimento per la classe mip ExecutionState
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: 976bca60f3f494a0fbf196e6512b00bdcdd63992
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/28/2018
ms.locfileid: "47446312"
---
# <a name="class-mipexecutionstate"></a>Classe mip::ExecutionState 
Interfaccia per tutti gli stati necessari per eseguire il motore.
I client dovrebbero chiamare i metodi solo per ottenere lo stato necessario. Di conseguenza, per motivi di efficienza, è consigliabile che i client implementino questa interfaccia in modo che lo stato corrispondente sia calcolato in modo dinamico anziché in anticipo.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
 public std::string GetNewLabelId() const  |  Ottiene l'ID dell'etichetta di riservatezza da applicare al documento.
 public ActionSource GetNewLabelActionSource() const  |  Ottiene l'origine per una nuova azione per l'etichetta.
 public std::string GetContentIdentifier() const  |  Ottiene l'identificatore di contenuto che descrive il documento. Esempio per un file: [path] esempio per un messaggio di posta elettronica: [Subject:Sender].
 public ContentState GetContentState() const  |  Ottiene lo stato del contenuto mentre l'applicazione interagisce con esso.
public std::pair<bool, std::string> IsDowngradeJustified() const  |  L'implementazione dovrebbe restituire un valore che indica se è stata fornita una giustificazione per effettuare il downgrade di un'etichetta esistente.
 public AssignmentMethod GetNewLabelAssignmentMethod() const  |  Ottiene il metodo di assegnazione della nuova etichetta.
public std::vector<std::pair<std::string, std::string>> GetNewLabelExtendedProperties() const  |  Restituisce le proprietà estese della nuova etichetta.
public std::vector<std::pair<std::string, std::string>> GetContentMetadata(const std::vector<std::string>& names, const std::vector<std::string>& namePrefixes) const  |  Ottiene gli elementi dei metadati dal contenuto.
public std::shared_ptr<ProtectionDescriptor> GetProtectionDescriptor() const  |  Ottiene il descrittore di protezione.
 public ContentFormat GetContentFormat() const  |  Ottiene il formato del contenuto.
 public ActionType GetSupportedActions() const  |  Ottiene un'enumerazione mascherata che descrive tutti i tipi di azioni supportati.
public virtual std::map<std::string, std::shared_ptr<ClassificationResult>> GetClassificationResults(const std::vector<std::string> &) const  |  Restituisce una mappa dei risultati della classificazione.
  
## <a name="members"></a>Membri
  
### <a name="getnewlabelid"></a>GetNewLabelId
Ottiene l'ID dell'etichetta di riservatezza da applicare al documento.

  
**Restituisce**: ID dell'etichetta di riservatezza da applicare al contenuto se esistente, in caso contrario una stringa vuota per rimuovere l'etichetta.
  
### <a name="getnewlabelactionsource"></a>GetNewLabelActionSource
Ottiene l'origine per una nuova azione per l'etichetta.

  
**Restituisce**: origine azione.
  
### <a name="getcontentidentifier"></a>GetContentIdentifier
Ottiene l'identificatore di contenuto che descrive il documento. Esempio per un file: [path] esempio per un messaggio di posta elettronica: [Subject:Sender].

  
**Restituisce**: identificatore di contenuto da applicare al contenuto.
Questo valore viene usato dal controllo come descrizione leggibile del contenuto
  
### <a name="getcontentstate"></a>GetContentState
Ottiene lo stato del contenuto mentre l'applicazione interagisce con esso.

  
**Restituisce**: stato dei dati del contenuto
  
### <a name="isdowngradejustified"></a>IsDowngradeJustified
L'implementazione dovrebbe restituire un valore che indica se è stata fornita una giustificazione per effettuare il downgrade di un'etichetta esistente.

  
**Restituisce**: true se è stata fornita una giustificazione per il downgrade insieme al messaggio di giustificazione, in caso contrario false 
  
**Vedere anche**: [mip::JustifyAction](class_mip_justifyaction.md)
  
### <a name="getnewlabelassignmentmethod"></a>GetNewLabelAssignmentMethod
Ottiene il metodo di assegnazione della nuova etichetta.

  
**Restituisce**: metodo di assegnazione STANDARD, PRIVILEGED, AUTO. 
  
**Vedere anche**: mip::AssignmentMethod
  
### <a name="getnewlabelextendedproperties"></a>GetNewLabelExtendedProperties
Restituisce le proprietà estese della nuova etichetta.

  
**Restituisce**: proprietà estese applicate al contenuto.
  
### <a name="getcontentmetadata"></a>GetContentMetadata
Ottiene gli elementi dei metadati dal contenuto.

  
**Restituisce**: metadati applicati al contenuto. Ogni elemento dei metadati è una coppia di nome e valore.
  
### <a name="protectiondescriptor"></a>ProtectionDescriptor
Ottiene il descrittore di protezione.

  
**Restituisce**: descrittore di protezione
  
### <a name="getcontentformat"></a>GetContentFormat
Ottiene il formato del contenuto.

  
**Restituisce**: DEFAULT, EMAIL 
  
**Vedere anche**: mip::ContentFormat
  
### <a name="actiontype"></a>ActionType
Ottiene un'enumerazione mascherata che descrive tutti i tipi di azioni supportati.

  
**Restituisce**: enumerazione mascherata che descrive tutti i tipi di azioni supportati.
ActionType::Justify deve essere supportato. Quando una modifica dei criteri e dell'etichetta richiede una giustificazione, verrà restituita sempre un'azione di giustificazione.
  
### <a name="classificationresult"></a>ClassificationResult
Restituisce una mappa dei risultati della classificazione.

Parametri:  
* **classificationId**: elenco di ID classificazione. 



  
**Restituisce**: elenco di risultati della classificazione.