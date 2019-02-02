---
title: Classe mip::ProtectionHandler
description: Documenta la classe mip::protectionhandler di Microsoft Information Protection (MIP) SDK.
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: 37358a2160c190978a21c491249dab42598d49b6
ms.sourcegitcommit: be05adc7750e22c110b261882de0389b9dfb2726
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/02/2019
ms.locfileid: "55651327"
---
# <a name="class-mipprotectionhandler"></a>Classe mip::ProtectionHandler 
Gestisce azioni correlate alla protezione per una configurazione di protezione specifica.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
Public std:: shared_ptr\<Stream\> CreateProtectedStream (const std:: shared_ptr\<Stream\>& backingStream, contentStartPosition int64_t, int64_t contentSize)  |  Crea un flusso protetto che consentirà la crittografia/decrittografia del contenuto.
public int64_t EncryptBuffer(int64_t offsetFromStart, const uint8_t* inputBuffer, int64_t inputBufferSize, uint8_t* outputBuffer, int64_t outputBufferSize, bool isFinal)  |  Crittografa un buffer.
public int64_t DecryptBuffer(int64_t offsetFromStart, const uint8_t* inputBuffer, int64_t inputBufferSize, uint8_t* outputBuffer, int64_t outputBufferSize, bool isFinal)  |  Decrittografa un buffer.
public int64_t GetProtectedContentLength(int64_t unprotectedLength, bool includesFinalBlock)  |  Calcola la dimensione (in byte) del contenuto se fosse da crittografare con questo [ProtectionHandler](class_mip_protectionhandler.md).
public int64_t GetBlockSize()  |  Ottiene la dimensione del blocco (in byte) per la modalità crittografia usata da questo [ProtectionHandler](class_mip_protectionhandler.md).
Public std:: Vector\<std:: String\> GetRights() const  |  Ottiene i diritti concessi all'utente/identità associata a questo [ProtectionHandler](class_mip_protectionhandler.md).
public bool AccessCheck(const std::string& right) const  |  Controlla se il gestore di protezione concede l'accesso utente al diritto specificato.
public const std::string GetIssuedTo()  |  Ottiene l'utente associato al gestore di protezione.
public const std::string GetOwner()  |  Ottiene indirizzo e-mail del proprietario del contenuto.
public bool IsIssuedToOwner()  |  Ottiene un valore che indica se l'utente corrente è o meno il proprietario del contenuto.
Public std:: shared_ptr\<ProtectionDescriptor\> GetProtectionDescriptor()  |  Ottiene i dettagli della protezione.
public const std::string GetContentId()  |  Ottiene l'identificatore univoco del documento/contenuto.
public bool DoesUseDeprecatedAlgorithms()  |  Ottiene un valore che indica se il gestore di protezione usa o meno algoritmi di crittografia deprecati per compatibilità con le versioni precedenti.
public bool IsAuditedExtractAllowed()  |  Ottiene un valore che indica se il gestore di protezione concede o meno all'utente il diritto 'audited extract'.
Public std:: Vector const\<uint8_t\> GetSerializedPublishingLicense()  |  Serializza [ProtectionHandler](class_mip_protectionhandler.md) in una licenza di pubblicazione
Public std:: Vector const\<uint8_t\> GetSerializedProtectionInfo()  |  Ottiene le informazioni di protezione.
  
## <a name="members"></a>Membri
  
### <a name="createprotectedstream-function"></a>CreateProtectedStream (funzione)
Crea un flusso protetto che consentirà la crittografia/decrittografia del contenuto.

Parametri:  
* **backingStream**: Il backup di flusso da cui lettura/scrittura 


* **contentStartPosition**: Posizione (in byte) iniziale all'interno del flusso sottostante in cui inizia il contenuto protetto 


* **contentSize**: Dimensioni (in byte) di contenuti protetti entro il backup di flusso



  
**Restituisce**: Flusso protetto
  
### <a name="encryptbuffer-function"></a>EncryptBuffer (funzione)
Crittografa un buffer.

Parametri:  
* **offsetFromStart**: Posizione relativa di inputBuffer sin dall'inizio del contenuto del testo non crittografato 


* **inputBuffer**: Buffer del contenuto di testo non crittografato da crittografare 


* **inputBufferSize**: Dimensioni (in byte) del buffer di input 


* **outputBuffer**: Buffer in cui verrà copiato il contenuto crittografato 


* **outputBufferSize**: Dimensioni (in byte) del buffer di output 


* **isFinal**: Se il buffer di input contiene i byte finale come testo non crittografato o meno



  
**Restituisce**: Dimensioni effettive (in byte) del contenuto crittografato
  
### <a name="decryptbuffer-function"></a>DecryptBuffer (funzione)
Decrittografa un buffer.

Parametri:  
* **offsetFromStart**: Posizione relativa di inputBuffer sin dall'inizio del contenuto crittografato 


* **inputBuffer**: Buffer di contenuto crittografato verrà decrittografato 


* **inputBufferSize**: Dimensioni (in byte) del buffer di input 


* **outputBuffer**: Buffer in cui verrà copiato il contenuto decrittografato 


* **outputBufferSize**: Dimensioni (in byte) del buffer di output 


* **isFinal**: Se il buffer di input contiene l'ultimi byte crittografati o meno



  
**Restituisce**: Dimensioni effettive (in byte) del contenuto decrittografato
  
### <a name="getprotectedcontentlength-function"></a>GetProtectedContentLength (funzione)
Calcola la dimensione (in byte) del contenuto se fosse da crittografare con questo [ProtectionHandler](class_mip_protectionhandler.md).

Parametri:  
* **unprotectedLength**: Dimensioni (in byte) del contenuto protetto 


* **includesFinalBlock**: Descrive se il contenuto protetto in questione include il blocco finale o meno. Ad esempio, in modalità di crittografia CBC4k, i blocchi protetti non finali hanno le stesse dimensioni di quelli non protetti, ma i blocchi protetti finali sono di dimensioni superiori rispetto ai corrispondenti non protetti.



  
**Restituisce**: Dimensioni (in byte) del contenuto protetto
  
### <a name="getblocksize-function"></a>GetBlockSize (funzione)
Ottiene la dimensione del blocco (in byte) per la modalità crittografia usata da questo [ProtectionHandler](class_mip_protectionhandler.md).

  
**Restituisce**: Dimensione del blocco (in byte)
  
### <a name="getrights-function"></a>GetRights (funzione)
Ottiene i diritti concessi all'utente/identità associata a questo [ProtectionHandler](class_mip_protectionhandler.md).

  
**Restituisce**: Autorizzazioni concesse all'utente
  
### <a name="accesscheck-function"></a>AccessCheck (funzione)
Controlla se il gestore di protezione concede l'accesso utente al diritto specificato.

Parametri:  
* **right**: Diritto da controllare



  
**Restituisce**: Se il gestore di protezione concede l'accesso utente specificato a destra o non
  
### <a name="getissuedto-function"></a>GetIssuedTo (funzione)
Ottiene l'utente associato al gestore di protezione.

  
**Restituisce**: Utente associato al gestore di protezione
  
### <a name="getowner-function"></a>GetOwner (funzione)
Ottiene indirizzo e-mail del proprietario del contenuto.

  
**Restituisce**: Indirizzo e-mail del proprietario del contenuto
  
### <a name="isissuedtoowner-function"></a>IsIssuedToOwner (funzione)
Ottiene un valore che indica se l'utente corrente è o meno il proprietario del contenuto.

  
**Restituisce**: Se l'utente corrente è il proprietario del contenuto o meno
  
### <a name="getprotectiondescriptor-function"></a>GetProtectionDescriptor (funzione)
Ottiene i dettagli della protezione.

  
**Restituisce**: Dettagli protezione
  
### <a name="getcontentid-function"></a>GetContentId (funzione)
Ottiene l'identificatore univoco del documento/contenuto.

  
**Restituisce**: Identificatore univoco del contenuto
  
### <a name="doesusedeprecatedalgorithms-function"></a>DoesUseDeprecatedAlgorithms (funzione)
Ottiene un valore che indica se il gestore di protezione usa o meno algoritmi di crittografia deprecati per compatibilità con le versioni precedenti.

  
**Restituisce**: Se utilizzata dal gestore di protezione di algoritmi di crittografia deprecati o non
  
### <a name="isauditedextractallowed-function"></a>IsAuditedExtractAllowed function
Ottiene un valore che indica se il gestore di protezione concede o meno all'utente il diritto 'audited extract'.

  
**Restituisce**: Se il gestore di protezione concede utente "audited extract", a destra o No
  
### <a name="getserializedpublishinglicense-function"></a>GetSerializedPublishingLicense (funzione)
Serializza [ProtectionHandler](class_mip_protectionhandler.md) in una licenza di pubblicazione

  
**Restituisce**: Licenza di pubblicazione serializzato
  
### <a name="getserializedprotectioninfo-function"></a>GetSerializedProtectionInfo function
Ottiene le informazioni di protezione.

  
**Restituisce**: Informazioni di protezione dati serializzati