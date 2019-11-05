---
title: Funzioni
description: Funzioni.
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 11/4/2019
ms.openlocfilehash: cfc80ab9e4704c9efa5d3105f36c668bce26a6b9
ms.sourcegitcommit: 7a8eef5eb9d6440c6e2300cb3f264da31061b00d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/05/2019
ms.locfileid: "73591633"
---
# <a name="functions"></a>Funzioni

## <a name="mip_cc_auth_callback"></a>mip_cc_auth_callback

definizione della funzione di callback per l'acquisizione del token OAuth2

**Parametri**

Parametro | Description
|---|---|
| autenticazione | Indirizzo di posta elettronica per il quale verrà acquisito il token |
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

Parametro | Description
|---|---|
| URL | URL per cui l'SDK richiede il consenso dell'utente |

**Return**: risposta di consenso dell'utente

```c
MIP_CC_CALLBACK(mip_cc_consent_callback,
    mip_cc_consent,
    const char*);
```

## <a name="mip_cc_createdictionary"></a>MIP_CC_CreateDictionary

Creare un dizionario di chiavi/valori stringa

**Parametri**

Parametro | Description
|---|---|
| Voci | Matrice di coppie chiave/valore |
| count | Numero di coppie chiave/valore |
| Dizionario | Output Dizionario appena creato |

**Return**: codice risultato che indica l'esito positivo o negativo

**Nota**: è necessario liberare un Mip_cc_dictionary chiamando MIP_CC_ReleaseDictionary 

```c
mip_cc_result MIP_CC_CreateDictionary(
    const mip_cc_kv_pair* entries,
    const int64_t count,
    mip_cc_dictionary* dictionary);
```

## <a name="mip_cc_dictionary_getentries"></a>MIP_CC_Dictionary_GetEntries

Ottenere le coppie chiave/valore che compongono un dizionario

**Parametri**

Parametro | Description
|---|---|
| Dizionario | Dizionario di origine |
| Voci | Output Matrice di coppie chiave/valore, memoria di proprietà dell'oggetto mip_cc_dictionary |
| count | Output Numero di coppie chiave/valore |

**Return**: codice risultato che indica l'esito positivo o negativo

**Nota**: la memoria per ' entrys ' è di proprietà dell'oggetto mip_cc_dictionary, quindi non deve essere liberata in modo indipendente 

```c
mip_cc_result MIP_CC_Dictionary_GetEntries(
    const mip_cc_dictionary dictionary,
    mip_cc_kv_pair** entries,
    int64_t* count);
```

## <a name="mip_cc_releasedictionary"></a>MIP_CC_ReleaseDictionary

Rilasciare le risorse associate a un dizionario

**Parametri**

Parametro | Description
|---|---|
| Dizionario | Dizionario da rilasciare |

```c
void MIP_CC_ReleaseDictionary(mip_cc_dictionary dictionary);
```

## <a name="mip_cc_http_send_callback_fn"></a>mip_cc_http_send_callback_fn

Definizione della funzione di callback per l'emissione di una richiesta HTTP

**Parametri**

Parametro | Description
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

Parametro | Description
|---|---|
| IDRichiesta | ID della richiesta HTTP da annullare. |

```c
MIP_CC_CALLBACK(mip_cc_http_cancel_callback_fn,
    void,
    const char*);
```

## <a name="mip_cc_createhttpdelegate"></a>MIP_CC_CreateHttpDelegate

Crea un delegato HTTP che può essere usato per eseguire l'override dello stack HTTP predefinito di MIP

**Parametri**

Parametro | Description
|---|---|
| sendCallback | Puntatore a funzione per l'emissione di richieste HTTP |
| cancelCallback | Puntatore a funzione per l'annullamento delle richieste HTTP |
| httpDelegate | Output Handle per oggetto delegato HTTP |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_CreateHttpDelegate(
    const mip_cc_http_send_callback_fn sendCallback,
    const mip_cc_http_cancel_callback_fn cancelCallback,
    mip_cc_http_delegate* httpDelegate);
```

## <a name="mip_cc_notifyhttpdelegateresponse"></a>MIP_CC_NotifyHttpDelegateResponse

Notifica a un delegato HTTP che una risposta HTTP è pronta

**Parametri**

Parametro | Description
|---|---|
| httpDelegate | Handle per oggetto delegato HTTP |
| IDRichiesta | ID della richiesta HTTP associata a questa operazione |
| result | Stato operazione riuscita/non riuscita |
| Risposta | Risposta HTTP se l'operazione è riuscita, altrimenti nullptr |

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

Parametro | Description
|---|---|
| httpDelegate | Delegato HTTP da rilasciare |

```c
void MIP_CC_ReleaseHttpDelegate(mip_cc_http_delegate httpDelegate);
```

## <a name="mip_cc_logger_init_callback_fn"></a>mip_cc_logger_init_callback_fn

Definizione della funzione di callback per l'inizializzazione del logger

**Parametri**

Parametro | Description
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

Parametro | Description
|---|---|
| Livello | livello di registrazione per l'istruzione log. |
| Messaggio | messaggio per l'istruzione log. |
| Funzione | nome della funzione per l'istruzione log. |
| file | nome del file in cui è stata generata l'istruzione log. |
| linea | numero di riga in cui è stata generata l'istruzione log. |

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

Parametro | Description
|---|---|
| initCallback | Puntatore a funzione per l'inizializzazione |
| flushCallback | Puntatore a funzione per lo scaricamento dei log |
| writeCallback | Puntatore a funzione per la scrittura di un'istruzione log |
| loggerDelegate | Output Handle per l'oggetto delegato del logger |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_CreateLoggerDelegate(
    const mip_cc_logger_init_callback_fn initCallback,
    const mip_cc_logger_flush_callback_fn flushCallback,
    const mip_cc_logger_write_callback_fn writeCallback,
    mip_cc_logger_delegate* loggerDelegate);
```

## <a name="mip_cc_releaseloggerdelegate"></a>MIP_CC_ReleaseLoggerDelegate

Rilasciare le risorse associate a un handle del delegato del logger

**Parametri**

Parametro | Description
|---|---|
| loggerDelegate | Delegato del logger da rilasciare |

```c
void MIP_CC_ReleaseLoggerDelegate(mip_cc_logger_delegate loggerDelegate);
```

## <a name="mip_cc_createmipcontext"></a>MIP_CC_CreateMipContext

Creare un contesto MIP per gestire lo stato condiviso tra tutte le istanze del profilo

**Parametri**

Parametro | Description
|---|---|
| applicationInfo | Informazioni sull'applicazione che utilizza l'SDK di protezione |
| percorso | Percorso del file in cui sono archiviati i dati di registrazione, telemetria e altro materiale collaterale per la protezione |
| logLevel | Livello di registrazione minimo per. miplog |
| isOfflineOnly | Abilita/Disabilita le operazioni di rete (non tutte le azioni supportate quando offline) |
| loggerDelegateOverride | Opzionale Implementazione dell'override del logger |
| telemetryOverride | Opzionale Impostazioni di telemetria sottoposte a override. Se NULL, verranno usate le impostazioni predefinite |
| mipContext | Output Istanza del contesto MIP appena creata |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_CreateMipContext(
    const mip_cc_application_info* applicationInfo,
    const char* path,
    const mip_cc_log_level logLevel,
    const bool isOfflineOnly,
    const mip_cc_logger_delegate loggerDelegateOverride,
    const mip_cc_telemetry_configuration telemetryOverride,
    mip_cc_mip_context* mipContext);
```

## <a name="mip_cc_createmipcontextwithcustomfeaturesettings"></a>MIP_CC_CreateMipContextWithCustomFeatureSettings

Creare un contesto MIP per gestire lo stato condiviso tra tutte le istanze del profilo

**Parametri**

Parametro | Description
|---|---|
| applicationInfo | Informazioni sull'applicazione che utilizza l'SDK di protezione |
| percorso | Percorso del file in cui sono archiviati i dati di registrazione, telemetria e altro materiale collaterale per la protezione |
| logLevel | Livello di registrazione minimo per. miplog |
| isOfflineOnly | Abilita/Disabilita le operazioni di rete (non tutte le azioni supportate quando offline) |
| loggerDelegateOverride | Opzionale Implementazione dell'override del logger |
| telemetryOverride | Opzionale Impostazioni di telemetria sottoposte a override. Se NULL, verranno usate le impostazioni predefinite |
| featureSettings | Opzionale Matrice di override di funzionalità personalizzate |
| featureSettingsSize | Dimensioni delle sostituzioni di funzionalità personalizzate (in numero di sostituzioni) |
| mipContext | Output Istanza del contesto MIP appena creata |

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
    mip_cc_mip_context* mipContext);
```

## <a name="mip_cc_releasemipcontext"></a>MIP_CC_ReleaseMipContext

Rilascia le risorse associate a un contesto MIP

**Parametri**

Parametro | Description
|---|---|
| mipContext | Contesto MIP da rilasciare |

```c
void MIP_CC_ReleaseMipContext(mip_cc_mip_context mipContext);
```

## <a name="mip_cc_protectiondescriptor_getprotectiontype"></a>MIP_CC_ProtectionDescriptor_GetProtectionType

Ottiene il tipo di protezione, indipendentemente dal fatto che sia definito da un modello RMS

**Parametri**

Parametro | Description
|---|---|
| protectionDescriptor | Descrittore associato al contenuto protetto |
| ProtectionType | Output Tipo di protezione |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_ProtectionDescriptor_GetProtectionType(
    const mip_cc_protection_descriptor protectionDescriptor,
    mip_cc_protection_type* protectionType);
```

## <a name="mip_cc_protectiondescriptor_getownersize"></a>MIP_CC_ProtectionDescriptor_GetOwnerSize

Ottiene le dimensioni del buffer necessarie per archiviare il proprietario

**Parametri**

Parametro | Description
|---|---|
| protectionDescriptor | Descrittore associato al contenuto protetto |
| ownerSize | Output Dimensioni del buffer per il possesso del proprietario (in numero di caratteri) |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_ProtectionDescriptor_GetOwnerSize(
    const mip_cc_protection_descriptor protectionDescriptor,
    int64_t* ownerSize);
```

## <a name="mip_cc_protectiondescriptor_getowner"></a>MIP_CC_ProtectionDescriptor_GetOwner

Ottiene il proprietario della protezione

**Parametri**

Parametro | Description
|---|---|
| protectionDescriptor | Descrittore associato al contenuto protetto |
| ownerBuffer | Output Buffer in cui verrà copiato il proprietario. |
| ownerBufferSize | Dimensioni (in numero di caratteri) di ownerBuffer. |
| actualOwnerSize | Output Numero di caratteri scritti nel buffer |

**Return**: codice risultato che indica l'esito positivo o negativo

**Nota**: se ownerBuffer è null o insufficiente, viene restituito MIP_RESULT_ERROR_INSUFFICIENT_BUFFER e actualOwnerSize viene impostato sulle dimensioni minime del buffer richiesto. 

```c
mip_cc_result MIP_CC_ProtectionDescriptor_GetOwner(
    const mip_cc_protection_descriptor protectionDescriptor,
    char* ownerBuffer,
    const int64_t ownerBufferSize,
    int64_t* actualOwnerSize);
```

## <a name="mip_cc_protectiondescriptor_getnamesize"></a>MIP_CC_ProtectionDescriptor_GetNameSize

Ottiene le dimensioni del buffer necessarie per archiviare il nome

**Parametri**

Parametro | Description
|---|---|
| protectionDescriptor | Descrittore associato al contenuto protetto |
| nameSize | Output Dimensione del buffer in cui memorizzare il nome (in numero di caratteri) |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_ProtectionDescriptor_GetNameSize(
    const mip_cc_protection_descriptor protectionDescriptor,
    int64_t* nameSize);
```

## <a name="mip_cc_protectiondescriptor_getname"></a>MIP_CC_ProtectionDescriptor_GetName

Ottiene il nome della protezione

**Parametri**

Parametro | Description
|---|---|
| protectionDescriptor | Descrittore associato al contenuto protetto |
| nameBuffer | Output Buffer in cui verrà copiato il nome. |
| nameBufferSize | Dimensioni (in numero di caratteri) di nameBuffer. |
| actualNameSize | Output Numero di caratteri scritti nel buffer |

**Return**: codice risultato che indica l'esito positivo o negativo

**Nota**: se nameBuffer è null o insufficiente, viene restituito MIP_RESULT_ERROR_INSUFFICIENT_BUFFER e actualNameSize viene impostato sulle dimensioni minime del buffer richiesto. 

```c
mip_cc_result MIP_CC_ProtectionDescriptor_GetName(
    const mip_cc_protection_descriptor protectionDescriptor,
    char* nameBuffer,
    const int64_t nameBufferSize,
    int64_t* actualNameSize);
```

## <a name="mip_cc_protectiondescriptor_getdescriptionsize"></a>MIP_CC_ProtectionDescriptor_GetDescriptionSize

Ottiene la dimensione del buffer necessaria per archiviare la descrizione

**Parametri**

Parametro | Description
|---|---|
| protectionDescriptor | Descrittore associato al contenuto protetto |
| descriptionSize | Output Dimensione del buffer in cui memorizzare la descrizione (in numero di caratteri) |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_ProtectionDescriptor_GetDescriptionSize(
    const mip_cc_protection_descriptor protectionDescriptor,
    int64_t* descriptionSize);
```

## <a name="mip_cc_protectiondescriptor_getdescription"></a>MIP_CC_ProtectionDescriptor_GetDescription

Ottiene la descrizione della protezione

**Parametri**

Parametro | Description
|---|---|
| protectionDescriptor | Descrittore associato al contenuto protetto |
| descriptionBuffer | Output Buffer in cui verrà copiata la descrizione. |
| descriptionBufferSize | Dimensioni (in numero di caratteri) di descriptionBuffer. |
| actualDescriptionSize | Output Numero di caratteri scritti nel buffer |

**Return**: codice risultato che indica l'esito positivo o negativo

**Nota**: se descriptionBuffer è null o insufficiente, viene restituito MIP_RESULT_ERROR_INSUFFICIENT_BUFFER e actualDescriptionSize viene impostato sulle dimensioni minime del buffer richiesto. 

```c
mip_cc_result MIP_CC_ProtectionDescriptor_GetDescription(
    const mip_cc_protection_descriptor protectionDescriptor,
    char* descriptionBuffer,
    const int64_t descriptionBufferSize,
    int64_t* actualDescriptionSize);
```

## <a name="mip_cc_protectiondescriptor_gettemplateid"></a>MIP_CC_ProtectionDescriptor_GetTemplateId

Ottiene l'ID modello

**Parametri**

Parametro | Description
|---|---|
| protectionDescriptor | Descrittore associato al contenuto protetto |
| templateId | Output ID modello associato alla protezione |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_ProtectionDescriptor_GetTemplateId(
    const mip_cc_protection_descriptor protectionDescriptor,
    mip_cc_guid* templateId);
```

## <a name="mip_cc_protectiondescriptor_getlabelid"></a>MIP_CC_ProtectionDescriptor_GetLabelId

Ottiene l'ID etichetta

**Parametri**

Parametro | Description
|---|---|
| protectionDescriptor | Descrittore associato al contenuto protetto |
| LabelId | Output ID etichetta associato alla protezione |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_ProtectionDescriptor_GetLabelId(
    const mip_cc_protection_descriptor protectionDescriptor,
    mip_cc_guid* labelId);
```

## <a name="mip_cc_protectiondescriptor_getcontentid"></a>MIP_CC_ProtectionDescriptor_GetContentId

Ottiene l'ID contenuto

**Parametri**

Parametro | Description
|---|---|
| protectionDescriptor | Descrittore associato al contenuto protetto |
| contentId | Output ID contenuto associato alla protezione |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_ProtectionDescriptor_GetContentId(
    const mip_cc_protection_descriptor protectionDescriptor,
    mip_cc_guid* contentId);
```

## <a name="mip_cc_protectiondescriptor_doescontentexpire"></a>MIP_CC_ProtectionDescriptor_DoesContentExpire

Ottiene un valore che indica se il contenuto ha una data di scadenza

**Parametri**

Parametro | Description
|---|---|
| protectionDescriptor | Descrittore associato al contenuto protetto |
| doesContentExpire | Output Indica se il contenuto scade |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_ProtectionDescriptor_DoesContentExpire(
    const mip_cc_protection_descriptor protectionDescriptor,
    bool* doesContentExpire);
```

## <a name="mip_cc_protectiondescriptor_getcontentvaliduntil"></a>MIP_CC_ProtectionDescriptor_GetContentValidUntil

Ottiene l'ora di scadenza della protezione (in secondi da Epoch)

**Parametri**

Parametro | Description
|---|---|
| protectionDescriptor | Descrittore associato al contenuto protetto |
| contentValidUntil | Output Data di scadenza del contenuto (in secondi da Epoch) |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_ProtectionDescriptor_GetContentValidUntil(
    const mip_cc_protection_descriptor protectionDescriptor,
    int64_t* contentValidUntil);
```

## <a name="mip_cc_protectiondescriptor_doesallowofflineaccess"></a>MIP_CC_ProtectionDescriptor_DoesAllowOfflineAccess

Ottiene un valore che indica se è consentito o meno l'accesso offline

**Parametri**

Parametro | Description
|---|---|
| protectionDescriptor | Descrittore associato al contenuto protetto |
| doesAllowOfflineAccess | Output Indica se è consentito o meno l'accesso offline |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_ProtectionDescriptor_DoesAllowOfflineAccess(
    const mip_cc_protection_descriptor protectionDescriptor,
    bool* doesAllowOfflineAccess);
```

## <a name="mip_cc_protectiondescriptor_getreferrersize"></a>MIP_CC_ProtectionDescriptor_GetReferrerSize

Ottiene le dimensioni del buffer necessarie per archiviare il referrer

**Parametri**

Parametro | Description
|---|---|
| protectionDescriptor | Descrittore associato al contenuto protetto |
| referrerSize | Output Dimensione del buffer in cui memorizzare il referrer (in numero di caratteri) |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_ProtectionDescriptor_GetReferrerSize(
    const mip_cc_protection_descriptor protectionDescriptor,
    int64_t* referrerSize);
```

## <a name="mip_cc_protectiondescriptor_getreferrer"></a>MIP_CC_ProtectionDescriptor_GetReferrer

Ottiene il referrer di protezione

**Parametri**

Parametro | Description
|---|---|
| protectionDescriptor | Descrittore associato al contenuto protetto |
| referrerBuffer | Output Buffer in cui verrà copiato il referrer. |
| referrerBufferSize | Dimensioni (in numero di caratteri) di referrerBuffer. |
| actualReferrerSize | Output Numero di caratteri scritti nel buffer |

**Return**: codice risultato che indica l'esito positivo o negativo

**Nota**: se referrerBuffer è null o insufficiente, viene restituito MIP_RESULT_ERROR_INSUFFICIENT_BUFFER e actualReferrerSize viene impostato sulle dimensioni minime del buffer richiesto. 

```c
mip_cc_result MIP_CC_ProtectionDescriptor_GetReferrer(
    const mip_cc_protection_descriptor protectionDescriptor,
    char* referrerBuffer,
    const int64_t referrerBufferSize,
    int64_t* actualReferrerSize);
```

## <a name="mip_cc_releaseprotectiondescriptor"></a>MIP_CC_ReleaseProtectionDescriptor

Rilascia le risorse associate a un descrittore di protezione

**Parametri**

Parametro | Description
|---|---|
| protectionDescriptor | Descrittore di protezione da rilasciare |

```c
void MIP_CC_ReleaseProtectionDescriptor(mip_cc_protection_descriptor protectionDescriptor);
```

## <a name="mip_cc_createstringlist"></a>MIP_CC_CreateStringList

Creare un elenco di stringhe

**Parametri**

Parametro | Description
|---|---|
| Stringhe | Matrice di stringhe |
| count | Numero di stringhe |
| stringList | Output Elenco di stringhe appena creato |

**Return**: codice risultato che indica l'esito positivo o negativo

**Nota**: è necessario liberare un Mip_cc_string_list chiamando MIP_CC_ReleaseStringList 

```c
mip_cc_result MIP_CC_CreateStringList(
    const char** strings,
    const int64_t count,
    mip_cc_string_list* stringList);
```

## <a name="mip_cc_stringlist_getstrings"></a>MIP_CC_StringList_GetStrings

Ottenere stringhe che compongono un elenco di stringhe

**Parametri**

Parametro | Description
|---|---|
| stringList | Elenco di stringhe di origine |
| Stringhe | Output Matrice di stringhe, memoria di proprietà dell'oggetto mip_cc_string_list |
| count | Output Numero di stringhe |

**Return**: codice risultato che indica l'esito positivo o negativo

**Nota**: la memoria per ' Strings ' è di proprietà dell'oggetto mip_cc_string_list, quindi non deve essere liberata in modo indipendente 

```c
mip_cc_result MIP_CC_StringList_GetStrings(
    const mip_cc_string_list stringList,
    const char*** strings,
    int64_t* count);
```

## <a name="mip_cc_releasestringlist"></a>MIP_CC_ReleaseStringList

Rilasciare le risorse associate a un elenco di stringhe

**Parametri**

Parametro | Description
|---|---|
| stringList | Elenco di stringhe da rilasciare |

```c
void MIP_CC_ReleaseStringList(mip_cc_string_list stringList);
```

## <a name="mip_cc_dispatch_task_callback_fn"></a>mip_cc_dispatch_task_callback_fn

Definizione della funzione di callback per l'invio di un'attività asincrona

**Parametri**

Parametro | Description
|---|---|
| TaskId | Identificatore univoco dell'attività |

```c
MIP_CC_CALLBACK(mip_cc_dispatch_task_callback_fn,
    void,
    const mip_cc_async_task*);
```

## <a name="mip_cc_cancel_task_callback_fn"></a>mip_cc_cancel_task_callback_fn

Funzione di callback per l'annullamento di un'attività in background

**Parametri**

Parametro | Description
|---|---|
| TaskId | Identificatore univoco dell'attività |

**Return**: true se l'attività è stata annullata correttamente; in caso contrario, false

```c
MIP_CC_CALLBACK(mip_cc_cancel_task_callback_fn,
    bool,
    const char*);
```

## <a name="mip_cc_createtaskdispatcherdelegate"></a>MIP_CC_CreateTaskDispatcherDelegate

Crea un delegato del dispatcher di attività che può essere usato per eseguire l'override della gestione delle attività asincrone predefinite di MIP

**Parametri**

Parametro | Description
|---|---|
| dispatchTaskCallback | Puntatore a funzione per l'invio di attività asincrone |
| cancelTaskCallback | Puntatore a funzione per l'annullamento delle attività in background |
| cancelAllTasksCallback | Puntatore a funzione per l'annullamento di tutte le attività in background |
| taskDispatcher | Output Handle per l'oggetto delegato del dispatcher attività |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_CreateTaskDispatcherDelegate(
    const mip_cc_dispatch_task_callback_fn dispatchTaskCallback,
    const mip_cc_cancel_task_callback_fn cancelTaskCallback,
    const mip_cc_cancel_all_tasks_callback_fn cancelAllTasksCallback,
    mip_cc_task_dispatcher_delegate* taskDispatcher);
```

## <a name="mip_cc_executedispatchedtask"></a>MIP_CC_ExecuteDispatchedTask

Notifica a un delegato TaskDispatcher che un'attività è pianificata per l'esecuzione nel thread corrente

**Parametri**

Parametro | Description
|---|---|
| taskDispatcher | Handle per l'oggetto delegato del dispatcher attività |
| TaskId | ID dell'attività asincrona associata a questa operazione |

**Nota**: questa funzione deve essere chiamata dall'applicazione quando è pianificata l'esecuzione di un'attività. Il risultato sarà l'esecuzione immediata dell'attività sul thread corrente. L'ID deve corrispondere a quello di un'attività non annullata in precedenza. 

```c
void MIP_CC_ExecuteDispatchedTask(const mip_cc_task_dispatcher_delegate taskDispatcher, const char* taskId);
```

## <a name="mip_cc_releasetaskdispatcherdelegate"></a>MIP_CC_ReleaseTaskDispatcherDelegate

Rilasciare le risorse associate a un handle del delegato del dispatcher attività

**Parametri**

Parametro | Description
|---|---|
| taskDispatcher | Delegato Dispatcher attività da rilasciare |

```c
void MIP_CC_ReleaseTaskDispatcherDelegate(mip_cc_task_dispatcher_delegate taskDispatcher);
```

## <a name="mip_cc_telemetryconfiguration_sethostname"></a>MIP_CC_TelemetryConfiguration_SetHostName

Impostare un nome host di telemetria che sostituirà le impostazioni di telemetria interne

**Parametri**

Parametro | Description
|---|---|
| telemetryConfig | Configurazione della telemetria |
| Nome host | Nome dell'host |

**Return**: codice risultato che indica l'esito positivo o negativo

**Nota**: questa proprietà viene impostata quando un'applicazione client usa lo stesso componente di telemetria aria/1Ds e desidera le impostazioni di telemetria interne (memorizzazione nella cache, registrazione, priorità e così via) da usare anziché le impostazioni predefinite del MIP 

```c
mip_cc_result MIP_CC_TelemetryConfiguration_SetHostName(
    const mip_cc_telemetry_configuration telemetryConfig,
    const char* hostName);
```

## <a name="mip_cc_telemetryconfiguration_setlibraryname"></a>MIP_CC_TelemetryConfiguration_SetLibraryName

Impostare un override della libreria condivisa di telemetria

**Parametri**

Parametro | Description
|---|---|
| telemetryConfig | Configurazione della telemetria |
| NomeLibreria | Nome della DLL che implementa l'API C di aria/1DS SDK |

**Return**: codice risultato che indica l'esito positivo o negativo

**Nota**: questa proprietà viene impostata quando un client ha una DLL di telemetria esistente che implementa l'API C di aria/1Ds SDK da usare al posto di mip_ClientTelemetry. dll 

```c
mip_cc_result MIP_CC_TelemetryConfiguration_SetLibraryName(
    const mip_cc_telemetry_configuration telemetryConfig,
    const char* libraryName);
```

## <a name="mip_cc_telemetryconfiguration_sethttpdelegate"></a>MIP_CC_TelemetryConfiguration_SetHttpDelegate

Esegui override dello stack HTTP di telemetria predefinito con il proprio client

**Parametri**

Parametro | Description
|---|---|
| telemetryConfig | Configurazione della telemetria |
| httpDelegate | Istanza di callback HTTP implementata dall'applicazione client |

**Return**: codice risultato che indica l'esito positivo o negativo

**Nota**: se questa proprietà non è impostata, il componente di telemetria userà lo stack HTTP predefinito del MIP 

```c
mip_cc_result MIP_CC_TelemetryConfiguration_SetHttpDelegate(
    const mip_cc_telemetry_configuration telemetryConfig,
    const mip_cc_http_delegate httpDelegate);
```

## <a name="mip_cc_telemetryconfiguration_setisnetworkdetectionenabled"></a>MIP_CC_TelemetryConfiguration_SetIsNetworkDetectionEnabled

Indica se il componente di telemetria è autorizzato a eseguire il ping dello stato della rete in un thread in background

**Parametri**

Parametro | Description
|---|---|
| telemetryConfig | Configurazione della telemetria |
| isCachingEnabled | Indica se il componente di telemetria è autorizzato a eseguire il ping dello stato della rete in un thread in background |

**Return**: codice risultato che indica l'esito positivo o negativo

**Nota**: il valore predefinito è' true ' 

```c
mip_cc_result MIP_CC_TelemetryConfiguration_SetIsNetworkDetectionEnabled(
    const mip_cc_telemetry_configuration telemetryConfig,
    const bool isNetworkDetectionEnabled);
```

## <a name="mip_cc_telemetryconfiguration_setislocalcachingenabled"></a>MIP_CC_TelemetryConfiguration_SetIsLocalCachingEnabled

Imposta un valore che indica se il componente di telemetria può scrivere le cache sul disco

**Parametri**

Parametro | Description
|---|---|
| telemetryConfig | Configurazione della telemetria |
| isCachingEnabled | Indica se il componente di telemetria può scrivere cache sul disco |

**Return**: codice risultato che indica l'esito positivo o negativo

**Nota**: il valore predefinito è' true ' 

```c
mip_cc_result MIP_CC_TelemetryConfiguration_SetIsLocalCachingEnabled(
    const mip_cc_telemetry_configuration telemetryConfig,
    const bool isCachingEnabled);
```

## <a name="mip_cc_telemetryconfiguration_setistraceloggingenabled"></a>MIP_CC_TelemetryConfiguration_SetIsTraceLoggingEnabled

Imposta un valore che indica se il componente di telemetria può scrivere i log su disco

**Parametri**

Parametro | Description
|---|---|
| telemetryConfig | Configurazione della telemetria |
| isTraceLoggingEnabled | Indica se il componente di telemetria è autorizzato a scrivere log su disco |

**Return**: codice risultato che indica l'esito positivo o negativo

**Nota**: il valore predefinito è' true ' 

```c
mip_cc_result MIP_CC_TelemetryConfiguration_SetIsTraceLoggingEnabled(
    const mip_cc_telemetry_configuration telemetryConfig,
    const bool isTraceLoggingEnabled);
```

## <a name="mip_cc_telemetryconfiguration_setistelemetryoptedout"></a>MIP_CC_TelemetryConfiguration_SetIsTelemetryOptedOut

Imposta un valore che indica se un'applicazione o un utente ha rifiutato la telemetria facoltativa

**Parametri**

Parametro | Description
|---|---|
| telemetryConfig | Configurazione della telemetria |
| isTelemetryOptedOut | Se un'applicazione o un utente non ha rifiutato la telemetria facoltativa |

**Return**: codice risultato che indica l'esito positivo o negativo

**Nota**: il valore predefinito è' false ' 

```c
mip_cc_result MIP_CC_TelemetryConfiguration_SetIsTelemetryOptedOut(
    const mip_cc_telemetry_configuration telemetryConfig,
    const bool isTelemetryOptedOut);
```

## <a name="mip_cc_telemetryconfiguration_setcustomsettings"></a>MIP_CC_TelemetryConfiguration_SetCustomSettings

Imposta le impostazioni di telemetria personalizzate

**Parametri**

Parametro | Description
|---|---|
| telemetryConfig | Configurazione della telemetria |
| customSettings | Impostazioni di telemetria personalizzate |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_TelemetryConfiguration_SetCustomSettings(
    const mip_cc_telemetry_configuration telemetryConfig,
    const mip_cc_dictionary customSettings);
```

## <a name="mip_cc_releasetelemetryconfiguration"></a>MIP_CC_ReleaseTelemetryConfiguration

Rilascia le risorse associate a impostazioni del profilo di protezione

**Parametri**

Parametro | Description
|---|---|
| profileSettings | Impostazioni del profilo di protezione da rilasciare |

```c
void MIP_CC_ReleaseTelemetryConfiguration(mip_cc_telemetry_configuration telemetryConfig);
```

## <a name="mip_cc_releaseprotectionengine"></a>MIP_CC_ReleaseProtectionEngine

Rilasciare le risorse associate a un motore di protezione

**Parametri**

Parametro | Description
|---|---|
| Motore | Motore di protezione da rilasciare |

```c
void MIP_CC_ReleaseProtectionEngine(mip_cc_protection_engine engine);
```

## <a name="mip_cc_protectionengine_createprotectionhandlerforpublishing"></a>MIP_CC_ProtectionEngine_CreateProtectionHandlerForPublishing

Crea un gestore protezione per la pubblicazione di nuovo contenuto

**Parametri**

Parametro | Description
|---|---|
| Motore | Motore in cui verrà creato un gestore |
| impostazioni | Impostazioni del gestore protezione |
| contesto | Contesto client che verrà passato in modo opaco a HttpDelegate e AuthDelegate |
| Gestore | Output Istanza del gestore protezione appena creata |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_ProtectionEngine_CreateProtectionHandlerForPublishing(
    const mip_cc_protection_engine engine,
    const mip_cc_protection_handler_publishing_settings settings,
    const void* context,
    mip_cc_protection_handler* handler);
```

## <a name="mip_cc_protectionengine_createprotectionhandlerforconsumption"></a>MIP_CC_ProtectionEngine_CreateProtectionHandlerForConsumption

Crea un gestore protezione per l'utilizzo del contenuto esistente

**Parametri**

Parametro | Description
|---|---|
| Motore | Motore in cui verrà creato un gestore |
| impostazioni | Impostazioni del gestore protezione |
| contesto | Contesto client che verrà passato in modo opaco a HttpDelegate e AuthDelegate |
| Gestore | Output Istanza del gestore protezione appena creata |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_ProtectionEngine_CreateProtectionHandlerForConsumption(
  const mip_cc_protection_engine engine,
  const mip_cc_protection_handler_consumption_settings settings,
  const void* context,
  mip_cc_protection_handler* handler);
```

## <a name="mip_cc_protectionengine_getengineidsize"></a>MIP_CC_ProtectionEngine_GetEngineIdSize

Ottiene le dimensioni del buffer necessario per l'ID del motore

**Parametri**

Parametro | Description
|---|---|
| Motore | Motore di protezione |
| idSize | Output Dimensione del buffer in cui memorizzare l'ID del motore (in numero di caratteri) |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_ProtectionEngine_GetEngineIdSize(
    const mip_cc_protection_engine engine,
    int64_t* idSize);
```

## <a name="mip_cc_protectionengine_getengineid"></a>MIP_CC_ProtectionEngine_GetEngineId

Ottiene l'ID del motore

**Parametri**

Parametro | Description
|---|---|
| Motore | Motore di protezione |
| idBuffer | Output Buffer in cui verrà copiato l'ID. |
| idBufferSize | Dimensioni (in numero di caratteri) di idBuffer. |
| actualIdSize | Output Numero di caratteri scritti nel buffer |

**Return**: codice risultato che indica l'esito positivo o negativo

**Nota**: se idBuffer è null o insufficiente, viene restituito MIP_RESULT_ERROR_INSUFFICIENT_BUFFER e actualIdSize viene impostato sulle dimensioni minime del buffer richiesto. 

```c
mip_cc_result MIP_CC_ProtectionEngine_GetEngineId(
    const mip_cc_protection_engine engine,
    char* idBuffer,
    const int64_t idBufferSize,
    int64_t* actualIdSize);
```

## <a name="mip_cc_protectionengine_gettemplatessize"></a>MIP_CC_ProtectionEngine_GetTemplatesSize

Ottiene il numero di modelli RMS associati a un motore di protezione

**Parametri**

Parametro | Description
|---|---|
| Motore | Motore di protezione |
| contesto | Contesto client che verrà passato in modo opaco a HttpDelegate e AuthDelegate |
| templatesSize | Output Numero di modelli |

**Return**: codice risultato che indica l'esito positivo o negativo

**Nota**: questa API può causare un'operazione HTTP indipendente. Si consiglia di usare ' MIP_CC_ProtectionEngine_GetTemplates ' direttamente con un buffer predefinito per evitare operazioni HTTP aggiuntive superflue. 

```c
mip_cc_result MIP_CC_ProtectionEngine_GetTemplatesSize(
    const mip_cc_protection_engine engine,
    const void* context,
    int64_t* templatesSize);
```

## <a name="mip_cc_protectionengine_gettemplates"></a>MIP_CC_ProtectionEngine_GetTemplates

Ottenere la raccolta di modelli disponibili per un utente

**Parametri**

Parametro | Description
|---|---|
| Motore | Motore di protezione |
| contesto | Contesto client che verrà passato in modo opaco a HttpDelegate e AuthDelegate |
| templateBuffer | Output Buffer in cui verranno copiati i modelli. |
| templateBufferSize | Dimensioni (in numero di elementi) di templateBuffer. |
| actualTemplatesSize | Output Numero di ID modello scritti nel buffer |

**Return**: codice risultato che indica l'esito positivo o negativo

**Nota**: se templateBuffer è null o insufficiente, viene restituito MIP_RESULT_ERROR_INSUFFICIENT_BUFFER e actualTemplateSize viene impostato sulle dimensioni minime del buffer richiesto. 

```c
mip_cc_result MIP_CC_ProtectionEngine_GetTemplates(
    const mip_cc_protection_engine engine,
    const void* context,
    mip_cc_guid* templateBuffer,
    const int64_t templateBufferSize,
    int64_t* actualTemplatesSize);
```

## <a name="mip_cc_protectionengine_getrightsforlabelid"></a>MIP_CC_ProtectionEngine_GetRightsForLabelId

Ottiene l'elenco dei diritti concessi a un utente per un ID etichetta

**Parametri**

Parametro | Description
|---|---|
| Motore | Motore di protezione |
| contesto | Contesto client che verrà passato in modo opaco a HttpDelegate e AuthDelegate |
| documentId | ID documento assegnato al documento |
| LabelId | ID etichetta applicato al documento |
| ownerEmail | Proprietario del documento |
| delagedUserEmail | Messaggio di posta elettronica dell'utente se l'utente o l'applicazione di autenticazione agisce per conto di un altro utente, vuoto se non è presente alcun valore |
| diritti | Output Elenco dei diritti concessi a un utente, memoria di proprietà del chiamante |

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
    mip_cc_string_list* rights);
```

## <a name="mip_cc_protectionengine_getclientdatasize"></a>MIP_CC_ProtectionEngine_GetClientDataSize

Ottiene le dimensioni dei dati client associati a un motore di protezione

**Parametri**

Parametro | Description
|---|---|
| Motore | Motore di protezione |
| clientDataSize | Output Dimensioni dei dati client (in numero di caratteri) |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_ProtectionEngine_GetClientDataSize(
    const mip_cc_protection_engine engine,
    int64_t* clientDataSize);
```

## <a name="mip_cc_protectionengine_getclientdata"></a>MIP_CC_ProtectionEngine_GetClientData

Ottenere i dati client associati a un motore di protezione

**Parametri**

Parametro | Description
|---|---|
| Motore | Motore di protezione |
| clientDataBuffer | Output Buffer in cui verranno copiati i dati client |
| clientDataBufferSize | Dimensioni (in numero di caratteri) di clientDataBuffer. |
| actualClientDataSize | Output Numero di caratteri scritti nel buffer |

**Return**: codice risultato che indica l'esito positivo o negativo

**Nota**: se clientDataBuffer è null o insufficiente, viene restituito MIP_RESULT_ERROR_INSUFFICIENT_BUFFER e actualClientDataSize viene impostato sulle dimensioni minime del buffer richiesto. 

```c
mip_cc_result MIP_CC_ProtectionEngine_GetClientData(
    const mip_cc_protection_engine engine,
    char* clientDataBuffer,
    const int64_t clientDataBufferSize,
    int64_t* actualClientDataSize);
```

## <a name="mip_cc_createprotectionenginesettingswithidentity"></a>MIP_CC_CreateProtectionEngineSettingsWithIdentity

Creare un oggetto impostazioni usato per creare un nuovo motore di protezione

**Parametri**

Parametro | Description
|---|---|
| autenticazione | Identità che verrà associata a ProtectionEngine |
| clientData | Dati client personalizzabili archiviati insieme al motore |
| locale | Impostazioni locali in cui vengono restituiti i risultati del testo |
| engineSettings | Output Istanza di impostazioni appena creata |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_CreateProtectionEngineSettingsWithIdentity(
    const mip_cc_identity* identity,
    const char* clientData,
    const char* locale,
    mip_cc_protection_engine_settings* engineSettings);
```

## <a name="mip_cc_protectionenginesettings_setclientdata"></a>MIP_CC_ProtectionEngineSettings_SetClientData

Imposta i dati client che verranno archiviati in maniera opaca insieme a questo motore e mantengono tra le sessioni

**Parametri**

Parametro | Description
|---|---|
| impostazioni | Impostazioni motore |
| clientData | Dati client |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_ProtectionEngineSettings_SetClientData(
    const mip_cc_protection_engine_settings engineSettings,
    const char* clientData);
```

## <a name="mip_cc_protectionenginesettings_setcustomsettings"></a>MIP_CC_ProtectionEngineSettings_SetCustomSettings

Configura le impostazioni personalizzate, usate per il controllo e il controllo delle funzionalità.

**Parametri**

Parametro | Description
|---|---|
| engineSettings | Impostazioni motore |
| customSettings | Coppie chiave/valore di impostazioni personalizzate |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_ProtectionEngineSettings_SetCustomSettings(
    const mip_cc_protection_engine_settings engineSettings,
    const mip_cc_dictionary customSettings);
```

## <a name="mip_cc_protectionenginesettings_setsessionid"></a>MIP_CC_ProtectionEngineSettings_SetSessionId

Imposta l'ID di sessione che può essere usato per correlare i log e i dati di telemetria

**Parametri**

Parametro | Description
|---|---|
| impostazioni | Impostazioni motore |
| sessionId | ID sessione che rappresenta la durata di un motore di protezione |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_ProtectionEngineSettings_SetSessionId(
    const mip_cc_protection_engine_settings engineSettings,
    const char* sessionId);
```

## <a name="mip_cc_protectionenginesettings_setcloudendpointbaseurl"></a>MIP_CC_ProtectionEngineSettings_SetCloudEndpointBaseUrl

Imposta l'URL di base per tutte le richieste di servizio

**Parametri**

Parametro | Description
|---|---|
| impostazioni | Impostazioni motore |
| cloudEndpointBaseUrl | URL di base (ad esempio 'https://api.aadrm.com ') |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_ProtectionEngineSettings_SetCloudEndpointBaseUrl(
    const mip_cc_protection_engine_settings engineSettings,
    const char* cloudEndpointBaseUrl);
```

## <a name="mip_cc_releaseprotectionenginesettings"></a>MIP_CC_ReleaseProtectionEngineSettings

Rilasciare le risorse associate a impostazioni del motore di protezione

**Parametri**

Parametro | Description
|---|---|
| engineSettings | Impostazioni del motore di protezione da rilasciare |

```c
void MIP_CC_ReleaseProtectionEngineSettings(mip_cc_protection_engine_settings engineSettings);
```

## <a name="mip_cc_createprotectionhandlerpublishingsettings"></a>MIP_CC_CreateProtectionHandlerPublishingSettings

Creare un oggetto impostazioni utilizzato per creare un gestore protezione per la pubblicazione di nuovo contenuto

**Parametri**

Parametro | Description
|---|---|
| descrittore | Dettagli sulla protezione |
| impostazioni | Output Istanza di impostazioni appena creata |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_CreateProtectionHandlerPublishingSettings(
    const mip_cc_protection_descriptor descriptor,
    mip_cc_protection_handler_publishing_settings* settings);
```

## <a name="mip_cc_protectionhandlerpublishingsettings_setisdeprecatedalgorithmpreferred"></a>MIP_CC_ProtectionHandlerPublishingSettings_SetIsDeprecatedAlgorithmPreferred

Imposta un valore che indica se è preferibile un algoritmo di crittografia deprecato (BCE) per la compatibilità con le versioni precedenti

**Parametri**

Parametro | Description
|---|---|
| impostazioni | Impostazioni del gestore protezione |
| isDeprecatedAlgorithmPreferred | Indica se è preferibile l'algoritmo deprecato |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_ProtectionHandlerPublishingSettings_SetIsDeprecatedAlgorithmPreferred(
    const mip_cc_protection_handler_publishing_settings settings,
    const bool isDeprecatedAlgorithmPreferred);
```

## <a name="mip_cc_protectionhandlerpublishingsettings_setisauditedextractionallowed"></a>MIP_CC_ProtectionHandlerPublishingSettings_SetIsAuditedExtractionAllowed

Imposta un valore che indica se le applicazioni non compatibili con MIP possono aprire contenuto protetto

**Parametri**

Parametro | Description
|---|---|
| impostazioni | Impostazioni del gestore protezione |
| isAuditedExtractionAllowed | Indica se le applicazioni non compatibili con MIP possono aprire contenuto protetto |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_ProtectionHandlerPublishingSettings_SetIsAuditedExtractionAllowed(
    const mip_cc_protection_handler_publishing_settings settings,
    const bool isAuditedExtractionAllowed);
```

## <a name="mip_cc_protectionhandlerpublishingsettings_setispublishingformatjson"></a>MIP_CC_ProtectionHandlerPublishingSettings_SetIsPublishingFormatJson

Imposta un valore che indica se PL è in formato JSON (il valore predefinito è XML)

**Parametri**

Parametro | Description
|---|---|
| impostazioni | Impostazioni del gestore protezione |
| isPublishingFormatJson | Indica se il PL risultante deve essere in formato JSON |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_ProtectionHandlerPublishingSettings_SetIsPublishingFormatJson(
    const mip_cc_protection_handler_publishing_settings settings,
    const bool isPublishingFormatJson);
```

## <a name="mip_cc_protectionhandlerpublishingsettings_setdelegateduseremail"></a>MIP_CC_ProtectionHandlerPublishingSettings_SetDelegatedUserEmail

Imposta l'utente delegato

**Parametri**

Parametro | Description
|---|---|
| impostazioni | Impostazioni del gestore protezione |
| delegatedUserEmail | Indirizzo di posta elettronica dell'utente delegato |

**Return**: codice risultato che indica l'esito positivo o negativo

**Nota**: un utente delegato viene specificato quando l'utente o l'applicazione di autenticazione agisce per conto di un altro utente 

```c
mip_cc_result MIP_CC_ProtectionHandlerPublishingSettings_SetDelegatedUserEmail(
    const mip_cc_protection_handler_publishing_settings settings,
    const char* delegatedUserEmail);
```

## <a name="mip_cc_createprotectionhandlerconsumptionsettings"></a>MIP_CC_CreateProtectionHandlerConsumptionSettings

Creare un oggetto impostazioni utilizzato per creare un gestore protezione per l'utilizzo del contenuto esistente

**Parametri**

Parametro | Description
|---|---|
| publishingLicenseBuffer | Buffer contenente la licenza di pubblicazione non elaborata |
| publishingLicenseBufferSize | Dimensioni del buffer delle licenze di pubblicazione |
| isOfflineOnly | Se è consentito il recupero di una nuova licenza dal server RMS |
| delegatedUserEmail | Opzionale Utente per conto del quale verranno eseguite le operazioni di protezione |
| impostazioni | Output Istanza di impostazioni appena creata |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_CreateProtectionHandlerConsumptionSettings(
    const uint8_t* publishingLicenseBuffer,
    const int64_t publishingLicenseBufferSize,
    mip_cc_protection_handler_consumption_settings* settings);
```

## <a name="mip_cc_protectionhandlerconsumptionsettings_setisofflineonly"></a>MIP_CC_ProtectionHandlerConsumptionSettings_SetIsOfflineOnly

Imposta un valore che indica se la creazione del gestore protezione consente operazioni HTTP online

**Parametri**

Parametro | Description
|---|---|
| impostazioni | Impostazioni del gestore protezione |
| isOfflineOnly | True se le operazioni HTTP sono proibite, altrimenti false |

**Return**: codice risultato che indica l'esito positivo o negativo

**Nota**: se questa proprietà è impostata su true, la creazione del gestore protezione avrà esito positivo solo se il contenuto è già stato precedentemente decrittografato e la relativa licenza non è scaduta. Se il contenuto memorizzato nella cache non viene trovato, verrà restituito un risultato MIP_RESULT_ERROR_NETWORK. 

```c
mip_cc_result MIP_CC_ProtectionHandlerConsumptionSettings_SetIsOfflineOnly(
    const mip_cc_protection_handler_consumption_settings settings,
    const bool isOfflineOnly);
```

## <a name="mip_cc_protectionhandlerconsumptionsettings_setdelegateduseremail"></a>MIP_CC_ProtectionHandlerConsumptionSettings_SetDelegatedUserEmail

Imposta l'utente delegato

**Parametri**

Parametro | Description
|---|---|
| impostazioni | Impostazioni del gestore protezione |
| delegatedUserEmail | Indirizzo di posta elettronica dell'utente delegato |

**Return**: codice risultato che indica l'esito positivo o negativo

**Nota**: un utente delegato viene specificato quando l'utente o l'applicazione di autenticazione agisce per conto di un altro utente 

```c
mip_cc_result MIP_CC_ProtectionHandlerConsumptionSettings_SetDelegatedUserEmail(
    const mip_cc_protection_handler_consumption_settings settings,
    const char* delegatedUserEmail);
```

## <a name="mip_cc_protectionhandler_getserializedpublishinglicensesize"></a>MIP_CC_ProtectionHandler_GetSerializedPublishingLicenseSize

Ottiene le dimensioni della licenza di pubblicazione (in byte)

**Parametri**

Parametro | Description
|---|---|
| Gestore | Gestore che rappresenta il contenuto protetto |
| publishingLicenseBufferSize | Output Dimensioni della licenza di pubblicazione (in byte) |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_ProtectionHandler_GetSerializedPublishingLicenseSize(
    const mip_cc_protection_handler handler,
    int64_t* publishingLicenseBufferSize);
```

## <a name="mip_cc_protectionhandler_getserializedpublishinglicense"></a>MIP_CC_ProtectionHandler_GetSerializedPublishingLicense

Ottiene la licenza di pubblicazione

**Parametri**

Parametro | Description
|---|---|
| Gestore | Gestore che rappresenta il contenuto protetto |
| publishingLicenseBuffer | Output Buffer in cui verrà scritta la licenza di pubblicazione |
| publishingLicenseBufferSize | Dimensioni del buffer delle licenze di pubblicazione |
| actualPublishingLicenseSize | Output Dimensioni effettive della licenza di pubblicazione (in byte) |

**Return**: codice risultato che indica l'esito positivo o negativo

**Nota**: se publishingLicenseBuffer è null o insufficiente, viene restituito MIP_RESULT_ERROR_INSUFFICIENT_BUFFER e actualPublishingLicenseSize viene impostato sulle dimensioni minime del buffer richiesto. 

```c
mip_cc_result MIP_CC_ProtectionHandler_GetSerializedPublishingLicense(
    const mip_cc_protection_handler handler,
    uint8_t* publishingLicenseBuffer,
    const int64_t publishingLicenseBufferSize,
    int64_t* actualPublishingLicenseSize);
```

## <a name="mip_cc_protectionhandler_getprotectiondescriptor"></a>MIP_CC_ProtectionHandler_GetProtectionDescriptor

Ottiene il descrittore di protezione

**Parametri**

Parametro | Description
|---|---|
| Gestore | Gestore che rappresenta il contenuto protetto |
| descrittore | Output Descrittore di protezione |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_ProtectionHandler_GetProtectionDescriptor(
    const mip_cc_protection_handler handler,
    mip_cc_protection_descriptor* descriptor);
```

## <a name="mip_cc_protectionhandler_getrights"></a>MIP_CC_ProtectionHandler_GetRights

Ottiene l'elenco dei diritti concessi a un utente

**Parametri**

Parametro | Description
|---|---|
| Gestore | Gestore che rappresenta il contenuto protetto |
| diritti | Output Elenco dei diritti concessi a un utente, memoria di proprietà del chiamante |

**Return**: codice risultato che indica l'esito positivo o negativo

**Nota**: la variabile ' Rights ' deve essere rilasciata dal chiamante chiamando MIP_CC_ReleaseStringList 

```c
mip_cc_result MIP_CC_ProtectionHandler_GetRights(
    const mip_cc_protection_handler handler,
    mip_cc_string_list* rights);
```

## <a name="mip_cc_protectionhandler_getprotectedcontentsize"></a>MIP_CC_ProtectionHandler_GetProtectedContentSize

Calcola le dimensioni del contenuto protetto, il factoring nella spaziatura interna e così via.

**Parametri**

Parametro | Description
|---|---|
| Gestore | Gestore che rappresenta il contenuto protetto |
| unprotectedSize | Dimensioni del contenuto non protetto/non crittografato (in byte) |
| includesFinalBlock | Descrive se il contenuto non protetto in questione include il blocco finale o meno. |
| protectedSize | Output Dimensioni del contenuto protetto |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_ProtectionHandler_GetProtectedContentSize(
    const mip_cc_protection_handler handler,
    const int64_t unprotectedSize,
    const bool includesFinalBlock,
    int64_t* protectedSize);
```

## <a name="mip_cc_protectionhandler_getblocksize"></a>MIP_CC_ProtectionHandler_GetBlockSize

Ottiene la dimensione del blocco (in byte) per la modalità di crittografia utilizzata da un gestore di protezione.

**Parametri**

Parametro | Description
|---|---|
| Gestore | Gestore che rappresenta il contenuto protetto |
| blockSize | Output Dimensioni blocco (in byte) |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_ProtectionHandler_GetBlockSize(
    const mip_cc_protection_handler handler,
    int64_t* blockSize);
```

## <a name="mip_cc_protectionhandler_getissuedusersize"></a>MIP_CC_ProtectionHandler_GetIssuedUserSize

Ottiene le dimensioni del buffer necessarie per archiviare l'utente a cui è stato concesso l'accesso al contenuto protetto

**Parametri**

Parametro | Description
|---|---|
| Gestore | Gestore che rappresenta il contenuto protetto |
| issuedUserSize | Output Dimensioni del buffer per l'utente rilasciato (in numero di caratteri) |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_ProtectionHandler_GetIssuedUserSize(
    const mip_cc_protection_handler handler,
    int64_t* issuedUserSize);
```

## <a name="mip_cc_protectionhandler_getissueduser"></a>MIP_CC_ProtectionHandler_GetIssuedUser

Ottiene l'utente a cui è stato concesso l'accesso al contenuto protetto

**Parametri**

Parametro | Description
|---|---|
| Gestore | Gestore che rappresenta il contenuto protetto |
| issuedUserBuffer | Output Buffer in cui verrà copiato l'utente emesso. |
| issuedUserBufferSize | Dimensioni (in numero di caratteri) di issuedUserBuffer. |
| actualIssuedUserSize | Output Numero di caratteri scritti nel buffer |

**Return**: codice risultato che indica l'esito positivo o negativo

**Nota**: se issuedUserBuffer è null o insufficiente, viene restituito MIP_RESULT_ERROR_INSUFFICIENT_BUFFER e actualIssuedUserSize viene impostato sulle dimensioni minime del buffer richiesto. 

```c
mip_cc_result MIP_CC_ProtectionHandler_GetIssuedUser(
    const mip_cc_protection_handler handler,
    char* issuedUserBuffer,
    const int64_t issuedUserBufferSize,
    int64_t* actualIssuedUserSize);
```

## <a name="mip_cc_protectionhandler_getownersize"></a>MIP_CC_ProtectionHandler_GetOwnerSize

Ottiene le dimensioni del buffer necessarie per archiviare il proprietario del contenuto protetto

**Parametri**

Parametro | Description
|---|---|
| Gestore | Gestore che rappresenta il contenuto protetto |
| ownerSize | Output Dimensioni del buffer per l'utente rilasciato (in numero di caratteri) |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_ProtectionHandler_GetOwnerSize(
    const mip_cc_protection_handler handler,
    int64_t* ownerSize);
```

## <a name="mip_cc_protectionhandler_getowner"></a>MIP_CC_ProtectionHandler_GetOwner

Ottiene il proprietario del contenuto protetto

**Parametri**

Parametro | Description
|---|---|
| Gestore | Gestore che rappresenta il contenuto protetto |
| ownerBuffer | Output Buffer in cui verrà copiato l'utente emesso. |
| ownerBufferSize | Dimensioni (in numero di caratteri) di ownerBuffer. |
| actualOwnerSize | Output Numero di caratteri scritti nel buffer |

**Return**: codice risultato che indica l'esito positivo o negativo

**Nota**: se ownerBuffer è null o insufficiente, viene restituito MIP_RESULT_ERROR_INSUFFICIENT_BUFFER e actualOwnerSize viene impostato sulle dimensioni minime del buffer richiesto. 

```c
mip_cc_result MIP_CC_ProtectionHandler_GetOwner(
    const mip_cc_protection_handler handler,
    char* ownerBuffer,
    const int64_t ownerBufferSize,
    int64_t* actualOwnerSize);
```

## <a name="mip_cc_protectionhandler_getcontentid"></a>MIP_CC_ProtectionHandler_GetContentId

Ottiene il contenuto di IE del contenuto protetto

**Parametri**

Parametro | Description
|---|---|
| Gestore | Gestore che rappresenta il contenuto protetto |
| contentId | Output ID contenuto |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_ProtectionHandler_GetContentId(
    const mip_cc_protection_handler handler,
    mip_cc_guid* contentId);
```

## <a name="mip_cc_protectionhandler_doesusedeprecatedalgorithm"></a>MIP_CC_ProtectionHandler_DoesUseDeprecatedAlgorithm

Ottiene un valore che indica se il gestore della protezione utilizza un algoritmo di crittografia deprecato (BCE) per la compatibilità con le versioni precedenti

**Parametri**

Parametro | Description
|---|---|
| Gestore | Gestore che rappresenta il contenuto protetto |
| doesUseDeprecatedAlgorithm | Output Indica se il gestore della protezione usa un algoritmo di crittografia deprecato |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_ProtectionHandler_DoesUseDeprecatedAlgorithm(
    const mip_cc_protection_handler handler,
    bool* doesUseDeprecatedAlgorithm);
```

## <a name="mip_cc_protectionhandler_decryptbuffer"></a>MIP_CC_ProtectionHandler_DecryptBuffer

Decrittografare un buffer

**Parametri**

Parametro | Description
|---|---|
| offsetFromStart | Posizione relativa di inputBuffer dall'inizio del contenuto crittografato |
| inputBuffer | Buffer di contenuto crittografato che verrà decrittografato |
| inputBufferSize | Dimensioni (in byte) del buffer di input |
| outputBuffer | Output Buffer in cui verrà copiato il contenuto decrittografato |
| outputBufferSize | Dimensioni (in byte) del buffer di output |
| documentoÈ | Se il buffer di input contiene i byte crittografati finali |
| actualDecryptedSize | Output Dimensioni effettive del contenuto crittografato (in byte) |

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
    int64_t *actualDecryptedSize);
```

## <a name="mip_cc_releaseprotectionhandlerpublishingsettings"></a>MIP_CC_ReleaseProtectionHandlerPublishingSettings

Rilasciare le risorse associate a impostazioni del gestore protezione

**Parametri**

Parametro | Description
|---|---|
| impostazioni | Impostazioni del gestore di protezione da rilasciare |

```c
void MIP_CC_ReleaseProtectionHandlerPublishingSettings(mip_cc_protection_handler_publishing_settings settings);
```

## <a name="mip_cc_releaseprotectionhandlerconsumptionsettings"></a>MIP_CC_ReleaseProtectionHandlerConsumptionSettings

Rilasciare le risorse associate a impostazioni del gestore protezione

**Parametri**

Parametro | Description
|---|---|
| impostazioni | Impostazioni del gestore di protezione da rilasciare |

```c
void MIP_CC_ReleaseProtectionHandlerConsumptionSettings(mip_cc_protection_handler_consumption_settings settings);
```

## <a name="mip_cc_releaseprotectionhandler"></a>MIP_CC_ReleaseProtectionHandler

Rilasciare le risorse associate a un gestore protezione

**Parametri**

Parametro | Description
|---|---|
| Gestore | Gestore di protezione da rilasciare |

```c
void MIP_CC_ReleaseProtectionHandler(mip_cc_protection_handler handler);
```

## <a name="mip_cc_loadprotectionprofile"></a>MIP_CC_LoadProtectionProfile

Carica un profilo

**Parametri**

Parametro | Description
|---|---|
| impostazioni | Impostazioni profilo |
| Profilo | Output Istanza del profilo di protezione appena creata |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_LoadProtectionProfile(
    const mip_cc_protection_profile_settings settings,
    mip_cc_protection_profile* profile);
```

## <a name="mip_cc_releaseprotectionprofile"></a>MIP_CC_ReleaseProtectionProfile

Rilascia le risorse associate a un profilo di protezione

**Parametri**

Parametro | Description
|---|---|
| Profilo | Profilo di protezione da rilasciare |

```c
void MIP_CC_ReleaseProtectionProfile(mip_cc_protection_profile profile);
```

## <a name="mip_cc_protectionprofilesettings_setsessionid"></a>MIP_CC_ProtectionProfileSettings_SetSessionId

Imposta l'ID di sessione che può essere usato per correlare i log e i dati di telemetria

**Parametri**

Parametro | Description
|---|---|
| impostazioni | Impostazioni profilo |
| sessionId | ID sessione che rappresenta la durata di un profilo di protezione |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_ProtectionProfileSettings_SetSessionId(
    const mip_cc_protection_profile_settings settings,
    const char* sessionId);
```

## <a name="mip_cc_protectionprofilesettings_setcancachelicenses"></a>MIP_CC_ProtectionProfileSettings_SetCanCacheLicenses

Configura se le licenze dell'utente finale (contratti) verranno memorizzate nella cache localmente

**Parametri**

Parametro | Description
|---|---|
| impostazioni | Impostazioni profilo |
| canCacheLicenses | Indica se il motore deve memorizzare nella cache una licenza quando apre il contenuto protetto |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_ProtectionProfileSettings_SetCanCacheLicenses(
    const mip_cc_protection_profile_settings settings,
    const bool canCacheLicenses);
```

## <a name="mip_cc_protectionprofilesettings_sethttpdelegate"></a>MIP_CC_ProtectionProfileSettings_SetHttpDelegate

Esegui override dello stack HTTP predefinito con il proprio client

**Parametri**

Parametro | Description
|---|---|
| impostazioni | Impostazioni del profilo a cui verrà assegnato il delegato HTTP |
| httpDelegate | Istanza di callback HTTP implementata dall'applicazione client |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_ProtectionProfileSettings_SetHttpDelegate(
    const mip_cc_protection_profile_settings settings,
    const mip_cc_http_delegate httpDelegate);
```

## <a name="mip_cc_protectionprofilesettings_settaskdispatcherdelegate"></a>MIP_CC_ProtectionProfileSettings_SetTaskDispatcherDelegate

Esegui override del dispatcher attività asincrono predefinito con il proprio client

**Parametri**

Parametro | Description
|---|---|
| impostazioni | Impostazioni del profilo a cui verrà assegnato il delegato del dispatcher attività |
| taskDispatcherDelegate | Istanza di callback Dispatcher attività implementata dall'applicazione client |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_ProtectionProfileSettings_SetTaskDispatcherDelegate(
    const mip_cc_protection_profile_settings settings,
    const mip_cc_task_dispatcher_delegate taskDispatcherDelegate);
```

## <a name="mip_cc_protectionprofilesettings_setcustomsettings"></a>MIP_CC_ProtectionProfileSettings_SetCustomSettings

Configura le impostazioni personalizzate, usate per il controllo e il controllo delle funzionalità.

**Parametri**

Parametro | Description
|---|---|
| impostazioni | Impostazioni profilo |
| customSettings | Coppie chiave/valore di impostazioni personalizzate |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_ProtectionProfileSettings_SetCustomSettings(
    const mip_cc_protection_profile_settings settings,
    const mip_cc_dictionary customSettings);
```

## <a name="mip_cc_releaseprotectionprofilesettings"></a>MIP_CC_ReleaseProtectionProfileSettings

Rilascia le risorse associate a impostazioni del profilo di protezione

**Parametri**

Parametro | Description
|---|---|
| impostazioni | Impostazioni del profilo di protezione da rilasciare |

```c
void MIP_CC_ReleaseProtectionProfileSettings(mip_cc_protection_profile_settings profilsettingseSettings);
```

## <a name="mip_cc_action_gettype"></a>MIP_CC_Action_GetType

Ottiene il tipo di un'azione

**Parametri**

Parametro | Description
|---|---|
| action | Azione |
| actionType | Output Tipo di azione |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_Action_GetType(
    const mip_cc_action action,
    mip_cc_action_type* actionType);
```

## <a name="mip_cc_action_getid"></a>MIP_CC_Action_GetId

Ottiene l'ID di un'azione

**Parametri**

Parametro | Description
|---|---|
| action | Azione |
| ID | Output ID azione univoco |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_Action_GetId(
    const mip_cc_action action,
    mip_cc_guid* id);
```

## <a name="mip_cc_actionresult_getactions"></a>MIP_CC_ActionResult_GetActions

Ottenere azioni che compongono il risultato di un'azione

**Parametri**

Parametro | Description
|---|---|
| actionResult | Risultato dell'azione di origine |
| Azioni | Output Matrice di azioni, memoria di proprietà dell'oggetto mip_cc_action_result |
| count | Output Numero di coppie chiave/valore |

**Return**: codice risultato che indica l'esito positivo o negativo

**Nota**: la memoria per ' actions ' è di proprietà dell'oggetto mip_cc_action_result, quindi non deve essere liberata in modo indipendente 

```c
mip_cc_result MIP_CC_ActionResult_GetActions(
    const mip_cc_action_result actionResult,
    mip_cc_action** actions,
    int64_t* count);
```

## <a name="mip_cc_releaseactionresult"></a>MIP_CC_ReleaseActionResult

Rilasciare le risorse associate al risultato di un'azione

**Parametri**

Parametro | Description
|---|---|
| actionResult | Risultato dell'azione da rilasciare |

```c
void MIP_CC_ReleaseActionResult(mip_cc_action_result actionResult);
```

## <a name="mip_cc_addcontentfooteraction_getuielementnamesize"></a>MIP_CC_AddContentFooterAction_GetUIElementNameSize

Ottiene le dimensioni del buffer necessarie per archiviare il nome dell'elemento dell'interfaccia utente dell'azione "Aggiungi piè di pagina contenuto"

**Parametri**

Parametro | Description
|---|---|
| action | azione "Aggiungi piè di pagina contenuto" |
| nameSize | Output Dimensione del buffer in cui memorizzare il nome dell'elemento dell'interfaccia utente (in numero di caratteri) |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_AddContentFooterAction_GetUIElementNameSize(
    const mip_cc_action action,
    int64_t* nameSize);
```

## <a name="mip_cc_addcontentfooteraction_getuielementname"></a>MIP_CC_AddContentFooterAction_GetUIElementName

Ottiene il nome dell'elemento dell'interfaccia utente dell'azione "Aggiungi piè di pagina contenuto"

**Parametri**

Parametro | Description
|---|---|
| action | azione "Aggiungi piè di pagina contenuto" |
| nameBuffer | Output Buffer in cui verrà copiato il nome dell'elemento dell'interfaccia utente. |
| nameBufferSize | Dimensioni (in numero di caratteri) di nameBuffer. |
| actualNameSize | Output Numero di caratteri scritti nel buffer |

**Return**: codice risultato che indica l'esito positivo o negativo

**Nota**: se nameBuffer è null o insufficiente, viene restituito MIP_RESULT_ERROR_INSUFFICIENT_BUFFER e actualNameSize viene impostato sulle dimensioni minime del buffer richiesto. 

```c
mip_cc_result MIP_CC_AddContentFooterAction_GetUIElementName(
    const mip_cc_action action,
    char* nameBuffer,
    const int64_t nameBufferSize,
    int64_t* actualNameSize);
```

## <a name="mip_cc_addcontentfooteraction_gettextsize"></a>MIP_CC_AddContentFooterAction_GetTextSize

Ottiene le dimensioni del buffer necessarie per archiviare un testo dell'azione "Aggiungi piè di pagina contenuto"

**Parametri**

Parametro | Description
|---|---|
| action | azione "Aggiungi piè di pagina contenuto" |
| nameSize | Output Dimensioni del buffer per il mantenimento del testo (in numero di caratteri) |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_AddContentFooterAction_GetTextSize(
    const mip_cc_action action,
    int64_t* textSize);
```

## <a name="mip_cc_addcontentfooteraction_gettext"></a>MIP_CC_AddContentFooterAction_GetText

Ottiene il testo dell'azione "Aggiungi piè di pagina contenuto"

**Parametri**

Parametro | Description
|---|---|
| action | azione "Aggiungi piè di pagina contenuto" |
| textBuffer | Output Buffer in cui verrà copiato il testo. |
| textBufferSize | Dimensioni (in numero di caratteri) di textBuffer. |
| actualTextSize | Output Numero di caratteri scritti nel buffer |

**Return**: codice risultato che indica l'esito positivo o negativo

**Nota**: se TextBuffer è null o insufficiente, viene restituito MIP_RESULT_ERROR_INSUFFICIENT_BUFFER e actualTextSize viene impostato sulle dimensioni minime del buffer richiesto. 

```c
mip_cc_result MIP_CC_AddContentFooterAction_GetText(
    const mip_cc_action action,
    char* textBuffer,
    const int64_t textBufferSize,
    int64_t* actualTextSize);
```

## <a name="mip_cc_addcontentfooteraction_getfontnamesize"></a>MIP_CC_AddContentFooterAction_GetFontNameSize

Ottiene le dimensioni del buffer necessarie per archiviare il nome del tipo di carattere dell'azione "Aggiungi piè di pagina contenuto"

**Parametri**

Parametro | Description
|---|---|
| action | azione "Aggiungi piè di pagina contenuto" |
| nameSize | Output Dimensione del buffer in cui memorizzare il nome del tipo di carattere (in numero di caratteri) |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_AddContentFooterAction_GetFontNameSize(
    const mip_cc_action action,
    int64_t* nameSize);
```

## <a name="mip_cc_addcontentfooteraction_getfontname"></a>MIP_CC_AddContentFooterAction_GetFontName

Ottiene il nome del tipo di carattere dell'azione "Aggiungi piè di pagina contenuto"

**Parametri**

Parametro | Description
|---|---|
| action | azione "Aggiungi piè di pagina contenuto" |
| nameBuffer | Output Buffer in cui verrà copiato il nome del tipo di carattere. |
| nameBufferSize | Dimensioni (in numero di caratteri) di nameBuffer. |
| actualNameSize | Output Numero di caratteri scritti nel buffer |

**Return**: codice risultato che indica l'esito positivo o negativo

**Nota**: se nameBuffer è null o insufficiente, viene restituito MIP_RESULT_ERROR_INSUFFICIENT_BUFFER e actualNameSize viene impostato sulle dimensioni minime del buffer richiesto. 

```c
mip_cc_result MIP_CC_AddContentFooterAction_GetFontName(
    const mip_cc_action action,
    char* nameBuffer,
    const int64_t nameBufferSize,
    int64_t* actualNameSize);
```

## <a name="mip_cc_addcontentfooteraction_getfontsize"></a>MIP_CC_AddContentFooterAction_GetFontSize

Ottiene le dimensioni del carattere Integer

**Parametri**

Parametro | Description
|---|---|
| action | azione "Aggiungi piè di pagina contenuto" |
| FontSize | Output Dimensioni carattere |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_AddContentFooterAction_GetFontSize(
    const mip_cc_action action,
    int32_t* fontSize);
```

## <a name="mip_cc_addcontentfooteraction_getfontcolorsize"></a>MIP_CC_AddContentFooterAction_GetFontColorSize

Ottiene le dimensioni del buffer necessarie per archiviare il colore del carattere dell'azione "Aggiungi piè di pagina contenuto"

**Parametri**

Parametro | Description
|---|---|
| action | azione "Aggiungi piè di pagina contenuto" |
| colorSize | Output Dimensioni del buffer per mantenere il colore del carattere (in numero di caratteri) |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_AddContentFooterAction_GetFontColorSize(
    const mip_cc_action action,
    int64_t* colorSize);
```

## <a name="mip_cc_addcontentfooteraction_getfontcolor"></a>MIP_CC_AddContentFooterAction_GetFontColor

Ottiene il colore del carattere dell'azione "Aggiungi piè di pagina contenuto" (ad esempio, "#000000")

**Parametri**

Parametro | Description
|---|---|
| action | azione "Aggiungi piè di pagina contenuto" |
| colorBuffer | Output Buffer in cui verrà copiato il colore del carattere. |
| colorBufferSize | Dimensioni (in numero di caratteri) di colorBuffer. |
| actualColorSize | Output Numero di caratteri scritti nel buffer |

**Return**: codice risultato che indica l'esito positivo o negativo

**Nota**: se colorBuffer è null o insufficiente, viene restituito MIP_RESULT_ERROR_INSUFFICIENT_BUFFER e actualColorSize viene impostato sulle dimensioni minime del buffer richiesto. 

```c
mip_cc_result MIP_CC_AddContentFooterAction_GetFontColor(
    const mip_cc_action action,
    char* colorBuffer,
    const int64_t colorBufferSize,
    int64_t* actualColorSize);
```

## <a name="mip_cc_addcontentfooteraction_getalignment"></a>MIP_CC_AddContentFooterAction_GetAlignment

Ottiene l'allineamento

**Parametri**

Parametro | Description
|---|---|
| action | azione "Aggiungi piè di pagina contenuto" |
| Allineamento | Output Allineamento |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_AddContentFooterAction_GetAlignment(
    const mip_cc_action action,
    mip_cc_content_mark_alignment* alignment);
```

## <a name="mip_cc_addcontentfooteraction_getmargin"></a>MIP_CC_AddContentFooterAction_GetMargin

Ottiene le dimensioni del margine

**Parametri**

Parametro | Description
|---|---|
| action | azione "Aggiungi piè di pagina contenuto" |
| marginSize | Output Dimensioni margine (in mm) |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_AddContentFooterAction_GetMargin(
    const mip_cc_action action,
    int32_t* marginSize);
```

## <a name="mip_cc_addcontentheaderaction_getuielementnamesize"></a>MIP_CC_AddContentHeaderAction_GetUIElementNameSize

Ottiene le dimensioni del buffer necessarie per archiviare il nome dell'elemento dell'interfaccia utente dell'azione "Aggiungi intestazione contenuto"

**Parametri**

Parametro | Description
|---|---|
| action | azione "Aggiungi intestazione contenuto" |
| nameSize | Output Dimensione del buffer in cui memorizzare il nome dell'elemento dell'interfaccia utente (in numero di caratteri) |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_AddContentHeaderAction_GetUIElementNameSize(
    const mip_cc_action action,
    int64_t* nameSize);
```

## <a name="mip_cc_addcontentheaderaction_getuielementname"></a>MIP_CC_AddContentHeaderAction_GetUIElementName

Ottiene il nome dell'elemento dell'interfaccia utente dell'azione "Aggiungi intestazione contenuto"

**Parametri**

Parametro | Description
|---|---|
| action | azione "Aggiungi intestazione contenuto" |
| nameBuffer | Output Buffer in cui verrà copiato il nome dell'elemento dell'interfaccia utente. |
| nameBufferSize | Dimensioni (in numero di caratteri) di nameBuffer. |
| actualNameSize | Output Numero di caratteri scritti nel buffer |

**Return**: codice risultato che indica l'esito positivo o negativo

**Nota**: se nameBuffer è null o insufficiente, viene restituito MIP_RESULT_ERROR_INSUFFICIENT_BUFFER e actualNameSize viene impostato sulle dimensioni minime del buffer richiesto. 

```c
mip_cc_result MIP_CC_AddContentHeaderAction_GetUIElementName(
    const mip_cc_action action,
    char* nameBuffer,
    const int64_t nameBufferSize,
    int64_t* actualNameSize);
```

## <a name="mip_cc_addcontentheaderaction_gettextsize"></a>MIP_CC_AddContentHeaderAction_GetTextSize

Ottiene le dimensioni del buffer necessarie per archiviare il testo dell'azione "Aggiungi intestazione contenuto"

**Parametri**

Parametro | Description
|---|---|
| action | azione "Aggiungi intestazione contenuto" |
| nameSize | Output Dimensioni del buffer per il mantenimento del testo (in numero di caratteri) |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_AddContentHeaderAction_GetTextSize(
    const mip_cc_action action,
    int64_t* textSize);
```

## <a name="mip_cc_addcontentheaderaction_gettext"></a>MIP_CC_AddContentHeaderAction_GetText

Ottiene il testo dell'azione "Aggiungi intestazione contenuto"

**Parametri**

Parametro | Description
|---|---|
| action | azione "Aggiungi intestazione contenuto" |
| textBuffer | Output Buffer in cui verrà copiato il testo. |
| textBufferSize | Dimensioni (in numero di caratteri) di textBuffer. |
| actualTextSize | Output Numero di caratteri scritti nel buffer |

**Return**: codice risultato che indica l'esito positivo o negativo

**Nota**: se TextBuffer è null o insufficiente, viene restituito MIP_RESULT_ERROR_INSUFFICIENT_BUFFER e actualTextSize viene impostato sulle dimensioni minime del buffer richiesto. 

```c
mip_cc_result MIP_CC_AddContentHeaderAction_GetText(
    const mip_cc_action action,
    char* textBuffer,
    const int64_t textBufferSize,
    int64_t* actualTextSize);
```

## <a name="mip_cc_addcontentheaderaction_getfontnamesize"></a>MIP_CC_AddContentHeaderAction_GetFontNameSize

Ottiene le dimensioni del buffer necessarie per archiviare il nome del tipo di carattere dell'azione "Aggiungi intestazione contenuto"

**Parametri**

Parametro | Description
|---|---|
| action | azione "Aggiungi intestazione contenuto" |
| nameSize | Output Dimensione del buffer in cui memorizzare il nome del tipo di carattere (in numero di caratteri) |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_AddContentHeaderAction_GetFontNameSize(
    const mip_cc_action action,
    int64_t* nameSize);
```

## <a name="mip_cc_addcontentheaderaction_getfontname"></a>MIP_CC_AddContentHeaderAction_GetFontName

Ottiene il nome del tipo di carattere dell'azione "Aggiungi intestazione contenuto"

**Parametri**

Parametro | Description
|---|---|
| action | azione "Aggiungi intestazione contenuto" |
| nameBuffer | Output Buffer in cui verrà copiato il nome del tipo di carattere. |
| nameBufferSize | Dimensioni (in numero di caratteri) di nameBuffer. |
| actualNameSize | Output Numero di caratteri scritti nel buffer |

**Return**: codice risultato che indica l'esito positivo o negativo

**Nota**: se nameBuffer è null o insufficiente, viene restituito MIP_RESULT_ERROR_INSUFFICIENT_BUFFER e actualNameSize viene impostato sulle dimensioni minime del buffer richiesto. 

```c
mip_cc_result MIP_CC_AddContentHeaderAction_GetFontName(
    const mip_cc_action action,
    char* nameBuffer,
    const int64_t nameBufferSize,
    int64_t* actualNameSize);
```

## <a name="mip_cc_addcontentheaderaction_getfontsize"></a>MIP_CC_AddContentHeaderAction_GetFontSize

Ottiene le dimensioni del carattere Integer

**Parametri**

Parametro | Description
|---|---|
| action | azione "Aggiungi intestazione contenuto" |
| FontSize | Output Dimensioni carattere |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_AddContentHeaderAction_GetFontSize(
    const mip_cc_action action,
    int32_t* fontSize);
```

## <a name="mip_cc_addcontentheaderaction_getfontcolorsize"></a>MIP_CC_AddContentHeaderAction_GetFontColorSize

Ottiene le dimensioni del buffer necessarie per archiviare il colore del carattere dell'azione "Aggiungi intestazione contenuto"

**Parametri**

Parametro | Description
|---|---|
| action | azione "Aggiungi intestazione contenuto" |
| colorSize | Output Dimensioni del buffer per mantenere il colore del carattere (in numero di caratteri) |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_AddContentHeaderAction_GetFontColorSize(
    const mip_cc_action action,
    int64_t* colorSize);
```

## <a name="mip_cc_addcontentheaderaction_getfontcolor"></a>MIP_CC_AddContentHeaderAction_GetFontColor

Ottiene il colore del carattere dell'azione "Aggiungi intestazione contenuto", ad esempio "#000000".

**Parametri**

Parametro | Description
|---|---|
| action | azione "Aggiungi intestazione contenuto" |
| colorBuffer | Output Buffer in cui verrà copiato il colore del carattere. |
| colorBufferSize | Dimensioni (in numero di caratteri) di colorBuffer. |
| actualColorSize | Output Numero di caratteri scritti nel buffer |

**Return**: codice risultato che indica l'esito positivo o negativo

**Nota**: se colorBuffer è null o insufficiente, viene restituito MIP_RESULT_ERROR_INSUFFICIENT_BUFFER e actualColorSize viene impostato sulle dimensioni minime del buffer richiesto. 

```c
mip_cc_result MIP_CC_AddContentHeaderAction_GetFontColor(
    const mip_cc_action action,
    char* colorBuffer,
    const int64_t colorBufferSize,
    int64_t* actualColorSize);
```

## <a name="mip_cc_addcontentheaderaction_getalignment"></a>MIP_CC_AddContentHeaderAction_GetAlignment

Ottiene l'allineamento

**Parametri**

Parametro | Description
|---|---|
| action | azione "Aggiungi intestazione contenuto" |
| Allineamento | Output Allineamento |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_AddContentHeaderAction_GetAlignment(
    const mip_cc_action action,
    mip_cc_content_mark_alignment* alignment);
```

## <a name="mip_cc_addcontentheaderaction_getmargin"></a>MIP_CC_AddContentHeaderAction_GetMargin

Ottiene le dimensioni del margine

**Parametri**

Parametro | Description
|---|---|
| action | azione "Aggiungi intestazione contenuto" |
| marginSize | Output Dimensioni margine (in mm) |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_AddContentHeaderAction_GetMargin(
    const mip_cc_action action,
    int32_t* marginSize);
```

## <a name="mip_cc_addwatermarkaction_getuielementnamesize"></a>MIP_CC_AddWatermarkAction_GetUIElementNameSize

Ottiene le dimensioni del buffer necessarie per archiviare il nome dell'elemento dell'interfaccia utente dell'azione "add watermark"

**Parametri**

Parametro | Description
|---|---|
| action | azione "Aggiungi filigrana" |
| nameSize | Output Dimensione del buffer in cui memorizzare il nome dell'elemento dell'interfaccia utente (in numero di caratteri) |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_AddWatermarkAction_GetUIElementNameSize(
    const mip_cc_action action,
    int64_t* nameSize);
```

## <a name="mip_cc_addwatermarkaction_getuielementname"></a>MIP_CC_AddWatermarkAction_GetUIElementName

Ottiene il nome dell'elemento dell'interfaccia utente dell'azione "Aggiungi filigrana"

**Parametri**

Parametro | Description
|---|---|
| action | azione "Aggiungi filigrana" |
| nameBuffer | Output Buffer in cui verrà copiato il nome dell'elemento dell'interfaccia utente. |
| nameBufferSize | Dimensioni (in numero di caratteri) di nameBuffer. |
| actualNameSize | Output Numero di caratteri scritti nel buffer |

**Return**: codice risultato che indica l'esito positivo o negativo

**Nota**: se nameBuffer è null o insufficiente, viene restituito MIP_RESULT_ERROR_INSUFFICIENT_BUFFER e actualNameSize viene impostato sulle dimensioni minime del buffer richiesto. 

```c
mip_cc_result MIP_CC_AddWatermarkAction_GetUIElementName(
    const mip_cc_action action,
    char* nameBuffer,
    const int64_t nameBufferSize,
    int64_t* actualNameSize);
```

## <a name="mip_cc_addwatermarkaction_getlayout"></a>MIP_CC_AddWatermarkAction_GetLayout

Ottiene il layout della filigrana

**Parametri**

Parametro | Description
|---|---|
| action | azione "Aggiungi filigrana" |
| Layout | Output Layout filigrana |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_AddWatermarkAction_GetLayout(
    const mip_cc_action action,
    mip_cc_watermark_layout* layout);
```

## <a name="mip_cc_addwatermarkaction_gettextsize"></a>MIP_CC_AddWatermarkAction_GetTextSize

Ottiene le dimensioni del buffer necessarie per archiviare il testo dell'azione "Aggiungi filigrana"

**Parametri**

Parametro | Description
|---|---|
| action | azione "Aggiungi filigrana" |
| nameSize | Output Dimensioni del buffer per il mantenimento del testo (in numero di caratteri) |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_AddWatermarkAction_GetTextSize(
    const mip_cc_action action,
    int64_t* textSize);
```

## <a name="mip_cc_addwatermarkaction_gettext"></a>MIP_CC_AddWatermarkAction_GetText

Ottiene il testo dell'azione "Aggiungi filigrana"

**Parametri**

Parametro | Description
|---|---|
| action | azione "Aggiungi filigrana" |
| textBuffer | Output Buffer in cui verrà copiato il testo. |
| textBufferSize | Dimensioni (in numero di caratteri) di textBuffer. |
| actualTextSize | Output Numero di caratteri scritti nel buffer |

**Return**: codice risultato che indica l'esito positivo o negativo

**Nota**: se TextBuffer è null o insufficiente, viene restituito MIP_RESULT_ERROR_INSUFFICIENT_BUFFER e actualTextSize viene impostato sulle dimensioni minime del buffer richiesto. 

```c
mip_cc_result MIP_CC_AddWatermarkAction_GetText(
    const mip_cc_action action,
    char* textBuffer,
    const int64_t textBufferSize,
    int64_t* actualTextSize);
```

## <a name="mip_cc_addwatermarkaction_getfontnamesize"></a>MIP_CC_AddWatermarkAction_GetFontNameSize

Ottiene le dimensioni del buffer necessarie per archiviare il nome del tipo di carattere dell'azione "Aggiungi filigrana"

**Parametri**

Parametro | Description
|---|---|
| action | azione "Aggiungi filigrana" |
| nameSize | Output Dimensione del buffer in cui memorizzare il nome del tipo di carattere (in numero di caratteri) |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_AddWatermarkAction_GetFontNameSize(
    const mip_cc_action action,
    int64_t* nameSize);
```

## <a name="mip_cc_addwatermarkaction_getfontname"></a>MIP_CC_AddWatermarkAction_GetFontName

Ottiene il nome del tipo di carattere dell'azione "Aggiungi filigrana"

**Parametri**

Parametro | Description
|---|---|
| action | azione "Aggiungi filigrana" |
| nameBuffer | Output Buffer in cui verrà copiato il nome del tipo di carattere. |
| nameBufferSize | Dimensioni (in numero di caratteri) di nameBuffer. |
| actualNameSize | Output Numero di caratteri scritti nel buffer |

**Return**: codice risultato che indica l'esito positivo o negativo

**Nota**: se nameBuffer è null o insufficiente, viene restituito MIP_RESULT_ERROR_INSUFFICIENT_BUFFER e actualNameSize viene impostato sulle dimensioni minime del buffer richiesto. 

```c
mip_cc_result MIP_CC_AddWatermarkAction_GetFontName(
    const mip_cc_action action,
    char* nameBuffer,
    const int64_t nameBufferSize,
    int64_t* actualNameSize);
```

## <a name="mip_cc_addwatermarkaction_getfontsize"></a>MIP_CC_AddWatermarkAction_GetFontSize

Ottiene le dimensioni del carattere Integer

**Parametri**

Parametro | Description
|---|---|
| action | azione "Aggiungi filigrana" |
| FontSize | Output Dimensioni carattere |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_AddWatermarkAction_GetFontSize(
    const mip_cc_action action,
    int32_t* fontSize);
```

## <a name="mip_cc_addwatermarkaction_getfontcolorsize"></a>MIP_CC_AddWatermarkAction_GetFontColorSize

Ottiene le dimensioni del buffer necessarie per archiviare il colore del carattere dell'azione "Aggiungi filigrana"

**Parametri**

Parametro | Description
|---|---|
| action | azione "Aggiungi filigrana" |
| colorSize | Output Dimensioni del buffer per mantenere il colore del carattere (in numero di caratteri) |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_AddWatermarkAction_GetFontColorSize(
    const mip_cc_action action,
    int64_t* colorSize);
```

## <a name="mip_cc_addwatermarkaction_getfontcolor"></a>MIP_CC_AddWatermarkAction_GetFontColor

Ottiene il colore del carattere dell'azione "Aggiungi filigrana" (ad esempio, "#000000")

**Parametri**

Parametro | Description
|---|---|
| action | azione "Aggiungi filigrana" |
| colorBuffer | Output Buffer in cui verrà copiato il colore del carattere. |
| colorBufferSize | Dimensioni (in numero di caratteri) di colorBuffer. |
| actualColorSize | Output Numero di caratteri scritti nel buffer |

**Return**: codice risultato che indica l'esito positivo o negativo

**Nota**: se colorBuffer è null o insufficiente, viene restituito MIP_RESULT_ERROR_INSUFFICIENT_BUFFER e actualColorSize viene impostato sulle dimensioni minime del buffer richiesto. 

```c
mip_cc_result MIP_CC_AddWatermarkAction_GetFontColor(
    const mip_cc_action action,
    char* colorBuffer,
    const int64_t colorBufferSize,
    int64_t* actualColorSize);
```

## <a name="mip_cc_releasecontentlabel"></a>MIP_CC_ReleaseContentLabel

Rilasciare le risorse associate a un'etichetta di contenuto

**Parametri**

Parametro | Description
|---|---|
| contentLabel | Etichetta da rilasciare |

```c
void MIP_CC_ReleaseContentLabel(mip_cc_content_label contentLabel);
```

## <a name="mip_cc_contentlabel_getcreationtime"></a>MIP_CC_ContentLabel_GetCreationTime

Ottiene l'ora in cui è stata applicata l'etichetta

**Parametri**

Parametro | Description
|---|---|
| contentLabel | Label |
| creationTime | Output Ora di applicazione dell'etichetta al documento (in secondi da Epoch) |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_ContentLabel_GetCreationTime(
    const mip_cc_content_label contentLabel,
    int64_t* creationTime);
```

## <a name="mip_cc_contentlabel_getassignmentmethod"></a>MIP_CC_ContentLabel_GetAssignmentMethod

Ottiene il metodo di assegnazione dell'etichetta

**Parametri**

Parametro | Description
|---|---|
| contentLabel | Label |
| assignmentMethod | Output Metodo di assegnazione (ad esempio ' standard ' o ' privileged ') |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_ContentLabel_GetAssignmentMethod(
    const mip_cc_content_label contentLabel,
    mip_cc_label_assignment_method* assignmentMethod);
```

## <a name="mip_cc_contentlabel_getextendedproperties"></a>MIP_CC_ContentLabel_GetExtendedProperties

Ottiene le proprietà estese

**Parametri**

Parametro | Description
|---|---|
| contentLabel | Label |
| proprietà | Output Dizionario di proprietà estese, memoria di proprietà del chiamante |

**Return**: codice risultato che indica l'esito positivo o negativo

**Nota**: la variabile ' Properties ' deve essere rilasciata dal chiamante chiamando MIP_CC_ReleaseDictionary 

```c
mip_cc_result MIP_CC_ContentLabel_GetExtendedProperties(
    const mip_cc_content_label contentLabel,
    mip_cc_dictionary* properties);
```

## <a name="mip_cc_contentlabel_isprotectionappliedfromlabel"></a>MIP_CC_ContentLabel_IsProtectionAppliedFromLabel

Ottiene un valore che indica se una protezione è stata applicata da un'etichetta.

**Parametri**

Parametro | Description
|---|---|
| contentLabel | Label |
| isProtectionAppliedByLabel | Output Se il documento è protetto e la protezione è stata applicata in modo esplicito da questa etichetta. |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_ContentLabel_IsProtectionAppliedFromLabel(
    const mip_cc_content_label contentLabel,
    bool* isProtectionAppliedByLabel);
```

## <a name="mip_cc_contentlabel_getlabel"></a>MIP_CC_ContentLabel_GetLabel

Ottiene le proprietà dell'etichetta generica da un'istanza dell'etichetta di contenuto

**Parametri**

Parametro | Description
|---|---|
| contentLabel | Label |
| etichetta | Output Etichetta generica, memoria di proprietà del chiamante |

**Return**: codice risultato che indica l'esito positivo o negativo

**Nota**: la variabile ' label ' deve essere rilasciata dal chiamante chiamando MIP_CC_ReleaseLabel 

```c
mip_cc_result MIP_CC_ContentLabel_GetLabel(
    const mip_cc_content_label contentLabel,
    mip_cc_label* label);
```

## <a name="mip_cc_customaction_getnamesize"></a>MIP_CC_CustomAction_GetNameSize

Ottiene le dimensioni del buffer necessarie per archiviare il nome di un'azione "personalizzata"

**Parametri**

Parametro | Description
|---|---|
| action | azione "personalizzata" |
| nameSize | Output Dimensione del buffer in cui memorizzare il nome (in numero di caratteri) |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_CustomAction_GetNameSize(
    const mip_cc_action action,
    int64_t* nameSize);
```

## <a name="mip_cc_customaction_getname"></a>MIP_CC_CustomAction_GetName

Ottiene il nome di un'azione "personalizzata"

**Parametri**

Parametro | Description
|---|---|
| action | azione "personalizzata" |
| nameBuffer | Output Buffer in cui verrà copiato il nome. |
| nameBufferSize | Dimensioni (in numero di caratteri) di nameBuffer. |
| actualNameSize | Output Numero di caratteri scritti nel buffer |

**Return**: codice risultato che indica l'esito positivo o negativo

**Nota**: se nameBuffer è null o insufficiente, viene restituito MIP_RESULT_ERROR_INSUFFICIENT_BUFFER e actualNameSize viene impostato sulle dimensioni minime del buffer richiesto. 

```c
mip_cc_result MIP_CC_CustomAction_GetName(
    const mip_cc_action action,
    char* nameBuffer,
    const int64_t nameBufferSize,
    int64_t* actualNameSize);
```

## <a name="mip_cc_customaction_getproperties"></a>MIP_CC_CustomAction_GetProperties

Ottiene le proprietà di un'azione "personalizzata".

**Parametri**

Parametro | Description
|---|---|
| action | azione "personalizzata" |
| proprietà | Output Dizionario di proprietà, memoria di proprietà del chiamante |

**Return**: codice risultato che indica l'esito positivo o negativo

**Nota**: la variabile ' Properties ' deve essere rilasciata dal chiamante chiamando MIP_CC_ReleaseDictionary 

```c
mip_cc_result MIP_CC_CustomAction_GetProperties(
    const mip_cc_action action,
    mip_cc_dictionary* properties);
```

## <a name="mip_cc_metadata_callback"></a>mip_cc_metadata_callback

Definizione della funzione di callback per recuperare il documento metatdata, filtrato in base al nome e al prefisso

**Parametri**

Parametro | Description
|---|---|
| nomi | Matrice di nomi di chiavi di metadati da includere nel risultato |
| namesSize | Numero di valori nella matrice ' names ' |
| namePrefixes | Matrice di prefissi dei nomi di chiave dei metadati da includere nel risultato |
| namePrefixesSize | Numero di valori nella matrice ' namesPrefixes ' |
| contesto | Il contesto dell'applicazione è stato passato in modo opaco dalla chiamata API al callback |
| metadati | Output Dizionario della chiave/valori dei metadati, creato dall'applicazione client. Questo dizionario verrà rilasciato da MIP. |

```c
MIP_CC_CALLBACK(mip_cc_metadata_callback,
    void,
    const char**,
    const int64_t,
    const char**,
    const int64_t,
    const void*,
    mip_cc_dictionary*);
```

## <a name="mip_cc_releaselabel"></a>MIP_CC_ReleaseLabel

Rilasciare le risorse associate a un'etichetta

**Parametri**

Parametro | Description
|---|---|
| etichetta | Etichetta da rilasciare |

```c
void MIP_CC_ReleaseLabel(mip_cc_label label);
```

## <a name="mip_cc_label_getid"></a>MIP_CC_Label_GetId

Ottiene l'ID etichetta

**Parametri**

Parametro | Description
|---|---|
| etichetta | Label |
| LabelId | Output ID etichetta |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_Label_GetId(
    const mip_cc_label label,
    mip_cc_guid* labelId);
```

## <a name="mip_cc_label_getnamesize"></a>MIP_CC_Label_GetNameSize

Ottiene le dimensioni del buffer necessarie per archiviare il nome

**Parametri**

Parametro | Description
|---|---|
| etichetta | Label |
| nameSize | Output Dimensione del buffer in cui memorizzare il nome (in numero di caratteri) |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_Label_GetNameSize(
    const mip_cc_label label,
    int64_t* nameSize);
```

## <a name="mip_cc_label_getname"></a>MIP_CC_Label_GetName

Ottiene il nome dell'etichetta

**Parametri**

Parametro | Description
|---|---|
| etichetta | Label |
| nameBuffer | Output Buffer in cui verrà copiato il nome. |
| nameBufferSize | Dimensioni (in numero di caratteri) di nameBuffer. |
| actualNameSize | Output Numero di caratteri scritti nel buffer |

**Return**: codice risultato che indica l'esito positivo o negativo

**Nota**: se nameBuffer è null o insufficiente, viene restituito MIP_RESULT_ERROR_INSUFFICIENT_BUFFER e actualNameSize viene impostato sulle dimensioni minime del buffer richiesto. 

```c
mip_cc_result MIP_CC_Label_GetName(
    const mip_cc_label label,
    char* nameBuffer,
    const int64_t nameBufferSize,
    int64_t* actualNameSize);
```

## <a name="mip_cc_label_getdescriptionsize"></a>MIP_CC_Label_GetDescriptionSize

Ottiene la dimensione del buffer necessaria per archiviare la descrizione

**Parametri**

Parametro | Description
|---|---|
| etichetta | Label |
| descriptionSize | Output Dimensione del buffer in cui memorizzare la descrizione (in numero di caratteri) |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_Label_GetDescriptionSize(
    const mip_cc_label label,
    int64_t* descriptionSize);
```

## <a name="mip_cc_label_getdescription"></a>MIP_CC_Label_GetDescription

Ottiene la descrizione dell'etichetta

**Parametri**

Parametro | Description
|---|---|
| etichetta | Label |
| descriptionBuffer | Output Buffer in cui verrà copiata la descrizione. |
| descriptionBufferSize | Dimensioni (in numero di caratteri) di descriptionBuffer. |
| actualDescriptionSize | Output Numero di caratteri scritti nel buffer |

**Return**: codice risultato che indica l'esito positivo o negativo

**Nota**: se descriptionBuffer è null o insufficiente, viene restituito MIP_RESULT_ERROR_INSUFFICIENT_BUFFER e actualDescriptionSize viene impostato sulle dimensioni minime del buffer richiesto. 

```c
mip_cc_result MIP_CC_Label_GetDescription(
    const mip_cc_label label,
    char* descriptionBuffer,
    const int64_t descriptionBufferSize,
    int64_t* actualDescriptionSize);
```

## <a name="mip_cc_label_getcolorsize"></a>MIP_CC_Label_GetColorSize

Ottiene le dimensioni del buffer necessarie per archiviare il colore

**Parametri**

Parametro | Description
|---|---|
| etichetta | Label |
| colorSize | Output Dimensione del buffer in cui mantenere il colore (in numero di caratteri) |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_Label_GetColorSize(
    const mip_cc_label label,
    int64_t* colorSize);
```

## <a name="mip_cc_label_getcolor"></a>MIP_CC_Label_GetColor

Ottiene il colore dell'etichetta

**Parametri**

Parametro | Description
|---|---|
| etichetta | Label |
| colorBuffer | Output Buffer in cui verrà copiato il colore (in #RRGGBB formato). |
| colorBufferSize | Dimensioni (in numero di caratteri) di colorBuffer. |
| actualColorSize | Output Numero di caratteri scritti nel buffer |

**Return**: codice risultato che indica l'esito positivo o negativo

**Nota**: se colorBuffer è null o insufficiente, viene restituito MIP_RESULT_ERROR_INSUFFICIENT_BUFFER e actualColorSize viene impostato sulle dimensioni minime del buffer richiesto. 

```c
mip_cc_result MIP_CC_Label_GetColor(
    const mip_cc_label label,
    char* colorBuffer,
    const int64_t colorBufferSize,
    int64_t* actualColorSize);
```

## <a name="mip_cc_label_getsensitivity"></a>MIP_CC_Label_GetSensitivity

Ottiene il livello di sensibilità dell'etichetta. Un valore più alto significa più sensibile.

**Parametri**

Parametro | Description
|---|---|
| etichetta | Label |
| sensibilità | Output Livello di riservatezza |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_Label_GetSensitivity(
    const mip_cc_label label,
    int32_t* sensitivity);
```

## <a name="mip_cc_label_gettooltipsize"></a>MIP_CC_Label_GetTooltipSize

Ottiene le dimensioni del buffer necessarie per archiviare la descrizione comando

**Parametri**

Parametro | Description
|---|---|
| etichetta | Label |
| tooltipSize | Output Dimensione del buffer in cui memorizzare la descrizione comando (in numero di caratteri) |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_Label_GetTooltipSize(
    const mip_cc_label label,
    int64_t* tooltipSize);
```

## <a name="mip_cc_label_gettooltip"></a>MIP_CC_Label_GetTooltip

Ottiene la descrizione comando dell'etichetta

**Parametri**

Parametro | Description
|---|---|
| etichetta | Label |
| tooltipBuffer | Output Buffer in cui verrà copiata la descrizione comando. |
| tooltipBufferSize | Dimensioni (in numero di caratteri) di tooltipBuffer. |
| actualTooltipSize | Output Numero di caratteri scritti nel buffer |

**Return**: codice risultato che indica l'esito positivo o negativo

**Nota**: se tooltipBuffer è null o insufficiente, viene restituito MIP_RESULT_ERROR_INSUFFICIENT_BUFFER e actualTooltipSize viene impostato sulle dimensioni minime del buffer richiesto. 

```c
mip_cc_result MIP_CC_Label_GetTooltip(
    const mip_cc_label label,
    char* tooltipBuffer,
    const int64_t tooltipBufferSize,
    int64_t* actualTooltipSize);
```

## <a name="mip_cc_label_getautotooltipsize"></a>MIP_CC_Label_GetAutoTooltipSize

Ottiene la dimensione del buffer necessaria per archiviare la descrizione comando di classificazione automatica

**Parametri**

Parametro | Description
|---|---|
| etichetta | Label |
| tooltipSize | Output Dimensione del buffer in cui memorizzare la descrizione comando (in numero di caratteri) |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_Label_GetAutoTooltipSize(
    const mip_cc_label label,
    int64_t* tooltipSize);
```

## <a name="mip_cc_label_getautotooltip"></a>MIP_CC_Label_GetAutoTooltip

Ottiene la descrizione comando per la classificazione automatica delle etichette

**Parametri**

Parametro | Description
|---|---|
| etichetta | Label |
| tooltipBuffer | Output Buffer in cui verrà copiata la descrizione comando. |
| tooltipBufferSize | Dimensioni (in numero di caratteri) di tooltipBuffer. |
| actualTooltipSize | Output Numero di caratteri scritti nel buffer |

**Return**: codice risultato che indica l'esito positivo o negativo

**Nota**: se tooltipBuffer è null o insufficiente, viene restituito MIP_RESULT_ERROR_INSUFFICIENT_BUFFER e actualTooltipSize viene impostato sulle dimensioni minime del buffer richiesto. 

```c
mip_cc_result MIP_CC_Label_GetAutoTooltip(
    const mip_cc_label label,
    char* tooltipBuffer,
    const int64_t tooltipBufferSize,
    int64_t* actualTooltipSize);
```

## <a name="mip_cc_label_isactive"></a>MIP_CC_Label_IsActive

Ottiene un valore che indica se un'etichetta è attiva o meno.

**Parametri**

Parametro | Description
|---|---|
| etichetta | Label |
| isActive | Output Indica se un'etichetta è considerata attiva. |

**Return**: codice risultato che indica l'esito positivo o negativo

**Nota**: è possibile applicare solo le etichette attive. Non è possibile applicare le etichette Inactivte e vengono usate solo a scopo di visualizzazione. 

```c
mip_cc_result MIP_CC_Label_IsActive(
    const mip_cc_label label,
    bool* isActive);
```

## <a name="mip_cc_label_getparent"></a>MIP_CC_Label_GetParent

Ottiene l'etichetta padre, se disponibile.

**Parametri**

Parametro | Description
|---|---|
| etichetta | Label |
| padre | Output Etichetta padre, se presente, else null |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_Label_GetParent(
    const mip_cc_label label,
    mip_cc_label* parent);
```

## <a name="mip_cc_label_getchildrensize"></a>MIP_CC_Label_GetChildrenSize

Ottiene il numero di etichette figlio

**Parametri**

Parametro | Description
|---|---|
| etichetta | Label |
| bambiniDimensione | Output Numero di elementi figlio |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_Label_GetChildrenSize(
    const mip_cc_label label,
    int64_t* childrenSize);
```

## <a name="mip_cc_label_getchildren"></a>MIP_CC_Label_GetChildren

Ottiene le etichette figlio

**Parametri**

Parametro | Description
|---|---|
| etichetta | Label |
| childrenBuffer | Output Buffer in cui verranno copiate le etichette figlio. Etichette figlio |
| childrenBufferSize | Dimensioni (in numero di etichette) di childrenBuffer. |
| actualChildrenSize | Output Numero di etichette figlio scritte nel buffer |

**Return**: codice risultato che indica l'esito positivo o negativo

**Nota**: se childrenBuffer è null o insufficiente, viene restituito MIP_RESULT_ERROR_INSUFFICIENT_BUFFER e actualChildrenSize viene impostato sulle dimensioni minime del buffer richiesto. 

```c
mip_cc_result MIP_CC_Label_GetChildren(
    const mip_cc_label label,
    mip_cc_label* childrenBuffer,
    const int64_t childrenBufferSize,
    int64_t* actualChildrenSize);
```

## <a name="mip_cc_label_getcustomsettings"></a>MIP_CC_Label_GetCustomSettings

Ottiene le impostazioni personalizzate definite dal criterio di un'etichetta

**Parametri**

Parametro | Description
|---|---|
| etichetta | Label |
| impostazioni | Output Dizionario di impostazioni, di proprietà del chiamante |

**Return**: codice risultato che indica l'esito positivo o negativo

**Nota**: la variabile ' Settings ' deve essere rilasciata dal chiamante chiamando MIP_CC_ReleaseDictionary 

```c
mip_cc_result MIP_CC_Label_GetCustomSettings(
    const mip_cc_label label,
    mip_cc_dictionary* settings);
```

## <a name="mip_cc_metadataaction_getmetadatatoremove"></a>MIP_CC_MetadataAction_GetMetadataToRemove

Ottiene i metadati dell'azione "Metadata" da rimuovere

**Parametri**

Parametro | Description
|---|---|
| action | azione "metadati" |
| metadataNames | Output Nomi chiave dei metadati da rimuovere, memoria di proprietà del chiamante |

**Return**: codice risultato che indica l'esito positivo o negativo

**Nota**: la variabile ' metadataNames ' deve essere rilasciata dal chiamante chiamando MIP_CC_ReleaseStringList @note la rimozione dei metadati deve essere eseguita prima di aggiungere i metadati 

```c
mip_cc_result MIP_CC_MetadataAction_GetMetadataToRemove(
    const mip_cc_action action,
    mip_cc_string_list* metadataNames);
```

## <a name="mip_cc_metadataaction_getmetadatatoadd"></a>MIP_CC_MetadataAction_GetMetadataToAdd

Ottiene i metadati dell'azione "Metadata" da aggiungere

**Parametri**

Parametro | Description
|---|---|
| action | azione "metadati" |
| metadati | Output Coppie chiave/valore di metadati da aggiungere, memoria di proprietà del chiamante |

**Return**: codice risultato che indica l'esito positivo o negativo

**Nota**: la variabile ' Metadata ' deve essere rilasciata dal chiamante chiamando MIP_CC_ReleaseDictionary @note la rimozione dei metadati deve essere eseguita prima di aggiungere i metadati 

```c
mip_cc_result MIP_CC_MetadataAction_GetMetadataToAdd(
    const mip_cc_action action,
    mip_cc_dictionary* metadata);
```

## <a name="mip_cc_releasepolicyengine"></a>MIP_CC_ReleasePolicyEngine

Rilasciare le risorse associate a un motore dei criteri

**Parametri**

Parametro | Description
|---|---|
| Motore | Motore dei criteri da rilasciare |

```c
void MIP_CC_ReleasePolicyEngine(mip_cc_policy_engine engine);
```

## <a name="mip_cc_policyengine_getengineidsize"></a>MIP_CC_PolicyEngine_GetEngineIdSize

Ottiene le dimensioni del buffer necessario per l'ID del motore

**Parametri**

Parametro | Description
|---|---|
| Motore | Motore dei criteri |
| idSize | Output Dimensione del buffer in cui memorizzare l'ID del motore (in numero di caratteri) |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_PolicyEngine_GetEngineIdSize(
    const mip_cc_policy_engine engine,
    int64_t* idSize);
```

## <a name="mip_cc_policyengine_getengineid"></a>MIP_CC_PolicyEngine_GetEngineId

Ottiene l'ID del motore

**Parametri**

Parametro | Description
|---|---|
| Motore | Motore dei criteri |
| idBuffer | Output Buffer in cui verrà copiato l'ID. |
| idBufferSize | Dimensioni (in numero di caratteri) di idBuffer. |
| actualIdSize | Output Numero di caratteri scritti nel buffer |

**Return**: codice risultato che indica l'esito positivo o negativo

**Nota**: se idBuffer è null o insufficiente, viene restituito MIP_RESULT_ERROR_INSUFFICIENT_BUFFER e actualIdSize viene impostato sulle dimensioni minime del buffer richiesto. 

```c
mip_cc_result MIP_CC_PolicyEngine_GetEngineId(
    const mip_cc_policy_engine engine,
    char* idBuffer,
    const int64_t idBufferSize,
    int64_t* actualIdSize);
```

## <a name="mip_cc_policyengine_getmoreinfourlsize"></a>MIP_CC_PolicyEngine_GetMoreInfoUrlSize

Ottiene le dimensioni dei dati client associati a un motore di criteri

**Parametri**

Parametro | Description
|---|---|
| Motore | Motore dei criteri |
| moreInfoUrlSize | Output Dimensioni dei dati client (in numero di caratteri) |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_PolicyEngine_GetMoreInfoUrlSize(
    const mip_cc_policy_engine engine,
    int64_t* moreInfoUrlSize);
```

## <a name="mip_cc_policyengine_getmoreinfourl"></a>MIP_CC_PolicyEngine_GetMoreInfoUrl

Ottenere i dati client associati a un motore dei criteri

**Parametri**

Parametro | Description
|---|---|
| Motore | Motore dei criteri |
| moreInfoUrlBuffer | Output Buffer in cui verranno copiati i dati client |
| moreInfoUrlBufferSize | Dimensioni (in numero di caratteri) di moreInfoUrlBuffer. |
| actualMoreInfoUrlSize | Output Numero di caratteri scritti nel buffer |

**Return**: codice risultato che indica l'esito positivo o negativo

**Nota**: se moreInfoUrlBuffer è null o insufficiente, viene restituito MIP_RESULT_ERROR_INSUFFICIENT_BUFFER e actualMoreInfoUrlSize viene impostato sulle dimensioni minime del buffer richiesto. 

```c
mip_cc_result MIP_CC_PolicyEngine_GetMoreInfoUrl(
    const mip_cc_policy_engine engine,
    char* moreInfoUrlBuffer,
    const int64_t moreInfoUrlBufferSize,
    int64_t* actualMoreInfoUrlSize);
```

## <a name="mip_cc_policyengine_islabelingrequired"></a>MIP_CC_PolicyEngine_IsLabelingRequired

Ottiene un valore che indica se i criteri stabiliscono che è necessario etichettare un documento.

**Parametri**

Parametro | Description
|---|---|
| Motore | Motore dei criteri |
| isLabelingRequired | Output Indica se i criteri stabiliscono che è necessario etichettare un documento |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_PolicyEngine_IsLabelingRequired(
    const mip_cc_policy_engine engine,
    bool* isLabelingRequired);
```

## <a name="mip_cc_policyengine_getpolicyfileidsize"></a>MIP_CC_PolicyEngine_GetPolicyFileIdSize

Ottiene le dimensioni dei dati client associati a un motore di criteri

**Parametri**

Parametro | Description
|---|---|
| Motore | Motore dei criteri |
| policyFileIdSize | Output Dimensioni dei dati client (in numero di caratteri) |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_PolicyEngine_GetPolicyFileIdSize(
    const mip_cc_policy_engine engine,
    int64_t* policyFileIdSize);
```

## <a name="mip_cc_policyengine_getpolicyfileid"></a>MIP_CC_PolicyEngine_GetPolicyFileId

Ottenere i dati client associati a un motore dei criteri

**Parametri**

Parametro | Description
|---|---|
| Motore | Motore dei criteri |
| policyFileIdBuffer | Output Buffer in cui verranno copiati i dati client |
| policyFileIdBufferSize | Dimensioni (in numero di caratteri) di policyFileIdBuffer. |
| actualPolicyFileIdSize | Output Numero di caratteri scritti nel buffer |

**Return**: codice risultato che indica l'esito positivo o negativo

**Nota**: se policyFileIdBuffer è null o insufficiente, viene restituito MIP_RESULT_ERROR_INSUFFICIENT_BUFFER e actualPolicyFileIdSize viene impostato sulle dimensioni minime del buffer richiesto. 

```c
mip_cc_result MIP_CC_PolicyEngine_GetPolicyFileId(
    const mip_cc_policy_engine engine,
    char* policyFileIdBuffer,
    const int64_t policyFileIdBufferSize,
    int64_t* actualPolicyFileIdSize);
```

## <a name="mip_cc_policyengine_getsensitivityfileidsize"></a>MIP_CC_PolicyEngine_GetSensitivityFileIdSize

Ottiene le dimensioni dei dati client associati a un motore di criteri

**Parametri**

Parametro | Description
|---|---|
| Motore | Motore dei criteri |
| sensitivityFileIdSize | Output Dimensioni dei dati client (in numero di caratteri) |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_PolicyEngine_GetSensitivityFileIdSize(
    const mip_cc_policy_engine engine,
    int64_t* sensitivityFileIdSize);
```

## <a name="mip_cc_policyengine_getsensitivityfileid"></a>MIP_CC_PolicyEngine_GetSensitivityFileId

Ottenere i dati client associati a un motore dei criteri

**Parametri**

Parametro | Description
|---|---|
| Motore | Motore dei criteri |
| sensitivityFileIdBuffer | Output Buffer in cui verranno copiati i dati client |
| sensitivityFileIdBufferSize | Dimensioni (in numero di caratteri) di sensitivityFileIdBuffer. |
| actualSensitivityFileIdSize | Output Numero di caratteri scritti nel buffer |

**Return**: codice risultato che indica l'esito positivo o negativo

**Nota**: se sensitivityFileIdBuffer è null o insufficiente, viene restituito MIP_RESULT_ERROR_INSUFFICIENT_BUFFER e actualSensitivityFileIdSize viene impostato sulle dimensioni minime del buffer richiesto. 

```c
mip_cc_result MIP_CC_PolicyEngine_GetSensitivityFileId(
    const mip_cc_policy_engine engine,
    char* sensitivityFileIdBuffer,
    const int64_t sensitivityFileIdBufferSize,
    int64_t* actualSensitivityFileIdSize);
```

## <a name="mip_cc_policyengine_hasclassificationrules"></a>MIP_CC_PolicyEngine_HasClassificationRules

Ottiene un valore che indica se il criterio ha regole automatiche o consigliate

**Parametri**

Parametro | Description
|---|---|
| Motore | Motore dei criteri |
| hasClassificationRules | Output Indica se i criteri hanno regole automatiche o di raccomandazione |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_PolicyEngine_HasClassificationRules(
    const mip_cc_policy_engine engine,
    bool* hasClassificationRules);
```

## <a name="mip_cc_policyengine_getlastpolicyfetchtime"></a>MIP_CC_PolicyEngine_GetLastPolicyFetchTime

Ottiene l'ora dell'ultimo recupero dei criteri

**Parametri**

Parametro | Description
|---|---|
| Motore | Motore dei criteri |
| lastPolicyFetchTime | Output Ora dell'ultimo recupero dei criteri (in secondi da Epoch) |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_PolicyEngine_GetLastPolicyFetchTime(
    const mip_cc_policy_engine engine,
    int64_t* lastPolicyFetchTime);
```

## <a name="mip_cc_policyengine_getsensitivitylabelssize"></a>MIP_CC_PolicyEngine_GetSensitivityLabelsSize

Ottiene il numero di etichette di riservatezza associate al motore dei criteri

**Parametri**

Parametro | Description
|---|---|
| Motore | Motore dei criteri |
| labelsSize | Output Numero di etichette |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_PolicyEngine_GetSensitivityLabelsSize(
    const mip_cc_policy_engine engine,
    int64_t* labelsSize);
```

## <a name="mip_cc_policyengine_getsensitivitylabels"></a>MIP_CC_PolicyEngine_GetSensitivityLabels

Ottiene le etichette di riservatezza associate al motore dei criteri

**Parametri**

Parametro | Description
|---|---|
| Motore | Motore dei criteri |
| labelBuffer | Output Buffer in cui verranno copiate le etichette. Le etichette sono di proprietà del client |
| labelBufferSize | Dimensioni (in numero di etichette) di labelBuffer. |
| actualLabelsSize | Output Numero di etichette scritte nel buffer |

**Return**: codice risultato che indica l'esito positivo o negativo

**Nota**: se labelBuffer è null o insufficiente, viene restituito MIP_RESULT_ERROR_INSUFFICIENT_BUFFER e actualLabelsSize viene impostato sulle dimensioni minime del buffer richiesto. 

```c
mip_cc_result MIP_CC_PolicyEngine_GetSensitivityLabels(
    const mip_cc_policy_engine engine,
    mip_cc_label* labelBuffer,
    const int64_t labelBufferSize,
    int64_t* actualLabelsSize);
```

## <a name="mip_cc_policyengine_getlabelbyid"></a>MIP_CC_PolicyEngine_GetLabelById

Ottiene l'etichetta di riservatezza in base all'ID

**Parametri**

Parametro | Description
|---|---|
| Motore | Motore dei criteri |
| LabelId | ID etichetta |
| etichetta | Output Etichetta di riservatezza. Questo valore è di proprietà del chiamante e deve essere rilasciato con MIP_CC_ReleaseLabel. |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_PolicyEngine_GetLabelById(
    const mip_cc_policy_engine engine,
    const char* labelId,
    mip_cc_label* label);
```

## <a name="mip_cc_policyengine_getsensitivitytypessize"></a>MIP_CC_PolicyEngine_GetSensitivityTypesSize

Ottiene il numero di tipi di riservatezza associati al motore dei criteri.

**Parametri**

Parametro | Description
|---|---|
| Motore | Motore dei criteri |
| sensitivityTypesSize | Output Numero di tipi di riservatezza |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_PolicyEngine_GetSensitivityTypesSize(
    const mip_cc_policy_engine engine,
    int64_t* sensitivityTypesSize);
```

## <a name="mip_cc_policyengine_getsensitivitytypes"></a>MIP_CC_PolicyEngine_GetSensitivityTypes

Ottiene i tipi di riservatezza associati al motore dei criteri.

**Parametri**

Parametro | Description
|---|---|
| Motore | Motore dei criteri |
| sensitivityTypeBuffer | Output Buffer in cui verranno copiati i tipi di riservatezza. Sensibilità |
| sensitivityTypeBufferSize | Dimensioni (in numero di tipi di riservatezza) del sensitivityTypeBuffer. |
| actualSensitivityTypesSize | Output Numero di tipi di riservatezza scritti nel buffer |

**Return**: codice risultato che indica l'esito positivo o negativo

**Nota**: se sensitivityTypeBuffer è null o insufficiente, viene restituito MIP_RESULT_ERROR_INSUFFICIENT_BUFFER e actualSensitivityTypesSize viene impostato sulle dimensioni minime del buffer richiesto. 

```c
mip_cc_result MIP_CC_PolicyEngine_GetSensitivityTypes(
    const mip_cc_policy_engine engine,
    mip_cc_sensitivity_type* sensitivityTypeBuffer,
    const int64_t sensitivityTypeBufferSize,
    int64_t* actualSensitivityTypesSize);
```

## <a name="mip_cc_policyengine_createpolicyhandler"></a>MIP_CC_PolicyEngine_CreatePolicyHandler

Creazione di un gestore dei criteri per l'esecuzione di funzioni correlate ai criteri

**Parametri**

Parametro | Description
|---|---|
| Motore | Motore dei criteri |
| isAuditDiscoveryEnabled | Indica se l'individuazione del controllo è abilitata |
| Gestore | Output Istanza del gestore criteri appena creata |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_PolicyEngine_CreatePolicyHandler(
    const mip_cc_policy_engine engine,
    const bool isAuditDiscoveryEnabled,
    mip_cc_policy_handler* handler);
```

## <a name="mip_cc_policyengine_sendapplicationauditevent"></a>MIP_CC_PolicyEngine_SendApplicationAuditEvent

Registra un evento specifico dell'applicazione nella pipeline di controllo

**Parametri**

Parametro | Description
|---|---|
| Livello | Livello dell'evento: info/Error/Warning |
| eventType | Descrizione del tipo di evento |
| eventData | Dati associati all'evento. |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_PolicyEngine_SendApplicationAuditEvent(
    const mip_cc_policy_engine engine,
    const char* level,
    const char* eventType,
    const char* eventData);
```

## <a name="mip_cc_policyengine_getpolicydataxmlsize"></a>MIP_CC_PolicyEngine_GetPolicyDataXmlSize

Ottiene le dimensioni del codice XML dei dati dei criteri

**Parametri**

Parametro | Description
|---|---|
| Motore | Motore dei criteri |
| XmlSize | Output Dimensioni del codice XML dei dati dei criteri (in numero di caratteri) |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_PolicyEngine_GetPolicyDataXmlSize(
    const mip_cc_policy_engine engine,
    int64_t* xmlSize);
```

## <a name="mip_cc_policyengine_getpolicydataxml"></a>MIP_CC_PolicyEngine_GetPolicyDataXml

Ottiene il codice XML dei dati dei criteri

**Parametri**

Parametro | Description
|---|---|
| Motore | Motore dei criteri |
| XmlBuffer | Output Buffer in cui verrà copiato il codice XML. |
| xmlBufferSize | Dimensioni (in numero di caratteri) di XmlBuffer. |
| actualXmlSize | Output Numero di caratteri scritti nel buffer |

**Return**: codice risultato che indica l'esito positivo o negativo

**Nota**: se XmlBuffer è null o insufficiente, verrà restituito MIP_RESULT_ERROR_INSUFFICIENT_BUFFER e actualXmlSize verrà impostato sulle dimensioni minime del buffer richiesto. 

```c
mip_cc_result MIP_CC_PolicyEngine_GetPolicyDataXml(
    const mip_cc_policy_engine engine,
    char* xmlBuffer,
    const int64_t xmlBufferSize,
    int64_t* actualXmlSize);
```

## <a name="mip_cc_policyengine_getsensitivitytypesdataxmlsize"></a>MIP_CC_PolicyEngine_GetSensitivityTypesDataXmlSize

Ottiene le dimensioni dei dati XML dei tipi di riservatezza

**Parametri**

Parametro | Description
|---|---|
| Motore | Motore dei criteri |
| XmlSize | Output Dimensioni del codice XML dei dati dei criteri (in numero di caratteri) |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_PolicyEngine_GetSensitivityTypesDataXmlSize(
    const mip_cc_policy_engine engine,
    int64_t* xmlSize);
```

## <a name="mip_cc_policyengine_getsensitivitytypesdataxml"></a>MIP_CC_PolicyEngine_GetSensitivityTypesDataXml

Ottiene il codice XML di dati dei tipi di riservatezza

**Parametri**

Parametro | Description
|---|---|
| Motore | Motore dei criteri |
| XmlBuffer | Output Buffer in cui verrà copiato il codice XML. |
| xmlBufferSize | Dimensioni (in numero di caratteri) di XmlBuffer. |
| actualXmlSize | Output Numero di caratteri scritti nel buffer |

**Return**: codice risultato che indica l'esito positivo o negativo

**Nota**: se XmlBuffer è null o insufficiente, verrà restituito MIP_RESULT_ERROR_INSUFFICIENT_BUFFER e actualXmlSize verrà impostato sulle dimensioni minime del buffer richiesto. 

```c
mip_cc_result MIP_CC_PolicyEngine_GetSensitivityTypesDataXml(
    const mip_cc_policy_engine engine,
    char* xmlBuffer,
    const int64_t xmlBufferSize,
    int64_t* actualXmlSize);
```

## <a name="mip_cc_policyengine_getclientdatasize"></a>MIP_CC_PolicyEngine_GetClientDataSize

Ottiene le dimensioni dei dati client associati a un motore di criteri

**Parametri**

Parametro | Description
|---|---|
| Motore | Motore dei criteri |
| clientDataSize | Output Dimensioni dei dati client (in numero di caratteri) |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_PolicyEngine_GetClientDataSize(
    const mip_cc_policy_engine engine,
    int64_t* clientDataSize);
```

## <a name="mip_cc_policyengine_getclientdata"></a>MIP_CC_PolicyEngine_GetClientData

Ottenere i dati client associati a un motore dei criteri

**Parametri**

Parametro | Description
|---|---|
| Motore | Motore dei criteri |
| clientDataBuffer | Output Buffer in cui verranno copiati i dati client |
| clientDataBufferSize | Dimensioni (in numero di caratteri) di clientDataBuffer. |
| actualClientDataSize | Output Numero di caratteri scritti nel buffer |

**Return**: codice risultato che indica l'esito positivo o negativo

**Nota**: se clientDataBuffer è null o insufficiente, viene restituito MIP_RESULT_ERROR_INSUFFICIENT_BUFFER e actualClientDataSize viene impostato sulle dimensioni minime del buffer richiesto. 

```c
mip_cc_result MIP_CC_PolicyEngine_GetClientData(
    const mip_cc_policy_engine engine,
    char* clientDataBuffer,
    const int64_t clientDataBufferSize,
    int64_t* actualClientDataSize);
```

## <a name="mip_cc_createpolicyenginesettingswithidentity"></a>MIP_CC_CreatePolicyEngineSettingsWithIdentity

Creare un oggetto impostazioni usato per creare un nuovo motore dei criteri

**Parametri**

Parametro | Description
|---|---|
| autenticazione | Identità che verrà associata a PolicyEngine |
| clientData | Dati client personalizzabili archiviati insieme al motore |
| locale | Impostazioni locali in cui vengono restituiti i risultati del testo |
| loadSensitivityTypes | Se è necessario caricare anche i dati dei tipi di riservatezza (per la classificazione) |
| impostazioni | Output Istanza di impostazioni appena creata |

**Return**: codice risultato che indica l'esito positivo o negativo

**Nota**:' loadSensitivityTypes ' deve essere ' true ' solo se l'applicazione prevede di chiamare MIP_CC_PolicyEngine_GetSensitivityTypes in un secondo momento. In caso contrario, deve essere false per evitare un'operazione HTTP non necessaria. 

```c
mip_cc_result MIP_CC_CreatePolicyEngineSettingsWithIdentity(
    const mip_cc_identity* identity,
    const char* clientData,
    const char* locale,
    bool loadSensitivityTypes,
    mip_cc_policy_engine_settings* settings);
```

## <a name="mip_cc_policyenginesettings_setclientdata"></a>MIP_CC_PolicyEngineSettings_SetClientData

Imposta i dati client che verranno archiviati in maniera opaca insieme a questo motore e mantengono tra le sessioni

**Parametri**

Parametro | Description
|---|---|
| impostazioni | Impostazioni motore |
| clientData | Dati client |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_PolicyEngineSettings_SetClientData(
    const mip_cc_policy_engine_settings settings,
    const char* clientData);
```

## <a name="mip_cc_policyenginesettings_setcustomsettings"></a>MIP_CC_PolicyEngineSettings_SetCustomSettings

Configura le impostazioni personalizzate, usate per il controllo e il controllo delle funzionalità.

**Parametri**

Parametro | Description
|---|---|
| impostazioni | Impostazioni motore |
| customSettings | Coppie chiave/valore di impostazioni personalizzate |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_PolicyEngineSettings_SetCustomSettings(
    const mip_cc_policy_engine_settings settings,
    const mip_cc_dictionary customSettings);
```

## <a name="mip_cc_policyenginesettings_setsessionid"></a>MIP_CC_PolicyEngineSettings_SetSessionId

Imposta l'ID di sessione che può essere usato per correlare i log e i dati di telemetria

**Parametri**

Parametro | Description
|---|---|
| impostazioni | Impostazioni motore |
| sessionId | ID di sessione che rappresenta la durata di un motore dei criteri |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_PolicyEngineSettings_SetSessionId(
    const mip_cc_policy_engine_settings settings,
    const char* sessionId);
```

## <a name="mip_cc_policyenginesettings_setcloudendpointbaseurl"></a>MIP_CC_PolicyEngineSettings_SetCloudEndpointBaseUrl

Imposta l'URL di base per tutte le richieste di servizio

**Parametri**

Parametro | Description
|---|---|
| impostazioni | Impostazioni motore |
| cloudEndpointBaseUrl | URL di base (ad esempio 'https://api.aadrm.com ') |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_PolicyEngineSettings_SetCloudEndpointBaseUrl(
    const mip_cc_policy_engine_settings settings,
    const char* cloudEndpointBaseUrl);
```

## <a name="mip_cc_policyenginesettings_setdelegateduseremail"></a>MIP_CC_PolicyEngineSettings_SetDelegatedUserEmail

Imposta l'utente delegato

**Parametri**

Parametro | Description
|---|---|
| impostazioni | Impostazioni motore |
| delegatedUserEmail | Indirizzo di posta elettronica dell'utente delegato |

**Return**: codice risultato che indica l'esito positivo o negativo

**Nota**: un utente delegato viene specificato quando l'utente o l'applicazione di autenticazione agisce per conto di un altro utente 

```c
mip_cc_result MIP_CC_PolicyEngineSettings_SetDelegatedUserEmail(
    const mip_cc_policy_engine_settings settings,
    const char* delegatedUserEmail);
```

## <a name="mip_cc_releasepolicyenginesettings"></a>MIP_CC_ReleasePolicyEngineSettings

Rilasciare le risorse associate a impostazioni del motore dei criteri

**Parametri**

Parametro | Description
|---|---|
| impostazioni | Impostazioni del motore dei criteri da rilasciare |

```c
void MIP_CC_ReleasePolicyEngineSettings(mip_cc_policy_engine_settings settings);
```

## <a name="mip_cc_releasepolicyhandler"></a>MIP_CC_ReleasePolicyHandler

Rilasciare le risorse associate a un gestore dei criteri

**Parametri**

Parametro | Description
|---|---|
| Gestore | Gestore dei criteri da rilasciare |

```c
void MIP_CC_ReleasePolicyHandler(mip_cc_policy_handler handler);
```

## <a name="mip_cc_policyhandler_getsensitivitylabel"></a>MIP_CC_PolicyHandler_GetSensitivityLabel

Ottiene l'etichetta corrente di un documento

**Parametri**

Parametro | Description
|---|---|
| Gestore | Gestore criteri |
| documentState | Stato del documento |
| contesto | Il contesto dell'applicazione viene trasmesso in modo opaco a qualsiasi callback |
| contentLabel | Etichetta attualmente applicata a un documento |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_PolicyHandler_GetSensitivityLabel(
    const mip_cc_policy_handler handler,
    const mip_cc_document_state* documentState,
    const void* context,
    mip_cc_content_label* contentLabel);
```

## <a name="mip_cc_policyhandler_computeactions"></a>MIP_CC_PolicyHandler_ComputeActions

Esegue le regole dei criteri in base allo stato fornito e determina le azioni corrispondenti

**Parametri**

Parametro | Description
|---|---|
| Gestore | Gestore criteri |
| documentState | Stato del documento |
| applicationState | Stato azione applicazione |
| contesto | Il contesto dell'applicazione viene trasmesso in modo opaco a qualsiasi callback |
| actionResult | Output Azioni che devono essere eseguite dall'applicazione, memoria di proprietà del chiamante |

**Return**: codice risultato che indica l'esito positivo o negativo

**Nota**: la variabile ' ActionResult ' deve essere rilasciata dal chiamante chiamando MIP_CC_ReleaseActionResult 

```c
mip_cc_result MIP_CC_PolicyHandler_ComputeActions(
    const mip_cc_policy_handler handler,
    const mip_cc_document_state* documentState,
    const mip_cc_application_action_state* applicationState,
    const void* context,
    mip_cc_action_result* actionResult);
```

## <a name="mip_cc_policyhandler_notifycommittedactions"></a>MIP_CC_PolicyHandler_NotifyCommittedActions

Chiamata eseguita dall'applicazione dopo l'applicazione delle azioni calcolate e i dati di cui è stato eseguito il commit su disco

**Parametri**

Parametro | Description
|---|---|
| Gestore | Gestore criteri |
| documentState | Stato del documento |
| applicationState | Stato azione applicazione |
| contesto | Il contesto dell'applicazione viene trasmesso in modo opaco a qualsiasi callback |

**Return**: codice risultato che indica l'esito positivo o negativo

**Nota**: una chiamata a questa funzione è necessaria per trasmettere i dati di controllo dell'etichetta completi. 

```c
mip_cc_result MIP_CC_PolicyHandler_NotifyCommittedActions(
    const mip_cc_policy_handler handler,
    const mip_cc_document_state* documentState,
    const mip_cc_application_action_state* applicationState,
    const void* context);
```

## <a name="mip_cc_loadpolicyprofile"></a>MIP_CC_LoadPolicyProfile

Carica un profilo

**Parametri**

Parametro | Description
|---|---|
| impostazioni | Impostazioni profilo |
| Profilo | Output Istanza del profilo criteri appena creata |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_LoadPolicyProfile(
    const mip_cc_policy_profile_settings settings,
    mip_cc_policy_profile* profile);
```

## <a name="mip_cc_releasepolicyprofile"></a>MIP_CC_ReleasePolicyProfile

Rilasciare le risorse associate a un profilo criteri

**Parametri**

Parametro | Description
|---|---|
| Profilo | Profilo criteri da rilasciare |

```c
void MIP_CC_ReleasePolicyProfile(mip_cc_policy_profile profile);
```

## <a name="mip_cc_policyprofilesettings_setsessionid"></a>MIP_CC_PolicyProfileSettings_SetSessionId

Imposta l'ID di sessione che può essere usato per correlare i log e i dati di telemetria

**Parametri**

Parametro | Description
|---|---|
| impostazioni | Impostazioni profilo |
| sessionId | ID di sessione che rappresenta la durata di un profilo di criteri |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_PolicyProfileSettings_SetSessionId(
    const mip_cc_policy_profile_settings settings,
    const char* sessionId);
```

## <a name="mip_cc_policyprofilesettings_sethttpdelegate"></a>MIP_CC_PolicyProfileSettings_SetHttpDelegate

Esegui override dello stack HTTP predefinito con il proprio client

**Parametri**

Parametro | Description
|---|---|
| impostazioni | Impostazioni del profilo a cui verrà assegnato il delegato HTTP |
| httpDelegate | Istanza di callback HTTP implementata dall'applicazione client |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_PolicyProfileSettings_SetHttpDelegate(
    const mip_cc_policy_profile_settings settings,
    const mip_cc_http_delegate httpDelegate);
```

## <a name="mip_cc_policyprofilesettings_settaskdispatcherdelegate"></a>MIP_CC_PolicyProfileSettings_SetTaskDispatcherDelegate

Esegui override del dispatcher attività asincrono predefinito con il proprio client

**Parametri**

Parametro | Description
|---|---|
| impostazioni | Impostazioni del profilo a cui verrà assegnato il delegato del dispatcher attività |
| taskDispatcherDelegate | Istanza di callback Dispatcher attività implementata dall'applicazione client |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_PolicyProfileSettings_SetTaskDispatcherDelegate(
    const mip_cc_policy_profile_settings settings,
    const mip_cc_task_dispatcher_delegate taskDispatcherDelegate);
```

## <a name="mip_cc_policyprofilesettings_setcustomsettings"></a>MIP_CC_PolicyProfileSettings_SetCustomSettings

Configura le impostazioni personalizzate, usate per il controllo e il controllo delle funzionalità.

**Parametri**

Parametro | Description
|---|---|
| impostazioni | Impostazioni profilo |
| customSettings | Coppie chiave/valore di impostazioni personalizzate |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_PolicyProfileSettings_SetCustomSettings(
    const mip_cc_policy_profile_settings settings,
    const mip_cc_dictionary customSettings);
```

## <a name="mip_cc_releasepolicyprofilesettings"></a>MIP_CC_ReleasePolicyProfileSettings

Rilasciare le risorse associate a impostazioni del profilo criteri

**Parametri**

Parametro | Description
|---|---|
| impostazioni | Impostazioni del profilo dei criteri da rilasciare |

```c
void MIP_CC_ReleasePolicyProfileSettings(mip_cc_policy_profile_settings profilsettingseSettings);
```

## <a name="mip_cc_protectbytemplateaction_gettemplateid"></a>MIP_CC_ProtectByTemplateAction_GetTemplateId

Ottiene l'ID modello dell'azione "Proteggi per modello"

**Parametri**

Parametro | Description
|---|---|
| action | azione "Proteggi per modello" |
| templateId | Output ID del modello che definisce le protezioni |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_ProtectByTemplateAction_GetTemplateId(
    const mip_cc_action action,
    mip_cc_guid* templateId);
```

## <a name="mip_cc_removecontentfooteraction_getuielementnames"></a>MIP_CC_RemoveContentFooterAction_GetUIElementNames

Ottiene i nomi degli elementi dell'interfaccia utente dell'azione "Rimuovi piè di pagina contenuto" da rimuovere

**Parametri**

Parametro | Description
|---|---|
| action | azione "Rimuovi piè di pagina contenuto" |
| nomi | Output Nomi degli elementi dell'interfaccia utente da rimuovere, memoria di proprietà del chiamante |

**Return**: codice risultato che indica l'esito positivo o negativo

**Nota**: la variabile ' names ' deve essere rilasciata dal chiamante chiamando MIP_CC_ReleaseStringList 

```c
mip_cc_result MIP_CC_RemoveContentFooterAction_GetUIElementNames(
    const mip_cc_action action,
    mip_cc_string_list* names);
```

## <a name="mip_cc_removecontentheaderaction_getuielementnames"></a>MIP_CC_RemoveContentHeaderAction_GetUIElementNames

Ottiene i nomi degli elementi dell'interfaccia utente dell'azione "Rimuovi intestazione contenuto" da rimuovere

**Parametri**

Parametro | Description
|---|---|
| action | azione "Rimuovi intestazione contenuto" |
| nomi | Output Nomi degli elementi dell'interfaccia utente da rimuovere, memoria di proprietà del chiamante |

**Return**: codice risultato che indica l'esito positivo o negativo

**Nota**: la variabile ' names ' deve essere rilasciata dal chiamante chiamando MIP_CC_ReleaseStringList 

```c
mip_cc_result MIP_CC_RemoveContentHeaderAction_GetUIElementNames(
    const mip_cc_action action,
    mip_cc_string_list* names);
```

## <a name="mip_cc_removewatermarkaction_getuielementnames"></a>MIP_CC_RemoveWatermarkAction_GetUIElementNames

Ottiene i nomi degli elementi dell'interfaccia utente dell'azione "Rimuovi filigrana" da rimuovere

**Parametri**

Parametro | Description
|---|---|
| action | azione "Rimuovi piè di pagina filigrana" |
| nomi | Output Nomi degli elementi dell'interfaccia utente da rimuovere, memoria di proprietà del chiamante |

**Return**: codice risultato che indica l'esito positivo o negativo

**Nota**: la variabile ' names ' deve essere rilasciata dal chiamante chiamando MIP_CC_ReleaseStringList 

```c
mip_cc_result MIP_CC_RemoveWatermarkAction_GetUIElementNames(
    const mip_cc_action action,
    mip_cc_string_list* names);
```

## <a name="mip_cc_releasesensitivitytype"></a>MIP_CC_ReleaseSensitivityType

Rilasciare le risorse associate a un tipo di riservatezza

**Parametri**

Parametro | Description
|---|---|
| sensitivityType | Tipo di riservatezza da rilasciare |

```c
void MIP_CC_ReleaseSensitivityType(mip_cc_sensitivity_type sensitivityType);
```

## <a name="mip_cc_sensitivitytype_getrulepackageidsize"></a>MIP_CC_SensitivityType_GetRulePackageIdSize

Ottiene le dimensioni del buffer necessarie per archiviare l'ID del pacchetto di regole del tipo di riservatezza

**Parametri**

Parametro | Description
|---|---|
| sensitivityType | Tipo di riservatezza |
| idSize | Output Dimensioni del buffer per l'ID del pacchetto della regola (in numero di caratteri) |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_SensitivityType_GetRulePackageIdSize(
    const mip_cc_sensitivity_type sensitivityType,
    int64_t* idSize);
```

## <a name="mip_cc_sensitivitytype_getrulepackageid"></a>MIP_CC_SensitivityType_GetRulePackageId

Ottiene l'ID del pacchetto di regole del tipo di riservatezza

**Parametri**

Parametro | Description
|---|---|
| sensitivityType | Tipo di riservatezza |
| idBuffer | Output Buffer in cui verrà copiato l'ID. |
| idBufferSize | Dimensioni (in numero di caratteri) di idBuffer. |
| actualIdSize | Output Numero di caratteri scritti nel buffer |

**Return**: codice risultato che indica l'esito positivo o negativo

**Nota**: se idBuffer è null o insufficiente, viene restituito MIP_RESULT_ERROR_INSUFFICIENT_BUFFER e actualIdSize viene impostato sulle dimensioni minime del buffer richiesto. 

```c
mip_cc_result MIP_CC_SensitivityType_GetRulePackageId(
    const mip_cc_sensitivity_type sensitivityType,
    char* idBuffer,
    const int64_t idBufferSize,
    int64_t* actualIdSize);
```

## <a name="mip_cc_sensitivitytype_getrulepackagesize"></a>MIP_CC_SensitivityType_GetRulePackageSize

Ottiene le dimensioni del buffer necessarie per archiviare il pacchetto di regole di un tipo di riservatezza

**Parametri**

Parametro | Description
|---|---|
| sensitivityType | Tipo di riservatezza |
| rulePackageSize | Output Dimensioni del buffer per il mantenimento del pacchetto di regole (in numero di caratteri) |

**Return**: codice risultato che indica l'esito positivo o negativo

```c
mip_cc_result MIP_CC_SensitivityType_GetRulePackageSize(
    const mip_cc_sensitivity_type sensitivityType,
    int64_t* rulePackageSize);
```

## <a name="mip_cc_sensitivitytype_getrulepackage"></a>MIP_CC_SensitivityType_GetRulePackage

Ottiene il pacchetto di regole del tipo di riservatezza

**Parametri**

Parametro | Description
|---|---|
| sensitivityType | Tipo di riservatezza |
| rulePackageBuffer | Output Buffer in cui verrà copiato il pacchetto di regole. |
| rulePackageBufferSize | Dimensioni (in numero di caratteri) di rulePackageBuffer. |
| actualRulePackageSize | Output Numero di caratteri scritti nel buffer |

**Return**: codice risultato che indica l'esito positivo o negativo

**Nota**: se rulePackageBuffer è null o insufficiente, viene restituito MIP_RESULT_ERROR_INSUFFICIENT_BUFFER e actualRulePackageSize viene impostato sulle dimensioni minime del buffer richiesto. 

```c
mip_cc_result MIP_CC_SensitivityType_GetRulePackage(
    const mip_cc_sensitivity_type sensitivityType,
    char* rulePackageBuffer,
    const int64_t rulePackageBufferSize,
    int64_t* actualRulePackageSize);
```

