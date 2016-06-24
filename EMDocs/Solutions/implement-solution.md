---
# required metadata

title: Implementazione di una soluzione per proteggere la posta elettronica e gli allegati aziendali
description:
keywords:
author: karthikaraman
manager: swadhwa
ms.date: 04/28/2016
ms.topic: article
ms.prod:
ms.service:
ms.technology:
ms.assetid: edc744d8-97d9-42e0-8906-6f0dedd8d629

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: 
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Implementazione di una soluzione per proteggere la posta elettronica e gli allegati aziendali
Questo articolo aiuta a preparare e implementare una soluzione per proteggere i contenuti e gli allegati dei messaggi di posta elettronica aziendali.

## Aspetti da considerare per la pianificazione dell'implementazione:

-   **Supporto per la piattaforma del dispositivo**: è necessario considerare anche se si vuole consentire l'accesso alla posta elettronica su piattaforme non supportate da Intune. Con la funzionalità Gestione dei dispositivi mobili di Intune sono supportati i sistemi operativi seguenti:

    -   Apple iOS 7.1 e versioni successive (i dispositivi iOS 6.0 e 7.0 registrati in precedenza restano registrati ma possono essere registrati nuovi dispositivi)

    -   Google Android 2.3.4 e versioni successive (incluso Samsung KNOX)

    -   Windows Phone 8.0 e versioni successive

    -   Windows RT e versioni successive

    -   Computer Windows 8.1 e versioni successive

-   **Tipi di app di posta elettronica**: la soluzione EMS supporta attualmente i client che usano il protocollo EAS e le app Outlook (in precedenza Accompli in iOS e Android).

-   **Criteri**: la soluzione EMS e i relativi componenti includono diversi criteri tramite cui vengono gestiti la sicurezza e l'accesso. Stabilire i criteri che devono essere configurati dall'amministratore IT. I tre criteri chiavi da usare per la ricerca e la pianificazione per la protezione dell'accesso alla posta elettronica e ai relativi dati:

    -   **Criteri di conformità del dispositivo**: determinare il significato del termine conformità per la società. Intune include diverse regole che è possibile impostare, ma non tutte le regole potrebbero essere valide per un'azienda. È possibile modificare i criteri in qualsiasi momento, ma è buona norma
        determinare un set di criteri di base per la società. I criteri di conformità sono orientati ai gruppi di utenti e di dispositivi di Intune.

    -   **Criteri di accesso condizionale**: i criteri di accesso condizionale sono orientati ai gruppi di sicurezza di Azure AD. Stabilire gli utenti a cui i criteri devono essere indirizzati e se ci sono utenti che devono essere esenti. L'accesso condizionale è supportato sia dalla soluzione basata su cloud che dall'implementazione ibrida.

    -   **Gestione di applicazioni mobili**: determinare le app che devono essere gestite e i criteri MAM da applicare a tali app.

-   **Considerazioni sulla gestione del dispositivo**: selezionare l'opzione di gestione del dispositivo più adatta ai requisiti dell'organizzazione prima di implementare la soluzione. Sono disponibili due opzioni:

    -   Unificare System Center Configuration Manager con Microsoft Intune per gestire tutti i dispositivi tramite un'unica console. Questo approccio viene definito *Implementazione ibrida*, i cui vantaggi sono:

        -   Console di gestione unica con controlli avanzati di Rights Management per gestire computer locali nonché a dispositivi mobili

        -   Funzionalità avanzate di distribuzione e individuazione degli obiettivi

        -   Massima scalabilità per aziende di grandi dimensioni

    -   Gestire i dispositivi mobili tramite Microsoft Intune separatamente dai dispositivi locali gestiti mediante System Center Configuration Manager. Questo approccio viene definito *Implementazione autonoma di Intune*, i cui vantaggi sono:

        -   Console semplice basata sul Web personalizzata specificamente per la gestione dei dispositivi mobili

        -   Accesso rapido alle funzionalità più recenti

    Sebbene la migrazione sia sempre possibile, è consigliabile scegliere l'approccio da usare prima di implementarlo perché condizionerà molte delle decisioni da prendere durante l'implementazione.

-   **Ambiente di Exchange**:

    -   Distribuzione dei connettori di Exchange e modalità di connessione quando vengono implementati i servizi di bilanciamento del carico di rete.

    -   Exchange Online: multi-tenant o dedicato? Se è dedicato, individuare l'architettura del tenant per stabilire se è possibile usare l'accesso condizionale basato su Azure AD o se è necessario un connettore locale.

-   **Sincronizzazione di Azure AD e Active Directory Federation Services (AD FS) o altro servizio federato di terze parti**:

    -   L'accesso condizionale è progettato per essere usato con i clienti che hanno federato il servizio di gestione delle identità con AD FS. Le regole di accesso client rimarranno valide, tuttavia è consigliabile effettuare un test completo. I requisiti per la sincronizzazione delle directory e AD FS non sono diversi da quelli per Office 365.

    -   Dovrebbero funzionare anche i servizi federativi di terze parti come Ping. È consigliabile effettuare un test prima dell'implementazione.

## Implementazione locale
Se si ha un'implementazione esistente di System Center Configuration Manager, Active Directory e/o Exchange Server è possibile estendere l'infrastruttura esistente grazie all'integrazione con Intune, Azure AD e Office 365. Con questa implementazione ibrida è possibile fornire un'esperienza di gestione coerente tra dispositivi locali e nel cloud. Intune e Configuration Manager offrono un set di funzionalità simile per consentire l'accesso alla posta elettronica con restrizioni in base allo stato del dispositivo.

Per le implementazioni di Exchange Online dedicato dipende dall'implementazione corrente se conviene sfruttare i vantaggi della soluzione basata su cloud descritta in precedenza o dell'implementazione ibrida. Stabilire con il team degli account la soluzione più appropriata in base all'implementazione corrente.

## Operazioni e valutazione di incidenza
Dopo aver implementato la soluzione, è necessario gestire l'ambiente e identificare i potenziali rischi per la sicurezza. Sia Intune che AD Azure includono funzionalità di monitoraggio e creazione di report che consentono di monitorare e rispondere rapidamente in caso di problemi di sicurezza.

Di seguito sono elencate alcune delle funzionalità di creazione di report:

-   Gli avvisi e i report di Intune consentono di monitorare lo stato e l'integrità dei dispositivi gestiti da Intune.

-   Azure AD include funzionalità di controllo e registrazione delle attività. È possibile monitorare elementi quali modifiche delle password e gestione degli utenti. Azure Active Directory Premium include avvisi e report di sicurezza avanzati per le anomalie. Questi avvisi sono basati su report dettagliati basati sulle tecniche di Machine Learning che mostrano l'attività di accesso, criteri di accesso incoerenti e potenziali aree di rischio.

## Come proseguire
Per istruzioni dettagliate su come distribuire una soluzione per proteggere i contenuti e gli allegati dei messaggi di posta elettronica aziendali, vedere uno degli argomenti seguenti, a seconda dell'ambiente specifico:

- [Usare l'accesso condizionale con Microsoft Intune](conditional-access-intune.md)
- [Usare l'accesso condizionale con Microsoft Intune e Configuration Manager](conditional-access-intune-configmgr.md)


<!--HONumber=Apr16_HO4-->


