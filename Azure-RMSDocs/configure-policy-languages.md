---
title: Configurare etichette per lingue diverse in Azure Information Protection
description: È possibile aggiungere il supporto di varie lingue per le etichette che gli utenti visualizzano sulla barra di Information Protection e per i modelli visualizzati dagli utenti, specificando le lingue nei criteri di Azure Information Protection e importando le traduzioni.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 03/16/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: a0e89fd0-795b-4e7a-aea9-ff6fc9163bde
ROBOTS: NOINDEX
ms.subservice: aiplabels
ms.custom: admin
ms.openlocfilehash: f6a9f17a6679d9752f11b5209d9ce083c8ef8009
ms.sourcegitcommit: f6d536b6a3b5e14e24f0b9e58d17a3136810213b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/26/2021
ms.locfileid: "98809793"
---
# <a name="how-to-configure-labels-and-templates-for-different-languages-in-azure-information-protection"></a>Come configurare etichette e modelli per varie lingue in Azure Information Protection

>***Si applica a**: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*
>
>***Pertinente per**: [Azure Information Protection client classico per Windows](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients). Per il client di etichettatura unificata, vedere [informazioni sulle etichette di riservatezza](/microsoft-365/compliance/sensitivity-labels) dalla documentazione Microsoft 365. Per configurare lingue diverse per le etichette di riservatezza, usare il parametro *LocaleSettings* per il cmdlet [set-label](/powershell/module/exchange/policy-and-compliance/set-label) . *

> [!NOTE] 
> Per offrire un'esperienza per i clienti unificata e semplificata, il **client classico di Azure Information Protection** e **Gestione etichette** nel portale di Azure saranno **deprecati** a partire dal **31 marzo 2021**. In questo intervallo di tempo tutti i clienti correnti di Azure Information Protection possono passare alla soluzione di etichettatura unificata usando la piattaforma di etichettatura unificata di Microsoft Information Protection. Altre informazioni nell'[avviso ufficiale sulla deprecazione](https://aka.ms/aipclassicsunset).
>

Anche se le etichette predefinite per Azure Information Protection supportano più lingue, è necessario configurare il supporto per i nomi di etichetta e le descrizioni specificate. Per questa configurazione è necessario:

1. Selezionare le lingue usate dagli utenti. 

2. Esportare i nomi di etichetta e le descrizioni correnti in un file.

3. Modificare il file specificando le traduzioni.

4. Reimportare il file nei criteri di Azure Information Protection.

È anche possibile configurare modelli per varie lingue quando è vera una delle condizioni seguenti. Questa configurazione è idonea se gli utenti o gli amministratori hanno l'esigenza di vedere il nome e la descrizione del modello corrente nella lingua localizzata.

- Il modello è stato creato nel portale di Azure classico o con PowerShell e il modello non è collegato a un'etichetta mediante l'impostazione di protezione **Seleziona un modello predefinito**.

- Non si dispone di una sottoscrizione che supporta le etichette, pertanto è possibile creare e gestire i modelli solo nel portale di Azure.

Selezionare le lingue che corrispondono alle impostazioni lingua degli utenti per Office e Windows. Tali nomi e descrizioni di etichette vengono poi visualizzati rispettivamente nella barra di Azure Information Protection nelle app di Office e nella finestra di dialogo **Classifica e proteggi - Azure Information Protection**. Per altre informazioni su quale lingua venga scelta, vedere la sezione [Come il client di Azure Information Protection determina la lingua da visualizzare](#how-the-azure-information-protection-client-determines-the-language-to-display) in questa pagina. 

## <a name="to-configure-labels-and-templates-for-different-languages"></a>Per configurare etichette e modelli per lingue diverse

1. Aprire una nuova finestra del browser e accedere al [portale di Azure](configure-policy.md#signing-in-to-the-azure-portal), se questa operazione non è già stata eseguita. Quindi passare al riquadro **Azure Information Protection**.
    
    Ad esempio, nella casella di ricerca di risorse, servizi e documentazione: iniziare a digitare **Informazioni** e selezionare **Azure Information Protection**.

2. Dall'opzione di menu **Gestisci**  >  **linguaggi** : nel riquadro **Azure Information Protection-lingue** selezionare **Aggiungi una nuova lingua per la traduzione**. Selezionare le lingue da aggiungere, quindi scegliere **OK**. È possibile digitare il nome della lingua nella casella di ricerca o scorrere l'elenco delle lingue disponibili.

3. Le lingue selezionate ora vengono visualizzate nel riquadro **Azure Information Protection-lingue** :
    
    - Per aggiungere un'altra lingua selezionare **Aggiungi una nuova lingua per la conversione** e ripetere il passaggio precedente. 
        
        > [!NOTE]
        > Assicurarsi di selezionare le lingue che gli utenti hanno per Office e per Windows. In alcuni casi potrebbe essere necessario eseguire due selezioni diverse per computer.
        
    - Nel caso in cui si voglia modificare la scelta di una lingua, selezionare una voce dall'elenco e fare clic su **Rimuovi**.

4. Quando tutte le lingue che si vuole supportare sono elencate, selezionare la casella di controllo accanto a **NOME LINGUA** per selezionare tutte le voci, o in alternativa, selezionare le singole voci, e fare clic su **Esporta** per salvare una copia locale dei nomi e delle descrizioni delle etichette esistenti in un file. 
    
    Il file scaricato viene denominato **exported localization.zip** e viene salvato nella cartella Download locale. È anche possibile accedere selezionando il nome del file nella barra di stato del portale di Azure.

5. Estrarre i file da **exported localization.zip** in modo da avere file con estensione xml per ogni lingua selezionata per il download. 

6. Modificare ogni file con estensione xml: per ogni stringa all'interno di tag `<LocalizedText>`, immettere le traduzioni per ogni lingua scelta. 

7. Quando è stato modificato ogni file con estensione xml, creare una nuova cartella compressa contenente i file. La cartella compressa può avere qualsiasi nome, ma deve avere estensione zip.
    
    Suggerimento: non è necessario attendere fino a quando non è stato modificato ogni file di lingua scaricato. Al contrario, è possibile distribuire lingue diverse in più fasi, includendo nel file ZIP un subset dei file totali scaricati. Dopo aver completato le traduzioni per più lingue, ripetere i passaggi 7 e 8.

8. Tornare al riquadro **Azure Information Protection-linguaggi** e selezionare **Importa**. Si noti che se questa opzione non è disponibile, è necessario deselezionare per prima cosa la casella di controllo **NOME LINGUA** o le caselle di controllo per le lingue selezionate singolarmente.
    
    Dopo il completamento dell'importazione i nomi e le descrizioni localizzati vengono scaricati per gli utenti.

È necessario ripetere questa procedura se è necessario per supportare una nuova lingua, creare nuove etichette o si modifica il nome o la descrizione delle etichette nel portale di Azure.

## <a name="how-the-azure-information-protection-client-determines-the-language-to-display"></a>Come il client di Azure Information Protection determina la lingua da visualizzare

Quando gli utenti scaricano un criterio di Azure Information Protection che supporta lingue diverse, la lingua con cui vengono visualizzati i nomi di etichetta e le descrizioni dei comandi per gli utenti è determinata dalla logica seguente:

**Per le etichette e le descrizioni comandi visualizzate dagli utenti nella barra Azure Information Protection nelle app di Office**:

- Quando è presente una corrispondenza diretta con la lingua dell'app di Office, le descrizioni e i nomi delle etichette vengono visualizzati in tale lingua.

- Quando non è presente alcuna corrispondenza con la lingua dell'app di Office, le descrizioni e i nomi delle etichette vengono visualizzati nella lingua specificata per impostazione predefinita per tutti gli utenti. Tale lingua è in genere l'inglese, ovvero la lingua usata nel criterio predefinito.

**Per le etichette e le descrizioni comandi visualizzate dagli utenti quando usano il tasto destro del mouse per classificare e proteggere i file o le cartelle**:

- Quando c'è una corrispondenza diretta con la lingua del sistema operativo, le descrizioni e i nomi delle etichette vengono visualizzati in tale lingua.

- Quando non è presente alcuna corrispondenza con la lingua del sistema operativo, le descrizioni e i nomi delle etichette vengono visualizzati nella lingua specificata per impostazione predefinita per tutti gli utenti. Tale lingua è in genere l'inglese, ovvero la lingua usata nel criterio predefinito.

## <a name="when-localized-label-names-are-not-used"></a>Quando non vengono usati i nomi di etichetta localizzati

Negli scenari seguenti non vengono usati nomi di etichette, ed etichette secondarie, localizzati. Per garantire la coerenza nel tenant, per gli oggetti seguenti viene sempre usata la lingua predefinita:

- Log dell'uso del client

- PowerShell (output da Get-AIPFileStatus)

- Metadati documento e intestazioni di posta elettronica


## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sulle opzioni disponibili per le etichette e su altre configurazioni dei criteri di Azure Information Protection, usare i collegamenti nella sezione [Configurazione dei criteri dell'organizzazione](configure-policy.md#configuring-your-organizations-policy).