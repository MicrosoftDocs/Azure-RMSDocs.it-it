---
title: Domande frequenti per il client di Azure Information Protection classico
description: Alcune domande frequenti su Azure Information Protection e il relativo servizio di protezione, Azure Rights Management (Azure RMS). Le domande frequenti qui elencate sono rilevanti solo per il client AIP classico.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 03/07/2021
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.suite: ems
ms.custom: admin
search.appverid:
- MET150
ms.openlocfilehash: 9f53544a201d3500f63c472b5cdd58e01c69dc1f
ms.sourcegitcommit: 8a45d209273d748ee0f2a96c97893288c0b7efa5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/08/2021
ms.locfileid: "102446899"
---
# <a name="frequently-asked-questions-for-the-azure-information-protection-classic-client"></a>Domande frequenti relative al client di Azure Information Protection classico

>***Si applica a**: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*
>
>***Pertinente per**: solo per il [client classico AIP Unified Labeling](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients). Per ulteriori informazioni, vedere [domande frequenti per Azure Information Protection](faqs.md). *

Questo articolo elenca le domande frequenti relative al solo Azure Information Protection client classico.

>[!NOTE] 
> Per offrire un'esperienza per i clienti unificata e semplificata, il **client classico di Azure Information Protection** e **Gestione etichette** nel portale di Azure saranno **deprecati** a partire dal **31 marzo 2021**. In questo intervallo di tempo tutti i clienti correnti di Azure Information Protection possono passare alla soluzione di etichettatura unificata usando la piattaforma di etichettatura unificata di Microsoft Information Protection. Altre informazioni nell'[avviso ufficiale sulla deprecazione](https://aka.ms/aipclassicsunset).

## <a name="is-the-azure-information-protection-client-only-for-subscriptions-that-include-classification-and-labeling"></a>Il client Azure Information Protection è disponibile solo per le sottoscrizioni che includono la classificazione e l'assegnazione di etichette?

No. Il client AIP classico può essere usato anche con le sottoscrizioni che includono solo il servizio Azure Rights Management, solo per la protezione dei dati.

Quando il client classico viene installato senza un criterio di Azure Information Protection, il client opera automaticamente in [modalità di sola protezione](./rms-client/client-protection-only-mode.md), che consente agli utenti di applicare modelli Rights Management e autorizzazioni personalizzate. 

Se successivamente si acquista una sottoscrizione che include la classificazione e l'assegnazione di etichette, il client passa automaticamente alla modalità standard durante il download dei criteri di Azure Information Protection.


## <a name="whats-the-difference-between-windows-server-fci-and-the-azure-information-protection-scanner"></a>Qual è la differenza tra il cluster di failover di Windows Server e il Azure Information Protection scanner?

L'infrastruttura di classificazione file di Windows Server è stata storicamente un'opzione per classificare i documenti e quindi proteggerli tramite il [connettore Rights Management](deploy-rms-connector.md) (solo documenti di Office) o uno [script di PowerShell](./rms-client/configure-fci.md) (tutti i tipi di file). 

Si consiglia ora di usare lo [scanner di Azure Information Protection](deploy-aip-scanner.md). Lo scanner usa il client Azure Information Protection e i criteri di Azure Information Protection per assegnare etichette ai documenti (tutti i tipi di file) in modo che questi documenti possano essere poi classificati e, facoltativamente, protetti.

Le differenze principali tra queste due soluzioni sono le seguenti:

|  |Infrastruttura di classificazione file di Windows Server  |Scanner di Azure Information Protection  |
|---------|---------|---------|
|**Archivi dati supportati**    | Cartelle locali in Windows Server        | - Condivisione file di Windows e NAS (Network-Attached Storage)<br /><br />- SharePoint Server 2016 e SharePoint Server 2013. Anche SharePoint Server 2010 è supportato per i clienti che dispongono del [supporto "Extended" per questa versione di SharePoint](https://support.microsoft.com/lifecycle/search?alpha=SharePoint%20Server%202010).        |
|**Modalità operativa**     |In tempo reale         |Esegue sistematicamente la ricerca per indicizzazione degli archivi dati una volta o ripetutamente         |
|**Tipi di file supportati**     | - Per impostazione predefinita, sono protetti tutti i tipi di file <br /><br />- Specifici tipi di file possono essere esclusi dalla protezione modificando il Registro di sistema|Supporto per i tipi di file: <br /><br />- I tipi di file Office e i documenti PDF sono protetti per impostazione predefinita <br /><br />- Altri tipi di file possono essere inclusi nella protezione modificando il Registro di sistema|

### <a name="setting-rights-management-owners"></a>Impostazione dei proprietari di Rights Management

Per impostazione predefinita, per l'istanza del cluster di failover di Windows Server e per lo scanner Azure Information Protection, il [proprietario del Rights Management](configure-usage-rights.md#rights-management-issuer-and-rights-management-owner) è impostato sull'account che protegge il file.

Eseguire l'override delle impostazioni predefinite come indicato di seguito:

- **FCI di Windows Server**: impostare il proprietario Rights Management come un singolo account per tutti i file o impostare in modo dinamico il proprietario Rights Management per ogni file. 

    Per impostare in modo dinamico il proprietario di Rights Management, usare il parametro **-OwnerMail [posta elettronica proprietario file di origine]** e relativo valore. Questa configurazione recupera l'indirizzo di posta elettronica dell'utente da Active Directory usando il nome dell'account utente specificato nella proprietà del proprietario del file.

- **Azure Information Protection scanner**: per i file appena protetti, impostare il proprietario Rights Management in modo che sia un singolo account per tutti i file in un archivio dati specificato, specificando l'impostazione **predefinita del proprietario** nel profilo dello scanner. 

    L'impostazione dinamica del proprietario Rights Management per ogni file non è supportata e il proprietario Rights Management non viene modificato per i file precedentemente protetti. 

    > [!NOTE]
    > Quando lo scanner protegge i file inclusi in siti e librerie di SharePoint, il proprietario di Rights Management viene impostato in modo dinamico per ogni file usando il valore Editor di SharePoint.

## <a name="can-a-file-have-more-than-one-classification"></a>Un file può avere più di una classificazione?

Poiché gli utenti possono selezionare una sola etichetta alla volta per ogni documento o messaggio di posta elettronica, la classificazione è spesso una sola. Tuttavia, se gli utenti selezionano un'etichetta secondaria, vengono effettivamente applicate due etichette contemporaneamente, ovvero un'etichetta primaria e un'etichetta secondaria. Se si usano etichette secondarie, il file può avere due classificazioni che indicano una relazione padre/figlio per un ulteriore livello di controllo.

Ad esempio, l'etichetta **Confidential** può contenere etichette secondarie, ad esempio **Legal** e **Finance**. È possibile applicare contrassegni visivi di classificazione e modelli di Rights Management diversi alle etichette secondarie. Un utente non può selezionare l'etichetta **riservata** autonomamente; solo una delle relative etichette secondarie, ad esempio **Legal**. Di conseguenza, l'etichetta impostata visualizzata dall'utente sarà **Confidential \ Legal** (Riservato \ Legale). I metadati di tale file includono una sola proprietà di testo personalizzato per **Confidential** (Riservato), una proprietà di testo personalizzato per **Legal** (Legale) e un'altra proprietà che contiene entrambi i valori, **Confidential Legal** (Riservato Legale). 

Quando si usano etichette secondarie, non configurare contrassegni visivi, protezione e condizioni nell'etichetta principale. Quando si usano etichette secondarie, configurare queste impostazioni solo nell'etichetta secondaria. Se si configurano le impostazioni nell'etichetta principale e nella relativa etichetta secondaria, le impostazioni dell'etichetta secondaria hanno priorità.
## <a name="how-do-i-prevent-somebody-from-removing-or-changing-a-label"></a>Come si può impedire a un utente di rimuovere o modificare un'etichetta?

Sebbene esista un' [impostazione dei criteri](configure-policy-settings.md) che richiede agli utenti di indicare perché abbassano un'etichetta di classificazione, rimuovendo un'etichetta o rimuovendo la protezione, questa impostazione non impedisce tali azioni. Per impedire agli utenti di rimuovere o modificare un'etichetta, è necessario che il contenuto sia già protetto e che le autorizzazioni di protezione non concedano all'utente il [diritto di utilizzo](configure-usage-rights.md) per l'esportazione o il controllo completo

## <a name="how-can-dlp-solutions-and-other-applications-integrate-with-azure-information-protection"></a>Come è possibile integrare soluzioni DLP e altre applicazioni con Azure Information Protection?

Per la classificazione, Azure Information Protection usa metadati persistenti che includono un'etichetta di testo non crittografata. Queste informazioni possono essere lette da soluzioni DLP e da altre applicazioni. 

Per altre informazioni su questi metadati, vedere [Etichettare le informazioni archiviate in documenti e messaggi di posta elettronica](configure-policy.md#label-information-stored-in-emails-and-documents).

Per esempi dell'uso di questi metadati con le regole del flusso di posta di Exchange Online, vedere [Configurazione delle regole del flusso di posta per le etichette di Exchange Online](configure-exo-rules.md).

## <a name="can-i-create-a-document-template-that-automatically-includes-the-classification"></a>È possibile creare un modello di documento che include automaticamente la classificazione?

Sì. È possibile configurare un'etichetta per [applicare un'intestazione o un piè di pagina che include il nome dell'etichetta](configure-policy-markings.md). Tuttavia, se non soddisfa i requisiti, solo per il client classico di Azure Information Protection, è possibile creare un modello di documento con la formattazione desiderata e aggiungere la classificazione come codice campo. 

Ad esempio, si potrebbe usare una tabella nell'intestazione del documento che visualizza la classificazione. Oppure usare una formulazione specifica per un'introduzione che fa riferimento alla classificazione del documento.

Per aggiungere questo codice di campo nel documento:

1. Etichettare il documento e salvarlo. Questa azione consente di creare nuovi campi di metadati che è ora possibile usare per il codice di campo.

2. Nel documento, posizionare il cursore dove si vuole aggiungere la classificazione dell'etichetta e quindi nella scheda **Inserisci** selezionare **Testo** > **Parti rapide** > **Campo**.

3. Nella finestra di dialogo **Campo** selezionare **Informazioni documento** nell'elenco a discesa **Categorie**. Nell'elenco a discesa **Nome campi** selezionare quindi **DOCPROPERTY**.

4. Nell'elenco a discesa **Proprietà** selezionare **Riservatezza** e selezionare **OK**.

La classificazione dell'etichetta corrente viene visualizzata nel documento e questo valore verrà aggiornato automaticamente ogni volta che si apre il documento o si usa il modello. Pertanto, se l'etichetta cambia, la classificazione visualizzata per questo codice di campo viene aggiornata automaticamente nel documento.

## <a name="how-is-classification-for-emails-using-azure-information-protection-different-from-exchange-message-classification"></a>In che modo la classificazione per i messaggi di posta elettronica utilizza Azure Information Protection diversa dalla classificazione dei messaggi di Exchange?

La classificazione dei messaggi di Exchange è una funzionalità precedente in grado di classificare i messaggi di posta elettronica e viene implementata indipendentemente dalle etichette Azure Information Protection o dalle etichette di riservatezza che applicano

Tuttavia, è possibile integrare questa funzionalità precedente con le etichette, in modo che quando gli utenti classificano un messaggio di posta elettronica usando Outlook sul Web e usando alcune applicazioni di posta elettronica per dispositivi mobili, la classificazione delle etichette e i contrassegni di etichetta corrispondenti vengono aggiunti automaticamente.

È possibile applicare la stessa tecnica per usare le etichette con Outlook sul web e le applicazioni di posta elettronica per dispositivi mobili.

Si noti che non è necessario eseguire questa operazione se si usa Outlook sul Web con Exchange Online, perché questa combinazione supporta l'etichettatura incorporata quando si pubblicano le etichette di riservatezza da Office 365 Security & Compliance Center, Microsoft 365 Security Center o Microsoft Compliance Center.

Se non è possibile usare le etichette predefinite con Outlook sul Web, vedere la procedura di configurazione per questa soluzione alternativa: [integrazione con la classificazione dei messaggi di Exchange legacy](rms-client/client-admin-guide-customizations.md#integration-with-the-legacy-exchange-message-classification)

## <a name="how-do-i-configure-a-mac-computer-to-protect-and-track-documents"></a>Come si configura un computer Mac per proteggere e rilevare i documenti?

Prima di tutto, assicurarsi di avere installato Office per Mac usando il collegamento di installazione software da https://admin.microsoft.com. Per istruzioni complete, vedere [scaricare e installare o reinstallare Microsoft 365 o Office 2019 in un PC o Mac](https://support.office.com/article/Download-and-install-or-reinstall-Office-365-or-Office-2016-on-a-PC-or-Mac-4414EAAF-0478-48BE-9C42-23ADC4716658).

Aprire Outlook e creare un profilo usando il Microsoft 365 account aziendale o dell'Istituto di istruzione. Creare un nuovo messaggio, quindi eseguire le operazioni seguenti per configurare Office in modo che possa proteggere documenti e messaggi di posta elettronica usando il servizio Azure Rights Management:

1. Nel nuovo messaggio, nella scheda **Opzioni** fare clic su **Autorizzazioni**, quindi fare clic su **Verifica credenziali**.

2. Quando richiesto, specificare di nuovo Microsoft 365 i dettagli dell'account aziendale o dell'Istituto di istruzione e selezionare **Accedi**.

    Vengono scaricati i modelli di Azure Rights Management e **Verifica credenziali** viene sostituito da opzioni che includono **Nessuna restrizione**, **Non inoltrare**, nonché tutti i modelli di Azure Rights Management pubblicati per il tenant. Ora è possibile annullare questo nuovo messaggio.

Per proteggere un messaggio di posta elettronica o un documento: nella scheda **Opzioni** fare clic su **Autorizzazioni** e scegliere un'opzione o un modello che protegga il messaggio di posta elettronica o il documento.

Per tenere traccia di un documento dopo averlo protetto: da un computer Windows in cui è installato il client di Azure Information Protection classico, registrare il documento con il sito di rilevamento dei documenti usando un'applicazione di Office o Esplora file. Per le istruzioni, vedere [Rilevare e revocare i documenti](./rms-client/client-track-revoke.md). Dal computer Mac ora è possibile usare il Web browser e accedere al sito di rilevamento dei documenti (https://track.azurerms.com)) per rilevare e revocare il documento.

## <a name="when-i-test-revocation-in-the-document-tracking-site-i-see-a-message-that-says-people-can-still-access-the-document-for-up-to-30-daysis-this-time-period-configurable"></a>Quando si esegue il test delle revoche nel sito di rilevamento dei documenti, viene visualizzato un messaggio che informa che gli utenti possono continuare ad accedere al documento fino a 30 giorni: è possibile configurare questo periodo di tempo?

Sì. Questo messaggio riflette la [licenza d'uso](configure-usage-rights.md#rights-management-use-license) per quel file specifico.

Se si revoca un file, tale azione può essere applicata solo quando l'utente viene autenticato per il servizio Azure Rights Management. Pertanto, se un file ha un periodo di validità della licenza d'uso di 30 giorni e l'utente ha già aperto il documento, l'utente continua ad avere accesso al documento per la durata della licenza d'uso. Quando la licenza scade, l'utente deve ripetere l'autenticazione e a quel punto gli viene negato l'accesso perché il documento ormai è revocato.

L'utente che ha protetto il documento, l'[autorità di certificazione di Rights Management](configure-usage-rights.md#rights-management-issuer-and-rights-management-owner), è esente da questa revoca e può sempre accedere ai propri documenti.

Il valore predefinito per il periodo di validità della licenza d'uso per un tenant è di 30 giorni e questa impostazione può essere modificata da un'impostazione più restrittiva in un'etichetta o un modello. Per altre informazioni sulla licenza d'uso e su come configurarla, vedere la documentazione sulla [licenza d'uso di Rights Management](configure-usage-rights.md#rights-management-use-license).

## <a name="whats-the-difference-between-byok-and-hyok-and-when-should-i-use-them"></a>Qual è la differenza tra BYOK e HYOK e quando usarli?

**Bring your own key** (BYOK) nel contesto di Azure Information Protection è il caso in cui si crea la propria chiave locale per la protezione di Azure Rights Management, quindi si trasferisce la chiave a un modulo di protezione hardware (HSM) in Azure Key Vault dove si continua a essere proprietari della chiave e a gestirla. Se non si esegue questa operazione, la protezione di Azure Rights Management userà una chiave che viene creata e gestita automaticamente in Azure. Questa configurazione predefinita è detta "gestita da Microsoft" anziché "gestita dal cliente" (opzione BYOK).

Per altre informazioni sulla modalità BYOK e se sia consigliabile scegliere questa topologia di chiave per l'organizzazione, vedere [Pianificazione e implementazione della chiave del tenant di Azure Information Protection](plan-implement-tenant-key.md).

**Hold your own key** (HYOK) nel contesto di Azure Information Protection serve alle poche organizzazioni che hanno un subset di documenti o messaggi di posta elettronica che non possono essere protetti da una chiave archiviata nel cloud. Per queste organizzazioni si applica tale restrizione anche se hanno creato e gestito la chiave usando la modalità BYOK. La restrizione è spesso dovuta a ragioni normative o di conformità e la configurazione HYOK deve essere applicata solo alle informazioni "top secret" che non saranno mai condivise all'esterno dell'organizzazione, ma usate solo nella rete interna, e non devono essere accessibili da dispositivi mobili.

Per queste eccezioni (in genere inferiori al 10% di tutti i contenuti che devono essere protetti), le organizzazioni possono usare una soluzione locale, Active Directory Rights Management Services, per creare la chiave che rimane locale. Con questa soluzione i computer ottengono i criteri di Azure Information Protection dal cloud, ma questo contenuto identificato può essere protetto usando la chiave locale.

Per altre informazioni su HYOK e per assicurarsi di aver compreso le relative linee guida, limitazioni e restrizioni di utilizzo, vedere [Requisiti e restrizioni HYOK per la protezione di AD RMS](configure-adrms-restrictions.md).

## <a name="what-do-i-do-if-my-question-isnt-here"></a>Cosa fare se la domanda non è presente?

Esaminare prima di tutto le domande frequenti elencate di seguito, specifiche per la classificazione e l'assegnazione di etichette, o specifiche per la protezione dei dati. Il [servizio Azure Rights Management (Azure RMS)](what-is-azure-rms.md) fornisce la tecnologia di protezione dei dati per Azure Information Protection. Azure RMS può essere usato con la classificazione e l'assegnazione di etichette o in modo indipendente. 

- [Domande frequenti su Azure Information Protection](faqs.md)

- [Domande frequenti per la classificazione e l'assegnazione di etichette](faqs-infoprotect.md)

- [Domande frequenti per la protezione dati](faqs-rms.md)

Se la domanda non risponde, vedere i collegamenti e le risorse elencate in [informazioni e supporto per Azure Information Protection](information-support.md).

Esistono anche Domande frequenti progettate per gli utenti finali:

- [Domande frequenti sull'app Azure Information Protection per iOS e Android](./rms-client/mobile-app-faq.md)

- [Domande frequenti per l'app RMS sharing per computer Mac](/previous-versions/msdn10/dn451248(v=msdn.10))