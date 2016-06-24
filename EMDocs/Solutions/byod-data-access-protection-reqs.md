---
# required metadata

title: Requisiti di protezione e accesso ai dati
description:
keywords:
author: YuriDio
manager: swadhwa
ms.date: 04/28/2016
ms.topic: article
ms.prod:
ms.service:
ms.technology:
ms.assetid: 29eddc34-5ca5-4169-89b6-8137b03ab7f0

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: 
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Requisiti di protezione e accesso ai dati

Uno degli elementi più importanti quando si consente agli utenti di accedere alle risorse aziendali dai propri dispositivi è proteggere i dati dell'azienda e preservarne le informazioni. L'azienda potrebbe avere una serie di requisiti di conformità da implementare per garantire la protezione dei dati indipendentemente da dove risiedono. La figura seguente illustra le interazioni tra utenti e dispositivi per l'accesso ai dati e i componenti da prendere in considerazione per questo sottodominio.

![Requisiti di protezione e accesso ai dati](./media/BYOD_Figure3.png)

La tabella seguente contiene le domande sulla protezione e l'accesso ai dati a cui è necessario rispondere per formulare i requisiti per la progettazione della soluzione.

## Domande da chiedere

Le domande sui requisiti di protezione e accesso ai dati sono suddivise in tre aree:

- Archiviazione
- Rete
- Directory
- Autorizzazione
- Criteri e conformità

### Archiviazione

- Mentre i dati sono inattivi nel data center, la crittografia è abilitata?
- L'azienda fornirà l'accesso offline ai dati che risiedono nell'archivio del data center (in altri termini, i dati verranno sincronizzati nei dispositivi degli utenti)?
    - In tal caso, l'azienda vuole mantenere lo stesso formato dei dati (crittografato o normale) nei dispositivi degli utenti?
- Si ha una quota di archiviazione attualmente implementata nel sistema per ogni utente?
    - In tal caso, si intende aumentare questa quota per gli utenti che sono autorizzati a usare i propri dispositivi?
- I criteri aziendali consentono agli utenti di usare unità di archiviazione esterne nei computer aziendali?
    - In caso contrario, si intende estendere questi criteri agli utenti che accedono ai dati dai propri dispositivi?
- I criteri aziendali consentono agli utenti di usare l'archiviazione basata su cloud dai computer aziendali?
    - In caso contrario, si intende estendere questi criteri agli utenti che accedono ai dati dai propri dispositivi?

### Rete

- Si ha un tipo di crittografia di rete in locale?
    - In tal caso, è limitata alle comunicazioni tra server o viene crittografata l'intera rete?
- Si intende avere requisiti diversi per l'accesso ai dati quando gli utenti sono fisicamente all'esterno della rete aziendale e quando invece sono fisicamente all'interno della rete aziendale?
    - In tal caso, quali sono i requisiti?
- Si prevede un aumento dell'attività di rete consentendo agli utenti di usare i propri dispositivi nella rete aziendale?
    - In tal caso, la capacità di rete esistente è in grado di gestire il nuovo traffico?
- L'azienda usa i meccanismi di controllo di rete?
    - In tal caso, si intende estendere questa funzionalità agli utenti che porteranno i propri dispositivi per connettersi alla rete aziendale?

### Directory

- L'azienda usa una sola directory utente o ha più provider?
- La directory aziendale risiede in locale, nel cloud o in entrambe le posizioni (soluzione ibrida)?
- Quando gli utenti accederanno alle app dai propri dispositivi, in quale directory verranno autenticati?
- L'azienda intende federare l'autenticazione tra i servizi in locale e nel cloud?

### Autenticazione

- Quale tipo di autenticazione viene usato attualmente nell'ambiente?
- Si intende mantenere questo metodo di autenticazione o si vuole ottimizzarlo prima di consentire agli utenti di usare i propri dispositivi per accedere alle risorse aziendali?
- È prevista l'autenticazione a più fattori nell'ambiente esistente?
- Si intente autenticare i dispositivi degli utenti o solo gli utenti?
- Si intende abilitare Single Sign-On per le app che sono accessibili dai dispositivi degli utenti?
- Si intende sfruttare le risorse cloud per fornire un livello di autenticazione aggiuntivo per gli utenti remoti?

### Autorizzazione

- Nell'ambiente esistente dopo l'autenticazione degli utenti sono previsti altri controlli per verificare se gli utenti sono autorizzati ad accedere alle informazioni che richiedono?
- Si intende fornire l'accesso condizionale in base a un set di regole predefinite per gli utenti remoti?
- È prevista nell'azienda l'applicazione di autorizzazioni per i dati che risiedono in locale o nel cloud?
- L'azienda usa il [principio della necessità di sapere (need to know)](http://en.wikipedia.org/wiki/Need_to_know) per autorizzare l'accesso ai dati?

### Criteri e conformità

- L'azienda prevede dei criteri per definire il modo in cui viene classificato l'accesso ai dati?
- L'azienda deve essere conforme a delle norme per la privacy e la gestione dei dati?
    - In tal caso, in che modo queste norme regolano i criteri esistenti di accesso ai dati per le risorse locali?
- L'azienda prevede criteri per la [gestione di dispositivi mobili (MDM, Mobile Device Management)](mdm-design-considerations-guide.md) e la [gestione di applicazioni mobili (MAM, Mobile Application Management) ](https://blogs.technet.microsoft.com/cbernier/2016/01/05/microsoft-intune-mobile-application-management-mam-standalone/)?
- L'azienda prevede dei criteri per la confisca dei dispositivi in caso di controversia legale o indagine investigativa?


<!--HONumber=Apr16_HO3-->


