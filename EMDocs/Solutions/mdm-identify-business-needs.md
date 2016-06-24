---
# required metadata

title: Identificazione delle esigenze aziendali
description:
keywords:
author: YuriDio
manager: swadhwa
ms.date: 04/28/2016
ms.topic: article
ms.prod:
ms.service:
ms.technology:
ms.assetid: 85783069-14fb-4ead-a159-657d694eb1a7

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: 
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Identificare le proprie esigenze aziendali

>[!NOTE]
>Questo argomento fa parte di una guida più ampia dedicata alle considerazioni di progettazione. Per leggere la guida dall'inizio, vedere l'[argomento principale](mdm-design-considerations-guide.md). Per scaricare una copia della versione integrale della guida, visitare la raccolta [TechNet](https://gallery.technet.microsoft.com/Mobile-Device-Management-7d401582).

Ogni società dispone di requisiti diversi. Anche se le società appartengono allo stesso settore, i requisiti aziendali effettivi possono variare. È possibile sfruttare le procedure consigliate del settore, ma in definitiva sono le esigenze aziendali che identificano i requisiti della soluzione più adatta per la gestione dei dispositivi mobili. Per identificare più facilmente le esigenze aziendali, rispondere alle domande seguenti:

- **Utenti:** uno degli elementi fondamentali dell'adozione della mobilità consiste nel mettere l'utente al centro della soluzione di mobilità e consentirgli di essere più produttivo, assicurando allo stesso tempo la protezione e la disponibilità dei dati della società. Questo è importante per comprendere quali sono i requisiti dell'utente.
    - L'utente sarà in grado di portare il proprio dispositivo e accedere alle risorse della società?
        - In caso affermativo, quali sono i requisiti per accedere alle risorse della società?
    - La società ha esigenze diverse per gli utenti?
        - In caso affermativo, in che modo il profilo di ciascun utente avrà un impatto sulla strategia di mobilità?
    - Gli utenti saranno in grado di accedere tramite il dispositivo mobile a tutte le app a cui hanno accesso nell'ambiente locale?
        - In caso contrario, quali app saranno disponibili per gli utenti?
            - Queste app sono disponibili per tutte le piattaforme per dispositivi mobili supportate?
            - Sarà necessario modificare o aggiornare eventuali app per eseguirle su tutte le piattaforme per dispositivi mobili supportate?
    - Gli utenti hanno solo bisogno di accesso di base alle funzionalità di posta elettronica (inclusi calendario, contatti e attività)?

- **Proprietà dei dispositivi:** è necessario comprendere i criteri di proprietà dei dispositivi per la società.
    - Chi è proprietario del dispositivo mobile? 
        - Il dipendente?
        - La società?  
        - Entrambi?
- **Piattaforme:** comprendere quali sistemi operativi per dispositivi mobili verranno usati dalla società è molto importante per le decisioni relative ad adozione e supporto.
    - Quali sistemi operativi per dispositivi mobili saranno supportati?
        - Android?
        - iOS?
        - Microsoft Windows?,
        - Windows Phone?
        - Tutti?
        - Una combinazione delle opzioni precedenti?
    - Quale versione del sistema operativo per dispositivi mobili sarà supportata?
        - Solo la più recente?
        - Versione attuale -1 (la versione attuale più la versione precedente)?
- **Applicazioni:** poiché il motivo principale dell'adozione della mobilità è l'aumento della produttività, le applicazioni (app) usate dai dipendenti devono poter essere eseguite in tutti i sistemi operativi dei dispositivi mobili usati nell'organizzazione. Si tratta di un punto importante da tenere in considerazione, perché sebbene in alcune società le app principali possono essere completamente portatili per l'esecuzione in un ambiente mobile, in altre può essere necessario comprendere quali opzioni sono disponibili per aiutarle a distribuire le proprie app sui dispositivi mobili. Per semplificare l'identificazione dei requisiti delle singole app, è opportuno porsi le domande seguenti.
    - Le app richiedono l'accesso a Internet dai dispositivi degli utenti? 
    - Le app raccolgono informazioni personali sull'utente?
        - In tal caso, le app informano gli utenti sulle questioni di privacy e sulla raccolta dei dati durante l'installazione?
    - Le app richiedono l'integrazione con i servizi cloud?
        - Le app sono state sviluppate per l'esecuzione in un sistema operativo o possono essere eseguite in qualsiasi sistema operativo?
    - Si ha intenzione di consentire agli utenti di usare le app tramite Desktop remoto dai propri dispositivi personali?
    - Le app richiedono l'accesso a tempo pieno alle risorse aziendali o possono essere eseguite in modalità offline?
    - Le app sono integrate con i social network?
    - Per gli utenti BYOD saranno disponibili tutte le app?
    - Come si intende distribuire queste app ai dispositivi degli utenti?
    - Quali sono le opzioni di distribuzione per queste app?
    - Il requisito di installazione varia a seconda del dispositivo di destinazione o è lo stesso?
    - Quanto spazio è necessario in un dispositivo di destinazione per installare ogni app? 
    - Le app eseguono la crittografia dei dati prima della trasmissione attraverso la rete dai dispositivi degli utenti al server app nel back-end?
    - Le app possono essere disinstallate in remoto attraverso la rete o devono essere disinstallate tramite le console dei dispositivi?
    - La società ha l'esigenza di consentire l'accesso ai dati delle applicazioni SaaS ai propri partner?
    - Le app funzionano in una rete a bassa latenza? 
    - Le app forniscono le funzionalità di autenticazione?
        - In tal caso, quale metodo di autenticazione usano le app?

Durante questa attività, è anche necessario valutare se la società dispone di criteri di gestione e conformità esistenti per dispositivi mobili e in che modo questi criteri possono influire sulla scelta della soluzione di gestione dei dispositivi mobili.

>[!TIP] Assicurarsi di prendere appunti per ogni risposta e di comprendere la logica alla base della risposta. La sezione successiva esaminerà le opzioni disponibili e i vantaggi e svantaggi di ogni opzione.  Avendo risposto a queste domande, sarà possibile selezionare la soluzione più adatta a soddisfare le esigenze aziendali.




<!--HONumber=Jun16_HO1-->


