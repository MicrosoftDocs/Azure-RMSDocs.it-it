---
title: Configurare e gestire i modelli per Azure Information Protection
description: "È possibile configurare e gestire i modelli di Rights Management dal portale di Azure."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 01/08/2018
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 8301aabb-047d-4892-935c-7574f6af8813
ms.reviewer: eymanor
ms.suite: ems
ms.openlocfilehash: f69a163566a9654ee6286c4bf9ca4d018e8f8db5
ms.sourcegitcommit: fc789ce08821e031d3a2b22d850b4318302d3585
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/08/2018
---
# <a name="configuring-and-managing-templates-for-azure-information-protection"></a>Configurazione e gestione dei modelli per Azure Information Protection

>*Si applica a: Azure Information Protection*

>[!NOTE]
>Questa funzionalità sostituisce la configurazione di modelli personalizzati nel portale di Azure classico. Il portale classico è stato ritirato e ora è necessario usare il portale di Azure. Per un riferimento rapido a istruzioni procedurali, vedere [Tasks that you used to do with the Azure classic portal](migrate-portal.md) (Attività che si eseguivano con il portale di Azure classico).


I modelli di Rights Management sono ora integrati con i criteri di Azure Information Protection. 

**Se si ha una sottoscrizione che include la classificazione, l'etichettatura e la protezione (Azure Information Protection P1 o P2):**

- I modelli di Rights Management che non sono integrati con le etichette per il tenant vengono visualizzati nella sezione **Protection templates** (Modelli di protezione) dopo le etichette nel pannello **Azure Information Protection - Criteri globali**. È possibile convertire i modelli in etichette o collegarsi a essi quando si configura la protezione per le etichette. 

**Se si ha una sottoscrizione che include solo la protezione (una sottoscrizione Office 365 con il servizio Azure Rights Management):**

- I modelli di Rights Management per il tenant vengono visualizzati nel pannello **Azure Information Protection - Criteri globali**, sezione **Protection templates** (Modelli di protezione). Non viene visualizzata alcuna etichetta. Sono visualizzate anche le impostazioni di configurazione specifiche per la classificazione e assegnazione di etichette, ma tali impostazioni non hanno alcun effetto sui modelli o non possono essere configurate. 

## <a name="default-templates"></a>Modelli predefiniti

Quando si ottiene la sottoscrizione ad Azure Information Protection o una sottoscrizione Office 365 che include il servizio Azure Rights Management, vengono creati automaticamente due modelli predefiniti per il tenant. Questi modelli consentono di limitare l'accesso agli utenti autorizzati dell'organizzazione. Quando vengono creati, questi modelli dispongono delle autorizzazioni elencate nella documentazione [Configurazione dei diritti di utilizzo per Azure Rights Management](configure-usage-rights.md#rights-included-in-the-default-templates).

I modelli sono configurati in modo da consentire l'accesso offline per sette giorni e non hanno una data di scadenza.

>[!NOTE]
> È possibile modificare queste impostazioni e i nomi e le descrizioni dei modelli predefiniti. Questa capacità non era attivata con il portale di Azure classico e non è supportata per PowerShell.

Questi modelli predefiniti semplificano l'attivazione immediata della protezione dei dati sensibili dell'organizzazione. Questi modelli possono essere usati con le etichette di Azure Information Protection o autonomamente con [applicazioni e servizi](../understand-explore/applications-support.md) che possono usare i modelli di Rights Management.

È anche possibile creare modelli personalizzati. Anche se è probabile che siano necessari solo alcuni modelli, è possibile configurare fino a 500 modelli personalizzati salvati in Azure.

### <a name="default-template-names"></a>Nomi del modello predefinito

Se è stata attivata recentemente una sottoscrizione, i modelli predefiniti vengono creati con i nomi seguenti:

- **Riservato\Tutti i dipendenti** che concede le autorizzazioni di lettura e modifica per il contenuto protetto.

- **Riservatezza elevata\Tutti i dipendenti** che concede le autorizzazioni di sola lettura per il contenuto protetto.

Se la sottoscrizione è stata attivata in passato, i modelli predefiniti vengono creati con i nomi seguenti:

- **\<nome dell'organizzazione> - Riservato** che concede le autorizzazioni di lettura e modifica per il contenuto protetto.

- **\<nome dell'organizzazione> - Solo visione riservata** che concede le autorizzazioni di sola lettura per il contenuto protetto. 

È possibile rinominare e riconfigurare questi modelli predefiniti quando si usa il portale di Azure.

>[!NOTE]
>Se non vengono visualizzati nel pannello **Azure Information Protection - criteri globali**, i modelli predefiniti vengono convertiti in etichette o collegati a un'etichetta. Continuano a esistere come modelli ma, nel portale di Azure, essi vengono visualizzati come parte di una configurazione di etichetta che include la protezione Azure RMS. È sempre possibile verificare quali sono i modelli del tenant eseguendo [Get-AadrmTemplate](/powershell/module/aadrm/get-aadrmtemplate) dal [modulo PowerShell di AADRM](administer-powershell.md).
>
>È possibile convertire manualmente i modelli, come illustrato nella sezione successiva, [Per convertire i modelli in etichette](#to-convert-templates-to-labels), quindi rinominarli se si desidera. In alternativa, vengono convertiti automaticamente per l'utente se il criterio di Azure Information Protection è stato creato di recente e il servizio di Azure Rights Management per il tenant è stato attivato in quel momento.

Nel pannello **Azure Information Protection - criteri globali**, i modelli archiviati sono visualizzati come non disponibili. Non è possibile selezionare questi modelli per le etichette, ma è possibile convertirli in etichette.

## <a name="considerations-for-templates-in-the-azure-portal"></a>Considerazioni sui modelli nel portale di Azure

Prima di modificare i modelli o convertirli in etichette, assicurarsi di essere a conoscenza delle seguenti modifiche e considerazioni. A causa delle modifiche di implementazione, l'elenco seguente è particolarmente importante se si è già gestito dei modelli nel portale di Azure classico.

- Dopo aver modificato o convertito un modello e salvato i criteri di Azure Information Protection, vengono apportate le modifiche seguenti ai [diritti di utilizzo](configure-usage-rights.md) originali. Se necessario, è possibile aggiungere o rimuovere i diritti di utilizzo individuali tramite PowerShell con i cmdlet [New-AadrmRightsDefinition](/powershell/module/aadrm/set-aadrmtemplateproperty) e [Set-AadrmTemplateProperty](/powershell/module/aadrm/new-aadrmrightsdefinition).
    
    - **Salva con nome, Esporta** (nome comune) è stato rimosso. Nel portale di Azure non è possibile specificare manualmente questo diritto di utilizzo che tuttavia è incluso nel diritto di utilizzo Controllo completo che può essere aggiunto quando necessario.
    
    - **Consenti macro** (nome comune) viene aggiunto automaticamente. Questo diritto di utilizzo è obbligatorio per la barra di Azure Information Protection nelle app Office.
    

- Le impostazioni **Pubblicato** e **Archiviato** sono visualizzate rispettivamente come **Abilitato**: **Attivata** e **Abilitato**: **Disattivata** nel pannello **Etichetta**. I modelli che si desidera mantenere ma che non devono essere visibili a utenti o servizi devono essere impostati su **Abilitato**: **OFF**.

- Non è possibile copiare o eliminare un modello nel portale di Azure. Quando il modello viene convertito in un'etichetta, è possibile configurare l'etichetta per interrompere l'uso del modello selezionando **Non configurato** per l'opzione **Configurare le autorizzazioni per documenti e messaggi di posta elettronica contenenti questa etichetta** opzione. In alternativa, è possibile eliminare l'etichetta. In entrambi gli scenari, tuttavia, il modello non viene eliminato e rimane in uno stato archiviato.
    
    È ora possibile eliminare il modello usando il cmdlet PowerShell [Remove-AadrmTemplate](/powershell/module/aadrm/remove-aadrmtemplate). È anche possibile usare questo cmdlet di PowerShell per i modelli che non vengono convertiti in etichette. Tuttavia, se si elimina un modello che è stato usato per proteggere il contenuto, tale contenuto non potrà più essere aperto. Eliminare i modelli solo se si è certi che non sono stati usati per proteggere documenti o messaggi di posta elettronica nell'ambiente di produzione. Come precauzione è necessario considerare prima l'esportazione del modello come back up tramite il cmdlet [Export-AadrmTemplate](/powershell/module/aadrm/export-aadrmtemplate). 

- I modelli di reparto , ovvero i modelli configurati per un ambito specifico, sono visualizzati in Criteri globali. Attualmente, se si modifica e si salva un modello di reparto, la configurazione dell'ambito viene rimossa. L'equivalente di un modello con ambito nei criteri di Azure Information Protection sono i [criteri con ambito](configure-policy-scope.md). Se si converte il modello in etichetta, è possibile selezionare un ambito esistente.
    
    Inoltre, attualmente non è possibile specificare l'impostazione di compatibilità dell'applicazione per un modello di reparto. Se necessario, è possibile specificare l'impostazione di compatibilità dell'applicazione usando PowerShell con il cmdlet [Set-AadrmTemplateProperty](/powershell/module/aadrm/set-aadrmtemplateproperty).

- Durante la conversione o il collegamento di un modello a un'etichetta, questo non può più essere usato da altre etichette. Inoltre, questo modello non viene più visualizzato nella sezione **Protection templates** (Modelli di protezione). 

- Non è possibile creare un nuovo modello dalla sezione **Protection templates** (Modelli di protezione). È invece possibile creare un'etichetta con l'impostazione **Proteggi** e configurare i diritti di utilizzo e le impostazioni dal pannello **Protezione**. Per istruzioni complete, vedere [Per creare un nuovo modello](#to-create-a-new-template).

## <a name="to-configure-the-templates-in-the-azure-information-protection-policy"></a>Per configurare i modelli nei criteri di Azure Information Protection

1. Se non è già stato fatto, aprire una nuova finestra del browser e accedere al [portale di Azure](https://portal.azure.com) come amministratore globale o della sicurezza. Quindi passare al pannello **Azure Information Protection**.     
    
    Ad esempio, dal menu principale fare clic su **Altri servizi** e iniziare a digitare **Informazioni** nella casella Filtro. Selezionare **Azure Information Protection**.

2. Se il nuovo modello da configurare è destinato a tutti gli utenti, restare nel pannello **Azure Information Protection - Criteri globali**.
    
    Se il modello da configurare si trova in un [criterio con ambito](configure-policy-scope.md) per essere applicato solo agli utenti selezionati, nel menu **CRITERI** selezionare **Criteri con ambito**. Selezionare quindi i criteri con ambito nel pannello **Azure Information Protection - Criteri con ambito**.

3. Nel pannello **Azure Information Protection - Criteri globali** o nel pannello **Criteri:\<nome>** individuare il modello da configurare:
    
    - Se si ha una sottoscrizione che include la classificazione, l'etichettatura e la protezione: espandere **Protection templates** (Modelli di protezione) dopo le etichette.
    
    - Se si ha una sottoscrizione che include solo la protezione: i modelli vengono visualizzati come etichette.

4. Selezionare il modello e, se necessario, modificare il nome del modello e la descrizione nel pannello **Etichetta** modificando **Nome etichetta** e **Descrizione**. Selezionare quindi **Protezione** con il valore **Azure (cloud key)** (Azure - Chiave cloud) per aprire il pannello **Protezione**.

5. Nel pannello **Protezione** è possibile modificare le autorizzazioni, la scadenza del contenuto e le impostazioni dell'accesso offline. Per altre informazioni sulla configurazione delle impostazioni di protezione, vedere [Come configurare un'etichetta per la protezione di Rights Management](configure-policy-protection.md)
    
    Fare clic su **OK** per mantenere le modifiche e nel pannello **Etichetta** fare clic su **Salva**.

6. Per rendere disponibili le modifiche per le applicazioni e i servizi degli utenti, nel pannello **Azure Information Protection** iniziale fare clic su **Pubblica**.

> [!NOTE]
> È anche possibile modificare un modello usando il pulsante **Modifica modello** del pannello **Protezione** se è stata configurata un'etichetta per l'uso di un modello predefinito. Se nessun'altra etichetta usa il modello selezionato, questo pulsante converte il modello in un'etichetta e attiva il passaggio 5. Per altre informazioni su cosa accade quando i modelli vengono convertiti in etichette, vedere la sezione seguente.

## <a name="to-convert-templates-to-labels"></a>Per convertire i modelli in etichette

Se si ha una sottoscrizione che include la classificazione, l'etichettatura e la protezione, è possibile convertire un modello in etichetta. Quando si converte un modello il modello originale viene mantenuto, ma ora viene visualizzato nel portale di Azure come incluso in una nuova etichetta.

Ad esempio, se si converte un'etichetta denominata **Marketing** che concede diritti di utilizzo al gruppo marketing, nel portale di Azure viene visualizzata come etichetta denominata **Marketing** con le stesse impostazioni di protezione. Se si modificano le impostazioni di protezione nella nuova etichetta creata, la modifica viene eseguita nel modello e gli utenti o i servizi che usano il modello riceveranno le nuove impostazioni di protezione al successivo aggiornamento del modello. 

Sebbene non sia necessario convertire tutti i modelli in etichette, se si esegue questa operazione le impostazioni di protezione saranno completamente integrate con la funzionalità delle etichette e non sarà necessario gestire le impostazioni separatamente.

Per convertire un modello in un'etichetta, fare clic con il pulsante destro del mouse sul modello e selezionare **Converti in etichetta**. In alternativa, usare il menu di scelta rapida per selezionare questa opzione. 

È anche possibile convertire un modello in un'etichetta quando si configura un'etichetta per la protezione e un modello predefinito, usando il pulsante **Modifica modello**. 

Quando si converte un modello in etichetta:

- Il nome del modello viene convertito in un nuovo nome di etichetta e la descrizione del modello viene convertita nella descrizione dell'etichetta. 

- Se lo stato del modello è pubblicato, questa impostazione viene mappata su **Abilitato**: **Attivata** per l'etichetta che verrà visualizzata agli utenti alla successiva pubblicazione dei criteri di Azure Information Protection. Se lo stato del modello è archiviato, questa impostazione viene mappata su **Abilitato**: **Disattivata** per l'etichetta che non viene visualizzata come etichetta disponibile agli utenti.

- Le impostazioni di protezione vengono mantenute e, se necessario, è possibile modificarle e aggiungere altre impostazioni di etichetta, ad esempio gli indicatori visivi e le condizioni.

- Il modello originale non viene più visualizzato in **Protection templates** (Modelli di protezione) e non può essere selezionato come modello predefinito quando si configura la protezione per un'etichetta. Per modificare questo modello nel portale di Azure è ora possibile modificare l'etichetta che è stata creata durante la conversione del modello. Il modello rimane disponibile per il servizio Azure Rights Management e può essere gestito con i [comandi di PowerShell](administer-powershell.md).  

## <a name="to-create-a-new-template"></a>Per creare un nuovo modello

Quando si crea una nuova etichetta con l'impostazione di protezione **Azure RMS** o **Azure (cloud key)** (Azure - Chiave cloud) viene creato un nuovo modello personalizzato, al quale possono accedere i servizi e le applicazioni che si integrano con i modelli di Rights Management.

1. Se il nuovo modello è destinato a tutti gli utenti, restare nel pannello **Azure Information Protection - Criteri globali**.
    
     Se il modello da configurare è un modello di reparto e come tale verrà applicato solo agli utenti selezionati, nel menu **CRITERI** selezionare **Criteri con ambito**. Quindi creare o selezionare i [criteri con ambito](configure-policy-scope.md) nel pannello **Azure Information Protection - Criteri con ambito**.

2. Nel pannello **Azure Information Protection - Criteri globali** o nel pannello **Criteri:\<nome>** fare clic su **Aggiungi una nuova etichetta**.

3. Nel pannello **Etichetta** mantenere il valore predefinito **Abilitato**: **Attivata** per pubblicare il nuovo modello o modificare l'impostazione in **Disattivata** per creare il modello come modello archiviato. Immettere quindi un nome di etichetta e una descrizione per il nome del modello e la descrizione.

4. Per **Configurare le autorizzazioni per documenti e messaggi di posta elettronica contenenti questa etichetta** selezionare **Proteggi**, quindi selezionare **Protezione**:
    
     ![Configurare la protezione per un'etichetta di Azure Information Protection](../media/info-protect-protection-bar-configured.png)

5. Nel pannello **Protezione** è possibile modificare le autorizzazioni, la scadenza del contenuto e le impostazioni dell'accesso offline. Per altre informazioni sulla configurazione delle impostazioni di protezione, vedere [Come configurare un'etichetta per la protezione di Rights Management](configure-policy-protection.md)
    
    Fare clic su **OK** per mantenere le modifiche e nel pannello **Etichetta** fare clic su **Salva**.

6. Per rendere disponibili i modelli per le applicazioni e i servizi degli utenti, nel pannello **Azure Information Protection** iniziale fare clic su **Pubblica**.


## <a name="next-steps"></a>Passaggi successivi

Come avviene per tutte le modifiche apportate ai criteri di Azure Information Protection, il download di questi modelli potrebbe richiedere fino a 15 minuti in un computer che esegue il client Azure Information Protection. Per informazioni sul download e l'aggiornamento dei modelli nei computer e nei servizi, vedere [Aggiornamento dei modelli per gli utenti](refresh-templates.md).

Tutte le operazioni che è possibile configurare nel portale di Azure per creare e gestire modelli possono essere eseguite tramite PowerShell. Inoltre, PowerShell fornisce più opzioni che non sono disponibili nel portale. Per altre informazioni, vedere la [Guida di riferimento di PowerShell per i modelli personalizzati](configure-templates-with-powershell.md). 

Per altre informazioni sulla configurazione dei criteri di Azure Information Protection, usare i collegamenti nella sezione [Configurazione dei criteri dell'organizzazione](configure-policy.md#configuring-your-organizations-policy).  

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
