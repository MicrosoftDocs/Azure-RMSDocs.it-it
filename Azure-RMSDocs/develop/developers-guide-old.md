---
title: Guida per gli sviluppatori | Azure RMS
description: Panoramica dell&quot;uso degli strumenti per gli sviluppatori; SDK, librerie aggiuntive ed esempi di codice.
keywords: 
author: bruceperlerms
ms.author: bruceper
manager: mbaldwin
ms.date: 11/15/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: a22e6bd0-8ce8-45b4-9a32-273126ab831e
audience: developer
ms.reviewer: kartikk
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 329dce4c8bb5a6de3ecb7bbd7e734b4acbf339c9
ms.openlocfilehash: bbf266512a80ece05253cbfab7b9ab40505f3f67


---

# <a name="developers-guide"></a>Guida per gli sviluppatori

## <a name="overview"></a>Panoramica ##
Questa guida descrive l'ampio set di strumenti e codici di esempio applicabili a tutte le piattaforme supportate, una suite di SDK di Rights Management e strumenti di gestione di PowerShell.

[**Strumenti ed esempi di codice**](#code-samples-and-tools) per tutti i sistemi operativi supportati: Android, iOS/OS X, client Windows e Windows Phone.

[**Linee guida su PowerShell**](#powershell-guidance): per le operazioni di amministrazione e di protezione in blocco di Rights Management.

[**Software Development Kit**](#software-development-kits): configurati per offrire il supporto per vari tipi di sistemi operativi per dispositivi mobili, tra cui Android e iOS, e il supporto esteso per i client Windows.


---

## <a name="code-samples-and-tools"></a>Esempi di codice e strumenti

Questa raccolta di esempi di codice RMS e strumenti di supporto per gli sviluppatori fornita da Microsoft è compatibile con tutti i sistemi operativi Android, iOS/OS X, Windows Phone e Windows Desktop e viene aggiornata periodicamente per mantenere la compatibilità con il relativo SDK supportato.

### <a name="android"></a>Android

Gli elementi seguenti vengono eseguiti su Android supportati da [RMS SDK 4.2](active-directory-rights-management-services-multi-platform-thin-client-sdk-portal.md) e versioni successive di 4.x SDK.

- [Applicazione di esempio e libreria dell'interfaccia utente](https://github.com/AzureAD/rms-sdk-ui-for-android) in GitHub; in questo modo è possibile iniziare rapidamente e riusare l'interfaccia utente standard nelle app.
- Gli [scenari di uso di Android](https://msdn.microsoft.com/en-us/library/dn758246(v=vs.85).aspx) in Java rappresentano gli scenari di sviluppo principali per familiarizzare con RMS SDK. Gli esempi includono l'uso del formato Microsoft Protected File, i formati di file protetti personalizzati e i controlli dell'interfaccia utente personalizzati.

### <a name="ios-os-x"></a>iOS/OS X

Gli elementi seguenti vengono eseguiti su iOS/OS X supportati da [RMS SDK 4.2](active-directory-rights-management-services-multi-platform-thin-client-sdk-portal.md) e versioni successive di 4.x SDK.

- Gli [scenari di uso di iOS/OS X](https://msdn.microsoft.com/en-us/library/dn758307(v=vs.85).aspx) in Objective C rappresentano gli scenari di sviluppo principali per familiarizzare con RMS SDK. Gli esempi includono l'uso del formato Microsoft Protected File, i formati di file protetti personalizzati e i controlli dell'interfaccia utente personalizzati.
- [Applicazione di esempio e libreria dell'interfaccia utente](https://github.com/AzureAD/rms-sdk-ui-for-ios) in GitHub; in questo modo è possibile iniziare rapidamente e riusare l'interfaccia utente standard nelle app. Supportate **solo su iOS**.

### <a name="windows-desktop"></a>Desktop Windows

Gli elementi seguenti vengono eseguiti su Windows Desktop supportati da [RMS SDK 2.1](microsoft-information-protection-and-control-client-portal.md) e versioni successive di 2.x SDK.

- [PDF protetto PFILE di lettura](https://blogs.msdn.microsoft.com/rms/2015/11/09/reading-a-pfile-protected-pdf/) è un esempio di codice semplice nel Blog per sviluppatori RMS che usa l'API del file MSIPC per decrittografare e aprire un documento PDF protetto PFILE.
- [IpcManagedAPI](https://github.com/Azure-Samples/Azure-Information-Protection-Samples/tree/master/IpcManagedAPI) è una rappresentazione .NET (c#) di RMS SDK 2.1 per facilitare l'abilitazione a RMS dell'applicazione gestita.
- [IPCNotepad](https://github.com/Azure-Samples/Azure-Information-Protection-Samples/tree/master/IpcNotepad) è un'applicazione esemplificativa abilitata per RMS che illustra l'esecuzione dei passaggi di base che deve eseguire un'applicazione abilitata per RMS per la protezione e l'utilizzo di contenuto con restrizioni.
- [IpcDIp](https://github.com/Azure-Samples/Azure-Information-Protection-Samples/tree/master/IpcDlpApp) è un'applicazione esemplificativa di protezione dalla perdita di dati abilitata per RMS che illustra l'esecuzione dei passaggi di base che deve eseguire un'applicazione abilitata per RMS usando l'API del file per la protezione e l'utilizzo di contenuto con restrizioni.
- [IpcAzureApp](https://github.com/Azure-Samples/Azure-Information-Protection-Samples/tree/master/IpcAzureApp) è un esempio che illustra come usare RMS SDK nell'applicazione Azure per proteggere i dati nell'archiviazione Blob di Azure.
- [RmsDocumentInspector](https://github.com/Azure-Samples/Azure-Information-Protection-Samples/tree/master/RmsDocumentInspector) è uno strumento in grado di fornire informazioni su qualsiasi file RMS protetto, ad esempio i diritti utente o l'id contenuto.
- [RmsFileWatcher](https://github.com/Azure-Samples/Azure-Information-Protection-Samples/tree/master/RmsFileWatcher) è un esempio che illustra come creare un'applicazione Windows che controlla le directory nel file system e applica i criteri di protezione RMS a ogni modifica, ad esempio per i file modificati o i file aggiunti.

### <a name="windows-store-and-phone"></a>Windows Store e Phone

- [Libreria dell'interfaccia utente per Windows Store](https://github.com/AzureAD/rms-sdk-ui-for-windowsstore): una libreria dell'interfaccia utente per Microsoft RMS SDK v4.1 per le applicazioni di Windows Store. Questa libreria è facoltativa e uno sviluppatore può scegliere di creare la propria interfaccia utente quando usa Microsoft RMS SDK v4.1

- [Libreria dell'interfaccia utente per Windows Phone](https://github.com/AzureAD/rms-sdk-ui-for-winphone): una libreria dell'interfaccia utente per Microsoft RMS SDK v4.1 per le applicazioni di Windows Phone. Questa libreria è facoltativa e uno sviluppatore può scegliere di creare la propria interfaccia utente quando usa Microsoft RMS SDK v4.1

- [Applicazione di esempio](https://github.com/Azure-Samples/active-directory-dotnet-rms-windowsstore): l'esempio per Microsoft RMS SDK v4.1 per le applicazioni di Windows Store fornisce un esempio di utilizzo del documento di base per la piattaforma.

---

## <a name="powershell-guidance"></a>Linee guida su PowerShell
Sono disponibili cmdlet di PowerShell per le operazioni di amministrazione e di protezione in blocco di Rights Management.

I [cmdlet di Azure Rights Management](https://msdn.microsoft.com/library/azure/dn629398.aspx) consentono di amministrare Azure RMS dalla riga di comando. Oltre a consentire l'automazione, questi cmdlet supportano una serie di processi affidabili e ripetuti in grado di ridurre il sovraccarico amministrativo. Inoltre, per alcune configurazioni e operazioni avanzate di Azure RMS è necessario Azure PowerShell.

I [cmdlet di protezione RMS](https://msdn.microsoft.com/library/azure/mt433195.aspx) possono essere usati con la protezione dati di Azure Rights Management (Azure RMS) da Azure Information Protection o con Active Directory Rights Management Services (AD RMS) e integrano altri moduli PowerShell per queste distribuzioni di Rights Management. Usare i cmdlet di protezione RMS per proteggere e rimuovere in blocco la protezione di file di qualsiasi tipo.

---

## <a name="software-development-kits"></a>Software Development Kit


Sono ora disponibili tre generazioni di RMS SDK, descritte nella tabella seguente.

| SDK | Descrizione |
|------|---------|
| [RMS SDK 4.2](active-directory-rights-management-services-multi-platform-thin-client-sdk-portal.md) | Semplice set di strumenti all'avanguardia che offre un'esperienza di sviluppo leggera per abilitare la protezione delle informazioni nelle app per dispositivi Android, iOS, Mac OS X, Windows Phone/RT e Linux/C++ tramite i servizi di Microsoft Rights Management |
| [RMS SDK 2.1](microsoft-information-protection-and-control-client-portal.md) | SDK potente che consente agli sviluppatori di applicazioni Windows Desktop e ai provider di soluzioni basate su server di abilitare la tecnologia Rights Management nei loro prodotti|
|[AD RMS SDK](https://msdn.microsoft.com/library/cc530379.aspx)|** NOTA **: la funzionalità per l'uso di AD RMS SDK esposta dal client in Msdrm.dll è disponibile in Windows Server 2012, Windows 8, Windows Server 2008 R2, Windows 7, Windows Server 2008 e Windows Vista. È possibile che in versioni successive sia stata modificata o non sia più disponibile. Al suo posto, usare Microsoft Rights Management Services SDK 2.1, che sfrutta le funzionalità esposte dal client in Msipc.dll.|
|[API di script AD RMS](https://msdn.microsoft.com/en-us/library/bb968797.aspx)| Usata per creare script per l'amministrazione di un'installazione di AD RMS|



<!--HONumber=Nov16_HO3-->


