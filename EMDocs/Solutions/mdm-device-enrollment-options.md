---
# required metadata

title: Opzioni di registrazione dei dispositivi
description:
keywords:
author: andredm7
manager: swadhwa
ms.date: 05/31/2016
ms.topic: article
ms.prod:
ms.service:
ms.technology:
ms.assetid: 54082b94-1d21-44d5-9fba-af6e04397def

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: 
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---


# Opzioni di registrazione dei dispositivi

>[!NOTE]
>Questo argomento fa parte di una guida più ampia dedicata alle considerazioni di progettazione. Per leggere la guida dall'inizio, vedere l'[argomento principale](mdm-design-considerations-guide.md). Per scaricare una copia della versione integrale della guida, visitare la raccolta [TechNet](https://gallery.technet.microsoft.com/Mobile-Device-Management-7d401582).

La registrazione dei dispositivi in Microsoft Intune, sia autonomo che connesso a System Center 2012 R2 Configuration Manager, richiede la preparazione del servizio per i dispositivi. Per registrare i dispositivi mobili in MDM per Office 365, è necessario anche attivare la gestione dei dispositivi mobili, configurare le impostazioni di base e includere ogni utente in un [criterio di sicurezza](https://technet.microsoft.com/library/ms.o365.cc.newdevicepolicy.aspx) per consentire la risposta a un messaggio di registrazione al successivo accesso dell'utente a Office 365 sul proprio dispositivo mobile. Gli utenti devono completare le procedure di registrazione e attivazione su ogni dispositivo mobile che useranno per accedere ai messaggi di posta elettronica e ai documenti di Office 365.

È necessario configurare Intune autonomo per definire la soluzione dell'autorità di gestione del dispositivo mobile, che può essere Intune o un'infrastruttura di Configuration Manager locale. Questo significa semplicemente chiedersi quale piattaforma di gestione si vuole usare per gestire i dispositivi registrati in Intune: Intune *o* Configuration Manager? È *molto importante* comprendere l'[impatto della scelta dell'opzione migliore](/Intune/deployuse/enroll-devices-in-microsoft-intune) per l'organizzazione, poiché dopo aver scelto la soluzione non è facile cambiarla. Per modificare questa configurazione in un secondo momento, sarà necessario rivolgersi al supporto tecnico Microsoft per assistenza. Per i tenant di Office 365 è più facile designare e modificare l'autorità di gestione dei dispositivi mobili scegliendo MDM per Office 365 o Intune. È possibile cambiare facilmente l'autorità di gestione a livello di utente modificando l'assegnazione delle licenze per un utente. 

Per la maggior parte delle organizzazioni che usano già Configuration Manager per gestire PC, server e altri dispositivi, connettere la soluzione locale con Intune e gestire i dispositivi con Configuration Manager di solito rappresenta la scelta migliore. Per assegnare l'autorità di gestione dei dispositivi mobili a Configuration Manager è necessario creare una [sottoscrizione a Intune](https://portal.office.com/Signup/Signup.aspx?OfferId=40BE278A-DFD1-470a-9EF7-9F2596EA7FF9&dl=INTUNE_A&ali=1#0) e selezionare l'opzione che consente a Configuration Manager di gestire la sottoscrizione a Intune e i dispositivi registrati in Intune. È anche possibile creare la sottoscrizione a Intune [dall'interno della console di Configuration Manager](https://technet.microsoft.com/library/jj884158.aspx).

Per poter registrare determinati tipi di dispositivi mobili che eseguono diversi tipi di sistemi operativi mobili, è anche necessario preparare il servizio Intune o MDM per Office 365 con requisiti di configurazione specifici. Ad esempio, se si prevede di registrare dispositivi basati su Apple iOS, è necessario **[configurare Intune con un certificato del servizio APN (Apple Push Notification)](https://technet.microsoft.com/library/dn408185.aspx)** prima di eseguire la registrazione dei dispositivi con iOS. Se non si esegue questa configurazione, Intune non è in grado di comunicare con il servizio APN e i dispositivi basati su iOS. I dispositivi mobili che eseguono i sistemi operativi **[Android](https://technet.microsoft.com/library/dn764960.aspx)** o **[Windows Phone](https://technet.microsoft.com/library/dn764959.aspx)** hanno requisiti di registrazione separati.

Le risposte alle domande del passaggio 1 aiutano a decidere in che modo verranno registrati i dispositivi nella soluzione di gestione dei dispositivi mobili adottata. La tabella seguente mette a confronto i vantaggi e gli svantaggi di ogni scenario di registrazione:

| Area  | Dispositivi registrati dagli amministratori | Dispositivi registrati autonomamente dagli utenti |
| ------------- | ------------- | ------------ |
| Costi | I costi di supporto/assistenza tecnica potrebbero diminuire poiché le registrazioni dei dispositivi vengono eseguite da amministratori esperti. | Potenziale incremento dei costi di supporto o delle chiamate all'assistenza tecnica, in quanto gli utenti meno esperti potrebbero aver bisogno di aiuto per eseguire la registrazione |
| Praticità  | Ogni dispositivo viene registrato senza alcuna interazione dell'utente, riducendo gli errori di registrazione. È possibile che gli utenti debbano concordare con gli amministratori quando consegnare e ritirare i dispositivi mobili, attività che richiede pianificazione e monitoraggio nella registrazione dei dispositivi.| Registrazione dei dispositivi più rapida rispetto a un processo di registrazione centralizzato nella maggior parte dei casi. Questo metodo è più pratico e flessibile per i proprietari/gli utenti dei dispositivi |
| Administration | Semplificazione del supporto per i processi di registrazione dei dispositivi più complessi, automatizzati, in blocco o altamente personalizzati. Gli amministratori controllano attentamente la registrazione di tutti i dispositivi, eseguendo uno screening preliminare di ogni dispositivo o utente all'inizio del processo di registrazione. | Le attività amministrative relativamente semplici vengono trasferite agli utenti, consentendo risparmi in termini di tempo, pianificazione, monitoraggio e costi generali di amministrazione. |
| Sicurezza | Se si supporta una strategia BYOD, è più probabile che gli amministratori possano vedere o rivelare informazioni personali riservate dell'utente se non vengono implementati controlli di sicurezza appropriati. | I moderni utenti di dispositivi mobili potrebbero percepire questa centralizzazione come complessa e poco pratica e cercare quindi soluzioni alternative che potrebbero compromettere i processi relativi alla sicurezza e alla conformità della registrazione |

L'organizzazione potrebbe voler consentire entrambi gli scenari di registrazione, adottando un approccio flessibile per impiegare metodi diversi per reparti o situazioni diverse. In tal caso, la soluzione di gestione dei dispositivi mobili deve essere in grado di supportare entrambi gli scenari.

<!--HONumber=Jun16_HO1-->


