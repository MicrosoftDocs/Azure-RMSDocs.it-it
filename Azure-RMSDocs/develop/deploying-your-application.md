---
title: Distribuzione dell'applicazione | Azure RMS
description: Questo argomento descrive le opzioni di distribuzione per l'applicazione abilitata all'uso di diritti
keywords: 
author: bruceperlerms
manager: mbaldwin
ms.date: 09/25/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 4B785564-6839-49ED-A243-E2A6DFF88B2E
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 44e90a1de74d62469bd8a99a2d49d1e57d2d0f62
ms.openlocfilehash: e1bc56fc108101d0af833a84ba52821c8b18736d


---

# Distribuire in ambiente di produzione


Questo argomento descrive le opzioni di distribuzione per l'applicazione abilitata all'uso di diritti.

## Richiesta di un contratto di licenza di produzione

 Prima di rilasciare un'applicazione sviluppata con Rights Management Services SDK 2.1, è necessario sottoscrivere un contratto di licenza di produzione per ottenere un certificato di produzione.

È possibile ottenere il certificato sottoscrivendo un contratto di licenza di produzione.

Inviare un messaggio di posta elettronica a [RMLA@microsoft.com](mailto:rmla@microsoft.com) e includere le seguenti informazioni:

- Nome completo dell'azienda
- Indirizzo fisico dell'azienda (inclusi città, stato, paese o regione e CAP)
- Indirizzo postale dell'azienda (inclusi città, stato, paese o regione e CAP)
- Numero di telefono e numero di fax dell'azienda
- URL dell'azienda
- Paese o regione di integrazione
- Nome del prodotto o dell'applicazione
- Nome e cognome del richiedente
- Titolo o posizione del richiedente
- Indirizzo di posta elettronica del richiedente

Anche se un account di posta elettronica non è strettamente necessario, durante il processo di sottoscrizione le comunicazioni vengono inviate tramite posta elettronica. È possibile ottenere un account di posta elettronica in Microsoft Outlook.com. Se non si dispone di un account e non se ne desidera uno, è possibile inviare una sottoscrizione all'indirizzo seguente:

      Active Directory Rights Management License Agreements (ADRMLA)

      Microsoft Corporation

      One Microsoft Way

      Redmond, WA 98052-6399

Per richiedere un contratto, attenersi alla procedura seguente:
- Inviare le informazioni in lingua inglese, come dovrebbero apparire nel contratto.
- Inviare tutte le informazioni richieste. Informazioni mancanti o incomplete possono ritardare il processo di elaborazione della richiesta.

Il team di Active Directory Rights Management Licensing Agreement (ADRMLA) risponderà alla richiesta tramite posta elettronica entro tre giorni lavorativi; se la richiesta è stata inviata tramite servizio postale, il tempo di attesa potrebbe prolungarsi. La risposta includerà il modulo per i contratti di licenza e altre istruzioni. Leggere, firmare e restituire tutte le pagine del contratto al team ADRMLA. Non modificare i tipi di carattere o riformattare i paragrafi del contratto di licenza.

Assicurarsi di seguire le istruzioni ricevute dal team ADRMLA. Le istruzioni elencano le informazioni digitali necessarie per compilare la richiesta di certificato. Seguendo le istruzioni dettagliate si ridurranno i ritardi.


## Opzioni di installazione e requisiti per Rights Management Service Client 2.1

Poiché è stato utilizzato RMS SDK 2.1, è necessario distribuire il client 2.1 di Active Directory Rights Management Service su un computer gestito dall'utente.

### RMS Client 2.1

RMS Client 2.1 è un software per computer client progettato per proteggere l'accesso e l'utilizzo di informazioni tra applicazioni che usano RMS, in locale o in un data center Microsoft.

RMS Client 2.1 non è un componente del sistema operativo Windows. RMS Client 2.1 è disponibile come download facoltativo che, previa lettura e accettazione del relativo contratto di licenza, può essere distribuito liberamente con un software di terze parti per consentire l'accesso client a contenuti protetti da diritti mediante l'uso e la distribuzione di server RMS nell'ambiente in uso.


> [!IMPORTANT]
> Il client 2.1 di AD RMS è specifico dell'architettura e deve corrispondere all'architettura del sistema operativo di destinazione.


## Opzioni di installazione di RMS Client 2.1

-   **Ridistribuzione di RMS Client 2.1**

    L'approccio consigliato consiste nell'aggregare il pacchetto di installazione client di RMS con un'applicazione o soluzione usando la tecnologia di installazione desiderata. Il client RMS può essere ridistribuito gratuitamente e in bundle con altre applicazioni e soluzioni IT.

    È possibile scegliere di installare RMS Client 2.1 in modo interattivo avviando il relativo programma di installazione, oppure di installarlo automaticamente. I passaggi per l'integrazione sono riportati di seguito:

    -   Scaricare il programma di installazione del client 2.1 di RMS
    -   Integrare il programma di installazione di RMS Client 2.1 con il programma di installazione dell'applicazione

    Due ottimi esempi di integrazione di RMS Client 2.1 con l'applicazione sono il pacchetto del programma di installazione RMS SDK 2.1 e il pacchetto Esplora cartella protetta da diritti. Provare a eseguirne l'installazione per comprendere l'approccio.

-   **Rendere RMS Client 2.1 un prerequisito per l'installazione dell'applicazione**

    In questo caso, si creerà un prerequisito tale che l'installazione dell'applicazione avrà esito negativo se RMS Client 2.1 non è presente nel computer dell'utente finale.

    Se il client non è presente, trasmettere un messaggio di errore che indica dove è possibile scaricare una copia di RMS Client 2.1.

    Se il client è presente, procedere con l'installazione dell'applicazione.

## Abilitazione di Azure Rights Management Services con l'applicazione

> [!NOTE]
> Se è stata eseguita la migrazione al nuovo modello di ADAL per l'autenticazione, non è necessario installare SIA. Per ulteriori informazioni, vedere [ADAL authentication for your RMS enabled application](adal-auth.md) (Autenticazione ADAL per l'applicazione abilitata per RMS).
> Inoltre, è possibile **certificare l'applicazione per Windows 10**. Eseguendo l'aggiornamento dell'applicazione per l'uso dell'autenticazione ADAL anziché dell'Assistente per l'accesso a Microsoft Online, l'utente e i clienti potranno: Installare RMS Client 2.1 senza necessità di privilegi amministrativi sul computer


Affinché l'utente finale possa sfruttare i vantaggi dei servizi di Azure Rights Management, è necessario distribuire l'*Assistente per l'accesso a Microsoft Online Services*. Lo sviluppatore dell'applicazione non è a conoscenza se l'utente finale userà RMS (locale) o i servizi di Azure Rights Management (servizio cloud).


> [!IMPORTANT]
> Se l'applicazione client verrà eseguita con RMS basato su Azure, sarà necessario creare i propri tenant. Per altre informazioni vedere [Azure RMS requirements: Cloud subscriptions that support Azure RMS](../get-started/requirements-subscriptions.md) (Requisiti per Azure RMS: sottoscrizioni cloud che supportano Azure RMS).
> Per ulteriori informazioni sull'esecuzione con Azure RMS, vedere [Consentire all'applicazione di servizio di usare RMS basato su cloud](how-to-use-file-api-with-aadrm-cloud.md).

-   Scaricare l'[Assistente per l'accesso ai Microsoft Online Services](http://www.microsoft.com/en-us/download/details.aspx?id=28177) dall'Area download Microsoft.
-   Assicurarsi che la distribuzione di un'applicazione abilitata all'uso di diritti includa una verifica dei prerequisiti per la selezione di questo servizio.
-   Per eseguire i test e per l'uso dei servizi online da parte degli utenti finali, vedere l'argomento di TechNet [Configurazione di Rights Management](https://TechNet.Microsoft.Com/en-us/library/jj585002.aspx).

Per ulteriori informazioni sull'abilitazione dell'applicazione per l'uso di RMS per i servizi di Azure Rights Management, vedere [Consentire all'applicazione di usare RMS basato su cloud](how-to-use-file-api-with-aadrm-cloud.md).

## Argomenti correlati

* [Assistente per l'accesso a Microsoft Online Services](http://www.microsoft.com/en-us/download/details.aspx?id=28177)
* [Configurazione di Rights Management](https://TechNet.Microsoft.Com/en-us/library/jj585002.aspx)
* [Consentire all'applicazione di usare RMS basato su cloud](how-to-use-file-api-with-aadrm-cloud.md)
 

 



<!--HONumber=Oct16_HO1-->


