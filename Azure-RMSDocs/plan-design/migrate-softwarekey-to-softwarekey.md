---
title: Passaggio 2&colon; Migrazione da una chiave protetta tramite software a un&quot;altra | Azure Information Protection
description: "Istruzioni che fanno parte del percorso di migrazione da AD RMS ad Azure Information Protection e si applicano solo se la chiave di AD RMS è protetta tramite software e si vuole eseguire la migrazione ad Azure Information Protection con una chiave del tenant protetta tramite software."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 11/23/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 81a5cf4f-c1f3-44a9-ad42-66e95f33ed27
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 5aac7b9fae12642c9846a70c5d271c7600af4096
ms.openlocfilehash: 07b2a94625f006c07f72c543488f69d4cae3a9ec


---


# <a name="step-2-software-protected-key-to-software-protected-key-migration"></a>Passaggio 2: Migrazione da una chiave protetta tramite software a un'altra

>*Si applica a: Active Directory Rights Management Services, Azure Information Protection, Office 365*


Queste istruzioni fanno parte del [percorso di migrazione da AD RMS ad Azure Information Protection](migrate-from-ad-rms-to-azure-rms.md) e si applicano solo se la chiave di AD RMS è protetta tramite software e si vuole eseguire la migrazione ad Azure Information Protection con una chiave del tenant protetta tramite software. 

Se non si tratta dello scenario di configurazione prescelto, tornare al [Passaggio 2. Esportare i dati di configurazione da AD RMS e importarli in Azure RMS](migrate-from-ad-rms-phase1.md#step-2-export-configuration-data-from-ad-rms-and-import-it-to-azure-information-protection), quindi scegliere una configurazione diversa.

Usare la procedura seguente per importare la configurazione di AD RMS in Azure Information Protection. La chiave del tenant di Azure Information Protection verrà gestita da Microsoft.

## <a name="to-import-the-configuration-data-to-azure-information-protection"></a>Per importare i dati di configurazione in Azure Information Protection

1.  In una workstation connessa a Internet scaricare e installare il modulo Windows PowerShell per Azure Rights Management (versione minima 2.5.0.0), che include il cmdlet [Import-AadrmTpd](http://msdn.microsoft.com/library/azure/dn857523.aspx). Il servizio Azure Rights Management (Azure RMS) assicura la protezione per Azure Information Protection.

    > [!TIP]
    > Se il modulo è stato scaricato e installato in precedenza, verificarne il numero di versione eseguendo il comando seguente: `(Get-Module aadrm -ListAvailable).Version`

    Per istruzioni di installazione, vedere [Installazione di Windows PowerShell per Azure Rights Management](../deploy-use/install-powershell.md).

2.  Avviare Windows PowerShell con l'opzione **Esegui come amministratore** e usare il cmdlet [Connect-AadrmService](http://msdn.microsoft.com/library/azure/dn629415.aspx) per connettersi al servizio Azure RMS:

    ```
    Connect-AadrmService
    ```
    Quando richiesto, immettere le credenziali dell'amministratore del tenant [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)]. In genere, viene usato un account amministratore globale per Azure Active Directory o Office 365.

3.  Usare il cmdlet [Import-AadrmTpd](http://msdn.microsoft.com/library/azure/dn857523.aspx) per caricare il file del primo dominio di pubblicazione trusted esportato (file con estensione xml). Se si hanno più file con estensione xml, perché erano disponibili più domini di pubblicazione trusted, scegliere il file contenente il dominio di pubblicazione trusted esportato che si vuole usare in Azure Information Protection per proteggere il contenuto dopo la migrazione. Utilizzare il seguente comando:

    ```
    Import-AadrmTpd -TpdFile <PathToTpdPackageFile> -ProtectionPassword <secure string> -Active $True -Verbose
    ```
    È possibile usare [ConvertTo-SecureString - AsPlaintext](https://technet.microsoft.com/library/hh849818.aspx) o [Read-Host](https://technet.microsoft.com/library/hh849945.aspx) per specificare la password come stringa sicura. Quando si usa ConvertTo-SecureString e la password contiene caratteri speciali, immettere la password tra virgolette singole o caratteri speciali di escape.
    
    Ad esempio:eseguire innanzitutto **$TPD_Password = Read-Host - AsSecureString** e immettere la password specificata in precedenza. Eseguire quindi **Import-AadrmTpd -TpdFile E:\contosokey1.xml -ProtectionPassword $TPD_Password -Active $true -Verbose**. Quando richiesto, confermare che si vuole eseguire questa azione.
    
4.  Al termine del comando, ripetere il passaggio 3 per ogni restante file con estensione xml creato esportando i propri domini di pubblicazione trusted. Ad esempio, è necessario avere almeno un file aggiuntivo da importare in caso di aggiornamento del cluster AD RMS per la modalità di crittografia 2. Per questi file impostare **-Active** su **false** quando si esegue il comando di importazione. Ad esempio: **Import-AadrmTpd -TpdFile E:\contosokey2.xml -ProtectionPassword $TPD_Password -Active $false -Verbose**

5.  Usare il cmdlet [Disconnect-AadrmService](http://msdn.microsoft.com/library/azure/dn629416.aspx) per disconnettersi dal servizio Azure Rights Management:

    ```
    Disconnect-AadrmService
    ```


È ora possibile andare al [Passaggio 3. Attivare il tenant di Azure Information Protection](migrate-from-ad-rms-phase1.md#step-3-activate-your-azure-information-protection-tenant).





<!--HONumber=Nov16_HO4-->


