---
# required metadata

title: Indicazioni sull'architettura per la protezione di documenti e messaggi di posta elettronica aziendali
description:
keywords:
author: karthikaraman
manager: swadhwa
ms.date: 04/28/2016
ms.topic: article
ms.prod:
ms.service:
ms.technology:
ms.assetid: fc9c7d79-d2ca-4cb2-8456-c7a88cbbf6fd

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer:
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Indicazioni sull'architettura per la protezione di documenti e messaggi di posta elettronica aziendali
Questo argomento contiene una panoramica che illustra come garantire la protezione dei dati della società con un'esperienza utente semplice e senza impatto sulla produttività. Descrive inoltre come fornire accesso sicuro alla posta elettronica aziendale e proteggere i dati aziendali nei messaggi di posta elettronica e negli allegati usando la soluzione Microsoft Enterprise Mobility Suite.

Questa sezione descrive l'architettura per la protezione di documenti e messaggi di posta elettronica aziendali. Per indicazioni per la distribuzione di una soluzione, vedere [Informazioni su come distribuire una soluzione per la protezione di documenti e messaggi di posta elettronica aziendali](learn-how-to-deploy-a-solution-for-protecting-company-email-and-documents.md).

> [!TIP]
> È possibile scaricare una copia di questo argomento nella raccolta [TechNet](https://gallery.technet.microsoft.com/Managing-Access-and-Help-b7a05d0d/file/140056/1/Managing%20Access%20and%20Help%20Protect%20Corporate%20Email%20Data%20on%20Mobile%20Devices.pdf).

I dipendenti vogliono poter usare i propri dispositivi per accedere alle risorse aziendali e agli strumenti di produttività. Il reparto IT deve assicurarsi che i dipendenti abbiano questa possibilità proteggendo al contempo i dati sensibili aziendali. BYOD ([Bring your own device](byod-design-considerations-guide.md)) pone un problema specifico in ciò che deve essere una separazione tra dati personali e dati di lavoro nei dispositivi personali, impedendo la condivisione intenzionale o accidentale dei dati aziendali.

**Alcuni studi hanno dimostrato che:**

-   il 37% della forza lavoro del mondo è mobile

-   il 53% dei messaggi di posta elettronica totali è stato aperto in un telefono cellulare o un tablet nel terzo trimestre del 2014

-   il 61% dei lavoratori combina attività personali e lavorative nei propri dispositivi

Tenere presente che:

-   La posta elettronica è spesso l'applicazione più usata in tutti i dispositivi.

-   Il contenuto dei messaggi di posta elettronica e i relativi allegati possono essere copiati, condivisi o spostati in altre posizioni all'esterno dell'ambito del reparto IT, con il rischio di compromettere la sicurezza dell'azienda.

Poiché gli utenti finali vogliono lavorare usando i propri dispositivi personali e la posta elettronica è l'applicazione maggiormente usata, il primo passo per il reparto IT è quello di assicurarsi che gli utenti finali possano accedere alla posta elettronica aziendale con i propri dispositivi garantendo però che i dati sensibili presenti nei messaggi di posta elettronica non vengano compromessi.

## Panoramica
Microsoft offre Enterprise Mobility Suite (EMS), una soluzione completa per la gestione delle identità, dei dispositivi mobili e delle app nonché per la protezione dei dati. EMS fornisce un modello di sicurezza a più livelli che consente al reparto IT di gestire l'accesso alla posta elettronica, ai dati e alle applicazioni aziendali da quasi qualsiasi dispositivo.

EMS è composto dai servizi cloud seguenti:

![Immagine che illustra i servizi cloud inclusi in EMS: Microsoft Azure AD Premium, Microsoft Intune e Microsoft Azure Rights Management](./media/ProtectEmail/Enterprise-Mobility-Suite.png)

Con l'uso di EMS i dati sono protetti sia all'interno che all'esterno della rete aziendale:

-   I dipendenti possono accedere alla posta elettronica aziendale, alle applicazioni lavorative e ai dati aziendali con il dispositivo desiderato senza doversi preoccupare di compromettere le informazioni aziendali riservate.

-   I dati aziendali sono protetti a ogni livello: utente, dispositivo, applicazione e, infine, a livello dei dati stessi.

-   L'amministratore IT può assicurarsi che l'accesso ai dati aziendali venga eseguito solo da utenti attendibili con dispositivi gestiti e compatibili e nel contesto di applicazioni gestite.

Le app gestite da Intune includono le app di Office per dispositivi mobili, fondamentali per questa soluzione. Con le app di Office per dispositivi mobili è possibile contribuire a massimizzare la produttività dei dipendenti, impedendo la fuga di dati. Ad esempio, l'amministratore IT può impostare dei criteri che impediscono la copia dei dati aziendali in uno spazio di archiviazione cloud personale come Dropbox.

Quando i dipendenti vengono trasferiti o cambiano lavoro oppure perdono il proprio dispositivo, EMS consente di cancellare in remoto e in modo selettivo i dati aziendali dal dispositivo. Tale operazione può essere eseguita dall'utente finale o dall'amministratore IT.

## Come EMS consente di proteggere i dati
Il modello di sicurezza a 4 livelli per identità, dispositivi, app e dati garantisce che l'accesso alle risorse aziendali venga eseguito solo dall'utente desiderato, in un dispositivo che soddisfa una serie di criteri di conformità configurati e nei limiti delle app gestite.

![Immagine che illustra il modello di sicurezza a 4 livelli per identità, dispositivi, applicazioni e dati](./media/ProtectEmail/Protecting_your_data.png)

La protezione dei dati inizia con la definizione e la convalida dell'identità dell'utente. *Azure AD/*, uno strumento di gestione aziendale delle identità e degli accessi che offre accesso Single Sign-On, autenticazione a più fattori, password self-service e altro ancora, fornisce la funzionalità per il **livello identità** del modello di sicurezza.

Basandosi sull'identità come punto di riferimento, l'amministratore IT può usare *Microsoft Intune* per assicurarsi che i dispositivi mobili siano registrati, gestiti e conformi ai criteri aziendali. Questo è il **livello dispositivo**.

Il terzo livello è il **livello gestione delle app** con l'ecosistema di app gestite da Intune. Questo ecosistema consente all'amministratore IT di mantenere i dati sensibili all'interno dell'ecosistema di app gestite, permettendo allo stesso tempo agli utenti di essere produttivi usando strumenti necessari e familiari come Office.

*Azure Rights Management (Azure RMS)* completa il modello di sicurezza proteggendo i dati a livello file. I criteri di sicurezza che vengono applicati ai dati si spostano con i dati, consentendo di proteggere i dati in transito e i dati archiviati, indipendentemente dal dispositivo usato per accedervi. Questo è il **livello dati** del modello di sicurezza.

## Come proseguire
- [Guardare](https://www.youtube.com/watch?v=ltcZvm4VOFU) questo video per informazioni su come iscriversi per ottenere un account di prova e iniziare.

- Per capire meglio quali sono i requisiti di progettazione della gestione dei dispositivi mobili, vedere [Mobile Device Management Design Considerations Guide](mdm-design-considerations-guide.md) (Guida alle considerazioni sulla progettazione per la gestione dei dispositivi mobili).

- [Informazioni su come distribuire una soluzione per la protezione di documenti e messaggi di posta elettronica aziendali](learn-how-to-deploy-a-solution-for-protecting-company-email-and-documents.md).

Se, poi, si vuole approfondire la conoscenza di EMS e Azure Active Directory, è possibile ottenere altre informazioni da questi articoli:
- [Architettura EMS](https://azure.microsoft.com/en-us/documentation/infographics/enterprise-mobility/)

- [Informazioni su Azure Active Directory](https://azure.microsoft.com/en-us/documentation/articles/active-directory-whatis/)

- [Come Azure Active Directory supporta Office 365, Microsoft Intune e altri servizi Microsoft?](https://azure.microsoft.com/en-us/documentation/articles/active-directory-administer/#what-is-an-azure-ad-tenant)

- [Come Azure Active Directory consente di gestire le identità](https://azure.microsoft.com/en-us/documentation/articles/active-directory-administer/)

- [Informazioni su Microsoft Azure Rights Management](https://technet.microsoft.com/en-us/library/jj585026.aspx)

- [Supporto di Microsoft Azure Rights Management da parte delle applicazioni](https://technet.microsoft.com/en-us/library/jj585004.aspx)


<!--HONumber=Apr16_HO4-->


