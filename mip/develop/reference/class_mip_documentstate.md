---
title: Classe MIP::D ocumentState
description: Documenta la classe MIP::d ocumentstate dell'SDK Microsoft Information Protection (MIP).
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 02/14/2020
ms.openlocfilehash: a49683730f120b3d43e2c8f9381a86f0df1a400d
ms.sourcegitcommit: 2d3c638fb576f3f074330a33d077db0cf0e7d4e7
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/20/2020
ms.locfileid: "77490133"
---
# <a name="class-mipdocumentstate"></a>Classe MIP::D ocumentState 
  
## <a name="summary"></a>Riepilogo
 Members                        | Descrizioni                                
--------------------------------|---------------------------------------------
public std::string GetContentIdentifier() const  |  Ottiene la descrizione del contenuto che descrive il documento. esempio per un file: [percorso\nomefile] esempio per un messaggio di posta elettronica: [Subject: sender].
public virtual DataState GetDataState () const  |  Ottiene lo stato del contenuto mentre l'applicazione interagisce con esso.
public std:: Vector\<std::p Air\<std:: String, std:: String\>\> GetContentMetadata (const std:: Vector\<std:: String\>& Names, const std:: Vector\<std:: String\>& namePrefixes) const  |  Ottiene gli elementi dei metadati dal contenuto.
public std:: shared_ptr\<ProtectionDescriptor\> GetProtectionDescriptor () const  |  Ottiene il descrittore di protezione.
public ContentFormat GetContentFormat() const  |  Ottiene il formato del contenuto.
public virtual std:: shared_ptr\<ClassificationResults\> GetClassificationResults (const std:: Vector\<std:: shared_ptr\<ClassificationRequest\>\> &) const  |  Restituisce una mappa dei risultati della classificazione.
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

  
**Restituisce**: metadati applicati al contenuto. Ogni elemento dei metadati è una coppia di nome e valore.
  
### <a name="getprotectiondescriptor-function"></a>GetProtectionDescriptor (funzione)
Ottiene il descrittore di protezione.

  
**Restituisce**: descrittore di protezione
  
### <a name="getcontentformat-function"></a>GetContentFormat (funzione)
Ottiene il formato del contenuto.

  
**Restituisce**: DEFAULT, EMAIL 
  
**Vedere anche**: [MIP:: ContentFormat](mip-enums-and-structs.md#contentformat-enum)
  
### <a name="getclassificationresults-function"></a>GetClassificationResults (funzione)
Restituisce una mappa dei risultati della classificazione.

Parametri:  
* **classificationIds**: elenco di ID di classificazione. 



  
**Restituisce**: un elenco di risultati della classificazione. restituisce nullptr se nessun ciclo di classificazione viene eseguito.
  
### <a name="getauditmetadata-function"></a>GetAuditMetadata (funzione)
Restituisce una mappa delle coppie chiave-valore di controllo specifiche dell'applicazione.

  
**Returns**: elenco della chiave registrata dei metadati di controllo specifici dell'applicazione: coppie valore mittente: ID di posta elettronica per i destinatari del mittente: rappresenta una matrice JSON di destinatari per un messaggio di posta elettronica LastModifiedBy: ID di posta elettronica per l'utente che ha apportato l'ultima modifica al contenuto LastModifiedDate: data dell'Ultima modifica del contenuto
  
### <a name="getlastmodifiedtime-function"></a>GetLastModifiedTime (funzione)
Restituisce un punto di ora all'Ultima modifica apportata al documento.

  
**Returns**: ora dell'Ultima modifica del punto di tempo dei documenti.