---
title: Esercitazione - Usare le impostazioni dei criteri di Azure Information Protection per classificare i dati
description: Esercitazione introduttiva che illustra la configurazione delle impostazioni dei criteri di Azure Information Protection per agevolare la classificazione dei documenti e dei messaggi di posta elettronica dell'organizzazione.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 10/01/2019
ms.topic: tutorial
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: aiplabels
ms.custom: admin
ms.openlocfilehash: 73f242b50e53eb7f5408bf99902daf0214d37268
ms.sourcegitcommit: d939dd4191965f68a5e59e13ed612e40bfa28556
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/01/2019
ms.locfileid: "71712574"
---
# <a name="tutorial-configure-azure-information-protection-policy-settings-that-work-together"></a>Esercitazione: Configurare impostazioni dei criteri di Azure Information Protection che interagiscono tra loro

>*Si applica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*
>
> *Istruzioni per: [Client Azure Information Protection per Windows](faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*

In questa esercitazione si apprenderà come:
> [!div class="checklist"]
> * Configurare impostazioni dei criteri che interagiscono tra loro
> * Vedere le impostazioni in azione

Invece di affidare agli utenti il compito di etichettare manualmente documenti e messaggi di posta elettronica, è possibile usare le impostazioni dei criteri di Azure Information Protection per:

- Assicurare un livello base di classificazione per i contenuti nuovi e modificati

- Informare gli utenti sull'uso delle etichette e semplificare l'applicazione dell'etichetta corretta

È possibile completare questa esercitazione in circa 15 minuti.

## <a name="prerequisites"></a>Prerequisiti 

Per completare questa esercitazione, è necessario:

1. Disporre di una sottoscrizione che includa un piano 1 o 2 di Azure Information Protection.
    
    In assenza di una sottoscrizione con questo piano, è possibile creare un account [gratuito](https://admin.microsoft.com/Signup/Signup.aspx?OfferId=87dd2714-d452-48a0-a809-d2f58c4f68b7) per l'organizzazione.

2. Il pannello Azure Information Protection viene aggiunto al portale di Azure e una o più etichette vengono pubblicate nei criteri globali di Azure Information Protection.
    
    Questi passaggi sono illustrati nell'[Avvio rapido: Aggiungere Azure Information Protection al portale di Azure e visualizzare i criteri](quickstart-viewpolicy.md).

3. Deve essere installato il client Azure Information Protection (versione classica) nel computer in uso con Windows (almeno Windows 7 con Service Pack 1). 
    
    È possibile installare la versione classica del client accedendo all'[Area download Microsoft](https://www.microsoft.com/en-us/download/details.aspx?id=53018) e scaricando **AzInfoProtection.exe** dalla pagina di Azure Information Protection. 
    
    Se si usa un client di assegnazione di etichette diverso per la versione classica del client, vedere la documentazione di Office per informazioni sulle impostazioni dei criteri per le etichette di riservatezza. Ad esempio, [Panoramica delle etichette di riservatezza](/microsoft-365/compliance/sensitivity-labels).

4. È stato eseguito l'accesso alle app di Office da una delle seguenti categorie:
    
    - App di Office con versione minima 1805, build 9330.2078 da Office 365 Business o Microsoft 365 Business quando all'utente viene assegnata una licenza per Azure Rights Management (nota anche come Azure Information Protection per Office 365).
    
    - Office 365 ProPlus.
    
    - Office Professional Plus 2019.
    
    - Office Professional Plus 2016.
    
    - Office Professional Plus 2013 con Service Pack 1.
    
    - Office Professional Plus 2010 con Service Pack 2.

Per un elenco completo dei prerequisiti per l'uso di Azure Information Protection, vedere [Requisiti per Azure Information Protection](requirements.md).

A questo punto, procedere con l'esercitazione.

## <a name="edit-the-azure-information-protection-policy"></a>Modificare i criteri di Azure Information Protection

Invece di affidare agli utenti il compito di etichettare manualmente documenti e messaggi di posta elettronica, è possibile usare alcune delle impostazioni dei criteri per garantire un livello base di classificazione. 

Tramite il portale di Azure verranno modificati i criteri globali per la modifica delle impostazioni dei criteri per tutti gli utenti.

1. Aprire una nuova finestra del browser e accedere al [portale di Azure](https://portal.azure.com) come amministratore globale. Passare quindi ad **Azure Information Protection**. 
    
    Ad esempio, dal menu hub fare clic su **Tutti i servizi** e iniziare a digitare **Informazioni** nella casella Filtro. Selezionare **Azure Information Protection**.
    
    Se non si è l'amministratore globale, usare il collegamento seguente per i ruoli alternativi: [Accesso al portale di Azure](configure-policy.md#signing-in-to-the-azure-portal)

2. Selezionare **Classificazioni** > **Criteri** > **Globale** per aprire il pannello **Criteri: Globale**. 

3. Individuare le impostazioni dei criteri dopo le etichette nella sezione **Configure settings to display and apply on Information Protection end users** (Configurare le impostazioni da visualizzare e applicare per gli utenti finali di Information Protection). Le impostazioni personali potrebbero avere valori diversi da quelli visualizzati:
    
    ![Esercitazione di Azure Information Protection - Impostazioni predefinite](./media/defaultsettings-aip.png)

4. Modificare le impostazioni in modo che corrispondano ai valori nella tabella seguente. Prendere nota delle impostazioni modificate nel caso in cui si voglia ripristinarle al termine di questa esercitazione. 

    |Impostazione|Valore|Informazioni|
    |-------|-----|-----|
    |**Selezionare l'etichetta predefinita**|**Generalee**|L'etichetta **Generale** è una delle etichette predefinite che Azure Information Protection può creare automaticamente. Questo passaggio è trattato nell'Avvio rapido [Creare e pubblicare etichette](quickstart-viewpolicy.md#create-and-publish-labels). Se non si dispone di un'etichetta denominata **Generale**, selezionarne un'altra dall'elenco a discesa. Ai documenti e ai messaggi di posta elettronica senza etichetta verrà applicata automaticamente questa etichetta come classificazione di base. Gli utenti potranno tuttavia modificare l'etichetta selezionata impostandone un'altra.|
    |**Tutti i documenti e i messaggi di posta elettronica devono avere un'etichetta**|**Sì**|Questa impostazione è nota anche come etichettatura obbligatoria, perché impedisce agli utenti il salvataggio di documenti o l'invio di messaggi di posta elettronica senza etichetta. Insieme all'etichetta predefinita, i documenti e i messaggi di posta elettronica avranno l'etichetta predefinita impostata o un'etichetta scelta dagli utenti.
    |**Per i messaggi di posta elettronica con allegati, applica un'etichetta corrispondente alla classificazione più elevata di questi allegati**|**Consigliato**|Questa impostazione richiede agli utenti di selezionare un'etichetta di classificazione superiore per i messaggi di posta elettronica quando si allegano documenti contenenti una classificazione più elevata rispetto all'etichetta predefinita selezionata.
    |**Visualizza la barra di Information Protection nelle app Office**|**Sì**|La visualizzazione della barra di Information Protection rende più semplice per gli utenti visualizzare e modificare l'etichetta predefinita.
    
    A questo punto le impostazioni dovrebbero avere un aspetto simile al seguente:
    
    ![Esercitazione di Azure Information Protection - Impostazioni predefinite modificate](./media/defaultsettings-aip-changed.png)

5. Selezionare **Salva** nel pannello **Criteri: Globale** e, se viene richiesto di confermare l'operazione, scegliere **OK**. 

## <a name="see-your-policy-settings-in-action"></a>Vedere le impostazioni dei criteri in azione 

Per questa esercitazione si useranno Word e Outlook per vedere le modifiche ai criteri in azione. Se queste app erano già state caricate prima della modifica delle impostazioni dei criteri, riavviarle per scaricare le modifiche.

### <a name="default-label-and-the-information-protection-bar"></a>Etichetta predefinita e barra di Information Protection

Aprire un nuovo documento in Word. Si noterà che il documento viene etichettato automaticamente come **Generale** e che non sono stati gli utenti a selezionare un'etichetta. 

Con la barra di Information Protection visualizzata che mostra le etichette disponibili, è facile per gli utenti vedere l'etichetta attualmente selezionata e modificarla se l'etichetta predefinita non è appropriata:

![Esercitazione di Azure Information Protection - Nuovo documento con etichetta predefinita](./media/defaultlabel-word.png)

Anziché modificare l'etichetta, chiudere la barra di Information Protection per confrontare l'esperienza se non viene visualizzata la barra:

![Esercitazione di Azure Information Protection - Chiudere la barra](./media/infoprotect-bar-close.png)

L'etichetta **Generale** è ancora selezionata, ma è molto meno evidente. È anche meno evidente come selezionare un'altra etichetta. A tale scopo, gli utenti devono selezionare il pulsante **Proteggi**:

![Esercitazione di Azure Information Protection - Pulsante Proteggi selezionato](./media/infoprotect-protectbutton-pulldown.png)

A questo punto, si noterà che nel menu a discesa l'etichetta **Generale** è selezionata, dal momento che riporta un segno di spunta. Per modificare l'etichetta attualmente selezionata, gli utenti possono selezionarne un'altra dall'elenco. Se gli utenti non hanno familiarità con l'assegnazione delle etichette, probabilmente non si ricorderanno di selezionare ogni volta il pulsante **Proteggi**. Potrebbero anche non sapere che possono selezionare un'altra etichetta.

Per visualizzare nuovamente la barra di Information Protection, selezionare **Mostra barra** dal menu a discesa.

> [!TIP]
> È possibile selezionare un'altra etichetta predefinita per Outlook, configurando un'[impostazione client avanzata](./rms-client/client-admin-guide-customizations.md#set-a-different-default-label-for-outlook).

### <a name="mandatory-labeling"></a>Etichettatura obbligatoria

È possibile modificare l'etichetta **Generale** attualmente selezionata impostandone un'altra, ma non è possibile rimuoverla. Avendo impostato l'opzione **Tutti i documenti e i messaggi di posta elettronica devono avere un'etichetta** su **Sì**, l'icona **Elimina l'etichetta** non è disponibile nella barra di Information Protection. 

Se questa impostazione non è stata modificata, questa icona viene visualizzata nella barra di Information Protection:

![Esercitazione di Azure Information Protection - Chiudere la barra](./media/infoprotect-deletelabel-icon.png)

Insieme a un'etichetta predefinita, l'etichettatura obbligatoria garantisce che i documenti e i messaggi di posta elettronica nuovi e modificati abbiano una classificazione di base di propria scelta. 

Se con l'impostazione di etichettatura obbligatoria non è stata impostata un'etichetta predefinita, agli utenti viene sempre richiesto di selezionare un'etichetta durante il salvataggio di un documento senza etichetta o l'invio di un messaggio di posta elettronica senza etichetta. Per molti utenti, questi continui prompt possono essere frustranti e anche comportare l'assegnazione di etichette meno accurate. La richiesta di selezionare un'etichetta al termine del lavoro su un documento o un messaggio di posta elettronica comporta un'interruzione del flusso di lavoro per gli utenti ed esiste pertanto il rischio che le etichette vengano selezionate in modo casuale per poter passare all'operazione successiva.

### <a name="recommendations-for-emails-with-attachments"></a>Suggerimenti per i messaggi di posta elettronica con allegati

Per il documento di Word aperto, scegliere un'etichetta con una classificazione superiore rispetto a **Generale**, ad esempio una delle etichette secondarie in **Riservato**, come **Riservato - Chiunque (senza protezione)** . Salvare il documento in locale e assegnare un nome qualsiasi. 

Avviare Outlook e creare un nuovo messaggio di posta elettronica. Come con Word, il nuovo messaggio di posta elettronica viene etichettato automaticamente come **Generale** ed è visualizzata la barra di Information Protection.

Aggiungere il documento di Word appena etichettato come allegato al messaggio di posta elettronica. Viene visualizzato un prompt per la modifica dell'etichetta del messaggio di posta elettronica in **Riservato**, in modo da corrispondere all'allegato di Word. È possibile accettare il suggerimento o ignorarlo:

![Esercitazione di Azure Information Protection - Prompt per riassegnare l'etichetta al messaggio di posta elettronica in modo che corrisponda all'allegato etichettato](./media/infoprotect-matchemail-label.png)

Se si sceglie **Ignora**, la nuova etichetta non viene applicata e il messaggio di posta elettronica mantiene l'etichetta predefinita configurata **Generale**. Le etichette disponibili sono ancora visibili per selezionare un'alternativa.

Se si seleziona **Modifica ora**, il messaggio di posta elettronica viene rietichettato con l'etichetta secondaria **Riservato**. Gli utenti possono comunque modificare l'etichetta prima di inviare il messaggio di posta elettronica, selezionando l'icona di modifica etichetta:

![Esercitazione di Azure Information Protection - Icona Modifica l'etichetta](./media/infoprotect-editlabel-icon.png)

La barra di Information Protection viene nuovamente visualizzata per consentire agli utenti di selezionare un'etichetta alternativa.

Poiché l'etichetta viene selezionata prima di inviare il messaggio di posta elettronica, non è necessario inviare effettivamente il messaggio per verificare il funzionamento di questa impostazione dei criteri. È possibile chiudere il messaggio di posta elettronica senza inviarlo o salvarlo.

Tuttavia, si potrebbe voler ripetere questo esercizio allegando anche un altro documento con una classificazione superiore (etichetta secondaria di **Riservatezza elevata**). Si noterà quindi in che modo il prompt viene modificato per applicare l'etichetta di classificazione superiore. Se si testano più allegati con etichette secondarie che hanno la stessa etichetta padre, è necessario configurare [un'impostazione client avanzata](./rms-client/client-admin-guide-customizations.md#enable-order-support-for-sublabels-on-attachments) per supportare il relativo ordinamento nel portale di Azure.

## <a name="clean-up-resources"></a>Pulizia delle risorse

Se non si vogliono mantenere le modifiche apportate in questa esercitazione, seguire questa procedura:

1. Selezionare **Classificazioni** > **Criteri** > **Globale** per aprire il pannello **Criteri: Globale**.

2. Ripristinare i valori originali precedentemente annotati per le impostazioni dei criteri e quindi selezionare **Salva**.

Riavviare le app Word e Outlook per scaricare queste modifiche.

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sulla modifica delle impostazioni dei criteri di Azure Information Protection, vedere [Come configurare le impostazioni dei criteri per Azure Information Protection](configure-policy-settings.md).

Le impostazioni dei criteri che sono state modificate hanno contribuito a garantire un livello di classificazione di base, oltre a incoraggiare gli utenti a selezionare un'etichetta appropriata. Il passaggio successivo consiste nel potenziare questa strategia controllando il contenuto di documenti e messaggi di posta elettronica e quindi consigliando o applicando automaticamente un'etichetta appropriata. È possibile eseguire questa operazione configurando le etichette per le condizioni. Per altre informazioni, vedere [Come configurare le condizioni per la classificazione automatica e consigliata per Azure Information Protection](configure-policy-classification.md).
