---
title: Domande frequenti su Azure Information Protection
description: Alcune domande frequenti su Azure Information Protection e sul relativo servizio di protezione dei dati, Azure Rights Management (Azure RMS).
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 05/15/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 71ce491f-41c1-4d15-9646-455a6eaa157d
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: cbceb3f3e68c558576cc275793dac6feb3b9245b
ms.sourcegitcommit: 04eb4990e2bf0004684221592cb93df35e6acebe
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/30/2017
---
# <a name="frequently-asked-questions-for-azure-information-protection"></a>Domande frequenti su Azure Information Protection

>*Si applica a: Azure Information Protection, Office 365*

Di seguito sono riportate alcune possibili domande su Azure Information Protection o sul servizio Azure Rights Management (Azure RMS) e le relative risposte.

La pagina delle domande frequenti verrà aggiornata periodicamente e le nuove aggiunte saranno pubblicate negli annunci mensili di aggiornamento della documentazione sul [blog di Enterprise Mobility + Security](https://blogs.technet.microsoft.com/enterprisemobility/?product=azure-information-protection,azure-rights-management-services).

## <a name="whats-the-difference-between-azure-information-protection-and-azure-rights-management"></a>Quale è la differenza tra Azure Information Protection e Azure Rights Management?

Azure Information Protection offre funzionalità per la classificazione, l'assegnazione di etichette e la protezione per i documenti e i messaggi di posta elettronica di un'organizzazione. La tecnologia di protezione è basata sul servizio Azure Rights Management, che è ora un componente di Azure Information Protection.

## <a name="what-is-the-role-of-identity-management-for-azure-information-protection"></a>Qual è il ruolo della gestione delle identità per Azure Information Protection?

Un utente deve avere un nome utente e una password validi per accedere al contenuto protetto da Azure Information Protection. Per altre informazioni su come Azure Information Protection consente di proteggere i dati, vedere [Il ruolo di Azure Information Protection nella protezione dei dati](/enterprise-mobility-security/solutions/azure-information-protection-securing-data). 

## <a name="what-subscription-do-i-need-for-azure-information-protection-and-what-features-are-included"></a>Quale sottoscrizione è necessaria per Azure Information Protection e quali funzionalità sono incluse?
Vedere le [informazioni sulla sottoscrizione](https://www.microsoft.com/cloud-platform/azure-information-protection-pricing) e l'[elenco delle funzionalità](https://www.microsoft.com/cloud-platform/azure-information-protection-features) nel sito Azure Information Protection. 

Se si ha un abbonamento a Office 365 che include Rights Management, scaricare il [foglio dati di licenza di Azure Information Protection](http://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf) dalla pagina **Funzionalità**.

## <a name="is-the-azure-information-protection-client-only-for-subscriptions-that-include-classification-and-labeling"></a>Il client Azure Information Protection è disponibile solo per le sottoscrizioni che includono la classificazione e l'assegnazione di etichette?

No. Anche se quasi tutte le presentazioni e demo del client Azure Information Protection illustrano le funzionalità di classificazione e assegnazione di etichette, questo client può essere usato anche con le sottoscrizioni che includono solo il servizio Azure Rights Management per la protezione dei dati.

Quando viene installato il client Azure Information Protection per Windows e non sono configurati criteri per Azure Information Protection, il client funziona automaticamente in [modalità di sola protezione](../rms-client/client-protection-only-mode.md). In questa modalità gli utenti possono applicare facilmente modelli di Rights Management e autorizzazioni personalizzate. Se successivamente si acquista una sottoscrizione che include la classificazione e l'assegnazione di etichette, il client passa automaticamente alla modalità standard durante il download dei criteri di Azure Information Protection.

Se si usa l'applicazione RMS sharing per Windows, è consigliabile sostituirla con il client Azure Information Protection. Il supporto per questa applicazione di condivisione terminerà il 31 gennaio 2018. Per una più facile transizione, vedere [Attività eseguite in precedenza con l'applicazione RMS sharing](../rms-client/upgrade-client-app.md).

## <a name="does-azure-information-protection-support-on-premises-and-hybrid-scenarios"></a>Azure Information Protection supporta scenari locali e ibridi?

Sì. Anche se è una soluzione basata sul cloud, Azure Information Protection può classificare, etichettare e proteggere documenti e messaggi di posta elettronica archiviati in locale, oltre che nel cloud.

Se si hanno Exchange Server, SharePoint Server e file server Windows, è possibile distribuire il [connettore Rights Management](../deploy-use/deploy-rms-connector.md) per consentire a questi server locali di usare il servizio Azure Rights Management per proteggere messaggi di posta elettronica e documenti. È inoltre possibile sincronizzare ed eseguire la federazione dei controller di dominio di Active Directory con Azure AD per un'esperienza di autenticazione più semplice per gli utenti, ad esempio utilizzando [Azure AD Connect](http://azure.microsoft.com/documentation/articles/active-directory-aadconnect/).

Il servizio Azure Rights Management genera e gestisce automaticamente i certificati XrML come richiesto e quindi non usa un'infrastruttura PKI locale. Per altre informazioni sull'uso dei certificati in Azure Rights Management, vedere la sezione [Procedura dettagliata del funzionamento di Azure RMS: primo uso, protezione dei contenuti, utilizzo del contenuto](../understand-explore/how-does-it-work.md#walkthrough-of-how-azure-rms-works-first-use-content-protection-content-consumption) nell'articolo [Funzionamento di Azure RMS](../understand-explore/how-does-it-work.md).

## <a name="ive-heard-a-new-release-is-going-to-be-available-soon-for-azure-information-protectionwhen-will-it-be-released"></a>Secondo alcune voci, sarà presto disponibile una nuova versione di Azure Information Protection. Quando verrà rilasciata?

La documentazione tecnica non contiene informazioni sulle versioni future. Per questo tipo di informazioni e per gli annunci di nuove versioni, visitare il [blog di Enterprise Mobility + Security](https://blogs.technet.microsoft.com/enterprisemobility/?product=azure-information-protection,azure-rights-management-services) e ottenere gli aggiornamenti più recenti da [Dan Plastina @TheRMSGuy](https://twitter.com/TheRMSGuy) su Twitter. Se si è interessati a una versione di Office, assicurarsi di vedere anche il [blog di Office](https://blogs.office.com/).

## <a name="where-can-i-find-supporting-information-for-azure-information-protectionsuch-as-legal-compliance-and-slas"></a>Dov'è possibile reperire le informazioni di supporto per Azure Information Protection, ad esempio le note legali, le informazioni sulla conformità e i contratti di servizio?

Vedere [Informazioni su conformità e supporto per Azure Information Protection](../understand-explore/compliance.md).

## <a name="how-can-i-report-a-problem-or-send-feedback-for-azure-information-protection"></a>Come è possibile segnalare un problema o inviare commenti e suggerimenti per Azure Information Protection?

Per il supporto tecnico, usare i canali di supporto standard oppure [contattare il supporto tecnico Microsoft](information-support.md#to-contact-microsoft-support).

Per inviare commenti e suggerimenti per possibili miglioramenti o nuove funzionalità, fare clic su **Proteggi** e quindi su **Guida e commenti** nel gruppo **Protezione** della scheda **Home** dell'applicazione di Office. Nella finestra di dialogo **Microsoft Azure Information Protection** fare clic su **Invia commenti e suggerimenti**. Verrà aperto un messaggio di posta elettronica da inviare al team di Information Protection. È anche possibile rivolgersi al team di ingegneri nel [sito di Yammer per Azure Information Protection](https://www.yammer.com/askipteam/). 

## <a name="what-do-i-do-if-my-question-isnt-here"></a>Cosa fare se la domanda non è presente?

In primo luogo, esaminare le domande frequenti relative alle funzionalità di classificazione e assegnazione di etichette o alla protezione dei dati. Il servizio Azure Rights Management (Azure RMS) fornisce la tecnologia di protezione dati per Azure Information Protection e può essere usato con o senza le funzionalità per la classificazione e l'assegnazione di etichette: 

- [Domande frequenti sulla classificazione e l'assegnazione di etichette](faqs-infoprotect.md)

- [Domande frequenti sulla protezione dei dati](faqs-rms.md)

Per eventuali altri dubbi, usare i collegamenti e le risorse elencate in [Informazioni e supporto per Azure Information Protection](information-support.md).

Inoltre, esistono Domande frequenti progettate per gli utenti finali:

- [Domande frequenti sull'app Azure Information Protection per iOS e Android](../rms-client/mobile-app-faq.md)

- [Domande frequenti sull'app RMS per computer Mac e dispositivi Windows Phone](https://technet.microsoft.com/dn451248)

- [Domande frequenti sull'applicazione Rights Management sharing per Windows](https://technet.microsoft.com/dn467883)


[!INCLUDE[Commenting house rules](../includes/houserules.md)]

