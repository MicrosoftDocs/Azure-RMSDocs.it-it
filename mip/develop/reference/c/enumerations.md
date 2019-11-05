---
title: Enumerazioni
description: Enumerazioni
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 11/4/2019
ms.openlocfilehash: f1ad15819d10bcded670fe519db07667b7e7331e
ms.sourcegitcommit: 7a8eef5eb9d6440c6e2300cb3f264da31061b00d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/05/2019
ms.locfileid: "73591625"
---
# <a name="enumerations"></a>Enumerazioni

## <a name="mip_cc_cache_storage_type"></a>mip_cc_cache_storage_type

Tipo di archiviazione per le cache

| Campo | Description |
|---|---|
|  MIP_CACHE_STORAGE_TYPE_IN_MEMORY = 0         | Archiviazione in memoria  |
|  MIP_CACHE_STORAGE_TYPE_ON_DISK = 1           | Archiviazione su disco  |
|  MIP_CACHE_STORAGE_TYPE_ON_DISK_ENCRYPTED = 2  | Archiviazione su disco con crittografia (se supportata dalla piattaforma)  |


```c
typedef enum {
  MIP_CACHE_STORAGE_TYPE_IN_MEMORY = 0,        
  MIP_CACHE_STORAGE_TYPE_ON_DISK = 1,          
  MIP_CACHE_STORAGE_TYPE_ON_DISK_ENCRYPTED = 2 
} mip_cc_cache_storage_type;

```

## <a name="mip_cc_content_format"></a>mip_cc_content_format

Formato contenuto

| Campo | Description |
|---|---|
|  MIP_CONTENT_FORMAT_DEFAULT = 0  | Formato file standard  |
|  MIP_CONTENT_FORMAT_EMAIL = 1    | Posta elettronica  |


```c
typedef enum {
  MIP_CONTENT_FORMAT_DEFAULT = 0, 
  MIP_CONTENT_FORMAT_EMAIL = 1,   
} mip_cc_content_format;

```

## <a name="mip_cc_label_assignment_method"></a>mip_cc_label_assignment_method

Descrive in che modo viene applicata una nuova etichetta

| Campo | Description |
|---|---|
|  MIP_LABEL_ASSIGNMENT_METHOD_STANDARD = 0    | Le assegnazioni di etichette standard non sostituiranno una precedente assegnazione con privilegi.  |
|  MIP_LABEL_ASSIGNMENT_METHOD_PRIVILEGED = 1  | Un'assegnazione di etichetta con privilegi non verrà sostituita da assegnazioni standard future.  |
|  MIP_LABEL_ASSIGNMENT_METHOD_AUTO = 2        | riservato. Non utilizzare.  |


```c
typedef enum {
  MIP_LABEL_ASSIGNMENT_METHOD_STANDARD = 0,   
  MIP_LABEL_ASSIGNMENT_METHOD_PRIVILEGED = 1, 
  MIP_LABEL_ASSIGNMENT_METHOD_AUTO = 2,       
} mip_cc_label_assignment_method;

```

## <a name="mip_cc_content_mark_alignment"></a>mip_cc_content_mark_alignment

Allineamento per i segni di contenuto (intestazione contenuto o piè di pagina contenuto)

| Campo | Description |
|---|---|
|  MIP_CONTENT_MARK_ALIGNMENT_LEFT = 0    | Il contrassegno del contenuto è allineato a sinistra  |
|  MIP_CONTENT_MARK_ALIGNMENT_RIGHT = 1   | Il contrassegno del contenuto è allineato a destra  |
|  MIP_CONTENT_MARK_ALIGNMENT_CENTER = 2  | Il contrassegno del contenuto è centrato  |


```c
typedef enum {
  MIP_CONTENT_MARK_ALIGNMENT_LEFT = 0,   
  MIP_CONTENT_MARK_ALIGNMENT_RIGHT = 1,  
  MIP_CONTENT_MARK_ALIGNMENT_CENTER = 2, 
} mip_cc_content_mark_alignment;

```

## <a name="mip_cc_watermark_layout"></a>mip_cc_watermark_layout

Layout per le filigrane

| Campo | Description |
|---|---|
|  MIP_WATERMARK_LAYOUT_HORIZONTAL = 0  | Il layout della filigrana è orizzontale  |
|  MIP_WATERMARK_LAYOUT_DIAGONAL = 1    | Il layout della filigrana è diagonale  |


```c
typedef enum {
  MIP_WATERMARK_LAYOUT_HORIZONTAL = 0, 
  MIP_WATERMARK_LAYOUT_DIAGONAL = 1,   
} mip_cc_watermark_layout;

```

## <a name="mip_cc_consent"></a>mip_cc_consent

Risposta di un utente quando viene richiesto il consenso per connettersi a un endpoint di servizio non riconosciuto

| Campo | Description |
|---|---|
|  MIP_CONSENT_ACCEPT_ALWAYS = 0  | Consenso e ricorda questa decisione  |
|  MIP_CONSENT_ACCEPT = 1         | Consenso solo una volta  |
|  MIP_CONSENT_REJECT = 2          | Non fornisce il consenso  |


```c
typedef enum {
  MIP_CONSENT_ACCEPT_ALWAYS = 0, 
  MIP_CONSENT_ACCEPT = 1,        
  MIP_CONSENT_REJECT = 2         
} mip_cc_consent;

```

## <a name="mip_cc_flighting_feature"></a>mip_cc_flighting_feature

Definisce nuove funzionalità in base al nome

| Campo | Description |
|---|---|
|  MIP_FLIGHTING_FEATURE_SERVICE_DISCOVERY = 0      | Utilizzare una chiamata HTTP separata per determinare gli endpoint di servizio RMS (impostazione predefinita false) |
|  MIP_FLIGHTING_FEATURE_AUTH_INFO_CACHE = 1        | Memorizzare nella cache le richieste OAuth2 per dominio/tenant per ridurre le risposte 401 non necessarie. Disabilitare per le app/i servizi che gestiscono la propria autenticazione HTTP (valore predefinito true)  |
|  MIP_FLIGHTING_FEATURE_LINUX_ENCRYPTED_CACHE = 2  | Abilita Caching crittografato per piattaforme Linux (impostazione predefinita false)  |
|  MIP_FLIGHTING_FEATURE_SINGLE_DOMAIN_NAME = 3     | Abilitare il nome della singola società per la ricerca DNS. ad esempio https://corprights  |
|  MIP_FLIGHTING_FEATURE_POLICY_AUTH = 4            | Abilitare l'autenticazione HTTP automatica per le richieste inviate al servizio criteri. Disabilitare per le app/i servizi che gestiscono la propria autenticazione HTTP (valore predefinito true)  |


```c
typedef enum {
  MIP_FLIGHTING_FEATURE_SERVICE_DISCOVERY = 0,     
  MIP_FLIGHTING_FEATURE_AUTH_INFO_CACHE = 1,       
  MIP_FLIGHTING_FEATURE_LINUX_ENCRYPTED_CACHE = 2, 
  MIP_FLIGHTING_FEATURE_SINGLE_DOMAIN_NAME = 3,    
  MIP_FLIGHTING_FEATURE_POLICY_AUTH = 4,           
} mip_cc_flighting_feature;

```

## <a name="mip_cc_http_request_type"></a>mip_cc_http_request_type

Tipo di richiesta HTTP

| Campo | Description |
|---|---|
|  HTTP_REQUEST_TYPE_GET = 0   | HTTP GET  |
|  HTTP_REQUEST_TYPE_POST = 1  | POST HTTP  |


```c
typedef enum {
  HTTP_REQUEST_TYPE_GET = 0,  
  HTTP_REQUEST_TYPE_POST = 1, 
} mip_cc_http_request_type;

```

## <a name="mip_cc_http_result"></a>mip_cc_http_result

Stato di esito positivo/negativo dell'operazione HTTP

| Campo | Description |
|---|---|
|  HTTP_RESULT_OK = 0       | Operazione HTTP completata correttamente  |
|  HTTP_RESULT_FAILURE = 1  | Operazione HTTP non riuscita (ad esempio, timeout, errori di rete e così via)  |


```c
typedef enum {
  HTTP_RESULT_OK = 0,      
  HTTP_RESULT_FAILURE = 1, 
} mip_cc_http_result;

```

## <a name="mip_cc_log_level"></a>mip_cc_log_level

Livello di registrazione

| Campo | Description |
|---|---|
|  MIP_LOG_LEVEL_TRACE = 0   | Trace  |
|  MIP_LOG_LEVEL_INFO        | Informazioni  |
|  MIP_LOG_LEVEL_WARNING     | Avviso  |
|  MIP_LOG_LEVEL_ERROR       | Errore di  |


```c
typedef enum {
  MIP_LOG_LEVEL_TRACE = 0,  
  MIP_LOG_LEVEL_INFO,       
  MIP_LOG_LEVEL_WARNING,    
  MIP_LOG_LEVEL_ERROR,      
} mip_cc_log_level;

```

## <a name="mip_cc_protection_type"></a>mip_cc_protection_type

Descrizione del fatto che la protezione sia definita da un modello o ad hoc

| Campo | Description |
|---|---|
|  MIP_PROTECTION_TYPE_TEMPLATE_BASED = 0  | Basato su un modello RMS  |
|  MIP_PROTECTION_TYPE_CUSTOM = 1          | Protezione personalizzata ad hoc  |


```c
typedef enum {
  MIP_PROTECTION_TYPE_TEMPLATE_BASED = 0, 
  MIP_PROTECTION_TYPE_CUSTOM = 1,         
} mip_cc_protection_type;

```

## <a name="mip_cc_result"></a>mip_cc_result

Esito positivo/negativo API

| Campo | Description |
|---|---|
|  MIP_RESULT_ERROR_UNKNOWN                    | Errore sconosciuto  |
|  MIP_RESULT_ERROR_INSUFFICIENT_BUFFER        | Il buffer fornito dall'applicazione è troppo piccolo  |
|  MIP_RESULT_ERROR_BAD_INPUT                  | Input non valido passato dall'applicazione  |
|  MIP_RESULT_ERROR_FILE_IO_ERROR              | Errore di i/o file generale  |
|  MIP_RESULT_ERROR_NETWORK                    | Errore generale di rete (ad esempio, servizio non raggiungibile)  |
|  MIP_RESULT_ERROR_TRANSIENT_NETWORK          | Errore di rete temporaneo (ad esempio, gateway non valido)  |
|  MIP_RESULT_ERROR_INTERNAL                   | Errore interno imprevisto  |
|  MIP_RESULT_ERROR_JUSTIFICATION_REQUIRED     | Per completare l'azione sul file, è necessario specificare una giustificazione.  |
|  MIP_RESULT_ERROR_NOT_SUPPORTED_OPERATION    | Opeation non è supportato  |
|  MIP_RESULT_ERROR_PRIVILEGED_REQUIRED        | Impossibile eseguire l'override dell'etichetta Privileged quando si usa il metodo standard  |
|  MIP_RESULT_ERROR_ACCESS_DENIED              | L'utente non dispone dei diritti per accedere al servizio  |
|  MIP_RESULT_ERROR_CONSENT_DENIED             | Non è stato concesso il consenso a un'operazione che richiede il consenso dell'utente  |
|  MIP_RESULT_ERROR_POLICY_SYNC                | Tentativo di sincronizzazione dei dati dei criteri non riuscito  |
|  MIP_RESULT_ERROR_NO_PERMISSIONS             | L'utente non è riuscito ad accedere al contenuto (ad esempio, nessuna autorizzazione e contenuto revocato)  |
|  MIP_RESULT_ERROR_NO_AUTH_TOKEN              | L'utente non è riuscito a ottenere l'accesso al contenuto a causa di un token di autenticazione vuoto  |
|  MIP_RESULT_ERROR_SERVICE_DISABLED           | L'utente non è riuscito a ottenere l'accesso al contenuto a causa della disabilitazione del servizio  |
|  MIP_RESULT_ERROR_PROXY_AUTH                 | Autenticazione proxy non riuscita  |
|  MIP_RESULT_ERROR_NO_POLICY                  | Nessun criterio configurato per l'utente/tenant  |
|  MIP_RESULT_ERROR_OPERATION_CANCELLED        | Operazione annullata  |
|  MIP_RESULT_ERROR_ADHOC_PROTECTION_REQUIRED  | È necessario impostare la protezione ad hoc per completare l'azione sul file  |
|  MIP_RESULT_ERROR_DEPRECATED_API             | Il chiamante ha richiamato un'API deprecata  |
|  MIP_RESULT_ERROR_TEMPLATE_NOT_FOUND         | ID modello non riconosciuto  |
|  MIP_RESULT_ERROR_LABEL_NOT_FOUND            | ID etichetta non riconosciuto  |
|  MIP_RESULT_ERROR_LABEL_DISABLED             | Label disabilitato o inattivo  |


```c
typedef enum {
  MIP_RESULT_SUCCESS = 0,

  // MIP C API errors
  MIP_RESULT_ERROR_UNKNOWN,                   
  MIP_RESULT_ERROR_INSUFFICIENT_BUFFER,       

  // MIP C++ exceptions
  MIP_RESULT_ERROR_BAD_INPUT,                 
  MIP_RESULT_ERROR_FILE_IO_ERROR,             
  MIP_RESULT_ERROR_NETWORK,                   
  MIP_RESULT_ERROR_TRANSIENT_NETWORK,         
  MIP_RESULT_ERROR_INTERNAL,                  
  MIP_RESULT_ERROR_JUSTIFICATION_REQUIRED,    
  MIP_RESULT_ERROR_NOT_SUPPORTED_OPERATION,   
  MIP_RESULT_ERROR_PRIVILEGED_REQUIRED,       
  MIP_RESULT_ERROR_ACCESS_DENIED,             
  MIP_RESULT_ERROR_CONSENT_DENIED,            
  MIP_RESULT_ERROR_POLICY_SYNC,               
  MIP_RESULT_ERROR_NO_PERMISSIONS,            
  MIP_RESULT_ERROR_NO_AUTH_TOKEN,             
  MIP_RESULT_ERROR_SERVICE_DISABLED,          
  MIP_RESULT_ERROR_PROXY_AUTH,                
  MIP_RESULT_ERROR_NO_POLICY,                 
  MIP_RESULT_ERROR_OPERATION_CANCELLED,       
  MIP_RESULT_ERROR_ADHOC_PROTECTION_REQUIRED, 
  MIP_RESULT_ERROR_DEPRECATED_API,            
  MIP_RESULT_ERROR_TEMPLATE_NOT_FOUND,        
  MIP_RESULT_ERROR_LABEL_NOT_FOUND,           
  MIP_RESULT_ERROR_LABEL_DISABLED,            
} mip_cc_result;

```

## <a name="mip_cc_action_type"></a>mip_cc_action_type

Maschera di bit del tipo di azione

| Campo | Description |
|---|---|
|  MIP_ACTION_TYPE_ADD_CONTENT_FOOTER = 1 < < 0      | Aggiunge un piè di pagina contenuto al tipo di azione del documento. |
|  MIP_ACTION_TYPE_ADD_CONTENT_HEADER = 1 < < 1      | Aggiunge un'intestazione contenuto al tipo di azione del documento. |
|  MIP_ACTION_TYPE_ADD_WATERMARK = 1 < < 2           | Aggiunge una filigrana al tipo di azione dell'intero documento. |
|  MIP_ACTION_TYPE_CUSTOM = 1 < < 3                  | Tipo di azione definito personalizzato. |
|  MIP_ACTION_TYPE_JUSTIFY = 1 < < 4                 | Tipo di azione di allineamento. |
|  MIP_ACTION_TYPE_METADATA = 1 < < 5                | Tipo di azione di modifica dei metadati. |
|  MIP_ACTION_TYPE_PROTECT_ADHOC = 1 < < 6           | Tipo di azione di protezione con criteri ad hoc. |
|  MIP_ACTION_TYPE_PROTECT_BY_TEMPLATE = 1 < < 7     | Tipo di azione di protezione con modello. |
|  MIP_ACTION_TYPE_PROTECT_DO_NOT_FORWARD = 1 < < 8  | Tipo di azione di protezione senza inoltro. |
|  MIP_ACTION_TYPE_REMOVE_CONTENT_FOOTER = 1 < < 9   | Tipo di azione di rimozione del piè di pagina contenuto. |
|  MIP_ACTION_TYPE_REMOVE_CONTENT_HEADER = 1 < < 10  | Tipo di azione di rimozione dell'intestazione contenuto. |
|  MIP_ACTION_TYPE_REMOVE_PROTECTION = 1 < < 11      | Tipo di azione di rimozione di agenti protezione. |
|  MIP_ACTION_TYPE_REMOVE_WATERMARK = 1 < < 12       | Tipo di azione di rimozione della filigrana. |
|  MIP_ACTION_TYPE_APPLY_LABEL = 1 < < 13            | Tipo di azione di applicazione dell'etichetta. |
|  MIP_ACTION_TYPE_RECOMMEND_LABEL = 1 < < 14        | Tipo di azione di etichetta consigliata. |


```c
typedef enum {
  MIP_ACTION_TYPE_ADD_CONTENT_FOOTER = 1 << 0,     
  MIP_ACTION_TYPE_ADD_CONTENT_HEADER = 1 << 1,     
  MIP_ACTION_TYPE_ADD_WATERMARK = 1 << 2,          
  MIP_ACTION_TYPE_CUSTOM = 1 << 3,                 
  MIP_ACTION_TYPE_JUSTIFY = 1 << 4,                
  MIP_ACTION_TYPE_METADATA = 1 << 5,               
  MIP_ACTION_TYPE_PROTECT_ADHOC = 1 << 6,          
  MIP_ACTION_TYPE_PROTECT_BY_TEMPLATE = 1 << 7,    
  MIP_ACTION_TYPE_PROTECT_DO_NOT_FORWARD = 1 << 8, 
  MIP_ACTION_TYPE_REMOVE_CONTENT_FOOTER = 1 << 9,  
  MIP_ACTION_TYPE_REMOVE_CONTENT_HEADER = 1 << 10, 
  MIP_ACTION_TYPE_REMOVE_PROTECTION = 1 << 11,     
  MIP_ACTION_TYPE_REMOVE_WATERMARK = 1 << 12,      
  MIP_ACTION_TYPE_APPLY_LABEL = 1 << 13,           
  MIP_ACTION_TYPE_RECOMMEND_LABEL = 1 << 14,       
} mip_cc_action_type;

```

## <a name="mip_cc_label_action_state"></a>mip_cc_label_action_state

Descrive le operazioni che l'applicazione sta tentando di eseguire sull'etichetta corrente

| Campo | Description |
|---|---|
|  MIP_LABEL_ACTION_STATE_NO_CHANGE = 0  | L'etichetta corrente non deve essere modificata.  |
|  MIP_LABEL_ACTION_STATE_REMOVE = 1     | L'etichetta corrente deve essere rimossa.  |
|  MIP_LABEL_ACTION_STATE_UPDATE = 2     | L'etichetta corrente deve essere modificata.  |


```c
typedef enum {
  MIP_LABEL_ACTION_STATE_NO_CHANGE = 0, 
  MIP_LABEL_ACTION_STATE_REMOVE = 1,    
  MIP_LABEL_ACTION_STATE_UPDATE = 2,    
} mip_cc_label_action_state;

```

## <a name="mip_cc_label_action_type"></a>mip_cc_label_action_type

Azioni correlate alle etichette che un'applicazione riconosce e supporta

| Campo | Description |
|---|---|
|  MIP_LABEL_ACTION_TYPE_ADD_CONTENT_FOOTER = 1 < < 0      | Aggiunge un piè di pagina contenuto al tipo di azione del documento.  |
|  MIP_LABEL_ACTION_TYPE_ADD_CONTENT_HEADER = 1 < < 1      | Aggiunge un'intestazione contenuto al tipo di azione del documento.  |
|  MIP_LABEL_ACTION_TYPE_ADD_WATERMARK = 1 < < 2           | Aggiunge una filigrana al tipo di azione dell'intero documento.  |
|  MIP_LABEL_ACTION_TYPE_CUSTOM = 1 < < 3                  | Tipo di azione definito personalizzato.  |
|  MIP_LABEL_ACTION_TYPE_JUSTIFY = 1 < < 4                 | Tipo di azione di allineamento.  |
|  MIP_LABEL_ACTION_TYPE_METADATA = 1 < < 5                | Tipo di azione di modifica dei metadati.  |
|  MIP_LABEL_ACTION_TYPE_PROTECT_ADHOC = 1 < < 6           | Tipo di azione di protezione con criteri ad hoc.  |
|  MIP_LABEL_ACTION_TYPE_PROTECT_BY_TEMPLATE = 1 < < 7     | Tipo di azione di protezione con modello.  |
|  MIP_LABEL_ACTION_TYPE_PROTECT_DO_NOT_FORWARD = 1 < < 8  | Tipo di azione di protezione senza inoltro.  |
|  MIP_LABEL_ACTION_TYPE_REMOVE_CONTENT_FOOTER = 1 < < 9   | Tipo di azione di rimozione del piè di pagina contenuto.  |
|  MIP_LABEL_ACTION_TYPE_REMOVE_CONTENT_HEADER = 1 < < 10  | Tipo di azione di rimozione dell'intestazione contenuto.  |
|  MIP_LABEL_ACTION_TYPE_REMOVE_PROTECTION = 1 < < 11      | Tipo di azione di rimozione di agenti protezione.  |
|  MIP_LABEL_ACTION_TYPE_REMOVE_WATERMARK = 1 < < 12       | Tipo di azione di rimozione della filigrana.  |
|  MIP_LABEL_ACTION_TYPE_APPLY_LABEL = 1 < < 13            | Tipo di azione di applicazione dell'etichetta.  |
|  MIP_LABEL_ACTION_TYPE_RECOMMEND_LABEL = 1 < < 14        | Tipo di azione di etichetta consigliata.  |


```c
typedef enum {
  MIP_LABEL_ACTION_TYPE_ADD_CONTENT_FOOTER = 1 << 0,     
  MIP_LABEL_ACTION_TYPE_ADD_CONTENT_HEADER = 1 << 1,     
  MIP_LABEL_ACTION_TYPE_ADD_WATERMARK = 1 << 2,          
  MIP_LABEL_ACTION_TYPE_CUSTOM = 1 << 3,                 
  MIP_LABEL_ACTION_TYPE_JUSTIFY = 1 << 4,                
  MIP_LABEL_ACTION_TYPE_METADATA = 1 << 5,               
  MIP_LABEL_ACTION_TYPE_PROTECT_ADHOC = 1 << 6,          
  MIP_LABEL_ACTION_TYPE_PROTECT_BY_TEMPLATE = 1 << 7,    
  MIP_LABEL_ACTION_TYPE_PROTECT_DO_NOT_FORWARD = 1 << 8, 
  MIP_LABEL_ACTION_TYPE_REMOVE_CONTENT_FOOTER = 1 << 9,  
  MIP_LABEL_ACTION_TYPE_REMOVE_CONTENT_HEADER = 1 << 10, 
  MIP_LABEL_ACTION_TYPE_REMOVE_PROTECTION = 1 << 11,     
  MIP_LABEL_ACTION_TYPE_REMOVE_WATERMARK = 1 << 12,      
  MIP_LABEL_ACTION_TYPE_APPLY_LABEL = 1 << 13,           
  MIP_LABEL_ACTION_TYPE_RECOMMEND_LABEL = 1 << 14,       
} mip_cc_label_action_type;

```

## <a name="mip_cc_data_state"></a>mip_cc_data_state

Definisce lo stato dei dati quando un'applicazione agisce su di essa

| Campo | Description |
|---|---|
|  MIP_DATA_STATE_REST = 0    | Dati inattivi archiviati fisicamente in database/file/warehouse  |
|  MIP_DATA_STATE_MOTION = 1  | Dati che attraversano una rete o che risiedono temporaneamente nella memoria del computer per la lettura o l'aggiornamento  |
|  MIP_DATA_STATE_USE = 2     | Dati attivi con modifiche costanti archiviati fisicamente in database/file/warehouse e così via  |


```c
typedef enum {
  MIP_DATA_STATE_REST = 0,   
  MIP_DATA_STATE_MOTION = 1, 
  MIP_DATA_STATE_USE = 2,    
} mip_cc_data_state;

```

