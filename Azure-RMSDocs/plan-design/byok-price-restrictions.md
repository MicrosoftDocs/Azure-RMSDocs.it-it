---
title: "Prezzi e restrizioni della modalità BYOK - Azure Information Protection"
description: Informazioni sulle restrizioni quando si usano chiavi gestite dal cliente (&quot;bring your own key&quot; o BYOK) con Azure RMS.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/23/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: f5930ed3-a6cf-4eac-b2ec-fcf63aa4e809
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: ab3b25ebd04565f8cd0e9236c1241f38d4a2e8b2
ms.sourcegitcommit: 31e128cc1b917bf767987f0b2144b7f3b6288f2e
translationtype: HT
---
# <a name="byok-pricing-and-restrictions"></a>Prezzi e restrizioni della modalità BYOK

>*Si applica a: Azure Information Protection, Office 365*


Le organizzazioni che hanno una sottoscrizione che include Azure Information Protection possono configurare il tenant di Azure Information Protection per usare una chiave gestita dal cliente (BYOK) e [registrarne l'utilizzo](../deploy-use/log-analyze-usage.md) senza alcun costo aggiuntivo. 

La chiave deve essere archiviata in Insieme di credenziali delle chiavi di Azure, per il quale è necessario disporre di una sottoscrizione di Azure a pagamento (o di valutazione). È anche necessario usare il livello di servizio Premium di Insieme di credenziali delle chiavi di Azure per supportare le chiavi protette dal modulo di protezione hardware. L'uso di una chiave protetta dal modulo di protezione hardware in Insieme di credenziali delle chiavi di Azure comporta l'addebito di un costo mensile. Per altre informazioni, vedere la pagina [dei prezzi di Insieme di credenziali delle chiavi di Azure](https://azure.microsoft.com/en-us/pricing/details/key-vault/).

Quando si usa Insieme di credenziali delle chiavi di Azure per la chiave del tenant Azure Information Protection, è consigliabile usare un insieme di credenziali delle chiavi dedicato per questa chiave con una sottoscrizione dedicata, per garantire che venga usata solo dal servizio Azure Rights Management. 

## <a name="benefits-of-using-azure-key-vault"></a>Vantaggi dell'uso di Insieme di credenziali delle chiavi di Azure

Oltre alla funzionalità di registrazione dell'utilizzo di Azure Information Protection, per una maggiore sicurezza è possibile creare riferimenti incrociati con la [registrazione di Insieme di credenziali delle chiavi di Azure](https://azure.microsoft.com/documentation/articles/key-vault-logging/) per controllare in modo indipendente se la chiave viene usata solo dal servizio Azure Rights Management. Se necessario, è possibile revocare immediatamente l'accesso alla chiave rimuovendo le autorizzazioni per l'insieme di credenziali delle chiavi.

Altri vantaggi dell'uso di Insieme di credenziali delle chiavi di Azure per la chiave del tenant Azure Information Protection:

- Insieme di credenziali delle chiavi di Azure offre una soluzione di gestione centralizzata delle chiavi coerente per molti servizi basati su cloud o persino locali che usano la crittografia.

- Insieme di credenziali delle chiavi di Azure supporta un numero di interfacce predefinite per la gestione delle chiavi, tra cui PowerShell, l'interfaccia della riga di comando, API REST e il portale di Azure. Altri servizi e strumenti sono stati integrati nell'insieme di credenziali delle chiavi per fornire funzionalità ottimizzate per attività specifiche, ad esempio il monitoraggio. Ad esempio, è possibile analizzare i log di utilizzo delle chiavi con Log Analytics da Operations Management Suite, impostare avvisi quando vengono soddisfatti determinati criteri e così via.

- Insieme di credenziali delle chiavi di Azure fornisce la separazione dei ruoli, una procedura di sicurezza consigliata di comprovata efficacia. Gli amministratori di Azure Information Protection possono concentrarsi sulla gestione della protezione e della classificazione dei dati, mentre gli amministratori di Insieme di credenziali delle chiavi di Azure possono concentrarsi sulla gestione delle chiavi di crittografia e dei criteri speciali che potrebbero essere necessari per la sicurezza o la conformità.

- Alcune organizzazioni hanno restrizioni relative alla posizione della chiave master. Insieme di credenziali delle chiavi di Azure fornisce un alto livello di controllo sull'archiviazione della chiave master perché il servizio è disponibile in molte aree di Azure. Attualmente, è possibile scegliere tra 28 aree di Azure e si prevede di aumentare questo numero. Per altre informazioni, vedere la pagina [Prodotti disponibili in base all'area] (https://azure.microsoft.com/regions/services/) nel sito di Azure.

Oltre alla gestione delle chiavi, Insieme di credenziali delle chiavi di Azure offre agli amministratori della protezione la stessa esperienza di gestione per archiviare, accedere e gestire i certificati e i segreti, ad esempio le password, per altri servizi e applicazioni che usano la crittografia. 

Per altre informazioni su Insieme di credenziali delle chiavi di Azure, vedere [Cos'è l'insieme di credenziali chiave di Azure?](https://azure.microsoft.com/documentation/articles/key-vault-whatis/) e visitare il [blog del team di Insieme di credenziali delle chiavi di Azure](https://blogs.technet.microsoft.com/kv/) per le informazioni più recenti e per scoprire come viene usata questa tecnologia dagli altri servizi.


## <a name="restrictions-when-using-byok"></a>Restrizioni per l'uso di BYOK

Se sono presenti utenti che hanno effettuato l'iscrizione per un account gratuito con RMS per utenti singoli, non è possibile usare BYOK o la registrazione dell'utilizzo perché questa configurazione non ha un amministratore tenant per configurare tali funzionalità.


> [!NOTE]
> Per altre informazioni, vedere [RMS per utenti singoli e Azure Rights Management](../understand-explore/rms-for-individuals.md).

![BYOK non supporta Exchange Online](../media/RMS_BYOK_noExchange.png)

La modalità BYOK e la registrazione dell'utilizzo possono essere usate facilmente con ogni applicazione che si integra con il servizio Azure Rights Management (Azure RMS) usato da Azure Information Protection. ad esempio servizi cloud come SharePoint Online, server locali che eseguono Exchange e SharePoint che si integrano con Azure RMS usando il connettore RMS e applicazioni client come Office 2016 e Office 2013. È possibile ottenere log di utilizzo indipendentemente dall'applicazione che richiede Azure RMS.

È presente tuttavia un'eccezione, Attualmente, la **modalità BYOK di Azure RMS non è compatibile con Exchange Online**. Se si vuole usare Exchange Online, è consigliabile distribuire Azure RMS con la modalità predefinita per la gestione delle chiavi, in base alla quale Microsoft genera e gestisce la chiave. È possibile passare a BYOK successivamente, ad esempio, quando Exchange Online supporterà la modalità BYOK per Azure RMS. Se non è possibile aspettare, tuttavia, si può distribuire subito Azure RMS con BYOK, con una funzionalità RMS ridotta per Exchange Online (i messaggi di posta elettronica e gli allegati non protetti rimangono completamente funzionanti):

-   I messaggi di posta elettronica protetti o gli allegati protetti in Outlook Web Access non possono essere visualizzati.

-   I messaggi di posta elettronica protetti nei dispositivi mobili che usano Exchange ActiveSync IRM non possono essere visualizzati.

-   La decrittografia del trasporto (ad esempio, per l'analisi antimalware) e la decrittografia del giornale di registrazione non sono possibili, quindi i messaggi di posta elettronica e gli allegati protetti verranno ignorati.

-   Le regole di protezione del trasporto e la prevenzione della perdita dei dati che applicano i criteri IRM non sono possibili e non è quindi possibile applicare la protezione RMS usando questi metodi.

-   La ricerca di messaggi di posta elettronica protetti è basata sul server, quindi i messaggi di posta elettronica protetti verranno ignorati.

Quando si usa la modalità BYOK di Azure RMS con una funzionalità RMS ridotta per Exchange Online, RMS funzionerà con i client di posta elettronica in Outlook su Windows e Mac e con altri client di posta elettronica che non usano Exchange ActiveSync IRM.

Se si esegue la migrazione ad Azure RMS da AD RMS, la chiave potrebbe essere stata importata come dominio di pubblicazione trusted in Exchange Online (ovvero in modalità BYOK nella terminologia di Exchange, che è diversa dalla modalità BYOK di Insieme di credenziali delle chiavi di Azure). In questo scenario è necessario rimuovere il dominio di pubblicazione trusted da Exchange Online per evitare conflitti tra modelli e criteri. Per ulteriori informazioni, vedere [Remove-RMSTrustedPublishingDomain](https://technet.microsoft.com/library/jj200720%28v=exchg.150%29.aspx) nella libreria di cmdlet di Exchange Online.

In alcuni casi l'eccezione relativa alla modalità BYOK di Azure RMS per Exchange Online non costituisce in effetti un problema. Ad esempio, le organizzazioni che devono usare la modalità BYOK e la registrazione eseguono le proprie applicazioni dati, ad esempio Exchange, SharePoint, Office, in locale e usano Azure RMS per funzionalità non facilmente disponibili con istanze locali di AD RMS, ad esempio collaborazione con altre società e accesso da client mobili. Sia la modalità BYOK che la registrazione sono compatibili con questo scenario e consentono all'organizzazione di disporre del controllo completo sulla sottoscrizione di Azure RMS.

## <a name="next-steps"></a>Passaggi successivi

Per gestire la propria chiave, passare all'articolo relativo all'[implementazione della chiave del tenant di Azure Rights Management](plan-implement-tenant-key.md#implementing-your-azure-information-protection-tenant-key).

Se si è deciso di usare la configurazione predefinita in cui Microsoft gestisce la chiave del tenant, vedere la sezione [Passaggi successivi](plan-implement-tenant-key.md#next-steps) dell'articolo Pianificazione e implementazione della chiave del tenant di Azure Rights Management.

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
