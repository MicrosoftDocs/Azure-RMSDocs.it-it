---
# required metadata

title: Opzioni di monitoraggio dei dispositivi
description:
keywords:
author: robmazz
manager: swadhwa
ms.date: 04/28/2016
ms.topic: article
ms.prod:
ms.service:
ms.technology:
ms.assetid: 23cfc12a-fa96-4fb3-8de1-af4569e8cb71

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: 
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Opzioni di monitoraggio dei dispositivi

>[!NOTE]
>Questo argomento fa parte di una guida più ampia dedicata alle considerazioni di progettazione. Per leggere la guida dall'inizio, vedere l'[argomento principale](mdm-design-considerations-guide.md). Per scaricare una copia della versione integrale della guida, visitare la raccolta [TechNet](https://gallery.technet.microsoft.com/Mobile-Device-Management-7d401582).

Il monitoraggio e la comprensione dello stato e della configurazione di tutti i dispositivi mobili gestiti dall'organizzazione aiuta a rilevare problemi e mancanza di conformità, nonché a gestire l'inventario dei dispositivi. In assenza di report dettagliati su hardware, software e stato della conformità, è impossibile assicurarsi che i criteri dei dispositivi siano effettivamente applicati e funzionino correttamente. Il monitoraggio proattivo consente di ridurre l'impatto di piccoli problemi prima che diventino più complessi e più costosi da risolvere.

[Intune](/Intune/deployuse/monitoring-and-reports-with-microsoft-intune), [MDM per Office 365](https://technet.microsoft.com/library/faa7d8e5-645d-4d59-839c-c8d4c1869e4a(v=technet.10).aspx) e una [distribuzione ibrida](https://technet.microsoft.com/library/gg699377.aspx) di Intune e Configuration Manager includono tutti il monitoraggio e la creazione di report per agevolare la gestione di dispositivi, utenti e conformità ai criteri e alle procedure dell'organizzazione. Usando report incorporati e report personalizzati, è possibile monitorare la gestione dei dispositivi mobili in aree quali:

- Report di aggiornamento per il software
- Report sull'inventario del software
- Report sull'inventario dell'hardware
- Report sulle licenze
- Report sulla mancata conformità

A seconda della configurazione dell'infrastruttura, è possibile creare una varietà di report per monitorare l'organizzazione. Le funzionalità di monitoraggio e creazione di report basate su Intune rappresentano il fondamento dei report in MDM per Office 365, nonché delle distribuzioni autonome di Intune. Questi report possono anche essere perfettamente integrati con le funzionalità di creazione report di Configuration Manager quando quest'ultimo è connesso a Intune in una distribuzione ibrida. Ogni prodotto, come illustrato di seguito, dispone di funzionalità di creazione di report diverse ma complementari. È importante esplorare le sfumature delle funzionalità di creazione di report di ogni soluzione di gestione dei dispositivi mobili per assicurarsi di scegliere una soluzione che includa i report necessari.

![Monitoraggio e creazione di report integrati per i dispositivi mobili](./media/MDM_Figure_05.png)

**Monitoraggio e creazione di report integrati per i dispositivi mobili**

Le risposte alle domande nell'attività 2 aiutano a determinare le esigenze di monitoraggio e creazione di report per i dispositivi mobili. Gli elenchi che seguono illustrano i vantaggi e gli svantaggi delle funzionalità di monitoraggio e creazione di report per ogni soluzione MDM.

## Intune (autonomo)

**Vantaggi**

- Panoramica/dashboard di monitoraggio
- Avvisi quando vengono rilevati errori nei dispositivi di rete direttamente gestiti
- Un feed RSS del servizio Intune può inviare notifiche relative a problemi del servizio e alla manutenzione programmata
- Tre livelli di avvisi (critico, avviso, informativo) con soglie e notifiche di avviso tramite posta elettronica
- Filtraggio degli avvisi in base al tipo di dispositivo
- Controllo dello stato di qualsiasi dispositivo gestito
- Genera report sui dispositivi che non soddisfano i criteri IT
- Monitoraggio dei dettagli nelle aree seguenti:
 - Sistema
 - Sistema operativo
 - Archiviazione
 - Exchange ActiveSync
 - System Enclosure
 - Rete
 - Servizio

**Svantaggi**

- Solo avvisi tramite posta elettronica, non tramite messaggi di testo o messaggi vocali

## Gestione dei dispositivi mobili per Office 365

**Vantaggi**

- Panoramica/dashboard di monitoraggio
- Tre livelli di avvisi (critico, avviso, informativo) con soglie e notifiche di avviso tramite posta elettronica
- Filtraggio degli avvisi in base al tipo di dispositivo
- Controllo dello stato di qualsiasi dispositivo gestito
- Genera report sui dispositivi che non soddisfano i criteri IT

**Svantaggi**

- Solo report sullo stato di conformità dei dispositivi mobili

## Ibrida (Intune con Configuration Manager)

**Vantaggi**

- Tutte le funzionalità di monitoraggio e creazione di report di Intune autonomo, oltre alle seguenti:
 - Funzionalità di monitoraggio e creazione di report complete, basate su soglia e consolidate per tutti i dispositivi dell'organizzazione, inclusi quelli non mobili e quelli non registrati in Intune.
 - Funzionalità di creazione di report avanzate di SQL Server Reporting Services (SSRS) ed esperienza di creazione completa offerta da Generatore report di Reporting Services

**Svantaggi**

- Richiede requisiti di configurazione aggiuntivi per la connessione di Intune all'infrastruttura di Configuration Manager locale
- Le organizzazioni che per il momento non hanno configurato un'infrastruttura di Configuration Manager dovranno pianificarla, installarla e configurarla prima dell'integrazione con Intune

È possibile esaminare i dettagli sulle opzioni di monitoraggio dei dispositivi mobili prendendo in considerazione gli elementi seguenti:

- Intune: **[Come monitorare i dispositivi mobili](https://technet.microsoft.com/library/jj733634.aspx)** e [gestire i report](/Intune/deployuse/monitoring-and-reports-with-microsoft-intune)
- Configuration Manager: [Monitoraggio dei dispositivi mobili](https://technet.microsoft.com/library/gg682128.aspx) e [gestione dei report](https://technet.microsoft.com/library/gg699377.aspx)
- MDM per Office 365: [Panoramica e attività di gestione dei dispositivi](https://technet.microsoft.com/en-us/library/ms.o365.cc.devicepolicy.aspx)

<!--HONumber=Apr16_HO2-->


