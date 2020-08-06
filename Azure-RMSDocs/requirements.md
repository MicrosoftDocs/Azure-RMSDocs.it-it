---
title: Requisiti per Azure Information Protection - AIP
description: Identificare i prerequisiti necessari per distribuire Azure Information Protection nell'organizzazione.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 08/04/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: dc78321d-d759-4653-8818-80da74b6cdeb
ms.subservice: prereqs
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: cb55fb0acedc56c2b866d7ce681320c2dc9c2fcd
ms.sourcegitcommit: dec5df81b569283a72f0a983d3f53b82cbbc562c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/05/2020
ms.locfileid: "87802124"
---
# <a name="azure-information-protection-requirements"></a>Requisiti di Azure Information Protection

>*Si applica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

Prima di distribuire Azure Information Protection, assicurarsi che il sistema soddisfi i prerequisiti seguenti:

- [Sottoscrizione di Azure Information Protection](#subscription-for-azure-information-protection)
- [Azure Active Directory](#azure-active-directory)
- [Dispositivi client](#client-devices)
- [Applicazioni](#applications)
- [Firewall e infrastruttura di rete](#firewalls-and-network-infrastructure)

## <a name="subscription-for-azure-information-protection"></a>Sottoscrizione di Azure Information Protection

È necessario disporre di uno dei seguenti elementi, a seconda delle funzionalità di Azure Information Protection in uso:

- ** [Piano di Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection/)**. Obbligatorio per la classificazione, l'assegnazione di etichette e la protezione tramite il Azure Information Protection scanner o il client (classica o unificata con etichetta)

- ** [Piano di Office 365 che include Azure Information Protection](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)**. Obbligatorio solo per la protezione.

Per verificare che la sottoscrizione includa le funzionalità di Azure Information Protection che si desidera utilizzare, controllare l'elenco delle funzionalità [Azure Information Protection prezzi](https://azure.microsoft.com/pricing/details/information-protection).

Per domande sulle licenze, leggere le [domande frequenti](https://azure.microsoft.com/pricing/details/information-protection#faq) sulle licenze.

> [!TIP]
> Per verificare se il piano disponibile di Office 365 o la versione autonoma di Exchange Online supporta le [nuove funzionalità di Office 365 Message Encryption](https://techcommunity.microsoft.com/t5/Security-Privacy-and-Compliance/Email-Encryption-and-Rights-Protection/ba-p/110801) per inviare messaggi di posta elettronica protetti a indirizzi di posta elettronica personali, ad esempio, Gmail, Yahoo e Microsoft, vedere le risorse seguenti:
>
> - [Descrizione del servizio Exchange Online](https://technet.microsoft.com/library/exchange-online-service-description.aspx)
>
> - [Office 365 Education](https://technet.microsoft.com/library/mt844095.aspx)
>
> - [Office 365 US Government](https://technet.microsoft.com/library/mt774581.aspx)

Non pubblicare eventuali domande sulle sottoscrizioni o sulle licenze in questa pagina. Cercare invece le risposte nelle [domande frequenti](https://azure.microsoft.com/pricing/details/information-protection#faq) per le licenze. Per domande senza risposta, contattare l'Account Manager designato da Microsoft o il [supporto tecnico Microsoft](information-support.md#to-contact-microsoft-support).

## <a name="azure-active-directory"></a>Azure Active Directory

Per supportare l'autenticazione e l'autorizzazione per Azure Information Protection, è necessario disporre di un Azure Active Directory (AD). Per usare gli account utente dal Director locale (AD DS), è necessario configurare anche l'integrazione della directory.

- **Single Sign-on (SSO)** è supportato per Azure Information Protection in modo che agli utenti non vengano richieste ripetutamente le credenziali. Se si usa un'altra soluzione fornitore per la Federazione, verificare con tale fornitore la modalità di configurazione per Azure AD. WS-Trust è un requisito comune per queste soluzioni per il supporto di Single Sign-On. 

- **Multi-factor authentication** è supportato con Azure Information Protection quando si dispone del software client richiesto e l'infrastruttura di supporto per l'autenticazione a più fattori è stata configurata correttamente.

L'accesso condizionale è supportato in anteprima per i documenti protetti da Azure Information Protection. Per altre informazioni, vedere: [Azure Information Protection è elencato come app cloud disponibile per l'accesso condizionale, come funziona?](faqs.md#i-see-azure-information-protection-is-listed-as-an-available-cloud-app-for-conditional-accesshow-does-this-work)

Sono necessari altri prerequisiti per scenari specifici, ad esempio quando si usa Office 2010, basato su certificati o l'autenticazione a più fattori, oppure quando i valori UPN non corrispondono agli indirizzi di posta elettronica dell'utente. Per ulteriori informazioni, vedere [requisiti aggiuntivi Azure ad per Azure Information Protection](requirements-azure-ad.md).

Per altre informazioni, vedere:

- [Che cos'è una directory di Azure AD?](/azure/active-directory/fundamentals/active-directory-whatis)
- [Integrare domini Active Directory locali con Azure Active Directory](/azure/architecture/reference-architectures/identity/azure-ad).

## <a name="client-devices"></a>Dispositivi client

I computer utente o i dispositivi mobili devono essere eseguiti in un sistema operativo che supporta Azure Information Protection.

- [Sistemi operativi supportati per i dispositivi client](#supported-operating-systems-for-client-devices)
- [Macchine virtuali](#virtual-machines)
- [Supporto server](#server-support)
- [Requisiti aggiuntivi per client](#additional-requirements-per-client)

### <a name="supported-operating-systems-for-client-devices"></a>Sistemi operativi supportati per i dispositivi client

I sistemi operativi seguenti supportano sia l'etichetta unificata Azure Information Protection che i client di Azure Information Protection: 

- **Windows 10** (x86, x64). La grafia non è supportata nella build di Windows 10 RS4 e versioni successive.
 
- **Windows 8.1** (x86, x64)

- **Windows 8** (x86, x64)

- **Windows Server 2019**

- **Windows Server 2016**

- **Windows server 2012 R2** e **Windows Server 2012**

[Entrambi i client](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients) consentono agli utenti di classificare ed etichettare documenti e messaggi di posta elettronica.

Per informazioni dettagliate sul supporto nelle versioni precedenti di Windows, contattare il account Microsoft o il rappresentante del supporto tecnico.

> [!NOTE]
> Quando il Azure Information Protection client protegge i dati tramite il servizio Azure Rights Management, i dati possono essere usati dagli [stessi dispositivi](#client-devices) che supportano il servizio Azure Rights Management.
>

### <a name="virtual-machines"></a>Macchine virtuali
Se si lavora con macchine virtuali, controllare se il fornitore del software per la soluzione desktop virtuale è come configurazioni aggiuntive necessarie per l'esecuzione del Azure Information Protection l'assegnazione di etichette unificata o il client di Azure Information Protection. 

Per le soluzioni Citrix, ad esempio, potrebbe essere necessario [disabilitare i hook dell'API (Application Programming Interface) Citrix](https://support.citrix.com/article/CTX107825) per Office, il Azure Information Protection client di etichetta unificata o il client di Azure Information Protection. 

Queste applicazioni utilizzano rispettivamente i file seguenti: **winword.exe**, **excel.exe**, **outlook.exe**, **powerpnt.exe**, **msip.app.exe**msip.viewer.exe**msip.viewer.exe**

### <a name="server-support"></a>Supporto server

Per ognuna delle versioni server elencate in precedenza, i client Azure Information Protection sono supportati per Servizi Desktop remoto. 

Se si eliminano i profili utente quando si usa il Azure Information Protection client con Servizi Desktop remoto, non eliminare la cartella **%AppData%\Microsoft\Protect** .

Inoltre, Server Core e nano server non sono supportati.

### <a name="additional-requirements-per-client"></a>Requisiti aggiuntivi per client

Ogni client Azure Information Protection presenta prerequisiti aggiuntivi. Per informazioni dettagliate, vedere:

- [Azure Information Protection prerequisiti per l'assegnazione di etichette unificata ai client](./rms-client/clientv2-admin-guide-install.md#additional-prerequisites-for-the-azure-information-protection-unified-labeling-client)

- [Prerequisiti di Azure Information Protection client](./rms-client/client-admin-guide-install.md#additional-prerequisites-for-the-azure-information-protection-client)

## <a name="applications"></a>Applicazioni

I client Azure Information Protection possono etichettare e proteggere documenti e messaggi di posta elettronica usando Microsoft **Word**, **Excel**, **PowerPoint**e **Outlook** da una delle edizioni di Office seguenti:

- **App di Office versione minima 1805**, Build 9330,2078 da Office 365 Business o Microsoft 365 business. 

    Questa edizione è supportata solo quando all'utente viene assegnata una licenza per Azure Rights Management, nota anche come Azure Information Protection per Office 365.

- **Office 365 ProPlus**

- **Office Professional Plus 2019**

- **Office Professional Plus 2016**

- **Office Professional Plus 2013 con Service Pack 1**

- **Office Professional Plus 2010 con Service Pack 2**

Con le altre edizioni di Office non è possibile proteggere i documenti e i messaggi di posta elettronica usando un servizio Rights Management. Per queste edizioni, Azure Information Protection è supportato solo per la classificazione e le etichette che applicano la protezione non vengono visualizzate per gli utenti. 

Queste etichette verrebbero altrimenti visualizzate sulla barra del Azure Information Protection o nel client Unified Labeling sulla barra multifunzione di Office (dal pulsante **Proteggi** nel client classico o il pulsante **sensibilità** nel client Unified Labeling). 

Per altre informazioni, vedere [applicazioni che supportano la protezione dei dati di Azure Rights Management](requirements-applications.md).

### <a name="office-features-and-capabilities-not-supported"></a>Funzionalità e funzionalità di Office non supportate

- I client Azure Information Protection, incluse le etichette classiche e unificate, non supportano più versioni di Office nello stesso computer o scambiano gli account utente in Office.

- La funzionalità di Unione di Office [mail](https://support.office.com/article/use-mail-merge-for-bulk-email-letters-labels-and-envelopes-f488ed5b-b849-4c11-9cff-932c49474705) non è supportata con alcuna funzionalità Azure Information Protection.

## <a name="firewalls-and-network-infrastructure"></a>Firewall e infrastruttura di rete

Se si dispone di un firewall o di dispositivi di rete simili che sono configurati per consentire connessioni specifiche, i requisiti di connettività di rete sono elencati in questo articolo di Office: [URL e intervalli di indirizzi IP di office 365 > Microsoft 365 comuni e Office Online](https://docs.microsoft.com/office365/enterprise/urls-and-ip-address-ranges#microsoft-365-common-and-office-online).

Azure Information Protection prevede i requisiti aggiuntivi seguenti:

- **Client di etichetta unificata**. Per scaricare etichette ed etichettare i criteri, consentire l'URL seguente tramite HTTPS: ***. Protection.Outlook.com**

- **Proxy Web**. Se si usa un proxy Web che richiede l'autenticazione, è necessario configurare il proxy per l'uso dell'autenticazione integrata di Windows con le credenziali di accesso Active Directory dell'utente.

    
- **Connessioni da client a servizio TLS**. Non terminare le connessioni da client a servizio TLS, ad esempio per eseguire l'ispezione a livello di pacchetto, all'URL **AADRM.com** . Se si terminano le connessione, viene interrotta l'associazione dei certificati usati dai client RMS con le autorità di certificazione gestite da Microsoft per contribuire a proteggere le comunicazioni con il servizio Azure Rights Management.
     
    Per determinare se la connessione client viene terminata prima che raggiunga il servizio Rights Management di Azure, usare i comandi di PowerShell seguenti:

    ```ps
    $request = [System.Net.HttpWebRequest]::Create("https://admin.na.aadrm.com/admin/admin.svc")
    $request.GetResponse()
    $request.ServicePoint.Certificate.Issuer
    ```

    Il risultato dovrebbe indicare che la CA emittente è da una CA Microsoft, ad esempio: `CN=Microsoft Secure Server CA 2011, O=Microsoft Corporation, L=Redmond, S=Washington, C=US` . 
    
    Se viene visualizzato un nome della CA emittente che non è di Microsoft, è probabile che la connessione client-servizio protetta venga terminata e che sia necessaria una riconfigurazione nel firewall.

- **TLS versione 1,2 o successiva** (solo client di etichetta unificata). Il client di etichettatura unificata richiede una versione di TLS 1,2 o successiva per garantire l'uso di protocolli crittograficamente sicuri e allinearsi alle linee guida per la sicurezza di Microsoft.

### <a name="coexistence-of-ad-rms-with-azure-rms"></a>Coesistenza di AD RMS con Azure RMS

L'uso di AD RMS e Azure RMS affiancato, nella stessa organizzazione, per proteggere il contenuto dallo stesso utente nella stessa organizzazione, è supportato **solo** in ad RMS per la [protezione di HYOK (Mantieni la propria chiave)](configure-adrms-restrictions.md) con Azure Information Protection.

Questo scenario *non* è supportato durante la [migrazione](migrate-from-ad-rms-to-azure-rms.md).
I percorsi di migrazione supportati includono:

* [Da AD RMS a Azure Information Protection](migrate-from-ad-rms-to-azure-rms.md)

* [Da Azure Information Protection a AD RMS](/powershell/module/aipservice/Set-AipServiceMigrationUrl)

> [!TIP]
> Se si distribuisce Azure Information Protection e poi si decide di interrompere l'uso del servizio cloud, vedere [Rimozione delle autorizzazioni e disattivazione di Azure Information Protection](decommission-deactivate.md).

Per altri scenari non di migrazione, in cui entrambi i servizi sono attivi nella stessa organizzazione, entrambi i servizi devono essere configurati in modo che solo uno di essi consente a tutti gli utenti di proteggere il contenuto. Configurare gli scenari seguenti:

* Usare i reindirizzamenti per la [migrazione di un AD RMS Azure RMS](migrate-from-ad-rms-to-azure-rms.md)

* Se entrambi i servizi devono essere attivi contemporaneamente per utenti diversi, utilizzare le configurazioni lato servizio per applicare l'esclusività.  Usare i controlli di onboarding Azure RMS nel servizio cloud e un ACL nell'URL di pubblicazione per impostare la modalità di sola **lettura** per ad RMS.

### <a name="service-tags"></a>Tag di servizio

Assicurarsi di consentire l'accesso a tutte le porte per i seguenti tag del servizio:

- **AzureInformationProtection**
- **AzureActiveDirectory**
- **AzureFrontDoor.Frontend**

Il servizio Azure Information Protection dipende anche da due indirizzi IP specifici:
 - **13.107.6.181** 
 - **13.107.9.181**

Assicurarsi di creare regole per consentire l'accesso in uscita a questi indirizzi IP specifici.

## <a name="supported-on-premises-servers-for-azure-rights-management-data-protection"></a>Server locali supportati per la protezione dei dati Rights Management di Azure

I server locali seguenti sono supportati con Azure Information Protection quando si usa il connettore Azure Rights Management.

Questo connettore funge da interfaccia di comunicazione e inoltra tra i server locali e il servizio Azure Rights Management, che viene usato da Azure Information Protection per proteggere i documenti e i messaggi di posta elettronica di Office. 

Per usare questo connettore, è necessario configurare la sincronizzazione delle directory tra le foreste Active Directory e Azure Active Directory.

I server supportati includono:

|Tipo di server  |Versioni supportate  |
|---------|---------|
|**Exchange Server**     | -Exchange Server 2016 </br>-Exchange Server 2013 </br>-Exchange Server 2010       |
|**Office SharePoint Server**     |-Office SharePoint Server 2016 </br>-Office SharePoint Server 2013 </br>-Office SharePoint Server 2010         |
|**File server che eseguono Windows Server e usano la funzionalità Infrastruttura di classificazione file**     |- Windows Server 2016 </br>- Windows Server 2012 R2 </br>- Windows Server 2012       |
| | |

<!-- i think that half of this note was removed at some point, without this other half. keeping it here in case we ever need it..>
    > You can also use these cmdlets with servers running later versions of Windows Server, with the benefit that these cmdlets can protect all file types. The RMS connector protects Office files only. For how-to instructions, see [RMS Protection with Windows Server File Classification Infrastructure &#40;FCI&#41;](./rms-client/configure-fci.md).
-->

Per altre informazioni, vedere [Deploying the Azure Rights Management Connector](deploy-rms-connector.md).

## <a name="supported-operating-systems-for-azure-rights-management"></a>Sistemi operativi supportati per Azure Rights Management

I sistemi operativi seguenti supportano il servizio Azure Rights Management, che fornisce la protezione dei dati per AIP:

|OS  |Versioni supportate  |
|---------|---------|
|**Computer Windows**     |-Windows 7 (x86, x64) </br>- Windows 8 (x86, x64) </br>- Windows 8.1 (x86, x64) </br>- Windows 10 (x86, x64)       | 
|**macOS**     |   la versione minima di macOS è 10.8 (Mountain Lion)      |
|**Telefoni e Tablet Android**     | Versione minima di Android 6,0        |
|**iPhone e iPad**     | Versione minima di iOS 11,0        |
|**Telefoni e Tablet Windows** | Windows 10 Mobile|
| | |



## <a name="next-steps"></a>Passaggi successivi

Dopo aver esaminato tutti i requisiti di AIP e aver verificato che il sistema sia conforme, continuare con la [preparazione di utenti e gruppi per Azure Information Protection](prepare.md).

