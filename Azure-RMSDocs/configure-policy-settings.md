---
title: Configurare le impostazioni dei criteri per Azure Information Protection - AIP
description: Configurare le impostazioni nei criteri di Azure Information Protection da applicare a tutti gli utenti e tutti i dispositivi.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 03/16/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 629815c0-457d-4697-a4cc-df0e6cc0c1a6
ROBOTS: NOINDEX
ms.subservice: aiplabels
ms.custom: admin
ms.openlocfilehash: 06b54317abbd5258bddd43ee18febc6470c1ba89
ms.sourcegitcommit: f6d536b6a3b5e14e24f0b9e58d17a3136810213b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/26/2021
ms.locfileid: "98809749"
---
# <a name="how-to-configure-the-policy-settings-for-azure-information-protection"></a>Come configurare le impostazioni dei criteri per Azure Information Protection

>***Si applica a**: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*
>
>***Pertinente per**: [Azure Information Protection client classico per Windows](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients). Per il client di etichettatura unificata, vedere [informazioni sulle etichette di riservatezza](/microsoft-365/compliance/sensitivity-labels) dalla documentazione di Microsoft 365. *

> [!NOTE] 
> Per offrire un'esperienza per i clienti unificata e semplificata, il **client classico di Azure Information Protection** e **Gestione etichette** nel portale di Azure saranno **deprecati** a partire dal **31 marzo 2021**. In questo intervallo di tempo tutti i clienti correnti di Azure Information Protection possono passare alla soluzione di etichettatura unificata usando la piattaforma di etichettatura unificata di Microsoft Information Protection. Altre informazioni nell'[avviso ufficiale sulla deprecazione](https://aka.ms/aipclassicsunset).

Oltre al titolo della barra e alla descrizione comando di Information Protection, nei criteri di Azure Information Protection sono disponibili alcune impostazioni che è possibile configurare indipendentemente dalle etichette:

![Impostazioni globali dei criteri di Azure Information Protection](./media/defaultsettings-aip.png)

Si noti che le impostazioni dei criteri potrebbero avere valori predefiniti diversi, a seconda di quando è stata acquistata la sottoscrizione di Azure Information Protection. Alcune impostazioni potrebbero derivare anche da un'[impostazione client personalizzata](./rms-client/client-admin-guide-customizations.md).

## <a name="to-configure-the-policy-settings"></a>Per configurare le impostazioni dei criteri

1. Aprire una nuova finestra del browser e accedere al [portale di Azure](configure-policy.md#signing-in-to-the-azure-portal), se questa operazione non è già stata eseguita. Quindi passare al riquadro **Azure Information Protection**.
    
    Ad esempio, nella casella di ricerca di risorse, servizi e documentazione: iniziare a digitare **Informazioni** e selezionare **Azure Information Protection**.

2. Dall'opzione di menu **classificazioni**  >  **criteri** : nel riquadro **Azure Information Protection-criteri** selezionare **globale** se le impostazioni che si desidera configurare verranno applicate a tutti gli utenti.
    
    Se le impostazioni da configurare si trovano in un [criterio con ambito](configure-policy-scope.md) per essere applicate solo a utenti selezionati, selezionare invece il criterio con ambito.

3. Nel riquadro **criteri** configurare le impostazioni:
    
   - **Select the default label** (Selezionare l'etichetta predefinita): quando si seleziona questa opzione, selezionare l'etichetta da assegnare ai documenti e ai messaggi di posta elettronica che non hanno un'etichetta. Non è possibile impostare un'etichetta come predefinita se contiene etichette secondarie.
        
        Questa impostazione si applica alle app di Office e allo scanner. Non è applicabile a Esplora file o PowerShell.
    
    - **Inviare i dati di controllo a Azure Information Protection Analytics**: prima di creare un'area di lavoro di Azure log Analytics per [Azure Information Analytics](reports-aip.md), i valori per questa impostazione sono **disattivati** e **non sono configurati**. Quando si crea l'area di lavoro, i valori diventano **No** e **Sì**.
        
        Quando l'impostazione è impostata **su on**, i client che supportano il reporting centrale inviano i dati al servizio Azure Information Protection. Queste informazioni includono le etichette applicate e quando un utente seleziona un'etichetta con una classificazione più bassa o rimuove un'etichetta. Per ulteriori informazioni sulle informazioni inviate e archiviate, vedere la sezione [informazioni raccolte e inviate a Microsoft](reports-aip.md#information-collected-and-sent-to-microsoft) nella documentazione relativa al reporting centrale. Impostare questa impostazione criterio su **disattivato** per impedire l'invio di questi dati.
    
    - **All documents and emails must have a label** (Tutti i documenti e i messaggi di posta elettronica devono avere un'etichetta): quando si imposta questa opzione su **Sì**, a tutti i documenti e messaggi di posta elettronica inviati deve essere applicata un'etichetta. L'etichetta può essere assegnata manualmente da un utente, automaticamente o come risultato di una [condizione](configure-policy-classification.md) oppure per impostazione predefinita selezionando l'opzione **Select the default label** (Selezionare l'etichetta predefinita).
        
       Se al momento del salvataggio di un documento o dell'invio di un messaggio di posta elettronica non è assegnata un'etichetta, viene chiesto all'utente di selezionarne una. Ad esempio:
        
       ![Prompt di Azure Information Protection se è impostata l'assegnazione di etichette](./media/info-protect-enforce-labelv2.png)
        
       Questa opzione non viene applicata quando si rimuove un'etichetta con il cmdlet [Set-AIPFileLabel](/powershell/module/azureinformationprotection/set-aipfilelabel) di PowerShell con il parametro *RemoveLabel*.
        
   - **Users must provide justification to set a lower classification label, remove a label, or remove protection** (Gli utenti devono specificare una giustificazione per impostare un'etichetta di classificazione inferiore, rimuovere un'etichetta o rimuovere la protezione): quando questa opzione viene impostata su **On** (Attiva) e l'utente esegue una qualsiasi di queste azioni, ad esempio modifica l'etichetta **Public** in **Personal**, viene chiesto di specificare una spiegazione per questa azione. L'utente può ad esempio spiegare che il documento non contiene informazioni riservate. L'azione e il motivo della relativa giustificazione vengono registrati nel registro eventi di Windows locale: **registri applicazioni e servizi**  >  **Azure Information Protection**.  
        
       ![Richiesta di Azure Information Protection se la nuova classificazione è inferiore](./media/info-protect-lower-justification.png)
        
       Questa opzione non è applicabile per abbassare la classificazione delle etichette secondarie sotto la stessa etichetta padre.
        
   - **For email messages with attachments, apply a label that matches the highest classification of those attachments** (Per i messaggi di posta elettronica con allegati, applica un'etichetta che corrisponda alla classificazione più elevata di tali elementi): quando questa opzione viene impostata su **Recommended** (Consigliata), viene richiesto di applicare un'etichetta ai messaggi di posta elettronica. L'etichetta viene scelta in modo dinamico, in base alle etichette di classificazione che vengono applicate agli allegati, e viene selezionata l'etichetta di classificazione più elevata. L'allegato deve essere un file fisico e non può essere un collegamento a un file (ad esempio, un collegamento a un file in Microsoft SharePoint o OneDrive). Gli utenti possono accettare il suggerimento o ignorarlo. Quando si imposta questa opzione su **Automatico**, l'etichetta viene applicata automaticamente, ma gli utenti possono rimuoverla o selezionarne un'altra prima di inviare il messaggio di posta elettronica.
        
        Per prendere in considerazione l'ordine delle etichette secondarie quando si usa questa impostazione dei criteri, è necessario [configurare un'impostazione client avanzata](./rms-client/client-admin-guide-customizations.md#enable-order-support-for-sublabels-on-attachments).
        
        Quando l'allegato con l'etichetta di classificazione più alta è configurato per la protezione con l'impostazione anteprima delle autorizzazioni definite dall'utente:-quando le autorizzazioni definite dall'utente dell'etichetta includono Outlook (non inviare), tale etichetta viene applicata e non viene applicata la protezione in diretta al messaggio di posta elettronica. Quando le autorizzazioni definite dall'utente dell'etichetta sono solo per Word, Excel, PowerPoint ed Esplora file, non si applica né tale etichetta né un tipo di protezione al messaggio di posta elettronica.
    
   - **Display the Information Protection bar in Office apps** (Visualizza la barra di Information Protection nelle app di Office) : quando questa impostazione è disattivata, gli utenti non possono selezionare etichette da una barra in Word, Excel, PowerPoint e Outlook. Gli utenti devono invece selezionare le etichette dal pulsante **Proteggi** sulla barra multifunzione. Quando questa impostazione è attivata, gli utenti possono selezionare le etichette dalla barra o dal pulsante.
        
       Quando questa impostazione è attivata, può essere usata in combinazione con un'impostazione client avanzata, in modo che gli utenti possano [nascondere in modo permanente la barra di Azure Information Protection](./rms-client/client-admin-guide-customizations.md#permanently-hide-the-azure-information-protection-bar) se scelgono di non visualizzare la barra. Questa operazione può essere eseguita deselezionando l'opzione **Mostra barra** dal pulsante **Proteggi** .
    
   - **Add the Do Not Forward button to the Outlook ribbon** (Aggiungi il pulsante Non inoltrare alla barra multifunzione Outlook): quando questa impostazione è attivata, gli utenti possono selezionare questo pulsante dal gruppo **Protezione** sulla barra multifunzione di Outlook oltre a selezionare l'opzione **Non inoltrare** dai menu di Outlook. Per garantire che gli utenti classifichino i messaggi di posta elettronica e li proteggano, potrebbe essere preferibile non aggiungere questo pulsante, ma [configurare un'etichetta per la protezione](configure-policy-protection.md) e un'autorizzazione user = defined per Outlook. Dal punto di vista funzionale, questa impostazione equivale a selezionare il pulsante **Non inoltrare**, ma quando questa funzionalità viene inclusa con un'etichetta, i messaggi di posta elettronica vengono classificati e protetti.
    
       Questa impostazione dei criteri può essere configurata anche con un'impostazione client avanzata come [personalizzazione client](./rms-client/client-admin-guide-customizations.md#hide-or-show-the-do-not-forward-button-in-outlook).
    
   - **Make the custom permissions option available to users** (Rendi disponibile l'opzione per le autorizzazioni personalizzate): quando questa impostazione è attivata, gli utenti visualizzano le opzioni per specificare impostazioni di protezione personalizzate che possono sostituire eventuali impostazioni di protezione incluse con una configurazione di etichetta. Gli utenti possono visualizzare anche un'opzione per rimuovere la protezione. Quando questa impostazione è disattivata, queste opzioni non vengono visualizzate agli utenti.
        
       Si noti che questa impostazione dei criteri non influisce sulle autorizzazioni personalizzate che gli utenti possono configurare dalle opzioni dei menu di Office. Tuttavia, questa impostazione può essere configurata anche con un'impostazione client avanzata come [personalizzazione client](./rms-client/client-admin-guide-customizations.md#make-the-custom-permissions-options-available-or-unavailable-to-users).
        
       Le opzioni per le autorizzazioni personalizzate si trovano nelle posizioni seguenti:
        
       - Dalla barra multifunzione nelle applicazioni di Office: scheda **Home** > gruppo **Protezione** > **Proteggi** > **Autorizzazioni personalizzate**
        
       - Da Esplora file: fare clic con il pulsante destro del mouse su > **classificare e proteggere le**  >  **autorizzazioni personalizzate**
    
   - **Provide a custom URL for the Azure Information Protection client "Tell me more" web page** (Specifica un URL personalizzato per la pagina Web "Ulteriori informazioni" del client di Azure Information Protection): questo collegamento viene visualizzato nella finestra di dialogo **Microsoft Azure Information Protection** della sezione **Guida e commenti** dopo aver selezionato **Proteggi** > **Guida e commenti** dalla scheda **Home** di un'applicazione Office. Per impostazione predefinita, questo collegamento indirizza l'utente al sito Web di [Azure Information Protection](https://www.microsoft.com/cloud-platform/azure-information-protection). Se si preferisce che questo collegamento indirizzi l'utente a un'altra pagina Web, è possibile immettere un URL HTTP o HTTPS (consigliato). Non viene effettuato alcun controllo per verificare che l'URL personalizzato sia accessibile o venga correttamente visualizzato su tutti i dispositivi.
        
       Per l'help desk, ad esempio, è possibile immettere la pagina della documentazione Microsoft che include informazioni sull'installazione e l'uso del client: `https://docs.microsoft.com/information-protection/rms-client/info-protect-client` . O informazioni sulla versione di rilascio: `https://docs.microsoft.com/information-protection/rms-client/client-version-release-history` . In alternativa, è possibile pubblicare una pagina Web personalizzata con informazioni sulle modalità di contatto dell'help desk o con un video che illustra agli utenti come usare le etichette configurate in precedenza.

4. Per salvare le modifiche e renderle disponibili agli utenti, fare clic su **Salva**.

Quando fa clic su **Salva**, le modifiche diventano automaticamente disponibili per utenti e servizi. Non è più presente un'opzione di pubblicazione separata.

## <a name="next-steps"></a>Passaggi successivi

Per vedere come alcune delle impostazioni relative ai criteri possano interagire, seguire l'esercitazione [Configurare impostazioni dei criteri di Azure Information Protection che interagiscono tra loro](infoprotect-settings-tutorial.md).

Per altre informazioni sulla configurazione dei criteri di Azure Information Protection, usare i collegamenti nella sezione [Configurazione dei criteri dell'organizzazione](configure-policy.md#configuring-your-organizations-policy).