---
title: Client di Azure Information Protection&colon; cronologia delle versioni
description: Informazioni sugli elementi nuovi o modificati in una versione del client di Azure Information Protection per Windows.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 03/06/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 6ebd0ca3-1864-4b3d-bb3e-a168eee5eb1d
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: cfd5eae4191cb0b09d8d43f9f708c80ff724d136
ms.sourcegitcommit: 31e128cc1b917bf767987f0b2144b7f3b6288f2e
translationtype: HT
---
# <a name="azure-information-protection-client-version-release-history"></a>Client di Azure Information Protection: cronologia delle versioni

>*Si applica a: Azure Information Protection*

Il team di Azure Information Protection aggiorna regolarmente il client di Azure Information Protection con correzioni e nuove funzionalità. Il client è incluso nel Microsoft Update Catalog (categoria **Azure Information Protection**) ed è sempre possibile scaricare la versione di disponibilità generale più recente e la prossima versione (la versione di anteprima) dall'[Area download Microsoft](https://www.microsoft.com/en-us/download/details.aspx?id=53018).

Le versioni di anteprima non devono essere distribuite agli utenti finali nelle reti di produzione, ma possono essere usate per visualizzare e provare le nuove funzionalità e correzioni che saranno disponibili nella prossima versione di disponibilità generale. 

Usare le informazioni seguenti per visualizzare gli elementi nuovi o modificati di una versione di disponibilità generale. La versione più recente è elencata per prima. Per informazioni sulla versione di anteprima corrente, vedere le informazioni riportate nella pagina di download.

> [!NOTE]
> Poiché le correzioni di minore rilevanza non sono elencate, se si verifica un problema con il client di Azure Information Protection, controllare prima che tale problema non riguardi la versione di disponibilità generale più recente. In caso affermativo, verificare la versione di anteprima corrente.
>  
> Se il problema persiste, vedere le informazioni contenute in [Opzioni di supporto e risorse della community](../get-started/information-support.md#support-options-and-community-resources). È anche possibile rivolgersi al team di Azure Information Protection nel [sito di Yammer](https://www.yammer.com/askipteam/).

## <a name="version-131552"></a>Versione 1.3.155.2

**Data di rilascio**: 08/02/2017

**Nuovi requisiti**:

Microsoft .NET Framework

- Questa versione del client Azure Information Protection richiede Microsoft .NET Framework 4.6.2 come versione minima. Se questo non è presente, il programma di installazione prova a scaricarlo e installarlo. Al termine dell'installazione del client Azure Information Protection, potrebbe essere necessario riavviare il computer.

- Se il visualizzatore Azure Information Protection viene installato separatamente, è necessario Microsoft .NET Framework 4.5.2 come versione minima. Se questo non è presente, il programma di installazione non lo scarica e installa.

**Nuove funzionalità**:

- Nuovo client unificato che riunisce le funzionalità dell'applicazione di condivisione Rights Management per Windows e il client Azure Information Protection. Include:
    
    - Integrazione con Esplora file (clic con il pulsante destro del mouse) per l'applicazione di etichette e protezione. Supporta altri formati di file e la selezione di più file.
    - Un visualizzatore per documenti protetti (include PDF protetti per SharePoint).
    - Cmdlet di PowerShell per ottenere e impostare etichette per i file archiviati in locale o in condivisioni di rete. Questi cmdlet vengono installati con i cmdlet forniti in precedenza con lo strumento di protezione RMS (modulo RMSProtection).
    - Log di utilizzo del client che registrano informazioni, ad esempio su quale etichetta è stata applicata, come e da chi.

Questa versione del client è la [versione con disponibilità generale](https://blogs.technet.microsoft.com/enterprisemobility/2017/02/08/azure-information-protection-december-update-moves-to-general-availability/) del client in anteprima annunciato per la prima volta nel mese di dicembre 2016. Per altre informazioni su questa versione del client, vedere le guide seguenti:

- [Guida per l'amministratore del client di Azure Information Protection](client-admin-guide.md)

- [Guida per l'utente di Azure Information Protection](client-user-guide.md)


## <a name="version-1240"></a>Versione 1.2.4.0

**Data di rilascio**: 27/10/2016

**Correzioni**:

- L'installazione del client viene completata quando il servizio Windows Update è disattivato.

- In Office 2016, quando si salva un documento ed è configurata un'etichetta per un'intestazione o un piè di pagina, il cursore non passa all'intestazione o al piè di pagina.

- La classificazione automatica funziona in Word per il testo nelle caselle di testo combinate.

**Nuove funzionalità**:

- Opzione per test diagnostici e ripristino che l'utente può eseguire dall'applicazione di Office quando è installato il client di Azure Information Protection: nel gruppo **Protezione** della scheda **Home** fare clic su **Proteggi**, scegliere **Guida e commenti e suggerimenti** e quindi **Esegui diagnostica**. 

    Per altre informazioni su questa opzione, vedere la sezione [Per verificare l'installazione o lo stato di connessione o inviare commenti e suggerimenti](client-admin-guide.md#additional-checks-to-verify-installation-connection-status-or-send-feedback) della documentazione relativa all'installazione del client.

## <a name="version-11230"></a>Versione 1.1.23.0

**Data di rilascio**: 01/10/2016

Disponibilità generale.

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sull'installazione del client:

- Per utenti: [Scaricare e installare il client](install-client-app.md)

- Per amministratori: [Guida per l'amministratore del client di Azure Information Protection](client-admin-guide.md)


[!INCLUDE[Commenting house rules](../includes/houserules.md)]