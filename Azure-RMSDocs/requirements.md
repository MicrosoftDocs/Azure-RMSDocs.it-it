---
title: Requisiti per Azure Information Protection - AIP
description: Identificare i prerequisiti per distribuire Azure Information Protection per l'organizzazione.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 07/16/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: dc78321d-d759-4653-8818-80da74b6cdeb
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 4b70be66db156dc92f57aaf0cc9ba3ce2413dd65
ms.sourcegitcommit: ce47b16c16d93e710c0ff95588e1631ccc0e2829
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/23/2019
ms.locfileid: "68387398"
---
# <a name="requirements-for-azure-information-protection"></a>Requisiti per Azure Information Protection

>*Si applica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

Prima di distribuire Azure Information Protection per l'organizzazione, verificare di soddisfare i prerequisiti seguenti. 

## <a name="subscription-for-azure-information-protection"></a>Sottoscrizione di Azure Information Protection

**Per classificazione, assegnazione di etichette e protezione**: è necessario un [piano di Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection/). 

**Per la sola funzionalità di protezione**: è necessario un [piano di Office 365 che include Azure Information Protection](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf).

Per assicurarsi che la sottoscrizione dell'organizzazione includa le funzionalità di Azure Information Protection da usare, esaminare l'elenco delle funzionalità nella pagina [Prezzi di Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection).

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

Per supportare l'autenticazione e l'autorizzazione utente per Azure Information Protection, l'organizzazione deve avere Azure Active Directory (Azure AD). Inoltre, se si desidera usare gli account utente dalla directory locale (AD DS), è necessario anche configurare l'integrazione delle directory.

L'accesso Single Sign-On (SSO) è supportato per Azure Information Protection, in modo che agli utenti non vengono richieste ripetutamente le credenziali. Se si usa la soluzione di un altro fornitore per la federazione, verificare con il fornitore come configurarla per Azure AD. WS-Trust è un requisito comune per queste soluzioni per il supporto di Single Sign-On. 

Multi-Factor Authentication (MFA) è supportato in Azure Information Protection quando si ha il software client richiesto e l'infrastruttura di supporto MFA è configurata correttamente.

L'accesso condizionale è supportato in anteprima per i documenti protetti da Azure Information Protection. Per altre informazioni, vedere le seguenti domande frequenti: [Azure Information Protection è elencata come un'app cloud disponibile per l'accesso condizionale, come funziona?](faqs.md#i-see-azure-information-protection-is-listed-as-an-available-cloud-app-for-conditional-accesshow-does-this-work)

Per altre informazioni sui requisiti di autenticazione, vedere [Requisiti di Azure Active Directory per Azure Information Protection](requirements-azure-ad.md). 

Per altre informazioni sui requisiti relativi agli account utente e di gruppo per l'autorizzazione, vedere [Preparazione di utenti e gruppi per Azure Information Protection](prepare.md).

## <a name="client-devices"></a>Dispositivi client

Gli utenti devono avere dispositivi client, quali computer o dispositivi mobili, che eseguono un sistema operativo che supporta Azure Information Protection.

I dispositivi seguenti supportano il client di Azure Information Protection Unified Labeling e il client di Azure Information Protection. [Entrambi i client](faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client) consentono agli utenti di classificare ed etichettare documenti e messaggi di posta elettronica:

- Windows 10 (x86, x64)
    
    - Nessun supporto per la grafia nella build Windows 10 RS4 e versioni successive. 

- Windows 8.1 (x86, x64)

- Windows 8 (x86, x64)

- Windows 7 Service Pack 1 (x86, x64)

- Windows Server 2016 

- Windows Server 2012 R2 e Windows Server 2012

- Windows Server 2008 R2 

Oltre a installare il client di in computer fisici, è anche possibile installarlo nelle macchine virtuali. Verificare che il fornitore del software per la soluzione desktop virtuale disponga di configurazioni aggiuntive che potrebbero essere necessarie per eseguire la Azure Information Protection client di etichetta unificata o il client di Azure Information Protection. Per le soluzioni Citrix, ad esempio, potrebbe essere necessario [disabilitare i hook dell'API (Application Programming Interface) Citrix](https://support.citrix.com/article/CTX107825) per Office (Winword. exe, Excel. exe, Outlook. exe, Powerpnt. exe) e il file eseguibile per il Azure Information Protection unificato assegnazione di etichette a client o client Azure Information Protection (MSIP. app. exe, MSIP. Viewer. exe).

Per le versioni server elencate, i client Azure Information Protection sono supportati per Servizi Desktop remoto. Se si eliminano i profili utente quando si usa il Azure Information Protection client con Servizi Desktop remoto, non eliminare la cartella **%AppData%\Microsoft\Protect** .

Quando il Azure Information Protection client protegge i dati tramite il servizio Azure Rights Management, i dati possono essere usati dagli [stessi dispositivi](requirements-client-devices.md) che supportano il servizio Azure Rights Management.

I client di Azure Information Protection hanno prerequisiti aggiuntivi elencati nelle rispettive guide di amministrazione:

- Client per l'etichettatura unificata di Azure Information Protection: [Prerequisiti](./rms-client/clientv2-admin-guide-install.md#additional-prerequisites-for-the-azure-information-protection-unified-labeling-client)

- Client Azure Information Protection: [Prerequisiti](./rms-client/client-admin-guide-install.md#additional-prerequisites-for-the-azure-information-protection-client)


## <a name="applications"></a>Applicazioni

I client Azure Information Protection possono etichettare e proteggere documenti e messaggi di posta elettronica usando le applicazioni di Office **Word**, **Excel**, **PowerPoint**e **Outlook** delle edizioni di Office seguenti:

- App di Office con versione minima 1805, build 9330.2078 da Office 365 Business o Microsoft 365 Business quando all'utente viene assegnata una licenza per Azure Rights Management (nota anche come Azure Information Protection per Office 365)

- Office 365 ProPlus

- Office Professional Plus 2019

- Office Professional Plus 2016

- Office Professional Plus 2013 con Service Pack 1

- Office Professional Plus 2010 con Service Pack 2

Con le altre edizioni di Office non è possibile proteggere i documenti e i messaggi di posta elettronica usando un servizio Rights Management. Per queste edizioni Azure Information Protection è supportato solo per la classificazione. Di conseguenza, le etichette che applicano la protezione non vengono visualizzate dagli utenti sulla barra di Azure Information Protection o dal pulsante **Proteggi** sulla barra multifunzione di Office. 

I client Azure Information Protection non supportano più versioni di Office nello stesso computer. Questi client non supportano anche il cambio di account utente in Office.

Per informazioni sulle edizioni di Office che supportano il servizio di protezione, vedere [Applicazioni che supportano la protezione dati di Azure Rights Management](requirements-applications.md).

## <a name="firewalls-and-network-infrastructure"></a>Firewall e infrastruttura di rete

Se si ha un firewall o simili dispositivi di rete intermedi che devono essere configurati per consentire connessioni specifiche, i requisiti di connettività di rete sono inclusi nell'articolo di Office [Office 365 URLs and IP address ranges](https://support.office.com/en-US/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2) (URL e intervalli di indirizzi IP per Office 365). Vedere la sezione **Microsoft 365 Common and Office Online** (Comuni per Microsoft 365 e Office Online).

Oltre alle informazioni nell'articolo di Office, le istruzioni seguenti sono specifiche per Azure Information Protection:

- Per il client Unified Labeling per scaricare etichette ed etichettare i criteri: Consentire l'URL * **. Protection.Outlook.com** su HTTPS.

- Se si usa un proxy Web che richiede l'autenticazione, configurarlo per l'uso dell'autenticazione integrata di Windows con le credenziali di accesso di Active Directory dell'utente.

- Non terminare la connessione TLS dal client al servizio, ad esempio per il controllo a livello di pacchetti, all'URL **aadrm.com**. In questo modo viene interrotta l'associazione del certificato usata dai client RMS con le autorità di certificazione gestite da Microsoft per la protezione delle comunicazioni con il servizio Azure Rights Management.
    
    - Suggerimento: grazie alla modalità di visualizzazione delle connessioni protette in Chrome, è possibile usare questo browser per verificare rapidamente se la connessione client viene terminata prima di raggiungere il servizio Azure Rights Management. Immettere l'URL seguente nella barra degli indirizzi del browser:`https://admin.na.aadrm.com/admin/admin.svc` 
    
        Non preoccuparsi di ciò che viene visualizzato nella finestra del browser. Fare invece clic sull'icona a forma di lucchetto nella barra degli indirizzi per visualizzare le informazioni sul sito. Le informazioni sul sito consentono di visualizzare l'autorità di certificazione (CA) emittente. Se il certificato non è emesso da una CA Microsoft, è molto probabile che la connessione protetta dal client al servizio venga terminata e richieda interventi di riconfigurazione nel firewall. L'immagine seguente mostra un esempio di CA emittente Microsoft. Se risulta che il certificato è emesso da una CA interna, questa configurazione non è compatibile con Azure Information Protection.
        
        ![Controllo del certificato emesso per le connessioni di Azure Information Protection](./media/certificate-checking.png)

### <a name="on-premises-servers"></a>Server locali

Se si vuole usare il servizio Azure Rights Management di Azure Information Protection con server locali, sono supportati i prodotti seguenti:

- Exchange Server

- SharePoint Server

- File server di Windows Server che supportano la funzionalità Infrastruttura di classificazione file

Per informazioni sui requisiti aggiuntivi per questo scenario, vedere [Server locali che supportano la protezione dati di Azure Rights Management](requirements-servers.md).

### <a name="coexistence-of-ad-rms-with-azure-rms"></a>Coesistenza di AD RMS con Azure RMS

Lo scenario di distribuzione seguente non è supportato, a meno che non si usi AD RMS per la [protezione HYOK](configure-adrms-restrictions.md) con Azure Information Protection (configurazione "Hold Your Own Key"):

- Esecuzione side-by-side di AD RMS e di Azure RMS nella stessa organizzazione tranne che durante la migrazione, come descritto in [Migrazione da AD RMS ad Azure Information Protection](migrate-from-ad-rms-to-azure-rms.md).

È disponibile un percorso di migrazione supportato [da AD RMS ad Azure Information Protection](migrate-from-ad-rms-to-azure-rms.md) e da [Azure Information Protection ad AD RMS](/powershell/module/aipservice/Set-AipServiceMigrationUrl). Se si distribuisce Azure Information Protection e poi si decide di interrompere l'uso del servizio cloud, vedere [Rimozione delle autorizzazioni e disattivazione di Azure Information Protection](decommission-deactivate.md).

