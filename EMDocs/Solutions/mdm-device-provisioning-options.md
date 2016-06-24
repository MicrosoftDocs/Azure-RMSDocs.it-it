---
# required metadata

title: Opzioni di provisioning dei dispositivi
description:
keywords:
author: andredm7
manager: swadhwa
ms.date: 05/31/2016
ms.topic: article
ms.prod:
ms.service:
ms.technology:
ms.assetid: 991cd722-089c-4e8c-80b9-b82e405cc891

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: 
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Opzioni di provisioning dei dispositivi

>[!NOTE]
>Questo argomento fa parte di una guida più ampia dedicata alle considerazioni di progettazione. Per leggere la guida dall'inizio, vedere l'[argomento principale](mdm-design-considerations-guide.md). Per scaricare una copia della versione integrale della guida, visitare la raccolta [TechNet](https://gallery.technet.microsoft.com/Mobile-Device-Management-7d401582).

Quando un utente può usare e registrare il proprio dispositivo, aumentano i requisiti sia per l'utente sia per l'IT, con conseguenze in diverse aree. Ad esempio, la figura che segue illustra una panoramica del processo di registrazione per un'organizzazione che usa sia Intune che Configuration Manager. Questo esempio illustra il certificato, l'applicazione Web e le considerazioni di sincronizzazione di cui è necessario tenere conto durante la pianificazione della soluzione:

![Panoramica del processo di registrazione per dispositivi mobili usando una distribuzione ibrida di Intune e ConfigMgr](./media/MDM_Figure_04.png)

**Panoramica del processo di registrazione per dispositivi mobili usando una distribuzione ibrida di Intune e ConfigMgr**

1. Con <token>Windows Server 2012 R2, è stato introdotto un nuovo concetto noto come registrazione del dispositivo.  Gli utenti possono registrare i propri dispositivi per l'accesso Single Sign-On e l'accesso ai dati aziendali tramite l'aggiunta all'area di lavoro.  Durante il processo di registrazione viene installato un certificato sul dispositivo. Dopo aver registrato il dispositivo e averlo reso noto alla soluzione di gestione dei dispositivi, l'utente ottiene l'accesso alle risorse aziendali che in precedenza non erano disponibili al di fuori del PC appartenente al dominio.
2. Gli utenti possono registrare dispositivi e configurarli per la gestione con Intune [usando il portale aziendale](/Intune/deployuse/enroll-devices-in-microsoft-intune) e quindi sfruttare il Portale aziendale di Microsoft Intune per facilitare l'accesso ad applicazioni e dati aziendali ed essere in grado di gestire i propri dispositivi, eseguendo attività come la cancellazione remota in caso di smarrimento, furto o sostituzione.
3. È possibile pubblicare l'accesso alle risorse aziendali con la funzionalità integrata [Proxy applicazione Web](https://technet.microsoft.com/library/dn584107.aspx), disponibile in Windows Server 2012 R2, in base alle informazioni sulla presenza del dispositivo (ossia se è registrato) e all'identità dell'utente. Se si usa Enterprise Mobility Suite, è anche possibile pubblicare applicazioni con il proxy di applicazione di AD Azure. È possibile usare l'autenticazione a più fattori tramite l'[autenticazione attiva di Azure](https://azure.microsoft.com/documentation/articles/multi-factor-authentication-get-started-cloud/).
4. Per offrire agli amministratori una visualizzazione unificata dell'intero ambiente, i dati di Intune vengono sincronizzati con Configuration Manager per consentire la gestione unificata sia in locale che nel cloud.
5. Durante il processo di registrazione viene creato un nuovo oggetto dispositivo in Active Directory.  Tale oggetto dispositivo stabilisce un collegamento tra l'utente e il dispositivo, rendendolo noto alla soluzione di gestione dei dispositivi e consentendo al dispositivo di eseguire l'autenticazione. In sostanza, si tratta di una semplice autenticazione a due fattori.

In base alle risposte date alle domande del passaggio 1, l'utente dovrebbe essere in grado di determinare in che modo vuole che siano gestiti i dispositivi nella soluzione di gestione dei dispositivi mobili. Gli elenchi riportati di seguito indicano i vantaggi e gli svantaggi di ogni opzione di provisioning.

## Intune (autonomo)

**Vantaggi**

- Supporta la registrazione e il provisioning di tutti i principali sistemi operativi per dispositivi mobili (Android, iOS, Windows 10, Windows 8.x e Windows Phone)
- Servizio basato sul cloud, è possibile registrare i dispositivi mobili da qualsiasi posizione con accesso a Internet
- I dispositivi possono essere registrati tramite un portale aziendale centralizzato e personalizzabile
- Opzioni avanzate di provisioning dei dispositivi per i dispositivi mobili

**Svantaggi**

- Interfaccia di gestione aggiuntiva per il provisioning dei dispositivi mobili (solo) se si usa una piattaforma di gestione locale per i dispositivi non mobili
- Criteri di sicurezza e conformità dei dispositivi separati per il servizio basato sul cloud e la piattaforma di gestione locale 

## Gestione dei dispositivi mobili per Office 365

**Vantaggi**

- Perfettamente integrata con i tenant di Office 365, l'opzione offre un'unica console per la gestione dei dispositivi mobili e dei servizi tenant di Office 365, ovvero Exchange Online, SharePoint Online e Skype for Business
- Supporta la registrazione e il provisioning di tutti i principali sistemi operativi per dispositivi mobili (Android, iOS, Windows 10, Windows 8.1 e Windows Phone)
- Opzioni di provisioning di base dei dispositivi per i dispositivi mobili

**Svantaggi**

- Interfaccia di gestione aggiuntiva per il provisioning dei dispositivi mobili (solo) se si usa una piattaforma di gestione locale per i dispositivi non mobili
- Criteri di sicurezza e conformità dei dispositivi separati per il servizio basato sul cloud e la piattaforma di gestione locale
- Opzioni meno avanzate di provisioning dei dispositivi

## Ibrida (Intune con Configuration Manager)

**Vantaggi**

- Integrazione nativa di Intune (servizio di gestione dei dispositivi basato su cloud) con System Center 2012 Configuration Manager e System Center 2012 R2 Configuration Manager (piattaforme di gestione dei dispositivi locali)
- Supporta la registrazione e il provisioning di tutti i principali sistemi operativi per dispositivi mobili (Android, iOS e Windows Phone) e include il provisioning per tutti i principali sistemi operativi per dispositivi non mobili
- Supporta opzioni avanzate di provisioning dei dispositivi mobili tramite la connettività di Intune

**Svantaggi**

- Le organizzazioni che per il momento non hanno configurato un'infrastruttura di Configuration Manager dovranno pianificarla, installarla e configurarla prima dell'integrazione con Intune
- Richiede requisiti di configurazione aggiuntivi per la connessione di Intune all'infrastruttura di Configuration Manager locale

Per altre informazioni sulle opzioni di registrazione e provisioning dei dispositivi mobili, assicurarsi di esaminare le procedure di [attivazione delle registrazioni dei dispositivi mobili](/Intune/deployuse/enroll-devices-in-microsoft-intune) in Intune e di confrontare requisiti e procedure per [attivare le registrazioni dei dispositivi mobili](https://technet.microsoft.com/library/jj884158.aspx) in Configuration Manager e MDM per Office 365.

<!--HONumber=Jun16_HO1-->


