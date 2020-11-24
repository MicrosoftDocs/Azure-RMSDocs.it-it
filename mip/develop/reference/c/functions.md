---
title: Funzioni
description: Funzioni.
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 9/22/2020
ms.openlocfilehash: 8cb8d6550ecdc0d7ea342c3e6484a7a23b7f590d
ms.sourcegitcommit: 3f5f9f7695b9ed3c45e9230cd8b8cb39a1c5a5ed
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/23/2020
ms.locfileid: "95567368"
---
# <a name="functions"></a>Funzioni

## <a name="mip_cc_auth_callback"></a>mip_cc_auth_callback

definizione della funzione di callback per l'acquisizione del token OAuth2

**Parametri**

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

**Parametri**

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

**Parametri**

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

**Parametri**

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

**Parametri**

Parametro | Descrizione
|---|---|
| dictionary | Dizionario da rilasciare |

```c
void MIP_CC_ReleaseDictionary(mip_cc_dictionary dictionary);
```

## <a name="mip_cc_http_send_callback_fn"></a>mip_cc_http_send_callback_fn

Definizione della funzione di callback per l'emissione di una richiesta HTTP

**Parametri**

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

**Parametri**

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

**Parametri**

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

**Parametri**

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

**Parametri**

Parametro | Descrizione
|---|---|
| httpDelegate | Delegato HTTP da rilasciare |

```c
void MIP_CC_ReleaseHttpDelegate(mip_cc_http_delegate httpDelegate);
```

## <a name="mip_cc_logger_init_callback_fn"></a>mip_cc_logger_init_callback_fn

Definizione della funzione di callback per l'inizializzazione del logger

**Parametri**

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

**Parametri**

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

**Parametri**

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

**Parametri**

Parametro | Descrizione
|---|---|
| loggerDelegate | Delegato del logger da rilasciare |

```c
void MIP_CC_ReleaseLoggerDelegate(mip_cc_logger_delegate loggerDelegate);
```

## <a name="mip_cc_createmipcontext"></a>MIP_CC_CreateMipContext

Creare un contesto MIP per gestire lo stato condiviso tra tutte le istanze del profilo

**Parametri**

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

**Parametri**

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

**Parametri**

Parametro | Descrizione
|---|---|
| mipContext | Contesto MIP da rilasciare |

```c
void MIP_CC_ReleaseMipContext(mip_cc_mip_context mipContext);
```

## <a name="mip_cc_protectiondescriptor_getprotectiontype"></a>MIP_CC_ProtectionDescriptor_GetProtectionType

Ottiene il tipo di protezione, indipendentemente dal fatto che sia definito da un modello RMS

**Parametri**

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

**Parametri**

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

**Parametri**

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

**Parametri**

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

**Parametri**

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

**Parametri**

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

**Parametri**

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

**Parametri**

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

**Parametri**

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

**Parametri**

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

**Parametri**

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

**Parametri**

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

**Parametri**

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

**Parametri**

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

**Parametri**

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

**Parametri**

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

**Parametri**

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

**Parametri**

Parametro | Descrizione
|---|---|
| protectionDescriptor | Descrittore di protezione da rilasciare |

```c
void MIP_CC_ReleaseProtectionDescriptor(mip_cc_protection_descriptor protectionDescriptor);
```

## <a name="mip_cc_createstringlist"></a>MIP_CC_CreateStringList

Creare un elenco di stringhe

**Parametri**

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

**Parametri**

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

**Parametri**

Parametro | Descrizione
|---|---|
| stringList | Elenco di stringhe da rilasciare |

```c
void MIP_CC_ReleaseStringList(mip_cc_string_list stringList);
```

## <a name="mip_cc_dispatch_task_callback_fn"></a>mip_cc_dispatch_task_callback_fn

Definizione della funzione di callback per l'invio di un'attività asincrona

**Parametri**

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

**Parametri**

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

**Parametri**

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

**Parametri**

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

**Parametri**

Parametro | Descrizione
|---|---|
| taskDispatcher | Delegato Dispatcher attività da rilasciare |

```c
void MIP_CC_ReleaseTaskDispatcherDelegate(mip_cc_task_dispatcher_delegate taskDispatcher);
```

## <a name="mip_cc_createtelemetryconfiguration"></a>MIP_CC_CreateTelemetryConfiguration

Creare un oggetto impostazioni utilizzato per creare un profilo di protezione

**Parametri**

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

**Parametri**

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

**Parametri**

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

**Parametri**

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

**Parametri**

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

**Parametri**

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

**Parametri**

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

**Parametri**

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

**Parametri**

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

**Parametri**

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

**Parametri**

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

**Parametri**

Parametro | Descrizione
|---|---|
| profileSettings | Impostazioni del profilo di protezione da rilasciare |

```c
void MIP_CC_ReleaseTelemetryConfiguration(mip_cc_telemetry_configuration telemetryConfig);
```

## <a name="mip_cc_templatedescriptor_getid"></a>MIP_CC_TemplateDescriptor_GetId

Ottiene l'ID modello

**Parametri**

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

**Parametri**

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

**Parametri**

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

**Parametri**

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

**Parametri**

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

**Parametri**

Parametro | Descrizione
|---|---|
| templateDescriptor | Descrittore del modello da rilasciare |

```c
void MIP_CC_ReleaseTemplateDescriptor(mip_cc_template_descriptor templateDescriptor);
```

## <a name="mip_cc_actionresult_getactions"></a>MIP_CC_ActionResult_GetActions

Ottenere azioni che compongono il risultato di un'azione

**Parametri**

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

**Parametri**

Parametro | Descrizione
|---|---|
| actionResult | Risultato dell'azione da rilasciare |

```c
void MIP_CC_ReleaseActionResult(mip_cc_action_result actionResult);
```

## <a name="mip_cc_addcontentfooteraction_getuielementnamesize"></a>MIP_CC_AddContentFooterAction_GetUIElementNameSize

Ottiene le dimensioni del buffer necessarie per archiviare il nome dell'elemento dell'interfaccia utente dell'azione "Aggiungi piè di pagina contenuto"

**Parametri**

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

**Parametri**

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

**Parametri**

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

**Parametri**

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

**Parametri**

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

**Parametri**

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

**Parametri**

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

**Parametri**

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

**Parametri**

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

**Parametri**

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

**Parametri**

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

**Parametri**

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

**Parametri**

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

**Parametri**

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

**Parametri**

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

**Parametri**

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

**Parametri**

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

**Parametri**

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

**Parametri**

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

**Parametri**

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

**Parametri**

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

**Parametri**

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

**Parametri**

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

**Parametri**

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

**Parametri**

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

**Parametri**

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

**Parametri**

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

**Parametri**

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

**Parametri**

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

**Parametri**

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

**Parametri**

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

**Parametri**

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

**Parametri**

Parametro | Descrizione
|---|---|
| contentLabel | Etichetta da rilasciare |

```c
void MIP_CC_ReleaseContentLabel(mip_cc_content_label contentLabel);
```

## <a name="mip_cc_contentlabel_getcreationtime"></a>MIP_CC_ContentLabel_GetCreationTime

Ottiene l'ora in cui è stata applicata l'etichetta

**Parametri**

Parametro | Descrizione
|---|---|
| contentLabel | Label |
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

**Parametri**

Parametro | Descrizione
|---|---|
| contentLabel | Label |
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

**Parametri**

Parametro | Descrizione
|---|---|
| contentLabel | Label |
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

**Parametri**

Parametro | Descrizione
|---|---|
| contentLabel | Label |
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

**Parametri**

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

**Parametri**

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

**Parametri**

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

**Parametri**

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

## <a name="mip_cc_releaselabel"></a>MIP_CC_ReleaseLabel

Rilasciare le risorse associate a un'etichetta

**Parametri**

Parametro | Descrizione
|---|---|
| label | Etichetta da rilasciare |

```c
void MIP_CC_ReleaseLabel(mip_cc_label label);
```

## <a name="mip_cc_label_getid"></a>MIP_CC_Label_GetId

Ottiene l'ID etichetta

**Parametri**

Parametro | Descrizione
|---|---|
| label | Label |
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

**Parametri**

Parametro | Descrizione
|---|---|
| label | Label |
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

**Parametri**

Parametro | Descrizione
|---|---|
| label | Label |
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

**Parametri**

Parametro | Descrizione
|---|---|
| label | Label |
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

**Parametri**

Parametro | Descrizione
|---|---|
| label | Label |
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

**Parametri**

Parametro | Descrizione
|---|---|
| label | Label |
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

**Parametri**

Parametro | Descrizione
|---|---|
| label | Label |
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

**Parametri**

Parametro | Descrizione
|---|---|
| label | Label |
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

**Parametri**

Parametro | Descrizione
|---|---|
| label | Label |
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

**Parametri**

Parametro | Descrizione
|---|---|
| label | Label |
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

**Parametri**

Parametro | Descrizione
|---|---|
| label | Label |
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

**Parametri**

Parametro | Descrizione
|---|---|
| label | Label |
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

**Parametri**

Parametro | Descrizione
|---|---|
| label | Label |
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

**Parametri**

Parametro | Descrizione
|---|---|
| label | Label |
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

**Parametri**

Parametro | Descrizione
|---|---|
| label | Label |
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

**Parametri**

Parametro | Descrizione
|---|---|
| label | Label |
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

**Parametri**

Parametro | Descrizione
|---|---|
| label | Label |
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

**Parametri**

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

**Parametri**

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

**Parametri**

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

**Parametri**

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

**Parametri**

Parametro | Descrizione
|---|---|
| dictionary | Dizionario da rilasciare |

```c
void MIP_CC_ReleaseMetadataDictionary(mip_cc_metadata_dictionary dictionary);
```

## <a name="mip_cc_releasepolicyhandler"></a>MIP_CC_ReleasePolicyHandler

Rilasciare le risorse associate a un gestore dei criteri

**Parametri**

Parametro | Descrizione
|---|---|
| gestore | Gestore dei criteri da rilasciare |

```c
void MIP_CC_ReleasePolicyHandler(mip_cc_policy_handler handler);
```

## <a name="mip_cc_policyhandler_getsensitivitylabel"></a>MIP_CC_PolicyHandler_GetSensitivityLabel

Ottiene l'etichetta corrente di un documento

**Parametri**

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

**Parametri**

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

**Parametri**

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

## <a name="mip_cc_protectadhocdkaction_getdoublekeyencryptionurlsize"></a>MIP_CC_ProtectAdhocDkAction_GetDoubleKeyEncryptionUrlSize

Ottiene le dimensioni del buffer necessarie per archiviare l'URL di crittografia a chiave doppia.

**Parametri**

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

**Parametri**

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

## <a name="mip_cc_protectdonotforwarddkaction_getdoublekeyencryptionurlsize"></a>MIP_CC_ProtectDoNotForwardDkAction_GetDoubleKeyEncryptionUrlSize

Ottiene le dimensioni del buffer necessarie per archiviare l'URL di crittografia a chiave doppia.

**Parametri**

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

**Parametri**

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

**Parametri**

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

**Parametri**

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

**Parametri**

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

**Parametri**

Parametro | Descrizione
|---|---|
| sensitivityType | Tipo di riservatezza da rilasciare |

```c
void MIP_CC_ReleaseSensitivityType(mip_cc_sensitivity_type sensitivityType);
```

## <a name="mip_cc_sensitivitytype_getrulepackageidsize"></a>MIP_CC_SensitivityType_GetRulePackageIdSize

Ottiene le dimensioni del buffer necessarie per archiviare l'ID del pacchetto di regole del tipo di riservatezza

**Parametri**

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

**Parametri**

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

**Parametri**

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

**Parametri**

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

