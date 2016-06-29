---
# required metadata

title: Guida per gli sviluppatori | Azure RMS
description: Panoramica dell'uso degli strumenti per gli sviluppatori; SDK, librerie aggiuntive ed esempi di codice.
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: a22e6bd0-8ce8-45b4-9a32-273126ab831e
# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Guida per gli sviluppatori

## Panoramica ##
Questa guida descrive la suite di SDK di Rights Management e un ampio set di strumenti ed esempi di codice relativi a tutte le piattaforme supportate. 

## Software Development Kit ##
Sono ora disponibili tre generazioni di RMS SDK, descritte nella tabella seguente.

| SDK | Descrizione |
|------|---------|
| [RMS SDK 4.2](active-directory-rights-management-services-multi-platform-thin-client-sdk-portal.md) | Semplice set di strumenti all'avanguardia che offre un'esperienza di sviluppo leggera per abilitare la protezione delle informazioni nelle app per dispositivi Android, iOS, Mac OS X, Windows Phone/RT e Linux/C++ tramite i servizi di Microsoft Rights Management |
| [RMS SDK 2.1](microsoft-information-protection-and-control-client-portal.md) | SDK potente che consente agli sviluppatori di applicazioni Windows Desktop e ai provider di soluzioni basate su server di abilitare la tecnologia Rights Management nei loro prodotti|
|[AD RMS SDK](https://msdn.microsoft.com/en-us/library/cc530379(v=vs.85).aspx)|** NOTA **: la funzionalità per l'uso di AD RMS SDK esposta dal client in Msdrm.dll è disponibile in Windows Server 2012, Windows 8, Windows Server 2008 R2, Windows 7, Windows Server 2008 e Windows Vista. È possibile che in versioni successive sia stata modificata o non sia più disponibile. Al suo posto, usare Microsoft Rights Management Services SDK 2.1, che sfrutta le funzionalità esposte dal client in Msipc.dll.|
|[API di script AD RMS](https://msdn.microsoft.com/en-us/library/bb968797(v=vs.85).aspx)| Usata per creare script per l'amministrazione di un'installazione di AD RMS|

## Esempi di codice e strumenti
Questa raccolta di esempi di codice RMS e strumenti di supporto per gli sviluppatori fornita da Microsoft è compatibile con tutti i sistemi operativi Android, iOS/OS X, Windows Phone e Windows Desktop e viene aggiornata periodicamente per mantenere la compatibilità con il relativo SDK supportato.

### Android

Gli elementi seguenti vengono eseguiti su Android supportati da [RMS SDK 4.2](active-directory-rights-management-services-multi-platform-thin-client-sdk-portal.md) e versioni successive di 4.x SDK.

- [Applicazione di esempio e libreria dell'interfaccia utente](https://github.com/AzureAD/rms-sdk-ui-for-android) in GitHub; in questo modo è possibile iniziare rapidamente e riusare l'interfaccia utente standard nelle app.
- Gli [scenari di uso di Android](https://msdn.microsoft.com/en-us/library/dn758246(v=vs.85).aspx) in Java rappresentano gli scenari di sviluppo principali per familiarizzare con RMS SDK. Gli esempi includono l'uso del formato Microsoft Protected File, i formati di file protetti personalizzati e i controlli dell'interfaccia utente personalizzati.

### iOS/OS X

Gli elementi seguenti vengono eseguiti su iOS/OS X supportati da [RMS SDK 4.2](active-directory-rights-management-services-multi-platform-thin-client-sdk-portal.md) e versioni successive di 4.x SDK.

- Gli [scenari di uso di iOS/OS X](https://msdn.microsoft.com/en-us/library/dn758307(v=vs.85).aspx) in Objective C rappresentano gli scenari di sviluppo principali per familiarizzare con RMS SDK. Gli esempi includono l'uso del formato Microsoft Protected File, i formati di file protetti personalizzati e i controlli dell'interfaccia utente personalizzati.
- [Applicazione di esempio e libreria dell'interfaccia utente](https://github.com/AzureAD/rms-sdk-ui-for-ios) in GitHub; in questo modo è possibile iniziare rapidamente e riusare l'interfaccia utente standard nelle app. Supportate **solo su iOS**.

### Desktop Windows

Gli elementi seguenti vengono eseguiti su Windows Desktop supportati da [RMS SDK 2.1](microsoft-information-protection-and-control-client-portal.md) e versioni successive di 2.x SDK.

- [PDF protetto PFILE di lettura](https://blogs.msdn.microsoft.com/rms/2015/11/09/reading-a-pfile-protected-pdf/) è un esempio di codice semplice nel Blog per sviluppatori RMS che usa l'API del file MSIPC per decrittografare e aprire un documento PDF protetto PFILE.
- [IpcManagedAPI](https://github.com/Azure-Samples/active-directory-dotnet-rms) è una rappresentazione .NET (c#) di RMS SDK 2.1 per facilitare l'abilitazione a RMS dell'applicazione gestita.
- [IPCNotepad](https://code.msdn.microsoft.com/ipcnotepad-sample-f67dae80) è un'applicazione esemplificativa abilitata per RMS che illustra l'esecuzione dei passaggi di base che deve eseguire un'applicazione abilitata per RMS per la protezione e l'utilizzo di contenuto con restrizioni.
- [IpcDIp](https://github.com/Azure-Samples/active-directory-dotnet-rms) è un'applicazione esemplificativa di protezione dalla perdita di dati abilitata per RMS che illustra l'esecuzione dei passaggi di base che deve eseguire un'applicazione abilitata per RMS usando l'API del file per la protezione e l'utilizzo di contenuto con restrizioni.
- [IpcAzureApp](https://github.com/Azure-Samples/active-directory-dotnet-rms) è un esempio che illustra come usare RMS SDK nell'applicazione Azure per proteggere i dati nell'archiviazione Blob di Azure.
- [RmsDocumentInspector](https://github.com/Azure-Samples/active-directory-dotnet-rms) è uno strumento in grado di fornire informazioni su qualsiasi file RMS protetto, ad esempio i diritti utente o l'id contenuto.
- [RmsFileWatcher](https://github.com/Azure-Samples/active-directory-dotnet-rms) è un esempio che illustra come creare un'applicazione Windows che controlla le directory nel file system e applica i criteri di protezione RMS a ogni modifica, ad esempio per i file modificati o i file aggiunti.

### Windows Store e Phone

- [Libreria dell'interfaccia utente per Windows Store](https://github.com/AzureAD/rms-sdk-ui-for-windowsstore): una libreria dell'interfaccia utente per Microsoft RMS SDK v4.1 per le applicazioni di Windows Store. Questa libreria è facoltativa e uno sviluppatore può scegliere di creare la propria interfaccia utente quando usa Microsoft RMS SDK v4.1

- [Libreria dell'interfaccia utente per Windows Phone](https://github.com/AzureAD/rms-sdk-ui-for-winphone): una libreria dell'interfaccia utente per Microsoft RMS SDK v4.1 per le applicazioni di Windows Phone. Questa libreria è facoltativa e uno sviluppatore può scegliere di creare la propria interfaccia utente quando usa Microsoft RMS SDK v4.1

- [Applicazione di esempio](https://github.com/Azure-Samples/active-directory-dotnet-rms-windowsstore): l'esempio per Microsoft RMS SDK v4.1 per le applicazioni di Windows Store fornisce un esempio di utilizzo del documento di base per la piattaforma.


<!--HONumber=Apr16_HO4-->


