---
title: Configurare le impostazioni dei criteri per Azure Information Protection - AIP
description: Configurare le impostazioni nei criteri di Azure Information Protection da applicare a tutti gli utenti e tutti i dispositivi.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 12/04/2018
ms.topic: conceptual
ms.service: information-protection
ms.assetid: 629815c0-457d-4697-a4cc-df0e6cc0c1a6
ms.openlocfilehash: aa39e1150dbb4310fb0e075d01385f40a18a3e1d
ms.sourcegitcommit: d06594550e7ff94b4098a2aa379ef2b19bc6123d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/07/2018
ms.locfileid: "53023703"
---
# <a name="how-to-configure-the-policy-settings-for-azure-information-protection"></a>Come configurare le impostazioni dei criteri per Azure Information Protection

>*Si applica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*

Oltre al titolo della barra e alla descrizione comando di Information Protection, nei criteri di Azure Information Protection sono disponibili alcune impostazioni che è possibile configurare indipendentemente dalle etichette:

![Impostazioni globali dei criteri di Azure Information Protection](./media/info-protect-policy-default-settingsv3.png)

Si noti che le impostazioni dei criteri potrebbero avere valori predefiniti diversi, a seconda di quando è stata acquistata la sottoscrizione di Azure Information Protection. Alcune impostazioni potrebbero derivare anche da un'[impostazione client personalizzata](./rms-client/client-admin-guide-customizations.md).

Per configurare queste impostazioni:

1. Se non è già stato fatto, aprire una nuova finestra del browser e [accedere al portale di Azure](configure-policy.md#signing-in-to-the-azure-portal). Quindi passare al pannello **Azure Information Protection**.
    
    Ad esempio, dal menu hub fare clic su **Tutti i servizi** e iniziare a digitare **Informazioni** nella casella Filtro. Selezionare **Azure Information Protection**.

2. Dall'opzione di menu **Classificazioni** > **Criteri**: nel pannello **Azure Information Protection - Criteri** selezionare **Globale** se le impostazioni da configurare si applicheranno a tutti gli utenti.
    
    Se le impostazioni da configurare si trovano in un [criterio con ambito](configure-policy-scope.md) per essere applicate solo a utenti selezionati, selezionare invece il criterio con ambito.

3. Nel pannello **Criteri** configurare le impostazioni:
    
    - **Selezionare l'etichetta predefinita**: quando si seleziona questa opzione, selezionare l'etichetta da assegnare ai documenti e ai messaggi di posta elettronica che non hanno un'etichetta. Non è possibile impostare un'etichetta come predefinita se contiene etichette secondarie. 
    
    - **Tutti i documenti e i messaggi di posta elettronica devono avere un'etichetta**: quando si imposta questa opzione su **Sì**, a tutti i documenti e messaggi di posta elettronica inviati deve essere applicata un'etichetta. L'etichetta può essere assegnata manualmente da un utente, automaticamente o come risultato di una [condizione](configure-policy-classification.md) oppure per impostazione predefinita selezionando l'opzione **Selezionare l'etichetta predefinita**.
        
        Se al momento del salvataggio di un documento o dell'invio di un messaggio di posta elettronica non è assegnata un'etichetta, viene chiesto all'utente di selezionarne una. Ad esempio:
        
        ![Prompt di Azure Information Protection se è impostata l'assegnazione di etichette](./media/info-protect-enforce-labelv2.png)
        
        Questa opzione non viene applicata quando si rimuove un'etichetta con il cmdlet [Set-AIPFileLabel](/powershell/module/azureinformationprotection/set-aipfilelabel) di PowerShell con il parametro *RemoveLabel*.
        
    - **Users must provide justification to set a lower classification label, remove a label, or remove protection** (Gli utenti devono specificare una giustificazione per impostare un'etichetta di classificazione inferiore, rimuovere un'etichetta o rimuovere la protezione): quando questa opzione viene impostata su **On** (Attiva) e l'utente esegue una qualsiasi di queste azioni, ad esempio modifica l'etichetta **Public** in **Personal**, viene chiesto di specificare una spiegazione per questa azione. L'utente può ad esempio spiegare che il documento non contiene informazioni riservate. L'azione e la relativa giustificazione vengono registrate nel registro eventi di Windows locale: **Applicazioni e servizi** > **Azure Information Protection**.  
        
        ![Richiesta di Azure Information Protection se la nuova classificazione è inferiore](./media/info-protect-lower-justification.png)
        
        Questa opzione non è applicabile per abbassare la classificazione delle etichette secondarie sotto la stessa etichetta padre.
        
    - **For email messages with attachments, apply a label that matches the highest classification of those attachments** (Per i messaggi di posta elettronica con allegati, applica un'etichetta che corrisponda alla classificazione più elevata di tali elementi): quando questa opzione viene impostata su **Recommended** (Consigliata), viene richiesto di applicare un'etichetta ai messaggi di posta elettronica. L'etichetta viene scelta in modo dinamico, in base alle etichette di classificazione che vengono applicate agli allegati, e viene selezionata l'etichetta di classificazione più elevata. L'allegato deve essere un file fisico e non un collegamento a un file, ad esempio in SharePoint o OneDrive for Business. Gli utenti possono accettare il suggerimento o ignorarlo. Quando si imposta questa opzione su **Automatico**, l'etichetta viene applicata automaticamente, ma gli utenti possono rimuoverla o selezionarne un'altra prima di inviare il messaggio di posta elettronica.
    
    Quando l'allegato con l'etichetta di classificazione più elevata è configurato per la protezione con l'impostazione di anteprima delle autorizzazioni definite dall'utente, il messaggio di posta elettronica viene etichettato con la stessa classificazione, ma la protezione non viene applicata.
    
    - **Display the Information Protection bar in Office apps** (Visualizza la barra di Information Protection nelle app di Office) : quando questa impostazione è disattivata, gli utenti non possono selezionare etichette da una barra in Word, Excel, PowerPoint e Outlook. Gli utenti devono invece selezionare le etichette dal pulsante **Proteggi** sulla barra multifunzione. Quando questa impostazione è attivata, gli utenti possono selezionare le etichette dalla barra o dal pulsante.
        
        Quando questa impostazione è attivata, può essere usata in combinazione con un'impostazione client avanzata, in modo che gli utenti possano [nascondere in modo permanente la barra di Azure Information Protection](./rms-client/client-admin-guide-customizations.md#permanently-hide-the-azure-information-protection-bar) se scelgono di non visualizzare la barra. A tale scopo, è necessario deselezionare l'opzione **Mostra barra** dal pulsante **Proteggi**.
    
    - **Add the Do Not Forward button to the Outlook ribbon** (Aggiungi il pulsante Non inoltrare alla barra multifunzione Outlook): quando questa impostazione è attivata, gli utenti possono selezionare questo pulsante dal gruppo **Protezione** sulla barra multifunzione di Outlook oltre a selezionare l'opzione **Non inoltrare** dai menu di Outlook. Per garantire che gli utenti possano classificare i messaggi di posta elettronica, oltre a proteggerli, è preferibile non aggiungere questo pulsante e invece [configurare un'etichetta per la protezione](configure-policy-protection.md) e un'autorizzazione definita dall'utente per Outlook. Dal punto di vista funzionale, questa impostazione equivale a selezionare il pulsante **Non inoltrare**, ma quando questa funzionalità viene inclusa con un'etichetta, i messaggi di posta elettronica vengono classificati e protetti.
    
        Questa impostazione dei criteri può essere configurata anche con un'impostazione client avanzata come [personalizzazione client](./rms-client/client-admin-guide-customizations.md#hide-or-show-the-do-not-forward-button-in-outlook).
    
    - **Make the custom permissions option available to users** (Rendi disponibile l'opzione per le autorizzazioni personalizzate): quando questa impostazione è attivata, gli utenti visualizzano le opzioni per specificare impostazioni di protezione personalizzate che possono sostituire eventuali impostazioni di protezione incluse con una configurazione di etichetta. Gli utenti possono visualizzare anche un'opzione per rimuovere la protezione. Quando questa impostazione è disattivata, queste opzioni non vengono visualizzate agli utenti.
        
        Si noti che questa impostazione dei criteri non influisce sulle autorizzazioni personalizzate che gli utenti possono configurare dalle opzioni dei menu di Office. Tuttavia, questa impostazione può essere configurata anche con un'impostazione client avanzata come [personalizzazione client](./rms-client/client-admin-guide-customizations.md#make-the-custom-permissions-options-available-or-unavailable-to-users).
        
        Le opzioni per le autorizzazioni personalizzate si trovano nelle posizioni seguenti:
        
        - Dalla barra multifunzione nelle applicazioni di Office: scheda **Home** > gruppo **Protezione** > **Proteggi** > **Autorizzazioni personalizzate**
        
        - In File Explorer fare clic con il pulsante destro del mouse su > **Classifica e proteggi** > **Autorizzazioni personalizzate**
    
    - **Provide a custom URL for the Azure Information Protection client "Tell me more" web page** (Specifica un URL personalizzato per la pagina Web "Ulteriori informazioni" del client di Azure Information Protection): questo collegamento viene visualizzato nella finestra di dialogo **Microsoft Azure Information Protection** della sezione **Guida e commenti** dopo aver selezionato **Proteggi** > **Guida e commenti** dalla scheda **Home** di un'applicazione Office. Per impostazione predefinita, questo collegamento indirizza l'utente al sito Web di [Azure Information Protection](https://www.microsoft.com/cloud-platform/azure-information-protection). Se si preferisce che questo collegamento indirizzi l'utente a un'altra pagina Web, è possibile immettere un URL HTTP o HTTPS (consigliato). Non viene effettuato alcun controllo per verificare che l'URL personalizzato sia accessibile o venga correttamente visualizzato su tutti i dispositivi.
        
        Per l'help desk, è ad esempio possibile immettere la pagina della documentazione Microsoft che include informazioni sull'installazione e sull'uso del client (**https://docs.microsoft.com/information-protection/rms-client/info-protect-client**) o informazioni sulla versione di rilascio (**https://docs.microsoft.com/information-protection/rms-client/client-version-release-history**). In alternativa, è possibile pubblicare una pagina Web personalizzata con informazioni sulle modalità di contatto dell'help desk o con un video che illustra agli utenti come usare le etichette configurate in precedenza.

3. Per salvare le modifiche e renderle disponibili agli utenti, fare clic su **Salva**.

Quando fa clic su **Salva**, le modifiche diventano automaticamente disponibili per utenti e servizi. Non è più presente un'opzione di pubblicazione separata.

## <a name="next-steps"></a>Passaggi successivi

Per vedere come alcune delle impostazioni relative ai criteri possano interagire, seguire l'esercitazione [Configurare impostazioni dei criteri di Azure Information Protection che interagiscono tra loro](infoprotect-settings-tutorial.md).

Per altre informazioni sulla configurazione dei criteri di Azure Information Protection, usare i collegamenti nella sezione [Configurazione dei criteri dell'organizzazione](configure-policy.md#configuring-your-organizations-policy).

