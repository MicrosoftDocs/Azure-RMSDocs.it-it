---
title: Configurare etichette per lingue diverse in Azure Information Protection
description: È possibile aggiungere il supporto di varie lingue per le etichette che gli utenti visualizzano sulla barra di Information Protection e per i modelli visualizzati dagli utenti, specificando le lingue nei criteri di Azure Information Protection e importando le traduzioni.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 09/28/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: a0e89fd0-795b-4e7a-aea9-ff6fc9163bde
ms.subservice: aiplabels
ms.custom: admin
ms.openlocfilehash: e1f5b3c05ae7e8c0717ef4d0227eacda8eeade3e
ms.sourcegitcommit: f14ec329cef1967d2d66b0d550501449ee55abf9
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/29/2019
ms.locfileid: "71673910"
---
# <a name="how-to-configure-labels-and-templates-for-different-languages-in-azure-information-protection"></a>Come configurare etichette e modelli per varie lingue in Azure Information Protection

>*Si applica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*
>
> *Istruzioni per: [Client Azure Information Protection per Windows](faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*

> [!NOTE]
> Queste istruzioni sono valide per il client Azure Information Protection (classico) e non per il client di Azure Information Protection Unified labeling. Non si è certi della differenza tra questi client? Vedere queste [domande frequenti](faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client).
> 
> Se si cercano informazioni per configurare lingue diverse per le etichette di riservatezza, usare Office 365 Sicurezza e conformità PowerShell e il parametro *LocaleSettings* per [set-label](https://docs.microsoft.com/powershell/module/exchange/policy-and-compliance/set-label?view=exchange-ps).

Anche se le etichette predefinite per Azure Information Protection supportano più lingue, è necessario configurare il supporto per i nomi di etichetta e le descrizioni specificate. Per questa configurazione è necessario:

1. Selezionare le lingue usate dagli utenti. 

2. Esportare i nomi di etichetta e le descrizioni correnti in un file.

3. Modificare il file specificando le traduzioni.

4. Reimportare il file nei criteri di Azure Information Protection.

È anche possibile configurare modelli per varie lingue quando è vera una delle condizioni seguenti. Questa configurazione è idonea se gli utenti o gli amministratori hanno l'esigenza di vedere il nome e la descrizione del modello corrente nella lingua localizzata.

- Il modello è stato creato nel portale di Azure classico o con PowerShell e il modello non è collegato a un'etichetta mediante l'impostazione di protezione **Seleziona un modello predefinito**.

- Non si dispone di una sottoscrizione che supporta le etichette, pertanto è possibile creare e gestire i modelli solo nel portale di Azure.

Selezionare le lingue che corrispondono alle impostazioni lingua degli utenti per Office e Windows. Tali nomi e descrizioni di etichette vengono poi visualizzati rispettivamente nella barra di Azure Information Protection nelle app di Office e nella finestra di dialogo **Classifica e proteggi - Azure Information Protection**. Per altre informazioni su quale lingua venga scelta, vedere la sezione [Come il client di Azure Information Protection determina la lingua da visualizzare](#how-the-azure-information-protection-client-determines-the-language-to- display) in questa pagina. 

## <a name="to-configure-labels-and-templates-for-different-languages"></a>Per configurare etichette e modelli per lingue diverse

1. Se non è già stato fatto, aprire una nuova finestra del browser e [accedere al portale di Azure](configure-policy.md#signing-in-to-the-azure-portal). Quindi passare al pannello **Azure Information Protection**.
    
    Ad esempio, dal menu hub fare clic su **Tutti i servizi** e iniziare a digitare **Informazioni** nella casella Filtro. Selezionare **Azure Information Protection**.

2. Dall'opzione di menu **Gestisci** > **Lingue**: Nel pannello **Azure Information Protection - Lingue** selezionare **Aggiungi una nuova lingua per la conversione**. Selezionare le lingue da aggiungere, quindi scegliere **OK**. È possibile digitare il nome della lingua nella casella di ricerca o scorrere l'elenco delle lingue disponibili.

3. Le lingue selezionate vengono visualizzate nel pannello **Azure Information Protection - Lingue**:
    
    - Per aggiungere un'altra lingua selezionare **Aggiungi una nuova lingua per la conversione** e ripetere il passaggio precedente. 
        
        > [!NOTE]
        > Assicurarsi di selezionare le lingue che gli utenti hanno per Office e per Windows. In alcuni casi potrebbe essere necessario eseguire due selezioni diverse per computer.
        
    - Nel caso in cui si voglia modificare la scelta di una lingua, selezionare una voce dall'elenco e fare clic su **Rimuovi**.

4. Quando tutte le lingue che si vuole supportare sono elencate, selezionare la casella di controllo accanto a **NOME LINGUA** per selezionare tutte le voci, o in alternativa, selezionare le singole voci, e fare clic su **Esporta** per salvare una copia locale dei nomi e delle descrizioni delle etichette esistenti in un file. 
    
    Il file scaricato viene denominato **exported localization.zip** e viene salvato nella cartella Download locale. È anche possibile accedere selezionando il nome del file nella barra di stato del portale di Azure.

5. Estrarre i file da **exported localization.zip** in modo da avere file con estensione xml per ogni lingua selezionata per il download. 

6. Modificare ogni file XML: per ogni stringa all'interno di tag `<LocalizedText>` immettere le traduzioni per ogni lingua scelta. 

7. Quando è stato modificato ogni file con estensione xml, creare una nuova cartella compressa contenente i file. La cartella compressa può avere qualsiasi nome, ma deve avere estensione zip.
    
    Suggerimento: Non è necessario attendere di completare la modifica di ogni file di lingua scaricato. Al contrario, è possibile distribuire lingue diverse in più fasi, includendo nel file ZIP un subset dei file totali scaricati. Dopo aver completato le traduzioni per più lingue, ripetere i passaggi 7 e 8.

8. Tornare al pannello **Azure Information Protection - Lingue** e selezionare **Importa**. Si noti che se questa opzione non è disponibile, è necessario deselezionare per prima cosa la casella di controllo **NOME LINGUA** o le caselle di controllo per le lingue selezionate singolarmente.
    
    Dopo il completamento dell'importazione i nomi e le descrizioni localizzati vengono scaricati per gli utenti.

È necessario ripetere questa procedura se è necessario per supportare una nuova lingua, creare nuove etichette o si modifica il nome o la descrizione delle etichette nel portale di Azure.

## <a name="how-the-azure-information-protection-client-determines-the-language-to-display"></a>Come il client di Azure Information Protection determina la lingua da visualizzare

Quando gli utenti scaricano un criterio di Azure Information Protection che supporta lingue diverse, la lingua con cui vengono visualizzati i nomi di etichetta e le descrizioni dei comandi per gli utenti è determinata dalla logica seguente:

**Per le etichette e le descrizioni dei comandi che gli utenti visualizzano sulla barra di Azure Information Protection nelle applicazioni Office:**

- Quando è presente una corrispondenza diretta con la lingua dell'app di Office, le descrizioni e i nomi delle etichette vengono visualizzati in tale lingua.

- Quando non è presente alcuna corrispondenza con la lingua dell'app di Office, le descrizioni e i nomi delle etichette vengono visualizzati nella lingua specificata per impostazione predefinita per tutti gli utenti. Tale lingua è in genere l'inglese, ovvero la lingua usata nel criterio predefinito.

**Per le etichette e le descrizioni dei comandi che gli utenti visualizzano quando usano il tasto destro del mouse per classificare e proteggere i file o le cartelle:**

- Quando c'è una corrispondenza diretta con la lingua del sistema operativo, le descrizioni e i nomi delle etichette vengono visualizzati in tale lingua.

- Quando non è presente alcuna corrispondenza con la lingua del sistema operativo, le descrizioni e i nomi delle etichette vengono visualizzati nella lingua specificata per impostazione predefinita per tutti gli utenti. Tale lingua è in genere l'inglese, ovvero la lingua usata nel criterio predefinito.

## <a name="when-localized-label-names-are-not-used"></a>Quando non vengono usati i nomi di etichetta localizzati

Negli scenari seguenti non vengono usati nomi di etichette, ed etichette secondarie, localizzati. Per garantire la coerenza nel tenant, per gli oggetti seguenti viene sempre usata la lingua predefinita:

- Log dell'uso del client

- PowerShell (output da Get-AIPFileStatus)

- Metadati documento e intestazioni di posta elettronica


## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sulle opzioni disponibili per le etichette e su altre configurazioni dei criteri di Azure Information Protection, usare i collegamenti nella sezione [Configurazione dei criteri dell'organizzazione](configure-policy.md#configuring-your-organizations-policy).



