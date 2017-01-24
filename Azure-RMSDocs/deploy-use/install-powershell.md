---
title: Installazione di Windows PowerShell per Azure Rights Management | Azure Information Protection
description: "Istruzioni per l&quot;installazione di Windows PowerShell per il servizio Azure Rights Management di Azure Information Protection. Il nome di questo modulo è AADRM."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 09/25/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 0d665ed6-b1de-4d63-854a-bc57c1c49844
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 7068e0529409eb783f16bc207a17be27cd5d82a8
ms.openlocfilehash: 11f884779316626f81b3f75b9562ce58646f6ba3


---

# <a name="installing-windows-powershell-for-azure-rights-management"></a>Installazione di Windows PowerShell per Microsoft Azure Rights Management

>*Si applica a: Azure Information Protection, Office 365*

Usare le istruzioni seguenti per l'installazione del modulo Windows PowerShell per il servizio Azure Rights Management di Azure Information Protection.

È possibile usare questo modulo di PowerShell per amministrare il servizio Azure Rights Management dalla riga di comando usando qualsiasi computer dotato di connessione a Internet e che soddisfa i prerequisiti elencati nella sezione seguente. Windows PowerShell per [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] supporta l'uso di script per l'automazione oppure può essere necessario per scenari di configurazione avanzata. Per altre informazioni sulle attività di amministrazione e sulle configurazioni supportate dal modulo, vedere l'articolo relativo all'[amministrazione di Azure Rights Management tramite Windows PowerShell](administer-powershell.md).

## <a name="prerequisites"></a>Prerequisiti
Questa tabella elenca i prerequisiti per l'installazione e l'uso di Windows PowerShell per [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)].

|Requisito|Altre informazioni|
|---------------|--------------------|
|Una versione di Windows in grado di supportare il modulo di amministrazione di [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)]|Controllare l'elenco dei sistemi operativi supportati nella sezione **Requisiti di sistema** della [pagina di download per Azure Rights Management Administration Tool](http://go.microsoft.com/fwlink/?LinkId=257721).|
|Versione minima di Windows PowerShell: 2.0|Il supporto per il modulo di amministrazione di [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] è stato introdotto per la prima volta in Windows PowerShell 2.0.<br /><br />Per impostazione predefinita, con la maggior parte dei sistemi operativi Windows viene installata almeno la versione 2.0 di Windows PowerShell. Se è necessario installare Windows PowerShell 2.0, vedere [Installare Windows PowerShell 2.0](http://msdn.microsoft.com/library/ff637750.aspx).<br /><br />Suggerimento: è possibile verificare quale versione di Windows PowerShell sia in esecuzione digitando `$PSVersionTable` in una sessione di PowerShell.|
|Versione minima di Microsoft .NET Framework: 4.5<br /><br />Nota: questa versione di Microsoft .NET Framework è inclusa nei sistemi operativi successivi. È pertanto necessario installarla manualmente solo se il sistema operativo client è inferiore a Windows 8.0 o se il sistema operativo server è inferiore a Windows Server 2012.|Se la versione minima di Microsoft .NET Framework non è ancora installata, è possibile scaricare [Microsoft .NET Framework 4.5](http://www.microsoft.com/download/details.aspx?id=30653).<br /><br />La versione minima di Microsoft .NET Framework è necessaria per alcune classi usate dal modulo di amministrazione di [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)].|

> [!NOTE]
> A partire dalla versione 2.5.0.0 del modulo di amministrazione di Rights Management, l'Assistente per l'accesso ai Microsoft Online Services non è più necessario.
> 
> Se è installata una versione precedente del modulo di amministrazione di Rights Management, usare **Programmi e funzionalità** per disinstallare **Amministrazione di Windows Azure AD Rights Management** prima di installare la versione più recente.


## <a name="how-to-install-the-rights-management-administration-module"></a>Come installare il modulo di amministrazione di Rights Management

1.  Passare all'Area download Microsoft e [scaricare Azure Rights Management Administration Tool](https://go.microsoft.com/fwlink/?LinkId=257721), contenente il modulo di amministrazione di [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] per Windows PowerShell.

2.  Nella cartella locale in cui è stato scaricato e salvato il file del programma di installazione di [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] fare doppio clic sul file eseguibile scaricato per la propria piattaforma (WindowsAzureADRightsManagementAdministration_x64 o WindowsAzureADRightsManagementAdministration_x86.exe) per avviare l'installazione guidata dell'amministrazione di Azure AD Rights Management.

3.  Completare la procedura guidata.

Windows PowerShell per [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] è ora installato.

## <a name="next-steps"></a>Passaggi successivi
Per visualizzare i cmdlet disponibili, avviare Windows PowerShell con l'opzione **Esegui come amministratore** e digitare quanto segue:

```
Get-Command -Module aadrm
```
Utilizzare il comando `the Get-Help <cmdlet_name>` per visualizzare le informazioni della Guida per un cmdlet specifico.

Per altre informazioni:

-   Elenco completo dei cmdlet disponibili: [Cmdlet di Azure Rights Management](https://msdn.microsoft.com/library/windowsazure/dn629398.aspx)

-   Elenco dei principali scenari di configurazione che supportano Windows PowerShell, disponibile nell'articolo relativo all'[amministrazione di Azure Rights Management tramite Windows PowerShell](administer-powershell.md)

Prima di poter eseguire i comandi che consentono di configurare il servizio [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)], è necessario connettersi al servizio usando il cmdlet [Connect-AadrmService](https://msdn.microsoft.com/library/windowsazure/dn629415.aspx). Al termine dell'esecuzione dei comandi di configurazione desiderati, disconnettersi dal servizio usando il cmdlet [Disconnect-AadrmService](https://msdn.microsoft.com/library/windowsazure/dn629416.aspx) .

> [!NOTE]
> Se il servizio Azure Rights Management non è stato ancora attivato, attivarlo usando il cmdlet [Enable-Aadrm](https://msdn.microsoft.com/library/windowsazure/dn629412.aspx) dopo essersi connessi al servizio.

## <a name="see-also"></a>Vedere anche
[Amministrazione di Azure Rights Management mediante Windows PowerShell](administer-powershell.md)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]


<!--HONumber=Jan17_HO4-->


