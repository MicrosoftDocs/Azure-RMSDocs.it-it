---
title: Eseguire la migrazione da AD RMS ad Azure Information Protection - Fase 4
description: Fase 4 della migrazione da AD RMS ad Azure Information Protection. Vengono descritti i passaggi 8 e 9 della migrazione da AD RMS ad Azure Information Protection.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 03/08/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: d51e7bdd-2e5c-4304-98cc-cf2e7858557d
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: d36f47e586ac1295dcc79e43a9e061b4c7c7fe1e
ms.sourcegitcommit: 31e128cc1b917bf767987f0b2144b7f3b6288f2e
translationtype: HT
---
# <a name="migration-phase-4---post-migration-tasks"></a>Fase 4 della migrazione: attività post-migrazione

>*Si applica a: Active Directory Rights Management Services, Azure Information Protection, Office 365*


Usare le informazioni seguenti per la fase 4 della migrazione da AD RMS ad Azure Information Protection. Di seguito vengono illustrati i passaggi 8 e 9 dell'operazione descritta in [Migrazione da AD RMS ad Azure Information Protection](migrate-from-ad-rms-to-azure-rms.md).


## <a name="step-8-decommission-ad-rms"></a>Passaggio 8. Rimuovere le autorizzazioni di AD RMS

rimuovere il punto di connessione del servizio da Active Directory per impedire ai computer di individuare l'infrastruttura Rights Management locale. Questo passaggio è facoltativo per i client esistenti di cui è stata eseguita la migrazione, a seguito del reindirizzamento configurato nel Registro di sistema (ad esempio eseguendo lo script di migrazione). Tuttavia, la rimozione del punto di connessione del servizio impedirà ai nuovi client e potenzialmente ai servizi e agli strumenti correlati a RMS di trovare il punto di connessione del servizio al termine della migrazione, quando tutte le connessioni dovrebbero essere state trasferite al servizio Azure Rights Management. 

Per rimuovere il punto di connessione del servizio, assicurarsi di avere eseguito l'accesso come amministratore aziendale del dominio e quindi seguire questa procedura:

1. Nella console di Active Directory Rights Management Services fare clic con il pulsante destro del mouse sul cluster AD RMS e quindi scegliere **Proprietà**.

2. Fare clic sulla scheda **SCP** .

3. Selezionare la casella di controllo **Cambia SCP** .

4. Selezionare **Rimuovi SCP corrente** e quindi fare clic su **OK**.

Monitorare l'attività dei server AD RMS, ad esempio controllando le [richieste nel report di integrità del sistema ](https://technet.microsoft.com/library/ee221012%28v=ws.10%29.aspx) o la [tabella ServiceRequest](http://technet.microsoft.com/library/dd772686%28v=ws.10%29.aspx) oppure [controllando l'accesso utente ai contenuti protetti](http://social.technet.microsoft.com/wiki/contents/articles/3440.ad-rms-frequently-asked-questions-faq.aspx). Dopo aver verificato che i client RMS non comunicano più con questi server e che usano Azure Information Protection, è possibile rimuovere il ruolo del server AD RMS da questi server. Se si usano server dedicati, per precauzione è preferibile arrestare innanzitutto i server per un certo periodo di tempo. In questo modo si verifica che non vengano segnalati problemi che potrebbero richiederne il riavvio, così da garantire la continuità del servizio mentre si esaminano i motivi per cui i client non usano Azure Information Protection.

Dopo la rimozione delle autorizzazioni dei server AD RMS, è possibile cogliere l'opportunità per esaminare i modelli nel portale di Azure classico e consolidarli in modo che gli utenti ne abbiano meno da scegliere oppure riconfigurarli o eventualmente aggiungerne di nuovi. Potrebbe anche essere il momento opportuno per pubblicare i modelli predefiniti. Per altre informazioni, vedere [Configurazione di modelli personalizzati per il servizio Azure Rights Management](../deploy-use/configure-custom-templates.md).

## <a name="step-9-re-key-your-azure-information-protection-tenant-key"></a>Passaggio 9. Reimpostare la chiave del tenant di Azure Information Protection
Questo passaggio è obbligatorio al termine della migrazione se per la distribuzione di AD RMS è stata usata la Modalità crittografia 1 di RMS. La reimpostazione della chiave crea infatti una nuova chiave del tenant che usa la Modalità crittografia 2 di RMS. L'uso di Azure RMS con la Modalità crittografia 1 è supportato solo durante il processo di migrazione.

Questo passaggio è facoltativo ma consigliato al termine della migrazione, anche se è stata usata la Modalità crittografia 2 di RMS. La reimpostazione della chiave in questo scenario consente di proteggere la chiave del tenant di Azure Information Protection da possibili violazioni della sicurezza per la chiave di AD RMS.

Quando si reimposta la chiave del tenant di Azure Information Protection, un'operazione detta anche "rollover della chiave", viene creata una nuova chiave e la chiave originale viene archiviata. Poiché tuttavia il passaggio da una chiave all'altra non avviene immediatamente, ma nell'arco di alcune settimane, evitare di attendere che si sospetti una violazione della chiave originale, ma reimpostare la chiave del tenant di Azure Information Protection non appena la migrazione è completata.

Per reimpostare la chiave del tenant di Azure Information Protection, seguire questa procedura:

- Se la chiave del tenant è gestita da Microsoft, contattare il [supporto tecnico Microsoft](../get-started/information-support.md#to-contact-microsoft-support) e aprire un **caso di supporto relativo ad Azure Information Protection con una richiesta riguardante la reimpostazione della chiave di Azure Information Protection dopo la migrazione da AD RMS**. È necessario dimostrare di essere un amministratore del tenant di Azure Information Protection. Si tenga presente che la conferma di questo processo richiede diversi giorni. Il servizio è soggetto ai costi di supporto standard; la ridistribuzione della chiave del tenant non è un servizio di assistenza gratuito.

- Se la chiave del tenant è gestita dall'utente (BYOK): in Azure Key Vault reimpostare la chiave che si sta usando per il tenant di Azure Information Protection e quindi eseguire nuovamente il cmdlet [Use-AadrmKeyVaultKey](/powershell/aadrm/vlatest/use-aadrmkeyvaultkey) per specificare l'URL della nuova chiave. 

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sulla gestione della chiave del tenant di Azure Information Protection, vedere [Operazioni relative alla chiave del tenant di Azure Rights Management](../deploy-use/operations-tenant-key.md).

Dopo aver completato la migrazione, rivedere la [Guida di orientamento per la distribuzione](deployment-roadmap.md) per identificare eventuali altre attività di distribuzione che può essere necessario eseguire.

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
