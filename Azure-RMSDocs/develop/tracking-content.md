---
title: Come abilitare la revoca e il rilevamento dei documenti | Azure RMS
description: Linee guida di base per implementare il rilevamento del contenuto del documento, nonché un codice di esempio per aggiornare i metadati e un pulsante Rileva utilizzo per l'app.
keywords: ''
author: msmbaldwin
ms.author: mbaldwin
manager: barbkess
ms.date: 02/23/2017
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: F5089765-9D94-452B-85E0-00D22675D847
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
ms.custom: dev
experimental: true
experiment_id: priyamo-test-20160729
ms.openlocfilehash: 5159f39d5b91c748abe9fe7e0734c4a6eacbe4d5
ms.sourcegitcommit: d01580c266de1019de5f895d65c4732f2c98456b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/19/2020
ms.locfileid: "95568371"
---
# <a name="how-to-enable-document-tracking-and-revocation"></a>Procedura: Abilitare la revoca e il rilevamento dei documenti

Questo argomento illustra le linee guida di base per implementare il rilevamento del contenuto del documento, nonché un codice di esempio per aggiornare i metadati e per creare il pulsante **Rileva utilizzo** per l'app.

## <a name="steps-to-implement-document-tracking"></a>Passaggi per implementare il rilevamento del documento

I passaggi 1 e 2 consentono il rilevamento del documento. Il passaggio 3 consente agli utenti delle app di raggiungere il sito per rilevare e revocare i documenti protetti.

1. Aggiungere i metadati associati al rilevamento dei documenti
2. Registrare il documento con il servizio RMS
3. Aggiungere il pulsante Rileva utilizzo all'app

Seguono i dettagli di implementazione per questi passaggi.

## <a name="1-add-document-tracking-metadata"></a>1. aggiungere i metadati di rilevamento dei documenti

Rilevamento dei documenti è una funzionalità del sistema di Rights Management. L'aggiunta di metadati specifici durante il processo di protezione di un documento fa sì che si possa registrare il documento stesso con il portale del servizio di rilevamento, che fornisce quindi diverse opzioni per il rilevamento.

Usare queste API per aggiungere o aggiornare una licenza con i metadati di rilevamento dei documenti.


Dal punto di vista operativo, solo le proprietà relative al **nome contenuto** e al **tipo di notifica** sono necessarie per rilevamento dei documenti.


- [IpcCreateLicenseMetadataHandle](/previous-versions/windows/desktop/msipc/ipccreatelicensemetadatahandle)
- [IpcSetLicenseMetadataProperty](/previous-versions/windows/desktop/msipc/ipcsetlicensemetadataproperty)

  È probabile che si imposteranno tutte le proprietà dei metadati, elencate qui sotto in base al tipo.

  Per ulteriori informazioni, vedere [License metadata property types](/previous-versions/windows/desktop/msipc/license-metadata-property-types) (Tipi di proprietà dei metadati di licenza).

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

- [IpcSerializeLicenseWithMetadata](/previous-versions/windows/desktop/msipc/ipcserializelicensemetadata)

Usare l'API appropriata per aggiungere metadati al file o flusso.

- [IpcfEncryptFileWithMetadata](/previous-versions/windows/desktop/msipc/ipcfencryptfilewithmetadata)
- [IpcfEncryptFileStreamWithMetadata](/previous-versions/windows/desktop/msipc/ipcfencryptfilestreamwithmetadata)

Infine, usare questa API per registrare il documento rilevato con il sistema di rilevamento.

- [IpcRegisterLicense](/previous-versions/windows/desktop/msipc/ipcregisterlicense)


## <a name="2-register-the-document-with-the-rms-service"></a>2. registrare il documento con il servizio RMS

Di seguito è riportato un frammento di codice che mostra un esempio di impostazione dei metadati di rilevamento del documento e la chiamata per la registrazione con il sistema di rilevamento.

**C++**:

  ```cpp
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

     wstring wstrContentName("MyDocument.txt");
     bool sendLicenseRegistrationNotificationEmail = FALSE;

     hr = IpcRegisterLicense( pSerializedLicense,
                        0,
                        pContext,
                        wstrContentName.c_str(),
                        sendLicenseRegistrationNotificationEmail);
  ```

## <a name="add-a-track-usage-button-to-your-app"></a>Aggiungere un pulsante **Rileva utilizzo** all'app

Aggiungere un elemento dell'interfaccia utente **Rileva utilizzo** all'app con uno dei seguenti formati di URL è semplice:

- Usando l'ID contenuto
  - Ottenere l'ID contenuto utilizzando [IpcGetLicenseProperty](/previous-versions/windows/desktop/msipc/ipcgetlicenseproperty) o [IpcGetSerializedLicenseProperty](/previous-versions/windows/desktop/msipc/ipcgetserializedlicenseproperty) se la licenza viene serializzata e usare la proprietà licenza **IPC_LI_CONTENT_ID**. Per altre informazioni, vedere [tipi di proprietà di licenza](/previous-versions/windows/desktop/msipc/license-property-types).
  - Con i metadati **ContentID** e **Issuer** , usare il formato seguente: `https://track.azurerms.com/#/{ContentId}/{Issuer}`

    Ad esempio: `https://track.azurerms.com/#/summary/05405df5-8ad6-4905-9f15-fc2ecbd8d0f7/janedoe@microsoft.com`

- Se non si ha accesso a tali metadati, ovvero si sta esaminando la versione non protetta del documento, è possibile usare il **Content_Name** nel formato seguente: `https://track.azurerms.com/#/?q={ContentName}`

  Esempio - https://track.azurerms.com/#/?q=Secret!.txt

Il client deve soltanto aprire un browser con l'URL appropriato. Il portale di rilevamento dei documenti RMS gestirà l'autenticazione ed eventuali reindirizzamenti necessari.

## <a name="related-topics"></a>Argomenti correlati

* [Tipi di proprietà dei metadati di licenza](/previous-versions/windows/desktop/msipc/license-metadata-property-types)
* [Preferenze di notifica](/previous-versions/windows/desktop/msipc/notification-preference)
* [Tipo di notifica](/previous-versions/windows/desktop/msipc/notification-type)
* [IpcCreateLicenseMetadataHandle](/previous-versions/windows/desktop/msipc/ipccreatelicensemetadatahandle)
* [IpcSetLicenseMetadataProperty](/previous-versions/windows/desktop/msipc/ipcsetlicensemetadataproperty)
* [IpcSerializeLicenseWithMetadata](/previous-versions/windows/desktop/msipc/ipcserializelicensemetadata)
* [IpcfEncryptFileWithMetadata](/previous-versions/windows/desktop/msipc/ipcfencryptfilewithmetadata)
* [IpcfEncryptFileStreamWithMetadata](/previous-versions/windows/desktop/msipc/ipcfencryptfilestreamwithmetadata)
* [IpcRegisterLicense](/previous-versions/windows/desktop/msipc/ipcregisterlicense)