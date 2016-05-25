---
# required metadata

title: Ottenere una licenza di produzione | Azure RMS
description: Rilascio di un'applicazione sviluppata con RMS SDK 2.1, necessario un contratto di licenza di produzione.
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 6749817E-FF34-4384-BF63-39AEA5C372CA
# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Ottenere una licenza di produzione

Prima di rilasciare un'applicazione sviluppata con Rights Management Services SDK 2.1, è necessario sottoscrivere un contratto di licenza di produzione per ottenere un certificato di produzione.

> [!IMPORTANT]
> Se l'applicazione client verrà eseguita con RMS basato su Azure, è necessario richiedere un tenant di Azure RMS. Inviare un messaggio di posta elettronica a <rmcstbeta@microsoft.com> con la richiesta del tenant.

Per ulteriori informazioni sull'esecuzione con Azure RMS, vedere [Consentire all'applicazione di servizio di usare RMS basato su cloud](how-to-use-file-api-with-aadrm-cloud.md).


Il certificato di produzione e il certificato di pre-produzione eseguono una funzione simile, ma sono destinati ad ambienti diversi. Entrambi contengono una catena di certificati con un certificato emesso dall'autorità di certificazione Microsoft (CA) alla radice di attendibilità, ma il certificato di preproduzione viene usato solo quando si sviluppa un'applicazione di RMS. Il certificato di produzione viene utilizzato in ambienti successivi al rilascio. Il certificato di produzione e la chiave privata associata vengono usati per creare e firmare un manifesto che identifichi i file che possono o devono essere caricati nello spazio di processo dell'applicazione, oltre a quelli che non devono essere caricati.

Per ulteriori informazioni sulle chiavi, vedere [Test dell'applicazione abilitata all'uso di diritti](running-your-first-application.md).

È possibile ottenere il certificato sottoscrivendo un contratto di licenza di produzione.

## Richiesta di un contratto di licenza di produzione

-   Inviare un messaggio di posta elettronica a [RMLA@microsoft.com](mailto:rmla@microsoft.com) e includere le seguenti informazioni:

    -   Nome completo dell'azienda

    -   Indirizzo fisico dell'azienda (inclusi città, stato, paese o regione e CAP)
    -   Indirizzo postale dell'azienda (inclusi città, stato, paese o regione e CAP)
    -   Numero di telefono e numero di fax dell'azienda
    -   URL dell'azienda
    -   Paese o regione di integrazione
    -   Nome del prodotto o dell'applicazione
    -   Nome e cognome del richiedente
    -   Titolo o posizione del richiedente
    -   Indirizzo di posta elettronica del richiedente

    Anche se un account di posta elettronica non è strettamente necessario, durante il processo di sottoscrizione le comunicazioni vengono inviate tramite posta elettronica. È possibile ottenere un account di posta elettronica in Microsoft Outlook.com. Se non si dispone di un account e non se ne desidera uno, è possibile inviare una sottoscrizione all'indirizzo seguente:

    `Active Directory Rights Management License Agreements (ADRMLA)`

    `Microsoft Corporation`

    `One Microsoft Way`

    `Redmond, WA 98052-6399`

    Per richiedere un contratto, attenersi alla procedura seguente:

    -   Inviare le informazioni in lingua inglese, come dovrebbero apparire nel contratto.
    -   Inviare tutte le informazioni richieste. Informazioni mancanti o incomplete possono ritardare il processo di elaborazione della richiesta.

    Il team di Active Directory Rights Management Licensing Agreement (ADRMLA) risponderà alla richiesta tramite posta elettronica entro tre giorni lavorativi; se la richiesta è stata inviata tramite servizio postale, il tempo di attesa potrebbe prolungarsi. La risposta includerà il modulo per i contratti di licenza e altre istruzioni. Leggere, firmare e restituire tutte le pagine del contratto al team ADRMLA. Non modificare i tipi di carattere o riformattare i paragrafi del contratto di licenza.

    Assicurarsi di seguire le istruzioni ricevute dal team ADRMLA. Le istruzioni elencano le informazioni digitali necessarie per compilare la richiesta di certificato. Seguendo le istruzioni dettagliate si ridurranno i ritardi.

    Dopo averlo creato, il team ADRMLA inoltrerà il certificato di produzione all'utente. Il certificato viene creato in base al contratto di licenza e alle informazioni digitali fornite (tra cui una chiave pubblica). Si noti che potrebbero essere necessari fino a 15 giorni lavorativi perché il team ADRMLA invii il certificato tramite posta elettronica; se la comunicazione viene effettuata tramite servizio postale, il periodo di attesa potrebbe prolungarsi.

## Argomenti correlati

* [Procedura](how-to-use-msipc.md)
* [Test dell'applicazione abilitata all'uso di diritti](running-your-first-application.md)
 

 





<!--HONumber=Apr16_HO4-->


