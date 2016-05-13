---
# required metadata

title: Confronto tra Azure Rights Management e AD RMS | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 8123bd62-1814-4d79-b306-e20c1a00e264

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Confronto tra Azure Rights Management e AD RMS
Se già si conosce o si è distribuito in precedenza Active Directory Rights Management Services (AD RMS), è possibile chiedersi quali siano le differenze con [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] (Azure RMS) in termini di funzionalità e requisiti. La tabella seguente riporta un confronto delle funzionalità e dei vantaggi di Azure RMS e AD RMS. Per domande di confronto specifiche sulla sicurezza, vedere la sezione [Controlli crittografici per la firma e la crittografia](compare-azure-rms-ad-rms.md#cryptographic-controls-for-signing-and-encryption) in questo articolo.

> [!NOTE]
> Per un confronto più agevole, alcune delle informazioni riportate di seguito sono tratte da [Requisiti per Azure Rights Management](../get-started/requirements-azure-rms.md). Fare riferimento a tale articolo per informazioni più specifiche sul supporto e sulla versione per [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)].

|Azure RMS|AD RMS|
|-----------------------------------------------------------------------------------------|--------------------------------------------------------|
|Supporta le funzionalità IRM (Information Rights Management) nei Microsoft Online Services come Exchange Online e SharePoint Online, nonché Office 365.<br /><br />Supporta inoltre i prodotti server Microsoft locali, ad esempio Exchange Server, SharePoint Server e i file server che eseguono Windows Server e l'infrastruttura di classificazione file.|Supporta i prodotti server Microsoft locali, ad esempio Exchange Server, SharePoint Server e i file server che eseguono Windows Server e l'infrastruttura di classificazione file.|
|Consente il trust implicito tra le organizzazioni e gli utenti in qualsiasi organizzazione. Questo significa che è possibile condividere il contenuto protetto tra gli utenti all'interno della stessa organizzazione o in organizzazioni diverse quando gli utenti dispongono di [!INCLUDE[o365_1](../includes/o365_1_md.md)] o [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] oppure si iscrivono a RMS per singoli.|I trust devono essere definiti in modo esplicito in una relazione punto a punto diretta tra due organizzazioni mediante domini utente affidabili o trust federativi creati mediante Active Directory Federation Services (AD FS).|
|Fornisce due modelli predefiniti di criteri per i diritti di utilizzo che limitano l'accesso al contenuto per l'organizzazione: uno fornisce la visualizzazione in sola lettura del contenuto protetto e l'altro fornisce le autorizzazioni di scrittura o modifica del contenuto protetto.<br /><br />È anche possibile creare modelli personalizzati, inclusi modelli di reparto, visibili solo per un sottoinsieme di utenti. Per altre informazioni, vedere [Configurazione di modelli personalizzati per Azure Rights Management](../deploy-use/configure-custom-templates.md).<br /><br />Gli utenti inoltre possono definire un proprio set di autorizzazioni se i modelli non sono sufficienti.|Non sono disponibili modelli predefiniti di criteri per i diritti di utilizzo, è quindi necessario creare e distribuirli. Per altre informazioni, vedere [Considerazioni sui modelli di criteri di AD RMS](http://go.microsoft.com/fwlink/?LinkId=154765).<br /><br />Gli utenti inoltre possono definire un proprio set di autorizzazioni se i modelli non sono sufficienti.|
|La versione minima supportata di Microsoft Office è Office 2010, che richiede l'[applicazione RMS sharing](../rms-client/sharing-app-windows.md).<br /><br />Microsoft Office per Mac:<br /><br />Microsoft Office per Mac 2016: supportato<br /><br />Microsoft Office per Mac 2011: non supportato|La versione minima supportata di Microsoft Office è Office 2007.<br /><br />Microsoft Office per Mac:<br /><br />Microsoft Office per Mac 2016: supportato<br /><br />Microsoft Office per Mac 2011: supportato|
|Supporta l'[applicazione RMS sharing](../rms-client/sharing-app-windows.md) per computer Windows e Mac e dispositivi mobili.<br /><br />Inoltre, l'applicazione di RMS sharing prevede le seguenti restrizioni:<br /><br />Condivisione con persone in un'altra organizzazione.<br /><br />Notifica tramite posta elettronica, che consente al mittente di sapere quando un utente tenta di aprire un allegato protetto.<br /><br />Sito di rilevamento dei documenti per gli utenti, che include la possibilità di revocare un documento.|Supporta l'[applicazione RMS sharing](../rms-client/sharing-app-windows.md) per computer Windows e Mac e dispositivi mobili. Tuttavia, la condivisione non supporta la condivisione con persone in un'altra organizzazione, la notifica tramite posta elettronica o il sito di rilevamento dei documenti e la possibilità per gli utenti di revocare i documenti.|
|Tutti i tipi di file possono essere protetti con la [protezione nativa o generica](../rms-client/sharing-app-admin-guide-technical.md#levels-of-protection-native-and-generic) quando si usa l'applicazione RMS sharing.<br /><br />Per altre applicazioni, controllare la [tabella delle funzionalità dei dispositivi client](../get-started/requirements-client-devices.md#client-device-capabilities).|Tutti i tipi di file possono essere protetti con la [protezione nativa o generica](../rms-client/sharing-app-admin-guide-technical.md#levels-of-protection-native-and-generic) quando si usa l'applicazione RMS sharing.<br /><br />Per altre applicazioni, controllare la [tabella delle funzionalità dei dispositivi client](../get-started/requirements-client-devices.md#client-device-capabilities).|
|La versione minima supportata del client Windows è Windows 7.|La versione minima supportata del client Windows è Windows Vista Service Pack 2.|
|Il supporto dei dispositivi mobili include Windows Phone, Android, iOS e Windows RT.<br /><br />In tutte le piattaforme per dispositivi mobili che supportano il protocollo Exchange ActiveSync IRM è garantito anche il supporto per la posta elettronica tramite tale protocollo.|Il supporto dei dispositivi mobili include Windows Phone, Android, iOS e Windows RT e richiede l'[estensione per dispositivo mobile di Active Directory Rights Management Services](http://technet.microsoft.com/library/dn673574.aspx).<br /><br />La posta elettronica mediante IRM di Exchange ActiveSync è supportata in tutte le piattaforme di dispositivi mobili che supportano questo protocollo.|
|Supporta Multi-Factor Authentication (MFA) per i computer e dispositivi mobili.<br /><br />Per altre informazioni, vedere [Multi-Factor Authentication (MFA) e Azure RMS](../get-started/requirements-azure-ad.md#multi-factor-authentication-mfa-and-azure-rms).|Supporta l'autenticazione con smart card se IIS è configurato per richiedere i certificati.|
|Supporta la modalità crittografia 2 senza configurazioni aggiuntive, pertanto è garantita una sicurezza più avanzata per la lunghezza delle chiavi e gli algoritmi di crittografia.<br /><br />Per altre informazioni, vedere la sezione [Controlli crittografici per la firma e la crittografia](#cryptographic-controls-for-signing-and-encryption) di questo articolo e [Modalità crittografia di AD RMS](http://go.microsoft.com/fwlink/?LinkId=266659).|Supporta la modalità crittografia 1 per impostazione predefinita e richiede configurazioni aggiuntive per supportare la modalità crittografia 2 per una sicurezza più avanzata.<br /><br />Per altre informazioni, vedere la sezione [Controlli crittografici per la firma e la crittografia](#cryptographic-controls-for-signing-and-encryption) di questo articolo e [Modalità crittografia di AD RMS](http://go.microsoft.com/fwlink/?LinkId=266659).|
|Supporta la migrazione da AD RMS e, se richiesto, ad AD RMS:<br /><br />[Migrazione da AD RMS ad Azure Rights Management](../plan-design/migrate-from-ad-rms-to-azure-rms.md)<br /><br />[Rimozione delle autorizzazioni e disattivazione di Azure Rights Management](../deploy-use/decommission-deactivate.md)|Supporta la migrazione da RMS di Azure ad Azure RMS:<br /><br />[Rimozione delle autorizzazioni e disattivazione di Azure Rights Management](../deploy-use/decommission-deactivate.md)<br /><br />[Migrazione da AD RMS ad Azure Rights Management](../plan-design/migrate-from-ad-rms-to-azure-rms.md)|
|Richiede una licenza di RMS per proteggere il contenuto. Per utilizzare il contenuto protetto da RMS di Azure (include gli utenti da un'altra organizzazione) non è necessaria nessuna licenza di RMS.<br /><br />Per altre informazioni, vedere l'articolo relativo alle [sottoscrizioni cloud che supportano Azure RMS](../get-started/requirements-subscriptions.md).|Richiede una licenza di RMS per proteggere il contenuto e di utilizzare il contenuto protetto da RMS di AD.<br /><br />Per ulteriori informazioni sulle licenze per AD RMS, vedere [Licenze di accesso client e gestione delle licenze](https://www.microsoft.com/en-us/Licensing/product-licensing/client-access-license.aspx) per informazioni di carattere generale, ma contattare il partner Microsoft o il rappresentante Microsoft per informazioni specifiche.|

## Controlli crittografici per la firma e la crittografia
[!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] usa sempre RSA 2048 per la crittografia a chiave pubblica e SHA 256 per le operazioni di firma. AD RMS invece supporta RSA 1024 e RSA 2048, nonché SHA 1 o SHA 256 per le operazioni di firma.

[!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] e AD RMS usano entrambi AES 128 per la crittografia simmetrica.

[!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] è conforme a FIPS 140-2 quando la chiave del tenant viene creata e gestita da Microsoft (impostazione predefinita) o se si gestisce direttamente la propria chiave del tenant (servizio noto come BYOK). Per altre informazioni sulla gestione della chiave del tenant, vedere [Pianificazione e implementazione della chiave del tenant di Azure Rights Management](../plan-design/plan-implement-tenant-key.md).

## Passaggi successivi
Se si vuole eseguire la migrazione da AD RMS ad Azure RMS, vedere [Migrazione da AD RMS ad Azure Rights Management](../plan-design/migrate-from-ad-rms-to-azure-rms.md).




<!--HONumber=Apr16_HO3-->


