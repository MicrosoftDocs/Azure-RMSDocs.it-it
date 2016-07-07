---
title: Generare e trasferire la propria chiave del tenant tramite Internet | Azure RMS
description: 
keywords: 
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 1bff9b06-8c5a-4b1d-9962-6668219210e6
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 7a9c8b531ec342e7d5daf0cbcacd6597a79e6a55
ms.openlocfilehash: 20cfa722f7008c52f4fbc219a4de04c50ee3548d


---


# Generare e trasferire la propria chiave del tenant tramite Internet

*Si applica a: Azure Rights Management, Office 365*

Se si vuole [gestire la chiave del tenant](plan-implement-tenant-key.md#choose-your-tenant-key-topology-managed-by-microsoft-the-default-or-managed-by-you-byok-) e trasferirla tramite Internet invece di recarsi in una struttura Microsoft per trasferirla di persona, seguire queste procedure:


## Preparare la workstation connessa a Internet
Per preparare la workstation connessa a Internet, seguire questi 3 passaggi:

-   [Passaggio 1: Installare Windows PowerShell per Azure Rights Management](#step-1-install-windows-powershell-for-azure-rights-management)

-   [Passaggio 2: Ottenere l'ID del tenant di Azure Active Directory](#step-2-get-your-azure-active-directory-tenant-id)

-   [Passaggio 3: Scaricare il set di strumenti BYOK](#step-3-download-the-byok-toolset)

### Passaggio 1: Installare Windows PowerShell per Azure Rights Management
Dalla workstation connessa a Internet scaricare e installare il modulo Windows PowerShell per Azure Rights Management.

> [!NOTE]
> Se il modulo Windows PowerShell è stato scaricato in precedenza, eseguire il comando seguente per verificare che la versione in uso sia almeno la versione 2.1.0.0: `(Get-Module aadrm -ListAvailable).Version`

Per istruzioni di installazione, vedere [Installazione di Windows PowerShell per Azure Rights Management](../deploy-use/install-powershell.md).

### Passaggio 2: Ottenere l'ID del tenant di Azure Active Directory
Avviare Windows PowerShell con l'opzione **Esegui come amministratore** , quindi eseguire i comandi indicati di seguito.

-   Usare il cmdlet [Connect-AadrmService](http://msdn.microsoft.com/library/windowsazure/dn629415.aspx) per connettersi al servizio Azure RMS:

    ```
    Connect-AadrmService
    ```
    Quando viene chiesto, immettere le credenziali dell'amministratore del tenant [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)]. In genere, viene usato un account amministratore globale per Azure Active Directory o Office 365.

-   Usare il cmdlet [Get-AadrmConfiguration](http://msdn.microsoft.com/library/windowsazure/dn629410.aspx) per visualizzare la configurazione del tenant:

    ```
    Get-AadrmConfiguration
    ```
    Nel file di output salvare il GUID presente nella prima riga (BPOSId), che rappresenta l'ID tenant di Azure Active Directory necessario in seguito nella preparazione della chiave del tenant per il caricamento.

-   Usare il cmdlet [Disconnect-AadrmService](http://msdn.microsoft.com/library/windowsazure/dn629416.aspx) per disconnettersi dal servizio Azure RMS fino a quando non si è pronti per caricare la chiave:

    ```
    Disconnect-AadrmService
    ```

Non chiudere la finestra di Windows PowerShell.

### Passaggio 3: Scaricare il set di strumenti BYOK
Accedere all'Area download Microsoft e [scaricare il set di strumenti BYOK](http://go.microsoft.com/fwlink/?LinkId=335781) a seconda dell'area geografica di appartenenza.

|area|Nome pacchetto|
|----------|----------------|
|America del Nord|AzureRMS-BYOK-tools-UnitedStates.zip|
|Europa|AzureRMS-BYOK-tools-Europe.zip|
|Asia|AzureRMS-BYOK-tools-AsiaPacific.zip|
Il set di strumenti include gli elementi seguenti:

-   Pacchetto di chiavi per lo scambio delle chiavi con un nome che inizia con **BYOK-KEK-pkg-**.

-   Pacchetto relativo all'ambiente di sicurezza con un nome che inizia con **BYOK-SecurityWorld-pkg-**.

-   Script python denominato **verifykeypackage.py**.

-   File eseguibile dalla riga di comando denominato **KeyTransferRemote.exe**, file di metadati denominato **KeyTransferRemote.exe.config** e DLL associate.

-   Componente Visual C++ Redistributable Package denominato **vcredist_x64.exe**.

Copiare il pacchetto in un'unità USB o in un altro dispositivo di archiviazione portatile.

## Preparare la workstation disconnessa
Per preparare la workstation non connessa a una rete (Internet o la rete interna), seguire questi 2 passaggi.

-   [Passaggio 1: Preparare la workstation disconnessa con il modulo di protezione hardware Thales](#step-1-prepare-the-disconnected-workstation-with-thales-hsm)

-   [Passaggio 2: Installare il set di strumenti BYOK nella workstation disconnessa](#step-2-install-the-byok-toolset-on-the-disconnected-workstation)

### Passaggio 1: Preparare la workstation disconnessa con il modulo di protezione hardware Thales
Nella workstation disconnessa installare il software di supporto nCipher (Thales) in un computer Windows, quindi collegare un modulo di protezione hardware Thales a tale computer.

Assicurarsi che gli strumenti Thales si trovino nel percorso appropriato **(%nfast_home%\bin** e **%nfast_home%\python\bin**). Digitare ad esempio

```
set PATH=%PATH%;”%nfast_home%\bin”;”%nfast_home%\python\bin”
```
Per altre informazioni, vedere la guida dell'utente inclusa con il modulo di protezione Thales o visitare il sito Web di Thales per Azure RMS all'indirizzo [http://www.thales-esecurity.com/msrms/cloud](http://www.thales-esecurity.com/msrms/cloud).

### Passaggio 2: Installare il set di strumenti BYOK nella workstation disconnessa
Copiare il pacchetto del set di strumenti BYOK dall'unità USB o da un altro dispositivo di archiviazione portatile, quindi eseguire le operazioni seguenti:

1.  Estrarre i file dal pacchetto scaricato in una cartella qualsiasi.

2.  In tale cartella eseguire vcredist_x64.exe.

3.  Seguire le istruzioni per installare i componenti di runtime di Visual C++ per Visual Studio 2012.

## Generare la chiave del tenant
Nella workstation disconnessa eseguire questi 3 passaggi per generare la propria chiave tdel tenant:

-   [Passaggio 1: Creare un ambiente di sicurezza](#step-1-create-a-security-world)

-   [Passaggio 2: Convalidare il pacchetto scaricato](#step-2-validate-the-downloaded-package)

-   [Passaggio 3: Creare una nuova chiave](#step-3-create-a-new-key)

### Passaggio 1: Creare un ambiente di sicurezza
Avviare un prompt dei comandi ed eseguire il programma new-world di Thales.

```
new-world.exe --initialize --cipher-suite=DLf1024s160mRijndael --module=1 --acs-quorum=2/3
```
Tale programma crea un file di **ambiente di sicurezza** nel percorso %NFAST_KMDATA%\local\world, che corrisponde alla cartella C:\ProgramData\nCipher\Key Management Data\local. È possibile creare valori diversi per il quorum, ma nell'esempio viene chiesto di immettere tre schede vuote e un codice PIN per ciascuna scheda. Qualsiasi coppia di schede dovrà quindi disporre di accesso amministrativo all'ambiente di sicurezza (il quorum specificato).  Tali schede diventano il **set di schede amministrative** per il nuovo ambiente di sicurezza. È possibile specificare la password o il PIN per ogni scheda di ACS in questa fase oppure aggiungerli successivamente con un comando.

> [!TIP]
> È possibile verificare lo stato della configurazione attuale del modulo di protezione hardware usando il comando `nkminfo` .

Eseguire quindi le operazioni seguenti:

1.  Installare il provider CNG di Thales come descritto nella documentazione di Thales e configurarlo per usare il nuovo ambiente di sicurezza.

2.  Eseguire il backup del file relativo all'ambiente **%nfast_kmdata%\local**. Proteggere il file relativo all'ambiente, le schede amministrative e i codici PIN relativi e verificare che nessuna singola persona possa accedere a più di una scheda.

### Passaggio 2: Convalidare il pacchetto scaricato
Questo passaggio è facoltativo, ma è consigliato in modo che sia possibile convalidare gli elementi seguenti:

-   Chiave per lo scambio delle chiavi inclusa nel set di strumenti generato da un modulo di protezione hardware Thales originale.

-   Hash dell'ambiente di sicurezza di Azure RMS incluso nel set di strumenti generato da un modulo di protezione hardware Thales originale.

-   Impossibilità di esportare la chiave per lo scambio delle chiavi.

> [!NOTE]
> Per convalidare il pacchetto scaricato, il modulo di protezione hardware deve essere connesso e acceso e deve essere associato a un ambiente di sicurezza (ad esempio quello appena creato).

#### Per convalidare il pacchetto scaricato

1.  Eseguire lo script verifykeypackage.py associando uno dei comandi seguenti, a seconda dell'area geografica di appartenenza:

    -   America del Nord

        ```
        python verifykeypackage.py -k BYOK-KEK-pkg-NA-1 -w BYOK-SecurityWorld-pkg-NA-1
        ```

    -   Europa

        ```
        python verifykeypackage.py -k BYOK-KEK-pkg-EU-1 -w BYOK-SecurityWorld-pkg-EU-1
        ```

    -   Asia

        ```
        python verifykeypackage.py -k BYOK-KEK-pkg-AP-1 -w BYOK-SecurityWorld-pkg-AP-1
        ```

    > [!TIP]
    > Il software Thales include un interprete Python nel percorso %NFAST_HOME%\python\bin

2.  Assicurarsi di visualizzare il risultato positivo seguente, che indica il completamento della convalida: **Result:  SUCCESS**

Questo script consente di convalidare la catena di firmatari fino alla chiave radice di Thales. La funzione hash di questa chiave radice è incorporata nello script e il relativo valore deve essere **59178a47 de508c3f 291277ee 184f46c4 f1d9c639**. Si può anche confermare questo valore separatamente sul [sito Web di Thales](http://www.thalesesec.com/).

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
cngimport --import -M --key=contosokey --appname=simple contosokey
```
Quando si esegue il comando, usare le istruzioni seguenti:

-   Sostituire *contosokey* con lo stesso valore specificato in [Passaggio 1: Creare un ambiente di sicurezza](#step-1-create-a-security-world) nella sezione *Generare la chiave del tenant*.

-   Usare l'opzione **-M** in modo che la chiave sia adatta per lo scenario. Senza questa opzione, la chiave risultante sarà una chiave specifica per l'utente corrente.

-   L'opzione **appname** corrisponde al nome dell'app indicato nel file della chiave. Se sono state usate queste istruzioni per creare una nuova chiave, è stato usato il valore simple, come illustrato nel comando. Se tuttavia si sta eseguendo la migrazione di una chiave esistente protetta dal modulo di protezione hardware per una migrazione di AD RMS in Azure RMS, specificare il nome esistente in questo comando e nei comandi seguenti quando viene usata l'opzione appname.

Questo comando crea un file di chiave in formato token nella cartella %NFAST_KMDATA%\local dell'utente con un nome che inizia con **key_caping_`_`** seguito da un SID. Ad esempio: **key_caping_machine--801c1a878c925fd9df4d62ba001b94701c039e2fb**. Questo file contiene una chiave crittografata.

> [!TIP]
> È possibile verificare lo stato attuale della configurazione delle chiavi usando il comando `nkminfo –k` .

Eseguire il backup del file di chiave in formato token in un percorso sicuro.

> [!IMPORTANT]
> Quando in seguito si trasferisce la chiave ad Azure RMS, Microsoft non può esportarla nuovamente nei dispositivi dell'utente, pertanto è estremamente importante eseguire il backup della chiave e dell'ambiente di sicurezza in modo sicuro. Per ottenere informazioni aggiuntive e procedure consigliate per eseguire il backup della chiave, contattare Thales.

A questo punto è possibile trasferire la propria chiave del tenant ad Azure RMS.

## Preparare la chiave del tenant per il trasferimento
Nella workstation disconnessa eseguire questi 4 passaggi per preparare la propria chiave del tenant:

-   [Passaggio 1: Creare una copia della chiave con autorizzazioni ridotte](#step-1-create-a-copy-of-your-key-with-reduced-permissions)

-   [Passaggio 2: Verificare la nuova copia della chiave](#step-2-inspect-the-new-copy-of-the-key)

-   [Passaggio 3: Crittografare la chiave tramite la chiave per lo scambio di chiavi di Microsoft](#step-3-encrypt-your-key-by-using-microsoft-s-key-exchange-key)

-   [Passaggio 4: Copiare il pacchetto di trasferimento della chiave nella workstation connessa a Internet](#step-4-copy-your-key-transfer-package-to-the-internet-connected-workstation)

### Passaggio 1: Creare una copia della chiave con autorizzazioni ridotte
Per ridurre le autorizzazioni sulla chiave del tenant, eseguire le operazioni seguenti:

-   A un prompt dei comandi eseguire uno dei comandi seguenti, a seconda dell'area geografica di appartenenza:

    -   America del Nord

        ```
        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-NA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-NA-1
        ```

    -   Europa

        ```
        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-EU-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-EU-1
        ```

    -   Asia

        ```
        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-AP-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-AP-1
        ```

Quando si esegue questo comando, sostituire *contosokey* con lo stesso valore specificato in [Passaggio 1: Creare un ambiente di sicurezza](#step-1-create-a-security-world) nella sezione *Generare la chiave del tenant*.

Verrà richiesto di inserire le schede di ACS dell'ambiente di sicurezza e, se specificati, la password o il PIN.

Al termine dell'esecuzione del comando, verrà visualizzato **Result: SUCCESS** e la copia della chiave del tenant con autorizzazioni ridotte si troverà nel file denominato key_xferacId_*&lt;contosokey&gt;*.

### Passaggio 2: Verificare la nuova copia della chiave
Se si desidera, eseguire le utilità Thales per confermare le autorizzazioni minime sulla nuova chiave del tenant:

-   aclprint.py

    ```
    "%nfast_home%\bin\preload.exe" -m 1 -A xferacld -K contosokey "%nfast_home%\python\bin\python" "%nfast_home%\python\examples\aclprint.py"
    ```

-   kmfile-dump.exe

    ```
    "%nfast_home%\bin\kmfile-dump.exe" "%NFAST_KMDATA%\local\key_xferacld_contosokey"
    ```

Quando si esegue questo comando, sostituire *contosokey* con lo stesso valore specificato in [Passaggio 1: Creare un ambiente di sicurezza](#step-1-create-a-security-world) nella sezione *Generare la chiave del tenant*.

### Passaggio 3: Crittografare la chiave tramite la chiave per lo scambio di chiavi di Microsoft
Eseguire uno dei comandi seguenti, a seconda dell'area geografica di appartenenza:

-   America del Nord

    ```
    KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-NA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-NA-1 -TenantBposId GUID -KeyFriendlyName ContosoFirstkey
    ```

-   Europa

    ```
    KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-EU-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-EU-1 -TenantBposId GUID -KeyFriendlyName ContosoFirstkey
    ```

-   Asia

    ```
    KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-AP-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-AP-1 -TenantBposId GUID -KeyFriendlyName ContosoFirstkey
    ```

Quando si esegue il comando, usare le istruzioni seguenti:

-   Sostituire *contosokey* con l'identificatore usato per generare la chiave in [Passaggio 1: Creare un ambiente di sicurezza](#step-1-create-a-security-world) nella sezione *Generare la chiave del tenant*.

-   Sostituire *GUID* con il proprio ID tenant di Azure Active Directory recuperato in [Passaggio 2: Ottenere l'ID del tenant di Azure Active Directory](#step-2-get-your-azure-active-directory-tenant-id) nella sezione *Preparare la workstation connessa a Internet*.

-   Sostituire *ContosoFirstKey* con un'etichetta usata per il nome del file di output.

Al completamento dell'operazione verrà visualizzato il messaggio **Result: SUCCESS** e nella cartella corrente sarà presente un nuovo file denominato: TransferPackage-*ContosoFirstkey*.byok

### Passaggio 4: Copiare il pacchetto di trasferimento della chiave nella workstation connessa a Internet
Usare un'unità USB o un altro dispositivo di archiviazione portatile per copiare il file di output creato nel passaggio precedente (*KeyTransferPackage-ContosoFirstkey*.byok) nella workstation connessa a Internet.

> [!NOTE]
> Usare le procedure di sicurezza per proteggere il file, poiché include la chiave privata.

## Trasferire la chiave del tenant ad Azure RMS
Nella workstation connessa a Internet eseguire questi 3 passaggi per trasferire la nuova chiave del tenant ad Azure RMS:

-   [Passaggio 1: Connettersi ad Azure RMS](#step-1-connect-to-azure-rms)

-   [Passaggio 2: Caricare il pacchetto della chiave](#step-2-upload-the-key-package)

-   [Passaggio 3: Enumerare le chiavi tenant (in base alle esigenze)](#step-3-enumerate-your-tenant-keys-as-needed)

### Passaggio 1: Connettersi ad Azure RMS
Tornare alla finestra di Windows PowerShell e digitare i comandi indicati di seguito.

1.  Per riconnettersi al servizio [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)]:

    ```
    Connect-AadrmService
    ```

2.  Usare il cmdlet [Get-AadrmKeys](http://msdn.microsoft.com/library/windowsazure/dn629420.aspx) per visualizzare la configurazione della chiave del tenant corrente:

    ```
    Get-AadrmKeys
    ```

### Passaggio 2: Caricare il pacchetto della chiave
Usare il cmdlet [Add-AadrmKey](http://msdn.microsoft.com/library/windowsazure/dn629418.aspx) per caricare il pacchetto di trasferimento della chiave copiata dalla workstation disconnessa:

```
Add-AadrmKey –KeyFile <PathToPackageFile> -Verbose
```
> [!WARNING]
> Viene chiesto di confermare l'azione. È importante tenere presente che questa azione non può essere annullata. Quando si carica una chiave del tenant, quest'ultima diventa automaticamente la chiave del tenant primaria dell'organizzazione e gli utenti inizieranno a usarla quando proteggono documenti e file.

Se il caricamento riesce, viene visualizzato un messaggio che indica che la chiave è stata aggiunta: **The Rights management service successfully added the key.**

Prevedere un ritardo di replica prima che la modifica si propaghi a tutti i data center di [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)].

### Passaggio 3: Enumerare le chiavi tenant (in base alle esigenze)
Usare nuovamente il cmdlet Get-AadrmKeys per visualizzare le modifiche apportate alla chiave del tenant e tutte le volte che si desidera visualizzare un elenco delle proprie chiavi del tenant. Le chiavi tenant visualizzate includono la chiave iniziale generata da Microsoft e tutte le chiavi aggiunte dall'utente:

```
Get-AadrmKeys
```
La chiave del tenant contrassegnata come **Attiva** è quella usata attualmente dall'organizzazione per proteggere documenti e file.

Tutti i passaggi necessari per trasferire la propria chiave tramite Internet sono stati completati ed è possibile continuare con i passaggi successivi per la pianificazione e l'implementazione della chiave del tenant.


> [!div class="button"]
[Passaggi successivi >>](plan-implement-tenant-key.md#next-steps)





<!--HONumber=Jun16_HO4-->


