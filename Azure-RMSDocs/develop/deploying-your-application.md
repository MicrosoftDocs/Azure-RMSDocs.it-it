---
# required metadata

title: Distribuzione dell'applicazione | Azure RMS
description: Questo argomento descrive le opzioni di distribuzione per l'applicazione abilitata all'uso di diritti
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 4B785564-6839-49ED-A243-E2A6DFF88B2E
# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---
** Il contenuto di questo SDK non è aggiornato. Per un breve periodo, la [versione attuale](https://msdn.microsoft.com/library/windows/desktop/hh535290(v=vs.85).aspx) della documentazione sarà disponibile su MSDN. **
# Distribuzione dell'applicazione


Questo argomento descrive le opzioni di distribuzione per l'applicazione abilitata all'uso di diritti.

> [!IMPORTANT]
> È consigliabile prima di tutto testare l'applicazione Rights Management Services SDK 2.1 con l'ambiente di pre-produzione RMS in un server RMS. Quindi, se si vuole consentire al cliente di usare l'applicazione con il servizio Azure RMS, eseguire il test in tale ambiente. Per ulteriori informazioni, vedere [Consentire all'applicazione di servizio di usare RMS basato su cloud](how-to-use-file-api-with-aadrm-cloud.md).

 

## Opzioni di installazione per il client 2.1 di Active Directory Rights Management Services

Dopo aver creato il file manifesto usando un certificato di produzione, l'applicazione è pronta per essere distribuita. Poiché è stato utilizzato RMS SDK 2.1, è necessario distribuire il client 2.1 di Active Directory Rights Management Service su un computer gestito dall'utente.

### Client 2.1 di AD RMS

Il client 2.1 di AD RMS è un software per computer client progettato per proteggere l'accesso e l'utilizzo di informazioni tra applicazioni che usano RMS, in locale o in un data center Microsoft.

Il client 2.1 di AD RMS non è un componente del sistema operativo Windows. Il client 2.1 di AD RMS è disponibile come download facoltativo che, previa lettura e accettazione del relativo contratto di licenza, può essere distribuito liberamente con un software di terze parti per consentire l'accesso client a contenuti protetti da diritti mediante l'uso e la distribuzione di server RMS nell'ambiente in uso.

> [!IMPORTANT] Il client 2.1 di AD RMS è specifico dell'architettura e deve corrispondere all'architettura del sistema operativo di destinazione.


## Opzioni di installazione del client 2.1 di AD RMS

-   **Ridistribuzione del client 2.1 di AD RMS**

    L'approccio consigliato consiste nell'aggregare il pacchetto di installazione client di RMS con un'applicazione o soluzione usando la tecnologia di installazione desiderata. Il client RMS può essere ridistribuito gratuitamente e in bundle con altre applicazioni e soluzioni IT.

    È possibile scegliere di installare il client 2.1 di AD RMS in modo interattivo avviando il relativo programma di installazione, oppure di installarlo automaticamente. I passaggi per l'integrazione sono riportati di seguito:

    -   Scaricare il programma di installazione del client 2.1 di RMS
    -   Integrare il programma di installazione del client 2.1 di AD RMS con il programma di installazione dell'applicazione

    Due ottimi esempi di integrazione del client 2.1 di AD RMS con l'applicazione sono il pacchetto del programma di installazione RMS SDK 2.1 e il pacchetto Esplora cartella protetta da diritti. Provare a eseguirne l'installazione per comprendere l'approccio.

-   **Rendere il client 2.1 di AD RMS un prerequisito per l'installazione dell'applicazione**

    In questo caso, si creerà un prerequisito tale che l'installazione dell'applicazione avrà esito negativo se il client 2.1 di AD RMS non è presente nel computer dell'utente finale.

    Se il client non è presente, fornire un messaggio di errore che indica dove è possibile scaricare una copia del client 2.1 di AD RMS.

    Se il client è presente, procedere con l'installazione dell'applicazione.

## Abilitazione di Azure Rights Management Services con l'applicazione

> [!NOTE]
> Se è stata eseguita la migrazione al nuovo modello di ADAL per l'autenticazione, non è necessario installare SIA. Per ulteriori informazioni, vedere l'autenticazione ADAL per l'applicazione abilitata per RMS.

- **Certificazione dell'applicazione per Windows 10**: aggiornando l'applicazione per usare l'autenticazione ADAL piuttosto che l'Assistente per l'accesso a Microsoft Online, l'utente e i suoi clienti saranno in grado di:
  - Usare Multi-Factor Authentication
  - Installare il client RMS 2.1 senza necessità di privilegi amministrativi sul computer
 
  Affinché l'utente finale possa sfruttare i vantaggi dei servizi di Azure Rights Management, è necessario distribuire l'*Assistente per l'accesso a Microsoft Online Services*. Lo sviluppatore dell'applicazione non è a conoscenza se l'utente finale userà RMS (locale) o i servizi di Azure Rights Management (servizio cloud).

> [!IMPORTANT]
> Per eseguire l'applicazione del client 2.1 di RMS SDK con Azure RMS è necessario richiedere un tenant di Azure RMS. Inviare un messaggio di posta elettronica a <rmcstbeta@microsoft.com> con la richiesta del tenant.

-   Scaricare l'[Assistente per l'accesso ai Microsoft Online Services](http://www.microsoft.com/en-us/download/details.aspx?id=28177) dall'Area download Microsoft.
-   Assicurarsi che la distribuzione di un'applicazione abilitata all'uso di diritti includa una verifica dei prerequisiti per la selezione di questo servizio.
-   Per eseguire i test e per l'uso dei servizi online da parte degli utenti finali, vedere l'argomento di TechNet [Configurazione di Rights Management](https://TechNet.Microsoft.Com/en-us/library/jj585002.aspx).

Per ulteriori informazioni sull'abilitazione dell'applicazione per l'uso di RMS per i servizi di Azure Rights Management, vedere [Consentire all'applicazione di usare RMS basato su cloud](how-to-use-file-api-with-aadrm-cloud.md).

## Argomenti correlati

* [Procedura](how-to-use-msipc.md)
* [Assistente per l'accesso a Microsoft Online Services](http://www.microsoft.com/en-us/download/details.aspx?id=28177)
* [Configurazione di Rights Management](https://TechNet.Microsoft.Com/en-us/library/jj585002.aspx)
* [Consentire all'applicazione di usare RMS basato su cloud](how-to-use-file-api-with-aadrm-cloud.md)
 

 





<!--HONumber=Jun16_HO1-->


