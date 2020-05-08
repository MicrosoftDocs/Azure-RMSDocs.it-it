---
title: Note Rrelease per la Rights Management Services SDK v4. x
description: Descrive importanti modifiche e funzionalità di questa versione e di quelle precedenti.
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
ms.custom: has-adal-ref
ms.openlocfilehash: 5d4aa9206865493c5fd2c4b2abdb96c3f72e5399
ms.sourcegitcommit: 298843953f9792c5879e199fd1695abf3d25aa70
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/08/2020
ms.locfileid: "82971949"
---
# <a name="whats-new-and-release-notes"></a>Novità e note sulla versione

[!INCLUDE [deprecation notice](../includes/deprecation-warning.md)]

## <a name="whats-new"></a>Novità

Questo argomento descrive importanti modifiche e funzionalità in questa nuova versione di RMS SDK v4. x.

-   [Novità di luglio 2017](#new-for-july-2017)
-   [Aggiornamento di ottobre 2016](#october-2016-update)
-   [Aggiornamento di giugno 2016](#june-2016-update)
-   [Aggiornamento di dicembre 2015](#december-2015-update)
-   [Aggiornamento di luglio 2015: aggiunta del supporto per lo sviluppo Linux/C++](#july-2015-update---adds-support-for-linux--c-development)
-   [Aggiornamento del 2015 maggio-aggiunta del controllo di registrazione](#may-2015-update---adds-logging-control)
-   [Aggiornamento di febbraio 2015: aggiunta del supporto per applicazioni Windows Store](#february-2015-update---adds-windows-store-application-support)
-   [Aggiornamento di gennaio 2015: aggiunta del supporto per la piattaforma WinPhone](#january-2015-update---adds-winphone-platform-support)
-   [Aggiornamento di ottobre 2014: aggiornamento a Microsoft RMS SDK 4.1](#october-2014-update---upgrade-to-microsoft-rms-sdk-41)
-   [Note sulla versione](#release-notes)
-   [Domande frequenti](#frequently-asked-questions)

### <a name="new-for-july-2017"></a>Novità di luglio 2017

L'aggiornamento della versione di luglio comprende l'incremento del numero di revisione dell'SDK alla versione 4.2.5.

- Android SDK: l'app può ora **impostare immediatamente il livello di registrazione ** con Android SDK. Per altre informazioni, vedere [Procedura: Abilitare la registrazione delle prestazioni e dell'errore](https://docs.microsoft.com/information-protection/develop/enabling-logging).
- Il livello di registrazione non è supportato da iOS SDK.
- In caso di token di accesso NULL, SDK ora restituisce un errore.

### <a name="october-2016-update"></a>Aggiornamento di ottobre 2016

- Implementazione di alcune correzioni di bug back-end.
- Bitcode abilitato per Apple iOS/OSX SDK.

### <a name="june-2016-update"></a>Aggiornamento di giugno 2016

- **Supporto per l'autenticazione moderna**: consente l'accesso basato su Active Directory Authentication Library (ADAL) alle app con il supporto predefinito per RMS. Abilita funzionalità di accesso come Multi-Factor Authentication (MFA), provider di identità di terze parti basati su SAML con applicazioni client RMS, autenticazione basata su smart card e certificati ed elimina la necessità per le app con il supporto predefinito per RMS di usare il protocollo di autenticazione di base.
- **Supporto per il rilevamento dei documenti**: ora gli sviluppatori possono abilitare il rilevamento dei documenti quando attivano la protezione dei documenti nelle app.
- Miglioramenti delle prestazioni.
- Correzioni di bug

### <a name="december-2015-update"></a>Aggiornamento di dicembre 2015

Con questa versione è disponibile la versione 4.2 SDK RMS per i dispositivi, che aggiunge:

-   Rilevamento dei documenti, RMS solo online, per sistemi operativi iOS/OS X e Android.

    Per informazioni dettagliate e linee guida sull'uso in iOS/OS X, vedere la classe [MSLicenseMetadata](https://msdn.microsoft.com/library/mt573683.aspx) che offre informazioni sul rilevamento e il metodo aggiuntivo di registrazione del rilevamento dei documenti in [MSUserPolicy](https://msdn.microsoft.com/library/dn790796.aspx). Ci sono aggiunte simili per Android in [LicenseMetadata](https://msdn.microsoft.com/library/mt573675.aspx) e [UserPolicy](https://msdn.microsoft.com/library/dn790887.aspx).

    Per una descrizione dettagliata della funzionalità di rilevamento dei documenti, vedere [Procedura: Usare il rilevamento dei documenti](how-to-use-document-tracking.md).

-   Set di metodi sincroni paralleli alle versioni asincrone per l'API Android:

    [Metodo sincrono CustomProtectedInputStream.create](https://msdn.microsoft.com/library/mt631362.aspx)

    [Metodo sincrono CustomProtectedOutputStream.create](https://msdn.microsoft.com/library/mt631363.aspx)

    [Metodo sincrono ProtectedFileInputStream.create](https://msdn.microsoft.com/library/mt631375.aspx)

    [Metodo sincrono ProtectedFileOutputStream.create](https://msdn.microsoft.com/library/mt631376.aspx)

    [Metodo sincrono TemplateDescriptor.getTemplates](https://msdn.microsoft.com/library/mt631380.aspx)

    [Metodo sincrono UserPolicy.acquire](https://msdn.microsoft.com/library/mt631384.aspx)

    [Metodo sincrono UserPolicy.create (PolicyDescriptor…)**](https://msdn.microsoft.com/library/mt631385.aspx)

    [Metodo sincrono UserPolicy.create (TempalteDescriptor…)](https://msdn.microsoft.com/library/mt631386.aspx)

-   È stata aggiunta una nuova classe [ProtectedBuffer](https://msdn.microsoft.com/library/mt631369.aspx) all'API Android.
-   Aggiornamenti per migliorare i messaggi di errore e la risoluzione ottimale dei problemi di prestazioni.
-   Miglioramenti significativi delle prestazioni per le operazioni crittografiche.

### <a name="july-2015-update---adds-support-for-linux--c-development"></a>Aggiornamento di luglio 2015: aggiunta del supporto per lo sviluppo Linux/C++

In questa versione sono stati aggiunti gli aggiornamenti seguenti:

-   RMS SDK 4.1 RMS per piattaforme Linux

    Per altre informazioni, vedere [Introduzione](get-started.md).

### <a name="may-2015-update---adds-logging-control"></a>Aggiornamento di maggio 2015: aggiunta del controllo registrazione

In questa versione è stato aggiunto il supporto per gli aggiornamenti seguenti:

-   iOS

    I processi di crittografia e decrittografia dell'app possono operare in modo indipendente e in parallelo.

    Per altre informazioni, vedere [MSProtector](https://msdn.microsoft.com/library/mt210993.aspx).

    Abilitazione delle impostazioni di controllo a livello di registro.

    Per altre informazioni, vedere [Procedura: Abilitare la registrazione delle prestazioni e dell'errore](enabling-logging.md).

    Aggiunta del supporto per la cancellazione della cache.

    Per altre informazioni, vedere [MSProtection:resetStateWithCompletionBlock](https://msdn.microsoft.com/library/mt210991.aspx).

### <a name="february-2015-update---adds-windows-store-application-support"></a>Aggiornamento di febbraio 2015: aggiunta del supporto per applicazioni Windows Store

In questa versione è stato aggiunto il supporto per le applicazioni Windows Store; è anche disponibile la parità funzionale con Windows Phone, Android e la versione iOS/OS X di RMS SDK 4.1.

### <a name="january-2015-update---adds-winphone-platform-support"></a>Aggiornamento di gennaio 2015: aggiunta del supporto per la piattaforma WinPhone

In questa versione è stato aggiunto il supporto per il sistema operativo Windows Phone; è anche disponibile la parità funzionale con Android e la versione iOS/OS X di RMS SDK 4.1.

### <a name="october-2014-update---upgrade-to-microsoft-rms-sdk-41"></a>Aggiornamento di ottobre 2014: aggiornamento a Microsoft RMS SDK 4.1

Nella versione 4.1 di RMS SDK sono state aggiunte le nuove funzionalità seguenti a Google Android e Apple iOS/OS X.

-   Estensioni dell'API Android e iOS/OS X inerenti l'*elaborazione del consenso utente*, per permettere all'utente di confermare i comportamenti dell'SDK. Attualmente, i tipi di consenso supportati sono il rilevamento dei documenti e l'accesso a URL del servizio AD RMS sconosciuti.

    Per altre informazioni, vedere l'esempio della versione dell'API Android dell'[interfaccia ConsentCallback](https://msdn.microsoft.com/library/dn833503.aspx).

-   Sono ora supportati iOS 8 e OS X 10.10 (Yosemite). Sono state apportate anche alcune modifiche ai nomi di proprietà richiesti da Xcode 6.

    Ad esempio MSUserPolicy.name è stato modificato in [MSUserPolicy.policyName](https://msdn.microsoft.com/library/dn790799.aspx).

## <a name="release-notes"></a>Note sulla versione

In questa sezione vengono presentate alcune informazioni sulle versioni correnti e precedenti delle API di Microsoft Rights Management SDK 4.x, che gli sviluppatori devono tenere presenti.

**AD RMS SDK 4.1 - iOS/OS X e piattaforme Android - Versione di disponibilità generale**

-   **Supporto per AD RMS**: gli amministratori IT possono usare le app abilitate per RMS sui dispositivi mobili con le nuove estensioni del dispositivo mobile del server AD RMS.
-   **Utilizzo offline**: gli utenti finali possono accedere offline ai dati protetti da RMS.
-   **Autenticazione separata**: gli sviluppatori possono usare la propria libreria di autenticazione per Azure RMS e AD RMS o usare la libreria consigliata [Azure AD Authentication Library (ADAL)](https://MSDN.Microsoft.Com/library/jj573266.aspx).
-   **Interfaccia utente separata**: gli sviluppatori possono compilare la propria interfaccia utente per proteggere e usare documenti protetti da RMS.
-   **API riprogettata**: gli sviluppatori possono ora sfruttare un'API di crittografia e decrittografia semplice e trasparente che offre comportamenti RMS ed esperienza utente coerenti, con un impegno minimo.

**Comune a tutte le piattaforme**

-   Le API RMS SDK 4.x non sono *thread-safe*.

**Android**

-   Quando si usa un'app di esempio in un dispositivo Amazon® Kindle per visualizzare allegati con estensione ptxt, è innanzitutto necessario scaricare il file prima di visualizzarlo.

    **Soluzione**: si tratta di un problema noto che verrà risolto in un secondo momento.

-   Un'applicazione che usa l'SDK può arrestarsi qualora siano consentite più istanze.

    **Soluzione**: verificare che l'applicazione non consenta le chiamate a più istanze per l'API Android.

-   Quando si utilizza il [metodo Metodo protectedfileoutputstream](https://msdn.microsoft.com/library/dn790855.aspx). Write (\[ \] matrice di byte, offset int, Lunghezza int) con una lunghezza diversa dal valore *Array. length* , non è possibile utilizzare il contenuto in un secondo momento utilizzando l'SDK.

    **Soluzione**: si tratta di un problema noto. Per attenuarlo, passare sempre una matrice di *byte \[ * con lo stesso valore di lunghezza del parametro length oppure usare il metodo [Metodo protectedfileoutputstream](https://msdn.microsoft.com/library/dn790855.aspx). Write (array di\[ \] byte).

**iOS e OS X**

-   Esistono due varianti regionali di portoghese supportate dagli SDK iOS e OS X. A causa di un bug, la prima localizzazione non è attualmente supportata in toto. A causa di questo bug, il portoghese non è completamente supportato. È tradotta la maggior parte del testo ma non l'interfaccia utente.

    1. Portoghese

    2. Portoghese (Portogallo)

**Solo iOS**

-   RMS SDK 4. x non visualizza l'indicatore dell'attività di rete.

    Secondo le Human Interface Guidelines di Apple, si tratta di un comportamento facoltativo noto per iOS.

**Solo OS X**

-   RMS SDK 4. x non visualizza l'indicatore dell'attività di rete.

    Secondo le Human Interface Guidelines di Apple, si tratta di un comportamento facoltativo noto per OS X.

-   **Soluzione**: per creare un'applicazione con interfaccia a documenti multipli (MDI) usando l'SDK per OS X, attenersi alle linee guida seguenti.

    I metodi seguenti non devono essere eseguiti contemporaneamente. Per monitorare il completamento dell'esecuzione, usare i blocchi di completamento come indicato di seguito.

    - [MSProtectedData.protectedDataWithProtectedFile](https://msdn.microsoft.com/library/dn758351.aspx)
    - [MSCustomProtectedData.customProtectedDataWithPolicy](https://msdn.microsoft.com/library/dn758315.aspx)



**Nota**  le applicazioni MDI non sono supportate dall'API di iOS.

## <a name="frequently-asked-questions"></a>Domande frequenti

**Tutte le piattaforme**

**D**: non è possibile visualizzare l'interfaccia utente per la selezione delle **autorizzazioni personalizzate** nel flusso di lavoro di protezione. Perché?

**R**: si tratta di un problema noto che verrà risolto in un secondo momento.

**D**: come si ottengono nuovi tenant dell'organizzazione per provare l'SDK e le applicazioni di esempio?

**R**: per richiedere le credenziali per le organizzazioni di test di Azure AD RMS, inviare un messaggio a <rmcstbeta@microsoft.com>.

**D**: nella documentazione non sono visualizzate informazioni dettagliate sulla gerarchia di test. Perché?

**R**: non è presente alcun concetto di gerarchia di test nei nuovi SDK di AD RMS. Si usa sempre la gerarchia di produzione.

**D**: nella versione 2.1 di RMS SDK è necessario un manifesto generato per ogni applicazione che implementa la protezione delle informazioni. È un requisito ancora valido per la versione 4.0 e successive dell'SDK?

**R**: no, i manifesti non sono più necessari a partire dalla versione 3.0 dell'SDK di Rights Management.

**Android**

**D**: in quali ambienti di sviluppo è stato testato l'SDK?

**R**: Eclipse Juno che usa Google API 15 e versioni successive.

**D**: è possibile chiamare il metodo di annullamento Cancel () dal thread dell'interfaccia utente?
**R**: è necessario chiamare il metodo Cancel () da un thread non appartenente all'interfaccia utente, in caso contrario la connessione di rete potrebbe interrompersi.

**iOS**

**D**: quali sono le piattaforme verificate per lo sviluppo SDK?

**R**: Xcode 5.0 con iOS 7 e versioni successive.

**D**: è stato chiamato un metodo Cancel () su un'operazione, tuttavia viene comunque ricevuta la notifica del completamento dell'operazione. Perché?

**R:**: non tutte le operazioni possono essere annullate, pertanto l'operazione di annullamento viene eseguita nel miglior modo possibile.

**OS x**

**D**: il framework dell'applicazione di esempio è adattato a Xcode 5; è possibile lavorare con Xcode 4.6?

**R**: l'SDK per OS X funziona soltanto con Xcode 4.6 e versioni successive, nonché con OS X 10.8 e versioni successive.
