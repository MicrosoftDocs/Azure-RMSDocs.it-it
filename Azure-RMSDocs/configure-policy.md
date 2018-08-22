---
title: Configurare i criteri di Azure Information Protection
description: Per configurare le funzioni di classificazione, aggiunta di etichette e protezione, è necessario configurare i criteri di Azure Information Protection.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 08/02/2018
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: ba0e8119-886c-4830-bd26-f98fb14b2933
ms.reviewer: eymanor
ms.suite: ems
ms.openlocfilehash: 5bb41669d8f2d4abed72094d33c6136380ed8020
ms.sourcegitcommit: 5fdf013fe05b65517b56245e1807875d80be6e70
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2018
ms.locfileid: "39490104"
---
# <a name="configuring-the-azure-information-protection-policy"></a>Configurazione dei criteri di Azure Information Protection

>*Si applica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*

Per configurare le funzioni di classificazione, aggiunta di etichette e protezione, è necessario configurare i criteri di Azure Information Protection. Questi criteri vengono quindi scaricati nei computer in cui è installato il [client di Azure Information Protection](https://www.microsoft.com/en-us/download/details.aspx?id=53018).

I criteri contengono etichette e impostazioni:

- Le etichette applicano un valore di classificazione a documenti e a messaggi di posta elettronica e possono facoltativamente proteggerne il contenuto. Il client Azure Information Protection visualizza queste etichette nelle app di Office e quando gli utenti fanno clic con il pulsante destro del mouse in Esplora File. È possibile applicare queste etichette anche tramite PowerShell e l'analisi di Azure Information Protection.

- Le impostazioni modificano il comportamento predefinito del client Azure Information Protection. È ad esempio possibile selezionare un'etichetta predefinita, se tutti i documenti e i messaggi di posta elettronica devono avere un'etichetta e se la barra di Azure Information Protection viene visualizzata nelle app di Office.

## <a name="subscription-support"></a>Supporto della sottoscrizione

Azure Information Protection supporta livelli diversi di sottoscrizioni:

- Azure Information Protection P2: supporta tutte le funzionalità di classificazione, etichettatura e protezione.

- Azure Information Protection P1: supporta la maggior parte delle funzionalità di classificazione, etichettatura e protezione, ad eccezione della classificazione automatica o di HYOK.

- Office 365 con il servizio Azure Rights Management: supporta le funzionalità di protezione, ma non quelle di classificazione ed etichettatura.

Le opzioni che richiedono una sottoscrizione di Azure Information Protection P2 sono identificate nel portale.

Se l'organizzazione dispone di varie sottoscrizioni, è responsabilità dell'organizzazione assicurarsi che gli utenti non usino funzionalità non concesse in licenza per l'uso al loro account. Il client Azure Information Protection non gestisce il controllo e l'applicazione delle licenze. Quando si configurano opzioni per le quali non tutti gli utenti hanno una licenza, usare criteri con ambito o un'impostazione del Registro di sistema per garantire che l'organizzazione mantenga la conformità con le licenze:

- **Se l'organizzazione dispone di una combinazione di licenze di Azure Information Protection P1 e Azure Information Protection P2**: per gli utenti con licenza P2, creare e usare uno o più [criteri con ambito](configure-policy-scope.md) quando si configurano le opzioni che richiedono una licenza di Azure Information Protection P2. Assicurarsi che i criteri globali non contengano opzioni che richiedono una licenza di Azure Information Protection P2.

- **Se l'organizzazione dispone di una sottoscrizione di Azure Information Protection, ma alcuni utenti hanno solo una licenza per Office 365 che include il servizio Azure Rights Management**: modificare il Registro di sistema nei computer degli utenti che non hanno una licenza di Azure Information Protection, in modo che non scarichino i criteri di Azure Information Protection. Per istruzioni, vedere la personalizzazione seguente nella guida per l'amministratore: [Applicare la modalità di sola protezione quando l'organizzazione dispone di licenze miste](./rms-client/client-admin-guide-customizations.md#enforce-protection-only-mode-when-your-organization-has-a-mix-of-licenses).

Per altre informazioni sulle sottoscrizioni, vedere [Quale sottoscrizione è necessaria per Azure Information Protection e quali funzionalità sono incluse?](faqs.md#what-subscription-do-i-need-for-azure-information-protection-and-what-features-are-included)

## <a name="signing-in-to-the-azure-portal"></a>Accesso al portale di Azure

Per accedere al portale di Azure per configurare e gestire Azure Information Protection:

- Usare il collegamento seguente: https://portal.azure.com

- Usare un account che dispone di uno dei seguenti [ruoli di amministratore](/azure/active-directory/active-directory-assign-admin-roles-azure-portal):
    
    - **Amministratore di Information Protection**

    - **Amministratore della sicurezza**

    - **Amministratore globale / Amministratore società**


## <a name="to-access-the-azure-information-protection-blade-for-the-first-time"></a>Per accedere al pannello Azure Information Protection per la prima volta

1. Accedere al portale di Azure.

2. Nel menu dell'hub selezionare **Crea una risorsa** e quindi nella casella di ricerca per il Marketplace digitare **Azure Information Protection**. 
    
3. Selezionare **Azure Information Protection** nell'elenco dei risultati. Nel pannello **Azure Information Protection** fare clic su **Crea**.
    
    > [!TIP] 
    > Facoltativamente, selezionare **Aggiungi al dashboard** per creare un riquadro **Azure Information Protection** nel dashboard, in modo da ignorare la ricerca del servizio al successivo accesso al portale.
    
    Fare di nuovo clic su **Crea**.

4. Quando ci si connette al servizio per la prima volta viene visualizzata automaticamente la pagina **Avvio rapido**. Consultare le risorse suggerite o usare le altre opzioni di menu. Usare la procedura seguente per configurare le etichette selezionabili dagli utenti.

Quando si accede di nuovo al pannello **Azure Information Protection** viene selezionata automaticamente l'opzione **Etichette**, che consente di visualizzare e configurare etichette per tutti gli utenti. È possibile tornare alla pagina **Avvio rapido** selezionandola nel menu **GENERALE**.

## <a name="how-to-configure-the-azure-information-protection-policy"></a>Come configurare i criteri di Azure Information Protection

1. Assicurarsi di avere eseguito l'accesso al portale di Azure usando uno di questi ruoli amministrativi: Amministratore di Information Protection, Amministratore della sicurezza o Amministratore globale. Vedere la [sezione precedente](#signing-in-to-the-azure-portal) per altre informazioni su questi ruoli amministrativi.

2. Se necessario, passare al pannello **Azure Information Protection**: ad esempio, nel menu hub fare clic su **Tutti i servizi** e iniziare a digitare **Information Protection** nella casella Filtro. Selezionare **Azure Information Protection** nei risultati. 
    
    Il pannello **Azure Information Protection - Etichette** viene aperto automaticamente per consentire la visualizzazione e la modifica delle etichette esistenti. Le etichette possono essere rese disponibili per tutti gli utenti, per utenti selezionati o per nessun utente, aggiungendole o rimuovendole da un criterio.

3. Per visualizzare e modificare i criteri, selezionare **Criteri** nelle opzioni di menu. Per visualizzare e modificare il criterio ottenuto da tutti gli utenti, selezionare il criterio **Globale**. Per creare un criterio personalizzato per gli utenti selezionati, selezionare **Aggiungi un nuovo criterio**.
    

### <a name="overview-of-the-policy"></a>Panoramica dei criteri

Un criterio di Azure Information Protection contiene gli elementi seguenti che è possibile configurare:
    
- Etichette incluse che consentono ad amministratori e utenti di classificare (e, facoltativamente, proteggere) documenti e messaggi di posta elettronica.

- Titolo e descrizione comando della barra Information Protection visualizzata nelle applicazioni di Office.

- Opzione per impostare un'etichetta predefinita come punto di partenza per la classificazione di documenti e messaggi di posta elettronica.

- Opzione per applicare la classificazione quando gli utenti salvano documenti e inviano messaggi di posta elettronica.

- Opzione per richiedere agli utenti di specificare un motivo quando selezionano un'etichetta con un livello di riservatezza inferiore rispetto all'originale.

- Opzione per etichettare automaticamente un messaggio di posta elettronica, in base ai relativi allegati.

- Opzione per controllare se la barra di Information Protection viene visualizzata nelle applicazioni di Office.

- Opzione per controllare se il pulsante Non inoltrare viene visualizzato in Outlook.

- Opzione per consentire agli utenti di specificare le proprie autorizzazioni per i documenti.

- Opzione per fornire un collegamento alla guida personalizzata per gli utenti.

Azure Information Protection viene distribuito con [criteri predefiniti](configure-policy-default.md), che contengono cinque etichette principali. Due di queste etichette contengono etichette secondarie che forniscono sottocategorie in caso di necessità. Quando un'etichetta è configurata con etichette secondarie, gli utenti non possono selezionare l'etichetta principale ma devono selezionare una delle etichette secondarie.

Le etichette di Azure Information Protection possono essere usate con l'intera gamma di dati che in genere vengono creati e archiviati da un'organizzazione, dalla classificazione minima per i dati personali alla classificazione più elevata per dati particolarmente riservati. 

È possibile usare le etichette predefinite così come sono oppure personalizzarle, eliminarle e crearne di nuove. Per altre informazioni, usare i collegamenti nella sezione successiva per individuare le opzioni rilevanti e sapere come configurarle.

È possibile creare qualsiasi numero di etichette. Tuttavia, se le etichette diventano troppo numerose e non consentono agli utenti di individuare e selezionare l'etichetta appropriata con facilità, creare criteri con ambito in modo che gli utenti visualizzino solo le etichette rilevanti. Il limite massimo di etichette per l'applicazione della protezione è 500.

Quando si apportano modifiche in un pannello di Azure Information Protection, fare clic su **Save** (Salva) per salvare le modifiche oppure su **Discard** (Ignora) per ripristinare le ultime impostazioni salvate. Quando si salvano le modifiche a un criterio o si apportano modifiche alle etichette aggiunte ai criteri, le modifiche vengono pubblicate automaticamente. Non è presente un'opzione di pubblicazione separata.

Il client Azure Information Protection verifica la disponibilità di eventuali modifiche ogni volta che viene avviata un'applicazione di Office supportata e scarica le modifiche come criteri di Azure Information Protection più recenti. I criteri del client vengono aggiornati anche nei modi seguenti:

- Quando si fa clic con il pulsante destro del mouse per classificare e proteggere un file o una cartella.

- Quando si eseguono i [cmdlet di PowerShell](./rms-client/client-admin-guide-powershell.md) per l'etichettatura e la protezione (Get-AIPFileStatus, Set-AIPFileClassification e Set-AIPFileLabel).

- Ogni 24 ore.

- Per lo [scanner di Azure Information Protection](deploy-aip-scanner.md): all'avvio del servizio (se il criterio è antecedente a un'ora) e ogni ora durante le operazioni.


>[!NOTE]
>Quando il client scarica i criteri, prevedere un'attesa di alcuni minuti prima che ritorni completamente operativo. Il tempo effettivo varia a seconda di fattori quali le dimensioni e la complessità della configurazione dei criteri e la connettività di rete. Se l'azione risultante delle etichette non corrisponde alle ultime modifiche, attendere fino a 15 minuti e riprovare.

### <a name="configuring-your-organizations-policy"></a>Configurazione dei criteri dell'organizzazione

Usare le informazioni seguenti per configurare i criteri di Azure Information Protection:

- [Criteri predefiniti di Information Protection](configure-policy-default.md)

- [Come configurare le impostazioni dei criteri](configure-policy-settings.md)

- [Come creare una nuova etichetta](configure-policy-new-label.md)

- [Come aggiungere o rimuovere un'etichetta](configure-policy-add-remove-label.md)
 
- [Come eliminare o riordinare un'etichetta](configure-policy-delete-reorder.md)

- [Come modificare o personalizzare un'etichetta esistente](configure-policy-change-label.md)

- [Come configurare un'etichetta per la protezione](configure-policy-protection.md)

- [Come configurare un'etichetta per applicare i contrassegni visivi](configure-policy-markings.md)

- [Come configurare le condizioni per la classificazione automatica e consigliata](configure-policy-classification.md)

- [Come configurare i criteri per utenti specifici con i criteri con ambito](configure-policy-scope.md)

- [Come configurare e gestire i modelli](configure-policy-templates.md)

- [Come configurare etichette per lingue diverse](configure-policy-languages.md)

## <a name="next-steps"></a>Passaggi successivi

Per un esempio di come personalizzare i criteri predefiniti e osservare il comportamento risultante in un'applicazione di Office, seguire l'[Esercitazione introduttiva di Azure Information Protection](infoprotect-quick-start-tutorial.md).
