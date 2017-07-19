---
title: Configurare etichette per lingue diverse in Azure Information Protection
description: "È possibile aggiungere il supporto per lingue diverse per le etichette che gli utenti visualizzano sulla barra di Information Protection specificando le lingue nei criteri di Azure Information Protection e importando le traduzioni."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 07/05/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: a0e89fd0-795b-4e7a-aea9-ff6fc9163bde
ms.openlocfilehash: ec99bf36e8904a7304a9d33c32d17ba92e2e22d2
ms.sourcegitcommit: 8b768e7e249e124f24acdf630d165eaf743f9c21
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/05/2017
---
# <a name="how-to-configure-labels-for-different-languages-in-azure-information-protection"></a>Come configurare etichette per lingue diverse in Azure Information Protection

>*Si applica a: Azure Information Protection*

>[!NOTE]
>Questa funzionalità è attualmente in anteprima e deve essere usata insieme con la versione di **anteprima** del client di Azure Information Protection che è possibile scaricare da [Microsoft Download Center](https://www.microsoft.com/en-us/download/details.aspx?id=53018).

Per impostazione predefinita, i nomi e le descrizioni delle etichette supportano una sola lingua visualizzata per tutti gli utenti dell'organizzazione. È possibile aggiungere il supporto per lingue diverse selezionandole, esportando i nomi e le descrizioni delle etichette correnti in un file, modificando il file inserendovi le traduzioni e quindi importando nuovamente il file nei criteri di Azure Information Protection.

Selezionare le lingue che corrispondono alle impostazioni lingua degli utenti per Office e Windows. Tali nomi e descrizioni di etichette vengono poi visualizzati rispettivamente nella barra di Azure Information Protection nelle app di Office e nella casella di dialogo **Classifica e proteggi - Azure Information Protection**. Per altre informazioni su quale lingua venga scelta, vedere la sezione [Come il client di Azure Information Protection determina la lingua da visualizzare](#how-the-azure-information-protection-client-determines-the-language-to- display) in questa pagina. 

## <a name="to-configure-labels-to-display-in-different-languages"></a>Per configurare le etichette da visualizzare in lingue diverse

1. Se non è già stato fatto, in una nuova finestra del browser accedere al [portale di Azure](https://portal.azure.com) come amministratore globale o della sicurezza e quindi passare al pannello **Azure Information Protection**. 
    
    Ad esempio, dal menu principale fare clic su **Altri servizi** e iniziare a digitare **Informazioni** nella casella Filtro. Selezionare **Azure Information Protection**.

2. Nel pannello iniziale **Azure Information Protection** individuare **GESTISCI** e selezionare **Lingue (anteprima)**.

3. Nel pannello **Azure Information Protection - Lingue (anteprima)** individuare la prima lingua che si vuole aggiungere digitandone il nome nella casella di ricerca o scorrendo l'elenco delle lingue disponibili. 

4. Selezionare la lingua e scegliere **OK**.

5. Nel pannello successivo verrà visualizzata la lingua selezionata aggiunta a un elenco:
    
    - Per aggiungere un'altra lingua, selezionare **Aggiungi una nuova lingua per la conversione** e ripetere i passaggi 3 e 4. 
        
        > [!NOTE]
        > Assicurarsi di selezionare le lingue che gli utenti hanno per Office e per Windows. In alcuni casi potrebbe essere necessario eseguire due selezioni diverse per computer.
        
    - Nel caso in cui si voglia modificare la scelta di una lingua, selezionare una voce dall'elenco e fare clic su **Rimuovi**.

6. Quando tutte le lingue che si vuole supportare sono elencate, selezionare la casella di controllo accanto a **NOME LINGUA** per selezionare tutte le voci, o in alternativa, selezionare le singole voci, e fare clic su **Esporta** per salvare una copia locale dei nomi e delle descrizioni delle etichette esistenti in un file. 
    
    Il file scaricato viene denominato **exported localization.zip** e viene salvato nella cartella Download locale. È anche possibile accedere selezionando il nome del file nella barra di stato del portale di Azure.

7. Estrarre i file da **exported localization.zip** in modo da avere file con estensione xml per ogni lingua selezionata per il download. 

8. Modificare ogni file con estensione xml: per ogni stringa all'interno di tag `<LocalizedText>`, immettere le traduzioni per ogni lingua scelta. 

9. Quando è stato modificato ogni file con estensione xml, creare una nuova cartella compressa contenente i file. La cartella compressa può avere qualsiasi nome, ma deve avere estensione zip.

10. Tornare al pannello del portale di Azure e selezionare **Importa**. Si noti che se questa opzione non è disponibile, è necessario deselezionare per prima cosa la casella di controllo **NOME LINGUA** o le caselle di controllo per le lingue selezionate singolarmente.
    
    Al termine dell'importazione, i nomi e le descrizioni delle etichette localizzate verranno scaricati per gli utenti alla pubblicazione successiva dei criteri di Azure Information Protection. È possibile fare clic su **Pubblica** dal pannello **Criteri globali** o **Criteri con ambito**.

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

[!INCLUDE[Commenting house rules](../includes/houserules.md)]


