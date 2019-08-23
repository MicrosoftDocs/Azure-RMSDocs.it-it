---
title: Funzioni
description: Funzioni
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.date: 01/28/2019
ms.author: mbaldwin
ms.openlocfilehash: 80d13de3778648c2e0230ac37c559b0ca1f62a07
ms.sourcegitcommit: fcde8b31f8685023f002044d3a1d1903e548d207
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/21/2019
ms.locfileid: "69882815"
---
# <a name="functions"></a>Funzioni

## <a name="summary"></a>Riepilogo 

### <a name="namespace-mip"></a>Spazio dei nomi MIP
| Funzioni per ambito spazio dei nomi   | Descrizioni                                |
|--------------------------------|---------------------------------------------|
public std:: String GetAssignmentMethodString (metodo AssignmentMethod)       |  Converte l'enumerazione AssignmentMethod in una descrizione di stringa.
public static std:: String GetActionSourceString (ActionSource actionSource)       |  Ottenere il nome dell'origine dell'azione.
public static std:: String GetDataStateString (MIP::D ataState state)       |  Ottenere il nome dello stato del contenuto.
public const std::string& GetCustomSettingPolicyDataName()       |  Nome dell'impostazione per specificare in modo esplicito i dati dei criteri.
public const std::string& GetCustomSettingExportPolicyFileName()       |  Nome dell'impostazione per specificare in modo esplicito il percorso del file in cui esportare i dati dei criteri di controllo del codice sorgente.
public const std:: String & GetCustomSettingSensitivityTypesDataName ()       |  Nome dell'impostazione per specificare in modo esplicito i dati di riservatezza.
public const std::string& GetCustomSettingPolicyDataFile()       |  Nome dell'impostazione per specificare in modo esplicito il percorso del file di dati dei criteri.
public const std:: String & GetCustomSettingSensitivityTypesDataFile ()       |  Nome dell'impostazione per specificare in modo esplicito il percorso del file di dati dei tipi di riservatezza.
public const std:: String & GetCustomSettingLabelCustomPropertiesSyncEnabled ()       |  Nome dell'impostazione che consente di abilitare l'etichetta in base alle proprietà personalizzate e alle proprietà personalizzate tramite le funzionalità di etichetta.
public const std::\<map FlightingFeature,\>bool & GetDefaultFeatureSettings ()       |  Ottiene un valore che indica se una funzionalità è abilitata per impostazione predefinita.
public MIP_API void __CDECL ReleaseAllResources ()       |  Rilascia tutte le risorse (thread e così via) prima dell'arresto.
public MIP_API std:: shared_ptr\<MIP:: Stream\> CreateStreamFromStdStream (const std::\<shared_ptr std::\>IStream & stdIStream)       |  Crea un [flusso](class_mip_stream.md) da std::istream.
public MIP_API std:: shared_ptr\<MIP:: Stream\> CreateStreamFromStdStream (const std::\<shared_ptr std::\>ostream & stdOStream)       |  Crea un [flusso](class_mip_stream.md) da std::ostream.
public MIP_API std:: shared_ptr\<MIP:: Stream\> CreateStreamFromStdStream (const std::\<shared_ptr std::\>iostream & stdIOStream)       |  Crea un [flusso](class_mip_stream.md) da std::iostream.
public MIP_API std:: shared_ptr\<MIP:: Stream\> CreateStreamFromBuffer (uint8_t * buffer, const int64_t size)       |  Crea un [flusso](class_mip_stream.md) da un buffer.
public MIP_API std:: Vector\<uint8_t\> ReadFromStream (const std::\<shared_ptr MIP::\>Stream & Stream)       |  Leggere tutti i byte del flusso.

### <a name="namespace-mipauditmetadatakeys"></a>Spazio dei nomi MIP:: auditmetadatakeys
 Members                        | Descrizioni                                
--------------------------------|---------------------------------------------
public std:: String sender ()       |  Controllare le chiavi dei metadati nella rappresentazione di stringa.
Destinatari std:: String pubblici ()       | _Non ancora documentato._
public std:: String LastModifiedBy ()       | _Non ancora documentato._
public std:: String LastModifiedDate ()       | _Non ancora documentato._


### <a name="namespace-miprights"></a>Spazio dei nomi MIP:: Rights

 Members                        | Descrizioni                                
--------------------------------|---------------------------------------------
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
public std:: Vector\<std:: String\> EmailRights ()       |  Ottiene un elenco di diritti che si applicano ai messaggi di posta elettronica.
public std:: Vector\<std:: String\> EditableDocumentRights ()       |  Ottiene un elenco di diritti che si applicano ai documenti.
public std:: Vector\<std:: String\> CommonRights ()       |  Ottiene un elenco di diritti che si applicano in tutti gli scenari.

### <a name="namespace-miproles"></a>Spazio dei nomi MIP:: Roles

 Members                        | Descrizioni                                
--------------------------------|---------------------------------------------
public std::string Viewer()       |  Ottiene l'identificatore della stringa per il ruolo "viewer".
public std::string Reviewer()       |  Ottiene l'identificatore della stringa per il ruolo "reviewer".
public std::string Author()       |  Ottiene l'identificatore della stringa per il ruolo "author".
public std::string CoOwner()       |  Ottiene l'identificatore della stringa per il ruolo "co-owner".

## <a name="namespace-mip"></a>Spazio dei nomi MIP

### <a name="getassignmentmethodstring-function"></a>GetAssignmentMethodString (funzione)
Converte l'enumerazione AssignmentMethod in una descrizione di stringa.

Parametri:  
* **Metodo**: metodo di assegnazione. 



  
**Restituisce**: Descrizione della stringa del metodo di assegnazione.
  
### <a name="getactionsourcestring-function"></a>GetActionSourceString (funzione)
Ottenere il nome dell'origine dell'azione.

Parametri:  
* **actionSource**: Origine dell'azione. 



  
**Restituisce**: Rappresentazione di stringa dell'origine dell'azione.
  
### <a name="getdatastatestring-function"></a>GetDataStateString (funzione)
Ottenere il nome dello stato del contenuto.

Parametri:  
* **actionSource**: Stato del contenuto su cui si sta lavorando. 



  
**Restituisce**: Rappresentazione di stringa dello stato del contenuto.
  
### <a name="getcustomsettingpolicydataname-function"></a>GetCustomSettingPolicyDataName (funzione)
Nome dell'impostazione per specificare in modo esplicito i dati dei criteri.

  
**Restituisce**: Chiave delle impostazioni personalizzate.
  
### <a name="getcustomsettingexportpolicyfilename-function"></a>GetCustomSettingExportPolicyFileName (funzione)
Nome dell'impostazione per specificare in modo esplicito il percorso del file in cui esportare i dati dei criteri di controllo del codice sorgente.

  
**Restituisce**: Chiave delle impostazioni personalizzate.
  
### <a name="getcustomsettingsensitivitytypesdataname-function"></a>GetCustomSettingSensitivityTypesDataName (funzione)
Nome dell'impostazione per specificare in modo esplicito i dati di riservatezza.

  
**Restituisce**: Chiave delle impostazioni personalizzate.
  
### <a name="getcustomsettingpolicydatafile-function"></a>GetCustomSettingPolicyDataFile (funzione)
Nome dell'impostazione per specificare in modo esplicito il percorso del file di dati dei criteri.

  
**Restituisce**: Chiave delle impostazioni personalizzate.
  
### <a name="getcustomsettingsensitivitytypesdatafile-function"></a>GetCustomSettingSensitivityTypesDataFile (funzione)
Nome dell'impostazione per specificare in modo esplicito il percorso del file di dati dei tipi di riservatezza.

  
**Restituisce**: Chiave delle impostazioni personalizzate.
  
### <a name="getcustomsettingexternallabelsenabled-function"></a>GetCustomSettingExternalLabelsEnabled (funzione)
Nome dell'impostazione che consente di abilitare la funzionalità "etichette esterne".

  
**Restituisce**: Chiave delle impostazioni personalizzate.
  
### <a name="releaseallresources-function"></a>ReleaseAllResources (funzione)
Rilascia tutte le risorse (thread e così via) prima dell'arresto.
Questa funzione deve essere chiamata esattamente una volta prima della terminazione del processo. Fornisce al MIP la possibilità di annullare l'inizializzazione in un momento in cui è ancora garantita la possibilità di caricare le librerie dipendenti e il join dei thread è ancora possibile. Le applicazioni devono rilasciare i riferimenti a tutti gli oggetti MIP (ad esempio, profili, motori, gestori) prima di chiamare questa funzione.
Se questa funzione non viene chiamata, MIP verrà naturalmente scaricato come parte del processo standard teardown. In alcune piattaforme, questo può causare un deadlock (ad esempio, i thread non possono essere aggiunti a Win32 in risposta al processo teardown) o arresti anomali (ad esempio, l'ordine di scaricamento della DLL per le librerie a caricamento ritardato in Win32 non è controllato da MIP, quindi le librerie dipendenti possono sono stati scaricati dal momento in cui viene eseguito il codice di arresto MIP, causando errori di lettura non validi.
  
### <a name="createstreamfromstdstream-function"></a>CreateStreamFromStdStream (funzione)
Crea un [flusso](class_mip_stream.md) da std::istream.

Parametri:  
* **stdIStream**: Backup di STD:: IStream



  
**Restituisce**: Wrapping di un [flusso](class_mip_stream.md) std:: IStream
  
### <a name="createstreamfromstdstream-function"></a>CreateStreamFromStdStream (funzione)
Crea un [flusso](class_mip_stream.md) da std::ostream.

Parametri:  
* **stdOStream**: Supporto di STD:: ostream



  
**Restituisce**: [Flusso](class_mip_stream.md) di wrapping di un oggetto std:: ostream
  
### <a name="createstreamfromstdstream-function"></a>CreateStreamFromStdStream (funzione)
Crea un [flusso](class_mip_stream.md) da std::iostream.

Parametri:  
* **stdIOStream**: Supporto di STD:: iostream



  
**Restituisce**: [Flusso](class_mip_stream.md) di wrapping di un oggetto std:: iostream
  
### <a name="createstreamfrombuffer-function"></a>CreateStreamFromBuffer (funzione)
Crea un [flusso](class_mip_stream.md) da un buffer.

Parametri:  
* **buffer**: Puntatore a un buffer



  
**Restituisce**: Dimensioni dimensione del buffer
  



## <a name="namespace-mipauditmetadatakeys"></a>Spazio dei nomi MIP:: auditmetadatakeys

### <a name="sender-function"></a>Funzione sender
Controllare le chiavi dei metadati nella rappresentazione di stringa.
  
### <a name="recipients-function"></a>Funzione Recipients
_Non ancora documentato._

  
### <a name="lastmodifiedby-function"></a>LastModifiedBy (funzione)
_Non ancora documentato._

  
### <a name="lastmodifieddate-function"></a>LastModifiedDate (funzione)
_Non ancora documentato._






## <a name="namespace-miprights"></a>Spazio dei nomi MIP:: Rights

### <a name="owner-function"></a>Funzione Owner
Ottiene l'identificatore della stringa per il diritto "owner".

  
**Restituisce**: Identificatore di stringa per il diritto ' Owner '
  
### <a name="view-function"></a>Funzione View
Ottiene l'identificatore della stringa per il diritto "view".

  
**Restituisce**: Identificatore di stringa per "View" Right
  
### <a name="auditedextract-function"></a>AuditedExtract (funzione)
Ottiene l'identificatore della stringa per il diritto "audited extract".

  
**Restituisce**: Identificatore di stringa per "controllo Estratto" a destra
  
### <a name="edit-function"></a>Modifica funzione
Ottiene l'identificatore della stringa per il diritto "edit".

  
**Restituisce**: Identificatore di stringa per il diritto ' Edit '
  
### <a name="export-function"></a>Funzione Export
Ottiene l'identificatore della stringa per il diritto "export".

  
**Restituisce**: Identificatore di stringa per ' export ' a destra
  
### <a name="extract-function"></a>Estrai funzione
Ottiene l'identificatore della stringa per il diritto "extract".

  
**Restituisce**: Identificatore di stringa per ' Extract ' a destra
  
### <a name="print-function"></a>Funzione Print
Ottiene l'identificatore della stringa per il diritto "print".

  
**Restituisce**: Identificatore di stringa per "Print" Right
  
### <a name="comment-function"></a>Funzione Comment
Ottiene l'identificatore della stringa per il diritto "comment".

  
**Restituisce**: Identificatore di stringa per il diritto ' comment '
  
### <a name="reply-function"></a>Funzione Reply
Ottiene l'identificatore della stringa per il diritto "reply".

  
**Restituisce**: Identificatore di stringa per "Reply" Right
  
### <a name="replyall-function"></a>ReplyAll (funzione)
Ottiene l'identificatore della stringa per il diritto "reply all".

  
**Restituisce**: Identificatore di stringa per il diritto ' Rispondi a tutti '
  
### <a name="forward-function"></a>Funzione di avanzamento
Ottiene l'identificatore della stringa per il diritto "forward".

  
**Restituisce**: Identificatore di stringa per il diritto ' inoltr '
  
### <a name="emailrights-function"></a>EmailRights (funzione)
Ottiene un elenco di diritti che si applicano ai messaggi di posta elettronica.

  
**Restituisce**: Elenco dei diritti che si applicano ai messaggi di posta elettronica
  
### <a name="editabledocumentrights-function"></a>EditableDocumentRights (funzione)
Ottiene un elenco di diritti che si applicano ai documenti.

  
**Restituisce**: Elenco di diritti che si applicano ai documenti
  
### <a name="commonrights-function"></a>CommonRights (funzione)
Ottiene un elenco di diritti che si applicano in tutti gli scenari.

  
**Restituisce**: Elenco di diritti che si applicano a tutti gli scenari


## <a name="namespace-miproles"></a>Spazio dei nomi MIP:: Roles

### <a name="viewer-function"></a>Funzione Viewer
Ottiene l'identificatore della stringa per il ruolo "viewer".

  
**Restituisce**: Identificatore di stringa per il ruolo ' Viewer ' un visualizzatore può solo visualizzare il contenuto. Non può modificarlo, copiarlo o stamparlo.
  
### <a name="reviewer-function"></a>Revisore (funzione)
Ottiene l'identificatore della stringa per il ruolo "reviewer".

  
**Restituisce**: Identificatore di stringa per il ruolo "revisore" un revisore può visualizzare e modificare il contenuto. Non può copiarlo o stamparlo.
  
### <a name="author-function"></a>Author (funzione)
Ottiene l'identificatore della stringa per il ruolo "author".

  
**Restituisce**: Identificatore di stringa per il ruolo "autore". l'autore può visualizzare, modificare, copiare e stampare il contenuto.
  
### <a name="coowner-function"></a>Funzione CoOwner
Ottiene l'identificatore della stringa per il ruolo "co-owner".

  
**Restituisce**: Identificatore di stringa per il ruolo "comproprietario" un comproprietario dispone di tutte le autorizzazioni