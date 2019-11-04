---
title: Confrontare Azure Information Protection e AD RMS - AIP
description: Se già si conosce o si è distribuito in precedenza Active Directory Rights Management Services (AD RMS), è possibile chiedersi quali siano le differenze con Azure Information Protection in termini di funzionalità e requisiti.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 10/23/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 8123bd62-1814-4d79-b306-e20c1a00e264
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: d0cd811adcd773446c60a3442bb5687210931ed0
ms.sourcegitcommit: fbd1834eaacb17857e59421d7be0942a9a0eefb2
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/02/2019
ms.locfileid: "73444836"
---
# <a name="comparing-azure-information-protection-and-ad-rms"></a>Confronto tra Azure Information Protection e AD RMS

>*Si applica a: Active Directory Rights Management Services, [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

Se già si conosce o si è distribuito in precedenza Active Directory Rights Management Services (AD RMS), è possibile chiedersi quali siano le differenze con Azure Information Protection in termini di funzionalità e requisiti come soluzione di protezione delle informazioni.

Di seguito sono descritte alcune delle differenze principali di Azure Information Protection:

- **Nessuna infrastruttura server necessaria**: Azure Information Protection non richiede i server aggiuntivi e i certificati PKI richiesti da AD RMS, poiché vengono forniti da Microsoft Azure. Ciò rende questa soluzione cloud più veloce da distribuire e più semplice da gestire.

- **Autenticazione basata sul cloud**: Azure Information Protection usa Azure AD per l'autenticazione di utenti interni e di utenti di altre organizzazioni. Ciò significa che gli utenti possono essere autenticati anche quando non sono connessi alla rete interna ed è più facile condividere il contenuto protetto con gli utenti di altre organizzazioni. Molte organizzazioni che eseguono servizi Azure o usano Office 365 hanno già account utente in Azure AD. In caso contrario, RMS per utenti singoli consente agli utenti di creare un account gratuito oppure è possibile usare un account Microsoft per le [applicazioni che supportano questo tipo di autenticazione per Azure Information Protection](secure-collaboration-documents.md#supported-scenarios-for-opening-protected-documents). In confronto, per condividere AD RMS contenuto protetto con un'altra organizzazione, è necessario configurare trust espliciti a ogni organizzazione.

- **Supporto incorporato per i dispositivi mobili**: non sono necessarie modifiche alla distribuzione per Azure Information Protection supportare i dispositivi mobili e i computer Mac. Per supportare questi dispositivi con AD RMS, è necessario installare l'estensione per dispositivi mobili, configurare AD FS per la federazione e creare record aggiuntivi per il servizio DNS pubblico.

- **Modelli predefiniti**: Azure Information Protection crea automaticamente modelli predefiniti che limitano l'accesso al contenuto alla propria organizzazione. Questi modelli consentono di iniziare a proteggere immediatamente i dati sensibili. Non sono disponibili modelli predefiniti per AD RMS.

- **Modelli di reparto**: noti anche come modelli con ambito. Azure Information Protection supporta i modelli di reparto per i modelli aggiuntivi che vengono creati. Questa configurazione consente di specificare un sottoinsieme di utenti che possono visualizzare modelli specifici nelle applicazioni client. Limitando il numero di modelli che gli utenti visualizzano, si semplifica la selezione dei criteri corretti definiti per i diversi gruppi di utenti. AD RMS non supporta i modelli di reparto.

- **Rilevamento e revoca dei documenti**: Azure Information Protection supporta queste funzionalità con il client di Azure Information Protection (classico), mentre ad RMS No.

- **Classificazione e assegnazione di etichette**: Azure Information Protection supporta le etichette che applicano la classificazione e, facoltativamente, la protezione. Queste funzionalità sono fornite con il [client di Azure Information Protection (classico) e il client di Azure Information Protection Unified Labeling](./rms-client/use-client.md#choose-which-labeling-client-to-use-for-windows-computers). Usando questi client, la classificazione e l'assegnazione di etichette possono essere integrate con le applicazioni di Office, Esplora file, PowerShell e uno scanner per gli archivi dati locali. AD RMS non supporta le funzionalità di classificazione e assegnazione di etichette.

Inoltre, poiché è un servizio cloud, Azure Information Protection può distribuire nuove funzionalità e correzioni in modo più rapido rispetto a una soluzione locale basata su server. Non sono previste nuove funzionalità per AD RMS in Windows Server.

Per altre differenze, usare la tabella seguente per un confronto affiancato. Per domande di confronto specifiche sulla sicurezza, vedere la sezione [Controlli crittografici per la firma e la crittografia](#cryptographic-controls-for-signing-and-encryption) in questo articolo.

|Azure Information Protection|RMS di AD|
|-----------------------------------------------------------------------------------------|--------------------------------------------------------|
|Supporta le funzionalità IRM (Information Rights Management) nei Microsoft Online Services e nei prodotti server Microsoft locali.|Supporta le funzionalità IRM (Information Rights Management) per i prodotti server Microsoft locali ed Exchange Online.|
|Abilita automaticamente la collaborazione sicura su documenti con qualsiasi organizzazione che usa Azure AD per l'autenticazione.|La collaborazione sicura sui documenti all'esterno dell'organizzazione richiede la definizione di relazioni di trust di autenticazione in modo esplicito in una relazione point-to-point diretta tra le due organizzazioni. È necessario configurare domini utente trusted o relazioni di trust federative mediante Active Directory Federation Services (AD FS).|
|Inviare un messaggio di posta elettronica protetto (eventualmente con documenti di Office allegati protetti automaticamente) agli utenti quando non esiste alcuna relazione di trust di autenticazione. Questo scenario è reso possibile usando la federazione con provider social o un passcode monouso e un browser Web per la visualizzazione.|Non è supportato l'invio di posta elettronica protetta se non esiste alcuna relazione di trust di autenticazione.|
|Supporta il client di Azure Information Protection (classico) e il Azure Information Protection client di etichetta unificata per le attività di protezione e utilizzo.|Supporta il client di Azure Information Protection (classico) per le attività di protezione e utilizzo. <br /><br />Supporta il Azure Information Protection client unificato per l'assegnazione di etichette solo a consumo ed è necessario installare l' [estensione del dispositivo Mobile Active Directory Rights Management Services](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn673574\(v=ws.11\)).
|Supporta Multi-Factor Authentication (MFA) per i computer e dispositivi mobili.<br /><br />Per altre informazioni, vedere [Multi-Factor Authentication (MFA) e Azure Information Protection](./requirements-azure-ad.md#multi-factor-authentication-mfa-and-azure-information-protection).|Supporta l'autenticazione con smart card se IIS è configurato per richiedere i certificati.|
|Supporta la modalità crittografia 2 per impostazione predefinita per offrire un livello di sicurezza consigliato per le lunghezze delle chiavi e gli algoritmi di crittografia.|Supporta la modalità crittografia 1 per impostazione predefinita e richiede una configurazione aggiuntiva per supportare la modalità crittografia 2 per un livello di sicurezza consigliato.<br /><br />Per ulteriori informazioni, vedere [ad RMS modalità di crittografia](https://go.microsoft.com/fwlink/?LinkId=266659).|
|Richiede una licenza di Azure Information Protection o una licenza di Azure Rights Management con Office 365 per proteggere il contenuto. <br /><br />Per utilizzare il contenuto protetto da Azure Information Protection (inclusi gli utenti di un'altra organizzazione) non è necessaria alcuna licenza.<br /><br />Per ulteriori informazioni sulle licenze, incluse le differenze tra una licenza P1 e P2, vedere l' [elenco delle funzionalità](https://www.microsoft.com/cloud-platform/azure-information-protection-features) nel sito Azure Information Protection.|Richiede una licenza di RMS per proteggere il contenuto e di utilizzare il contenuto protetto da RMS di AD.<br /><br />Per ulteriori informazioni sulle licenze, vedere licenze di [accesso client e licenze di gestione](https://www.microsoft.com/en-us/Licensing/product-licensing/client-access-license.aspx) per informazioni generali, ma contattare il partner Microsoft o il rappresentante Microsoft per informazioni specifiche.|

## <a name="cryptographic-controls-for-signing-and-encryption"></a>Controlli crittografici per la firma e la crittografia
Per impostazione predefinita, Azure Information Protection usa RSA 2048 per la crittografia a chiave pubblica e SHA 256 per le operazioni di firma. AD RMS invece supporta RSA 1024 e RSA 2048, nonché SHA 1 o SHA 256 per le operazioni di firma.

Azure Information Protection e AD RMS usano entrambi AES 128 per la crittografia simmetrica.

Azure Information Protection è conforme a FIPS 140-2 se le dimensioni della chiave del tenant sono 2048 bit, ovvero l'impostazione predefinita al momento dell'attivazione del servizio Azure Rights Management. 

Per altre informazioni sui controlli crittografici, vedere [Controlli crittografici usati in Azure RMS: algoritmi e lunghezze delle chiavi](how-does-it-work.md#cryptographic-controls-used-by-azure-rms-algorithms-and-key-lengths).


## <a name="next-steps"></a>Passaggi successivi
Per informazioni più dettagliate sui requisiti per l'uso di Azure Information Protection, ad esempio il supporto dei dispositivi e le versioni minime, vedere [requisiti per l'Azure Information Protection](requirements.md).

Se si sta cercando di eseguire la migrazione da AD RMS a Azure Information Protection, vedere [migrazione da ad RMS a Azure Information Protection](migrate-from-ad-rms-to-azure-rms.md).

Potrebbero essere interessati le domande frequenti seguenti:
- [Qual è la differenza tra Azure Information Protection e Microsoft Information Protection?](faqs.md#whats-the-difference-between-azure-information-protection-and-microsoft-information-protection)
- [Qual è la differenza tra Azure Information Protection e Rights Management di Azure?](faqs.md#whats-the-difference-between-azure-information-protection-and-azure-rights-management)

