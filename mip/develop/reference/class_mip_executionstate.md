---
title: Classe mip::ExecutionState
description: 'Documenta la classe MIP:: ExecutionState di Microsoft Information Protection (MIP) SDK.'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 08/27/2019
ms.openlocfilehash: d73a9e814401dc634f95e14ff4447edd071e63ba
ms.sourcegitcommit: 1499790746145d40d667d138baa6e18598421f0e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/27/2019
ms.locfileid: "70055128"
---
# <a name="class-mipexecutionstate"></a>Classe mip::ExecutionState 
Interfaccia per tutti gli stati necessari per eseguire il motore.
I client dovrebbero chiamare i metodi solo per ottenere lo stato necessario. Di conseguenza, per motivi di efficienza, è consigliabile che i client implementino questa interfaccia in modo che lo stato corrispondente sia calcolato in modo dinamico anziché in anticipo.
  
## <a name="summary"></a>Riepilogo
 Members                        | Descrizioni                                
--------------------------------|---------------------------------------------
public std:: shared_ptr\<label\> GetNewLabel () const  |  Ottiene l'ID dell'etichetta di riservatezza da applicare al documento.
public std::string GetContentIdentifier() const  |  Ottiene la descrizione del contenuto che descrive il documento. esempio per un file: [percorso\nomefile] esempio per un messaggio di posta elettronica: [Subject: sender].
public virtual DataState GetDataState () const  |  Ottiene lo stato del contenuto mentre l'applicazione interagisce con esso.
public std::p aria\<bool, std:: String\> IsDowngradeJustified () const  |  L'implementazione dovrebbe restituire un valore che indica se è stata fornita una giustificazione per effettuare il downgrade di un'etichetta esistente.
public AssignmentMethod GetNewLabelAssignmentMethod() const  |  Ottiene il metodo di assegnazione della nuova etichetta.
public virtual std:: Vector\<std::p Air\<std:: String, std:: String\> \> GetNewLabelExtendedProperties () const  |  Restituisce le proprietà estese della nuova etichetta.
public std:: Vector\<std::p Air\<std:: String, std:: String\> \> GetContentMetadata (const std::\<vector std::\>String & Names, const std:: Vector\<std:: String\>& namePrefixes) const  |  Ottiene gli elementi dei metadati dal contenuto.
public std:: shared_ptr\<ProtectionDescriptor\> GetProtectionDescriptor () const  |  Ottiene il descrittore di protezione.
public ContentFormat GetContentFormat() const  |  Ottiene il formato del contenuto.
public ActionType GetSupportedActions() const  |  Ottiene un'enumerazione mascherata che descrive tutti i tipi di azioni supportati.
public virtual std:: shared_ptr\<ClassificationResults\> GetClassificationResults (const std::\<vector std::\<shared_ptr\> ClassificationRequest\> &) const  |  Restituisce una mappa dei risultati della classificazione.
public virtual std:: Map\<std:: String, std:: String\> GetAuditMetadata () const  |  Restituisce una mappa delle coppie chiave-valore di controllo specifiche dell'applicazione.
  
## <a name="members"></a>Members
  
### <a name="getnewlabel-function"></a>GetNewLabel (funzione)
Ottiene l'ID dell'etichetta di riservatezza da applicare al documento.

  
**Restituisce**: ID dell'etichetta di riservatezza da applicare al contenuto se esistente altrimenti vuoto per rimuovere l'etichetta.
  
### <a name="getcontentidentifier-function"></a>GetContentIdentifier (funzione)
Ottiene la descrizione del contenuto che descrive il documento. esempio per un file: [percorso\nomefile] esempio per un messaggio di posta elettronica: [Subject: sender].

  
**Restituisce**: Descrizione del contenuto da applicare al contenuto.
Questo valore viene usato dal controllo come descrizione leggibile del contenuto
  
### <a name="getdatastate-function"></a>GetDataState (funzione)
Ottiene lo stato del contenuto mentre l'applicazione interagisce con esso.

  
**Restituisce**: Stato dei dati di contenuto
  
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
  
### <a name="getcontentmetadata-function"></a>GetContentMetadata (funzione)
Ottiene gli elementi dei metadati dal contenuto.

  
**Restituisce**: Metadati applicati al contenuto. Ogni elemento dei metadati è una coppia di nome e valore.
  
### <a name="getprotectiondescriptor-function"></a>GetProtectionDescriptor (funzione)
Ottiene il descrittore di protezione.

  
**Restituisce**: Descrittore di protezione
  
### <a name="getcontentformat-function"></a>GetContentFormat (funzione)
Ottiene il formato del contenuto.

  
**Restituisce**: IMPOSTAZIONE PREDEFINITA, POSTA ELETTRONICA 
  
**Vedere anche**: [MIP:: ContentFormat](mip-enums-and-structs.md#contentformat-enum)
  
### <a name="getsupportedactions-function"></a>GetSupportedActions (funzione)
Ottiene un'enumerazione mascherata che descrive tutti i tipi di azioni supportati.

  
**Restituisce**: Enumerazione mascherata che descrive tutti i tipi di azione supportati.
ActionType::Justify deve essere supportato. Quando una modifica dei criteri e dell'etichetta richiede una giustificazione, verrà restituita sempre un'azione di giustificazione.
  
### <a name="getclassificationresults-function"></a>GetClassificationResults (funzione)
Restituisce una mappa dei risultati della classificazione.

Parametri:  
* **classificationIds**: elenco di ID di classificazione. 



  
**Restituisce**: Elenco di risultati della classificazione. restituisce nullptr se nessun ciclo di classificazione viene eseguito.
  
### <a name="getauditmetadata-function"></a>GetAuditMetadata (funzione)
Restituisce una mappa delle coppie chiave-valore di controllo specifiche dell'applicazione.

  
**Restituisce**: Elenco dei metadati di controllo specifici dell'applicazione chiave registrata: coppie valore mittente: ID di posta elettronica per i destinatari del mittente: Rappresenta una matrice JSON di destinatari per un LastModifiedBy di posta elettronica: ID di posta elettronica per l'utente che ha apportato l'ultima modifica al contenuto LastModifiedDate: Data dell'Ultima modifica apportata al contenuto