---
# required metadata

title: Specificare i requisiti di accesso
description:
keywords:
author: YuriDio
manager: swadhwa
ms.date: 04/28/2016
ms.topic: article
ms.prod:
ms.service:
ms.technology:
ms.assetid: 1cdc3cdf-cb71-46d5-99fd-05ec96771b81

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: 
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Specificare i requisiti di accesso

>[!NOTE]
>Questo argomento fa parte di una guida più ampia dedicata alle considerazioni di progettazione. Per leggere la guida dall'inizio, vedere l'[argomento principale](mdm-design-considerations-guide.md). Per scaricare una copia della versione integrale della guida, visitare la raccolta [TechNet](https://gallery.technet.microsoft.com/Mobile-Device-Management-7d401582).

Un dispositivo mobile che non è in grado di usare app o di accedere ai dati aziendali necessari per lavorare non è utile per i dipendenti. È pertanto fondamentale comprendere in che modo i dati verranno trasmessi dal percorso di origine (locale o cloud) al dispositivo mobile. 

I dati verranno trasmessi da e verso i dispositivi mobili e devono essere fatte considerazioni specifiche per ogni percorso. Molte aziende che dispongono di criteri di sicurezza non considerano il fatto che l'uso dei dispositivi mobili può causare un aumento della probabilità di una perdita di dati aziendali. È quindi opportuno rivedere gli attuali criteri aziendali per garantire che i requisiti sviluppati per l'autenticazione, l'autorizzazione e il controllo di accesso siano allineati con quelli aziendali.
 
Rispondere alle domande seguenti per determinare i requisiti di accesso per i dispositivi mobili:

- Autenticazione e autorizzazione: nell'ambito della strategia per consentire agli utenti l'accesso ai dati aziendali dai dispositivi mobili, è necessario identificare gli utenti idonei per l'accesso. Alcune aziende decidono di consentire l'accesso ai dati inizialmente solo a una parte degli utenti e successivamente ai dipendenti che lo richiedono, in base alle esigenze aziendali. Per limitare l'accesso, è necessario che la soluzione esegua l'autenticazione (per confermare che l'identità dell'utente corrisponda a quella dichiarata) e l'autorizzazione (per valutare se all'utente debba essere consentito l'accesso ai dati per i quali ha fatto richiesta) in base ai criteri aziendali. 

Quando si progetta la soluzione MDM, considerare quanto segue:

- L'organizzazione dispone di un servizio della directory corrente per l'autenticazione e l'autorizzazione?
    - In caso affermativo, la soluzione MDM esegue l'integrazione con il servizio di directory per autenticare e autorizzare l'accesso alle risorse?
    - L'autenticazione per l'organizzazione deve essere centralizzata o può essere ibrida?
    - L'organizzazione intende eseguire l'autenticazione a più fattori per gli utenti mobili?
    - L'organizzazione usa un'infrastruttura a chiave pubblica (PKI) locale per emettere certificati?
        - In caso affermativo, la soluzione MDM dispone della funzionalità per eseguire l'autenticazione tramite certificati digitali?
            - In caso affermativo, la soluzione MDM dispone della funzionalità per eseguire l'integrazione con un'infrastruttura a chiave pubblica locale esistente?
- È necessario che l'organizzazione usi i servizi della directory corrente per autenticare gli utenti che accedono alle app di terze parti?
    - In caso affermativo, la soluzione MDM consente agli utenti di usare Single Sign-On (SSO) per autenticare le app di terze parti?


**Controllo di accesso**: dopo aver autenticato e autorizzato un utente, è necessario convalidare le richieste di accesso a una risorsa con il livello di accesso per l'utente. La risorsa richiesta può essere rappresentata da un'app o da dati. Quando si progetta la soluzione, considerare quanto segue:

- È necessario che la società disponga di un diverso livello di controllo per la gestione dei dispositivi mobili e della soluzione MDM?
    - In caso affermativo, la soluzione MDM supporta il controllo di accesso basato sui ruoli (RBAC)?
- È necessario che la società disponga di diversi livelli di accesso in base alla posizione dell'utente?
    - In caso affermativo, la soluzione MDM consente di creare restrizioni del controllo di accesso in base alla posizione dell'utente?
- È necessario che la società controlli l'accesso alle app?
    - In caso affermativo, la soluzione MDM consente di controllare l'accesso alle app installate nel dispositivo mobile?
- È necessario che la società controlli l'accesso in base a un set di condizioni?
    - In caso affermativo, la soluzione MDM consente di disporre del controllo di accesso condizionale?
    - In caso affermativo, la soluzione MDM consente di abilitare o disabilitare la funzionalità dell'applicazione in base all'identità dell'utente?
    - In caso affermativo, la soluzione MDM consente di gestire un'attestazione dispositivo?

Leggere l'articolo [Accesso sicuro alle risorse ovunque e con qualsiasi dispositivo](https://technet.microsoft.com/library/dn550982) per comprendere meglio l'uso delle funzionalità integrate di Windows Server 2012 R2 insieme a Configuration Manager per consentire l'accesso alle risorse aziendali. 


<!--HONumber=Apr16_HO2-->


