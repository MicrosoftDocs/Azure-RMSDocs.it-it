---
title: Installare PowerShell per AADRM - AIP
description: Istruzioni per l'installazione di Windows PowerShell per il servizio Azure Rights Management di Azure Information Protection. Il nome di questo modulo è AADRM.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 12/12/2018
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 0d665ed6-b1de-4d63-854a-bc57c1c49844
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 789c3178827e52c27759268b1340b53c3add1c39
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/14/2019
ms.locfileid: "56259712"
---
# <a name="installing-the-aadrm-powershell-module"></a>Installazione del modulo PowerShell AADRM

>*Si applica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

Usare le istruzioni seguenti per l'installazione del modulo Windows PowerShell per il servizio Azure Rights Management da Azure Information Protection. Il nome di questo modulo è AADRM.

È possibile usare questo modulo di PowerShell per amministrare il servizio Azure Rights Management dalla riga di comando usando qualsiasi computer dotato di connessione a Internet e che soddisfa i prerequisiti elencati nella sezione seguente. Windows PowerShell per Azure Rights Management supporta l'uso di script per l'automazione oppure può essere necessario per scenari di configurazione avanzata. Per altre informazioni sulle attività di amministrazione e sulle configurazioni supportate dal modulo, vedere l'articolo relativo all'[amministrazione di Azure Rights Management tramite Windows PowerShell](administer-powershell.md).

## <a name="prerequisites"></a>Prerequisiti
Questa tabella elenca i prerequisiti per installare e usare il modulo PowerShell AADRM per il servizio Azure Rights Management di Azure Information Protection.

|Requisito|Altre informazioni|
|---------------|--------------------|
|Versione minima di Windows PowerShell: 3.0|È possibile verificare quale versione di Windows PowerShell sia in esecuzione digitando `$PSVersionTable` in una sessione di PowerShell. <br /><br /> Se è necessario installare una versione successiva di Windows PowerShell, vedere [Aggiornamento di Windows PowerShell esistente](/powershell/scripting/setup/installing-windows-powershell#upgrading-existing-windows-powershell).|
|Versione minima di Microsoft .NET Framework: 4.5<br /><br />Nota: Questa versione di Microsoft .NET Framework è inclusa nei sistemi operativi successivi. È pertanto necessario installarla manualmente se il sistema operativo client è inferiore a Windows 8.0 o se il sistema operativo server è inferiore a Windows Server 2012.|Se la versione minima di Microsoft .NET Framework non è ancora installata, è possibile scaricare [Microsoft .NET Framework 4.5](https://www.microsoft.com/download/details.aspx?id=30653).<br /><br />La versione minima di Microsoft .NET Framework è necessaria per alcune classi usate dal modulo AADRM.|

A partire dalla versione 2.5.0.0 del modulo AADRM, l'Assistente per l'accesso ai Microsoft Online Services non è più necessario.

> [!NOTE]
> 
> Se si è installata una versione del modulo AADRM con Azure Rights Management Administration Tool, usare **Programmi e funzionalità** per disinstallare **Amministrazione di Windows Azure AD Rights Management** prima di installare l'ultima versione del modulo AADRM da PowerShell Gallery.


## <a name="how-to-install-the-aadrm-module"></a>Come installare il modulo AADRM

Il modulo AADRM è stato spostato in [PowerShell Gallery](/powershell/gallery/readme) e non è più disponibile nell'Area download Microsoft. 

### <a name="to-install-the-aadrm-module-from-the-powershell-gallery"></a>Per installare il modulo AADRM da PowerShell Gallery

Se non si ha familiarità con PowerShell Gallery, vedere [Introduzione a PowerShell Gallery](/powershell/gallery/psgallery/psgallery_gettingstarted). Seguire le istruzioni per i requisiti della raccolta, che includono l'installazione del modulo PowerShellGet e del provider NuGet.

Per visualizzare i dettagli del modulo AADRM in PowerShell Gallery, consultare la [pagina AADRM](https://www.powershellgallery.com/packages/AADRM).

Per installare il modulo AADRM, avviare una sessione di PowerShell con l'opzione **Esegui come amministratore** e digitare:

    Install-Module -Name AADRM

Se si riceve un avviso relativo all'installazione da un repository non attendibile, è possibile premere Y per confermare. In alternativa, premere N e configurare PowerShell Gallery come repository attendibile usando il comando `Set-PSRepository -Name PSGallery -InstallationPolicy Trusted` e quindi eseguire di nuovo il comando per l'installazione del modulo AADRM.  

Se si dispone di una versione precedente del modulo AADRM installata da PowerShell Gallery, aggiornarlo all'ultima versione digitando:

    Update-Module -Name AADRM


## <a name="next-steps"></a>Passaggi successivi
In una sessione di Windows PowerShell verificare la versione del modulo installato. Questo controllo è particolarmente importante se si è eseguito l'aggiornamento da una versione precedente:

```
(Get-Module AADRM –ListAvailable).Version
```

Nota: se questo comando non riesce, eseguire prima **Import-Module AADRM**.

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

-   Elenco dei principali scenari di configurazione che supportano PowerShell: [Amministrazione di Azure Rights Management mediante Windows PowerShell](administer-powershell.md)

Prima di poter eseguire i comandi che consentono di configurare il servizio Azure Rights Management, è necessario connettersi al servizio usando il cmdlet [Connect-AadrmService](/powershell/aadrm/vlatest/connect-aadrmservice). Al termine dell'esecuzione dei comandi di configurazione, è consigliabile disconnettersi dal servizio usando il cmdlet [Disconnect-AadrmService](/powershell/aadrm/vlatest/disconnect-aadrmservice). Se non ci si disconnette, la connessione viene interrotta automaticamente dopo un periodo di inattività. A causa della disconnessione automatica, si noterà che ogni tanto è necessario riconnettersi a una sessione di PowerShell. 

> [!NOTE]
> Se il servizio Azure Rights Management non è stato ancora attivato, attivarlo usando il cmdlet [Enable-Aadrm](/powershell/aadrm/vlatest/enable-aadrm) dopo essersi connessi al servizio.

