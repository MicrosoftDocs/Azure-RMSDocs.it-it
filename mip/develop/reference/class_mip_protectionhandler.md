---
title: Classe mip::ProtectionHandler
description: Documenta la classe MIP::p rotectionhandler dell'SDK Microsoft Information Protection (MIP).
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 07/16/2019
ms.openlocfilehash: 306748121e34122a5623aea3e1d7ff4ba7f14787
ms.sourcegitcommit: fcde8b31f8685023f002044d3a1d1903e548d207
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/21/2019
ms.locfileid: "69883419"
---
# <a name="class-mipprotectionhandler"></a>Classe mip::ProtectionHandler 
Gestisce azioni correlate alla protezione per una configurazione di protezione specifica.
  
## <a name="summary"></a>Riepilogo
 Members                        | Descrizioni                                
--------------------------------|---------------------------------------------
public std:: shared_ptr\<Stream\> CreateProtectedStream (const std::\<shared_ptr\>Stream & backingStream, int64_t contentStartPosition, int64_t contentSize)  |  Crea un flusso protetto che consentirà la crittografia/decrittografia del contenuto.
public int64_t EncryptBuffer(int64_t offsetFromStart, const uint8_t* inputBuffer, int64_t inputBufferSize, uint8_t* outputBuffer, int64_t outputBufferSize, bool isFinal)  |  Crittografa un buffer.
public int64_t DecryptBuffer(int64_t offsetFromStart, const uint8_t* inputBuffer, int64_t inputBufferSize, uint8_t* outputBuffer, int64_t outputBufferSize, bool isFinal)  |  Decrittografa un buffer.
public int64_t GetProtectedContentLength(int64_t unprotectedLength, bool includesFinalBlock)  |  Calcola la dimensione (in byte) del contenuto se fosse da crittografare con questo [ProtectionHandler](class_mip_protectionhandler.md).
public int64_t GetBlockSize()  |  Ottiene la dimensione del blocco (in byte) per la modalità crittografia usata da questo [ProtectionHandler](class_mip_protectionhandler.md).
public std:: Vector\<std:: String\> getrights () const  |  Ottiene i diritti concessi all'utente/identità associata a questo [ProtectionHandler](class_mip_protectionhandler.md).
public bool AccessCheck(const std::string& right) const  |  Controlla se il gestore di protezione concede l'accesso utente al diritto specificato.
public const std::string GetIssuedTo()  |  Ottiene l'utente associato al gestore di protezione.
public const std::string GetOwner()  |  Ottiene indirizzo e-mail del proprietario del contenuto.
public bool IsIssuedToOwner()  |  Ottiene un valore che indica se l'utente corrente è o meno il proprietario del contenuto.
public std:: shared_ptr\<ProtectionDescriptor\> GetProtectionDescriptor ()  |  Ottiene i dettagli della protezione.
public const std::string GetContentId()  |  Ottiene l'identificatore univoco del documento/contenuto.
public bool DoesUseDeprecatedAlgorithms()  |  Ottiene un valore che indica se il gestore di protezione usa o meno algoritmi di crittografia deprecati per compatibilità con le versioni precedenti.
public bool IsAuditedExtractAllowed()  |  Ottiene un valore che indica se il gestore di protezione concede o meno all'utente il diritto 'audited extract'.
public const std::\<vector\> uint8_t GetSerializedPublishingLicense ()  |  Serializza [ProtectionHandler](class_mip_protectionhandler.md) in una licenza di pubblicazione
  
## <a name="members"></a>Members
  
### <a name="createprotectedstream-function"></a>CreateProtectedStream (funzione)
Crea un flusso protetto che consentirà la crittografia/decrittografia del contenuto.

Parametri:  
* **backingStream**: Flusso di backup da cui leggere/scrivere 


* **contentStartPosition**: Posizione iniziale (in byte) all'interno del flusso di backup in cui inizia il contenuto protetto 


* **contentSize**: Dimensioni (in byte) del contenuto protetto nel flusso di backup



  
**Restituisce**: Flusso protetto
  
### <a name="encryptbuffer-function"></a>EncryptBuffer (funzione)
Crittografa un buffer.

Parametri:  
* **offsetFromStart**: Posizione relativa di inputBuffer dall'inizio del contenuto non crittografato 


* **inputBuffer**: Buffer di contenuto non crittografato che verrà crittografato 


* **inputBufferSize**: Dimensioni (in byte) del buffer di input 


* **outputBuffer**: Buffer in cui verrà copiato il contenuto crittografato 


* **outputBufferSize**: Dimensioni (in byte) del buffer di output 


* **isFinal**: Se il buffer di input contiene i byte non crittografati finali



  
**Restituisce**: Dimensioni effettive (in byte) del contenuto crittografato
  
### <a name="decryptbuffer-function"></a>DecryptBuffer (funzione)
Decrittografa un buffer.

Parametri:  
* **offsetFromStart**: Posizione relativa di inputBuffer dall'inizio del contenuto crittografato 


* **inputBuffer**: Buffer di contenuto crittografato che verrà decrittografato 


* **inputBufferSize**: Dimensioni (in byte) del buffer di input 


* **outputBuffer**: Buffer in cui verrà copiato il contenuto decrittografato 


* **outputBufferSize**: Dimensioni (in byte) del buffer di output 


* **isFinal**: Se il buffer di input contiene i byte crittografati finali



  
**Restituisce**: Dimensioni effettive (in byte) del contenuto decrittografato
  
### <a name="getprotectedcontentlength-function"></a>GetProtectedContentLength (funzione)
Calcola la dimensione (in byte) del contenuto se fosse da crittografare con questo [ProtectionHandler](class_mip_protectionhandler.md).

Parametri:  
* **unprotectedLength**: Dimensioni (in byte) del contenuto non protetto 


* **includesFinalBlock**: Descrive se il contenuto non protetto in questione include il blocco finale o meno. Ad esempio, in modalità di crittografia CBC4k, i blocchi protetti non finali hanno le stesse dimensioni di quelli non protetti, ma i blocchi protetti finali sono di dimensioni superiori rispetto ai corrispondenti non protetti.



  
**Restituisce**: Dimensioni (in byte) del contenuto protetto
  
### <a name="getblocksize-function"></a>GetBlockSize (funzione)
Ottiene la dimensione del blocco (in byte) per la modalità crittografia usata da questo [ProtectionHandler](class_mip_protectionhandler.md).

  
**Restituisce**: Dimensioni blocco (in byte)
  
### <a name="getrights-function"></a>Funzione getrights
Ottiene i diritti concessi all'utente/identità associata a questo [ProtectionHandler](class_mip_protectionhandler.md).

  
**Restituisce**: Diritti concessi all'utente
  
### <a name="accesscheck-function"></a>AccessCheck (funzione)
Controlla se il gestore di protezione concede l'accesso utente al diritto specificato.

Parametri:  
* a **destra**: Diritto di controllo



  
**Restituisce**: Se il gestore protezione concede l'accesso utente al diritto specificato
  
### <a name="getissuedto-function"></a>GetIssuedTo (funzione)
Ottiene l'utente associato al gestore di protezione.

  
**Restituisce**: Utente associato al gestore protezione
  
### <a name="getowner-function"></a>Funzione GetOwner
Ottiene indirizzo e-mail del proprietario del contenuto.

  
**Restituisce**: Indirizzo e-mail del proprietario del contenuto
  
### <a name="isissuedtoowner-function"></a>IsIssuedToOwner (funzione)
Ottiene un valore che indica se l'utente corrente è o meno il proprietario del contenuto.

  
**Restituisce**: Se l'utente corrente è il proprietario del contenuto
  
### <a name="getprotectiondescriptor-function"></a>GetProtectionDescriptor (funzione)
Ottiene i dettagli della protezione.

  
**Restituisce**: Dettagli sulla protezione
  
### <a name="getcontentid-function"></a>GetContentId (funzione)
Ottiene l'identificatore univoco del documento/contenuto.

  
**Restituisce**: Identificatore univoco del contenuto
  
### <a name="doesusedeprecatedalgorithms-function"></a>DoesUseDeprecatedAlgorithms (funzione)
Ottiene un valore che indica se il gestore di protezione usa o meno algoritmi di crittografia deprecati per compatibilità con le versioni precedenti.

  
**Restituisce**: Se il gestore protezione usa algoritmi di crittografia deprecati o meno
  
### <a name="isauditedextractallowed-function"></a>IsAuditedExtractAllowed (funzione)
Ottiene un valore che indica se il gestore di protezione concede o meno all'utente il diritto 'audited extract'.

  
**Restituisce**: Se il gestore protezione concede a right o no l'utente ' audited Extract '
  
### <a name="getserializedpublishinglicense-function"></a>GetSerializedPublishingLicense (funzione)
Serializza [ProtectionHandler](class_mip_protectionhandler.md) in una licenza di pubblicazione

  
**Restituisce**: Licenza di pubblicazione serializzata