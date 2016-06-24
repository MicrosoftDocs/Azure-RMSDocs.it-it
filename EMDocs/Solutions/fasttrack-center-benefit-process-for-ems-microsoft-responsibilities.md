---
# required metadata

title: Processo FastTrack Center Benefit per Enterprise Mobility Suite: responsabilità di Microsoft
description:
keywords:
author: staciebarker
manager: jeffgilb
ms.date: 04/28/2016
ms.topic: article
ms.prod:
ms.service:
ms.technology:
ms.assetid: c8fd871e-f1bc-43ec-a5f3-ad025df9b026

# optional metadata

ROBOTS: noindex
#audience:
#ms.devlang:
ms.reviewer: 
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Processo FastTrack Center Benefit per Enterprise Mobility Suite: responsabilità di Microsoft
Le sezioni seguenti spiegano le responsabilità di Microsoft se si usa [FastTrack Center Benefit per Enterprise Mobility Suite (EMS)](fasttrack-center-benefit-for-enterprise-mobility-suite-ems.md) per ottenere Azure Active Directory Premium, Microsoft Intune e/o Azure Rights Management pronti all'uso.

Per altre informazioni sul processo di caricamento FastTrack, vedere [Processo FastTrack Center Benefit per Enterprise Mobility Suite (EMS)](fasttrack-center-benefit-process-for-enterprise-mobility-suite-ems.md).


## Generale

-   Viene fornita assistenza remota per le attività di configurazione necessarie, come illustrato nelle descrizioni dettagliate delle fasi.

-   All'utente vengono forniti documentazione, strumenti software, console di amministrazione e script disponibili per ridurre o eliminare le attività di configurazione.

## Fase di avvio

-   Contattare l'utente entro 30 giorni dall'acquisto di licenze idonee per un nuovo tenant.

-   Collaborare con l'utente per avviare l'onboarding.

-   Definire i servizi idonei per l'onboarding.

## Fase di valutazione

-   Fornire una panoramica sull'amministrazione.

-   Fornire indicazioni su:

    -   Esigenze relative a DNS, rete e infrastruttura.

    -   Esigenze del client (browser Internet, sistema operativo client e servizi).

    -   Identità dell'utente e provisioning.

    -   Abilitazione dei servizi che sono stati acquistati e definiti come parte dell'onboarding.

-   Stabilire la sequenza temporale per le attività di correzione.

-   Fornire un elenco di controllo della correzione.

## Fase di correzione

-   Effettuare conferenze telefoniche con l'utente in base a una pianificazione concordata per esaminare lo stato di avanzamento delle attività di correzione.

-   Fornire assistenza per l'esecuzione di strumenti allo scopo di identificare e risolvere problemi e per l'interpretazione dei risultati.

## Fase di abilitazione
Fornire indicazioni su:

-   Attivazione del tenant dei servizi online di Microsoft.

-   Configurazione di protocolli TCP/IP e porte del firewall.

-   Configurazione del DNS per i servizi idonei.

-   Convalida di connettività ai servizi online di Microsoft.

-   Per un ambiente a foresta singola:

    -   Installazione di un server di sincronizzazione delle directory tra Servizi di dominio Active Directory (AD DS) e i Microsoft Online Services idonei, se necessario.

    -   Configurazione della sincronizzazione delle password (hash della password) in Microsoft Intune (Azure Active Directory) con lo strumento Azure Active Directory Connect.

        > [!NOTE] Sviluppo e implementazione di estensioni di regole personalizzate sono esterni all'ambito.

-   Per una singola foresta se la destinazione sono le identità federate: installazione e configurazione di Active Directory Federation Services (AD FS) per l'autenticazione di domini locali con Microsoft Intune in un solo sito e configurazione a tolleranza di errore, se necessario.

    > [!NOTE] Per tutte le configurazioni a più foreste, le distribuzioni di AD FS sono esterne all'ambito.

-   Test della funzionalità SSO (Single Sign-On) se distribuita.

### Fase di abilitazione: Azure Active Directory Premium

Fornire indicazioni su:

-   Attivazione del tenant di Microsoft Azure Active Directory Premium.

-   Configurazione delle porte del firewall.

-   Configurazione di DNS per i servizi idonei.

-   Convalida della connettività ai servizi Microsoft Azure Active Directory Premium.

-   Per un ambiente a foresta singola:

    -   Installazione di una sincronizzazione delle directory tra Servizi di dominio Active Directory e Azure Active Directory Connect, se necessario.

    -   Configurazione della sincronizzazione delle password con lo strumento di connessione di Azure Active Directory.

-   Per un ambiente a più foreste:

    -   Installare la sincronizzazione di Azure Active Directory Connect e impostarla per scenari a più foreste. La sincronizzazione hash e il writeback delle password supportano più foreste.  Tuttavia, gli altri scenari di writeback non sono supportati.

    -   Configurare la sincronizzazione tra le foreste locali di Active Directory e la directory di Microsoft Azure Active Directory Premium (Azure Active Directory).

        > [!NOTE] Sviluppo e implementazione per estensioni di regole personalizzate non rientrano nell'ambito.

-   Per una singola foresta se la destinazione sono le identità federate: installazione e configurazione di Active Directory Federation Services (AD FS) per l'autenticazione di domini locali con Microsoft Azure AD Premium in una configurazione con un solo sito a tolleranza di errore, se necessario.

    > [!NOTE] Per tutte le configurazioni di più foreste le distribuzioni di AD FS non rientrano nell'ambito.

-   Test della funzionalità SSO (Single Sign-On), se distribuita.

### Fase di abilitazione: Azure Active Directory Premium con Azure Active Directory Connect e Active Directory Federation Services (AD FS)

Fornire indicazioni sulla configurazione di:

-   Provisioning utenti, incluse le licenze.

-   Sincronizzazione delle directory di Azure Active Directory Connect, con writeback delle password e sincronizzazione degli hash delle password.

-   Active Directory Federation Services (AD FS).

- Reimpostazione della password self-service (SSPR).

- Azure Multi-Factor Authentication (MFA).

- Un'applicazione integrata, che può includere applicazioni SSO (Single Sign-On) per SaaS.

- Report sull'utilizzo e sulla sicurezza per gli amministratori.

- Gestione di gruppi self-service (SSGM).

- Proxy applicazione.

- Notifiche dell'amministratore.

- Schermata di accesso personalizzata, con logo, testo e immagini.
 
### Fase di abilitazione – Microsoft Intune
Fornire indicazioni su:

-   Concessione di licenze agli utenti finali. Se necessario, verrà fornita anche assistenza su come attivare i contratti multilicenza per il tenant del servizio cloud Microsoft.

-   Configurazione delle identità da usare con Microsoft Intune, tramite Active Directory locale o le identità cloud.

-   Aggiunta di utenti alla sottoscrizione di Microsoft Intune, definizione dei ruoli di amministratore IT e creazione di gruppi di utenti e di dispositivi.

-   Configurazione dell'autorità di gestione dei dispositivi mobili in base alle specifiche esigenze di gestione:

    -   Impostare Microsoft Intune come autorità MDM quando è l'unica soluzione MDM o è in combinazione con Gestione di dispositivi mobili per Office 365.

    -   Se è presente un'implementazione esistente di System Center Configuration Manager e si vogliono espandere le funzionalità di gestione con Microsoft Intune, impostare Configuration Manager come autorità MDM.

        > [!NOTE] Per usare Gestione di applicazioni mobili solo nei dispositivi di proprietà degli utenti finali, nei dispositivi condivisi o nei dispositivi di tipo chiosco multimediale, la configurazione di un'autorità MDM non è necessaria.

-   Se Gestione di dispositivi mobili rientra nel proprio ambito, verranno fornite istruzioni su:

    -   Configurazione dei gruppi di test da usare per la convalida dei criteri di gestione MDM.

    -   Configurazione dei servizi e dei criteri di gestione MDM quali:

        -   Distribuzione dell'applicazione per ogni piattaforma supportata tramite collegamenti Web o collegamenti diretti.

        -   Criteri di accesso condizionale.

        -   Distribuzione dei profili di posta elettronica.

        -   Configurazione di Microsoft Intune Exchange Connector, quando applicabile.

    -   Registrazione di un massimo di due dispositivi di test per ogni piattaforma supportata in Microsoft Intune o in Configuration Manager con il servizio Microsoft Intune.

    -   Uso dei report sull'inventario hardware e software.

-   Se Gestione di applicazioni mobili (MAM) rientra nel proprio ambito o se si cerca di integrare la soluzione MDM di terze parti esistente con i criteri MAM, verranno fornite istruzioni su:

    -   Configurazione dei criteri MAM per ogni piattaforma supportata.

    -   Configurazione dei criteri di accesso condizionale per le app gestite.

    -   Indirizzamento ai gruppi di utenti appropriati con i criteri MAM descritti in precedenza.

    -   Uso dei report sull'utilizzo delle applicazioni gestite.

-   Se la gestione del PC rientra nel proprio ambito, verranno fornite istruzioni su:

    -   Installazione del software client di Intune, se necessario.

    -   Uso dei report sul software e l'hardware disponibili in Intune.

### Fase di abilitazione: Azure Right Management Premium

Fornire indicazioni su:

-   Attivazione del tenant di Azure RMS.

-   Aggiunta di altri amministratori di protezione delle informazioni per la gestione dei modelli.

-   Assegnazione di un account utente con privilegi avanzati ad Azure RMS.

-   Concessione di licenze a due utenti pilota per Azure RMS.

-   Configurazione di due gruppi di distribuzione di test per la convalida dei criteri.

-   Configurazione di un modello di Azure RMS personalizzato per la directory.

-   Istruzioni per la configurazione dell'integrazione di SharePoint Online ed Exchange Online con Azure RMS, inclusi:

    -   Configurazione e convalida dell'integrazione di Exchange Online con Azure RMS.

    -   Configurazione di una regola del flusso di posta di test per crittografare messaggi riservati inviati a destinatari esterni all'organizzazione.

    -   Configurazione e convalida della protezione di SharePoint Online per una libreria di test da proteggere con Azure RMS.

-   Configurazione di un server locale con il connettore RMS, quando applicabile:

    -   Configurazione e convalida dell'integrazione di Exchange 2013/2010 locale con Azure RMS.

    -   Configurazione di una regola del flusso di posta di test per crittografare messaggi riservati inviati a destinatari esterni all'organizzazione tramite il connettore.

    -   Configurazione e convalida della protezione di SharePoint 2013/2010 locale per una libreria di test da proteggere con Azure RMS.

-   Configurazione dell'applicazione di condivisione RMS per dispositivi Windows e non Windows.

Leggere la parte successiva del processo di caricamento di FastTrack: [Processo FastTrack Center Benefit per Enterprise Mobility Suite: responsabilità dell'utente](fasttrack-center-benefit-process-for-ems-your-responsibilities.md)

### Altre informazioni
Vedere [Enterprise Mobility Suite](https://www.microsoft.com/en-us/server-cloud/enterprise-mobility/overview.aspx).



<!--HONumber=Jun16_HO1-->


