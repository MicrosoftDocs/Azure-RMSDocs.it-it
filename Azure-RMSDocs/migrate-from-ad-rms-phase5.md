---
title: 'Eseguire la migrazione da AD RMS ad Azure Information Protection: fase 5'
description: Fase 5 della migrazione da AD RMS ad Azure Information Protection che include i passaggi 10 e 12 della migrazione da AD RMS ad Azure Information Protection.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 08/22/2018
ms.topic: conceptual
ms.service: information-protection
ms.assetid: d51e7bdd-2e5c-4304-98cc-cf2e7858557d
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: e535295c4393d2d7267174f587fcbbf34fa986b0
ms.sourcegitcommit: d06594550e7ff94b4098a2aa379ef2b19bc6123d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/07/2018
ms.locfileid: "53023873"
---
# <a name="migration-phase-5---post-migration-tasks"></a>Fase 5 della migrazione: attività post-migrazione

>*Si applica a: Active Directory Rights Management Services, [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](http://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*


Usare le informazioni seguenti per la fase 5 della migrazione da AD RMS ad Azure Information Protection. Queste procedure illustrano i passaggi 10 e 12 della [Migrazione da AD RMS ad Azure Information Protection](migrate-from-ad-rms-to-azure-rms.md).

## <a name="step-10-deprovision-ad-rms"></a>Passaggio 10. Deprovisioning di AD RMS

rimuovere il punto di connessione del servizio da Active Directory per impedire ai computer di individuare l'infrastruttura Rights Management locale. Questo passaggio è facoltativo per i client esistenti di cui è stata eseguita la migrazione, a seguito del reindirizzamento configurato nel Registro di sistema (ad esempio eseguendo lo script di migrazione). Tuttavia, la rimozione del punto di connessione del servizio impedisce ai nuovi client e potenzialmente ai servizi e agli strumenti correlati a RMS di trovare il punto di connessione del servizio al termine della migrazione, quando tutte le connessioni dovrebbero essere state trasferite al servizio Azure Rights Management. 

Per rimuovere il punto di connessione del servizio, assicurarsi di avere eseguito l'accesso come amministratore aziendale del dominio e quindi seguire questa procedura:

1. Nella console di Active Directory Rights Management Services fare clic con il pulsante destro del mouse sul cluster AD RMS e quindi scegliere **Proprietà**.

2. Fare clic sulla scheda **SCP** .

3. Selezionare la casella di controllo **Cambia SCP** .

4. Selezionare **Rimuovi SCP corrente** e quindi fare clic su **OK**.

Monitorare ora l'attività dei server AD RMS, ad esempio controllando le [richieste nel report di integrità del sistema ](https://technet.microsoft.com/library/ee221012%28v=ws.10%29.aspx) o la [tabella ServiceRequest](https://technet.microsoft.com/library/dd772686%28v=ws.10%29.aspx) oppure [controllando l'accesso utente ai contenuti protetti](http://social.technet.microsoft.com/wiki/contents/articles/3440.ad-rms-frequently-asked-questions-faq.aspx). 

Dopo aver verificato che i client RMS non comunicano più con questi server e che usano Azure Information Protection, è possibile rimuovere il ruolo del server AD RMS da questi server. Se si usano server dedicati, per precauzione è preferibile arrestare innanzitutto i server per un certo periodo di tempo. In questo modo si verifica che non vengano segnalati problemi che potrebbero richiederne il riavvio, così da garantire la continuità del servizio mentre si esaminano i motivi per cui i client non usano Azure Information Protection.

Dopo aver effettuato il deprovisioning dei server AD RMS, è anche possibile esaminare i modelli nel portale di Azure. Ad esempio convertirli in etichette, consolidarli in modo che gli utenti abbiano un elenco ridotto oppure riconfigurarli. Potrebbe anche essere il momento opportuno per pubblicare i modelli predefiniti. Per altre informazioni, vedere [Configurazione e gestione dei modelli per Azure Information Protection](./configure-policy-templates.md).

>[!IMPORTANT]
> Alla fine della migrazione, il cluster AD RMS non può essere usato con Azure Information Protection e con l'opzione HYOK (Hold Your Own Key). Se si decide di usare l'opzione HYOK per un'etichetta di Azure Information Protection, a causa dei reindirizzamenti ora disponibili, il cluster AD RMS in uso deve avere vari URL di gestione licenze per quelli nei cluster migrati.

## <a name="step-11-complete-client-migration-tasks"></a>Passaggio 11. Completare le attività di migrazione dei client

Per client dispositivo mobili e computer MAC: rimuovere i record DNS SRV creati al momento della distribuzione dell'[estensione per dispositivo mobile di AD RMS](https://technet.microsoft.com/library/dn673574.aspx).

Dopo che queste modifiche DNS sono state propagate, questi client individueranno e inizieranno a usare automaticamente il servizio Azure Rights Management. I computer Mac che eseguono Mac Office memorizzano invece le informazioni nella cache di AD RMS. Per questi computer, questo processo può durare fino a 30 giorni. 

Per forzare i computer Mac a eseguire immediatamente il processo di individuazione, cercare "adal" nel keychain ed eliminare tutte le voci ADAL. Eseguire poi i comandi seguenti in questi computer:

````

rm -r ~/Library/Cache/MSRightsManagement

rm -r ~/Library/Caches/com.microsoft.RMS-XPCService

rm -r ~/Library/Caches/Microsoft\ Rights\ Management\ Services

rm -r ~/Library/Containers/com.microsoft.RMS-XPCService

rm -r ~/Library/Containers/com.microsoft.RMSTestApp

rm ~/Library/Group\ Containers/UBF8T346G9.Office/DRM.plist

killall cfprefsd

````

Dopo che tutti i computer Windows esistenti sono stati migrati in Azure Information Protection, non c'è nessun motivo per continuare a usare i controlli di onboarding e mantenere il gruppo **AIPMigrated** creato per il processo di migrazione. 

Rimuovere prima i controlli di onboarding ed eliminare poi il gruppo **AIPMigrated** e qualsiasi metodo di distribuzione software creato per distribuire gli script di migrazione.

Per rimuovere i controlli di onboarding:

1. In una sessione di PowerShell, connettersi al servizio Azure Rights Management e, quando richiesto, specificare le credenziali di amministratore globale:

        Connect-Aadrmservice

2. Eseguire il comando seguente e immettere **Y** per confermare:

        Set-AadrmOnboardingControlPolicy -UseRmsUserLicense $False
    
    Si noti che questo comando rimuove qualsiasi applicazione della licenza per il servizio di protezione Azure Rights Management, in modo che tutti i computer possano proteggere documenti e messaggi di posta elettronica.

3. Verificare che i controlli di selezione non siano più impostati:

        Get-AadrmOnboardingControlPolicy

    Nell'output, **License** deve includere **False** e non c'è nessun GUID visualizzato in **SecurityGroupOjbectId**

Infine, se si usa Office 2010 ed è stata abilitata l'attività **AD RMS Rights Policy Template Management (Automated)** (Gestione modelli di criteri per i diritti di utilizzo AD RMS - Automatizzata) nella libreria dell'Utilità di pianificazione di Windows, disabilitare questa attività perché non viene usata dal client Azure Information Protection. Questa attività viene in genere abilitata tramite Criteri di gruppo e supporta una distribuzione AD RMS. È possibile trovare questa attività nel seguente percorso: **Microsoft** > **Windows** > **Client Microsoft Active Directory Rights Management Services**

## <a name="step-12-rekey-your-azure-information-protection-tenant-key"></a>Passaggio 12. Reimpostare la chiave del tenant di Azure Information Protection

Questo passaggio è consigliato al termine della migrazione, se per la distribuzione di AD RMS è stata usata la Modalità crittografia 1 di RMS. La reimpostazione delle chiavi dà come risultato una protezione che usa la Modalità di crittografia 2 di RMS. 

Anche se per la distribuzione di AD RMS è stata usata la Modalità crittografia 2, è comunque consigliabile eseguire questo passaggio poiché una nuova chiave consente di proteggere il tenant da possibili violazioni della protezione della chiave di AD RMS.

Quando si reimposta la chiave del tenant di Azure Information Protection (operazione detta anche "rollover della chiave"), la chiave attualmente attiva viene archiviata e Azure Information Protection inizia a usare una chiave diversa specificata dall'utente. Questa nuova chiave può essere una chiave creata in Azure Key Vault o la chiave predefinita creata automaticamente per il tenant.

Il passaggio da una chiave all'altra non avviene immediatamente, ma richiede alcune settimane. Per questo motivo, se si sospetta una violazione della chiave originale, procedere alla reimpostazione non appena la migrazione è completata.

Per reimpostare la chiave del tenant di Azure Information Protection:

- **Se la chiave del tenant è gestita da Microsoft**: eseguire il cmdlet PowerShell [Set-AadrmKeyProperties](/powershell/module/aadrm/set-aadrmkeyproperties) e specificare l'identificatore per la chiave creata automaticamente per il tenant. È possibile identificare il valore da specificare eseguendo il cmdlet [Get-AadrmKeys](/powershell/module/aadrm/get-aadrmkeys). La chiave creata automaticamente per il tenant porta la data di creazione meno recente, in modo da poterla identificare usando il comando seguente:
    
        (Get-AadrmKeys) | Sort-Object CreationTime | Select-Object -First 1

- **Se la chiave del tenant è gestita dall'utente (BYOK):** in Azure Key Vault ripetere il processo di creazione della chiave che si sta usando per il tenant di Azure Information Protection, quindi eseguire nuovamente il cmdlet [Use-AadrmKeyVaultKey](/powershell/aadrm/vlatest/use-aadrmkeyvaultkey) per specificare l'URI della nuova chiave. 

Per altre informazioni sulla gestione della chiave del tenant di Azure Information Protection, vedere [Operazioni relative alla chiave del tenant di Azure Information Protection](./operations-tenant-key.md).


## <a name="next-steps"></a>Passaggi successivi

Dopo aver completato la migrazione, rivedere la [guida di orientamento alla distribuzione](deployment-roadmap.md) per identificare eventuali altre attività di distribuzione che può essere necessario eseguire.

