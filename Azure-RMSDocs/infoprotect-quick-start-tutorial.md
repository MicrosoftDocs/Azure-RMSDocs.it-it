---
title: Esercitazione - Modificare i criteri di Azure Information Protection e creare una nuova etichetta - AIP
description: Esercitazione introduttiva per la modifica dei criteri di Azure Information Protection per l'organizzazione. Il completamento dell'esercitazione richiede circa 15 minuti.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 02/29/2019
ms.topic: tutorial
ms.collection: M365-security-compliance
ms.service: information-protection
ms.openlocfilehash: 5a9c1ebae0678125c19fd35ce4c5275aa056ce45
ms.sourcegitcommit: d716d3345a6a5adc63814dee28f7c01b55b96770
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/14/2019
ms.locfileid: "57829026"
---
# <a name="tutorial-edit-the-azure-information-protection-policy-and-create-a-new-label"></a>Esercitazione: Modificare i criteri di Azure Information Protection e creare una nuova etichetta

>*Si applica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*

In questa esercitazione si apprenderà come:
> [!div class="checklist"]
> * Configurare le impostazioni dei criteri
> * Creare una nuova etichetta 
> * Configurare l'etichetta per contrassegni visivi, classificazione consigliata e protezione
> * Vedere le impostazioni e le etichette in azione

Come conseguenza di questa configurazione, gli utenti vedranno che viene applicata un'etichetta predefinita quando si crea un nuovo documento o messaggio di posta elettronica. Tuttavia, verrà chiesto loro di applicare la nuova etichetta quando vengono rilevate informazioni sulla carta di credito. Quando si applica la nuova etichetta, il contenuto viene riclassificato e protetto, con un piè di pagina e una filigrana corrispondenti. 

È possibile completare questa esercitazione in circa 15 minuti.

## <a name="prerequisites"></a>Prerequisiti 

Per completare questa esercitazione, è necessario:

1. Disporre di una sottoscrizione che includa un piano 2 di Azure Information Protection.
    
    In assenza di una sottoscrizione con un piano 2 di Azure Information Protection, è possibile creare un account [gratuito](https://admin.microsoft.com/Signup/Signup.aspx?OfferId=87dd2714-d452-48a0-a809-d2f58c4f68b7) per l'organizzazione.

2. Aver aggiunto il pannello di Azure Information Protection nel portale di Azure e aver verificato che il servizio di protezione è attivato.

    Se occorre assistenza per queste azioni, vedere [Avvio rapido: Introduzione ad Azure Information Protection nel portale di Azure](quickstart-viewpolicy.md)

3. Aver installato il client Azure Information Protection nel computer in uso. 
    
    Per installare il client, andare all'[Area download Microsoft](https://www.microsoft.com/en-us/download/details.aspx?id=53018) e scaricare **AzInfoProtection.exe** dalla pagina di Azure Information Protection.

4. Disporre di un computer con Windows (versione minima Windows 7 con Service Pack 1), in cui è stato eseguito l'accesso alle app di Office da una delle categorie seguenti:
    
    - App di Office con versione minima 1805, build 9330.2078 da Office 365 Business o Microsoft 365 Business quando all'utente viene assegnata una licenza per Azure Rights Management (nota anche come Azure Information Protection per Office 365).
    
    - Office 365 ProPlus.
    
    - Office Professional Plus 2019.
    
    - Office Professional Plus 2016.
    
    - Office Professional Plus 2013 con Service Pack 1.
    
    - Office Professional Plus 2010 con Service Pack 2.

Per un elenco completo dei prerequisiti per l'uso di Azure Information Protection, vedere [Requisiti per Azure Information Protection](requirements.md).

A questo punto, procedere con l'esercitazione.

## <a name="edit-the-azure-information-protection-policy"></a>Modificare i criteri di Azure Information Protection

Tramite il portale di Azure, si procederà per prima cosa alla modifica di alcune impostazioni dei criteri e quindi si creerà una nuova etichetta.

### <a name="edit-the-policy-settings"></a>Modificare le impostazioni dei criteri

1. Aprire una nuova finestra del browser e accedere al [portale di Azure](https://portal.azure.com) come amministratore globale. Passare quindi ad **Azure Information Protection**. 
    
    Ad esempio, dal menu hub fare clic su **Tutti i servizi** e iniziare a digitare **Informazioni** nella casella Filtro. Selezionare **Azure Information Protection**.
    
    Se non si è l'amministratore globale, usare il collegamento seguente per i ruoli alternativi: [Accesso al portale di Azure](configure-policy.md#signing-in-to-the-azure-portal)

2. Selezionare **Classificazioni** > **Criteri** > **Globale** per aprire il pannello **Criteri: Globale**. 

3. Individuare le impostazioni dei criteri dopo le etichette nella sezione **Configure settings to display and apply on Information Protection end users** (Configurare le impostazioni da visualizzare e applicare per gli utenti finali di Information Protection). 
    
    Prendere nota dell'attuale configurazione delle impostazioni, in particolare delle opzioni **Selezionare l'etichetta predefinita** e **Gli utenti devono fornire una giustificazione per impostare un'etichetta di classificazione inferiore, rimuovere un'etichetta o rimuovere la protezione**. Ad esempio:
    
    ![Esercitazione di Azure Information Protection - Impostazioni dei criteri da modificare](./media/info-protect-policy-default-settings.png)
    
    Queste impostazioni dei criteri verranno usate più avanti nell'esercitazione quando si vedranno in azione.

4. Selezionare **General** per **Selezionare l'etichetta predefinita**. 

    Se non si ha questa etichetta perché si sta usando una versione precedente dei criteri, scegliere **Internal** come etichetta equivalente.

5. Impostare l'opzione **Gli utenti devono fornire una giustificazione per impostare un'etichetta di classificazione inferiore, rimuovere un'etichetta o rimuovere la protezione** su **Sì**, se non lo è già.

6. Assicurarsi inoltre che **Visualizza la barra di Information Protection nelle app Office** sia impostata su **Sì**.

7. Selezionare **Salva** nel pannello **Criteri: Globale** e, se viene richiesto di confermare l'operazione, scegliere **OK**. Chiudere il pannello.

### <a name="create-a-new-label-for-protection-visual-markers-and-a-condition-to-prompt-for-classification"></a>Creare una nuova etichetta per la protezione, contrassegni visivi e una condizione per la richiesta di classificazione

Ora verrà creata una nuova etichetta secondaria per **Confidential** (Riservato).

1. Dall'opzione di menu **Classificazioni** > **Etichette**: Fare clic con il pulsante destro del mouse sull'etichetta **Confidential** e selezionare **Aggiungi un'etichetta secondaria**.
    
    Se non esiste un'etichetta denominata **Riservato**, è possibile selezionare un'altra etichetta o crearne una nuova e procedere con l'esercitazione con piccole differenze.

2. Nel pannello **Etichetta secondaria** specificare il nome dell'etichetta di **Finance** (Contabilità) e aggiungere la descrizione seguente: **Dati riservati che contengono informazioni di contabilità destinate solo ai dipendenti**.
    
    Il testo descrive come si intende usare l'etichetta selezionata ed è visibile agli utenti come descrizione comando, per aiutarli a decidere quale etichetta selezionare.

3. Per **Configurare le autorizzazioni per documenti e messaggi di posta elettronica contenenti questa etichetta**, selezionare **Proteggi**, che apre automaticamente il pannello **Protezione** selezionando l'opzione **Protezione**:
    
    ![Configurazione di un'etichetta di Azure Information Protection per la protezione](./media/info-protect-protection-bar-configured.png) 
    
4. Nel pannello **Protezione** verificare che sia selezionata l'opzione **Azure (cloud key)** (Azure - Chiave cloud). Questa opzione usa il servizio Azure Rights Management per proteggere documenti e messaggi di posta elettronica. Assicurarsi anche che l'opzione **Imposta autorizzazioni** sia selezionata. Selezionare quindi **Aggiungi autorizzazioni**.

5. Nel pannello **Aggiungi autorizzazioni** selezionare **Aggiungi \<nome organizzazione >- Tutti i membri**. Se ad esempio il nome dell'organizzazione è VanArsdel Ltd, viene visualizzata la seguente opzione da selezionare:
    
    ![Concessione delle autorizzazioni di protezione a tutti i membri per un'etichetta di Azure Information Protection](./media/info-protect-protection-all-members.png) 
    
    Questa opzione seleziona automaticamente tutti gli utenti dell'organizzazione a cui si possono concedere le autorizzazioni. Tuttavia, altre opzioni consentono di esplorare e cercare utenti o gruppi del tenant. Se invece si seleziona l'opzione **Immettere i dettagli**, è possibile specificare singoli indirizzi di posta elettronica o anche tutti gli utenti di un'altra organizzazione.

6. Per le autorizzazioni, selezionare **Revisore** dalle opzioni predefinite. Come si può notare, questo livello di autorizzazione concede automaticamente alcune delle autorizzazioni elencate ma non tutte:
    
    ![Concessione delle autorizzazioni di protezione al coautore per un'etichetta di Azure Information Protection](./media/info-protect-protection-reviewer.png)
    
    È possibile selezionare diversi livelli di autorizzazione o specificare singoli diritti di utilizzo usando l'opzione **Personalizzato**. Ma per questa esercitazione mantenere l'opzione **Revisore**. È possibile provare altre autorizzazioni in un secondo momento e vedere come limitano le operazioni che gli utenti specificati possono eseguire con il documento o il messaggio di posta elettronica protetto.

7. Fare clic su **OK** per chiudere il pannello **Aggiungi autorizzazioni** e vedere in che modo viene aggiornato il pannello **Protezione** per riflettere la configurazione. Ad esempio:
    
     ![Pannello Protezione con configurazione delle autorizzazioni per un'etichetta di Azure Information Protection](./media/info-protect-protection-configured.png)
    
    Se si seleziona **Aggiungi autorizzazioni**, viene di nuovo visualizzato il pannello **Aggiungi autorizzazioni**, in modo tale che sia possibile aggiungere altri utenti e concedere loro autorizzazioni diverse. Ad esempio, concedere l'accesso a un gruppo specifico solo per la visualizzazione. Ma per questa esercitazione viene usato un solo set di autorizzazioni per tutti gli utenti.

8. Rivedere e mantenere i valori predefiniti per la scadenza del contenuto e l'accesso offline, quindi fare clic su **OK** per salvare e chiudere il pannello **Protezione**.

8. Tornare al pannello **Etichetta secondaria** e individuare la sezione **Configurare il contrassegno visivo**:
    
    Per l'impostazione **I documenti con questa etichetta includono un piè di pagina** fare clic su **On** e quindi digitare **Classificato come Riservato** nella casella **Testo**. 
    
    Per l'opzione **I documenti con questa etichetta includono un'intestazione** fare clic su **On** e quindi, nella casella **Testo della filigrana**, digitare il nome dell'organizzazione. Ad esempio, **VanArsdel, Ltd** 
    
    Anche se è possibile modificare l'aspetto di questi contrassegni visivi, per il momento verranno mantenute le impostazioni predefinite.
    
9. Individuare la sezione **Configurare le condizioni per l'applicazione automatica di questa etichetta**:
    
    Fare clic su **Aggiungi una nuova condizione** e quindi nel pannello **Condizione** selezionare quanto segue:
    
    a. **Scegliere il tipo di condizione**: mantenere l'impostazione predefinita **Tipi di informazioni**.
    
    b. Per **Scegliere un settore**: mantenere l'impostazione predefinita **Tutti**.
    
    c. Nella casella di ricerca **Selezionare i tipi di informazioni** digitare **numero di carta di credito**. Selezionare quindi **Numero carta di credito** nei risultati della ricerca.
    
    d. **Numero minimo di occorrenze**: mantenere l'impostazione predefinita **1**.
    
    e. **Conta solo le occorrenze con valori univoci**: mantenere l'impostazione predefinita **No**.
    
    ![Esercitazione di Azure Information Protection - Configurare la condizione della carta di credito](./media/step2-configure-condition.png)
    
    Fare clic su **Salva** per tornare al pannello **Etichetta secondaria**.

10. Nel pannello **Etichetta secondaria** si può osservare che **Numero carta di credito** è visualizzato come **nome della condizione** con **1** **occorrenza**:
    
    ![Esercitazione di Azure Information Protection - Configurare la condizione della carta di credito](./media/step2-see-condition.png)

11. Per **Specificare se l'etichetta viene applicata automaticamente o se viene consigliata all'utente**: mantenere il valore predefinito **Consigliata** e non modificare il suggerimento di criterio predefinito. 

12. Nella casella **Aggiungi note per l'uso da parte dell'amministratore** specificare che è **solo a scopo di test**.

13. Fare clic su **Salva** nel pannello **Etichetta secondaria**. Se viene richiesto di confermare l'operazione, fare clic su **OK**. La nuova etichetta viene creata e salvata, ma non viene ancora aggiunta a un criterio.

14. Dall'opzione di menu **Classificazioni** > **Criteri**: selezionare di nuovo **Globale** e quindi selezionare il collegamento **Aggiungi o rimuovi etichette** dopo le etichette.

15. Nel pannello **Policy: Aggiungi o rimuovi etichette** selezionare l'etichetta appena creata e l'etichetta secondaria denominata **Finance** (Contabilità), quindi fare clic su **OK**.

16. Nel pannello **Criteri: Globale** è ora possibile vedere la nuova etichetta secondaria nei criteri globali, configurata per i contrassegni visivi e la protezione. Ad esempio:

    ![Esercitazione di Azure Information Protection - Nuova etichetta secondaria](./media/info-protect-policy-configuredv2.png)
    
    Si vedrà anche che sono configurate le impostazioni per l'etichetta predefinita e la giustificazione:
    
    ![Esercitazione di Azure Information Protection - Impostazioni configurate](./media/info-protect-settings-configuredv2.png)
    

17. Fare clic su **Salva** nel pannello **Criteri: Globale**. Se viene richiesto di confermare l'azione, fare clic su **OK**.

Al termine di questa esercitazione è possibile chiudere il portale di Azure o lasciarlo aperto per provare altre opzioni di configurazione.

È il momento di sperimentare i risultati delle modifiche.

## <a name="see-classification-labeling-and-protection-in-action"></a>Vedere la classificazione, l'aggiunta di etichette e la protezione in azione 

Le modifiche apportate ai criteri e la nuova etichetta creata si applicano a Word, Excel, PowerPoint e Outlook. Per questa esercitazione, si userà Word per vederle in azione. 

Aprire un nuovo documento in Word. Dal momento che è installato il client Azure Information Protection, verrà visualizzato quanto segue:

![Esercitazione di Azure Information Protection - Client installato](./media/word2016-calloutsv2.png)

- Nella scheda **Home** un gruppo **Protezione** con un pulsante denominato **Proteggi**.
    
    Fare clic su **Proteggi** > **Guida e commenti e suggerimenti** e nella finestra di dialogo **Microsoft Azure Information Protection** verificare lo stato del client. Dovrebbe venire visualizzata l'indicazione **Connesso come** seguita dal nome dell'utente. Dovrebbe inoltre essere visualizzata un'indicazione di data e ora per l'ultima connessione e per il download dei criteri di Information Protection. Verificare che il nome utente visualizzato sia corretto per il tenant.

- La nuova barra di Information Protection sotto la barra multifunzione. Visualizza il titolo **Sensibilità** e le etichette illustrate nel portale di Azure.

### <a name="to-manually-change-our-default-label"></a>Per modificare manualmente l'etichetta predefinita

1. Sulla barra di Information Protection selezionare l'ultima etichetta e osservare come vengono visualizzate le etichette secondarie:
    
    ![Esercitazione di Azure Information Protection - Visualizzazione delle etichette secondarie](./media/info-protect-sub-labelsv2.png)

2. Selezionare una delle etichette secondarie e osservare come le altre etichette non vengono più visualizzate sulla barra ora che si è selezionata un'etichetta per il documento. Il valore **Sensitivity** (Riservatezza) cambia per visualizzare il nome dell'etichetta principale e secondaria con una corrispondente variazione del colore dell'etichetta. Ad esempio:
    
    ![Esercitazione di Azure Information Protection - Etichetta secondaria selezionata](./media/info-protect-sub-label-selectedv2.png)

3. Sulla barra di Information Protection fare clic sull'icona **Edit Label** (Modifica l'etichetta) che si trova accanto al valore dell'etichetta selezionata:
    
    ![Esercitazione di Azure Information Protection - Icona Modifica l'etichetta](./media/info-protect-edit-label-selectedv2.png)
    
    Questa azione visualizza nuovamente le etichette disponibili.

4. Selezionare la prima etichetta, **Personal**. Poiché è stata selezionata un'etichetta classificata a un livello inferiore rispetto a quella selezionata in precedenza per questo documento, viene chiesto di giustificare il motivo per cui si sta abbassando il livello di classificazione:
    
    ![Esercitazione di Azure Information Protection - Richiesta di giustificazione dell'abbassamento](./media/info-protect-lower-justification.png)
    
    Selezionare **L'etichetta precedente non è più applicabile** e fare clic su **Conferma**. Il valore **Sensitivity** (Riservatezza) diventa **Personale** e le altre etichette vengono nuovamente nascoste.

### <a name="to-remove-the-classification-completely"></a>Per rimuovere completamente la classificazione

1. Sulla barra di Information Protection, fare nuovamente clic sull'icona **Modifica l'etichetta**. Tuttavia, anziché scegliere una delle etichette, fare clic sull'icona **Elimina l'etichetta**:
    
    ![Esercitazione di Azure Information Protection - Icona Elimina l'etichetta](./media/delete-icon-from-personalv2.png)
    
2. Questa volta, quando richiesto, digitare "Il documento non richiede la classificazione" e fare clic su **Conferma**.  
    
    Per il valore **Riservatezza** viene visualizzato **Non impostato**, come avviene inizialmente per i nuovi documenti se non si imposta un'etichetta predefinita come impostazione dei criteri.

### <a name="to-see-a-recommendation-prompt-for-labeling-and-automatic-protection"></a>Per visualizzare un messaggio di azione consigliata per l'assegnazione di etichette e la protezione automatica

1. Nel documento di Word, digitare un numero di carta di credito valido, ad esempio: **4242-4242-4242-4242**. 

2. Salvare il documento in locale con qualsiasi nome file. 

3. Viene visualizzata ora un prompt per applicare l'etichetta configurata per la protezione quando vengono rilevati numeri di carta di credito. Se non si è d'accordo con il suggerimento, l'impostazione dei criteri consente di rifiutarlo, selezionando **Dismiss** (Ignora). La disponibilità di un suggerimento con la possibilità di ignorarlo consente agli utenti di ridurre i falsi positivi quando si usa una classificazione automatica. Per questa esercitazione, fare clic su **Change now** (Modifica ora).

    ![Esercitazione di Azure Information Protection - Messaggio di azione consigliata](./media/change-nowv2.png)

    Oltre al documento che indica ora che l'etichetta configurata è applicata, ad esempio **Confidential\Finance** (Riservato\Contabilità), verrà immediatamente visualizzata la filigrana del nome dell'organizzazione sulla pagina e viene anche applicato il piè di pagina **Classificato come Riservato**. 

    Il documento è protetto anche con le autorizzazioni specificate per questa etichetta. È possibile verificare se il documento è protetto facendo clic sulla scheda **File** e visualizzare le informazioni per **Proteggi documento**. Il documento risulta protetto da **Confidential\Finance** (Riservato\Contabilità) e la descrizione dell'etichetta. 
    
    A causa della configurazione di protezione dell'etichetta, solo i dipendenti possono aprire il documento e alcune azioni sono limitate. Ad esempio, poiché non sono autorizzati a stampare, copiare ed estrarre il contenuto, non possono stampare il documento o eseguirne una copia. Tali restrizioni consentono di evitare la perdita di dati. Il proprietario del documento può stamparlo e copiarne il contenuto. Tuttavia, se si invia il documento via posta elettronica a un altro utente dell'organizzazione, quest'ultimo non potrà eseguire queste operazioni.

4. È ora possibile chiudere il documento.

## <a name="clean-up-resources"></a>Pulizia delle risorse

Se non si vogliono mantenere le modifiche apportate in questa esercitazione, seguire questa procedura:

1. Selezionare **Classificazioni** > **Criteri** > **Globale** per aprire il pannello **Criteri: Globale**.

2. Ripristinare i valori originali precedentemente annotati per le impostazioni dei criteri e quindi selezionare **Salva**. 

3. Dall'opzione di menu **Classificazioni** > **Etichetta**: nel pannello **Azure Information Protection - Etichetta** selezionare il menu di scelta rapida (**...**) per l'etichetta **Finance** (Contabilità) creata.

4. Selezionare **Elimina questa etichetta** e, se viene richiesto di confermare l'operazione, scegliere **OK**.

Riavviare Word per scaricare queste modifiche.

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sulla modifica dei criteri di Azure Information Protection, vedere [Configurazione dei criteri di Azure Information Protection](configure-policy.md).

Per altre informazioni su dove viene registrata l'attività di assegnazione delle etichette, vedere [Registrazione dell'utilizzo per il client Azure Information Protection](./rms-client/client-admin-guide-files-and-logging.md#usage-logging-for-the-azure-information-protection-client).

