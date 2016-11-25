---
title: Come configurare le impostazioni dei criteri globali | Azure Information Protection
description: Nei criteri di Azure Information Protection sono disponibili 3 impostazioni valide per tutti gli utenti e tutti i dispositivi.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 11/16/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 629815c0-457d-4697-a4cc-df0e6cc0c1a6
translationtype: Human Translation
ms.sourcegitcommit: 8fa2ed9ff9ebe5c850ab5681e4dcc1f3d3c676b3
ms.openlocfilehash: de5f5fbddb84e4444751e9fefbfe6ec3fe3e45e4


---

# <a name="how-to-configure-the-global-policy-settings-for-azure-information-protection"></a>Come configurare le impostazioni dei criteri globali per Azure Information Protection

>*Si applica a: Azure Information Protection*

Nei criteri di Azure Information Protection sono disponibili quattro impostazioni valide per tutti gli utenti e tutti i dispositivi:

![Impostazioni globali dei criteri di Azure Information Protection](../media/info-protect-policy-settings.png)


Per configurare queste impostazioni:

1. Se non è già stato fatto, in una nuova finestra del browser accedere al [portale di Azure](https://portal.azure.com) come amministratore globale e quindi passare al pannello **Azure Information Protection**. 
    
    Ad esempio, dal menu principale fare clic su **Altri servizi** e iniziare a digitare **Informazioni** nella casella Filtro. Selezionare **Azure Information Protection**.

2. Nel pannello **Azure Information Protection** configurare queste impostazioni globali:

    - **Tutti i documenti e i messaggi di posta elettronica devono avere un'etichetta**: quando si imposta questa opzione su **Sì**, a tutti i documenti e messaggi di posta elettronica inviati deve essere applicata un'etichetta. L'etichetta può essere assegnata manualmente da un utente, automaticamente o come risultato di una [condizione](configure-policy-classification.md) oppure per impostazione predefinita selezionando l'opzione **Selezionare l'etichetta predefinita**. 

    Se al momento del salvataggio di un documento o dell'invio di un messaggio di posta elettronica non è assegnata un'etichetta, all'utente viene chiesto di selezionarne una:

    ![Richiesta di Azure Information Protection se la nuova classificazione è inferiore](../media/info-protect-enforce-label.png)

    - **Selezionare l'etichetta predefinita**: quando si seleziona questa opzione, selezionare l'etichetta da assegnare ai documenti e ai messaggi di posta elettronica che non hanno un'etichetta. Non è possibile impostare un'etichetta come predefinita se contiene etichette secondarie. 

    - **Users must provide justification to set a lower classification label, remove a label, or remove protection** (Gli utenti sono obbligati a giustificare un abbassamento del livello di classificazione dell'etichetta, la rimozione di un'etichetta o la rimozione della protezione). Quando l'opzione viene impostata su **On** (On) e viene eseguita un'azione qualsiasi, ad esempio viene modificata l'etichetta **Segret** (Segreto) in **Personal** (Personale), all'utente viene chiesto di dare una spiegazione per questa azione. L'utente può ad esempio spiegare che il documento non contiene informazioni riservate. L'azione e la relativa giustificazione vengono registrati nel registro eventi di Windows locale: **Application** > **Microsoft Azure Information Protection**.  

    ![Richiesta di Azure Information Protection se la nuova classificazione è inferiore](../media/info-protect-lower-justification.png)

    Questa opzione non è applicabile alle etichette secondarie.

    - **Provide a custom URL for the Azure Information Protection client "Tell me more" web page** (Specifica un URL personalizzato per la pagina Web "Ulteriori informazioni" del client di Azure Information Protection): questo link viene visualizzato nella finestra di dialogo **Microsoft Azure Information Protection** della sezione **Guida e commenti** dopo aver selezionato **Proteggi** > **Guida e commenti** dalla scheda **Home** di un'applicazione Office. Per impostazione predefinita, questo collegamento indirizza l'utente al sito Web di [Azure Information Protection](https://www.microsoft.com/en-us/cloud-platform/azure-information-protection). Se si preferisce che questo collegamento indirizzi l'utente a un'altra pagina Web, è possibile immettere un URL HTTP o HTTPS (consigliato). Non viene effettuato alcun controllo per verificare che l'URL personalizzato sia accessibile o venga correttamente visualizzato su tutti i dispositivi.
    
    Per il proprio help desk, ad esempio, è possibile scegliere di immettere la pagina della documentazione Microsoft con informazioni sull'installazione e l'uso del client (**https://docs.microsoft.com/information-protection/rms-client/info-protect-client**) o con informazioni sulla versione di rilascio (**https://docs.microsoft.com/information-protection/rms-client/client-version-release-history**). In alternativa, è possibile pubblicare una pagina Web personalizzata con informazioni sulle modalità di contatto dell'help desk o con un video che illustra agli utenti come usare le etichette configurate in precedenza.

3. Fare clic su **Save** (Salva) per salvare le modifiche.

4. Per mettere le modifiche a disposizione degli utenti, fare clic su **Publish** (Pubblica).

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sulla configurazione dei criteri di Azure Information Protection, usare i collegamenti nella sezione [Configurazione dei criteri dell'organizzazione](configure-policy.md#configuring-your-organizations-policy).  












<!--HONumber=Nov16_HO3-->


