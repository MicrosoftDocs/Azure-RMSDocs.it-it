---
# required metadata

title: Pianificazione e implementazione della chiave del tenant di Azure Rights Management | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 06/14/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: f0d33c5f-a6a6-44a1-bdec-5be1bc8e1e14

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Pianificazione e implementazione della chiave del tenant di Azure Rights Management

*Si applica a: Azure Rights Management, Office 365*

In questo argomento sono contenute informazioni per pianificare e gestire la chiave del tenant RMS (Rights Management Service) per Azure RMS. Anziché affidare a Microsoft la gestione della chiave del tenant (impostazione predefinita), per rispettare i criteri aziendali potrebbe essere necessario, ad esempio, gestire autonomamente la propria chiave del tenant  in base alla modalità BYOK (Bring Your Own Key).

> [!NOTE]
> La chiave del tenant RMS è nota anche come certificato concessore di licenze server (SLC, Server Licensor Certificate). Azure RMS gestisce una o più chiavi per ogni organizzazione che effettua una sottoscrizione a Azure RMS. Tutte le volte che in un'organizzazione si usa una chiave per RMS, ad esempio chiavi utente, chiavi computer o chiavi di crittografia documenti, la chiave si concatena a livello di crittografia alla chiave del tenant RMS dell'utente.

**Panoramica:** Usare la tabella seguente come guida rapida per la topologia consigliata delle chiavi del tenant. Per altre informazioni, vedere quindi la documentazione aggiuntiva.

Se si distribuisce Azure RMS con una chiave del tenant gestita da Microsoft, sarà possibile passare alla modalità BYOK in un secondo momento. Non è tuttavia attualmente possibile passare dalla modalità BYOK alla gestione da parte di Microsoft per la chiave del tenant di Azure RMS.

|Requisito aziendale|Topologia di chiave del tenant consigliata|
|------------------------|-----------------------------------|
|Distribuire Azure RMS rapidamente e senza che sia necessario hardware speciale|Gestita da Microsoft|
|Necessità di ottenere la funzionalità IRM completa in Exchange Online con Azure RMS|Gestita da Microsoft|
|Le chiavi vengono create dall'utente e protette in un modulo di protezione hardware|BYOK<br /><br />Questa configurazione darà attualmente come risultato una funzionalità IRM ridotta in Exchange Online. Per altre informazioni, vedere [Prezzi e restrizioni della modalità BYOK](byok-price-restrictions.md).|

## Scegliere la topologia di chiave del tenant: gestione di Microsoft (impostazione predefinita) o BYOK
È innanzitutto necessario decidere la topologia di chiave del tenant più adatta per l'organizzazione. Per impostazione predefinita, Azure RMS genera la chiave del tenant e gestisce la maggior parte degli aspetti del relativo ciclo di vita. Questa opzione è quella più semplice e prevede il sovraccarico amministrativo minore. Nella maggior parte dei casi non è nemmeno necessario disporre di una chiave del tenant, ma è sufficiente iscriversi ad Azure RMS e la parte rimanente del processo di gestione delle chiavi viene eseguita da Microsoft.

In alternativa, se si desidera il controllo completo sulla chiave del tenant, è possibile creare la propria chiave e conservarne la copia master in locale. Questo scenario viene spesso definito con il termine modalità BYOK e prevede lo schema seguente.

1.  Generazione della chiave del tenant utente in locale, in base ai criteri IT dell'organizzazione.

2.  Trasferimento sicuro della chiave del tenant da un modulo di protezione hardware di proprietà dell'utente a moduli di protezioni hardware di proprietà e gestiti da Microsoft. Grazie a questo processo, la chiave del tenant non oltrepassa mai i confini dell'ambiente hardware protetto.

3.  Quando si trasferisce la chiave del tenant a Microsoft, la protezione viene assicurata da moduli di protezione hardware Thales. Microsoft ha collaborato con Thales per garantire che la chiave del tenant dell'utente non possa essere estratta da moduli di protezione hardware di Microsoft.

Anche se è facoltativo, i log di utilizzo di Azure RMS disponibili in tempo quasi reale sono utili per sapere esattamente come e quando viene usata la chiave del tenant.

> [!NOTE]
> Come misura di protezione aggiuntiva, Azure RMS usa ambienti di sicurezza separati per i propri data center in America del Nord, nei paesi EMEA (Europa, Medio Oriente e Africa) e in Asia. Quando si gestisce la propria chiave del tenant, quest'ultima è associata all'ambiente di sicurezza in cui è registrato il tenant RMS. Una chiave del tenant di un cliente europeo, ad esempio, non può essere usata in data center che si trovano in America del Nord o in Asia.

## Ciclo di vita della chiave del tenant
Se si decide di affidare a Microsoft la gestione della chiave del tenant, Microsoft gestisce la maggior parte delle operazioni del ciclo di vita della chiave. Se invece l'utente decide di gestire in modo autonomo la propria chiave del tenant, è responsabile di molte operazione del ciclo di vita della chiave e di alcune procedure aggiuntive.

Nei diagrammi seguenti vengono illustrate e confrontate le due opzioni. Nel primo diagramma viene illustrato il minor sovraccarico amministrativo che l'utente deve sostenere nella configurazione predefinita quando Microsoft gestisce la chiave del tenant.

![Ciclo di vita della chiave del tenant di Azure RMS: chiave gestita da Microsoft, impostazione predefinita](../media/RMS_BYOK_cloud.png)

Nel secondo diagramma vengono illustrati i passaggi aggiuntivi necessari quando l'utente gestisce la propria chiave del tenant.

![Ciclo di vita della chiave del tenant di Azure RMS: chiave gestita dall'utente, BYOK](../media/RMS_BYOK_onprem.png)

Se si decide di affidare a Microsoft la gestione della chiave del tenant, non è necessaria alcuna azione aggiuntiva per generare la chiave ed è possibile passare direttamente alla sezione [Passaggi successivi](plan-implement-tenant-key.md#next-steps).

Se invece si decide di gestire in modo autonomo la propria chiave del tenant, leggere le sezioni seguenti per ottenere altre informazioni.

## Implementazione della chiave del tenant di Azure Rights Management

Usare le informazioni e le procedure descritte in questa sezione se si è deciso di generare e gestire la propria chiave del tenant in base allo schema BYOK.


> [!IMPORTANT]
> Se si è già iniziato a usare [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] (servizio attivato) e sono presenti utenti che eseguono Office 2010, [contattare il supporto Microsoft](../get-started/information-support#to-contact-microsoft-support) prima di eseguire queste procedure. A seconda dello scenario e dei requisiti, è comunque possibile usare la modalità BYOK con alcune limitazioni o con passaggi aggiuntivi.
> 
> [Contattare il supporto Microsoft](../get-started/information-support#to-contact-microsoft-support) anche quando l'organizzazione prevede criteri specifici per la gestione delle chiavi.

### Prerequisiti per la modalità BYOK
Nella tabella seguente sono elencati i prerequisiti per la modalità BYOK.

|Requisito|Altre informazioni|
|---------------|--------------------|
|Sottoscrizione che supporta Azure RMS.|Per altre informazioni sulle sottoscrizioni disponibili, vedere [Sottoscrizioni cloud che supportano Azure RMS](../get-started/requirements-subscriptions.md).|
|Non si usa RMS per singoli utenti o per Exchange Online. Se si usa Exchange Online, si conoscono e si accettano le limitazioni relative all'uso della modalità BYOK con questa configurazione.|Per altre informazioni sulle restrizioni per la modalità BYOK e sulle limitazioni attuali, vedere [Prezzi e restrizioni della modalità BYOK](byok-price-restrictions.md).<br /><br />**Importante**: attualmente, la modalità BYOK non è compatibile con Exchange Online.|
|Moduli di protezione hardware Thales, smart card e software di supporto.<br /><br />**Nota**: se si esegue la migrazione da AD RMS ad Azure RMS, passando da una chiave software a una chiave hardware, sarà necessaria almeno la versione 11.62 per i driver Thales.|È necessario disporre dell'accesso ai moduli di protezione hardware Thales e averne una conoscenza a livello operativo. Per l'elenco dei modelli compatibili o per acquistare un modulo di protezione hardware qualora non se ne sia già in possesso, vedere la pagina relativa ai [moduli di protezione hardware Thales](http://www.thales-esecurity.com/msrms/buy) .|
|Se si desidera trasferire la propria chiave del tenant tramite Internet anziché recarsi fisicamente a Redmond negli Stati Uniti, è necessario soddisfare 3 requisiti:<br /><br />1: una workstation x64 offline con sistema operativo Windows 7 o versioni successive e software nShield Thales versione 11.62 o successive.<br /><br />Se la workstation esegue Windows 7, è necessario [installare Microsoft .NET Framework 4.5](http://go.microsoft.com/fwlink/?LinkId=225702).<br /><br />2: una workstation connessa a Internet con sistema operativo Windows 7 o versioni successive.<br /><br />3: un'unità USB o altro dispositivo di archiviazione portatile con almeno 16 MB di spazio disponibile.|Tali prerequisiti non sono necessari se ci si reca a Redmond e si trasferisce la propria chiave di persona.<br /><br />Per motivi di sicurezza, si consiglia che la prima workstation non sia connessa a una rete. Questa condizione tuttavia non viene applicata a livello di codice.<br /><br />Nota: nelle istruzioni seguenti si fa riferimento alla prima workstation come **workstation disconnessa**.<br /><br />Se inoltre la propria chiave del tenant è destinata a essere usata in una rete di produzione, si consiglia di usare una seconda workstation separata per scaricare il set di strumenti e caricare la chiave del tenant. A scopo di test è comunque possibile usare la prima workstation.<br /><br />Nota: nelle istruzioni seguenti si fa riferimento alla seconda workstation come **workstation connessa a Internet**.|

Le procedure per generare e usare la propria chiave del tenant dipendono dalle modalità di esecuzione di tali operazioni, ovvero tramite Internet o di persona.

-   **Tramite Internet:** In questo caso sono necessari alcuni passaggi di configurazione aggiuntivi, ad esempio il download e l'uso di un set di strumenti e di cmdlet di Windows PowerShell. Non è necessario tuttavia essere presenti in un ufficio Microsoft per trasferire la chiave del tenant, perché la sicurezza è garantita grazie ai metodi indicati di seguito.

    -   La chiave del tenant viene generata in una workstation offline per ridurre la superficie di attacco.

    -   La crittografia della chiave del tenant viene eseguita tramite una chiave per lo scambio delle chiavi che rimane crittografata fino al momento del trasferimento ai moduli di protezione hardware di Azure RMS. Solo la versione crittografata della chiave del tenant viene inviata dalla workstation originale.

    -   Uno strumento imposta proprietà sulla chiave del tenant che consentono di associarla all'ambiente di sicurezza di Azure RMS. Di conseguenza, dopo che i moduli di protezione hardware di Azure RMS ricevono la chiave del tenant e ne eseguono la decrittografia, sono gli unici componenti a poterla usare. La chiave del tenant non può essere esportata. Questa associazione viene applicata dai moduli di protezione hardware Thales.

    -   La chiave per lo scambio delle chiavi usata per crittografare la chiave del tenant viene generata nei moduli di protezione hardware di Azure RMS e non è esportabile. I moduli di protezione hardware applicano la regola in base alla quale non può esistere una versione non crittografata della chiave per lo scambio delle chiavi all'esterno dei moduli stessi. Il set di strumenti include inoltre un'attestazione di Thales che dichiara che la chiave per lo scambio delle chiavi non è esportabile e che è stata generata in un modulo di protezione hardware originale prodotto da Thales.

    -   Il set di strumenti include un'attestazione di Thales che dichiara che anche l'ambiente di sicurezza di Azure RMS è stato generato in un modulo di protezione hardware originale prodotto da Thales. In questo modo l'utente ha la conferma che Microsoft usa hardware originale.

    -   Microsoft usa chiavi per lo scambio delle chiavi e ambienti di sicurezza separati in ogni area geografica per garantire che sia possibile usare la chiave del tenant solo nei data center presenti nell'area geografica in cui è stata generata. Una chiave del tenant di un cliente europeo, ad esempio, non può essere usata in data center che si trovano in America del Nord o in Asia.

    > [!NOTE]
    > La chiave del tenant può spostarsi in modo sicuro tra computer e reti non attendibili perché è crittografata e protetta con autorizzazioni a livello di controllo di accesso, condizione che la rende accessibile solo all'interno dei moduli di protezione hardware dell'utente e di quelli di Microsoft per Azure RMS. È possibile usare gli script disponibili nel set di strumenti per verificare le misure di sicurezza e leggere altre informazioni sul funzionamento in Thales della [gestione delle chiavi hardware nel cloud RMS](https://www.thales-esecurity.com/knowledge-base/white-papers/hardware-key-management-in-the-rms-cloud).

-   **Di persona**: in questo caso è necessario [contattare il supporto Microsoft](../get-started/information-support#to-contact-microsoft-support) per pianificare un appuntamento per il trasferimento della chiave per Azure RMS. È necessario recarsi di persona in un ufficio Microsoft a Redmond, Washington, Stati Uniti, per trasferire la propria chiave del tenant nell'ambiente di sicurezza di Azure RMS.

Per istruzioni sulle procedure, selezionare se si intende generare e trasferire la chiave del tenant tramite Internet o di persona: 

- [Tramite Internet](generate-tenant-key-internet.md)
- [Di persona](generate-tenant-key-in-person.md)


## Passaggi successivi

Dopo la pianificazione e, se necessario, la generazione della chiave del tenant, effettuare le operazioni seguenti:

1.  Iniziare a usare la chiave del tenant.

    -   Se non è ancora stato fatto, è ora necessario attivare Rights Management in modo che l'organizzazione possa iniziare a usare RMS. In questo caso gli utenti iniziano immediatamente a usare la chiave del tenant (gestita da Microsoft o gestita in modo autonomo).

        Per altre informazioni, vedere [Attivazione di Azure Rights Management](../deploy-use/activate-service.md).

    -   Se Rights Management è già stato attivato e si è deciso di gestire la propria chiave del tenant, gli utenti passano gradualmente dalla chiave del tenant precedente a quella nuova e questa transizione in fasi successive può richiedere alcune settimane per essere completata. I documenti e i file protetti con la chiave del tenant precedente rimangono accessibili agli utenti autorizzati.

2.  Valutare l'opportunità di usare la registrazione dei dati di utilizzo per tenere traccia di ogni transazione eseguita da RMS.

    Se si è deciso di gestire la propria chiave del tenant, la registrazione include informazioni sull'uso della chiave stessa. Vedere l'esempio seguente di un file di log visualizzato in Excel in cui i tipi di richiesta **Decrypt** e **SignDigest** mostrano che la chiave del tenant è attualmente usata.

    ![file di log visualizzato in Excel in cui è attualmente usata la chiave del tenant](../media/RMS_Logging.gif)

    Per ulteriori informazioni sulla registrazione dei dati di utilizzo, vedere [Registrazione e analisi dell'utilizzo di Azure Rights Management](../deploy-use/log-analyze-usage.md).

3.  Gestire la propria chiave del tenant.

    Per altre informazioni, vedere [Operazioni relative alla chiave del tenant di Azure Rights Management](../deploy-use/operations-tenant-key.md).



<!--HONumber=Jun16_HO2-->


