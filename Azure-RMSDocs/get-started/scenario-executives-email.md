---
title: Scenario AIP - Scambiarsi informazioni con privilegi tra dirigenti
description: "Questo scenario e la documentazione di supporto per l&quot;utente usano la tecnologia di protezione Azure Rights Management affinché i dirigenti possano scambiarsi in modo sicuro messaggi e allegati tramite posta elettronica e i criteri limitino automaticamente l&quot;accesso ai dirigenti senza che sia necessario alcun intervento da parte loro."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/23/2017
ms.topic: get-started-article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: e18cf5df-859e-4028-8d19-39b0842df33d
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 2131f40b51f34de7637c242909f10952b1fa7d9f
ms.openlocfilehash: 1407a7bee800fec0ba8498d0439586378003ed54
ms.lasthandoff: 02/24/2017


---

# <a name="scenario---executives-securely-exchange-privileged-information"></a>Scenario - Scambiarsi informazioni con privilegi tra dirigenti

>*Si applica a: Azure Information Protection, Office 365*

Questo scenario e la documentazione di supporto per l'utente usano la tecnologia Azure Rights Management di Azure Information Protection affinché i dirigenti possano scambiarsi in modo sicuro messaggi e allegati tramite posta elettronica e i criteri limitino automaticamente l'accesso ai dirigenti senza che sia necessario alcun intervento da parte loro. I messaggi di posta elettronica e gli eventuali allegati saranno automaticamente protetti da Azure Rights Management.

Se necessario, è possibile aggiungere un'eccezione alla regola, ad esempio l'abbreviazione DNP (per "Non proteggere") nell'oggetto del messaggio di posta elettronica, in modo che i dirigenti possano specificare l'abbreviazione se devono inviare un messaggio di posta elettronica non protetto ad esempio ad altri dirigenti, per esaminarlo prima di procedere all'inoltro.

Le istruzioni sono adatte ai casi seguenti:

-   Dirigenti che condividono informazioni riservate tra loro, da non condividere con altri utenti.

-   Quando inviano questi messaggi, i dirigenti devono semplicemente inviarli a un indirizzo di posta elettronica dell'ufficio anziché a uno personale.

-   I dirigenti dispongono di un modo per eseguire l'override della regola autonomamente se devono inviare un messaggio di posta elettronica non protetto ad altri dirigenti.

## <a name="deployment-instructions"></a>Istruzioni di distribuzione
![Istruzioni per l'amministratore per la distribuzione rapida di Azure RMS](../media/AzRMS_AdminBanner.png)

Verificare che siano soddisfatti i requisiti seguenti e quindi seguire le istruzioni per le procedure di supporto prima di passare alla documentazione dell'utente.

## <a name="requirements-for-this-scenario"></a>Requisiti per questo scenario
Per le istruzioni di funzionamento di questo scenario, sono necessari i requisiti seguenti:

|Requisito|Altre informazioni|
|---------------|--------------------------------|
|Definizione di account e gruppi per Office 365 o Azure Active Directory:<br /><br />- Un gruppo abilitato alla posta elettronica denominato **Dirigenti** e tutti i dirigenti membri di questo gruppo<br /><br />- Un gruppo abilitato alla posta elettronica denominato **Amministratori RMS** e tutti gli amministratori che configurano Azure RMS membri di questo gruppo|[Preparazione per Azure Information Protection](../plan-design/prepare.md)|
|La chiave del tenant di Azure Information Protection è gestita da Microsoft, non viene usato il sistema BYOK|[Pianificazione e implementazione della chiave del tenant di Azure Information Protection](../plan-design/plan-implement-tenant-key.md)|
|Azure Rights Management non è attivato|[Attivazione di Azure Rights Management](../deploy-use/activate-service.md)|
|Una di queste configurazioni:<br /><br />- Exchange Online è abilitato per Azure Rights Management<br /><br />- Il connettore RMS è installato e configurato per Exchange locale|Per Exchange Online: vedere le informazioni riportate in [Exchange Online: configurazione di IRM](../deploy-use/configure-office365.md#exchange-online-irm-configuration).<br /><br />Per Exchange locale: [Distribuzione del connettore di Azure Rights Management](../deploy-use/deploy-rms-connector.md)|
|Configurazione di un modello personalizzato, come descritto di seguito|[Configurazione di modelli personalizzati per il servizio Azure Rights Management](../deploy-use/configure-custom-templates.md)|
|Configurare una regola di protezione del trasporto per IRM, come descritto più avanti in questo articolo|Per Exchange Online: [Mail flow or transport rules](https://technet.microsoft.com/library/jj919238(v=exchg.150).aspx) (Regole di trasporto o del flusso di posta elettronica)<br /><br />Per Exchange 2013: [Creare una regola di protezione del trasporto](https://technet.microsoft.com/en-us/library/dd302432(v=exchg.150))<br /><br />Per Exchange 2010: [Creare una regola di protezione del trasporto](https://technet.microsoft.com/library/dd302432(v=exchg.141))|

### <a name="to-configure-the-custom-template-for-executives"></a>Per configurare il modello personalizzato per i dirigenti:

1.  Nel portale classico di Azure: Creare un nuovo modello personalizzato per Azure Rights Management, contenente i valori e le impostazioni seguenti:

    -   Nome: **Dirigenti**

    -   Diritti: concedere al gruppo dei **Dirigenti** abilitati per la posta i diritti di **Comproprietario**

    -   Ambito: Selezionare il gruppo dei **Dirigenti** e il gruppo degli **Amministratori RMS** abilitati per la posta elettronica.

2.  Pubblicare il nuovo modello.

3.  Solo per Exchange Online: aggiornare i modelli usando il comando Windows PowerShell per Exchange Online:

    ```
    Import-RMSTrustedPublishingDomain -Name "RMS Online -1" -RefreshTemplates -RMSOnline
    ```

### <a name="to-configure-the-transport-rule-for-irm"></a>Per configurare la regola del trasporto per IRM

-   Usare la documentazione di Exchange indicata nella tabella per informazioni sulla procedura per creare la regola del trasporto con le seguenti impostazioni:

    -   Nome: **Applica i modelli Dirigenti ai messaggi di posta elettronica dei dirigenti**

    -   Specificare il gruppo dei **Dirigenti** come mittente e destinatario della regola e delle altre condizioni.

    -   Per l'azione, selezionare **Applica protezione dei diritti al messaggio con** e quindi selezionare il modello **Dirigenti** configurato.

    -   Aggiungere l'eccezione **DNP** (come abbreviazione di "Non proteggere") o le parole scelte per identificare questa eccezione, da includere nell'oggetto.

    -   Verificare che la regola sia configurata per **Imponi**.

## <a name="user-documentation-instructions"></a>Istruzioni sulla documentazione per l'utente
A meno che non si desideri fornire istruzioni su come specificare **DNP** o le parole o frasi scelte per l'eccezione nell'oggetto del messaggio di posta elettronica, non esistono istruzioni sulle procedure da fornire agli utenti per questo scenario, perché la protezione dei messaggi di posta elettronica da e verso i dirigenti dell'azienda non richiede alcuna azione speciale da parte degli stessi. I messaggi di posta elettronica e gli eventuali allegati vengono protetti automaticamente in modo che solo i membri del gruppo Dirigenti possano accedervi.

Tuttavia, può essere necessario informare i dirigenti e l'help desk sulla protezione automatica dei messaggi e su come limitare l'uso di tali messaggi. Ad esempio, se i messaggi o gli allegati vengono inoltrati ad altri utenti, non possono essere letti in modo corretto. Se è stato configurata l'eccezione DNP (o una equivalente), verificare che il supporto tecnico sia a conoscenza di questa configurazione in modo che i dirigenti possano eseguire l'override della regola autonomamente, senza richiedere azioni da un amministratore di Exchange.

Usando il modello seguente, copiare e incollare l'annuncio in una comunicazione per gli utenti finali e apportare tali modifiche in base all'ambiente:

1.  Sostituire le istanze di *&lt;nome organizzazione&gt;* con il nome dell'organizzazione.

2.  Se si sceglie una stringa diversa da DNP per l'esenzione, sostituire anche tale valore e la relativa spiegazione.

3.  Sostituire *&lt;dominio di posta elettronica&gt;* con il nome di dominio della posta elettronica dell'organizzazione.

4.  Sostituire *&lt;dettagli contatto&gt;* con istruzioni su come gli utenti possono contattare il supporto tecnico, ad esempio il collegamento a un sito Web, un indirizzo di posta elettronica o un numero di telefono.

5.  Apportare altre eventuali modifiche a questo annuncio e quindi inviarlo agli utenti.

La documentazione dell'esempio mostra come questo annuncio viene visualizzato dagli utenti, dopo le personalizzazioni.

![Documentazione dell'utente del modello per la distribuzione rapida di Azure RMS](../media/AzRMS_UsersBanner.png)

### <a name="it-announcement-ltorganization-namegt-executive-emails-are-now-automatically-protected"></a>Annuncio IT: la posta elettronica dei dirigenti di &lt;Nome organizzazione&gt; è ora protetta automaticamente
Da questo momento, ogni volta che si inviano messaggi di posta elettronica a un altro dirigente di &lt;nome organizzazione&gt; i contenuti dei messaggi e gli eventuali allegati verranno protetti automaticamente in modo che solo un altro dirigente della società possa accedervi per leggere le informazioni, stamparli, copiarli e così via. Questa restrizione si applica anche se il messaggio di posta elettronica viene inoltrato ad altri utenti o se vengono salvati gli allegati. Questa protezione consente di impedire la perdita di dati sensibili e informazioni riservate.

Si noti che se si vuole che altri utenti che non sono dirigenti di &lt;nome organizzazione&gt; possano leggere e modificare le informazioni contenute in questi messaggi di posta elettronica, è necessario inviarle separatamente. In alternativa, per eseguire l'override della protezione automatica, digitare le lettere **DNP** (come abbreviazione di Non proteggere) all'interno dell'oggetto del messaggio di posta elettronica.

Quando si inviano informazioni aziendali riservate a un altro dirigente di &lt;nome organizzazione&gt;, ricordarsi di inviarle all'indirizzo di posta elettronica dell'ufficio (*nome*@&lt;dominio di posta elettronica&gt;) e non a un indirizzo personale.

**Serve assistenza?**

-   Contattare il supporto tecnico: &lt;dettagli contatto&gt;

### <a name="example-user-documentation"></a>Esempio di documentazione per l'utente
![Esempio di documentazione dell'utente per la distribuzione rapida di Azure RMS](../media/AzRMS_ExampleBanner.png)

#### <a name="it-announcement-vanarsdel-executive-emails-are-now-automatically-protected"></a>Annuncio IT: Protezione automatica dei messaggi di posta elettronica dei dirigenti di VanArsdel
Da questo momento, ogni volta che si inviano messaggi di posta elettronica a un altro dirigente della società VanArsdel, i contenuti dei messaggi e gli eventuali allegati verranno protetti automaticamente in modo che solo un altro dirigente della società possa accedervi per leggere le informazioni, stamparlo, copiarlo e così via. Questa restrizione si applica anche se il messaggio di posta elettronica viene inoltrato ad altri utenti o se vengono salvati gli allegati. Questa protezione consente di impedire la perdita di dati sensibili e informazioni riservate.

Si noti che se si desidera che altri utenti non dirigenti di VanArsdel possano leggere e modificare le informazioni contenute in questi messaggi di posta elettronica, è necessario inviarle separatamente. In alternativa, per eseguire l'override della protezione automatica, digitare le lettere **DNP** (come abbreviazione di Non proteggere) all'interno dell'oggetto del messaggio di posta elettronica.

Quando si inviano informazioni aziendali riservate a un altro dirigente di VanArsdel, ricordarsi di inviarle al relativo indirizzo di posta elettronica (*nome*@vanarsdelltd.com) dell'ufficio e non a un indirizzo personale.

**Serve assistenza?**

-   Contattare il supporto tecnico: helpdesk@vanarsdelltd.com

[!INCLUDE[Commenting house rules](../includes/houserules.md)]

