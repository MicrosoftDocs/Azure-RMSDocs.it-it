---
title: "Prezzi e restrizioni della modalità BYOK | Azure RMS"
description: "Le organizzazioni che hanno una sottoscrizione che include Azure Rights Management possono usare chiavi gestite dal cliente (BYOK) in Insieme di credenziali delle chiavi di Azure e registrarne l'utilizzo senza alcun costo aggiuntivo. Tuttavia, per usare Insieme di credenziali delle chiavi di Azure, è necessaria una sottoscrizione di Azure che supporti l'insieme di credenziali delle chiavi con chiavi protette dal modulo di protezione hardware. L'uso di una chiave in Insieme di credenziali delle chiavi di Azure comporta l'addebito di una tariffa mensile. Per altre informazioni, vedere la pagina dei prezzi di Insieme di credenziali delle chiavi di Azure."
author: cabailey
manager: mbaldwin
ms.date: 08/17/2016
ms.topic: article
ms.prod: 
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: f5930ed3-a6cf-4eac-b2ec-fcf63aa4e809
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 26b043f1f9e7a1e0cd00c2f31c28f7d6685f0232
ms.openlocfilehash: 8505032a2a12f84c245e834e71d0b7b0d12e894f


---

# Prezzi e restrizioni della modalità BYOK

>*Si applica a: Azure Rights Management, Office 365*


Le organizzazioni che hanno una sottoscrizione che include Azure Rights Management possono usare chiavi gestite dal cliente (BYOK) in Insieme di credenziali delle chiavi di Azure e registrarne l'utilizzo senza alcun costo aggiuntivo. Tuttavia, per usare Insieme di credenziali delle chiavi di Azure, è necessaria una sottoscrizione di Azure che supporti l'insieme di credenziali delle chiavi con chiavi protette dal modulo di protezione hardware. L'uso di una chiave in Insieme di credenziali delle chiavi di Azure comporta l'addebito di una tariffa mensile. Per altre informazioni, vedere la pagina [dei prezzi di Insieme di credenziali delle chiavi di Azure](https://azure.microsoft.com/en-us/pricing/details/key-vault/).

Se sono presenti utenti che hanno effettuato l'iscrizione per un account gratuito tramite RMS per utenti singoli, non è possibile usare la modalità BYOK e la registrazione dell'utilizzo perché questa configurazione non dispone di un amministratore tenant per configurare tali funzionalità.


> [!NOTE]
> Per altre informazioni, vedere [RMS per utenti singoli e Azure Rights Management](../understand-explore/rms-for-individuals.md).

![BYOK non supporta Exchange Online](../media/RMS_BYOK_noExchange.png)

La modalità BYOK e la registrazione dell'utilizzo possono essere usate facilmente con ogni applicazione che si integra con Azure RMS, ad esempio servizi cloud come SharePoint Online, server locali che eseguono Exchange e SharePoint che si integrano con Azure RMS usando il connettore RMS e applicazioni client come Office 2016 e Office 2013. È possibile ottenere log di utilizzo indipendentemente dall'applicazione che richiede Azure RMS.

È presente tuttavia un'eccezione, Attualmente, la **modalità BYOK di Azure RMS non è compatibile con Exchange Online**. Se si vuole usare Exchange Online, è consigliabile distribuire Azure RMS con la modalità predefinita per la gestione delle chiavi, in base alla quale Microsoft genera e gestisce la chiave. È possibile passare a BYOK successivamente, ad esempio, quando Exchange Online supporterà la modalità BYOK per Azure RMS. Se non è possibile aspettare, tuttavia, si può distribuire subito Azure RMS con BYOK, con una funzionalità RMS ridotta per Exchange Online (i messaggi di posta elettronica e gli allegati non protetti rimangono completamente funzionanti):

-   I messaggi di posta elettronica protetti o gli allegati protetti in Outlook Web Access non possono essere visualizzati.

-   I messaggi di posta elettronica protetti nei dispositivi mobili che usano Exchange ActiveSync IRM non possono essere visualizzati.

-   La decrittografia del trasporto (ad esempio, per l'analisi antimalware) e la decrittografia del giornale di registrazione non sono possibili, quindi i messaggi di posta elettronica e gli allegati protetti verranno ignorati.

-   Le regole di protezione del trasporto e la prevenzione della perdita dei dati che applicano i criteri IRM non sono possibili e non è quindi possibile applicare la protezione RMS usando questi metodi.

-   La ricerca di messaggi di posta elettronica protetti è basata sul server, quindi i messaggi di posta elettronica protetti verranno ignorati.

Quando si usa la modalità BYOK di Azure RMS con una funzionalità RMS ridotta per Exchange Online, RMS funzionerà con i client di posta elettronica in Outlook su Windows e Mac e con altri client di posta elettronica che non usano Exchange ActiveSync IRM.

Se si esegue la migrazione ad Azure RMS da AD RMS, la chiave potrebbe essere stata importata come dominio di pubblicazione trusted in Exchange Online (ovvero in modalità BYOK nella terminologia di Exchange, che è diversa dalla modalità BYOK di Insieme di credenziali delle chiavi di Azure). In questo scenario è necessario rimuovere il dominio di pubblicazione trusted da Exchange Online per evitare conflitti tra modelli e criteri. Per ulteriori informazioni, vedere [Remove-RMSTrustedPublishingDomain](https://technet.microsoft.com/library/jj200720%28v=exchg.150%29.aspx) nella libreria di cmdlet di Exchange Online.

In alcuni casi l'eccezione relativa alla modalità BYOK di Azure RMS per Exchange Online non costituisce in effetti un problema. Ad esempio, le organizzazioni che devono usare la modalità BYOK e la registrazione eseguono le proprie applicazioni dati, ad esempio Exchange, SharePoint, Office, in locale e usano Azure RMS per funzionalità non facilmente disponibili con istanze locali di AD RMS, ad esempio collaborazione con altre società e accesso da client mobili. Sia la modalità BYOK che la registrazione sono compatibili con questo scenario e consentono all'organizzazione di disporre del controllo completo sulla sottoscrizione di Azure RMS.

## Passaggi successivi

Per gestire la propria chiave, passare all'articolo relativo all'[implementazione della chiave del tenant di Azure Rights Management](plan-implement-tenant-key.md#implementing-your-azure-rights-management-tenant-key).

Se si è deciso di usare la configurazione predefinita in cui Microsoft gestisce la chiave del tenant, vedere la sezione [Passaggi successivi](plan-implement-tenant-key.md#next-steps) dell'articolo Pianificazione e implementazione della chiave del tenant di Azure Rights Management.




<!--HONumber=Aug16_HO4-->


