---
title: Esercitazione per l'avvio rapido - Passaggio 2 - AIP
description: "Passaggio 2 di un'esercitazione introduttiva per provare rapidamente a usare Azure Information Protection: configurare i criteri."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 07/21/2018
ms.topic: article
ms.service: information-protection
ms.assetid: 3bc193c2-0be0-4c8e-8910-5d2cee5b14f7
ms.openlocfilehash: daf2f9054576e5c1584b694b2358966b18e22fda
ms.sourcegitcommit: 7ba9850e5bb07b14741bb90ebbe98f1ebe057b10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/23/2018
ms.locfileid: "42808018"
---
# <a name="step-2-configure-the-azure-information-protection-policy"></a>Passaggio 2: Configurare i criteri di Azure Information Protection

>*Si applica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*

Il criterio predefinito disponibile con Azure è utilizzabile senza alcuna operazione di configurazione. Tuttavia si esaminerà questo criterio e vi si apporterà qualche modifica.

1. Continuando dal [passaggio 1](infoprotect-tutorial-step1.md) e sempre nel portale di Azure selezionare **CLASSIFICAZIONI** > **Criteri** > **Globale**Criteri globali per aprire il pannello **Criteri: Globale**. Questo pannello mostra i criteri predefiniti di Azure Information Protection creati per il tenant.

2. Dedicare alcuni minuti ad acquisire familiarità con le etichette visualizzate:
    
    - Etichette per la classificazione: **Personal**, **Public**, **General**, **Confidential** (Riservato) e **Highly Confidential** (Riservatezza elevata). Le ultime due etichette si espandono per visualizzare le etichette secondarie, offrendo esempi di come una classificazione può avere sottocategorie:
    
       > [!NOTE]
       > I criteri predefiniti potrebbero essere leggermente diversi da quelli illustrati in questa esercitazione. Ad esempio, si ha un'etichetta denominata **Internal** anziché **General**, e **Secret** anziché **Highly Confidential** (Riservatezza elevata). Forse non sono disponibili le etichette denominate **Recipients Only** (Solo destinatari) o non è disponibile alcuna etichetta. Queste modifiche avvengono perché esistono diverse versioni del criterio predefinito, a seconda di quando è stato creato per il tenant. Oppure è possibile che tali modifiche siano state apportate manualmente prima di iniziare l'esercitazione.
       > 
       > Se i criteri predefiniti hanno un aspetto diverso, è comunque possibile eseguire l'esercitazione, ma è necessario tenere presente queste modifiche quando si leggono le istruzioni e si fa riferimento alle immagini incluse di seguito. Se si vogliono modificare i criteri predefiniti in modo che corrispondano ai criteri predefiniti correnti, vedere [Criteri predefiniti di Azure Information Protection](configure-policy-default.md).
    
    - Con la configurazione predefinita, alcune etichette non hanno contrassegni visivi configurati. I contrassegni visivi sono il piè di pagina, l'intestazione e la filigrana. In base ai criteri predefiniti, per alcune etichette può essere impostata una protezione. Ad esempio: 
    
    ![Esercitazione introduttiva di Azure Information Protection, passaggio 3: Criterio predefinito](./media/info-protect-policy-default-labelsv2.png)
    
3. Dopo le etichette, nella sezione **Configure settings to display and apply on Information Protection end users** (Configurare le impostazioni da visualizzare e applicare per gli utenti finali di Information Protection) vengono visualizzate anche alcune impostazioni dei criteri. Ad esempio non è presente un'etichetta predefinita (non tutti i documenti e i messaggi di posta elettronica devono avere un'etichetta) e gli utenti non devono dare una giustificazione quando modificano le etichette:
    
    ![Esercitazione introduttiva di Azure Information Protection, passaggio 3: Criterio predefinito](./media/info-protect-policy-default-settings.png)

## <a name="changing-the-settings-for-a-default-label-and-prompt-for-justification"></a>Modifica delle impostazioni per un'etichetta predefinita e per la richiesta di giustificazione

Nel corso di questa esercitazione verranno modificate alcune impostazioni dei criteri per poterne osservare il funzionamento:

1. Selezionare **General** per **Selezionare l'etichetta predefinita**. 

    Se non si ha questa etichetta perché si sta usando una versione precedente dei criteri, scegliere **Internal** come etichetta equivalente.

2. Impostare l'opzione **Gli utenti devono fornire una giustificazione per la configurazione di un'etichetta di classificazione più bassa, la rimozione di un'etichetta o la rimozione della protezione** su **On**.

3. Individuare anche l'impostazione **Make the custom permissions option available to users** (Rendi l'opzione delle autorizzazioni personalizzate disponibile per gli utenti). Se questa impostazione è **Off** impostarla su **On**.
    
    È possibile che non sia necessario modificare questa impostazione poiché il valore predefinito dipende dalla propria sottoscrizione. Le autorizzazioni personalizzate verranno usate in seguito nell'esercitazione per condividere un documento protetto con l'utente specificato quando si fa clic con il pulsante destro del mouse sul file in Esplora file.

4. Selezionare **Salva** nel pannello **Criteri: Globale** e, se viene richiesto di confermare l'operazione, selezionare **OK**. Chiudere il pannello.

## <a name="creating-a-new-label-for-protection-visual-markers-and-a-condition-to-prompt-for-classification"></a>Creazione di una nuova etichetta per la protezione, di contrassegni visivi e di una condizione per la richiesta di classificazione

Ora verrà creata una nuova etichetta secondaria per **Confidential** (Riservato).

1. Dall'opzione di menu **CLASSIFICAZIONI** > **Etichette**: fare clic con il pulsante destro del mouse sull'etichetta **Confidential** (Riservato), quindi selezionare **Aggiungi un'etichetta secondaria**.
    
    Se non esiste un'etichetta denominata **Confidential**, è possibile selezionare un'altra etichetta o crearne una nuova e procedere con l'esercitazione con piccole differenze.

2. Nel pannello **Etichetta secondaria** specificare il nome dell'etichetta di **Finance** (Contabilità) e aggiungere la descrizione seguente: **Dati riservati che contengono informazioni di contabilità destinate solo ai dipendenti**.
    
    Il testo descrive come si intende usare l'etichetta selezionata ed è visibile agli utenti come descrizione comando, per aiutarli a decidere quale etichetta selezionare.

3. Per **Configurare le autorizzazioni per documenti e messaggi di posta elettronica contenenti questa etichetta** selezionare **Proteggi**, quindi selezionare **Protezione**:
    
    ![Configurare la protezione per un'etichetta di Azure Information Protection](./media/info-protect-protection-bar-configured.png) 
    
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
    
    a. **Scegliere il tipo di condizione**: mantenere il valore predefinito di **Tipi di informazioni**.
    
    b. Nella casella di ricerca **Selezionare i tipi di informazioni** digitare **numero di carta di credito**. Selezionare quindi **Numero carta di credito** nei risultati della ricerca.
    
    c. **Numero minimo di occorrenze**: mantenere il valore predefinito **1**.
    
    d. **Conta solo le occorrenze con valori univoci**: mantenere il valore predefinito **Off**.
    
    ![Esercitazione introduttiva di Azure Information Protection, passaggio 3: Configurare la condizione della carta di credito](./media/step2-configure-condition.png)
    
    Fare clic su **Salva** per tornare al pannello **Etichetta secondaria**.

10. Nel pannello **Etichetta secondaria** si può osservare che **Numero carta di credito** è visualizzato come **nome della condizione** con **1** **occorrenza**:
    
    ![Esercitazione introduttiva di Azure Information Protection, passaggio 3: Configurare la condizione della carta di credito](./media/step2-see-condition.png)

11. Per **Specificare se l'etichetta viene applicata automaticamente o se viene consigliata all'utente** mantenere l'impostazione predefinita **Consigliata** e non modificare il suggerimento per i criteri predefiniti. 

12. Nella casella **Enter notes for internal housekeeping** (Note per la gestione interna) digitare **For testing purposes only** (Solo a scopo di test).

13. Fare clic su **Salva** nel pannello **Etichetta secondaria**. Se viene richiesto di confermare, fare clic su **OK**. La nuova etichetta viene creata e salvata, ma non viene ancora aggiunta a un criterio.

14. Dall'opzione di menu **CLASSIFICAZIONI** > **Criteri**: selezionare di nuovo **Globale** e quindi selezionare il collegamento **Aggiungi o rimuovi etichette** dopo le etichette.

15. Nel pannello **Criteri: Aggiungi o rimuovi etichette** selezionare l'etichetta appena creata, l'etichetta secondaria denominata **Finance** (Contabilità), quindi fare clic su **OK**.

16. Nel pannello **Criteri: Globale** è ora possibile vedere la nuova etichetta secondaria nei criteri globali, configurata per i contrassegni visivi e la protezione. Ad esempio:

    ![Esercitazione introduttiva di Azure Information Protection, passaggio 3: Configurazione del criterio predefinito](./media/info-protect-policy-configuredv2.png)
    
    Si vedrà anche che le impostazioni sono configurate con le modifiche per l'etichetta predefinita e la giustificazione:
    
    ![Esercitazione introduttiva di Azure Information Protection, passaggio 3: impostazioni configurate](./media/info-protect-settings-configuredv2.png)
    

17. Fare clic su **Salva** nel pannello **Criteri: Globale**. Se viene richiesto di confermare l'azione, fare clic su **OK**.

Al termine di questa esercitazione è possibile chiudere il portale di Azure o lasciarlo aperto per provare altre opzioni di configurazione.

Dopo aver esaminato il criterio predefinito e aver apportato alcune modifiche, il passaggio successivo prevede l'installazione del client di Azure Information Protection.

|Se si desiderano altre informazioni|Informazioni aggiuntive|
|--------------------------------|--------------------------|
|Informazioni sui criteri predefiniti e sulle diverse versioni|[Criteri predefiniti di Azure Information Protection](configure-policy-default.md)|
|Informazioni sulla configurazione dei criteri|[Configurazione dei criteri di Azure Information Protection](configure-policy.md)|
|Istruzioni dettagliate per la configurazione di un'etichetta per la protezione|[Come configurare un'etichetta per la protezione di Rights Management](configure-policy-protection.md)|
|Informazioni dettagliate sulle autorizzazioni|[Configurazione dei diritti di utilizzo per Azure Rights Management](configure-usage-rights.md)|



>[!div class="step-by-step"]
[&#171; Passaggio 1](infoprotect-tutorial-step1.md)
[Passaggio 3 &#187;](infoprotect-tutorial-step3.md)
