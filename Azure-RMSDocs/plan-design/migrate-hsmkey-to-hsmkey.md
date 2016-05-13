---
# required metadata

title: Passaggio 2&colon; Migrazione da una chiave protetta tramite HSM a un'altra | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: c5bbf37e-f1bf-4010-a60f-37177c9e9b39

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Passaggio 2: Migrazione da una chiave protetta tramite HSM a un'altra

Queste istruzioni fanno parte del [percorso di migrazione da AD RMS ad Azure Rights Management](migrate-from-ad-rms-to-azure-rms.md) e si applicano solo se la chiave di AD RMS è protetta tramite HSM e se si vuole eseguire la migrazione ad Azure Rights Management con una chiave del tenant protetta tramite HSM. 

Se non si tratta dello scenario di configurazione prescelto, tornare al [Passaggio 2. Esportare i dati di configurazione da AD RMS e importarli in Azure RMS](migrate-from-ad-rms-to-azure-rms.md#step-2-export-configuration-data-from-ad-rms-and-import-it-to-azure-rms), quindi scegliere una configurazione diversa.

> [!NOTE]
> Queste istruzioni presuppongono che la chiave di AD RMS sia protetta da modulo. Questa è la situazione comune. Se la chiave di AD RMS è protetta tramite OCS, contattare il team all'indirizzo [AskIPTeam@microsoft.com](mailto: askipteam@microsoft.com?subject=AD%20RMS%20migration%20with%20OCS-protected%20key) prima di eseguire queste istruzioni.

Questa procedura in due parti consente di importare la chiave HSM e la configurazione di AD RMS in Azure RMS. La chiave del tenant di Azure RMS verrà gestita dall'utente (BYOK).

Innanzitutto è necessario creare il pacchetto e la chiave HSM in modo che sia pronta da trasferire in Azure RMS e quindi importarla con i dati di configurazione.

## Parte 1: Il pacchetto della chiave HSM è quindi pronto per essere trasferito ad Azure RMS

1.  Seguire la procedura riportata nella sezione [Implementazione della modalità BYOK](plan-implement-tenant-key.md#BKMK_ImplementBYOK) dell'argomento [Pianificazione e implementazione della chiave del tenant di Azure Rights Management](plan-implement-tenant-key.md), usando la procedura **Generare e trasferire la propria chiave del tenant tramite Internet** con le eccezioni seguenti:

    -   Non seguire la procedura per **generare la chiave del tenant**, perché ne esiste già una equivalente nella distribuzione di AD RMS. È necessario identificare la chiave usata dal server AD RMS dall'installazione di Thales e usare questa chiave durante la migrazione. I file di chiave crittografati di Thales sono in genere denominati **key_(keyAppName)_(keyIdentifier)** in locale nel server.

    -   Non seguire la procedura per **trasferire la chiave del tenant ad Azure RMS**, che usa il comando Add-AadrmKey.  Al contrario, la chiave HSM preparata verrà trasferita quando si caricherà il dominio di pubblicazione attendibile esportato, utilizzando il comando Import-AadrmTpd.

2.  Nella workstation connessa a Internet, nella sessione PowerShell di Windows, riconnettersi al servizio Azure RMS.

Ora che la chiave HSM è stata preparata per Azure RMS, si è pronti per importare i file di chiave HSM e dati di configurazione di AD RMS.

## Parte 2: Importare i dati di configurazione e la chiave HSM ad Azure RMS

1.  Ancora sulla workstation connettersi a Internet e nella sessione di Windows PowerShell, caricare il primo file di dominio (. Xml) attendibile esportato editrice. Se si hanno più un file XML, perché avevi più domini di pubblicazione trusted, scegliere il file che contiene il dominio di pubblicazione trusted esportato che corrisponde alla chiave di HSM che si desidera utilizzare in Azure RMS per proteggere il contenuto dopo la migrazione. Utilizzare il seguente comando:

    ```
    Import-AadrmTpd -TpdFile <PathToTpdPackageFile> -ProtectionPassword -HsmKeyFile <PathToBYOKPackage> -Active $True -Verbose
    ```
    Ad esempio: **Import -TpdFile E:\no_key_tpd_contosokey1.xml  -HsmKeyFile E:\KeyTransferPackage-contosokey.byok -ProtectionPassword -Active $true -Verbose**

    Quando richiesto, immettere la password specificata in precedenza e confermare che si desidera eseguire questa azione.

2.  Al termine del comando, ripetere il passaggio 1 per ogni restante file XML creato esportando il tuo domini di pubblicazione trusted. Per questi file impostare **-Active** su **false** quando si esegue il comando di importazione.  Ad esempio: **Import -TpdFile E:\contosokey2.xml -HsmKeyFile E:\KeyTransferPackage-contosokey.byok -ProtectionPassword -Active $false -Verbose**

3.  Usare il cmdlet [Disconnect-AadrmService](http://msdn.microsoft.com/library/windowsazure/dn629416.aspx) per disconnettersi dal servizio Azure RMS:

    ```
    Disconnect-AadrmService
    ```

È ora possibile andare al [Passaggio 3. Attivare il tenant di RMS](migrate-from-ad-rms-to-azure-rms.md#BKMK_Step3Migration).



<!--HONumber=Apr16_HO3-->


