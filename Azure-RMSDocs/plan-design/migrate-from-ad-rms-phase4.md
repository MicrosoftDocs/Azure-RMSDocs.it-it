---
title: Migrazione da AD RMS ad Azure Rights Management - Fase 4 | Azure RMS
description: Usare le seguenti informazioni per la fase 4 della migrazione da AD RMS ad Azure Rights Management (Azure RMS). Queste procedure illustrano i passaggi 8 e 9 di Migrazione da AD RMS ad Azure Rights Management.
author: cabailey
manager: mbaldwin
ms.date: 08/17/2016
ms.topic: article
ms.prod: 
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: d51e7bdd-2e5c-4304-98cc-cf2e7858557d
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 26b043f1f9e7a1e0cd00c2f31c28f7d6685f0232
ms.openlocfilehash: dc462c4e710b2be9a1e1501fd7f003674bcf9d12


---

# Fase 4 della migrazione: attività post-migrazione

>*Si applica a: Active Directory Rights Management Services, Azure Rights Management*


Usare le seguenti informazioni per la fase 4 della migrazione da AD RMS ad Azure Rights Management (Azure RMS). Queste procedure illustrano i passaggi 8 e 9 di [Migrazione da AD RMS ad Azure Rights Management](migrate-from-ad-rms-to-azure-rms.md).


## Passaggio 8. Rimuovere le autorizzazioni di AD RMS

Facoltativo: rimuovere il punto di connessione del servizio da Active Directory per impedire ai computer di individuare l'infrastruttura Rights Management locale. Questo passaggio è facoltativo a causa del reindirizzamento configurato nel Registro di sistema, ad esempio eseguendo lo script di migrazione. Per rimuovere il punto di connessione del servizio, usare lo strumento AD SCP Register da [Rights Management Services Administration Toolkit](http://www.microsoft.com/download/details.aspx?id=1479).

Monitorare l'attività dei server AD RMS, ad esempio controllando le [richieste nel report di integrità del sistema ](https://technet.microsoft.com/library/ee221012%28v=ws.10%29.aspx) o la [tabella ServiceRequest](http://technet.microsoft.com/library/dd772686%28v=ws.10%29.aspx) oppure [controllando l'accesso utente ai contenuti protetti](http://social.technet.microsoft.com/wiki/contents/articles/3440.ad-rms-frequently-asked-questions-faq.aspx). Dopo aver verificato che i client RMS non comunicano più con questi server e che usano Azure RMS, è possibile rimuovere il ruolo del server AD RMS da questi server. Se si usano server dedicati, per precauzione è possibile scegliere di arrestare innanzitutto i server per un certo intervallo di tempo per verificare che non vengano segnalati problemi che potrebbero richiederne il riavvio, in modo da garantire la continuità del servizio mentre si esaminano i motivi per cui i client non usano Azure RMS.

Dopo la rimozione delle autorizzazioni dei server AD RMS, è possibile cogliere l'opportunità per esaminare i modelli nel portale di Azure classico e consolidarli in modo che gli utenti ne abbiano meno da scegliere oppure riconfigurarli o eventualmente aggiungerne di nuovi. Potrebbe anche essere il momento opportuno per pubblicare i modelli predefiniti. Per altre informazioni, vedere [Configurazione di modelli personalizzati per Azure Rights Management](../deploy-use/configure-custom-templates.md).

## Passaggio 9. Reimpostare la chiave del tenant di Azure RMS
Questo passaggio è applicabile solo se la topologia della chiave del tenant scelta è gestita da Microsoft anziché dal cliente (BYOK con Insieme di credenziali delle chiavi di Azure).

Questo passaggio è facoltativo, ma consigliato quando la chiave del tenant Azure RMS è gestita da Microsoft ed è stata eseguita la migrazione da AD RMS. La ridistribuzione in questo scenario consente di proteggere la chiave del tenant di Azure RMS da possibili violazioni della sicurezza per la chiave di AD RMS.

Quando si reimposta la chiave del tenant di Azure RMS, un'operazione detta anche "rollover della chiave", viene creata una nuova chiave e la chiave originale viene archiviata. Poiché tuttavia il passaggio da una chiave all'altra non avviene immediatamente, ma nell'arco di alcune settimane, evitare di attendere che si sospetti una violazione della chiave originale, ma reimpostare la chiave del tenant di Azure RMS non appena la migrazione è completata.

Per reimpostare la chiave del tenant di Azure RMS gestita da Microsoft [contattare il supporto tecnico Microsoft](../get-started/information-support.md#to-contact-microsoft-support) e aprire un **caso di supporto relativo ad Azure Rights Management con una richiesta per reimpostare la chiave di Azure RMS dopo la migrazione da AD RMS**. È necessario dimostrare di essere un amministratore del tenant di Azure RMS ed essere consapevoli che la conferma di questo processo richiede diversi giorni. Il servizio è soggetto ai costi di supporto standard. La reimpostazione della chiave del tenant non è un servizio di supporto gratuito.


## Passaggi successivi

Per altre informazioni sulla gestione della chiave del tenant di RMS, vedere [Operazioni relative alla chiave del tenant di Azure Rights Management](../deploy-use/operations-tenant-key.md).

Dopo aver completato la migrazione, rivedere la [guida di orientamento alla distribuzione](deployment-roadmap.md) per identificare eventuali altre attività di distribuzione che può essere necessario eseguire.




<!--HONumber=Aug16_HO4-->


