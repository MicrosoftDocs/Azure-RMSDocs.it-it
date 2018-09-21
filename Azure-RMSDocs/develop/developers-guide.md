---
title: Guida per gli sviluppatori di Azure Information Protection
description: Gli sviluppatori possono usare Azure Information Protection per proteggere e gestire file di tutti i tipi
author: lleonard-msft
ms.author: bryanla
manager: mbaldwin
ms.date: 10/11/2017
ms.topic: conceptual
ms.service: information-protection
ms.assetid: a53c2df2-a0a2-4f1f-995b-75ba55e4489b
ms.suite: ems
ms.reviewer: kartikk
ms.openlocfilehash: 54eaa9819ce1bffd85bb11b7e1936abacbd5457b
ms.sourcegitcommit: 07af86511a394274f10cf1340de4cf4bad6d1675
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/20/2018
ms.locfileid: "46473801"
---
# <a name="azure-information-protection-developers-guide"></a>Guida per gli sviluppatori di Azure Information Protection

Questa guida serve a comprendere gli strumenti per l'estensione e l'integrazione con il servizio Rights Management di Azure Information Protection.

>Il SDK di Azure Information Protection include il componente Rights Management. È in corso lo sviluppo di un componente di classificazione e un componente di assegnazione etichette.

## <a name="service-applications"></a>Applicazioni di servizio

Le applicazioni di servizio forniscono funzionalità per proteggere le informazioni durante l'esportazione da un sistema di gestione dei contenuti aziendali, da un'applicazione aziendale o da una soluzione aziendale basata su cloud. Le applicazioni di prevenzione della perdita dei dati (DLP) e Cloud Application Security (CAS) sono esempi di applicazioni di servizio. L'SDK per lo sviluppo di applicazioni di servizio è disponibile tramite due modelli di programmazione.

- [C++](https://www.microsoft.com/download/details.aspx?id=38397)
- [API gestita da C#](https://github.com/Azure-Samples/Azure-Information-Protection-Samples/tree/master/IpcManagedAPI)

### <a name="examples-of-service-applications"></a>Esempi di applicazioni di servizio

- [IpcDIp](https://github.com/Azure-Samples/active-directory-dotnet-rms) è un'applicazione DLP abilitata per RMS di esempio che illustra i passaggi di base che devono essere eseguiti da un'applicazione DLP abilitata per RMS mediante l'API file di RMS per la protezione e l'utilizzo di contenuto con restrizioni.
- [IpcAzureApp](https://github.com/Azure-Samples/active-directory-dotnet-rms) è un esempio che illustra come usare RMS SDK nelle applicazioni Azure per proteggere i dati in un'archiviazione BLOB di Azure.
- [RmsFileWatcher](https://github.com/Azure-Samples/active-directory-dotnet-rms) è un esempio che illustra come creare un'applicazione Windows che controlla le directory nel file system e applica i criteri di protezione RMS a ogni modifica, ad esempio per i file modificati o i file aggiunti.
- [ProtectFilesInDir](https://github.com/Azure-Samples/Azure-Information-Protection-Samples/tree/master/ProtectFilesInDir) è un esempio di applicazione console semplice che accetta una directory come input e consente di proteggere tutti i file solo in tale directory, senza ricorsione.

## <a name="powershell-guides"></a>Guide di PowerShell

I cmdlet PowerShell, usati dagli amministratori di Azure Rights Management, sono utili anche per sviluppare e testare le applicazioni di servizio. Per altre informazioni, vedere [Uso di PowerShell con il client Azure Information Protection](/azure/information-protection/rms-client/client-admin-guide-powershell).

## <a name="user-applications"></a>Applicazioni utente

Le applicazioni utente possono essere create con RMS SDK 2.1 o RMS SDK 4.2.
La versione 4.2 è basata su client REST con API specifiche del sistema operativo per alcuni dei sistemi operativi più diffusi, tra cui iOS/OSX, Android, Linux e Windows. La versione 2.1 viene usata per creare applicazioni native basate su Windows.

### <a name="user-application-development-guides"></a>Guide di sviluppo per le applicazioni utente

- [Sviluppo dell'applicazione](developing-your-application.md)
- [Controllo dell'applicazione](how-to-set-up-your-test-environment.md)
- [Distribuzione dell'applicazione](deploying-your-application.md)

### <a name="user-application-samples"></a>Esempi di applicazioni utente

- [AzureIP Test](https://github.com/Azure-Samples/Azure-Information-Protection-Samples/tree/master/AzureIP_Test) è un'applicazione console di esempio che consente di crittografare i documenti con un modello di Azure o un criterio ad hoc.
- [IPCNotepad](https://github.com/Azure-Samples/Azure-Information-Protection-Samples/tree/master/AzureIP_Test) è un'applicazione abilitata per RMS di esempio che illustra i passaggi di base che devono essere eseguiti da ogni applicazione abilitata per RMS per la protezione e l'utilizzo di contenuto con restrizioni.
- [RmsDocumentInspector](https://github.com/Azure-Samples/active-directory-dotnet-rms) è uno strumento in grado di fornire informazioni su qualsiasi file RMS protetto, ad esempio i diritti utente o l'id contenuto.

## <a name="development-environment-setup"></a>Configurazione dell'ambiente di sviluppo

Le guide seguenti illustrano i passaggi di configurazione specifici del sistema operativo per un ambiente di sviluppo di applicazioni usando strumenti comuni.

[![Installazione per iOS e OS X](../media/develop/ios-icon.png)](ios-sdk.md)
[![Installazione per Android](../media/develop/android-icon.png)](android-sdk.md)
[![Installazione per Windows Phone](../media/develop/windows-phone-icon.png)](windows-phone-apps.md)
[![Installazione del servizio di Windows](../media/develop/windows-icon.png)](install-the-rms-sdk.md)
[![Installazione per Linux](../media/develop/linux-icon.png)](linux-setup.md)


## <a name="how-tos"></a>Procedure

Ognuno degli argomenti seguenti contiene indicazioni specifiche per un aspetto dell'implementazione di un'applicazione. Le applicazioni di servizio vengono create mediante RMS SDK 2.x. Le applicazioni utente vengono create mediante RMS SDK 4.x. Il collegamento dell'articolo viene definito con tipo di applicazione, servizio e utente.

### <a name="general"></a>Generale

- [Procedura: Abilitare la revoca e il rilevamento dei documenti (servizio)](tracking-content.md)
- [Come distribuire il client](../rms-client/client-deployment-notes.md)
- [Come distribuire l'app di servizio in un altro tenant] (how-to-deploy-app.md)
- [Procedura: Installare e configurare un server RMS (servizio)](how-to-install-and-configure-an-rms-server.md)
- [Procedura: Usare il rilevamento dei documenti (utente)](how-to-use-document-tracking.md)
- [Come rinnovare una chiave simmetrica in Azure Information Protection](how-to-renew-symmetric-key.md)

### <a name="security-and-authentication"></a>Sicurezza e autenticazione

- [Come configurare un'applicazione del servizio app per usare l'account di accesso di Azure Active Directory](https://docs.microsoft.com/azure/app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication)
- [Procedura: Usare l'autenticazione ADAL](how-to-use-adal-authentication.md)
- [Configurare Azure RMS per l'autenticazione ADAL (servizio)](adal-auth.md)
- [Procedura: Impostare la modalità di sicurezza dell'API (servizio)](setting-the-api-security-mode-api-mode.md)
- [Procedura: Consentire all'applicazione di servizio di usare RMS basato su cloud (servizio)](how-to-use-file-api-with-aadrm-cloud.md)
- [Come registrare l'app e abilitarla per RMS con Azure AD (utente)](authentication-integration.md)

### <a name="configuration-and-performance-management"></a>Configurazione e gestione delle prestazioni

- [Procedura: Aggiungere diritti espliciti di proprietario (servizio)](add-explicit-owner-rights.md)
- [Configurazione dell'API file (servizio)](file-api-configuration.md)
- [Come usare i diritti predefiniti (utente)](built-in-rights-usage-restriction-reference.md)
- [Come abilitare la registrazione delle prestazioni e dell'errore (utente)](enabling-logging.md)

## <a name="introduction-and-datasheets"></a>Introduzione e fogli dati

[Introduzione ad Azure Information Protection](https://www.microsoft.com/cloud-platform/azure-information-protection)

## <a name="other-resources"></a>Altre risorse

- [Guida per le procedura di sicurezza consigliate](security-guidelines.md)
- [Blog per sviluppatori RMS](https://blogs.msdn.microsoft.com/rms/)
- [Domande frequenti su Azure Information Protection](https://docs.microsoft.com/information-protection/get-started/faqs)

### <a name="support-articles"></a>Articoli di supporto

- [Formati di file supportati](supported-file-formats.md)
- [Piattaforme supportate](supported-platforms.md)
- [Informazioni sulle restrizioni di utilizzo](understanding-usage-restrictions.md)

### <a name="message-protocol-and-file-formats"></a>Protocolli e formati file dei messaggi

- [Protocollo Client-to-Server](https://msdn.microsoft.com/library/cc243191.aspx)
- [Protocollo Rights-Managed Email Object](https://msdn.microsoft.com/library/cc463909(v=EXCHG.80).aspx)
- [Formato di file Compound File Binary](https://msdn.microsoft.com/library/dd942138.aspx)

#### <a name="rights-managed-email-message"></a>Messaggio di posta elettronica gestito da diritti

- [Formato di file msg (parte 1)](https://blogs.msdn.microsoft.com/openspecification/2009/11/06/msg-file-format-part-1/)
- [Formato di file msg (parte 2)](https://blogs.msdn.microsoft.com/openspecification/2010/06/20/msg-file-format-rights-managed-email-message-part-2/)

### <a name="api-reference"></a>Informazioni di riferimento sulle API

- [Informazioni di riferimento sulle API di Windows](https://msdn.microsoft.com/library/hh535292.aspx)
  - [Codici di errore di Windows SDK](https://msdn.microsoft.com/library/hh535248.aspx)
- [Informazioni di riferimento sulle API per Windows Phone e Windows Store](https://msdn.microsoft.com/library/dn891914.aspx)
- [Informazioni di riferimento sulle API di iOS/OSX](https://msdn.microsoft.com/library/dn758306.aspx)
- [Informazioni di riferimento sulle API di Android](https://msdn.microsoft.com/library/dn758245.aspx)
- [Informazioni di riferimento sulle API di Linux](http://azuread.github.io/rms-sdk-for-cpp/annotated.html)

### <a name="previous-versions"></a>Versioni precedenti

- [AD RMS SDK](https://msdn.microsoft.com/library/cc530379.aspx) è la prima versione di RMS SDK.
- [Strumento di scripting di AD RMS](https://msdn.microsoft.com/library/bb968797.aspx) è uno strumento di amministrazione per un'installazione di AD RMS.

### <a name="see-also"></a>Vedere anche

- [Terminologia per sviluppatori](terms.md)
- [Terminologia di Azure Information Protection - ITPro](../terminology.md)

