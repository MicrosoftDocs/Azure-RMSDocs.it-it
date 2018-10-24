---
title: Classe mip PolicyEngine
description: Riferimento per la classe mip PolicyEngine
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: 57dd325e9c00a3cb2a4056f7ef0b522efef5d0c4
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/28/2018
ms.locfileid: "47446040"
---
# <a name="class-mippolicyengine"></a>Classe mip::PolicyEngine 
Questa classe fornisce un'interfaccia per tutte le funzioni del motore.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
 public const Settings& GetSettings() const  |  Ottiene [Settings](class_mip_policyengine_settings.md) del motore dei criteri.
public const std::vector<std::shared_ptr<Label>>& ListSensitivityLabels()  |  Elenca le etichette di riservatezza associate al motore dei criteri.
 public const std::string& GetMoreInfoUrl() const  |  Fornire un URL per la ricerca di altre informazioni su criteri/etichette.
 public bool IsLabelingRequired() const  |  Controlla se il criterio determina che un documento deve essere o meno etichettato.
public std::shared_ptr<Label> GetDefaultSensitivityLabel()  |  Ottiene l'etichetta di riservatezza predefinita.
public std::shared_ptr<PolicyHandler> CreatePolicyHandler(const std::string& contentIdentifier)  |  Creare un gestore dei criteri per eseguire funzioni relative ai criteri nello stato di esecuzione di un file.
 public void SendApplicationAuditEvent(const std::string& level, const std::string& eventType, const std::string& eventData)  |  Registra un evento specifico dell'applicazione per la pipeline di controllo.
  
## <a name="members"></a>Membri
  
### <a name="settings"></a>Impostazioni
Ottiene [Settings](class_mip_policyengine_settings.md) del motore dei criteri.

  
**Restituisce**: impostazioni del motore dei criteri. 
  
**Vedere anche**: [mip::PolicyEngine::Settings](class_mip_policyengine_settings.md)
  
### <a name="label"></a>Label
Elenca le etichette di riservatezza associate al motore dei criteri.

  
**Restituisce**: elenco di etichette di riservatezza.
  
### <a name="getmoreinfourl"></a>GetMoreInfoUrl
Fornire un URL per la ricerca di altre informazioni su criteri/etichette.

  
**Restituisce**: URL in formato stringa.
  
### <a name="islabelingrequired"></a>IsLabelingRequired
Controlla se il criterio determina che un documento deve essere o meno etichettato.

  
**Restituisce**: true se l'assegnazione di etichette è obbligatoria, in caso contrario false.
  
### <a name="label"></a>Label
Ottiene l'etichetta di riservatezza predefinita.

  
**Restituisce**: etichetta di riservatezza predefinita se esistente, nullptr se non è impostata un'etichetta predefinita.
  
### <a name="policyhandler"></a>PolicyHandler
Creare un gestore dei criteri per eseguire funzioni relative ai criteri nello stato di esecuzione di un file.

Parametri:  
* **contentIdentifier**: identificatore leggibile per il contenuto. Esempio per un file: "C:\mip-sdk-for-cpp\files\audit.docx" [path] esempio per un messaggio di posta elettronica: "RE: Audit design:user1@contoso.com" [Subject:Sender]



  
**Restituisce**: gestore dei criteri.
  
### <a name="sendapplicationauditevent"></a>SendApplicationAuditEvent
Registra un evento specifico dell'applicazione per la pipeline di controllo.

Parametri:  
* **description**: descrizione del livello di log: info/errore/avviso 


* **eventType**: descrizione del tipo di evento 


* **eventData**: dati associati all'evento

