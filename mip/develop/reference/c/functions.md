---
title: Funzioni
description: Funzioni.
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 4/16/2020
ms.openlocfilehash: 12aa46260b9c1ed2bac5f1e02c1e358292e86835
ms.sourcegitcommit: dc50f9a6c2f66544893278a7fd16dff38eef88c6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2020
ms.locfileid: "88564382"
---
# <a name="functions-c"></a>Funzioni (C)

## <a name="mip_cc_auth_callback"></a>mip_cc_auth_callback

definizione della funzione di callback per l'acquisizione del token OAuth2

**Parameters**

Parametro | Descrizione
|---|---|
| identity | Indirizzo di posta elettronica per il quale verrà acquisito il token |
| challenge | OAuth2 Challenge |
| contesto | Contesto dell'applicazione opaco passato all'API MIP che ha generato questo callback di autenticazione |
| tokenBuffer | Output Buffer in cui verrà copiato il token. Se null,' actualTokenSize ' verrà popolato, ma |
| tokenBufferSize | Dimensioni (in byte) del buffer di output |
| actualTokenSize | Output Dimensioni effettive (in byte) del token |

**Return**: true è il token recuperato. else false

```c
MIP_CC_CALLBACK(mip_cc_auth_callback,
    bool,
    const mip_cc_identity*,
    const mip_cc_oauth2_challenge*,
    const void*,
    uint8_t*,
    const int64_t,
    int64_t*);
```

## <a name="mip_cc_consent_callback"></a>mip_cc_consent_callback

definizione della funzione di callback per il consenso dell'utente per l'accesso all'endpoint del servizio esterno

**Parameters**

Parametro | Descrizione
|---|---|
| url | URL per cui l'SDK richiede il consenso dell'utente |

**Return**: risposta di consenso dell'utente

```c
MIP_CC_CALLBACK(mip_cc_consent_callback,
    mip_cc_consent,
    const char*);
```

## <a name="mip_cc_createdictionary"></a>MIP_CC_CreateDictionary

Creare un dizionario di chiavi/valori stringa

**Parameters**

Parametro | Descrizione
|---|---|
| entries | Matrice di coppie chiave/valore |
| count | Numero di coppie chiave/valore |
| dictionary | Output Dizionario appena creato |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

**Nota**: è necessario liberare un mip_cc_dictionary chiamando MIP_CC_ReleaseDictionary 

```c
mip_cc_result MIP_CC_CreateDictionary(
    const mip_cc_kv_pair* entries,
    const int64_t count,
    mip_cc_dictionary* dictionary,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_dictionary_getentries"></a>MIP_CC_Dictionary_GetEntries

Ottenere le coppie chiave/valore che compongono un dizionario

**Parameters**

Parametro | Descrizione
|---|---|
| dictionary | Dizionario di origine |
| entries | Output Matrice di coppie chiave/valore, memoria di proprietà dell'oggetto mip_cc_dictionary |
| count | Output Numero di coppie chiave/valore |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

**Nota**: la memoria per ' voci ' è di proprietà dell'oggetto mip_cc_dictionary, quindi non deve essere liberata in modo indipendente 

```c
mip_cc_result MIP_CC_Dictionary_GetEntries(
    const mip_cc_dictionary dictionary,
    mip_cc_kv_pair** entries,
    int64_t* count,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_releasedictionary"></a>MIP_CC_ReleaseDictionary

Rilasciare le risorse associate a un dizionario

**Parameters**

Parametro | Descrizione
|---|---|
| dictionary | Dizionario da rilasciare |

```c
void MIP_CC_ReleaseDictionary(mip_cc_dictionary dictionary);
```

## <a name="mip_cc_http_send_callback_fn"></a>mip_cc_http_send_callback_fn

Definizione della funzione di callback per l'emissione di una richiesta HTTP

**Parameters**

Parametro | Descrizione
|---|---|
| richiesta | Richiesta HTTP che deve essere eseguita dall'applicazione |
| contesto | Lo stesso contesto opaco passato alla chiamata API MIP che ha generato questa richiesta HTTP |

```c
MIP_CC_CALLBACK(mip_cc_http_send_callback_fn,
    void,
    const mip_cc_http_request*,
    const void*);
```

## <a name="mip_cc_http_cancel_callback_fn"></a>mip_cc_http_cancel_callback_fn

Definizione della funzione di callback per l'annullamento di una richiesta HTTP

**Parameters**

Parametro | Descrizione
|---|---|
| requestId | ID della richiesta HTTP da annullare. |

```c
MIP_CC_CALLBACK(mip_cc_http_cancel_callback_fn,
    void,
    const char*);
```

## <a name="mip_cc_createhttpdelegate"></a>MIP_CC_CreateHttpDelegate

Crea un delegato HTTP che può essere usato per eseguire l'override dello stack HTTP predefinito di MIP

**Parameters**

Parametro | Descrizione
|---|---|
| sendCallback | Puntatore a funzione per l'emissione di richieste HTTP |
| cancelCallback | Puntatore a funzione per l'annullamento delle richieste HTTP |
| httpDelegate | Output Handle per oggetto delegato HTTP |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_CreateHttpDelegate(
    const mip_cc_http_send_callback_fn sendCallback,
    const mip_cc_http_cancel_callback_fn cancelCallback,
    mip_cc_http_delegate* httpDelegate,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_notifyhttpdelegateresponse"></a>MIP_CC_NotifyHttpDelegateResponse

Notifica a un delegato HTTP che una risposta HTTP è pronta

**Parameters**

Parametro | Descrizione
|---|---|
| httpDelegate | Handle per oggetto delegato HTTP |
| requestId | ID della richiesta HTTP associata a questa operazione |
| result | Stato operazione riuscita/non riuscita |
| response | Risposta HTTP se l'operazione è riuscita, altrimenti nullptr |

**Nota**: questa funzione deve essere chiamata dall'applicazione quando un'operazione HTTP è stata completata. L'ID della risposta HTTP deve corrispondere all'ID della richiesta HTTP per consentire a MIP di correlare una risposta alla richiesta 

```c
void MIP_CC_NotifyHttpDelegateResponse(
    const mip_cc_http_delegate httpDelegate,
    const char* requestId,
    const mip_cc_http_result result,
    const mip_cc_http_response* response);
```

## <a name="mip_cc_releasehttpdelegate"></a>MIP_CC_ReleaseHttpDelegate

Rilasciare le risorse associate a un handle del delegato HTTP

**Parameters**

Parametro | Descrizione
|---|---|
| httpDelegate | Delegato HTTP da rilasciare |

```c
void MIP_CC_ReleaseHttpDelegate(mip_cc_http_delegate httpDelegate);
```

## <a name="mip_cc_logger_init_callback_fn"></a>mip_cc_logger_init_callback_fn

Definizione della funzione di callback per l'inizializzazione del logger

**Parameters**

Parametro | Descrizione
|---|---|
| storagePath | Percorso del file in cui è possibile archiviare i log |

```c
MIP_CC_CALLBACK(mip_cc_logger_init_callback_fn,
    void,
    const char*);
```

## <a name="mip_cc_logger_write_callback_fn"></a>mip_cc_logger_write_callback_fn

Definizione della funzione di callback per la scrittura di un'istruzione log

**Parameters**

Parametro | Descrizione
|---|---|
| livello | livello di registrazione per l'istruzione log. |
| message | messaggio per l'istruzione log. |
| function | nome della funzione per l'istruzione log. |
| file | nome del file in cui è stata generata l'istruzione log. |
| line | numero di riga in cui è stata generata l'istruzione log. |

```c
MIP_CC_CALLBACK(mip_cc_logger_write_callback_fn,
    void,
    const mip_cc_log_level,
    const char*,
    const char*,
    const char*,
    const int32_t);
```

## <a name="mip_cc_createloggerdelegate"></a>MIP_CC_CreateLoggerDelegate

Crea un delegato del logger che può essere usato per eseguire l'override del logger predefinito di MIP

**Parameters**

Parametro | Descrizione
|---|---|
| initCallback | Puntatore a funzione per l'inizializzazione |
| flushCallback | Puntatore a funzione per lo scaricamento dei log |
| writeCallback | Puntatore a funzione per la scrittura di un'istruzione log |
| loggerDelegate | Output Handle per l'oggetto delegato del logger |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_CreateLoggerDelegate(
    const mip_cc_logger_init_callback_fn initCallback,
    const mip_cc_logger_flush_callback_fn flushCallback,
    const mip_cc_logger_write_callback_fn writeCallback,
    mip_cc_logger_delegate* loggerDelegate,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_releaseloggerdelegate"></a>MIP_CC_ReleaseLoggerDelegate

Rilasciare le risorse associate a un handle del delegato del logger

**Parameters**

Parametro | Descrizione
|---|---|
| loggerDelegate | Delegato del logger da rilasciare |

```c
void MIP_CC_ReleaseLoggerDelegate(mip_cc_logger_delegate loggerDelegate);
```

## <a name="mip_cc_createmipcontext"></a>MIP_CC_CreateMipContext

Creare un contesto MIP per gestire lo stato condiviso tra tutte le istanze del profilo

**Parameters**

Parametro | Descrizione
|---|---|
| applicationInfo | Informazioni sull'applicazione che utilizza l'SDK di protezione |
| path | Percorso del file in cui sono archiviati i dati di registrazione, telemetria e altro materiale collaterale per la protezione |
| logLevel | Livello di registrazione minimo per. miplog |
| isOfflineOnly | Abilita/Disabilita le operazioni di rete (non tutte le azioni supportate quando offline) |
| loggerDelegateOverride | Opzionale Implementazione dell'override del logger |
| telemetryOverride | Opzionale Impostazioni di telemetria sottoposte a override. Se NULL, verranno usate le impostazioni predefinite |
| mipContext | Output Istanza del contesto MIP appena creata |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_CreateMipContext(
    const mip_cc_application_info* applicationInfo,
    const char* path,
    const mip_cc_log_level logLevel,
    const bool isOfflineOnly,
    const mip_cc_logger_delegate loggerDelegateOverride,
    const mip_cc_telemetry_configuration telemetryOverride,
    mip_cc_mip_context* mipContext,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_createmipcontextwithcustomfeaturesettings"></a>MIP_CC_CreateMipContextWithCustomFeatureSettings

Creare un contesto MIP per gestire lo stato condiviso tra tutte le istanze del profilo

**Parameters**

Parametro | Descrizione
|---|---|
| applicationInfo | Informazioni sull'applicazione che utilizza l'SDK di protezione |
| path | Percorso del file in cui sono archiviati i dati di registrazione, telemetria e altro materiale collaterale per la protezione |
| logLevel | Livello di registrazione minimo per. miplog |
| isOfflineOnly | Abilita/Disabilita le operazioni di rete (non tutte le azioni supportate quando offline) |
| loggerDelegateOverride | Opzionale Implementazione dell'override del logger |
| telemetryOverride | Opzionale Impostazioni di telemetria sottoposte a override. Se NULL, verranno usate le impostazioni predefinite |
| featureSettings | Opzionale Matrice di override di funzionalità personalizzate |
| featureSettingsSize | Dimensioni delle sostituzioni di funzionalità personalizzate (in numero di sostituzioni) |
| mipContext | Output Istanza del contesto MIP appena creata |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_CreateMipContextWithCustomFeatureSettings(
    const mip_cc_application_info* applicationInfo,
    const char* path,
    const mip_cc_log_level logLevel,
    const bool isOfflineOnly,
    const mip_cc_logger_delegate loggerDelegateOverride,
    const mip_cc_telemetry_configuration telemetryOverride,
    const mip_cc_feature_override* featureSettings,
    const int64_t featureSettingsSize,
    mip_cc_mip_context* mipContext,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_releasemipcontext"></a>MIP_CC_ReleaseMipContext

Rilascia le risorse associate a un contesto MIP

**Parameters**

Parametro | Descrizione
|---|---|
| mipContext | Contesto MIP da rilasciare |

```c
void MIP_CC_ReleaseMipContext(mip_cc_mip_context mipContext);
```

## <a name="mip_cc_protectiondescriptor_getprotectiontype"></a>MIP_CC_ProtectionDescriptor_GetProtectionType

Ottiene il tipo di protezione, indipendentemente dal fatto che sia definito da un modello RMS

**Parameters**

Parametro | Descrizione
|---|---|
| protectionDescriptor | Descrittore associato al contenuto protetto |
| protectionType | Output Tipo di protezione |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_ProtectionDescriptor_GetProtectionType(
    const mip_cc_protection_descriptor protectionDescriptor,
    mip_cc_protection_type* protectionType,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectiondescriptor_getownersize"></a>MIP_CC_ProtectionDescriptor_GetOwnerSize

Ottiene le dimensioni del buffer necessarie per archiviare il proprietario

**Parameters**

Parametro | Descrizione
|---|---|
| protectionDescriptor | Descrittore associato al contenuto protetto |
| ownerSize | Output Dimensioni del buffer per il possesso del proprietario (in numero di caratteri) |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_ProtectionDescriptor_GetOwnerSize(
    const mip_cc_protection_descriptor protectionDescriptor,
    int64_t* ownerSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectiondescriptor_getowner"></a>MIP_CC_ProtectionDescriptor_GetOwner

Ottiene il proprietario della protezione

**Parameters**

Parametro | Descrizione
|---|---|
| protectionDescriptor | Descrittore associato al contenuto protetto |
| ownerBuffer | Output Buffer in cui verrà copiato il proprietario. |
| ownerBufferSize | Dimensioni (in numero di caratteri) di ownerBuffer. |
| actualOwnerSize | Output Numero di caratteri scritti nel buffer |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

**Nota**: se ownerBuffer è null o insufficiente, verrà restituito MIP_RESULT_ERROR_INSUFFICIENT_BUFFER e actualOwnerSize verrà impostato sulle dimensioni minime del buffer richiesto. 

```c
mip_cc_result MIP_CC_ProtectionDescriptor_GetOwner(
    const mip_cc_protection_descriptor protectionDescriptor,
    char* ownerBuffer,
    const int64_t ownerBufferSize,
    int64_t* actualOwnerSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectiondescriptor_getnamesize"></a>MIP_CC_ProtectionDescriptor_GetNameSize

Ottiene le dimensioni del buffer necessarie per archiviare il nome

**Parameters**

Parametro | Descrizione
|---|---|
| protectionDescriptor | Descrittore associato al contenuto protetto |
| nameSize | Output Dimensione del buffer in cui memorizzare il nome (in numero di caratteri) |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_ProtectionDescriptor_GetNameSize(
    const mip_cc_protection_descriptor protectionDescriptor,
    int64_t* nameSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectiondescriptor_getname"></a>MIP_CC_ProtectionDescriptor_GetName

Ottiene il nome della protezione

**Parameters**

Parametro | Descrizione
|---|---|
| protectionDescriptor | Descrittore associato al contenuto protetto |
| nameBuffer | Output Buffer in cui verrà copiato il nome. |
| nameBufferSize | Dimensioni (in numero di caratteri) di nameBuffer. |
| actualNameSize | Output Numero di caratteri scritti nel buffer |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

**Nota**: se nameBuffer è null o insufficiente, verrà restituito MIP_RESULT_ERROR_INSUFFICIENT_BUFFER e actualNameSize verrà impostato sulle dimensioni minime del buffer richiesto. 

```c
mip_cc_result MIP_CC_ProtectionDescriptor_GetName(
    const mip_cc_protection_descriptor protectionDescriptor,
    char* nameBuffer,
    const int64_t nameBufferSize,
    int64_t* actualNameSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectiondescriptor_getdescriptionsize"></a>MIP_CC_ProtectionDescriptor_GetDescriptionSize

Ottiene la dimensione del buffer necessaria per archiviare la descrizione

**Parameters**

Parametro | Descrizione
|---|---|
| protectionDescriptor | Descrittore associato al contenuto protetto |
| descriptionSize | Output Dimensione del buffer in cui memorizzare la descrizione (in numero di caratteri) |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_ProtectionDescriptor_GetDescriptionSize(
    const mip_cc_protection_descriptor protectionDescriptor,
    int64_t* descriptionSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectiondescriptor_getdescription"></a>MIP_CC_ProtectionDescriptor_GetDescription

Ottiene la descrizione della protezione

**Parameters**

Parametro | Descrizione
|---|---|
| protectionDescriptor | Descrittore associato al contenuto protetto |
| descriptionBuffer | Output Buffer in cui verrà copiata la descrizione. |
| descriptionBufferSize | Dimensioni (in numero di caratteri) di descriptionBuffer. |
| actualDescriptionSize | Output Numero di caratteri scritti nel buffer |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

**Nota**: se descriptionBuffer è null o insufficiente, verrà restituito MIP_RESULT_ERROR_INSUFFICIENT_BUFFER e actualDescriptionSize verrà impostato sulle dimensioni minime del buffer richiesto. 

```c
mip_cc_result MIP_CC_ProtectionDescriptor_GetDescription(
    const mip_cc_protection_descriptor protectionDescriptor,
    char* descriptionBuffer,
    const int64_t descriptionBufferSize,
    int64_t* actualDescriptionSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectiondescriptor_gettemplateid"></a>MIP_CC_ProtectionDescriptor_GetTemplateId

Ottiene l'ID modello

**Parameters**

Parametro | Descrizione
|---|---|
| protectionDescriptor | Descrittore associato al contenuto protetto |
| templateId | Output ID modello associato alla protezione |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_ProtectionDescriptor_GetTemplateId(
    const mip_cc_protection_descriptor protectionDescriptor,
    mip_cc_guid* templateId,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectiondescriptor_getlabelid"></a>MIP_CC_ProtectionDescriptor_GetLabelId

Ottiene l'ID etichetta

**Parameters**

Parametro | Descrizione
|---|---|
| protectionDescriptor | Descrittore associato al contenuto protetto |
| labelId | Output ID etichetta associato alla protezione |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_ProtectionDescriptor_GetLabelId(
    const mip_cc_protection_descriptor protectionDescriptor,
    mip_cc_guid* labelId,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectiondescriptor_getcontentid"></a>MIP_CC_ProtectionDescriptor_GetContentId

Ottiene l'ID contenuto

**Parameters**

Parametro | Descrizione
|---|---|
| protectionDescriptor | Descrittore associato al contenuto protetto |
| contentId | Output ID contenuto associato alla protezione |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_ProtectionDescriptor_GetContentId(
    const mip_cc_protection_descriptor protectionDescriptor,
    mip_cc_guid* contentId,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectiondescriptor_doescontentexpire"></a>MIP_CC_ProtectionDescriptor_DoesContentExpire

Ottiene un valore che indica se il contenuto ha una data di scadenza

**Parameters**

Parametro | Descrizione
|---|---|
| protectionDescriptor | Descrittore associato al contenuto protetto |
| doesContentExpire | Output Indica se il contenuto scade |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_ProtectionDescriptor_DoesContentExpire(
    const mip_cc_protection_descriptor protectionDescriptor,
    bool* doesContentExpire,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectiondescriptor_getcontentvaliduntil"></a>MIP_CC_ProtectionDescriptor_GetContentValidUntil

Ottiene l'ora di scadenza della protezione (in secondi da Epoch)

**Parameters**

Parametro | Descrizione
|---|---|
| protectionDescriptor | Descrittore associato al contenuto protetto |
| contentValidUntil | Output Data di scadenza del contenuto (in secondi da Epoch) |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_ProtectionDescriptor_GetContentValidUntil(
    const mip_cc_protection_descriptor protectionDescriptor,
    int64_t* contentValidUntil,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectiondescriptor_doesallowofflineaccess"></a>MIP_CC_ProtectionDescriptor_DoesAllowOfflineAccess

Ottiene un valore che indica se è consentito o meno l'accesso offline

**Parameters**

Parametro | Descrizione
|---|---|
| protectionDescriptor | Descrittore associato al contenuto protetto |
| doesAllowOfflineAccess | Output Indica se è consentito o meno l'accesso offline |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_ProtectionDescriptor_DoesAllowOfflineAccess(
    const mip_cc_protection_descriptor protectionDescriptor,
    bool* doesAllowOfflineAccess,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectiondescriptor_getreferrersize"></a>MIP_CC_ProtectionDescriptor_GetReferrerSize

Ottiene le dimensioni del buffer necessarie per archiviare il referrer

**Parameters**

Parametro | Descrizione
|---|---|
| protectionDescriptor | Descrittore associato al contenuto protetto |
| referrerSize | Output Dimensione del buffer in cui memorizzare il referrer (in numero di caratteri) |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_ProtectionDescriptor_GetReferrerSize(
    const mip_cc_protection_descriptor protectionDescriptor,
    int64_t* referrerSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectiondescriptor_getreferrer"></a>MIP_CC_ProtectionDescriptor_GetReferrer

Ottiene il referrer di protezione

**Parameters**

Parametro | Descrizione
|---|---|
| protectionDescriptor | Descrittore associato al contenuto protetto |
| referrerBuffer | Output Buffer in cui verrà copiato il referrer. |
| referrerBufferSize | Dimensioni (in numero di caratteri) di referrerBuffer. |
| actualReferrerSize | Output Numero di caratteri scritti nel buffer |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

**Nota**: se referrerBuffer è null o insufficiente, verrà restituito MIP_RESULT_ERROR_INSUFFICIENT_BUFFER e actualReferrerSize verrà impostato sulle dimensioni minime del buffer richiesto. 

```c
mip_cc_result MIP_CC_ProtectionDescriptor_GetReferrer(
    const mip_cc_protection_descriptor protectionDescriptor,
    char* referrerBuffer,
    const int64_t referrerBufferSize,
    int64_t* actualReferrerSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectiondescriptor_getdoublekeyurlsize"></a>MIP_CC_ProtectionDescriptor_GetDoubleKeyUrlSize

Ottiene le dimensioni del buffer necessarie per archiviare l'URL della chiave doppia

**Parameters**

Parametro | Descrizione
|---|---|
| protectionDescriptor | Descrittore associato al contenuto protetto |
| url | Output Dimensione del buffer in cui memorizzare l'URL della chiave doppia (in numero di caratteri) |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_ProtectionDescriptor_GetDoubleKeyUrlSize(
    const mip_cc_protection_descriptor protectionDescriptor,
    int64_t* urlSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectiondescriptor_getdoublekeyurl"></a>MIP_CC_ProtectionDescriptor_GetDoubleKeyUrl

Ottiene l'URL della chiave doppia

**Parameters**

Parametro | Descrizione
|---|---|
| protectionDescriptor | Descrittore associato al contenuto protetto |
| urlBuffer | Output Buffer in cui verrà copiato l'URL. |
| urlBufferSize | Dimensioni (in numero di caratteri) di urlBuffer. |
| actualUrlSize | Output Numero di caratteri scritti nel buffer |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

**Nota**: se urlBuffer è null o insufficiente, verrà restituito MIP_RESULT_ERROR_INSUFFICIENT_BUFFER e actualUrlSize verrà impostato sulle dimensioni minime del buffer richiesto. 

```c
mip_cc_result MIP_CC_ProtectionDescriptor_GetDoubleKeyUrl(
    const mip_cc_protection_descriptor protectionDescriptor,
    char* urlBuffer,
    const int64_t urlBufferSize,
    int64_t* actualUrlSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_releaseprotectiondescriptor"></a>MIP_CC_ReleaseProtectionDescriptor

Rilascia le risorse associate a un descrittore di protezione

**Parameters**

Parametro | Descrizione
|---|---|
| protectionDescriptor | Descrittore di protezione da rilasciare |

```c
void MIP_CC_ReleaseProtectionDescriptor(mip_cc_protection_descriptor protectionDescriptor);
```

## <a name="mip_cc_createstringlist"></a>MIP_CC_CreateStringList

Creare un elenco di stringhe

**Parameters**

Parametro | Descrizione
|---|---|
| stringhe | Matrice di stringhe |
| count | Numero di stringhe |
| stringList | Output Elenco di stringhe appena creato |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

**Nota**: è necessario liberare un mip_cc_string_list chiamando MIP_CC_ReleaseStringList 

```c
mip_cc_result MIP_CC_CreateStringList(
    const char** strings,
    const int64_t count,
    mip_cc_string_list* stringList,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_stringlist_getstrings"></a>MIP_CC_StringList_GetStrings

Ottenere stringhe che compongono un elenco di stringhe

**Parameters**

Parametro | Descrizione
|---|---|
| stringList | Elenco di stringhe di origine |
| stringhe | Output Matrice di stringhe, memoria di proprietà dell'oggetto mip_cc_string_list |
| count | Output Numero di stringhe |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

**Nota**: la memoria per ' Strings ' è di proprietà dell'oggetto mip_cc_string_list, quindi non deve essere liberata in modo indipendente 

```c
mip_cc_result MIP_CC_StringList_GetStrings(
    const mip_cc_string_list stringList,
    const char*** strings,
    int64_t* count,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_releasestringlist"></a>MIP_CC_ReleaseStringList

Rilasciare le risorse associate a un elenco di stringhe

**Parameters**

Parametro | Descrizione
|---|---|
| stringList | Elenco di stringhe da rilasciare |

```c
void MIP_CC_ReleaseStringList(mip_cc_string_list stringList);
```

## <a name="mip_cc_dispatch_task_callback_fn"></a>mip_cc_dispatch_task_callback_fn

Definizione della funzione di callback per l'invio di un'attività asincrona

**Parameters**

Parametro | Descrizione
|---|---|
| taskId | Identificatore univoco dell'attività |

```c
MIP_CC_CALLBACK(mip_cc_dispatch_task_callback_fn,
    void,
    const mip_cc_async_task*);
```

## <a name="mip_cc_cancel_task_callback_fn"></a>mip_cc_cancel_task_callback_fn

Funzione di callback per l'annullamento di un'attività in background

**Parameters**

Parametro | Descrizione
|---|---|
| taskId | Identificatore univoco dell'attività |

**Return**: true se l'attività è stata annullata correttamente; in caso contrario, false

```c
MIP_CC_CALLBACK(mip_cc_cancel_task_callback_fn,
    bool,
    const char*);
```

## <a name="mip_cc_createtaskdispatcherdelegate"></a>MIP_CC_CreateTaskDispatcherDelegate

Crea un delegato del dispatcher di attività che può essere usato per eseguire l'override della gestione delle attività asincrone predefinite di MIP

**Parameters**

Parametro | Descrizione
|---|---|
| dispatchTaskCallback | Puntatore a funzione per l'invio di attività asincrone |
| cancelTaskCallback | Puntatore a funzione per l'annullamento delle attività in background |
| cancelAllTasksCallback | Puntatore a funzione per l'annullamento di tutte le attività in background |
| taskDispatcher | Output Handle per l'oggetto delegato del dispatcher attività |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_CreateTaskDispatcherDelegate(
    const mip_cc_dispatch_task_callback_fn dispatchTaskCallback,
    const mip_cc_cancel_task_callback_fn cancelTaskCallback,
    const mip_cc_cancel_all_tasks_callback_fn cancelAllTasksCallback,
    mip_cc_task_dispatcher_delegate* taskDispatcher,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_executedispatchedtask"></a>MIP_CC_ExecuteDispatchedTask

Notifica a un delegato TaskDispatcher che un'attività è pianificata per l'esecuzione nel thread corrente

**Parameters**

Parametro | Descrizione
|---|---|
| taskDispatcher | Handle per l'oggetto delegato del dispatcher attività |
| taskId | ID dell'attività asincrona associata a questa operazione |

**Nota**: questa funzione deve essere chiamata dall'applicazione quando è pianificata l'esecuzione di un'attività. Il risultato sarà l'esecuzione immediata dell'attività sul thread corrente. L'ID deve corrispondere a quello di un'attività non annullata in precedenza. 

```c
void MIP_CC_ExecuteDispatchedTask(const mip_cc_task_dispatcher_delegate taskDispatcher, const char* taskId);
```

## <a name="mip_cc_releasetaskdispatcherdelegate"></a>MIP_CC_ReleaseTaskDispatcherDelegate

Rilasciare le risorse associate a un handle del delegato del dispatcher attività

**Parameters**

Parametro | Descrizione
|---|---|
| taskDispatcher | Delegato Dispatcher attività da rilasciare |

```c
void MIP_CC_ReleaseTaskDispatcherDelegate(mip_cc_task_dispatcher_delegate taskDispatcher);
```

## <a name="mip_cc_createtelemetryconfiguration"></a>MIP_CC_CreateTelemetryConfiguration

Creare un oggetto impostazioni utilizzato per creare un profilo di protezione

**Parameters**

Parametro | Descrizione
|---|---|
| telemetryConfig | Output Istanza di configurazione di telemetria appena creata contenente le impostazioni predefinite |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_CreateTelemetryConfiguration(
    mip_cc_telemetry_configuration* telemetryConfig,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_telemetryconfiguration_sethostname"></a>MIP_CC_TelemetryConfiguration_SetHostName

Impostare un nome host di telemetria che sostituirà le impostazioni di telemetria interne

**Parameters**

Parametro | Descrizione
|---|---|
| telemetryConfig | Configurazione della telemetria |
| hostName | Nome host |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

**Nota**: questa proprietà viene impostata quando un'applicazione client usa lo stesso componente di telemetria aria/1Ds e desidera le impostazioni di telemetria interne (memorizzazione nella cache, registrazione, priorità e così via) da usare anziché le impostazioni predefinite del MIP 

```c
mip_cc_result MIP_CC_TelemetryConfiguration_SetHostName(
    const mip_cc_telemetry_configuration telemetryConfig,
    const char* hostName,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_telemetryconfiguration_setlibraryname"></a>MIP_CC_TelemetryConfiguration_SetLibraryName

Impostare un override della libreria condivisa di telemetria

**Parameters**

Parametro | Descrizione
|---|---|
| telemetryConfig | Configurazione della telemetria |
| NomeLibreria | Nome della DLL che implementa l'API C di aria/1DS SDK |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

**Nota**: questa proprietà viene impostata quando un client ha una DLL di telemetria esistente che implementa l'API C di aria/1Ds SDK da usare al posto di mip_ClientTelemetry.dll 

```c
mip_cc_result MIP_CC_TelemetryConfiguration_SetLibraryName(
    const mip_cc_telemetry_configuration telemetryConfig,
    const char* libraryName,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_telemetryconfiguration_sethttpdelegate"></a>MIP_CC_TelemetryConfiguration_SetHttpDelegate

Esegui override dello stack HTTP di telemetria predefinito con il proprio client

**Parameters**

Parametro | Descrizione
|---|---|
| telemetryConfig | Configurazione della telemetria |
| httpDelegate | Istanza di callback HTTP implementata dall'applicazione client |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

**Nota**: se questa proprietà non è impostata, il componente di telemetria userà lo stack HTTP predefinito del MIP 

```c
mip_cc_result MIP_CC_TelemetryConfiguration_SetHttpDelegate(
    const mip_cc_telemetry_configuration telemetryConfig,
    const mip_cc_http_delegate httpDelegate,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_telemetryconfiguration_settaskdispatcherdelegate"></a>MIP_CC_TelemetryConfiguration_SetTaskDispatcherDelegate

Esegui override del dispatcher attività asincrono predefinito con il proprio client

**Parameters**

Parametro | Descrizione
|---|---|
| telemetryConfig | Configurazione della telemetria |
| taskDispatcherDelegate | Istanza di callback Dispatcher attività implementata dall'applicazione client |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_TelemetryConfiguration_SetTaskDispatcherDelegate(
    const mip_cc_telemetry_configuration telemetryConfig,
    const mip_cc_task_dispatcher_delegate taskDispatcherDelegate,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_telemetryconfiguration_setisnetworkdetectionenabled"></a>MIP_CC_TelemetryConfiguration_SetIsNetworkDetectionEnabled

Indica se il componente di telemetria è autorizzato a eseguire il ping dello stato della rete in un thread in background

**Parameters**

Parametro | Descrizione
|---|---|
| telemetryConfig | Configurazione della telemetria |
| isCachingEnabled | Indica se il componente di telemetria è autorizzato a eseguire il ping dello stato della rete in un thread in background |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

**Nota**: il valore predefinito è' true ' 

```c
mip_cc_result MIP_CC_TelemetryConfiguration_SetIsNetworkDetectionEnabled(
    const mip_cc_telemetry_configuration telemetryConfig,
    const bool isNetworkDetectionEnabled,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_telemetryconfiguration_setislocalcachingenabled"></a>MIP_CC_TelemetryConfiguration_SetIsLocalCachingEnabled

Imposta un valore che indica se il componente di telemetria può scrivere le cache sul disco

**Parameters**

Parametro | Descrizione
|---|---|
| telemetryConfig | Configurazione della telemetria |
| isCachingEnabled | Indica se il componente di telemetria può scrivere cache sul disco |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

**Nota**: il valore predefinito è' true ' 

```c
mip_cc_result MIP_CC_TelemetryConfiguration_SetIsLocalCachingEnabled(
    const mip_cc_telemetry_configuration telemetryConfig,
    const bool isCachingEnabled,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_telemetryconfiguration_setistraceloggingenabled"></a>MIP_CC_TelemetryConfiguration_SetIsTraceLoggingEnabled

Imposta un valore che indica se il componente di telemetria può scrivere i log su disco

**Parameters**

Parametro | Descrizione
|---|---|
| telemetryConfig | Configurazione della telemetria |
| isTraceLoggingEnabled | Indica se il componente di telemetria è autorizzato a scrivere log su disco |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

**Nota**: il valore predefinito è' true ' 

```c
mip_cc_result MIP_CC_TelemetryConfiguration_SetIsTraceLoggingEnabled(
    const mip_cc_telemetry_configuration telemetryConfig,
    const bool isTraceLoggingEnabled,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_telemetryconfiguration_setistelemetryoptedout"></a>MIP_CC_TelemetryConfiguration_SetIsTelemetryOptedOut

Imposta un valore che indica se un'applicazione o un utente ha rifiutato la telemetria facoltativa

**Parameters**

Parametro | Descrizione
|---|---|
| telemetryConfig | Configurazione della telemetria |
| isTelemetryOptedOut | Se un'applicazione o un utente non ha rifiutato la telemetria facoltativa |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

**Nota**: il valore predefinito è' false ' 

```c
mip_cc_result MIP_CC_TelemetryConfiguration_SetIsTelemetryOptedOut(
    const mip_cc_telemetry_configuration telemetryConfig,
    const bool isTelemetryOptedOut,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_telemetryconfiguration_setcustomsettings"></a>MIP_CC_TelemetryConfiguration_SetCustomSettings

Imposta le impostazioni di telemetria personalizzate

**Parameters**

Parametro | Descrizione
|---|---|
| telemetryConfig | Configurazione della telemetria |
| customSettings | Impostazioni di telemetria personalizzate |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_TelemetryConfiguration_SetCustomSettings(
    const mip_cc_telemetry_configuration telemetryConfig,
    const mip_cc_dictionary customSettings,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_telemetryconfiguration_addmaskedproperty"></a>MIP_CC_TelemetryConfiguration_AddMaskedProperty

Imposta una proprietà di telemetria su maschera

**Parameters**

Parametro | Descrizione
|---|---|
| telemetryConfig | Configurazione della telemetria |
| eventName | Nome evento |
| propertyName | Nome proprietà |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_TelemetryConfiguration_AddMaskedProperty(
    const mip_cc_telemetry_configuration telemetryConfig,
    const char* eventName,
    const char* propertyName,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_releasetelemetryconfiguration"></a>MIP_CC_ReleaseTelemetryConfiguration

Rilascia le risorse associate a impostazioni del profilo di protezione

**Parameters**

Parametro | Descrizione
|---|---|
| profileSettings | Impostazioni del profilo di protezione da rilasciare |

```c
void MIP_CC_ReleaseTelemetryConfiguration(mip_cc_telemetry_configuration telemetryConfig);
```

## <a name="mip_cc_releaseprotectionengine"></a>MIP_CC_ReleaseProtectionEngine

Rilasciare le risorse associate a un motore di protezione

**Parameters**

Parametro | Descrizione
|---|---|
| motore | Motore di protezione da rilasciare |

```c
void MIP_CC_ReleaseProtectionEngine(mip_cc_protection_engine engine);
```

## <a name="mip_cc_protectionengine_createprotectionhandlerforpublishing"></a>MIP_CC_ProtectionEngine_CreateProtectionHandlerForPublishing

Crea un gestore protezione per la pubblicazione di nuovo contenuto

**Parameters**

Parametro | Descrizione
|---|---|
| motore | Motore in cui verrà creato un gestore |
| impostazioni | Impostazioni del gestore protezione |
| contesto | Contesto client che verrà passato in modo opaco a HttpDelegate e AuthDelegate |
| gestore | Output Istanza del gestore protezione appena creata |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_ProtectionEngine_CreateProtectionHandlerForPublishing(
    const mip_cc_protection_engine engine,
    const mip_cc_protection_handler_publishing_settings settings,
    const void* context,
    mip_cc_protection_handler* handler,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectionengine_createprotectionhandlerforconsumption"></a>MIP_CC_ProtectionEngine_CreateProtectionHandlerForConsumption

Crea un gestore protezione per l'utilizzo del contenuto esistente

**Parameters**

Parametro | Descrizione
|---|---|
| motore | Motore in cui verrà creato un gestore |
| impostazioni | Impostazioni del gestore protezione |
| contesto | Contesto client che verrà passato in modo opaco a HttpDelegate e AuthDelegate |
| gestore | Output Istanza del gestore protezione appena creata |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_ProtectionEngine_CreateProtectionHandlerForConsumption(
  const mip_cc_protection_engine engine,
  const mip_cc_protection_handler_consumption_settings settings,
  const void* context,
  mip_cc_protection_handler* handler,
  mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectionengine_getengineidsize"></a>MIP_CC_ProtectionEngine_GetEngineIdSize

Ottiene le dimensioni del buffer necessario per l'ID del motore

**Parameters**

Parametro | Descrizione
|---|---|
| motore | Motore di protezione |
| idSize | Output Dimensione del buffer in cui memorizzare l'ID del motore (in numero di caratteri) |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_ProtectionEngine_GetEngineIdSize(
    const mip_cc_protection_engine engine,
    int64_t* idSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectionengine_getengineid"></a>MIP_CC_ProtectionEngine_GetEngineId

Ottiene l'ID del motore

**Parameters**

Parametro | Descrizione
|---|---|
| motore | Motore di protezione |
| idBuffer | Output Buffer in cui verrà copiato l'ID. |
| idBufferSize | Dimensioni (in numero di caratteri) di idBuffer. |
| actualIdSize | Output Numero di caratteri scritti nel buffer |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

**Nota**: se idBuffer è null o insufficiente, verrà restituito MIP_RESULT_ERROR_INSUFFICIENT_BUFFER e actualIdSize verrà impostato sulle dimensioni minime del buffer richiesto. 

```c
mip_cc_result MIP_CC_ProtectionEngine_GetEngineId(
    const mip_cc_protection_engine engine,
    char* idBuffer,
    const int64_t idBufferSize,
    int64_t* actualIdSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectionengine_gettemplatessize"></a>MIP_CC_ProtectionEngine_GetTemplatesSize

Ottiene il numero di modelli RMS associati a un motore di protezione

**Parameters**

Parametro | Descrizione
|---|---|
| motore | Motore di protezione |
| contesto | Contesto client che verrà passato in modo opaco a HttpDelegate e AuthDelegate |
| templatesSize | Output Numero di modelli |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

**Nota**: questa API può causare un'operazione HTTP indipendente. Si consiglia di usare ' MIP_CC_ProtectionEngine_GetTemplates ' direttamente con un buffer predefinito per evitare operazioni HTTP aggiuntive superflue. 

```c
mip_cc_result MIP_CC_ProtectionEngine_GetTemplatesSize(
    const mip_cc_protection_engine engine,
    const void* context,
    int64_t* templatesSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectionengine_gettemplates"></a>MIP_CC_ProtectionEngine_GetTemplates

Ottenere la raccolta di modelli disponibili per un utente

**Parameters**

Parametro | Descrizione
|---|---|
| motore | Motore di protezione |
| contesto | Contesto client che verrà passato in modo opaco a HttpDelegate e AuthDelegate |
| mip_cc_template_descriptor | [Output] buffer per la creazione di gestori di modelli. |
| templateBufferSize | Dimensioni (in numero di elementi) di templateBuffer. |
| actualTemplatesSize | Output Numero di ID modello scritti nel buffer |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

**Nota**: se templateBuffer è null o insufficiente, verrà restituito MIP_RESULT_ERROR_INSUFFICIENT_BUFFER e actualTemplateSize verrà impostato sulle dimensioni minime del buffer richiesto. Ogni mip_cc_template_descriptor deve essere rilasciata dal chiamante chiamando MIP_CC_ReleaseTemplateDescriptor (). 

```c
mip_cc_result MIP_CC_ProtectionEngine_GetTemplates(
    const mip_cc_protection_engine engine,
    const void* context,
    mip_cc_template_descriptor* templateDescriptors,
    const int64_t templateBufferSize,
    int64_t* actualTemplatesSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectionengine_getrightsforlabelid"></a>MIP_CC_ProtectionEngine_GetRightsForLabelId

Ottiene l'elenco dei diritti concessi a un utente per un ID etichetta

**Parameters**

Parametro | Descrizione
|---|---|
| motore | Motore di protezione |
| contesto | Contesto client che verrà passato in modo opaco a HttpDelegate e AuthDelegate |
| documentId | ID documento assegnato al documento |
| labelId | ID etichetta applicato al documento |
| ownerEmail | Proprietario del documento |
| delagedUserEmail | Messaggio di posta elettronica dell'utente se l'utente o l'applicazione di autenticazione agisce per conto di un altro utente, vuoto se non è presente alcun valore |
| diritti | Output Elenco dei diritti concessi a un utente, memoria di proprietà del chiamante |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

**Nota**: la variabile ' Rights ' deve essere rilasciata dal chiamante chiamando MIP_CC_ReleaseStringList 

```c
mip_cc_result MIP_CC_ProtectionEngine_GetRightsForLabelId(
    const mip_cc_protection_engine engine,
    const void* context,
    const char* documentId,
    const char* labelId,
    const char* ownerEmail,
    const char* delegatedUserEmail,
    mip_cc_string_list* rights,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectionengine_getclientdatasize"></a>MIP_CC_ProtectionEngine_GetClientDataSize

Ottiene le dimensioni dei dati client associati a un motore di protezione

**Parameters**

Parametro | Descrizione
|---|---|
| motore | Motore di protezione |
| clientDataSize | Output Dimensioni dei dati client (in numero di caratteri) |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_ProtectionEngine_GetClientDataSize(
    const mip_cc_protection_engine engine,
    int64_t* clientDataSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectionengine_getclientdata"></a>MIP_CC_ProtectionEngine_GetClientData

Ottenere i dati client associati a un motore di protezione

**Parameters**

Parametro | Descrizione
|---|---|
| motore | Motore di protezione |
| clientDataBuffer | Output Buffer in cui verranno copiati i dati client |
| clientDataBufferSize | Dimensioni (in numero di caratteri) di clientDataBuffer. |
| actualClientDataSize | Output Numero di caratteri scritti nel buffer |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

**Nota**: se clientDataBuffer è null o insufficiente, verrà restituito MIP_RESULT_ERROR_INSUFFICIENT_BUFFER e actualClientDataSize verrà impostato sulle dimensioni minime del buffer richiesto. 

```c
mip_cc_result MIP_CC_ProtectionEngine_GetClientData(
    const mip_cc_protection_engine engine,
    char* clientDataBuffer,
    const int64_t clientDataBufferSize,
    int64_t* actualClientDataSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_createprotectionenginesettingswithidentity"></a>MIP_CC_CreateProtectionEngineSettingsWithIdentity

Creare un oggetto impostazioni usato per creare un nuovo motore di protezione

**Parameters**

Parametro | Descrizione
|---|---|
| identity | Identità che verrà associata a ProtectionEngine |
| clientData | Dati client personalizzabili archiviati insieme al motore |
| locale | Impostazioni locali in cui vengono restituiti i risultati del testo |
| engineSettings | Output Istanza di impostazioni appena creata |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_CreateProtectionEngineSettingsWithIdentity(
    const mip_cc_identity* identity,
    const char* clientData,
    const char* locale,
    mip_cc_protection_engine_settings* engineSettings,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectionenginesettings_setclientdata"></a>MIP_CC_ProtectionEngineSettings_SetClientData

Imposta i dati client che verranno archiviati in maniera opaca insieme a questo motore e mantengono tra le sessioni

**Parameters**

Parametro | Descrizione
|---|---|
| impostazioni | Impostazioni motore |
| clientData | Dati client |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_ProtectionEngineSettings_SetClientData(
    const mip_cc_protection_engine_settings engineSettings,
    const char* clientData,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectionenginesettings_setcustomsettings"></a>MIP_CC_ProtectionEngineSettings_SetCustomSettings

Configura le impostazioni personalizzate, usate per il controllo e il controllo delle funzionalità.

**Parameters**

Parametro | Descrizione
|---|---|
| engineSettings | Impostazioni motore |
| customSettings | Coppie chiave/valore di impostazioni personalizzate |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_ProtectionEngineSettings_SetCustomSettings(
    const mip_cc_protection_engine_settings engineSettings,
    const mip_cc_dictionary customSettings,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectionenginesettings_setsessionid"></a>MIP_CC_ProtectionEngineSettings_SetSessionId

Imposta l'ID di sessione che può essere usato per correlare i log e i dati di telemetria

**Parameters**

Parametro | Descrizione
|---|---|
| impostazioni | Impostazioni motore |
| sessionID | ID sessione che rappresenta la durata di un motore di protezione |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_ProtectionEngineSettings_SetSessionId(
    const mip_cc_protection_engine_settings engineSettings,
    const char* sessionId,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectionenginesettings_setcloud"></a>MIP_CC_ProtectionEngineSettings_SetCloud

Imposta il cloud che influiscono sugli URL dell'endpoint per tutte le richieste di servizio

**Parameters**

Parametro | Descrizione
|---|---|
| impostazioni | Impostazioni motore |
| cloud | Identificatore cloud (impostazione predefinita = sconosciuta) |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

**Nota**: se il cloud non è specificato, sarà determinato dalla ricerca DNS del dominio di identità del motore, se possibile, in caso contrario al cloud globale. 

```c
mip_cc_result MIP_CC_ProtectionEngineSettings_SetCloud(
    const mip_cc_protection_engine_settings engineSettings,
    const mip_cc_cloud cloud,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectionenginesettings_setcloudendpointbaseurl"></a>MIP_CC_ProtectionEngineSettings_SetCloudEndpointBaseUrl

Imposta l'URL di base per tutte le richieste di servizio

**Parameters**

Parametro | Descrizione
|---|---|
| impostazioni | Impostazioni motore |
| cloudEndpointBaseUrl | URL di base (ad esempio ' https://api.aadrm.com ') |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

**Nota**: questo valore verrà letto e deve essere impostato solo per Cloud = MIP_CLOUD_CUSTOM 

```c
mip_cc_result MIP_CC_ProtectionEngineSettings_SetCloudEndpointBaseUrl(
    const mip_cc_protection_engine_settings engineSettings,
    const char* cloudEndpointBaseUrl,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_releaseprotectionenginesettings"></a>MIP_CC_ReleaseProtectionEngineSettings

Rilasciare le risorse associate a impostazioni del motore di protezione

**Parameters**

Parametro | Descrizione
|---|---|
| engineSettings | Impostazioni del motore di protezione da rilasciare |

```c
void MIP_CC_ReleaseProtectionEngineSettings(mip_cc_protection_engine_settings engineSettings);
```

## <a name="mip_cc_createprotectionhandlerpublishingsettings"></a>MIP_CC_CreateProtectionHandlerPublishingSettings

Creare un oggetto impostazioni utilizzato per creare un gestore protezione per la pubblicazione di nuovo contenuto

**Parameters**

Parametro | Descrizione
|---|---|
| descrittore | Dettagli sulla protezione |
| impostazioni | Output Istanza di impostazioni appena creata |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_CreateProtectionHandlerPublishingSettings(
    const mip_cc_protection_descriptor descriptor,
    mip_cc_protection_handler_publishing_settings* settings,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectionhandlerpublishingsettings_setisdeprecatedalgorithmpreferred"></a>MIP_CC_ProtectionHandlerPublishingSettings_SetIsDeprecatedAlgorithmPreferred

Imposta un valore che indica se è preferibile un algoritmo di crittografia deprecato (BCE) per la compatibilità con le versioni precedenti

**Parameters**

Parametro | Descrizione
|---|---|
| impostazioni | Impostazioni del gestore protezione |
| isDeprecatedAlgorithmPreferred | Indica se è preferibile l'algoritmo deprecato |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_ProtectionHandlerPublishingSettings_SetIsDeprecatedAlgorithmPreferred(
    const mip_cc_protection_handler_publishing_settings settings,
    const bool isDeprecatedAlgorithmPreferred,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectionhandlerpublishingsettings_setisauditedextractionallowed"></a>MIP_CC_ProtectionHandlerPublishingSettings_SetIsAuditedExtractionAllowed

Imposta un valore che indica se le applicazioni non compatibili con MIP possono aprire contenuto protetto

**Parameters**

Parametro | Descrizione
|---|---|
| impostazioni | Impostazioni del gestore protezione |
| isAuditedExtractionAllowed | Indica se le applicazioni non compatibili con MIP possono aprire contenuto protetto |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_ProtectionHandlerPublishingSettings_SetIsAuditedExtractionAllowed(
    const mip_cc_protection_handler_publishing_settings settings,
    const bool isAuditedExtractionAllowed,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectionhandlerpublishingsettings_setispublishingformatjson"></a>MIP_CC_ProtectionHandlerPublishingSettings_SetIsPublishingFormatJson

Imposta un valore che indica se PL è in formato JSON (il valore predefinito è XML)

**Parameters**

Parametro | Descrizione
|---|---|
| impostazioni | Impostazioni del gestore protezione |
| isPublishingFormatJson | Indica se il PL risultante deve essere in formato JSON |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_ProtectionHandlerPublishingSettings_SetIsPublishingFormatJson(
    const mip_cc_protection_handler_publishing_settings settings,
    const bool isPublishingFormatJson,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectionhandlerpublishingsettings_setdelegateduseremail"></a>MIP_CC_ProtectionHandlerPublishingSettings_SetDelegatedUserEmail

Imposta l'utente delegato

**Parameters**

Parametro | Descrizione
|---|---|
| impostazioni | Impostazioni del gestore protezione |
| delegatedUserEmail | Indirizzo di posta elettronica dell'utente delegato |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

**Nota**: un utente delegato viene specificato quando l'utente o l'applicazione di autenticazione agisce per conto di un altro utente 

```c
mip_cc_result MIP_CC_ProtectionHandlerPublishingSettings_SetDelegatedUserEmail(
    const mip_cc_protection_handler_publishing_settings settings,
    const char* delegatedUserEmail,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectionhandlerpublishingsettings_setprelicenseuseremail"></a>MIP_CC_ProtectionHandlerPublishingSettings_SetPreLicenseUserEmail

Imposta un utente con licenza preliminare

**Parameters**

Parametro | Descrizione
|---|---|
| impostazioni | Impostazioni del gestore protezione |
| preLicenseUserEmail | Indirizzo di posta elettronica dell'utente con licenza preliminare |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

**Nota**: quando si deve recuperare una licenza preliminare durante la pubblicazione, viene specificato un utente con licenza preliminare 

```c
mip_cc_result MIP_CC_ProtectionHandlerPublishingSettings_SetPreLicenseUserEmail(
    const mip_cc_protection_handler_publishing_settings settings,
    const char* preLicenseUserEmail,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_createprotectionhandlerconsumptionsettings"></a>MIP_CC_CreateProtectionHandlerConsumptionSettings

Creare un oggetto impostazioni utilizzato per creare un gestore protezione per l'utilizzo del contenuto esistente

**Parameters**

Parametro | Descrizione
|---|---|
| publishingLicenseBuffer | Buffer contenente la licenza di pubblicazione non elaborata |
| publishingLicenseBufferSize | Dimensioni del buffer delle licenze di pubblicazione |
| impostazioni | Output Istanza di impostazioni appena creata |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_CreateProtectionHandlerConsumptionSettings(
    const uint8_t* publishingLicenseBuffer,
    const int64_t publishingLicenseBufferSize,
    mip_cc_protection_handler_consumption_settings* settings,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_createprotectionhandlerconsumptionsettingswithprelicense"></a>MIP_CC_CreateProtectionHandlerConsumptionSettingsWithPreLicense

Creare un oggetto impostazioni utilizzato per creare un gestore protezione per l'utilizzo del contenuto esistente

**Parameters**

Parametro | Descrizione
|---|---|
| preLicenseBuffer | Buffer contenente il buffer pre-licenza RAW |
| preLicenseBufferSize | Dimensioni del buffer di pre-licenza |
| publishingLicenseBuffer | Buffer contenente la licenza di pubblicazione non elaborata |
| publishingLicenseBufferSize | Dimensioni del buffer delle licenze di pubblicazione |
| impostazioni | Output Istanza di impostazioni appena creata |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_CreateProtectionHandlerConsumptionSettingsWithPreLicense(
    const uint8_t* preLicenseBuffer,
    const int64_t preLicenseBufferSize,
    const uint8_t* publishingLicenseBuffer,
    const int64_t publishingLicenseBufferSize,
    mip_cc_protection_handler_consumption_settings* settings,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectionhandlerconsumptionsettings_setisofflineonly"></a>MIP_CC_ProtectionHandlerConsumptionSettings_SetIsOfflineOnly

Imposta un valore che indica se la creazione del gestore protezione consente operazioni HTTP online

**Parameters**

Parametro | Descrizione
|---|---|
| impostazioni | Impostazioni del gestore protezione |
| isOfflineOnly | True se le operazioni HTTP sono proibite, altrimenti false |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

**Nota**: se questa proprietà è impostata su true, la creazione del gestore protezione avrà esito positivo solo se il contenuto è già stato precedentemente decrittografato e la relativa licenza non è scaduta. Se il contenuto memorizzato nella cache non viene trovato, verrà restituito un risultato MIP_RESULT_ERROR_NETWORK. 

```c
mip_cc_result MIP_CC_ProtectionHandlerConsumptionSettings_SetIsOfflineOnly(
    const mip_cc_protection_handler_consumption_settings settings,
    const bool isOfflineOnly,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectionhandlerconsumptionsettings_setdelegateduseremail"></a>MIP_CC_ProtectionHandlerConsumptionSettings_SetDelegatedUserEmail

Imposta l'utente delegato

**Parameters**

Parametro | Descrizione
|---|---|
| impostazioni | Impostazioni del gestore protezione |
| delegatedUserEmail | Indirizzo di posta elettronica dell'utente delegato |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

**Nota**: un utente delegato viene specificato quando l'utente o l'applicazione di autenticazione agisce per conto di un altro utente 

```c
mip_cc_result MIP_CC_ProtectionHandlerConsumptionSettings_SetDelegatedUserEmail(
    const mip_cc_protection_handler_consumption_settings settings,
    const char* delegatedUserEmail,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectionhandler_getserializedpublishinglicensesize"></a>MIP_CC_ProtectionHandler_GetSerializedPublishingLicenseSize

Ottiene le dimensioni della licenza di pubblicazione (in byte)

**Parameters**

Parametro | Descrizione
|---|---|
| gestore | Gestore che rappresenta il contenuto protetto |
| publishingLicenseBufferSize | Output Dimensioni della licenza di pubblicazione (in byte) |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_ProtectionHandler_GetSerializedPublishingLicenseSize(
    const mip_cc_protection_handler handler,
    int64_t* publishingLicenseBufferSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectionhandler_getserializedpublishinglicense"></a>MIP_CC_ProtectionHandler_GetSerializedPublishingLicense

Ottiene la licenza di pubblicazione

**Parameters**

Parametro | Descrizione
|---|---|
| gestore | Gestore che rappresenta il contenuto protetto |
| publishingLicenseBuffer | Output Buffer in cui verrà scritta la licenza di pubblicazione |
| publishingLicenseBufferSize | Dimensioni del buffer delle licenze di pubblicazione |
| actualPublishingLicenseSize | Output Dimensioni effettive della licenza di pubblicazione (in byte) |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

**Nota**: se publishingLicenseBuffer è null o insufficiente, verrà restituito MIP_RESULT_ERROR_INSUFFICIENT_BUFFER e actualPublishingLicenseSize verrà impostato sulle dimensioni minime del buffer richiesto. 

```c
mip_cc_result MIP_CC_ProtectionHandler_GetSerializedPublishingLicense(
    const mip_cc_protection_handler handler,
    uint8_t* publishingLicenseBuffer,
    const int64_t publishingLicenseBufferSize,
    int64_t* actualPublishingLicenseSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectionhandler_getserializedprelicensesize"></a>MIP_CC_ProtectionHandler_GetSerializedPreLicenseSize

Ottiene le dimensioni della pre-licenza (in byte)

**Parameters**

Parametro | Descrizione
|---|---|
| gestore | Gestore che rappresenta il contenuto protetto |
| format | Formato di pre-licenza |
| preLicenseBufferSize | Output Dimensioni della licenza preliminare (in byte) |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_ProtectionHandler_GetSerializedPreLicenseSize(
    const mip_cc_protection_handler handler,
    mip_cc_pre_license_format format,
    int64_t* preLicenseBufferSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectionhandler_getserializedprelicense"></a>MIP_CC_ProtectionHandler_GetSerializedPreLicense

Ottiene la pre-licenza

**Parameters**

Parametro | Descrizione
|---|---|
| gestore | Gestore che rappresenta il contenuto protetto |
| format | Formato di pre-licenza |
| preLicenseBuffer | Output Buffer in cui verrà scritta la licenza preliminare |
| preLicenseBufferSize | Dimensioni del buffer di pre-licenza |
| actualPreLicenseSize | Output Dimensioni effettive della licenza preliminare (in byte) |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

**Nota**: se preLicenseBuffer è null o insufficiente, verrà restituito MIP_RESULT_ERROR_INSUFFICIENT_BUFFER e actualPreLicenseSize verrà impostato sulle dimensioni minime del buffer richiesto. 

```c
mip_cc_result MIP_CC_ProtectionHandler_GetSerializedPreLicense(
    const mip_cc_protection_handler handler,
    mip_cc_pre_license_format format,
    uint8_t* preLicenseBuffer,
    const int64_t preLicenseBufferSize,
    int64_t* actualPreLicenseSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectionhandler_getprotectiondescriptor"></a>MIP_CC_ProtectionHandler_GetProtectionDescriptor

Ottiene il descrittore di protezione

**Parameters**

Parametro | Descrizione
|---|---|
| gestore | Gestore che rappresenta il contenuto protetto |
| descrittore | Output Descrittore di protezione |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_ProtectionHandler_GetProtectionDescriptor(
    const mip_cc_protection_handler handler,
    mip_cc_protection_descriptor* descriptor,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectionhandler_getrights"></a>MIP_CC_ProtectionHandler_GetRights

Ottiene l'elenco dei diritti concessi a un utente

**Parameters**

Parametro | Descrizione
|---|---|
| gestore | Gestore che rappresenta il contenuto protetto |
| diritti | Output Elenco dei diritti concessi a un utente, memoria di proprietà del chiamante |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

**Nota**: la variabile ' Rights ' deve essere rilasciata dal chiamante chiamando MIP_CC_ReleaseStringList 

```c
mip_cc_result MIP_CC_ProtectionHandler_GetRights(
    const mip_cc_protection_handler handler,
    mip_cc_string_list* rights,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectionhandler_getprotectedcontentsize"></a>MIP_CC_ProtectionHandler_GetProtectedContentSize

Calcola le dimensioni del contenuto protetto, il factoring nella spaziatura interna e così via.

**Parameters**

Parametro | Descrizione
|---|---|
| gestore | Gestore che rappresenta il contenuto protetto |
| unprotectedSize | Dimensioni del contenuto non protetto/non crittografato (in byte) |
| includesFinalBlock | Descrive se il contenuto non protetto in questione include il blocco finale o meno. |
| protectedSize | Output Dimensioni del contenuto protetto |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_ProtectionHandler_GetProtectedContentSize(
    const mip_cc_protection_handler handler,
    const int64_t unprotectedSize,
    const bool includesFinalBlock,
    int64_t* protectedSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectionhandler_getblocksize"></a>MIP_CC_ProtectionHandler_GetBlockSize

Ottiene la dimensione del blocco (in byte) per la modalità di crittografia utilizzata da un gestore di protezione.

**Parameters**

Parametro | Descrizione
|---|---|
| gestore | Gestore che rappresenta il contenuto protetto |
| blockSize | Output Dimensioni blocco (in byte) |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_ProtectionHandler_GetBlockSize(
    const mip_cc_protection_handler handler,
    int64_t* blockSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectionhandler_getissuedusersize"></a>MIP_CC_ProtectionHandler_GetIssuedUserSize

Ottiene le dimensioni del buffer necessarie per archiviare l'utente a cui è stato concesso l'accesso al contenuto protetto

**Parameters**

Parametro | Descrizione
|---|---|
| gestore | Gestore che rappresenta il contenuto protetto |
| issuedUserSize | Output Dimensioni del buffer per l'utente rilasciato (in numero di caratteri) |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_ProtectionHandler_GetIssuedUserSize(
    const mip_cc_protection_handler handler,
    int64_t* issuedUserSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectionhandler_getissueduser"></a>MIP_CC_ProtectionHandler_GetIssuedUser

Ottiene l'utente a cui è stato concesso l'accesso al contenuto protetto

**Parameters**

Parametro | Descrizione
|---|---|
| gestore | Gestore che rappresenta il contenuto protetto |
| issuedUserBuffer | Output Buffer in cui verrà copiato l'utente emesso. |
| issuedUserBufferSize | Dimensioni (in numero di caratteri) di issuedUserBuffer. |
| actualIssuedUserSize | Output Numero di caratteri scritti nel buffer |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

**Nota**: se issuedUserBuffer è null o insufficiente, verrà restituito MIP_RESULT_ERROR_INSUFFICIENT_BUFFER e actualIssuedUserSize verrà impostato sulle dimensioni minime del buffer richiesto. 

```c
mip_cc_result MIP_CC_ProtectionHandler_GetIssuedUser(
    const mip_cc_protection_handler handler,
    char* issuedUserBuffer,
    const int64_t issuedUserBufferSize,
    int64_t* actualIssuedUserSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectionhandler_getownersize"></a>MIP_CC_ProtectionHandler_GetOwnerSize

Ottiene le dimensioni del buffer necessarie per archiviare il proprietario del contenuto protetto

**Parameters**

Parametro | Descrizione
|---|---|
| gestore | Gestore che rappresenta il contenuto protetto |
| ownerSize | Output Dimensioni del buffer per l'utente rilasciato (in numero di caratteri) |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_ProtectionHandler_GetOwnerSize(
    const mip_cc_protection_handler handler,
    int64_t* ownerSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectionhandler_getowner"></a>MIP_CC_ProtectionHandler_GetOwner

Ottiene il proprietario del contenuto protetto

**Parameters**

Parametro | Descrizione
|---|---|
| gestore | Gestore che rappresenta il contenuto protetto |
| ownerBuffer | Output Buffer in cui verrà copiato l'utente emesso. |
| ownerBufferSize | Dimensioni (in numero di caratteri) di ownerBuffer. |
| actualOwnerSize | Output Numero di caratteri scritti nel buffer |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

**Nota**: se ownerBuffer è null o insufficiente, verrà restituito MIP_RESULT_ERROR_INSUFFICIENT_BUFFER e actualOwnerSize verrà impostato sulle dimensioni minime del buffer richiesto. 

```c
mip_cc_result MIP_CC_ProtectionHandler_GetOwner(
    const mip_cc_protection_handler handler,
    char* ownerBuffer,
    const int64_t ownerBufferSize,
    int64_t* actualOwnerSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectionhandler_getcontentid"></a>MIP_CC_ProtectionHandler_GetContentId

Ottiene il contenuto di IE del contenuto protetto

**Parameters**

Parametro | Descrizione
|---|---|
| gestore | Gestore che rappresenta il contenuto protetto |
| contentId | Output ID contenuto |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_ProtectionHandler_GetContentId(
    const mip_cc_protection_handler handler,
    mip_cc_guid* contentId,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectionhandler_doesusedeprecatedalgorithm"></a>MIP_CC_ProtectionHandler_DoesUseDeprecatedAlgorithm

Ottiene un valore che indica se il gestore della protezione utilizza un algoritmo di crittografia deprecato (BCE) per la compatibilità con le versioni precedenti

**Parameters**

Parametro | Descrizione
|---|---|
| gestore | Gestore che rappresenta il contenuto protetto |
| doesUseDeprecatedAlgorithm | Output Indica se il gestore della protezione usa un algoritmo di crittografia deprecato |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_ProtectionHandler_DoesUseDeprecatedAlgorithm(
    const mip_cc_protection_handler handler,
    bool* doesUseDeprecatedAlgorithm,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectionhandler_decryptbuffer"></a>MIP_CC_ProtectionHandler_DecryptBuffer

Decrittografare un buffer

**Parameters**

Parametro | Descrizione
|---|---|
| offsetFromStart | Posizione relativa di inputBuffer dall'inizio del contenuto crittografato |
| inputBuffer | Buffer di contenuto crittografato che verrà decrittografato |
| inputBufferSize | Dimensioni (in byte) del buffer di input |
| outputBuffer | Output Buffer in cui verrà copiato il contenuto decrittografato |
| outputBufferSize | Dimensioni (in byte) del buffer di output |
| documentoÈ | Se il buffer di input contiene i byte crittografati finali |
| actualDecryptedSize | Output Dimensioni effettive del contenuto crittografato (in byte) |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_ProtectionHandler_DecryptBuffer(
    const mip_cc_protection_handler handler,
    const int64_t offsetFromStart,
    const uint8_t* inputBuffer,
    const int64_t inputBufferSize,
    uint8_t* outputBuffer,
    const int64_t outputBufferSize,
    const bool isFinal,
    int64_t *actualDecryptedSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_releaseprotectionhandlerpublishingsettings"></a>MIP_CC_ReleaseProtectionHandlerPublishingSettings

Rilasciare le risorse associate a impostazioni del gestore protezione

**Parameters**

Parametro | Descrizione
|---|---|
| impostazioni | Impostazioni del gestore di protezione da rilasciare |

```c
void MIP_CC_ReleaseProtectionHandlerPublishingSettings(mip_cc_protection_handler_publishing_settings settings);
```

## <a name="mip_cc_releaseprotectionhandlerconsumptionsettings"></a>MIP_CC_ReleaseProtectionHandlerConsumptionSettings

Rilasciare le risorse associate a impostazioni del gestore protezione

**Parameters**

Parametro | Descrizione
|---|---|
| impostazioni | Impostazioni del gestore di protezione da rilasciare |

```c
void MIP_CC_ReleaseProtectionHandlerConsumptionSettings(mip_cc_protection_handler_consumption_settings settings);
```

## <a name="mip_cc_releaseprotectionhandler"></a>MIP_CC_ReleaseProtectionHandler

Rilasciare le risorse associate a un gestore protezione

**Parameters**

Parametro | Descrizione
|---|---|
| gestore | Gestore di protezione da rilasciare |

```c
void MIP_CC_ReleaseProtectionHandler(mip_cc_protection_handler handler);
```

## <a name="mip_cc_loadprotectionprofile"></a>MIP_CC_LoadProtectionProfile

Carica un profilo

**Parameters**

Parametro | Descrizione
|---|---|
| impostazioni | Impostazioni del profilo |
| profile | Output Istanza del profilo di protezione appena creata |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_LoadProtectionProfile(
    const mip_cc_protection_profile_settings settings,
    mip_cc_protection_profile* profile,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_releaseprotectionprofile"></a>MIP_CC_ReleaseProtectionProfile

Rilascia le risorse associate a un profilo di protezione

**Parameters**

Parametro | Descrizione
|---|---|
| profile | Profilo di protezione da rilasciare |

```c
void MIP_CC_ReleaseProtectionProfile(mip_cc_protection_profile profile);
```

## <a name="mip_cc_createprotectionprofilesettings"></a>MIP_CC_CreateProtectionProfileSettings

Creare un oggetto impostazioni utilizzato per creare un profilo di protezione

**Parameters**

Parametro | Descrizione
|---|---|
| mipContext | Contesto globale condiviso tra tutti i profili |
| cacheStorageType | Configurazione della cache di archiviazione |
| authCallback | Oggetto callback da usare per l'autenticazione, implementato dall'applicazione client |
| Dell'consentcallback | Oggetto callback da usare per il consenso, implementato dall'applicazione client |
| impostazioni | Output Istanza di impostazioni appena creata |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_CreateProtectionProfileSettings(
    const mip_cc_mip_context mipContext,
    const mip_cc_cache_storage_type cacheStorageType,
    const mip_cc_auth_callback authCallback,
    const mip_cc_consent_callback consentCallback,
    mip_cc_protection_profile_settings* settings,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectionprofilesettings_setsessionid"></a>MIP_CC_ProtectionProfileSettings_SetSessionId

Imposta l'ID di sessione che può essere usato per correlare i log e i dati di telemetria

**Parameters**

Parametro | Descrizione
|---|---|
| impostazioni | Impostazioni del profilo |
| sessionID | ID sessione che rappresenta la durata di un profilo di protezione |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_ProtectionProfileSettings_SetSessionId(
    const mip_cc_protection_profile_settings settings,
    const char* sessionId,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectionprofilesettings_setcancachelicenses"></a>MIP_CC_ProtectionProfileSettings_SetCanCacheLicenses

Configura se le licenze dell'utente finale (contratti) verranno memorizzate nella cache localmente

**Parameters**

Parametro | Descrizione
|---|---|
| impostazioni | Impostazioni del profilo |
| canCacheLicenses | Indica se il motore deve memorizzare nella cache una licenza quando apre il contenuto protetto |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_ProtectionProfileSettings_SetCanCacheLicenses(
    const mip_cc_protection_profile_settings settings,
    const bool canCacheLicenses,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectionprofilesettings_sethttpdelegate"></a>MIP_CC_ProtectionProfileSettings_SetHttpDelegate

Esegui override dello stack HTTP predefinito con il proprio client

**Parameters**

Parametro | Descrizione
|---|---|
| impostazioni | Impostazioni del profilo a cui verrà assegnato il delegato HTTP |
| httpDelegate | Istanza di callback HTTP implementata dall'applicazione client |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_ProtectionProfileSettings_SetHttpDelegate(
    const mip_cc_protection_profile_settings settings,
    const mip_cc_http_delegate httpDelegate,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectionprofilesettings_settaskdispatcherdelegate"></a>MIP_CC_ProtectionProfileSettings_SetTaskDispatcherDelegate

Esegui override del dispatcher attività asincrono predefinito con il proprio client

**Parameters**

Parametro | Descrizione
|---|---|
| impostazioni | Impostazioni del profilo a cui verrà assegnato il delegato del dispatcher attività |
| taskDispatcherDelegate | Istanza di callback Dispatcher attività implementata dall'applicazione client |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_ProtectionProfileSettings_SetTaskDispatcherDelegate(
    const mip_cc_protection_profile_settings settings,
    const mip_cc_task_dispatcher_delegate taskDispatcherDelegate,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectionprofilesettings_setcustomsettings"></a>MIP_CC_ProtectionProfileSettings_SetCustomSettings

Configura le impostazioni personalizzate, usate per il controllo e il controllo delle funzionalità.

**Parameters**

Parametro | Descrizione
|---|---|
| impostazioni | Impostazioni del profilo |
| customSettings | Coppie chiave/valore di impostazioni personalizzate |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_ProtectionProfileSettings_SetCustomSettings(
    const mip_cc_protection_profile_settings settings,
    const mip_cc_dictionary customSettings,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_releaseprotectionprofilesettings"></a>MIP_CC_ReleaseProtectionProfileSettings

Rilascia le risorse associate a impostazioni del profilo di protezione

**Parameters**

Parametro | Descrizione
|---|---|
| impostazioni | Impostazioni del profilo di protezione da rilasciare |

```c
void MIP_CC_ReleaseProtectionProfileSettings(mip_cc_protection_profile_settings profilsettingseSettings);
```

## <a name="mip_cc_templatedescriptor_getid"></a>MIP_CC_TemplateDescriptor_GetId

Ottiene l'ID modello

**Parameters**

Parametro | Descrizione
|---|---|
| protectionDescriptor | Descrittore associato al contenuto protetto |
| templateId | Output ID modello associato alla protezione |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_TemplateDescriptor_GetId(
    const mip_cc_template_descriptor protectionDescriptor,
    mip_cc_guid* templateId,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_templatedescriptor_getnamesize"></a>MIP_CC_TemplateDescriptor_GetNameSize

Ottiene le dimensioni del buffer necessarie per archiviare il nome

**Parameters**

Parametro | Descrizione
|---|---|
| templateDescriptor | Descrittore associato al modello |
| nameSize | Output Dimensione del buffer in cui memorizzare il nome (in numero di caratteri) |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_TemplateDescriptor_GetNameSize(
    const mip_cc_template_descriptor templateDescriptor,
    int64_t* nameSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_templatedescriptor_getname"></a>MIP_CC_TemplateDescriptor_GetName

Ottiene il nome del modello

**Parameters**

Parametro | Descrizione
|---|---|
| templateDescriptor | Descrittore associato al modello |
| nameBuffer | Output Buffer in cui verrà copiato il nome. |
| nameBufferSize | Dimensioni (in numero di caratteri) di nameBuffer. |
| actualNameSize | Output Numero di caratteri scritti nel buffer |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

**Nota**: se NameBuffer è null o insufficiente, verrà restituito MIP_RESULT_ERROR_INSUFFICIENT_BUFFER e actualNameSize verrà impostato sulle dimensioni minime del buffer richiesto. 

```c
mip_cc_result MIP_CC_TemplateDescriptor_GetName(
    const mip_cc_template_descriptor templateDescriptor,
    char* nameBuffer,
    const int64_t nameBufferSize,
    int64_t* actualNameSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_templatedescriptor_getdescriptionsize"></a>MIP_CC_TemplateDescriptor_GetDescriptionSize

Ottiene la dimensione del buffer necessaria per archiviare la descrizione

**Parameters**

Parametro | Descrizione
|---|---|
| templateDescriptor | Descrittore associato al modello |
| descriptionSize | Output Dimensione del buffer in cui memorizzare la descrizione (in numero di caratteri) |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_TemplateDescriptor_GetDescriptionSize(
    const mip_cc_template_descriptor templateDescriptor,
    int64_t* descriptionSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_templatedescriptor_getdescription"></a>MIP_CC_TemplateDescriptor_GetDescription

Ottiene la descrizione del modello

**Parameters**

Parametro | Descrizione
|---|---|
| templateDescriptor | Descrittore associato al modello |
| descriptionBuffer | Output Buffer in cui verrà copiata la descrizione. |
| descriptionBufferSize | Dimensioni (in numero di caratteri) di descriptionBuffer. |
| actualNameSize | Output Numero di caratteri scritti nel buffer |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

**Nota**: se descriptionBuffer è null o insufficiente, verrà restituito MIP_RESULT_ERROR_INSUFFICIENT_BUFFER e actualDescriptionSize verrà impostato sulle dimensioni minime del buffer richiesto. 

```c
mip_cc_result MIP_CC_TemplateDescriptor_GetDescription(
    const mip_cc_template_descriptor templateDescriptor,
    char* nameBuffer,
    const int64_t nameBufferSize,
    int64_t* actualNameSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_releasetemplatedescriptor"></a>MIP_CC_ReleaseTemplateDescriptor

Rilasciare le risorse associate a un descrittore di modello

**Parameters**

Parametro | Descrizione
|---|---|
| templateDescriptor | Descrittore del modello da rilasciare |

```c
void MIP_CC_ReleaseTemplateDescriptor(mip_cc_template_descriptor templateDescriptor);
```

## <a name="mip_cc_action_gettype"></a>MIP_CC_Action_GetType

Ottiene il tipo di un'azione

**Parameters**

Parametro | Descrizione
|---|---|
| action | Azione |
| actionType | Output Tipo di azione |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_Action_GetType(
    const mip_cc_action action,
    mip_cc_action_type* actionType,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_action_getid"></a>MIP_CC_Action_GetId

Ottiene l'ID di un'azione

**Parameters**

Parametro | Descrizione
|---|---|
| action | Azione |
| id | Output ID azione univoco |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_Action_GetId(
    const mip_cc_action action,
    mip_cc_guid* id,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_actionresult_getactions"></a>MIP_CC_ActionResult_GetActions

Ottenere azioni che compongono il risultato di un'azione

**Parameters**

Parametro | Descrizione
|---|---|
| actionResult | Risultato dell'azione di origine |
| Azioni | Output Matrice di azioni, memoria di proprietà dell'oggetto mip_cc_action_result |
| count | Output Numero di coppie chiave/valore |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

**Nota**: la memoria per ' actions ' è di proprietà dell'oggetto mip_cc_action_result, quindi non deve essere liberata in modo indipendente 

```c
mip_cc_result MIP_CC_ActionResult_GetActions(
    const mip_cc_action_result actionResult,
    mip_cc_action** actions,
    int64_t* count,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_releaseactionresult"></a>MIP_CC_ReleaseActionResult

Rilasciare le risorse associate al risultato di un'azione

**Parameters**

Parametro | Descrizione
|---|---|
| actionResult | Risultato dell'azione da rilasciare |

```c
void MIP_CC_ReleaseActionResult(mip_cc_action_result actionResult);
```

## <a name="mip_cc_addcontentfooteraction_getuielementnamesize"></a>MIP_CC_AddContentFooterAction_GetUIElementNameSize

Ottiene le dimensioni del buffer necessarie per archiviare il nome dell'elemento dell'interfaccia utente dell'azione "Aggiungi piè di pagina contenuto"

**Parameters**

Parametro | Descrizione
|---|---|
| action | azione "Aggiungi piè di pagina contenuto" |
| nameSize | Output Dimensione del buffer in cui memorizzare il nome dell'elemento dell'interfaccia utente (in numero di caratteri) |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_AddContentFooterAction_GetUIElementNameSize(
    const mip_cc_action action,
    int64_t* nameSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_addcontentfooteraction_getuielementname"></a>MIP_CC_AddContentFooterAction_GetUIElementName

Ottiene il nome dell'elemento dell'interfaccia utente dell'azione "Aggiungi piè di pagina contenuto"

**Parameters**

Parametro | Descrizione
|---|---|
| action | azione "Aggiungi piè di pagina contenuto" |
| nameBuffer | Output Buffer in cui verrà copiato il nome dell'elemento dell'interfaccia utente. |
| nameBufferSize | Dimensioni (in numero di caratteri) di nameBuffer. |
| actualNameSize | Output Numero di caratteri scritti nel buffer |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

**Nota**: se nameBuffer è null o insufficiente, verrà restituito MIP_RESULT_ERROR_INSUFFICIENT_BUFFER e actualNameSize verrà impostato sulle dimensioni minime del buffer richiesto. 

```c
mip_cc_result MIP_CC_AddContentFooterAction_GetUIElementName(
    const mip_cc_action action,
    char* nameBuffer,
    const int64_t nameBufferSize,
    int64_t* actualNameSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_addcontentfooteraction_gettextsize"></a>MIP_CC_AddContentFooterAction_GetTextSize

Ottiene le dimensioni del buffer necessarie per archiviare un testo dell'azione "Aggiungi piè di pagina contenuto"

**Parameters**

Parametro | Descrizione
|---|---|
| action | azione "Aggiungi piè di pagina contenuto" |
| nameSize | Output Dimensioni del buffer per il mantenimento del testo (in numero di caratteri) |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_AddContentFooterAction_GetTextSize(
    const mip_cc_action action,
    int64_t* textSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_addcontentfooteraction_gettext"></a>MIP_CC_AddContentFooterAction_GetText

Ottiene il testo dell'azione "Aggiungi piè di pagina contenuto"

**Parameters**

Parametro | Descrizione
|---|---|
| action | azione "Aggiungi piè di pagina contenuto" |
| textBuffer | Output Buffer in cui verrà copiato il testo. |
| textBufferSize | Dimensioni (in numero di caratteri) di textBuffer. |
| actualTextSize | Output Numero di caratteri scritti nel buffer |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

**Nota**: se TextBuffer è null o insufficiente, verrà restituito MIP_RESULT_ERROR_INSUFFICIENT_BUFFER e actualTextSize verrà impostato sulle dimensioni minime del buffer richiesto. 

```c
mip_cc_result MIP_CC_AddContentFooterAction_GetText(
    const mip_cc_action action,
    char* textBuffer,
    const int64_t textBufferSize,
    int64_t* actualTextSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_addcontentfooteraction_getfontnamesize"></a>MIP_CC_AddContentFooterAction_GetFontNameSize

Ottiene le dimensioni del buffer necessarie per archiviare il nome del tipo di carattere dell'azione "Aggiungi piè di pagina contenuto"

**Parameters**

Parametro | Descrizione
|---|---|
| action | azione "Aggiungi piè di pagina contenuto" |
| nameSize | Output Dimensione del buffer in cui memorizzare il nome del tipo di carattere (in numero di caratteri) |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_AddContentFooterAction_GetFontNameSize(
    const mip_cc_action action,
    int64_t* nameSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_addcontentfooteraction_getfontname"></a>MIP_CC_AddContentFooterAction_GetFontName

Ottiene il nome del tipo di carattere dell'azione "Aggiungi piè di pagina contenuto"

**Parameters**

Parametro | Descrizione
|---|---|
| action | azione "Aggiungi piè di pagina contenuto" |
| nameBuffer | Output Buffer in cui verrà copiato il nome del tipo di carattere. |
| nameBufferSize | Dimensioni (in numero di caratteri) di nameBuffer. |
| actualNameSize | Output Numero di caratteri scritti nel buffer |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

**Nota**: se nameBuffer è null o insufficiente, verrà restituito MIP_RESULT_ERROR_INSUFFICIENT_BUFFER e actualNameSize verrà impostato sulle dimensioni minime del buffer richiesto. 

```c
mip_cc_result MIP_CC_AddContentFooterAction_GetFontName(
    const mip_cc_action action,
    char* nameBuffer,
    const int64_t nameBufferSize,
    int64_t* actualNameSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_addcontentfooteraction_getfontsize"></a>MIP_CC_AddContentFooterAction_GetFontSize

Ottiene le dimensioni del carattere Integer

**Parameters**

Parametro | Descrizione
|---|---|
| action | azione "Aggiungi piè di pagina contenuto" |
| fontSize | Output Dimensioni carattere |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_AddContentFooterAction_GetFontSize(
    const mip_cc_action action,
    int32_t* fontSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_addcontentfooteraction_getfontcolorsize"></a>MIP_CC_AddContentFooterAction_GetFontColorSize

Ottiene le dimensioni del buffer necessarie per archiviare il colore del carattere dell'azione "Aggiungi piè di pagina contenuto"

**Parameters**

Parametro | Descrizione
|---|---|
| action | azione "Aggiungi piè di pagina contenuto" |
| colorSize | Output Dimensioni del buffer per mantenere il colore del carattere (in numero di caratteri) |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_AddContentFooterAction_GetFontColorSize(
    const mip_cc_action action,
    int64_t* colorSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_addcontentfooteraction_getfontcolor"></a>MIP_CC_AddContentFooterAction_GetFontColor

Ottiene il colore del carattere dell'azione "Aggiungi piè di pagina contenuto" (ad esempio, "#000000")

**Parameters**

Parametro | Descrizione
|---|---|
| action | azione "Aggiungi piè di pagina contenuto" |
| colorBuffer | Output Buffer in cui verrà copiato il colore del carattere. |
| colorBufferSize | Dimensioni (in numero di caratteri) di colorBuffer. |
| actualColorSize | Output Numero di caratteri scritti nel buffer |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

**Nota**: se colorBuffer è null o insufficiente, verrà restituito MIP_RESULT_ERROR_INSUFFICIENT_BUFFER e actualColorSize verrà impostato sulle dimensioni minime del buffer richiesto. 

```c
mip_cc_result MIP_CC_AddContentFooterAction_GetFontColor(
    const mip_cc_action action,
    char* colorBuffer,
    const int64_t colorBufferSize,
    int64_t* actualColorSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_addcontentfooteraction_getalignment"></a>MIP_CC_AddContentFooterAction_GetAlignment

Ottiene l'allineamento

**Parameters**

Parametro | Descrizione
|---|---|
| action | azione "Aggiungi piè di pagina contenuto" |
| allineamento | Output Allineamento |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_AddContentFooterAction_GetAlignment(
    const mip_cc_action action,
    mip_cc_content_mark_alignment* alignment,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_addcontentfooteraction_getmargin"></a>MIP_CC_AddContentFooterAction_GetMargin

Ottiene le dimensioni del margine

**Parameters**

Parametro | Descrizione
|---|---|
| action | azione "Aggiungi piè di pagina contenuto" |
| marginSize | Output Dimensioni margine (in mm) |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_AddContentFooterAction_GetMargin(
    const mip_cc_action action,
    int32_t* marginSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_addcontentheaderaction_getuielementnamesize"></a>MIP_CC_AddContentHeaderAction_GetUIElementNameSize

Ottiene le dimensioni del buffer necessarie per archiviare il nome dell'elemento dell'interfaccia utente dell'azione "Aggiungi intestazione contenuto"

**Parameters**

Parametro | Descrizione
|---|---|
| action | azione "Aggiungi intestazione contenuto" |
| nameSize | Output Dimensione del buffer in cui memorizzare il nome dell'elemento dell'interfaccia utente (in numero di caratteri) |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_AddContentHeaderAction_GetUIElementNameSize(
    const mip_cc_action action,
    int64_t* nameSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_addcontentheaderaction_getuielementname"></a>MIP_CC_AddContentHeaderAction_GetUIElementName

Ottiene il nome dell'elemento dell'interfaccia utente dell'azione "Aggiungi intestazione contenuto"

**Parameters**

Parametro | Descrizione
|---|---|
| action | azione "Aggiungi intestazione contenuto" |
| nameBuffer | Output Buffer in cui verrà copiato il nome dell'elemento dell'interfaccia utente. |
| nameBufferSize | Dimensioni (in numero di caratteri) di nameBuffer. |
| actualNameSize | Output Numero di caratteri scritti nel buffer |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

**Nota**: se nameBuffer è null o insufficiente, verrà restituito MIP_RESULT_ERROR_INSUFFICIENT_BUFFER e actualNameSize verrà impostato sulle dimensioni minime del buffer richiesto. 

```c
mip_cc_result MIP_CC_AddContentHeaderAction_GetUIElementName(
    const mip_cc_action action,
    char* nameBuffer,
    const int64_t nameBufferSize,
    int64_t* actualNameSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_addcontentheaderaction_gettextsize"></a>MIP_CC_AddContentHeaderAction_GetTextSize

Ottiene le dimensioni del buffer necessarie per archiviare il testo dell'azione "Aggiungi intestazione contenuto"

**Parameters**

Parametro | Descrizione
|---|---|
| action | azione "Aggiungi intestazione contenuto" |
| nameSize | Output Dimensioni del buffer per il mantenimento del testo (in numero di caratteri) |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_AddContentHeaderAction_GetTextSize(
    const mip_cc_action action,
    int64_t* textSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_addcontentheaderaction_gettext"></a>MIP_CC_AddContentHeaderAction_GetText

Ottiene il testo dell'azione "Aggiungi intestazione contenuto"

**Parameters**

Parametro | Descrizione
|---|---|
| action | azione "Aggiungi intestazione contenuto" |
| textBuffer | Output Buffer in cui verrà copiato il testo. |
| textBufferSize | Dimensioni (in numero di caratteri) di textBuffer. |
| actualTextSize | Output Numero di caratteri scritti nel buffer |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

**Nota**: se TextBuffer è null o insufficiente, verrà restituito MIP_RESULT_ERROR_INSUFFICIENT_BUFFER e actualTextSize verrà impostato sulle dimensioni minime del buffer richiesto. 

```c
mip_cc_result MIP_CC_AddContentHeaderAction_GetText(
    const mip_cc_action action,
    char* textBuffer,
    const int64_t textBufferSize,
    int64_t* actualTextSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_addcontentheaderaction_getfontnamesize"></a>MIP_CC_AddContentHeaderAction_GetFontNameSize

Ottiene le dimensioni del buffer necessarie per archiviare il nome del tipo di carattere dell'azione "Aggiungi intestazione contenuto"

**Parameters**

Parametro | Descrizione
|---|---|
| action | azione "Aggiungi intestazione contenuto" |
| nameSize | Output Dimensione del buffer in cui memorizzare il nome del tipo di carattere (in numero di caratteri) |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_AddContentHeaderAction_GetFontNameSize(
    const mip_cc_action action,
    int64_t* nameSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_addcontentheaderaction_getfontname"></a>MIP_CC_AddContentHeaderAction_GetFontName

Ottiene il nome del tipo di carattere dell'azione "Aggiungi intestazione contenuto"

**Parameters**

Parametro | Descrizione
|---|---|
| action | azione "Aggiungi intestazione contenuto" |
| nameBuffer | Output Buffer in cui verrà copiato il nome del tipo di carattere. |
| nameBufferSize | Dimensioni (in numero di caratteri) di nameBuffer. |
| actualNameSize | Output Numero di caratteri scritti nel buffer |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

**Nota**: se nameBuffer è null o insufficiente, verrà restituito MIP_RESULT_ERROR_INSUFFICIENT_BUFFER e actualNameSize verrà impostato sulle dimensioni minime del buffer richiesto. 

```c
mip_cc_result MIP_CC_AddContentHeaderAction_GetFontName(
    const mip_cc_action action,
    char* nameBuffer,
    const int64_t nameBufferSize,
    int64_t* actualNameSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_addcontentheaderaction_getfontsize"></a>MIP_CC_AddContentHeaderAction_GetFontSize

Ottiene le dimensioni del carattere Integer

**Parameters**

Parametro | Descrizione
|---|---|
| action | azione "Aggiungi intestazione contenuto" |
| fontSize | Output Dimensioni carattere |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_AddContentHeaderAction_GetFontSize(
    const mip_cc_action action,
    int32_t* fontSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_addcontentheaderaction_getfontcolorsize"></a>MIP_CC_AddContentHeaderAction_GetFontColorSize

Ottiene le dimensioni del buffer necessarie per archiviare il colore del carattere dell'azione "Aggiungi intestazione contenuto"

**Parameters**

Parametro | Descrizione
|---|---|
| action | azione "Aggiungi intestazione contenuto" |
| colorSize | Output Dimensioni del buffer per mantenere il colore del carattere (in numero di caratteri) |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_AddContentHeaderAction_GetFontColorSize(
    const mip_cc_action action,
    int64_t* colorSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_addcontentheaderaction_getfontcolor"></a>MIP_CC_AddContentHeaderAction_GetFontColor

Ottiene il colore del carattere dell'azione "Aggiungi intestazione contenuto", ad esempio "#000000".

**Parameters**

Parametro | Descrizione
|---|---|
| action | azione "Aggiungi intestazione contenuto" |
| colorBuffer | Output Buffer in cui verrà copiato il colore del carattere. |
| colorBufferSize | Dimensioni (in numero di caratteri) di colorBuffer. |
| actualColorSize | Output Numero di caratteri scritti nel buffer |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

**Nota**: se colorBuffer è null o insufficiente, verrà restituito MIP_RESULT_ERROR_INSUFFICIENT_BUFFER e actualColorSize verrà impostato sulle dimensioni minime del buffer richiesto. 

```c
mip_cc_result MIP_CC_AddContentHeaderAction_GetFontColor(
    const mip_cc_action action,
    char* colorBuffer,
    const int64_t colorBufferSize,
    int64_t* actualColorSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_addcontentheaderaction_getalignment"></a>MIP_CC_AddContentHeaderAction_GetAlignment

Ottiene l'allineamento

**Parameters**

Parametro | Descrizione
|---|---|
| action | azione "Aggiungi intestazione contenuto" |
| allineamento | Output Allineamento |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_AddContentHeaderAction_GetAlignment(
    const mip_cc_action action,
    mip_cc_content_mark_alignment* alignment,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_addcontentheaderaction_getmargin"></a>MIP_CC_AddContentHeaderAction_GetMargin

Ottiene le dimensioni del margine

**Parameters**

Parametro | Descrizione
|---|---|
| action | azione "Aggiungi intestazione contenuto" |
| marginSize | Output Dimensioni margine (in mm) |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_AddContentHeaderAction_GetMargin(
    const mip_cc_action action,
    int32_t* marginSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_addwatermarkaction_getuielementnamesize"></a>MIP_CC_AddWatermarkAction_GetUIElementNameSize

Ottiene le dimensioni del buffer necessarie per archiviare il nome dell'elemento dell'interfaccia utente dell'azione "add watermark"

**Parameters**

Parametro | Descrizione
|---|---|
| action | azione "Aggiungi filigrana" |
| nameSize | Output Dimensione del buffer in cui memorizzare il nome dell'elemento dell'interfaccia utente (in numero di caratteri) |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_AddWatermarkAction_GetUIElementNameSize(
    const mip_cc_action action,
    int64_t* nameSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_addwatermarkaction_getuielementname"></a>MIP_CC_AddWatermarkAction_GetUIElementName

Ottiene il nome dell'elemento dell'interfaccia utente dell'azione "Aggiungi filigrana"

**Parameters**

Parametro | Descrizione
|---|---|
| action | azione "Aggiungi filigrana" |
| nameBuffer | Output Buffer in cui verrà copiato il nome dell'elemento dell'interfaccia utente. |
| nameBufferSize | Dimensioni (in numero di caratteri) di nameBuffer. |
| actualNameSize | Output Numero di caratteri scritti nel buffer |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

**Nota**: se nameBuffer è null o insufficiente, verrà restituito MIP_RESULT_ERROR_INSUFFICIENT_BUFFER e actualNameSize verrà impostato sulle dimensioni minime del buffer richiesto. 

```c
mip_cc_result MIP_CC_AddWatermarkAction_GetUIElementName(
    const mip_cc_action action,
    char* nameBuffer,
    const int64_t nameBufferSize,
    int64_t* actualNameSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_addwatermarkaction_getlayout"></a>MIP_CC_AddWatermarkAction_GetLayout

Ottiene il layout della filigrana

**Parameters**

Parametro | Descrizione
|---|---|
| action | azione "Aggiungi filigrana" |
| layout | Output Layout filigrana |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_AddWatermarkAction_GetLayout(
    const mip_cc_action action,
    mip_cc_watermark_layout* layout,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_addwatermarkaction_gettextsize"></a>MIP_CC_AddWatermarkAction_GetTextSize

Ottiene le dimensioni del buffer necessarie per archiviare il testo dell'azione "Aggiungi filigrana"

**Parameters**

Parametro | Descrizione
|---|---|
| action | azione "Aggiungi filigrana" |
| textSize | Output Dimensioni del buffer per il mantenimento del testo (in numero di caratteri) |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_AddWatermarkAction_GetTextSize(
    const mip_cc_action action,
    int64_t* textSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_addwatermarkaction_gettext"></a>MIP_CC_AddWatermarkAction_GetText

Ottiene il testo dell'azione "Aggiungi filigrana"

**Parameters**

Parametro | Descrizione
|---|---|
| action | azione "Aggiungi filigrana" |
| textBuffer | Output Buffer in cui verrà copiato il testo. |
| textBufferSize | Dimensioni (in numero di caratteri) di textBuffer. |
| actualTextSize | Output Numero di caratteri scritti nel buffer |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

**Nota**: se TextBuffer è null o insufficiente, verrà restituito MIP_RESULT_ERROR_INSUFFICIENT_BUFFER e actualTextSize verrà impostato sulle dimensioni minime del buffer richiesto. 

```c
mip_cc_result MIP_CC_AddWatermarkAction_GetText(
    const mip_cc_action action,
    char* textBuffer,
    const int64_t textBufferSize,
    int64_t* actualTextSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_addwatermarkaction_getfontnamesize"></a>MIP_CC_AddWatermarkAction_GetFontNameSize

Ottiene le dimensioni del buffer necessarie per archiviare il nome del tipo di carattere dell'azione "Aggiungi filigrana"

**Parameters**

Parametro | Descrizione
|---|---|
| action | azione "Aggiungi filigrana" |
| nameSize | Output Dimensione del buffer in cui memorizzare il nome del tipo di carattere (in numero di caratteri) |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_AddWatermarkAction_GetFontNameSize(
    const mip_cc_action action,
    int64_t* nameSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_addwatermarkaction_getfontname"></a>MIP_CC_AddWatermarkAction_GetFontName

Ottiene il nome del tipo di carattere dell'azione "Aggiungi filigrana"

**Parameters**

Parametro | Descrizione
|---|---|
| action | azione "Aggiungi filigrana" |
| nameBuffer | Output Buffer in cui verrà copiato il nome del tipo di carattere. |
| nameBufferSize | Dimensioni (in numero di caratteri) di nameBuffer. |
| actualNameSize | Output Numero di caratteri scritti nel buffer |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

**Nota**: se nameBuffer è null o insufficiente, verrà restituito MIP_RESULT_ERROR_INSUFFICIENT_BUFFER e actualNameSize verrà impostato sulle dimensioni minime del buffer richiesto. 

```c
mip_cc_result MIP_CC_AddWatermarkAction_GetFontName(
    const mip_cc_action action,
    char* nameBuffer,
    const int64_t nameBufferSize,
    int64_t* actualNameSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_addwatermarkaction_getfontsize"></a>MIP_CC_AddWatermarkAction_GetFontSize

Ottiene le dimensioni del carattere Integer

**Parameters**

Parametro | Descrizione
|---|---|
| action | azione "Aggiungi filigrana" |
| fontSize | Output Dimensioni carattere |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_AddWatermarkAction_GetFontSize(
    const mip_cc_action action,
    int32_t* fontSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_addwatermarkaction_getfontcolorsize"></a>MIP_CC_AddWatermarkAction_GetFontColorSize

Ottiene le dimensioni del buffer necessarie per archiviare il colore del carattere dell'azione "Aggiungi filigrana"

**Parameters**

Parametro | Descrizione
|---|---|
| action | azione "Aggiungi filigrana" |
| colorSize | Output Dimensioni del buffer per mantenere il colore del carattere (in numero di caratteri) |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_AddWatermarkAction_GetFontColorSize(
    const mip_cc_action action,
    int64_t* colorSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_addwatermarkaction_getfontcolor"></a>MIP_CC_AddWatermarkAction_GetFontColor

Ottiene il colore del carattere dell'azione "Aggiungi filigrana" (ad esempio, "#000000")

**Parameters**

Parametro | Descrizione
|---|---|
| action | azione "Aggiungi filigrana" |
| colorBuffer | Output Buffer in cui verrà copiato il colore del carattere. |
| colorBufferSize | Dimensioni (in numero di caratteri) di colorBuffer. |
| actualColorSize | Output Numero di caratteri scritti nel buffer |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

**Nota**: se colorBuffer è null o insufficiente, verrà restituito MIP_RESULT_ERROR_INSUFFICIENT_BUFFER e actualColorSize verrà impostato sulle dimensioni minime del buffer richiesto. 

```c
mip_cc_result MIP_CC_AddWatermarkAction_GetFontColor(
    const mip_cc_action action,
    char* colorBuffer,
    const int64_t colorBufferSize,
    int64_t* actualColorSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_releasecontentlabel"></a>MIP_CC_ReleaseContentLabel

Rilasciare le risorse associate a un'etichetta di contenuto

**Parameters**

Parametro | Descrizione
|---|---|
| contentLabel | Etichetta da rilasciare |

```c
void MIP_CC_ReleaseContentLabel(mip_cc_content_label contentLabel);
```

## <a name="mip_cc_contentlabel_getcreationtime"></a>MIP_CC_ContentLabel_GetCreationTime

Ottiene l'ora in cui è stata applicata l'etichetta

**Parameters**

Parametro | Descrizione
|---|---|
| contentLabel | Etichetta |
| creationTime | Output Ora di applicazione dell'etichetta al documento (in secondi da Epoch) |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_ContentLabel_GetCreationTime(
    const mip_cc_content_label contentLabel,
    int64_t* creationTime,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_contentlabel_getassignmentmethod"></a>MIP_CC_ContentLabel_GetAssignmentMethod

Ottiene il metodo di assegnazione dell'etichetta

**Parameters**

Parametro | Descrizione
|---|---|
| contentLabel | Etichetta |
| assignmentMethod | Output Metodo di assegnazione (ad esempio ' standard ' o ' privileged ') |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_ContentLabel_GetAssignmentMethod(
    const mip_cc_content_label contentLabel,
    mip_cc_label_assignment_method* assignmentMethod,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_contentlabel_getextendedproperties"></a>MIP_CC_ContentLabel_GetExtendedProperties

Ottiene le proprietà estese

**Parameters**

Parametro | Descrizione
|---|---|
| contentLabel | Etichetta |
| properties | Output Dizionario di proprietà estese, memoria di proprietà del chiamante |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

**Nota**: la variabile ' Properties ' deve essere rilasciata dal chiamante chiamando MIP_CC_ReleaseDictionary 

```c
mip_cc_result MIP_CC_ContentLabel_GetExtendedProperties(
    const mip_cc_content_label contentLabel,
    mip_cc_metadata_dictionary* properties,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_contentlabel_isprotectionappliedfromlabel"></a>MIP_CC_ContentLabel_IsProtectionAppliedFromLabel

Ottiene un valore che indica se una protezione è stata applicata da un'etichetta.

**Parameters**

Parametro | Descrizione
|---|---|
| contentLabel | Etichetta |
| isProtectionAppliedByLabel | Output Se il documento è protetto e la protezione è stata applicata in modo esplicito da questa etichetta. |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_ContentLabel_IsProtectionAppliedFromLabel(
    const mip_cc_content_label contentLabel,
    bool* isProtectionAppliedByLabel,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_contentlabel_getlabel"></a>MIP_CC_ContentLabel_GetLabel

Ottiene le proprietà dell'etichetta generica da un'istanza dell'etichetta di contenuto

**Parameters**

Parametro | Descrizione
|---|---|
| contentLabel | Etichetta |
| label | Output Etichetta generica, memoria di proprietà del chiamante |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

**Nota**: la variabile ' label ' deve essere rilasciata dal chiamante chiamando MIP_CC_ReleaseLabel 

```c
mip_cc_result MIP_CC_ContentLabel_GetLabel(
    const mip_cc_content_label contentLabel,
    mip_cc_label* label,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_customaction_getnamesize"></a>MIP_CC_CustomAction_GetNameSize

Ottiene le dimensioni del buffer necessarie per archiviare il nome di un'azione "personalizzata"

**Parameters**

Parametro | Descrizione
|---|---|
| action | azione "personalizzata" |
| nameSize | Output Dimensione del buffer in cui memorizzare il nome (in numero di caratteri) |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_CustomAction_GetNameSize(
    const mip_cc_action action,
    int64_t* nameSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_customaction_getname"></a>MIP_CC_CustomAction_GetName

Ottiene il nome di un'azione "personalizzata"

**Parameters**

Parametro | Descrizione
|---|---|
| action | azione "personalizzata" |
| nameBuffer | Output Buffer in cui verrà copiato il nome. |
| nameBufferSize | Dimensioni (in numero di caratteri) di nameBuffer. |
| actualNameSize | Output Numero di caratteri scritti nel buffer |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

**Nota**: se nameBuffer è null o insufficiente, verrà restituito MIP_RESULT_ERROR_INSUFFICIENT_BUFFER e actualNameSize verrà impostato sulle dimensioni minime del buffer richiesto. 

```c
mip_cc_result MIP_CC_CustomAction_GetName(
    const mip_cc_action action,
    char* nameBuffer,
    const int64_t nameBufferSize,
    int64_t* actualNameSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_customaction_getproperties"></a>MIP_CC_CustomAction_GetProperties

Ottiene le proprietà di un'azione "personalizzata".

**Parameters**

Parametro | Descrizione
|---|---|
| action | azione "personalizzata" |
| properties | Output Dizionario di proprietà, memoria di proprietà del chiamante |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

**Nota**: la variabile ' Properties ' deve essere rilasciata dal chiamante chiamando MIP_CC_ReleaseDictionary 

```c
mip_cc_result MIP_CC_CustomAction_GetProperties(
    const mip_cc_action action,
    mip_cc_dictionary* properties,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_metadata_callback"></a>mip_cc_metadata_callback

Definizione della funzione di callback per recuperare il documento metatdata, filtrato in base al nome e al prefisso

**Parameters**

Parametro | Descrizione
|---|---|
| nomi | Matrice di nomi di chiavi di metadati da includere nel risultato |
| namesSize | Numero di valori nella matrice ' names ' |
| namePrefixes | Matrice di prefissi dei nomi di chiave dei metadati da includere nel risultato |
| namePrefixesSize | Numero di valori nella matrice ' namesPrefixes ' |
| contesto | Il contesto dell'applicazione è stato passato in modo opaco dalla chiamata API al callback |
| metadata | Output Dizionario della chiave/valori dei metadati, creato dall'applicazione client. Questo dizionario verrà rilasciato da MIP. |

```c
MIP_CC_CALLBACK(mip_cc_metadata_callback,
    void,
    const char**,
    const int64_t,
    const char**,
    const int64_t,
    const void*,
    mip_cc_metadata_dictionary*);
```

## <a name="mip_cc_releaselabel"></a>MIP_CC_ReleaseLabel

Rilasciare le risorse associate a un'etichetta

**Parameters**

Parametro | Descrizione
|---|---|
| label | Etichetta da rilasciare |

```c
void MIP_CC_ReleaseLabel(mip_cc_label label);
```

## <a name="mip_cc_label_getid"></a>MIP_CC_Label_GetId

Ottiene l'ID etichetta

**Parameters**

Parametro | Descrizione
|---|---|
| label | Etichetta |
| labelId | Output ID etichetta |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_Label_GetId(
    const mip_cc_label label,
    mip_cc_guid* labelId,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_label_getnamesize"></a>MIP_CC_Label_GetNameSize

Ottiene le dimensioni del buffer necessarie per archiviare il nome

**Parameters**

Parametro | Descrizione
|---|---|
| label | Etichetta |
| nameSize | Output Dimensione del buffer in cui memorizzare il nome (in numero di caratteri) |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_Label_GetNameSize(
    const mip_cc_label label,
    int64_t* nameSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_label_getname"></a>MIP_CC_Label_GetName

Ottiene il nome dell'etichetta

**Parameters**

Parametro | Descrizione
|---|---|
| label | Etichetta |
| nameBuffer | Output Buffer in cui verrà copiato il nome. |
| nameBufferSize | Dimensioni (in numero di caratteri) di nameBuffer. |
| actualNameSize | Output Numero di caratteri scritti nel buffer |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

**Nota**: se nameBuffer è null o insufficiente, verrà restituito MIP_RESULT_ERROR_INSUFFICIENT_BUFFER e actualNameSize verrà impostato sulle dimensioni minime del buffer richiesto. 

```c
mip_cc_result MIP_CC_Label_GetName(
    const mip_cc_label label,
    char* nameBuffer,
    const int64_t nameBufferSize,
    int64_t* actualNameSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_label_getdescriptionsize"></a>MIP_CC_Label_GetDescriptionSize

Ottiene la dimensione del buffer necessaria per archiviare la descrizione

**Parameters**

Parametro | Descrizione
|---|---|
| label | Etichetta |
| descriptionSize | Output Dimensione del buffer in cui memorizzare la descrizione (in numero di caratteri) |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_Label_GetDescriptionSize(
    const mip_cc_label label,
    int64_t* descriptionSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_label_getdescription"></a>MIP_CC_Label_GetDescription

Ottiene la descrizione dell'etichetta

**Parameters**

Parametro | Descrizione
|---|---|
| label | Etichetta |
| descriptionBuffer | Output Buffer in cui verrà copiata la descrizione. |
| descriptionBufferSize | Dimensioni (in numero di caratteri) di descriptionBuffer. |
| actualDescriptionSize | Output Numero di caratteri scritti nel buffer |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

**Nota**: se descriptionBuffer è null o insufficiente, verrà restituito MIP_RESULT_ERROR_INSUFFICIENT_BUFFER e actualDescriptionSize verrà impostato sulle dimensioni minime del buffer richiesto. 

```c
mip_cc_result MIP_CC_Label_GetDescription(
    const mip_cc_label label,
    char* descriptionBuffer,
    const int64_t descriptionBufferSize,
    int64_t* actualDescriptionSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_label_getcolorsize"></a>MIP_CC_Label_GetColorSize

Ottiene le dimensioni del buffer necessarie per archiviare il colore

**Parameters**

Parametro | Descrizione
|---|---|
| label | Etichetta |
| colorSize | Output Dimensione del buffer in cui mantenere il colore (in numero di caratteri) |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_Label_GetColorSize(
    const mip_cc_label label,
    int64_t* colorSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_label_getcolor"></a>MIP_CC_Label_GetColor

Ottiene il colore dell'etichetta

**Parameters**

Parametro | Descrizione
|---|---|
| label | Etichetta |
| colorBuffer | Output Buffer in cui verrà copiato il colore (in #RRGGBB formato). |
| colorBufferSize | Dimensioni (in numero di caratteri) di colorBuffer. |
| actualColorSize | Output Numero di caratteri scritti nel buffer |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

**Nota**: se colorBuffer è null o insufficiente, verrà restituito MIP_RESULT_ERROR_INSUFFICIENT_BUFFER e actualColorSize verrà impostato sulle dimensioni minime del buffer richiesto. 

```c
mip_cc_result MIP_CC_Label_GetColor(
    const mip_cc_label label,
    char* colorBuffer,
    const int64_t colorBufferSize,
    int64_t* actualColorSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_label_getsensitivity"></a>MIP_CC_Label_GetSensitivity

Ottiene il livello di sensibilità dell'etichetta. Un valore più alto significa più sensibile.

**Parameters**

Parametro | Descrizione
|---|---|
| label | Etichetta |
| sensitivity | Output Livello di riservatezza |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_Label_GetSensitivity(
    const mip_cc_label label,
    int32_t* sensitivity,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_label_gettooltipsize"></a>MIP_CC_Label_GetTooltipSize

Ottiene le dimensioni del buffer necessarie per archiviare la descrizione comando

**Parameters**

Parametro | Descrizione
|---|---|
| label | Etichetta |
| tooltipSize | Output Dimensione del buffer in cui memorizzare la descrizione comando (in numero di caratteri) |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_Label_GetTooltipSize(
    const mip_cc_label label,
    int64_t* tooltipSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_label_gettooltip"></a>MIP_CC_Label_GetTooltip

Ottiene la descrizione comando dell'etichetta

**Parameters**

Parametro | Descrizione
|---|---|
| label | Etichetta |
| tooltipBuffer | Output Buffer in cui verrà copiata la descrizione comando. |
| tooltipBufferSize | Dimensioni (in numero di caratteri) di tooltipBuffer. |
| actualTooltipSize | Output Numero di caratteri scritti nel buffer |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

**Nota**: se tooltipBuffer è null o insufficiente, verrà restituito MIP_RESULT_ERROR_INSUFFICIENT_BUFFER e actualTooltipSize verrà impostato sulle dimensioni minime del buffer richiesto. 

```c
mip_cc_result MIP_CC_Label_GetTooltip(
    const mip_cc_label label,
    char* tooltipBuffer,
    const int64_t tooltipBufferSize,
    int64_t* actualTooltipSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_label_getautotooltipsize"></a>MIP_CC_Label_GetAutoTooltipSize

Ottiene la dimensione del buffer necessaria per archiviare la descrizione comando di classificazione automatica

**Parameters**

Parametro | Descrizione
|---|---|
| label | Etichetta |
| tooltipSize | Output Dimensione del buffer in cui memorizzare la descrizione comando (in numero di caratteri) |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_Label_GetAutoTooltipSize(
    const mip_cc_label label,
    int64_t* tooltipSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_label_getautotooltip"></a>MIP_CC_Label_GetAutoTooltip

Ottiene la descrizione comando per la classificazione automatica delle etichette

**Parameters**

Parametro | Descrizione
|---|---|
| label | Etichetta |
| tooltipBuffer | Output Buffer in cui verrà copiata la descrizione comando. |
| tooltipBufferSize | Dimensioni (in numero di caratteri) di tooltipBuffer. |
| actualTooltipSize | Output Numero di caratteri scritti nel buffer |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

**Nota**: se tooltipBuffer è null o insufficiente, verrà restituito MIP_RESULT_ERROR_INSUFFICIENT_BUFFER e actualTooltipSize verrà impostato sulle dimensioni minime del buffer richiesto. 

```c
mip_cc_result MIP_CC_Label_GetAutoTooltip(
    const mip_cc_label label,
    char* tooltipBuffer,
    const int64_t tooltipBufferSize,
    int64_t* actualTooltipSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_label_isactive"></a>MIP_CC_Label_IsActive

Ottiene un valore che indica se un'etichetta è attiva o meno.

**Parameters**

Parametro | Descrizione
|---|---|
| label | Etichetta |
| isActive | Output Indica se un'etichetta è considerata attiva. |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

**Nota**: è possibile applicare solo le etichette attive. Non è possibile applicare le etichette Inactivte e vengono usate solo a scopo di visualizzazione. 

```c
mip_cc_result MIP_CC_Label_IsActive(
    const mip_cc_label label,
    bool* isActive,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_label_getparent"></a>MIP_CC_Label_GetParent

Ottiene l'etichetta padre, se disponibile.

**Parameters**

Parametro | Descrizione
|---|---|
| label | Etichetta |
| padre | Output Etichetta padre, se presente, else null |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_Label_GetParent(
    const mip_cc_label label,
    mip_cc_label* parent,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_label_getchildrensize"></a>MIP_CC_Label_GetChildrenSize

Ottiene il numero di etichette figlio

**Parameters**

Parametro | Descrizione
|---|---|
| label | Etichetta |
| bambiniDimensione | Output Numero di elementi figlio |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_Label_GetChildrenSize(
    const mip_cc_label label,
    int64_t* childrenSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_label_getchildren"></a>MIP_CC_Label_GetChildren

Ottiene le etichette figlio

**Parameters**

Parametro | Descrizione
|---|---|
| label | Etichetta |
| childrenBuffer | Output Buffer in cui verranno copiate le etichette figlio. Etichette figlio |
| childrenBufferSize | Dimensioni (in numero di etichette) di childrenBuffer. |
| actualChildrenSize | Output Numero di etichette figlio scritte nel buffer |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

**Nota**: se childrenBuffer è null o insufficiente, verrà restituito MIP_RESULT_ERROR_INSUFFICIENT_BUFFER e actualChildrenSize verrà impostato sulle dimensioni minime del buffer richieste 

```c
mip_cc_result MIP_CC_Label_GetChildren(
    const mip_cc_label label,
    mip_cc_label* childrenBuffer,
    const int64_t childrenBufferSize,
    int64_t* actualChildrenSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_label_getcustomsettings"></a>MIP_CC_Label_GetCustomSettings

Ottiene le impostazioni personalizzate definite dal criterio di un'etichetta

**Parameters**

Parametro | Descrizione
|---|---|
| label | Etichetta |
| impostazioni | Output Dizionario di impostazioni, di proprietà del chiamante |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

**Nota**: la variabile ' Settings ' deve essere rilasciata dal chiamante chiamando MIP_CC_ReleaseDictionary 

```c
mip_cc_result MIP_CC_Label_GetCustomSettings(
    const mip_cc_label label,
    mip_cc_dictionary* settings,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_metadataaction_getmetadatatoremove"></a>MIP_CC_MetadataAction_GetMetadataToRemove

Ottiene i metadati dell'azione "Metadata" da rimuovere

**Parameters**

Parametro | Descrizione
|---|---|
| action | azione "metadati" |
| metadataNames | Output Nomi chiave dei metadati da rimuovere, memoria di proprietà del chiamante |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

**Nota**: la variabile ' metadataNames ' deve essere rilasciata dal chiamante chiamando MIP_CC_ReleaseStringList la @note rimozione dei metadati deve essere eseguita prima di aggiungere i metadati 

```c
mip_cc_result MIP_CC_MetadataAction_GetMetadataToRemove(
    const mip_cc_action action,
    mip_cc_string_list* metadataNames,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_metadataaction_getmetadatatoadd"></a>MIP_CC_MetadataAction_GetMetadataToAdd

Ottiene i metadati dell'azione "Metadata" da aggiungere

**Parameters**

Parametro | Descrizione
|---|---|
| action | azione "metadati" |
| metadata | [Output] elenco di voci di metadati da aggiungere, memoria di proprietà del chiamante |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

**Nota**: la variabile ' Metadata ' deve essere rilasciata dal chiamante chiamando MIP_CC_ReleaseDictionary la @note rimozione dei metadati deve essere eseguita prima di aggiungere i metadati 

```c
mip_cc_result MIP_CC_MetadataAction_GetMetadataToAdd(
    const mip_cc_action action,
    mip_cc_metadata_dictionary* metadata,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_createmetadatadictionary"></a>MIP_CC_CreateMetadataDictionary

Creare un dizionario di chiavi/valori stringa

**Parameters**

Parametro | Descrizione
|---|---|
| entries | Matrice di voci di metadati |
| count | Numero di voci di metadati |
| dictionary | Output Dizionario appena creato |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

**Nota**: è necessario liberare un mip_cc_dictionary chiamando MIP_CC_ReleaseDictionary 

```c
mip_cc_result MIP_CC_CreateMetadataDictionary(
    const mip_cc_metadata_entry* entries,
    const int64_t count,
    mip_cc_metadata_dictionary* dictionary,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_metadatadictionary_getentries"></a>MIP_CC_MetadataDictionary_GetEntries

Ottenere le voci di metadati che compongono un dizionario

**Parameters**

Parametro | Descrizione
|---|---|
| dictionary | Dizionario di origine |
| entries | Output Matrice di voci di metadati, memoria di proprietà dell'oggetto mip_cc_dictionary |
| count | Output Numero di voci di metadati |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

**Nota**: la memoria per ' voci ' è di proprietà dell'oggetto mip_cc_dictionary, quindi non deve essere liberata in modo indipendente 

```c
mip_cc_result MIP_CC_MetadataDictionary_GetEntries(
    const mip_cc_metadata_dictionary dictionary,
    mip_cc_metadata_entry** entries,
    int64_t* count,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_releasemetadatadictionary"></a>MIP_CC_ReleaseMetadataDictionary

Rilasciare le risorse associate a un dizionario

**Parameters**

Parametro | Descrizione
|---|---|
| dictionary | Dizionario da rilasciare |

```c
void MIP_CC_ReleaseMetadataDictionary(mip_cc_metadata_dictionary dictionary);
```

## <a name="mip_cc_releasepolicyengine"></a>MIP_CC_ReleasePolicyEngine

Rilasciare le risorse associate a un motore dei criteri

**Parameters**

Parametro | Descrizione
|---|---|
| motore | Motore dei criteri da rilasciare |

```c
void MIP_CC_ReleasePolicyEngine(mip_cc_policy_engine engine);
```

## <a name="mip_cc_policyengine_getengineidsize"></a>MIP_CC_PolicyEngine_GetEngineIdSize

Ottiene le dimensioni del buffer necessario per l'ID del motore

**Parameters**

Parametro | Descrizione
|---|---|
| motore | Motore dei criteri |
| idSize | Output Dimensione del buffer in cui memorizzare l'ID del motore (in numero di caratteri) |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_PolicyEngine_GetEngineIdSize(
    const mip_cc_policy_engine engine,
    int64_t* idSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_policyengine_getengineid"></a>MIP_CC_PolicyEngine_GetEngineId

Ottiene l'ID del motore

**Parameters**

Parametro | Descrizione
|---|---|
| motore | Motore dei criteri |
| idBuffer | Output Buffer in cui verrà copiato l'ID. |
| idBufferSize | Dimensioni (in numero di caratteri) di idBuffer. |
| actualIdSize | Output Numero di caratteri scritti nel buffer |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

**Nota**: se idBuffer è null o insufficiente, verrà restituito MIP_RESULT_ERROR_INSUFFICIENT_BUFFER e actualIdSize verrà impostato sulle dimensioni minime del buffer richiesto. 

```c
mip_cc_result MIP_CC_PolicyEngine_GetEngineId(
    const mip_cc_policy_engine engine,
    char* idBuffer,
    const int64_t idBufferSize,
    int64_t* actualIdSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_policyengine_getmoreinfourlsize"></a>MIP_CC_PolicyEngine_GetMoreInfoUrlSize

Ottiene le dimensioni dei dati client associati a un motore di criteri

**Parameters**

Parametro | Descrizione
|---|---|
| motore | Motore dei criteri |
| moreInfoUrlSize | Output Dimensioni dei dati client (in numero di caratteri) |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_PolicyEngine_GetMoreInfoUrlSize(
    const mip_cc_policy_engine engine,
    int64_t* moreInfoUrlSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_policyengine_getmoreinfourl"></a>MIP_CC_PolicyEngine_GetMoreInfoUrl

Ottenere i dati client associati a un motore dei criteri

**Parameters**

Parametro | Descrizione
|---|---|
| motore | Motore dei criteri |
| moreInfoUrlBuffer | Output Buffer in cui verranno copiati i dati client |
| moreInfoUrlBufferSize | Dimensioni (in numero di caratteri) di moreInfoUrlBuffer. |
| actualMoreInfoUrlSize | Output Numero di caratteri scritti nel buffer |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

**Nota**: se moreInfoUrlBuffer è null o insufficiente, verrà restituito MIP_RESULT_ERROR_INSUFFICIENT_BUFFER e actualMoreInfoUrlSize verrà impostato sulle dimensioni minime del buffer richiesto. 

```c
mip_cc_result MIP_CC_PolicyEngine_GetMoreInfoUrl(
    const mip_cc_policy_engine engine,
    char* moreInfoUrlBuffer,
    const int64_t moreInfoUrlBufferSize,
    int64_t* actualMoreInfoUrlSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_policyengine_islabelingrequired"></a>MIP_CC_PolicyEngine_IsLabelingRequired

Ottiene un valore che indica se i criteri stabiliscono che è necessario etichettare un documento.

**Parameters**

Parametro | Descrizione
|---|---|
| motore | Motore dei criteri |
| isLabelingRequired | Output Indica se i criteri stabiliscono che è necessario etichettare un documento |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_PolicyEngine_IsLabelingRequired(
    const mip_cc_policy_engine engine,
    bool* isLabelingRequired,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_policyengine_getpolicyfileidsize"></a>MIP_CC_PolicyEngine_GetPolicyFileIdSize

Ottiene le dimensioni dei dati client associati a un motore di criteri

**Parameters**

Parametro | Descrizione
|---|---|
| motore | Motore dei criteri |
| policyFileIdSize | Output Dimensioni dei dati client (in numero di caratteri) |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_PolicyEngine_GetPolicyFileIdSize(
    const mip_cc_policy_engine engine,
    int64_t* policyFileIdSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_policyengine_getpolicyfileid"></a>MIP_CC_PolicyEngine_GetPolicyFileId

Ottenere i dati client associati a un motore dei criteri

**Parameters**

Parametro | Descrizione
|---|---|
| motore | Motore dei criteri |
| policyFileIdBuffer | Output Buffer in cui verranno copiati i dati client |
| policyFileIdBufferSize | Dimensioni (in numero di caratteri) di policyFileIdBuffer. |
| actualPolicyFileIdSize | Output Numero di caratteri scritti nel buffer |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

**Nota**: se policyFileIdBuffer è null o insufficiente, verrà restituito MIP_RESULT_ERROR_INSUFFICIENT_BUFFER e actualPolicyFileIdSize verrà impostato sulle dimensioni minime del buffer richiesto. 

```c
mip_cc_result MIP_CC_PolicyEngine_GetPolicyFileId(
    const mip_cc_policy_engine engine,
    char* policyFileIdBuffer,
    const int64_t policyFileIdBufferSize,
    int64_t* actualPolicyFileIdSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_policyengine_getsensitivityfileidsize"></a>MIP_CC_PolicyEngine_GetSensitivityFileIdSize

Ottiene le dimensioni dei dati client associati a un motore di criteri

**Parameters**

Parametro | Descrizione
|---|---|
| motore | Motore dei criteri |
| sensitivityFileIdSize | Output Dimensioni dei dati client (in numero di caratteri) |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_PolicyEngine_GetSensitivityFileIdSize(
    const mip_cc_policy_engine engine,
    int64_t* sensitivityFileIdSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_policyengine_getsensitivityfileid"></a>MIP_CC_PolicyEngine_GetSensitivityFileId

Ottenere i dati client associati a un motore dei criteri

**Parameters**

Parametro | Descrizione
|---|---|
| motore | Motore dei criteri |
| sensitivityFileIdBuffer | Output Buffer in cui verranno copiati i dati client |
| sensitivityFileIdBufferSize | Dimensioni (in numero di caratteri) di sensitivityFileIdBuffer. |
| actualSensitivityFileIdSize | Output Numero di caratteri scritti nel buffer |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

**Nota**: se sensitivityFileIdBuffer è null o insufficiente, verrà restituito MIP_RESULT_ERROR_INSUFFICIENT_BUFFER e actualSensitivityFileIdSize verrà impostato sulle dimensioni minime del buffer richiesto. 

```c
mip_cc_result MIP_CC_PolicyEngine_GetSensitivityFileId(
    const mip_cc_policy_engine engine,
    char* sensitivityFileIdBuffer,
    const int64_t sensitivityFileIdBufferSize,
    int64_t* actualSensitivityFileIdSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_policyengine_hasclassificationrules"></a>MIP_CC_PolicyEngine_HasClassificationRules

Ottiene un valore che indica se il criterio ha regole automatiche o consigliate

**Parameters**

Parametro | Descrizione
|---|---|
| motore | Motore dei criteri |
| hasClassificationRules | Output Indica se i criteri hanno regole automatiche o di raccomandazione |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_PolicyEngine_HasClassificationRules(
    const mip_cc_policy_engine engine,
    bool* hasClassificationRules,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_policyengine_getlastpolicyfetchtime"></a>MIP_CC_PolicyEngine_GetLastPolicyFetchTime

Ottiene l'ora dell'ultimo recupero dei criteri

**Parameters**

Parametro | Descrizione
|---|---|
| motore | Motore dei criteri |
| lastPolicyFetchTime | Output Ora dell'ultimo recupero dei criteri (in secondi da Epoch) |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_PolicyEngine_GetLastPolicyFetchTime(
    const mip_cc_policy_engine engine,
    int64_t* lastPolicyFetchTime,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_policyengine_getsensitivitylabelssize"></a>MIP_CC_PolicyEngine_GetSensitivityLabelsSize

Ottiene il numero di etichette di riservatezza associate al motore dei criteri

**Parameters**

Parametro | Descrizione
|---|---|
| motore | Motore dei criteri |
| labelsSize | Output Numero di etichette |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_PolicyEngine_GetSensitivityLabelsSize(
    const mip_cc_policy_engine engine,
    int64_t* labelsSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_policyengine_getsensitivitylabels"></a>MIP_CC_PolicyEngine_GetSensitivityLabels

Ottiene le etichette di riservatezza associate al motore dei criteri

**Parameters**

Parametro | Descrizione
|---|---|
| motore | Motore dei criteri |
| labelBuffer | Output Buffer in cui verranno copiate le etichette. Le etichette sono di proprietà del client |
| labelBufferSize | Dimensioni (in numero di etichette) di labelBuffer. |
| actualLabelsSize | Output Numero di etichette scritte nel buffer |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

**Nota**: se labelBuffer è null o insufficiente, verrà restituito MIP_RESULT_ERROR_INSUFFICIENT_BUFFER e actualLabelsSize verrà impostato sulle dimensioni minime del buffer richieste 

```c
mip_cc_result MIP_CC_PolicyEngine_GetSensitivityLabels(
    const mip_cc_policy_engine engine,
    mip_cc_label* labelBuffer,
    const int64_t labelBufferSize,
    int64_t* actualLabelsSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_policyengine_getlabelbyid"></a>MIP_CC_PolicyEngine_GetLabelById

Ottiene l'etichetta di riservatezza in base all'ID

**Parameters**

Parametro | Descrizione
|---|---|
| motore | Motore dei criteri |
| labelId | ID etichetta |
| label | Output Etichetta di riservatezza. Questo valore è di proprietà del chiamante e deve essere rilasciato con MIP_CC_ReleaseLabel. |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_PolicyEngine_GetLabelById(
    const mip_cc_policy_engine engine,
    const char* labelId,
    mip_cc_label* label,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_policyengine_getsensitivitytypessize"></a>MIP_CC_PolicyEngine_GetSensitivityTypesSize

Ottiene il numero di tipi di riservatezza associati al motore dei criteri.

**Parameters**

Parametro | Descrizione
|---|---|
| motore | Motore dei criteri |
| sensitivityTypesSize | Output Numero di tipi di riservatezza |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_PolicyEngine_GetSensitivityTypesSize(
    const mip_cc_policy_engine engine,
    int64_t* sensitivityTypesSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_policyengine_getsensitivitytypes"></a>MIP_CC_PolicyEngine_GetSensitivityTypes

Ottiene i tipi di riservatezza associati al motore dei criteri.

**Parameters**

Parametro | Descrizione
|---|---|
| motore | Motore dei criteri |
| sensitivityTypeBuffer | Output Buffer in cui verranno copiati i tipi di riservatezza. Sensibilità |
| sensitivityTypeBufferSize | Dimensioni (in numero di tipi di riservatezza) del sensitivityTypeBuffer. |
| actualSensitivityTypesSize | Output Numero di tipi di riservatezza scritti nel buffer |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

**Nota**: se sensitivityTypeBuffer è null o insufficiente, verrà restituito MIP_RESULT_ERROR_INSUFFICIENT_BUFFER e actualSensitivityTypesSize verrà impostato sulle dimensioni minime del buffer richieste 

```c
mip_cc_result MIP_CC_PolicyEngine_GetSensitivityTypes(
    const mip_cc_policy_engine engine,
    mip_cc_sensitivity_type* sensitivityTypeBuffer,
    const int64_t sensitivityTypeBufferSize,
    int64_t* actualSensitivityTypesSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_policyengine_createpolicyhandler"></a>MIP_CC_PolicyEngine_CreatePolicyHandler

Creazione di un gestore dei criteri per l'esecuzione di funzioni correlate ai criteri

**Parameters**

Parametro | Descrizione
|---|---|
| motore | Motore dei criteri |
| isAuditDiscoveryEnabled | Indica se l'individuazione del controllo è abilitata |
| gestore | Output Istanza del gestore criteri appena creata |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_PolicyEngine_CreatePolicyHandler(
    const mip_cc_policy_engine engine,
    const bool isAuditDiscoveryEnabled,
    mip_cc_policy_handler* handler,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_policyengine_sendapplicationauditevent"></a>MIP_CC_PolicyEngine_SendApplicationAuditEvent

Registra un evento specifico dell'applicazione nella pipeline di controllo

**Parameters**

Parametro | Descrizione
|---|---|
| livello | Livello dell'evento: info/Error/Warning |
| eventType | Descrizione del tipo di evento |
| eventData | Dati associati all'evento. |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_PolicyEngine_SendApplicationAuditEvent(
    const mip_cc_policy_engine engine,
    const char* level,
    const char* eventType,
    const char* eventData,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_policyengine_gettenantidsize"></a>MIP_CC_PolicyEngine_GetTenantIdSize

Ottiene le dimensioni dell'ID tenant

**Parameters**

Parametro | Descrizione
|---|---|
| motore | Motore dei criteri |
| tenantIdSize | Output Dimensioni dell'ID tenant (in numero di caratteri) |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_PolicyEngine_GetTenantIdSize(
    const mip_cc_policy_engine engine,
    int64_t* tenantIdSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_policyengine_gettenantid"></a>MIP_CC_PolicyEngine_GetTenantId

Ottiene l'ID tenant

**Parameters**

Parametro | Descrizione
|---|---|
| motore | Motore dei criteri |
| tenantIdBuffer | Output Buffer in cui verrà copiato l'ID tenant. |
| tenantIdBufferSize | Dimensioni (in numero di caratteri) di tenantIdBuffer. |
| actualTenantIdSize | Output Numero di caratteri scritti nel buffer |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

**Nota**: se tenantIdBuffer è null o insufficiente, verrà restituito MIP_RESULT_ERROR_INSUFFICIENT_BUFFER e actualTenantIdSize verrà impostato sulle dimensioni minime del buffer richiesto. 

```c
mip_cc_result MIP_CC_PolicyEngine_GetTenantId(
    const mip_cc_policy_engine engine,
    char* tenantIdBuffer,
    const int64_t tenantIdBufferSize,
    int64_t* actualTenantIdSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_policyengine_getpolicydataxmlsize"></a>MIP_CC_PolicyEngine_GetPolicyDataXmlSize

Ottiene le dimensioni del codice XML dei dati dei criteri

**Parameters**

Parametro | Descrizione
|---|---|
| motore | Motore dei criteri |
| XmlSize | Output Dimensioni del codice XML dei dati dei criteri (in numero di caratteri) |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_PolicyEngine_GetPolicyDataXmlSize(
    const mip_cc_policy_engine engine,
    int64_t* xmlSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_policyengine_getpolicydataxml"></a>MIP_CC_PolicyEngine_GetPolicyDataXml

Ottiene il codice XML dei dati dei criteri

**Parameters**

Parametro | Descrizione
|---|---|
| motore | Motore dei criteri |
| XmlBuffer | Output Buffer in cui verrà copiato il codice XML. |
| xmlBufferSize | Dimensioni (in numero di caratteri) di XmlBuffer. |
| actualXmlSize | Output Numero di caratteri scritti nel buffer |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

**Nota**: se XmlBuffer è null o insufficiente, verrà restituito MIP_RESULT_ERROR_INSUFFICIENT_BUFFER e actualXmlSize verrà impostato sulle dimensioni minime del buffer richiesto. 

```c
mip_cc_result MIP_CC_PolicyEngine_GetPolicyDataXml(
    const mip_cc_policy_engine engine,
    char* xmlBuffer,
    const int64_t xmlBufferSize,
    int64_t* actualXmlSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_policyengine_getsensitivitytypesdataxmlsize"></a>MIP_CC_PolicyEngine_GetSensitivityTypesDataXmlSize

Ottiene le dimensioni dei dati XML dei tipi di riservatezza

**Parameters**

Parametro | Descrizione
|---|---|
| motore | Motore dei criteri |
| XmlSize | Output Dimensioni del codice XML dei dati dei criteri (in numero di caratteri) |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_PolicyEngine_GetSensitivityTypesDataXmlSize(
    const mip_cc_policy_engine engine,
    int64_t* xmlSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_policyengine_getsensitivitytypesdataxml"></a>MIP_CC_PolicyEngine_GetSensitivityTypesDataXml

Ottiene il codice XML di dati dei tipi di riservatezza

**Parameters**

Parametro | Descrizione
|---|---|
| motore | Motore dei criteri |
| XmlBuffer | Output Buffer in cui verrà copiato il codice XML. |
| xmlBufferSize | Dimensioni (in numero di caratteri) di XmlBuffer. |
| actualXmlSize | Output Numero di caratteri scritti nel buffer |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

**Nota**: se XmlBuffer è null o insufficiente, verrà restituito MIP_RESULT_ERROR_INSUFFICIENT_BUFFER e actualXmlSize verrà impostato sulle dimensioni minime del buffer richiesto. 

```c
mip_cc_result MIP_CC_PolicyEngine_GetSensitivityTypesDataXml(
    const mip_cc_policy_engine engine,
    char* xmlBuffer,
    const int64_t xmlBufferSize,
    int64_t* actualXmlSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_policyengine_getclientdatasize"></a>MIP_CC_PolicyEngine_GetClientDataSize

Ottiene le dimensioni dei dati client associati a un motore di criteri

**Parameters**

Parametro | Descrizione
|---|---|
| motore | Motore dei criteri |
| clientDataSize | Output Dimensioni dei dati client (in numero di caratteri) |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_PolicyEngine_GetClientDataSize(
    const mip_cc_policy_engine engine,
    int64_t* clientDataSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_policyengine_getclientdata"></a>MIP_CC_PolicyEngine_GetClientData

Ottenere i dati client associati a un motore dei criteri

**Parameters**

Parametro | Descrizione
|---|---|
| motore | Motore dei criteri |
| clientDataBuffer | Output Buffer in cui verranno copiati i dati client |
| clientDataBufferSize | Dimensioni (in numero di caratteri) di clientDataBuffer. |
| actualClientDataSize | Output Numero di caratteri scritti nel buffer |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

**Nota**: se clientDataBuffer è null o insufficiente, verrà restituito MIP_RESULT_ERROR_INSUFFICIENT_BUFFER e actualClientDataSize verrà impostato sulle dimensioni minime del buffer richiesto. 

```c
mip_cc_result MIP_CC_PolicyEngine_GetClientData(
    const mip_cc_policy_engine engine,
    char* clientDataBuffer,
    const int64_t clientDataBufferSize,
    int64_t* actualClientDataSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_createpolicyenginesettingswithidentity"></a>MIP_CC_CreatePolicyEngineSettingsWithIdentity

Creare un oggetto impostazioni usato per creare un nuovo motore dei criteri

**Parameters**

Parametro | Descrizione
|---|---|
| identity | Identità che verrà associata a PolicyEngine |
| clientData | Dati client personalizzabili archiviati insieme al motore |
| locale | Impostazioni locali in cui vengono restituiti i risultati del testo |
| loadSensitivityTypes | Se è necessario caricare anche i dati dei tipi di riservatezza (per la classificazione) |
| impostazioni | Output Istanza di impostazioni appena creata |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

**Nota**:' loadSensitivityTypes ' deve essere ' true ' solo se l'applicazione prevede una chiamata successiva MIP_CC_PolicyEngine_GetSensitivityTypes. In caso contrario, deve essere false per evitare un'operazione HTTP non necessaria. 

```c
mip_cc_result MIP_CC_CreatePolicyEngineSettingsWithIdentity(
    const mip_cc_identity* identity,
    const char* clientData,
    const char* locale,
    bool loadSensitivityTypes,
    mip_cc_policy_engine_settings* settings,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_policyenginesettings_setclientdata"></a>MIP_CC_PolicyEngineSettings_SetClientData

Imposta i dati client che verranno archiviati in maniera opaca insieme a questo motore e mantengono tra le sessioni

**Parameters**

Parametro | Descrizione
|---|---|
| impostazioni | Impostazioni motore |
| clientData | Dati client |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_PolicyEngineSettings_SetClientData(
    const mip_cc_policy_engine_settings settings,
    const char* clientData,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_policyenginesettings_setcustomsettings"></a>MIP_CC_PolicyEngineSettings_SetCustomSettings

Configura le impostazioni personalizzate, usate per il controllo e il controllo delle funzionalità.

**Parameters**

Parametro | Descrizione
|---|---|
| impostazioni | Impostazioni motore |
| customSettings | Coppie chiave/valore di impostazioni personalizzate |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_PolicyEngineSettings_SetCustomSettings(
    const mip_cc_policy_engine_settings settings,
    const mip_cc_dictionary customSettings,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_policyenginesettings_setsessionid"></a>MIP_CC_PolicyEngineSettings_SetSessionId

Imposta l'ID di sessione che può essere usato per correlare i log e i dati di telemetria

**Parameters**

Parametro | Descrizione
|---|---|
| impostazioni | Impostazioni motore |
| sessionID | ID di sessione che rappresenta la durata di un motore dei criteri |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_PolicyEngineSettings_SetSessionId(
    const mip_cc_policy_engine_settings settings,
    const char* sessionId,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_policyenginesettings_setcloud"></a>MIP_CC_PolicyEngineSettings_SetCloud

Imposta il cloud che influiscono sugli URL dell'endpoint per tutte le richieste di servizio

**Parameters**

Parametro | Descrizione
|---|---|
| impostazioni | Impostazioni motore |
| cloud | Identificatore cloud (impostazione predefinita = sconosciuta) |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

**Nota**: se il cloud non è specificato, l'impostazione predefinita sarà cloud globale. 

```c
mip_cc_result MIP_CC_PolicyEngineSettings_SetCloud(
    const mip_cc_policy_engine_settings settings,
    const mip_cc_cloud cloud,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_policyenginesettings_setcloudendpointbaseurl"></a>MIP_CC_PolicyEngineSettings_SetCloudEndpointBaseUrl

Imposta l'URL di base per tutte le richieste di servizio

**Parameters**

Parametro | Descrizione
|---|---|
| impostazioni | Impostazioni motore |
| cloudEndpointBaseUrl | URL di base (ad esempio ' https://dataservice.protection.outlook.com ') |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

**Nota**: questo valore verrà letto e deve essere impostato solo per Cloud = MIP_CLOUD_CUSTOM 

```c
mip_cc_result MIP_CC_PolicyEngineSettings_SetCloudEndpointBaseUrl(
    const mip_cc_policy_engine_settings settings,
    const char* cloudEndpointBaseUrl,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_policyenginesettings_setdelegateduseremail"></a>MIP_CC_PolicyEngineSettings_SetDelegatedUserEmail

Imposta l'utente delegato

**Parameters**

Parametro | Descrizione
|---|---|
| impostazioni | Impostazioni motore |
| delegatedUserEmail | Indirizzo di posta elettronica dell'utente delegato |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

**Nota**: un utente delegato viene specificato quando l'utente o l'applicazione di autenticazione agisce per conto di un altro utente 

```c
mip_cc_result MIP_CC_PolicyEngineSettings_SetDelegatedUserEmail(
    const mip_cc_policy_engine_settings settings,
    const char* delegatedUserEmail,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_policyenginesettings_setlabelfilter"></a>MIP_CC_PolicyEngineSettings_SetLabelFilter

Imposta il filtro etichette

**Parameters**

Parametro | Descrizione
|---|---|
| impostazioni | Impostazioni motore |
| labelFilter | enum che rappresenta il filtro etichette, se non è impostato il valore predefinito è Hyok, doublekeyencryption |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_PolicyEngineSettings_SetLabelFilter(
    const mip_cc_policy_engine_settings settings,
    const mip_cc_label_filter labelFilter,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_releasepolicyenginesettings"></a>MIP_CC_ReleasePolicyEngineSettings

Rilasciare le risorse associate a impostazioni del motore dei criteri

**Parameters**

Parametro | Descrizione
|---|---|
| impostazioni | Impostazioni del motore dei criteri da rilasciare |

```c
void MIP_CC_ReleasePolicyEngineSettings(mip_cc_policy_engine_settings settings);
```

## <a name="mip_cc_releasepolicyhandler"></a>MIP_CC_ReleasePolicyHandler

Rilasciare le risorse associate a un gestore dei criteri

**Parameters**

Parametro | Descrizione
|---|---|
| gestore | Gestore dei criteri da rilasciare |

```c
void MIP_CC_ReleasePolicyHandler(mip_cc_policy_handler handler);
```

## <a name="mip_cc_policyhandler_getsensitivitylabel"></a>MIP_CC_PolicyHandler_GetSensitivityLabel

Ottiene l'etichetta corrente di un documento

**Parameters**

Parametro | Descrizione
|---|---|
| gestore | Gestore criteri |
| documentState | Stato del documento |
| contesto | Il contesto dell'applicazione viene trasmesso in modo opaco a qualsiasi callback |
| contentLabel | Etichetta attualmente applicata a un documento |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_PolicyHandler_GetSensitivityLabel(
    const mip_cc_policy_handler handler,
    const mip_cc_document_state* documentState,
    const void* context,
    mip_cc_content_label* contentLabel,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_policyhandler_computeactions"></a>MIP_CC_PolicyHandler_ComputeActions

Esegue le regole dei criteri in base allo stato fornito e determina le azioni corrispondenti

**Parameters**

Parametro | Descrizione
|---|---|
| gestore | Gestore criteri |
| documentState | Stato del documento |
| applicationState | Stato azione applicazione |
| contesto | Il contesto dell'applicazione viene trasmesso in modo opaco a qualsiasi callback |
| actionResult | Output Azioni che devono essere eseguite dall'applicazione, memoria di proprietà del chiamante |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

**Nota**: la variabile ' ActionResult ' deve essere rilasciata dal chiamante chiamando MIP_CC_ReleaseActionResult 

```c
mip_cc_result MIP_CC_PolicyHandler_ComputeActions(
    const mip_cc_policy_handler handler,
    const mip_cc_document_state* documentState,
    const mip_cc_application_action_state* applicationState,
    const void* context,
    mip_cc_action_result* actionResult,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_policyhandler_notifycommittedactions"></a>MIP_CC_PolicyHandler_NotifyCommittedActions

Chiamata eseguita dall'applicazione dopo l'applicazione delle azioni calcolate e i dati di cui è stato eseguito il commit su disco

**Parameters**

Parametro | Descrizione
|---|---|
| gestore | Gestore criteri |
| documentState | Stato del documento |
| applicationState | Stato azione applicazione |
| contesto | Il contesto dell'applicazione viene trasmesso in modo opaco a qualsiasi callback |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

**Nota**: una chiamata a questa funzione è necessaria per trasmettere i dati di controllo dell'etichetta completi. 

```c
mip_cc_result MIP_CC_PolicyHandler_NotifyCommittedActions(
    const mip_cc_policy_handler handler,
    const mip_cc_document_state* documentState,
    const mip_cc_application_action_state* applicationState,
    const void* context,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_policyprofile_acquireauthtoken"></a>MIP_CC_PolicyProfile_AcquireAuthToken

Attivare un callback di autenticazione

**Parameters**

Parametro | Descrizione
|---|---|
| profile | Profilo |
| cloud | Cloud di Azure |
| authCallback | Callback di autenticazione che verrà richiamato |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

**Nota**: MIP non memorizza nella cache o non esegue altre operazioni con il valore restituito dal delegato di autenticazione. Questa funzione è consigliata per le applicazioni che non sono "connesse" fino a quando MIP richiede un token di autenticazione. Consente a un'applicazione di recuperare un token prima che MIP ne richieda effettivamente uno. 

```c
mip_cc_result MIP_CC_PolicyProfile_AcquireAuthToken(
    const mip_cc_policy_profile profile,
    const mip_cc_cloud cloud,
    const mip_cc_auth_callback authCallback,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_loadpolicyprofile"></a>MIP_CC_LoadPolicyProfile

Carica un profilo

**Parameters**

Parametro | Descrizione
|---|---|
| impostazioni | Impostazioni del profilo |
| profile | Output Istanza del profilo criteri appena creata |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_LoadPolicyProfile(
    const mip_cc_policy_profile_settings settings,
    mip_cc_policy_profile* profile,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_releasepolicyprofile"></a>MIP_CC_ReleasePolicyProfile

Rilasciare le risorse associate a un profilo criteri

**Parameters**

Parametro | Descrizione
|---|---|
| profile | Profilo criteri da rilasciare |

```c
void MIP_CC_ReleasePolicyProfile(mip_cc_policy_profile profile);
```

## <a name="mip_cc_createpolicyprofilesettings"></a>MIP_CC_CreatePolicyProfileSettings

Creare un oggetto impostazioni usato per creare un profilo criteri

**Parameters**

Parametro | Descrizione
|---|---|
| mipContext | Contesto globale condiviso tra tutti i profili |
| cacheStorageType | Configurazione della cache di archiviazione |
| authCallback | Oggetto callback da usare per l'autenticazione, implementato dall'applicazione client |
| impostazioni | Output Istanza di impostazioni appena creata |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_CreatePolicyProfileSettings(
    const mip_cc_mip_context mipContext,
    const mip_cc_cache_storage_type cacheStorageType,
    const mip_cc_auth_callback authCallback,
    mip_cc_policy_profile_settings* settings,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_policyprofilesettings_setsessionid"></a>MIP_CC_PolicyProfileSettings_SetSessionId

Imposta l'ID di sessione che può essere usato per correlare i log e i dati di telemetria

**Parameters**

Parametro | Descrizione
|---|---|
| impostazioni | Impostazioni del profilo |
| sessionID | ID di sessione che rappresenta la durata di un profilo di criteri |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_PolicyProfileSettings_SetSessionId(
    const mip_cc_policy_profile_settings settings,
    const char* sessionId,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_policyprofilesettings_sethttpdelegate"></a>MIP_CC_PolicyProfileSettings_SetHttpDelegate

Esegui override dello stack HTTP predefinito con il proprio client

**Parameters**

Parametro | Descrizione
|---|---|
| impostazioni | Impostazioni del profilo a cui verrà assegnato il delegato HTTP |
| httpDelegate | Istanza di callback HTTP implementata dall'applicazione client |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_PolicyProfileSettings_SetHttpDelegate(
    const mip_cc_policy_profile_settings settings,
    const mip_cc_http_delegate httpDelegate,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_policyprofilesettings_settaskdispatcherdelegate"></a>MIP_CC_PolicyProfileSettings_SetTaskDispatcherDelegate

Esegui override del dispatcher attività asincrono predefinito con il proprio client

**Parameters**

Parametro | Descrizione
|---|---|
| impostazioni | Impostazioni del profilo a cui verrà assegnato il delegato del dispatcher attività |
| taskDispatcherDelegate | Istanza di callback Dispatcher attività implementata dall'applicazione client |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_PolicyProfileSettings_SetTaskDispatcherDelegate(
    const mip_cc_policy_profile_settings settings,
    const mip_cc_task_dispatcher_delegate taskDispatcherDelegate,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_policyprofilesettings_setcustomsettings"></a>MIP_CC_PolicyProfileSettings_SetCustomSettings

Configura le impostazioni personalizzate, usate per il controllo e il controllo delle funzionalità.

**Parameters**

Parametro | Descrizione
|---|---|
| impostazioni | Impostazioni del profilo |
| customSettings | Coppie chiave/valore di impostazioni personalizzate |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_PolicyProfileSettings_SetCustomSettings(
    const mip_cc_policy_profile_settings settings,
    const mip_cc_dictionary customSettings,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_releasepolicyprofilesettings"></a>MIP_CC_ReleasePolicyProfileSettings

Rilasciare le risorse associate a impostazioni del profilo criteri

**Parameters**

Parametro | Descrizione
|---|---|
| impostazioni | Impostazioni del profilo dei criteri da rilasciare |

```c
void MIP_CC_ReleasePolicyProfileSettings(mip_cc_policy_profile_settings profileSettings);
```

## <a name="mip_cc_protectadhocdkaction_getdoublekeyencryptionurlsize"></a>MIP_CC_ProtectAdhocDkAction_GetDoubleKeyEncryptionUrlSize

Ottiene le dimensioni del buffer necessarie per archiviare l'URL di crittografia a chiave doppia.

**Parameters**

Parametro | Descrizione
|---|---|
| action | azione "Proteggi per criteri ad hoc con doppia chiave" |
| urlSize | Output Dimensione del buffer in cui memorizzare l'URL (in numero di caratteri) |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_ProtectAdhocDkAction_GetDoubleKeyEncryptionUrlSize(
    const mip_cc_action action,
    int64_t* urlSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectadhocdkaction_getdoublekeyencryptionurl"></a>MIP_CC_ProtectAdhocDkAction_GetDoubleKeyEncryptionUrl

Ottiene l'URL di crittografia a chiave doppia

**Parameters**

Parametro | Descrizione
|---|---|
| action | azione "Proteggi per criteri ad hoc con doppia chiave" |
| urlBuffer | Output Buffer in cui verrà copiato l'URL. |
| urlBufferSize | Dimensioni (in numero di caratteri) di urlBuffer. |
| actualUrlSize | Output Numero di caratteri scritti nel buffer |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

**Nota**: se urlBuffer è null o insufficiente, verrà restituito MIP_RESULT_ERROR_INSUFFICIENT_BUFFER e actualUrlSize verrà impostato sulle dimensioni minime del buffer richiesto. 

```c
mip_cc_result MIP_CC_ProtectAdhocDkAction_GetDoubleKeyEncryptionUrl(
    const mip_cc_action action,
    char* urlBuffer,
    const int64_t urlBufferSize,
    int64_t* actualUrlSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectbytemplateaction_gettemplateid"></a>MIP_CC_ProtectByTemplateAction_GetTemplateId

Ottiene l'ID modello dell'azione "Proteggi per modello"

**Parameters**

Parametro | Descrizione
|---|---|
| action | azione "Proteggi per modello" |
| templateId | Output ID del modello che definisce le protezioni |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_ProtectByTemplateAction_GetTemplateId(
    const mip_cc_action action,
    mip_cc_guid* templateId,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectbytemplatedkaction_gettemplateid"></a>MIP_CC_ProtectByTemplateDkAction_GetTemplateId

Ottiene un ID modello dell'azione "Proteggi per modello con chiave doppia"

**Parameters**

Parametro | Descrizione
|---|---|
| action | azione "Proteggi per modello" |
| templateId | Output ID del modello che definisce le protezioni |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_ProtectByTemplateDkAction_GetTemplateId(
    const mip_cc_action action,
    mip_cc_guid* templateId,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectbytemplatedkaction_getdoublekeyencryptionurlsize"></a>MIP_CC_ProtectByTemplateDkAction_GetDoubleKeyEncryptionUrlSize

Ottiene le dimensioni del buffer necessarie per archiviare l'URL di crittografia a chiave doppia.

**Parameters**

Parametro | Descrizione
|---|---|
| action | azione "Proteggi per modello con doppia chiave" |
| urlSize | Output Dimensione del buffer in cui memorizzare l'URL (in numero di caratteri) |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_ProtectByTemplateDkAction_GetDoubleKeyEncryptionUrlSize(
    const mip_cc_action action,
    int64_t* urlSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectbytemplatedkaction_getdoublekeyencryptionurl"></a>MIP_CC_ProtectByTemplateDkAction_GetDoubleKeyEncryptionUrl

Ottiene l'URL di crittografia a chiave doppia

**Parameters**

Parametro | Descrizione
|---|---|
| action | azione "Proteggi per modello con doppia chiave" |
| urlBuffer | Output Buffer in cui verrà copiato l'URL. |
| urlBufferSize | Dimensioni (in numero di caratteri) di urlBuffer. |
| actualUrlSize | Output Numero di caratteri scritti nel buffer |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

**Nota**: se urlBuffer è null o insufficiente, verrà restituito MIP_RESULT_ERROR_INSUFFICIENT_BUFFER e actualUrlSize verrà impostato sulle dimensioni minime del buffer richiesto. 

```c
mip_cc_result MIP_CC_ProtectByTemplateDkAction_GetDoubleKeyEncryptionUrl(
    const mip_cc_action action,
    char* urlBuffer,
    const int64_t urlBufferSize,
    int64_t* actualUrlSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectdonotforwarddkaction_getdoublekeyencryptionurlsize"></a>MIP_CC_ProtectDoNotForwardDkAction_GetDoubleKeyEncryptionUrlSize

Ottiene le dimensioni del buffer necessarie per archiviare l'URL di crittografia a chiave doppia.

**Parameters**

Parametro | Descrizione
|---|---|
| action | azione "Proteggi da DP senza inoltri con chiave doppia" |
| urlSize | Output Dimensione del buffer in cui memorizzare l'URL (in numero di caratteri) |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_ProtectDoNotForwardDkAction_GetDoubleKeyEncryptionUrlSize(
    const mip_cc_action action,
    int64_t* urlSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectdonotforwarddkaction_getdoublekeyencryptionurl"></a>MIP_CC_ProtectDoNotForwardDkAction_GetDoubleKeyEncryptionUrl

Ottiene l'URL di crittografia a chiave doppia

**Parameters**

Parametro | Descrizione
|---|---|
| action | azione "Proteggi da DP senza inoltri con chiave doppia" |
| urlBuffer | Output Buffer in cui verrà copiato l'URL. |
| urlBufferSize | Dimensioni (in numero di caratteri) di urlBuffer. |
| actualUrlSize | Output Numero di caratteri scritti nel buffer |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

**Nota**: se urlBuffer è null o insufficiente, verrà restituito MIP_RESULT_ERROR_INSUFFICIENT_BUFFER e actualUrlSize verrà impostato sulle dimensioni minime del buffer richiesto. 

```c
mip_cc_result MIP_CC_ProtectDoNotForwardDkAction_GetDoubleKeyEncryptionUrl(
    const mip_cc_action action,
    char* urlBuffer,
    const int64_t urlBufferSize,
    int64_t* actualUrlSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_removecontentfooteraction_getuielementnames"></a>MIP_CC_RemoveContentFooterAction_GetUIElementNames

Ottiene i nomi degli elementi dell'interfaccia utente dell'azione "Rimuovi piè di pagina contenuto" da rimuovere

**Parameters**

Parametro | Descrizione
|---|---|
| action | azione "Rimuovi piè di pagina contenuto" |
| nomi | Output Nomi degli elementi dell'interfaccia utente da rimuovere, memoria di proprietà del chiamante |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

**Nota**: la variabile ' names ' deve essere rilasciata dal chiamante chiamando MIP_CC_ReleaseStringList 

```c
mip_cc_result MIP_CC_RemoveContentFooterAction_GetUIElementNames(
    const mip_cc_action action,
    mip_cc_string_list* names,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_removecontentheaderaction_getuielementnames"></a>MIP_CC_RemoveContentHeaderAction_GetUIElementNames

Ottiene i nomi degli elementi dell'interfaccia utente dell'azione "Rimuovi intestazione contenuto" da rimuovere

**Parameters**

Parametro | Descrizione
|---|---|
| action | azione "Rimuovi intestazione contenuto" |
| nomi | Output Nomi degli elementi dell'interfaccia utente da rimuovere, memoria di proprietà del chiamante |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

**Nota**: la variabile ' names ' deve essere rilasciata dal chiamante chiamando MIP_CC_ReleaseStringList 

```c
mip_cc_result MIP_CC_RemoveContentHeaderAction_GetUIElementNames(
    const mip_cc_action action,
    mip_cc_string_list* names,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_removewatermarkaction_getuielementnames"></a>MIP_CC_RemoveWatermarkAction_GetUIElementNames

Ottiene i nomi degli elementi dell'interfaccia utente dell'azione "Rimuovi filigrana" da rimuovere

**Parameters**

Parametro | Descrizione
|---|---|
| action | azione "Rimuovi piè di pagina filigrana" |
| nomi | Output Nomi degli elementi dell'interfaccia utente da rimuovere, memoria di proprietà del chiamante |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

**Nota**: la variabile ' names ' deve essere rilasciata dal chiamante chiamando MIP_CC_ReleaseStringList 

```c
mip_cc_result MIP_CC_RemoveWatermarkAction_GetUIElementNames(
    const mip_cc_action action,
    mip_cc_string_list* names,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_releasesensitivitytype"></a>MIP_CC_ReleaseSensitivityType

Rilasciare le risorse associate a un tipo di riservatezza

**Parameters**

Parametro | Descrizione
|---|---|
| sensitivityType | Tipo di riservatezza da rilasciare |

```c
void MIP_CC_ReleaseSensitivityType(mip_cc_sensitivity_type sensitivityType);
```

## <a name="mip_cc_sensitivitytype_getrulepackageidsize"></a>MIP_CC_SensitivityType_GetRulePackageIdSize

Ottiene le dimensioni del buffer necessarie per archiviare l'ID del pacchetto di regole del tipo di riservatezza

**Parameters**

Parametro | Descrizione
|---|---|
| sensitivityType | Tipo di riservatezza |
| idSize | Output Dimensioni del buffer per l'ID del pacchetto della regola (in numero di caratteri) |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_SensitivityType_GetRulePackageIdSize(
    const mip_cc_sensitivity_type sensitivityType,
    int64_t* idSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_sensitivitytype_getrulepackageid"></a>MIP_CC_SensitivityType_GetRulePackageId

Ottiene l'ID del pacchetto di regole del tipo di riservatezza

**Parameters**

Parametro | Descrizione
|---|---|
| sensitivityType | Tipo di riservatezza |
| idBuffer | Output Buffer in cui verrà copiato l'ID. |
| idBufferSize | Dimensioni (in numero di caratteri) di idBuffer. |
| actualIdSize | Output Numero di caratteri scritti nel buffer |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

**Nota**: se idBuffer è null o insufficiente, verrà restituito MIP_RESULT_ERROR_INSUFFICIENT_BUFFER e actualIdSize verrà impostato sulle dimensioni minime del buffer richiesto. 

```c
mip_cc_result MIP_CC_SensitivityType_GetRulePackageId(
    const mip_cc_sensitivity_type sensitivityType,
    char* idBuffer,
    const int64_t idBufferSize,
    int64_t* actualIdSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_sensitivitytype_getrulepackagesize"></a>MIP_CC_SensitivityType_GetRulePackageSize

Ottiene le dimensioni del buffer necessarie per archiviare il pacchetto di regole di un tipo di riservatezza

**Parameters**

Parametro | Descrizione
|---|---|
| sensitivityType | Tipo di riservatezza |
| rulePackageSize | Output Dimensioni del buffer per il mantenimento del pacchetto di regole (in numero di caratteri) |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_SensitivityType_GetRulePackageSize(
    const mip_cc_sensitivity_type sensitivityType,
    int64_t* rulePackageSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_sensitivitytype_getrulepackage"></a>MIP_CC_SensitivityType_GetRulePackage

Ottiene il pacchetto di regole del tipo di riservatezza

**Parameters**

Parametro | Descrizione
|---|---|
| sensitivityType | Tipo di riservatezza |
| rulePackageBuffer | Output Buffer in cui verrà copiato il pacchetto di regole. |
| rulePackageBufferSize | Dimensioni (in numero di caratteri) di rulePackageBuffer. |
| actualRulePackageSize | Output Numero di caratteri scritti nel buffer |
| errorInfo | Output Opzionale Informazioni sull'errore se il risultato dell'operazione è errore |

**Return**: codice risultato che indica l'esito positivo o negativo

**Nota**: se rulePackageBuffer è null o insufficiente, verrà restituito MIP_RESULT_ERROR_INSUFFICIENT_BUFFER e actualRulePackageSize verrà impostato sulle dimensioni minime del buffer richiesto. 

```c
mip_cc_result MIP_CC_SensitivityType_GetRulePackage(
    const mip_cc_sensitivity_type sensitivityType,
    char* rulePackageBuffer,
    const int64_t rulePackageBufferSize,
    int64_t* actualRulePackageSize,
    mip_cc_error* errorInfo);
```

