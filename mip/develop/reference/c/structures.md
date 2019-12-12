---
title: Strutture
description: Strutture.
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 11/4/2019
ms.openlocfilehash: aa544dfbd046ae8c3137cbc115d9af6ea219bc07
ms.sourcegitcommit: 474cd033de025bab280cb7a9721ac7ffc2d60b55
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/05/2019
ms.locfileid: "73591610"
---
# <a name="structures"></a>Strutture

## <a name="mip_cc_application_info"></a>mip_cc_application_info

Uno struct che include informazioni specifiche dell'applicazione 

| Campo | Description |
|---|---|
| applicationId | Identificatore dell'applicazione impostato nel portale di AAD, (deve essere un GUID senza parentesi quadre).  |
| applicationName | Nome dell'applicazione, (deve contenere solo caratteri ASCII validi, escluso ';')  |
| applicationVersion | Versione dell'applicazione in uso, (deve contenere solo caratteri ASCII validi, escluso ';')   |


```c
typedef struct {
  const char* applicationId;      
  const char* applicationName;    
  const char* applicationVersion; 
} mip_cc_application_info;

```

## <a name="mip_cc_oauth2_challenge"></a>mip_cc_oauth2_challenge

Informazioni fornite da un server per generare un token OAuth2

| Campo | Description |
|---|---|
| authority | Autorità OAuth2  |
| risorse | Risorsa OAuth2  |
| ambito | Ambito OAuth2  |


```c
typedef struct {
  const char* authority; 
  const char* resource;  
  const char* scope;     
} mip_cc_oauth2_challenge;

```

## <a name="mip_cc_guid"></a>mip_cc_guid

GUID

```c
typedef struct {
  char guid[37];
} mip_cc_guid;

```

## <a name="mip_cc_kv_pair"></a>mip_cc_kv_pair

Coppia chiave/valore

| Campo | Description |
|---|---|
| key | Codice  |
| Valore | Value  |


```c
typedef struct {
  const char* key;   
  const char* value; 
} mip_cc_kv_pair;

```

## <a name="mip_cc_http_header"></a>mip_cc_http_header

Intestazione richiesta/risposta HTTP

| Campo | Description |
|---|---|
| name | Nome/chiave dell'intestazione  |
| Valore | Valore intestazione  |


```c
typedef struct {
  const char* name;  
  const char* value; 
} mip_cc_http_header;

```

## <a name="mip_cc_http_request"></a>mip_cc_http_request

Richiesta HTTP

| Campo | Description |
|---|---|
| ID | ID richiesta univoco: correlato con la stessa proprietà in mip_cc_http_response  |
| tipo | Tipo di richiesta HTTP (ad esempio, GET e POST)  |
| url | URL della richiesta HTTP  |
| bodySize | Dimensioni del corpo della richiesta HTTP in byte  |
| body | Corpo della richiesta HTTP con memorizzazione nel buffer  |
| headersCount | Numero di intestazioni di richiesta HTTP  |
| intestazioni | Buffer contenente intestazioni di richiesta HTTP  |


```c
typedef struct {
  const char* id;                    
  mip_cc_http_request_type type;     
  const char* url;                   
  int64_t bodySize;                  
  const uint8_t* body;               
  int64_t headersCount;              
  const mip_cc_http_header* headers; 
} mip_cc_http_request;

```

## <a name="mip_cc_http_response"></a>mip_cc_http_response

Risposta HTTP

| Campo | Description |
|---|---|
| ID | ID richiesta univoco: correlato con la stessa proprietà in mip_cc_http_request  |
| statusCode | Codice di stato della risposta HTTP  |
| bodySize | Dimensione del corpo della risposta HTTP in byte  |
| body | Corpo della risposta HTTP del buffer  |
| headersCount | Numero di intestazioni di risposta HTTP  |
| intestazioni | Buffer contenente intestazioni di risposta HTTP  |


```c
typedef struct {
  const char* id;                    
  int32_t statusCode;                
  int64_t bodySize;                  
  const uint8_t* body;               
  int64_t headersCount;              
  const mip_cc_http_header* headers; 
} mip_cc_http_response;

```

## <a name="mip_cc_identity"></a>mip_cc_identity

Uno struct che include informazioni specifiche dell'applicazione 

| Campo | Description |
|---|---|
| Posta elettronica | Indirizzo di posta elettronica utente  |


```c
typedef struct {
  const char* email;          
} mip_cc_identity;

```

## <a name="mip_cc_feature_override"></a>mip_cc_feature_override

Definisce lo stato abilitato/disabilitato di una singola funzionalità

| Campo | Description |
|---|---|
| Funzionalità di | Nome funzionalità  |
| Valore | Stato abilitato/disabilitato  |


```c
typedef struct {
  mip_cc_flighting_feature feature; 
  bool value;                       
} mip_cc_feature_override;

```

## <a name="mip_cc_user_rights"></a>mip_cc_user_rights

Un gruppo di utenti e i diritti associati

| Campo | Description |
|---|---|
| utenti | Elenco di utenti  |
| usersCount | Numero di utenti  |
| diritti | Elenco dei diritti  |
| rightsCount | Numero di diritti  |


```c
typedef struct {
  const char** users;  
  int64_t usersCount;  
  const char** rights; 
  int64_t rightsCount; 
} mip_cc_user_rights;

```

## <a name="mip_cc_user_roles"></a>mip_cc_user_roles

Un gruppo di utenti e i ruoli associati

| Campo | Description |
|---|---|
| utenti | Elenco di utenti  |
| usersCount | Numero di utenti  |
| roles | Elenco dei ruoli  |
| rolesCount | Numero di ruoli  |


```c
typedef struct {
  const char** users;  
  int64_t usersCount;  
  const char** roles; 
  int64_t rolesCount; 
} mip_cc_user_roles;

```

## <a name="mip_cc_async_task"></a>mip_cc_async_task

Definisce una singola richiesta di invio di attività asincrona

| Campo | Description |
|---|---|
| ID | ID attività  |
| delayMs | Ritardo fino all'esecuzione dell'attività (in millisecondi)  |
| executeOnIndependentThread | Indica se l'attività deve essere eseguita in un thread completamente indipendente o se può riutilizzare un thread condiviso  |


```c
typedef struct {
  const char* id;                   
  int64_t delayMs;                  
  bool executeOnIndependentThread;  
} mip_cc_async_task;

```

## <a name="mip_cc_application_action_state"></a>mip_cc_application_action_state

Rappresenta lo stato corrente dell'applicazione durante l'esecuzione di un'operazione correlata all'etichetta

| Campo | Description |
|---|---|
| actionState | Descrive se/in che modo un'applicazione tenta di modificare lo stato dell'etichetta.  |
| newLabel | Se ' actionType ' è' UPDATE ': nuova etichetta.  |
| newLabelExtendedProperties | Se ' actionType ' è' UPDATE ': proprietà aggiuntive da scrivere nei metadati.  |
| newLabelAssignementMethod | Se ' actionType ' è' UPDATE ': il metodo di assegnazione della nuova etichetta.  |
| isDowngradeJustified | Se ' actionType ' è' UPDATE ': indica se il downgrade di un'etichetta è stato giustificato dall'utente.  |
| downgradeJustification | Se ' actionType ' è' UPDATE ': testo per la giustificazione del downgrade dell'etichetta fornito dall'utente.  |
| supportedActions | Maschera di enumerazione che descrive le azioni correlate all'etichetta che un'applicazione è in grado di eseguire.  |


```c
typedef struct {
  mip_cc_label_action_state actionState;                    
  mip_cc_label newLabel;                                    
  mip_cc_dictionary newLabelExtendedProperties;             
  mip_cc_label_assignment_method newLabelAssignementMethod; 
  bool isDowngradeJustified;                                
  const char* downgradeJustification;                       
  mip_cc_label_action_type supportedActions;                
} mip_cc_application_action_state;

```

## <a name="mip_cc_document_state"></a>mip_cc_document_state

Rappresenta lo stato corrente di un documento in grado di riconoscere le etichette.

| Campo | Description |
|---|---|
| contentId | Descrizione del documento leggibile visibile nel portale di controllo dei tenant. Esempio per un file: [percorso\nomefile]; esempio per un messaggio di posta elettronica: [Subject: sender]. |
| DataState | Stato dei dati del documento che interagisce con l'applicazione  |
| contentMetadataCallback | Callback dei metadati del documento  |
| protectionDescriptor | Descrittore di protezione se il documento è attualmente protetto; in caso contrario, null  |
| contentFormat | Formato del documento (file e indirizzo di posta elettronica)  |
| auditMetadata | Metadati facoltativi specifici dell'applicazione usati quando si inviano report di controllo. Valori riconosciuti:' sender ': indirizzo di posta elettronica del mittente; ' Recipients ': matrice JSON di destinatari di posta elettronica; ' LastModifiedBy ': indirizzo di posta elettronica dell'utente che ha apportato l'ultima modifica a un documento; ' LastModifiedDate ': data dell'Ultima modifica di un documento. |

```c
typedef struct {
  const char* contentId;
  mip_cc_data_state dataState;
  mip_cc_metadata_callback contentMetadataCallback;
  mip_cc_protection_descriptor protectionDescriptor;
  mip_cc_content_format contentFormat;
  mip_cc_dictionary auditMetadata;
} mip_cc_document_state;