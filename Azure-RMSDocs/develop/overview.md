---
title: Panoramica - RMS SDK 4.2 | Azure RMS
description: AD RMS e AZURE RMS sono tecnologie di protezione che consenteno di proteggere le informazioni digitali da usi non autorizzati.
keywords: 
author: bruceperlerms
manager: mbaldwin
ms.date: 07/11/2016
ms.topic: article
ms.prod: 
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 8A13494E-C1D7-407D-BCD1-A406915EA578
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 5d2339ece646fc51410186d43facdea28ac8fdfe
ms.openlocfilehash: da491f008043b11a04cbfe48acb952e67ad86dda


---

# Panoramica

Microsoft Rights Management SDK 4.2 è una tecnologia di protezione delle informazioni disponibile per piattaforme diverse.  È un kit per sviluppatori (SDK, Software Developer Kit) o framework progettato per i computer client e i dispositivi. La sua funzione è quella di proteggere l'accesso e l'utilizzo di informazioni che passano attraverso le applicazioni abilitate all'uso di diritti. Gli SDK per queste piattaforme offrono una API semplice per gli sviluppatori di applicazioni per proteggere o utilizzare il contenuto digitale, recuperare modelli, acquisire criteri da un server e altre attività di gestione dei diritti correlate.

Per ulteriori informazioni sulle piattaforme attualmente supportate, vedere il portale di documentazione per sviluppatori alla sezione [Microsoft Rights Management SDK](active-directory-rights-management-services-multi-platform-thin-client-sdk-portal.md).

Di seguito sono riportati alcuni possibili scenari:

-   Uno studio legale intende impedire la stampa o l’inoltro di messaggi di posta elettronica riservati da un dispositivo mobile.
-   Gli sviluppatori di software di progettazione assistita da computer e di produzione desiderano limitare l'accesso ai disegni a un piccolo gruppo di utenti all'interno della divisione di ricerca senza richiedere l'utilizzo di password.
-   I proprietari di una app mobile di progettazione grafica intendono usare una singola licenza che consenta la visualizzazione gratuita di copie a bassa risoluzione delle proprie immagini, ma che richieda il pagamento per l'accesso alle versioni ad alta risoluzione.
-   I proprietari di una raccolta documenti online desiderano abilitare i diritti a visualizzare, stampare o modificare i documenti in base all'identità dell'utente quando gli stessi vengono scaricati su un dispositivo mobile.
-   Un'azienda intende pubblicare informazioni riservate sui dipendenti in un sito Web interno che limiti la visualizzazione e la modifica dei privilegi a determinati utenti.

MS RMS SDK 4.2 può essere scaricato, previa lettura e accettazione del relativo contratto di licenza, e distribuito liberamente con un software di terze parti per consentire l'accesso client a contenuti protetti da diritti mediante l'uso e la distribuzione di server AD RMS nell'ambiente o nei servizi Azure RMS. Per ulteriori informazioni, vedere [Introduzione](get-started.md).

## Caratteristiche di SDK


MS RMS SDK 4.2 offre alcune nuove funzionalità interessanti che includono quanto segue:

-   **API riprogettata**: l'API di MS RMS SDK 4.2 è stata riprogettata per raggiungere una semplicità massima, in modo che gli sviluppatori possano sfruttare una API di crittografia e decrittografia semplice e trasparente che offra comportamenti RMS coerenti con uno sforzo minimo
-   **Supporto ibrido per AD RMS e Azure RMS**: una singola app abilitata per RMS può utilizzare e proteggere il contenuto dal server AD RMS (con estensione per dispositivi mobili di AD RMS) e dal servizio Azure RMS. MS RMS SDK 4.2 rileva in modo trasparente l'endpoint pertinente che gli amministratori IT possono configurare.
-   **Possibilità di portare la propria raccolta di autenticazioni**: lo sviluppatore di applicazioni può scegliere la raccolta di autenticazioni da usare con MS RMS SDK 4.2. Che si tratti di [Azure AD Authentication Library](https://msdn.microsoft.com/library/jj573266.aspx) o della raccolta personalizzata dell'organizzazione, MS RMS SDK 4.2 isola lo stack dell'autenticazione per scegliere la libreria più adatta alle proprie esigenze.
-   **Possibilità di visualizzare un'interfaccia utente personalizzata**: MS RMS SDK 4.2 consente ora di implementare un'interfaccia utente personalizzata. Dalla protezione del contenuto e la scelta dei modelli di visualizzazione, fino alla modifica delle autorizzazioni durante l'uso di contenuto protetto, MS RMS SDK 4.2 non impone l'interfaccia utente integrata nelle app. Se si desidera, tuttavia, è possibile utilizzare le raccolte di UI di Microsoft RMS per tutte le piattaforme tramite il nostro [account GitHub](https://github.com/AzureAD/).
-   **Accesso al contenuto protetto non in linea**: MS RMS SDK 4.2 consente agli utenti di app di accedere ai contenuti protetti anche quando non è disponibile una connessione a internet. MS RMS SDK 4.2 memorizza nella cache i criteri di utilizzo del contenuto protetto in modo sicuro in modo che gli utenti possano accedere ai dati RMS protetti anche quando non sono in linea.

Usare la guida [Introduzione](get-started.md) per iniziare il progetto di app per dispositivi per le informazioni protette.

## Argomenti correlati

* [Microsoft Rights Management SDK](active-directory-rights-management-services-multi-platform-thin-client-sdk-portal.md)
* [Introduzione](get-started.md)
* [Azure AD Authentication Library](https://msdn.microsoft.com/en-us/library/jj573266.aspx)
* [Account GitHub](https://github.com/AzureAD/)
 

 






<!--HONumber=Aug16_HO4-->


