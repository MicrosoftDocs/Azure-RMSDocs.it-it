---
# required metadata

title: Test dell'applicazione abilitata all'uso di diritti | Azure RMS
description: Descrive la procedura per completare il test dell'applicazione abilitata all'uso di diritti per SDK RMS 2.1.
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 43b611a8-2cc0-49a8-9db9-e81321c38f7a

# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

﻿
# Test dell'applicazione abilitata all'uso di diritti

Questo argomento descrive la procedura per portare a termine il test dell'applicazione abilitata all'uso di diritti per SDK Rights Management Services 2.1.

Per pubblicare e usare contenuto protetto, un'applicazione Rights Management Services (RMS) si serve di diversi tipi di certificati e licenze, ciascuno dei quali è costituito da una catena di certificati che conduce alla fine a un'autorità di certificazione Microsoft. Microsoft fornisce le seguenti gerarchie:

-   La gerarchia di pre-produzione può essere usata per sviluppare e testare applicazioni.
-   La gerarchia di produzione deve essere usata da applicazioni rilasciate

Quando si sviluppa un'applicazione è consigliabile usare la gerarchia di pre-produzione. In questo modo, è possibile lavorare senza firmare un contratto di licenza di produzione con Microsoft.

> [!IMPORTANT]
> È consigliabile prima di tutto testare l'applicazione SDK RMS 2.1 con l'ambiente di pre-produzione RMS in un server RMS. Quindi, per consentire al cliente di usare l'applicazione con il servizio Azure RMS, eseguire il test in tale ambiente. Per altre informazioni, vedere [Consentire all'applicazione di servizio di usare RMS basato su cloud](how-to-use-file-api-with-aadrm-cloud.md).

 

### Prerequisiti

-   Configurazione dell'ambiente di sviluppo di SDK RMS 2.1. Per altre informazioni, vedere [Impostazione dell'ambiente di sviluppo pre-produzione](how-to-set-up-the-pre-production-development-environment.md).
-   Per un esempio di applicazione, vedere [IPCHelloWorld - Applicazione di esempio](how-to-build-your-first-application.md).

Istruzioni

### Passaggio 1:

Creare e compilare un'applicazione abilitata all'uso dei diritti. Per le opzioni, vedere la sezione Prerequisiti riportata in precedenza.

### Passaggio 2: Generare un manifesto dell'applicazione mediante la catena di certificati di pre-produzione

È necessario generare un manifesto dell'applicazione prima di eseguirla.

**Nota**: se l’applicazione usa la modalità dell’API del Server (**IPC\_API\_MODE\_SERVER**), non è necessario usare un manifesto dell’applicazione. È possibile testare l'applicazione rispetto a un server AD RMS di produzione e non è necessario ottenere una licenza di produzione quando si passa all'ambiente di produzione. Per altre informazioni sulle applicazioni in modalità server, vedere [Tipi di applicazioni](application-types.md).

 

Questo processo è noto anche come firma dell'applicazione. È possibile generare il manifesto usando una catena di certificati di produzione o la catena di certificati di pre-produzione che viene installata con l' SDK. È consigliabile usare la catena di certificati di pre-produzione durante lo sviluppo.

Per altre informazioni sulle catene di chiavi e certificati, vedere [Informazioni sulle catene di certificati](understanding-certificate-chains.md).

Per informazioni su come firmare un'applicazione con una catena di certificati di produzione, vedere [Passaggio all'ambiente di produzione](switching-to-the-production-environment.md).

Per generare un manifesto dell'applicazione mediante la catena di certificati di pre-produzione, eseguire questi passaggi nel computer di sviluppo:

1.  Copiare i file seguenti dalle directory di installazione nella stessa cartella dell'applicazione.

    %MSIPCSdkDir%\\Tools\\Genmanifest.exe

    %MSIPCSdkDir%\\bin\\Isvtier5appsigningprivkey.dat

    %MSIPCSdkDir%\\bin\\Isvtier5appsigningpubkey.dat

    %MSIPCSdkDir%\\bin\\Isvtier5appsignsdk\_client.xml

    %MSIPCSdkDir%\\bin\\YourAppName.isv.mcf

2.  Nella cartella dell'applicazione, rinominare il file di configurazione del manifesto, YourAppName.isv.mcf, con il nome dell'applicazione aggiungendo l'estensione del nome file .mcf. Ad esempio se l'applicazione è denominata MyApp.exe, rinominarla YourAppName.isv.mcf MyApp.exe.mcf.

3.  Usare un editor di testo per aggiungere l'applicazione al file di configurazione del manifesto. A tale scopo, sostituire il testo del segnaposto &lt;YourAppName&gt;.exe nell'elenco dei moduli all'interno del file .mcf con il nome dell'applicazione. ad esempio, MyApp.exe.

    Il processo di firma genererà un errore se il file .mcf viene usato senza alcuna modifica.

4.  Eseguire Genmanifest.exe per generare il manifesto dell'applicazione. Questo è noto anche come firma dell'applicazione. L'output di questa operazione deve essere un file .man. Ad esempio, se l'applicazione è denominata MyApp.exe e il file di configurazione del manifesto è denominato MyApp.exe.mcf, eseguire il comando seguente:

    **genmanifest.exe -chain isvtier5appsignsdk\_client.xml MyApp.exe.mcf MyApp.exe.man**

### Passaggio 3: Eseguire l'applicazione

È possibile eseguire l'applicazione da qualsiasi directory, ma il manifesto dell'applicazione (MyApp.exe.man) deve essere nella stessa directory del file eseguibile (MyApp.exe).

-   **Uso dell'ambiente RMS a una casella**

    Se si usa l'ambiente RMS a una casella per testare l'applicazione, copiare il file eseguibile dell'applicazione e il manifesto dell'applicazione in qualsiasi directory nell'ambiente a una casella ed eseguire l'applicazione.

    Per informazioni sull'ambiente RMS a una casella, vedere [Configurare l'ambiente di test](how-to-set-up-your-test-environment.md).

-   **Uso di una configurazione del Server di pre-produzione**

    Se si sta testando l'applicazione rispetto a un server RMS configurato per la pre-produzione, assicurarsi di aver configurato Active Directory Rights Management Services Client 2.1 sul computer su cui l'applicazione sarà eseguita; ad esempio, nel computer di sviluppo. Assicurarsi che sia l'eseguibile dell'applicazione che il manifesto dell'applicazione si trovino nella stessa directory del computer, quindi eseguire l'applicazione.

    Per informazioni su come configurare il client nel computer in uso, vedere [Configurare il client](how-to-configure-the-ad-rms-client-2-0.md). Per informazioni sull'installazione di un server RMS, vedere [Installare e configurare il server](how-to-install-and-configure-an-rms-server.md).

### Argomenti correlati

* [Procedura](how-to-use-msipc.md)
* [Configurare il client](how-to-configure-the-ad-rms-client-2-0.md)
* [Installare e configurare il server](how-to-install-and-configure-an-rms-server.md)
* [IPCHelloWorld - Applicazione di esempio](how-to-build-your-first-application.md)
* [Impostazione dell'ambiente di sviluppo di pre-produzione](how-to-set-up-the-pre-production-development-environment.md)
* [Passaggio all'ambiente di produzione](switching-to-the-production-environment.md)
* [Configurare l'ambiente di test](how-to-set-up-your-test-environment.md)
* [Informazioni sulle catene di certificati](understanding-certificate-chains.md)
 

 





<!--HONumber=Apr16_HO3-->


