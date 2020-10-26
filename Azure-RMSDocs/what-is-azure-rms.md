---
title: Panoramica della protezione di Azure Rights Management - AIP
description: Informazioni su Azure Rights Management (Azure RMS), la tecnologia di protezione usata da Azure Information Protection.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 07/21/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: aeeebcd7-6646-4405-addf-ee1cc74df5df
ms.subservice: azurerms
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
search.appverid:
- MET150
ms.openlocfilehash: e5a9f0039dc21942ac975aa9bf7a80cc957b40e8
ms.sourcegitcommit: d01580c266de1019de5f895d65c4732f2c98456b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/19/2020
ms.locfileid: "92177848"
---
# <a name="what-is-azure-rights-management"></a>Informazioni su Microsoft Azure Rights Management

>*Si applica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*


Azure Rights Management, spesso abbreviato in Azure RMS, è la tecnologia di protezione usata da [Azure Information Protection](what-is-information-protection.md).

Azure RMS è un servizio di protezione basato sul cloud che usa criteri di crittografia, identità e autorizzazione per proteggere file e messaggi di posta elettronica su più dispositivi, tra cui telefoni, tablet e PC. Le impostazioni di protezione seguono i dati anche quando questi escono dai confini dell'organizzazione, mantenendo il contenuto protetto sia all'interno che all'esterno di essa.

L'immagine seguente mostra come Azure RMS fornisce protezione per Microsoft 365, oltre che per i server e i servizi locali. La protezione è supportata anche dai dispositivi degli utenti finali di uso comune che eseguono Windows, macOS, iOS e Android.

![Funzionamento di Azure RMS](./media/AzRMS_elements.png)

Usare Azure RMS con abbonamenti a Microsoft 365 o sottoscrizioni di Azure Information Protection. Per altre informazioni sui singoli tipi di sottoscrizione e sulle funzionalità supportate, vedere il sito [Prezzi di Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection/).

### <a name="sample-azure-rms-use-case"></a>Esempio di caso d'uso di Azure RMS

Si supponga che un dipendente invii un documento a una società partner tramite posta elettronica o che salvi il documento sull'unità cloud della società.

L'uso della protezione permanente di Azure RMS contribuisce a garantire la sicurezza dei dati aziendali, può essere obbligatoria per soddisfare i requisiti di conformità normativa e di esibizione ai fini giuridici oppure può rappresentare un esempio di procedure consigliate per la gestione delle informazioni.

Azure RMS assicura che le persone e i servizi autorizzati, ad esempio quelli di ricerca e indicizzazione, possano continuare a leggere e analizzare i dati protetti.

Questa possibilità, definita anche "ragionamento sui dati", riveste un ruolo di importanza cruciale nel mantenimento del controllo sui dati dell'organizzazione, un risultato non facilmente raggiungibile con altre soluzioni di protezione delle informazioni che usano la crittografia peer-to-peer. 

## <a name="business-problems-solved-by-azure-rights-management"></a>Problemi aziendali risolti da Azure Rights Management

Usare gli elenchi e le tabelle seguenti per identificare i requisiti o i problemi che può dover affrontare l'organizzazione in merito alla protezione di documenti e messaggi di posta elettronica e per scoprire la soluzione offerta dalla tecnologia Azure Rights Management.

- [Funzionalità di protezione](#protection-features)
- [Funzionalità di collaborazione](#collaboration-features)
- [Funzionalità di supporto della piattaforma](#platform-support-features)
- [Funzionalità per l'infrastruttura](#infrastructure-features)

> [!TIP]
> Gli utenti che hanno già acquisito familiarità con la versione locale di Rights Management, Active Directory Rights Management Services (AD RMS), possono essere interessati alla tabella comparativa disponibile in [Confronto tra Azure Rights Management e AD RMS](compare-on-premise.md).

### <a name="protection-features"></a>Funzionalità di protezione

|Funzionalità  |Descrizione  |
|---------|---------|
|**Protezione di più tipi di file**     | Nelle prime implementazioni di Rights Management era possibile proteggere con la protezione nativa soltanto i file di Office. </br></br>Oggi la protezione generica, offerta inizialmente dall'applicazione di condivisione Rights Management e ora dal client Azure Information Protection, consente di supportare più [tipi di file](./rms-client/client-admin-guide-file-types.md).        |
|**Protezione dei file in qualsiasi situazione** . | Quando un file è [protetto](./rms-client/client-classify-protect.md), la protezione rimane associata al file stesso anche se questo viene salvato o copiato in un'area di archiviazione non controllata dal reparto IT, ad esempio un servizio di archiviazione cloud.|
|     |         |


### <a name="collaboration-features"></a>Funzionalità di collaborazione

|Funzionalità  |Descrizione  |
|---------|---------|
|**Condivisione sicura delle informazioni**     |  I [file protetti](./rms-client/client-classify-protect.md) possono essere condivisi in modo sicuro con altri utenti, come nel caso di un allegato a un messaggio di posta elettronica o un collegamento a un sito di SharePoint. </br></br> Se le informazioni sensibili si trovano all'interno di un messaggio di posta elettronica, è possibile proteggere il messaggio oppure usare l'opzione **Non inoltrare** di Outlook.       |
|**Supporto della collaborazione business-to-business**     |  Poiché Azure Rights Management è un servizio cloud, per poter condividere contenuti protetti con altre organizzazioni non è necessario configurare esplicitamente trust con queste ultime. </br></br>La collaborazione con organizzazioni che dispongono già di una directory di Microsoft 365 o di Azure AD è supportata automaticamente. </br></br>Per le organizzazioni senza Microsoft 365 o una directory di Azure AD, gli utenti possono registrarsi per la sottoscrizione gratuita di [RMS per utenti singoli](rms-for-individuals.md) oppure usare un account Microsoft per le [applicazioni supportate](secure-collaboration-documents.md#supported-scenarios-for-opening-protected-documents).       |
| | |

> [!TIP]
> Allegare file protetti anziché proteggere un intero messaggio di posta elettronica, consente di lasciare in chiaro il testo del messaggio. 
>
> È possibile, ad esempio, includere le istruzioni per il primo utilizzo se il messaggio di posta elettronica viene inviato all'esterno dell'organizzazione. Se si allega un file protetto, chiunque può leggere le istruzioni, ma solo gli utenti autorizzati potranno aprire il documento, anche se il messaggio di posta elettronica o il documento viene inoltrato ad altre persone.

### <a name="platform-support-features"></a>Funzionalità di supporto della piattaforma

Azure RMS supporta un'ampia varietà di piattaforme e applicazioni, tra cui:

|Funzionalità  |Descrizione  |
|---------|---------|
|**Dispositivi di uso comune** </br>non solo computer Windows     | I [dispositivi client](requirements.md#client-devices) comprendono: </br></br>- Computer e telefoni Windows </br>- Computer Mac </br>- Tablet e telefoni iOS </br>- Tablet e telefoni Android        |
|**Servizi locali**     | Oltre a garantire [facile integrazione con Office 365](office-apps-services-support.md), Azure Rights Management può essere usato anche con i servizi locali seguenti quando si distribuisce il [connettore RMS](deploy-rms-connector.md): </br></br>- Exchange Server 2016 </br>- SharePoint Server </br>- Windows Server con la funzionalità Infrastruttura di classificazione file        |
|**Estendibilità dell'applicazione**     |Azure Rights Management offre una stretta integrazione con le applicazioni e i servizi di Microsoft Office ed estende il supporto ad altre applicazioni tramite il [client Azure Information Protection](./rms-client/aip-client.md ). </br></br>Gli [SDK di Azure Information Protection](./develop/developers-guide.md) forniscono agli sviluppatori interni e ai fornitori di software le API necessarie per la creazione di applicazioni personalizzate con supporto per Azure Information Protection. </br></br>Per altre informazioni, vedere [Altre applicazioni che supportano le API di Rights Management](api-support.md).         |
| | |

### <a name="infrastructure-features"></a>Funzionalità per l'infrastruttura

Azure RMS offre le funzionalità seguenti a supporto dei reparti IT e delle organizzazioni che si occupano di infrastrutture:

- **Possibilità di creare criteri semplici e flessibili** . I [modelli di protezione personalizzati](configure-policy-templates.md) forniscono agli amministratori una soluzione rapida e semplice per applicare i criteri e permettono agli utenti di usare il livello di protezione corretto per ciascun documento, nonché di limitare l'accesso al personale dell'organizzazione. Ad esempio:

    - Per condividere a livello aziendale un documento sulle strategie, applicare a tutti i dipendenti interni un criterio di sola lettura. 
    - Nel caso di un documento più riservato, ad esempio un report finanziario, consentire l'accesso ai soli dirigenti dell'azienda.

- **Facilità di attivazione** . Per le nuove sottoscrizioni, l'attivazione è automatica. Per le sottoscrizione esistenti, è possibile [attivare il servizio Rights Management](activate-service.md) con solo pochi clic nel portale di gestione o due comandi di PowerShell.

- **Servizi di controllo e monitoraggio** . È possibile [controllare e monitorare l'utilizzo](log-analyze-usage.md) dei file protetti, anche all'esterno dell'organizzazione. 

    Ad esempio, se un dipendente di Contoso, Ltd lavora a un progetto comune con tre persone della società Fabrikam, Inc, potrebbe inviare ai partner Fabrikam un documento protetto e *di sola lettura* . 

    La funzionalità di controllo di Azure RMS può fornire le seguenti informazioni:

    - Se i partner Fabrikam hanno aperto il documento e quando. 
    - Se altre persone, che non sono state specificate, hanno tentato senza successo di aprire il documento. Questo può accadere se il messaggio di posta elettronica è stato inoltrato oppure salvato in un percorso condiviso.

    Il [sito di rilevamento dei documenti](./rms-client/client-track-revoke.md), inoltre, consente a utenti e amministratori di monitorare e, se necessario, revocare l'accesso ai documenti protetti.

- **Scalabilità a livello di intera organizzazione** . Poiché Azure Rights Management viene eseguito come servizio cloud e offre l'elasticità tipica di Azure in termini di scalabilità verticale e orizzontale, non è necessario effettuare il provisioning di server locali aggiuntivi o distribuire tali server.

- **Capacità di mantenere il controllo dell'IT sui dati** . Le organizzazioni possono usufruire di funzionalità di controllo IT, ad esempio:

    |Funzionalità  |Descrizione  |
    |---------|---------|
    |Gestione della chiave del tenant    |   È possibile gestire la propria chiave del tenant con la soluzione "[Bring Your Own Key](plan-implement-tenant-key.md)" (BYOK), archiviando la chiave del tenant all'interno di moduli di protezione hardware.      |
    |Controllo e registrazione dell'utilizzo    |   Usare le funzionalità di controllo e [registrazione dell'utilizzo](log-analyze-usage.md) per eseguire analisi per ottenere informazioni aziendali dettagliate, monitorare i possibili abusi e, in caso di perdita di informazioni, eseguire analisi per scopi legali.      |
    |Delega dell'accesso     |  È possibile delegare l'accesso mediante la [funzionalità di utente con privilegi avanzati](configure-super-users.md), assicurando che gli addetti del reparto IT possano sempre accedere ai contenuti protetti, anche nel caso di documenti protetti da un utente che non fa più parte dell'organizzazione. </br> Paragonate all'accesso delegato, le soluzioni di crittografia peer-to-peer rischiano la perdita dell'accesso ai dati aziendali.       |
    |Sincronizzazione di Active Directory     |   Sincronizzazione [solo degli attributi della directory richiesti da Azure RMS](/azure/active-directory/hybrid/reference-connect-sync-attributes-synchronized#azure-rms) per supportare un'identità comune per gli account Active Directory locali usando una [soluzione di identità ibrida](/azure/active-directory/hybrid/), come Azure AD Connect.      |
    |Single Sign-On     | Abilitazione dell'accesso Single-Sign On senza replicare le password nel cloud usando AD FS.        |
    |Migrazione da AD RMS |Se si è distribuito Active Directory Rights Management Services (AD RMS), è possibile [eseguire la migrazione al servizio Azure Rights Management](migrate-from-ad-rms-to-azure-rms.md) senza perdere l'accesso ai dati protetti in precedenza da AD RMS. |
    | | |


> [!NOTE]
> Le organizzazioni possono sempre decidere di sospendere l'uso del servizio Azure Rights Management senza perdere l'accesso al contenuto protetto in precedenza da Azure Rights Management. 
> 
> Per altre informazioni, vedere [Rimozione delle autorizzazioni e disattivazione di Azure Rights Management](decommission-deactivate.md). 
> 



## <a name="security-compliance-and-regulatory-requirements"></a>Requisiti di sicurezza, conformità e normativi
Azure Rights Management supporta i requisiti di sicurezza, conformità e normativi seguenti:

- **Uso di crittografia standard del settore e supporto per FIPS 140-2.** Per altre informazioni, vedere [Controlli crittografici usati in Azure RMS: algoritmi e lunghezze delle chiavi](how-does-it-work.md#cryptographic-controls-used-by-azure-rms-algorithms-and-key-lengths).

- **Supporto per moduli di protezione hardware (HSM) nCipher nShield** per archiviare la chiave del tenant in data center di Microsoft Azure. 

    Azure Rights Management usa ambienti di sicurezza separati per i propri data center in America del Nord, nei paesi EMEA (Europa, Medio Oriente e Africa) e in Asia, così da limitare l'uso delle chiavi all'area pertinente.

- **Certificazione per gli standard seguenti:**

    -   ISO/IEC 27001:2013 (include [ISO/IEC 27018](https://azure.microsoft.com/blog/2015/02/16/azure-first-cloud-computing-platform-to-conform-to-isoiec-27018-only-international-set-of-privacy-controls-in-the-cloud/))
    -   Attestazioni SOC 2 SSAE 16/ISAE 3402
    -   HIPAA BAA
    -   EU Model Clause
    -   FedRAMP come parte di Azure Active Directory nella certificazione di Office 365, FedRAMP Agency ATO (Authority to Operate) rilasciato da HHS
    -   PCI DSS Livello 1

Per altre informazioni su queste certificazioni esterne, vedere il [Centro protezione Azure](https://azure.microsoft.com/support/trust-center/compliance/).

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni tecniche sul funzionamento del servizio Azure Rights Management, vedere [Funzionamento di Azure RMS](how-does-it-work.md).
