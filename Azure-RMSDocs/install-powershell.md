---
title: Installare il modulo AIPService PowerShell per Azure Information Protection
description: Istruzioni per installare PowerShell per il servizio di protezione di Azure Information Protection. Il nome di questo modulo è AIPService.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 07/05/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 0d665ed6-b1de-4d63-854a-bc57c1c49844
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: d6f5ccc34669781f4ec9723014d5254444255649
ms.sourcegitcommit: 849c493cef6b2578945c528f4e17373a2ef26287
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/04/2019
ms.locfileid: "67563403"
---
# <a name="installing-the-aipservice-powershell-module"></a>Installazione del modulo PowerShell AIPService

>*Si applica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

Usare le informazioni seguenti per installare il modulo Windows PowerShell per il servizio di protezione di Azure Information Protection. Il nome di questo modulo è AIPService e sostituisce la versione precedente che è stata denominata AADRM.

È possibile usare questo modulo di PowerShell per amministrare il servizio di protezione (Azure Rights Management) dalla riga di comando usando qualsiasi computer dotato di una connessione Internet e che soddisfi i prerequisiti elencati nella sezione successiva. Windows PowerShell per Azure Information Protection supporta lo scripting per l'automazione oppure può essere necessario per scenari di configurazione avanzata. Per altre informazioni sulle attività di amministrazione e le configurazioni supportate dal modulo, vedere [amministrazione protezione di Azure Information Protection tramite PowerShell](administer-powershell.md).

## <a name="prerequisites"></a>Prerequisiti
Questa tabella elenca i prerequisiti per installare e usare il modulo AIPService PowerShell per il servizio di protezione di Azure Information Protection.

|Requisito|Altre informazioni|
|---------------|--------------------|
|Versione minima di Windows PowerShell: 3.0|È possibile verificare quale versione di Windows PowerShell sia in esecuzione digitando `$PSVersionTable` in una sessione di PowerShell. <br /><br /> Se è necessario installare una versione successiva di Windows PowerShell, vedere [Aggiornamento di Windows PowerShell esistente](/powershell/scripting/setup/installing-windows-powershell#upgrading-existing-windows-powershell).|
|Versione minima di Microsoft .NET Framework: 4.5<br /><br />Nota: Questa versione di Microsoft .NET Framework è inclusa nei sistemi operativi successivi, è pertanto necessario installarla manualmente solo se il sistema operativo client è inferiore a Windows 8.0 o del sistema operativo server è inferiore a Windows Server 2012.|Se la versione minima di Microsoft .NET Framework non è ancora installata, è possibile scaricare [Microsoft .NET Framework 4.5](https://www.microsoft.com/download/details.aspx?id=30653).<br /><br />La versione minima di Microsoft .NET Framework è necessaria per alcune delle classi che usa il modulo AIPService.|

## <a name="if-you-have-the-aadrm-module-installed"></a>Se si dispone del modulo AADRM installato

Il modulo AIPService sostituisce il precedente modulo, AADRM. Se hai il precedente modulo installato, disinstallarlo e quindi installare il modulo AIPService.

Il modulo più recente ha alias ai nomi di cmdlet nel modulo precedente in modo che tutti gli script esistenti continueranno a funzionare. Tuttavia, prevede di aggiornare tali riferimenti prima il precedente modulo rientra in un supporto. Supporto per il modulo AADRM terminerà il 15 luglio 2020.

Se è installato il modulo AADRM da PowerShell Gallery, per disinstallare l'estensione, avviare una sessione di PowerShell con il **Esegui come amministratore** opzione e digitare:

    Uninstall-Module -Name AADRM

Se è installato il modulo AADRM con Azure Rights Management Administration Tool, usare **programmi e funzionalità** disinstallare **amministrazione di Microsoft Azure AD Rights Management**.

## <a name="how-to-install-the-aipservice-module"></a>Come installare il modulo AIPService

Il modulo AIPService è nel [PowerShell Gallery](/powershell/gallery/readme) e non è disponibile da Microsoft Download Center. 

### <a name="to-install-the-aipservice-module-from-the-powershell-gallery"></a>Per installare il modulo AIPService da PowerShell Gallery

Se non si ha familiarità con PowerShell Gallery, vedere [Introduzione a PowerShell Gallery](/powershell/gallery/psgallery/psgallery_gettingstarted). Seguire le istruzioni per i requisiti della raccolta, che includono l'installazione del modulo PowerShellGet e del provider NuGet.

Per visualizzare informazioni dettagliate sul modulo AIPService in PowerShell Gallery, visitare il [AIPService pagina](https://www.powershellgallery.com/packages/AIPService).

Per installare il modulo AIPService, avviare una sessione di PowerShell con il **Esegui come amministratore** opzione e digitare:

    Install-Module -Name AIPService

Se si riceve un avviso relativo all'installazione da un repository non attendibile, è possibile premere Y per confermare. Alternativa, premere N e configurare PowerShell Gallery come repository attendibile usando il comando `Set-PSRepository -Name PSGallery -InstallationPolicy Trusted` ed eseguire nuovamente il comando per installare il modulo AIPService.  

Se si dispone di una versione precedente del modulo AIPService installate dalla raccolta, aggiornarlo all'ultima versione digitando:

    Update-Module -Name AIPService


## <a name="next-steps"></a>Passaggi successivi
In una sessione di Windows PowerShell verificare la versione del modulo installato. Questo controllo è particolarmente importante se si è eseguito l'aggiornamento da una versione precedente:

```
(Get-Module AIPService –ListAvailable).Version
```

Nota: Se questo comando non riesce, eseguire innanzitutto **Import-Module AIPService**.

Per visualizzare i cmdlet disponibili, digitare quanto segue:

```
Get-Command -Module AIPService
```

Usare il comando `Get-Help <cmdlet_name>` per visualizzare le informazioni della Guida per un cmdlet specifico e quindi impostare il parametro **-online** per visualizzare le informazioni della Guida più recenti dal sito della documentazione Microsoft. Ad esempio:

```
Get-Help Connect-AipService -online
```

Per altre informazioni:

-   Elenco completo dei cmdlet disponibili: [Modulo AIPService](/powershell/module/aipservice/?view=azureipps#aipservice)

-   Elenco dei principali scenari di configurazione che supportano PowerShell: [Amministrazione di protezione di Azure Information Protection tramite PowerShell](administer-powershell.md)

Prima di poter eseguire i comandi che consentono di configurare il servizio di protezione, è necessario connettersi al servizio usando il [Connect-AipService](/powershell/module/aipservice/connect-aipservice) cmdlet.

Al termine dell'esecuzione dei comandi di configurazione, come procedura consigliata, disconnettersi dal servizio usando il [Disconnect-AipService](/powershell/module/aipservice/disconnect-aipservice) cmdlet. Se non ci si disconnette, la connessione viene interrotta automaticamente dopo un periodo di inattività. A causa della disconnessione automatica, si noterà che ogni tanto è necessario riconnettersi a una sessione di PowerShell. 

> [!NOTE]
> Se il servizio di protezione non è ancora attivato, è possibile eseguire questa operazione dopo essersi connessi al servizio, usando il [Enable-AipService](/powershell/module/aipservice/enable-aipservice) cmdlet.

