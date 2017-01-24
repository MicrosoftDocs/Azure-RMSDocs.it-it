---
title: 'Gestione di Microsoft: operazioni del ciclo di vita della chiave del tenant | Azure Information Protection'
description: Informazioni sulle operazioni del ciclo di vita rilevanti se Microsoft gestisce la chiave del tenant per Azure Information Protection (impostazione predefinita).
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 09/25/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 3c48cda6-e004-4bbd-adcf-589815c56c55
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 7068e0529409eb783f16bc207a17be27cd5d82a8
ms.openlocfilehash: 0aad5eeb88dd471ece1bf6425a4efe8050bbdf2c


---


# <a name="microsoft-managed-tenant-key-lifecycle-operations"></a>Gestione di Microsoft: operazioni del ciclo di vita della chiave del tenant

>*Si applica a: Azure Information Protection, Office 365*

Se la chiave del tenant per Azure Information Protection viene gestita da Microsoft (impostazione predefinita), usare le sezioni seguenti per ottenere altre informazioni sulle operazioni del ciclo di vita rilevanti per questa topologia.

## <a name="revoke-your-tenant-key"></a>Revocare la chiave del tenant
Quando si annulla la sottoscrizione di Azure Information Protection, l'uso della chiave del tenant in Azure Information Protection viene interrotto e non è necessaria alcuna azione da parte dell'utente.

## <a name="re-key-your-tenant-key"></a>Ridistribuire la chiave del tenant
Il processo di ridistribuzione della chiave è denominato anche rollover della chiave. Non ridistribuire la chiave tenant a meno che non sia effettivamente necessario. Alcuni client precedenti, ad esempio Office 2010, non erano progettati per gestire in modo efficiente le modifiche delle chiavi. In questo scenario è necessario cancellare lo stato di Rights Management nei computer tramite Criteri di gruppo o un meccanismo equivalente. In alcuni casi è tuttavia opportuno forzare la ridistribuzione della chiave del tenant, Ad esempio:

-   La società è stata divisa in due o più società. Quando si ridistribuisce la chiave del tenant, la nuova società non potrà accedere al nuovo contenuto pubblicato dai dipendenti e sarà in grado di accedere al vecchio contenuto se dispone di una copia della chiave del tenant precedente.

-   Eventuale violazione della copia master della chiave del tenant (copia in proprio possesso).

È possibile reimpostare la chiave del tenant [contattando il supporto Microsoft](../get-started/information-support.md#to-contact-microsoft-support) per aprire un **caso di supporto tecnico di Azure Information Protection con una richiesta per reimpostare la chiave del tenant di Azure Information Protection**. È necessario dimostrare di essere un amministratore del tenant di Azure Information Protection. Si tenga presente che la conferma di questo processo richiede diversi giorni. Il servizio è soggetto ai costi di supporto standard; la ridistribuzione della chiave del tenant non è un servizio di assistenza gratuito.

Quando si ridistribuisce la chiave del tenant, il nuovo contenuto è protetto tramite la nuova chiave. Poiché questo processo viene eseguito per fasi, per un certo periodo di tempo parte del nuovo contenuto continuerà a essere protetto tramite la chiave del tenant precedente. Il contenuto protetto in precedenza rimane tale rispetto alla chiave del tenant precedente. Per supportare questo scenario, Azure Information Protection mantiene la chiave del tenant precedente in modo da emettere licenze per il vecchio contenuto.

## <a name="backup-and-recover-your-tenant-key"></a>Eseguire il backup e il ripristino della chiave del tenant
Microsoft è responsabile delle operazioni di backup della chiave del tenant e non è necessaria alcuna azione da parte dell'utente.

## <a name="export-your-tenant-key"></a>Esportare la chiave del tenant
Per esportare la configurazione di Azure Information Protection e la chiave del tenant, seguire le istruzioni descritte in questi tre passaggi:

### <a name="step-1-initiate-export"></a>Passaggio 1: Avviare l'esportazione

-   A tale scopo, [contattare il supporto tecnico Microsoft](../get-started/information-support.md#to-contact-microsoft-support) per aprire un **caso di supporto tecnico di Azure Information Protection con una richiesta di esportazione della chiave di Azure Information Protection**. È necessario dimostrare di essere un amministratore del tenant di Azure Information Protection. Si tenga presente che la conferma di questo processo richiede diversi giorni. Il servizio è soggetto ai costi di supporto standard; l'esportazione della chiave del tenant non è un servizio di assistenza gratuito.

### <a name="step-2-wait-for-verification"></a>Passaggio 2: Attendere la verifica

-   Microsoft verifica che la richiesta di rilasciare la chiave del tenant di Azure Information Protection sia legittima. L'operazione può richiedere fino a 3 settimane.

### <a name="step-3-receive-key-instructions-from-css"></a>Passaggio 3: Ricevere istruzioni sulla chiave dal Servizio Supporto Tecnico Clienti Microsoft

-   Il Servizio Supporto Tecnico Clienti Microsoft invierà la configurazione di Azure Information Protection e la chiave del tenant crittografata in un file protetto da password con estensione tpd. A tale scopo, il Servizio Supporto Tecnico Clienti Microsoft invia all'utente che ha avviato l'esportazione un messaggio di posta elettronica in cui è disponibile uno strumento da eseguire da un prompt dei comandi nel modo seguente:

    ```
    AadrmTpd.exe -createkey
    ```
    In questo modo viene generata una coppia di chiavi RSA e le parti pubblica e privata vengono salvate come file nella cartella corrente. Ad esempio: **PublicKey-FA29D0FE-5049-4C8E-931B-96C6152B0441.txt** e **PrivateKey-FA29D0FE-5049-4C8E-931B-96C6152B0441.txt**.

    Rispondere al messaggio di posta elettronica ricevuto da CSS allegando il file con il nome che inizia con **PublicKey**. A questo punto il Servizio Supporto Tecnico Clienti Microsoft invierà all'utente un file TDP con estensione xml crittografato tramite la chiave RSA. Copiare questo file nella stessa cartella in cui è stato eseguito lo strumento AadrmTpd in origine ed eseguire nuovamente lo strumento, usando il file che inizia con **PrivateKey** e il file ricevuto da CSS. Ad esempio:

    ```
    AadrmTpd.exe -key PrivateKey-FA29D0FE-5049-4C8E-931B-96C6152B0441.txt -target TPD-77172C7B-8E21-48B7-9854-7A4CEAC474D0.xml
    ```
    L'output del comando deve essere costituito da due file, ovvero il file con estensione tpd protetto da password e un file che ne contiene la password. Per scopi di riferimento incrociato, a entrambi deve essere associato lo stesso GUID come file di chiave pubblica e privata utilizzati per l’esecuzione del comando AadrmTpd.exe -createkey:

    -   Password-FA29D0FE-5049-4C8E-931B-96C6152B0441.txt

    -   ExportedTPD-FA29D0FE-5049-4C8E-931B-96C6152B0441.xml

    Eseguire il backup di questi file e archiviarli in modo sicuro per garantire che sia possibile decrittografare contenuto protetto tramite la chiave del tenant specifica. Se inoltre si esegue la migrazione ad AD RMS, è possibile importare il file con estensione tpd (il file che inizia con **ExportedTDP**) nel proprio server AD RMS.

### <a name="step-4-ongoing-protect-your-tenant-key"></a>Passaggio 4: In corso: Proteggere la chiave del tenant

-   Dopo aver ricevuto la chiave del tenant, tenerla in posizione sicura per evitare che utenti malintenzionati possano accedere e decrittografare tutti i documenti protetti dalla chiave.

    Se si esporta della chiave del tenant perché non si vuole più usare Azure Information Protection, come procedura consigliata disattivare subito il servizio Azure Rights Management dal tenant di Azure Information Protection. Non aspettare di effettuare questa operazione dopo aver ricevuto la chiave del tenant, in quanto questa precauzione consente di ridurre le conseguenze dovute all'accesso alla chiave del tenant da parte di utenti malintenzionati. Per istruzioni, vedere [Rimozione delle autorizzazioni e disattivazione di Azure Rights Management](decommission-deactivate.md).

## <a name="respond-to-a-breach"></a>Rispondere a una violazione di sicurezza
Indipendentemente dall'affidabilità, nessun sistema di sicurezza può considerarsi completo se non prevede un processo di risposta alle violazioni di sicurezza. La chiave del tenant può essere violata o rubata e anche se è protetta in modo efficiente, potrebbero essere presenti vulnerabilità nella tecnologia dei moduli di protezione hardware di generazione corrente e nella lunghezza e negli algoritmi correlati alle chiavi correnti.

Microsoft ha predisposto un team apposito per rispondere agli eventi imprevisti correlati alla sicurezza che possono verificarsi nei suoi prodotti e servizi. Non appena riceve un report plausibile su un evento imprevisto, il team si attiva per esaminarne l'ambito, la causa radice e le soluzioni. Se l'evento imprevisto influisce sulle risorse dell'utente, Microsoft invierà un messaggio di posta elettronica di notifica agli amministratori di tenant di Azure Information Protection all'indirizzo indicato al momento della sottoscrizione.

In caso di violazione di sicurezza, l'azione più efficace che l'utente o Microsoft possa intraprendere dipende dall'ambito della violazione stessa. Microsoft collaborerà con l'utente durante l'intero processo. Nella tabella seguente vengono descritte alcune situazioni tipiche e la risposta più probabile, sebbene la risposta esatta dipenda da tutte le informazioni raccolte durante l'analisi.

|Descrizione evento imprevisto|Risposta probabile|
|------------------------|-------------------|
|Perdita della chiave del tenant.|Ridistribuire la chiave del tenant. Vedere la sezione [Ridistribuire la chiave del tenant](operations-microsoft-managed-tenant-key.md#re-key-your-tenant-key) in questo articolo.|
|Diritti di accesso alla chiave del tenant ottenuti da un utente non autorizzato o da malware, ma nessuna perdita della chiave.|La ridistribuzione della chiave del tenant non è sufficiente ed è necessaria un'analisi della causa radice. Se l'utente non autorizzato ha ottenuto l'accesso a causa di un bug del processo o del software, questo problema deve essere risolto.|
|Vulnerabilità scoperta nell'algoritmo RSA o nella lunghezza della chiave oppure attacchi di forza bruta diventati realizzabili a livello di calcolo.|Microsoft deve aggiornare Azure Information Protection per supportare nuovi algoritmi e lunghezze maggiori della chiave che siano resilienti e invitare tutti i clienti a rinnovare le proprie chiavi del tenant.|

[!INCLUDE[Commenting house rules](../includes/houserules.md)]




<!--HONumber=Jan17_HO4-->


