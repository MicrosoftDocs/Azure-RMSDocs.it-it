---
title: Classe ExecutionState
description: 'Documenta la classe ExecutionState:: undefined di Microsoft Information Protection (MIP) SDK.'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 09/21/2020
ms.openlocfilehash: f73c3e366f1be0647d2c9a7de78f37b6a9a95549
ms.sourcegitcommit: 3f5f9f7695b9ed3c45e9230cd8b8cb39a1c5a5ed
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/23/2020
ms.locfileid: "95566992"
---
# <a name="class-executionstate"></a>Classe ExecutionState 
Interfaccia per tutti gli stati necessari per eseguire il motore.
I client dovrebbero chiamare i metodi solo per ottenere lo stato necessario. Di conseguenza, per motivi di efficienza, è consigliabile che i client implementino questa interfaccia in modo che lo stato corrispondente sia calcolato in modo dinamico anziché in anticipo.
  
## <a name="summary"></a>Riepilogo
 Members                        | Descrizioni                                
--------------------------------|---------------------------------------------
public std:: shared_ptr \<Label\> GetNewLabel () const  |  Ottiene l'ID dell'etichetta di riservatezza da applicare al documento.
public std::string GetContentIdentifier() const  |  Ottiene la descrizione del contenuto che descrive il documento. esempio per un file: [percorso\nomefile] esempio per un messaggio di posta elettronica: [Subject: sender].
public virtual DataState GetDataState () const  |  Ottiene lo stato del contenuto mentre l'applicazione interagisce con esso.
STD pubblico::p aria \<bool, std::string\> IsDowngradeJustified () const  |  L'implementazione dovrebbe restituire un valore che indica se è stata fornita una giustificazione per effettuare il downgrade di un'etichetta esistente.
public AssignmentMethod GetNewLabelAssignmentMethod() const  |  Ottiene il metodo di assegnazione della nuova etichetta.
public virtual std:: Vector \<std::pair\<std::string, std::string\> \> GetNewLabelExtendedProperties () const  |  Restituisce le proprietà estese della nuova etichetta.
public std:: Vector \<MetadataEntry\> GetContentMetadata (const std:: vector \<std::string\>& names, const std:: Vector \<std::string\>& namePrefixes) const  |  Ottiene gli elementi dei metadati dal contenuto.
public std::shared_ptr\<ProtectionDescriptor\> GetProtectionDescriptor() const  |  Ottiene il descrittore di protezione.
public ContentFormat GetContentFormat() const  |  Ottiene il formato del contenuto.
public virtual MetadataVersion GetContentMetadataVersion () const  |  Ottiene la versione dei metadati più elevata supportata dall'applicazione per il tenant.
public ActionType GetSupportedActions() const  |  Ottiene un'enumerazione mascherata che descrive tutti i tipi di azioni supportati.
public virtual std:: shared_ptr \<ClassificationResults\> GetClassificationResults (const std:: vector \<std::shared_ptr\<ClassificationRequest\> \> &) const  |  Restituisce una mappa dei risultati della classificazione.
public virtual std:: Map \<std::string, std::string\> GetAuditMetadata () const  |  Restituisce una mappa delle coppie chiave-valore di controllo specifiche dell'applicazione.
  
## <a name="members"></a>Members
  
### <a name="getnewlabel-function"></a>GetNewLabel (funzione)
Ottiene l'ID dell'etichetta di riservatezza da applicare al documento.

  
**Restituisce**: ID dell'etichetta di riservatezza da applicare al contenuto se esistente, in caso contrario una stringa vuota per rimuovere l'etichetta.
  
### <a name="getcontentidentifier-function"></a>GetContentIdentifier (funzione)
Ottiene la descrizione del contenuto che descrive il documento. esempio per un file: [percorso\nomefile] esempio per un messaggio di posta elettronica: [Subject: sender].

  
**Restituisce**: Descrizione del contenuto da applicare al contenuto.
Questo valore viene usato dal controllo come descrizione leggibile del contenuto
  
### <a name="getdatastate-function"></a>GetDataState (funzione)
Ottiene lo stato del contenuto mentre l'applicazione interagisce con esso.

  
**Restituisce**: stato dei dati del contenuto
  
### <a name="isdowngradejustified-function"></a>IsDowngradeJustified (funzione)
L'implementazione dovrebbe restituire un valore che indica se è stata fornita una giustificazione per effettuare il downgrade di un'etichetta esistente.

  
**Restituisce**: true se è stata fornita una giustificazione per il downgrade insieme al messaggio di giustificazione, in caso contrario false 
  
**Vedere anche**: MIP:: JustifyAction
  
### <a name="getnewlabelassignmentmethod-function"></a>GetNewLabelAssignmentMethod (funzione)
Ottiene il metodo di assegnazione della nuova etichetta.

  
**Restituisce**: metodo di assegnazione STANDARD, PRIVILEGED, AUTO. 
  
**Vedere anche**: mip::AssignmentMethod
  
### <a name="getnewlabelextendedproperties-function"></a>GetNewLabelExtendedProperties (funzione)
Restituisce le proprietà estese della nuova etichetta.

  
**Restituisce**: proprietà estese applicate al contenuto.
  
### <a name="getcontentmetadata-function"></a>GetContentMetadata (funzione)
Ottiene gli elementi dei metadati dal contenuto.

  
**Restituisce**: metadati applicati al contenuto. Ogni elemento dei metadati è una coppia di nome e valore.
  
### <a name="getprotectiondescriptor-function"></a>GetProtectionDescriptor (funzione)
Ottiene il descrittore di protezione.

  
**Restituisce**: descrittore di protezione
  
### <a name="getcontentformat-function"></a>GetContentFormat (funzione)
Ottiene il formato del contenuto.

  
**Restituisce**: DEFAULT, EMAIL 
  
**Vedere anche**: mip::ContentFormat
  
### <a name="getcontentmetadataversion-function"></a>GetContentMetadataVersion (funzione)
Ottiene la versione dei metadati più elevata supportata dall'applicazione per il tenant.

  
**Restituisce**: versione dei metadati del contenuto. Se è 0, i metadati non vengono sottoposti a controllo delle versioni. Se un formato di file supporta più versioni di metadati, ciò consente a MIP di comprendere tutti i metadati e di segnalare le modifiche granulari ai metadati in base alla versione.
  
### <a name="getsupportedactions-function"></a>GetSupportedActions (funzione)
Ottiene un'enumerazione mascherata che descrive tutti i tipi di azioni supportati.

  
**Restituisce**: enumerazione mascherata che descrive tutti i tipi di azioni supportati.
ActionType::Justify deve essere supportato. Quando una modifica dei criteri e dell'etichetta richiede una giustificazione, verrà restituita sempre un'azione di giustificazione.
  
### <a name="getclassificationresults-function"></a>GetClassificationResults (funzione)
Restituisce una mappa dei risultati della classificazione.

Parametri  
* **classificationIds**: elenco di ID di classificazione. 



  
**Restituisce**: un elenco di risultati della classificazione. restituisce nullptr se nessun ciclo di classificazione viene eseguito.
  
### <a name="getauditmetadata-function"></a>GetAuditMetadata (funzione)
Restituisce una mappa delle coppie chiave-valore di controllo specifiche dell'applicazione.

  
**Returns**: elenco della chiave registrata dei metadati di controllo specifici dell'applicazione: coppie valore mittente: ID di posta elettronica per i destinatari del mittente: rappresenta una matrice JSON di destinatari per un messaggio di posta elettronica LastModifiedBy: ID di posta elettronica per l'utente che ha apportato l'ultima modifica al contenuto LastModifiedDate: data dell'Ultima modifica del contenuto