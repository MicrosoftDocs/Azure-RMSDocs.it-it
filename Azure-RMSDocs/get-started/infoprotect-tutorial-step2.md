---
title: Esercitazione per l'avvio rapido - Passaggio 2 - AIP
description: 'Passaggio 2 di un''esercitazione introduttiva per provare rapidamente a usare Azure Information Protection: configurare i criteri.'
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 05/23/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 3bc193c2-0be0-4c8e-8910-5d2cee5b14f7
ms.openlocfilehash: b91bfea99170b747bb199b3c966ae8c89fae5359
ms.sourcegitcommit: 04eb4990e2bf0004684221592cb93df35e6acebe
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/30/2017
---
<a id="step-2-configure-and-publish-the-azure-information-protection-policy" class="xliff"></a>

# Passaggio 2: Configurare e pubblicare criteri di Azure Information Protection

>*Si applica a: Azure Information Protection*

Il criterio predefinito disponibile con Azure è utilizzabile senza alcuna operazione di configurazione. Tuttavia si esaminerà questo criterio e vi si apporterà qualche modifica.

1. In una nuova finestra del browser accedere al [portale di Azure](https://portal.azure.com) come amministratore globale o della sicurezza per il tenant.

2. Nel menu hub fare clic su **Nuovo** e quindi, nell'elenco **Marketplace**, selezionare **Sicurezza e identità**. Nel pannello**Sicurezza e identità**, nell'elenco **App in primo piano**, selezionare **Azure Information Protection**. Nel pannello **Azure Information Protection** fare clic su **Crea**.

    Questa operazione attiva il servizio per il tenant e crea il pannello **Azure Information Protection** in modo che al successivo accesso al portale sarà possibile selezionare il servizio dall'elenco **More services** (Altri servizi) dell'hub. 

    > [!TIP] 
    > Selezionare **Aggiungi al dashboard** per creare un riquadro **Azure Information Protection** nel dashboard, in modo da ignorare la ricerca del servizio al successivo accesso al portale.

3. Leggere le informazioni disponibili nella pagina **Avvio rapido** che si apre automaticamente quando ci si connette al servizio per la prima volta. È possibile tornare a questa pagina in un secondo momento. Per questa esercitazione, fare clic su **Criteri globali** per aprire il pannello **Criteri: globali**. Questo pannello, che si apre automaticamente per connessioni successive al servizio, visualizza i criteri predefiniti di Information Protection creati automaticamente per il tenant:
    
    - Etichette per la classificazione: **Personal**, **Public**, **General**, **Confidential** (Riservato) e **Highly Confidential** (Riservatezza elevata). Le ultime due etichette si espandono per visualizzare le etichette secondarie **Tutti i dipendenti** e **Chiunque (senza protezione)**, offrendo esempi di come una classificazione può avere sottocategorie.
    
       > [!NOTE]
       > I criteri predefiniti potrebbero essere leggermente diversi da quelli illustrati in questa esercitazione. Ad esempio, si ha un'etichetta denominata **Internal** anziché **General**, e **Secret** anziché **Highly Confidential** (Riservatezza elevata). In questo caso, è possibile che si stia usando una versione precedente dei criteri predefiniti. Oppure è possibile che tali modifiche siano state apportate manualmente prima di iniziare l'esercitazione.
       > 
       > Se i criteri predefiniti hanno un aspetto diverso, è comunque possibile eseguire l'esercitazione, ma è necessario tenere presente queste modifiche quando si leggono le istruzioni e si fa riferimento alle immagini incluse di seguito. Se si vogliono modificare i criteri predefiniti in modo che corrispondano ai criteri predefiniti correnti, vedere [Criteri predefiniti di Azure Information Protection](../deploy-use/configure-policy-default.md).

    - Con la configurazione predefinita, alcune etichette non hanno contrassegni visivi configurati, ad esempio piè di pagina, intestazione, filigrana, e per nessuna delle etichette è impostata la protezione: 
    
    ![Esercitazione introduttiva di Azure Information Protection, passaggio 3: Criterio predefinito](../media/info-protect-policy-default-labelsv2.png)
    
    Alcune impostazioni dei criteri non sono definite, ad esempio, tutti i documenti e i messaggi di posta elettronica non devono avere un'etichetta, non c'è un'etichetta predefinita e gli utenti non devono specificare una giustificazione quando modificano le etichette:
    
    ![Esercitazione introduttiva di Azure Information Protection, passaggio 3: Criterio predefinito](../media/info-protect-policy-default-settings.png)

<a id="changing-the-settings-for-a-default-label-and-prompt-for-justification" class="xliff"></a>

## Modifica delle impostazioni per un'etichetta predefinita e per la richiesta di giustificazione

Nel corso di questa esercitazione verranno modificate alcune impostazioni dei criteri per poterne osservare il funzionamento:

1. Impostare **Select the default label** (Selezionare l'etichetta predefinita) su **General**. 

    Se non si ha questa etichetta perché si sta usando una versione precedente dei criteri, scegliere **Internal** come etichetta equivalente.

2. Impostare **Gli utenti devono fornire una giustificazione per la configurazione di un'etichetta di classificazione più bassa, la rimozione di un'etichetta o la rimozione della protezione** su **On**.

<a id="configuring-a-label-for-protection-a-watermark-and-a-condition-to-prompt-for-classification" class="xliff"></a>

## Configurazione di un'etichetta per la protezione, di una filigrana e di una condizione per la richiesta di classificazione

Verranno modificate ora le impostazioni di una delle etichette secondarie, ovvero **All Employees** (Tutti i dipendenti) dall'etichetta principale **Confidential** (Riservato). 

Se l'etichetta **Confidential** (Riservato) non ha etichette secondarie perché si sta usando una versione precedente dei criteri, è possibile usare l'etichetta **Confidential** (Riservato) come alternativa. I passaggi di configurazione saranno gli stessi, ma il nome del pannello dell'etichetta sarà **Confidential** (Riservato) anziché **All Employees** (Tutti i dipendenti).

1. Assicurarsi che l'etichetta **Confidential** (Riservato) sia espansa e selezionare **All Employees** (Tutti i dipendenti) da tale etichetta.
    
    Nel nuovo pannello **Label: All Employees** (Etichetta: Tutti i dipendenti) sono ora visibili le impostazioni disponibili per ogni etichetta. 

2. Leggere il testo **Description** (Descrizione) per questa etichetta. Descrive come l'etichetta selezionata deve essere usata ed è visibile agli utenti come descrizione comando, per aiutarli a decidere quale etichetta selezionare.

3. Identificare la sezione **Set permissions for documents and emails containing this label** (Configurare le autorizzazioni per documenti e messaggi di posta elettronica contenenti questa etichetta) e selezionare **Protect** (Proteggi):
    
    ![Configurare la protezione per un'etichetta di Azure Information Protection](../media/info-protect-protection-barv2.png) 
    
    Per effetto di questa operazione viene aperto il pannello **Protezione**.
    
3. Nel pannello **Protezione** verificare che l'opzione **Azure RMS** sia selezionata, che sia possibile **selezionare un modello predefinito**, quindi fare clic sulla casella di riepilogo e selezionare il modello predefinito **\<nome dell'organizzazione> - Riservato**.     
    
    Ad esempio, se il nome dell'organizzazione è VanArsdel, Ltd, verrà visualizzata la voce **VanArsdel, Ltd - Confidential** e sarà possibile selezionarla: 
    
    ![Esercitazione introduttiva di Azure Information Protection, passaggio 3: Impostare la protezione di Azure RMS](../media/step2-select-rms-template.png)
    
    Se questo modello di Azure Rights Management è disabilitato, selezionare un modello alternativo. Tuttavia, se si seleziona un modello di reparto, assicurarsi che l'account sia incluso nell'ambito.
    
4. Fare clic su **OK** per salvare le modifiche e chiudere il pannello **Protection** (Protezione). È possibile vedere questa modifica di configurazione nel pannello **Label: All Employees** (Etichetta: Tutti i dipendenti):
    
    ![Esercitazione introduttiva di Azure Information Protection, passaggio 3: protezione configurata di Azure RMS](../media/protection-bar-configured.png)
    
5. Nel pannello **Label: All Employees** (Etichetta: Tutti i dipendenti), trovare la sezione **Set visual marking** (Configura il contrassegno visivo):
    
    Per l'opzione **I documenti con questa etichetta includono un'intestazione** fare clic su **On** e quindi, nella casella **Testo della filigrana**, digitare il nome dell'organizzazione. Ad esempio, **VanArsdel, Ltd**: 
    
    ![Esercitazione introduttiva di Azure Information Protection, passaggio 3: Impostare la protezione di Azure RMS](../media/step2-configure-watermark.png)
    
    Anche se è possibile modificare le dimensioni, il colore e il layout delle filigrane, per il momento verranno mantenute le impostazioni predefinite.
    
6. Individuare la sezione **Configurare le condizioni per l'applicazione automatica di questa etichetta**:
    
    Fare clic su **Add a new condition** (Aggiungi una nuova condizione) e quindi nel pannello **Condition** (Condizione) selezionare quanto segue:
    
    a. **Scegliere il tipo di condizione**: mantenere il valore **Predefinito**.
    
    b. **Seleziona predefinito**: dal menu a discesa selezionare **Numero carta di credito**.
    
    c. **Numero minimo di occorrenze**: mantenere il valore predefinito **1**.
    
    d. **Conta solo le occorrenze con valori univoci**: mantenere il valore predefinito **Off**.
    
    ![Esercitazione introduttiva di Azure Information Protection, passaggio 3: Configurare la condizione della carta di credito](../media/step2-configure-condition.png)
    
    Fare clic su **Save** (Salva) per tornare al pannello **Label: All Employees** (Etichetta: Tutti i dipendenti).

7. Nel pannello **Label: All Employees** (Etichetta: Tutti i dipendenti) si noterà che **Credit Card Number** (Numero della carta di credito) viene visualizzato come **CONDITION NAME** (Nome della condizione), con il valore **1** in **OCCURRENCES** (Occorrenze):
    
    ![Esercitazione introduttiva di Azure Information Protection, passaggio 3: Configurare la condizione della carta di credito](../media/step2-see-condition.png)

8. Per **Specificare se l'etichetta viene applicata automaticamente o se viene consigliata all'utente**: mantenere l'impostazione predefinita **Consigliata** e non modificare il suggerimento per i criteri predefiniti:
    
    ![Esercitazione introduttiva di Azure Information Protection, passaggio 3: Classificazione consigliata](../media/step2-keep-recommendedv2.png)

9. Nella casella **Immettere note per la manutenzione interna** digitare **For testing purposes only** (Solo a scopo di test):
    
    ![Esercitazione introduttiva di Azure Information Protection, passaggio 3: Digitare le note](../media/step2-type-notes.png)

10. Fare clic su **Save** (Salva) nel pannello **Label: All Employees** (Etichetta: Tutti i dipendenti). Quindi, nel pannello **Criteri: Globale** fare di nuovo clic su **Salva**.
    
    A questo punto, le etichette visualizzano la protezione di Azure RMS dell'etichetta appena configurata:

    ![Esercitazione introduttiva di Azure Information Protection, passaggio 3: Configurazione del criterio predefinito](../media/info-protect-policy-configuredv2.png)
    
    E le impostazioni sono configurate con le modifiche per l'etichetta predefinita e la giustificazione:
    
    ![Esercitazione introduttiva di Azure Information Protection, passaggio 3: impostazioni configurate](../media/info-protect-settings-configuredv2.png)
    
11. Ora che le modifiche sono state apportate e salvate, devono essere rese disponibili agli utenti. A tale scopo, nel pannello iniziale di **Azure Information Protection** fare clic su **Publish** (Pubblica) e su **Sì** per confermare.

    ![Esercitazione introduttiva di Azure Information Protection, passaggio 3: pubblicare i criteri configurati](../media/info-protect-publish.png)

Al termine di questa esercitazione è possibile chiudere il portale di Azure o lasciarlo aperto per provare altre opzioni di configurazione.

Dopo aver esaminato il criterio predefinito e aver apportato alcune modifiche, il passaggio successivo prevede l'installazione del client di Azure Information Protection.

|Se si desiderano altre informazioni|Informazioni aggiuntive|
|--------------------------------|--------------------------|
|Informazioni sulle opzioni di configurazione per i criteri|[Configurazione dei criteri di Azure Information Protection](../deploy-use/configure-policy.md)|


>[!div class="step-by-step"]
[&#171; Passaggio 1](infoprotect-tutorial-step1.md)
[Passaggio 3 &#187;](infoprotect-tutorial-step3.md)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]