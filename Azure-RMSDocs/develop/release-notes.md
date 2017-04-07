---
title: "Novità e note sulla versione | Azure RMS"
description: "Descrive importanti modifiche e funzionalità in questa nuova versione di SDK RMS."
author: bruceperlerms
ms.author: bruceper
manager: mbaldwin
ms.date: 02/23/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 4fa1c686-b00b-4734-9abb-141ce582a6af
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
ms.openlocfilehash: acd6dc2190996787b5354407bbaedec921a5b48c
ms.sourcegitcommit: 31e128cc1b917bf767987f0b2144b7f3b6288f2e
translationtype: HT
---
# <a name="whats-new-and-release-notes"></a>Novità e note sulla versione

## <a name="whats-new"></a>Novità
SDK 4.2 Microsoft Rights Management offre maggiore facilità e flessibilità nell'abilitazione di applicazioni RMS. Questo argomento descrive importanti modifiche e funzionalità in questa versione di SDK RMS.

### <a name="new-for-june-2016"></a>Novità di giugno 2016

- **Supporto dell'autenticazione moderna**: consente l'accesso basato su Active Directory Authentication Library (ADAL) alle app con il supporto predefinito per RMS. Attiva funzionalità di accesso come l'autenticazione a più fattori (MFA), provider di identità di terze parti basati su SAML con applicazioni client RMS, autenticazione basata su smart card e certificati ed elimina la necessità per le app con supporto predefinito per RMS di usare il protocollo di autenticazione di base.
- **Supporto del rilevamento dei documenti**: ora gli sviluppatori possono abilitare il rilevamento di documenti quando attivano la protezione dei documenti nelle app
- Miglioramenti delle prestazioni
- Correzione di bug


### <a name="december-2015-update"></a>Aggiornamento di dicembre 2015

Con questa versione, è ora disponibile la versione 4.2 SDK RMS per i dispositivi e aggiunge:

-   Rilevamento dei documenti, RMS solo online, per sistemi operativi iOS/OS X e Android.

    Per informazioni dettagliate e linee guida sull'uso in iOS/OS X, vedere la classe [MSLicenseMetadata](https://msdn.microsoft.com/library/mt573683.aspx) che offre informazioni di rilevamento e il metodo di registrazione del rilevamento del documento aggiuntivo in [MSUserPolicy](https://msdn.microsoft.com/library/dn790796.aspx). Ci sono aggiunte simili per Android in [LicenseMetadata](https://msdn.microsoft.com/library/mt573675.aspx) e [UserPolicy](https://msdn.microsoft.com/library/dn790887.aspx).

    Per una descrizione dettagliata della funzionalità di rilevamento del documento, vedere [Procedura: Usare il rilevamento dei documenti](how-to-use-document-tracking.md).

-   Set di metodi sincroni che le versioni asincrone in parallelo per l'API Android:

    [Metodo sincrono CustomProtectedInputStream.create](https://msdn.microsoft.com/library/mt631362.aspx)

    [Metodo sincrono CustomProtectedOutputStream.create](https://msdn.microsoft.com/library/mt631363.aspx)

    [Metodo sincrono ProtectedFileInputStream.create](https://msdn.microsoft.com/library/mt631375.aspx)

    [Metodo sincrono ProtectedFileOutputStream.create](https://msdn.microsoft.com/library/mt631376.aspx)

    [Metodo sincrono TemplateDescriptor.getTemplates](https://msdn.microsoft.com/library/mt631380.aspx)

    [Metodo sincrono UserPolicy.acquire](https://msdn.microsoft.com/library/mt631384.aspx)

    [Metodo sincrono UserPolicy.create (PolicyDescriptor…)**](https://msdn.microsoft.com/library/mt631385.aspx)

    [Metodo sincrono UserPolicy.create (TemplateDescriptor...)](https://msdn.microsoft.com/library/mt631386.aspx)

-   È stata aggiunta una nuova classe [ProtectedBuffer](https://msdn.microsoft.com/library/mt631369.aspx) all'API Android.
-   Aggiornamenti per migliorare i messaggi di errore e l'esperienza di risoluzione dei problemi.
-   Miglioramenti significativi delle prestazioni per le operazioni di crittografia.

### <a name="july-2015-update---adds-support-for-linux--c-development"></a>Aggiornamento di luglio 2015: aggiunta del supporto per Linux / sviluppo C++

Questa versione aggiunge le funzionalità seguenti:

-   SDK 4.1 RMS per piattaforme Linux

    Per altre informazioni, vedere [Introduzione](get-started.md).

### <a name="may-2015-update---adds-logging-control"></a>Aggiornamento di maggio 2015: aggiunta del controllo di registrazione

Questa versione aggiunge il supporto per le funzionalità seguenti:

-   iOS

    La crittografia e decrittografia dell'app può operare in modo indipendente e in parallelo.

    Per altre informazioni, vedere [MSProtector](https://msdn.microsoft.com/library/mt210993.aspx).

    Impostazioni di controllo a livello log abilitate.

    Per altre informazioni, vedere [Procedura: Abilitare la registrazione delle prestazioni e dell'errore](enabling-logging.md)

    Aggiunta del supporto di cancellazione della cache.

    Per altre informazioni, vedere [MSProtection:resetStateWithCompletionBlock](https://msdn.microsoft.com/library/mt210991.aspx).

### <a name="february-2015-update---adds-windows-store-application-support"></a>Aggiornamento di febbraio 2015: aggiunta del supporto di applicazioni Windows Store

Questa versione aggiunge il supporto per applicazioni Windows Store e offre la parità funzionale con la versione per Windows Phone, Android e iOS/OS X di SDK 4.1 RMS.

### <a name="january-2015-update---adds-winphone-platform-support"></a>Aggiornamento di gennaio 2015: aggiunta del supporto della piattaforma WinPhone

Questa versione aggiunge il supporto per il sistema operativo Windows Phone e offre la parità funzionale con la versione per Android e iOS/OS X di SDK 4.1 RMS.

### <a name="october-2014-update---upgrade-to-microsoft-rms-sdk-41"></a>Aggiornamento di ottobre 2014: l'aggiornamento a SDK 4.1 Microsoft RMS

La versione 4.1 di SDK RMS aggiunge le nuove funzionalità seguenti a Google Android e Apple iOS / OS X.

-   Estensioni dell'API SDK Android e iOS/OS X per l'elaborazione del *consenso dell'utente*, consentendo all'utente di confermare i comportamenti dell'SDK. Attualmente, il rilevamento dei documenti l'accesso a URL di servizio AD RMS sconosciuti sono i tipi di consenso supportati.

    Per altre informazioni, vedere come esempio, la versione dell'API Android dell'[interfaccia ConsentCallback](https://msdn.microsoft.com/library/dn833503.aspx).

-   Supporto ora di iOS 8 e OS X 10.10 (Yosemite). Sono state inoltre apportate alcune modifiche al nome di proprietà richieste da Xcode 6.

    Esempio; MSUserPolicy.name modificato in [MSUserPolicy.policyName](https://msdn.microsoft.com/library/dn790799.aspx).

## <a name="release-notes"></a>Note sulla versione

Questa sezione descrive le informazioni sulle versioni correnti e precedenti di Microsoft Rights Management SDK 4.x API, che gli sviluppatori devono tenere presenti.

**SDK 4.1 AD RMS: versione disponibilità globale per piattaforme iOS / OS X e Android**

-   **Supporto per AD RMS**: gli amministratori IT possono usare le app con abilitazione per RMS sui dispositivi mobili con le nuove estensioni del dispositivo mobile del server AD RMS disponibili.
-   **Uso offline**: gli utenti finali possono accedere ai dati protetti RMS offline.
-   **Autenticazione separata**: gli sviluppatori possono usare la propria libreria di autenticazione per Azure RMS e AD RMS, o usare [Azure AD Authentication Library (ADAL)](https://MSDN.Microsoft.Com/library/jj573266.aspx), che è la scelta più consigliata.
-   **Interfaccia utente separata**: gli sviluppatori possono compilare la propria interfaccia utente per proteggere e usare documenti protetti RMS.
-   **API riprogettata**: gli sviluppatori possono ora sfruttare una API di crittografia e decrittografia semplice e trasparente che offre comportamenti RMS ed esperienza utente coerenti con uno sforzo minimo

**Comuni a tutte le piattaforme**

-   Le API RMS SDK 4.x non sono *thread-safe*.

**Android**

-   Quando si usa un'applicazione di esempio in un dispositivo Amazon® Kindle per visualizzare gli allegati con estensione .ptxt, è necessario prima scaricare il file per visualizzarlo.

    **Soluzione**: questo è un problema noto e sarà risolto in un secondo momento.

-   Un'applicazione che usa il SDK potrebbe bloccarsi se sono consentite più istanze.

    **Soluzione**: assicurarsi che l'applicazione non consenta chiamate multi-istanza per l'API Android.

-   Se si usa il metodo [ProtectedFileOutputStream](https://msdn.microsoft.com/library/dn790855.aspx).write(byte\[\] array, int offset, int length) con una lunghezza diversa dal valore *array.length*, non è possibile leggere il contenuto in un secondo momento usando SDK.

    **Soluzione**: questo è un problema noto. Per limitare il problema, passare sempre un array *byte \[\]* con lo stesso valore di lunghezza del parametro di lunghezza oppure usare il metodo [ProtectedFileOutputStream](https://msdn.microsoft.com/library/dn790855.aspx).write(byte\[\] array).

**iOS e OS X**

-   Esistono due varianti regionali di portoghese supportati dai nostri SDK iOS e OS X. Sfortunatamente, a causa di un bug, la prima localizzazione non è attualmente supportata completamente. A causa di questo bug, il portoghese non è supportato completamente. La maggior parte del testo viene tradotta, ma non l'interfaccia utente.

    1. Portoghese

    2. Portoghese (Portogallo)

**Solo iOS**

-   RMS SDK 4.x non visualizza l'indicatore di attività di rete.

    Si tratta di un comportamento facoltativo noto per iOS, in base alle linee guida dell'interfaccia umana Apple.

**Solo OS X**

-   RMS SDK 4.x non visualizza l'indicatore di attività di rete.

    Si tratta di un comportamento facoltativo noto per OS X, in base alle linee guida dell'interfaccia umana Apple.

-   **Soluzione**: per creare un'applicazione multiple document interface (MDI) tramite SDK OS X, usare le linee guida seguenti.

    I metodi seguenti non devono essere eseguiti contemporaneamente. Per monitorare per il completamento dell'esecuzione, Usare l'approccio di blocco di completamento, come indicato.

    - [MSProtectedData.protectedDataWithProtectedFile](https://msdn.microsoft.com/library/dn758351.aspx)
    - [MSCustomProtectedData.customProtectedDataWithPolicy](https://msdn.microsoft.com/library/dn758315.aspx)



**Nota**: le applicazioni MDI non sono supportate dall'API di iOS.

## <a name="frequently-asked-questions"></a>Domande frequenti

**Tutte le piattaforme**

**D**: nel flusso di lavoro di protezione non è presente un'interfaccia utente per la selezione delle **autorizzazioni personalizzate**. Perché?

**R**: si tratta di un problema noto e sarà risolto in un secondo momento.

**D**: Come si ottengono nuovi tenant dell'organizzazione per provare SDK e applicazioni di esempio?

**R**: Per richiedere le credenziali per le organizzazioni di test di Azure AD RMS, inviare un messaggio di posta elettronica all'indirizzo <rmcstbeta@microsoft.com>.

**D**: Non sono visualizzate le informazioni dettagliate della gerarchia di test nella documentazione. Perché?

**R**: non esiste alcun concetto di gerarchia test con i nuovi SDK AD RMS. Si userà sempre la gerarchia di produzione.

**D**: Nella versione 2.1 di RMS SDK era necessario un manifesto generato per ciascuna applicazione che implementasse la protezione delle informazioni, è questo ancora vero per le versioni 4.0 e versioni successive di SDK?

**R**: No, i manifesti non sono più necessari per le versioni 3.0 e quelle successive di Rights Management SDK.

**Android**

**D**: Con quali ambienti di sviluppo è stato testato l'SDK?

**R**: Eclipse Juno che usa Google API 15 e versioni successive.

**D**: è possibile chiamare Cancel () un metodo di annullamento dal thread dell'interfaccia utente?
**R**: È necessario chiamare Cancel () da un thread non dell'interfaccia utente, poiché questo potrebbe interrompere una connessione di rete.

**iOS**

**D**: Quali piattaforme sono verificate per lo sviluppo SDK?

**R**: Xcode 5.0 con iOS 7 e versioni successive.

**D**: È stata eseguita la chiamata di un metodo Cancel () su un'operazione, tuttavia è stata comunque ricevuta la notifica di completamento dell'operazione. Perché?

**R**: Non è possibile annullare tutte le operazioni, pertanto un'operazione di annullamento viene eseguita nel modo migliore possibile.

**OS X**

**D**: Il framework dell'app di esempio è stato adattato a Xcode 5, è possibile lavorare con Xcode 4.6?

**R**: L'SDK di OS X funziona con Xcode 4.6 e versioni successive soltanto, nonché con OS X è 10.8 e versioni successive.

[!INCLUDE[Commenting house rules](../includes/houserules.md)]