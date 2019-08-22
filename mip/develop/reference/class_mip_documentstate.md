---
title: Classe MIP::D ocumentState
description: Documenta la classe MIP::d ocumentstate dell'SDK Microsoft Information Protection (MIP).
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 07/16/2019
ms.openlocfilehash: 44fc6faf6b92e9f31dad96185e18b50be3a97e32
ms.sourcegitcommit: fcde8b31f8685023f002044d3a1d1903e548d207
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/21/2019
ms.locfileid: "69892903"
---
# <a name="class-mipdocumentstate"></a>Classe MIP::D ocumentState 
  
## <a name="summary"></a>Riepilogo
 Members                        | Descrizioni                                
--------------------------------|---------------------------------------------
public std::string GetContentIdentifier() const  |  Ottiene la descrizione del contenuto che descrive il documento. esempio per un file: [percorso\nomefile] esempio per un messaggio di posta elettronica: [Subject: sender].
public virtual DataState GetDataState () const  |  Ottiene lo stato del contenuto mentre l'applicazione interagisce con esso.
public std:: Vector\<std::p Air\<std:: String, std:: String\> \> GetContentMetadata (const std::\<vector std::\>String & Names, const std:: Vector\<std:: String\>& namePrefixes) const  |  Ottiene gli elementi dei metadati dal contenuto.
public std:: shared_ptr\<ProtectionDescriptor\> GetProtectionDescriptor () const  |  Ottiene il descrittore di protezione.
public ContentFormat GetContentFormat() const  |  Ottiene il formato del contenuto.
public virtual std:: shared_ptr\<ClassificationResults\> GetClassificationResults (const std::\<vector std::\<shared_ptr\> ClassificationRequest\> &) const  |  Restituisce una mappa dei risultati della classificazione.
public virtual std:: Map\<std:: String, std:: String\> GetAuditMetadata () const  |  Restituisce una mappa delle coppie chiave-valore di controllo specifiche dell'applicazione.
  
## <a name="members"></a>Members
  
### <a name="getcontentidentifier-function"></a>GetContentIdentifier (funzione)
Ottiene la descrizione del contenuto che descrive il documento. esempio per un file: [percorso\nomefile] esempio per un messaggio di posta elettronica: [Subject: sender].

  
**Restituisce**: Descrizione del contenuto da applicare al contenuto.
Questo valore viene usato dal controllo come descrizione leggibile del contenuto
  
### <a name="getdatastate-function"></a>GetDataState (funzione)
Ottiene lo stato del contenuto mentre l'applicazione interagisce con esso.

  
**Restituisce**: Stato dei dati di contenuto
  
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
  
### <a name="getclassificationresults-function"></a>GetClassificationResults (funzione)
Restituisce una mappa dei risultati della classificazione.

Parametri:  
* **classificationIds**: elenco di ID di classificazione. 



  
**Restituisce**: Elenco di risultati della classificazione. restituisce nullptr se nessun ciclo di classificazione viene eseguito.
  
### <a name="getauditmetadata-function"></a>GetAuditMetadata (funzione)
Restituisce una mappa delle coppie chiave-valore di controllo specifiche dell'applicazione.

  
**Restituisce**: Elenco dei metadati di controllo specifici dell'applicazione chiave registrata: coppie valore mittente: ID di posta elettronica per i destinatari del mittente: Rappresenta una matrice JSON di destinatari per un LastModifiedBy di posta elettronica: ID di posta elettronica per l'utente che ha apportato l'ultima modifica al contenuto LastModifiedDate: Data dell'Ultima modifica apportata al contenuto