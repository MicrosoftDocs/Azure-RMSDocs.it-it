---
title: Generare e trasferire la chiave del tenant di persona | Azure RMS
description: 
keywords: 
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 3281e45e-cf69-4dc5-946b-3029851d3152
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 67129d6cdac124947fc07aa4d42523686227752e
ms.openlocfilehash: 8e77298121a84f6feb16a992da81bd9c3bb7b20b


---

# Generare e trasferire la propria chiave del tenant di persona

*Si applica a: Azure Rights Management, Office 365*


Se si è deciso di [gestire la chiave del tenant](plan-implement-tenant-key.md#choose-your-tenant-key-topology-managed-by-microsoft-the-default-or-managed-by-you-byok) e la si vuole trasferire di persona anziché tramite Internet, seguire queste procedure.

## Generare la chiave del tenant
Per generare la propria chiave del tenant, eseguire questi 3 passaggi.

-   [Passaggio 1: Preparare una workstation con un modulo di protezione hardware Thales](#step-1-prepare-a-workstation-with-thales-hsm)

-   [Passaggio 2: Creare un ambiente di sicurezza](#step-2-create-a-security-world)

-   [Passaggio 3: Creare una nuova chiave](#step-3-create-a-new-key)

### Passaggio 1: Preparare una workstation con un modulo di protezione hardware Thales
Installare il software di supporto nCipher (Thales) in un computer Windows e collegare un modulo di protezione hardware Thales a tale computer. Verificare che gli strumenti Thales si trovino nel percorso locale. Per altre informazioni, vedere la guida dell'utente inclusa con il modulo di protezione Thales o visitare il sito Web di Thales per Azure RMS all'indirizzo [http://www.thales-esecurity.com/msrms/cloud](http://www.thales-esecurity.com/msrms/cloud).

### Passaggio 2: Creare un ambiente di sicurezza
Avviare un prompt dei comandi ed eseguire il programma new-world di Thales.

```
new-world.exe --initialize --cipher-suite=DLf1024s160mRijndael --module=1 --acs-quorum=2/3
```
Tale programma crea un file di **ambiente di sicurezza** nel percorso %NFAST_KMDATA%\local\world, che corrisponde alla cartella C:\ProgramData\nCipher\Key Management Data\local. È possibile creare valori diversi per il quorum, ma nell'esempio viene chiesto di immettere tre schede vuote e un codice PIN per ciascuna scheda. Qualsiasi coppia di schede consentirà di accedere in modo completo all'ambiente di sicurezza.  Tali schede diventano il **set di schede amministrative** per il nuovo ambiente di sicurezza.

Eseguire quindi le operazioni seguenti:

1.  Installare il provider CNG di Thales come descritto nella documentazione di Thales e configurarlo per usare il nuovo ambiente di sicurezza.

2.  Eseguire il backup del file relativo all'ambiente. Proteggere il file relativo all'ambiente, le schede amministrative e i codici PIN relativi e verificare che nessuna singola persona possa accedere a più di una scheda.

A questo punto si può creare una nuova chiave che costituirà la chiave del tenant RMS dell'utente.

### Passaggio 3: Creare una nuova chiave
Generare una chiave CNG tramite i programmi **generatekey** e **cngimport** di Thales.

Eseguire il comando seguente per generare la chiave:

```
generatekey --generate simple type=RSA size=2048 protect=module ident=contosokey plainname=contosokey nvram=no pubexp=
```
Quando si esegue il comando, usare le istruzioni seguenti:

-   Il parametro **protect** deve essere impostato sul valore **module**, come illustrato. Verrà creata una chiave protetta tramite modulo. Il set di strumenti BYOK non supporta le chiavi protette con OCS.

-   Per le dimensioni della chiave si consigliano 2048 bit, ma sono supportate anche chiavi RSA di 1024 bit per clienti AD RMS esistenti che possiedono tali chiavi e che stanno eseguendo la migrazione ad Azure RMS.

-   Sostituire il valore di *contosokey* per gli elementi **ident** e **plainname** con qualsiasi valore di stringa. Per ridurre i sovraccarichi amministrativi e i rischi di errore, si consiglia di usare lo stesso valore per entrambi gli elementi e di usare tutti caratteri minuscoli.

-   L'elemento pubexp viene lasciato vuoto in questo esempio (impostazione predefinita), ma è possibile indicare valori specifici. Per altre informazioni, vedere la documentazione di Thales.

Eseguire il comando seguente per importare la chiave in CNG:

```
cngimport --import –M --key=contosokey --appname=simple contosokey
```
Quando si esegue il comando, usare le istruzioni seguenti:

-   Sostituire *contosokey* con lo stesso valore specificato nel passaggio 1.

-   Usare l'opzione **-M** in modo che la chiave sia adatta per lo scenario. Senza questa opzione, la chiave risultante sarà una chiave specifica per l'utente corrente.

Tale comando crea un file di chiave in formato token nella cartella %NFAST_KMDATA%\local dell'utente con un nome che inizia con **key_caping`_`** seguito da un SID. Ad esempio: **key_caping_machine--801c1a878c925fd9df4d62ba001b94701c039e2fb**. Questo file contiene una chiave crittografata.

Eseguire il backup del file di chiave in formato token in un percorso sicuro.

> [!IMPORTANT]
> Quando in seguito si trasferisce la chiave ad Azure RMS, Microsoft disporrà di una copia non recuperabile della chiave dell'utente. In questo modo nessuno potrà recuperare la chiave dai moduli di protezione hardware presso Microsoft e l'utente manterrà il controllo esclusivo della propria chiave del tenant. Di conseguenza, l'esecuzione del backup sicuro della chiave e dell'ambiente di sicurezza costituisce un aspetto estremamente importante. Per ottenere informazioni aggiuntive e procedure consigliate per eseguire il backup della chiave, contattare Thales.

A questo punto è possibile trasferire la propria chiave del tenant ad Azure RMS.

## Trasferire la chiave del tenant ad Azure RMS
Dopo aver generato la propria chiave, prima di usarla è necessario trasferirla ad Azure RMS. Per garantire il livello più elevato di sicurezza, questo trasferimento consiste in un processo manuale che richiede la presenza dell'utente negli uffici Microsoft a Redmond, Washington, Stati Uniti. Per completare questo processo, eseguire questi 3 passaggi.

-   [Passaggio 1: Trasferire la chiave a Microsoft](#step-1-bring-your-key-to-microsoft)

-   [Passaggio 2: Trasferire la chiave all'ambiente di sicurezza di Azure RMS](#step-2-transfer-your-key-to-the-azure-rms-security-world)

-   [Passaggio 3: Procedure di chiusura](#step-3-closing-procedures)

### Passaggio 1: Trasferire la chiave a Microsoft

-   Contattare il Servizio Supporto Clienti Microsoft per pianificare un appuntamento per il trasferimento della chiave per Azure RMS. Portare negli uffici Microsoft a Redmond gli elementi seguenti:

    -   Un quorum delle proprie schede amministrative. Se sono state seguite le istruzioni precedenti nella sezione [Passaggio 2: Creare un ambiente di sicurezza](#step-2-create-a-security-world), si tratta di due qualsiasi delle tre schede in proprio possesso.

    -   Personale autorizzato ad avere le schede amministrative e i codici PIN, in genere due (uno per ogni scheda).

    -   File relativo all'ambiente di sicurezza (%NFAST_KMDATA%\local\world) in un'unità USB.

    -   File di chiave in formato token in un'unità USB.

### Passaggio 2: Trasferire la chiave all'ambiente di sicurezza di Azure RMS

1.  All'arrivo negli uffici Microsoft per trasferire la chiave, si verifica quanto segue:

    -   Microsoft fornisce all'utente una workstation offline con il modulo di protezione hardware Thales collegato, il software Thales installato e un file relativo all'ambiente di sicurezza di Azure RMS pre-caricato nella cartella C:\Temp\Destination.

    -   In questa workstation l'utente carica il proprio file relativo all'ambiente di sicurezza e il file di chiave in formato token dall'unità USB nella cartella C:\Temp\Source.

    -   Gli operatori di Azure RMS trasferiscono in modo sicuro la chiave all'ambiente di sicurezza di Azure RMS tramite utilità Thales.

    Questo processo sembrerà analogo al seguente, in cui l'ultimo parametro di key-xfer-im in questo esempio viene sostituito dal nome file di chiave in formato token dell'utente:

    **C:\&gt; mk-reprogram.exe --owner c:\Temp\Destination add c:\Temp\Source**

    **C:\&gt; key-xfer-im.exe c:\Temp\Source c:\Temp\Destination --module c:\Temp\Source\key_caping_machine--801c1a878c925fd9df4d62ba001b94701c039e2fb**

2.  Mk-reprogram chiederà all'utente e agli operatori di Azure RMS di inserire le schede amministrative e di immettere i codici PIN corrispondenti. Tali comandi restituiscono un file di chiave in formato token nella cartella C:\Temp\Destination che contiene la chiave dell'utente protetta dall'ambiente di sicurezza di Azure RMS.

### Passaggio 3: Procedure di chiusura

-   In presenza dell'utente, gli operatori di Azure RMS eseguono le operazioni seguenti:

    -   Esecuzione di uno strumento sviluppato da Microsoft in collaborazione con Thales che rimuove due autorizzazioni, ovvero l'autorizzazione per recuperare la chiave e quella per modificare le autorizzazioni. Al termine dell'operazione, questa copia della chiave è bloccata nell'ambiente di sicurezza di Azure RMS. I moduli di protezione hardware Thales non consentiranno agli operatori di Azure RMS di recuperare la copia in testo non crittografato della chiave dell'utente con le proprie schede amministrative.

    -   Copia del file di chiave risultante in un'unità USB da caricare in seguito nel servizio Azure RMS.

    -   Ripristino delle impostazioni predefinite del modulo di protezione hardware e cancellazione dei dati nella workstation.

Tutti i passaggi necessari per trasferire la chiave di persona sono stati completati ed è possibile tornare all'organizzazione per eseguire i passaggi successivi per la pianificazione e l'implementazione della chiave del tenant.

> [!div class="button"]
[Passaggi successivi >>](plan-implement-tenant-key.md#next-steps)






<!--HONumber=Jul16_HO3-->


