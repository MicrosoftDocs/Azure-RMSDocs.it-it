---
# required metadata

title: Configurare Azure RMS per l'autenticazione ADAL | Azure RMS
description: Illustra i passaggi per configurare l'autenticazione basata su Azure ADAL
keywords: authentication, RMS, ADAL
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: f89f59b7-33d1-4ab3-bb64-1e9bda269935

# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Configurare Azure RMS per l'autenticazione ADAL

Questo argomento illustra i passaggi per configurare l'autenticazione basata su Azure ADAL.

## Configurazione dell'autenticazione di Azure

Sono necessari:

- Una [sottoscrizione Microsoft Azure](https://azure.microsoft.com/en-us/) (è sufficiente una versione di prova gratuita). Per altre informazioni, vedere [How users sing up for RMS for individuals](../understand-explore/rms-for-individuals-user-sign-up.md) (Come eseguire l'iscrizione a RMS per utenti singoli).
- Un abbonamento a Microsoft Azure Rights Management (è sufficiente un account [RMS per utenti singoli](https://technet.microsoft.com/en-us/library/dn592127.aspx) gratuito).

> [!NOTE] Chiedere all'amministratore IT se si dispone di un abbonamento a Microsoft Azure Rights Management e richiedere all'amministratore IT di eseguire i passaggi descritti di seguito. Se l'organizzazione non dispone di un abbonamento, è necessario che l'amministratore IT crei un nuovo abbonamento. Inoltre, è necessario che l'amministratore IT sottoscriva l'abbonamento con un *account aziendale o dell'istituto di istruzione* anziché un *account Microsoft*, ad esempio un account Hotmail.

Dopo aver effettuato l'iscrizione a Microsoft Azure:

- Accedere al [portale di gestione di Azure](https://manage.windowsazure.com) per l'organizzazione usando un account con privilegi amministrativi.

![Accesso ad Azure](../media/AzurePortalLogin.png)

- Scorrere verso il basso fino all'applicazione **Active Directory** a sinistra del portale.

![Selezionare Active Directory](../media/AzureADPick.png)

- Se non è già stata creata una directory, scegliere il pulsante **Nuovo** nell'angolo inferiore sinistro del portale.

![Selezionare Nuovo](../media/AzureNewBtn.png)

- Selezionare la scheda **Rights Management** è assicurarsi che lo **Stato Rights Management** sia **Attivo**, **Sconosciuto** o **Non autorizzato**. Se lo stato è **Inattivo**, scegliere il pulsante **Attiva** nella parte inferiore centrale del portale e confermare la selezione.

![Scegliere Attiva](../media/RMTab.png)

- Creare una nuova *applicazione nativa* nella directory selezionando la directory e scegliendo Applicazioni.

![Selezionare Applicazioni](../media/CreateNativeApp.png)

- Scegliere quindi il pulsante **Aggiungi** nella parte inferiore centrale del portale.

![Selezionare Aggiungi](../media/AddAppBtn.png)

- Al prompt scegliere **Aggiungi un'applicazione che l'organizzazione sta sviluppando**.

![Selezionare Aggiungi un'applicazione che l'organizzazione sta sviluppando](../media/AddAnAppPick.png)

- Assegnare un nome all'applicazione selezionando **Applicazione client nativa** e scegliendo il pulsante **Avanti**.

![Assegnare un nome all'applicazione](../media/TellUsInput.png)

- Aggiungere un URI di reindirizzamento e scegliere Avanti.
  È necessario che l'URI di reindirizzamento sia un URI valido e univoco nella directory. Ad esempio, è possibile specificare `com.mycompany.myapplication://authorize`.

![Aggiungere un URI di reindirizzamento](../media/RedirectURI.png)

- Selezionare l'applicazione nella directory e scegliere **Configura**.

![Scegliere Configura](../media/ConfigYourApp.png)

>[!NOTE] Copiare l'**ID client** e l'**URI di reindirizzamento** e archiviarli per usarli in seguito durante la configurazione del client RMS.

- Scorrere nella parte inferiore delle impostazioni dell'applicazione e scegliere il pulsante **Aggiungi applicazione** in **Autorizzazioni per altre applicazioni**.

>[!NOTE] Le **Autorizzazioni delegate** che vengono visualizzate per Windows Azure Active Directory sono corrette per impostazione predefinita; oltre alle impostazioni predefinite è necessario selezionare soltanto l'opzione **Accedi e leggi il profilo di un altro utente**.

![Selezionare Aggiungi applicazione](../media/PermissionsToOtherBtn.png)

- Aggiungere questo GUID `00000012-0000-0000-c000-000000000000` nella casella di modifica **Che inizia con** e scegliere il pulsante con il segno di spunta.

![Aggiungere il GUID](../media/AddGUID.png)

- Scegliere il pulsante Più accanto a **Microsoft Rights Management**.

![Selezionare il pulsante +](../media/ChoosePlusBtn.png)

- Scegliere il segno di spunta nell'angolo inferiore sinistro della finestra di dialogo.

![Scegliere il segno di spunta](../media/ChooseCheck.png)

- È ora possibile aggiungere una dipendenza all'applicazione per Azure RMS. Per aggiungere la dipendenza, selezionare la nuova voce **Microsoft Rights Management Services** in **Autorizzazioni per altre applicazioni** e selezionare la casella di controllo **Creare e accedere al contenuto protetto per gli utenti** in **Autorizzazioni delegate**.

![Impostare le autorizzazioni](../media/AddDependency.png)

- Salvare l'applicazione per rendere permanenti le modifiche scegliendo l'icona **Salva** nella parte inferiore centrale del portale.

![Selezionare Salva](../media/SaveApplication.png)


<!--HONumber=Jun16_HO2-->


