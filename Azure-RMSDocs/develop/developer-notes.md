---
title: Istruzioni per sviluppatori per Azure Information Protection SDK 2.1 | Documentazione Microsoft
description: Una raccolta di argomenti con procedure per lo sviluppo con AIP SDK 2.1
keywords: 
author: bruceperlerms
ms.author: bruceper
manager: mbaldwin
ms.date: 01/23/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 5A9F04FD-0FCD-482F-8671-36FE93B783B0
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 5df7da98abf4e7c8e39b610fe374d67cf2954338
ms.openlocfilehash: 1c10eb8f7a68138761931d1c8a1715a03b7ff0a9
ms.lasthandoff: 01/24/2017


---

# <a name="developer-guidance"></a>Istruzioni per sviluppatori

Questa sezione descrive le indicazioni specifiche per diversi scenari di sviluppo importanti, nonché informazioni generali sullo sviluppo con questo SDK. Gli scenari in questa sezione sono specifici per la versione corrente di Rights Management Services SDK 2.1 e possono subire modifiche nelle versioni successive.
- [Procedura: Usare l'autenticazione ADAL](how-to-use-adal-authentication.md): autenticazione con Azure RMS per l'app usando Azure Active Directory Authentication Library (ADAL).
- [Procedura: Aggiungere diritti proprietario espliciti](add-explicit-owner-rights.md): l'applicazione deve aggiungere in modo esplicito i diritti "proprietario" durante la creazione di una licenza da zero ([IpcCreateLicenseFromScratch](https://msdn.microsoft.com/library/hh535256.aspx)).
- [Procedura: Eseguire il debug dell'applicazione abilitata all'uso di diritti](debugging-applications-that-use-ad-rms.md): questo argomento illustra come eseguire il debug dell'applicazione e usare il Registro eventi di Windows.
- [Procedura: Abilitare il rilevamento e la revoca dei documenti](tracking-content.md): questo argomento illustra le linee guida di base per implementare il rilevamento del contenuto del documento, nonché un codice di esempio per aggiornare i metadati e per creare il pulsante **Rileva utilizzo** per l'app.
- [Procedura: Abilitare la notifica tramite posta elettronica](how-to-enable-email-notification.md): notifica tramite posta elettronica inviata al proprietario di un contenuto protetto quando qualcuno accede al contenuto.
- [Procedura: Consentire all'applicazione di servizio di usare RMS basato su cloud](how-to-use-file-api-with-aadrm-cloud.md): questo argomento descrive i passaggi per la configurazione dell'applicazione di servizio per l'uso di Azure Rights Management.
- [Procedura: Installare e configurare un server RMS](how-to-install-and-configure-an-rms-server.md): questo argomento descrive la procedura di collegamento a un server RMS o ad Azure RMS per il test dell'applicazione abilitata all'uso di diritti.
- [Procedura: Impostare la modalità di sicurezza dell'API](setting-the-api-security-mode-api-mode.md): è possibile scegliere la modalità di sicurezza eseguita dall'applicazione API file tramite la funzione [IpcSetGlobalProperty](https://msdn.microsoft.com/library/hh535270.aspx).
- [Procedura: Usare le impostazioni di crittografia](working-with-encryption.md): questo argomento descrive i pacchetti di crittografia e illustra alcuni frammenti di codice che ne consentono l'uso.
- [Tipi di applicazioni](application-types.md): questo argomento illustra i tipi di applicazioni che è possibile scegliere di creare come abilitate all'uso di diritti.
- [Configurazione dell'API file](file-api-configuration.md): il comportamento dell'API file può essere configurato tramite le impostazioni del Registro di sistema.
- [Linee guida sulla sicurezza](security-guidelines.md): fornisce agli sviluppatori l'orientamento e le indicazioni per l'utilizzo all'interno dell'ecosistema AIP.
- [Formati di file supportati](supported-file-formats.md): l'API file supporta i formati nativi e PFile
- [Piattaforme supportate](supported-platforms.md): questo argomento identifica le piattaforme client e server di RMS SDK 2.1 supportate.
- [Informazioni sulle restrizioni di utilizzo](understanding-usage-restrictions.md): tutte le applicazioni abilitate per RMS devono imporre restrizioni di utilizzo, che sono definite dalle costanti elencate in questo argomento.

 
## <a name="related-topics"></a>Argomenti correlati
* [Panoramica](ad-rms-overview.md)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
