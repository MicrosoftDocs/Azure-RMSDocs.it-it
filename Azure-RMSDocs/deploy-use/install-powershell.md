---
title: Installare PowerShell per AADRM - AIP
description: "Istruzioni per l'installazione di Windows PowerShell per il servizio Azure Rights Management di Azure Information Protection. Il nome di questo modulo è AADRM."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/20/2018
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 0d665ed6-b1de-4d63-854a-bc57c1c49844
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 757901d4c16b36dfe14e31f5ab9910c47b0b1917
ms.sourcegitcommit: 31c79d948ec3089a4dc65639f1842c07c7aecba6
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/20/2018
---
# <a name="installing-the-aadrm-powershell-module"></a>Installazione del modulo PowerShell AADRM

>*Si applica a: Azure Information Protection, Office 365*

Usare le istruzioni seguenti per l'installazione del modulo Windows PowerShell per il servizio Azure Rights Management di Azure Information Protection. Il nome di questo modulo è AADRM.

È possibile usare questo modulo di PowerShell per amministrare il servizio Azure Rights Management dalla riga di comando usando qualsiasi computer dotato di connessione a Internet e che soddisfa i prerequisiti elencati nella sezione seguente. Windows PowerShell per [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] supporta l'uso di script per l'automazione oppure può essere necessario per scenari di configurazione avanzata. Per altre informazioni sulle attività di amministrazione e sulle configurazioni supportate dal modulo, vedere l'articolo relativo all'[amministrazione di Azure Rights Management tramite Windows PowerShell](administer-powershell.md).

## <a name="prerequisites"></a>Prerequisiti
Questa tabella elenca i prerequisiti per installare e usare il modulo PowerShell AADRM per il servizio Azure Rights Management di Azure Information Protection.

|Requisito|Altre informazioni|
|---------------|--------------------|
|Versione minima di Windows PowerShell: 3.0|È possibile verificare quale versione di Windows PowerShell sia in esecuzione digitando `$PSVersionTable` in una sessione di PowerShell. <br /><br /> Se è necessario installare una versione successiva di Windows PowerShell, vedere [Aggiornamento di Windows PowerShell esistente](/powershell/scripting/setup/installing-windows-powershell#upgrading-existing-windows-powershell).|
|Versione minima di Microsoft .NET Framework: 4.5<br /><br />Nota: questa versione di Microsoft .NET Framework è inclusa nei sistemi operativi successivi. È pertanto necessario installarla manualmente solo se il sistema operativo client è inferiore a Windows 8.0 o se il sistema operativo server è inferiore a Windows Server 2012.|Se la versione minima di Microsoft .NET Framework non è ancora installata, è possibile scaricare [Microsoft .NET Framework 4.5](http://www.microsoft.com/download/details.aspx?id=30653).<br /><br />La versione minima di Microsoft .NET Framework è necessaria per alcune classi usate dal modulo AADRM.|

> [!NOTE]
> A partire dalla versione 2.5.0.0 del modulo AADRM, l'Assistente per l'accesso ai Microsoft Online Services non è più necessario.
> 
> Se è installata una versione precedente del modulo AADRM, usare **Programmi e funzionalità** per disinstallare **Amministrazione di Windows Azure AD Rights Management** prima di installare la versione più recente.


## <a name="how-to-install-the-aadrm-module"></a>Come installare il modulo AADRM

Il modulo AADRM sta migrando a [PowerShell Gallery](/powershell/gallery/readme), ma per un periodo di tempo limitato è disponibile anche nel Microsoft Download Center. 

### <a name="to-install-the-aadrm-module-from-the-powershell-gallery"></a>Per installare il modulo AADRM da PowerShell Gallery

Se non si ha familiarità con PowerShell Gallery, vedere [Introduzione a PowerShell Gallery](/powershell/gallery/psgallery/psgallery_gettingstarted). Seguire le istruzioni per i requisiti della raccolta, che includono l'installazione del modulo PowerShellGet e del provider NuGet.

Per visualizzare i dettagli del modulo AADRM in PowerShell Gallery, consultare la [pagina AADRM](https://www.powershellgallery.com/packages/AADRM).

Per installare il modulo AADRM, avviare una sessione di PowerShell e digitare:

    Install-Module -Name AADRM


### <a name="to-install-the-aadrm-module-from-the-microsoft-download-center"></a>Per installare il modulo AADRM dall'Area download Microsoft

1. Passare all'Area download Microsoft e individuare [Azure Rights Management Administration Tool](https://go.microsoft.com/fwlink/?LinkId=257721), contenente il modulo di amministrazione di [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] per Windows PowerShell.

2. Scaricare e salvare il file del programma di installazione [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)], **WindowsAzureADRightsManagementAdministration_x64**. Quindi fare doppio clic su questo file per avviare l'installazione guidata di Amministrazione di Azure AD Rights Management.

3.  Completare la procedura guidata, che consente di installare il modulo PowerShell AADRM.

## <a name="next-steps"></a>Passaggi successivi
In una sessione di Windows PowerShell, verificare la versione del modulo installato. Questo controllo è particolarmente importante se si è eseguito l'aggiornamento da una versione precedente:

```
(Get-Module AADRM –ListAvailable).Version
```

Nota: se questo comando non riesce, eseguire innanzitutto **Import-Module AADRM**.

Per visualizzare i cmdlet disponibili, digitare quanto segue:

```
Get-Command -Module AADRM
```

Usare il comando `Get-Help <cmdlet_name>` per visualizzare le informazioni della Guida per un cmdlet specifico e quindi impostare il parametro **-online** per visualizzare le informazioni della Guida più recenti dal sito della documentazione Microsoft. Ad esempio:

```
Get-Help Connect-AadrmService -online
```

Per altre informazioni:

-   Elenco completo dei cmdlet disponibili: [Modulo AADRM](/powershell/aadrm/vlatest/rightsmanagement)

-   Elenco dei principali scenari di configurazione che supportano PowerShell: [Amministrazione del servizio Azure Rights Management tramite Windows PowerShell](administer-powershell.md)

Prima di poter eseguire i comandi che consentono di configurare il servizio [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)], è necessario connettersi al servizio usando il cmdlet [Connect-AadrmService](/powershell/aadrm/vlatest/connect-aadrmservice). Al termine dell'esecuzione dei comandi di configurazione, è consigliabile disconnettersi dal servizio usando il cmdlet [Disconnect-AadrmService](/powershell/aadrm/vlatest/disconnect-aadrmservice). Se non ci si disconnette, la connessione viene interrotta automaticamente dopo un periodo di inattività. A causa della disconnessione automatica, si noterà che ogni tanto è necessario riconnettersi a una sessione di PowerShell. 

> [!NOTE]
> Se il servizio Azure Rights Management non è stato ancora attivato, attivarlo usando il cmdlet [Enable-Aadrm](/powershell/aadrm/vlatest/enable-aadrm) dopo essersi connessi al servizio.


[!INCLUDE[Commenting house rules](../includes/houserules.md)]