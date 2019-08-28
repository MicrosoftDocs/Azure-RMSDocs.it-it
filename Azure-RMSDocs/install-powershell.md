---
title: Installare il modulo PowerShell AIPService per Azure Information Protection
description: Istruzioni per l'installazione di PowerShell per il servizio di protezione da Azure Information Protection. Il nome di questo modulo è AIPService.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 08/27/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 0d665ed6-b1de-4d63-854a-bc57c1c49844
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 89820a815e664589051a91f273cb63280e70713a
ms.sourcegitcommit: 72ae1f635e51ef6c6deb1833a30ff11e5918a3e7
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/28/2019
ms.locfileid: "70063738"
---
# <a name="installing-the-aipservice-powershell-module"></a>Installazione del modulo PowerShell AIPService

>*Si applica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

Usare le informazioni seguenti per installare il modulo di Windows PowerShell per il servizio di protezione da Azure Information Protection. Il nome di questo modulo è AIPService e sostituisce la versione precedente denominata AADRM.

È possibile usare questo modulo di PowerShell per amministrare il servizio di protezione (Rights Management di Azure) dalla riga di comando usando qualsiasi computer Windows dotato di connessione a Internet e che soddisfi i prerequisiti elencati nella sezione successiva. Windows PowerShell per Azure Information Protection supporta la creazione di script per l'automazione o potrebbe essere necessario per scenari di configurazione avanzati. Per altre informazioni sulle attività di amministrazione e sulle configurazioni supportate dal modulo, vedere [amministrazione della protezione da Azure Information Protection tramite PowerShell](administer-powershell.md).

## <a name="prerequisites"></a>Prerequisiti
Questa tabella elenca i prerequisiti per installare e usare il modulo di PowerShell AIPService per il servizio di protezione da Azure Information Protection.

|Requisito|Altre informazioni|
|---------------|--------------------|
|Versione minima di Windows PowerShell: 3,0|È possibile verificare quale versione di Windows PowerShell sia in esecuzione digitando `$PSVersionTable` in una sessione di PowerShell. <br /><br /> Se è necessario installare una versione successiva di Windows PowerShell, vedere [Aggiornamento di Windows PowerShell esistente](/powershell/scripting/setup/installing-windows-powershell#upgrading-existing-windows-powershell).|
|Versione minima di Microsoft .NET Framework: 4,5<br /><br />Nota: Questa versione di Microsoft .NET Framework è inclusa nei sistemi operativi successivi, quindi è necessario installarla manualmente solo se il sistema operativo client è inferiore a Windows 8,0 o se il sistema operativo server è inferiore a Windows Server 2012.|Se la versione minima di Microsoft .NET Framework non è ancora installata, è possibile scaricare [Microsoft .NET Framework 4.5](https://www.microsoft.com/download/details.aspx?id=30653).<br /><br />Questa versione minima di Microsoft .NET Framework è obbligatoria per alcune delle classi utilizzate dal modulo AIPService.|

## <a name="if-you-have-the-aadrm-module-installed"></a>Se è installato il modulo AADRM

Il modulo AIPService sostituisce il modulo precedente, AADRM. Se è stato installato il modulo precedente, disinstallarlo e quindi installare il modulo AIPService.

Il modulo più recente presenta alias ai nomi dei cmdlet nel modulo precedente, in modo che gli script esistenti continuino a funzionare. Tuttavia, pianificare l'aggiornamento di questi riferimenti prima che il modulo precedente non sia più supportato. Il supporto per il modulo AADRM terminerà il 15 luglio 2020.

Se il modulo AADRM è stato installato dalla PowerShell Gallery, per disinstallarlo, avviare una sessione di PowerShell con l'opzione **Esegui come amministratore** e digitare:

    Uninstall-Module -Name AADRM

Se il modulo AADRM è stato installato con lo strumento di amministrazione di Azure Rights Management, usare **programmi e funzionalità** per disinstallare **Windows Azure AD Rights Management Administration**.

## <a name="how-to-install-the-aipservice-module"></a>Come installare il modulo AIPService

Il modulo AIPService si trova nel [PowerShell Gallery](/powershell/gallery/readme) e non è disponibile nell'area download Microsoft. 

### <a name="to-install-the-aipservice-module-from-the-powershell-gallery"></a>Per installare il modulo AIPService dalla PowerShell Gallery

Se non si ha familiarità con PowerShell Gallery, vedere [Introduzione a PowerShell Gallery](/powershell/gallery/psgallery/psgallery_gettingstarted). Seguire le istruzioni per i requisiti della raccolta, che includono l'installazione del modulo PowerShellGet e del provider NuGet.

Per visualizzare i dettagli sul modulo AIPService nel PowerShell Gallery, visitare la [pagina AIPService](https://www.powershellgallery.com/packages/AIPService).

Per installare il modulo AIPService, avviare una sessione di PowerShell con l'opzione **Esegui come amministratore** e digitare:

    Install-Module -Name AIPService

Se si riceve un avviso relativo all'installazione da un repository non attendibile, è possibile premere Y per confermare. In alternativa, premere N e configurare il PowerShell Gallery come repository attendibile usando il comando `Set-PSRepository -Name PSGallery -InstallationPolicy Trusted` e quindi eseguire di nuovo il comando per installare il modulo AIPService.  

Se nella raccolta è installata una versione precedente del modulo AIPService, aggiornarla alla versione più recente digitando:

    Update-Module -Name AIPService


## <a name="next-steps"></a>Passaggi successivi
In una sessione di Windows PowerShell verificare la versione del modulo installato. Questo controllo è particolarmente importante se si è eseguito l'aggiornamento da una versione precedente:

```
(Get-Module AIPService –ListAvailable).Version
```

Nota: Se il comando ha esito negativo, eseguire prima **Import-Module AIPService**.

Per visualizzare i cmdlet disponibili, digitare quanto segue:

```
Get-Command -Module AIPService
```

Usare il comando `Get-Help <cmdlet_name>` per visualizzare le informazioni della Guida per un cmdlet specifico e quindi impostare il parametro **-online** per visualizzare le informazioni della Guida più recenti dal sito della documentazione Microsoft. Esempio:

```
Get-Help Connect-AipService -online
```

Per altre informazioni:

-   Elenco completo dei cmdlet disponibili: [Modulo AIPService](/powershell/module/aipservice/?view=azureipps#aipservice)

-   Elenco dei principali scenari di configurazione che supportano PowerShell: [Amministrazione della protezione da Azure Information Protection tramite PowerShell](administer-powershell.md)

Prima di poter eseguire tutti i comandi che configurano il servizio di protezione, è necessario connettersi al servizio usando il cmdlet [Connect-AipService](/powershell/module/aipservice/connect-aipservice) .

Al termine dell'esecuzione dei comandi di configurazione, è consigliabile disconnettersi dal servizio usando il cmdlet [Disconnect-AipService](/powershell/module/aipservice/disconnect-aipservice) . Se non ci si disconnette, la connessione viene interrotta automaticamente dopo un periodo di inattività. A causa della disconnessione automatica, si noterà che ogni tanto è necessario riconnettersi a una sessione di PowerShell. 

> [!NOTE]
> Se il servizio di protezione non è ancora attivato, è possibile eseguire questa operazione dopo la connessione al servizio usando il cmdlet [Enable-AipService](/powershell/module/aipservice/enable-aipservice) .

