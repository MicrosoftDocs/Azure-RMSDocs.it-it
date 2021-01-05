---
title: Requisiti per Azure Information Protection - AIP
description: Identificare i prerequisiti necessari per distribuire Azure Information Protection nell'organizzazione.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 11/19/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: dc78321d-d759-4653-8818-80da74b6cdeb
ms.subservice: prereqs
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 229b67b152845cfb1e0499f1df9eb08ba28b49df
ms.sourcegitcommit: 73befea74644d272e2d8d1d4b95df55c7741ccbe
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/24/2020
ms.locfileid: "97762309"
---
# <a name="azure-information-protection-requirements"></a>Requisiti per Azure Information Protection

>****Si applica a** _: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)_
>
>***Rilevante per**: [Client di etichettatura unificata di AIP e client classico di AIP](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients).*

Prima di distribuire Azure Information Protection, assicurarsi che il sistema soddisfi i prerequisiti seguenti:

- [Sottoscrizione di Azure Information Protection](#subscription-for-azure-information-protection)
- [Azure Active Directory](#azure-active-directory)
- [Dispositivi client](#client-devices)
- [Applicazioni](#applications)
- [Firewall e infrastruttura di rete](#firewalls-and-network-infrastructure)

## <a name="subscription-for-azure-information-protection"></a>Sottoscrizione di Azure Information Protection

È necessario avere uno dei seguenti elementi, a seconda delle funzionalità di Azure Information Protection in uso:

- **Un [piano di Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection/)** . Obbligatorio per la classificazione, l'etichettatura e la protezione tramite lo scanner o il client di Azure Information Protection.

- **Un [piano di Office 365 che include Azure Information Protection](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)** . Obbligatorio solo per la protezione.

Per verificare se la sottoscrizione include le funzionalità di Azure Information Protection da usare, esaminare l'elenco delle funzionalità in [Prezzi di Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection).

Per domande sulle licenze, leggere le [domande frequenti](https://azure.microsoft.com/pricing/details/information-protection#faq) sulle licenze.

> [!TIP]
> Per verificare se il proprio piano supporta le [nuove funzionalità di Office 365 Message Encryption](https://techcommunity.microsoft.com/t5/Security-Privacy-and-Compliance/Email-Encryption-and-Rights-Protection/ba-p/110801) per inviare messaggi di posta elettronica protetti a indirizzi di posta elettronica personali, ad esempio, Gmail, Yahoo e Microsoft, vedere le risorse seguenti:
>
> - [Descrizione del servizio Exchange Online](/office365/servicedescriptions/exchange-online-service-description/exchange-online-service-description)
>
> - [Microsoft 365 Compliance Licensing Comparison](/office365/servicedescriptions/microsoft-365-service-descriptions/microsoft-365-business-service-description)
>
> - [Office 365 Education](/office365/servicedescriptions/office-365-platform-service-description/office-365-education)
>
> - [Office 365 US Government](/office365/servicedescriptions/office-365-platform-service-description/office-365-us-government/office-365-us-government)

Non pubblicare eventuali domande sulle sottoscrizioni o sulle licenze in questa pagina. Cercare invece le risposte nelle [domande frequenti](https://azure.microsoft.com/pricing/details/information-protection#faq) per le licenze. Per domande senza risposta, contattare l'Account Manager designato da Microsoft o il [supporto tecnico Microsoft](information-support.md#to-contact-microsoft-support).

## <a name="azure-active-directory"></a>Azure Active Directory

Per supportare l'autenticazione e l'autorizzazione per Azure Information Protection, è necessario avere Azure Active Directory (Azure AD). Per usare gli account utente dalla directory locale (AD DS), è necessario anche configurare l'integrazione delle directory.

- L'accesso **Single Sign-On (SSO)** è supportato per Azure Information Protection, in modo che agli utenti non vengono richieste ripetutamente le credenziali. Se si usa la soluzione di un altro fornitore per la federazione, verificare con il fornitore come configurarla per Azure AD. WS-Trust è un requisito comune per queste soluzioni per il supporto di Single Sign-On. 

- L'**autenticazione a più fattori (MFA)** è supportata in Azure Information Protection quando si ha il software client richiesto e l'infrastruttura di supporto MFA è configurata correttamente.

L'accesso condizionale è supportato in anteprima per i documenti protetti da Azure Information Protection. Per altre informazioni, vedere: [Azure Information Protection è elencata come un'app cloud disponibile per l'accesso condizionale, come funziona?](faqs.md#i-see-azure-information-protection-is-listed-as-an-available-cloud-app-for-conditional-accesshow-does-this-work)

Per scenari specifici sono necessari altri prerequisiti, ad esempio quando si usa l'autenticazione basata su certificato o a più fattori, quando i valori UPN non corrispondono agli indirizzi di posta elettronica degli utenti o quando si usa [Office 2010](known-issues.md#aip-for-windows-and-office-versions-in-extended-support).

Per altre informazioni, vedere:

- [Requisiti aggiuntivi di Azure AD per Azure Information Protection](requirements-azure-ad.md).
- [Che cos'è una directory di Azure AD?](/azure/active-directory/fundamentals/active-directory-whatis)
- [Integrare i domini di Active Directory locali con Azure Active Directory](/azure/architecture/reference-architectures/identity/azure-ad).

## <a name="client-devices"></a>Dispositivi client

I computer o i dispositivi mobili degli utenti devono eseguire un sistema operativo che supporta Azure Information Protection.

- [Sistemi operativi supportati per i dispositivi client](#supported-operating-systems-for-client-devices)
- [Macchine virtuali](#virtual-machines)
- [Supporto server](#server-support)
- [Requisiti aggiuntivi per i singoli client](#additional-requirements-per-client)

### <a name="supported-operating-systems-for-client-devices"></a>Sistemi operativi supportati per i dispositivi client

I client di Azure Information Protection per Windows sono supportati dai sistemi operativi seguenti:

- **Windows 10** (x86, x64). La scrittura manuale non è supportata nella build RS4 di Windows 10 e successive.
 
- **Windows 8.1** (x86, x64)

- **Windows 8** (x86, x64)

- **Windows Server 2019**

- **Windows Server 2016**

- **Windows Server 2012 R2** e **Windows Server 2012**

Per informazioni dettagliate sul supporto nelle versioni precedenti di Windows, contattare l'account o il rappresentante del supporto tecnico Microsoft.

> [!NOTE]
> Quando i client di Azure Information Protection proteggono i dati tramite il servizio Azure Rights Management, i dati possono essere usati dagli [stessi dispositivi](#client-devices) che supportano il servizio Azure Rights Management.
>
### <a name="arm64"></a>ARM64 

ARM64 **non** è attualmente supportato. 

### <a name="virtual-machines"></a>Macchine virtuali

Se si usano macchine virtuali, controllare con il fornitore del software per la soluzione desktop virtuale se sono necessarie configurazioni aggiuntive per l'esecuzione dell'etichettatura unificata di Azure Information Protection o del client di Azure Information Protection. 

Ad esempio, per le soluzioni Citrix può essere necessario [disabilitare gli hook dell'API Citrix](https://support.citrix.com/article/CTX107825) per Office, il client dell'etichettatura unificata di Azure Information Protection o il client di Azure Information Protection. 

Queste applicazioni usano rispettivamente i file seguenti: **winword.exe**, **excel.exe**, **outlook.exe**, **powerpnt.exe**, **msip.app.exe**, **msip.viewer.exe**

### <a name="server-support"></a>Supporto server

Per ogni versione del server elencata sopra, i client di Azure Information Protection sono supportati per Servizi Desktop remoto. 

Se si eliminano profili utente quando si usano i client di Azure Information Protection con Servizi Desktop remoto, non eliminare la cartella **%Appdata%\Microsoft\Protect**.

Inoltre, Server Core e Nano Server non sono supportati.

### <a name="additional-requirements-per-client"></a>Requisiti aggiuntivi per i singoli client

Ogni client di Azure Information Protection ha requisiti aggiuntivi. Per informazioni dettagliate, vedere:

- [Requisiti per il client di etichettatura unificata di Azure Information Protection](./rms-client/reqs-ul-client.md)

- [Requisiti per il client di Azure Information Protection](./rms-client/client-admin-guide-install.md#additional-prerequisites-for-the-azure-information-protection-client)

## <a name="applications"></a>Applicazioni

I client di Azure Information Protection consentono di etichettare e proteggere documenti e messaggi di posta elettronica usando Microsoft **Word**, **Excel**, **PowerPoint** e **Outlook** di una delle edizioni di Office seguenti:

- **App di Office** per le versioni elencate nella [tabella delle versioni supportate di Microsoft 365 App in base al canale di aggiornamento](/officeupdates/update-history-microsoft365-apps-by-date), da Microsoft 365 Apps for business o Microsoft 365 Business Premium quando all'utente è assegnata una licenza per Azure Rights Management (noto anche come Azure Information Protection per Office 365)

- **Microsoft 365 Apps for enterprise**

- **Office Professional Plus 2019**

- **Office Professional Plus 2016**

- **Office Professional Plus 2013 con Service Pack 1**

- **Office Professional Plus 2010 con Service Pack 2**

Con le altre edizioni di Office non è possibile proteggere i documenti e i messaggi di posta elettronica usando un servizio Rights Management. Per queste edizioni, Azure Information Protection è supportato solo per la classificazione e le etichette che applicano la protezione non vengono visualizzate per gli utenti. 

Le etichette vengono visualizzate in una barra nella parte superiore del documento di Office, accessibile tramite il pulsante **Riservatezza** nel client di etichettatura unificata o il pulsante **Proteggi** nel client classico.

Per altre informazioni, vedere [Applicazioni che supportano la protezione dati di Azure Rights Management](requirements-applications.md) e [AIP per versioni di Windows e di Office con supporto "Extended"](known-issues.md#aip-for-windows-and-office-versions-in-extended-support).

### <a name="office-features-and-capabilities-not-supported"></a>Funzionalità e capacità di Office non supportate

- I client di Azure Information Protection per Windows non supportano più versioni di Office nello stesso computer o il passaggio da un account utente a un altro in Office.

- La funzionalità di [stampa unione](https://support.office.com/article/use-mail-merge-for-bulk-email-letters-labels-and-envelopes-f488ed5b-b849-4c11-9cff-932c49474705) di Office non è supportata con alcuna funzionalità di Azure Information Protection.

## <a name="firewalls-and-network-infrastructure"></a>Firewall e infrastruttura di rete

Se si ha un firewall o simili dispositivi di rete intermedi che devono essere configurati per consentire connessioni specifiche, i requisiti di connettività di rete sono descritti nell'articolo di Office seguente: [Microsoft 365 Common e Office Online](/office365/enterprise/urls-and-ip-address-ranges#microsoft-365-common-and-office-online).

Azure Information Protection ha i requisiti aggiuntivi seguenti:

- **Client di etichettatura unificata**. Per scaricare le etichette e i criteri delle etichette, consentire l'URL seguente tramite HTTPS: **_.protection.outlook.com_*

- **Proxy Web**. Se si usa un proxy Web che richiede l'autenticazione, è necessario configurare il proxy per l'uso dell'autenticazione integrata di Windows con le credenziali di accesso di Active Directory dell'utente.

    Per supportare i file **Proxy.pac** quando si usa un proxy per acquisire un token, aggiungere la nuova chiave del Registro di sistema seguente:

    - **Percorso**: `Computer\HKEY_LOCAL_MACHINE\SOFTWARE\WOW6432Node\Microsoft\MSIP\`
    - **Chiave**: `UseDefaultCredentialsInProxy`
    - **Tipo**: `DWORD`
    - **Valore**: `1`
    
- **Connessioni da client a servizio TLS**. Non terminare le connessioni da client a servizio TLS, ad esempio per il controllo a livello di pacchetti, all'URL **aadrm.com**. Se si terminano le connessione, viene interrotta l'associazione dei certificati usati dai client RMS con le autorità di certificazione gestite da Microsoft per contribuire a proteggere le comunicazioni con il servizio Azure Rights Management.
     
    Per determinare se la connessione client viene terminata prima che raggiunga il servizio Azure Rights Management, usare i comandi di PowerShell seguenti:

    ```PowerShell
    $request = [System.Net.HttpWebRequest]::Create("https://admin.na.aadrm.com/admin/admin.svc")
    $request.GetResponse()
    $request.ServicePoint.Certificate.Issuer
    ```

    Il risultato dovrebbe indicare che la CA emittente è una CA Microsoft, ad esempio: `CN=Microsoft Secure Server CA 2011, O=Microsoft Corporation, L=Redmond, S=Washington, C=US`. 
    
    Se la CA emittente non è Microsoft, è probabile che la connessione protetta da client a servizio venga terminata e richieda una riconfigurazione nel firewall.

- **TLS versione 1.2 o successiva** (solo client di etichettatura unificata). Il client di etichettatura unificata richiede TLS versione 1.2 o successiva per garantire l'uso di protocolli crittograficamente sicuri e l'allineamento alle linee guida per la sicurezza di Microsoft.

### <a name="coexistence-of-ad-rms-with-azure-rms"></a>Coesistenza di AD RMS con Azure RMS

L'uso di AD RMS e Azure RMS nella stessa organizzazione per proteggere il contenuto dello stesso utente nella stessa organizzazione, è supportato **solo** in AD RMS per la [protezione HYOK (Hold your own key)](configure-adrms-restrictions.md) con Azure Information Protection.

Questo scenario *non* è supportato durante la [migrazione](migrate-from-ad-rms-to-azure-rms.md).
I percorsi di migrazione supportati includono:

* [Da AD RMS ad Azure Information Protection](migrate-from-ad-rms-to-azure-rms.md)

* [Da Azure Information Protection ad AD RMS](/powershell/module/aipservice/Set-AipServiceMigrationUrl)

> [!TIP]
> Se si distribuisce Azure Information Protection e poi si decide di interrompere l'uso del servizio cloud, vedere [Rimozione delle autorizzazioni e disattivazione di Azure Information Protection](decommission-deactivate.md).

Per altri scenari non di migrazione in cui entrambi i servizi sono attivi nella stessa organizzazione, entrambi i servizi devono essere configurati in modo che solo uno di essi consenta a un determinato utente di proteggere il contenuto. Configurare questo tipo di scenari come segue:

* Usare i reindirizzamenti per una [migrazione da AD RMS ad Azure RMS](migrate-from-ad-rms-to-azure-rms.md)

* Se entrambi i servizi devono essere attivi contemporaneamente per utenti diversi, usare le configurazioni lato servizio per imporre l'esclusività.  Usare i controlli di onboarding di Azure RMS nel servizio cloud e un elenco di controllo di accesso (ACL) nell'URL di pubblicazione per impostare la modalità di **sola lettura** per AD RMS.

### <a name="service-tags"></a>Tag di servizio

Se si usa un endpoint Azure e un gruppo di sicurezza di rete, assicurarsi di consentire l'accesso a tutte le porte per i tag del servizio seguenti:

- **AzureInformationProtection**
- **AzureActiveDirectory**
- **AzureFrontDoor.Frontend**

In questo caso il servizio Azure Information Protection dipende anche da due indirizzi IP specifici:

 - **13.107.6.181** 
 - **13.107.9.181**
 - **Porta 443** per il traffico HTTPS

Assicurarsi di creare regole per consentire l'accesso in uscita a questi indirizzi IP specifici e tramite questa porta.

## <a name="supported-on-premises-servers-for-azure-rights-management-data-protection"></a>Server locali supportati per la protezione dati di Azure Rights Management

I server locali seguenti sono supportati con Azure Information Protection quando si usa il connettore di Azure Rights Management.

Il connettore funge da interfaccia di comunicazione ed esegue l'inoltro tra i server locali e il servizio Azure Rights Management usato da Azure Information Protection per proteggere messaggi di posta elettronica e documenti di Office. 

Per usare questo connettore, è necessario configurare la sincronizzazione delle directory tra le foreste Active Directory e Azure Active Directory.

I server supportati includono:

|Tipo di server  |Versioni supportate  |
|---------|---------|
|**Exchange Server**     | - Exchange Server 2016 </br>- Exchange Server 2013 </br>- Exchange Server 2010       |
|**Office SharePoint Server**     |- Office SharePoint Server 2016 </br>- Office SharePoint Server 2013 </br>- Office SharePoint Server 2010         |
|**File server che eseguono Windows Server e usano la funzionalità Infrastruttura di classificazione file**     |- Windows Server 2016 </br>- Windows Server 2012 R2 </br>- Windows Server 2012       |
| | |

Per ulteriori informazioni, vedere [Distribuzione del connettore di Azure Rights Management](deploy-rms-connector.md).

## <a name="supported-operating-systems-for-azure-rights-management"></a>Sistemi operativi supportati per Azure Rights Management

I sistemi operativi seguenti supportano il servizio Azure Rights Management che offre la protezione dati per AIP:

|OS  |Versioni supportate  |
|---------|---------|
|**Computer Windows**     |- Windows 7 (x86, x64) </br>- Windows 8 (x86, x64) </br>- Windows 8.1 (x86, x64) </br>- Windows 10 (x86, x64)       | 
|**macOS**     |   la versione minima di macOS è 10.8 (Mountain Lion)      |
|**Telefoni e tablet Android**     | Versione minima di Android: 6.0        |
|**iPhone e iPad**     | Versione minima di iOS: 11.0        |
|**Telefoni e tablet Windows** | Windows 10 Mobile|
| | |



## <a name="next-steps"></a>Passaggi successivi

Dopo aver esaminato tutti i requisiti di AIP e aver verificato che il sistema sia conforme, continuare con [Preparazione di utenti e gruppi per Azure Information Protection](prepare.md).