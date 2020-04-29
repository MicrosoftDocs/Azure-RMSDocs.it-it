---
title: Classe DocumentState
description: 'Documenta la classe documentstate:: undefined di Microsoft Information Protection (MIP) SDK.'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 04/16/2020
ms.openlocfilehash: 674e43b89a43fe90fa1fb38fb7c6d1d51a7326e0
ms.sourcegitcommit: f54920bf017902616589aca30baf6b64216b6913
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/22/2020
ms.locfileid: "81763322"
---
# <a name="class-documentstate"></a>Classe DocumentState 
  
## <a name="summary"></a>Riepilogo
 Members                        | Descrizioni                                
--------------------------------|---------------------------------------------
public std::string GetContentIdentifier() const  |  Ottiene la descrizione del contenuto che descrive il documento. esempio per un file: [percorso\nomefile] esempio per un messaggio di posta elettronica: [Subject: sender].
public virtual DataState GetDataState () const  |  Ottiene lo stato del contenuto mentre l'applicazione interagisce con esso.
public std:: Vector\<MetadataEntry\> GetContentMetadata (const std::\<vector std::\> String& names, const std\<:: Vector STD\> :: String& namePrefixes) const  |  Ottiene gli elementi dei metadati dal contenuto.
public std:: shared_ptr\<ProtectionDescriptor\> GetProtectionDescriptor () const  |  Ottiene il descrittore di protezione.
public ContentFormat GetContentFormat() const  |  Ottiene il formato del contenuto.
public virtual unsigned int GetContentMetadataVersion () const  |  Ottiene la versione dei metadati più elevata supportata dall'applicazione per il tenant.
public virtual std:: shared_ptr\<ClassificationResults\> GetClassificationResults (const std::\<vector std::\<shared_ptr\> \> ClassificationRequest &) const  |  Restituisce una mappa dei risultati della classificazione.
public virtual std:: Map\<std:: String, std:: String\> GetAuditMetadata () const  |  Restituisce una mappa delle coppie chiave-valore di controllo specifiche dell'applicazione.
public virtual std:: Chrono:: time_point\<std:: Chrono:: system_clock\> GetLastModifiedTime () const  |  Restituisce un punto di ora all'Ultima modifica apportata al documento.
  
## <a name="members"></a>Members
  
### <a name="getcontentidentifier-function"></a>GetContentIdentifier (funzione)
Ottiene la descrizione del contenuto che descrive il documento. esempio per un file: [percorso\nomefile] esempio per un messaggio di posta elettronica: [Subject: sender].

  
**Restituisce**: Descrizione del contenuto da applicare al contenuto.
Questo valore viene usato dal controllo come descrizione leggibile del contenuto
  
### <a name="getdatastate-function"></a>GetDataState (funzione)
Ottiene lo stato del contenuto mentre l'applicazione interagisce con esso.

  
**Restituisce**: stato dei dati del contenuto
  
### <a name="getcontentmetadata-function"></a>GetContentMetadata (funzione)
Ottiene gli elementi dei metadati dal contenuto.

  
**Restituisce**: metadati applicati al contenuto. 
  
**Vedere anche**: MIP:: MetadataEntry.
  
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
  
### <a name="getclassificationresults-function"></a>GetClassificationResults (funzione)
Restituisce una mappa dei risultati della classificazione.

Parametri  
* **classificationIds**: elenco di ID di classificazione. 



  
**Restituisce**: un elenco di risultati della classificazione. restituisce nullptr se nessun ciclo di classificazione viene eseguito.
  
### <a name="getauditmetadata-function"></a>GetAuditMetadata (funzione)
Restituisce una mappa delle coppie chiave-valore di controllo specifiche dell'applicazione.

  
**Returns**: elenco della chiave registrata dei metadati di controllo specifici dell'applicazione: coppie valore mittente: ID di posta elettronica per i destinatari del mittente: rappresenta una matrice JSON di destinatari per un messaggio di posta elettronica LastModifiedBy: ID di posta elettronica per l'utente che ha apportato l'ultima modifica al contenuto LastModifiedDate: data dell'Ultima modifica del contenuto
  
### <a name="getlastmodifiedtime-function"></a>GetLastModifiedTime (funzione)
Restituisce un punto di ora all'Ultima modifica apportata al documento.

  
**Returns**: ora dell'Ultima modifica del punto di tempo dei documenti.