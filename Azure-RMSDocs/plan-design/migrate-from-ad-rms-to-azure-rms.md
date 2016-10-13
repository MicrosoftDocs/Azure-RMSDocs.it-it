---
title: Migrazione da AD RMS ad Azure Information Protection | Azure Information Protection
description: "Istruzioni per la migrazione della distribuzione di Active Directory Rights Management Services (AD RMS) ad Azure Information Protection. Dopo la migrazione, gli utenti avranno comunque accesso ai documenti e ai messaggi di posta elettronica che l'organizzazione ha protetto tramite AD RMS, nonché al nuovo contenuto che verrà protetto con Azure Information Protection."
author: cabailey
manager: mbaldwin
ms.date: 09/25/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 828cf1f7-d0e7-4edf-8525-91896dbe3172
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: bb240b92a86bfc37685556ba2ce71b9eea56ae88
ms.openlocfilehash: c3e926b48dfc66da71e4e3f16f9359b3cb8322c6


---

# Migrazione da AD RMS ad Azure Information Protection

>*Si applica a: Active Directory Rights Management Services, Azure Information Protection, Office 365*

Usare il set di istruzioni seguente per la migrazione della distribuzione di Active Directory Rights Management Services (AD RMS) ad Azure Information Protection. Dopo la migrazione, gli utenti avranno comunque accesso ai documenti e ai messaggi di posta elettronica che l'organizzazione ha protetto tramite AD RMS, nonché al nuovo contenuto che verrà protetto con il servizio Azure Rights Management di Azure Information Protection.

Se non si è certi che questa migrazione di AD RMS sia adatta alla propria organizzazione

-   Per un'introduzione ad Azure Information Protection, vedere [Che cos'è Azure Information Protection?](../understand-explore/what-is-information-protection.md)

-   Per un confronto tra Azure Information Protection e AD RMS, vedere [Confronto tra Azure Information Protection e AD RMS](../understand-explore/compare-azure-rms-ad-rms.md).

## Prerequisiti per la migrazione da AD RMS ad Azure Information Protection
Prima di iniziare il processo di migrazione ad Azure Information Protection, verificare che i prerequisiti seguenti siano soddisfatti e accertarsi di avere compreso le possibili limitazioni.

- **Distribuzione di RMS supportata:**
    
    - Le versioni seguenti di AD RMS supportano una migrazione ad Azure Information Protection:
    
        - Windows Server 2008 R2 (x64)
        
        - Windows Server 2012 (x64)
        
        - Windows Server 2012 R2 (x64)
        
    - Modalità di crittografia 2:

        - I server e i client di AD RMS devono essere in esecuzione in modalità di crittografia 2 prima di iniziare la migrazione ad Azure Information Protection.
        
        Anche se la chiave del certificato concessore di licenze server (SLC) corrente deve usare la modalità di crittografia 2, le chiavi precedenti configurate per la modalità di crittografia 1 sono supportate in Azure Information Protection come chiavi archiviate. Per altre informazioni sulle modalità di crittografia e su come passare alla modalità di crittografia 2, vedere [Modalità di crittografia di AD RMS](https://technet.microsoft.com/library/hh867439(v=ws.10).aspx).
        
    - Sono supportate tutte le topologie di AD RMS valide:
    
        - Singola foresta, singolo cluster RMS
        
        - Singola foresta, più cluster RMS di sola gestione delle licenze
        
        - Più foreste, più cluster RMS
        
    Nota: per impostazione predefinita, viene eseguita la migrazione di più cluster RMS a un singolo tenant di Azure Information Protection. Se si vuole separare i tenant di Azure Information Protection, è necessario considerarli come diverse migrazioni. Non è possibile importare una chiave da un cluster RMS in più tenant di Azure Information Protection.

- **Tutti i requisiti per l'esecuzione di Azure Information Protection, incluso un tenant di Azure Information Protection (non attivato):**

    Vedere [Requisiti per Azure Information Protection](../get-started/requirements-azure-rms.md).

    Anche se è necessario avere un tenant di Azure Information Protection per poter eseguire la migrazione da AD RMS, è consigliabile non attivare il servizio Rights Management prima della migrazione. Questo passaggio è incluso nel processo di migrazione dopo l'esportazione delle chiavi e dei modelli da AD RMS e la relativa importazione in Azure Information Protection. Tuttavia, se il servizio Rights Management è già attivato, è ugualmente possibile eseguire la migrazione da AD RMS.


- **Preparazione per Azure Information Protection:**

    - Sincronizzazione della directory tra la directory locale e Azure Active Directory

    - Gruppi abilitati alla posta elettronica in Azure Active Directory

    Vedere [Preparazione per Azure Information Protection](prepare.md).


- **Se è stata usata la funzionalità Information Rights Management (IRM) di Exchange Server** (ad esempio le regole di trasporto e Outlook Web Access) o SharePoint Server con AD RMS:

    - Pianificare un breve intervallo di tempo durante il quale IRM non sarà disponibile in questi server
 
    Si potrà continuare a usare IRM in questi server con il servizio Azure Rights Management dopo la migrazione. Uno dei passaggi della migrazione consiste tuttavia nel disattivare temporaneamente il servizio IRM, installare e configurare un connettore, riconfigurare i server e quindi riabilitare IRM.

    Questa è la sola interruzione del servizio durante il processo di migrazione.

- **Se si vuole gestire la propria chiave del tenant di Azure Information Protection tramite una chiave protetta da HSM**:

    - Per questa configurazione facoltativa è necessario usare Insieme di credenziali delle chiavi di Azure e una sottoscrizione di Azure che supporti l'insieme di credenziali delle chiavi con chiavi protette tramite HMS. Per altre informazioni, vedere la pagina [dei prezzi di Insieme di credenziali delle chiavi di Azure](https://azure.microsoft.com/en-us/pricing/details/key-vault/). 


Limitazioni:

-   Anche se il processo di migrazione supporta la migrazione della chiave del certificato concessore di licenze server (SLC) in un modulo di protezione hardware (HSM) per Azure Information Protection, Exchange Online non supporta attualmente questa configurazione per il servizio Rights Management usato da Azure Information Protection. Se si vuole la funzionalità IRM completa con Exchange Online dopo la migrazione ad Azure Information Protection, la chiave del tenant di Azure Information Protection deve essere [gestita da Microsoft](../plan-design/plan-implement-tenant-key.md#choose-your-tenant-key-topology-managed-by-microsoft-the-default-or-managed-by-you-byok). In alternativa, è possibile eseguire IRM con funzionalità ridotta in Exchange Online quando il tenant di Azure Information Protection è gestito dall'utente (BYOK). Per altre informazioni sull'uso di Exchange Online con il servizio Azure Rights Management, vedere [Passaggio 6. Configurare l’integrazione IRM per Exchange Online](migrate-from-ad-rms-phase3.md#step-6-configure-irm-integration-for-exchange-online).

-   Se sono presenti software e client non supportati dal servizio Rights Management usato da Azure Information Protection, questi non saranno in grado di proteggere o utilizzare il contenuto protetto da Azure Rights Management. Verificare le sezioni relative alle applicazioni e ai client supportati nell’articolo [Requisiti per Azure Rights Management](../get-started/requirements-azure-rms.md).

-   Se si importa la chiave locale in Azure Information Protection come archiviata (non si imposta il dominio di pubblicazione trusted come attivo durante il processo di importazione) e si esegue la migrazione degli utenti in batch per una migrazione graduale, il nuovo contenuto protetto dagli utenti di cui è stata eseguita la migrazione non sarà accessibile agli utenti che rimangono in AD RMS. In questo scenario, quando possibile, eseguire la migrazione degli utenti in tempi brevi e in batch logici, in modo che, quelli che collaborano tra loro, vengano sottoposti a migrazione insieme.

    Questa limitazione non viene applicata quando si imposta il dominio di pubblicazione trusted come attivo durante il processo di importazione, perché tutti gli utenti proteggeranno il contenuto usando la stessa chiave. Si consiglia questa configurazione perché consente di eseguire la migrazione di tutti gli utenti in modo indipendente e con gradualità.

-   Se si collabora con partner esterni, ad esempio tramite domini utente trusted o la federazione, anche questi dovranno eseguire la migrazione ad Azure Information Protection contemporaneamente alla migrazione dall'utente o il prima possibile. Per continuare ad accedere ai contenuti precedentemente protetti dall'organizzazione usando Azure Information Protection, i partner dovranno apportare modifiche di configurazione al client simili a quelle apportate dall'utente e descritte in questo documento.

    A causa delle differenze di configurazione tra l'utente e i partner, le istruzioni precise per questa riconfigurazione non rientrano nell'ambito di questo documento. Per assistenza, [contattare il supporto Microsoft](../get-started/information-support.md#support-options-and-community-resources).

## Panoramica dei passaggi per la migrazione da AD RMS ad Azure Information Protection


I passaggi della migrazione possono essere suddivisi in 4 fasi eseguibili in momenti diversi e da amministratori diversi.

[**FASE 1: CONFIGURAZIONE LATO SERVER PER AD RMS**](migrate-from-ad-rms-phase1.md)

- **Passaggio 1. Scaricare Azure RMS Management Administration Tool**

    Per il processo di migrazione è necessario eseguire uno o più cmdlet di Windows PowerShell dal modulo di Azure RMS installato con Azure RMS Management Administration Tool.

- **Passaggio 2: Esportare i dati di configurazione da AD RMS e importarli in Azure Information Protection**

    Esportare i dati di configurazione (chiavi, modelli, URL) da AD RMS in un file XML e quindi caricare il file nel servizio Azure Rights Management di Azure Information Protection usando il cmdlet Import-AadrmTpd di Windows PowerShell. Potrebbero essere necessari altri passaggi, a seconda della configurazione della chiave di AD RMS

    - **Migrazione da una chiave protetta tramite software a un'altra**:

        Da chiavi basate su password gestite a livello centrale in AD RMS a chiave del tenant di Azure Information Protection gestita da Microsoft. Questo è il percorso di migrazione più semplice e non richiede altri passaggi.

    - **Migrazione da una chiave protetta tramite HSM a un'altra**:

        Da chiavi archiviate da un modulo di protezione hardware per AD RMS a chiave del tenant di Azure Information Protection gestita dal cliente (scenario "bring your own key" o BYOK). È necessario eseguire altri passaggi per trasferire la chiave dal modulo di protezione hardware di Thales locale a Insieme di credenziali delle chiavi di Azure e autorizzare il servizio Azure Rights Management all'uso di tale chiave. La chiave protetta tramite HSM esistente deve essere protetta dal modulo. Le chiavi protette da OCS non sono supportate dai servizi di Rights Management.

    - **Migrazione da una chiave protetta tramite software a una chiave protetta tramite HSM**:

        Da chiavi basate su password gestite a livello centrale in AD RMS a chiave del tenant di Azure Information Protection gestita dal cliente (scenario "bring your own key" o BYOK). È necessaria la configurazione più estesa, perché è innanzitutto necessario estrarre la chiave software e importarla in un modulo di protezione hardware locale e quindi eseguire i passaggi aggiuntivi per trasferire la chiave dal modulo di protezione hardware di Thales locale a un modulo di protezione hardware di Insieme di credenziali delle chiavi di Azure e autorizzare il servizio Azure Rights Management all'uso dell'insieme di credenziali che archivia la chiave.

- **Passaggio 3. Attivare il tenant di Azure Information Protection**

    Se possibile, eseguire questo passaggio dopo il processo di importazione, non prima.

- **Passaggio 4. Configurare i modelli importati**

    Quando si importano i modelli di criteri per i diritti di utilizzo, il relativo stato viene archiviato. Se si vuole che gli utenti possano visualizzarli e usarli, è necessario modificare lo stato del modello in Pubblicato nel portale di Azure classico.


[**FASE 2: CONFIGURAZIONE LATO CLIENT**](migrate-from-ad-rms-phase2.md)


- **Passaggio 5: Riconfigurare i client per l'uso di Azure Information Protection**

    È necessario riconfigurare i computer Windows esistenti per l'uso del servizio Azure Information Protection anziché AD RMS. Questo passaggio si applica ai computer dell'organizzazione e ai computer di organizzazioni partner, nel caso si sia collaborato con esse durante l'esecuzione di AD RMS.

    Inoltre, se per supportare dispositivi mobili, quali telefoni e iPad iOS, telefoni e tablet Android, Windows Phone e computer Mac, è stata distribuita l’[estensione per dispositivo mobile](http://technet.microsoft.com/library/dn673574.aspx), sarà necessario rimuovere i record SRV in DNS che reindirizzavano questi client all'uso di AD RMS.


[**FASE 3: CONFIGURAZIONE DI SERVIZI DI SUPPORTO**](migrate-from-ad-rms-phase3.md)


- **Passaggio 6: Configurare l'integrazione IRM con Exchange Online**

    Questo passaggio è obbligatorio se si vuole usare Exchange Online con il servizio Azure Rights Management di Azure Information Protection.


- **Passaggio 7: Distribuire il connettore RMS**

    Questo passaggio è obbligatorio se si vuole usare uno dei seguenti servizi locali con il servizio Azure Rights Management per proteggere messaggi di posta elettronica e documenti di Office:

    - Exchange Server (ad esempio, le regole di trasporto e Outlook Web Access)

    - SharePoint Server

    - Windows Server con la funzionalità Infrastruttura di classificazione file


[**FASE 4: ATTIVITÀ POST-MIGRAZIONE**](migrate-from-ad-rms-phase4.md )

- **Passaggio 8: Rimuovere le autorizzazioni di AD RMS**

    Dopo aver verificato che tutti i client usano Azure Information Protection e non accedono più ai server AD RMS, sarà possibile rimuovere le autorizzazioni per la distribuzione di AD RMS.


- **Passaggio 9: Reimpostare la chiave del tenant di Azure Information Protection**

    Questo passaggio è facoltativo ma consigliato se la topologia della chiave del tenant di Azure Information Protection scelta al passaggio 2 è gestita da Microsoft. Questo passaggio non è applicabile se la topologia della chiave del tenant di Azure Information Protection scelta è gestita dal cliente (BYOK).


## Passaggi successivi
Per iniziare la migrazione, passare a [Fase 1: configurazione lato server](migrate-from-ad-rms-phase1.md).




<!--HONumber=Sep16_HO4-->


