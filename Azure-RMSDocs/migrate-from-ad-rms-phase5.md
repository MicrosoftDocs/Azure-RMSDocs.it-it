---
title: 'Eseguire la migrazione da AD RMS ad Azure Information Protection: fase 5'
description: Fase 5 della migrazione da AD RMS ad Azure Information Protection che include i passaggi 10 e 12 della migrazione da AD RMS ad Azure Information Protection.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 11/11/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: d51e7bdd-2e5c-4304-98cc-cf2e7858557d
ms.subservice: migration
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin, has-adal-ref
ms.openlocfilehash: fd030502c6d6583e72be63fa424ff8186ebaadc7
ms.sourcegitcommit: af7ac2eeb8f103402c0036dd461c77911fbc9877
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/18/2021
ms.locfileid: "98560306"
---
# <a name="migration-phase-5---post-migration-tasks"></a>Fase 5 della migrazione: attività post-migrazione

>***Si applica a**: Active Directory Rights Management Services, [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*
>
>***Rilevante per**: [Client di etichettatura unificata e client classico di AIP](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

Usare le informazioni seguenti per la fase 5 della migrazione da AD RMS ad Azure Information Protection. Queste procedure illustrano i passaggi 10 e 12 della [Migrazione da AD RMS ad Azure Information Protection](migrate-from-ad-rms-to-azure-rms.md).

## <a name="step-10-deprovision-ad-rms"></a>Passaggio 10. Deprovisioning di AD RMS

rimuovere il punto di connessione del servizio da Active Directory per impedire ai computer di individuare l'infrastruttura Rights Management locale. Questo passaggio è facoltativo per i client esistenti di cui è stata eseguita la migrazione, a seguito del reindirizzamento configurato nel Registro di sistema (ad esempio eseguendo lo script di migrazione). Tuttavia, la rimozione del punto di connessione del servizio impedisce ai nuovi client e potenzialmente ai servizi e agli strumenti correlati a RMS di trovare il punto di connessione del servizio al termine della migrazione, quando tutte le connessioni dovrebbero essere state trasferite al servizio Azure Rights Management.

Per rimuovere il punto di connessione del servizio, assicurarsi di avere eseguito l'accesso come amministratore aziendale del dominio e quindi seguire questa procedura:

1. Nella console di Active Directory Rights Management Services fare clic con il pulsante destro del mouse sul cluster AD RMS e quindi scegliere **Proprietà**.

2. Fare clic sulla scheda **SCP**.

3. Selezionare la casella di controllo **Cambia SCP**.

4. Selezionare **Rimuovi SCP corrente** e quindi fare clic su **OK**.

Monitorare ora l'attività dei server AD RMS, ad esempio controllando le [richieste nel report di integrità del sistema ](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ee221012(v=ws.10)) o la [tabella ServiceRequest](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd772686(v=ws.10)) oppure [controllando l'accesso utente ai contenuti protetti](https://social.technet.microsoft.com/wiki/contents/articles/3440.ad-rms-frequently-asked-questions-faq.aspx).

Dopo aver verificato che i client RMS non comunicano più con questi server e che usano Azure Information Protection, è possibile rimuovere il ruolo del server AD RMS da questi server. Se si usano server dedicati, è possibile che si preferisca arrestare prima di tutto i server per un periodo di tempo. In questo modo si verifica che non vengano segnalati problemi che potrebbero richiederne il riavvio, così da garantire la continuità del servizio mentre si esaminano i motivi per cui i client non usano Azure Information Protection.

Dopo aver effettuato il deprovisioning dei server di AD RMS, è possibile che si desideri esaminare il modello e le etichette. Ad esempio, convertire i modelli in etichette, consolidarli in modo che gli utenti possano scegliere o riconfigurarli. Questo è anche il momento opportuno per pubblicare i modelli predefiniti.

Per le etichette di riservatezza e il client di etichettatura unificata, usare l'interfaccia di amministrazione di assegnazione di etichette, tra cui il Centro sicurezza Microsoft 365, il centro di conformità Microsoft 365 o il Microsoft 365 Security & Compliance Center. Per altre informazioni, vedere la documentazione di Microsoft 365.

Se si usa il client classico, usare il portale di Azure. Per altre informazioni, vedere [Configurazione e gestione dei modelli per Azure Information Protection](./configure-policy-templates.md).

>[!IMPORTANT]
> Al termine di questa migrazione, il cluster di AD RMS non può essere usato con Azure Information Protection e con l'opzione[HYOK](configure-adrms-restrictions.md)(Mantieni la chiave personalizzata). 
>
> Se si usa il client classico con HYOK, a causa dei reindirizzamenti attualmente disponibili, il cluster AD RMS usato deve avere URL di licenza diversi per quelli nei cluster di cui è stata eseguita la migrazione.
>
### <a name="additional-configuration-for-computers-that-run-office-2010"></a>Configurazione aggiuntiva per computer che eseguono Office 2010

> [!IMPORTANT]
> Il supporto esteso per Office 2010 è terminato il 13 ottobre 2020. Per altre informazioni, vedere [AIP e versioni legacy di Windows e Office](known-issues.md#aip-and-legacy-windows-and-office-versions).
> 

Se i client migrati eseguono Office 2010, gli utenti potrebbero riscontrare ritardi nell'apertura di contenuti protetti dopo il deprovisioning dei server di AD RMS. In alternativa, gli utenti potrebbero visualizzare messaggi che non dispongono di credenziali per aprire il contenuto protetto. Per risolvere questi problemi, creare un reindirizzamento di rete per questi computer, che reindirizza il nome FQDN dell'URL AD RMS all'indirizzo IP locale del computer (127.0.0.1). È possibile eseguire questa operazione configurando il file hosts locale in ogni computer o usando DNS.

- **Reindirizzamento tramite il file hosts locale**: aggiungere la riga seguente nel file hosts locale, sostituendo `<AD RMS URL FQDN>` con il valore per il cluster di ad RMS, senza prefissi o pagine Web:

    ```sh
    127.0.0.1 <AD RMS URL FQDN>
    ```

- **Reindirizzamento tramite DNS**: creare un nuovo record host (a) per il nome di dominio completo dell'URL ad RMS, che ha l'indirizzo IP 127.0.0.1.

## <a name="step-11-complete-client-migration-tasks"></a>Passaggio 11. Completare le attività di migrazione dei client

Per client dispositivo mobili e computer MAC: rimuovere i record DNS SRV creati al momento della distribuzione dell'[estensione per dispositivo mobile di AD RMS](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn673574(v=ws.11)).

Quando queste modifiche DNS sono state propagate, questi client verranno automaticamente individuati e inizieranno a usare il servizio Azure Rights Management. I computer Mac che eseguono Mac Office memorizzano invece le informazioni nella cache di AD RMS. Per questi computer, questo processo può durare fino a 30 giorni.

Per forzare i computer Mac a eseguire immediatamente il processo di individuazione, cercare "adal" nel keychain ed eliminare tutte le voci ADAL. Eseguire poi i comandi seguenti in questi computer:

````sh

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

    ```PowerShell
    Connect-AipService

2. Run the following command, and enter **Y** to confirm:

    ```PowerShell
    Set-AipServiceOnboardingControlPolicy -UseRmsUserLicense $False
    ```

    Si noti che questo comando rimuove qualsiasi applicazione della licenza per il servizio di protezione Azure Rights Management, in modo che tutti i computer possano proteggere documenti e messaggi di posta elettronica.

3. Verificare che i controlli di selezione non siano più impostati:

    ```PowerShell    
    Get-AipServiceOnboardingControlPolicy
    ```

    Nell'output, **License** deve includere **False** e non c'è nessun GUID visualizzato in **SecurityGroupOjbectId**

Infine, se si usa Office 2010 ed è stata abilitata l'attività **AD RMS Rights Policy Template Management (Automated)** (Gestione modelli di criteri per i diritti di utilizzo AD RMS - Automatizzata) nella libreria dell'Utilità di pianificazione di Windows, disabilitare questa attività perché non viene usata dal client Azure Information Protection. 

Questa attività viene in genere abilitata tramite Criteri di gruppo e supporta una distribuzione AD RMS. È possibile trovare questa attività nel percorso seguente: **Microsoft**  >  **Windows**  >  **Active Directory Rights Management Services client**. 

> [!IMPORTANT]
> Il supporto esteso per Office 2010 è terminato il 13 ottobre 2020. Per altre informazioni, vedere [AIP e versioni legacy di Windows e Office](known-issues.md#aip-and-legacy-windows-and-office-versions).

## <a name="step-12-rekey-your-azure-information-protection-tenant-key"></a>Passaggio 12. Reimpostare la chiave del tenant di Azure Information Protection

Questo passaggio è obbligatorio al termine della migrazione se la distribuzione di AD RMS usa la modalità di crittografia 1 di RMS perché questa modalità usa una chiave a 1024 bit e SHA-1. Questa configurazione viene considerata per offrire un livello di protezione inadeguato. Microsoft non approva l'uso di lunghezze di chiave inferiori, ad esempio chiavi RSA a 1024 bit e l'utilizzo associato di protocolli che offrono livelli di protezione inadeguati, ad esempio SHA-1.

La reimpostazione della reimpostazione dei risultati comporta la protezione che usa la modalità crittografia 2 di RMS, che restituisce una chiave a 2048 bit e SHA-256.

Anche se per la distribuzione di AD RMS è stata usata la Modalità crittografia 2, è comunque consigliabile eseguire questo passaggio poiché una nuova chiave consente di proteggere il tenant da possibili violazioni della protezione della chiave di AD RMS.

Quando si reimposta la chiave del tenant di Azure Information Protection (operazione detta anche "rollover della chiave"), la chiave attualmente attiva viene archiviata e Azure Information Protection inizia a usare una chiave diversa specificata dall'utente. Questa nuova chiave può essere una chiave creata in Azure Key Vault o la chiave predefinita creata automaticamente per il tenant.

Il passaggio da una chiave all'altra non avviene immediatamente, ma in alcune settimane. Per questo motivo, se si sospetta una violazione della chiave originale, procedere alla reimpostazione non appena la migrazione è completata.

Per reimpostare la chiave del tenant di Azure Information Protection:

- **Se la chiave del tenant è gestita da Microsoft**: eseguire il cmdlet di PowerShell [set-AipServiceKeyProperties](/powershell/module/aipservice/set-aipservicekeyproperties) e specificare l'identificatore di chiave per la chiave creata automaticamente per il tenant. È possibile identificare il valore da specificare eseguendo il cmdlet [Get-AipServiceKeys](/powershell/module/aipservice/get-aipservicekeys) . La chiave creata automaticamente per il tenant porta la data di creazione meno recente, in modo da poterla identificare usando il comando seguente:

        
    ```PowerShell
    (Get-AipServiceKeys) | Sort-Object CreationTime | Select-Object -First 1
    ```

- **Se la chiave del tenant è gestita dall'utente (BYOK)**: in Azure Key Vault, ripetere il processo di creazione della chiave per il tenant di Azure Information Protection, quindi eseguire di nuovo il cmdlet [use-AipServiceKeyVaultKey](/powershell/module/aipservice/use-aipservicekeyvaultkey) per specificare l'URI per la nuova chiave.

Per altre informazioni sulla gestione della chiave del tenant di Azure Information Protection, vedere [Operazioni relative alla chiave del tenant di Azure Information Protection](./operations-tenant-key.md).


## <a name="next-steps"></a>Passaggi successivi

Dopo aver completato la migrazione, vedere la Guida di [orientamento per la distribuzione di AIP per la classificazione, l'assegnazione di etichette e la protezione](deployment-roadmap-classify-label-protect.md) per identificare eventuali altre attività di distribuzione che potrebbero essere necessarie.
