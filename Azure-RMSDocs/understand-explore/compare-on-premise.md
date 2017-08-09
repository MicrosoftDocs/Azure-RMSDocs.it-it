---
title: Confrontare Azure Information Protection e AD RMS
description: "Se già si conosce o si è distribuito in precedenza Active Directory Rights Management Services (AD RMS), è possibile chiedersi quali siano le differenze con Azure Information Protection in termini di funzionalità e requisiti."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 07/31/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 8123bd62-1814-4d79-b306-e20c1a00e264
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 7b3a49925fc0486f7be161da501a59c1ec2ebdfc
ms.sourcegitcommit: 55a71f83947e7b178930aaa85a8716e993ffc063
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/31/2017
---
# <a name="comparing-azure-information-protection-and-ad-rms"></a>Confronto tra Azure Information Protection e AD RMS

>*Si applica a: Active Directory Rights Management Services, Azure Information Protection, Office 365*

Se già si conosce o si è distribuito in precedenza Active Directory Rights Management Services (AD RMS), è possibile chiedersi quali siano le differenze con Azure Information Protection in termini di funzionalità e requisiti come soluzione di protezione delle informazioni.

Di seguito sono descritte alcune delle differenze principali di Azure Information Protection:

- **Nessuna infrastruttura server necessaria**: Azure Information Protection non richiede i server aggiuntivi e i certificati PKI richiesti da AD RMS poiché vengono forniti da Microsoft Azure. Ciò rende questa soluzione cloud più veloce da distribuire e più semplice da gestire.

- **Autenticazione basata sul cloud**: Azure Information Protection usa Azure AD per l'autenticazione di utenti interni e di utenti di altre organizzazioni. Ciò consente di eseguire l'autenticazione degli utenti mobili anche quando non sono connessi alla rete interna e rende più facile la condivisione di contenuto protetto con utenti di altre organizzazioni. Molte organizzazioni che eseguono servizi Azure o usano Office 365 hanno già account utente in Azure AD. In caso contrario, RMS per utenti singoli consente di creare un account gratuito. Per condividere contenuto protetto tramite AD RMS con un'altra organizzazione è necessario configurare trust espliciti con ogni organizzazione.

- **Supporto integrato per dispositivi mobili**: non è necessaria alcuna modifica alla distribuzione di Azure RMS per supportare dispositivi mobili e computer Mac. Per supportare questi dispositivi con AD RMS, è necessario installare l'estensione per dispositivi mobili, configurare AD FS per la federazione e creare record aggiuntivi per il servizio DNS pubblico.

- **Modelli predefiniti**: Azure Information Protection crea due modelli predefiniti al momento dell'attivazione del servizio di protezione consentendo di proteggere immediatamente i dati importanti. Non sono disponibili modelli predefiniti per AD RMS.

- **Modelli di reparto**: Azure Information Protection supporta i modelli di reparto come impostazione di configurazione per modelli aggiuntivi creati. Questa impostazione consente di specificare gli utenti per i quali il modello è visibile nelle applicazioni client, ad esempio nelle app di Office, rendendo più semplice per gli utenti la selezione dei criteri corretti definiti per i diversi gruppi di utenti. AD RMS non supporta i modelli di reparto.

- **Rilevamento e revoca dei documenti**: Azure Information Protection supporta queste funzionalità con il client Azure Information Protection, mentre AD RMS non le supporta.

- **Classificazione e assegnazione di etichette**: Azure Information Protection supporta queste funzionalità con il client Azure Information Protection che si integra con le applicazioni di Office ed Esplora file, mentre AD RMS non le supporta.


Inoltre, poiché è un servizio cloud, Azure Information Protection può distribuire nuove funzionalità e correzioni in modo più rapido rispetto a una soluzione locale basata su server. Non sono previste nuove funzionalità per AD RMS in Windows Server 2016.

Per altre informazioni e differenze, vedere la tabella seguente per un confronto delle funzionalità e dei vantaggi offerti da Azure Information Protection e AD RMS. Per domande di confronto specifiche sulla sicurezza, vedere la sezione [Controlli crittografici per la firma e la crittografia](#cryptographic-controls-for-signing-and-encryption) in questo articolo.

> [!NOTE]
> Per un confronto più agevole, alcune delle informazioni riportate di seguito sono tratte da [Requisiti per Azure Information Protection](../get-started/requirements-azure-rms.md). Fare riferimento a tale articolo per informazioni più specifiche sul supporto e le versioni di [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)].

|Azure Information Protection|AD RMS|
|-----------------------------------------------------------------------------------------|--------------------------------------------------------|
|Supporta le funzionalità IRM (Information Rights Management) nei Microsoft Online Services come Exchange Online e SharePoint Online, nonché Office 365.<br /><br />Supporta inoltre i prodotti server Microsoft locali, ad esempio Exchange Server, SharePoint Server e i file server che eseguono Windows Server e l'infrastruttura di classificazione file.|Supporta i prodotti server Microsoft locali, ad esempio Exchange Server, SharePoint Server e i file server che eseguono Windows Server e l'infrastruttura di classificazione file.|
|Consente il trust implicito tra le organizzazioni e gli utenti in qualsiasi organizzazione. Questo significa che è possibile condividere il contenuto protetto tra gli utenti all'interno della stessa organizzazione o in organizzazioni diverse quando gli utenti dispongono di [!INCLUDE[o365_1](../includes/o365_1_md.md)] o [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] oppure si iscrivono a RMS per singoli.|I trust devono essere definiti in modo esplicito in una relazione punto a punto diretta tra due organizzazioni mediante domini utente affidabili o trust federativi creati mediante Active Directory Federation Services (AD FS).|
|Fornisce due modelli predefiniti di criteri per i diritti di utilizzo che limitano l'accesso al contenuto per l'organizzazione: uno fornisce la visualizzazione in sola lettura del contenuto protetto e l'altro fornisce le autorizzazioni di scrittura o modifica del contenuto protetto.<br /><br />È anche possibile creare modelli personalizzati, inclusi modelli di reparto, visibili solo per un sottoinsieme di utenti. Per altre informazioni, vedere [Configurazione e gestione dei modelli per Azure Information Protection](../deploy-use/configure-policy-templates.md).<br /><br />Gli utenti inoltre possono definire un proprio set di autorizzazioni se i modelli non sono sufficienti.|Non sono disponibili modelli predefiniti; è quindi necessario crearli e distribuirli. Per altre informazioni, vedere [Considerazioni sui modelli di criteri di AD RMS](http://go.microsoft.com/fwlink/?LinkId=154765).<br /><br />Gli utenti inoltre possono definire un proprio set di autorizzazioni se i modelli non sono sufficienti.|
|La versione minima supportata di Microsoft Office è Office 2010, che richiede il [client Azure Information Protection](../rms-client/aip-client.md) o l'applicazione RMS sharing.<br /><br />Microsoft Office per Mac:<br /><br />- Microsoft Office per Mac 2016: supportato<br /><br />- Microsoft Office per Mac 2011: non supportato|La versione minima supportata di Microsoft Office è Office 2007.<br /><br />Microsoft Office per Mac:<br /><br />- Microsoft Office per Mac 2016: supportato<br /><br />- Microsoft Office per Mac 2011: supportato|
|Supporta il [client Azure Information Protection](../rms-client/aip-client.md) per Windows, iOS e Android. I computer Mac e i dispositivi Windows Phone continuano a essere supportati dall'app RMS sharing.<br /><br />Il client Azure Information Protection supporta inoltre quanto segue:<br /><br />- Condivisione con utenti di un'altra organizzazione.<br /><br />- Sito di rilevamento dei documenti per gli utenti che include la possibilità di revocare un documento.|Supporta il [client Azure Information Protection](../rms-client/aip-client.md) per Windows, iOS e Android. I computer Mac e i dispositivi Windows Phone continuano a essere supportati dall'app RMS sharing. Non sono tuttavia supportati la condivisione con persone di un'altra organizzazione, il sito di rilevamento dei documenti e la possibilità per gli utenti di revocare i documenti.|
|Con il client Azure Information Protection è possibile classificare e proteggere la maggior parte dei [tipi di file](../rms-client/client-admin-guide-file-types.md).<br /><br />Per altre applicazioni, controllare la tabella [Requisiti per Azure RMS: applicazioni](../get-started/requirements-applications.md).|Con il client Azure Information Protection è possibile proteggere la maggior parte dei [tipi di file](../rms-client/client-admin-guide-file-types.md).<br /><br />Per altre applicazioni, controllare la tabella [Requisiti per Azure RMS: applicazioni](../get-started/requirements-applications.md).|
|La versione minima supportata del client Windows è Windows 7 SP1.|La versione minima supportata del client Windows è Windows Vista Service Pack 2.|
|Il supporto dei dispositivi mobili include Windows Phone, Android, iOS e Windows RT.<br /><br />In tutte le piattaforme per dispositivi mobili che supportano il protocollo Exchange ActiveSync IRM è garantito anche il supporto per la posta elettronica tramite tale protocollo.|Il supporto dei dispositivi mobili include Windows Phone, Android, iOS e Windows RT e richiede l'[estensione per dispositivo mobile di Active Directory Rights Management Services](http://technet.microsoft.com/library/dn673574.aspx).<br /><br />La posta elettronica mediante IRM di Exchange ActiveSync è supportata in tutte le piattaforme di dispositivi mobili che supportano questo protocollo.|
|Supporta Multi-Factor Authentication (MFA) per i computer e dispositivi mobili.<br /><br />Per altre informazioni, vedere [Multi-Factor Authentication (MFA) e Azure Information Protection](../get-started/requirements-azure-ad.md#multi-factor-authentication-mfa-and-azure-information-protection).|Supporta l'autenticazione con smart card se IIS è configurato per richiedere i certificati.|
|Supporta la modalità crittografia 2 senza configurazioni aggiuntive, pertanto è garantita una sicurezza più avanzata per la lunghezza delle chiavi e gli algoritmi di crittografia.<br /><br />Per altre informazioni, vedere la sezione [Controlli crittografici per la firma e la crittografia](#cryptographic-controls-for-signing-and-encryption) di questo articolo e [Modalità crittografia di AD RMS](http://go.microsoft.com/fwlink/?LinkId=266659).|Supporta la modalità crittografia 1 per impostazione predefinita e richiede configurazioni aggiuntive per supportare la modalità crittografia 2 per una sicurezza più avanzata.<br /><br />Per altre informazioni, vedere la sezione [Controlli crittografici per la firma e la crittografia](#cryptographic-controls-for-signing-and-encryption) di questo articolo e [Modalità crittografia di AD RMS](http://go.microsoft.com/fwlink/?LinkId=266659).|
|Supporta la migrazione da AD RMS e, se richiesto, ad AD RMS:<br /><br />- [Migrazione da AD RMS ad Azure Information Protection](../plan-design/migrate-from-ad-rms-to-azure-rms.md)<br /><br />- [Rimozione delle autorizzazioni e disattivazione di Azure Information Protection](../deploy-use/decommission-deactivate.md)|Supporta la migrazione da e verso Azure Information Protection:<br /><br />- [Rimozione delle autorizzazioni e disattivazione di Azure Rights Management](../deploy-use/decommission-deactivate.md)<br /><br />- [Migrazione da AD RMS ad Azure Information Protection](../plan-design/migrate-from-ad-rms-to-azure-rms.md)|
|Per proteggere il contenuto, è richiesta una licenza di Azure Information Protection o Azure Rights Management con Office 365. Per utilizzare il contenuto protetto da Azure Information Protection (inclusi gli utenti di un'altra organizzazione) non è necessaria alcuna licenza.<br /><br />Per altre informazioni, vedere l'[elenco delle funzionalità](https://www.microsoft.com/cloud-platform/azure-information-protection-features) nel sito Azure Information Protection.|Richiede una licenza di RMS per proteggere il contenuto e di utilizzare il contenuto protetto da RMS di AD.<br /><br />Per ulteriori informazioni sulle licenze per AD RMS, vedere [Licenze di accesso client e gestione delle licenze](https://www.microsoft.com/en-us/Licensing/product-licensing/client-access-license.aspx) per informazioni di carattere generale, ma contattare il partner Microsoft o il rappresentante Microsoft per informazioni specifiche.|

## <a name="cryptographic-controls-for-signing-and-encryption"></a>Controlli crittografici per la firma e la crittografia
Per impostazione predefinita, Azure Information Protection usa RSA 2048 per la crittografia a chiave pubblica e SHA 256 per le operazioni di firma. AD RMS invece supporta RSA 1024 e RSA 2048, nonché SHA 1 o SHA 256 per le operazioni di firma.

Azure Information Protection e AD RMS usano entrambi AES 128 per la crittografia simmetrica.

Azure Information Protection è conforme a FIPS 140-2 se la dimensione della chiave del tenant è 2048 bit, ovvero l'impostazione predefinita al momento dell'attivazione del servizio Azure Rights Management. 

Per altre informazioni sui controlli crittografici, vedere [Controlli crittografici usati in Azure RMS: algoritmi e lunghezze delle chiavi](how-does-it-work.md#cryptographic-controls-used-by-azure-rms-algorithms-and-key-lengths).


## <a name="next-steps"></a>Passaggi successivi
Se si vuole passare da AD RMS ad Azure Information Protection, vedere [Migrazione da AD RMS ad Azure Information Protection](../plan-design/migrate-from-ad-rms-to-azure-rms.md).

[!INCLUDE[Commenting house rules](../includes/houserules.md)]

