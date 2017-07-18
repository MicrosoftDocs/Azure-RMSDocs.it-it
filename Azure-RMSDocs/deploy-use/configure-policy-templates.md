---
title: Configurare e gestire i modelli nei criteri di Azure Information Protection
description: "Attualmente in anteprima, è ora possibile configurare e gestire i modelli di Rights Management dai criteri di Azure Information Protection."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 05/30/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 8301aabb-047d-4892-935c-7574f6af8813
ms.reviewer: eymanor
ms.suite: ems
ms.openlocfilehash: 1f41aad2d132e087e9122b2683be4b45185527de
ms.sourcegitcommit: 04eb4990e2bf0004684221592cb93df35e6acebe
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/30/2017
---
# <a name="configuring-and-managing-templates-in-the-azure-information-protection-policy"></a>Configurazione e gestione dei modelli nei criteri di Azure Information Protection

>*Si applica a: Azure Information Protection*

>[!NOTE]
>Questa funzionalità è attualmente in anteprima e soggetta a modifiche frequenti.
>
>Prima di testare questa funzionalità in anteprima con modelli personalizzati creati nel portale di Azure classico, verificare se è disponibile un backup recente dei modelli. È possibile eseguire il backup dei modelli personalizzati usando il cmdlet di PowerShell [Export-AadrmTemplate](/powershell/module/aadrm/export-aadrmtemplate) e, se necessario, usare [Import-AadrmTemplate](/powershell/module/aadrm/import-aadrmtemplate) per ripristinarli.
>
>A causa delle differenze nell'implementazione, non è consigliabile gestire gli stessi modelli dal portale di Azure classico e dal portale di Azure.


I modelli di Rights Management sono ora integrati con i criteri di Azure Information Protection. 

**Se si ha una sottoscrizione che include la classificazione, l'etichettatura e la protezione (Azure Information Protection P1 o P2):**

- I modelli di Rights Management per il tenant sono visualizzati nella nuova sezione **Modelli** dopo le etichette. È possibile convertire i modelli in etichette o continuare a gestirli come modelli separati e collegarsi a essi quando si configura la protezione per le etichette. 

**Se si ha una sottoscrizione che include solo la protezione (una sottoscrizione Office 365 con il servizio Azure Rights Management):**

- I modelli di Rights Management per il tenant sono visualizzati come etichette e attualmente sono disponibili anche le impostazioni di configurazione specifiche della classificazione e dell'etichettatura. 


## <a name="considerations-for-templates-in-the-azure-portal"></a>Considerazioni sui modelli nel portale di Azure

Prima di modificare i modelli o convertirli in etichette nel portale di Azure, tenere presente le seguenti modifiche nell'implementazione rispetto alla gestione dei modelli nel portale di Azure classico. Si prevede che alcune limitazioni vengano risolte nell'anteprima:

- Dopo aver modificato o convertito un modello e salvato i criteri di Azure Information Protection, vengono apportate le modifiche seguenti ai [diritti di utilizzo](configure-usage-rights.md) originali. Se necessario, è possibile aggiungere o rimuovere i diritti di utilizzo individuali tramite PowerShell con i cmdlet [New-AadrmRightsDefinition](/powershell/module/aadrm/set-aadrmtemplateproperty) e [Set-AadrmTemplateProperty](/powershell/module/aadrm/new-aadrmrightsdefinition).
    
    - **Salva con nome, Esporta** (nome comune) è stato rimosso. Nel portale di Azure non è possibile specificare manualmente questo diritto di utilizzo che tuttavia è incluso nel diritto di utilizzo Controllo completo che può essere aggiunto quando necessario.
    
    - **Consenti macro** (nome comune) viene aggiunto automaticamente. Questo diritto di utilizzo è obbligatorio per la barra di Azure Information Protection nelle app Office.
    
- Attualmente, i modelli predefiniti sono visualizzati ma non possono essere modificati o convertiti. 

- Non è possibile copiare o eliminare un modello. Per rimuovere un modello, usare il cmdlet PowerShell [Remove-AadrmTemplate](/powershell/module/aadrm/remove-aadrmtemplate). 

- Attualmente, i modelli che sono stati configurati per le lingue tramite il portale di Azure classico o PowerShell non visualizzano le lingue per il nome e le descrizioni, ma sono mantenuti.

- Le impostazioni **Pubblicato** e **Archiviato** sono visualizzate rispettivamente come **Abilitato**: **Attivata** e **Abilitato**: **Disattivata** nel pannello **Etichetta**.

- I modelli di reparto , ovvero i modelli configurati per un ambito specifico, sono visualizzati in Criteri globali. Attualmente, se si modifica e si salva un modello di reparto, la configurazione dell'ambito viene rimossa. L'equivalente di un modello con ambito nei criteri di Azure Information Protection sono i [criteri con ambito](configure-policy-scope.md). Se si converte il modello in etichetta, è possibile selezionare un ambito esistente.
    
    Inoltre, attualmente non è possibile specificare l'impostazione di compatibilità dell'applicazione per un modello di reparto. Se necessario, è possibile specificarla usando PowerShell con il cmdlet [Set-AadrmTemplateProperty](/powershell/module/aadrm/set-aadrmtemplateproperty).

- Poiché non è possibile creare un nuovo modello dal contenitore **Modelli**, creare un'etichetta con l'impostazione **Proteggi** e configurare i diritti di utilizzo e le impostazioni dal pannello **Protezione**. Per istruzioni complete, vedere [Per creare un nuovo modello](#to-create-a-new-template).

## <a name="to-configure-the-templates-in-the-azure-information-protection-policy"></a>Per configurare i modelli nei criteri di Azure Information Protection

1. In una nuova finestra del browser accedere al [portale di Azure](https://portal.azure.com) come amministratore globale o della sicurezza.

2. Passare al pannello **Azure Information Protection**: ad esempio, nel menu hub fare clic su **More services** (Altri servizi) e iniziare a digitare **Information Protection** nella casella Filtro. Selezionare **Azure Information Protection** nei risultati. 

2. Se il modello da configurare verrà applicato a tutti gli utenti, selezionare **Globale** nel pannello **Azure Information Protection**. Tuttavia, se il modello da configurare si trova in un [criterio con ambito](configure-policy-scope.md) in modo da essere applicato solo agli utenti selezionati, selezionare il criterio con ambito.

3. Nel pannello dei criteri individuare il modello che si vuole configurare:
    
    - Se si ha una sottoscrizione che include la classificazione, l'etichettatura e la protezione: espandere **Modelli** dopo le etichette.
    
    - Se si ha una sottoscrizione che include solo la protezione: i modelli vengono visualizzati come etichette.

4. Selezionare il modello e, se necessario, modificare il nome del modello e la descrizione nel pannello **Etichetta** modificando **Nome etichetta** e **Descrizione**. Selezionare quindi **Protezione** con valore **Azure RMS** per aprire il pannello **Protezione**.

5. Nel pannello **Protezione** è possibile modificare le autorizzazioni, la scadenza del contenuto e le impostazioni dell'accesso offline. Per altre informazioni sulla configurazione delle impostazioni di protezione, vedere [Come configurare un'etichetta per la protezione di Rights Management](configure-policy-protection.md)
    
    Fare clic su **OK** per mantenere le modifiche e nel pannello **Etichetta** fare clic su **Salva**.

6. Per rendere disponibili le modifiche per le applicazioni e i servizi degli utenti, nel pannello **Azure Information Protection** fare clic su **Pubblica**.

## <a name="to-convert-templates-to-labels"></a>Per convertire i modelli in etichette

Se si ha una sottoscrizione che include la classificazione, l'etichettatura e la protezione, è possibile convertire un modello in etichetta. Quando si esegue questa operazione, il modello originale viene mantenuto ma viene visualizzato nel portale di Azure incluso in una nuova etichetta.

Ad esempio, se si converte un'etichetta denominata **Marketing** che concede diritti di utilizzo al gruppo marketing, nel portale di Azure viene visualizzata come etichetta denominata **Marketing** con le stesse impostazioni di protezione. Se si modificano le impostazioni di protezione nella nuova etichetta creata, la modifica viene eseguita nel modello e gli utenti o i servizi che usano il modello riceveranno le nuove impostazioni di protezione al successivo aggiornamento del modello. 

Sebbene non sia necessario convertire tutti i modelli in etichette, se si esegue questa operazione le impostazioni di protezione saranno completamente integrate con la funzionalità delle etichette e non sarà necessario gestire le impostazioni separatamente.

Per convertire un modello in un'etichetta, fare clic con il pulsante destro del mouse sul modello e selezionare **Converti in etichetta**. In alternativa, usare il menu di scelta rapida per selezionare questa opzione.

Quando si converte un modello in etichetta:

- Il nome del modello viene convertito in un nuovo nome di etichetta e la descrizione del modello viene convertita nella descrizione dell'etichetta. 

- Se lo stato del modello è pubblicato, questa impostazione viene mappata su **Abilitato**: **Attivata** per l'etichetta che verrà visualizzata agli utenti alla successiva pubblicazione dei criteri di Azure Information Protection. Se lo stato del modello è archiviato, questa impostazione viene mappata su **Abilitato**: **Disattivata** per l'etichetta che non viene visualizzata come etichetta disponibile agli utenti.

- Le impostazioni di protezione vengono mantenute e, se necessario, è possibile modificarle e aggiungere altre impostazioni di etichetta, ad esempio gli indicatori visivi e le condizioni.

- Il modello originale non è più visualizzato in **Modelli** e per modificarlo nel portale di Azure è ora necessario modificare l'etichetta creata. Il modello rimane disponibile per il servizio Azure Rights Management e può essere gestito con i [comandi di PowerShell](administer-powershell.md).  

## <a name="to-create-a-new-template"></a>Per creare un nuovo modello

Quando si crea una nuova etichetta con l'impostazione di protezione **Azure RMS**, viene creato un nuovo modello personalizzato che può essere usato dai servizi e dalle applicazioni che si integrano con i modelli di Rights Management.

1. Se il nuovo modello che si vuole creare verrà applicato a tutti gli utenti, nel pannello **Criteri: Globale** fare clic su **Aggiungi una nuova etichetta**.
    
     Se il nuovo modello che si vuole creare è un modello di reparto da applicare solo agli utenti selezionati, innanzitutto selezionare o creare un criterio con ambito dal pannello iniziale **Azure Information Protection**.

2. Nel pannello **Etichetta** mantenere il valore predefinito **Abilitato**: **Attivata** per pubblicare il nuovo modello o modificare l'impostazione in **Disattivata** per creare il modello come modello archiviato. Immettere quindi un nome di etichetta e una descrizione per il nome del modello e la descrizione.

3. Per **Configurare le autorizzazioni per documenti e messaggi di posta elettronica contenenti questa etichetta** selezionare **Proteggi**, quindi selezionare **Protezione**:
    
     ![Configurare la protezione per un'etichetta di Azure Information Protection](../media/info-protect-protection-bar.png)

4. Nel pannello **Protezione** è possibile modificare le autorizzazioni, la scadenza del contenuto e le impostazioni dell'accesso offline. Per altre informazioni sulla configurazione delle impostazioni di protezione, vedere [Come configurare un'etichetta per la protezione di Rights Management](configure-policy-protection.md)
    
    Fare clic su **OK** per mantenere le modifiche e nel pannello **Etichetta** fare clic su **Salva**.

5. Per rendere disponibili i modelli per le applicazioni e i servizi degli utenti, nel pannello **Azure Information Protection** fare clic su **Pubblica**.


## <a name="next-steps"></a>Passaggi successivi

Come avviene per tutte le modifiche apportate ai criteri di Azure Information Protection, il download di questi modelli potrebbe richiedere fino a 15 minuti in un computer che esegue il client Azure Information Protection. Per informazioni sul download e l'aggiornamento dei modelli nei computer e nei servizi, vedere [Aggiornamento dei modelli per gli utenti](refresh-templates.md).

Per altre informazioni sulla configurazione dei criteri di Azure Information Protection, usare i collegamenti nella sezione [Configurazione dei criteri dell'organizzazione](configure-policy.md#configuring-your-organizations-policy).  

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
