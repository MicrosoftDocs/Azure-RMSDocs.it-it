---
title: Operazioni del ciclo di vita della chiave del tenant AIP gestite da Microsoft
description: Informazioni sulle operazioni del ciclo di vita rilevanti nel caso in cui la chiave del tenant per Azure Information Protection sia gestita da Microsoft (impostazione predefinita).
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 08/23/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 3c48cda6-e004-4bbd-adcf-589815c56c55
ms.subservice: kms
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 00e99f55130f25fa9368a7fdcd1f8c2795250c89
ms.sourcegitcommit: dc655736e531260c7718a8808f4f1016391d2d7d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/26/2019
ms.locfileid: "70020479"
---
# <a name="microsoft-managed-tenant-key-life-cycle-operations"></a>Gestito da Microsoft: operazioni del ciclo di vita della chiave del tenant

>*Si applica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

Se la chiave del tenant per Azure Information Protection viene gestita da Microsoft (impostazione predefinita), usare le sezioni seguenti per ottenere altre informazioni sulle operazioni del ciclo di vita pertinenti a questa topologia.

## <a name="revoke-your-tenant-key"></a>Revocare la chiave del tenant
Quando si annulla la sottoscrizione di Azure Information Protection, l'uso della chiave del tenant in Azure Information Protection viene interrotto e non è necessaria alcuna azione da parte dell'utente.

## <a name="rekey-your-tenant-key"></a>Reimpostare la chiave del tenant
Il processo di reimpostazione della chiave è noto anche come rollover della chiave. Quando si esegue questa operazione, Azure Information Protection interrompe l'uso della chiave del tenant esistente per proteggere documenti e messaggi di posta elettronica e inizia a usare una chiave diversa. I criteri e i modelli vengono subito abbandonati, ma questo passaggio è comunque graduale per i client e i servizi esistenti che usano Azure Information Protection. Ciò significa che, per un certo periodo di tempo, parte del nuovo contenuto continua a essere protetta tramite la chiave del tenant precedente.

Per reimpostare la chiave, è necessario configurare l'oggetto della chiave del tenant e specificare la chiave alternativa da usare. La chiave usata in precedenza viene quindi contrassegnata automaticamente come archiviata per Azure Information Protection. Questa configurazione assicura che il contenuto protetto tramite questa chiave rimanga accessibile.

Ecco alcuni casi in cui potrebbe essere necessario reimpostare una chiave per Azure Information Protection:

- È stata effettuata una migrazione da Active Directory Rights Management Services (AD RMS) con una chiave in Modalità crittografia 1. Una volta completata la migrazione, si desidera passare all'uso di una chiave che adotti la Modalità crittografia 2.

- La società è stata divisa in due o più società. Quando si reimposta la chiave del tenant, la nuova società non potrà accedere al nuovo contenuto pubblicato dai dipendenti e sarà in grado di accedere al vecchio contenuto se dispone di una copia della chiave del tenant precedente.

- Si vuole passare da una topologia di gestione delle chiavi a un'altra.

- Si sospetta una violazione della copia master della chiave del tenant in possesso dell'utente.

Per reimpostare una chiave, è possibile selezionare una chiave diversa gestita da Microsoft come chiave del tenant dell'utente, ma non è possibile creare una nuova chiave gestita da Microsoft. Per creare una nuova chiave, è necessario modificare la topologia della chiave per consentirne la gestione da parte del cliente (BYOK).

Se si esegue la migrazione da Active Directory Rights Management Services (AD RMS) e si sceglie la topologia di chiave gestita da Microsoft per Azure Information Protection, si dispone di più di una chiave gestita da Microsoft. In questo scenario, l'utente ha almeno due chiavi del tenant gestite da Microsoft. Una o più chiavi sono quelle importate da AD RMS. Sarà disponibile anche la chiave predefinita creata automaticamente per il tenant di Azure Information Protection dell'utente.

Per selezionare una chiave diversa come chiave del tenant attiva per Azure Information Protection, usare il cmdlet [set-AipServiceKeyProperties](/powershell/module/aipservice/set-aipservicekeyproperties) del modulo AIPService. Per facilitare l'identificazione della chiave da usare, usare il cmdlet [Get-AipServiceKeys](/powershell/module/aipservice/get-aipservicekeys) . È possibile identificare la chiave predefinita creata automaticamente per il tenant di Azure Information Protection eseguendo il comando seguente:

    (Get-AipServiceKeys) | Sort-Object CreationTime | Select-Object -First 1

Per modificare la topologia di chiave in modo che venga gestita dal cliente (BYOK), vedere [Implementazione dello scenario BYOK per la chiave del tenant di Azure Information Protection](plan-implement-tenant-key.md#implementing-byok-for-your-azure-information-protection-tenant-key).

## <a name="backup-and-recover-your-tenant-key"></a>Eseguire il backup e il ripristino della chiave del tenant
Microsoft è responsabile delle operazioni di backup della chiave del tenant e non è necessaria alcuna azione da parte dell'utente.

## <a name="export-your-tenant-key"></a>Esportare la chiave del tenant
Per esportare la configurazione di Azure Information Protection e la chiave del tenant, seguire le istruzioni descritte in questi tre passaggi:

### <a name="step-1-initiate-export"></a>Passaggio 1: Avviare l'esportazione

- [Contattare il supporto tecnico Microsoft](information-support.md#to-contact-microsoft-support) per aprire un **caso di supporto di Azure Information Protection con una richiesta di esportazione della chiave di Azure Information Protection**. È necessario dimostrare di essere un amministratore globale per il tenant e comprendere che questo processo richiede diversi giorni per la conferma. Il servizio è soggetto ai costi di supporto standard. L'esportazione della chiave del tenant non è un servizio di assistenza gratuito.

### <a name="step-2-wait-for-verification"></a>Passaggio 2: Attendi verifica

- Microsoft verifica che la richiesta di rilasciare la chiave del tenant di Azure Information Protection sia legittima. L'operazione può richiedere fino a tre settimane.

### <a name="step-3-receive-key-instructions-from-css"></a>Passaggio 3: Ricevi istruzioni chiave da CSS

- Il Servizio Supporto Tecnico Clienti Microsoft invia la configurazione di Azure Information Protection e la chiave del tenant crittografata in un file protetto da password. L'estensione del file è **tpd**. A tale scopo, il Servizio Supporto Tecnico Clienti Microsoft invia all'utente che ha avviato l'esportazione un messaggio di posta elettronica in cui è disponibile uno strumento da eseguire da un prompt dei comandi nel modo seguente:

    ```
    AadrmTpd.exe -createkey
    ```
    In questo modo viene generata una coppia di chiavi RSA e le parti pubblica e privata vengono salvate come file nella cartella corrente. Ad esempio:  **PublicKey-FA29D0FE-5049-4C8E-931B-96C6152B0441.txt** e **PrivateKey-FA29D0FE-5049-4C8E-931B-96C6152B0441.txt**.

    Rispondere al messaggio di posta elettronica ricevuto da CSS allegando il file con il nome che inizia con **PublicKey**. A questo punto CSS invierà all'utente un file TDP con estensione .xml crittografato tramite la chiave RSA. Copiare questo file nella stessa cartella in cui è stato eseguito lo strumento AadrmTpd in origine ed eseguire nuovamente lo strumento, usando il file che inizia con **PrivateKey** e il file ricevuto da CSS. Esempio:

    ```
    AadrmTpd.exe -key PrivateKey-FA29D0FE-5049-4C8E-931B-96C6152B0441.txt -target TPD-77172C7B-8E21-48B7-9854-7A4CEAC474D0.xml
    ```
    L'output di questo comando deve essere costituito da due file: uno contiene la password di testo normale per il file TPD protetto da password e l'altro è il file TPD protetto da password. I file hanno un nuovo GUID, ad esempio:
     
  - Password-5E4C2018-8C8C-4548-8705-E3218AA1544E.txt

  - ExportedTPD-5E4C2018-8C8C-4548-8705-E3218AA1544E.xml

    Eseguire il backup di questi file e archiviarli in modo sicuro per garantire che sia possibile decrittografare contenuto protetto tramite la chiave del tenant specifica. Se inoltre si esegue la migrazione ad AD RMS, è possibile importare il file con estensione tpd (il file che inizia con **ExportedTDP**) nel proprio server AD RMS.

### <a name="step-4-ongoing-protect-your-tenant-key"></a>Passaggio 4: In corso Proteggere la chiave del tenant

Dopo aver ricevuto la chiave del tenant, tenerla in posizione sicura per evitare che utenti malintenzionati possano accedere e decrittografare tutti i documenti protetti dalla chiave.

Se si esporta della chiave del tenant perché non si vuole più usare Azure Information Protection, come procedura consigliata disattivare subito il servizio Azure Rights Management dal tenant di Azure Information Protection. Non aspettare di effettuare questa operazione dopo aver ricevuto la chiave del tenant, in quanto questa precauzione consente di ridurre le conseguenze dovute all'accesso alla chiave del tenant da parte di utenti malintenzionati. Per istruzioni, vedere [Rimozione delle autorizzazioni e disattivazione di Azure Rights Management](decommission-deactivate.md).

## <a name="respond-to-a-breach"></a>Rispondere a una violazione di sicurezza
Indipendentemente dall'affidabilità, nessun sistema di sicurezza può considerarsi completo se non prevede un processo di risposta alle violazioni di sicurezza. La chiave del tenant può essere violata o rubata e anche se è protetta in modo efficiente, potrebbero essere presenti vulnerabilità nella tecnologia attuale della chiave o nella lunghezza e negli algoritmi correlati alle chiavi attuali.

Microsoft ha predisposto un team apposito per rispondere agli eventi imprevisti correlati alla sicurezza che possono verificarsi nei suoi prodotti e servizi. Non appena riceve un report plausibile su un evento imprevisto, il team si attiva per esaminarne l'ambito, la causa radice e le soluzioni. Se l'evento imprevisto influiscono sulle risorse, Microsoft invierà una notifica tramite posta elettronica agli amministratori globali del tenant.

In caso di violazione di sicurezza, l'azione più efficace che l'utente o Microsoft possa intraprendere dipende dall'ambito della violazione stessa. Microsoft collaborerà con l'utente durante l'intero processo. Nella tabella seguente vengono descritte alcune situazioni tipiche e la risposta più probabile, sebbene la risposta esatta dipenda da tutte le informazioni raccolte durante l'analisi.

|Descrizione evento imprevisto|Risposta probabile|
|------------------------|-------------------|
|Perdita della chiave del tenant.|Reimpostare la chiave del tenant. Vedere la sezione [Reimpostare la chiave del tenant](#rekey-your-tenant-key) in questo articolo.|
|Diritti di accesso alla chiave del tenant ottenuti da un utente non autorizzato o da malware, ma nessuna perdita della chiave.|La reimpostazione della chiave del tenant non è sufficiente ed è necessaria un'analisi della causa radice. Se l'utente non autorizzato ha ottenuto l'accesso a causa di un bug del processo o del software, questo problema deve essere risolto.|
|Vulnerabilità scoperta nell'algoritmo RSA o nella lunghezza della chiave oppure attacchi di forza bruta diventati realizzabili a livello di calcolo.|Microsoft deve aggiornare Azure Information Protection per supportare nuovi algoritmi e lunghezze maggiori della chiave che siano resilienti e invitare tutti i clienti a reimpostare la propria chiave del tenant.|


