---
title: Configurare e gestire i modelli per Azure Information Protection - AIP
description: Configurare e gestire i modelli di protezione, noti anche come modelli di Rights Management, dal portale di Azure.
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 1/06/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 8301aabb-047d-4892-935c-7574f6af8813
ms.subservice: aiplabels
ms.reviewer: eymanor
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 09e8358493e80099b38294c472f134cb0632943f
ms.sourcegitcommit: 3b50727cb50a612b12f248a5d18b00175aa775f7
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/08/2020
ms.locfileid: "75743459"
---
# <a name="configuring-and-managing-templates-for-azure-information-protection"></a>Configurazione e gestione dei modelli per Azure Information Protection

>*Si applica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*
>
> *Istruzioni per: [client di Azure Information Protection per Windows](faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*


I modelli di protezione, noti anche come modelli di Rights Management, sono un raggruppamento di impostazioni di protezione definite dall'amministratore per Azure Information Protection. Queste impostazioni includono i [diritti di utilizzo](configure-usage-rights.md) scelti per gli utenti autorizzati e i controlli di accesso per l'accesso con scadenza e offline. Questi modelli sono ora integrati con i criteri di Azure Information Protection: 

**Se si ha una sottoscrizione che include la classificazione, l'etichettatura e la protezione (Azure Information Protection P1 o P2):**

- I modelli che non sono integrati con le etichette per il tenant vengono visualizzati nella sezione **modelli di protezione** dopo le etichette nel riquadro **etichette Azure Information Protection** . Per passare a questo riquadro, selezionare l'opzione di menu **classificazioni** > **etichette** . È possibile convertire i modelli in etichette o collegarsi a essi quando si configura la protezione per le etichette. 

**Se si ha una sottoscrizione che include solo la protezione (una sottoscrizione Office 365 con il servizio Azure Rights Management):**

- I modelli per il tenant vengono visualizzati nella sezione **modelli di protezione** nel riquadro **etichette Azure Information Protection** . Per passare a questo riquadro, selezionare l'opzione di menu **classificazioni** > **etichette** . Non viene visualizzata alcuna etichetta. Sono visualizzate anche le impostazioni di configurazione specifiche per la classificazione e assegnazione di etichette, ma tali impostazioni non hanno alcun effetto sui modelli o non possono essere configurate. 

>[!NOTE]
>In alcuni servizi e applicazioni, possono essere visualizzati i modelli [Non inoltrare](configure-usage-rights.md#do-not-forward-option-for-emails) ed [Encrypt-Only](configure-usage-rights.md#encrypt-only-option-for-emails) (Solo crittografia) o **Crittografa**. Questi non sono modelli che è possibile modificare o eliminare, ma opzioni disponibili per impostazione predefinita con il servizio Exchange.

## <a name="default-templates"></a>Modelli predefiniti

Quando si ottiene la sottoscrizione ad Azure Information Protection o una sottoscrizione Office 365 che include il servizio Azure Rights Management, vengono creati automaticamente due modelli predefiniti per il tenant. Questi modelli consentono di limitare l'accesso agli utenti autorizzati dell'organizzazione. Quando vengono creati, questi modelli dispongono delle autorizzazioni elencate nella documentazione relativa alla [configurazione dei diritti di utilizzo per Azure Information Protection](configure-usage-rights.md#rights-included-in-the-default-templates) .

I modelli sono configurati in modo da consentire l'accesso offline per sette giorni e non hanno una data di scadenza.

>[!NOTE]
> È possibile modificare queste impostazioni e i nomi e le descrizioni dei modelli predefiniti. Questa capacità non era attivata con il portale di Azure classico e non è supportata per PowerShell.

Questi modelli predefiniti semplificano l'attivazione immediata della protezione dei dati sensibili dell'organizzazione. Questi modelli possono essere usati con le etichette di Azure Information Protection o autonomamente con [applicazioni e servizi](applications-support.md) che possono usare i modelli di Rights Management.

È anche possibile creare modelli personalizzati. Anche se è probabile che siano necessari solo alcuni modelli, è possibile configurare fino a 500 modelli personalizzati salvati in Azure.


### <a name="default-template-names"></a>Nomi del modello predefinito

Se è stata attivata recentemente una sottoscrizione, i modelli predefiniti vengono creati con i nomi seguenti:

- **Riservato\Tutti i dipendenti**

- **Riservatezza elevata\Tutti i dipendenti**

Se la sottoscrizione è stata ottenuta qualche tempo fa, è possibile creare i modelli predefiniti con i nomi seguenti:

- **nome dell'organizzazione \<>-Confidential**

- **\<nome organizzazione> - Solo visualizzazione riservata** 

È possibile rinominare e riconfigurare questi modelli predefiniti quando si usa il portale di Azure.

>[!NOTE]
>Se i modelli predefiniti non vengono visualizzati nel riquadro **Azure Information Protection-labels** , vengono convertiti in etichette o collegati a un'etichetta. Continuano a esistere come modelli, ma nel portale di Azure essi vengono visualizzati come parte di una configurazione di etichetta che include le impostazioni di protezione per una chiave del cloud. È sempre possibile verificare i modelli del tenant, eseguendo [Get-AipServiceTemplate](/powershell/module/aipservice/get-aipservicetemplate) dal [modulo PowerShell di AIPService](administer-powershell.md).
>
>È possibile convertire manualmente i modelli, come illustrato nella sezione successiva, [Per convertire i modelli in etichette](#to-convert-templates-to-labels), quindi rinominarli se si desidera. In alternativa, vengono convertiti automaticamente per l'utente se il criterio di Azure Information Protection è stato creato di recente e il servizio di Azure Rights Management per il tenant è stato attivato in quel momento.

I modelli archiviati sono visualizzati come non disponibili nel riquadro **etichette Azure Information Protection** . Non è possibile selezionare questi modelli per le etichette, ma è possibile convertirli in etichette.

## <a name="considerations-for-templates-in-the-azure-portal"></a>Considerazioni sui modelli nel portale di Azure

Prima di modificare i modelli o convertirli in etichette, assicurarsi di essere a conoscenza delle seguenti modifiche e considerazioni. A causa delle modifiche di implementazione, l'elenco seguente è particolarmente importante se si è già gestito dei modelli nel portale di Azure classico.

- Dopo aver modificato o convertito un modello e salvato i criteri di Azure Information Protection, vengono apportate le modifiche seguenti ai [diritti di utilizzo](configure-usage-rights.md) originali. Se necessario, è possibile aggiungere o rimuovere singoli diritti di utilizzo tramite il portale di Azure. In alternativa, usare PowerShell con i cmdlet [New-AipServiceRightsDefinition](/powershell/module/aipservice/new-aipservicerightsdefinition) e [set-AipServiceTemplateProperty](/powershell/module/aipservice/set-aipservicetemplateproperty) .
    
    - **Consenti macro** (nome comune) viene aggiunto automaticamente. Questo diritto di utilizzo è obbligatorio per la barra di Azure Information Protection nelle app Office.

- Le impostazioni **pubblicato** e **archiviato** sono visualizzate rispettivamente come **abilitato**: **attivata e** **abilitato**: **disattivata** nel riquadro **etichetta** . I modelli che si desidera mantenere ma che non devono essere visibili a utenti o servizi devono essere impostati su **Abilitato**: **OFF**.

- Non è possibile copiare o eliminare un modello nel portale di Azure. Quando il modello viene convertito in un'etichetta, è possibile configurare l'etichetta per interrompere l'uso del modello selezionando **Non configurato** per l'opzione **Configurare le autorizzazioni per documenti e messaggi di posta elettronica contenenti questa etichetta** opzione. In alternativa, è possibile eliminare l'etichetta. In entrambi gli scenari, tuttavia, il modello non viene eliminato e rimane in uno stato archiviato.
    
    A questo punto è possibile eliminare il modello usando il cmdlet [Remove-AipServiceTemplate](/powershell/module/aipservice/remove-aipservicetemplate) di PowerShell. È anche possibile usare questo cmdlet di PowerShell per i modelli che non vengono convertiti in etichette. Tuttavia, per garantire che il contenuto protetto in precedenza possa essere aperto e usato come previsto, in genere è consigliabile evitare di eliminare i modelli. Come procedura consigliata, eliminare i modelli solo se si è certi che non sono stati usati per proteggere documenti o messaggi di posta elettronica nell'ambiente di produzione. Come precauzione, è consigliabile prima di tutto esportare il modello come backup usando il cmdlet [Export-AipServiceTemplate](/powershell/module/aipservice/export-aipservicetemplate) . 

- Attualmente, se si modifica e si salva un modello di reparto, la configurazione dell'ambito viene rimossa. L'equivalente di un modello con ambito nei criteri di Azure Information Protection sono i [criteri con ambito](configure-policy-scope.md). Se si converte il modello in etichetta, è possibile selezionare un ambito esistente.
    
    Inoltre, non è possibile specificare l'impostazione di compatibilità dell'applicazione per un modello di reparto tramite il portale di Azure. Se necessario, è possibile impostare questa impostazione di compatibilità dell'applicazione usando il cmdlet [set-AipServiceTemplateProperty](/powershell/module/aipservice/set-aipservicetemplateproperty) e il parametro *EnableInLegacyApps* .

- Durante la conversione o il collegamento di un modello a un'etichetta, questo non può più essere usato da altre etichette. Inoltre, questo modello non viene più visualizzato nella sezione **Protection templates** (Modelli di protezione). 

- Non è possibile creare un nuovo modello dalla sezione **Protection templates** (Modelli di protezione). In alternativa, creare un'etichetta con l'impostazione **Proteggi** e configurare i diritti di utilizzo e le impostazioni dal riquadro **protezione** . Per istruzioni complete, vedere [Per creare un nuovo modello](#to-create-a-new-template).

## <a name="to-configure-the-templates-in-the-azure-information-protection-policy"></a>Per configurare i modelli nei criteri di Azure Information Protection

1. Se non è già stato fatto, aprire una nuova finestra del browser e [accedere al portale di Azure](configure-policy.md#signing-in-to-the-azure-portal). Passare quindi al riquadro **etichette Azure Information Protection** .
    
    Ad esempio, nella casella di ricerca per risorse, servizi e documenti: iniziare a digitare **informazioni** e selezionare **Azure Information Protection**.

2. Dall'opzione di menu **classificazioni** > **etichette** : nel riquadro **etichette Azure Information Protection** , espandere modelli di **protezione**, quindi individuare il modello che si desidera configurare.
    
3. Selezionare il modello e, nel riquadro **etichetta** , è possibile modificare il nome e la descrizione del modello, se necessario, modificando il **nome visualizzato** e la **Descrizione**dell'etichetta. Selezionare quindi **protezione** con il valore **Azure (chiave Cloud)** per aprire il riquadro **protezione** .

4. Nel riquadro **protezione** è possibile modificare le autorizzazioni, la scadenza del contenuto e le impostazioni di accesso offline. Per altre informazioni sulla configurazione delle impostazioni di protezione, vedere [Come configurare un'etichetta per la protezione di Rights Management](configure-policy-protection.md)
    
    Fare clic su **OK** per salvare le modifiche, quindi fare clic su **Salva**nel riquadro **etichetta** .
    
> [!NOTE]
> È anche possibile modificare un modello usando il pulsante **modifica modello** nel riquadro **protezione** se è stata configurata un'etichetta per l'uso di un modello predefinito. Se nessun'altra etichetta usa il modello selezionato, questo pulsante converte il modello in un'etichetta e attiva il passaggio 5. Per altre informazioni su cosa accade quando i modelli vengono convertiti in etichette, vedere la sezione seguente.

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

Quando si crea una nuova etichetta con l'impostazione di protezione **Azure (chiave cloud)** viene creato un nuovo modello personalizzato, al quale possono accedere i servizi e le applicazioni che si integrano con i modelli di Rights Management.

1. Dall'opzione di menu **classificazioni** > **etichette** : nel riquadro **etichette Azure Information Protection** selezionare **Aggiungi una nuova etichetta**.

2. Nel riquadro **etichetta** , Mantieni il valore predefinito **abilitato**: **on**, quindi immetti un nome e una descrizione per il nome del modello e la descrizione.

3. Per **Configurare le autorizzazioni per documenti e messaggi di posta elettronica contenenti questa etichetta** selezionare **Proteggi**, quindi selezionare **Protezione**:
    
     ![Configurare la protezione per un'etichetta di Azure Information Protection](./media/info-protect-protection-bar-configured.png)

4. Nel riquadro **protezione** è possibile modificare le autorizzazioni, la scadenza del contenuto e le impostazioni di accesso offline. Per altre informazioni sulla configurazione delle impostazioni di protezione, vedere [Come configurare un'etichetta per la protezione di Rights Management](configure-policy-protection.md)
    
    Fare clic su **OK** per salvare le modifiche, quindi fare clic su **Salva**nel riquadro **etichetta** .
    
    Nel riquadro **etichette di Azure Information Protection** è ora visibile la nuova etichetta visualizzata con la colonna **protezione** per indicare che contiene impostazioni di protezione. Queste impostazioni di protezione vengono visualizzate come modelli per le applicazioni e i servizi che supportano il servizio Azure Rights Management.
    
    Anche se l'etichetta è abilitata, per impostazione predefinita il modello viene archiviato. In modo che le applicazioni e i servizi possano usare il modello per proteggere documenti e messaggi di posta elettronica, completare il passaggio finale per pubblicare il modello.

5. Nell'opzione di menu **Classificazioni** > **Criteri** selezionare i criteri in cui includere le nuove impostazioni di protezione. Selezionare quindi **Add or remove labels** (Aggiungi o rimuovi etichette). Dal riquadro **criteri: Aggiungi o Rimuovi etichette** selezionare l'etichetta appena creata che contiene le impostazioni di protezione, selezionare **OK**e quindi fare clic su **Salva**.

## <a name="next-steps"></a>Passaggi successivi

Potrebbero essere necessari fino a 15 minuti prima che un computer che esegue il client di Azure Information Protection ottenga queste impostazioni modificate. Per informazioni sul download e l'aggiornamento dei modelli nei computer e nei servizi, vedere [Aggiornamento dei modelli per gli utenti](refresh-templates.md).

Tutte le operazioni che è possibile configurare nel portale di Azure per creare e gestire modelli possono essere eseguite tramite PowerShell. Inoltre, PowerShell fornisce più opzioni che non sono disponibili nel portale. Per altre informazioni, vedere la [Guida di riferimento di PowerShell per i modelli personalizzati](configure-templates-with-powershell.md). 

Per altre informazioni sulla configurazione dei criteri di Azure Information Protection, usare i collegamenti nella sezione [Configurazione dei criteri dell'organizzazione](configure-policy.md#configuring-your-organizations-policy).  

