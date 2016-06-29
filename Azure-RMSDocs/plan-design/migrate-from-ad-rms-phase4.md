---
# required metadata

title: Migrazione da AD RMS ad Azure Rights Management - Fase 4 | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 06/14/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: d51e7bdd-2e5c-4304-98cc-cf2e7858557d


# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Fase 4 della migrazione: attività post-migrazione

*Si applica a: Active Directory Rights Management Services, Azure Rights Management*


Usare le seguenti informazioni per la fase 4 della migrazione da AD RMS ad Azure Rights Management (Azure RMS). Queste procedure illustrano i passaggi 8 e 9 di [Migrazione da AD RMS ad Azure Rights Management](migrate-from-ad-rms-to-azure-rms.md).


## Passaggio 8. Rimuovere le autorizzazioni di AD RMS

Facoltativo: rimuovere il punto di connessione del servizio da Active Directory per impedire ai computer di individuare l'infrastruttura Rights Management locale. Questo passaggio è facoltativo a causa del reindirizzamento configurato nel Registro di sistema, ad esempio eseguendo lo script di migrazione. Per rimuovere il punto di connessione del servizio, usare lo strumento AD SCP Register da [Rights Management Services Administration Toolkit](http://www.microsoft.com/download/details.aspx?id=1479).

Monitorare l'attività dei server AD RMS, ad esempio controllando le [richieste nel report di integrità del sistema ](https://technet.microsoft.com/library/ee221012%28v=ws.10%29.aspx) o la [tabella ServiceRequest](http://technet.microsoft.com/library/dd772686%28v=ws.10%29.aspx) oppure [controllando l'accesso utente ai contenuti protetti](http://social.technet.microsoft.com/wiki/contents/articles/3440.ad-rms-frequently-asked-questions-faq.aspx). Dopo aver verificato che i client RMS non comunicano più con questi server e che usano Azure RMS, è possibile rimuovere il ruolo del server AD RMS da questi server. Se si usano server dedicati, per precauzione è possibile scegliere di arrestare innanzitutto i server per un certo intervallo di tempo per verificare che non vengano segnalati problemi che potrebbero richiederne il riavvio, in modo da garantire la continuità del servizio mentre si esaminano i motivi per cui i client non usano Azure RMS.

Dopo la rimozione delle autorizzazioni dei server AD RMS, è possibile cogliere l'opportunità per esaminare i modelli nel portale di Azure classico e consolidarli in modo che gli utenti ne abbiano meno da scegliere oppure riconfigurarli o eventualmente aggiungerne di nuovi. Potrebbe anche essere il momento opportuno per pubblicare i modelli predefiniti. Per altre informazioni, vedere [Configurazione di modelli personalizzati per Azure Rights Management](../deploy-use/configure-custom-templates.md).

## Passaggio 9. Reimpostare la chiave del tenant di Azure RMS
Questo passaggio è obbligatorio al termine della migrazione se per la distribuzione di AD RMS è stata usata la Modalità crittografia 1 di RMS. La reimpostazione della chiave crea infatti una nuova chiave del tenant che usa la Modalità crittografia 2 di RMS. L'uso di Azure RMS con la Modalità crittografia 1 è supportato solo durante il processo di migrazione.

Questo passaggio è facoltativo ma consigliato al termine della migrazione, anche se è stata usata la Modalità crittografia 2 di RMS, perché consente di proteggere la chiave del tenant di Azure RMS da possibili violazioni della sicurezza della chiave di AD RMS. Quando si reimposta la chiave del tenant di Azure RMS, un'operazione detta anche "rollover della chiave", viene creata una nuova chiave e la chiave originale viene archiviata. Poiché tuttavia il passaggio da una chiave all'altra non avviene immediatamente, ma nell'arco di alcune settimane, evitare di attendere che si sospetti una violazione della chiave originale, ma reimpostare la chiave del tenant di Azure RMS non appena la migrazione è completata.

Per reimpostare la chiave del tenant di Azure RMS:

-   Se la chiave del tenant di Azure RMS è gestita da Microsoft: per eseguire questa operazione, [contattare il supporto Microsoft](../get-started/information-support#to-contact-microsoft-support) e aprire un **caso di supporto relativo ad Azure Rights Management con una richiesta per reimpostare la chiave del tenant di Azure RMS**. È necessario dimostrare di essere un amministratore del tenant di Azure RMS ed essere consapevoli che la conferma di questo processo richiede diversi giorni. Il servizio è soggetto ai costi di supporto standard. La reimpostazione della chiave del tenant non è un servizio di supporto gratuito.

-   Se la chiave del tenant di Azure RMS è gestita dall'utente (BYOK): ripetere la procedura BYOK per generare e creare una nuova chiave tramite Internet o di persona.

Per altre informazioni sulla gestione della chiave del tenant di Azure RMS, vedere [Operazioni relative alla chiave del tenant di Azure Rights Management](../deploy-use/operations-tenant-key.md).

## Passaggi successivi

Dopo aver completato la migrazione, rivedere la [guida di orientamento alla distribuzione](deployment-roadmap.md) per identificare eventuali altre attività di distribuzione che può essere necessario eseguire.



<!--HONumber=Jun16_HO2-->


