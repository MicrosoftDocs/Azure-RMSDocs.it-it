---
# required metadata

title: Note per gli sviluppatori | Azure RMS
description: Questo argomento illustra indicazioni specifiche per diversi scenari di sviluppo importanti. 
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 5A9F04FD-0FCD-482F-8671-36FE93B783B0
# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---
** Il contenuto di questo SDK non è aggiornato. Per un breve periodo, la [versione attuale](https://msdn.microsoft.com/library/windows/desktop/hh535290(v=vs.85).aspx) della documentazione sarà disponibile su MSDN. **
# Note per gli sviluppatori

Questa sezione illustra indicazioni specifiche per diversi scenari di sviluppo importanti. Gli scenari in questa sezione sono specifici per la versione corrente di Rights Management Services SDK 2.1 e possono subire modifiche nelle versioni successive.

- [Aggiungere diritti proprietario espliciti](add-explicit-owner-rights.md): l'applicazione deve aggiungere in modo esplicito i diritti &quot;proprietario&quot; durante la creazione di una licenza da zero ([IpcCreateLicenseFromScratch](/rights-management/sdk/2.1/api/win/functions#msipc_ipccreatelicensefromscratch)).
- [Condizioni di errore comuni e relative soluzioni](common-error-conditions-and-solutions.md): messaggi di errore più comuni che possono essere visualizzati quando si usano gli strumenti di sviluppo RMS SDK 2.1.
- [Abilitazione della notifica tramite posta elettronica](how-to-enable-email-notification.md): notifica tramite posta elettronica inviata al proprietario di un contenuto protetto quando qualcuno accede al contenuto.
- [Configurazione dell'API file](file-api-configuration.md): il comportamento dell'API file può essere configurato tramite le impostazioni del Registro di sistema.
- [IPCHelloWorld - Applicazione di esempio](how-to-build-your-first-application.md): questo argomento contiene istruzioni per creare un'applicazione di esempio abilitata all'uso di diritti.
- [Impostazione della modalità di sicurezza dell'API](setting-the-api-security-mode-api-mode.md): è possibile scegliere la modalità di sicurezza eseguita dall'applicazione API file tramite la funzione [IpcSetGlobalProperty](/rights-management/sdk/2.1/api/win/functions#msipc_ipcsetglobalproperty).
- [Formati di file supportati](supported-file-formats.md): l'API file supporta i formati nativi e PFile.
- [Rilevamento del contenuto](tracking-content.md): questo argomento illustra le linee guida di base per l'implementazione del rilevamento del contenuto protetto con RMS SDK 2.1.
- [Uso della crittografia](working-with-encryption.md): questo argomento descrive i pacchetti di crittografia e illustra alcuni frammenti di codice che ne consentono l'uso.

 

## Argomenti correlati ##
* [Panoramica](ad-rms-overview.md)
* [Modalità d'uso](how-to-use-msipc.md)
 

 


<!--HONumber=Jun16_HO1-->


