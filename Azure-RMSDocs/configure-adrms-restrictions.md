---
title: Protezione HYOK (Holding your own key) per Azure Information Protection
description: Panoramica della protezione HYOK (AD RMS) con Azure Information Protection, degli scenari supportati e dei relativi prerequisiti, limitazioni e raccomandazioni.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 10/13/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 7667b5b0-c2e9-4fcf-970f-05577ba51126
ms.subservice: hyok
ms.custom: admin
ms.openlocfilehash: c5e401f831cfed9080ae1454c6ee73377591c176
ms.sourcegitcommit: d01580c266de1019de5f895d65c4732f2c98456b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/19/2020
ms.locfileid: "95568191"
---
# <a name="hold-your-own-key-hyok-details-for-azure-information-protection"></a>Details Your Own Key (HYOK) per Azure Information Protection

>*Si applica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*
>
> *Istruzioni per: [Client classico Azure Information Protection per Windows](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

>[!NOTE] 
> Per offrire un'esperienza per i clienti unificata e semplificata, il **client di Azure Information Protection client (versione classica)** e la **Gestione etichette** nel portale di Azure vengono **deprecati** a partire dal **31 marzo 2021**. In questo intervallo di tempo tutti i clienti correnti di Azure Information Protection possono passare alla soluzione di etichettatura unificata usando la piattaforma di etichettatura unificata di Microsoft Information Protection. Altre informazioni nell'[avviso ufficiale sulla deprecazione](https://aka.ms/aipclassicsunset).

Le configurazioni HYOK (Holding your own key) consentono ai clienti di AIP con il client classico di proteggere il contenuto altamente sensibile mantenendo al tempo stesso il controllo completo della chiave. HYOK usa una chiave aggiuntiva, inclusa nel cliente, archiviata in locale per contenuti estremamente sensibili, insieme alla protezione predefinita basata sul cloud usata per altro contenuto. 

Per altre informazioni sulle chiavi radice del tenant predefinite basate sul cloud, vedere [pianificazione e implementazione della chiave del tenant di Azure Information Protection](plan-implement-tenant-key.md).

## <a name="cloud-based-protection-vs-hyok"></a>Protezione basata sul cloud rispetto a HYOK

In genere, la protezione di documenti e messaggi di posta elettronica riservati usando Azure Information Protection usa una chiave basata sul cloud [generata da Microsoft](plan-implement-tenant-key.md#tenant-root-keys-generated-by-microsoft) o [dal cliente, usando una configurazione BYOK](byok-price-restrictions.md). 

Le chiavi basate sul cloud sono gestite in Azure Key Vault, che offre ai clienti i vantaggi seguenti:

- **Nessun requisito di infrastruttura server.** Le soluzioni cloud sono più veloci e convenienti da distribuire e gestire rispetto alle soluzioni locali.

- **L'autenticazione basata sul cloud** consente una condivisione più semplice con partner e utenti di altre organizzazioni. 

- **Stretta integrazione con altri servizi di Azure e Microsoft 365**, ad esempio ricerca, visualizzatori Web, viste trasformate tramite pivot, anti-malware, eDiscovery e approfondimenti.

- **Rilevamento dei documenti**, **revoca** e **notifiche tramite posta elettronica** per i documenti riservati che sono stati condivisi.

Tuttavia, alcune organizzazioni possono avere requisiti normativi che richiedono la crittografia di contenuti specifici usando una chiave isolata dal cloud. Questo isolamento significa che il contenuto crittografato può essere letto solo da applicazioni locali e servizi locali.

Con le configurazioni di HYOK, i tenant dei clienti hanno una [chiave basata sul cloud](plan-implement-tenant-key.md) da usare con contenuto che può essere archiviato nel cloud e una chiave locale per il contenuto che deve essere protetto solo in locale.

## <a name="hyok-guidance-and-best-practices"></a>Materiale sussidiario e procedure consigliate per HYOK

Quando si configura HYOK, tenere presenti le indicazioni seguenti:

- [Contenuto adatto per HYOK](#content-suitable-for-hyok)
- [Definire gli utenti che possono visualizzare le etichette configurate con HYOK](#define-the-users-who-can-see-hyok-configured-labels)
- [Supporto per HYOK e posta elettronica](#hyok-and-email-support)

> [!IMPORTANT]
> Una configurazione HYOK per Azure Information Protection non sostituisce una distribuzione completamente AD RMS e Azure Information Protection oppure un'alternativa alla [migrazione ad RMS a Azure Information Protection](migrate-from-ad-rms-to-azure-rms.md). 
>
> HYOK è supportato solo applicando etichette, non offre parità di funzionalità con AD RMS e non supporta tutte le configurazioni di distribuzione di AD RMS.

### <a name="content-suitable-for-hyok"></a>Contenuto adatto per HYOK

La protezione HYOK non offre i vantaggi della protezione basata sul cloud e spesso comporta il costo dell'opacità dei dati, perché è possibile accedere al contenuto solo da applicazioni e servizi locali. Anche per le organizzazioni che usano la protezione HYOK, è in genere adatto solo per un numero ridotto di documenti. 

Si consiglia di usare HYOK solo per il contenuto che soddisfa i criteri seguenti:

- Contenuto con la classificazione più alta all'interno dell'organizzazione ("Top Secret"), in cui l'accesso è limitato a poche persone
- Contenuto non condiviso all'esterno dell'organizzazione
- Contenuto che viene utilizzato solo nella rete interna.

### <a name="define-the-users-who-can-see-hyok-configured-labels"></a>Definire gli utenti che possono visualizzare le etichette configurate con HYOK

Per assicurarsi che solo gli utenti che devono applicare la protezione HYOK vedano le etichette configurate da HYOK, configurare i criteri per gli utenti con [criteri con ambito](configure-policy-scope.md).

### <a name="hyok-and-email-support"></a>Supporto per HYOK e posta elettronica

Microsoft 365 Services e altri Servizi online non possono decrittografare il contenuto protetto da HYOK.

Per i messaggi di posta elettronica, questa perdita di funzionalità include scanner di malware, Encrypt-Only Protection, soluzioni di prevenzione della perdita dei dati, regole di routing della posta elettronica, journaling, eDiscovery, soluzioni di archiviazione ed Exchange ActiveSync.

Gli utenti potrebbero non comprendere il motivo per cui alcuni dispositivi non sono in grado di aprire messaggi di posta elettronica protetti da HYOK, ottenendo chiamate aggiuntive al help desk. Tenere presente queste limitazioni gravi quando si configura la protezione HYOK con i messaggi di posta elettronica.

## <a name="supported-applications-for-hyok"></a>Applicazioni supportate per HYOK

Usare etichette Azure Information Protection per applicare HYOK a documenti e messaggi di posta elettronica specifici. HYOK è supportato per le versioni di Office 2013 e successive.

HYOK è un'opzione di configurazione dell'amministratore per le etichette e i flussi di lavoro rimangono invariati, indipendentemente dal fatto che il contenuto usi come chiave basata sul cloud o HYOK.

Le tabelle seguenti elencano gli scenari supportati per la protezione e l'utilizzo di contenuto con le etichette configurate in HYOK:

- [Supporto delle applicazioni Windows per HYOK](#windows-application-support-for-hyok)
- [supporto delle applicazioni macOS per HYOK](#macos-application-support-for-hyok)
- [supporto delle applicazioni iOS per HYOK](#ios-application-support-for-hyok)
- [Supporto delle applicazioni Android per HYOK](#android-application-support-for-hyok)

> [!NOTE]
> Le applicazioni Office Web e Universal non sono supportate per HYOK.

### <a name="windows-application-support-for-hyok"></a>Supporto delle applicazioni Windows per HYOK

|Applicazione  |Protezione  |Consumo  |
|---------|---------|---------|
|Azure Information Protection client con Microsoft 365 app, Office 2019, Office 2016 e Office 2013:</br>Word, Excel, PowerPoint, Outlook     | ![sì](media/yes-icon.png)        | ![sì](media/yes-icon.png)        |
|Client di Azure Information Protection     | ![sì](media/yes-icon.png)        | ![sì](media/yes-icon.png) |
|Visualizzatore di Azure Information Protection     |   Non applicabile      |  ![sì](media/yes-icon.png)       |
|Client di Azure Information Protection con cmdlet per le etichette di PowerShell     | ![sì](media/yes-icon.png)        | ![sì](media/yes-icon.png)        |
|Scanner di Azure Information Protection     |![sì](media/yes-icon.png)       |   ![sì](media/yes-icon.png)      |
| | | |

### <a name="macos-application-support-for-hyok"></a>supporto delle applicazioni macOS per HYOK

|Applicazione|Protezione|Consumo|
|----------------------|----------|-----------|
|Office per Mac: </br>Word, Excel, PowerPoint, Outlook|![No](media/no-icon.png)|![sì](media/yes-icon.png)|
| | | |

### <a name="ios-application-support-for-hyok"></a>supporto delle applicazioni iOS per HYOK

|Applicazione|Protezione|Consumo|
|----------------------|----------|-----------|
|Office Mobile: </br>Word, Excel, PowerPoint|![No](media/no-icon.png)| ![sì](media/yes-icon.png)|
|Office Mobile: </br>Solo Outlook|![No](media/no-icon.png)|![No](media/no-icon.png)|
|Visualizzatore di Azure Information Protection|Non applicabile|![sì](media/yes-icon.png)|

### <a name="android-application-support-for-hyok"></a>Supporto delle applicazioni Android per HYOK

|Applicazione|Protezione|Consumo|
|----------------------|----------|-----------|
|Office Mobile: </br>Word, Excel, PowerPoint|![No](media/no-icon.png)| ![sì](media/yes-icon.png)|
|Office Mobile: </br>Solo Outlook|![No](media/no-icon.png)|![No](media/no-icon.png)|
|Visualizzatore di Azure Information Protection|Non applicabile| ![sì](media/yes-icon.png)|


## <a name="implementing-hyok"></a>Implementazione di HYOK

Azure Information Protection supporta HYOK quando si dispone di un Active Directory Rights Management Services (AD RMS) conforme a tutti i [requisiti elencati di seguito](#requirements-for-ad-rms-to-support-hyok).

I criteri per i diritti di utilizzo e la chiave privata dell'organizzazione che proteggono questi criteri vengono gestiti e conservati in locale, mentre i criteri di Azure Information Protection per l'assegnazione di etichette e la classificazione rimangono gestiti e archiviati in Azure.

Per implementare la protezione HYOK:

1. [Verificare che il sistema sia conforme ai requisiti di AD RMS](#requirements-for-ad-rms-to-support-hyok)
1. [Individuare le informazioni che si desidera proteggere](#locating-the-information-to-specify-ad-rms-protection-with-an-azure-information-protection-label)

Quando si è pronti, continuare con [la configurazione di un'etichetta per la protezione Rights Management](configure-policy-protection.md).

### <a name="requirements-for-ad-rms-to-support-hyok"></a>Requisiti per AD RMS per il supporto di HYOK

Una distribuzione AD RMS deve soddisfare i requisiti seguenti per fornire la protezione HYOK per le etichette Azure Information Protection:

|Requisito  |Descrizione  |
|---------|---------|
|**Configurazione di AD RMS**     |Il sistema di AD RMS deve essere configurato in modi specifici per supportare HYOK. Per ulteriori informazioni, vedere di [seguito](#ad-rms-configuration-requirements).          |
|**Sincronizzazione delle directory**     |La sincronizzazione della directory deve essere configurata tra la Active Directory locale e la Azure Active Directory. </br></br>Gli utenti che utilizzeranno le etichette di protezione HYOK devono essere configurati per l'accesso Single Sign-on.         |
|**Configurazione per i trust definiti in modo esplicito**     |Se si condivide il contenuto protetto con HYOK con altri utenti esterni all'organizzazione, è necessario configurare AD RMS per i trust definiti in modo esplicito in una relazione punto a punto diretta con altre organizzazioni. </br></br>A tale scopo, utilizzare domini utente trusted (TUD) o trust federativi creati utilizzando Active Directory Federation Services (AD FS).         |
|**Microsoft Office versione supportata**     | Gli utenti che proteggono o utilizzano contenuti protetti da HYOK devono disporre di: </br></br>-Una versione di Office che supporta Information Rights Management (IRM) </br>-Microsoft Office Professional Plus versione 2013 o successiva con Service Pack 1, in esecuzione in Windows 7 Service Pack 1 o versioni successive. </br>-Per l'edizione basata su Office 2016 Microsoft Installer (MSI), è necessario disporre dell' [aggiornamento 4018295 per Microsoft Office 2016 rilasciato il 6 marzo 2018](https://support.microsoft.com/help/4018295/march-6-2018-update-for-office-2016-kb4018295). </br></br>**Nota:** Office 2010 e Office 2007 non sono supportati.        |

> [!IMPORTANT]
> Per soddisfare la garanzia elevata offerta dalla protezione HYOK, è consigliabile:
> - Individuare i server AD RMS al di fuori della rete perimetrale e verificare che vengano usati solo da dispositivi gestiti.
>
> - Configurare il cluster di AD RMS con un modulo di protezione hardware (HSM). Ciò consente di garantire che la chiave privata del certificato concessore di licenze server (SLC) non possa essere esposta o rubata se la distribuzione di AD RMS deve essere violata o compromessa.

> [!TIP]
> Per informazioni sulla distribuzione e istruzioni per AD RMS, vedere [Active Directory Rights Management Services](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831364(v=ws.11)) nella libreria di Windows Server. 

#### <a name="ad-rms-configuration-requirements"></a>Requisiti di configurazione di AD RMS

Per supportare HYOK, verificare che il sistema AD RMS disponga delle configurazioni seguenti:

|Requisito  |Descrizione  |
|---------|---------|
|**Versione di Windows**     |Come minimo, una delle seguenti versioni di Windows: </br></br>**Ambienti di produzione:** Windows Server 2012 R2</br>**Ambienti di test/valutazione**: Windows Server 2008 R2 con Service Pack 1        |
|**Topologia**     |HYOK richiede una delle seguenti topologie: </br>-Una singola foresta con un singolo cluster di AD RMS </br>-Più foreste, con AD RMS cluster in ognuno di essi. </br></br>**Gestione delle licenze per più foreste**</br> Se si dispone di più insiemi di strutture, ogni cluster AD RMS condivide un URL di licenza che punta allo stesso cluster AD RMS. </br>In questo AD RMS cluster importare tutti i certificati del dominio utente trusted (dominio utente trusted) da tutti gli altri cluster AD RMS. </br>Per altre informazioni su questa topologia, vedere [Dominio utente trusted](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd983944(v=ws.10)). </br></br>**Etichette dei criteri globali per più foreste**</br>Quando si hanno più cluster AD RMS in foreste diverse, eliminare le etichette presenti nei criteri globali che applicano la protezione HYOK (AD RMS) e configurare [criteri con ambito](configure-policy-scope.md) per ogni cluster. <br>Assegnare gli utenti per ogni cluster ai criteri con ambito, assicurandosi di non usare i gruppi che comporteranno l'assegnazione di un utente a più criteri con ambito.</br>In seguito a questa assegnazione ogni utente deve avere etichette per un solo cluster AD RMS.          |
|**Modalità crittografia**     | Il AD RMS deve essere configurato con la [modalità crittografia 2](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/hh867439(v=ws.10)). </br>Verificare la modalità controllando la AD RMS proprietà cluster, scheda **generale** .        |
|**Configurazione URL certificazione**     | Ogni server di AD RMS deve essere configurato per l'URL di certificazione. </br>Per ulteriori informazioni, vedere di [seguito](#configuring-ad-rms-servers-to-locate-the-certification-url).        |
|**Punti di connessione del servizio**     | Un punto di connessione del servizio (SCP) non viene usato quando si usa la protezione AD RMS con Azure Information Protection. </br></br>**Se si dispone di un SCP registrato per la distribuzione di ad RMS**, rimuoverlo per assicurarsi che l' [individuazione dei servizi](./rms-client/client-deployment-notes.md#rms-service-discovery) abbia esito positivo per la protezione Rights Management di Azure. </br></br>**Se si sta installando un nuovo cluster ad RMS per HYOK**, non registrare SCP quando si configura il primo nodo. Per ogni nodo aggiuntivo, assicurarsi che il server sia configurato per l'URL di certificazione prima di aggiungere il ruolo AD RMS e aggiungere il cluster esistente.         |
|**SSL/TLS**     |Negli ambienti di produzione, i server di AD RMS devono essere configurati per l'uso di SSL/TLS con un certificato x. 509 valido considerato attendibile dai client che si connettono. </br></br>Questa operazione non è necessaria a scopo di test o valutazione.         |
|**Modelli di diritti**     |È necessario disporre di modelli di diritti configurati per il AD RMS.         |
|**IRM di Exchange**    |Non è possibile configurare il AD RMS per Exchange IRM.         |
|**Dispositivi mobili/computer Mac**     | È necessario che l' [estensione Active Directory Rights Management Services dispositivo mobile](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn673574(v=ws.11)) sia installata e configurata.        |


#### <a name="configuring-ad-rms-servers-to-locate-the-certification-url"></a>Configurazione dei server AD RMS per individuare l'URL di certificazione

1. In ogni server AD RMS nel cluster, creare la voce del Registro di sistema seguente:

    ```sh
    Computer\HKEY_LOCAL_MACHINE\Software\Microsoft\DRMS\GICURL = "<string>"`
    ```

    Per \<string value> , specificare una delle stringhe seguenti:

    |Ambiente  |Valore stringa  |
    |---------|---------|
    |**Produzione** </br>(AD RMS cluster con SSL/TLS)     | `https://<cluster_name>/_wmcs/certification/certification.asmx`        |
    |**Test/valutazione** </br>(nessun SSL/TLS)     |`http://<cluster_name>/_wmcs/certification/certification.asmx`         |

2. Riavviare IIS.

### <a name="locating-the-information-to-specify-ad-rms-protection-with-an-azure-information-protection-label"></a>Individuazione delle informazioni per specificare la protezione di AD RMS con un'etichetta di Azure Information Protection

Per configurare HYOK-Protection labels è necessario specificare l'URL di gestione licenze del cluster AD RMS. 

Inoltre, è necessario specificare un modello configurato con le autorizzazioni che si desidera concedere agli utenti o consentire agli utenti di definire autorizzazioni e utenti. 

Eseguire le operazioni seguenti per individuare il GUID del modello e i valori dell'URL di gestione licenze dalla console di Active Directory Rights Management Services:

#### <a name="locate-a-template-guid"></a>Individuare il GUID di un modello

1. espandere il cluster e fare clic su **Modelli di criteri per i diritti di utilizzo**. 

1. Dalle informazioni sui **modelli di criteri di diritti distribuiti** , copiare il GUID dal modello che si vuole usare. 

Ad esempio: **82bf3474-6efe-4fa1-8827-d1bd93339119** 

#### <a name="locate-the-licensing-url"></a>Individuare l'URL di gestione licenze

1. Fare clic sul nome del cluster.
 
1. In **Dettagli cluster** copiare il valore **Gestione licenze** ad eccezione della stringa **/_wmcs/licensing**. 

Per esempio: **https://rmscluster.contoso.com** 
    
> [!NOTE]
> Se si dispone di valori di licenze Extranet e Intranet diversi, specificare il valore Extranet solo se si condivide il contenuto protetto con i partner. I partner che condividono contenuti protetti devono essere definiti con trust Point-to-Point espliciti. 
> 
> Se non si condivide contenuto protetto, utilizzare il valore Intranet e verificare che tutti i computer client che utilizzano AD RMS protezione con Azure Information Protection connettersi tramite una connessione Intranet. Ad esempio, i computer remoti devono usare una connessione VPN.
> 

## <a name="next-steps"></a>Passaggi successivi

Al termine della configurazione del sistema per il supporto di HYOK, continuare con la configurazione delle etichette per la protezione HYOK. Per ulteriori informazioni, vedere [come configurare un'etichetta per la protezione Rights Management](configure-policy-protection.md).