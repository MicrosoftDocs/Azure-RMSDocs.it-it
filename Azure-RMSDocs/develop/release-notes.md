---
title: "Novità e note sulla versione | Azure RMS"
description: "Descrive importanti modifiche e funzionalità in questa nuova versione di SDK RMS."
keywords: 
author: bruceperlerms
manager: mbaldwin
ms.date: 06/16/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 4fa1c686-b00b-4734-9abb-141ce582a6af
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: f7dd88d90357c99c69fe4fdde67c1544595e02f8
ms.openlocfilehash: eccc0ba9c13e0c35c8d0c8877ce92f9b99e83835


---

# Novità e note sulla versione

## Novità
SDK 4.2 Microsoft Rights Management offre maggiore facilità e flessibilità nell'abilitazione di applicazioni RMS. Questo argomento descrive importanti modifiche e funzionalità in questa nuova versione di SDK RMS.

-   [Novità di giugno 2016](#new_for_June_2016)
-   [Aggiornamento di dicembre 2015](#december_2015_update)
-   [Aggiornamento di luglio 2015: aggiunta del supporto per Linux / sviluppo C++](#july_2015_update_-_adds_support_for_linux___c___development)
-   [Aggiornamento di maggio 2015: aggiunta del controllo di registrazione](#may_2015_update_-_adds_logging_control)
-   [Aggiornamento di febbraio 2015: aggiunta del supporto di applicazioni Windows Store](#february_2015_update_-_adds_windows_store_application_support)
-   [Aggiornamento di gennaio 2015: aggiunta del supporto della piattaforma WinPhone](#january_2015_update_-_adds_winphone_platform_support)
-   [Aggiornamento di ottobre 2014: l'aggiornamento a SDK 4.1 Microsoft RMS](#october_2014_update_-_upgrade_to_microsoft_rms_sdk_4.1)
-   [Note sulla versione](#release-notes)
-   [Domande frequenti](#frequently_asked_questions)

### Novità di giugno 2016

- **Supporto dell'autenticazione moderna**: consente l'accesso basato su Active Directory Authentication Library (ADAL) alle app con il supporto predefinito per RMS. Attiva funzionalità di accesso come l'autenticazione a più fattori (MFA), provider di identità di terze parti basati su SAML con applicazioni client RMS, autenticazione basata su smart card e certificati ed elimina la necessità per le app con supporto predefinito per RMS di usare il protocollo di autenticazione di base.
- **Supporto del rilevamento dei documenti**: ora gli sviluppatori possono abilitare il rilevamento di documenti quando attivano la protezione dei documenti nelle app 
- Miglioramenti delle prestazioni
- Correzione di bug


### Aggiornamento di dicembre 2015

Con questa versione, è ora disponibile la versione 4.2 SDK RMS per i dispositivi e aggiunge:

-   Rilevamento dei documenti, RMS solo online, per sistemi operativi iOS/OS X e Android.

    Per informazioni dettagliate e linee guida sull'uso relative a iOS/OS X, vedere la classe [**MSLicenseMetadata**](/rights-management/sdk/4.2/api/iOS/mslicensemetadata#msipcthin2_mslicensemetadata_class_objc) che fornisce informazioni di rilevamento e il metodo di registrazione del rilevamento del documento aggiuntivo [**MSUserPolicy**](/rights-management/sdk/4.2/api/iOS/iOS#msipcthin2_msuserpolicy_interface_objc). Esistono aggiunte simili per Android in [**LicenseMetadata**](/rights-management/sdk/4.2/api/android/com.microsoft.rightsmanagement#msipcthin2_licensemetadata_interface_java) e [**UserPolicy**](/rights-management/sdk/4.2/api/android/userpolicy).

    Per una descrizione dettagliata della funzionalità di rilevamento del documento, vedere [**Procedura: rilevamento dei documenti usare**](how-to-use-document-tracking.md).

-   Set di metodi sincroni che le versioni asincrone in parallelo per l'API Android:

    [**Metodo sincrono CustomProtectedInputStream.create**](/rights-management/sdk/4.2/api/android/customprotectedinputstream#msipcthin2_customprotectedinputstream_create_synchronous_method_java)

    [**Metodo sincrono CustomProtectedOutputStream.create**](/rights-management/sdk/4.2/api/android/customprotectedoutputstream#msipcthin2_customprotectedoutputstream_create_synchronous_method)

    [**Metodo sincrono ProtectedFileInputStream.create**](/rights-management/sdk/4.2/api/android/protectedfileinputstream#msipcthin2_protectedfileinputstream_create_synchronous_method)

    [**Metodo sincrono ProtectedFileOutputStream.create**](/rights-management/sdk/4.2/api/android/customprotectedoutputstream#msipcthin2_customprotectedoutputstream_create_synchronous_method)

    [**Metodo sincrono TemplateDescriptor.getTemplates**](/rights-management/sdk/4.2/api/android/templatedescriptor#msipcthin2_templatedescriptor_gettemplates_synchronous_method_java)

    [**Metodo sincrono UserPolicy.acquire**](/rights-management/sdk/4.2/api/android/userpolicy#msipcthin2_userpolicy_acquire_synchronous_method_java)

    [**Metodo sincrono UserPolicy.create (PolicyDescriptor...)**](/rights-management/sdk/4.2/api/android/userpolicy#msipcthin2_userpolicy_create_policydescriptor_______synchronous_method_java)

    [**Metodo sincrono UserPolicy.create (TempalteDescriptor...)**](/rights-management/sdk/4.2/api/android/userpolicy#msipcthin2_userpolicy_create_templatedescriptor_______synchronous_method_java)

-   Aggiunta di una nuova classe [**ProtectedBuffer**](/rights-management/sdk/4.2/api/android/com.microsoft.rightsmanagement#msipcthin2_protectedbuffer_class) all'API di Android.
-   Aggiornamenti per migliorare i messaggi di errore e l'esperienza di risoluzione dei problemi.
-   Miglioramenti significativi delle prestazioni per le operazioni di crittografia.

### Aggiornamento di luglio 2015: aggiunta del supporto per Linux / sviluppo C++

Questa versione aggiunge le funzionalità seguenti:

-   SDK 4.1 RMS per piattaforme Linux

    Per altre informazioni, vedere [Introduzione](get-started.md).

### Aggiornamento di maggio 2015: aggiunta del controllo di registrazione

Questa versione aggiunge il supporto per le funzionalità seguenti:

-   iOS

    La crittografia e decrittografia dell'app può operare in modo indipendente e in parallelo.

    Per altre informazioni, vedere [**MSProtector**](/rights-management/sdk/4.2/api/iOS/iOS#msipcthin2_msprotector_class_objc).

    Impostazioni di controllo a livello log abilitate.

    Per altre informazioni, vedere [Procedura: Abilitare la registrazione delle prestazioni e dell'errore](enabling-logging.md)

    Aggiunta del supporto di cancellazione della cache.

    Per altre informazioni, vedere [**MSProtection:resetStateWithCompletionBlock**](/rights-management/sdk/4.2/api/iOS/msprotection#msipcthin2_msprotection_resetstatewithcompletionblock_method_objc).

### Aggiornamento di febbraio 2015: aggiunta del supporto di applicazioni Windows Store

Questa versione aggiunge il supporto per applicazioni Windows Store e offre la parità funzionale con la versione per Windows Phone, Android e iOS/OS X di SDK 4.1 RMS.

### Aggiornamento di gennaio 2015: aggiunta del supporto della piattaforma WinPhone

Questa versione aggiunge il supporto per il sistema operativo Windows Phone e offre la parità funzionale con la versione per Android e iOS/OS X di SDK 4.1 RMS.

## Aggiornamento di ottobre 2014: l'aggiornamento a SDK 4.1 Microsoft RMS

La versione 4.1 di SDK RMS aggiunge le nuove funzionalità seguenti a Google Android e Apple iOS / OS X.

-   Estensioni dell'API SDK Android e iOS/OS X per l'elaborazione del *consenso dell'utente*, consentendo all'utente di confermare i comportamenti dell'SDK. Attualmente, il rilevamento dei documenti l'accesso a URL di servizio AD RMS sconosciuti sono i tipi di consenso supportati.

    Per altre informazioni, vedere come esempio, la versione dell'API Android dell'[**interfaccia ConsentCallback**](/rights-management/sdk/4.2/api/android/com.microsoft.rightsmanagement#msipcthin2_consentcallback_interface_java).

-   Supporto ora di iOS 8 e OS X 10.10 (Yosemite). Sono state inoltre apportate alcune modifiche al nome di proprietà richieste da Xcode 6.

    Esempio; MSUserPolicy.name modificato in [**MSUserPolicy.policyName**](/rights-management/sdk/4.2/api/iOS/msuserpolicy#msipcthin2_msuserpolicy_name_property_objc).

## Note sulla versione

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

-   Durante l'uso del metodo [**ProtectedFileOutputStream**](/rights-management/sdk/4.2/api/android/protectedfileoutputstream#msipcthin2_protectedfileoutputstream_class_java)**.write(byte\[\] array, int offset, int length)** con una lunghezza diversa dal valore *array.length*, non è possibile usare il contenuto in un secondo momento usando SDK.

    **Soluzione**: questo è un problema noto. Per limitare il problema, passare sempre un array **byte \[\]** con lo stesso valore di lunghezza del parametro di lunghezza oppure usare il metodo [**ProtectedFileOutputStream**](/rights-management/sdk/4.2/api/android/protectedfileoutputstream#msipcthin2_protectedfileoutputstream_class_java)**.write(byte\[\] array)**.

**iOS e OS X**

-   Esistono due varianti regionali di portoghese supportati dai nostri SDK iOS e OS X. Sfortunatamente, a causa di un bug, la prima localizzazione non è attualmente supportata completamente. A causa di questo bug, il portoghese non è supportato completamente. La maggior parte del testo viene tradotta, ma non l'interfaccia utente.

    1. Portoghese

    2. Portoghese (Portogallo)

**solo iOS**

-   RMS SDK 4.x non visualizza l'indicatore di attività di rete.

    Si tratta di un comportamento facoltativo noto per iOS, in base alle linee guida dell'interfaccia umana Apple.

**Solo OS X**

-   RMS SDK 4.x non visualizza l'indicatore di attività di rete.

    Si tratta di un comportamento facoltativo noto per OS X, in base alle linee guida dell'interfaccia umana Apple.

-   **Soluzione**: per creare un'applicazione multiple document interface (MDI) tramite SDK OS X, usare le linee guida seguenti.

    I metodi seguenti non devono essere eseguiti contemporaneamente. Per monitorare per il completamento dell'esecuzione, Usare l'approccio di blocco di completamento, come indicato.

    - [**protectedDataWithProtectedFile**](/rights-management/sdk/4.2/api/iOS/msprotecteddata#msipcthin2_msprotecteddata_protecteddatawithprotectedfile_completionblock_method_objc)
    - [**customProtectedDataWithPolicy**](/rights-management/sdk/4.2/api/iOS/mscustomprotecteddata#msipcthin2_mscustomprotecteddata_customprotecteddatawithpolicy_protecteddata_contentstartposition_contentsize_completionblock_method_objc)



**Nota**: le applicazioni MDI non sono supportate dall'API di iOS.

## Domande frequenti

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

**OS x**

**D**: Il framework dell'app di esempio è stato adattato a Xcode 5, è possibile lavorare con Xcode 4.6?

**R**: L'SDK di OS X funziona con Xcode 4.6 e versioni successive soltanto, nonché con OS X è 10.8 e versioni successive.

 

 



<!--HONumber=Jul16_HO2-->


