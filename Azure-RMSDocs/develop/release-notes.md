---
title: Novità e note sulla versione
description: Descrive importanti modifiche e funzionalità in questa versione e nelle versioni precedenti.
author: msmbaldwin
ms.author: mbaldwin
manager: barbkess
ms.date: 12/11/2018
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 4fa1c686-b00b-4734-9abb-141ce582a6af
audience: developer
ms.reviewer: kartikk
ms.suite: ems
ms.openlocfilehash: d9fda9c7477c408e8003f48c85e6d35fec6a1884
ms.sourcegitcommit: 8da0aa8f9bb9f91375580a703682d23a81a441bf
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/02/2019
ms.locfileid: "58809812"
---
# <a name="whats-new-and-release-notes"></a>Novità e note sulla versione

## <a name="whats-new"></a>Novità

Questo argomento descrive importanti modifiche e funzionalità in questa nuova versione di RMS SDK v4.x.

-   [Novità di luglio 2017](#new-for-july-2017)
-   [Aggiornamento di ottobre 2016](#october-2016-update)
-   [Aggiornamento di giugno 2016](#june-2016-update)
-   [Aggiornamento di dicembre 2015](#december-2015-update)
-   [Aggiornamento di luglio 2015: aggiunta del supporto per Linux/sviluppo C++](#july-2015-update---adds-support-for-linux--c-development)
-   [Aggiornamento di maggio 2015: aggiunta del controllo registrazione](#may-2015-update---adds-logging-control)
-   [Aggiornamento di febbraio 2015: aggiunta del supporto per applicazioni di Windows Store](#february-2015-update---adds-windows-store-application-support)
-   [Aggiornamento di gennaio 2015: aggiunta del supporto per la piattaforma WinPhone](#january-2015-update---adds-winphone-platform-support)
-   [Aggiornamento di ottobre 2014: aggiornamento a Microsoft RMS SDK 4.1](#october-2014-update---upgrade-to-microsoft-rms-sdk-41)
-   [Note sulla versione](#release-notes)
-   [Domande frequenti](#frequently-asked-questions)

### <a name="new-for-july-2017"></a>Novità di luglio 2017

L'aggiornamento della versione di luglio comprende l'incremento del numero di revisione di SDK alla versione 4.2.5.

- Android SDK: l'app può ora **impostare immediatamente il livello di registrazione** con Android SDK. Per altre informazioni, vedere [Procedura: Come abilitare la registrazione delle prestazioni e dell'errore](https://docs.microsoft.com/information-protection/develop/enabling-logging)
- Il livello di registrazione non è supportato da iOS SDK. 
- In caso di token di accesso NULL, SDK ora restituisce un errore.

### <a name="october-2016-update"></a>Aggiornamento di ottobre 2016

- Implementazione di alcune correzioni di bug back-end.
- Bitcode abilitato per Apple iOS/OSX SDK.

### <a name="june-2016-update"></a>Aggiornamento di giugno 2016

- **Supporto per l'autenticazione moderna**: consente l'accesso basato su Active Directory Authentication Library (ADAL) alle app con il supporto predefinito per RMS. Abilita funzionalità di accesso come Multi-Factor Authentication (MFA), provider di identità di terze parti basati su SAML con applicazioni client RMS, autenticazione basata su smart card e certificati ed elimina la necessità per le app con il supporto predefinito per RMS di usare il protocollo di autenticazione di base.
- **Supporto del rilevamento dei documenti**: ora gli sviluppatori possono abilitare il rilevamento di documenti quando attivano la protezione dei documenti nelle app
- Miglioramenti delle prestazioni
- Correzione di bug

### <a name="december-2015-update"></a>Aggiornamento di dicembre 2015

Con questa versione, è ora disponibile la versione 4.2 SDK RMS per i dispositivi e aggiunge:

-   Rilevamento dei documenti, RMS solo online, per sistemi operativi iOS/OS X e Android.

    Per informazioni dettagliate e linee guida sull'uso in iOS/OS X, vedere la classe [MSLicenseMetadata](https://msdn.microsoft.com/library/mt573683.aspx) che offre informazioni sul rilevamento e il metodo aggiuntivo di registrazione del rilevamento dei documenti in [MSUserPolicy](https://msdn.microsoft.com/library/dn790796.aspx). Ci sono aggiunte simili per Android in [LicenseMetadata](https://msdn.microsoft.com/library/mt573675.aspx) e [UserPolicy](https://msdn.microsoft.com/library/dn790887.aspx).

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

Questa versione aggiunge gli aggiornamenti seguenti:

-   SDK 4.1 RMS per piattaforme Linux

    Per altre informazioni, vedere [Introduzione](get-started.md).

### <a name="may-2015-update---adds-logging-control"></a>Aggiornamento di maggio 2015: aggiunta del controllo di registrazione

Questa versione aggiunge il supporto per gli aggiornamenti seguenti:

-   iOS

    La crittografia e decrittografia dell'app può operare in modo indipendente e in parallelo.

    Per altre informazioni, vedere [MSProtector](https://msdn.microsoft.com/library/mt210993.aspx).

    Impostazioni di controllo a livello log abilitate.

    Per altre informazioni, vedere [Procedura: Come abilitare la registrazione delle prestazioni e dell'errore](enabling-logging.md)

    Aggiunta del supporto di cancellazione della cache.

    Per altre informazioni, vedere [MSProtection:resetStateWithCompletionBlock](https://msdn.microsoft.com/library/mt210991.aspx).

### <a name="february-2015-update---adds-windows-store-application-support"></a>Aggiornamento di febbraio 2015: aggiunta del supporto di applicazioni Windows Store

Questa versione aggiunge il supporto per applicazioni di Windows Store e offre parità funzionale rispetto alla versione per Windows Phone, Android e iOS/OS X di RMS SDK 4.1.

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
-   **Uso offline**: gli utenti finali possono accedere ai dati protetti tramite RMS offline.
-   **Autenticazione separata**: gli sviluppatori possono usare la propria libreria di autenticazione per Azure RMS e AD RMS, o usare [Azure AD Authentication Library (ADAL)](https://MSDN.Microsoft.Com/library/jj573266.aspx), che è la scelta più consigliata.
-   **Interfaccia utente separata**: gli sviluppatori possono compilare la propria interfaccia utente per proteggere e usare documenti protetti RMS.
-   **API riprogettata**: gli sviluppatori possono ora sfruttare una API di crittografia e decrittografia diretta e trasparente che offre comportamenti RMS ed esperienza utente coerenti con sforzo minimo.

**Comuni a tutte le piattaforme**

-   Le API RMS SDK 4.x non sono *thread-safe*.

**Android**

-   Quando si usa un'applicazione di esempio in un dispositivo Amazon® Kindle per visualizzare gli allegati con estensione .ptxt, è necessario prima scaricare il file per visualizzarlo.

    **Soluzione**: problema noto e sarà risolto in un secondo momento.

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

    Si tratta di un comportamento facoltativo noto per iOS, in base a quanto definito nella guida Human Interface Guidelines di Apple.

**Solo OS X**

-   RMS SDK 4.x non visualizza l'indicatore di attività di rete.

    Si tratta di un comportamento facoltativo noto per OS X, in base a quanto definito nella guida Human Interface Guidelines di Apple.

-   **Soluzione**: per creare un'applicazione multiple document interface (MDI) tramite SDK OS X, usare le linee guida seguenti.

    I metodi seguenti non devono essere eseguiti contemporaneamente. Per monitorare il completamento dell'esecuzione, usare i blocchi di completamento come indicato di seguito.

    - [MSProtectedData.protectedDataWithProtectedFile](https://msdn.microsoft.com/library/dn758351.aspx)
    - [MSCustomProtectedData.customProtectedDataWithPolicy](https://msdn.microsoft.com/library/dn758315.aspx)



**Nota**  le applicazioni MDI non sono supportate dall'API di iOS.

## <a name="frequently-asked-questions"></a>Domande frequenti

**Tutte le piattaforme**

**D**: Nel flusso di lavoro di protezione non è presente un'interfaccia utente per la selezione delle **autorizzazioni personalizzate**. Perché?

**R**: Si tratta di un problema noto e sarà risolto in un secondo momento.

**D**: Come si ottengono nuovi tenant dell'organizzazione per provare SDK e applicazioni di esempio?

**R**: Per richiedere le credenziali per le organizzazioni di test di Azure AD RMS, inviare un messaggio di posta elettronica all'indirizzo <rmcstbeta@microsoft.com>.

**D**: Non sono visualizzate le informazioni dettagliate della gerarchia di test nella documentazione. Perché?

**R**: Non esiste alcun concetto di gerarchia di test con i nuovi SDK AD RMS. Si userà sempre la gerarchia di produzione.

**D**: Nella versione 2.1 di RMS SDK è necessario un manifesto generato per ogni applicazione che implementa la protezione delle informazioni. È un requisito ancora valido per la versione 4.0 e le versioni di SDK successive?

**R**: No, i manifesti non sono più necessari per le versioni 3.0 e quelle successive di Rights Management SDK.

**Android**

**D**: Con quali ambienti di sviluppo è stato testato l'SDK?

**R**: Eclipse Juno che usa Google API 15 e versioni successive.

**D**: È possibile chiamare il metodo di annullamento cancel() dal thread dell'interfaccia utente?
**R**: È necessario chiamare cancel() da un thread non dell'interfaccia utente, poiché si potrebbe interrompere una connessione di rete.

**iOS**

**D**: Quali piattaforme sono state verificate per lo sviluppo SDK?

**R**: Xcode 5.0 con iOS 7 e versioni successive.

**D**: È stata eseguita la chiamata di un metodo cancel() per un'operazione ma si riceve comunque la notifica di completamento dell'operazione. Perché?

**R**: Non tutte le operazioni possono essere annullate, quindi l'operazione di annullamento viene eseguita nel modo migliore possibile.

**OS X**

**D**: Il framework dell'app di esempio è stato adattato a Xcode 5, è possibile lavorare con Xcode 4.6?

**R**: L'SDK di OS X funziona con Xcode 4.6 e versioni successive soltanto, nonché con OS X è 10.8 e versioni successive.
