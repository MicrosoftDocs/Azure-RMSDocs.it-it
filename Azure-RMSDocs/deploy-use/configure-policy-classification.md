---
title: Configurare le condizioni per un'etichetta di Azure Information Protection
description: Quando si configurano le condizioni per un'etichetta, è possibile assegnare automaticamente un'etichetta a un documento o messaggio di posta elettronica. In alternativa, è possibile richiedere agli utenti di selezionare l'etichetta consigliata.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 06/27/2018
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: e915f959-eafb-4375-8d2c-2f312edf2d29
ms.openlocfilehash: c7ef58cd42a793cacb3b64aec33d2cd0a0b105f4
ms.sourcegitcommit: 3f524c5af39bee39169f86d9c4e72c661c960d83
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/28/2018
ms.locfileid: "37068882"
---
# <a name="how-to-configure-conditions-for-automatic-and-recommended-classification-for-azure-information-protection"></a>Come configurare le condizioni per la classificazione automatica e consigliata per Azure Information Protection

>*Si applica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*

Quando si configurano le condizioni per un'etichetta, è possibile assegnare automaticamente un'etichetta a un documento o messaggio di posta elettronica. In alternativa, è possibile richiedere agli utenti di selezionare l'etichetta consigliata. 

Quando si configurano queste condizioni è possibile usare schemi predefiniti come **Numero della carta di credito** o **USA Social Security Number (SSN)** (Social Security Number - USA). In alternativa, è possibile definire una stringa o un modello personalizzato come condizione per la classificazione automatica. Queste condizioni si applicano al corpo del testo nei documenti e nei messaggi di posta elettronica, alle intestazioni e ai piè di pagina. Per altre informazioni sulle condizioni, vedere il passaggio 5 nella [procedura seguente](#to-configure-recommended-or-automatic-classification-for-a-label).

Per ottenere la migliore esperienza utente e garantire la continuità aziendale, è consigliabile iniziare con la classificazione consigliata dall'utente anziché quella automatica. Con questa configurazione gli utenti possono accettare la classificazione e la protezione associata o ignorare questi suggerimenti se non sono adatti al messaggio di posta elettronica o al documento in questione.

Ecco un esempio di richiesta quando si configura una condizione per l'applicazione di un'etichetta come azione consigliata, con un suggerimento di criterio personalizzato:

![Rilevamento e indicazione di Azure Information Protection](../media/info-protect-recommend-calloutsv2.png)

In questo esempio l'utente può fare clic su **Change now** (Cambia adesso) per applicare l'etichetta consigliata oppure ignorare il suggerimento selezionando **Dismiss** (Ignora). Se l'utente sceglie di ignorare il suggerimento e alla successiva apertura del documento la condizione è ancora applicabile, l'indicazione per l'etichetta viene visualizzata nuovamente. 

> [!IMPORTANT]
>Non configurare un'etichetta per la classificazione automatica e un'autorizzazione definita dall'utente. L'opzione per le autorizzazioni definite dall'utente è un'[impostazione di protezione](configure-policy-protection.md) che consente agli utenti di specificare a chi vengono concesse le autorizzazioni.
>
>Quando un'etichetta viene configurata per la classificazione automatica e per le autorizzazioni definite dall'utente, il contenuto viene verificato in base alle condizioni e l'impostazione di autorizzazione definita dall'utente non viene applicata. È possibile usare la classificazione e le autorizzazioni definite dall'utente consigliate.

## <a name="how-automatic-or-recommended-labels-are-applied"></a>Come vengono applicate le etichette di elaborazione automatica o consigliata

- La classificazione automatica si applica a Word, Excel e PowerPoint quando i documenti vengono salvati e a Outlook quando i messaggi di posta elettronica vengono inviati. 
    
    Non è possibile usare la classificazione automatica per documenti e messaggi di posta elettronica che in precedenza sono stati etichettati manualmente o automaticamente con una classificazione superiore. 

- La classificazione consigliata si applica a Word, Excel e PowerPoint quando i documenti vengono salvati. È possibile usare la classificazione consigliata per Outlook solo se si configura un'[impostazione client avanzata](../rms-client/client-admin-guide-customizations.md#enable-recommended-classification-in-outlook) attualmente in anteprima.
    
    Non è possibile usare la classificazione consigliata per documenti che sono stati etichettati in precedenza con una classificazione superiore. 

È possibile modificare questo comportamento in modo che il client Azure Information Protection verifichi periodicamente nei documenti le regole di condizione specificate. Per questa configurazione è necessaria un'[impostazione client avanzata](../rms-client/client-admin-guide-customizations.md#turn-on-classification-to-run-continuously-in-the-background), attualmente in anteprima.

### <a name="how-multiple-conditions-are-evaluated-when-they-apply-to-more-than-one-label"></a>Come vengono valutate più condizioni quando si applicano a più di un'etichetta

1. Le etichette sono ordinate per la valutazione, in base alla relativa posizione specificata nel criterio: l'etichetta posizionata per prima occupa la posizione più bassa (minore riservatezza) e l'etichetta posizionata per ultima occupa la posizione più alta (massima riservatezza).

2. Viene applicata l'etichetta per la massima riservatezza.
 
3. Viene applicata l'ultima etichetta secondaria.


## <a name="to-configure-recommended-or-automatic-classification-for-a-label"></a>Per configurare la classificazione consigliata o automatica per un'etichetta

1. Se non è già stato fatto, aprire una nuova finestra del browser e [accedere al portale di Azure](configure-policy.md#signing-in-to-the-azure-portal). Quindi passare al pannello **Azure Information Protection**. 
    
    Ad esempio, dal menu hub fare clic su **Tutti i servizi** e iniziare a digitare **Informazioni** nella casella Filtro. Selezionare **Azure Information Protection**.

2. Dall'opzione di menu **CLASSIFICAZIONI** > **Etichette**: nel pannello **Azure Information Protection - Etichette** selezionare l'etichetta che si vuole configurare.

3. Nel pannello **Etichetta**, nella sezione **Configurare le condizioni per l'applicazione automatica di questa etichetta**, fare clic su **Aggiungi una nuova condizione**.

4. Nel pannello **Condizione** selezionare **Tipi di informazioni** se si vuole usare una condizione predefinita oppure **Personalizzata** se si vuole specificare una condizione personalizzata:
    - Per **Tipi di informazioni** selezionare una delle condizioni disponibili nell'elenco, quindi selezionare il numero minimo di occorrenze e specificare se l'occorrenza deve avere un valore univoco per essere inclusa nel conteggio delle occorrenze.
        
        I tipi di informazioni usano il rilevamento di modelli e i tipi di informazioni riservate della prevenzione perdita dei dati (DLP) di Office 365. È possibile scegliere tra vari tipi di informazioni riservate comuni. Alcuni tipi sono specifici per determinate aree. Per altre informazioni, vedere [Elementi cercati dai tipi di informazioni riservate](https://support.office.com/article/What-the-sensitive-information-types-look-for-fd505979-76be-4d9f-b459-abef3fc9e86b) nella documentazione di Office.
        
        L'elenco dei tipi di informazioni selezionabili nel portale di Azure viene aggiornato periodicamente per includere i nuovi tipi aggiunti a DLP di Office. L'elenco esclude tuttavia i tipi di informazioni riservate specificati dall'utente e caricati come pacchetto di regole nel Centro sicurezza e conformità di Office 365. 
        
        Quando Azure Information Protection valuta i tipi di informazioni selezionati non usa l'impostazione del livello di attendibilità DLP di Office, ma ricerca corrispondenze in base al livello di attendibilità più basso.
    
    - Per **Custom** (Personalizzata), specificare un nome e una frase di cui cercare la corrispondenza, esclusi i punti interrogativi e i caratteri speciali. Quindi specificare se usare un'espressione regolare per la corrispondenza, se la distinzione tra maiuscole e minuscole è rilevante, il numero minimo di occorrenze e se l'occorrenza deve avere un valore univoco per essere inclusa nel conteggio delle occorrenze.
        
        Le espressioni regolari usano i criteri di espressione regolare di Office 365. Per altre informazioni, vedere [Definizione di corrispondenze basate su espressioni regolari](https://technet.microsoft.com/library/jj674702(v=exchg.150).aspx#Anchor_2) nella documentazione di Office. Inoltre, può risultare utile fare riferimento alla [sintassi delle espressioni regolari Perl](http://www.boost.org/doc/libs/1_66_0/libs/regex/doc/html/boost_regex/syntax/perl_syntax.html) da Boost.
        
5. Decidere se modificare i valori **Numero minimo di occorrenze** e **Conta solo le occorrenze con valori univoci**, quindi selezionare **Salva**. 
    
    Esempio per le opzioni relative alle occorrenze: si seleziona il tipo di informazioni per il codice fiscale, si imposta il numero minimo di occorrenze su 2 e in un documento compare due volte lo stesso codice fiscale. Se si imposta **Conta solo le occorrenze con valori univoci** su **Sì**, la condizione non è soddisfatta. Se invece si imposta questa opzione su **No**, la condizione è soddisfatta.

6. Tornare al pannello **Etichetta**, configurare le opzioni seguenti e quindi fare clic su **Salva**:
    
    - Scegliere la classificazione automatica o consigliata: per **Select how this label is applied: automatically or recommended to user** (Selezionare come applicare l'etichetta: automaticamente o consigliata all'utente) selezionare **Automatic** (Automatica) o **Recommended** (Consigliata).
    
    - Specificare il testo per la richiesta utente o il suggerimento di criteri: mantenere il testo predefinito o specificare una stringa personalizzata.

Quando fa clic su **Salva**, le modifiche diventano automaticamente disponibili per utenti e servizi. Non è più presente un'opzione di pubblicazione separata.

## <a name="next-steps"></a>Passaggi successivi

È consigliabile distribuire lo [scanner di Azure Information Protection](deploy-aip-scanner.md), che può usare le regole di classificazione automatica per trovare, classificare e proteggere i file in condivisioni di rete e archivi di file locali.  

Per altre informazioni sulla configurazione dei criteri di Azure Information Protection, usare i collegamenti nella sezione [Configurazione dei criteri dell'organizzazione](configure-policy.md#configuring-your-organizations-policy).

[!INCLUDE[Commenting house rules](../includes/houserules.md)]

