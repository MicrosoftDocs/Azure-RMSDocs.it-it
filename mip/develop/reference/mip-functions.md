---
title: Classi
description: Funzioni
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.date: 01/28/2019
ms.author: mbaldwin
ms.openlocfilehash: 4479cd9419d51e841906e6268427e184d4e1b4d3
ms.sourcegitcommit: f5d8cf4440a35afaa1ff1a58b2a022740ed85ffd
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/04/2019
ms.locfileid: "73558009"
---
# <a name="functions"></a>Funzioni



## <a name="namespace-mip"></a>Spazio dei nomi MIP

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
public const std:: Map\<FlightingFeature, bool\>& GetDefaultFeatureSettings ()       |  Ottiene un valore che indica se una funzionalità è abilitata per impostazione predefinita.
public MIP_API std:: shared_ptr\<MIP:: Stream\> CreateStreamFromStdStream (const std:: shared_ptr\<std:: IStream\>& stdIStream)       |  Crea un flusso da un std:: IStream.
public MIP_API std:: shared_ptr\<MIP:: Stream\> CreateStreamFromStdStream (const std:: shared_ptr\<std:: ostream\>& stdOStream)       |  Crea un flusso da un oggetto std:: ostream.
public MIP_API std:: shared_ptr\<MIP:: Stream\> CreateStreamFromStdStream (const std:: shared_ptr\<std:: iostream\>& stdIOStream)       |  Crea un flusso da un oggetto std:: iostream.
public MIP_API std:: shared_ptr\<MIP:: Stream\> CreateStreamFromBuffer (uint8_t * buffer, const int64_t size)       |  Crea un flusso da un buffer.
public MIP_API std:: Vector\<uint8_t\> ReadFromStream (const std:: shared_ptr\<MIP:: Stream\>& Stream)       |  Leggere tutti i byte del flusso.
public ActionType operator & (ActionType a, ActionType b)       |  Operatore and (&) per il tipo di azione enum.
public ActionType operator ^ (ActionType a, ActionType b)       |  Operatore XOR (^) per l'enumerazione del tipo di azione.

### <a name="getassignmentmethodstring-function"></a>GetAssignmentMethodString (funzione)
Converte l'enumerazione AssignmentMethod in una descrizione di stringa.

Parametri:  
* **Metodo**: metodo di assegnazione. 



  
**Restituisce**: una descrizione di stringa del metodo di assegnazione.
  
### <a name="getactionsourcestring-function"></a>GetActionSourceString (funzione)
Ottenere il nome dell'origine dell'azione.

Parametri:  
* **actionSource**: origine dell'azione. 



  
**Returns**: rappresentazione di stringa dell'origine dell'azione.
  
### <a name="getdatastatestring-function"></a>GetDataStateString (funzione)
Ottenere il nome dello stato del contenuto.

Parametri:  
* **actionSource**: lo stato del contenuto su cui si sta lavorando. 



  
**Returns**: rappresentazione di stringa dello stato del contenuto.
  
### <a name="getcustomsettingpolicydataname-function"></a>GetCustomSettingPolicyDataName (funzione)
Nome dell'impostazione per specificare in modo esplicito i dati dei criteri.

  
**Restituisce**: chiave delle impostazioni personalizzate.
  
### <a name="getcustomsettingexportpolicyfilename-function"></a>GetCustomSettingExportPolicyFileName (funzione)
Nome dell'impostazione per specificare in modo esplicito il percorso del file in cui esportare i dati dei criteri di controllo del codice sorgente.

  
**Restituisce**: chiave delle impostazioni personalizzate.
  
### <a name="getcustomsettingsensitivitytypesdataname-function"></a>GetCustomSettingSensitivityTypesDataName (funzione)
Nome dell'impostazione per specificare in modo esplicito i dati di riservatezza.

  
**Restituisce**: chiave delle impostazioni personalizzate.
  
### <a name="getcustomsettingpolicydatafile-function"></a>GetCustomSettingPolicyDataFile (funzione)
Nome dell'impostazione per specificare in modo esplicito il percorso del file di dati dei criteri.

  
**Restituisce**: chiave delle impostazioni personalizzate.
  
### <a name="getcustomsettingsensitivitytypesdatafile-function"></a>GetCustomSettingSensitivityTypesDataFile (funzione)
Nome dell'impostazione per specificare in modo esplicito il percorso del file di dati dei tipi di riservatezza.

  
**Restituisce**: chiave delle impostazioni personalizzate.
  
### <a name="getcustomsettinglabelcustompropertiessyncenabled-function"></a>GetCustomSettingLabelCustomPropertiesSyncEnabled (funzione)
Nome dell'impostazione che consente di abilitare l'etichetta in base alle proprietà personalizzate e alle proprietà personalizzate tramite le funzionalità di etichetta.

  
**Restituisce**: chiave delle impostazioni personalizzate.
  
### <a name="getdefaultfeaturesettings-function"></a>GetDefaultFeatureSettings (funzione)
Ottiene un valore che indica se una funzionalità è abilitata per impostazione predefinita.

  
**Returns**: stato predefinito delle funzionalità di Flight
  
### <a name="createstreamfromstdstream-function"></a>CreateStreamFromStdStream (funzione)
Crea un flusso da un std:: IStream.

Parametri:  
* **stdIStream**: std::istream sottostante



  
**Restituisce**: flusso di wrapping di un std:: IStream
  
### <a name="createstreamfromstdstream-function"></a>CreateStreamFromStdStream (funzione)
Crea un flusso da un oggetto std:: ostream.

Parametri:  
* **stdOStream**: std::ostream sottostante



  
**Restituisce**: flusso di wrapping di un oggetto std:: ostream
  
### <a name="createstreamfromstdstream-function"></a>CreateStreamFromStdStream (funzione)
Crea un flusso da un oggetto std:: iostream.

Parametri:  
* **stdIOStream**: std::iostream sottostante



  
**Restituisce**: flusso di wrapping di un oggetto std:: iostream
  
### <a name="createstreamfrombuffer-function"></a>CreateStreamFromBuffer (funzione)
Crea un flusso da un buffer.

Parametri:  
* **buffer**: puntatore a un buffer



  
**Restituisce**: dimensioni del buffer
  
### <a name="readfromstream-function"></a>ReadFromStream (funzione)
Leggere tutti i byte del flusso.

Parametri:  
* **puntatore**: a un flusso.



  
**Restituisce**: un vettore di byte.
  
### <a name="operator-function"></a>operatore | funzione
Operatore OR (|) per il tipo di azione enum.
  
### <a name="operator-function"></a>operatore & funzione
Operatore and (&) per il tipo di azione enum.
  
### <a name="operator-function"></a>funzione operator ^
Operatore XOR (^) per l'enumerazione del tipo di azione.

## <a name="namespace-mipauditmetadatakeys"></a>spazio dei nomi MIP:: auditmetadatakeys

 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public std:: String sender ()       |  Controllare le chiavi dei metadati nella rappresentazione di stringa.
Destinatari std:: String pubblici ()       | Non ancora documentato.
public std:: String LastModifiedBy ()       | Non ancora documentato.
public std:: String LastModifiedDate ()       | Non ancora documentato.
  
### <a name="sender-function"></a>Funzione sender
Controllare le chiavi dei metadati nella rappresentazione di stringa.
  
### <a name="recipients-function"></a>Funzione Recipients
_Non ancora documentato._

  
### <a name="lastmodifiedby-function"></a>LastModifiedBy (funzione)
_Non ancora documentato._

  
### <a name="lastmodifieddate-function"></a>LastModifiedDate (funzione)
_Non ancora documentato._


## <a name="namespace-miprights"></a>`mip::rights` dello spazio dei nomi 
  
 Membri                        | Descrizioni                                
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
  

### <a name="owner-function"></a>Funzione Owner
Ottiene l'identificatore della stringa per il diritto "owner".

  
**Restituisce**: identificatore della stringa per il diritto "owner"
  
### <a name="view-function"></a>Funzione View
Ottiene l'identificatore della stringa per il diritto "view".

  
**Restituisce**: identificatore della stringa per il diritto "view"
  
### <a name="auditedextract-function"></a>AuditedExtract (funzione)
Ottiene l'identificatore della stringa per il diritto "audited extract".

  
**Restituisce**: identificatore della stringa per il diritto "audited extract"
  
### <a name="edit-function"></a>Modifica funzione
Ottiene l'identificatore della stringa per il diritto "edit".

  
**Restituisce**: identificatore della stringa per il diritto "edit"
  
### <a name="export-function"></a>Funzione Export
Ottiene l'identificatore della stringa per il diritto "export".

  
**Restituisce**: identificatore della stringa per il diritto "export"
  
### <a name="extract-function"></a>Estrai funzione
Ottiene l'identificatore della stringa per il diritto "extract".

  
**Restituisce**: identificatore della stringa per il diritto "extract"
  
### <a name="print-function"></a>Funzione Print
Ottiene l'identificatore della stringa per il diritto "print".

  
**Restituisce**: identificatore della stringa per il diritto "print"
  
### <a name="comment-function"></a>Funzione Comment
Ottiene l'identificatore della stringa per il diritto "comment".

  
**Restituisce**: identificatore della stringa per il diritto "comment"
  
### <a name="reply-function"></a>Funzione Reply
Ottiene l'identificatore della stringa per il diritto "reply".

  
**Restituisce**: identificatore della stringa per il diritto "reply"
  
### <a name="replyall-function"></a>ReplyAll (funzione)
Ottiene l'identificatore della stringa per il diritto "reply all".

  
**Restituisce**: identificatore della stringa per il diritto "reply all"
  
### <a name="forward-function"></a>Funzione di avanzamento
Ottiene l'identificatore della stringa per il diritto "forward".

  
**Restituisce**: identificatore della stringa per il diritto "forward"
  
### <a name="emailrights-function"></a>EmailRights (funzione)
Ottiene un elenco di diritti che si applicano ai messaggi di posta elettronica.

  
**Restituisce**: elenco di diritti che si applicano ai messaggi di posta elettronica
  
### <a name="editabledocumentrights-function"></a>EditableDocumentRights (funzione)
Ottiene un elenco di diritti che si applicano ai documenti.

  
**Restituisce**: elenco di diritti che si applicano ai documenti
  
### <a name="commonrights-function"></a>CommonRights (funzione)
Ottiene un elenco di diritti che si applicano in tutti gli scenari.

  
**Restituisce**: elenco di diritti che si applicano in tutti gli scenari

## <a name="namespace-miproles"></a>spazio dei nomi MIP:: Roles
  
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public std::string Viewer()       |  Ottiene l'identificatore della stringa per il ruolo "viewer".
public std::string Reviewer()       |  Ottiene l'identificatore della stringa per il ruolo "reviewer".
public std::string Author()       |  Ottiene l'identificatore della stringa per il ruolo "author".
public std::string CoOwner()       |  Ottiene l'identificatore della stringa per il ruolo "co-owner".
  
### <a name="viewer-function"></a>Funzione Viewer
Ottiene l'identificatore della stringa per il ruolo "viewer".

  
**Restituisce**: identificatore della stringa per il ruolo "viewer". Un visualizzatore può solo visualizzare il contenuto. Non può modificarlo, copiarlo o stamparlo.
  
### <a name="reviewer-function"></a>Revisore (funzione)
Ottiene l'identificatore della stringa per il ruolo "reviewer".

  
**Restituisce**: identificatore della stringa per il ruolo "reviewer". Un revisore può visualizzare e modificare il contenuto. Non può copiarlo o stamparlo.
  
### <a name="author-function"></a>Author (funzione)
Ottiene l'identificatore della stringa per il ruolo "author".

  
**Restituisce**: identificatore della stringa per il ruolo "author". Un autore può visualizzare, modificare, copiare e stampare il contenuto.
  
### <a name="coowner-function"></a>Funzione CoOwner
Ottiene l'identificatore della stringa per il ruolo "co-owner".

  
**Restituisce**: identificatore della stringa per il ruolo "co-owner". Un comproprietario ha tutte le autorizzazioni

