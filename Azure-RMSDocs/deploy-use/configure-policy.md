---
title: Configurare i criteri di Azure Information Protection
description: "Per configurare le funzioni di classificazione, aggiunta di etichette e protezione, è necessario configurare i criteri di Azure Information Protection."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 07/31/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: ba0e8119-886c-4830-bd26-f98fb14b2933
ms.reviewer: eymanor
ms.suite: ems
ms.openlocfilehash: 88843833b87eb054f534a7c85e6a7c2e52797e9b
ms.sourcegitcommit: 55a71f83947e7b178930aaa85a8716e993ffc063
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/31/2017
---
# <a name="configuring-azure-information-protection-policy"></a>Configurazione dei criteri di Azure Information Protection

>*Si applica a: Azure Information Protection*

Per configurare le funzioni di classificazione, aggiunta di etichette e protezione, è necessario configurare i criteri di Azure Information Protection. Questi criteri vengono quindi scaricati nei computer in cui è installato il [client di Azure Information Protection](https://www.microsoft.com/en-us/download/details.aspx?id=53018).

## <a name="subscription-support"></a>Supporto della sottoscrizione

I criteri di Azure Information Protection supportano vari livelli di sottoscrizioni:

- Azure Information Protection P2: supporta tutte le funzionalità di classificazione, etichettatura e protezione.

- Azure Information Protection P1: supporta la maggior parte delle funzionalità di classificazione, etichettatura e protezione, ad eccezione della classificazione automatica o di HYOK.

- Office 365 con il servizio Azure Rights Management: supporta le funzionalità di protezione, ma non quelle di classificazione ed etichettatura.

Le opzioni che richiedono una sottoscrizione di Azure Information Protection P2 sono ora identificate nel portale.

Se per gli utenti del tenant esiste una combinazione di sottoscrizioni , è necessario verificare che i criteri di Azure Information Protection scaricati dagli utenti non contengano opzioni non concesse in licenza ai relativi account. Quando si configurano opzioni non concesse in licenza a tutti gli utenti, usare criteri con ambito in modo che gli utenti non siano configurati per usare le funzionalità per le quali hanno una licenza.

Per altre informazioni sulle sottoscrizioni, vedere [Quale sottoscrizione è necessaria per Azure Information Protection e quali funzionalità sono incluse?](../get-started/faqs.md#what-subscription-do-i-need-for-azure-information-protection-and-what-features-are-included)

Per altre informazioni su come configurare i criteri di ambito, vedere [Come configurare i criteri di Azure Information Protection per utenti specifici con i criteri con ambito](configure-policy-scope.md).

## <a name="how-to-configure-the-azure-information-protection-policy"></a>Come configurare i criteri di Azure Information Protection

1. In una nuova finestra del browser accedere al [portale di Azure](https://portal.azure.com) come amministratore globale o della sicurezza.

2. Passare al pannello **Azure Information Protection**: ad esempio, nel menu hub fare clic su **More services** (Altri servizi) e iniziare a digitare **Information Protection** nella casella Filtro. Selezionare **Azure Information Protection** nei risultati. 
    
    Quando ci si connette al servizio per la prima volta, si apre automaticamente la pagina **Avvio rapido**. Per configurare i criteri ottenuti da tutti gli utenti, fare clic su **Criteri globali** per aprire il pannello **Criteri: globali**. Questo pannello si aprirà automaticamente per le connessioni successive al servizio in modo che sia possibile visualizzare e modificare i criteri globali ottenuti da tutti gli utenti. 
    
    I criteri di Azure Information Protection contengono gli elementi seguenti che è possibile configurare:
    
    - Etichette che consentono agli utenti di classificare i documenti e i messaggi di posta elettronica.
    
    - Titolo e descrizione comando della barra Information Protection visualizzata nelle applicazioni di Office.
    
    - Opzione per applicare la classificazione quando gli utenti salvano documenti e inviano messaggi di posta elettronica.
    
    - Opzione per impostare un'etichetta predefinita come punto di partenza per la classificazione di documenti e messaggi di posta elettronica.
    
    - Opzione per richiedere agli utenti di specificare un motivo quando selezionano un'etichetta con un livello di riservatezza inferiore rispetto all'originale.
    
    - Opzione per etichettare automaticamente un messaggio di posta elettronica, in base ai relativi allegati.
    
    - Opzione per fornire un collegamento alla guida personalizzata per gli utenti.

Azure Information Protection viene distribuito con [criteri predefiniti](configure-policy-default.md), che contengono cinque etichette principali. Queste etichette sono utilizzabili con l'intera gamma di dati che un'organizzazione in genere crea e archivia, dalla classificazione minima dei dati personali alla classificazione più elevata di dati particolarmente riservati. 

È possibile usare le etichette predefinite così come sono oppure personalizzarle, eliminarle e crearne di nuove. Per altre informazioni, usare i collegamenti nella sezione successiva per individuare le opzioni rilevanti e sapere come configurarle. 

Quando si apportano modifiche in un pannello di Azure Information Protection, fare clic su **Save** (Salva) per salvare le modifiche oppure su **Discard** (Ignora) per ripristinare le ultime impostazioni salvate. 

Dopo avere apportato le modifiche desiderate, fare clic su **Publish** (Pubblica). 

Il client Azure Information Protection verifica la disponibilità di eventuali modifiche ogni volta che viene avviata un'applicazione di Office supportata e scarica le modifiche come criteri di Azure Information Protection più recenti. I criteri del client vengono aggiornati anche nei modi seguenti:

- Quando si fa clic con il pulsante destro del mouse per classificare e proteggere un file o una cartella.

- Quando si eseguono i [cmdlet di PowerShell](../rms-client/client-admin-guide-powershell.md) per l'etichettatura e la protezione (Get-AIPFileStatus, Set-AIPFileClassification e Set-AIPFileLabel).

- Ogni 24 ore.

>[!NOTE]
>Quando il client scarica i criteri, prevedere un'attesa di alcuni minuti prima che ritorni completamente operativo. Il tempo effettivo varia a seconda di fattori quali le dimensioni e la complessità della configurazione dei criteri e la connettività di rete. Se l'azione risultante delle etichette non corrisponde alle ultime modifiche, attendere fino a 15 minuti e riprovare.

### <a name="configuring-your-organizations-policy"></a>Configurazione dei criteri dell'organizzazione

Usare le informazioni seguenti per configurare i criteri di Azure Information Protection:

- [Criteri predefiniti di Information Protection](configure-policy-default.md)

- [Come configurare le impostazioni dei criteri](configure-policy-settings.md)

- [Come creare una nuova etichetta](configure-policy-new-label.md)

- [Come eliminare o riordinare un'etichetta](configure-policy-delete-reorder.md)

- [Come modificare o personalizzare un'etichetta esistente](configure-policy-change-label.md)

- [Come configurare un'etichetta per la protezione](configure-policy-protection.md)

- [Come configurare un'etichetta per applicare i contrassegni visivi](configure-policy-markings.md)

- [Come configurare le condizioni per la classificazione automatica e consigliata](configure-policy-classification.md)

- [Come configurare i criteri per utenti specifici con i criteri con ambito](configure-policy-scope.md)

- [Come configurare e gestire i modelli](configure-policy-templates.md)

- [Come configurare etichette per lingue diverse](configure-policy-languages.md)

## <a name="next-steps"></a>Passaggi successivi

Per un esempio di come personalizzare i criteri predefiniti e osservare il comportamento risultante in un'applicazione di Office, seguire l'[Esercitazione introduttiva di Azure Information Protection](../get-started/infoprotect-quick-start-tutorial.md).

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
