---
# required metadata

title: Sviluppare una strategia di gestione dei dispositivi mobili SaaS
description:
keywords:
author: robmazz
manager: swadhwa
ms.date: 04/28/2016
ms.topic: article
ms.prod:
ms.service:
ms.technology:
ms.assetid: b3cefcc5-b045-48f9-91f5-6d282a4428f3

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: 
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Sviluppare una strategia di gestione dei dispositivi mobili SaaS

>[!NOTE]
>Questo argomento fa parte di una guida più ampia dedicata alle considerazioni di progettazione. Per leggere la guida dall'inizio, vedere l'[argomento principale](mdm-design-considerations-guide.md). Per scaricare una copia della versione integrale della guida, visitare la raccolta [TechNet](https://gallery.technet.microsoft.com/Mobile-Device-Management-7d401582).

## Identificare i requisiti della soluzione SaaS

A seconda delle risposte fornite alle domande nell'Attività 1, dovrebbe essere possibile determinare quali elementi devono essere supportati dalla soluzione SaaS nella soluzione di gestione dei dispositivi mobili. La Tabella 20 consente di comprendere i vantaggi e gli svantaggi di ogni soluzione SaaS:

## Intune (autonomo)

**Vantaggi**

- Offerta come architettura cloud pubblica e multi-tenant
- Garantisce la scalabilità necessaria per supportare fino a 50.000 dispositivi mobili
- Non richiede alcun investimento aggiuntivo in un'infrastruttura locale, hardware o software
- Gli aggiornamenti e i miglioramenti delle funzionalità vengono eseguiti su base giornaliera. I miglioramenti delle principali caratteristiche e funzionalità vengono eseguiti su base mensile
- I servizi possono essere assegnati a centri dati in aree geografiche specifiche
- I centri dati di failover possono essere limitati a posizioni geografiche specifiche
- Certificata e conforme alla maggior parte degli standard governativi e del settore. Il contratto di servizio è supportato a livello finanziario, pertanto se il servizio o le funzionalità non sono disponibili, vengono annullati gli addebiti mensili

**Svantaggi**

- Non sono supportate le istanze di cloud privato
- Se è necessario supportare più di 50.000 dispositivi mobili, è necessario connettere Intune a Configuration Manager per gestire i dispositivi aggiuntivi

## Gestione dei dispositivi mobili per Office 365

**Vantaggi**

- Perfettamente integrata con i tenant commerciali di Office 365, l'opzione offre un'unica console per la gestione dei dispositivi mobili e dei servizi tenant di Office 365, ovvero Exchange Online, SharePoint Online e Skype for Business Online.
- Offerta nella piattaforma multi-tenant (pubblica) o privata (dedicata) di Office 365
- Nessun costo aggiuntivo per la gestione delle licenze per utenti o dispositivi, inclusa per impostazione predefinita nei piani commerciali di Office 365 (Business, Enterprise, Education e Government)

**Svantaggi**

- Non supporta la gestione di sistemi operativi non mobili
- Interfaccia di gestione aggiuntiva per il provisioning dei dispositivi mobili (solo) se si usa una piattaforma locale di gestione per i dispositivi non mobili.

## Ibrida (Intune con Configuration Manager)

**Vantaggi**

- Tutti i vantaggi di Intune autonomo, oltre alle funzionalità seguenti: integrazione nativa tra Intune (servizio di gestione dei dispositivi basato su cloud) e Configuration Manager (piattaforma di gestione dei dispositivi locale)
- Supporta opzioni avanzate di provisioning dei dispositivi mobili tramite la connettività di Intune
- Nuove caratteristiche e funzionalità del servizio di Intune estese all'infrastruttura locale di Configuration Manager con estensioni della piattaforma, in modo automatico o personalizzato.

**Svantaggi**

- Richiede requisiti di configurazione aggiuntivi per la connessione di Intune all'infrastruttura di Configuration Manager locale.
- Le organizzazioni che per il momento non hanno configurato un'infrastruttura di Configuration Manager dovranno pianificarla, installarla e configurarla prima dell'integrazione con Intune.

Assicurarsi di leggere l'articolo **[Proteggere i dati con Cancellazione remota, Blocco remoto o Reimpostazione passcode usando Microsoft Intune](https://technet.microsoft.com/library/jj676679.aspx)** per capire quali dati vengono rimossi e l'effetto sui dati che rimangono nel dispositivo dopo la cancellazione selettiva per ogni piattaforma. Se si usa un ambiente ibrido, vedere l'articolo [Proteggere i dati con Cancellazione remota, Blocco remoto o Reimpostazione passcode usando Configuration Manager](https://technet.microsoft.com/library/dn956981.aspx) per capire come si usa Configuration Manager per eseguire questa operazione.

Per altre informazioni sui requisiti e le funzionalità della soluzione SaaS, assicurarsi di esaminare la **[descrizione del servizio Microsoft Intune](https://technet.microsoft.com/library/dn600286.aspx)** per comprendere le differenze del supporto SaaS in [MDM per Office 365](https://technet.microsoft.com/library/faa7d8e5-645d-4d59-839c-c8d4c1869e4a(v=technet.10).aspx) e in un'infrastruttura [ibrida](https://technet.microsoft.com/library/jj884158.aspx) con Intune e Configuration Manager.

<!--HONumber=Apr16_HO2-->


