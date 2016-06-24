---
# required metadata

title: Raccogliere i requisiti di monitoraggio
description:
keywords:
author: robmazz
manager: swadhwa
ms.date: 04/28/2016
ms.topic: article
ms.prod:
ms.service:
ms.technology:
ms.assetid: ac136523-8089-409b-b74d-2d4c0ce399d4

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: 
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Raccogliere i requisiti di monitoraggio

>[!NOTE]
>Questo argomento fa parte di una guida più ampia dedicata alle considerazioni di progettazione. Per leggere la guida dall'inizio, vedere l'[argomento principale](mdm-design-considerations-guide.md). Per scaricare una copia della versione integrale della guida, visitare la raccolta [TechNet](https://gallery.technet.microsoft.com/Mobile-Device-Management-7d401582).

Il monitoraggio e l'acquisizione di informazioni sullo stato e sugli eventi dei dispositivi mobili è fondamentale per garantire che gli utenti e i dispositivi siano conformi ai criteri aziendali e alla strategia di sicurezza. Questo è particolarmente importante per le organizzazioni che devono garantire la conformità ai requisiti normativi governativi e alle linee guida di conformità del settore.

La creazione di report aiuta anche a raccogliere informazioni utili su software, hardware e licenze software dell'organizzazione per facilitare la gestione dell'inventario. 

È necessario essere consapevoli dell'importanza della privacy degli utenti quando si stabiliscono le linee guida per il monitoraggio e la creazione di report, specialmente quando gli utenti possono registrare i propri dispositivi personali nella soluzione di gestione dei dispositivi mobili dell'organizzazione. L'organizzazione non dovrebbe essere in grado di acquisire, monitorare, segnalare o condividere eventuali attività o informazioni personali.

In generale, le soluzioni di gestione dei dispositivi mobili dividono il monitoraggio in due aree generali:

- **Registrazione:** acquisizione e archiviazione delle informazioni e dello stato dei dispositivi mobili e delle relative applicazioni.
- **Creazione di report:** visualizzazione di report o notifiche, inclusi report standard e personalizzabili, che possono essere creati su richiesta, e report automatici di riepilogo e di stato del dashboard.

## Domande sulla pianificazione del monitoraggio

Rispondere alle domande seguenti relative alla pianificazione del monitoraggio dei dispositivi:

- Quali tipi di report regolari sono necessari per i dispositivi mobili?
 - Inventario dei dispositivi?
 - Uso dei dispositivi?
 - Accesso dei dispositivi?
 - Applicazioni dei dispositivi?
- I report devono essere condivisi?
 - Tra i ruoli IT?
 - All'esterno dell'organizzazione IT?
 - È necessario accedervi in modalità remota (all'esterno della rete aziendale)?
- Quali tipi di problemi dei dispositivi è necessario identificare?
- Per quali tipi di eventi acquisiti durante il monitoraggio è necessario intervenire? Con quale tempistica?
- Sono necessari report personalizzati, su richiesta?
- Quando viene annullata la registrazione di un dispositivo, è necessario acquisire eventi specifici relativi all'inventario e alla creazione di report?
- Dopo che è stata annullata la registrazione di un dispositivo, è necessario archiviare/conservare gli eventi legacy relativi all'inventario e alla creazione di report?
 
>[!TIP]
>Assicurarsi di prendere appunti per ogni risposta e di comprendere la logica alla base della risposta. Le attività successive esamineranno le opzioni disponibili e i vantaggi e svantaggi di ogni opzione.  Rispondere a queste domande consentirà di selezionare l'opzione più adatta alle esigenze aziendali.


<!--HONumber=Apr16_HO2-->


