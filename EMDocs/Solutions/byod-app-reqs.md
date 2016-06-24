---
# required metadata

title: Requisiti delle app
description:
keywords:
author: YuriDio
manager: swadhwa
ms.date: 04/28/2016
ms.topic: article
ms.prod:
ms.service:
ms.technology:
ms.assetid: 0c1313b9-361f-4732-a92c-23d0dac07733

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: 
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Requisiti delle app

Ogni organizzazione usa una serie di funzionalità tecniche per consentire al personale di eseguire le attività in modo ottimizzato e quasi sempre lo strumento principale è un'app. Queste funzionalità possono essere combinate in un approccio multipiattaforma in cui vengono usate diverse tecnologie per raggiungere un determinato obiettivo o tramite la creazione di un'app personalizzata in grado di eseguire un'attività o di automatizzare alcuni processi. Le app sono importanti da considerare per la progettazione della strategia BYOD. Gli utenti useranno diversi fattori di forma per l'impiego queste app. Pertanto, è necessario considerare la varietà di funzionalità che tali app devono supportare. La figura sottostante illustra il modo in cui utenti e dispositivi usano le app per l'impiego dei dati e le considerazioni per ogni componente del sottodominio Apps.

![Requisiti delle app](./media/BYOD_Figure5.png)

La sezione seguente contiene le domande sui requisiti delle app a cui è necessario rispondere per formulare i requisiti per la progettazione della soluzione.

## Domande da chiedere

I requisiti delle app sono classificati in sei aree:

- Esperienza
- Piattaforma
- Distribuzione
- Archiviazione
- Rete
- Sicurezza


### Esperienza

- Si intende conservare la stessa esperienza utente, indipendentemente dai dispositivi in cui verranno eseguite le app?
- Le app richiedono l'accesso a Internet dai dispositivi degli utenti?
- Le app richiedono l'input tramite tastiera?
- Le app raccolgano le informazioni sull'utente, ad esempio la posizione geografica?
    - In tal caso, le app informano gli utenti sulle questioni di privacy e sulla raccolta dei dati durante l'installazione?
- Le app richiedono l'integrazione con i servizi cloud?
- Quali tipi di app si intende rendere disponibili per gli utenti BYOD (ad esempio app basate su Web e app moderne)?
- Le app sono state sviluppate per l'esecuzione in un sistema operativo o possono essere eseguite in qualsiasi sistema operativo?
- Si intende consentire agli utenti di usare le app tramite Desktop remoto dai propri dispositivi personali?
- Le app richiedono l'accesso a tempo pieno alle risorse aziendali o possono essere eseguite in modalità offline?
- Le app sono integrate con i social network?


### Piattaforma

- Quale tipo di piattaforma back-end è necessaria per l'esecuzione di queste app?
- Si prevede un aumento dell'attività con l'adozione di BYOD che richiederà l'aggiornamento della piattaforma back-end per le app che dovranno essere usate dagli utenti remoti?
- La piattaforma back-end che supporterà le app risiede nella stessa infrastruttura degli altri server?
- La piattaforma che supporterà le app è completamente in locale o ci sono anche server che risiedono nel cloud?


### Distribuzione

- Si sa quali app saranno disponibili per gli utenti BYOD?
- Come si intende distribuire queste app ai dispositivi degli utenti?
- Quali sono le opzioni di distribuzione per queste app?
- Il requisito di installazione varia a seconda del dispositivo di destinazione o è lo stesso?
- Le app richiedono una gestione dei dispositivi mobili (MDM) per il corretto funzionamento?
- Si userà Windows Store o un altro app store per distribuire le app?
- Le app installano un certificato digitale durante la distribuzione?
    - In tal caso, quale autorità di certificazione verrà usata (privata o pubblica)?
- Gli utenti devono essere fisicamente connessi alla rete aziendale per eseguire l'installazione o è possibile installare l'app tramite Internet?

### Archiviazione

- Quanto spazio è necessario in un dispositivo di destinazione per installare ogni app?
- Le app eseguono la crittografia dei dati presenti nell'archivio di un dispositivo?
- È possibile installare le app nell'archivio esterno di un dispositivo di destinazione?
- Si prevede un aumento dell'attività di archiviazione nel server app back-end con l'adozione di BYOD?
    - In tal caso, si intende estendere la capacità di archiviazione del server app?
- I dati utilizzati dalle app risiedono nell'archiviazione in locale, nel cloud o in entrambe le posizioni?
- I dati utilizzati dalle app sono crittografati nell'archivio del data center o nel cloud?

### Rete

- Quali sono i requisiti di rete per le app che si intende distribuire per gli utenti BYOD?
- Le app eseguono la crittografia dei dati prima della trasmissione attraverso la rete dai dispositivi degli utenti al server app nel back-end?
    - In tal caso, quale metodo di crittografia usano le app?
- Si prevede un aumento dell'attività di rete con l'adozione di BYOD?
- Le app richiedono una connettività di rete completa per il funzionamento?
- Le app funzionano in una rete a bassa latenza?
- Le app possono essere disinstallate in remoto attraverso la rete o devono essere disinstallate tramite le console dei dispositivi?

### Sicurezza

- Le app sono state sviluppate con qualsiasi metodo di sviluppo della sicurezza?
- Le app forniscono le funzionalità di autenticazione?
    - In tal caso, quale metodo di autenticazione usano le app?
- Il metodo di autenticazione sfrutta i servizi cloud?
- Le app forniscono le funzionalità di autorizzazione?
    - In tal caso, quali livelli di autorizzazione forniscono le app?
- Le app sfruttano l'infrastruttura esistente per gestire l'autorizzazione?
- Le app forniscono le funzionalità di registrazione?
    - In tal caso, quali dati registrano? È possibile controllare il livello di registrazione?
- Le app forniscono la convalida dell'input?
- I criteri dell'azienda hanno standard specifici per la gestione e la convalida dell'input?
    - In tal caso, le app saranno conformi a tali requisiti?
- C'è un sottosistema comune di purificazione o di convalida dell'input che elabora i dati dall'esterno del sistema?
- Le app utilizzano una libreria esterna come la libreria JavaScript?
    - In tal caso, è stata eseguita una valutazione dei rischi di sicurezza per le chiamate esterne?
- Le app sono state convalidate in base al modello [STRIDE](https://msdn.microsoft.com/library/ee823878.aspx) (Spoofing, Tampering, Repudiation, Information disclosure, Denial of service, Elevation of privilege) contro spoofing, manomissione, ripudio, diffusione di informazioni, Denial of Service ed elevazione dei privilegi?
- Le app gestiranno dati contenenti informazioni personali?
- È stata eseguita un'analisi della privacy per queste app?
- Le app useranno riquadri animati?
    - In tal caso, questi riquadri animati causeranno inavvertitamente la diffusione di informazioni?



<!--HONumber=Apr16_HO3-->


