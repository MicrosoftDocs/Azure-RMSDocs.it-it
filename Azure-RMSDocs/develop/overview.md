---
title: Panoramica - RMS SDK 4.2 | Azure RMS
description: AD RMS e AZURE RMS sono tecnologie di protezione che consenteno di proteggere le informazioni digitali da usi non autorizzati.
keywords: ''
author: msmbaldwin
ms.author: mbaldwin
ms.date: 03/17/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.openlocfilehash: 8b095b9be9cf22facdd40d97aee89cfb55d46306
ms.sourcegitcommit: 5390bd1e0e4851b81a59094e80202f0761b7810f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/21/2020
ms.locfileid: "80068639"
---
# <a name="overview"></a>Panoramica

[!INCLUDE [deprecation notice](../includes/deprecation-warning.md)]

Microsoft Rights Management SDK 4.2 è una tecnologia di protezione delle informazioni disponibile per diverse piattaforme.  È un kit per sviluppatori (SDK, Software Developer Kit) o framework progettato per i computer client e i dispositivi. La sua funzione è quella di proteggere l'accesso e l'utilizzo di informazioni che passano attraverso le applicazioni abilitate all'uso di diritti. Gli SDK per queste piattaforme offrono una API semplice per gli sviluppatori di applicazioni per proteggere o utilizzare il contenuto digitale, recuperare modelli, acquisire criteri da un server e altre attività di gestione dei diritti correlate.

Per ulteriori informazioni sulle piattaforme attualmente supportate, vedere il portale di documentazione per sviluppatori alla sezione [Microsoft Rights Management SDK](active-directory-rights-management-services-multi-platform-thin-client-sdk-portal.md).

Di seguito sono riportati alcuni possibili scenari:

-   Uno studio legale intende impedire la stampa o l’inoltro di messaggi di posta elettronica riservati da un dispositivo mobile.
-   Gli sviluppatori di software di progettazione assistita da computer e di produzione desiderano limitare l'accesso ai disegni a un piccolo gruppo di utenti all'interno della divisione di ricerca senza richiedere l'utilizzo di password.
-   I proprietari di una app mobile di progettazione grafica intendono usare una singola licenza che consenta la visualizzazione gratuita di copie a bassa risoluzione delle proprie immagini, ma che richieda il pagamento per l'accesso alle versioni ad alta risoluzione.
-   I proprietari di una raccolta documenti online desiderano abilitare i diritti a visualizzare, stampare o modificare i documenti in base all'identità dell'utente quando gli stessi vengono scaricati su un dispositivo mobile.
-   Un'azienda intende pubblicare informazioni riservate sui dipendenti in un sito Web interno che limiti la visualizzazione e la modifica dei privilegi a determinati utenti.

MS RMS SDK 4.2 può essere scaricato, previa lettura e accettazione del relativo contratto di licenza, e distribuito liberamente con software di terze parti per consentire l'accesso client a contenuti protetti da diritti mediante l'uso e la distribuzione di server AD RMS nell'ambiente o di servizi Azure RMS. Per altre informazioni, vedere [Introduzione](get-started.md).

## <a name="sdk-highlights"></a>Caratteristiche di SDK


MS RMS SDK 4.2 offre nuove interessanti funzionalità, tra cui:

-   **API riprogettata**: l'API di MS RMS SDK 4.2 è stata riprogettata per la massima semplicità. Gli sviluppatori possono ora usare un'API di crittografia e decrittografia semplice e trasparente che consente comportamenti RMS coerenti con uno sforzo minimo.
-   **Supporto ibrido per AD RMS e Azure RMS**: una singola app abilitata per RMS può utilizzare e proteggere il contenuto dal server AD RMS (con estensione per dispositivi mobili di AD RMS) e dal servizio Azure RMS. MS RMS SDK 4.2 rileva in modo trasparente l'endpoint pertinente che gli amministratori IT possono configurare.
-   **Possibilità di usare la propria libreria di autenticazione**: lo sviluppatore di app può scegliere la libreria di autenticazione da usare con MS RMS SDK 4.2. Che si tratti di [Azure Active Directory Authentication Library](https://msdn.microsoft.com/library/jj573266.aspx) o della libreria personalizzata dell'organizzazione, MS RMS SDK 4.2 separa lo stack di autenticazione consentendo di scegliere la libreria più adatta alle proprie esigenze.
-   **Possibilità di visualizzare un'interfaccia utente personalizzata**: MS RMS SDK 4.2 consente ora di implementare un'interfaccia utente personalizzata. Dalla protezione del contenuto e scelta dei modelli alla visualizzazione e modifica delle autorizzazioni durante l'uso di contenuto protetto, MS RMS SDK 4.2 non applica alcuna interfaccia utente predefinita alle app. Se si desidera, tuttavia, è possibile utilizzare le raccolte di UI di Microsoft RMS per tutte le piattaforme tramite il nostro [account GitHub](https://github.com/AzureAD/).
-   **Accesso offline al contenuto protetto**: MS RMS SDK 4.2 consente agli utenti delle app di accedere al contenuto protetto anche in assenza di connettività Internet. MS RMS SDK 4.2 memorizza nella cache i criteri di consumo del contenuto protetto in modo che gli utenti possano accedere in modalità offline ai dati protetti da RMS.

Usare la guida [Introduzione](get-started.md) per iniziare il progetto di app per dispositivi per le informazioni protette.

## <a name="related-topics"></a>Argomenti correlati

* [Microsoft Rights Management SDK](active-directory-rights-management-services-multi-platform-thin-client-sdk-portal.md)
* [Introduzione](get-started.md)
* [Azure AD Authentication Library](https://msdn.microsoft.com/library/jj573266.aspx)
* [Account GitHub](https://github.com/AzureAD/)
