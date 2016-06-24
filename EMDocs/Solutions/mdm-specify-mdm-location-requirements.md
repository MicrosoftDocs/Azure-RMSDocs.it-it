---
# required metadata

title: Specificare i requisiti di posizione per la gestione dei dispositivi mobili
description:
keywords:
author: YuriDio
manager: swadhwa
ms.date: 04/28/2016
ms.topic: article
ms.prod:
ms.service:
ms.technology:
ms.assetid: c8824726-082e-417a-8522-183a69328ae4

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: 
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Specificare i requisiti di posizione per la gestione dei dispositivi mobili

>[!NOTE]
>Questo argomento fa parte di una guida più ampia dedicata alle considerazioni di progettazione. Per leggere la guida dall'inizio, vedere l'[argomento principale](mdm-design-considerations-guide.md). Per scaricare una copia della versione integrale della guida, visitare la raccolta [TechNet](https://gallery.technet.microsoft.com/Mobile-Device-Management-7d401582).

I requisiti di posizione sono uno dei numerosi fattori da tenere in considerazione quando si progetta la strategia di gestione dei dispositivi mobili. La posizione è importante dalla prospettiva della soluzione di gestione dei dispositivi mobili, nonché dal punto di vista del dispositivo stesso. Rispondere alle domande seguenti:

- Rilevamento degli utenti: per alcuni tipi di controllo dei dispositivi mobili può essere necessario implementare criteri che limitano l'accesso alle risorse aziendali in base alla posizione dell'utente.
    - La società deve implementare meccanismi per attivare il geofencing o la possibilità di applicare criteri in base alla posizione geografica del dispositivo? 
    - La società deve tenere traccia della posizione geografica dell'utente nel momento in cui accede a una risorsa aziendale?
- Modello amministrativo: a seconda della soluzione adottata per la gestione dei dispositivi mobili, l'amministrazione può essere distribuita in più siti (posizioni) o centralizzata in un'unica posizione. Un sito di amministrazione centrale è l'ideale per le distribuzioni su larga scala e offre un punto centrale di amministrazione e la flessibilità necessaria per supportare i dispositivi distribuiti in un'infrastruttura di rete globale. Un sito primario è adatto per le distribuzioni di dimensioni inferiori, ma offre meno opportunità di supportare la crescita futura. Determinare se il controllo della gestione dei dispositivi mobili dovrà essere centralizzato o distribuito.
    - La società necessita di un modello amministrativo centralizzato?
    - La soluzione di gestione dei dispositivi deve essere situata in locale?
        - In caso contrario, è possibile che risieda nel cloud?
        - In caso contrario, può essere ibrida?
    - La società necessita di un modello decentralizzato in cui sedi diverse hanno autonomia nell'amministrazione della gestione dei dispositivi?

>[!TIP] Assicurarsi di annotare ogni risposta e di comprendere la logica alla base della risposta. La sezione successiva esaminerà le opzioni disponibili e i vantaggi e svantaggi di ogni opzione.  Avendo risposto a queste domande, sarà possibile selezionare la soluzione più adatta a soddisfare le esigenze aziendali.



<!--HONumber=Apr16_HO2-->


