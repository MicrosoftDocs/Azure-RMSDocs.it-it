---
title: Usare PowerShell con il client di assegnazione di etichette unificato di Azure Information Protection
description: Istruzioni e informazioni per gli amministratori per gestire il client di assegnazione di etichette unificato di Azure Information Protection tramite PowerShell.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 04/17/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.suite: ems
ms.openlocfilehash: f3a0d3b3974714135289a8f3b262666b63739330
ms.sourcegitcommit: fff4c155c52c9ff20bc4931d5ac20c3ea6e2ff9e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/24/2019
ms.locfileid: "60181855"
---
# <a name="admin-guide-using-powershell-with-the-azure-information-protection-unified-client"></a>Guida dell'amministratore: Uso di PowerShell con il client unificato di Azure Information Protection

>*Si applica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8, Windows 7 with SP1, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2*
>
> *Istruzioni per: [Azure Information Protection unified client per l'assegnazione di etichette per Windows](../faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*

Quando si installa il client di assegnazione di etichette unificato di Azure Information Protection, vengono installati automaticamente i comandi di PowerShell. Ciò consente di gestire il client eseguendo i comandi che è possibile inserire negli script per l'automazione.

I cmdlet installati con il modulo di PowerShell **AzureInformationProtection**, che include cmdlet per l'assegnazione di etichette. Ad esempio: 

|Cmdlet per le etichette|Esempio di utilizzo|
|----------------|---------------|
|[Get-AIPFileStatus](/powershell/module/azureinformationprotection/get-aipfilestatus)|Per una cartella condivisa, identifica tutti i file con un'etichetta specifica.|
|[Set-AIPFileClassification](/powershell/module/azureinformationprotection/set-aipfileclassification)|Per una cartella condivisa, esaminare il contenuto dei file e quindi etichettare automaticamente i file senza etichetta, in base alle condizioni specificate.|
|[Set-AIPFileLabel](/powershell/module/azureinformationprotection/set-aipfilelabel)|Per una cartella condivisa, applica un'etichetta specificata a tutti i file privi di etichetta.|
|[Set-AIPAuthentication](/powershell/module/azureinformationprotection/set-aipauthentication)|Assegnare etichette ai file in modo interattivo, usando un account utente diverso con i propri.|

> [!TIP]
> Per usare cmdlet con percorsi di lunghezza superiore a 260 caratteri, usare l'[impostazione di Criteri di gruppo](https://blogs.msdn.microsoft.com/jeremykuhne/2016/07/30/net-4-6-2-and-long-paths-on-windows-10/) seguente disponibile a partire da Windows 10 versione 1607:<br /> **Criteri Computer locale** > **Configurazione computer** > **Modelli amministrativi** > **Tutte le impostazioni** > **NTFS** > **Abilita percorsi lunghi Win32** 
> 
> Per Windows Server 2016 è possibile usare la stessa impostazione di Criteri di gruppo quando si installano i modelli amministrativi più recenti (con estensione admx) per Windows 10.
>
> Per altre informazioni, vedere la sezione [Maximum Path Length Limitation](https://docs.microsoft.com/windows/desktop/FileIO/naming-a-file#maximum-path-length-limitation) (Limite massimo lunghezza del percorso) della documentazione per sviluppatori di Windows 10.

Questo modulo viene installato in **\Programmi (x86)\Microsoft Azure Information Protection** e aggiunge questa cartella alla variabile di sistema **PSModulePath**. Il file DLL per questo modulo si chiama **AIP.dll**.

### <a name="prerequisites-for-using-the-azureinformationprotection-module"></a>Prerequisiti per l'uso del modulo AzureInformationProtection

Oltre ai prerequisiti per l'installazione del modulo AzureInformationProtection, esistono prerequisiti aggiuntivi per quando si usano i cmdlet di assegnazione di etichette per Azure Information Protection:

1. Il servizio Azure Rights Management deve essere attivato.

2. Per rimuovere la protezione dai file per altri utenti tramite il proprio account: 

    - La funzionalità relativa agli utenti con privilegi avanzati deve essere abilitata per l'organizzazione e l'account deve essere configurato come account con privilegi avanzati per Azure Rights Management.

#### <a name="prerequisite-1-the-azure-rights-management-service-must-be-activated"></a>Prerequisito 1: il servizio Azure Rights Management deve essere attivato

Se il tenant di Azure Information Protection non è attivato per applicare la protezione, vedere le istruzioni [attivazione di Azure Rights Management](../activate-service.md).

#### <a name="prerequisite-2-to-remove-protection-from-files-for-others-using-your-own-account"></a>Prerequisito 2: per rimuovere la protezione dai file per altri utenti usando il proprio account

Gli scenari tipici per la rimozione della protezione dai file per altri utenti includono l'individuazione dei dati o il ripristino dei dati. Se si usano etichette per applicare la protezione, è possibile rimuovere la protezione impostando una nuova etichetta che non applica protezione oppure rimuovendo l'etichetta.

Per poter rimuovere la protezione dai file, è necessario avere diritti di utilizzo per Rights Management oppure un account utente con privilegi avanzati. Per l'individuazione dei dati o il ripristino dei dati, viene in genere usata la funzionalità per utenti con privilegi avanzati. Per abilitare questa funzionalità e configurare l'account come utente con privilegi avanzati, vedere [Configurazione degli utenti con privilegi avanzati per Azure Rights Management e servizi di individuazione o ripristino dei dati](../configure-super-users.md).


## <a name="next-steps"></a>Passaggi successivi
Per il tipo di Guida dei cmdlet all'interno di una sessione di PowerShell `Get-Help <cmdlet name> -online`. Ad esempio:  

    Get-Help Set-AIPFileLabel -online

Per altre informazioni necessarie per supportare il client Azure Information Protection, vedere gli argomenti seguenti:

- [Personalizzazioni](clientv2-admin-guide-customizations.md)

- [File del client e registrazione dell'utilizzo](clientv2-admin-guide-files-and-logging.md)

- [Tipi di file supportati](clientv2-admin-guide-file-types.md)
