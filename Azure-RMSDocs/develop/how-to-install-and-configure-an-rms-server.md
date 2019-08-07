---
title: Come installare, configurare e testare un server RMS | Azure RMS
description: Installare e configurare un server RMS per il test dell'applicazione abilitata all'uso di diritti.
keywords: ''
author: msmbaldwin
ms.author: mbaldwin
manager: barbkess
ms.date: 02/23/2017
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 32C7F387-CF7E-4CE0-AFC9-4C63FE1E134A
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
ms.custom: dev
ms.openlocfilehash: 59aa02318a0c6d7ee5e9857bead4c79248546320
ms.sourcegitcommit: 9968a003865ff2456c570cf552f801a816b1db07
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/05/2019
ms.locfileid: "68794106"
---
# <a name="how-to-install-configure-and-test-with-an-rms-server"></a>Procedura: installare, configurare e testare un server RMS

Questo argomento descrive la procedura di collegamento a un server RMS o ad Azure RMS per il test dell'applicazione abilitata all'uso di diritti.
 
## <a name="instructions"></a>Istruzioni

### <a name="step-1-setup-your-rms-server"></a>Passaggio 1: Configurare il server RMS

La procedura seguente consente di configurare il server RMS e include queste operazioni:

-   Installare il server
-   Registrare il server

1. **Installare il server**

   Active Directory Rights Management Services (AD RMS) è costituito da componenti server e client separati. Il componente server viene implementato come set di servizi Web che è possibile usare per amministrare un'infrastruttura RMS, emettere licenze per chi pubblica e chi utilizza i contenuti e rilasciare certificati per computer e utenti.

   A partire da Windows Server 2008, entrambi i componenti client e server sono inclusi nel sistema operativo. È possibile scaricare i componenti server per i sistemi operativi precedenti dalla posizione indicata di seguito.

   -   [Server RMS versione 1.0 SP2](https://go.microsoft.com/fwlink/p/?linkid=73722)

   Per configurare il componente server in Windows Server 2008, è necessario installare il ruolo AD RMS. Se si stanno sviluppando applicazioni su un sistema operativo server precedente, configurare il Registro di sistema dopo l'installazione del server RMS v1.0 SP2 ma prima del provisioning del servizio RMS.

2. **Registrare il server**

   È necessario registrare un server Rights Management Services (RMS) per consentirne l'identificazione nella gerarchia di pre-produzione o di produzione. Il processo di registrazione lascia un certificato del licenziante server nel computer server. Questo certificato rimanda a una radice di attendibilità Microsoft. La modalità di registrazione del server dipende dalla versione di RMS in uso.

   -   **Autoregistrazione**

       A partire da Windows Server 2008, è possibile registrare un server RMS nella gerarchia appropriata senza inviare informazioni a Microsoft. Quando si installa il ruolo RMS, vengono installati anche un certificato di autoregistrazione e una chiave privata. Questi componenti vengono usati per creare automaticamente il certificato del licenziante server. Non vengono scambiate informazioni con Microsoft.

   -   **Registrazione online**

       Se si usa AD RMS v1.0 SP2, è possibile registrare il server online. La registrazione viene eseguita in background durante il processo di provisioning, ma è necessario disporre di una connessione Internet.

       **HKEY\_LOCAL\_MACHINE**\\**Software**\\**Microsoft**\\**DRMS**\\**1.0**\\**UddiProvider** = 0e3d9bb8-b765-4a68-a329-51548685fed3

3. **Test con il server RMS**

    Per eseguire test con un server RMS, configurare l'individuazione sul lato server o sul lato client per abilitare Rights Management Services Client 2.1 per individuare e stabilire la comunicazione con il server RMS.

    > [!Note]
    > I test con Azure RMS non richiedono la configurazione di rilevamento.

   - Nell'individuazione del server, un amministratore registra un service connection point (SCP) per il cluster radice RMS con Active Directory e il client esegue una query ad Active Directory per individuare SCP e stabilire una connessione con il server.
   - Nell'individuazione del client, configurare le impostazioni di individuazione del servizio RMS nel Registro sul computer su cui è in esecuzione RMS Client 2.1. Queste impostazioni rimandano RMS Client 2.1 al server RMS da usare. Quando sono presenti, l'individuazione non viene eseguita sul lato server.

   Per configurare l'individuazione sul lato client, è possibile impostare le chiavi del registro seguenti in modo che puntino al server RMS. Per informazioni su come configurare l'individuazione sul lato servizio, vedere [Note sulla distribuzione del client RMS](https://technet.microsoft.com/library/jj159267(WS.10).aspx).

4. **EnterpriseCertification**

        HKEY_LOCAL_MACHINE
          SOFTWARE
            Microsoft
              MSIPC
                ServiceLocation
                  EnterpriseCertification

   **Valore**: (predefinito): [**http|https**]://RMSClusterName/ **_wmcs/Certification**

5. **EnterprisePublishing**

        HKEY_LOCAL_MACHINE
          SOFTWARE
            Microsoft
              MSIPC
                ServiceLocation
                  EnterprisePublishing
                  
   **Valore**: (predefinito): [**http|https**]://RMSClusterName/ **_wmcs/Licensing**

> [!NOTE]
> Per impostazione predefinita, queste chiavi non sono presenti nel registro e devono essere create.
> 
> [!IMPORTANT]
> Se si esegue un'applicazione a 32 bit su una versione a 64 bit di Windows, è necessario impostare queste chiavi nel percorso della chiave seguente:<p>
>   ```    
>   HKEY_LOCAL_MACHINE
>     SOFTWARE
>       Wow6432Node
>         Microsoft
>           MSIPC
>             ```
