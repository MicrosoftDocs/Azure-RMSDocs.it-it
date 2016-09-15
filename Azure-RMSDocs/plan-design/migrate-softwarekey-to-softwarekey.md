---
title: Passaggio 2&colon; Migrazione da una chiave protetta tramite software a un'altra | Azure RMS
description: "Istruzioni che fanno parte del percorso di migrazione da AD RMS ad Azure Rights Management e si applicano solo se la chiave di AD RMS è protetta tramite software e si vuole eseguire la migrazione ad Azure Rights Management con una chiave del tenant protetta tramite software."
author: cabailey
manager: mbaldwin
ms.date: 08/25/2016
ms.topic: article
ms.prod: 
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 81a5cf4f-c1f3-44a9-ad42-66e95f33ed27
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: ada00b6f6298e7d359c73eb38dfdac169eacb708
ms.openlocfilehash: 5ec3d2b275521807c6fd8f9ccfe1136db97d5d79


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
    Import-AadrmTpd -TpdFile <PathToTpdPackageFile> -ProtectionPassword -Active $True -Verbose
    ```
    Ad esempio: **Import-AadrmTpd -TpdFile E:\contosokey1.xml -ProtectionPassword -Active $true -Verbose**

    Quando richiesto, immettere la password specificata in precedenza e confermare che si desidera eseguire questa azione.

4.  Al termine del comando, ripetere il passaggio 3 per ogni restante file con estensione xml creato esportando i propri domini di pubblicazione trusted. Per questi file impostare **-Active** su **false** quando si esegue il comando di importazione. Ad esempio: **Import-AadrmTpd -TpdFile E:\contosokey2.xml -ProtectionPassword -Active $false -Verbose**

5.  Usare il cmdlet [Disconnect-AadrmService](http://msdn.microsoft.com/library/azure/dn629416.aspx) per disconnettersi dal servizio Azure RMS:

    ```
    Disconnect-AadrmService
    ```


È ora possibile andare al [Passaggio 3. Attivare il tenant di RMS](migrate-from-ad-rms-phase1.md#step-3-activate-your-rms-tenant).





<!--HONumber=Aug16_HO4-->


