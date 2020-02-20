---
title: Classe mip::ProtectionHandler
description: Documenta la classe MIP::p rotectionhandler dell'SDK Microsoft Information Protection (MIP).
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 02/14/2020
ms.openlocfilehash: 4b245ea2a579aa3d9a0fddfb503830d75577c2b7
ms.sourcegitcommit: 2d3c638fb576f3f074330a33d077db0cf0e7d4e7
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/20/2020
ms.locfileid: "77489657"
---
# <a name="class-mipprotectionhandler"></a>Classe mip::ProtectionHandler 
Gestisce azioni correlate alla protezione per una configurazione di protezione specifica.
  
## <a name="summary"></a>Riepilogo
 Members                        | Descrizioni                                
--------------------------------|---------------------------------------------
public std:: shared_ptr\<Stream\> CreateProtectedStream (const std:: shared_ptr\<Stream\>& backingStream, int64_t contentStartPosition, int64_t contentSize)  |  Crea un flusso protetto che consentirà la crittografia/decrittografia del contenuto.
public int64_t EncryptBuffer(int64_t offsetFromStart, const uint8_t* inputBuffer, int64_t inputBufferSize, uint8_t* outputBuffer, int64_t outputBufferSize, bool isFinal)  |  Crittografa un buffer.
public int64_t DecryptBuffer(int64_t offsetFromStart, const uint8_t* inputBuffer, int64_t inputBufferSize, uint8_t* outputBuffer, int64_t outputBufferSize, bool isFinal)  |  Decrittografa un buffer.
public int64_t GetProtectedContentLength(int64_t unprotectedLength, bool includesFinalBlock)  |  Calcola le dimensioni (in byte) del contenuto se deve essere crittografato con questo ProtectionHandler.
public int64_t GetBlockSize()  |  Ottiene la dimensione del blocco (in byte) per la modalità di crittografia utilizzata da questo ProtectionHandler.
public std:: Vector\<std:: String\> getrights () const  |  Ottiene i diritti concessi all'utente/identità associata a questo ProtectionHandler.
public bool AccessCheck(const std::string& right) const  |  Controlla se il gestore di protezione concede l'accesso utente al diritto specificato.
public const std::string GetIssuedTo()  |  Ottiene l'utente associato al gestore di protezione.
public const std::string GetOwner()  |  Ottiene indirizzo e-mail del proprietario del contenuto.
public bool IsIssuedToOwner()  |  Ottiene un valore che indica se l'utente corrente è o meno il proprietario del contenuto.
public std:: shared_ptr\<ProtectionDescriptor\> GetProtectionDescriptor ()  |  Ottiene i dettagli della protezione.
public const std::string GetContentId()  |  Ottiene l'identificatore univoco del documento/contenuto.
public bool DoesUseDeprecatedAlgorithms()  |  Ottiene un valore che indica se il gestore di protezione usa o meno algoritmi di crittografia deprecati per compatibilità con le versioni precedenti.
public bool IsAuditedExtractAllowed()  |  Ottiene un valore che indica se il gestore di protezione concede o meno all'utente il diritto 'audited extract'.
public const std:: Vector\<uint8_t\> GetSerializedPublishingLicense ()  |  Serializzare ProtectionHandler in una licenza di pubblicazione (PL)
  
## <a name="members"></a>Members
  
### <a name="createprotectedstream-function"></a>CreateProtectedStream (funzione)
Crea un flusso protetto che consentirà la crittografia/decrittografia del contenuto.

Parametri:  
* **backingStream**: flusso sottostante da cui leggere/scrivere 


* **contentStartPosition**: posizione di inizio (in byte) all'interno del flusso sottostante dove inizia il contenuto protetto 


* **contentSize**: dimensione (in byte) del contenuto protetto all'interno del flusso sottostante



  
**Restituisce**: flusso protetto
  
### <a name="encryptbuffer-function"></a>EncryptBuffer (funzione)
Crittografa un buffer.

Parametri:  
* **offsetFromStart**: posizione relativa di inputBuffer dall'inizio del contenuto di testo non crittografato 


* **inputBuffer**: buffer di contenuto di testo non crittografato che verrà crittografato 


* **inputBufferSize**: dimensione (in byte) del buffer di input 


* **outputBuffer**: buffer in cui verrà copiato il contenuto crittografato 


* **outputBufferSize**: dimensione (in byte) del buffer di output 


* **isFinal**: ottiene un valore che indica se il buffer di input contiene o meno i byte di testo non crittografato finali



  
**Restituisce**: dimensione effettiva (in byte) del contenuto crittografato
  
### <a name="decryptbuffer-function"></a>DecryptBuffer (funzione)
Decrittografa un buffer.

Parametri:  
* **offsetFromStart**: posizione relativa di inputBuffer dall'inizio del contenuto crittografato 


* **inputBuffer**: buffer di contenuto crittografato che verrà decrittografato 


* **inputBufferSize**: dimensione (in byte) del buffer di input 


* **outputBuffer**: buffer in cui verrà copiato il contenuto decrittografato 


* **outputBufferSize**: dimensione (in byte) del buffer di output 


* **isFinal**: ottiene un valore che indica se il buffer di input contiene o meno i byte crittografati finali



  
**Restituisce**: dimensione effettiva (in byte) del contenuto decrittografato
  
### <a name="getprotectedcontentlength-function"></a>GetProtectedContentLength (funzione)
Calcola le dimensioni (in byte) del contenuto se deve essere crittografato con questo ProtectionHandler.

Parametri:  
* **unprotectedLength**: dimensione (in byte) del contenuto non protetto 


* **includesFinalBlock**: descrive se il contenuto non protetto in questione include o meno il blocco finale. Ad esempio, in modalità di crittografia CBC4k, i blocchi protetti non finali hanno le stesse dimensioni di quelli non protetti, ma i blocchi protetti finali sono di dimensioni superiori rispetto ai corrispondenti non protetti.



  
**Restituisce**: dimensione (in byte) del contenuto protetto
  
### <a name="getblocksize-function"></a>GetBlockSize (funzione)
Ottiene la dimensione del blocco (in byte) per la modalità di crittografia utilizzata da questo ProtectionHandler.

  
**Restituisce**: dimensione del blocco (in byte)
  
### <a name="getrights-function"></a>Funzione getrights
Ottiene i diritti concessi all'utente/identità associata a questo ProtectionHandler.

  
**Restituisce**: diritti concessi all'utente
  
### <a name="accesscheck-function"></a>AccessCheck (funzione)
Controlla se il gestore di protezione concede l'accesso utente al diritto specificato.

Parametri:  
* **right**: diritto da controllare



  
**Restituisce**: valore che indica se il gestore di protezione concede o meno l'accesso utente al diritto specificato
  
### <a name="getissuedto-function"></a>GetIssuedTo (funzione)
Ottiene l'utente associato al gestore di protezione.

  
**Restituisce**: utente associato al gestore di protezione
  
### <a name="getowner-function"></a>Funzione GetOwner
Ottiene indirizzo e-mail del proprietario del contenuto.

  
**Restituisce**: indirizzo di posta elettronica del proprietario del contenuto
  
### <a name="isissuedtoowner-function"></a>IsIssuedToOwner (funzione)
Ottiene un valore che indica se l'utente corrente è o meno il proprietario del contenuto.

  
**Restituisce**: valore che indica se l'utente corrente è o meno il proprietario del contenuto
  
### <a name="getprotectiondescriptor-function"></a>GetProtectionDescriptor (funzione)
Ottiene i dettagli della protezione.

  
**Restituisce**: dettagli della protezione
  
### <a name="getcontentid-function"></a>GetContentId (funzione)
Ottiene l'identificatore univoco del documento/contenuto.

  
**Restituisce**: identificatore univoco del contenuto
  
### <a name="doesusedeprecatedalgorithms-function"></a>DoesUseDeprecatedAlgorithms (funzione)
Ottiene un valore che indica se il gestore di protezione usa o meno algoritmi di crittografia deprecati per compatibilità con le versioni precedenti.

  
**Restituisce**: valore che indica se il gestore di protezione usa o meno algoritmi di crittografia deprecati
  
### <a name="isauditedextractallowed-function"></a>IsAuditedExtractAllowed (funzione)
Ottiene un valore che indica se il gestore di protezione concede o meno all'utente il diritto 'audited extract'.

  
**Restituisce**: valore che indica se il gestore di protezione concede o meno all'utente il diritto 'audited extract'
  
### <a name="getserializedpublishinglicense-function"></a>GetSerializedPublishingLicense (funzione)
Serializzare ProtectionHandler in una licenza di pubblicazione (PL)

  
**Restituisce**: licenza di pubblicazione serializzata