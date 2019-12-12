---
title: Configurare le condizioni per un'etichetta di Azure Information Protection - AIP
description: Le condizioni per un'etichetta consentono di assegnare automaticamente un'etichetta a un documento o messaggio di posta elettronica. In alternativa, è possibile richiedere agli utenti di selezionare un'etichetta consigliata.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 10/14/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: e915f959-eafb-4375-8d2c-2f312edf2d29
ms.subservice: aiplabels
ms.custom: admin
ms.openlocfilehash: fce6fc49c830a1eb009d590ca124028810f663ee
ms.sourcegitcommit: 474cd033de025bab280cb7a9721ac7ffc2d60b55
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/05/2019
ms.locfileid: "73559592"
---
# <a name="how-to-configure-conditions-for-automatic-and-recommended-classification-for-azure-information-protection"></a>Come configurare le condizioni per la classificazione automatica e consigliata per Azure Information Protection

>*Si applica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*
>
> *Istruzioni per: [client di Azure Information Protection per Windows](faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*

> [!NOTE]
> Queste istruzioni si applicano al client Azure Information Protection (classico) e non al client per l'etichettatura unificata di Azure Information Protection. Non si è certi della differenza tra questi client? Vedere queste [domande frequenti](faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client).
> 
> Per informazioni su come configurare la classificazione automatica e consigliata per il client Unified Labeling, vedere la documentazione di Office. Ad esempio, [applicare automaticamente un'etichetta di riservatezza al contenuto](/microsoft-365/compliance/apply-sensitivity-label-automatically).

Quando si configurano le condizioni per un'etichetta, è possibile assegnare automaticamente un'etichetta a un documento o messaggio di posta elettronica. In alternativa, è possibile richiedere agli utenti di selezionare l'etichetta consigliata. 

Quando si configurano queste condizioni è possibile usare schemi predefiniti come **Numero della carta di credito** o **USA Social Security Number (SSN)** (Social Security Number - USA). In alternativa, è possibile definire una stringa o un modello personalizzato come condizione per la classificazione automatica. Queste condizioni si applicano al corpo del testo nei documenti e nei messaggi di posta elettronica, alle intestazioni e ai piè di pagina. Per altre informazioni sulle condizioni, vedere il passaggio 5 nella [procedura seguente](#to-configure-recommended-or-automatic-classification-for-a-label).

Per ottenere la migliore esperienza utente e garantire la continuità aziendale, è consigliabile iniziare con la classificazione consigliata dall'utente anziché quella automatica. Con questa configurazione gli utenti possono accettare la classificazione e la protezione associata o ignorare questi suggerimenti se non sono adatti al messaggio di posta elettronica o al documento in questione.

Ecco un esempio di richiesta quando si configura una condizione per l'applicazione di un'etichetta come azione consigliata, con un suggerimento di criterio personalizzato:

![Rilevamento e indicazione di Azure Information Protection](./media/info-protect-recommend-calloutsv2.png)

In questo esempio l'utente può fare clic su **Change now** (Cambia adesso) per applicare l'etichetta consigliata oppure ignorare il suggerimento selezionando **Dismiss** (Ignora). Se l'utente sceglie di ignorare il suggerimento e alla successiva apertura del documento la condizione è ancora applicabile, l'indicazione per l'etichetta viene visualizzata nuovamente.

Se si configura la classificazione automatica anziché consigliata, l'etichetta viene applicata automaticamente e l'utente visualizza comunque una notifica in Word, Excel e PowerPoint. Tuttavia, i pulsanti **modifica ora** e **Ignora** sono sostituiti con **OK**. In Outlook non viene inviata alcuna notifica per la classificazione automatica e l'etichetta viene applicata al momento dell'invio del messaggio di posta elettronica.

> [!IMPORTANT]
>Non configurare un'etichetta per la classificazione automatica e un'autorizzazione definita dall'utente. L'opzione per le autorizzazioni definite dall'utente è un'[impostazione di protezione](configure-policy-protection.md) che consente agli utenti di specificare a chi vengono concesse le autorizzazioni.
>
>Quando un'etichetta viene configurata per la classificazione automatica e per le autorizzazioni definite dall'utente, il contenuto viene verificato in base alle condizioni e l'impostazione di autorizzazione definita dall'utente non viene applicata. È possibile usare la classificazione e le autorizzazioni definite dall'utente consigliate.

## <a name="how-automatic-or-recommended-labels-are-applied"></a>Come vengono applicate le etichette di elaborazione automatica o consigliata

- La classificazione automatica si applica a Word, Excel e PowerPoint quando si salvano i documenti e si applica a Outlook quando si inviano messaggi di posta elettronica. 
    
    Non è possibile usare la classificazione automatica per documenti e messaggi di posta elettronica che in precedenza sono stati etichettati manualmente o automaticamente con una classificazione superiore. 

- La classificazione consigliata si applica a Word, Excel e PowerPoint quando si salvano i documenti. È possibile usare la classificazione consigliata per Outlook solo se si configura un'[impostazione client avanzata](./rms-client/client-admin-guide-customizations.md#enable-recommended-classification-in-outlook) attualmente in anteprima.
    
    Non è possibile usare la classificazione consigliata per documenti che sono stati etichettati in precedenza con una classificazione superiore. 

È possibile modificare questo comportamento in modo che il client Azure Information Protection verifichi periodicamente nei documenti le regole di condizione specificate. Questo, ad esempio, sarebbe appropriato se si usa il [salvataggio](https://support.office.com/article/what-is-autosave-6d6bd723-ebfd-4e40-b5f6-ae6e8088f7a5) automatico con le app di Office salvate automaticamente in SharePoint Online, OneDrive o OneDrive for business. Per supportare questo scenario, è possibile configurare un' [impostazione client avanzata](./rms-client/client-admin-guide-customizations.md#turn-on-classification-to-run-continuously-in-the-background) attualmente in anteprima. L'impostazione attiva la classificazione affinché venga eseguita in modo continuo in background.

### <a name="how-multiple-conditions-are-evaluated-when-they-apply-to-more-than-one-label"></a>Come vengono valutate più condizioni quando si applicano a più di un'etichetta

1. Le etichette sono ordinate per la valutazione, in base alla relativa posizione specificata nel criterio: l'etichetta posizionata per prima occupa la posizione più bassa (minore riservatezza) e l'etichetta posizionata per ultima occupa la posizione più alta (massima riservatezza).

2. Viene applicata l'etichetta per la massima riservatezza.
 
3. Viene applicata l'ultima etichetta secondaria.


## <a name="to-configure-recommended-or-automatic-classification-for-a-label"></a>Per configurare la classificazione consigliata o automatica per un'etichetta

1. Se non è già stato fatto, aprire una nuova finestra del browser e [accedere al portale di Azure](configure-policy.md#signing-in-to-the-azure-portal). Passare quindi al riquadro **Azure Information Protection**. 
    
    Ad esempio, nella casella di ricerca per risorse, servizi e documenti: iniziare a digitare **informazioni** e selezionare **Azure Information Protection**.

2. Dall'opzione di menu **classificazioni** > **etichette** : nel riquadro **etichette Azure Information Protection** selezionare l'etichetta da configurare.

3. Nel riquadro **etichetta** , nella sezione **configurare le condizioni per l'applicazione automatica di questa etichetta** , fare clic su **Aggiungi una nuova condizione**.

4. Nel riquadro **condizione** selezionare tipi di **informazioni** se si vuole usare una condizione predefinita oppure **personalizzata** se si vuole specificare il proprio:
    - Per **Tipi di informazioni** selezionare una delle condizioni disponibili nell'elenco, quindi selezionare il numero minimo di occorrenze e specificare se l'occorrenza deve avere un valore univoco per essere inclusa nel conteggio delle occorrenze.
        
        I tipi di informazioni usano il rilevamento di modelli e i tipi di informazioni riservate della prevenzione perdita dei dati (DLP) di Office 365. È possibile scegliere tra vari tipi di informazioni riservate comuni. Alcuni tipi sono specifici per determinate aree. Per altre informazioni, vedere [Elementi cercati dai tipi di informazioni riservate](/microsoft-365/compliance/what-the-sensitive-information-types-look-for) nella documentazione di Office 365.
        
        L'elenco dei tipi di informazioni selezionabili nel portale di Azure viene aggiornato periodicamente per includere i nuovi tipi aggiunti a DLP di Office. L'elenco esclude tuttavia i tipi di informazioni riservate specificati dall'utente e caricati come pacchetto di regole nel Centro sicurezza e conformità di Office 365.
        
        > [!IMPORTANT]
        > Alcuni tipi di informazioni richiedono una versione minima del client. [Altre informazioni](#sensitive-information-types-that-require-a-minimum-version-of-the-client) 
        
        Quando Azure Information Protection valuta i tipi di informazioni selezionati non usa l'impostazione del livello di attendibilità DLP di Office, ma ricerca corrispondenze in base al livello di attendibilità più basso.
    
    - Per **Custom** (Personalizzata), specificare un nome e una frase di cui cercare la corrispondenza, esclusi i punti interrogativi e i caratteri speciali. Quindi specificare se usare un'espressione regolare per la corrispondenza, se la distinzione tra maiuscole e minuscole è rilevante, il numero minimo di occorrenze e se l'occorrenza deve avere un valore univoco per essere inclusa nel conteggio delle occorrenze.
        
        Le espressioni regolari usano i criteri di espressione regolare di Office 365. Per informazioni su come specificare espressioni regolari per le condizioni personalizzate, vedere la seguente versione specifica della [sintassi delle espressioni regolari Perl](https://www.boost.org/doc/libs/1_37_0/libs/regex/doc/html/boost_regex/syntax/perl_syntax.html) da Boost.
        
5. Decidere se modificare i valori **Numero minimo di occorrenze** e **Conta solo le occorrenze con valori univoci**, quindi selezionare **Salva**. 
    
    Esempio per le opzioni relative alle occorrenze: si seleziona il tipo di informazioni per il codice fiscale, si imposta il numero minimo di occorrenze su 2 e in un documento compare due volte lo stesso codice fiscale. Se si imposta **Conta solo le occorrenze con valori univoci** su **Sì**, la condizione non è soddisfatta. Se invece si imposta questa opzione su **No**, la condizione è soddisfatta.

6. Tornare al riquadro **etichetta** , configurare gli elementi seguenti e quindi fare clic su **Save (Salva**):
    
    - Scegliere la classificazione automatica o consigliata: per **Select how this label is applied: automatically or recommended to user** (Selezionare come applicare l'etichetta: automaticamente o consigliata all'utente) selezionare **Automatic** (Automatica) o **Recommended** (Consigliata).
    
    - Specificare il testo per la richiesta utente o il suggerimento di criteri: mantenere il testo predefinito o specificare una stringa personalizzata.

Quando fa clic su **Salva**, le modifiche diventano automaticamente disponibili per utenti e servizi. Non è più presente un'opzione di pubblicazione separata.

### <a name="sensitive-information-types-that-require-a-minimum-version-of-the-client"></a>Tipi di informazioni riservate che richiedono una versione minima del client

Per i seguenti tipi di informazioni riservate è richiesta una versione minima di [1.48.204.0](./rms-client/client-version-release-history.md#version-1482040) del client Azure Information Protection:

- **Stringa di connessione del bus di servizio di Azure**
- **Stringa di connessione di Azure IoT**
- **Account di archiviazione di Azure**
- **Stringa di connessione del database IaaS di Azure e stringa di connessione di SQL di Azure**
- **Stringa di connessione di Cache Redis di Azure**
- **Azure SAS**
- **Stringa di connessione di SQL Server**
- **Chiave di autenticazione di Azure DocumentDB**
- **Password delle impostazioni di pubblicazione di Azure**
- **Chiave dell'account di archiviazione di Azure (generico)**

Per ulteriori informazioni su questi tipi di informazioni riservate, vedere il post di Blog seguente: [Azure Information Protection aiuta a garantire una maggiore sicurezza tramite l'individuazione automatica delle credenziali](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/Azure-Information-Protection-helps-you-to-be-more-secure-by/ba-p/360181)

Inoltre, a partire da 1.48.204.0 del client Azure Information Protection, i tipi di informazioni sensibili seguenti non sono supportati e non vengono più visualizzati nel portale di Azure. Se sono presenti etichette che usano questi tipi di informazioni riservate, è consigliabile rimuoverle perché non è possibile garantire il rilevamento corretto e i relativi riferimenti nei report dello scanner devono essere ignorati:

- **Numero di telefono EU**
- **Coordinate GPS EU**

## <a name="next-steps"></a>Passaggi successivi

È consigliabile distribuire lo [scanner di Azure Information Protection](deploy-aip-scanner.md), che può usare le regole di classificazione automatica per trovare, classificare e proteggere i file in condivisioni di rete e archivi di file locali.  

Per altre informazioni sulla configurazione dei criteri di Azure Information Protection, usare i collegamenti nella sezione [Configurazione dei criteri dell'organizzazione](configure-policy.md#configuring-your-organizations-policy).
