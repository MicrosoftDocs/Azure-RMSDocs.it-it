---
# required metadata

title: Piano per il miglioramento della protezione dei dispositivi mobili
description:
keywords:
author: YuriDio
manager: swadhwa
ms.date: 04/28/2016
ms.topic: article
ms.prod:
ms.service:
ms.technology:
ms.assetid: a4504456-a241-4380-ab92-3bc14c91347c

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: 
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Piano per il miglioramento della protezione dei dispositivi mobili

>[!NOTE]
>Questo argomento fa parte di una guida più ampia dedicata alle considerazioni di progettazione. Per leggere la guida dall'inizio, vedere l'[argomento principale](mdm-design-considerations-guide.md). Per scaricare una copia della versione integrale della guida, visitare la raccolta [TechNet](https://gallery.technet.microsoft.com/Mobile-Device-Management-7d401582).

L'accesso alle risorse aziendali sui dispositivi mobili consente agli utenti remoti e locali di essere più produttivi, ma aumenta anche i rischi per la sicurezza che è necessario limitare per proteggere i dati aziendali e mantenere la privacy degli utenti. La società potrebbe avere requisiti specifici su come soddisfare queste esigenze. Le regole di conformità possono variare ad esempio a seconda del settore in cui opera la società e ciò potrebbe portare a decisioni di progettazione diverse.
 
È necessario tuttavia esplorare e rispettare alcuni aspetti di sicurezza generali nella gestione dei dispositivi mobili, indipendentemente dal settore. Sono visualizzati nella figura seguente.

![Principali funzionalità di sicurezza per la piattaforma MDM](./media/MDM_Figure_08.png)

## Funzionalità di sicurezza in una soluzione MDM

Questo diagramma illustra le principali funzionalità di sicurezza necessarie in una soluzione MDM. Le principali aree da considerare sono le seguenti:

1. Considerazioni sulla protezione dei dati a livello dei dispositivi mobili:
    - Crittografia dei dati
    - Classificazione dei dati
    - Privacy del client
    - Containerizzazione
    - Imposizione dei criteri
    - Criteri di conformità
    - Protezione avanzata
2. Considerazioni sulla protezione dei dati in transito:
    - Crittografia dei dati
    - Autenticazione
    - Autorizzazione
3. Considerazioni sulla protezione dei dati inattivi nell'organizzazione locale:
    - Crittografia dei dati
    - Autenticazione
    - Autorizzazione
4. Considerazioni sulla protezione dei dati inattivi nel cloud:
    - Crittografia dei dati
    - Autenticazione
    - Autorizzazione

Le attività descritte nelle sezioni che seguono consentono di comprendere come le esigenze specifiche di sicurezza influiranno sulla scelta della soluzione MDM più adatta ai requisiti aziendali.

## Informazioni su questo passaggio

Questa sezione della guida include 12 passaggi. Il tempo totale necessario per leggere le sezioni è circa 36 minuti, ma è possibile passare direttamente a una sezione specifica.

- [Raccogliere informazioni sui requisiti di protezione dei dati](mdm-gather-data-protection-requirements.md)
- [Specificare i requisiti di privacy](mdm-specify-privacy-requirements.md)
- [Specificare i requisiti di accesso](mdm-specify-your-access-requirements.md)
- [Sviluppare i requisiti di risposta agli eventi imprevisti](mdm-develop-incident-response-requirements.md)
- [Pianificare la crittografia dei dati](mdm-data-encryption.md)
- [Pianificare la separazione dei dati](mdm-data-segregation.md)
- [Protezione avanzata dei dispositivi mobili](mdm-hardening-mobile-devices.md)
- [Privacy del client](mdm-client-privacy.md)
- [Classificazione dei dati](mdm-data-classification.md)
- [Autenticazione e autorizzazione](mdm-authentication-authorization.md)
- [Controllo di accesso alle risorse](mdm-access-control-resources.md)




<!--HONumber=Apr16_HO2-->


