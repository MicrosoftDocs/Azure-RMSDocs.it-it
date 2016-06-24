---
# required metadata

title: Identificare i requisiti di connettività SaaS
description:
keywords:
author: robmazz
manager: swadhwa
ms.date: 04/28/2016
ms.topic: article
ms.prod:
ms.service:
ms.technology:
ms.assetid: 6afbce4c-7500-4387-a19c-dff52c152097

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: 
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Identificare i requisiti di connettività SaaS

>[!NOTE]
>Questo argomento fa parte di una guida più ampia dedicata alle considerazioni di progettazione. Per leggere la guida dall'inizio, vedere l'[argomento principale](mdm-design-considerations-guide.md). Per scaricare una copia della versione integrale della guida, visitare la raccolta [TechNet](https://gallery.technet.microsoft.com/Mobile-Device-Management-7d401582).

La modalità di connessione dell'infrastruttura locale influirà sul modo in cui le identità di utenti e dispositivi vengono gestite con tutte le soluzioni MDM: Intune, MDM per Office 365 e distribuzioni ibride di Intune e Configuration Manager. Sia Intune che MDM per Office 365 sfruttano l'architettura dei servizi directory offerta dai servizi di Azure Active Directory. L'integrazione con Azure offre una notevole flessibilità durante la progettazione del supporto per la gestione delle identità nella soluzione di gestione dei dispositivi mobili.

La connessione dei servizi directory locali con Azure è il requisito chiave per l'abilitazione di Single Sign-On e per la gestione unificata degli account della directory, come illustrato nella figura riportata di seguito. Il servizio Single Sign-On facilita la connessione degli utenti con le risorse aziendali in locale e nel cloud. La gestione degli account da un'unica posizione semplifica il compito degli amministratori. Per l'accesso mobile, la sincronizzazione degli attributi e delle credenziali degli account della directory tra Azure e i servizi directory locali consente agli utenti di eseguire l'autenticazione nei dispositivi mobili per l'accesso alle risorse gestite da MDM per Office 365 o Intune.

![Panoramica della gestione integrata delle identità](./media/MDM_Figure_15.png)

**Panoramica della gestione integrata delle identità**

A seconda delle risposte fornite alle domande nell'Attività 2, dovrebbe essere possibile determinare la modalità di connessione della soluzione SaaS con la piattaforma locale di gestione dei client per la soluzione di gestione dei dispositivi mobili. Gli elenchi riportati di seguito aiutano a comprendere i vantaggi e gli svantaggi della connessione dell'infrastruttura locale con una soluzione SaaS.

## Intune (autonomo)

**Vantaggi**

- Perfettamente integrata con Azure Active Directory per la gestione dell'autenticazione e delle identità di utenti e dispositivi
- Supporta esperienze Single Sign-On e di gestione automatica delle credenziali utente che consentono l'utilizzo delle credenziali degli account locali esistenti
- Supporta l'accesso Single Sign-On a migliaia di applicazioni SaaS preintegrate
- Supporta la sicurezza di accesso alle applicazioni tramite l'applicazione dell'autenticazione a più fattori basata su regole per applicazioni locali e cloud

**Svantaggi**

- Le caratteristiche e funzionalità avanzate di connettività ai servizi directory richiedono l'associazione con Azure Active Directory Premium.

## Gestione dei dispositivi mobili per Office 365

**Vantaggi**

- Integrazione con i tenant di Office 365, che usano il backbone di Azure Active Directory per la gestione dell'autenticazione e delle identità di utenti e dispositivi
- I servizi directory locali possono essere connessi come parte dei servizi di connessione con Office 365
- Supporta esperienze Single Sign-On e di gestione automatica degli utenti che consentono l'utilizzo delle credenziali degli account locali esistenti
- Supporta l'autorizzazione a più fattori per le registrazioni dei dispositivi con il servizio di autenticazione a più fattori di Azure

**Svantaggi**

- Non supporta l'integrazione della gestione di applicazioni mobili con altre applicazioni o soluzioni SaaS

## Ibrida (Intune con Configuration Manager)

**Vantaggi**

- Tutti i vantaggi di Intune autonomo, oltre alle funzionalità seguenti:
 - Integrazione diretta con i servizi directory locali attraverso l'infrastruttura di Configuration Manager

**Svantaggi**

- Le organizzazioni che per il momento non hanno configurato un'infrastruttura di Configuration Manager dovranno pianificarla, installarla e configurarla prima dell'integrazione con Intune
- Richiede requisiti aggiuntivi per la distribuzione locale e modifiche della configurazione per le organizzazioni con Configuration Manager.

<!--HONumber=Apr16_HO2-->


