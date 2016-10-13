---
title: Esercitazione introduttiva, passaggio 1 | Azure Information Protection
description: Passaggio 2 dell'esercitazione introduttiva che consente di provare rapidamente Microsoft Azure Information Protection nell'organizzazione. L'esecuzione dell'esercitazione richiede circa 30 minuti.
author: cabailey
manager: mbaldwin
ms.date: 09/25/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 3bc193c2-0be0-4c8e-8910-5d2cee5b14f7
translationtype: Human Translation
ms.sourcegitcommit: b23022c5fbec3d4f6f19ab5017ecf9badf01a9e7
ms.openlocfilehash: c8cad9c4b6efe2630843bcb1618ecd535670e0fe


---

# Passaggio 2: Configurare e pubblicare criteri di Azure Information Protection

>*Si applica a: Azure Information Protection*

Il criterio predefinito disponibile con Azure è utilizzabile senza alcuna operazione di configurazione. Tuttavia si esaminerà questo criterio e vi si apporterà qualche modifica.

1. In una nuova finestra del browser accedere al [portale di Azure](https://portal.azure.com) come amministratore globale del tenant.

2. Nel menu hub fare clic su **Nuovo** e quindi, nell'elenco **Marketplace**, selezionare **Sicurezza e identità**. Nel pannello**Sicurezza e identità**, nell'elenco **App in primo piano**, selezionare **Azure Information Protection**. Nel pannello **Azure Information Protection** fare clic su **Crea**.

    Verrà creato il pannello **Azure Information Protection** in modo che al successivo accesso al portale sarà possibile selezionare il servizio dall'elenco **More services** (Altri servizi) dell'hub. 

    > [!TIP] 
    > Selezionare **Aggiungi al dashboard** per creare un riquadro **Azure Information Protection** nel dashboard, in modo da ignorare la ricerca del servizio al successivo accesso al portale.

3.  Analizzare il pannello **Azure Information Protection** principale che illustra il criterio di Information Protection creato automaticamente:
    
    - Etichette per la classificazione: **Personal** (Personale), **Public** (Pubblico), **Internal** (Interno), **Confidential** (Riservato) e **Secret** (Segreto). Leggere la descrizione di ognuna per comprendere l'uso a cui è destinata. Si noti che per **Secret** (Segreto) esistono due etichette secondarie: **All Company** (Tutta la società) e **My Group** (Gruppo personale). Questo è un esempio di sottocategorie di una classificazione.

    - Per impostazione predefinita, per le etichette **Internal** (Interno), **Confidential** (Riservato) e **Secret** (Segreto) sono configurati contrassegni visivi (ad esempio piè di pagina, intestazione, filigrana). Per nessuna delle etichette è impostata la protezione. Le tre impostazioni globali, poi, non sono impostate. I documenti e i messaggi di posta elettronica non devono quindi necessariamente avere un'etichetta. Non esiste un'etichetta predefinita e gli utenti non sono obbligati a giustificare un eventuale abbassamento del livello di classificazione.

    ![Esercitazione introduttiva di Azure Information Protection, passaggio 3: Criterio predefinito](../media/info-protect-policy.png)

## Modifica delle impostazioni globali per un modello predefinito e richiesta di giustificazione

Nel corso di questa esercitazione verranno modificate alcune impostazioni globali per scoprirne il funzionamento:

1. Impostare **Selezionare l'etichetta predefinita** su **Internal** (Interno).

2. Impostare **Users must provide justification to set a lower classification label, remove a label, or remove protection. ** (Gli utenti devono giustificare un abbassamento del livello di classificazione, la rimozione di un'etichetta o la rimozione della protezione) su **On**.

## Configurazione di un'etichetta per la protezione, di una filigrana e di una condizione per la richiesta di classificazione

Verranno ora modificate le impostazioni di una delle etichette, **Confidential** (Riservato):

1. Fare clic sull'etichetta **Confidential** (Riservato). 
    
    Nel nuovo pannello **Label: Confidential** (Etichetta: Riservato) sono ora visibili le impostazioni disponibili per ogni etichetta. 

2. Nel pannello **Label: Confidential** (Etichetta: Riservato) individuare la sezione **Configurare il modello RMS per la protezione di documenti e messaggi di posta elettronica contenenti questa etichetta**:
    
    Per l'opzione **Selezionare il modello RMS da** mantenere l'impostazione predefinita **Azure RMS**. Quindi, per **Select RMS template** (Selezionare il modello RMS), fare clic sull'elenco a discesa e selezionare il modello predefinito **\<Nome organizzazione> - Confidential** (Riservato). 
    
    Ad esempio, se il nome dell'organizzazione è VanArsdel, Ltd, verrà visualizzata la voce **VanArsdel, Ltd - Confidential** e sarà possibile selezionarla: 
    
    ![Esercitazione introduttiva di Azure Information Protection, passaggio 3: Impostare la protezione di Azure RMS](../media/step2-select-rms-template.png)
    
    Se questo modello di Azure Rights Management è disabilitato, selezionare un modello alternativo. Tuttavia, se si seleziona un modello di reparto, assicurarsi che l'account sia incluso nell'ambito.
    
3. Individuare la sezione **Configurare il contrassegno visivo**:
    
    Per l'opzione **I documenti con questa etichetta includono un'intestazione** fare clic su **On** e quindi, nella casella **Testo della filigrana**, digitare il nome dell'organizzazione. Ad esempio, **VanArsdel, Ltd**: 
    
    ![Esercitazione introduttiva di Azure Information Protection, passaggio 3: Impostare la protezione di Azure RMS](../media/step2-configure-watermark.png)
    
    Anche se è possibile modificare le dimensioni, il colore e il layout delle filigrane, per il momento verranno mantenute le impostazioni predefinite.
    
4. Individuare la sezione **Configurare le condizioni per l'applicazione automatica di questa etichetta**:
    
    Fare clic su **Add a new condition** (Aggiungi una nuova condizione) e quindi nel pannello **Condition** (Condizione) selezionare quanto segue:
    
    a. **Choose the type of condition** (Scegliere il tipo di condizione): mantenere il valore predefinito **Built-in** (Predefinita).
    
    b. **Select built-in** (Selezionare tipo predefinito): dal menu a discesa selezionare **Numero di carta di credito**.
    
    c. **Minimum number of occurrences** (Numero minimo di occorrenze): mantenere il valore predefinito **1**.
    
    d. **Conta solo le occorrenze con valori univoci**: mantenere il valore predefinito **Off**.
    
    ![Esercitazione introduttiva di Azure Information Protection, passaggio 3: Configurare la condizione della carta di credito](../media/step2-configure-condition.png)
    
    Fare clic su **Save** (Salva) per tornare al pannello **Label: Confidential** (Etichetta: Riservato).

5. Nel pannello **Label: Confidential** (Etichetta: Riservato) **Numero di carta di credito** è visualizzato come **CONDITION NAME** (NOME CONDIZIONE) **1** **OCCURRENCES** (OCCORRENZE):
    
    ![Esercitazione introduttiva di Azure Information Protection, passaggio 3: Configurare la condizione della carta di credito](../media/step2-see-condition.png)

6. Per **Select how this label is applied** (Selezionare come applicare l'etichetta): mantenere l'impostazione predefinita **Recommended** (Consigliata) e non modificare il suggerimento per i criteri predefiniti:
    
    ![Esercitazione introduttiva di Azure Information Protection, passaggio 3: Classificazione consigliata](../media/step2-keep-recommended.png)

7. Nella casella **Enter notes for internal housekeeping** (Note per la gestione interna) digitare **For testing purposes only** (Solo a scopo di test):
    
    ![Esercitazione introduttiva di Azure Information Protection, passaggio 3: Digitare le note](../media/step2-type-notes.png)

8. Fare clic su **Save** (Salva) su questo pannello **Label: Confidential** (Etichetta: Riservato). Quindi, nel pannello **Azure Information Protection** principale, fare di nuovo clic su **Save** (Salva).

9. Ora che le modifiche sono state apportate e salvate, devono essere rese disponibili agli utenti. A tale scopo fare clic su **Publish** (Pubblica) e su **Sì** per confermare.

![Esercitazione introduttiva di Azure Information Protection, passaggio 3: Configurazione del criterio predefinito](../media/info-protect-policy-configured.png)

Al termine di questa esercitazione è possibile chiudere il portale di Azure o lasciarlo aperto per provare altre opzioni di configurazione.

Dopo aver esaminato i criteri predefiniti e aver apportato alcune modifiche, il passaggio successivo prevede l'installazione del client di Azure Information Protection e l'applicazione Rights Management sharing.

|Se si desiderano altre informazioni|Informazioni aggiuntive|
|--------------------------------|--------------------------|
|Informazioni sulle opzioni di configurazione per i criteri|[Configurazione dei criteri di Azure Information Protection](../deploy-use/configure-policy.md)|


>[!div class="step-by-step"]
[&#171; Passaggio 1](infoprotect-tutorial-step1.md)
[Passaggio 3 &#187;](infoprotect-tutorial-step3.md)


<!--HONumber=Sep16_HO4-->


