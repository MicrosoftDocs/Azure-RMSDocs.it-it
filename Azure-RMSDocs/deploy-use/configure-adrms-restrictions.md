---
title: Protezione HYOK per Azure Information Protection
description: Identificare le restrizioni, i prerequisiti e le raccomandazioni se si seleziona la protezione HYOK (AD RMS) con Azure Information Protection.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 12/08/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 7667b5b0-c2e9-4fcf-970f-05577ba51126
ms.openlocfilehash: 6167b99593bacdf9e717c3b57839440bac39ecec
ms.sourcegitcommit: dd53f3dc2ea2456ab512e3a541d251924018444e
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/08/2018
---
# <a name="hold-your-own-key-hyok-requirements-and-restrictions-for-ad-rms-protection"></a>Requisiti e restrizioni HYOK per la protezione di AD RMS

>*Si applica a: Azure Information Protection*

Per proteggere documenti e messaggi di posta elettronica contenenti informazioni riservate, è in genere possibile applicare la protezione di Azure Rights Management (Azure RMS) e sfruttare i vantaggi seguenti:

- Infrastruttura server non necessaria. In questo modo, la soluzione è più veloce e conveniente da distribuire e gestire rispetto a una soluzione locale.

- Condivisione più agevole con partner e utenti di altre organizzazioni tramite l'autenticazione basata su cloud.

- Stretta integrazione con i servizi di Office 365, ad esempio ricerca, visualizzatori Web, viste trasformate tramite Pivot, anti-malware, eDiscovery e Delve.

- Monitoraggio di documenti, revoca e notifiche tramite posta elettronica per i documenti condivisi contenenti informazioni riservate.

Azure RMS consente di proteggere i documenti e i messaggi di posta elettronica dell'organizzazione tramite una chiave privata gestita da Microsoft (impostazione predefinita) o dall'utente (scenario BYOK o "bring your own key"). Le informazioni protette con Azure RMS non vengono mai inviate al cloud. I documenti e i messaggi di posta elettronica protetti non vengono archiviati in Azure a meno che non venga richiesto esplicitamente o si usi un altro servizio cloud che li archivia in Azure. Per altre informazioni sulle opzioni della chiave del tenant, vedere [Pianificazione e implementazione della chiave del tenant di Azure Information Protection](../plan-design/plan-implement-tenant-key.md). 

Tuttavia, alcune organizzazioni possono avere l'esigenza di proteggere un piccolo subset di documenti e messaggi di posta elettronica con una chiave ospitata in locale. Ad esempio, questa può essere necessaria per motivi normativi e di conformità.  

Questa configurazione viene a volte definita HYOK, ossia "hold your own key" ed è supportata da Azure Information Protection quando si dispone di una distribuzione di Active Directory Rights Management Services (AD RMS) attiva con i requisiti descritti nella sezione seguente.

In questo scenario HYOK, i criteri dei diritti e la chiave privata dell'organizzazione che protegge tali criteri vengono gestiti e conservati in locale, mentre i criteri di Azure Information Protection per l'applicazione di etichette e la classificazione vengono gestiti e archiviati in Azure. Come con la protezione di Azure RMS, le informazioni protette con AD RMS non vengono mai inviate al cloud.

> [!NOTE]
> Usare questa configurazione solo quando è necessario e solo per i documenti e i messaggi di posta elettronica che lo richiedono. La protezione di AD RMS non offre i vantaggi elencati che si ottengono quando si usa la protezione di Azure RMS e il suo scopo principale è la riservatezza dei dati.
>
> Anche per le organizzazioni che la usano, questa configurazione è in genere adatta a meno del 10% del contenuto da proteggere. Come prassi consigliata, usarla solo per i documenti o i messaggi di posta elettronica che soddisfano tutti i criteri seguenti:
> 
> **Il contenuto è classificato come altamente riservato all'interno dell'organizzazione e l'accesso è limitato a poche persone**
> 
> **Il contenuto non viene mai condiviso all'esterno dell'organizzazione**
> 
> **Il contenuto viene usato solo nella rete interna**
> 
> **Il contenuto non deve essere usato su computer Mac o dispositivi mobili**

Gli utenti non vengono informati quando un'etichetta usa la protezione di AD RMS anziché quella di Azure RMS. A causa delle restrizioni e delle limitazioni della protezione di AD RMS, assicurarsi di fornire indicazioni chiare sulle eccezioni relative ai casi in cui gli utenti devono selezionare le etichette che applicano la protezione di AD RMS. 

I [criteri con ambito](configure-policy-scope.md) costituiscono un buon metodo per assicurarsi che le etichette configurate per la protezione di AD RMS siano visibili solo agli utenti che devono applicare la protezione di AD RMS. 

## <a name="additional-limitations-when-using-hyok"></a>Limitazioni aggiuntive durante l'uso di HYOK

Oltre a non supportare i vantaggi elencati che si ottengono quando si usa la protezione di Azure RMS, l'uso della protezione di AD RMS con Azure Information Protection presenta le limitazioni seguenti:

- Non supporta Office 2010 o Office 2007.

- Richiedere agli utenti di non selezionare **Non inoltrare** in Outlook oppure fornire istruzioni specifiche. 

    È possibile configurare un'etichetta in modo che **Non inoltrare** usi HYOK o il servizio Azure Rights Management. In alternativa gli utenti possono selezionare direttamente Non inoltrare. Possono selezionare questa opzione con il pulsante **Non inoltrare** della scheda **Messaggio** della barra multifunzione di Office oppure con le opzioni di menu di Outlook. Le opzioni di menu **Non inoltrare** si trovano in **File** > **Autorizzazioni**e in corrispondenza del pulsante **Autorizzazioni** della scheda **Opzioni** della barra multifunzione. 
    
    Il client Azure Information Protection usa sempre Azure RMS quando gli utenti selezionano il pulsante **Non inoltrare** in Outlook. Se questo non è il comportamento desiderato, è possibile nascondere questo pulsante impostando l'[impostazione dei criteri ](../deploy-use/configure-policy-settings.md) **Add the Do Not Forward button to the Outlook ribbon** (Aggiungi il pulsante Non inoltrare alla barra multifunzione Outlook) su **Off** (Disattiva). 
    
    Quando gli utenti selezionano **Non inoltrare** in un'opzione di menu di Outlook possono scegliere tra Azure RMS e AD RMS, ma potrebbero non sapere quale opzione selezionare per il loro messaggio di posta elettronica. Se viene usato AD RMS quando dovrebbe essere usato Azure RMS, è possibile che gli utenti con cui si gestiscono condivisioni esterne non riescano ad aprire i messaggi di posta elettronica.

- Se si configurano autorizzazioni definite dall'utente per Word, Excel, PowerPoint e File Explorer, in File Explorer la protezione viene sempre applicata con Azure RMS anziché con HYOK (AD RMS). Questa limitazione non è valida per la versione di anteprima corrente del client.

- Se gli utenti scelgono un'etichetta in Outlook che applica la protezione di AD RMS e quindi cambiano idea prima di inviare la posta elettronica e selezionano un'etichetta che applica la protezione di Azure RMS, la nuova etichetta selezionata non viene applicata. In tal caso, viene visualizzato il messaggio di errore seguente: **Azure Information Protection non può applicare questa etichetta. Non si hanno le autorizzazioni necessarie per eseguire questa azione.**
    
    L'unica soluzione alternativa consiste nel chiudere il messaggio di posta elettronica e riavviare. La stessa limitazione si applica se, allo stesso modo, gli utenti scelgono prima un'etichetta che applica la protezione di Azure RMS e quindi la sostituiscono con un'etichetta che applica la protezione di AD RMS.

## <a name="requirements-for-hyok"></a>Requisiti per HYOK

Verificare che la distribuzione di AD RMS attiva soddisfi i requisiti seguenti per garantire la protezione di AD RMS per Azure Information Protection.

- Configurazione di AD RMS:
    
    - Versione minima di Windows Server 2012 R2: obbligatoria per gli ambienti di produzione, ma per scopi di testing o valutazione è possibile usare una versione minima di Windows Server 2008 R2 con Service Pack 1.
    
    - Una delle topologie seguenti:
        
        - Foresta singola con singolo cluster radice AD RMS. 
        
        - Più foreste con cluster radice AD RMS indipendenti e utenti che non dispongono di accesso ai contenuti protetti dagli utenti delle altre foreste.
        
        - Più foreste con cluster AD RMS in ognuna di esse. Ogni cluster AD RMS condivide un URL di gestione licenze che fa riferimento allo stesso cluster AD RMS. In questo cluster AD RMS è necessario importare tutti i certificati di dominio utente trusted (TUD) da tutti gli altri cluster AD RMS. Per altre informazioni su questa topologia, vedere [Trusted User Domains (Domini utente trusted)](https://technet.microsoft.com/library/dd983944(v=ws.10\).aspx).
        
    Quando si hanno più cluster AD RMS in foreste diverse, eliminare le etichette presenti nei criteri globali che applicano la protezione HYOK (AD RMS) e configurare [criteri con ambito](configure-policy-scope.md) per ogni cluster. Quindi assegnare gli utenti di ogni cluster ai criteri con ambito corrispondenti, evitando di usare gruppi per i quali un utente viene assegnato a più criteri con ambito. In seguito a questa assegnazione ogni utente deve avere etichette per un solo cluster AD RMS. 
    
    - [Modalità crittografia 2](https://technet.microsoft.com/library/hh867439.aspx): è possibile verificare la modalità controllando le proprietà del cluster AD RMS nella scheda **Generale**.
    
    - In Active Directory non è registrato un punto di connessione del servizio (SCP): il punto SCP non viene usato quando si usa la protezione di AD RMS con Azure Information Protection. Se è stato registrato un punto di connessione del servizio per la distribuzione di AD RMS è necessario rimuoverlo, per garantire il corretto funzionamento dell'[individuazione dei servizi](../rms-client/client-deployment-notes.md#rms-service-discovery) della protezione di Azure Rights Management.
    
    - I server AD RMS sono configurati per l'uso di SSL/TLS con un certificato x.509 valido considerato attendibile dai client di connessione: necessario per gli ambienti di produzione, ma non per scopi di testing o valutazione.
    
    - Modelli di diritti configurati.

- La sincronizzazione delle directory è configurata tra l'istanza locale di Active Directory e Azure Active Directory e gli utenti che usano la protezione di AD RMS sono configurati per l'accesso Single Sign-On.

- Se si condividono documenti o messaggi di posta elettronica protetti da AD RMS con altri utenti esterni all'organizzazione: AD RMS è configurato per i trust definiti in modo esplicito in una relazione punto a punto diretta con altre organizzazioni tramite domini utente trusted (TUD) o relazioni di trust federative create mediante Active Directory Federation Services (AD FS).

- Gli utenti hanno Office 2013 Pro Plus con Service Pack 1 o Office 2016 Pro Plus, in esecuzione in Windows 7 Service Pack 1 o versioni successive. Si noti che Office 2010 e Office 2007 non sono supportati per questo scenario.

> [!IMPORTANT]
> Per soddisfare la garanzia elevata offerta da questo scenario, è consigliabile che i server di AD RMS non si trovino nella rete perimetrale e che vengano usati solo nei computer ben gestiti (ad esempio, non nei dispositivi mobili o nei computer del gruppo di lavoro). 
> 
> È inoltre consigliabile che il cluster AD RMS usi un modulo di protezione hardware (HSM), in modo che la chiave privata per il certificato concessore di licenze server (SLC) non possa essere esposta o rubata se la distribuzione di AD RMS viene violata o compromessa. 

Per informazioni sulla distribuzione e istruzioni per AD RMS, vedere [Active Directory Rights Management Services](https://technet.microsoft.com/library/hh831364.aspx) nella libreria di Windows Server. 


## <a name="locating-the-information-to-specify-ad-rms-protection-with-an-azure-information-protection-label"></a>Individuazione delle informazioni per specificare la protezione di AD RMS con un'etichetta di Azure Information Protection

Quando si configura un'etichetta per la protezione **HYOK (AD RMS)** è necessario specificare l'URL di licenza del cluster AD RMS. È anche necessario specificare un modello configurato per le autorizzazioni da concedere agli utenti oppure consentire agli utenti di definire le autorizzazioni e gli utenti. 

I valori del GUID del modello e dell'URL sono disponibili nella console di Active Directory Rights Management Services:

- Per individuare il GUID di un modello, espandere il cluster e fare clic su **Modelli di criteri per i diritti di utilizzo**. In **Modelli di criteri per i diritti di utilizzo distribuiti** è quindi possibile copiare il GUID del modello che si vuole usare. Ad esempio: 82bf3474-6efe-4fa1-8827-d1bd93339119

- Per individuare l'URL di gestione licenze: fare clic sul nome del cluster. In **Dettagli cluster** copiare il valore **Gestione licenze** ad eccezione della stringa **/_wmcs/licensing**. Ad esempio: https://rmscluster.contoso.com 
    
    Se sono presenti un valore di gestione licenze Extranet e un valore di gestione licenze Intranet diversi tra loro: specificare il valore Extranet solo se si condividono documenti o messaggi di posta elettronica protetti con partner definiti mediante relazioni di trust esplicite da punto a punto. In caso contrario, usare il valore Intranet e assicurarsi che tutti i computer client che usano la protezione di AD RMS con Azure Information Protection si connettano tramite una connessione Intranet (ad esempio, i computer remoti devono usare una connessione VPN).

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni su questa funzionalità e indicazioni su quando usarla, vedere l'annuncio del post di blog [Azure Information Protection with HYOK (Hold Your Own Key)](https://cloudblogs.microsoft.com/enterprisemobility/2016/08/10/azure-information-protection-with-hyok-hold-your-own-key/) (Azure Information Protection con HYOK (Hold Your Own Key)).

Per configurare un'etichetta per la protezione di AD RMS, vedere [Come configurare un'etichetta per la protezione di Rights Management](../deploy-use/configure-policy-protection.md). 

[!INCLUDE[Commenting house rules](../includes/houserules.md)]