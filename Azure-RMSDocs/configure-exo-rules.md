---
title: Regole del flusso di posta di Exchange Online per le etichette di Azure Information Protection
description: Istruzioni ed esempi per configurare le regole del flusso di posta di Exchange Online per le etichette di Azure Information Protection.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 07/24/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: ba4e4a4d-5280-4e97-8f5c-303907db1bf5
ms.reviewer: shakella
ms.suite: ems
ms.openlocfilehash: f738f990e6a4c2f79e4eede12431c1afe15803cd
ms.sourcegitcommit: 7992e1dc791d6d919036f7aa98bcdd21a6c32ad0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/24/2019
ms.locfileid: "68428550"
---
# <a name="configuring-exchange-online-mail-flow-rules-for-azure-information-protection-labels"></a>Configurazione delle regole del flusso di posta di Exchange Online per le etichette di Azure Information Protection

>*Si applica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

Usare le informazioni seguenti per configurare le regole del flusso di posta in Exchange Online per usare le etichette di Azure Information Protection e per applicare una protezione aggiuntiva per scenari specifici. Ad esempio:

- L'etichetta predefinita è **Generale**, che non applica la protezione. Per i messaggi di posta elettronica con questa etichetta inviati all'esterno, applicare l'azione di protezione aggiuntiva Non inoltrare.

- Se un allegato con un'etichetta **Riservato\Partner** viene inviato tramite posta elettronica a qualcuno all'esterno dell'organizzazione e il messaggio di posta elettronica non è protetto, applicare l'azione di protezione aggiuntiva Encrypt-Only (Solo crittografia).

Le regole del flusso di posta che applicano la protezione come azione vengono ignorate se il messaggio di posta elettronica è già protetto. Ad esempio, un messaggio di posta elettronica protetto da Non inoltrare non può essere modificato da una regola del flusso di posta di Exchange per usare l'opzione Encrypt-Only (Solo crittografia).  

È possibile estendere questi esempi e anche modificarli, ad esempio aggiungendo altre condizioni. Per altre informazioni sulla configurazione delle regole del flusso di posta, vedere [Regole del flusso (regole di trasporto) di posta in Exchange Online](https://technet.microsoft.com/library/jj919238(v=exchg.150).aspx) nella documentazione di Exchange Online.

Per altre informazioni sulla configurazione di regole del flusso di posta per crittografare i messaggi di posta elettronica, vedere [Definire le regole del flusso di posta elettronica per crittografare i messaggi di posta elettronica in Office 365](https://support.office.com/article/define-mail-flow-rules-to-encrypt-email-messages-in-office-365-9b7daf19-d5f2-415b-bc43-a0f5f4a585e8) nella documentazione di Office. 

## <a name="prerequisite-know-your-label-guid"></a>Prerequisito: Conoscere il GUID dell'etichetta

Poiché un'etichetta di Azure Information Protection viene archiviata nei metadati, le regole del flusso di posta in Exchange Online possono leggere queste informazioni per i messaggi e i documenti di Office allegati. Le regole del flusso di posta non supportano l'analisi dei metadati per i documenti PDF.

Prima di configurare le regole del flusso di posta per identificare i messaggi e i documenti etichettati, assicurarsi di conoscere il GUID dell'etichetta di Azure Information Protection che si vuole usare. 

Per altre informazioni sui metadati archiviati da un'etichetta e su come identificare i GUID di etichetta, vedere [Etichettare le informazioni archiviate in documenti e messaggi di posta elettronica](configure-policy.md#label-information-stored-in-emails-and-documents).

## <a name="example-configurations"></a>Configurazioni di esempio

Per gli esempi seguenti, creare una nuova regola del flusso di posta seguendo questa procedura:

1. In un Web browser, usando un account aziendale o dell'istituto di istruzione a cui sono state concesse le autorizzazioni di amministratore globale, accedere a Office 365. 

2. Scegliere il riquadro **Amministrazione**.

3. Nell'interfaccia di amministrazione di Microsoft 365 scegliere **Interfacce di amministrazione** > **Exchange**.

4. Nell'interfaccia di amministrazione di Exchange: **flusso di posta** > **regole** >  **+**  > **Create a new rule** (Crea una nuova regola). 

> [!TIP]
> Se si verificano problemi con l'interfaccia utente quando si configurano le regole, provare a usare un browser diverso, ad esempio Internet Explorer.

Gli esempi hanno una sola condizione che applica la protezione quando un messaggio di posta elettronica viene inviato all'esterno dell'organizzazione. Per altre informazioni sulle altre condizioni che è possibile selezionare, vedere [Condizioni ed eccezioni della regola del flusso di posta (predicati) in Exchange Online](https://technet.microsoft.com/library/jj919235(v=exchg.150).aspx).


### <a name="example-1-rule-that-applies-the-do-not-forward-option-to-emails-that-are-labeled-general-when-they-are-sent-outside-the-organization"></a>Esempio 1: Regola che applica l'opzione Non inoltrare ai messaggi di posta elettronica con l'etichetta **Generale** quando vengono inviati all'esterno dell'organizzazione

In questo esempio l'etichetta **Generale** ha il GUID 0e421e6d-ea17-4fdb-8f01-93a3e71333b8. Sostituire il GUID della propria etichetta o etichetta secondaria da usare con questa regola. 

Nel criterio Azure Information Protection questa etichetta è stata configurata come predefinita per classificare i messaggi di posta elettronica come **Generale** e l'etichetta non applica la protezione. 

1. In **Nome** digitare un nome per la regola, ad esempio `Apply Do Not Forward for General emails sent externally`.
 
2. Per **Apply this rule if** (Applica questa regola se): selezionare **The recipient is located** (Il destinatario si trova), **Outside the organization** (All'esterno dell'organizzazione) e quindi **OK**.

3. Selezionare **Altre opzioni** e quindi selezionare **aggiungi condizione**.
 
4. Per **e**: selezionare **A message header** (Un'intestazione del messaggio) e quindi **includes any of these words** (include una di queste parole):
     
    a. Selezionare **Immetti il testo** e immettere `msip_labels`.
     
    b. Selezionare **Immetti le parole** e immettere `MSIP_Label_0e421e6d-ea17-4fdb-8f01-93a3e71333b8_Enabled=True;`
    
    c. Selezionare **+** e quindi **OK**.

5. Per **Do the following** (Eseguire le operazioni seguenti): selezionare **Modify the message security (Modifica la sicurezza del messaggio)**  > **Apply Office 365 Message Encryption and rights protection (Applica Office 365 Message Encryption e la protezione dei diritti)**  > **Non inoltrare** e quindi selezionare **OK**.
    
    La configurazione della regola ora dovrebbe essere simile alla seguente:  ![Regola del flusso di posta di Exchange Online configurata per un'etichetta di Azure Information Protection-esempio 1](./media/aip-exo-rule-ex1.png)

7. Selezionare **Salva** 

Per altre informazioni sull'opzione Non inoltrare, vedere [Opzione Non inoltrare per i messaggi di posta elettronica](configure-usage-rights.md#do-not-forward-option-for-emails).

### <a name="example-2-rule-that-applies-the-encrypt-only-option-to-emails-when-they-have-attachments-that-are-labeled-confidential--partners-and-these-emails-are-sent-outside-the-organization"></a>Esempio 2: Regola che applica l'opzione Encrypt-Only (Solo crittografia) ai messaggi di posta elettronica quando contengono allegati con l'etichetta **Riservato\Partner** e vengono inviati all'esterno dell'organizzazione

In questo esempio l'etichetta secondaria **Riservato\Partner** ha il GUID 0e421e6d-ea17-4fdb-8f01-93a3e71333b8. Sostituire il GUID della propria etichetta o etichetta secondaria da usare con questa regola. 

Questa etichetta viene usata per classificare e proteggere i documenti usati per la collaborazione con i partner.   

1. In **Nome** digitare un nome per la regola, ad esempio `Apply Encrypt to emails sent externally if protected attachments`.
 
2. Per **Apply this rule if** (Applica questa regola se): selezionare **The recipient is located** (Il destinatario si trova), **Outside the organization** (All'esterno dell'organizzazione) e quindi **OK**.

3. Selezionare **Altre opzioni** e quindi selezionare **aggiungi condizione**.
 
4. Per **e**: selezionare **Any attachment** (Qualsiasi allegato) e quindi selezionare **has these properties, including any of these words** (con queste proprietà, inclusa una di queste parole):
     
    a. Selezionare **+**  > **Specify a custom attachment property** (Specifica una proprietà allegato personalizzata).
  
    b. Per **Proprietà** immettere `MSIP_Label_0e421e6d-ea17-4fdb-8f01-93a3e71333b8_Enabled`.
    
    c. Per **Valore** immettere `True`
    
    d. Selezionare **Salva** e quindi **OK**.

5. Per **Do the following** (Eseguire le operazioni seguenti): selezionare **Modify the message security (Modifica la sicurezza del messaggio)**  > **Apply Office 365 Message Encryption and rights protection (Applica Office 365 Message Encryption e la protezione dei diritti)**  > **Crittografa** e quindi selezionare **OK**.
    
    La configurazione della regola ora dovrebbe essere simile alla seguente:  ![Regola del flusso di posta di Exchange Online configurata per un'etichetta di Azure Information Protection-esempio 2](./media/aip-exo-rule-ex2.png)

6. Selezionare **Salva** 

Per altre informazioni sull'opzione Crittografa, vedere [Opzione Encrypt-Only (Solo crittografia) per i messaggi di posta elettronica](configure-usage-rights.md#encrypt-only-option-for-emails).


## <a name="next-steps"></a>Passaggi successivi

Per informazioni sulla creazione e la configurazione delle etichette da usare con le regole del flusso di posta di Exchange Online, vedere [Configurazione dei criteri di Azure Information Protection](configure-policy.md).

Inoltre, per consentire la classificazione dei messaggi di posta elettronica che contengono allegati, considerare l'uso della seguente [impostazione di criteri](configure-policy-settings.md) di Azure Information Protection: **For email messages with attachments, apply a label that matches the highest classification of those attachments** (Per i messaggi di posta elettronica con allegati, applica un'etichetta che corrisponda alla classificazione più elevata di tali allegati).


