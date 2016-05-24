---
# required metadata

title: Firma dell'applicazione per la produzione | Azure RMS
description: Questo argomento descrive il processo di firma dell'applicazione per la modalità di produzione.
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 09BA148C-7D1E-43C8-92EA-24BBB6EFDB19
# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Firma dell'applicazione per la produzione

Questo argomento descrive il processo di firma dell'applicazione per la modalità di produzione.

## Firmare l'applicazione abilitata all'uso di diritti

Questa procedura presuppone che l'applicazione sia già stata firmata per una gerarchia di pre-produzione. In caso contrario, seguire la procedura descritta nell'articolo relativo al [test dell'applicazione abilitata all'uso di diritti](running-your-first-application.md).

Dopo aver ricevuto il certificato di produzione da Microsoft, saranno disponibili i file seguenti:

-   YourPrivateKey.dat
-   YourPublicKey.dat
-   ProductionCertificate.xml

Inserirli nella stessa directory di *GenManifest.exe* e del file binario dell'applicazione (.exe).

-   La procedura seguente consente di creare un nuovo file MCF con un certificato di produzione:

    -   Creare una nuova directory e posizionare i file in tale directory. Usare Notepad.exe per creare un file MCF per l'applicazione. Il file deve avere i contenuti seguenti.

        ``` syntax
        AUTO-GUID
        .\\YourPrivateKey.dat
        modulelist
        req     .\\<yourappname>.exe
        POLICYLIST
        INCLUSION
        PUBLICKEY .\\YourPublicKey.dat
        EXCLUSION
        ```

    -   Eseguire il comando seguente per firmare l'applicazione:

        **genmanifest.exe -chain ProductionCertificate.xml** *NomeApp***.mcf** *NomeApp***.exe.man**

        Se Genmanifest ha avuto esito positivo, verrà visualizzato solo il testo seguente:

        Se Genmanifest ha avuto esito negativo, verrà visualizzato un messaggio di errore.

    -   Il file *NomeApp*.exe.man deve essere posizionato sempre nella stessa directory di *NomeApp*.exe.

## Argomenti correlati

* [Procedura](how-to-use-msipc.md)
* [Test dell'applicazione abilitata all'uso di diritti](running-your-first-application.md)
 

 





<!--HONumber=Apr16_HO4-->


