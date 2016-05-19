---
# required metadata

title: Configurazione del client | Azure RMS
description: Istruzioni su come configurare il client 2.1 Active Directory Rights Management Services.
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 58051d42-5a0a-4b65-9e02-bcdbf17d3262

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
# Configurare il client

Questo argomento contiene le istruzioni su come configurare il client 2.1 Active Directory Rights Management Services.

**Importante**: se si effettuano i test dell'applicazione eseguendola nell'ambiente di ISV RMS con 1 casella, non è necessario configurare il client 2.1 AD RMS. Per altre informazioni, vedere [Test dell'applicazione abilitata all'uso dei diritti](running-your-first-application.md).

 

### Prerequisiti

-   È necessario disporre del client 2.1 AD RMS installato sul computer in cui si effettuerà il test dell'applicazione.

    -   Se si effettuano i test dell'applicazione sul computer di sviluppo deve essere già installato SDK 2.1 Rights Management Services. Il client 2.1 AD RMS dovrebbe essere automaticamente installato in questo momento.

        Per informazioni sull'installazione di SDK 2.1 RMS, vedere [Installare l'SDK](create-your-first-rights-aware-application.md).

    -   Se si effettua il test dell'applicazione su un computer diverso da quello di sviluppo, è possibile installare il client 2.1 AD RMS sul computer dalla [pagina di download del client 2.1 AD RMS Client](http://www.microsoft.com/en-us/download/details.aspx?id=38396).
        **Nota**: se l'applicazione usa la modalità dell'API del Server (**IPC\_API\_MODE\_SERVER**), non è necessario usare un manifesto dell'applicazione. È possibile eseguire il test dell'applicazione in un server RMS di produzione e non è necessario ottenere una licenza di produzione quando si passa all'ambiente di produzione. Per altre informazioni sulle applicazioni in modalità server, vedere [Tipi di applicazioni](application-types.md).

         

-   È necessario disporre di un server RMS installato e configurato per l'uso nell'ambiente di pre-produzione. Per altre informazioni, vedere [Installare e configurare il server](how-to-install-and-configure-an-rms-server.md).

Istruzioni

### Passaggio 1: Modalità di configurazione del client 2.1 RMS per la gerarchia dei certificati di pre-produzione

I passaggi seguenti viene descritto le modalità di installazione della runtime per sviluppatori, di configurazione del client per usare la gerarchia del certificato ISV (pre-produzione) e di configurazione dell'individuazione del servizio nel client.

1.  Copiare il runtime per sviluppatori, Ipcsecproc\_isv.dll, da %MSIPCSDKDIR%\\bin\\x86 (per le versioni a 32 bit di Windows) o %MSIPCSDKDIR\\bin\\x64 (per le versioni a 64 bit di Windows) su C:\\Programmi\\Active Directory Rights Management Services Client 2.1.

    **Importante**: se si esegue un'applicazione a 32 bit su una versione a 64 bit di Windows, è necessario copiare Ipcsecproc\_isv.dll from %MSIPCSDKDIR%\\bin\\x86 su C:\\Programmi(x86)\\Active Directory Rights Management Services Client 2.1.

     

2.  Configurare il client 2.1 AD RMS per usare la gerarchia di certificati (pre-produzione) ISV impostando il valore della chiave della **gerarchia** su 1.

    ```
    HKEY_LOCAL_MACHINE
       SOFTWARE
          Microsoft
             MSIPC
                Hierarchy DWORD = 00000001
                Data type
                DWORD
    ```

    **Nota**: senza il valore della **gerarchia** nel Registro è funzionalmente equivalente al valore impostato su 0 (zero), vale a dire che SDK 2.1 RMS funzionerà in modalità di produzione. Per altre informazioni sulle catene di chiavi e certificati, vedere [Informazioni sulle catene di certificati](understanding-certificate-chains.md).

    **Importante**  
    Se si esegue un'applicazione a 32 bit su una versione a 64 bit di Windows è necessario impostare il valore della **gerarchia** nel percorso della chiave seguente:

    ```
    HKEY_LOCAL_MACHINE
        SOFTWARE
           Wow6432Node
              Microsoft
                MSIPC
    ```
     

3.  Configurare l'individuazione sul lato server o sul lato client per abilitare il client 2.1 AD RMS per individuare e stabilire la comunicazione con il server RMS pre-produzione.

    -   Nell'individuazione del server, un amministratore registra un service connection point (SCP) per il cluster radice RMS di pre-produzione con Active Directory e il client esegue una query ad Active Directory per individuare SCP e stabilire una connessione con il server.
    -   Nell'individuazione del client, configurare le impostazioni di individuazione del servizio RMS nel Registro sul computer su cui è in esecuzione il client 2.1 AD RMS. Queste impostazioni, puntano il client 2.1 AD RMS al server RMS da usare. Quando sono presenti, l'individuazione non viene eseguita sul lato server.

    Per configurare l'individuazione sul lato client, è possibile impostare le seguenti chiavi del registro, in modo che punti al server RMS pre-produzione. Per informazioni su come configurare l'individuazione sul lato assistenza, vedere [Note sulla distribuzione del client 2.0 RMS](https://TechNet.Microsoft.Com/en-us/library/jj159267(WS.10).aspx).

|Chiave|Valore|
|---|-----|
|`HKEY_LOCAL_MACHINE\`<br>`SOFTWARE\`<br>`Microsoft\`<br>`MSIPC\`<br>`ServiceLocation\`<br>`EnterpriseCertification`|(valore predefinito):<br><br> [**http**&#124;**https**]**://** *RMSClusterName* **/_wmcs/Certification**|
|`HKEY_LOCAL_MACHINE\`<br>`SOFTWARE\`<br>`Microsoft\`<br>`MSIPC\`<br>`ServiceLocation\`<br>`EnterprisePublishing`|(valore predefinito):<br><br> [**http**&#124;**https**]**://** *RMSClusterName* **/_wmcs/Licensing**|


**Nota**: per impostazione predefinita, queste chiavi non sono presenti nel registro e devono essere create.
     
**Importante**  
    Se si esegue un'applicazione a 32 bit su una versione a 64 bit di Windows, è necessario impostare queste chiavi nel percorso della chiave seguente:


    HKEY_LOCAL_MACHINE
        SOFTWARE
           Wow6432Node
              Microsoft
                MSIPC
    

### Osservazioni

Le linee guida fornite in questo argomento non sono complete. Per informazioni dettagliate su come configurare AD RMS Client 2.1, vedere [Note sulla distribuzione di RMS Client 2.0](https://TechNet.Microsoft.Com/en-us/library/jj159267(WS.10).aspx).

### Argomenti correlati


* [Procedura](how-to-use-msipc.md)
* [Note sulla distribuzione del Client RMS 2.0](https://TechNet.Microsoft.Com/en-us/library/jj159267(WS.10).aspx)
* [Installare l'SDK](create-your-first-rights-aware-application.md)
* [Installare e configurare il server](how-to-install-and-configure-an-rms-server.md)
* [Test delle applicazioni abilitate all'uso di diritti](running-your-first-application.md)
* [Informazioni sulle catene di certificati](understanding-certificate-chains.md)
 

 


<!--HONumber=Apr16_HO3-->


