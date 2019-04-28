---
title: Classe mip::ExecutionState
description: 'Classe MIP:: executionstate di Microsoft Information Protection (MIP) SDK vengono documentate.'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: 318b87405ad9e6d6291f82a0bec3da6031e04ccd
ms.sourcegitcommit: fff4c155c52c9ff20bc4931d5ac20c3ea6e2ff9e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/24/2019
ms.locfileid: "60174120"
---
# <a name="class-mipexecutionstate"></a>Classe mip::ExecutionState 
Interfaccia per tutti gli stati necessari per eseguire il motore.
I client dovrebbero chiamare i metodi solo per ottenere lo stato necessario. Di conseguenza, per motivi di efficienza, è consigliabile che i client implementino questa interfaccia in modo che lo stato corrispondente sia calcolato in modo dinamico anziché in anticipo.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public std::string GetNewLabelId() const  |  Ottiene l'ID dell'etichetta di riservatezza da applicare al documento.
public ActionSource GetNewLabelActionSource() const  |  Ottiene l'origine per una nuova azione per l'etichetta.
public std::string GetContentIdentifier() const  |  Ottiene la descrizione del contenuto che descrive il documento. esempio relativo a un file: [percorso\nomefile] di esempio per un messaggio di posta elettronica: [mittente: soggetto].
public virtual DataState GetDataState() const  |  Ottiene lo stato del contenuto mentre l'applicazione interagisce con esso.
Public std:: Pair\<bool, std:: String\> IsDowngradeJustified() const  |  L'implementazione dovrebbe restituire un valore che indica se è stata fornita una giustificazione per effettuare il downgrade di un'etichetta esistente.
public AssignmentMethod GetNewLabelAssignmentMethod() const  |  Ottiene il metodo di assegnazione della nuova etichetta.
Public std:: Vector virtual\<std:: Pair\<std:: String, std:: String\> \> GetNewLabelExtendedProperties() const  |  Restituisce le proprietà estese della nuova etichetta.
Public std:: Vector\<std:: Pair\<std:: String, std:: String\> \> GetContentMetadata (const std:: Vector\<std:: String\>& nomi, const std:: Vector\<std:: String\>& namePrefixes) const  |  Ottiene gli elementi dei metadati dal contenuto.
Public std:: shared_ptr\<ProtectionDescriptor\> GetProtectionDescriptor() const  |  Ottiene il descrittore di protezione.
public ContentFormat GetContentFormat() const  |  Ottiene il formato del contenuto.
public ActionType GetSupportedActions() const  |  Ottiene un'enumerazione mascherata che descrive tutti i tipi di azioni supportati.
Public std:: shared_ptr virtual\<ClassificationResults\> GetClassificationResults (const std:: Vector\<std:: shared_ptr\<ClassificationRequest\> \> &) const  |  Restituisce una mappa dei risultati della classificazione.
public virtual std::map\<std::string, std::string\> GetAuditMetadata() const  |  Restituisce una mappa di coppie chiave-valore di controllo specifico dell'applicazione.
  
## <a name="members"></a>Membri
  
### <a name="getnewlabelid-function"></a>GetNewLabelId (funzione)
Ottiene l'ID dell'etichetta di riservatezza da applicare al documento.

  
**Restituisce**: ID etichetta di riservatezza da applicare al contenuto se esistente in caso contrario vuota per rimuovere l'etichetta.
  
### <a name="getnewlabelactionsource-function"></a>GetNewLabelActionSource (funzione)
Ottiene l'origine per una nuova azione per l'etichetta.

  
**Restituisce**: Origine azione.
  
### <a name="getcontentidentifier-function"></a>GetContentIdentifier (funzione)
Ottiene la descrizione del contenuto che descrive il documento. esempio relativo a un file: [percorso\nomefile] di esempio per un messaggio di posta elettronica: [mittente: soggetto].

  
**Restituisce**: Descrizione del contenuto da applicare al contenuto.
Questo valore viene usato dal controllo come descrizione leggibile del contenuto
  
### <a name="getdatastate-function"></a>GetDataState (funzione)
Ottiene lo stato del contenuto mentre l'applicazione interagisce con esso.

  
**Restituisce**: Stato dei dati del contenuto
  
### <a name="isdowngradejustified-function"></a>Funzione IsDowngradeJustified
L'implementazione dovrebbe restituire un valore che indica se è stata fornita una giustificazione per effettuare il downgrade di un'etichetta esistente.

  
**Restituisce**: True se il downgrade è justifiedalong con false il messageelse giustificazione 
  
**Vedere anche**: [mip::JustifyAction](class_mip_justifyaction.md)
  
### <a name="getnewlabelassignmentmethod-function"></a>GetNewLabelAssignmentMethod (funzione)
Ottiene il metodo di assegnazione della nuova etichetta.

  
**Restituisce**: Il metodo di assegnazione STANDARD, PRIVILEGED, AUTO. 
  
**Vedere anche**: [assignmentmethod](mip-enums-and-structs.md#assignmentmethod)
  
### <a name="getnewlabelextendedproperties-function"></a>GetNewLabelExtendedProperties (funzione)
Restituisce le proprietà estese della nuova etichetta.

  
**Restituisce**: Le proprietà estese applicate al contenuto.
  
### <a name="getcontentmetadata-function"></a>GetContentMetadata (funzione)
Ottiene gli elementi dei metadati dal contenuto.

  
**Restituisce**: I metadati applicati al contenuto. Ogni elemento dei metadati è una coppia di nome e valore.
  
### <a name="getprotectiondescriptor-function"></a>GetProtectionDescriptor (funzione)
Ottiene il descrittore di protezione.

  
**Restituisce**: Il descrittore di protezione
  
### <a name="getcontentformat-function"></a>GetContentFormat (funzione)
Ottiene il formato del contenuto.

  
**Restituisce**: IMPOSTAZIONE PREDEFINITA, POSTA ELETTRONICA 
  
**Vedere anche**: [contentformat](mip-enums-and-structs.md#contentformat)
  
### <a name="getsupportedactions-function"></a>GetSupportedActions (funzione)
Ottiene un'enumerazione mascherata che descrive tutti i tipi di azioni supportati.

  
**Restituisce**: Un'enumerazione con maschera che descrive tutti i tipi di azione supportata.
ActionType::Justify deve essere supportato. Quando una modifica dei criteri e dell'etichetta richiede una giustificazione, verrà restituita sempre un'azione di giustificazione.
  
### <a name="getclassificationresults-function"></a>GetClassificationResults (funzione)
Restituisce una mappa dei risultati della classificazione.

Parametri:  
* **classificationIds**: un elenco di ID di classificazione. 



  
**Restituisce**: Un elenco dei risultati di classificazione. restituire nullptr se eseguito alcun ciclo di classificazione.
  
### <a name="getauditmetadata-function"></a>GetAuditMetadata (funzione)
Restituisce una mappa di coppie chiave-valore di controllo specifico dell'applicazione.

  
**Restituisce**: Un elenco di coppie chiave: valore registrato di metadati controllo specifico dell'applicazione mittente: Id di posta elettronica del mittente, destinatari: Rappresenta una matrice JSON dei destinatari del messaggio di posta elettronica LastModifiedBy: Id di posta elettronica per l'utente che ha modificato il LastModifiedDate & lt; contenuto: Data che ultima modifica del contenuto