---
title: Classe mip ProtectionHandler
description: Riferimento per la classe mip ProtectionHandler
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: 6fbae05030f56d3c9e680e6de9c8177a11b2f1e2
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/28/2018
ms.locfileid: "47446754"
---
# <a name="class-mipprotectionhandler"></a>Classe mip::ProtectionHandler 
Gestisce azioni correlate alla protezione per una configurazione di protezione specifica.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public std::shared_ptr<Stream> CreateProtectedStream(const std::shared_ptr<Stream>& backingStream, int64_t contentStartPosition, int64_t contentSize)  |  Crea un flusso protetto che consentirà la crittografia/decrittografia del contenuto.
 public int64_t EncryptBuffer(int64_t offsetFromStart, const uint8_t* inputBuffer, int64_t inputBufferSize, uint8_t* outputBuffer, int64_t outputBufferSize, bool isFinal)  |  Crittografa un buffer.
 public int64_t DecryptBuffer(int64_t offsetFromStart, const uint8_t* inputBuffer, int64_t inputBufferSize, uint8_t* outputBuffer, int64_t outputBufferSize, bool isFinal)  |  Decrittografa un buffer.
 public int64_t GetProtectedContentLength(int64_t unprotectedLength, bool includesFinalBlock)  |  Calcola la dimensione (in byte) del contenuto se fosse da crittografare con questo [ProtectionHandler](class_mip_protectionhandler.md).
 public int64_t GetBlockSize()  |  Ottiene la dimensione del blocco (in byte) per la modalità crittografia usata da questo [ProtectionHandler](class_mip_protectionhandler.md).
public std::vector<std::string> GetRights() const  |  Ottiene i diritti concessi all'utente/identità associata a questo [ProtectionHandler](class_mip_protectionhandler.md).
 public bool AccessCheck(const std::string& right) const  |  Controlla se il gestore di protezione concede l'accesso utente al diritto specificato.
 public const std::string GetIssuedTo()  |  Ottiene l'utente associato al gestore di protezione.
 public const std::string GetOwner()  |  Ottiene indirizzo e-mail del proprietario del contenuto.
 public bool IsIssuedToOwner()  |  Ottiene un valore che indica se l'utente corrente è o meno il proprietario del contenuto.
public std::shared_ptr<ProtectionDescriptor> GetProtectionDescriptor()  |  Ottiene i dettagli della protezione.
 public const std::string GetContentId()  |  Ottiene l'identificatore univoco del documento/contenuto.
 public bool DoesUseDeprecatedAlgorithms()  |  Ottiene un valore che indica se il gestore di protezione usa o meno algoritmi di crittografia deprecati per compatibilità con le versioni precedenti.
 public bool IsAuditedExtractAllowed()  |  Ottiene un valore che indica se il gestore di protezione concede o meno all'utente il diritto 'audited extract'.
public const std::vector<uint8_t> GetSerializedPublishingLicense()  |  Serializza [ProtectionHandler](class_mip_protectionhandler.md) in una licenza di pubblicazione
  
## <a name="members"></a>Membri
  
### <a name="stream"></a>Flusso
Crea un flusso protetto che consentirà la crittografia/decrittografia del contenuto.

Parametri:  
* **backingStream**: flusso sottostante da cui leggere/scrivere 


* **contentStartPosition**: posizione di inizio (in byte) all'interno del flusso sottostante dove inizia il contenuto protetto 


* **contentSize**: dimensione (in byte) del contenuto protetto all'interno del flusso sottostante



  
**Restituisce**: flusso protetto
  
### <a name="encryptbuffer"></a>EncryptBuffer
Crittografa un buffer.

Parametri:  
* **offsetFromStart**: posizione relativa di inputBuffer dall'inizio del contenuto di testo non crittografato 


* **inputBuffer**: buffer di contenuto di testo non crittografato che verrà crittografato 


* **inputBufferSize**: dimensione (in byte) del buffer di input 


* **outputBuffer**: buffer in cui verrà copiato il contenuto crittografato 


* **outputBufferSize**: dimensione (in byte) del buffer di output 


* **isFinal**: ottiene un valore che indica se il buffer di input contiene o meno i byte di testo non crittografato finali



  
**Restituisce**: dimensione effettiva (in byte) del contenuto crittografato
  
### <a name="decryptbuffer"></a>DecryptBuffer
Decrittografa un buffer.

Parametri:  
* **offsetFromStart**: posizione relativa di inputBuffer dall'inizio del contenuto crittografato 


* **inputBuffer**: buffer di contenuto crittografato che verrà decrittografato 


* **inputBufferSize**: dimensione (in byte) del buffer di input 


* **outputBuffer**: buffer in cui verrà copiato il contenuto decrittografato 


* **outputBufferSize**: dimensione (in byte) del buffer di output 


* **isFinal**: ottiene un valore che indica se il buffer di input contiene o meno i byte crittografati finali



  
**Restituisce**: dimensione effettiva (in byte) del contenuto decrittografato
  
### <a name="getprotectedcontentlength"></a>GetProtectedContentLength
Calcola la dimensione (in byte) del contenuto se fosse da crittografare con questo [ProtectionHandler](class_mip_protectionhandler.md).

Parametri:  
* **unprotectedLength**: dimensione (in byte) del contenuto non protetto 


* **includesFinalBlock**: descrive se il contenuto non protetto in questione include o meno il blocco finale. Ad esempio, in modalità di crittografia CBC4k, i blocchi protetti non finali hanno le stesse dimensioni di quelli non protetti, ma i blocchi protetti finali sono di dimensioni superiori rispetto ai corrispondenti non protetti.



  
**Restituisce**: dimensione (in byte) del contenuto protetto
  
### <a name="getblocksize"></a>GetBlockSize
Ottiene la dimensione del blocco (in byte) per la modalità crittografia usata da questo [ProtectionHandler](class_mip_protectionhandler.md).

  
**Restituisce**: dimensione del blocco (in byte)
  
### <a name="getrights"></a>GetRights
Ottiene i diritti concessi all'utente/identità associata a questo [ProtectionHandler](class_mip_protectionhandler.md).

  
**Restituisce**: diritti concessi all'utente
  
### <a name="accesscheck"></a>AccessCheck
Controlla se il gestore di protezione concede l'accesso utente al diritto specificato.

Parametri:  
* **right**: diritto da controllare



  
**Restituisce**: valore che indica se il gestore di protezione concede o meno l'accesso utente al diritto specificato
  
### <a name="getissuedto"></a>GetIssuedTo
Ottiene l'utente associato al gestore di protezione.

  
**Restituisce**: utente associato al gestore di protezione
  
### <a name="getowner"></a>GetOwner
Ottiene indirizzo e-mail del proprietario del contenuto.

  
**Restituisce**: indirizzo di posta elettronica del proprietario del contenuto
  
### <a name="isissuedtoowner"></a>IsIssuedToOwner
Ottiene un valore che indica se l'utente corrente è o meno il proprietario del contenuto.

  
**Restituisce**: valore che indica se l'utente corrente è o meno il proprietario del contenuto
  
### <a name="protectiondescriptor"></a>ProtectionDescriptor
Ottiene i dettagli della protezione.

  
**Restituisce**: dettagli della protezione
  
### <a name="getcontentid"></a>GetContentId
Ottiene l'identificatore univoco del documento/contenuto.

  
**Restituisce**: identificatore univoco del contenuto
  
### <a name="doesusedeprecatedalgorithms"></a>DoesUseDeprecatedAlgorithms
Ottiene un valore che indica se il gestore di protezione usa o meno algoritmi di crittografia deprecati per compatibilità con le versioni precedenti.

  
**Restituisce**: valore che indica se il gestore di protezione usa o meno algoritmi di crittografia deprecati
  
### <a name="isauditedextractallowed"></a>IsAuditedExtractAllowed
Ottiene un valore che indica se il gestore di protezione concede o meno all'utente il diritto 'audited extract'.

  
**Restituisce**: valore che indica se il gestore di protezione concede o meno all'utente il diritto 'audited extract'
  
### <a name="getserializedpublishinglicense"></a>GetSerializedPublishingLicense
Serializza [ProtectionHandler](class_mip_protectionhandler.md) in una licenza di pubblicazione

  
**Restituisce**: licenza di pubblicazione serializzata