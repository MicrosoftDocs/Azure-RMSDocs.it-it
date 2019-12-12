---
title: Distribuzione dell'applicazione - AIP
description: Questo argomento illustra il processo di distribuzione dell'applicazione
keywords: distribuire, RMS, Azure Information Protection
author: msmbaldwin
ms.author: mbaldwin
manager: barbkess
ms.date: 03/13/2017
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 4B785564-6839-49ED-A243-E2A6DFF88B2E
audience: developer
ms.reviewer: kartikk
ms.suite: ems
ms.custom: dev
ms.openlocfilehash: 2c8b3407f31819614605fb77fb86a86159a898fd
ms.sourcegitcommit: 474cd033de025bab280cb7a9721ac7ffc2d60b55
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/05/2019
ms.locfileid: "68788533"
---
# <a name="deploy-into-production"></a>Distribuire in ambiente di produzione

Questo argomento illustra il processo di distribuzione dell'applicazione abilitata per Azure Information Protection (AIP)/Rights Management Services (RMS).

## <a name="request-an-information-protection-integration-agreement-ipia"></a>Richiedere un contratto per l'integrazione di Information Protection (IPIA, Information Protection Integration Agreement)
Prima di poter rilasciare un'applicazione sviluppata con Azure Information Protection/RMS, è necessario richiedere e concludere un contratto formale con Microsoft.

### <a name="begin-the-process"></a>Avviare il processo
Per ottenere il contratto, inviare un messaggio di posta elettronica all'indirizzo <strong>IPIA@microsoft.com</strong> con le informazioni seguenti:

**Oggetto:** Requesting IPIA for *nome azienda*

Nel corpo del messaggio di posta elettronica includere:
- Nome dell'applicazione e del prodotto
- Nome e cognome del richiedente
- Indirizzo di posta elettronica del richiedente

### <a name="next-steps"></a>Passaggi successivi
In seguito alla ricezione della richiesta del contratto, Microsoft invierà un modulo in forma di documento di Word.
Leggere i termini e le condizioni del contratto di integrazione di Information Protection e restituire il modulo all'indirizzo <strong>IPIA@microsoft.com</strong> con le informazioni seguenti:
- Ragione sociale dell'azienda
- Stato/provincia (Stati Uniti o Canada) o paese di costituzione
- URL dell'azienda
- Indirizzo di posta elettronica del contatto
- Ulteriori indirizzi dell'azienda (facoltativo)
- Nome dell'applicazione dell'azienda
- Breve descrizione dell'applicazione
- *ID tenant di Azure*
- *ID app* per l'applicazione
- Contatti, indirizzo di posta elettronica e numero di telefono dell'azienda per la corrispondenza relativa a situazioni critiche

### <a name="completing-the-agreement"></a>Conclusione del contratto
Al ricevimento del modulo, Microsoft invierà il collegamento al contratto di integrazione di Information Protection finale per la firma digitale. Dopo la firma da parte dell'azienda il contratto verrà sottoscritto anche dal rappresentante Microsoft appropriato e sarà così concluso.

### <a name="already-have-a-signed-ipia"></a>È già stato sottoscritto un contratto di integrazione di Information Protection?
Se è già stato sottoscritto un contratto di integrazione di Information Protection e si vuole aggiungere un nuovo *ID app* per un'applicazione da rilasciare, inviare un messaggio di posta elettronica all'indirizzo <strong>IPIA@microsoft.com</strong> e fornire le informazioni seguenti:
- Nome dell'applicazione dell'azienda
- Breve descrizione dell'applicazione
- ID tenant di Azure (anche se è uguale)
- ID app per l'applicazione
- Contatti, indirizzo di posta elettronica e numero di telefono dell'azienda per la corrispondenza relativa a situazioni critiche

Dopo aver inviato il messaggio di posta elettronica, si riceverà conferma della ricezione entro 72 ore.

## <a name="deploying-to-the-client-environment"></a>Distribuzione nell'ambiente client

Per distribuire l'applicazione sviluppata con gli strumenti di Azure Information Protection (AIP)/Rights Management Services (RMS), sarà necessario distribuire RMS Client 2.1 nel computer dell'utente finale.

### <a name="rmsclient21"></a>RMS Client 2.1
RMS Client 2.1 è progettato per proteggere l'accesso e l'utilizzo delle informazioni scambiate tra applicazioni abilitate per Azure Information Protection/RMS, sia in locale che in un data center Microsoft.

RMS Client 2.1 non è un componente del sistema operativo Windows. Il client viene fornito come download facoltativo che può essere liberamente distribuito con l'applicazione, in seguito alla presa in visione e accettazione del relativo contratto di licenza.

> [!IMPORTANT]
> RMS Client 2.1 è specifico dell'architettura e deve corrispondere all'architettura del sistema operativo di destinazione.


## <a name="rmsclient21-installation-options"></a>Opzioni di installazione di RMS Client 2.1

### <a name="creating-your-deployment-package"></a>Creazione del pacchetto di distribuzione

È consigliabile includere il pacchetto di installazione di RMS Client e l'applicazione o soluzione in un bundle usando la tecnologia di installazione desiderata. RMS Client può essere liberamente ridistribuito con altre applicazioni e soluzioni.

È possibile scegliere di installare RMS Client 2.1 in modo interattivo avviando il relativo programma di installazione oppure di installarlo in modo invisibile all'utente. I passaggi per l'integrazione sono riportati di seguito:

-   Scaricare il programma di installazione del client 2.1 di RMS
-   Integrare il programma di installazione di RMS Client 2.1 per l'esecuzione con il programma di installazione dell'applicazione

Un esempio di integrazione di RMS Client 2.1 con l'applicazione è il pacchetto [Rights Protected Folder Explorer](https://technet.microsoft.com/library/rights-protected-folder-explorer(v=ws.10).aspx). Provare a installarlo autonomamente per comprendere l'approccio.

### <a name="make-rmsclient21-a-pre-requisite-for-your-application-install"></a>Rendere RMS Client 2.1 un prerequisito per l'installazione dell'applicazione

In questo caso, si creerà un prerequisito tale che l'installazione dell'applicazione avrà esito negativo se RMS Client 2.1 non è presente nel computer dell'utente finale.

Se il client non è presente, trasmettere un messaggio di errore che indica dove è possibile scaricare una copia di RMS Client 2.1.

Se il client è presente, procedere con l'installazione dell'applicazione.

## <a name="enabling-azure-information-protection-services-with-your-application"></a>Abilitazione dei servizi Azure Information Protection con l'applicazione

> [!NOTE]
> Se è stata eseguita la migrazione al nuovo modello di ADAL per l'autenticazione, non è necessario installare l'**Assistente per l'accesso ai Microsoft Online Services**. Per ulteriori informazioni, vedere [ADAL authentication for your RMS enabled application](adal-auth.md) (Autenticazione ADAL per l'applicazione abilitata per RMS).
> Inoltre, è possibile **certificare l'applicazione per Windows 10**. Eseguendo l'aggiornamento dell'applicazione per l'uso dell'autenticazione ADAL anziché dell'Assistente per l'accesso a Microsoft Online, l'utente e i clienti potranno: Installare RMS Client 2.1 senza necessità di privilegi amministrativi sul computer

Affinché l'utente finale possa sfruttare i vantaggi dei servizi Information Protection, è necessario distribuire l'*Assistente per l'accesso ai Microsoft Online Services*. Lo sviluppatore dell'applicazione non sa se l'utente finale userà Information Protection tramite RMS (in locale) o tramite Azure Information Protection.


> [!IMPORTANT]
> Se l'applicazione client verrà eseguita con RMS basato su Azure, sarà necessario creare i propri tenant. Per altre informazioni vedere [Azure RMS requirements: Cloud subscriptions that support Azure RMS](../requirements.md) (Requisiti per Azure RMS: sottoscrizioni cloud che supportano Azure RMS).
> Per ulteriori informazioni sull'esecuzione con Azure RMS, vedere [Consentire all'applicazione di servizio di usare RMS basato su cloud](how-to-use-file-api-with-aadrm-cloud.md).

-   Scaricare l'[Assistente per l'accesso ai Microsoft Online Services](https://www.microsoft.com/download/details.aspx?id=28177) dall'Area download Microsoft.
-   Assicurarsi che la distribuzione di un'applicazione abilitata all'uso di diritti includa una verifica dei prerequisiti per la selezione di questo servizio.
-   Per eseguire i test e per l'uso dei servizi online da parte degli utenti finali, vedere l'argomento di TechNet [Configurazione di Rights Management](https://TechNet.Microsoft.Com/library/jj585002.aspx).

È inoltre necessario usare questa guida per configurare l'app: [Come configurare un'applicazione del servizio app per usare l'account di accesso di Azure Active Directory](https://docs.microsoft.com/azure/app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication).

Per ulteriori informazioni sull'abilitazione dell'applicazione per l'uso di RMS per i servizi di Azure Rights Management, vedere [Consentire all'applicazione di usare RMS basato su cloud](how-to-use-file-api-with-aadrm-cloud.md).

## <a name="related-topics"></a>Argomenti correlati

* [Assistente per l'accesso a Microsoft Online Services](https://www.microsoft.com/download/details.aspx?id=28177)
* [Configurazione di Rights Management](https://TechNet.Microsoft.Com/library/jj585002.aspx)
* [Consentire all'applicazione di usare RMS basato su cloud](how-to-use-file-api-with-aadrm-cloud.md)

