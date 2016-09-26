---
title: Passaggio 2&colon; Migrazione da una chiave protetta tramite software a un'altra | Azure RMS
description: "Istruzioni che fanno parte del percorso di migrazione da AD RMS ad Azure Rights Management e si applicano solo se la chiave di AD RMS è protetta tramite software e si vuole eseguire la migrazione ad Azure Rights Management con una chiave del tenant protetta tramite software."
author: cabailey
manager: mbaldwin
ms.date: 09/14/2016
ms.topic: article
ms.prod: 
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 81a5cf4f-c1f3-44a9-ad42-66e95f33ed27
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 459cbe65741ea415defced844034f62cfd4654ed
ms.openlocfilehash: 2bd9abcac99a06a29e5dacdd014e660358840adc


---


# Passaggio 2: Migrazione da una chiave protetta tramite software a un'altra

>*Si applica a: Active Directory Rights Management Services, Azure Rights Management*


Queste istruzioni fanno parte del [percorso di migrazione da AD RMS ad Azure Rights Management](migrate-from-ad-rms-to-azure-rms.md) e si applicano solo se la chiave di AD RMS è protetta tramite software e si vuole eseguire la migrazione ad Azure Rights Management con una chiave del tenant protetta tramite software. 

Se non si tratta dello scenario di configurazione prescelto, tornare al [Passaggio 2. Esportare i dati di configurazione da AD RMS e importarli in Azure RMS](migrate-from-ad-rms-phase1.md#step-2-export-configuration-data-from-ad-rms-and-import-it-to-azure-rms), quindi scegliere una configurazione diversa.

Usare la procedura seguente per importare la configurazione di AD RMS in Azure RMS. La chiave del tenant di Azure RMS verrà gestita da Microsoft.

## Per importare i dati di configurazione in Azure RMS

1.  In una workstation connessa a Internet scaricare e installare il modulo Windows PowerShell per Azure RMS (versione minima 2.5.0.0), che include il cmdlet [Import-AadrmTpd](http://msdn.microsoft.com/library/azure/dn857523.aspx).

    > [!TIP]
    > Se il modulo è stato scaricato e installato in precedenza, verificarne il numero di versione eseguendo il comando seguente: `(Get-Module aadrm -ListAvailable).Version`

    Per istruzioni di installazione, vedere [Installazione di Windows PowerShell per Azure Rights Management](../deploy-use/install-powershell.md).

2.  Avviare Windows PowerShell con l'opzione **Esegui come amministratore** e usare il cmdlet [Connect-AadrmService](http://msdn.microsoft.com/library/azure/dn629415.aspx) per connettersi al servizio Azure RMS:

    ```
    Connect-AadrmService
    ```
    Quando richiesto, immettere le credenziali dell'amministratore del tenant [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)]. In genere, viene usato un account amministratore globale per Azure Active Directory o Office 365.

3.  Usare il cmdlet [Import-AadrmTpd](http://msdn.microsoft.com/library/azure/dn857523.aspx) per caricare il file del primo dominio di pubblicazione trusted esportato (file con estensione xml). Se si hanno più file XML, perché avevi più domini di pubblicazione trusted, scegliere il file che contiene il dominio di pubblicazione trusted esportato che si desidera utilizzare in Azure RMS per proteggere il contenuto dopo la migrazione. Utilizzare il seguente comando:

    ```
    Import-AadrmTpd -TpdFile <PathToTpdPackageFile> -ProtectionPassword <secure string> -Active $True -Verbose
    ```
    È possibile usare [ConvertTo-SecureString - AsPlaintext](https://technet.microsoft.com/library/hh849818.aspx) o [Read-Host](https://technet.microsoft.com/library/hh849945.aspx) per specificare la password come stringa sicura. Quando si usa ConvertTo-SecureString e la password contiene caratteri speciali, immettere la password tra virgolette singole o caratteri speciali di escape.
    
    Ad esempio:eseguire innanzitutto **$TPD_Password = Read-Host - AsSecureString** e immettere la password specificata in precedenza. Eseguire quindi **Import-AadrmTpd -TpdFile E:\contosokey1.xml -ProtectionPassword $TPD_Password -Active $true -Verbose**. Quando richiesto, confermare che si vuole eseguire questa azione.
    
4.  Al termine del comando, ripetere il passaggio 3 per ogni restante file con estensione xml creato esportando i propri domini di pubblicazione trusted. Per questi file impostare **-Active** su **false** quando si esegue il comando di importazione. Ad esempio: **Import-AadrmTpd -TpdFile E:\contosokey2.xml -ProtectionPassword $TPD_Password -Active $false -Verbose**

5.  Usare il cmdlet [Disconnect-AadrmService](http://msdn.microsoft.com/library/azure/dn629416.aspx) per disconnettersi dal servizio Azure RMS:

    ```
    Disconnect-AadrmService
    ```


È ora possibile andare al [Passaggio 3. Attivare il tenant di RMS](migrate-from-ad-rms-phase1.md#step-3-activate-your-rms-tenant).





<!--HONumber=Sep16_HO2-->

