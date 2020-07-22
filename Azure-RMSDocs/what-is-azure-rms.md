---
title: Panoramica di Azure Rights Management Protection-AIP
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
ms.openlocfilehash: 6c479bbb5f63bbbdc98165bc0c99f43a4e9503b4
ms.sourcegitcommit: 16d2c7477b96c5e8f6e4328a61fe1dc3d12c878d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/22/2020
ms.locfileid: "86927404"
---
# <a name="what-is-azure-rights-management"></a>Informazioni su Microsoft Azure Rights Management

>*Si applica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*


Azure Rights Management, spesso abbreviato in Azure RMS, è la tecnologia di protezione usata da [Azure Information Protection](what-is-information-protection.md).

Azure RMS è un servizio di protezione basato sul cloud che usa criteri di crittografia, identità e autorizzazione per proteggere file e messaggi di posta elettronica su più dispositivi, tra cui telefoni, tablet e PC. Le impostazioni di protezione rimangono con i dati, anche quando lasciano i limiti dell'organizzazione, mantenendo i contenuti protetti sia all'interno che all'esterno dell'organizzazione.

Nell'immagine seguente viene illustrato come Azure RMS fornisce la protezione per Office 365, oltre che per server e servizi locali. La protezione è supportata anche dai più diffusi dispositivi per gli utenti finali che eseguono Windows, macOS, iOS e Android.

![Funzionamento di Azure RMS](./media/AzRMS_elements.png)

Usare Azure RMS con le sottoscrizioni o le sottoscrizioni di Office 365 per Azure Information Protection. Per ulteriori informazioni sui singoli tipi di sottoscrizione e sulle funzionalità supportate, vedere il sito dei [prezzi Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection/) .

### <a name="sample-azure-rms-use-case"></a>Esempio di caso d'uso Azure RMS

I dipendenti possono inviare tramite posta elettronica un documento a una società partner oppure salvare un documento nell'unità cloud.

L'uso della protezione permanente di Azure RMS consente di proteggere i dati aziendali e può anche essere legalmente necessario per la conformità, i requisiti di individuazione legale o le procedure consigliate per la gestione delle informazioni.

Azure RMS garantisce che gli utenti e i servizi autorizzati, ad esempio la ricerca e l'indicizzazione, possano continuare a leggere ed esaminare i dati protetti.

Garantire l'accesso continuo per utenti e servizi autorizzati, anche noto come "ragionamento sui dati", è un elemento fondamentale per mantenere il controllo dei dati dell'organizzazione. Questa funzionalità potrebbe non essere facilmente realizzata con altre soluzioni di protezione delle informazioni che usano la crittografia peer-to-peer. 

## <a name="business-problems-solved-by-azure-rights-management"></a>Problemi aziendali risolti da Azure Rights Management

Usare le tabelle e gli elenchi seguenti per identificare i requisiti aziendali o i problemi che l'organizzazione potrebbe avere per la protezione di documenti e messaggi di posta elettronica e il modo in cui la tecnologia Rights Management di Azure può soddisfare le proprie esigenze.

- [Funzionalità di protezione](#protection-features)
- [Funzionalità di collaborazione](#collaboration-features)
- [Funzionalità di supporto della piattaforma](#platform-support-features)
- [Funzionalità dell'infrastruttura](#infrastructure-features)

> [!TIP]
> Se si ha familiarità con la versione locale di Rights Management, Active Directory Rights Management Services (AD RMS), si potrebbe essere interessati alla tabella di confronto dal [confronto tra Rights Management e ad RMS di Azure](compare-on-premise.md).

### <a name="protection-features"></a>Funzionalità di protezione

|Funzionalità  |Descrizione  |
|---------|---------|
|**Protezione di più tipi di file**     | Nelle prime implementazioni di Rights Management, è possibile proteggere solo i file di Office, usando la protezione Rights Management nativa. </br></br>A questo punto, la protezione generica offerta per la prima volta dall'applicazione di condivisione Rights Management e ora offerta dal client Azure Information Protection significa che sono supportati più [tipi di file](./rms-client/client-admin-guide-file-types.md) .        |
|**Proteggi i file ovunque ti trovi**. | Quando un file è [protetto](./rms-client/client-classify-protect.md), la protezione rimane associata al file, anche se viene salvato o copiato nello spazio di archiviazione che non è sotto il controllo, ad esempio un servizio di archiviazione cloud.|
|     |         |


### <a name="collaboration-features"></a>Funzionalità di collaborazione

|Funzionalità  |Descrizione  |
|---------|---------|
|**Condivisione sicura delle informazioni**     |  [I file protetti](./rms-client/client-classify-protect.md) possono essere condivisi in modo sicuro con altri utenti, ad esempio un allegato a un messaggio di posta elettronica o un collegamento a un sito di SharePoint. </br></br> Se le informazioni riservate sono contenute in un messaggio di posta elettronica, proteggere il messaggio di posta elettronica oppure usare l'opzione **non inviare in** Outlook.       |
|**Supporto della collaborazione business-to-business**     |  Poiché Rights Management di Azure è un servizio cloud, non è necessario configurare in modo esplicito i trust con altre organizzazioni prima di poter condividere il contenuto protetto con loro. </br></br>La collaborazione con altre organizzazioni che dispongono già di un Office 365 o una directory Azure AD è supportata automaticamente. </br></br>Per le organizzazioni senza Office 365 o una directory Azure AD, gli utenti possono iscriversi per la sottoscrizione gratuita di [RMS per utenti singoli](rms-for-individuals.md) oppure usare una account Microsoft per [le applicazioni supportate](secure-collaboration-documents.md#supported-scenarios-for-opening-protected-documents).       |
| | |

> [!TIP]
> Se si alleghino file protetti, anziché proteggere un intero messaggio di posta elettronica, è possibile evitare la crittografia del testo della posta elettronica. 
>
> È possibile, ad esempio, includere le istruzioni per il primo utilizzo se il messaggio di posta elettronica viene inviato all'esterno dell'organizzazione. Se si aggiunge un file protetto, le istruzioni di base possono essere lette da chiunque, ma solo gli utenti autorizzati saranno in grado di aprire il documento, anche se il messaggio di posta elettronica o il documento viene inviato ad altri utenti.

### <a name="platform-support-features"></a>Funzionalità di supporto della piattaforma

Azure RMS supporta un'ampia gamma di piattaforme e applicazioni, tra cui:

|Funzionalità  |Descrizione  |
|---------|---------|
|**Dispositivi usati di frequente** </br>non solo computer Windows     | I [dispositivi supportati](./requirements-client-devices.md) includono: </br></br>- Computer e telefoni Windows </br>- Computer Mac </br>- Tablet e telefoni iOS </br>- Tablet e telefoni Android        |
|**Servizi locali**     | Oltre a funzionare [senza interruzioni con Office 365](office-apps-services-support.md), usare Azure Rights Management con i servizi locali seguenti quando si distribuisce il [connettore RMS](deploy-rms-connector.md): </br></br>- Exchange Server 2016 </br>- SharePoint Server </br>- Windows Server con la funzionalità Infrastruttura di classificazione file        |
|**Estendibilità delle applicazioni**     |Azure Rights Management offre una stretta integrazione con Microsoft Office le applicazioni e i servizi ed estende il supporto per altre applicazioni tramite il [client di Azure Information Protection](./rms-client/aip-client.md ). </br></br>Gli [sdk Azure Information Protection](./develop/developers-guide.md) offrono agli sviluppatori interni e ai fornitori di software le API per scrivere applicazioni personalizzate che supportano Azure Information Protection. </br></br>Per altre informazioni, vedere [Altre applicazioni che supportano le API di Rights Management](api-support.md).         |
| | |

### <a name="infrastructure-features"></a>Funzionalità dell'infrastruttura

Azure RMS offre le funzionalità seguenti per supportare i reparti IT e le organizzazioni di infrastruttura:

- **Creare criteri semplici e flessibili**. I [modelli di protezione personalizzati](configure-policy-templates.md) offrono agli amministratori una soluzione rapida e semplice per applicare i criteri e consentire agli utenti di applicare il livello di protezione corretto per ogni documento e di limitare l'accesso alle persone all'interno dell'organizzazione. Ad esempio:

    - Per condividere un documento di strategia a livello aziendale con tutti i dipendenti, applicare un criterio di sola lettura a tutti i dipendenti interni. 
    - Per un documento più sensibile, ad esempio un report finanziario, limitare l'accesso ai soli dirigenti.

- **Facile attivazione**. Per le nuove sottoscrizioni, l'attivazione è automatica. Per le sottoscrizioni esistenti, [l'attivazione del servizio Rights Management](activate-service.md) richiede solo un paio di clic nel portale di gestione o due comandi di PowerShell.

- **Servizi di controllo e monitoraggio**. [Controllare e monitorare l'utilizzo](log-analyze-usage.md) dei file protetti, anche dopo che questi file lasciano i limiti dell'organizzazione. 

    Se, ad esempio, un dipendente di Contoso, Ltd lavora su un progetto comune con tre persone di Fabrikam, Inc, potrebbe inviare ai partner Fabrikam un documento protetto e limitato alla sola *lettura*. 

    La funzionalità di controllo di Azure RMS può fornire le seguenti informazioni:

    - Indica se i partner Fabrikam hanno aperto il documento e quando. 
    - Indica se altri utenti, che non sono stati specificati, hanno tentato di aprire il documento. Questo problema può verificarsi se il messaggio di posta elettronica è stato inviato oppure è stato salvato in un percorso condiviso.

    Il [sito di rilevamento dei documenti](./rms-client/client-track-revoke.md), inoltre, consente a utenti e amministratori di monitorare e, se necessario, revocare l'accesso ai documenti protetti.

- **Possibilità di ridimensionare l'intera organizzazione**. Poiché Azure Rights Management viene eseguito come servizio cloud con l'elasticità di Azure per la scalabilità verticale e orizzontale, non è necessario eseguire il provisioning di server locali aggiuntivi o distribuirli.

- **Mantenere il controllo dei dati**. Le organizzazioni possono trarre vantaggio dalle funzionalità di controllo IT, ad esempio:

    |Funzionalità  |Descrizione  |
    |---------|---------|
    |Gestione delle chiavi del tenant    |   Gestire la propria chiave del tenant usando la soluzione "[Bring your own key](plan-implement-tenant-key.md)" (BYOK), archiviando la chiave del tenant in moduli di protezione hardware (HSM).      |
    |Controllo e registrazione dell'utilizzo    |   Usare le funzionalità di [registrazione](log-analyze-usage.md) di controllo e utilizzo per analizzare le informazioni aziendali, monitorare gli abusi ed eseguire analisi forensi per la perdita di informazioni.      |
    |Delega dell'accesso     |  Delegare l'accesso con la [funzionalità per utenti con privilegi avanzati](configure-super-users.md), garantendo la possibilità di accedere sempre ai contenuti protetti, anche se un documento è stato protetto da un dipendente che lascia l'organizzazione. </br> Paragonate all'accesso delegato, le soluzioni di crittografia peer-to-peer rischiano la perdita dell'accesso ai dati aziendali.       |
    |Sincronizzazione di Active Directory     |   Sincronizzare [solo gli attributi di directory che Azure RMS necessario](/azure/active-directory/hybrid/reference-connect-sync-attributes-synchronized#azure-rms) supportare un'identità comune per gli account di Active Directory locali, usando [una soluzione di identità ibrida](/azure/active-directory/hybrid/), ad esempio Azure ad Connect.      |
    |Single Sign-on     | Abilitare l'accesso Single Sign-on senza replicare le password nel cloud usando AD FS.        |
    |Migrazione da AD RMS |Se è stato distribuito Active Directory Rights Management Services (AD RMS), [eseguire la migrazione al servizio Azure Rights Management](migrate-from-ad-rms-to-azure-rms.md) senza perdere l'accesso ai dati precedentemente protetti da ad RMS. |
    | | |


> [!NOTE]
> Le organizzazioni hanno sempre la possibilità di smettere di usare il servizio Azure Rights Management senza perdere l'accesso ai contenuti precedentemente protetti da Azure Rights Management. 
> 
> Per altre informazioni, vedere [rimozione delle autorizzazioni e disattivazione di Azure Rights Management](decommission-deactivate.md). 
> 



## <a name="security-compliance-and-regulatory-requirements"></a>Requisiti di sicurezza, conformità e normativi
Azure Rights Management supporta i requisiti di sicurezza, conformità e normativi seguenti:

- **Uso della crittografia standard del settore e supporta FIPS 140-2.** Per altre informazioni, vedere [Controlli crittografici usati in Azure RMS: algoritmi e lunghezze delle chiavi](how-does-it-work.md#cryptographic-controls-used-by-azure-rms-algorithms-and-key-lengths).

- **Supporto per il modulo di protezione hardware nCipher nShield** per archiviare la chiave del tenant in Microsoft Azure Data Center. 

    Azure Rights Management usa ambienti di sicurezza separati per i propri data center in America del Nord, nei paesi EMEA (Europa, Medio Oriente e Africa) e in Asia, così da limitare l'uso delle chiavi all'area pertinente.

- **Certificazione per gli standard seguenti:**

    -   ISO/IEC 27001:2013 (include [ISO/IEC 27018](https://azure.microsoft.com/blog/2015/02/16/azure-first-cloud-computing-platform-to-conform-to-isoiec-27018-only-international-set-of-privacy-controls-in-the-cloud/))
    -   Attestazioni SOC 2 SSAE 16/ISAE 3402
    -   HIPAA BAA
    -   EU Model Clause
    -   FedRAMP come parte di Azure Active Directory nella certificazione di Office 365, FedRAMP Agency ATO (Authority to Operate) rilasciato da HHS
    -   PCI DSS Livello 1

Per ulteriori informazioni su queste certificazioni esterne, vedere la [Centro protezione di Azure](https://azure.microsoft.com/support/trust-center/compliance/).

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni tecniche sul funzionamento del servizio Azure Rights Management, vedere [Funzionamento di Azure RMS](how-does-it-work.md).
