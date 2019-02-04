---
title: Confrontare Azure Information Protection e AD RMS - AIP
description: Se già si conosce o si è distribuito in precedenza Active Directory Rights Management Services (AD RMS), è possibile chiedersi quali siano le differenze con Azure Information Protection in termini di funzionalità e requisiti.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 01/25/2019
ms.topic: conceptual
ms.service: information-protection
ms.assetid: 8123bd62-1814-4d79-b306-e20c1a00e264
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: ffaa0f341cbe9fd59a63c27b4114923049efcdc6
ms.sourcegitcommit: b1e08bc29d50187532f00dc215ab331e0a7dbebe
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/28/2019
ms.locfileid: "55146690"
---
# <a name="comparing-azure-information-protection-and-ad-rms"></a>Confronto tra Azure Information Protection e AD RMS

>*Si applica a: Active Directory Rights Management Services, [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

Se già si conosce o si è distribuito in precedenza Active Directory Rights Management Services (AD RMS), è possibile chiedersi quali siano le differenze con Azure Information Protection in termini di funzionalità e requisiti come soluzione di protezione delle informazioni.

Di seguito sono descritte alcune delle differenze principali di Azure Information Protection:

- **Non è richiesta un'infrastruttura server**: Azure Information Protection non richiede i server aggiuntivi e i certificati PKI richiesti da AD RMS, poiché vengono forniti da Microsoft Azure. Ciò rende questa soluzione cloud più veloce da distribuire e più semplice da gestire.

- **Autenticazione basata sul cloud**: Azure Information Protection usa Azure AD per l'autenticazione di utenti interni e di utenti di altre organizzazioni. Ciò consente di eseguire l'autenticazione degli utenti mobili anche quando non sono connessi alla rete interna e rende più facile la condivisione di contenuto protetto con utenti di altre organizzazioni. Molte organizzazioni che eseguono servizi Azure o usano Office 365 hanno già account utente in Azure AD. In caso contrario, RMS per utenti singoli consente agli utenti di creare un account gratuito oppure è possibile usare un account Microsoft per le [applicazioni che supportano questo tipo di autenticazione per Azure Information Protection](secure-collaboration-documents.md#supported-scenarios-for-opening-protected-documents). Per condividere contenuto protetto tramite AD RMS con un'altra organizzazione è necessario configurare trust espliciti con ogni organizzazione.

- **Supporto predefinito per dispositivi mobili**: non è necessaria alcuna modifica alla distribuzione di Azure RMS per supportare dispositivi mobili e computer Mac. Per supportare questi dispositivi con AD RMS, è necessario installare l'estensione per dispositivi mobili, configurare AD FS per la federazione e creare record aggiuntivi per il servizio DNS pubblico.

- **Modelli predefiniti**: Azure Information Protection crea modelli predefiniti al momento dell'attivazione del servizio di protezione consentendo di proteggere immediatamente i dati importanti. Non sono disponibili modelli predefiniti per AD RMS.

- **Modelli di reparto**: anche noti come modelli con ambito. Azure Information Protection supporta i modelli di reparto per i modelli aggiuntivi che vengono creati. Questa configurazione consente di specificare un sottoinsieme di utenti che possono visualizzare modelli specifici nelle applicazioni client. Limitando il numero di modelli che gli utenti visualizzano, si semplifica la selezione dei criteri corretti definiti per i diversi gruppi di utenti. AD RMS non supporta i modelli di reparto.

- **Rilevamento e revoca dei documenti**: Azure Information Protection supporta queste funzionalità con il client Azure Information Protection, mentre AD RMS non le supporta.

- **Classificazione e assegnazione di etichette**: Azure Information Protection supporta queste funzionalità con il client Azure Information Protection che si integra con le applicazioni di Office ed Esplora file, mentre AD RMS non le supporta. 


Inoltre, poiché è un servizio cloud, Azure Information Protection può distribuire nuove funzionalità e correzioni in modo più rapido rispetto a una soluzione locale basata su server. Non sono previste nuove funzionalità per AD RMS in Windows Server.

Per altre informazioni e differenze, vedere la tabella seguente per un confronto delle funzionalità e dei vantaggi offerti da Azure Information Protection e AD RMS. Per domande di confronto specifiche sulla sicurezza, vedere la sezione [Controlli crittografici per la firma e la crittografia](#cryptographic-controls-for-signing-and-encryption) in questo articolo.

> [!NOTE]
> Per un confronto più agevole, alcune delle informazioni riportate di seguito sono tratte da [Requisiti per Azure Information Protection](requirements.md). Fare riferimento a tale articolo per informazioni più specifiche sul supporto e le versioni di Azure Rights Management.

|Azure Information Protection|AD RMS|
|-----------------------------------------------------------------------------------------|--------------------------------------------------------|
|Supporta le funzionalità IRM (Information Rights Management) nei Microsoft Online Services come Exchange Online e SharePoint Online, nonché Office 365.<br /><br />Supporta inoltre i prodotti server Microsoft locali, ad esempio Exchange Server, SharePoint Server e i file server che eseguono Windows Server e l'infrastruttura di classificazione file (FCI, File Classification Infrastructure).|Supporta i prodotti server Microsoft locali, ad esempio Exchange Server, SharePoint Server e i file server che eseguono Windows Server e l'infrastruttura di classificazione file (FCI, File Classification Infrastructure).|
|Abilita automaticamente la collaborazione sicura su documenti con qualsiasi organizzazione che usa Azure AD per l'autenticazione. Questo significa che le organizzazioni possono proteggere i documenti che condividono internamente o con altre organizzazioni.|La collaborazione sicura sui documenti all'esterno dell'organizzazione richiede la definizione di relazioni di trust di autenticazione in modo esplicito in una relazione point-to-point diretta tra le due organizzazioni. È necessario configurare domini utente trusted o relazioni di trust federative mediante Active Directory Federation Services (AD FS).|
|Inviare un messaggio di posta elettronica protetto (eventualmente con documenti di Office allegati protetti automaticamente) agli utenti quando non esiste alcuna relazione di trust di autenticazione. Questo scenario è reso possibile usando la federazione con provider social o un passcode monouso e un browser Web per la visualizzazione.|Non è supportato l'invio di posta elettronica protetta se non esiste alcuna relazione di trust di autenticazione.|
|Offre modelli di protezione predefiniti che limitano l'accesso del contenuto all'organizzazione: uno che consente la visualizzazione in sola lettura del contenuto protetto e un altro modello che offre autorizzazioni di scrittura o modifica per il contenuto protetto.<br /><br />È anche possibile creare modelli personalizzati, inclusi modelli di reparto, visibili solo a un sottoinsieme di utenti. Per altre informazioni, vedere [Configurazione e gestione dei modelli per Azure Information Protection](configure-policy-templates.md).<br /><br />Gli utenti inoltre possono definire un proprio set di autorizzazioni se i modelli non sono sufficienti.|Non sono disponibili modelli predefiniti. È quindi necessario creare e distribuire modelli utente. Per altre informazioni, vedere [Considerazioni sui modelli di criteri di AD RMS](https://go.microsoft.com/fwlink/?LinkId=154765).<br /><br />Gli utenti inoltre possono definire un proprio set di autorizzazioni se i modelli non sono sufficienti.|
|La versione minima supportata di Microsoft Office è Office 2010, che richiede il [client Azure Information Protection](./rms-client/aip-client.md) o l'applicazione RMS sharing.|La versione minima supportata di Microsoft Office è Office 2010.|
|Supporta il [client Azure Information Protection](./rms-client/aip-client.md) per Windows, iOS e Android. I computer Mac continuano a essere supportati dall'app RMS sharing.<br /><br />Il client Azure Information Protection supporta inoltre quanto segue:<br /><br />- Condivisione con utenti di un'altra organizzazione.<br /><br />- Sito di rilevamento dei documenti per gli utenti che include la possibilità di revocare un documento.|Supporta il [client Azure Information Protection](./rms-client/aip-client.md) per Windows, iOS e Android. I computer Mac continuano a essere supportati dall'app RMS sharing. Non sono tuttavia supportati la condivisione con persone di un'altra organizzazione, il sito di rilevamento dei documenti e la possibilità per gli utenti di revocare i documenti.|
|Con il client Azure Information Protection è possibile classificare e proteggere la maggior parte dei [tipi di file](./rms-client/client-admin-guide-file-types.md).<br /><br />Per altre applicazioni, controllare la tabella [Requisiti per Azure RMS: applicazioni](./requirements-applications.md).|Con il client Azure Information Protection è possibile proteggere la maggior parte dei [tipi di file](./rms-client/client-admin-guide-file-types.md).<br /><br />Per altre applicazioni, controllare la tabella [Requisiti per Azure RMS: applicazioni](./requirements-applications.md).|
|La versione minima supportata del client Windows è Windows 7 SP1.|La versione minima supportata del client Windows è Windows 7 SP1.|
|Il supporto dei dispositivi mobili include Windows 10 Mobile, Android e iOS.<br /><br />In tutte le piattaforme per dispositivi mobili che supportano il protocollo Exchange ActiveSync IRM è garantito anche il supporto per la posta elettronica tramite tale protocollo.|Il supporto dei dispositivi mobili include Windows 10 Mobile, Android e iOS e richiede l'[estensione per dispositivo mobile di Active Directory Rights Management Services](https://technet.microsoft.com/library/dn673574.aspx).<br /><br />La posta elettronica mediante IRM di Exchange ActiveSync è supportata in tutte le piattaforme di dispositivi mobili che supportano questo protocollo.|
|Supporta Multi-Factor Authentication (MFA) per i computer e dispositivi mobili.<br /><br />Per altre informazioni, vedere [Multi-Factor Authentication (MFA) e Azure Information Protection](./requirements-azure-ad.md#multi-factor-authentication-mfa-and-azure-information-protection).|Supporta l'autenticazione con smart card se IIS è configurato per richiedere i certificati.|
|Supporta la modalità crittografia 2 senza configurazioni aggiuntive, pertanto è garantita una sicurezza più avanzata per la lunghezza delle chiavi e gli algoritmi di crittografia.<br /><br />Per altre informazioni, vedere la sezione [Controlli crittografici per la firma e la crittografia](#cryptographic-controls-for-signing-and-encryption) di questo articolo e [Modalità crittografia di AD RMS](https://go.microsoft.com/fwlink/?LinkId=266659).|Supporta la modalità crittografia 1 per impostazione predefinita e richiede configurazioni aggiuntive per supportare la modalità crittografia 2 per una sicurezza più avanzata.<br /><br />Per altre informazioni, vedere la sezione [Controlli crittografici per la firma e la crittografia](#cryptographic-controls-for-signing-and-encryption) di questo articolo e [Modalità crittografia di AD RMS](https://go.microsoft.com/fwlink/?LinkId=266659).|
|Supporta la migrazione da AD RMS e, se richiesto, ad AD RMS:<br /><br />- [Migrazione da AD RMS ad Azure Information Protection](migrate-from-ad-rms-to-azure-rms.md)<br /><br />- [Rimozione delle autorizzazioni e disattivazione di Azure Information Protection](decommission-deactivate.md)|Supporta la migrazione da e verso Azure Information Protection:<br /><br />- [Rimozione delle autorizzazioni e disattivazione di Azure Rights Management](decommission-deactivate.md)<br /><br />- [Migrazione da AD RMS ad Azure Information Protection](migrate-from-ad-rms-to-azure-rms.md)|
|Per proteggere il contenuto, è richiesta una licenza di Azure Information Protection o Azure Rights Management con Office 365. Per utilizzare il contenuto protetto da Azure Information Protection (inclusi gli utenti di un'altra organizzazione) non è necessaria alcuna licenza.<br /><br />Per altre informazioni, vedere l'[elenco delle funzionalità](https://www.microsoft.com/cloud-platform/azure-information-protection-features) nel sito Azure Information Protection.|Richiede una licenza di RMS per proteggere il contenuto e di utilizzare il contenuto protetto da RMS di AD.<br /><br />Per ulteriori informazioni sulle licenze per AD RMS, vedere [Licenze di accesso client e gestione delle licenze](https://www.microsoft.com/en-us/Licensing/product-licensing/client-access-license.aspx) per informazioni di carattere generale, ma contattare il partner Microsoft o il rappresentante Microsoft per informazioni specifiche.|

## <a name="cryptographic-controls-for-signing-and-encryption"></a>Controlli crittografici per la firma e la crittografia
Per impostazione predefinita, Azure Information Protection usa RSA 2048 per la crittografia a chiave pubblica e SHA 256 per le operazioni di firma. AD RMS invece supporta RSA 1024 e RSA 2048, nonché SHA 1 o SHA 256 per le operazioni di firma.

Azure Information Protection e AD RMS usano entrambi AES 128 per la crittografia simmetrica.

Azure Information Protection è conforme a FIPS 140-2 se le dimensioni della chiave del tenant sono 2048 bit, ovvero l'impostazione predefinita al momento dell'attivazione del servizio Azure Rights Management. 

Per altre informazioni sui controlli crittografici, vedere [Controlli crittografici usati in Azure RMS: Algoritmi e lunghezze delle chiavi](how-does-it-work.md#cryptographic-controls-used-by-azure-rms-algorithms-and-key-lengths).


## <a name="next-steps"></a>Passaggi successivi
Se si vuole passare da AD RMS ad Azure Information Protection, vedere [Migrazione da AD RMS ad Azure Information Protection](migrate-from-ad-rms-to-azure-rms.md).


