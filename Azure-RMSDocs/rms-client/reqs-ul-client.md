---
title: Requisiti aggiuntivi per l'installazione del client Azure Information Protection Unified Labeling
description: Informazioni per gli amministratori che devono comprendere i requisiti di sistema aggiuntivi per l'installazione del client Unified Labeling nelle reti aziendali.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 01/07/2021
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: v2client
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: f9915049894e0892ead767f2ddf392575eb8a99d
ms.sourcegitcommit: af7ac2eeb8f103402c0036dd461c77911fbc9877
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/18/2021
ms.locfileid: "98560288"
---
# <a name="additional-requirements-for-installing-the-unified-labeling-client-on-enterprise-networks"></a>Requisiti aggiuntivi per l'installazione del client Unified Labeling nelle reti aziendali

>***Si applica a**: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8, Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012 *
>
>*Se si dispone di Windows 7 o Office 2010, vedere [AIP e versioni legacy di Windows e Office](../known-issues.md#aip-and-legacy-windows-and-office-versions).*
>
>***Pertinente per**: [Azure Information Protection client di etichetta unificato per Windows](../faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients). Per il client classico, vedere la [Guida dell'amministratore del client classico](client-admin-guide-install.md). *

Prima di installare il client Azure Information Protection Unified Labeling nella rete aziendale, verificare che i computer dispongano delle versioni e delle applicazioni del sistema operativo necessarie per Azure Information Protection: [requisiti per Azure Information Protection](../requirements.md). 

Verificare quindi che siano disponibili gli elementi aggiuntivi necessari per l'installazione del client di Azure Information Protection Unified labeling.

> [!NOTE]
> Non tutti questi requisiti vengono verificati dal software di installazione.
>

## <a name="microsoft-net-framework-requirements"></a>Requisiti di Microsoft .NET Framework

Per impostazione predefinita, l'installazione completa del client Azure Information Protection Unified Labeling richiede una versione minima di Microsoft .NET Framework 4.6.2. 

Se questo Framework non è presente, l'installazione guidata dal programma di installazione eseguibile tenta di scaricare e installare questo prerequisito. Quando questo prerequisito viene installato come parte dell'installazione del client, è necessario riavviare il computer.  

Se si installa il [visualizzatore Azure Information Protection](clientv2-view-use-files.md) autonomamente, è necessario disporre di una versione minima di Microsoft .NET Framework 4.5.2. 

> [!IMPORTANT]
> Se per l'installazione del Visualizzatore manca una versione minima di Microsoft .NET Framework 4.5.2, il software di installazione *non* lo Scarica o lo installa.
> 

### <a name="disable-exploit-protection-net-2-or-3-only"></a>Disabilitare la protezione dagli exploit (solo .NET 2 o 3)

Il client AIP non è supportato nei computer con .NET 2 o 3 con la [protezione dagli exploit](/windows/security/threat-protection/microsoft-defender-atp/enable-exploit-protection) abilitata. 

In questi casi, è consigliabile aggiornare la versione di .NET. 

Se è necessario lasciare .NET versione 2 o 3, assicurarsi di disabilitare la [protezione dagli exploit](../known-issues.md#known-issues-for-aip-and-exploit-protection) prima di installare il client AIP.

## <a name="windows-powershell-minimum-requirements"></a>Requisiti minimi di Windows PowerShell

Il modulo PowerShell per il client richiede una versione minima di Windows PowerShell 4,0.

Se si sta lavorando a un sistema operativo precedente, potrebbe essere necessario inserire manualmente PowerShell. Per altre informazioni, vedere [How to Install Windows PowerShell 4.0](https://social.technet.microsoft.com/wiki/contents/articles/21016.how-to-install-windows-powershell-4-0.aspx) (Come installare Windows PowerShell 4.0). 

> [!IMPORTANT]
> Il programma di installazione *non* controlla né installa questo prerequisito. 
>
> Per verificare quale versione di Windows PowerShell è in esecuzione, digitare `$PSVersionTable` in una sessione di PowerShell.  
> 


## <a name="screen-resolution-requirements"></a>Requisiti di risoluzione dello schermo

I computer client con risoluzioni **800x600** e versioni precedenti non possono visualizzare completamente la finestra di dialogo **classifica e proteggi Azure Information Protection** quando si fa clic con il pulsante destro del mouse su un file o una cartella in Esplora file.   

## <a name="admin-permissions"></a>Autorizzazioni di amministratore

Per installare il client di Azure Information Protection Unified Labeling, è necessario disporre delle autorizzazioni amministrative locali nel computer client.
        
## <a name="windows-10-requirements"></a>Requisiti di Windows 10

I computer che eseguono Office 2010 richiedono l' **Assistente per l'accesso ai Microsoft Online Services versione 7.250.4303.0**, inclusa nell'installazione del client. 

Se si dispone di una versione più recente dell'assistente per l'accesso, disinstallarla prima di installare il client di Azure Information Protection Unified labeling. 

Controllare, ad esempio, la versione e disinstallare l'assistente per l'accesso tramite il **Pannello di controllo**  >  **programmi e funzionalità**  >  **Disinstalla o modifica programma**. 

> [!IMPORTANT]
> Il supporto esteso per Office 2010 è terminato il 13 ottobre 2020. Per altre informazioni, vedere [AIP e versioni legacy di Windows e Office](../known-issues.md#aip-and-legacy-windows-and-office-versions).
>

Solo per Windows 10 versione 1809, per le build del sistema operativo precedenti alla build 17763.348, installare [1 marzo 2019 - KB4482887 (build sistema operativo 17763.348)](https://support.microsoft.com/help/4482887/windows-10-update-kb4482887) per garantire che la barra di Information Protection venga visualizzata correttamente nelle applicazioni Office. Questo aggiornamento non è necessario se si usa Office 365 1902 o versione successiva.    

## <a name="configure-your-group-policy-to-prevent-disabling-aip"></a>Configurare i criteri di gruppo per impedire la disabilitazione di AIP

Per le versioni di Office 2013 e successive, è consigliabile configurare i criteri di gruppo per assicurarsi che il componente aggiuntivo **Microsoft Azure Information Protection** per le applicazioni di Office sia sempre abilitato.  Senza questo componente aggiuntivo, gli utenti non saranno in grado di assegnare etichette ai documenti o ai messaggi di posta elettronica nelle applicazioni di Office.   

Per Word, Excel, PowerPoint e Outlook, usare l' **elenco delle impostazioni di criteri di gruppo dei componenti aggiuntivi gestiti** documentati in [nessun componente aggiuntivo caricato a causa delle impostazioni di criteri di gruppo per i programmi Office 2013 e Office 2016](https://support.microsoft.com/help/2733070/no-add-ins-loaded-due-to-group-policy-settings-for-office-2013-and-off). 

Specificare i seguenti identificatori programmatici (ProgID) per AIP e impostare l'opzione su **1: il componente aggiuntivo è sempre abilitato**.

|Applicazione  |ProgID  |
|---------|---------|
|Word     |     `MSIP.WordAddin`    |
|Excel     |  `MSIP.ExcelAddin`       |
|PowerPoint     |   `MSIP.PowerPointAddin`      |
|Outlook | `MSIP.OutlookAddin` |
| | | 

## <a name="next-steps"></a>Passaggi successivi

Continuare con  [la guida dell'amministratore: installare il client di etichettatura unificata Azure Information Protection per gli utenti](clientv2-admin-guide-install.md).

Per altre informazioni, vedere:

- [File del client e registrazione dell'utilizzo](clientv2-admin-guide-files-and-logging.md)

- [Tipi di file supportati](clientv2-admin-guide-file-types.md)

- [Comandi di PowerShell](clientv2-admin-guide-powershell.md)