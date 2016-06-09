---
# required metadata

title: Installare e configurare il server | Azure RMS
description: Installare e configurare un server RMS per il test dell'applicazione abilitata all'uso di diritti.
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 32C7F387-CF7E-4CE0-AFC9-4C63FE1E134A
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
# Installare e configurare il server

Questo argomento descrive la procedura per installare e configurare un server RMS per il test dell'applicazione abilitata all'uso di diritti.

**Importante** Se si sta testando l'applicazione eseguendola nell'ambiente ISV RMS 1-box, non è necessario installare un server RMS, perché l'ambiente 1-box ne contiene già uno installato e configurato.
Per altre informazioni sull'ambiente ISV AD RMS 1-box, vedere [Configurare l'ambiente di test](how-to-set-up-your-test-environment.md).

 

## Istruzioni

### Passaggio 1: Configurare il server RMS

La procedura seguente consente di configurare il server RMS e include queste operazioni:

-   Configurare il Registro di sistema
-   Installare il server
-   Registrare il server

1.  **Configurare il Registro di sistema**

    Per specificare che si sta usando la gerarchia di certificati di pre-produzione, impostare i valori del Registro di sistema seguenti.

    **Nota** Se si usa Windows Server 2008 R2 o Windows Server 2008, impostare i valori del Registro di sistema prima di installare il servizio AD RMS.

    Se si usa AD RMS in Windows Server 2008 R2, è necessario impostare il valore **REG\_DWORD** seguente. Modificare questo valore impostandolo su 0 (zero) per passare alla gerarchia di produzione.

    **Computer**\\**HKEY\_LOCAL\_MACHINE**\\**Software**\\**Microsoft**\\**DRMS**\\**Hierarchy** = 0x00000001

    Se si usa AD RMS in Windows Server 2008 R2 e in Active Directory è già distribuito un altro servizio AD RMS come servizio di pre-produzione, aggiungere il valore di stringa vuota seguente al Registro di sistema.

    **Computer**\\**HKEY\_LOCAL\_MACHINE**\\**Software**\\**Microsoft**\\**DRMS**\\**GICURL** = ""

    Se si usa AD RMS in Windows Server 2008, è necessario impostare il valore **REG\_DWORD** seguente. Modificare questo valore impostandolo su 0 (zero) per passare alla gerarchia di produzione.

    **Computer**\\**HKEY\_LOCAL\_MACHINE**\\**Software**\\**Microsoft**\\**DRMS**\\**2.0**\\**Hierarchy** = 0x00000001

    Se si usa AD RMS in Windows Server 2008 e in Active Directory è già distribuito un altro servizio AD RMS come servizio di pre-produzione, aggiungere il valore di stringa vuota seguente al Registro di sistema.

    **Computer**\\**HKEY\_LOCAL\_MACHINE**\\**Software**\\**Microsoft**\\**DRMS**\\**2.0**\\**GICURL** = ""

2.  **Installare il server**

    Active Directory Rights Management Services (AD RMS) è costituito da componenti server e client separati. Il componente server viene implementato come set di servizi Web che è possibile usare per amministrare un'infrastruttura RMS, emettere licenze per chi pubblica e chi utilizza i contenuti e rilasciare certificati per computer e utenti.

    A partire da Windows Server 2008, entrambi i componenti client e server sono inclusi nel sistema operativo. È possibile scaricare i componenti server per i sistemi operativi precedenti dalla posizione indicata di seguito.

    -   [Server RMS v1.0 SP2](http://go.microsoft.com/fwlink/p/?linkid=73722)

    Per configurare il componente server in Windows Server 2008, è necessario installare il ruolo AD RMS. Prima di procedere, è però necessario configurare il Registro di sistema per specificare che si userà la gerarchia di certificati di pre-produzione invece della gerarchia di produzione. Se, tuttavia, si stanno sviluppando applicazioni su un sistema operativo server precedente, configurare il Registro di sistema dopo l'installazione del server RMS v1.0 SP2 ma prima del provisioning del servizio RMS.

    Per altre informazioni, vedere il passaggio 1 precedente, "Configurare il Registro di sistema".

3.  **Registrare il server**

    È necessario registrare un server Rights Management Services (RMS) per consentirne l'identificazione nella gerarchia di pre-produzione o di produzione. Il processo di registrazione lascia un certificato del licenziante server nel computer server. Questo certificato rimanda a una radice di attendibilità Microsoft. La modalità di registrazione del server dipende dalla versione di RMS in uso.

    -   **Autoregistrazione**

        A partire da Windows Server 2008, è possibile registrare un server RMS nella gerarchia appropriata senza inviare informazioni a Microsoft. Quando si installa il ruolo RMS, vengono installati anche un certificato di autoregistrazione e una chiave privata. Questi componenti vengono usati per creare automaticamente il certificato del licenziante server. Non vengono scambiate informazioni con Microsoft.

    -   **Registrazione online** Se si usa AD RMS v1.0 SP2, è possibile registrare il server online. La registrazione viene eseguita in background durante il processo di provisioning, ma è necessario disporre di una connessione Internet e specificare il valore del Registro di sistema appropriato per identificare la gerarchia in cui si sta registrando il server. Per la registrazione nella gerarchia di pre-produzione, aggiungere il valore **REG\_SZ** seguente ed effettuare il provisioning del server. Per la registrazione nella gerarchia di produzione, cancellare questo valore ed effettuare il provisioning del server.

        Per altre informazioni, vedere il passaggio 1 precedente, "Configurare il Registro di sistema".

        **HKEY\_LOCAL\_MACHINE**\\**Software**\\**Microsoft**\\**DRMS**\\**1.0**\\**UddiProvider** = 0e3d9bb8-b765-4a68-a329-51548685fed3

## Argomenti correlati

* [Modalità d'uso](how-to-use-msipc.md)
 

 





<!--HONumber=Jun16_HO1-->


