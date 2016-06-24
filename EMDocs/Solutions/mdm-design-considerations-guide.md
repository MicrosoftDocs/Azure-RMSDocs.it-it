---
# required metadata

title: Guida alle considerazioni sulla progettazione per la gestione dei dispositivi mobili
description:
keywords:
author: andredm7
manager: swadhwa
ms.date: 05/31/2016
ms.topic: article
ms.prod:
ms.service:
ms.technology:
ms.assetid: 7083b6b8-27a3-427b-b505-25d007d63cdd

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: 
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Guida alle considerazioni sulla progettazione per la gestione dei dispositivi mobili

Con tutte le diverse opzioni di progettazione e configurazione per le soluzioni di gestione dei dispositivi mobili (MDM), talvolta è difficile determinare la soluzione più adatta a soddisfare le esigenze dell'organizzazione. Questa guida alla progettazione consente di comprendere i requisiti di progettazione MDM e illustra una serie di passaggi e attività da seguire per progettare una soluzione MDM adatta alle esigenze aziendali e tecnologiche dell'organizzazione. 

## Introduzione

Nei passaggi e nelle attività di questa guida verranno presentate le tecnologie pertinenti e le opzioni di funzionalità disponibili per le organizzazioni per soddisfare i requisiti funzionali e di qualità del servizio (ad esempio disponibilità, scalabilità, prestazioni, gestibilità e sicurezza).

In particolare, questa guida consente dir rispondere alle domande seguenti:

- A quali domande è necessario rispondere per favorire l'adozione della soluzione di gestione dei dispositivi mobili che meglio soddisfa i requisiti aziendali?
- Qual è la sequenza di attività da completare per progettare una soluzione di gestione dei dispositivi mobili per l'organizzazione?
- Quali opzioni di configurazione e di tecnologia Microsoft per la gestione della mobilità sono disponibili per soddisfare i requisiti e quali sono i compromessi tra tali opzioni?

**Destinatari della guida** Architetti e professionisti IT responsabili della progettazione di una soluzione per la gestione dei dispositivi mobili per organizzazioni di medie o grandi dimensioni.

**Finalità della guida.** Questa guida è utile per comprendere come progettare una soluzione di gestione dei dispositivi mobili in grado di gestire i dispositivi di proprietà dell'azienda e i dispositivi personali degli utenti in diversi fattori di forma.

![Esempio di una soluzione MDM ibrida con Intune e System Center Configuration Manager](./media/MDM_Figure_01.png)
**Esempio di una soluzione MDM ibrida con Intune e System Center Configuration Manager**

La figura precedente illustra un esempio di soluzione di gestione ibrida, che usa i servizi cloud per l'integrazione con funzionalità locali allo scopo di gestire tutti i tipi di dispositivi, indipendentemente dalla loro posizione. Sebbene si tratti di uno scenario molto comune, la progettazione di gestione dei dispositivi mobili di ogni organizzazione potrebbe essere diversa dall'esempio per via dei requisiti di gestione specifici di ogni organizzazione.
 
Questa guida illustra in dettaglio una serie di passaggi e attività da seguire per facilitare la progettazione di una soluzione MDM personalizzata che soddisfi i requisiti specifici della propria organizzazione. Nei passaggi e nelle attività di questa guida vengono illustrate le tecnologie rilevanti e le opzioni di funzionalità disponibili per soddisfare i requisiti funzionali e di qualità del servizio per la gestione dei dispositivi mobili. 

Questa guida consente di progettare una soluzione MDM, ma non descrive opzioni specifiche relative all'implementazione o alle operazioni per le soluzioni di gestione, né le modalità per la migrazione da una soluzione MDM di terze parti esistente. Per altri dettagli sulle procedure di configurazione e distribuzione per [Microsoft Intune](/Intune/), [Gestione dei dispositivi mobili per Office 365](https://technet.microsoft.com/library/ms.o365.cc.devicepolicy.aspx) e [Microsoft System Center Configuration Manager](https://technet.microsoft.com/library/cc507089.aspx) visitare il sito docs.microsoft.com e le librerie TechNet usando i collegamenti disponibili nella sezione **Passaggi successivi e risorse aggiuntive** alla fine di questa guida.

È anche possibile trovare istruzioni sulla migrazione da altre soluzioni MDM in Microsoft Intune [qui](https://blogs.technet.microsoft.com/intunesupport/2016/02/10/new-guide-on-how-to-migrate-from-other-mdm-technologies-to-microsoft-intune/).

**Presupposti:** si ha familiarità con Microsoft Intune, System Center 2012 R2 Configuration Manager, Windows Server 2012 R2 e i dispositivi mobili che eseguono Windows Phone, iOS e Android. Si è già implementata una di queste soluzioni in un ambiente di produzione limitato o in un test iniziale per la gestione dei dispositivi mobili. In questa guida si presuppone che si desideri comprendere in che modo queste soluzioni possano soddisfare le esigenze aziendali in modo autonomo o in una soluzione integrata.

## Considerazioni sulla progettazione MDM
Questa guida illustra una serie di passaggi e attività da eseguire per progettare la soluzione più adatta ai propri requisiti. I passaggi sono presentati in una sequenza ordinata. Le considerazioni sulla progettazione apprese nei passaggi successivi potrebbero tuttavia richiedere una modifica delle decisioni prese nei passaggi precedenti, a causa di possibili conflitti nelle scelte di progettazione o dell'evoluzione della progettazione. In questa guida verranno segnalati potenziali conflitti di progettazione.

Per sviluppare una progettazione per la gestione dei dispositivi mobili adatta alle proprie esigenze, sarà necessario ripetere i passaggi seguenti finché non saranno state integrare tutte le considerazioni illustrate nella guida: 

- [Passaggio 1: Identificare i requisiti di gestione dei dispositivi mobili](mdm-step-1-identify-your-mobile-device-management-requirements.md)
- [Passaggio 2: Pianificare la gestione dei dispositivi mobili](mdm-step-2-plan-for-mobile-device-management.md)
- [Passaggio 3: Pianificare la protezione dei dispositivi mobili](mdm-step-3-plan-enhancing-mobile-devices-protection.md)
- [Passaggio 4: Pianificare la gestione dei dispositivi mobili SaaS (Software as a Service)](mdm-step-4-plan-for-software-as-a-service-mobile-device-management.md)
- [Passaggi successivi e risorse aggiuntive](mdm-next-steps-and-additional-resources.md)
        
## Versione scaricabile
È possibile scaricare una copia della versione integrale della guida dalla raccolta [TechNet](https://gallery.technet.microsoft.com/Mobile-Device-Management-7d401582).


<!--HONumber=Jun16_HO1-->


