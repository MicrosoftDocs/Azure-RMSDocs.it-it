---
title: Domande frequenti su Azure Information Protection
description: Alcune domande frequenti su Azure Information Protection e sul relativo servizio di protezione dei dati, Azure Rights Management (Azure RMS).
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/24/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 71ce491f-41c1-4d15-9646-455a6eaa157d
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 37ce3f1596878e28962119faef22bc1c61a067f8
ms.openlocfilehash: 0bb42f7ec5f2c1768c9eaaa7890b8b46853abd99
ms.lasthandoff: 02/25/2017


---

# <a name="frequently-asked-questions-for-azure-information-protection"></a>Domande frequenti su Azure Information Protection

>*Si applica a: Azure Information Protection, Office 365*

Di seguito sono riportate alcune possibili domande su Azure Information Protection o sul servizio Azure Rights Management (Azure RMS) e le relative risposte.

La pagina delle domande frequenti verrà aggiornata periodicamente e le nuove aggiunte saranno pubblicate negli annunci mensili di aggiornamento della documentazione sul [blog di Enterprise Mobility + Security](https://blogs.technet.microsoft.com/enterprisemobility/?product=azure-information-protection,azure-rights-management-services).

## <a name="whats-the-difference-between-azure-information-protection-and-azure-rights-management"></a>Quale è la differenza tra Azure Information Protection e Azure Rights Management?

Azure Information Protection offre funzionalità per la classificazione, l'assegnazione di etichette e la protezione per i documenti e i messaggi di posta elettronica di un'organizzazione. La tecnologia di protezione è basata sul servizio Azure Rights Management, che è ora un componente di Azure Information Protection.

## <a name="what-subscription-do-i-need-for-azure-information-protection-and-what-features-are-included"></a>Quale sottoscrizione è necessaria per Azure Information Protection e quali funzionalità sono incluse?
Vedere le [informazioni sulla sottoscrizione](https://www.microsoft.com/en-us/cloud-platform/azure-information-protection-pricing) e l'[elenco delle funzionalità](https://www.microsoft.com/en-us/cloud-platform/azure-information-protection-features) nel sito Azure Information Protection. 

Se si ha un abbonamento a Office 365 che include Rights Management, scaricare il [foglio dati di licenza di Azure Information Protection](http://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf) dalla pagina **Funzionalità**.

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

Per inviare feedback, ad esempio suggerimenti di possibili miglioramenti o nuove funzionalità: nel gruppo **Protezione** della scheda **Home** dell'applicazione di Office fare clic su **Proteggi** e quindi su **Guida e commenti**. Nella finestra di dialogo **Microsoft Azure Information Protection** fare clic su **Invia commenti e suggerimenti**. Verrà inviato un messaggio di posta elettronica al team di Information Protection. Al messaggio verranno allegati automaticamente i file di log del PC. 

È anche possibile rivolgersi al team di ingegneri nel [sito di Yammer per Azure Information Protection](https://www.yammer.com/askipteam/). 

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


