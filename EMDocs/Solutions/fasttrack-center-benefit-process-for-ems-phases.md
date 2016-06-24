---
# required metadata

title: Processo FastTrack Center Benefit per Enterprise Mobility Suite: fasi
description:
keywords:
author: staciebarker
manager: jeffgilb
ms.date: 04/28/2016
ms.topic: article
ms.prod:
ms.service:
ms.technology:
ms.assetid: e51f030b-8b08-4fea-96c9-d4ded435a264

# optional metadata

ROBOTS: noindex
#audience:
#ms.devlang:
ms.reviewer: 
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Processo FastTrack Center Benefit per Enterprise Mobility Suite: fasi
Quando si usa [FastTrack Center Benefit per Enterprise Mobility Suite (EMS)](fasttrack-center-benefit-for-enterprise-mobility-suite-ems.md) per ottenere Azure Active Directory Premium, Microsoft Intune e/o Azure Rights Management pronti all'uso, sono implicate nel processo varie fasi. Le sezioni seguenti descrivono ogni fase del processo di caricamento.

Per altre informazioni sul processo di caricamento FastTrack, vedere [Processo FastTrack Center Benefit per Enterprise Mobility Suite (EMS)](fasttrack-center-benefit-process-for-enterprise-mobility-suite-ems.md).


Il processo di caricamento è costituito da quattro fasi principali, come illustrato nella figura seguente:


![Le quattro fasi del processo di caricamento di FastTrack](./media/ft-2-onboarding-phases.png)


## Fase di avvio

Dopo aver acquistato il numero appropriato di licenze, attenersi alle istruzioni nel messaggio di conferma dell'acquisto per associare le licenze al tenant esistente o a un tenant nuovo. Microsoft verificherà l'idoneità per FastTrack Center Benefit e contatterà l'utente per offrire assistenza durante il processo di caricamento. È anche possibile richiedere assistenza da parte di [FastTrack Center](http://fasttrack.microsoft.com/) se si è pronti per distribuire questi servizi per l'organizzazione. Per richiedere assistenza, accedere a [FastTrack Center](http://fasttrack.microsoft.com/) (http://fasttrack.microsoft.com), andare nel dashboard, selezionare la scheda Offerte e quindi scegliere l'opzione per richiedere assistenza per Microsoft Intune, Azure Active Directory Premium o Azure Rights Management Premium. Una volta contattato il supporto tecnico di onboarding, verrà impostata la pianificazione di riunioni online.

Durante questa fase verrà illustrato il processo di onboarding, verranno verificati i dati e verrà impostata la riunione iniziale.

![Fase di avvio del caricamento](./media/ft-3-initiate-phase.png)

## Fase di valutazione

Una volta avviato il processo di onboarding, Microsoft assisterà l'utente nel valutare l'ambiente di origine e i requisiti. Verranno eseguiti strumenti per valutare l'ambiente e Microsoft guiderà l'utente nella valutazione di Active Directory locale, browser Internet, sistemi operativi dei dispositivi client, DNS, rete, infrastruttura e sistema di identità, qualora fossero necessarie modifiche per l'onboarding.

Microsoft offrirà anche informazioni aggiuntive su come adottare correttamente i servizi idonei.

In base all'installazione corrente, verrà suggerito un piano di correzione in modo che l'ambiente di origine sia conforme ai requisiti minimi per garantire il caricamento di EMS o dei sui singoli servizi cloud. Verranno inoltre stabilite delle chiamate di controllo appropriate per la fase di correzione.

![Fase di valutazione del caricamento](./media/ft-4-assess-phase.png)

## Fase di correzione
Se necessario, l'utente eseguirà le attività previste nel piano di correzione nell'ambiente di origine, in modo da soddisfare i requisiti per il caricamento e l'adozione di ogni servizio.

![Fase di correzione del caricamento](./media/ft-5-remediate-phase.png)

Prima di iniziare la fase di abilitazione, verranno verificati i risultati delle attività di correzione per essere certi che l'utente sia pronto a procedere.

## Fase di abilitazione
Dopo aver completato tutte le attività di correzione, il progetto passa alla configurazione dell'infrastruttura principale, richiesta per l'uso del servizio e il provisioning di ogni servizio cloud EMS idoneo.

**Fase di abilitazione - Funzionalità di base**

L'onboarding di base prevede il provisioning di servizi e l'integrazione di identità e tenant. Include anche la procedura per definire una base adatta al caricamento di servizi online, ad esempio Azure Active Directory Premium, Microsoft Intune e Azure Rights Management Premium.

![Fase di abilitazione del caricamento: funzionalità di base](./media/ft-6-enable-phase-core.png)

###Fase di abilitazione: Azure Active Directory Premium

L'ambiente di Azure Active Directory Premium può essere configurato usando la sincronizzazione delle directory di Azure Active Directory Connect e Active Directory Federation Services (AD FS), se necessario.

Per gli scenari di Azure Active Directory Premium che includono la sincronizzazione delle identità locali nel cloud, Microsoft supporterà l'utente aggiungendo amministratori IT e utenti alla sottoscrizione, configurando i prerequisiti di gestione, configurando Azure Active Directory Premium, impostando la sincronizzazione delle directory tramite Azure Active Directory Connect e Active Directory Federation Services (AD FS), usando lo strumento Azure Active Directory Connect, configurando utenti di test e convalidando i principali casi d'uso del servizio.

L'installazione di Azure Active Directory Premium include l'abilitazione delle funzionalità seguenti:

-   Reimpostazione della password self-service (SSPR)

-   Azure Multi-Factor Authentication (MFA)

-   Applicazione software come un servizio (SaaS): configurazione di un'applicazione SaaS da [Azure Active Directory Marketplace](https://azure.microsoft.com/marketplace/active-directory/).

-   Gestione di gruppi self-service (SSGM)

-   Report amministrativi

![Fase di abilitazione del caricamento: AADP](./media/ft-7-enable-phase-aadp.png)

###Fase di abilitazione – Microsoft Intune

In base alle esigenze di gestione dei dispositivi mobili e delle applicazioni mobili, verranno fornite informazioni su come usare Microsoft Intune per gestire i dispositivi. La procedura esatta dipende dall'ambiente di origine e può includere:

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

        -   Distribuzione di profili di posta elettronica, Wi-Fi e VPN.

        -   Configurazione di Microsoft Intune Exchange Connector, quando applicabile.

    -   Registrazione dei dispositivi di ogni [piattaforma supportata](https://technet.microsoft.com/library/dn600287.aspx) in Microsoft Intune o in Configuration Manager con il servizio Microsoft Intune.

-   Se Gestione di applicazioni mobili (MAM) rientra nel proprio ambito o se si cerca di integrare la soluzione MDM Microsoft o di terze parti esistente con i criteri MAM, verranno fornite istruzioni su:

    -   Configurazione dei criteri MAM per ogni piattaforma supportata.

    -   Configurazione dei criteri di accesso condizionale per le app gestite.

    -   Indirizzamento ai gruppi di utenti appropriati con i criteri MAM descritti in precedenza.

    -   Uso dei report sull'utilizzo delle applicazioni gestite.

-   Se la gestione del PC rientra nel proprio ambito, verranno fornite istruzioni su:

    -   Installazione del software client di Intune, se necessario.

    -   Uso dei report sul software e l'hardware disponibili in Intune.

Microsoft offrirà anche informazioni aggiuntive su come adottare correttamente i servizi idonei.

![Fase di abilitazione del caricamento: Intune](./media/ft-8-enable-phase-intune.png)

###Fase di abilitazione: Azure Right Management Premium

L'ambiente di Azure Right Management Premium può essere configurato usando la sincronizzazione delle directory di Azure Active Directory Connect e Active Directory Federation Services (AD FS), se necessario.

Per gli scenari di AzRMS che includono la sincronizzazione delle identità locali nel cloud, Microsoft supporterà l'utente aggiungendo amministratori IT e utenti alla sottoscrizione, configurando i prerequisiti di gestione, configurando Azure Right Management Premium, impostando la sincronizzazione delle directory tramite Azure Active Directory Connect e Active Directory Federation Services con Azure Active Directory Connect, configurando gli utenti di test e convalidando i casi d'uso di base per il servizio.

La configurazione di AzRMS include l'abilitazione delle funzionalità seguenti:

-   Abilitazione del servizio AzRMS

-   Configurazione di IRM per Exchange Online e Sharepoint Online

-   Connettore Rights Management con Exchange locale e Sharepoint locale

-   Applicazione di condivisione RMS per dispositivi Windows e non Windows

![Fase di abilitazione del caricamento: Azure RMS](./media/ft-7-enable-phase-aadp.png)

Leggere la parte successiva del processo di caricamento di FastTrack: [responsabilità di Microsoft](fasttrack-center-benefit-process-for-ems-microsoft-responsibilities.md)

### Altre informazioni
Vedere [Enterprise Mobility Suite](https://www.microsoft.com/en-us/server-cloud/enterprise-mobility/overview.aspx).



<!--HONumber=Jun16_HO1-->


