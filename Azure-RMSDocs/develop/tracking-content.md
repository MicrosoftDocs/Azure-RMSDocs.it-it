---
title: Come abilitare la revoca e il rilevamento dei documenti | Azure RMS
description: "Linee guida di base per implementare il rilevamento del contenuto del documento, nonché un codice di esempio per aggiornare i metadati e un pulsante Rileva utilizzo per l&quot;app."
keywords: 
author: bruceperlerms
ms.author: bruceper
manager: mbaldwin
ms.date: 02/23/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: F5089765-9D94-452B-85E0-00D22675D847
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
experimental: true
experiment_id: priyamo-test-20160729
translationtype: Human Translation
ms.sourcegitcommit: 7068e0529409eb783f16bc207a17be27cd5d82a8
ms.openlocfilehash: 1e1bf622bfae4d2cca3b30798dbf6cb5c794e24a


---

# <a name="how-to-enable-document-tracking-and-revocation"></a>Procedura: Abilitare la revoca e il rilevamento dei documenti

Questo argomento illustra le linee guida di base per implementare il rilevamento del contenuto del documento, nonché un codice di esempio per aggiornare i metadati e per creare il pulsante **Rileva utilizzo** per l'app.

## <a name="steps-to-implement-document-tracking"></a>Passaggi per implementare il rilevamento del documento

I passaggi 1 e 2 consentono il rilevamento del documento. Il passaggio 3 consente agli utenti delle app di raggiungere il sito per rilevare e revocare i documenti protetti.

1. Aggiungere i metadati associati al rilevamento dei documenti
2. Registrare il documento con il servizio RMS
3. Aggiungere il pulsante Rileva utilizzo all'app

Seguono i dettagli di implementazione per questi passaggi.

## <a name="1-add-document-tracking-metadata"></a>1. Aggiungere i metadati associati al rilevamento dei documenti

Rilevamento dei documenti è una funzionalità del sistema di Rights Management. L'aggiunta di metadati specifici durante il processo di protezione di un documento fa sì che si possa registrare il documento stesso con il portale del servizio di rilevamento, che fornisce quindi diverse opzioni per il rilevamento.

Usare queste API per aggiungere o aggiornare una licenza con i metadati di rilevamento dei documenti.


Dal punto di vista operativo, solo le proprietà relative al **nome contenuto** e al **tipo di notifica** sono necessarie per rilevamento dei documenti.


- [IpcCreateLicenseMetadataHandle](https://msdn.microsoft.com/library/dn974050.aspx)
- [IpcSetLicenseMetadataProperty](https://msdn.microsoft.com/library/dn974059.aspx)

  È probabile che si imposteranno tutte le proprietà dei metadati, elencate qui sotto in base al tipo.

  Per ulteriori informazioni, vedere [License metadata property types](https://msdn.microsoft.com/library/dn974062.aspx) (Tipi di proprietà dei metadati di licenza).

  - **IPC_MD_CONTENT_PATH**

    Consente di identificare il documento rilevato. Nei casi in cui un percorso completo non è possibile, è sufficiente fornire il nome del file.

  - **IPC_MD_CONTENT_NAME**

    Consente di identificare il nome del documento rilevato.

  - **IPC_MD_NOTIFICATION_TYPE**

    Consente di specificare quando verrà inviata una notifica. Per altre informazioni, vedere Tipo di modifica.

  - **IPC_MD_NOTIFICATION_PREFERENCE**

    Consente di indicare il tipo di notifica. Per altre informazioni, vedere Preferenze di modifica.

  - **IPC_MD_DATE_MODIFIED**

    È consigliabile impostare tale data ogni volta che l'utente fa clic su Salva.

  - **IPC_MD_DATE_CREATED**

    Consente di impostare la data di creazione del file

- [IpcSerializeLicenseWithMetadata](https://msdn.microsoft.com/library/dn974058.aspx)

Usare l'API appropriata per aggiungere metadati al file o flusso.

- [IpcfEncryptFileWithMetadata](https://msdn.microsoft.com/library/dn974052.aspx)
- [IpcfEncryptFileStreamWithMetadata](https://msdn.microsoft.com/library/dn974051.aspx)

Infine, usare questa API per registrare il documento rilevato con il sistema di rilevamento.

- [IpcRegisterLicense](https://msdn.microsoft.com/library/dn974057.aspx)


## <a name="2-register-the-document-with-the-rms-service"></a>2. Registrare il documento con il servizio RMS

Di seguito è riportato un frammento di codice che mostra un esempio di impostazione dei metadati di rilevamento del documento e la chiamata per la registrazione con il sistema di rilevamento.

      C++
      HRESULT hr = S_OK;
      LPCWSTR wszOutputFile = NULL;
      wstring wszWorkingFile;
      IPC_LICENSE_METADATA md = {0};

      md.cbSize = sizeof(IPC_LICENSE_METADATA);
      md.dwNotificationType = IPCD_CT_NOTIFICATION_TYPE_ENABLED;
      md.dwNotificationPreference = IPCD_CT_NOTIFICATION_PREF_DIGEST;
      //file origination date, current time for this example
      md.ftDateCreated = GetCurrentTime();
      md.ftDateModified = GetCurrentTime();

      LOGSTATUS_EX(L"Encrypt file with official template...");

      hr =IpcfEncryptFileWithMetadata( wszWorkingFile.c_str(),
                               m_wszTestTemplateID.c_str(),
                               IPCF_EF_TEMPLATE_ID,
                               0,
                               NULL,
                               NULL,
                               &md,
                               &wszOutputFile);

     /* This will contain the serialized license */
     PIPC_BUFFER pSerializedLicense;

     /* the context to use for the call */
     PCIPC_PROMPT_CTX pContext;

     wstring wstrContentName(“MyDocument.txt”);
     bool sendLicenseRegistrationNotificationEmail = FALSE;

     hr = IpcRegisterLicense( pSerializedLicense,
                        0,
                        pContext,
                        wstrContentName.c_str(),
                        sendLicenseRegistrationNotificationEmail);

## <a name="add-a-track-usage-button-to-your-app"></a>Aggiungere un pulsante **Rileva utilizzo** all'app

Aggiungere un elemento dell'interfaccia utente **Rileva utilizzo** all'app con uno dei seguenti formati di URL è semplice:

- Usando l'ID contenuto
  - Ottenere l'ID contenuto utilizzando [IpcGetLicenseProperty](https://msdn.microsoft.com/library/hh535265.aspx) o [IpcGetSerializedLicenseProperty](https://msdn.microsoft.com/library/hh995038.aspx) se la licenza viene serializzata e usare la proprietà licenza **IPC_LI_CONTENT_ID**. Per altre informazioni, vedere [License property types](https://msdn.microsoft.com/library/hh535287.aspx) (Tipi di proprietà di licenza).
  - Con i metadati **ContentId** e **Issuer**, usare il formato seguente: `https://track.azurerms.com/#/{ContentId}/{Issuer}`

    Ad esempio: `https://track.azurerms.com/#/summary/05405df5-8ad6-4905-9f15-fc2ecbd8d0f7/janedoe@microsoft.com`

- Se non si ha accesso ai metadati, ad esempio se si sta esaminando la versione del documento non protetta, è possibile usare **Content_Name** nel formato seguente: `https://track.azurerms.com/#/?q={ContentName}`

  Esempio: https://track.azurerms.com/#/?q=Secret!.txt

Il client deve soltanto aprire un browser con l'URL appropriato. Il portale di rilevamento dei documenti RMS gestirà l'autenticazione ed eventuali reindirizzamenti necessari.

## <a name="related-topics"></a>Argomenti correlati

* [Tipi di proprietà dei metadati di licenza](https://msdn.microsoft.com/library/dn974062.aspx)
* [Preferenze di notifica](https://msdn.microsoft.com/library/dn974063.aspx)
* [Tipo di notifica](https://msdn.microsoft.com/library/dn974064.aspx)
* [IpcCreateLicenseMetadataHandle](https://msdn.microsoft.com/library/dn974050.aspx)
* [IpcSetLicenseMetadataProperty](https://msdn.microsoft.com/library/dn974059.aspx)
* [IpcSerializeLicenseWithMetadata](https://msdn.microsoft.com/library/dn974058.aspx)
* [IpcfEncryptFileWithMetadata](https://msdn.microsoft.com/library/dn974052.aspx)
* [IpcfEncryptFileStreamWithMetadata](https://msdn.microsoft.com/library/dn974051.aspx)
* [IpcRegisterLicense](https://msdn.microsoft.com/library/dn974057.aspx)


[!INCLUDE[Commenting house rules](../includes/houserules.md)]


<!--HONumber=Jan17_HO1-->


