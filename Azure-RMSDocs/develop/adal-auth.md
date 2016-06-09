---
# required metadata

title: Autenticazione ADAL per l'applicazione abilitata per RMS | Azure RMS
description: Descrive il processo per l'autenticazione con ADAL
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
** Il contenuto di questo SDK non è aggiornato. Per un breve periodo, la [versione attuale](https://msdn.microsoft.com/library/windows/desktop/hh535290(v=vs.85).aspx) della documentazione sarà disponibile su MSDN. **
# Autenticazione ADAL per l'applicazione abilitata per RMS

L'autenticazione con Azure RMS per l'app usando Azure ADAL è ora inclusa nel client RMS 2.1.

Eseguendo l'aggiornamento dell'applicazione per l'uso dell'autenticazione ADAL anziché dell'Assistente per l'accesso a Microsoft Online, l'utente e i clienti potranno:

- Usare Multi-Factor Authentication
- Installare il client RMS 2.1 senza necessità di privilegi amministrativi sul computer
- Certificare l'applicazione per Windows 10

## Due approcci per l'autenticazione

In questo argomento sono descritti due approcci per l'autenticazione con i relativi esempi di codice.

- **Autenticazione interna**: autenticazione OAuth gestita da RMS SDK. Usare questo approccio per fare in modo che il client RMS visualizzi una richiesta di autenticazione ADAL quando è necessaria l'autenticazione. Per informazioni dettagliate sulla configurazione dell'applicazione, vedere la sezione "Autenticazione interna".

> [!NOTE] Se l'applicazione usa AD RMS SDK 2.1 con l'Assistente per l'accesso, è consigliabile utilizzare il metodo di autenticazione interna come percorso di migrazione dell'applicazione.

- **Autenticazione esterna**: autenticazione OAuth gestita dall'applicazione. Usare questo approccio per fare in modo che l'applicazione gestisca la propria autenticazione OAuth. Con questo approccio, il client RMS eseguirà un callback definito dall'applicazione quando è necessaria l'autenticazione. Per un esempio dettagliato, vedere "Autenticazione esterna" alla fine di questo argomento.

> [!NOTE] L'autenticazione esterna non implica la possibilità di modificare gli utenti: il client RMS usa sempre l'utente predefinito per un determinato tenant RMS.

### Autenticazione interna

Sono necessari:

- Un [abbonamento a Microsoft Azure](https://azure.microsoft.com/en-us/) (è sufficiente la versione di prova gratuita):
- Un abbonamento a Microsoft Azure Rights Management (è sufficiente un account [RMS per utenti singoli](https://technet.microsoft.com/en-us/library/dn592127.aspx) gratuito).

> [!NOTE] Chiedere all'amministratore IT se si dispone di un abbonamento a Microsoft Azure Rights Management e richiedere all'amministratore IT di eseguire i passaggi descritti di seguito. Se l'organizzazione non dispone di un abbonamento, è necessario che l'amministratore IT crei un nuovo abbonamento. Inoltre, è necessario che l'amministratore IT sottoscriva l'abbonamento con un account aziendale o dell'istituto di istruzione anziché un account Microsoft, ovvero un account Hotmail.

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

- Aggiungere un URI di reindirizzamento e scegliere Avanti. È necessario che l'URI di reindirizzamento sia un URI valido e univoco nella directory. Ad esempio, è possibile specificare `com.mycompany.myapplication://authorize`.

![Aggiungere un URI di reindirizzamento](../media/RedirectURI.png)

- Selezionare l'applicazione nella directory e scegliere **Configura**.

![Scegliere Configura](../media/ConfigYourApp.png)

>[!NOTE] Copiare l'**ID client** e l'**URI di reindirizzamento** e archiviarli per usarli in seguito durante la configurazione del client RMS.

- Scorrere nella parte inferiore delle impostazioni dell'applicazione e scegliere il pulsante **Aggiungi applicazione** in **Autorizzazioni per altre applicazioni**.

![Selezionare Aggiungi applicazione](../media/PermissionsToOtherBtn.png)

- Aggiungere questo GUID `00000012-0000-0000-c000-000000000000` nella casella di modifica **Che inizia con** e scegliere il pulsante con il segno di spunta.

![Aggiungere il GUID](../media/AddGUID.png)

- Scegliere il pulsante Più (+) accanto a **Microsoft Rights Management**.

![Selezionare il pulsante +](../media/ChoosePlusBtn.png)

- Scegliere il segno di spunta nell'angolo inferiore sinistro della finestra di dialogo.

![Scegliere il segno di spunta](../media/ChooseCheck.png)

- È ora possibile aggiungere una dipendenza all'applicazione per Azure RMS. Per aggiungere la dipendenza, selezionare la nuova voce **Microsoft Rights Management Services** in **Autorizzazioni per altre applicazioni** e selezionare la casella di controllo **Creare e accedere al contenuto protetto per gli utenti** in **Autorizzazioni delegate**.

![Impostare le autorizzazioni](../media/AddDependency.png)

- Salvare l'applicazione per rendere permanenti le modifiche scegliendo l'icona **Salva** nella parte inferiore centrale del portale.

![Selezionare Salva](../media/SaveApplication.png)

- È ora possibile configurare l'applicazione per l'uso dall'autenticazione ADAL interna inclusa in RMS SDK 2.1. Per configurare il client RMS, aggiungere una chiamata a [IpcSetGlobalProperty](/rights-management/sdk/2.1/api/win/IpcSetGlobalProperty) dopo la chiamata a [IpcInitialize](/rights-management/sdk/2.1/api/win/IpcInitialize) per configurare il client RMS. Usare il frammento di codice seguente come esempio.


    IpcInitialize();

    IPC_AAD_APPLICATION_ID applicationId = { 0 };   applicationId.cbSize = sizeof(IPC_AAD_APPLICATION_ID);   applicationId.wszClientId = L"GUID-provided-by-AAD-for-your-app-(no-brackets)";   applicationId.wszRedirectUri = L"RedirectionUriWeProvidedAADForOurApp://authorize";

    HRESULT hr = IpcSetGlobalProperty(IPC_EI_APPLICATION_ID, &amp;applicationId);

    if (FAILED(hr)) {    //Handle the error   }

### Autenticazione esterna

- Usare il codice seguente come esempio per la gestione dei token di autenticazione.


    extern HRESULT GetADALToken(LPVOID pContext, const IPC_NAME_VALUE_LIST&amp; Parameters, __out wstring wstrToken) throw();

    HRESULT GetLicenseKey(PCIPC_BUFFER pvLicense, __in LPVOID pContextForAdal, __out IPC_KEY_HANDLE &amp;hKey) { IPC_OAUTH2_CALLBACK pfGetADALToken =         [](LPVOID pvContext, PIPC_NAME_VALUE_LIST pParameters, IPC_AUTH_TOKEN_HANDLE* phAuthToken) -&gt; HRESULT { wstring wstrToken; HRESULT hr = GetADALToken(pvContext, *pParameters, wstrToken); return SUCCEEDED(hr) ? IpcCreateOAuth2Token(wstrToken.c_str(), OUT phAuthToken) : hr; };

      IPC_OAUTH2_CALLBACK_INFO callbackCredentialContext =
      {
          sizeof(IPC_OAUTH2_CALLBACK_INFO),
          pfGetADALToken,
          pContextForAdal
      };

      IPC_CREDENTIAL credentialContext =
      {
          IPC_CREDENTIAL_TYPE_OAUTH2,
          NULL
      };
      credentialContext.pcOAuth2 = &amp;callbackCredentialContext;

      IPC_PROMPT_CTX promptContext =
      {
        sizeof(IPC_PROMPT_CTX),
        NULL,
        IPC_PROMPT_FLAG_SILENT | IPC_PROMPT_FLAG_HAS_USER_CONSENT,
        NULL,
        &amp;credentialContext
      };

      hKey = 0L;
      return IpcGetKey(pvLicense, 0, &amp;promptContext, NULL, &amp;hKey);
  }

### Argomenti correlati
- [Tipi di dati](/rights-management/sdk/2.1/api/win/Data%20types)
- [Proprietà di ambiente](/rights-management/sdk/2.1/api/win/Environment%20properties)
- [IpcCreateOAuth2Token](/rights-management/sdk/2.1/api/win/IpcCreateOAuth2Token)
- [IpcGetKey](/rights-management/sdk/2.1/api/win/IpcGetKey)
- [IpcInitialize](/rights-management/sdk/2.1/api/win/IpcInitialize)
- [IPC_CREDENTIAL](/rights-management/sdk/2.1/api/win/IPC\_CREDENTIAL)
- [IPC_NAME_VALUE_LIST](/rights-management/sdk/2.1/api/win/IPC\_NAME\_VALUE\_LIST)
- [IPC_OAUTH2_CALLBACK_INFO](/rights-management/sdk/2.1/api/win/IPC\_OAUTH2\_CALLBACK\_INFO)
- [IPC_PROMPT_CTX](/rights-management/sdk/2.1/api/win/IPC\_PROMPT\_CTX)
- [IPC_AAD_APPLICATION_ID](/rights-management/sdk/2.1/api/win/IPC\_AAD\_APPLICATION\_ID)


<!--HONumber=Jun16_HO1-->


