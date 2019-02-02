---
title: Funzioni
description: Funzioni
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 01/28/2019
ms.author: bryanla
ms.openlocfilehash: ab176e53547ebb773b7cf8b3933fddfc1566d62b
ms.sourcegitcommit: be05adc7750e22c110b261882de0389b9dfb2726
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/02/2019
ms.locfileid: "55651191"
---
# <a name="functions"></a>Funzioni

## <a name="summary"></a>Riepilogo

| Funzioni di base all'ambito dello spazio dei nomi   | Descrizioni                                |
|--------------------------------|---------------------------------------------|
**Namespace `mip` :** |
Public std:: String GetAssignmentMethodString (AssignmentMethod metodo)       |  Converte una stringa descrittiva AssignmentMethod enum.
pubblico statico std:: String GetActionSourceString (ActionSource actionSource)       |  Ottenere il nome di origine di azione.
pubblico statico std:: String GetContentStateString (mip::ContentState stato)       |  Ottiene il nome dello stato del contenuto.
public const std::string& GetCustomSettingPolicyDataName()       |  Nome dell'impostazione per specificare in modo esplicito i dati dei criteri.
public const std::string& GetCustomSettingExportPolicyFileName()       |  Nome dell'impostazione per specificare in modo esplicito il percorso del file in cui esportare i dati dei criteri di controllo del codice sorgente.
Public std:: String const & GetCustomSettingSensitivityTypesDataName()       |  Nome dell'impostazione per specificare in modo esplicito i dati tra maiuscole e minuscole.
public const std::string& GetCustomSettingPolicyDataFile()       |  Nome dell'impostazione per specificare in modo esplicito il percorso del file di dati dei criteri.
Public std:: String const & GetCustomSettingSensitivityTypesDataFile()       |  Nome dell'impostazione di sensibilità di specificare in modo esplicito i tipi di percorso file di dati.
pubblica cdecl void MIP_API ReleaseAllResources()       |  Rilascia tutte le risorse (thread e così via) prima dell'arresto.
Public std:: shared_ptr MIP_API\<MIP:: Stream\> CreateStreamFromStdStream (const std:: shared_ptr\<std::istream\>& stdIStream)       |  Crea un [flusso](class_mip_stream.md) da std::istream.
Public std:: shared_ptr MIP_API\<MIP:: Stream\> CreateStreamFromStdStream (const std:: shared_ptr\<std::ostream\>& stdOStream)       |  Crea un [flusso](class_mip_stream.md) da std::ostream.
Public std:: shared_ptr MIP_API\<MIP:: Stream\> CreateStreamFromStdStream (const std:: shared_ptr\<std::iostream\>& stdIOStream)       |  Crea un [flusso](class_mip_stream.md) da std::iostream.
Public std:: shared_ptr MIP_API\<MIP:: Stream\> CreateStreamFromBuffer (buffer uint8_t *, const int64_t dimensioni)       |  Crea un [flusso](class_mip_stream.md) da un buffer.
 | 
**Namespace `mip::auditmetadatakeys` :** |
Public std:: String Sender()       |  Controllare le chiavi di metadati nella rappresentazione di stringa.
Public std:: String Recipients()       | _Non ancora documentato._
Public std:: String LastModifiedBy()       | _Non ancora documentato._
Public std:: String LastModifiedDate()       | _Non ancora documentato._
 | 
**Namespace `mip::rights` :** |
public std::string Owner()       |  Ottiene l'identificatore della stringa per il diritto "owner".
public std::string View()       |  Ottiene l'identificatore della stringa per il diritto "view".
public std::string AuditedExtract()       |  Ottiene l'identificatore della stringa per il diritto "audited extract".
public std::string Edit()       |  Ottiene l'identificatore della stringa per il diritto "edit".
public std::string Export()       |  Ottiene l'identificatore della stringa per il diritto "export".
public std::string Extract()       |  Ottiene l'identificatore della stringa per il diritto "extract".
public std::string Print()       |  Ottiene l'identificatore della stringa per il diritto "print".
public std::string Comment()       |  Ottiene l'identificatore della stringa per il diritto "comment".
public std::string Reply()       |  Ottiene l'identificatore della stringa per il diritto "reply".
public std::string ReplyAll()       |  Ottiene l'identificatore della stringa per il diritto "reply all".
public std::string Forward()       |  Ottiene l'identificatore della stringa per il diritto "forward".
Public std:: Vector\<std:: String\> EmailRights()       |  Ottiene un elenco di diritti che si applicano ai messaggi di posta elettronica.
Public std:: Vector\<std:: String\> EditableDocumentRights()       |  Ottiene un elenco di diritti che si applicano ai documenti.
Public std:: Vector\<std:: String\> CommonRights()       |  Ottiene un elenco di diritti che si applicano in tutti gli scenari.
 | 
**Namespace `mip::roles` :** |
public std::string Viewer()       |  Ottiene l'identificatore della stringa per il ruolo "viewer".
public std::string Reviewer()       |  Ottiene l'identificatore della stringa per il ruolo "reviewer".
public std::string Author()       |  Ottiene l'identificatore della stringa per il ruolo "author".
public std::string CoOwner()       |  Ottiene l'identificatore della stringa per il ruolo "co-owner".



## <a name="namespace-mip"></a>Namespace `mip`

### <a name="getassignmentmethodstring-function"></a>GetAssignmentMethodString (funzione)
Converte una stringa descrittiva AssignmentMethod enum.

Parametri:  
* **metodo**: un metodo di assegnazione. 



  
**Restituisce**: Una stringa descrittiva del metodo di assegnazione.
  
### <a name="getactionsourcestring-function"></a>GetActionSourceString (funzione)
Ottenere il nome di origine di azione.

Parametri:  
* **actionSource**: L'origine di azione. 



  
**Restituisce**: Rappresentazione di stringa dell'origine dell'azione.
  
### <a name="getcontentstatestring-function"></a>GetContentStateString (funzione)
Ottiene il nome dello stato del contenuto.

Parametri:  
* **actionSource**: Lo stato del contenuto in fase di elaborazione al momento. 



  
**Restituisce**: Rappresentazione di stringa dello stato del contenuto.
  
### <a name="getcustomsettingpolicydataname-function"></a>GetCustomSettingPolicyDataName (funzione)
Nome dell'impostazione per specificare in modo esplicito i dati dei criteri.

  
**Restituisce**: La chiave delle impostazioni personalizzate.
  
### <a name="getcustomsettingexportpolicyfilename-function"></a>GetCustomSettingExportPolicyFileName (funzione)
Nome dell'impostazione per specificare in modo esplicito il percorso del file in cui esportare i dati dei criteri di controllo del codice sorgente.

  
**Restituisce**: La chiave delle impostazioni personalizzate.
  
### <a name="getcustomsettingsensitivitytypesdataname-function"></a>GetCustomSettingSensitivityTypesDataName (funzione)
Nome dell'impostazione per specificare in modo esplicito i dati tra maiuscole e minuscole.

  
**Restituisce**: La chiave delle impostazioni personalizzate.
  
### <a name="getcustomsettingpolicydatafile-function"></a>GetCustomSettingPolicyDataFile (funzione)
Nome dell'impostazione per specificare in modo esplicito il percorso del file di dati dei criteri.

  
**Restituisce**: La chiave delle impostazioni personalizzate.
  
### <a name="getcustomsettingsensitivitytypesdatafile-function"></a>GetCustomSettingSensitivityTypesDataFile (funzione)
Nome dell'impostazione di sensibilità di specificare in modo esplicito i tipi di percorso file di dati.

  
**Restituisce**: La chiave delle impostazioni personalizzate.
  
### <a name="releaseallresources-function"></a>ReleaseAllResources (funzione)
Rilascia tutte le risorse (thread e così via) prima dell'arresto.
Se le librerie dinamiche MIP sono a caricamento ritardato da un'applicazione, questa funzione deve essere chiamata prima che l'applicazione scarichi in modo esplicito tali librerie MIP per evitare deadlock. Ad esempio, in win32, questa funzione deve essere chiamata prima delle chiamate a esplicitamente scaricamento DLL MIP tramite FreeLibrary o FUnloadDelayLoadedDLL2. Le applicazioni devono rilasciare i riferimenti a tutti gli oggetti MIP (ad esempio, profili, motori, gestori) prima di chiamare questa funzione.
  
### <a name="operator-function"></a>operatore | (funzione)
Operatore OR bit per bit ProtectionHandlerCreationOptions.

Parametri:  
* **a**: Valore a sinistra 


* **b**: Valore a destra



  
**Restituisce**: OR bit per bit di ProtectionHandlerCreationOptions
  
### <a name="createstreamfromstdstream-function"></a>CreateStreamFromStdStream (funzione)
Crea un [flusso](class_mip_stream.md) da std::istream.

Parametri:  
* **stdIStream**: Il backup std::istream



  
**Restituisce**: [Stream](class_mip_stream.md) wrapping un std::istream
  
### <a name="createstreamfromstdstream-function"></a>CreateStreamFromStdStream (funzione)
Crea un [flusso](class_mip_stream.md) da std::ostream.

Parametri:  
* **stdOStream**: Il backup std::ostream



  
**Restituisce**: [Stream](class_mip_stream.md) wrapping un std::ostream
  
### <a name="createstreamfromstdstream-function"></a>CreateStreamFromStdStream (funzione)
Crea un [flusso](class_mip_stream.md) da std::iostream.

Parametri:  
* **stdIOStream**: Il backup std::iostream



  
**Restituisce**: [Stream](class_mip_stream.md) wrapping un std::iostream
  
### <a name="createstreamfrombuffer-function"></a>CreateStreamFromBuffer (funzione)
Crea un [flusso](class_mip_stream.md) da un buffer.

Parametri:  
* **buffer**: Puntatore a un buffer



  
**Restituisce**: Dimensione delle dimensioni del buffer
  



## <a name="namespace-mipauditmetadatakeys"></a>Namespace `mip::auditmetadatakeys`

### <a name="sender-function"></a>Funzione mittente
Controllare le chiavi di metadati nella rappresentazione di stringa.
  
### <a name="recipients-function"></a>Funzione di destinatari
_Non ancora documentato._

  
### <a name="lastmodifiedby-function"></a>LastModifiedBy (funzione)
_Non ancora documentato._
  
### <a name="lastmodifieddate-function"></a>Funzione LastModifiedDate & lt
_Non ancora documentato._





## <a name="namespace-miprights"></a>Namespace `mip::rights`

### <a name="owner-function"></a>Funzione proprietario
Ottiene l'identificatore della stringa per il diritto "owner".

  
**Restituisce**: Identificatore di stringa per 'owner' a destra
  
### <a name="view-function"></a>Visualizzazione (funzione)
Ottiene l'identificatore della stringa per il diritto "view".

  
**Restituisce**: A destra della stringa identificatore 'view'
  
### <a name="auditedextract-function"></a>AuditedExtract (funzione)
Ottiene l'identificatore della stringa per il diritto "audited extract".

  
**Restituisce**: A destra della stringa identificatore "audited extract"
  
### <a name="edit-function"></a>Modifica funzione
Ottiene l'identificatore della stringa per il diritto "edit".

  
**Restituisce**: Identificatore di stringa per 'modifica' destra
  
### <a name="export-function"></a>Funzione di esportazione
Ottiene l'identificatore della stringa per il diritto "export".

  
**Restituisce**: Identificatore per 'export' a destra della stringa
  
### <a name="extract-function"></a>Estrai funzione
Ottiene l'identificatore della stringa per il diritto "extract".

  
**Restituisce**: Identificatore di stringa per 'estrarre' destra
  
### <a name="print-function"></a>Funzione di stampa
Ottiene l'identificatore della stringa per il diritto "print".

  
**Restituisce**: Identificatore di stringa per "stampa" a destra
  
### <a name="comment-function"></a>Funzione di commento
Ottiene l'identificatore della stringa per il diritto "comment".

  
**Restituisce**: A destra della stringa identificatore 'comment'
  
### <a name="reply-function"></a>Funzione di risposta
Ottiene l'identificatore della stringa per il diritto "reply".

  
**Restituisce**: Identificatore di stringa per "Rispondi" a destra
  
### <a name="replyall-function"></a>Funzione ReplyAll
Ottiene l'identificatore della stringa per il diritto "reply all".

  
**Restituisce**: Identificatore di stringa per "Rispondi a tutti" a destra
  
### <a name="forward-function"></a>Funzione di inoltro
Ottiene l'identificatore della stringa per il diritto "forward".

  
**Restituisce**: Identificatore di stringa per il diritto 'Avanti'
  
### <a name="emailrights-function"></a>Funzione EmailRights
Ottiene un elenco di diritti che si applicano ai messaggi di posta elettronica.

  
**Restituisce**: Un elenco di diritti che si applicano a messaggi di posta elettronica
  
### <a name="editabledocumentrights-function"></a>Funzione EditableDocumentRights
Ottiene un elenco di diritti che si applicano ai documenti.

  
**Restituisce**: Un elenco di diritti che si applicano ai documenti
  
### <a name="commonrights-function"></a>Funzione CommonRights
Ottiene un elenco di diritti che si applicano in tutti gli scenari.

  
**Restituisce**: Un elenco di diritti che si applicano in tutti gli scenari




## <a name="namespace-miproles"></a>Namespace `mip::roles`

### <a name="viewer-function"></a>Funzione del Visualizzatore
Ottiene l'identificatore della stringa per il ruolo "viewer".

  
**Restituisce**: Identificatore di stringa per il ruolo di "Visualizzatore" un visualizzatore può solo visualizzare il contenuto. Non può modificarlo, copiarlo o stamparlo.
  
### <a name="reviewer-function"></a>Funzione revisore
Ottiene l'identificatore della stringa per il ruolo "reviewer".

  
**Restituisce**: Identificatore di stringa per il ruolo 'revisore' un revisore può visualizzare e modificare il contenuto. Non può copiarlo o stamparlo.
  
### <a name="author-function"></a>Funzione autore
Ottiene l'identificatore della stringa per il ruolo "author".

  
**Restituisce**: Identificatore per il ruolo "author" un autore può visualizzare, modificare, copiare e stampare il contenuto della stringa.
  
### <a name="coowner-function"></a>Funzione coOwner
Ottiene l'identificatore della stringa per il ruolo "co-owner".

  
**Restituisce**: Identificatore di stringa per il ruolo 'Comproprietario' Comproprietario ha tutte le autorizzazioni
