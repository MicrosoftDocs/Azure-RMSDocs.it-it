---
# required metadata

title: Identificare i requisiti SaaS
description:
keywords:
author: robmazz
manager: swadhwa
ms.date: 04/28/2016
ms.topic: article
ms.prod:
ms.service:
ms.technology:
ms.assetid: 5380e56c-9c48-459e-aea5-95ad90dbb7d1

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: 
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Identificare i requisiti SaaS

>[!NOTE]
>Questo argomento fa parte di una guida più ampia dedicata alle considerazioni di progettazione. Per leggere la guida dall'inizio, vedere l'[argomento principale](mdm-design-considerations-guide.md). Per scaricare una copia della versione integrale della guida, visitare la raccolta [TechNet](https://gallery.technet.microsoft.com/Mobile-Device-Management-7d401582).

Ogni soluzione SaaS avrà requisiti, funzionalità di gestione dei dispositivi mobili e livelli di integrazione con le piattaforme e le reti locali diversi. Molte soluzioni SaaS offrono tenant o servizi di prova per valutare le relative caratteristiche e funzionalità, aspetto importante per determinare quale soluzione sia più adatta alle proprie esigenze. Molte soluzioni SaaS possono tuttavia presentare lievi differenze nelle caratteristiche e nelle funzionalità, a seconda del tipo di piattaforma.

La maggior parte delle soluzioni SaaS si basa su tre tipi di cloud:

- Multi-tenant
- Privato (dedicato)
- Ibrido

Prima di prendere decisioni sulla modalità d'uso di una soluzione SaaS per la gestione dei dispositivi mobili, sarà inoltre necessario esaminare le differenze tra questi tipi di architetture di piattaforma cloud e scegliere quella più adatta alle esigenze complessive dell'organizzazione. Le singole soluzioni SaaS offrono diversi livelli di supporto per aree quali la personalizzazione, la configurazione delle funzionalità, l'integrazione e la collaborazione.

## Tipi di cloud

Le soluzioni SaaS *multi-tenant* in genere vengono definite infrastrutture cloud "pubbliche". In questo caso l'architettura del software del servizio contiene una singola istanza, ma serve più tenant o più organizzazioni. La soluzione è progettata per garantire a ogni tenant una condivisione riservata dei relativi servizi, ad esempio la gestione di utenti o dispositivi, la configurazione e il supporto dati. I servizi e gli account tenant sono virtualmente separati e ogni tenant ha accesso all'infrastruttura della piattaforma tramite istanze distinte. Le soluzioni SaaS multi-tenant in genere offrono inoltre vantaggi in termini di costi, derivati dalla condivisione dell'infrastruttura e dalla distribuzione dei costi generali fra più tenant. La maggior parte delle piattaforme di gestione dei dispositivi mobili è disponibile in un'infrastruttura di piattaforma SaaS multi-tenant.
                
I servizi cloud *privati* o dedicati rappresentano istanze di soluzioni SaaS usate da una singola organizzazione o un singolo tenant. Può trattarsi di servizi cloud privati ospitati dall'organizzazione o di servizi cloud privati ospitati da un provider di terze parti. Le soluzioni cloud private in genere offrono anche maggiori opportunità di personalizzazione nelle aree relative ai servizi e alla sicurezza. Alcune soluzioni dedicate SaaS offrono servizi di gestione dei dispositivi mobili come parte di opzioni relative a tenant cloud privati di maggiori dimensioni.

Le soluzioni SaaS *ibride* possono offrire una combinazione di infrastrutture cloud private e multi-tenant oppure una combinazione di infrastrutture cloud ospitate (multi-tenant o private) e locali. Un'infrastruttura ibrida può includere anche l'utilizzo di una soluzione SaaS cloud esterna per la distribuzione di determinati tipi di servizi, ad esempio di applicazioni, e di risorse interne per altri tipi di servizi. La maggior parte delle soluzioni SaaS offre la possibilità di supportare una configurazione cloud ibrida, ma la profondità e la completezza dell'integrazione con piattaforme cloud ospitate o locali possono variare in modo significativo.

### Domande sul cloud

Come parte della pianificazione del ciclo di vita della gestione SaaS, è necessario rispondere a queste domande sulla pianificazione dei tipi di cloud:

- Qual è il livello di sicurezza necessario per dati dei dispositivi mobili memorizzati nella soluzione SaaS?
- In che modo la soluzione SaaS soddisfa i requisiti di rilevamento delle intrusioni e di prevenzione della perdita dei dati per i dispositivi mobili?
- L'organizzazione deve rispettare requisiti normativi, di certificazione o di conformità per i dispositivi mobili o per i dati archiviati nei dispositivi mobili? In caso affermativo, tali requisiti richiedono un livello di sicurezza, personalizzazione, scalabilità o resilienza specifico? Come viene controllata e rilevata la conformità?
- La soluzione SaaS deve essere connessa con altri servizi o piattaforme cloud che gestiranno i dispositivi mobili? In caso affermativo, tale connettività deve essere:
 - Preconfigurata o standardizzata?
 - Personalizzabile?
 - Supportata dalle piattaforme alle quali è necessario connettersi?
- È necessario connettere la soluzione SaaS con un'infrastruttura locale esistente di gestione dei dispositivi? In caso affermativo, tale connettività deve essere:
 - Supportata dalla piattaforma locale di gestione dei dispositivi?
 - Supportata dalla soluzione SaaS?
 - Supportata senza la necessità di risorse fisiche locali aggiuntive?
- I processi, le applicazioni e i servizi basati su cloud per i dispositivi mobili richiederanno diversi livelli di sicurezza, personalizzazione, scalabilità e resilienza?

## Scalabilità

La facilità di scalabilità è uno dei motivi principali per prendere in considerazione o distribuire una soluzione SaaS per la gestione dei dispositivi mobili nell'organizzazione. Per definizione, le soluzioni SaaS pubbliche offrono in genere la possibilità virtualmente illimitata di supportare un numero qualsiasi di utenti o dispositivi mobili. Le soluzioni SaaS private e ibride possono essere soggette a limiti di scalabilità, in base alle risorse disponibili nell'organizzazione. L'aumento o la diminuzione della scalabilità per supportare un numero maggiore o minore di utenti o dispositivi in genere dipende da un modello specifico di gestione licenze o dal pacchetto di prezzi utente/dispositivo per i cloud pubblici.

### Domande sulla scalabilità

Come parte della pianificazione del ciclo di vita della gestione SaaS, è necessario rispondere a queste domande sulla pianificazione della scalabilità del cloud:

- Di che tipo di piani a breve e a lungo termine dispone l'organizzazione per la crescita o la contrazione dell'infrastruttura di supporto per applicazioni e dispositivi mobili?
- Con quale rapidità l'organizzazione deve aumentare o ridurre i servizi di supporto per la gestione dei dispositivi mobili?
- Qual è il numero iniziale di dispositivi mobili e/o utenti che necessitano di supporto nella soluzione SaaS? Qual è la probabilità che questo numero cambi nell'anno seguente? Nei 3 anni seguenti? Nei 5 anni seguenti?
- Il numero di dispositivi mobili che necessitano di supporto per la soluzione SaaS cambia periodicamente, ad esempio con cadenza stagionale? Il cambiamento dipende dal numero di progetti attivi o inattivi dell'organizzazione?
- Le prestazioni della soluzione SaaS variano a seconda della scalabilità degli utenti e dei dispositivi mobili supportati? In caso affermativo, in quali aree? (nodi, dati, elaborazione e così via) Come viene misurata, rilevata e controllata la scalabilità delle prestazioni?

## Accessibilità

L'accesso facilitato alla soluzione SaaS è un altro componente chiave dell'architettura SaaS. La soluzione SaaS è ospitata in un'infrastruttura basata su cloud, pertanto è accessibile agli amministratori, agli utenti e ai dispositivi da qualsiasi posizione con accesso a Internet. L'amministrazione dei dispositivi mobili viene eseguita tramite un browser. Poiché molti provider di soluzioni SaaS gestiscono centri dati in aree geograficamente diverse, gli utenti e i dispositivi possono accedere "localmente" alla piattaforma, spesso evitando la latenza e i ritardi associati alla connessione con endpoint geograficamente distanti. L'accessibilità in genere può essere anche estesa tramite l'integrazione di soluzioni SaaS con piattaforme locali di gestione dei dispositivi.

### Domande sull'accessibilità

Come parte della pianificazione del ciclo di vita della gestione SaaS, è necessario rispondere a queste domande sulla pianificazione dell'accessibilità del cloud:

- Esistono requisiti specifici del browser per i dispositivi mobili nell'organizzazione? In caso affermativo, la soluzione SaaS supporta i browser richiesti?
- Gli utenti dei dispositivi mobili necessitano di requisiti speciali di accessibilità per le applicazioni o i servizi?
- L'organizzazione necessita dell'accesso all'infrastruttura SaaS che si trova nella stessa area geografica dei dispositivi dell'utente o dell'infrastruttura locale? Esistono conseguenze legali dell'archiviazione o dello spostamento oltre i confini internazionali dei dati dei dispositivi mobili?

## Resilienza

L'infrastruttura di SaaS è basata su cloud ed è ospitata in più centri dati, pertanto la resilienza è in genere meno soggetta a instabilità o a interruzioni rispetto ai servizi tradizionali ospitati localmente. Gli host del servizio in più sedi offrono protezione contro le interruzioni dei servizi basate sull'area geografica tramite l'infrastruttura di failover e processi per la replica dei dati in nodi di più centri dati. A seconda della soluzione SaaS, l'accesso al servizio potrebbe o meno rimanere nell'area geografica originale durante un failover.

### Domande sulla resilienza
 
Come parte della pianificazione del ciclo di vita della gestione SaaS, è necessario rispondere a queste domande sulla pianificazione della resilienza del cloud:

- In caso di failover primario della soluzione SaaS, quale sarà l'impatto sui servizi di gestione dei dispositivi mobili?
- In che modo i dati dei dispositivi mobili archiviati nella soluzione SaaS verranno condivisi in infrastrutture basate su cloud?
- Se il centro dati principale SaaS dei dispositivi mobili non è disponibile, i centri dati di failover si trovano nella stessa area geografica del centro dati principale? I centri dati di failover possono trovarsi all'esterno dei confini internazionali da cui operano i dispositivi mobili?
- La soluzione SaaS dispone di un contratto di servizio definito in cui è delineato il supporto per la gestione dei dispositivi mobili?


## Servizi aggiornati

Le soluzioni SaaS sono inoltre in grado di mantenere aggiornati i servizi e le applicazioni con la versione dell'applicazione, le funzionalità, gli aggiornamenti per la sicurezza e le correzioni di bug più recenti. Spesso questi aggiornamenti vengono pubblicati con frequenza elevata, talvolta anche con cadenza giornaliera. A seconda della soluzione SaaS, gli aggiornamenti possono essere immediatamente disponibili per tutti i clienti o rilasciati per fasi a gruppi più piccoli di clienti. Uno dei vantaggi principali è la possibilità di applicare la correzione di un bug eseguita per un cliente a tutti i clienti che usano il servizio.

### Domande sui servizi

Come parte della pianificazione del ciclo di vita della gestione SaaS, è necessario rispondere a queste domande sulla pianificazione dei servizi cloud:

- Con quale frequenza vengono aggiornate le caratteristiche e le funzionalità di gestione dei dispositivi mobili nel servizio SaaS?
- Quale sarà l'impatto degli aggiornamenti di caratteristiche e funzionalità sui servizi e sulle applicazioni cruciali per i dispositivi mobili?
- Gli aggiornamenti di caratteristiche e funzionalità della soluzione SaaS vengono distribuiti ai clienti in base a una pianificazione ad hoc o programmata?
- La soluzione SaaS supporta esenzioni dagli aggiornamenti a livello di servizio per le singole organizzazioni?
- La soluzione SaaS dispone di pianificazioni diverse per gli aggiornamenti dei servizi per le caratteristiche e funzionalità delle applicazioni per dispositivi mobili e di gestione dei dispositivi mobili?

>[!TIP]
>Assicurarsi di prendere appunti per ogni risposta e di comprendere la logica alla base della risposta. Le attività successive esamineranno le opzioni disponibili e i vantaggi e svantaggi di ogni opzione.  Rispondere a queste domande consentirà di selezionare l'opzione più adatta alle esigenze aziendali.

<!--HONumber=Apr16_HO2-->


