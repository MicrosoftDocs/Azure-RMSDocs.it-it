---
title: "Avvio rapido: Configurare un'etichetta che consente agli utenti di proteggere facilmente i messaggi di posta elettronica con Azure Information Protection (AIP)"
description: Configurare un'etichetta che protegge un messaggio di posta elettronica di un utente applicando automaticamente la protezione Non inoltrare.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 08/04/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: aiplabels
ms.custom: admin
ms.openlocfilehash: 6c669ec54448840276e409a41dde8e5149fe742e
ms.sourcegitcommit: f6d536b6a3b5e14e24f0b9e58d17a3136810213b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/26/2021
ms.locfileid: "98809360"
---
# <a name="quickstart-configure-a-label-for-users-to-easily-protect-emails-that-contain-sensitive-information"></a>Guida introduttiva: configurare un'etichetta che consente di proteggere facilmente i messaggi di posta elettronica contenenti informazioni riservate

>***Si applica a**: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*
>
> ***Rilevante per**: [Client classico Azure Information Protection per Windows](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

>[!NOTE]
> Per offrire un'esperienza per i clienti unificata e semplificata, il **client classico di Azure Information Protection** e **Gestione etichette** nel portale di Azure saranno **deprecati** a partire dal **31 marzo 2021**. In questo intervallo di tempo tutti i clienti correnti di Azure Information Protection possono passare alla soluzione di etichettatura unificata usando la piattaforma di etichettatura unificata di Microsoft Information Protection. Altre informazioni nell'[avviso ufficiale sulla deprecazione](https://aka.ms/aipclassicsunset).

In questo avvio rapido si configurerà un'etichetta di Azure Information Protection esistente per l'applicazione automatica dell'impostazione di protezione **Non inoltrare**.

Gli attuali criteri di Azure Information Protection contengono già due etichette che hanno questa configurazione:

- **Riservato\Solo i destinatari**

- **Riservatezza elevata\Solo i destinatari**

Tuttavia, se i criteri personali sono precedenti o se non è stata attivata la protezione nel momento in cui sono stati creati i criteri dell'organizzazione, queste etichette non sono disponibili.

**Tempo necessario**: È possibile completare questa configurazione in 5 minuti.

## <a name="prerequisites"></a>Prerequisiti

Per completare questa guida introduttiva, è necessario:

|Requisito  |Descrizione  |
|---------|---------|
|**Una sottoscrizione di supporto**     |  Sarà necessaria una sottoscrizione che includa [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection/). <br><br>In assenza di una di queste sottoscrizioni, è possibile creare un account [gratuito](https://admin.microsoft.com/Signup/Signup.aspx?OfferId=87dd2714-d452-48a0-a809-d2f58c4f68b7) per l'organizzazione.       |
|**AIP aggiunto al portale di Azure**    |  Aver aggiunto il riquadro Azure Information Protection al portale di Azure e aver verificato che il servizio di protezione sia attivato. <br><br>Per altre informazioni, vedere [Avvio rapido: Attività iniziali nel portale di Azure](quickstart-viewpolicy.md).       |
|**Un'etichetta esistente di Azure Information Protection da configurare**     | Usare una delle etichette predefinite o un'etichetta creata. Per altre informazioni, vedere [Avvio rapido: Creare una nuova etichetta di Azure Information Protection per utenti specifici](quickstart-label-specificusers.md). |
|**Client classico installato**    |   Per testare la nuova etichetta, è necessario che il client classico sia installato nel computer. <br><br>Il client classico Azure Information Protection verrà deprecato nel marzo 2021. Per distribuire il client classico AIP, aprire un ticket di supporto per ottenere l'accesso al download.  |
|**Un computer Windows, connesso alle app di Office** |Per testare la nuova etichetta, è necessario un computer che esegue Windows (almeno Windows 7 con Service Pack 1). <br><br>In questo computer accedere a una delle seguenti versioni delle app di Office: <br><br>- **App di Office** per le versioni elencate nella [tabella delle versioni supportate di Microsoft 365 Apps in base al canale di aggiornamento](/officeupdates/update-history-microsoft365-apps-by-date), da Microsoft 365 Apps for business o Microsoft 365 Business Premium quando all'utente è assegnata una licenza per Azure Rights Management (noto anche come Azure Information Protection per Office 365). <br>- **Microsoft 365 Apps for enterprise** <br>- **Office Professional Plus 2019** <br>- **Office Professional Plus 2016**<br>- **Office Professional Plus 2013 con Service Pack 1**<br>- **Office Professional Plus 2010 con Service Pack 2**|
| | |

Per un elenco completo dei prerequisiti per l'uso di Azure Information Protection, vedere [Requisiti per Azure Information Protection](requirements.md).

## <a name="configure-an-existing-label-to-apply-the-do-not-forward-protection"></a>Configurare un'etichetta esistente per l'applicazione della protezione Non inoltrare

1. Aprire una nuova finestra del browser e accedere al [portale di Azure](https://portal.azure.com) come amministratore globale. Passare quindi ad **Azure Information Protection**.

    Ad esempio, nella casella di ricerca di risorse, servizi e documentazione: iniziare a digitare **Information** e selezionare **Azure Information Protection**.

    Se non si è l'amministratore globale, usare il collegamento seguente per i ruoli alternativi: [Accesso al portale di Azure](configure-policy.md#signing-in-to-the-azure-portal)

1. Dall'opzione di menu **Classificazioni** > **Etichette**: nel riquadro **Azure Information Protection - Etichette** selezionare l'etichetta che si vuole configurare per applicare la protezione.

1. Nel riquadro **Etichetta** individuare **Configurare le autorizzazioni per documenti e messaggi di posta elettronica contenenti questa etichetta**. Selezionare **Proteggi** e il riquadro **Protezione** si apre automaticamente se in precedenza è stato selezionato **Non configurato** o **Rimuovi protezione**.

    Se il riquadro **Protezione** non si apre automaticamente, selezionare **Protezione**:

    :::image type="content" source="media/info-protect-protection-bar-configured.png" alt-text="Configurare la protezione per un'etichetta di Azure Information Protection":::

1. Nel riquadro **Protezione** verificare che l'opzione **Azure (chiave cloud)** sia selezionata.

1. Selezionare **Configura le autorizzazioni definite dall'utente (anteprima)** .

1. Assicurarsi che sia selezionata l'opzione seguente: **In Outlook applica Non inoltrare**.

1. Se selezionata, deselezionare l'opzione seguente: **In Word, Excel, PowerPoint e File Explorer richiedi all'utente le autorizzazioni personalizzate**.

1. Fare clic su **OK** nel riquadro **Protezione** e quindi su **Salva** nel riquadro **Etichetta**.

L'etichetta è ora configurata per essere visualizzata solo in Outlook e per applicare la protezione **Non inoltrare** ai messaggi di posta elettronica.

## <a name="test-your-new-label"></a>Testare la nuova etichetta

L'etichetta configurata viene visualizzata solo in Outlook e può essere applicata ai messaggi di posta elettronica inviati a qualsiasi destinatario esterno all'organizzazione se Exchange Online è configurato per le [nuove funzionalità di Crittografia messaggi di Office 365](https://support.office.com/article/7ff0c040-b25c-4378-9904-b1b50210d00e).

1. Nel computer in uso avviare Outlook e creare un nuovo messaggio di posta elettronica. Se Outlook è già aperto, riavviarlo per forzare un aggiornamento dei criteri.

2. Specificare i destinatari, digitare il testo del messaggio di posta elettronica e quindi applicare l'etichetta appena creata.

    Il messaggio di posta elettronica viene classificato in base al nome dell'etichetta e protetto con la restrizione Non inoltrare.

3. Inviare il messaggio di posta elettronica.

I destinatari non possono quindi inoltrare il messaggio di posta elettronica, né stamparlo, copiarne il contenuto, salvarne gli allegati o salvarlo con un altro nome. Il messaggio di posta elettronica protetto può essere letto da qualsiasi utente, su qualsiasi dispositivo.

## <a name="clean-up-resources"></a>Pulizia delle risorse

Se non si vuole mantenere questa configurazione e si preferisce ripristinare l'etichetta alla configurazione precedente, in modo che non venga applicata la protezione, seguire la procedura seguente:

1. Dall'opzione di menu **Classificazioni** > **Etichette**: nel riquadro **Azure Information Protection - Etichette** selezionare l'etichetta configurata.

1. Nel riquadro **Etichetta** individuare **Configurare le autorizzazioni per documenti e messaggi di posta elettronica contenenti questa etichetta**, selezionare **Non configurato** e quindi **Salva**.

## <a name="next-steps"></a>Passaggi successivi

Questa guida introduttiva include le informazioni strettamente indispensabili per gli utenti che vogliono configurare rapidamente un'etichetta per la protezione dei propri messaggi di posta elettronica. Se, tuttavia, questa configurazione è troppo restrittiva o non abbastanza restrittiva, vedere le altre configurazioni di esempio:

- [Etichetta per la posta elettronica protetta che supporta autorizzazioni meno restrittive rispetto a Non inoltrare](configure-policy-protection.md#example-4-label-for-protected-email-that-supports-less-restrictive-permissions-than-do-not-forward)

- [Etichetta che crittografa il contenuto, ma non limita chi può accedervi](configure-policy-protection.md#example-5-label-that-encrypts-content-but-doesnt-restrict-who-can-access-it)

Per istruzioni complete su come configurare un'etichetta che applichi la protezione, vedere [Come configurare un'etichetta per la protezione di Rights Management](configure-policy-protection.md).
