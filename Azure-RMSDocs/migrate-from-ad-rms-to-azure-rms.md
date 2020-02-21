---
title: Eseguire la migrazione da AD RMS ad Azure Information Protection
description: Istruzioni per la migrazione della distribuzione di Active Directory Rights Management Services (AD RMS) ad Azure Information Protection. Dopo la migrazione, gli utenti hanno ancora accesso ai documenti e ai messaggi di posta elettronica che l'organizzazione ha protetto usando AD RMS.
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 1/16/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 828cf1f7-d0e7-4edf-8525-91896dbe3172
ms.subservice: migration
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 7e1ec5241cfedf89b33258115afbc1ee86eae3b3
ms.sourcegitcommit: dd3143537e37951179b932993055a868191719b5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/20/2020
ms.locfileid: "77507638"
---
# <a name="migrating-from-ad-rms-to-azure-information-protection"></a>Migrazione da AD RMS ad Azure Information Protection

>*Si applica a: Active Directory Rights Management Services, [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

Usare il set di istruzioni seguente per la migrazione della distribuzione di Active Directory Rights Management Services (AD RMS) ad Azure Information Protection. 

Dopo la migrazione, i server AD RMS non sono più in uso, ma gli utenti hanno ancora accesso ai documenti e ai messaggi di posta elettronica che l'organizzazione ha protetto con AD RMS. Il contenuto appena protetto userà il sevizio Azure Rights Management (Azure RMS) da Azure Information Protection.

Se non si è certi che questa migrazione di AD RMS sia adatta alla propria organizzazione

- Per un'introduzione ad Azure Information Protection, vedere [Che cos'è Azure Information Protection?](./what-is-information-protection.md)

- Per un confronto tra Azure Information Protection e AD RMS, vedere [Confronto tra Azure Information Protection e AD RMS](./compare-on-premise.md).

## <a name="recommended-reading-before-you-migrate-to-azure-information-protection"></a>Letture consigliate prima di eseguire la migrazione ad Azure Information Protection

Sebbene non sia obbligatorio, può risultare utile leggere la documentazione seguente prima di iniziare la migrazione. Queste informazioni consentono di ottenere una migliore comprensione del funzionamento della tecnologia rilevante per ogni passaggio della migrazione.

- [Pianificazione e implementazione della chiave del tenant di Azure Information Protection](./plan-implement-tenant-key.md): informazioni sulle opzioni di gestione della chiave disponibili per il tenant di Azure Information Protection, in cui l'equivalente della chiave SLC nel cloud è gestita da Microsoft (impostazione predefinita) o dall'utente (configurazione BYOK o "Bring Your Own Key"). 

- [Individuazione del servizio RMS](./rms-client/client-deployment-notes.md#rms-service-discovery): questa sezione delle note sulla distribuzione del client RMS illustra che l'ordine per l'individuazione del servizio è **Registro di sistema**, quindi punto di **connessione del servizio (SCP)** , quindi **cloud**. Durante il processo di migrazione, quando il punto di connessione del servizio è ancora installato, è necessario configurare i client con le impostazioni del Registro di sistema per il tenant di Azure Information Protection, in modo che non usino il cluster AD RMS restituito dal punto di connessione del servizio.

- [Panoramica del connettore Microsoft Rights Management](./deploy-rms-connector.md#overview-of-the-microsoft-rights-management-connector): questa sezione della documentazione sul connettore RMS illustra come i server locali possono connettersi al servizio di Azure Rights Management per proteggere documenti e messaggi di posta elettronica.

Inoltre, se non si ha familiarità con il funzionamento di AD RMS, potrebbe risultare utile leggere il modo in cui funziona [Azure RMS? Dietro le quinte](./how-does-it-work.md) per facilitare l'identificazione dei processi tecnologici identici o diversi per la versione cloud.

## <a name="prerequisites-for-migrating-ad-rms-to-azure-information-protection"></a>Prerequisiti per la migrazione da AD RMS ad Azure Information Protection

Prima di iniziare il processo di migrazione ad Azure Information Protection, verificare che i prerequisiti seguenti siano soddisfatti e accertarsi di avere compreso le possibili limitazioni.

- **Distribuzione di RMS supportata:**
    
  - Le versioni seguenti di AD RMS supportano una migrazione ad Azure Information Protection:
           
      - Windows Server 2012 (x64)
        
      - Windows Server 2012 R2 (x64)
        
      - Windows Server 2016 (x64)
        
  - Sono supportate tutte le topologie di AD RMS valide:
    
      - Singola foresta, singolo cluster RMS
        
      - Singola foresta, più cluster RMS di sola gestione delle licenze
        
      - Più foreste, più cluster RMS
        
    Nota: per impostazione predefinita, viene eseguita la migrazione di più cluster AD RMS a un singolo tenant di Azure Information Protection. Se si vuole separare i tenant per Azure Information Protection, è necessario eseguire migrazioni diverse. Non è possibile importare una chiave da un cluster RMS in più tenant di Azure RMS.

- **Tutti i requisiti per eseguire Azure Information Protection, inclusa una sottoscrizione per Azure Information Protection (il servizio Azure Rights Management non è attivato):**

    Vedere [Requisiti per Azure Information Protection](./requirements.md).

    Si noti che se si dispone di computer che eseguono Office 2010, è necessario installare il [client di Azure Information Protection o il client di assegnazione di etichette unificata Azure Information Protection per gli utenti](faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client), in quanto questi client consentono di autenticare gli utenti nei servizi cloud. Per le versioni successive di Office, questi client sono necessari per la classificazione e l'assegnazione di etichette e il client Azure Information Protection è facoltativo ma consigliato se si vuole proteggere solo i dati. Per ulteriori informazioni, vedere le guide di amministrazione per il [client Azure Information Protection](./rms-client/client-admin-guide.md) e il [client di Azure Information Protection Unified Labeling](./rms-client/clientv2-admin-guide.md).

    Anche se è necessario avere una sottoscrizione per Azure Information Protection per poter eseguire la migrazione da AD RMS, è consigliabile che il servizio Rights Management per il tenant non venga attivato prima di iniziare la migrazione. Il processo di migrazione include questo passaggio di attivazione dopo aver esportato le chiavi e i modelli da AD RMS e averli importati nel tenant per Azure Information Protection. Tuttavia, se il servizio Rights Management è già attivato, è comunque possibile eseguire la migrazione da AD RMS con alcuni passaggi aggiuntivi.


- **Preparazione per Azure Information Protection:**

  - Sincronizzazione della directory tra la directory locale e Azure Active Directory

  - Gruppi abilitati alla posta elettronica in Azure Active Directory

    Vedere [Preparazione di utenti e gruppi per Azure Information Protection](prepare.md).

- **Se è stata usata la funzionalità Information Rights Management (IRM) di Exchange Server** (ad esempio le regole di trasporto e Outlook Web Access) o SharePoint Server con AD RMS:

  - Pianificare un breve intervallo di tempo durante il quale IRM non sarà disponibile in questi server
 
    È possibile continuare a usare IRM in questi server dopo la migrazione. Uno dei passaggi della migrazione consiste tuttavia nel disattivare temporaneamente il servizio IRM, installare e configurare un connettore, riconfigurare i server e quindi riabilitare IRM.

    Questa è la sola interruzione del servizio durante il processo di migrazione.

- **Se si vuole gestire la propria chiave del tenant di Azure Information Protection tramite una chiave protetta da HSM**:

    - Per questa configurazione facoltativa è necessario usare Insieme di credenziali delle chiavi di Azure e una sottoscrizione di Azure che supporti l'insieme di credenziali delle chiavi con chiavi protette tramite HMS. Per altre informazioni, vedere la pagina [dei prezzi di Insieme di credenziali delle chiavi di Azure](https://azure.microsoft.com/pricing/details/key-vault/). 


### <a name="cryptographic-mode-considerations"></a>Considerazioni sulla modalità di crittografia

Se il cluster AD RMS è attualmente in modalità crittografia 1, non aggiornare il cluster alla modalità crittografia 2 prima di iniziare la migrazione. Eseguire invece la migrazione con la modalità crittografia 1; è possibile reimpostare la chiave del tenant al termine della migrazione, come una delle attività di post-migrazione.

Per verificare la modalità di crittografia AD RMS:
 
- Per Windows Server 2012 R2 e Windows 2012: proprietà del cluster AD RMS > scheda **Generale**. 

### <a name="migration-limitations"></a>Limitazioni della migrazione

- Se sono presenti software e client non supportati dal servizio Rights Management usato da Azure Information Protection, questi non saranno in grado di proteggere o utilizzare il contenuto protetto da Azure Rights Management. Assicurarsi di controllare le sezioni applicazioni e client supportate dai [requisiti per Azure Information Protection](./requirements.md).

- Se la distribuzione di AD RMS è configurata per collaborare con partner esterni, ad esempio tramite domini utente trusted o federazione, anche questi dovranno eseguire la migrazione ad Azure Information Protection allo stesso tempo della migrazione o il prima possibile dopo la migrazione. Per continuare ad accedere ai contenuti precedentemente protetti dall'organizzazione usando Azure Information Protection, i partner dovranno apportare modifiche di configurazione al client simili a quelle apportate dall'utente e descritte in questo documento.
    
    A causa delle differenze di configurazione tra l'utente e i partner, le istruzioni precise per questa riconfigurazione non rientrano nell'ambito di questo documento. Vedere la sezione successiva per materiale sussidiario sulla pianificazione e [contattare il supporto Microsoft](./information-support.md#support-options-and-community-resources) per altre informazioni.

## <a name="migration-planning-if-you-collaborate-with-external-partners"></a>Pianificazione della migrazione se si collabora con partner esterni

Includere i partner di AD RMS in fase di pianificazione della migrazione perché anche questi devono essere migrati ad Azure Information Protection. Prima di eseguire i passaggi di migrazione seguenti, verificare che quanto indicato di seguito sia già configurato:

- I partner hanno un tenant Azure Active Directory che supporta il servizio Azure Rights Management.  
    
    Ad esempio, hanno una sottoscrizione a Office 365 E3 o E5, o a Enterprise Mobility + Security oppure una sottoscrizione autonoma per Azure Information Protection.

- Il loro servizio Azure Rights Management non è ancora attivato ma conoscono il relativo URL del servizio Azure Rights Management.

    È possibile ottenere queste informazioni installando lo strumento Azure Rights Management, connettendosi al servizio ([Connect-AipService](/powershell/module/aipservice/connect-aipservice)) e quindi visualizzando le informazioni sul tenant per il servizio Azure Rights Management ([Get-AipServiceConfiguration](/powershell/module/aipservice/get-aipserviceconfiguration)).

- Specificano gli URL per i loro cluster AD RMS e per il loro servizio Azure Rights Management, in modo che sia possibile configurare i client migrati per reindirizzare le richieste di contenuto protetto da AD RMS al servizio Azure Rights Management dei loro tenant. Le istruzioni per configurare il reindirizzamento del client sono incluse nel passaggio 7.

- Importano le chiavi radice cluster di AD RMS (SLC) nel loro tenant prima di iniziare la migrazione degli utenti. Analogamente, è necessario importare le chiavi radice cluster di AD RMS prima dell'inizio della migrazione degli utenti. Le istruzioni per l'importazione della chiave sono descritte in questo processo di migrazione, [passaggio 4. Esportare i dati di configurazione da AD RMS e importarli nel Azure Information Protection](migrate-from-ad-rms-phase2.md#step-4-export-configuration-data-from-ad-rms-and-import-it-to-azure-information-protection). 

## <a name="overview-of-the-steps-for-migrating-ad-rms-to-azure-information-protection"></a>Panoramica dei passaggi per la migrazione da AD RMS ad Azure Information Protection

I passaggi della migrazione possono essere suddivisi in cinque fasi eseguibili in momenti diversi e da amministratori diversi.

[**FASE 1: PREPARAZIONE DELLA MIGRAZIONE**](migrate-from-ad-rms-phase1.md)

- **Passaggio 1: installare il modulo PowerShell AIPService e identificare l'URL del tenant**

    Per il processo di migrazione è necessario eseguire uno o più cmdlet di PowerShell dal modulo AIPService. È necessario conoscere l'URL del servizio Azure Rights Management del tenant per completare molti passaggi necessari per la migrazione ed è possibile identificare questo valore tramite PowerShell.

- **Passaggio 2. Preparare la migrazione client**

    Se non è possibile eseguire la migrazione di tutti i client in una sola volta e la si esegue in batch, usare i controlli di onboarding e distribuire uno script di pre-migrazione. Tuttavia, se si eseguirà la migrazione di tutti gli elementi nello stesso momento piuttosto che eseguire una migrazione graduale, è possibile ignorare questo passaggio.

- **Passaggio 3: preparare la distribuzione di Exchange per la migrazione**

    Questo passaggio è obbligatorio se si usa attualmente la funzionalità IRM di Exchange Online o di Exchange locale per proteggere i messaggi di posta elettronica. Tuttavia, se si eseguirà la migrazione di tutti gli elementi nello stesso momento piuttosto che eseguire una migrazione graduale, è possibile ignorare questo passaggio.

[**FASE 2: CONFIGURAZIONE LATO SERVER PER AD RMS**](migrate-from-ad-rms-phase2.md)

- **Passaggio 4. Esportare i dati di configurazione da AD RMS e importarli in Azure Information Protection**

    Si esportano i dati di configurazione (chiavi, modelli, URL) da AD RMS a un file XML e quindi si carica il file nel servizio Rights Management di Azure da Azure Information Protection usando il cmdlet di PowerShell Import-AipServiceTpd. Identificare quindi la chiave del certificato concessore di licenze server da usare come chiave del tenant per il servizio Azure Rights Management. Potrebbero essere necessari altri passaggi, a seconda della configurazione della chiave di AD RMS:

    - **Migrazione da una chiave protetta tramite software a un'altra**:

        Da chiavi basate su password gestite a livello centrale in AD RMS a chiave del tenant di Azure Information Protection gestita da Microsoft. Questo è il percorso di migrazione più semplice e non richiede altri passaggi.

    - **Migrazione da una chiave protetta tramite HSM a un'altra**:

        Da chiavi archiviate da un modulo di protezione hardware per AD RMS a chiave del tenant di Azure Information Protection gestita dal cliente (scenario "bring your own key" o BYOK). Questa operazione richiede passaggi aggiuntivi per trasferire la chiave dal modulo di protezione hardware nCipher locale per Azure Key Vault e autorizzare il servizio Rights Management di Azure a usare questa chiave. La chiave protetta tramite HSM esistente deve essere protetta dal modulo. Le chiavi protette da OCS non sono supportate dai servizi di Rights Management.

    - **Migrazione da una chiave protetta tramite software a una chiave protetta tramite HSM**:

        Da chiavi basate su password gestite a livello centrale in AD RMS a chiave del tenant di Azure Information Protection gestita dal cliente (scenario "bring your own key" o BYOK). Questa operazione richiede la configurazione più lunga perché è necessario innanzitutto estrarre la chiave software e importarla in un modulo di protezione hardware locale, quindi eseguire i passaggi aggiuntivi per trasferire la chiave dal modulo di protezione hardware nCipher locale a un modulo di protezione hardware Azure Key Vault e autorizzare i diritti di Azure Servizio di gestione per usare l'insieme di credenziali delle chiavi in cui è archiviata la chiave.

- **Passaggio 5. Attivare il servizio Azure Rights Management**

    Se possibile, eseguire questo passaggio dopo il processo di importazione, non prima. Se il servizio è stato attivato prima dell'importazione, sono necessari passaggi aggiuntivi.

- **Passaggio 6. Configurare i modelli importati**

    Quando si importano i modelli di criteri per i diritti di utilizzo, il relativo stato viene archiviato. Se si vuole che gli utenti possano visualizzarli e usarli, è necessario modificare lo stato del modello in Pubblicato nel portale di Azure classico.


[**FASE 3: CONFIGURAZIONE LATO CLIENT**](migrate-from-ad-rms-phase3.md)

- **Passaggio 7: Riconfigurare i computer Windows per usare Azure Information Protection**

    Per usare il servizio Azure Rights Management invece del servizio AD RMS, è necessario riconfigurare i computer Windows esistenti. Questo passaggio si applica ai computer dell'organizzazione e ai computer di organizzazioni partner, nel caso si sia collaborato con esse durante l'esecuzione di AD RMS.

[**FASE 4: CONFIGURAZIONE DI SERVIZI DI SUPPORTO**](migrate-from-ad-rms-phase4.md)

- **Passaggio 8: configurare l'iterazione IRM per Exchange Online**

    Questo passaggio completa la migrazione di AD RMS per Exchange Online per l'uso del servizio Azure Rights Management.

- **Passaggio 9: configurare l'integrazione IRM per Exchange Server e SharePoint Server**

    Questo passaggio completa la migrazione di AD RMS per Exchange o per SharePoint locale per l'uso del servizio Azure Rights Management, che richiede la distribuzione del connettore Rights Management.


[**FASE 5: ATTIVITÀ POST-MIGRAZIONE**](migrate-from-ad-rms-phase5.md )

- **Passaggio 10: Deprovisioning di AD RMS**

    Dopo aver verificato che tutti i computer Windows usano il servizio Azure Rights Management e non accedono più ai server AD RMS, è possibile effettuare il deprovisioning della distribuzione di AD RMS.

- **Passaggio 11: Completare le attività di migrazione dei client**

    Se è stata distribuita l'[estensione per dispositivi mobili](https://technet.microsoft.com/library/dn673574.aspx) per supportare dispositivi mobili, ad esempio telefoni iOS e iPad, telefoni e tablet Android, telefoni e tablet Windows e computer Mac, è necessario rimuovere i record SRV in DNS che reindirizzavano questi client all'uso di AD RMS. 
    
    I controlli di onboarding configurati durante la fase di preparazione non sono più necessari. Tuttavia, se non sono stati usati controlli di onboarding perché si è scelto di eseguire la migrazione di tutti gli elementi contemporaneamente, anziché eseguire una migrazione graduale, è possibile ignorare le istruzioni per rimuovere i controlli di onboarding.
    
    Se i computer Windows eseguono Office 2010, verificare se è necessario disabilitare l'attività **AD RMS Rights Policy Template Management (Automated)** (Gestione modelli di criteri per i diritti di utilizzo AD RMS - Automatizzata).

- **Passaggio 12: Reimpostare la chiave del tenant di Azure Information Protection**

    Questo passaggio è consigliato se non era in esecuzione la modalità crittografia 2 prima della migrazione.


## <a name="next-steps"></a>Passaggi successivi
Per iniziare la migrazione, passare a [Fase 1: preparazione](migrate-from-ad-rms-phase1.md).

