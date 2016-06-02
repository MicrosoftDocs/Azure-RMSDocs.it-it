---
# required metadata

title: Passaggio 2&colon; Migrazione da una chiave protetta tramite software a una chiave protetta tramite HSM | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: c5f4c6ea-fd2a-423a-9fcb-07671b3c2f4f

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Passaggio 2: Migrazione da una chiave protetta tramite software a una chiave protetta tramite HSM

*Si applica a: Active Directory Rights Management Services, Azure Rights Management*


Queste istruzioni fanno parte del [percorso di migrazione da AD RMS ad Azure Rights Management](migrate-from-ad-rms-to-azure-rms.md) e si applicano solo se la chiave di AD RMS è protetta tramite software e si vuole eseguire la migrazione ad Azure Rights Management con una chiave del tenant protetta tramite HSM. 

Se non si tratta dello scenario di configurazione prescelto, tornare al [Passaggio 2. Esportare i dati di configurazione da AD RMS e importarli in Azure RMS](migrate-from-ad-rms-to-azure-rms.md#step-2-export-configuration-data-from-ad-rms-and-import-it-to-azure-rms), quindi scegliere una configurazione diversa.

Questa procedura in tre parti consente di importare la configurazione di AD RMS in Azure RMS. La chiave del tenant di Azure RMS verrà gestita dall'utente (BYOK).

È innanzitutto necessario estrarre la chiave del certificato concessore di licenze server (SLC) dai dati di configurazione e trasferire la chiave in un modulo di protezione hardware locale di Thales, quindi creare il pacchetto e trasferire la chiave del proprio modulo di protezione hardware in Azure RMS e infine importare i dati di configurazione.

## Parte 1: Estrarre il certificato concessore di licenze server (SLC) dai dati di configurazione e importare la chiave nel modulo di protezione hardware locale

1.  Seguire i passaggi seguenti riportati nella sezione [Implementazione della modalità BYOK](plan-implement-tenant-key.md#BKMK_ImplementBYOK) dell'argomento [Pianificazione e implementazione della chiave del tenant di Azure Rights Management](plan-implement-tenant-key.md):

    -   **Generare e trasferire la propria chiave del tenant tramite Internet**: **Preparare la workstation connessa a Internet**

    -   **Generare e trasferire la propria chiave del tenant tramite Internet**: **Preparare la workstation disconnessa**

    Non attenersi a questa procedura per generare la chiave del tenant, perché è già disponibile una chiave equivalente nel file di dati di configurazione (con estensione XML) esportati. Si eseguirà invece un comando per estrarre la chiave dal file e importarla nel modulo di protezione hardware locale.

2.  Nella workstation disconnessa eseguire il comando seguente:

    ```
    KeyTransferRemote.exe -ImportRmsCentrallyManagedKey -TpdFilePath <TPD> -ProtectionPassword -KeyIdentifier <KeyID> -ExchangeKeyPackage <BYOK-KEK-pka-Region> -NewSecurityWorldPackage <BYOK-SecurityWorld-pkg-Region>
    ```
    Ad esempio, per l'America del Nord: **KeyTransferRemote.exe -ImportRmsCentrallyManagedKey -TpdFilePath E:\contosokey1.xml -ProtectionPassword -KeyIdentifier contosorms1key –- -ExchangeKeyPackage &lt;BYOK-KEK-pka-NA-1&gt; -NewSecurityWorldPackage &lt;BYOK-SecurityWorld-pkg-NA-1&gt;**

    Informazioni aggiuntive:

    -   Il parametro ImportRmsCentrallyManagedKey indica che l'operazione consiste nell'importazione della chiave del certificato concessore di licenze server.

    -   Se non si specifica la password nel comando, verrà richiesto di farlo.

    -   Il parametro KeyIdentifier riguarda un nome descrittivo della chiave che crea il nome del file di chiave. È necessario usare solo caratteri ASCII minuscoli.

    -   Il parametro ExchangeKeyPackage indica un pacchetto di chiavi per lo scambio delle chiavi specifico dell'area geografica, il cui nome inizia con BYOK-KEK-pkg-.

    -   Il parametro NewSecurityWorldPackage indica un pacchetto di sicurezza di livello universale specifico dell'area geografica, il cui nome inizia con BYOK-SecurityWorld-pkg-.

    Questo comando produce quanto segue:

    -   File di chiave del modulo di protezione hardware: %NFAST_KMDATA%\local\key_mscapi_&lt;KeyID&gt;

    -   File di dati di configurazione di RMS con SLC rimosso: %NFAST_KMDATA%\local\no_key_tpd_&lt;KeyID&gt;.xml

3.  Se è disponibile più di un file di dati di configurazione di RMS, ripetere il passaggio 2 per il file restanti.

Dopo l'estrazione del certificato concessore di licenze server (SLC) in modo da avere una chiave basata sul modulo di protezione hardware, è possibile creare il pacchetto e trasferirlo in Azure RMS.

## Parte 2: Creare il pacchetto e trasferire la chiave del modulo di protezione hardware in Azure RMS

1.  Seguire i passaggi seguenti della sezione [Implementazione della modalità BYOK](plan-implement-tenant-key.md#BKMK_ImplementBYOK) di [Pianificazione e implementazione della chiave del tenant di Azure Rights Management](plan-implement-tenant-key.md):

    -   **Generare e trasferire la propria chiave del tenant tramite Internet**: **Preparare la chiave del tenant per il trasferimento**

    -   **Generare e trasferire la propria chiave del tenant tramite Internet**: **Trasferire la chiave del tenant ad Azure RMS**

Dopo avere trasferito la chiave del modulo di protezione hardware in Azure RMS, è possibile importare i dati di configurazione di AD RMS, che contengono solo un puntatore alla chiave del tenant appena trasferita.

## Parte 3: Importare i dati di configurazione in Azure RMS

1.  Sempre nella workstation connessa a Internet e nella sessione di Windows PowerShell, copiare i file di configurazione di RMS con SLC rimosso (dalla workstation disconnessa, %NFAST_KMDATA%\local\no_key_tpd_&lt;KeyID&gt;.xml)

2.  Caricare il primo file. Se si hanno più un file XML, perché avevi più domini di pubblicazione trusted, scegliere il file che contiene il dominio di pubblicazione trusted esportato che corrisponde alla chiave di HSM che si desidera utilizzare in Azure RMS per proteggere il contenuto dopo la migrazione. Utilizzare il seguente comando:

    ```
    Import-AadrmTpd -TpdFile <PathToNoKeyTpdPackageFile> -ProtectionPassword -HsmKeyFile <PathToKeyTransferPackage> -Active $true -Verbose
    ```
    Ad esempio: **Import -TpdFile E:\no_key_tpd_contosorms1key.xml -ProtectionPassword -HsmKeyFile E:\KeyTransferPackage-contosorms1key.byok -Active $true -Verbose**

    Quando richiesto, immettere la password specificata in precedenza e confermare che si desidera eseguire questa azione.

3.  Al termine del comando, ripetere il passaggio 2 per ogni restante file XML creato esportando il tuo domini di pubblicazione trusted. Per questi file impostare **-Active** su **false** quando si esegue il comando di importazione. Ad esempio: **Import -TpdFile E:\no_key_tpd_contosorms2key.xml -ProtectionPassword -HsmKeyFile E:\KeyTransferPackage-contosorms1key.byok -Active $false -Verbose**

4.  Usare il cmdlet [Disconnect-AadrmService](http://msdn.microsoft.com/library/windowsazure/dn629416.aspx) per disconnettersi dal servizio Azure RMS:

    ```
    Disconnect-AadrmService
    ```

È ora possibile andare al [Passaggio 3. Attivare il tenant di RMS](migrate-from-ad-rms-to-azure-rms.md#BKMK_Step3Migration).




<!--HONumber=Apr16_HO4-->


