---
title: 'Eseguire la migrazione da AD RMS ad Azure Information Protection: fase 5'
description: Fase 5 della migrazione da AD RMS ad Azure Information Protection che include i passaggi 10 e 12 della migrazione da AD RMS ad Azure Information Protection.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 07/03/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: d51e7bdd-2e5c-4304-98cc-cf2e7858557d
ms.subservice: migration
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: da6ee07bf47e4b392346e719a2c62f00133f498c
ms.sourcegitcommit: 9968a003865ff2456c570cf552f801a816b1db07
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/05/2019
ms.locfileid: "68793925"
---
# <a name="migration-phase-5---post-migration-tasks"></a>Fase 5 della migrazione: attività post-migrazione

>*Si applica a: Active Directory Rights Management Services, [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*


Usare le informazioni seguenti per la fase 5 della migrazione da AD RMS ad Azure Information Protection. Queste procedure illustrano i passaggi 10 e 12 della [Migrazione da AD RMS ad Azure Information Protection](migrate-from-ad-rms-to-azure-rms.md).

## <a name="step-10-deprovision-ad-rms"></a>Passaggio 10. Deprovisioning di AD RMS

rimuovere il punto di connessione del servizio da Active Directory per impedire ai computer di individuare l'infrastruttura Rights Management locale. Questo passaggio è facoltativo per i client esistenti di cui è stata eseguita la migrazione, a seguito del reindirizzamento configurato nel Registro di sistema (ad esempio eseguendo lo script di migrazione). Tuttavia, la rimozione del punto di connessione del servizio impedisce ai nuovi client e potenzialmente ai servizi e agli strumenti correlati a RMS di trovare il punto di connessione del servizio al termine della migrazione, quando tutte le connessioni dovrebbero essere state trasferite al servizio Azure Rights Management. 

Per rimuovere il punto di connessione del servizio, assicurarsi di avere eseguito l'accesso come amministratore aziendale del dominio e quindi seguire questa procedura:

1. Nella console di Active Directory Rights Management Services fare clic con il pulsante destro del mouse sul cluster AD RMS e quindi scegliere **Proprietà**.

2. Fare clic sulla scheda **SCP** .

3. Selezionare la casella di controllo **Cambia SCP** .

4. Selezionare **Rimuovi SCP corrente** e quindi fare clic su **OK**.

Monitorare ora l'attività dei server AD RMS, ad esempio controllando le [richieste nel report di integrità del sistema ](https://technet.microsoft.com/library/ee221012%28v=ws.10%29.aspx) o la [tabella ServiceRequest](https://technet.microsoft.com/library/dd772686%28v=ws.10%29.aspx) oppure [controllando l'accesso utente ai contenuti protetti](https://social.technet.microsoft.com/wiki/contents/articles/3440.ad-rms-frequently-asked-questions-faq.aspx). 

Dopo aver verificato che i client RMS non comunicano più con questi server e che usano Azure Information Protection, è possibile rimuovere il ruolo del server AD RMS da questi server. Se si usano server dedicati, per precauzione è preferibile arrestare innanzitutto i server per un certo periodo di tempo. In questo modo si verifica che non vengano segnalati problemi che potrebbero richiederne il riavvio, così da garantire la continuità del servizio mentre si esaminano i motivi per cui i client non usano Azure Information Protection.

Dopo aver effettuato il deprovisioning dei server AD RMS, è anche possibile esaminare i modelli nel portale di Azure. Ad esempio convertirli in etichette, consolidarli in modo che gli utenti abbiano un elenco ridotto oppure riconfigurarli. Potrebbe anche essere il momento opportuno per pubblicare i modelli predefiniti. Per altre informazioni, vedere [Configurazione e gestione dei modelli per Azure Information Protection](./configure-policy-templates.md).

>[!IMPORTANT]
> Alla fine della migrazione, il cluster AD RMS non può essere usato con Azure Information Protection e con l'opzione HYOK (Hold Your Own Key). Se si decide di usare l'opzione HYOK per un'etichetta di Azure Information Protection, a causa dei reindirizzamenti ora disponibili, il cluster AD RMS in uso deve avere vari URL di gestione licenze per quelli nei cluster migrati.

### <a name="addition-configuration-for-computers-that-run-office-2010"></a>Configurazione aggiuntiva per computer che eseguono Office 2010

Se i client migrati eseguono Office 2010, gli utenti potrebbero riscontrare ritardi nell'apertura di contenuti protetti dopo il deprovisioning dei server AD RMS. In alternativa, gli utenti potrebbero visualizzare messaggi che non dispongono di credenziali per aprire il contenuto protetto. Per risolvere questi problemi, creare un reindirizzamento di rete per questi computer, che reindirizza il nome FQDN dell'URL AD RMS all'indirizzo IP locale del computer (127.0.0.1). È possibile eseguire questa operazione configurando il file hosts locale in ogni computer o usando DNS.

Reindirizzamento tramite il file hosts locale:

- Aggiungere la riga seguente nel file hosts locale, sostituendo `<AD RMS URL FQDN>` con il valore per il cluster di ad RMS, senza prefissi o pagine Web:
    
        127.0.0.1 <AD RMS URL FQDN>

Reindirizzamento tramite DNS:
    
- Creare un nuovo record host (A) per il nome FQDN dell'URL AD RMS, che ha l'indirizzo IP 127.0.0.1.

## <a name="step-11-complete-client-migration-tasks"></a>Passaggio 11. Completare le attività di migrazione dei client

Per i client di dispositivi mobili e i computer Mac: Rimuovere i record SRV in DNS creati al momento della distribuzione dell' [estensione per dispositivo mobile di AD RMS](https://technet.microsoft.com/library/dn673574.aspx).

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

        Connect-AipService

2. Eseguire il comando seguente e immettere **Y** per confermare:

        Set-AipServiceOnboardingControlPolicy -UseRmsUserLicense $False
    
    Si noti che questo comando rimuove qualsiasi applicazione della licenza per il servizio di protezione Azure Rights Management, in modo che tutti i computer possano proteggere documenti e messaggi di posta elettronica.

3. Verificare che i controlli di selezione non siano più impostati:

        Get-AipServiceOnboardingControlPolicy

    Nell'output, **License** deve includere **False** e non c'è nessun GUID visualizzato in **SecurityGroupOjbectId**

Infine, se si usa Office 2010 ed è stata abilitata l'attività **AD RMS Rights Policy Template Management (Automated)** (Gestione modelli di criteri per i diritti di utilizzo AD RMS - Automatizzata) nella libreria dell'Utilità di pianificazione di Windows, disabilitare questa attività perché non viene usata dal client Azure Information Protection. Questa attività viene in genere abilitata tramite Criteri di gruppo e supporta una distribuzione AD RMS. È possibile trovare questa attività nella posizione seguente: **Microsoft** > **Windows** > **Active Directory Rights Management Services Client**

## <a name="step-12-rekey-your-azure-information-protection-tenant-key"></a>Passaggio 12. Reimpostare la chiave del tenant di Azure Information Protection

Questo passaggio è obbligatorio al termine della migrazione se la distribuzione di AD RMS usa la modalità di crittografia 1 di RMS perché questa modalità usa una chiave a 1024 bit e SHA-1. Questa configurazione viene considerata per offrire un livello di protezione inadeguato. Microsoft non approva l'uso di lunghezze di chiave inferiori, ad esempio chiavi RSA a 1024 bit e l'utilizzo associato di protocolli che offrono livelli di protezione inadeguati, ad esempio SHA-1.

La reimpostazione della reimpostazione dei risultati comporta la protezione che usa la modalità crittografia 2 di RMS, che restituisce una chiave a 2048 bit e SHA-256. 

Anche se per la distribuzione di AD RMS è stata usata la Modalità crittografia 2, è comunque consigliabile eseguire questo passaggio poiché una nuova chiave consente di proteggere il tenant da possibili violazioni della protezione della chiave di AD RMS.

Quando si reimposta la chiave del tenant di Azure Information Protection (operazione detta anche "rollover della chiave"), la chiave attualmente attiva viene archiviata e Azure Information Protection inizia a usare una chiave diversa specificata dall'utente. Questa nuova chiave può essere una chiave creata in Azure Key Vault o la chiave predefinita creata automaticamente per il tenant.

Il passaggio da una chiave all'altra non avviene immediatamente, ma richiede alcune settimane. Per questo motivo, se si sospetta una violazione della chiave originale, procedere alla reimpostazione non appena la migrazione è completata.

Per reimpostare la chiave del tenant di Azure Information Protection:

- **Se la chiave del tenant è gestita da Microsoft**: Eseguire il cmdlet di PowerShell [set-AipServiceKeyProperties](/powershell/module/aipservice/set-aipservicekeyproperties) e specificare l'identificatore di chiave per la chiave creata automaticamente per il tenant. È possibile identificare il valore da specificare eseguendo il cmdlet [Get-AipServiceKeys](/powershell/module/aipservice/get-aipservicekeys) . La chiave creata automaticamente per il tenant porta la data di creazione meno recente, in modo da poterla identificare usando il comando seguente:
    
        (Get-AipServiceKeys) | Sort-Object CreationTime | Select-Object -First 1

- **Se la chiave del tenant è gestita dall'utente (BYOK)** : In Azure Key Vault ripetere il processo di creazione della chiave per il tenant di Azure Information Protection, quindi eseguire di nuovo il cmdlet [use-AipServiceKeyVaultKey](/powershell/module/aipservice/use-aipservicekeyvaultkey) per specificare l'URI per la nuova chiave. 

Per altre informazioni sulla gestione della chiave del tenant di Azure Information Protection, vedere [Operazioni relative alla chiave del tenant di Azure Information Protection](./operations-tenant-key.md).


## <a name="next-steps"></a>Passaggi successivi

Dopo aver completato la migrazione, rivedere la [guida di orientamento alla distribuzione](deployment-roadmap.md) per identificare eventuali altre attività di distribuzione che può essere necessario eseguire.

