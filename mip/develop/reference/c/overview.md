---
title: Guida di riferimento a MIP SDK per C
description: Guida di riferimento a MIP SDK per C
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 11/4/2019
ms.openlocfilehash: 0187739b1f37a23051dbf6c3ddde8e992757f088
ms.sourcegitcommit: 474cd033de025bab280cb7a9721ac7ffc2d60b55
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/05/2019
ms.locfileid: "73592122"
---
# <a name="mip-sdk-for-c-reference"></a>Guida di riferimento a MIP SDK per C

Microsoft Information Protection (MIP) SDK per C consente agli sviluppatori di gestire e applicare i criteri di protezione dei dati ai dati e ad altre risorse digitali.

Il MIP SDK per C include

- [Enumerazioni](enumerations.md)
- [Strutture](structures.md)
- Le funzioni seguenti:

Function | Breve descrizione |
|---|---|
| [mip_cc_auth_callback](functions.md#mip_cc_auth_callback) | definizione della funzione di callback per l'acquisizione del token OAuth2 |
| [mip_cc_consent_callback](functions.md#mip_cc_consent_callback) | definizione della funzione di callback per il consenso dell'utente per l'accesso all'endpoint del servizio esterno |
| [MIP_CC_CreateDictionary](functions.md#mip_cc_createdictionary) | Creare un dizionario di chiavi/valori stringa |
| [MIP_CC_Dictionary_GetEntries](functions.md#mip_cc_dictionary_getentries) | Ottenere le coppie chiave/valore che compongono un dizionario |
| [MIP_CC_ReleaseDictionary](functions.md#mip_cc_releasedictionary) | Rilasciare le risorse associate a un dizionario |
| [mip_cc_http_send_callback_fn](functions.md#mip_cc_http_send_callback_fn) | Definizione della funzione di callback per l'emissione di una richiesta HTTP |
| [mip_cc_http_cancel_callback_fn](functions.md#mip_cc_http_cancel_callback_fn) | Definizione della funzione di callback per l'annullamento di una richiesta HTTP |
| [MIP_CC_CreateHttpDelegate](functions.md#mip_cc_createhttpdelegate) | Crea un delegato HTTP che può essere usato per eseguire l'override dello stack HTTP predefinito di MIP |
| [MIP_CC_NotifyHttpDelegateResponse](functions.md#mip_cc_notifyhttpdelegateresponse) | Notifica a un delegato HTTP che una risposta HTTP è pronta |
| [MIP_CC_ReleaseHttpDelegate](functions.md#mip_cc_releasehttpdelegate) | Rilasciare le risorse associate a un handle del delegato HTTP |
| [mip_cc_logger_init_callback_fn](functions.md#mip_cc_logger_init_callback_fn) | Definizione della funzione di callback per l'inizializzazione del logger |
| [mip_cc_logger_write_callback_fn](functions.md#mip_cc_logger_write_callback_fn) | Definizione della funzione di callback per la scrittura di un'istruzione log |
| [MIP_CC_CreateLoggerDelegate](functions.md#mip_cc_createloggerdelegate) | Crea un delegato del logger che può essere usato per eseguire l'override del logger predefinito di MIP |
| [MIP_CC_ReleaseLoggerDelegate](functions.md#mip_cc_releaseloggerdelegate) | Rilasciare le risorse associate a un handle del delegato del logger |
| [MIP_CC_CreateMipContext](functions.md#mip_cc_createmipcontext) | Creare un contesto MIP per gestire lo stato condiviso tra tutte le istanze del profilo |
| [MIP_CC_CreateMipContextWithCustomFeatureSettings](functions.md#mip_cc_createmipcontextwithcustomfeaturesettings) | Creare un contesto MIP per gestire lo stato condiviso tra tutte le istanze del profilo |
| [MIP_CC_ReleaseMipContext](functions.md#mip_cc_releasemipcontext) | Rilascia le risorse associate a un contesto MIP |
| [MIP_CC_ProtectionDescriptor_GetProtectionType](functions.md#mip_cc_protectiondescriptor_getprotectiontype) | Ottiene il tipo di protezione, indipendentemente dal fatto che sia definito da un modello RMS |
| [MIP_CC_ProtectionDescriptor_GetOwnerSize](functions.md#mip_cc_protectiondescriptor_getownersize) | Ottiene le dimensioni del buffer necessarie per archiviare il proprietario |
| [MIP_CC_ProtectionDescriptor_GetOwner](functions.md#mip_cc_protectiondescriptor_getowner) | Ottiene il proprietario della protezione |
| [MIP_CC_ProtectionDescriptor_GetNameSize](functions.md#mip_cc_protectiondescriptor_getnamesize) | Ottiene le dimensioni del buffer necessarie per archiviare il nome |
| [MIP_CC_ProtectionDescriptor_GetName](functions.md#mip_cc_protectiondescriptor_getname) | Ottiene il nome della protezione |
| [MIP_CC_ProtectionDescriptor_GetDescriptionSize](functions.md#mip_cc_protectiondescriptor_getdescriptionsize) | Ottiene la dimensione del buffer necessaria per archiviare la descrizione |
| [MIP_CC_ProtectionDescriptor_GetDescription](functions.md#mip_cc_protectiondescriptor_getdescription) | Ottiene la descrizione della protezione |
| [MIP_CC_ProtectionDescriptor_GetTemplateId](functions.md#mip_cc_protectiondescriptor_gettemplateid) | Ottiene l'ID modello |
| [MIP_CC_ProtectionDescriptor_GetLabelId](functions.md#mip_cc_protectiondescriptor_getlabelid) | Ottiene l'ID etichetta |
| [MIP_CC_ProtectionDescriptor_GetContentId](functions.md#mip_cc_protectiondescriptor_getcontentid) | Ottiene l'ID contenuto |
| [MIP_CC_ProtectionDescriptor_DoesContentExpire](functions.md#mip_cc_protectiondescriptor_doescontentexpire) | Ottiene un valore che indica se il contenuto ha una data di scadenza |
| [MIP_CC_ProtectionDescriptor_GetContentValidUntil](functions.md#mip_cc_protectiondescriptor_getcontentvaliduntil) | Ottiene l'ora di scadenza della protezione (in secondi da Epoch) |
| [MIP_CC_ProtectionDescriptor_DoesAllowOfflineAccess](functions.md#mip_cc_protectiondescriptor_doesallowofflineaccess) | Ottiene un valore che indica se è consentito o meno l'accesso offline |
| [MIP_CC_ProtectionDescriptor_GetReferrerSize](functions.md#mip_cc_protectiondescriptor_getreferrersize) | Ottiene le dimensioni del buffer necessarie per archiviare il referrer |
| [MIP_CC_ProtectionDescriptor_GetReferrer](functions.md#mip_cc_protectiondescriptor_getreferrer) | Ottiene il referrer di protezione |
| [MIP_CC_ReleaseProtectionDescriptor](functions.md#mip_cc_releaseprotectiondescriptor) | Rilascia le risorse associate a un descrittore di protezione |
| [MIP_CC_CreateStringList](functions.md#mip_cc_createstringlist) | Creare un elenco di stringhe |
| [MIP_CC_StringList_GetStrings](functions.md#mip_cc_stringlist_getstrings) | Ottenere stringhe che compongono un elenco di stringhe |
| [MIP_CC_ReleaseStringList](functions.md#mip_cc_releasestringlist) | Rilasciare le risorse associate a un elenco di stringhe |
| [mip_cc_dispatch_task_callback_fn](functions.md#mip_cc_dispatch_task_callback_fn) | Definizione della funzione di callback per l'invio di un'attività asincrona |
| [mip_cc_cancel_task_callback_fn](functions.md#mip_cc_cancel_task_callback_fn) | Funzione di callback per l'annullamento di un'attività in background |
| [MIP_CC_CreateTaskDispatcherDelegate](functions.md#mip_cc_createtaskdispatcherdelegate) | Crea un delegato del dispatcher di attività che può essere usato per eseguire l'override della gestione delle attività asincrone predefinite di MIP |
| [MIP_CC_ExecuteDispatchedTask](functions.md#mip_cc_executedispatchedtask) | Notifica a un delegato TaskDispatcher che un'attività è pianificata per l'esecuzione nel thread corrente |
| [MIP_CC_ReleaseTaskDispatcherDelegate](functions.md#mip_cc_releasetaskdispatcherdelegate) | Rilasciare le risorse associate a un handle del delegato del dispatcher attività |
| [MIP_CC_TelemetryConfiguration_SetHostName](functions.md#mip_cc_telemetryconfiguration_sethostname) | Impostare un nome host di telemetria che sostituirà le impostazioni di telemetria interne |
| [MIP_CC_TelemetryConfiguration_SetLibraryName](functions.md#mip_cc_telemetryconfiguration_setlibraryname) | Impostare un override della libreria condivisa di telemetria |
| [MIP_CC_TelemetryConfiguration_SetHttpDelegate](functions.md#mip_cc_telemetryconfiguration_sethttpdelegate) | Esegui override dello stack HTTP di telemetria predefinito con il proprio client |
| [MIP_CC_TelemetryConfiguration_SetIsNetworkDetectionEnabled](functions.md#mip_cc_telemetryconfiguration_setisnetworkdetectionenabled) | Indica se il componente di telemetria è autorizzato a eseguire il ping dello stato della rete in un thread in background |
| [MIP_CC_TelemetryConfiguration_SetIsLocalCachingEnabled](functions.md#mip_cc_telemetryconfiguration_setislocalcachingenabled) | Imposta un valore che indica se il componente di telemetria può scrivere le cache sul disco |
| [MIP_CC_TelemetryConfiguration_SetIsTraceLoggingEnabled](functions.md#mip_cc_telemetryconfiguration_setistraceloggingenabled) | Imposta un valore che indica se il componente di telemetria può scrivere i log su disco |
| [MIP_CC_TelemetryConfiguration_SetIsTelemetryOptedOut](functions.md#mip_cc_telemetryconfiguration_setistelemetryoptedout) | Imposta un valore che indica se un'applicazione o un utente ha rifiutato la telemetria facoltativa |
| [MIP_CC_TelemetryConfiguration_SetCustomSettings](functions.md#mip_cc_telemetryconfiguration_setcustomsettings) | Imposta le impostazioni di telemetria personalizzate |
| [MIP_CC_ReleaseTelemetryConfiguration](functions.md#mip_cc_releasetelemetryconfiguration) | Rilascia le risorse associate a impostazioni del profilo di protezione |
| [MIP_CC_ReleaseProtectionEngine](functions.md#mip_cc_releaseprotectionengine) | Rilasciare le risorse associate a un motore di protezione |
| [MIP_CC_ProtectionEngine_CreateProtectionHandlerForPublishing](functions.md#mip_cc_protectionengine_createprotectionhandlerforpublishing) | Crea un gestore protezione per la pubblicazione di nuovo contenuto |
| [MIP_CC_ProtectionEngine_CreateProtectionHandlerForConsumption](functions.md#mip_cc_protectionengine_createprotectionhandlerforconsumption) | Crea un gestore protezione per l'utilizzo del contenuto esistente |
| [MIP_CC_ProtectionEngine_GetEngineIdSize](functions.md#mip_cc_protectionengine_getengineidsize) | Ottiene le dimensioni del buffer necessario per l'ID del motore |
| [MIP_CC_ProtectionEngine_GetEngineId](functions.md#mip_cc_protectionengine_getengineid) | Ottiene l'ID del motore |
| [MIP_CC_ProtectionEngine_GetTemplatesSize](functions.md#mip_cc_protectionengine_gettemplatessize) | Ottiene il numero di modelli RMS associati a un motore di protezione |
| [MIP_CC_ProtectionEngine_GetTemplates](functions.md#mip_cc_protectionengine_gettemplates) | Ottenere la raccolta di modelli disponibili per un utente |
| [MIP_CC_ProtectionEngine_GetRightsForLabelId](functions.md#mip_cc_protectionengine_getrightsforlabelid) | Ottiene l'elenco dei diritti concessi a un utente per un ID etichetta |
| [MIP_CC_ProtectionEngine_GetClientDataSize](functions.md#mip_cc_protectionengine_getclientdatasize) | Ottiene le dimensioni dei dati client associati a un motore di protezione |
| [MIP_CC_ProtectionEngine_GetClientData](functions.md#mip_cc_protectionengine_getclientdata) | Ottenere i dati client associati a un motore di protezione |
| [MIP_CC_CreateProtectionEngineSettingsWithIdentity](functions.md#mip_cc_createprotectionenginesettingswithidentity) | Creare un oggetto impostazioni usato per creare un nuovo motore di protezione |
| [MIP_CC_ProtectionEngineSettings_SetClientData](functions.md#mip_cc_protectionenginesettings_setclientdata) | Imposta i dati client che verranno archiviati in maniera opaca insieme a questo motore e mantengono tra le sessioni |
| [MIP_CC_ProtectionEngineSettings_SetCustomSettings](functions.md#mip_cc_protectionenginesettings_setcustomsettings) | Configura le impostazioni personalizzate, usate per il controllo e il controllo delle funzionalità. |
| [MIP_CC_ProtectionEngineSettings_SetSessionId](functions.md#mip_cc_protectionenginesettings_setsessionid) | Imposta l'ID di sessione che può essere usato per correlare i log e i dati di telemetria |
| [MIP_CC_ProtectionEngineSettings_SetCloudEndpointBaseUrl](functions.md#mip_cc_protectionenginesettings_setcloudendpointbaseurl) | Imposta l'URL di base per tutte le richieste di servizio |
| [MIP_CC_ReleaseProtectionEngineSettings](functions.md#mip_cc_releaseprotectionenginesettings) | Rilasciare le risorse associate a impostazioni del motore di protezione |
| [MIP_CC_CreateProtectionHandlerPublishingSettings](functions.md#mip_cc_createprotectionhandlerpublishingsettings) | Creare un oggetto impostazioni utilizzato per creare un gestore protezione per la pubblicazione di nuovo contenuto |
| [MIP_CC_ProtectionHandlerPublishingSettings_SetIsDeprecatedAlgorithmPreferred](functions.md#mip_cc_protectionhandlerpublishingsettings_setisdeprecatedalgorithmpreferred) | Imposta un valore che indica se è preferibile un algoritmo di crittografia deprecato (BCE) per la compatibilità con le versioni precedenti |
| [MIP_CC_ProtectionHandlerPublishingSettings_SetIsAuditedExtractionAllowed](functions.md#mip_cc_protectionhandlerpublishingsettings_setisauditedextractionallowed) | Imposta un valore che indica se le applicazioni non compatibili con MIP possono aprire contenuto protetto |
| [MIP_CC_ProtectionHandlerPublishingSettings_SetIsPublishingFormatJson](functions.md#mip_cc_protectionhandlerpublishingsettings_setispublishingformatjson) | Imposta un valore che indica se PL è in formato JSON (il valore predefinito è XML) |
| [MIP_CC_ProtectionHandlerPublishingSettings_SetDelegatedUserEmail](functions.md#mip_cc_protectionhandlerpublishingsettings_setdelegateduseremail) | Imposta l'utente delegato |
| [MIP_CC_CreateProtectionHandlerConsumptionSettings](functions.md#mip_cc_createprotectionhandlerconsumptionsettings) | Creare un oggetto impostazioni utilizzato per creare un gestore protezione per l'utilizzo del contenuto esistente |
| [MIP_CC_ProtectionHandlerConsumptionSettings_SetIsOfflineOnly](functions.md#mip_cc_protectionhandlerconsumptionsettings_setisofflineonly) | Imposta un valore che indica se la creazione del gestore protezione consente operazioni HTTP online |
| [MIP_CC_ProtectionHandlerConsumptionSettings_SetDelegatedUserEmail](functions.md#mip_cc_protectionhandlerconsumptionsettings_setdelegateduseremail) | Imposta l'utente delegato |
| [MIP_CC_ProtectionHandler_GetSerializedPublishingLicenseSize](functions.md#mip_cc_protectionhandler_getserializedpublishinglicensesize) | Ottiene le dimensioni della licenza di pubblicazione (in byte) |
| [MIP_CC_ProtectionHandler_GetSerializedPublishingLicense](functions.md#mip_cc_protectionhandler_getserializedpublishinglicense) | Ottiene la licenza di pubblicazione |
| [MIP_CC_ProtectionHandler_GetProtectionDescriptor](functions.md#mip_cc_protectionhandler_getprotectiondescriptor) | Ottiene il descrittore di protezione |
| [MIP_CC_ProtectionHandler_GetRights](functions.md#mip_cc_protectionhandler_getrights) | Ottiene l'elenco dei diritti concessi a un utente |
| [MIP_CC_ProtectionHandler_GetProtectedContentSize](functions.md#mip_cc_protectionhandler_getprotectedcontentsize) | Calcola le dimensioni del contenuto protetto, il factoring nella spaziatura interna e così via. |
| [MIP_CC_ProtectionHandler_GetBlockSize](functions.md#mip_cc_protectionhandler_getblocksize) | Ottiene la dimensione del blocco (in byte) per la modalità di crittografia utilizzata da un gestore di protezione. |
| [MIP_CC_ProtectionHandler_GetIssuedUserSize](functions.md#mip_cc_protectionhandler_getissuedusersize) | Ottiene le dimensioni del buffer necessarie per archiviare l'utente a cui è stato concesso l'accesso al contenuto protetto |
| [MIP_CC_ProtectionHandler_GetIssuedUser](functions.md#mip_cc_protectionhandler_getissueduser) | Ottiene l'utente a cui è stato concesso l'accesso al contenuto protetto |
| [MIP_CC_ProtectionHandler_GetOwnerSize](functions.md#mip_cc_protectionhandler_getownersize) | Ottiene le dimensioni del buffer necessarie per archiviare il proprietario del contenuto protetto |
| [MIP_CC_ProtectionHandler_GetOwner](functions.md#mip_cc_protectionhandler_getowner) | Ottiene il proprietario del contenuto protetto |
| [MIP_CC_ProtectionHandler_GetContentId](functions.md#mip_cc_protectionhandler_getcontentid) | Ottiene il contenuto di IE del contenuto protetto |
| [MIP_CC_ProtectionHandler_DoesUseDeprecatedAlgorithm](functions.md#mip_cc_protectionhandler_doesusedeprecatedalgorithm) | Ottiene un valore che indica se il gestore della protezione utilizza un algoritmo di crittografia deprecato (BCE) per la compatibilità con le versioni precedenti |
| [MIP_CC_ProtectionHandler_DecryptBuffer](functions.md#mip_cc_protectionhandler_decryptbuffer) | Decrittografare un buffer |
| [MIP_CC_ReleaseProtectionHandlerPublishingSettings](functions.md#mip_cc_releaseprotectionhandlerpublishingsettings) | Rilasciare le risorse associate a impostazioni del gestore protezione |
| [MIP_CC_ReleaseProtectionHandlerConsumptionSettings](functions.md#mip_cc_releaseprotectionhandlerconsumptionsettings) | Rilasciare le risorse associate a impostazioni del gestore protezione |
| [MIP_CC_ReleaseProtectionHandler](functions.md#mip_cc_releaseprotectionhandler) | Rilasciare le risorse associate a un gestore protezione |
| [MIP_CC_LoadProtectionProfile](functions.md#mip_cc_loadprotectionprofile) | Carica un profilo |
| [MIP_CC_ReleaseProtectionProfile](functions.md#mip_cc_releaseprotectionprofile) | Rilascia le risorse associate a un profilo di protezione |
| [MIP_CC_ProtectionProfileSettings_SetSessionId](functions.md#mip_cc_protectionprofilesettings_setsessionid) | Imposta l'ID di sessione che può essere usato per correlare i log e i dati di telemetria |
| [MIP_CC_ProtectionProfileSettings_SetCanCacheLicenses](functions.md#mip_cc_protectionprofilesettings_setcancachelicenses) | Configura se le licenze dell'utente finale (contratti) verranno memorizzate nella cache localmente |
| [MIP_CC_ProtectionProfileSettings_SetHttpDelegate](functions.md#mip_cc_protectionprofilesettings_sethttpdelegate) | Esegui override dello stack HTTP predefinito con il proprio client |
| [MIP_CC_ProtectionProfileSettings_SetTaskDispatcherDelegate](functions.md#mip_cc_protectionprofilesettings_settaskdispatcherdelegate) | Esegui override del dispatcher attività asincrono predefinito con il proprio client |
| [MIP_CC_ProtectionProfileSettings_SetCustomSettings](functions.md#mip_cc_protectionprofilesettings_setcustomsettings) | Configura le impostazioni personalizzate, usate per il controllo e il controllo delle funzionalità. |
| [MIP_CC_ReleaseProtectionProfileSettings](functions.md#mip_cc_releaseprotectionprofilesettings) | Rilascia le risorse associate a impostazioni del profilo di protezione |
| [MIP_CC_Action_GetType](functions.md#mip_cc_action_gettype) | Ottiene il tipo di un'azione |
| [MIP_CC_Action_GetId](functions.md#mip_cc_action_getid) | Ottiene l'ID di un'azione |
| [MIP_CC_ActionResult_GetActions](functions.md#mip_cc_actionresult_getactions) | Ottenere azioni che compongono il risultato di un'azione |
| [MIP_CC_ReleaseActionResult](functions.md#mip_cc_releaseactionresult) | Rilasciare le risorse associate al risultato di un'azione |
| [MIP_CC_AddContentFooterAction_GetUIElementNameSize](functions.md#mip_cc_addcontentfooteraction_getuielementnamesize) | Ottiene le dimensioni del buffer necessarie per archiviare il nome dell'elemento dell'interfaccia utente dell'azione "Aggiungi piè di pagina contenuto" |
| [MIP_CC_AddContentFooterAction_GetUIElementName](functions.md#mip_cc_addcontentfooteraction_getuielementname) | Ottiene il nome dell'elemento dell'interfaccia utente dell'azione "Aggiungi piè di pagina contenuto" |
| [MIP_CC_AddContentFooterAction_GetTextSize](functions.md#mip_cc_addcontentfooteraction_gettextsize) | Ottiene le dimensioni del buffer necessarie per archiviare un testo dell'azione "Aggiungi piè di pagina contenuto" |
| [MIP_CC_AddContentFooterAction_GetText](functions.md#mip_cc_addcontentfooteraction_gettext) | Ottiene il testo dell'azione "Aggiungi piè di pagina contenuto" |
| [MIP_CC_AddContentFooterAction_GetFontNameSize](functions.md#mip_cc_addcontentfooteraction_getfontnamesize) | Ottiene le dimensioni del buffer necessarie per archiviare il nome del tipo di carattere dell'azione "Aggiungi piè di pagina contenuto" |
| [MIP_CC_AddContentFooterAction_GetFontName](functions.md#mip_cc_addcontentfooteraction_getfontname) | Ottiene il nome del tipo di carattere dell'azione "Aggiungi piè di pagina contenuto" |
| [MIP_CC_AddContentFooterAction_GetFontSize](functions.md#mip_cc_addcontentfooteraction_getfontsize) | Ottiene le dimensioni del carattere Integer |
| [MIP_CC_AddContentFooterAction_GetFontColorSize](functions.md#mip_cc_addcontentfooteraction_getfontcolorsize) | Ottiene le dimensioni del buffer necessarie per archiviare il colore del carattere dell'azione "Aggiungi piè di pagina contenuto" |
| [MIP_CC_AddContentFooterAction_GetFontColor](functions.md#mip_cc_addcontentfooteraction_getfontcolor) | Ottiene il colore del carattere dell'azione "Aggiungi piè di pagina contenuto" (ad esempio, "#000000") |
| [MIP_CC_AddContentFooterAction_GetAlignment](functions.md#mip_cc_addcontentfooteraction_getalignment) | Ottiene l'allineamento |
| [MIP_CC_AddContentFooterAction_GetMargin](functions.md#mip_cc_addcontentfooteraction_getmargin) | Ottiene le dimensioni del margine |
| [MIP_CC_AddContentHeaderAction_GetUIElementNameSize](functions.md#mip_cc_addcontentheaderaction_getuielementnamesize) | Ottiene le dimensioni del buffer necessarie per archiviare il nome dell'elemento dell'interfaccia utente dell'azione "Aggiungi intestazione contenuto" |
| [MIP_CC_AddContentHeaderAction_GetUIElementName](functions.md#mip_cc_addcontentheaderaction_getuielementname) | Ottiene il nome dell'elemento dell'interfaccia utente dell'azione "Aggiungi intestazione contenuto" |
| [MIP_CC_AddContentHeaderAction_GetTextSize](functions.md#mip_cc_addcontentheaderaction_gettextsize) | Ottiene le dimensioni del buffer necessarie per archiviare il testo dell'azione "Aggiungi intestazione contenuto" |
| [MIP_CC_AddContentHeaderAction_GetText](functions.md#mip_cc_addcontentheaderaction_gettext) | Ottiene il testo dell'azione "Aggiungi intestazione contenuto" |
| [MIP_CC_AddContentHeaderAction_GetFontNameSize](functions.md#mip_cc_addcontentheaderaction_getfontnamesize) | Ottiene le dimensioni del buffer necessarie per archiviare il nome del tipo di carattere dell'azione "Aggiungi intestazione contenuto" |
| [MIP_CC_AddContentHeaderAction_GetFontName](functions.md#mip_cc_addcontentheaderaction_getfontname) | Ottiene il nome del tipo di carattere dell'azione "Aggiungi intestazione contenuto" |
| [MIP_CC_AddContentHeaderAction_GetFontSize](functions.md#mip_cc_addcontentheaderaction_getfontsize) | Ottiene le dimensioni del carattere Integer |
| [MIP_CC_AddContentHeaderAction_GetFontColorSize](functions.md#mip_cc_addcontentheaderaction_getfontcolorsize) | Ottiene le dimensioni del buffer necessarie per archiviare il colore del carattere dell'azione "Aggiungi intestazione contenuto" |
| [MIP_CC_AddContentHeaderAction_GetFontColor](functions.md#mip_cc_addcontentheaderaction_getfontcolor) | Ottiene il colore del carattere dell'azione "Aggiungi intestazione contenuto", ad esempio "#000000". |
| [MIP_CC_AddContentHeaderAction_GetAlignment](functions.md#mip_cc_addcontentheaderaction_getalignment) | Ottiene l'allineamento |
| [MIP_CC_AddContentHeaderAction_GetMargin](functions.md#mip_cc_addcontentheaderaction_getmargin) | Ottiene le dimensioni del margine |
| [MIP_CC_AddWatermarkAction_GetUIElementNameSize](functions.md#mip_cc_addwatermarkaction_getuielementnamesize) | Ottiene le dimensioni del buffer necessarie per archiviare il nome dell'elemento dell'interfaccia utente dell'azione "add watermark" |
| [MIP_CC_AddWatermarkAction_GetUIElementName](functions.md#mip_cc_addwatermarkaction_getuielementname) | Ottiene il nome dell'elemento dell'interfaccia utente dell'azione "Aggiungi filigrana" |
| [MIP_CC_AddWatermarkAction_GetLayout](functions.md#mip_cc_addwatermarkaction_getlayout) | Ottiene il layout della filigrana |
| [MIP_CC_AddWatermarkAction_GetTextSize](functions.md#mip_cc_addwatermarkaction_gettextsize) | Ottiene le dimensioni del buffer necessarie per archiviare il testo dell'azione "Aggiungi filigrana" |
| [MIP_CC_AddWatermarkAction_GetText](functions.md#mip_cc_addwatermarkaction_gettext) | Ottiene il testo dell'azione "Aggiungi filigrana" |
| [MIP_CC_AddWatermarkAction_GetFontNameSize](functions.md#mip_cc_addwatermarkaction_getfontnamesize) | Ottiene le dimensioni del buffer necessarie per archiviare il nome del tipo di carattere dell'azione "Aggiungi filigrana" |
| [MIP_CC_AddWatermarkAction_GetFontName](functions.md#mip_cc_addwatermarkaction_getfontname) | Ottiene il nome del tipo di carattere dell'azione "Aggiungi filigrana" |
| [MIP_CC_AddWatermarkAction_GetFontSize](functions.md#mip_cc_addwatermarkaction_getfontsize) | Ottiene le dimensioni del carattere Integer |
| [MIP_CC_AddWatermarkAction_GetFontColorSize](functions.md#mip_cc_addwatermarkaction_getfontcolorsize) | Ottiene le dimensioni del buffer necessarie per archiviare il colore del carattere dell'azione "Aggiungi filigrana" |
| [MIP_CC_AddWatermarkAction_GetFontColor](functions.md#mip_cc_addwatermarkaction_getfontcolor) | Ottiene il colore del carattere dell'azione "Aggiungi filigrana" (ad esempio, "#000000") |
| [MIP_CC_ReleaseContentLabel](functions.md#mip_cc_releasecontentlabel) | Rilasciare le risorse associate a un'etichetta di contenuto |
| [MIP_CC_ContentLabel_GetCreationTime](functions.md#mip_cc_contentlabel_getcreationtime) | Ottiene l'ora in cui è stata applicata l'etichetta |
| [MIP_CC_ContentLabel_GetAssignmentMethod](functions.md#mip_cc_contentlabel_getassignmentmethod) | Ottiene il metodo di assegnazione dell'etichetta |
| [MIP_CC_ContentLabel_GetExtendedProperties](functions.md#mip_cc_contentlabel_getextendedproperties) | Ottiene le proprietà estese |
| [MIP_CC_ContentLabel_IsProtectionAppliedFromLabel](functions.md#mip_cc_contentlabel_isprotectionappliedfromlabel) | Ottiene un valore che indica se una protezione è stata applicata da un'etichetta. |
| [MIP_CC_ContentLabel_GetLabel](functions.md#mip_cc_contentlabel_getlabel) | Ottiene le proprietà dell'etichetta generica da un'istanza dell'etichetta di contenuto |
| [MIP_CC_CustomAction_GetNameSize](functions.md#mip_cc_customaction_getnamesize) | Ottiene le dimensioni del buffer necessarie per archiviare il nome di un'azione "personalizzata" |
| [MIP_CC_CustomAction_GetName](functions.md#mip_cc_customaction_getname) | Ottiene il nome di un'azione "personalizzata" |
| [MIP_CC_CustomAction_GetProperties](functions.md#mip_cc_customaction_getproperties) | Ottiene le proprietà di un'azione "personalizzata". |
| [mip_cc_metadata_callback](functions.md#mip_cc_metadata_callback) | Definizione della funzione di callback per recuperare il documento metatdata, filtrato in base al nome e al prefisso |
| [MIP_CC_ReleaseLabel](functions.md#mip_cc_releaselabel) | Rilasciare le risorse associate a un'etichetta |
| [MIP_CC_Label_GetId](functions.md#mip_cc_label_getid) | Ottiene l'ID etichetta |
| [MIP_CC_Label_GetNameSize](functions.md#mip_cc_label_getnamesize) | Ottiene le dimensioni del buffer necessarie per archiviare il nome |
| [MIP_CC_Label_GetName](functions.md#mip_cc_label_getname) | Ottiene il nome dell'etichetta |
| [MIP_CC_Label_GetDescriptionSize](functions.md#mip_cc_label_getdescriptionsize) | Ottiene la dimensione del buffer necessaria per archiviare la descrizione |
| [MIP_CC_Label_GetDescription](functions.md#mip_cc_label_getdescription) | Ottiene la descrizione dell'etichetta |
| [MIP_CC_Label_GetColorSize](functions.md#mip_cc_label_getcolorsize) | Ottiene le dimensioni del buffer necessarie per archiviare il colore |
| [MIP_CC_Label_GetColor](functions.md#mip_cc_label_getcolor) | Ottiene il colore dell'etichetta |
| [MIP_CC_Label_GetSensitivity](functions.md#mip_cc_label_getsensitivity) | Ottiene il livello di sensibilità dell'etichetta. Un valore più alto significa più sensibile. |
| [MIP_CC_Label_GetTooltipSize](functions.md#mip_cc_label_gettooltipsize) | Ottiene le dimensioni del buffer necessarie per archiviare la descrizione comando |
| [MIP_CC_Label_GetTooltip](functions.md#mip_cc_label_gettooltip) | Ottiene la descrizione comando dell'etichetta |
| [MIP_CC_Label_GetAutoTooltipSize](functions.md#mip_cc_label_getautotooltipsize) | Ottiene la dimensione del buffer necessaria per archiviare la descrizione comando di classificazione automatica |
| [MIP_CC_Label_GetAutoTooltip](functions.md#mip_cc_label_getautotooltip) | Ottiene la descrizione comando per la classificazione automatica delle etichette |
| [MIP_CC_Label_IsActive](functions.md#mip_cc_label_isactive) | Ottiene un valore che indica se un'etichetta è attiva o meno. |
| [MIP_CC_Label_GetParent](functions.md#mip_cc_label_getparent) | Ottiene l'etichetta padre, se disponibile. |
| [MIP_CC_Label_GetChildrenSize](functions.md#mip_cc_label_getchildrensize) | Ottiene il numero di etichette figlio |
| [MIP_CC_Label_GetChildren](functions.md#mip_cc_label_getchildren) | Ottiene le etichette figlio |
| [MIP_CC_Label_GetCustomSettings](functions.md#mip_cc_label_getcustomsettings) | Ottiene le impostazioni personalizzate definite dal criterio di un'etichetta |
| [MIP_CC_MetadataAction_GetMetadataToRemove](functions.md#mip_cc_metadataaction_getmetadatatoremove) | Ottiene i metadati dell'azione "Metadata" da rimuovere |
| [MIP_CC_MetadataAction_GetMetadataToAdd](functions.md#mip_cc_metadataaction_getmetadatatoadd) | Ottiene i metadati dell'azione "Metadata" da aggiungere |
| [MIP_CC_ReleasePolicyEngine](functions.md#mip_cc_releasepolicyengine) | Rilasciare le risorse associate a un motore dei criteri |
| [MIP_CC_PolicyEngine_GetEngineIdSize](functions.md#mip_cc_policyengine_getengineidsize) | Ottiene le dimensioni del buffer necessario per l'ID del motore |
| [MIP_CC_PolicyEngine_GetEngineId](functions.md#mip_cc_policyengine_getengineid) | Ottiene l'ID del motore |
| [MIP_CC_PolicyEngine_GetMoreInfoUrlSize](functions.md#mip_cc_policyengine_getmoreinfourlsize) | Ottiene le dimensioni dei dati client associati a un motore di criteri |
| [MIP_CC_PolicyEngine_GetMoreInfoUrl](functions.md#mip_cc_policyengine_getmoreinfourl) | Ottenere i dati client associati a un motore dei criteri |
| [MIP_CC_PolicyEngine_IsLabelingRequired](functions.md#mip_cc_policyengine_islabelingrequired) | Ottiene un valore che indica se i criteri stabiliscono che è necessario etichettare un documento. |
| [MIP_CC_PolicyEngine_GetPolicyFileIdSize](functions.md#mip_cc_policyengine_getpolicyfileidsize) | Ottiene le dimensioni dei dati client associati a un motore di criteri |
| [MIP_CC_PolicyEngine_GetPolicyFileId](functions.md#mip_cc_policyengine_getpolicyfileid) | Ottenere i dati client associati a un motore dei criteri |
| [MIP_CC_PolicyEngine_GetSensitivityFileIdSize](functions.md#mip_cc_policyengine_getsensitivityfileidsize) | Ottiene le dimensioni dei dati client associati a un motore di criteri |
| [MIP_CC_PolicyEngine_GetSensitivityFileId](functions.md#mip_cc_policyengine_getsensitivityfileid) | Ottenere i dati client associati a un motore dei criteri |
| [MIP_CC_PolicyEngine_HasClassificationRules](functions.md#mip_cc_policyengine_hasclassificationrules) | Ottiene un valore che indica se il criterio ha regole automatiche o consigliate |
| [MIP_CC_PolicyEngine_GetLastPolicyFetchTime](functions.md#mip_cc_policyengine_getlastpolicyfetchtime) | Ottiene l'ora dell'ultimo recupero dei criteri |
| [MIP_CC_PolicyEngine_GetSensitivityLabelsSize](functions.md#mip_cc_policyengine_getsensitivitylabelssize) | Ottiene il numero di etichette di riservatezza associate al motore dei criteri |
| [MIP_CC_PolicyEngine_GetSensitivityLabels](functions.md#mip_cc_policyengine_getsensitivitylabels) | Ottiene le etichette di riservatezza associate al motore dei criteri |
| [MIP_CC_PolicyEngine_GetLabelById](functions.md#mip_cc_policyengine_getlabelbyid) | Ottiene l'etichetta di riservatezza in base all'ID |
| [MIP_CC_PolicyEngine_GetSensitivityTypesSize](functions.md#mip_cc_policyengine_getsensitivitytypessize) | Ottiene il numero di tipi di riservatezza associati al motore dei criteri. |
| [MIP_CC_PolicyEngine_GetSensitivityTypes](functions.md#mip_cc_policyengine_getsensitivitytypes) | Ottiene i tipi di riservatezza associati al motore dei criteri. |
| [MIP_CC_PolicyEngine_CreatePolicyHandler](functions.md#mip_cc_policyengine_createpolicyhandler) | Creazione di un gestore dei criteri per l'esecuzione di funzioni correlate ai criteri |
| [MIP_CC_PolicyEngine_SendApplicationAuditEvent](functions.md#mip_cc_policyengine_sendapplicationauditevent) | Registra un evento specifico dell'applicazione nella pipeline di controllo |
| [MIP_CC_PolicyEngine_GetPolicyDataXmlSize](functions.md#mip_cc_policyengine_getpolicydataxmlsize) | Ottiene le dimensioni del codice XML dei dati dei criteri |
| [MIP_CC_PolicyEngine_GetPolicyDataXml](functions.md#mip_cc_policyengine_getpolicydataxml) | Ottiene il codice XML dei dati dei criteri |
| [MIP_CC_PolicyEngine_GetSensitivityTypesDataXmlSize](functions.md#mip_cc_policyengine_getsensitivitytypesdataxmlsize) | Ottiene le dimensioni dei dati XML dei tipi di riservatezza |
| [MIP_CC_PolicyEngine_GetSensitivityTypesDataXml](functions.md#mip_cc_policyengine_getsensitivitytypesdataxml) | Ottiene il codice XML di dati dei tipi di riservatezza |
| [MIP_CC_PolicyEngine_GetClientDataSize](functions.md#mip_cc_policyengine_getclientdatasize) | Ottiene le dimensioni dei dati client associati a un motore di criteri |
| [MIP_CC_PolicyEngine_GetClientData](functions.md#mip_cc_policyengine_getclientdata) | Ottenere i dati client associati a un motore dei criteri |
| [MIP_CC_CreatePolicyEngineSettingsWithIdentity](functions.md#mip_cc_createpolicyenginesettingswithidentity) | Creare un oggetto impostazioni usato per creare un nuovo motore dei criteri |
| [MIP_CC_PolicyEngineSettings_SetClientData](functions.md#mip_cc_policyenginesettings_setclientdata) | Imposta i dati client che verranno archiviati in maniera opaca insieme a questo motore e mantengono tra le sessioni |
| [MIP_CC_PolicyEngineSettings_SetCustomSettings](functions.md#mip_cc_policyenginesettings_setcustomsettings) | Configura le impostazioni personalizzate, usate per il controllo e il controllo delle funzionalità. |
| [MIP_CC_PolicyEngineSettings_SetSessionId](functions.md#mip_cc_policyenginesettings_setsessionid) | Imposta l'ID di sessione che può essere usato per correlare i log e i dati di telemetria |
| [MIP_CC_PolicyEngineSettings_SetCloudEndpointBaseUrl](functions.md#mip_cc_policyenginesettings_setcloudendpointbaseurl) | Imposta l'URL di base per tutte le richieste di servizio |
| [MIP_CC_PolicyEngineSettings_SetDelegatedUserEmail](functions.md#mip_cc_policyenginesettings_setdelegateduseremail) | Imposta l'utente delegato |
| [MIP_CC_ReleasePolicyEngineSettings](functions.md#mip_cc_releasepolicyenginesettings) | Rilasciare le risorse associate a impostazioni del motore dei criteri |
| [MIP_CC_ReleasePolicyHandler](functions.md#mip_cc_releasepolicyhandler) | Rilasciare le risorse associate a un gestore dei criteri |
| [MIP_CC_PolicyHandler_GetSensitivityLabel](functions.md#mip_cc_policyhandler_getsensitivitylabel) | Ottiene l'etichetta corrente di un documento |
| [MIP_CC_PolicyHandler_ComputeActions](functions.md#mip_cc_policyhandler_computeactions) | Esegue le regole dei criteri in base allo stato fornito e determina le azioni corrispondenti |
| [MIP_CC_PolicyHandler_NotifyCommittedActions](functions.md#mip_cc_policyhandler_notifycommittedactions) | Chiamata eseguita dall'applicazione dopo l'applicazione delle azioni calcolate e i dati di cui è stato eseguito il commit su disco |
| [MIP_CC_LoadPolicyProfile](functions.md#mip_cc_loadpolicyprofile) | Carica un profilo |
| [MIP_CC_ReleasePolicyProfile](functions.md#mip_cc_releasepolicyprofile) | Rilasciare le risorse associate a un profilo criteri |
| [MIP_CC_PolicyProfileSettings_SetSessionId](functions.md#mip_cc_policyprofilesettings_setsessionid) | Imposta l'ID di sessione che può essere usato per correlare i log e i dati di telemetria |
| [MIP_CC_PolicyProfileSettings_SetHttpDelegate](functions.md#mip_cc_policyprofilesettings_sethttpdelegate) | Esegui override dello stack HTTP predefinito con il proprio client |
| [MIP_CC_PolicyProfileSettings_SetTaskDispatcherDelegate](functions.md#mip_cc_policyprofilesettings_settaskdispatcherdelegate) | Esegui override del dispatcher attività asincrono predefinito con il proprio client |
| [MIP_CC_PolicyProfileSettings_SetCustomSettings](functions.md#mip_cc_policyprofilesettings_setcustomsettings) | Configura le impostazioni personalizzate, usate per il controllo e il controllo delle funzionalità. |
| [MIP_CC_ReleasePolicyProfileSettings](functions.md#mip_cc_releasepolicyprofilesettings) | Rilasciare le risorse associate a impostazioni del profilo criteri |
| [MIP_CC_ProtectByTemplateAction_GetTemplateId](functions.md#mip_cc_protectbytemplateaction_gettemplateid) | Ottiene l'ID modello dell'azione "Proteggi per modello" |
| [MIP_CC_RemoveContentFooterAction_GetUIElementNames](functions.md#mip_cc_removecontentfooteraction_getuielementnames) | Ottiene i nomi degli elementi dell'interfaccia utente dell'azione "Rimuovi piè di pagina contenuto" da rimuovere |
| [MIP_CC_RemoveContentHeaderAction_GetUIElementNames](functions.md#mip_cc_removecontentheaderaction_getuielementnames) | Ottiene i nomi degli elementi dell'interfaccia utente dell'azione "Rimuovi intestazione contenuto" da rimuovere |
| [MIP_CC_RemoveWatermarkAction_GetUIElementNames](functions.md#mip_cc_removewatermarkaction_getuielementnames) | Ottiene i nomi degli elementi dell'interfaccia utente dell'azione "Rimuovi filigrana" da rimuovere |
| [MIP_CC_ReleaseSensitivityType](functions.md#mip_cc_releasesensitivitytype) | Rilasciare le risorse associate a un tipo di riservatezza |
| [MIP_CC_SensitivityType_GetRulePackageIdSize](functions.md#mip_cc_sensitivitytype_getrulepackageidsize) | Ottiene le dimensioni del buffer necessarie per archiviare l'ID del pacchetto di regole del tipo di riservatezza |
| [MIP_CC_SensitivityType_GetRulePackageId](functions.md#mip_cc_sensitivitytype_getrulepackageid) | Ottiene l'ID del pacchetto di regole del tipo di riservatezza |
| [MIP_CC_SensitivityType_GetRulePackageSize](functions.md#mip_cc_sensitivitytype_getrulepackagesize) | Ottiene le dimensioni del buffer necessarie per archiviare il pacchetto di regole di un tipo di riservatezza |
| [MIP_CC_SensitivityType_GetRulePackage](functions.md#mip_cc_sensitivitytype_getrulepackage) | Ottiene il pacchetto di regole del tipo di riservatezza |
