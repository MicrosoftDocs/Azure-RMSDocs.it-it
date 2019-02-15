---
title: "Avvio rapido: Configurare un'etichetta che consente agli utenti di proteggere facilmente i messaggi di posta elettronica contenenti informazioni riservate - AIP"
description: Configurare un'etichetta che protegge un messaggio di posta elettronica di un utente applicando automaticamente la protezione Non inoltrare.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 02/15/2019
ms.topic: quickstart
ms.collection: M365-security-compliance
ms.service: information-protection
ms.openlocfilehash: 67fe46f94b83b219794251c9d7e1500f756669a3
ms.sourcegitcommit: 89d2c2595bc7abda9a8b5e505b7dcf963e18c822
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/14/2019
ms.locfileid: "56266030"
---
# <a name="quickstart-configure-a-label-for-users-to-easily-protect-emails-that-contain-sensitive-information"></a>Guida introduttiva: configurare un'etichetta che consente di proteggere facilmente i messaggi di posta elettronica contenenti informazioni riservate

>*Si applica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*

In questa guida introduttiva si configurerà un'etichetta esistente per l'applicazione automatica dell'impostazione di protezione Non inoltrare.

Gli attuali criteri di Azure Information Protection contengono già due etichette che hanno questa configurazione:

- **Riservato\Solo i destinatari**

- **Riservatezza elevata\Solo i destinatari**

Tuttavia, se i criteri personali sono precedenti o se non è stata attivata la protezione nel momento in cui sono stati creati i criteri dell'organizzazione, queste etichette non sono disponibili. 

È possibile completare questa configurazione in 5 minuti.

## <a name="prerequisites"></a>Prerequisiti

Per completare questa guida introduttiva, è necessario:

1. Disporre di una sottoscrizione che includa un piano 1 o 2 di Azure Information Protection.
    
    In assenza di una di queste sottoscrizioni, è possibile creare un account [gratuito](https://portal.office.com/Signup/Signup.aspx?OfferId=87dd2714-d452-48a0-a809-d2f58c4f68b7) per l'organizzazione.

2. Aver aggiunto il pannello di Azure Information Protection nel portale di Azure e aver verificato che il servizio di protezione è attivato.

    Se occorre assistenza per queste azioni, vedere [Avvio rapido: Attività iniziali nel portale di Azure](quickstart-viewpolicy.md).

3. Un'etichetta esistente di Azure Information Protection da configurare. 
    
    È possibile usare una delle etichette predefinite o un'etichetta creata. Se occorre assistenza per la creazione di una nuova etichetta, vedere [Avvio rapido: Creare una nuova etichetta di Azure Information Protection per utenti specifici](quickstart-label-specificusers.md).

4. Per testare la nuova etichetta: il client Azure Information Protection deve essere installato nei computer degli utenti. 
    
    Per provare l'etichetta, è possibile installare il client accedendo all'[Area download Microsoft](https://www.microsoft.com/en-us/download/details.aspx?id=53018) e scaricare **AzInfoProtection.exe** dalla pagina di Azure Information Protection.

5. Per testare la nuova etichetta: Disporre di un computer con Windows (versione minima Windows 7 con Service Pack 1), in cui è stato eseguito l'accesso alle app di Office da una delle categorie seguenti:
    
    - App di Office con versione minima 1805, build 9330.2078 da Office 365 Business o Microsoft 365 Business quando all'utente viene assegnata una licenza per Azure Rights Management (nota anche come Azure Information Protection per Office 365).
    
    - Office 365 ProPlus.
    
    - Office Professional Plus 2019.
    
    - Office Professional Plus 2016.
    
    - Office Professional Plus 2013 con Service Pack 1.
    
    - Office Professional Plus 2010 con Service Pack 2.

Per un elenco completo dei prerequisiti per l'uso di Azure Information Protection, vedere [Requisiti per Azure Information Protection](requirements.md).

## <a name="configure-an-existing-label-to-apply-the-do-not-forward-protection"></a>Configurare un'etichetta esistente per l'applicazione della protezione Non inoltrare

1. Aprire una nuova finestra del browser e accedere al [portale di Azure](https://portal.azure.com) come amministratore globale. Passare quindi ad **Azure Information Protection**. 
    
    Ad esempio, dal menu hub fare clic su **Tutti i servizi** e iniziare a digitare **Informazioni** nella casella Filtro. Selezionare **Azure Information Protection**.
    
    Se non si è l'amministratore globale, usare il collegamento seguente per i ruoli alternativi: [Accesso al portale di Azure](configure-policy.md#signing-in-to-the-azure-portal)

2. Dall'opzione di menu **Classificazioni** > **Etichette**: nel pannello **Azure Information Protection - Etichette** selezionare l'etichetta che si vuole configurare per l'applicazione della protezione. 

3. Nel pannello **Etichetta** individuare **Configurare il modello RMS per la protezione di documenti e messaggi di posta elettronica contenenti questa etichetta**. Selezionare **Proteggi** e quindi **Protezione**:
    
    ![Configurare la protezione per un'etichetta di Azure Information Protection](./media/info-protect-protection-bar-configured.png).

4. Nel pannello **Protezione** verificare che sia selezionata l'opzione **Azure (cloud key)** (Azure - Chiave cloud).
    
5. Selezionare **Configura le autorizzazioni definite dall'utente (anteprima)**.

6. Assicurarsi che sia selezionata l'opzione seguente: **In Outlook applica Non inoltrare**.

7. Se selezionata, deselezionare l'opzione seguente: **In Word, Excel, PowerPoint e File Explorer richiedi all'utente le autorizzazioni personalizzate**.

8. Fare clic su **OK** nel pannello **Protezione** e quindi fare clic su **Salva** nel pannello **Etichetta**.

L'etichetta è ora configurata per essere visualizzata solo in Outlook e per applicare la protezione Non inoltrare ai messaggi di posta elettronica.

## <a name="test-your-new-label"></a>Testare la nuova etichetta

L'etichetta configurata viene visualizzata solo in Outlook e può essere applicata ai messaggi di posta elettronica inviati a qualsiasi destinatario esterno all'organizzazione se Exchange Online è configurato per le [nuove funzionalità di Crittografia messaggi di Office 365](https://support.office.com/article/7ff0c040-b25c-4378-9904-b1b50210d00e).

1. Nel computer in uso avviare Outlook e creare un nuovo messaggio di posta elettronica. Se Outlook è già aperto, riavviarlo per forzare un aggiornamento dei criteri.

2. Specificare i destinatari, digitare il testo del messaggio di posta elettronica e quindi applicare l'etichetta appena creata. 
    
    Il messaggio di posta elettronica viene classificato in base al nome dell'etichetta e protetto con la restrizione Non inoltrare.

3. Inviare il messaggio di posta elettronica. 

Il risultato è che i destinatari non possono inoltrare il messaggio di posta elettronica, stamparlo, copiarne il contenuto, salvare gli allegati o salvare il messaggio di posta elettronica con un nome diverso. Il messaggio di posta elettronica protetto può essere letto da qualsiasi utente, su qualsiasi dispositivo.

## <a name="clean-up-resources"></a>Pulizia delle risorse

Se non si vuole mantenere questa configurazione e si preferisce ripristinare l'etichetta alla configurazione precedente, in modo che non venga applicata la protezione, seguire la procedura seguente:

1. Dall'opzione di menu **Classificazioni** > **Etichette**: nel pannello **Azure Information Protection - Etichette** selezionare l'etichetta configurata. 

3. Nel pannello **Etichetta** individuare la sezione **Configurare le autorizzazioni per documenti e messaggi di posta elettronica contenenti questa etichetta**, selezionare **Non configurato** e quindi **Salva**.

## <a name="next-steps"></a>Passaggi successivi

Questa guida introduttiva include le informazioni strettamente indispensabili per gli utenti che vogliono configurare rapidamente un'etichetta per la protezione dei propri messaggi di posta elettronica. Se, tuttavia, questa configurazione è troppo restrittiva o non abbastanza restrittiva, vedere le altre configurazioni di esempio:

- [Etichetta per la posta elettronica protetta che supporta autorizzazioni meno restrittive rispetto a Non inoltrare](configure-policy-protection.md#example-4-label-for-protected-email-that-supports-less-restrictive-permissions-than-do-not-forward)

- [Etichetta che crittografa il contenuto, ma non limita chi può accedervi](configure-policy-protection.md#example-5-label-that-encrypts-content-but-doesnt-restrict-who-can-access-it)

Per istruzioni complete su come configurare un'etichetta che applichi la protezione, vedere [Come configurare un'etichetta per la protezione di Rights Management](configure-policy-protection.md). 
