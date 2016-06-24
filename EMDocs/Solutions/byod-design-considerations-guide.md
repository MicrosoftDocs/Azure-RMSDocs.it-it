---
# required metadata

title: Guida alle considerazioni di progettazione per BYOD
description:
keywords:
author: YuriDio
manager: swadhwa
ms.date: 04/28/2016
ms.topic: article
ms.prod:
ms.service:
ms.technology:
ms.assetid: ed940ba8-866c-477f-a59b-beb620300a79

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: 
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Guida alle considerazioni di progettazione per BYOD

Con l'aumentare del numero di dispositivi usati dai dipendenti, la maggior parte delle organizzazioni si trova ad affrontare un problema non indifferente: consentire agli utenti di usare i dispositivi personali, proteggendo al tempo stesso i dati aziendali che si trovano in tali dispositivi. Si sta abbandonando il modello tradizionale, in cui l'azienda possiede e fornisce i dispositivi ai dipendenti, per passare a un modello in cui i dipendenti usano i dispositivi personali per alcune delle proprie attività lavorative. Questo modello viene spesso definito [Bring Your Own Device (BYOD)](https://technet.microsoft.com/library/dn645493.aspx). In questo modello i dipendenti possono usare i dispositivi personali per alcune attività lavorative, ma solo se consentono all'azienda di gestire alcuni aspetti dei loro dispositivi per garantire la sicurezza dei dati aziendali. Spesso, ciò significa che gli utenti autorizzano l'azienda a usare criteri personalizzati, applicare la protezione avanzata dei dispositivi o standardizzare il sistema operativo stabilito dai criteri aziendali. Leggendo il documento di Microsoft con le [considerazioni dei responsabili IT sulla trasformazione del modo di lavorare](http://download.microsoft.com/download/5/3/A/53A96632-02E3-416C-B209-D8725AA80AFE/CIO%20Considerations%20for%20Workstyle%20Transformation2.pdf), i dirigenti e i decisori possono anche identificare i vantaggi della scelta di un modello in cui le persone possono usare i propri dispositivi per essere più produttive al lavoro.

L'accesso ai dati e la protezione sono i principali problemi del modello BYOD, ma altre problematiche richiedono un approccio più ampio:

- Utenti e dispositivi: come è possibile consentire agli utenti di usare i propri dispositivi mantenendo la conformità ai criteri aziendali?
- Gestione: come verranno gestiti dal reparto IT i dispositivi non aziendali?
- App: come si accederà alle app line-of-business dai dispositivi degli utenti?

La decisione dipende dai requisiti, dalle funzionalità e dalle considerazioni di progettazione per un'infrastruttura di gestione dei dispositivi. Le tecnologie Microsoft sono considerate nel contesto dei requisiti e delle funzionalità, non viceversa. Si prevede che questo approccio avrà maggiore successo con gli architetti e i progettisti interessati ai problemi che devono essere risolti e ai metodi disponibili per risolverli. Solo a questo punto la scelta della tecnologia è rilevante.

Questa guida offre all'architetto di sistema e al responsabile della progettazione sistemi una serie di importanti considerazioni di progettazione da valutare prima di progettare un'infrastruttura BYOD (Bring Your Own Device) che consenta ai dipendenti di usare i propri dispositivi proteggendo i dati della società.

## Destinatari

I principali destinatari di questa guida sono gli architetti o i progettisti di sistema interessati alla comprensione dei problemi da prendere in considerazione prima di implementare un'infrastruttura BYOD. Altri possibili destinatari della guida sono i responsabili dell'implementazione IT, gli addetti alla sicurezza aziendale e gli esperti di gestione dei dispositivi.</para>
    
## Scopo
  
Lo scopo di questa guida è:

1. Fornire agli architetti o progettisti di sistema una serie di problemi e domande a cui rispondere per definire i requisiti per la progettazione di un'infrastruttura BYOD.
2. Fornire agli architetti o progettisti di sistema un insieme di opzioni di progettazione che possono essere valutate e scelte in base ai requisiti identificati. 

Le domande proposte possono essere usate per qualsiasi fornitore, ma gli esempi di opzioni disponibili si basano sulle funzionalità di Windows Server 2012 R2, System Center 2012 R2 e Microsoft Intune.

Questa guida include anche:

- Considerazioni di progettazione indipendenti dal fornitore per adattare un'infrastruttura per il modello BYOD. 
- Considerazioni di progettazione per gli utenti, i dispositivi, le piattaforme di gestione, le app e l'accesso ai dati e la relativa protezione.

Prima di adottare un modello BYOD in un ambiente di produzione, è necessario considerare i problemi di sicurezza, disponibilità, prestazioni e scalabilità per aree quali le connessioni di rete, l'archiviazione, il calcolo e la gestione delle identità. Si tende spesso a voler passare al modello BYOD prima di avere effettuato un'analisi concreta dell'ambiente corrente e delle operazioni da eseguire per permettere agli utenti di lavorare in modo sicuro da qualsiasi dispositivo ovunque.

*Non* è tra gli scopi di questa guida:

- Fornire indicazioni sulle prestazioni per i componenti dell'infrastruttura di un modello BYOD. 
- Suggerire ottimizzazioni delle prestazioni e procedure consigliate per i componenti dell'infrastruttura BYOD.
- Fornire linee guida per lo sviluppo di app per dispositivi mobili.
- Fornire procedure consigliate per lo sviluppo di app per dispositivi mobili.
- Dare indicazioni e suggerire procedure consigliate per componenti di terze parti.

## Definizione del problema

I problemi o le perplessità seguenti sono in genere quelli incontrati dalle aziende che provano ad adottare il BYOD:

- La piattaforma di gestione esistente non è in grado di consentire agli utenti di connettere i propri dispositivi e di accedere alle risorse aziendali.
- La strategia di sicurezza esistente non risolve le problematiche di sicurezza introdotte dal BYOD nell'ambiente.
- Gli utenti stanno adottando nuove tecnologie e richiedono l'accesso alle risorse aziendali per svolgere il proprio lavoro.
- I responsabili delle decisioni aziendali comprendono i vantaggi che il BYOD apporta all'azienda, principalmente nella produttività dell'utente consentendo di ridurre i costi operativi. Tuttavia, responsabili delle decisioni aziendali non sono sicuri di come adottare il BYOD rimanendo conformi alle regole e alle normative.

Le organizzazioni con un'infrastruttura di grandi dimensioni devono stabilire i requisiti prima di passare dalla gestione dei dispositivi stessi, in cui si presume che il reparto IT abbia il controllo totale dei dispositivi, a un modello in cui si presume che il reparto IT abbia meno controllo dei dispositivi ma allo stesso tempo debba soddisfare le esigenze degli utenti per l'accesso ai dati aziendali. Questo modello viene spesso definito come passaggio da un approccio IT incentrato sui dispositivi a uno incentrato sugli utenti. È necessario inoltre pianificare attentamente le stesse considerazioni e gli stessi requisiti per le app nuove ed esistenti o per lo spostamento delle app esistenti in un ambiente cloud. La Figura 1 include un diagramma concettuale del dominio del problema BYOD e delle aree trattate in questa guida.

![Dominio problematico](./media/BYOD_Figure1.png)



<!--HONumber=Apr16_HO4-->


