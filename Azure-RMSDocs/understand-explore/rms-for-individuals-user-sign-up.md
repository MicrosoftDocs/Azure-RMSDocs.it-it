---
title: "Modalità di iscrizione a RMS per utenti singoli - AIP"
description: Istruzioni per eseguire l&quot;iscrizione all&quot;account gratuito e informazioni tecniche sul funzionamento del processo.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/08/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: a60731bd-f78d-4f00-bb3e-354637b312ab
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 2131f40b51f34de7637c242909f10952b1fa7d9f
ms.openlocfilehash: 1134bff1935b3fada661865f31104e0316e8fecd
ms.lasthandoff: 02/24/2017


---

# <a name="how-users-sign-up-for-rms-for-individuals"></a>Modalità di iscrizione per RMS per utenti singoli

>*Si applica a: Azure Information Protection*

Per iscriversi per ottenere l'account gratuito, è necessario visitare la [pagina di Microsoft Azure Information Protection](https://portal.office.com/signup?sku=rms&ru=https%3A%2F%2Fportal.azurerms.com%2F%23%2Fdownload) e specificare il proprio indirizzo di posta elettronica aziendale. Il modo più comune con cui si verrà indirizzati a questa pagina per l'iscrizione è quando si riceve un messaggio di posta elettronica con un allegato protetto, che contiene istruzioni per iscriversi. Si riceverà un messaggio di posta elettronica di risposta da Microsoft e sarà quindi possibile completare la procedura di iscrizione inserendo i dettagli per creare l'account. Dopo il completamento, verrà visualizzata una pagina in cui è possibile scaricare Azure Information Protection per diversi dispositivi, con un collegamento alla guida per l'utente e un collegamento all'elenco aggiornato delle applicazioni che supportano la protezione di Rights Management in modo nativo. 

## <a name="to-sign-up-for-rms-for-individuals"></a>Per iscriversi per RMS per utenti singoli

1.  Su un computer Windows o Mac o un dispositivo mobile, andare alla [pagina di Microsoft Azure Information Protection](https://portal.office.com/signup?sku=rms&ru=https%3A%2F%2Fportal.azurerms.com%2F%23%2Fdownload).

2.  Digitare l'indirizzo di posta elettronica usato come indirizzo aziendale, ad esempio **janetm@contoso.com** o **p.dover@fabrikam.com**.

    > [!IMPORTANT]
    > Gli account di posta elettronica personali non sono supportati, pertanto non immettere un account Microsoft (definito in precedenza account Microsoft Live ID) né un altro account personale privato fornito dal proprio provider Internet.

3.  Fare clic su **Accedi**.

    Microsoft usa l'indirizzo di posta elettronica dell'utente per verificare se l'organizzazione dispone già di una [sottoscrizione a pagamento per Azure Information Protection](https://www.microsoft.com/en-us/cloud-platform/azure-information-protection-pricing) o di un [abbonamento a Office 365 che include la protezione dei dati mediante Azure Rights Management](http://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf). In tal caso, non è necessario RMS per utenti singoli quindi si verrà connessi immediatamente e l’iscrizione self-service per RMS per utenti singoli verrà annullata. Se non viene trovata una sottoscrizione a pagamento, si procederà al passaggio successivo.

4.  Attendere un messaggio di posta elettronica di conferma proveniente da Microsoft e inviato all'indirizzo di posta indicato Il messaggio proviene dal team di Office 365 (support@email.microsoftonline.com) e ha come oggetto il testo **Finish signing up for Microsoft Azure Information Protection** (Completare l'iscrizione a Microsoft Azure Information Protection).

5.  Quando si riceve il messaggio di posta elettronica, fare clic su **Yes, that's me (Sì, sono io)** per confermare l'indirizzo di posta elettronica e completare il processo di iscrizione.

6.  A questo punto viene aperta la pagina **One last thing ...(Un'ultima operazione)** dove specificare i dettagli per l'account. Digitare il nome, il cognome, specificare e confermare una password a scelta e quindi fare clic su **Start (Avvia)**.

7. Dopo aver creato l'account, verrà visualizzata una nuova pagina di Microsoft Azure Information Protection in cui è possibile scaricare e installare il client Azure Information Protection oppure fare clic sul collegamento alla [guida per l'utente](../rms-client/client-user-guide.md) per le procedure per i computer Windows.

Dopo avere creato l'account, è possibile iniziare a proteggere i file e a leggere quelli protetti da altri utenti. Quando viene chiesto di accedere per proteggere i file o leggere quelli protetti, immettere l'indirizzo di posta elettronica e la password usati per creare l'account per RMS per utenti singoli.

## <a name="technical-overview-of-the-sign-up-process"></a>Panoramica tecnica del processo di registrazione
RMS per utenti singoli usa un processo di iscrizione self-service impiegato anche da altri servizi che usano la tecnologia basata su Microsoft Cloud per autenticare gli utenti.

Questo è ciò che avviene in background quando un utente effettua l'iscrizione a RMS per utenti singoli e la sua organizzazione non dispone di un abbonamento a Office 365 o di una sottoscrizione di Azure e quindi non dispone di una directory in Azure per autenticare gli utenti:

1.  Quando il primo utente di un'organizzazione richiede una sottoscrizione di RMS per utenti singoli, il nome di dominio specificato nell'indirizzo di posta elettronica viene controllato per verificare se è già associato a un tenant Azure. Se non è presente alcun tenant esistente, viene creato automaticamente un nuovo tenant e una directory di Azure per l'organizzazione, che contiene un account per il primo utente. A differenza di una sottoscrizione di Azure a pagamento, questo primo account non è un amministratore globale, ma un utente standard. Il nuovo account usa l'indirizzo di posta elettronica e la password che l'utente ha specificato.

    > [!NOTE]
    > Alcuni nomi di dominio non possono essere usati per creare la directory e quindi neanche per RMS per utenti singoli.

    Se viene trovato un tenant esistente, viene controllato per sapere se dispone già di una sottoscrizione per Azure RMS. Quando non viene trovata alcuna sottoscrizione, è possibile aggiungere la sottoscrizione gratuita a RMS per utenti singoli.

2.  L'organizzazione riceve gratuitamente la sottoscrizione di RMS per utenti singoli. Ora, questo utente può essere autenticato da Azure e può proteggere i file e leggere i file protetti da altri utenti tramite Azure Rights Management. Per proteggere i file e leggere i file protetti, l'utente deve avere un'applicazione abilitata per RMS, come il [client Azure Information Protection](../rms-client/aip-client.md) gratuito.

3.  Quando un secondo utente della stessa organizzazione richiede una sottoscrizione di RMS per utenti singoli, viene aggiunto un nuovo account utente alla directory di Azure creata in precedenza, usando la sottoscrizione di RMS per utenti singoli dell'organizzazione. Questo secondo utente può eseguire tutte le operazioni che può eseguire il primo (proteggere file e leggere file protetti), ma i due utenti possono ora collaborare più facilmente in modo sicuro perché sono in grado di applicare rapidamente modelli predefiniti ai file per limitare l'accesso agli account presenti nella directory di Azure dell'organizzazione.

4.  Gli utenti della stessa organizzazione che successivamente richiedono la sottoscrizione seguono lo stesso schema, ovvero l'aggiunta di account utente (quando nuovi utenti eseguono l'iscrizione) alla directory di Azure dell'organizzazione. Maggiore è il numero di account aggiunto alla directory, maggiore è il numero di utenti che possono collaborare in modo sicuro con colleghi e partner e in grado di impedire con semplicità a persone non autorizzate di leggere i file qualora non dispongano dell'accesso ai file stessi.

Questo processo non prevede costi aggiuntivi per l'organizzazione né attività da parte dei membri del reparto IT, sebbene questi ultimi possano scegliere di effettuare una delle operazioni seguenti:

-   **Gestire gli account e il processo di iscrizione**: gli amministratori IT possono diventare proprietari della directory e degli account creati automaticamente in Azure. e quindi gestire gli account implementando le soluzioni di integrazione delle directory, ad esempio la sincronizzazione delle password e l'accesso Single Sign-On. In alternativa, possono impedire agli utenti di creare account o i iscriversi a RMS per utenti singoli.

    Per altre informazioni, vedere [Modalità di controllo da parte degli amministratori degli account creati per RMS per utenti singoli](rms-for-individuals-take-control.md).

-   **Gestire Rights Management**: gli amministratori IT possono convertire la sottoscrizione di RMS per utenti singoli per l'organizzazione in una sottoscrizione a pagamento che include Azure Rights Management. In questo caso, la directory e gli account Azure esistenti vengono mantenuti per consentire una semplice transizione agli utenti esistenti che usavano RMS per utenti singoli. Tutti i file protetti in precedenza dagli utenti rimarranno protetti in base agli stessi criteri e le persone cui era stato concesso di usare i file saranno ancora in grado di usarli nello stesso modo.

    Quando si sceglie questo tipo di comportamento, l'organizzazione è in grado di integrare Rights Management nei propri flussi di lavoro, servizi e archivi dati. In questo scenario è inoltre possibile gestire Rights Management perché si dispone del controllo sulla chiave del tenant dell'organizzazione per Azure Rights Management. A questo punto è possibile eseguire le operazioni seguenti:

    -   Configurare Exchange e SharePoint per supportare Azure Rights Management, anche se le due applicazioni sono eseguite in locale. Exchange e SharePoint sono supportate in modalità nativa per i servizi online e tramite un connettore per i server locali. Per altre informazioni, vedere i seguenti articoli:

        -   Le sezioni relative a Exchange Online e SharePoint Online in [Office 365: configurazione di client e servizi online](../deploy-use/configure-office365.md)

        -   [Distribuzione del connettore di Azure Rights Management](../deploy-use/deploy-rms-connector.md)

    -   Eseguire procedure di e-discovery sui dati di proprietà dell'azienda in modo che sia possibile, se richiesto, di decrittografare i file protetti tramite Rights Management. Per altre informazioni, vedere la pagina relativa alla [configurazione degli utenti con privilegi avanzati per Azure Rights Management e servizi di individuazione o ripristino dei dati](../deploy-use/configure-super-users.md).

    -   Registrare tutte le attività correlate all'uso di Rights Management nell'organizzazione. Questa operazione è estremamente utile perché consente non solo di monitorare i file protetti e gli utenti che vi hanno effettuato l'accesso, ma anche di identificare potenziali comportamenti sospetti di utenti non autorizzati che tentano di accedere a tali file. Per altre informazioni, vedere [Registrazione e analisi dell'utilizzo del servizio Azure Rights Management](../deploy-use/log-analyze-usage.md).

    -   Fornire agli utenti la possibilità di rilevare e revocare i documenti protetti, se queste funzionalità sono supportate dalla [sottoscrizione Azure RMS](https://technet.microsoft.com/dn858608). Per altre informazioni, vedere [Tenere traccia dei documenti e revocarli](../rms-client/sharing-app-track-revoke.md) nella [Guida dell'utente dell'applicazione RMS sharing](../rms-client/sharing-app-user-guide.md).

    -   Implementare una soluzione BYOK in modo da generare la chiave del tenant per Azure Rights Management in locale in base ai propri criteri IT e trasferirla in modo sicuro a Microsoft tramite un modulo di protezione hardware. Per altre informazioni, vedere [Pianificazione e implementazione della chiave del tenant di Azure Information Protection](../plan-design/plan-implement-tenant-key.md).


## <a name="next-steps"></a>Passaggi successivi
Vedere [Modalità di controllo da parte degli amministratori degli account creati per RMS per utenti singoli](rms-for-individuals-take-control.md).

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
