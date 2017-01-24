---
title: Restrizioni HYOK | Azure Information Protection
description: "Identificare le restrizioni, i prerequisiti e le raccomandazioni se si seleziona la protezione di AD RMS con Azure Information Protection. Questa soluzione è a volte definita &quot;hold your own key&quot; (HYOK)."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 01/13/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 7667b5b0-c2e9-4fcf-970f-05577ba51126
translationtype: Human Translation
ms.sourcegitcommit: 22af60687ad030e686ba843ced6d450487353a0e
ms.openlocfilehash: 66c19b296ce170d0f7f5317c87bee532edd9bb78


---

# <a name="hold-your-own-key-hyok-requirements-and-restrictions-for-ad-rms-protection"></a>Requisiti e restrizioni HYOK per la protezione di AD RMS

>*Si applica a: Azure Information Protection*

Per proteggere documenti e messaggi di posta elettronica contenenti informazioni riservate, è in genere possibile applicare la protezione di Azure Rights Management per sfruttare i vantaggi seguenti:

- Infrastruttura server non necessaria. In questo modo, la soluzione è più veloce e conveniente da distribuire e gestire rispetto a una soluzione locale.

- Condivisione più agevole con partner e utenti di altre organizzazioni tramite l'autenticazione basata su cloud.

- Stretta integrazione con i servizi di Office 365, ad esempio ricerca, visualizzatori Web, viste trasformate tramite Pivot, anti-malware, eDiscovery e Delve.

- Monitoraggio di documenti, revoca e notifiche tramite posta elettronica per i documenti condivisi contenenti informazioni riservate.

Azure RMS consente di proteggere i documenti e i messaggi di posta elettronica dell'organizzazione tramite una chiave privata gestita da Microsoft (impostazione predefinita) o dall'utente (scenario BYOK o "bring your own key"). Le informazioni protette con Azure RMS non vengono mai inviate al cloud. I documenti e i messaggi di posta elettronica protetti non vengono archiviati in Azure a meno che non venga richiesto esplicitamente o si usi un altro servizio cloud che li archivia in Azure. Per altre informazioni sulle opzioni della chiave del tenant, vedere [Pianificazione e implementazione della chiave del tenant di Azure Information Protection](../plan-design/plan-implement-tenant-key.md). 

Tuttavia, può essere necessario proteggere specifici documenti e messaggi di posta elettronica con una chiave ospitata in locale. Ad esempio, questa può essere necessaria per motivi normativi e di conformità. 

Questa configurazione viene a volte definita HYOK, ossia "hold your own key" ed è supportata da Azure Information Protection quando si dispone di una distribuzione di Active Directory Rights Management Services (AD RMS) attiva con i requisiti descritti nella sezione seguente. Questa funzionalità è ancora in stato di anteprima.

In questo scenario HYOK, i criteri dei diritti e la chiave privata dell'organizzazione che protegge tali criteri vengono gestiti e conservati in locale, mentre i criteri di Azure Information Protection per l'applicazione di etichette e la classificazione vengono gestiti e archiviati in Azure. Come con la protezione di Azure RMS, le informazioni protette con AD RMS non vengono mai inviate al cloud.

> [!NOTE]
> Usare questa configurazione solo quando è necessario e solo per i documenti e i messaggi di posta elettronica che lo richiedono. La protezione di AD RMS non offre i vantaggi elencati che si ottengono quando si usa la protezione di Azure RMS e il suo scopo principale è la riservatezza dei dati.

Gli utenti non vengono informati quando un'etichetta usa la protezione di AD RMS invece di quella di Azure RMS. A causa delle restrizioni della protezione di AD RMS, è necessario assicurarsi di fornire istruzioni chiare per la selezione, da parte degli utenti, delle etichette da applicare alla protezione di AD RMS.

## <a name="limitations-when-using-hyok"></a>Limitazioni durante l'uso di HYOK

Oltre a non supportare i vantaggi elencati che si ottengono quando si usa la protezione di Azure RMS, l'uso della protezione di AD RMS con Azure Information Protection presenta le limitazioni seguenti:

- Non supporta Office 2010 o Office 2007.

- Se si usa anche la protezione di Azure RMS: non usare l'opzione **Non inoltrare** quando si configura un'etichetta per la protezione di Azure RMS. È inoltre necessario indicare agli utenti di non selezionare manualmente questa opzione in Outlook. 

    Se l'opzione Non inoltrare viene applicata da un'etichetta o manualmente dagli utenti, l'opzione può essere applicata dalla distribuzione di AD RMS piuttosto che dal servizio di Azure Rights Management designato. In questo scenario, gli utenti esterni con cui sono state effettuate condivisioni non saranno in grado di aprire messaggi di posta elettronica con l'opzione Non inoltrare applicata.

## <a name="requirements-for-hyok"></a>Requisiti per HYOK

Verificare che la distribuzione di AD RMS attiva soddisfi i requisiti seguenti per garantire la protezione di AD RMS per Azure Information Protection.

- Configurazione di AD RMS:
    
    - Versione minima di Windows Server 2012 R2: obbligatoria per gli ambienti di produzione, ma per scopi di testing o valutazione è possibile usare una versione minima di Windows Server 2008 R2 con Service Pack 1.
    
    - Cluster radice di AD RMS singolo.
    
    - [Modalità di crittografia 2](https://technet.microsoft.com/library/hh867439.aspx): è possibile verificare la versione della modalità di crittografia del cluster AD RMS e il relativo stato di integrità tramite lo [strumento RMS Analyzer](https://www.microsoft.com/en-us/download/details.aspx?id=46437).   
    
    - In Active Directory non è registrato un punto di connessione del servizio (SCP). Il punto SCP non viene usato quando si usa la protezione di AD RMS con Azure Information Protection. Se è stato registrato un punto di connessione del servizio per la distribuzione di AD RMS, è necessario rimuoverlo per il corretto funzionamento dell'[individuazione dei servizi](../rms-client/client-deployment-notes.md#rms-service-discovery) per la protezione di Azure Rights Management.
    
    - I server AD RMS sono configurati per l'uso di SSL/TLS con un certificato x.509 valido considerato attendibile dai client di connessione: necessario per gli ambienti di produzione, ma non per scopi di testing o valutazione.
    
    - Modelli di diritti configurati.

- La sincronizzazione delle directory è configurata tra l'istanza locale di Active Directory e Azure Active Directory e gli utenti che usano la protezione di AD RMS sono configurati per l'accesso Single Sign-On.

- Se si condividono documenti o messaggi di posta elettronica protetti da AD RMS con altri utenti esterni all'organizzazione: AD RMS è configurato per i trust definiti in modo esplicito in una relazione punto a punto diretta con altre organizzazioni tramite domini utente trusted (TUD) o relazioni di trust federative create mediante Active Directory Federation Services (AD FS).

- Gli utenti hanno Office 2013 Pro Plus con Service 1 o Office 2016 Pro Plus, in esecuzione in Windows 7 Service Pack 1 o versioni successive. Si noti che Office 2010 e Office 2007 non sono supportati per questo scenario.

> [!IMPORTANT]
> Per soddisfare la garanzia elevata offerta da questo scenario, è consigliabile che i server di AD RMS non si trovino nella rete perimetrale e che vengano usati solo nei computer ben gestiti (ad esempio, non nei dispositivi mobili o nei computer del gruppo di lavoro). 
> 
> È inoltre consigliabile che il cluster AD RMS usi un modulo di protezione hardware (HSM), in modo che la chiave privata per il certificato concessore di licenze server (SLC) non possa essere esposta o rubata se la distribuzione di AD RMS viene violata o compromessa. 

Per informazioni sulla distribuzione e istruzioni per AD RMS, vedere [Active Directory Rights Management Services](https://technet.microsoft.com/library/hh831364.aspx) nella libreria di Windows Server. 


## <a name="locating-the-information-to-specify-ad-rms-protection-with-an-azure-information-protection-label"></a>Individuazione delle informazioni per specificare la protezione di AD RMS con un'etichetta di Azure Information Protection

Quando si configura un'etichetta per la protezione di AD RMS, è necessario specificare il GUID del modello e l'URL di gestione licenze del cluster AD RMS. Questi due valori sono disponibili nella console di Active Directory Rights Management Services:

- Per individuare il modello GUID: espandere il cluster e fare clic su **Modelli di criteri per i diritti di utilizzo**. In **Modelli di criteri per i diritti di utilizzo distribuiti** è quindi possibile copiare il GUID del modello che si vuole usare. Ad esempio: 82bf3474-6efe-4fa1-8827-d1bd93339119

- Per individuare l'URL di gestione licenze: fare clic sul nome del cluster. In **Dettagli cluster** copiare il valore **Gestione licenze** ad eccezione della stringa **/_wmcs/licensing**. Ad esempio: https://rmscluster.contoso.com 
    
    Se si ha un valore di licenza Extranet e un valore di gestione delle licenze Intranet diversi tra loro: specificare il valore Extranet solo se si condividono documenti o messaggi di posta elettronica protetti con i partner definiti con relazioni di trust esplicite da punto a punto. In caso contrario, usare il valore Intranet e assicurarsi che tutti i computer client che usano la protezione di AD RMS con Azure Information Protection si connettano tramite una connessione Intranet (ad esempio, i computer remoti devono usare una connessione VPN).

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni su questa funzionalità di anteprima, vedere l'annuncio del post di blog [Azure Information Protection with HYOK (Hold Your Own Key)](https://blogs.technet.microsoft.com/enterprisemobility/2016/08/10/azure-information-protection-with-hyok-hold-your-own-key/) (Azure Information Protection con HYOK (Hold Your Own Key)).

Per configurare un'etichetta per la protezione di AD RMS, vedere [Come configurare un'etichetta per applicare la protezione di Rights Management](../deploy-use/configure-policy-protection.md). 

[!INCLUDE[Commenting house rules](../includes/houserules.md)]


<!--HONumber=Jan17_HO4-->


