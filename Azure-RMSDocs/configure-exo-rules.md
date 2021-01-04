---
title: Regole del flusso di posta di Exchange Online per le etichette di Azure Information Protection
description: Istruzioni ed esempi per configurare le regole del flusso di posta di Exchange Online per le etichette di Azure Information Protection.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 10/26/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: ba4e4a4d-5280-4e97-8f5c-303907db1bf5
ROBOTS: NOINDEX
ms.reviewer: shakella
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: ca365962d470d009411e4e02de885acd2e7fb043
ms.sourcegitcommit: b32c16e41ba36167b5a3058b56a73183bdd4306d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/29/2020
ms.locfileid: "97806924"
---
# <a name="configuring-exchange-online-mail-flow-rules-for-azure-information-protection-labels"></a>Configurazione delle regole del flusso di posta di Exchange Online per le etichette di Azure Information Protection

>***Si applica a**: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*
>
>***Pertinente per**: [Azure Information Protection client classico per Windows](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients). Per il client di etichettatura unificata, vedere [informazioni sulle etichette di riservatezza e sulle](/microsoft-365/compliance/sensitivity-labels) [etichette DLP](/microsoft-365/compliance/dlp-sensitivity-label-as-condition) dalla documentazione di Microsoft 365. *

> [!NOTE] 
> Per offrire un'esperienza per i clienti unificata e semplificata, il **client classico di Azure Information Protection** e **Gestione etichette** nel portale di Azure saranno **deprecati** a partire dal **31 marzo 2021**. In questo intervallo di tempo tutti i clienti correnti di Azure Information Protection possono passare alla soluzione di etichettatura unificata usando la piattaforma di etichettatura unificata di Microsoft Information Protection. Altre informazioni nell'[avviso ufficiale sulla deprecazione](https://aka.ms/aipclassicsunset).

Usare le informazioni seguenti per configurare le regole del flusso di posta in Exchange Online per usare le etichette di Azure Information Protection e per applicare una protezione aggiuntiva per scenari specifici. Ad esempio:

- L'etichetta predefinita è **Generale**, che non applica la protezione. Per i messaggi di posta elettronica con questa etichetta inviati all'esterno, applicare l'azione di protezione aggiuntiva Non inoltrare.

- Se un allegato con un'etichetta **Riservato\Partner** viene inviato tramite posta elettronica a qualcuno all'esterno dell'organizzazione e il messaggio di posta elettronica non è protetto, applicare l'azione di protezione aggiuntiva Encrypt-Only (Solo crittografia).

Le regole del flusso di posta che applicano la protezione come azione vengono ignorate se il messaggio di posta elettronica è già protetto. Ad esempio, un messaggio di posta elettronica protetto da Non inoltrare non può essere modificato da una regola del flusso di posta di Exchange per usare l'opzione Encrypt-Only (Solo crittografia).  

È possibile estendere questi esempi e anche modificarli, ad esempio aggiungendo altre condizioni. Per altre informazioni sulla configurazione delle regole del flusso di posta, vedere [Regole del flusso (regole di trasporto) di posta in Exchange Online](/exchange/security-and-compliance/mail-flow-rules/mail-flow-rules) nella documentazione di Exchange Online.

Per ulteriori informazioni sulla configurazione delle regole del flusso di posta per crittografare i messaggi di posta elettronica, vedere [definire regole del flusso di posta per crittografare i messaggi di posta elettronica in Microsoft 365](https://support.office.com/article/define-mail-flow-rules-to-encrypt-email-messages-in-office-365-9b7daf19-d5f2-415b-bc43-a0f5f4a585e8) dalla documentazione di Office 

## <a name="prerequisite-know-your-label-guid"></a>Prerequisito: conosce il GUID dell'etichetta

Poiché un'etichetta di Azure Information Protection viene archiviata nei metadati, le regole del flusso di posta in Exchange Online possono leggere queste informazioni per i messaggi e i documenti di Office allegati. Le regole del flusso di posta non supportano l'analisi dei metadati per i documenti PDF.

Prima di configurare le regole del flusso di posta per identificare i messaggi e i documenti etichettati, assicurarsi di conoscere il GUID dell'etichetta di Azure Information Protection che si vuole usare. 

Per altre informazioni sui metadati archiviati da un'etichetta e su come identificare i GUID di etichetta, vedere [Etichettare le informazioni archiviate in documenti e messaggi di posta elettronica](configure-policy.md#label-information-stored-in-emails-and-documents).

## <a name="example-configurations"></a>Configurazioni di esempio

Per gli esempi seguenti, creare una nuova regola del flusso di posta seguendo questa procedura:

1. In un Web browser, usando un account aziendale o dell'Istituto di istruzione a cui sono state concesse le autorizzazioni di amministratore globale, accedere a Microsoft 365. 

2. Scegliere il riquadro **amministratore** .

3. Nell'interfaccia di amministrazione di Microsoft 365 scegliere **admin Centers**  >  **Exchange**.

4. Nell'interfaccia di amministrazione di Exchange: le regole del **flusso di posta**  >    >  **+**  >  **creano una nuova regola**. 

> [!TIP]
> Se si verificano problemi con l'interfaccia utente quando si configurano le regole, provare a usare un browser diverso, ad esempio Internet Explorer.

Gli esempi hanno una sola condizione che applica la protezione quando un messaggio di posta elettronica viene inviato all'esterno dell'organizzazione. Per altre informazioni sulle altre condizioni che è possibile selezionare, vedere [Condizioni ed eccezioni della regola del flusso di posta (predicati) in Exchange Online](/exchange/security-and-compliance/mail-flow-rules/conditions-and-exceptions).


### <a name="example-1-rule-that-applies-the-do-not-forward-option-to-emails-that-are-labeled-general-when-they-are-sent-outside-the-organization"></a>Esempio 1: Regola che applica l'opzione Non inoltrare ai messaggi di posta elettronica con l'etichetta **Generale** quando vengono inviati all'esterno dell'organizzazione

In questo esempio l'etichetta **Generale** ha il GUID 0e421e6d-ea17-4fdb-8f01-93a3e71333b8. Sostituire il GUID della propria etichetta o etichetta secondaria da usare con questa regola. 

Nel criterio Azure Information Protection questa etichetta è stata configurata come predefinita per classificare i messaggi di posta elettronica come **Generale** e l'etichetta non applica la protezione. 

1. In **Nome** digitare un nome per la regola, ad esempio `Apply Do Not Forward for General emails sent externally`.
 
2. Per **Apply this rule if** (Applica questa regola se): selezionare **The recipient is located** (Il destinatario si trova), selezionare **Outside the organization** (Fuori dall'organizzazione) e quindi selezionare **OK**.

3. Selezionare **Altre opzioni** e quindi selezionare **aggiungi condizione**.
 
4. Per **e**: selezionare **A message header** (Un'intestazione del messaggio) e quindi selezionare **includes any of these words** (include una di queste parole):
     
    a. Selezionare **Immetti il testo** e immettere `msip_labels`.
     
    b. Selezionare **Immetti le parole** e immettere `MSIP_Label_0e421e6d-ea17-4fdb-8f01-93a3e71333b8_Enabled=True`
    
    c. Selezionare **+** , quindi fare clic su **OK**.

5. Per **Do the following** (Esegui l'operazione seguente): selezionare **Modify the message security** (Modifica la sicurezza del messaggio) > **Apply Office 365 Message Encryption and rights protection** (Applica Office 365 Message Encryption e la protezione dei diritti) > **Non inoltrare** e quindi selezionare **OK**.
    
    La configurazione della regola dovrebbe ora essere simile alla seguente:  ![ regola del flusso di posta di Exchange Online configurata per un'etichetta di Azure Information Protection-esempio 1](./media/aip-exo-rule-ex1.png)

7. Selezionare **Salva** 

Per altre informazioni sull'opzione Non inoltrare, vedere [Opzione Non inoltrare per i messaggi di posta elettronica](configure-usage-rights.md#do-not-forward-option-for-emails).

### <a name="example-2-rule-that-applies-the-encrypt-only-option-to-emails-when-they-have-attachments-that-are-labeled-confidential--partners-and-these-emails-are-sent-outside-the-organization"></a>Esempio 2: Regola che applica l'opzione Encrypt-Only (Solo crittografia) ai messaggi di posta elettronica quando contengono allegati con l'etichetta **Riservato\Partner** e vengono inviati all'esterno dell'organizzazione

In questo esempio l'etichetta secondaria **Riservato\Partner** ha il GUID 0e421e6d-ea17-4fdb-8f01-93a3e71333b8. Sostituire il GUID della propria etichetta o etichetta secondaria da usare con questa regola. 

Questa etichetta viene usata per classificare e proteggere i documenti usati per la collaborazione con i partner.   

1. In **Nome** digitare un nome per la regola, ad esempio `Apply Encrypt to emails sent externally if protected attachments`.
 
2. Per **Apply this rule if** (Applica questa regola se): selezionare **The recipient is located** (Il destinatario si trova), selezionare **Outside the organization** (Fuori dall'organizzazione) e quindi selezionare **OK**.

3. Selezionare **Altre opzioni** e quindi selezionare **aggiungi condizione**.
 
4. Per **e**: selezionare **Any attachment** (Qualsiasi allegato) e quindi selezionare **has these properties, including any of these words** (con queste proprietà, inclusa una di queste parole):
     
    a. Selezionare **+**  >  **specificare una proprietà di allegato personalizzata**.
  
    b. Per **Proprietà** immettere `MSIP_Label_0e421e6d-ea17-4fdb-8f01-93a3e71333b8_Enabled`.
    
    c. Per **Valore** immettere `True`
    
    d. Selezionare **Salva** e quindi **OK**.

5. Per **Do the following** (Esegui l'operazione seguente): selezionare **Modify the message security** (Modifica la sicurezza del messaggio) > **Apply Office 365 Message Encryption and rights protection** (Applica Office 365 Message Encryption e la protezione dei diritti) > **Crittografa** e quindi selezionare **OK**.
    
    La configurazione della regola dovrebbe ora essere simile alla seguente:  ![ regola del flusso di posta di Exchange Online configurata per un'etichetta di Azure Information Protection-esempio 2](./media/aip-exo-rule-ex2.png)

6. Selezionare **Salva** 

Per altre informazioni sull'opzione Crittografa, vedere [Opzione Encrypt-Only (Solo crittografia) per i messaggi di posta elettronica](configure-usage-rights.md#encrypt-only-option-for-emails).


## <a name="next-steps"></a>Passaggi successivi

Per informazioni sulla creazione e la configurazione delle etichette da usare con le regole del flusso di posta di Exchange Online, vedere [Configurazione dei criteri di Azure Information Protection](configure-policy.md).

Per classificare i messaggi di posta elettronica contenenti allegati, considerare la possibilità di usare l'[impostazione dei criteri](configure-policy-settings.md) di Azure Information Protection seguente: **Per i messaggi di posta elettronica con allegati, applicare un'etichetta corrispondente alla classificazione più elevata di questi allegati**.