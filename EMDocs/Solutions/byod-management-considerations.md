---
# required metadata

title: Considerazioni sulla gestione
description:
keywords:
author: YuriDio
manager: swadhwa
ms.date: 04/28/2016
ms.topic: article
ms.prod:
ms.service:
ms.technology:
ms.assetid: ba8cc256-2075-457f-a827-7ec9213c5235

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: 
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Considerazioni sulla gestione

Un dominio di gestione è obbligatorio in un'infrastruttura che supporta un modello BYOD. Per supportare completamente le richieste del BYOD, il dominio di gestione deve poter consentire al reparto IT di monitorare le risorse, fornire funzionalità di creazione di rapporti, gestire le risorse di calcolo e archiviazione, abilitare la configurazione e l'automazione dei dispositivi e gestire la distribuzione e il provisioning delle app.

## Monitoraggio

Uno dei ruoli del dominio di gestione è monitorare le impostazioni di conformità, non solo per le risorse aziendali, ma anche per i dispositivi mobili di proprietà degli utenti. È opportuno valutare le considerazioni sulla conformità in base alla line of business dell'azienda. Alcune aziende potrebbero consentire che i dati aziendali risiedano nei dispositivi degli utenti solo se crittografati. Le impostazioni di sicurezza devono essere controllate dal reparto IT in modo da applicare tali criteri.

Il livello di gestione nei dispositivi degli utenti varia in base ai criteri aziendali e all'infrastruttura BYOD adottata dall'azienda. Se l'azienda stabilisce che è necessario fornire una funzionalità di cancellazione completa per accedere alle risorse aziendali, il reparto IT deve applicare questa impostazione su tutti i dispositivi monitorati. Il reparto IT deve inoltre poter ripristinare le impostazioni di fabbrica dei dispositivi, cancellando tutte le impostazioni e i dati personali, se necessario. La sezione seguente consente di determinare le opzioni di monitoraggio che saranno necessarie per l'infrastruttura BYOD.

### Opzioni di monitoraggio: vantaggi e svantaggi

Usare l'elenco che segue per comprendere i vantaggi e gli svantaggi di ogni opzione di monitoraggio:

- Agente di gestione installato nei dispositivi degli utenti
    - Vantaggi
        - Maggiore controllo sui dispositivi degli utenti
        - Funzionalità di cancellazione remota
        - Funzionalità di cancellazione selettiva
        - Gestione del ciclo di vita e della distribuzione delle app più veloce
    - Svantaggi
        - Necessità di installare un agente di gestione nei dispositivi degli utenti
        - Più intrusivo dal punto di vista degli utenti
        - Richiede un'infrastruttura di gestione back-end per supportare l'agente
- Agente di gestione non installato
    - Vantaggi
        - Non viene installato alcun agente di gestione nei dispositivi degli utenti
        - Applicazione dei criteri disponibile solo dal punto di vista delle app, ad esempio ActiveSync
    - Svantaggi
        - Disponibilità limitata di opzioni per la gestione dei dispositivi da parte del reparto IT

Come si vede nella tabella precedente, quando si progetta la soluzione di infrastruttura BYOD, se si desidera applicare i criteri aziendali, è necessario un agente installato nei dispositivi degli utenti.

Se l'azienda sceglie di supportare diversi tipi di dispositivi, è necessario comprendere le funzionalità dei dispositivi, ad esempio la crittografia di archiviazione, le opzioni di connettività VPN e i linguaggi di programmazione supportati. Valutare ciò che è possibile implementare per mantenere la conformità ai criteri aziendali. Il monitoraggio dei dispositivi per rispettare la conformità può essere eseguito con l'applicazione dei criteri. Provare ad abilitare la crittografia dei dispositivi mentre i dati sono inattivi nei dispositivi degli utenti. In questo modo sì può semplificare la strategia di prevenzione della perdita dei dati. L'applicazione di criteri, come ad esempio lo sblocco delle password, la cronologia delle password e le password complesse, può fornire una sicurezza simile nei dispositivi locali e mobili.

Le impostazioni di conformità in Configuration Manager consentono al reparto IT di gestire la configurazione e la conformità di server, computer portatili, computer desktop e dispositivi mobile all'interno dell'azienda. Provare a usare le impostazioni di conformità predefinite incorporate in Configuration Manager per i dispositivi mobili come punto di partenza e da lì personalizzare in base alle esigenze dell'azienda. Per altre informazioni sulle impostazioni di conformità in Configuration Manager, vedere [Introduzione alle impostazioni di conformità in Configuration Manager](https://technet.microsoft.com/en-us/library/gg682139.aspx).

Con la cancellazione selettiva di Windows il reparto IT può proteggere i dati aziendali dell'organizzazione dislocati nei dispositivi personali o aziendali. Gli sviluppatori possono creare delle app per usare un criterio di cancellazione selettiva di Windows sui dati proteggendoli in un dominio Internet di proprietà dell'organizzazione. Per altre informazioni sulla cancellazione selettiva di Windows, vedere Cancellazione selettiva di Windows per la gestione dei dati del dispositivo.

## Reporting

Le funzionalità di creazione di rapporti o semplicemente comprendere il comportamento di questi dispositivi è fondamentale per il reparto IT per mantenere il controllo dei dispositivi noti. I rapporti possono essere usati per comprendere meglio l'ambiente corrente. Di seguito sono indicate alcune domande che sorgono quando si prova a comprendere non solo l'ambiente, ma anche le funzionalità di alcuni dispositivi mobili:

- Quanti dispositivi iOS sono in uso nell'organizzazione?
- Quali versioni iOS sono in esecuzione in tali dispositivi?
- Quali app aziendali sono installate nei dispositivi?
- Ci sono dispositivi nell'organizzazione che sono stati sottoposti a jailbreak?

Provare a usare una soluzione di gestione in grado di fornire l'inventario dei dispositivi e rapporti personalizzabili. Se si sceglie questa opzione, si consentirà un approccio più flessibile per il reparto IT quando occorre individuare altre informazioni sui dispositivi degli utenti. Il reparto IT deve poter avere i rapporti su tutti i dispositivi che sono stati registrati in locale e nel cloud. La funzionalità di creazione di rapporti per il sistema di gestione può risiedere in locale o nel cloud, oppure può essere una combinazione di entrambe le soluzioni, denominata appunto soluzione ibrida. Usare la tabella seguente per determinare quale opzione di creazione di rapporti è appropriata per l'azienda.

### Opzioni di creazione di report: vantaggi e svantaggi

Usare l'elenco che segue per comprendere i vantaggi e gli svantaggi di ogni opzione di creazione di report:

- Infrastruttura locale
    - Vantaggi
        - Report centralizzato
        - Controllo completo del reparto IT
        - Personalizzabile
        - Controlli di sicurezza gestiti a livello locale
    - Svantaggi
        - Impossibile enumerare in modo nativo i dispositivi non locali
        - Maggiore sovraccarico amministrativo, rispetto alle soluzioni basate su cloud
- Basata su cloud
    - Vantaggi
        - Possibilità di creare report sui dispositivi che fanno parte del servizio cloud
        - Convenienza
        - Possibilità di creare e visualizzare i report da qualsiasi posizione
        - Costi amministrativi più bassi rispetto a una soluzione locale
    - Svantaggi
        - Impossibile enumerare in modo nativo i dispositivi locali
        - In genere richiede una sottoscrizione mensile al servizio
- Strategia ibrida
    - Vantaggi
        - Possibilità di creare report sui dispositivi che fanno parte del servizio cloud
        - Convenienza
        - Possibilità di creare e visualizzare i report da qualsiasi posizione
        - Integrazione con la soluzione di gestione locale
    - Svantaggi
        - In genere richiede una sottoscrizione mensile al servizio.

Grazie alla combinazione di Microsoft Intune con System Center 2012 R2, è possibile usare la funzionalità di creazione di report sia nei dispositivi locali che in quelli basati su cloud. Configuration Manager include molti rapporti predefiniti pronti per l'uso per UDM, inclusi i rapporti per le app, l'inventario hardware e la gestione delle impostazioni. Non è necessario creare rapporti personalizzati o separati per la gestione di PC e dispositivi mobili. Queste funzioni possono essere integrate.

Per altre informazioni sulle funzionalità di creazione di report di Configuration Manager, vedere [Introduzione alla creazione di report in Configuration Manager](https://technet.microsoft.com/library/gg682105.aspx).

## Calcolo e archiviazione

Dopo aver sviluppato nuove app e averne consentito l'accesso in remoto agli utenti dai propri dispositivi, le prestazioni delle app potrebbero risultare ridotte se la soluzione non è stata ben pianificata. Sebbene questa Guida alle considerazioni di progettazione non intenda offrire un'analisi approfondita relativa alle considerazioni sulle prestazioni, è necessario rispondere ad alcune domande sull'infrastruttura di gestione:

- La soluzione di gestione esistente usata dall'azienda è in grado di gestire le risorse di archiviazione e di calcolo per la piattaforma supportata dalle app a cui accedono i dispositivi degli utenti? 
- La soluzione di gestione esistente usata dall'azienda è in grado di aumentare le risorse di calcolo e di archiviazione per la piattaforma supportata dall'app a cui accedono i dispositivi degli utenti in base a un set di regole prestabilite?
Se la soluzione di gestione esistente non è in grado di soddisfare questi due requisiti, valutare l'utilizzo di una soluzione di gestione che possa gestire il calcolo e l'archiviazione affrontando i due requisiti fondamentali illustrati nella tabella seguente.

### Funzionalità di gestione di calcolo e archiviazione: vantaggi e svantaggi

Usare l'elenco che segue per comprendere i vantaggi e gli svantaggi di ogni opzione di gestione delle funzionalità:

- Pool di risorse
    - Vantaggi
        - Possibilità di allocare risorse di calcolo e archiviazione da un pool di risorse in percorsi diversi
        - Livello elevato di disponibilità.
        - Maggiore affidabilità rispetto alle soluzioni che non sono in grado di sfruttare il pooling delle risorse
    - Svantaggi
        - Poche soluzioni di gestione sono in grado di sfruttare i vantaggi offerti dal pooling delle risorse
        - Il sovraccarico iniziale da implementare può essere superiore se l'azienda non usa ancora i principi del cloud computing nel proprio centro dati
- Elasticità
    - Vantaggi
        - Possibilità di allocare in modo dinamico risorse di calcolo e archiviazione da un pool di risorse in base alle esigenze
        - Livello elevato di disponibilità
        - Maggiore semplicità di gestione dopo l'implementazione
    - Svantaggi
        - Poche soluzioni di gestione sono in grado di sfruttare i vantaggi offerti dalle funzionalità di elasticità
        - Il sovraccarico iniziale da implementare può essere superiore se l'azienda non usa ancora i principi del cloud computing nel proprio centro dati

System Center 2012 R2 è in grado di usare il pooling delle risorse e l'elasticità per gestire il calcolo e l'archiviazione. System Center 2012 R2 inoltre integra l'archiviazione con l'ottimizzazione dei dischi differenze per ridurre i requisiti di archiviazione, consentendo la condivisione di una grande percentuale di dati del disco tra più dischi virtuali e ottimizzando in tal modo i costi di archiviazione. I server virtualizzati con System Center 2012 R2 e che verranno usati dalle app degli utenti remoti possono avvalersi di questa tecnologia.

Per altre informazioni sulle funzionalità di archiviazione di System Center 2012 R2, vedere [Novità di VMM in System Center 2012 R2](https://technet.microsoft.com/library/dn246490.aspx). 

## Automazione

L'automazione può essere utilizzata per correggere i dispositivi non conformi e il reparto IT può assegnare diversi livelli di gravità della non conformità. È consigliabile usare l'automazione in diverse aree del BYOD, ad esempio potrebbe essere utile automatizzare la distribuzione dei nuovi servizi che verranno utilizzati dai dispositivi mobili e automatizzare il processo di autorizzazione per i dispositivi mobili.

Sebbene si noterà che tutti i sottodomini BYOD presentati possono sfruttare i vantaggi offerti dall'automazione, la responsabilità di automatizzare le risorse appartiene al sottodominio di gestione. L'automazione può essere integrata nel sistema operativo. Tuttavia, la soluzione di gestione che verrà adottata dall'azienda dovrà estendere tali funzionalità e consentire di ridurre le attività IT quotidiane per il monitoraggio e la creazione di rapporti sui risultati dell'automazione.
L'opzione di automazione più potente in System Center 2012 R2 è Windows PowerShell. Per altre informazioni sull'automazione di System Center 2012 R2, vedere [Automazione di System Center con Windows PowerShell](https://technet.microsoft.com/library/dn507037(v=sc.20).aspx). Tuttavia, è disponibile un'altra opzione che fornisce un tipo più semplice ma non molto affidabile di automazione delle attività: la sequenza di attività. Usare la tabella seguente per valutare i vantaggi e gli svantaggi di ogni opzione.

### Opzioni di automazione: vantaggi e svantaggi

Usare l'elenco che segue per comprendere i vantaggi e gli svantaggi di ogni opzione di automazione:

- Windows PowerShell
    - Vantaggi
        - Integrato con il sistema operativo
        - Più affidabile della sequenza di attività
        - Gestibile tramite script
        - Può usare principi di programmazione come procedure, cicli e matrici
        - Fornisce funzionalità oltre la piattaforma di gestione
    - Svantaggi
        - Richiede maggiori competenze tecniche per l'uso
        - In base all'attività in corso, lo sviluppo dello script di automazione iniziale potrebbe richiedere più tempo
- Sequenza di attività
    - Vantaggi
        - Facilità d'uso
        - Funzionalità nativa disponibile in System Center
    - Svantaggi
        - Funzionalità limitata
        - Non gestibile tramite script
        - Le funzionalità sono limitate per alcune attività all'interno dello stesso System Center

## Distribuzione e provisioning

Il passaggio successivo consiste nel comprendere le considerazioni per la distribuzione e il provisioning delle app per dispositivi remoti. Sorgono due domande fondamentali a cui rispondere:

- Come potranno accedere gli utenti alle app dai propri dispositivi?
- Come potrà il reparto IT eseguire il provisioning di queste app per gli utenti in modo efficace e descrittivo?

La soluzione di gestione che verrà adottata dall'azienda dovrà essere orientata anche alla distribuzione del software e al provisioning, indipendentemente dalla piattaforma usata dall'utente. Gli utenti devono essere in grado di accedere in modo sicuro a una posizione centralizzata dai propri dispositivi e installare le app a cui sono autorizzati per eseguire il lavoro.

Una sfida in quest'area è poter gestire diverse piattaforme mantenendo un'interfaccia di gestione centralizzata che consenta al reparto IT di identificare rapidamente i dispositivi connessi in locale e nel cloud. È necessario prendere in considerazione l'adozione di una piattaforma di gestione che consenta di consolidare entrambe le soluzione (in locali e nel cloud), nonché una piattaforma di gestione che sia in grado di gestire sistemi Windows e non Windows.

Per la gestione centralizzata in locale, è possibile usare Configuration Manager. Con questa opzione il reparto IT può sfruttare la funzionalità di registrazione aziendale per registrare i dispositivi con il server di Configuration Manager dell'azienda. Per altre informazioni sulla gestione dei dispositivi con Configuration Manager, vedere [Gestire i dispositivi mobili con Configuration Manager e Microsoft Intune](https://technet.microsoft.com/en-us/library/jj884158.aspx).

Per gestire altre piattaforme che non sono dispositivi basati su Windows, è possibile usare il servizio cloud di Microsoft Intune. Il portale aziendale di Microsoft Intune consente di registrare, gestire e installare le app concesse in licenza. Gli utenti possono accedere facilmente alle app e installarle sui propri dispositivi. 

>[!TIP] 
>Per altre informazioni su Microsoft Intune, vedere [Introduction to Intune](/intune/understand-explore/introduction-to-microsoft-intune) (Introduzione a Intune). 

Sebbene si tratti di due opzioni distinte, è possibile integrarle per fornire la distribuzione delle app e il provisioning da un'unica posizione. Usare la tabella seguente per identificare l'opzione appropriata al progetto BYOD.

| **Requisiti di progettazione**                                             | **Opzioni di distribuzione e provisioning**                |
|---------------------------------------------------------------------|--------------------------------------------------------|
| Distribuzione e provisioning di app in dispositivi presenti solo in locale.      | Microsoft System Center 2012                           |
| Distribuzione e provisioning di app in dispositivi che si trovano all'esterno dell'azienda.   | Microsoft Intune                                       |
| Distribuzione e provisioning di app in dispositivi non Windows.                   | Microsoft Intune                                       |
| Distribuzione e provisioning di app solo nei dispositivi locali, distribuzione e provisioning di app nei dispositivi situati all'esterno dell'azienda o distribuzione e provisioning di app nei dispositivi non Windows.       | Microsoft Intune integrato con Configuration Manager
                                                                    


<!--HONumber=Apr16_HO4-->


