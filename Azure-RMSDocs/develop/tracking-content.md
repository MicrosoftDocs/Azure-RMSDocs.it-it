---
# required metadata

title: Rilevamento del contenuto | Azure RMS
description: Linee guida di base per l'implementazione del rilevamento di documenti
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: F5089765-9D94-452B-85E0-00D22675D847
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
# Rilevamento del contenuto

Questo argomento illustra le linee guida di base per l'implementazione del rilevamento del contenuto protetto con Rights Management Services SDK 2.1.

Rilevamento dei documenti è una funzionalità del sistema di Rights Management. L'aggiunta di metadati specifici durante il processo di protezione di un documento fa sì che si possa registrare il documento stesso con il portale del servizio di rilevamento, che fornisce quindi diverse opzioni per il rilevamento.

Usare queste API per aggiungere o aggiornare una licenza con i metadati di rilevamento dei documenti.

-   [**IpcCreateLicenseMetadataHandle**](/rights-management/sdk/2.1/api/win/functions#msipc_ipccreatelicensemetadatahandle)
-   [**IpcSetLicenseMetadataProperty**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcsetlicensemetadataproperty)

    È probabile che si imposteranno tutte le proprietà dei metadati, elencate qui sotto in base al tipo.

    Per ulteriori informazioni, vedere [**i tipi di proprietà dei metadati di licenza**](/rights-management/sdk/2.1/api/win/license%20metadata%20property%20types#msipc_license_metadata_property_types).

    -   **IPC\_MD\_CONTENT\_PATH**

        Consente di identificare il documento rilevato. Nei casi in cui un percorso completo non è possibile, è sufficiente fornire il nome del file.

    -   **IPC\_MD\_CONTENT\_NAME**

        Consente di identificare il nome del documento rilevato.

    -   **IPC\_MD\_NOTIFICATION\_TYPE**

        Consente di specificare quando verrà inviata una notifica. Per ulteriori informazioni, vedere la pagina [**Tipo di modifica**](/rights-management/sdk/2.1/api/win/notification%20type#msipc_notification_type).

    -   **IPC\_MD\_NOTIFICATION\_PREFERENCE**

        Consente di indicare il tipo di notifica. Per ulteriori informazioni, vedere la pagina [**Preferenze di modifica**](/rights-management/sdk/2.1/api/win/constants#msipc_notification_preference).

    -   **IPC\_MD\_DATE\_MODIFIED**

        È consigliabile impostare tale data ogni volta che l'utente fa clic su **Salva**.

    -   **IPC\_MD\_DATE\_CREATED**

        La data di creazione del file.

-   [**IpcSerializeLicenseWithMetadata**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcserializelicensemetadata)

Usare l'API appropriata per aggiungere metadati al file o flusso.

-   [**IpcfEncryptFileWithMetadata**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcfencryptfilewithmetadata)
-   [**IpcfEncryptFileStreamWithMetadata**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcfencryptfilestreamwithmetadata)

Infine, usare questa API per registrare il documento rilevato con il sistema di rilevamento.

-   [**IpcRegisterLicense**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcregisterlicense)

Di seguito è riportato un frammento di codice che mostra un esempio di impostazione dei metadati di rilevamento del documento e la chiamata per la registrazione con il sistema di rilevamento.



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

    LOGSTATUS_EX(L&quot;Encrypt file with official template...&quot;);

    hr =IpcfEncryptFileWithMetadata(  wszWorkingFile.c_str(),
                                       m_wszTestTemplateID.c_str(),
                                       IPCF_EF_TEMPLATE_ID,
                                       0,
                                       NULL,
                                       NULL,
                                       &amp;md,
                                       &amp;wszOutputFile);

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


## Argomenti correlati


* [**Tipi di proprietà dei metadati di licenza**](/rights-management/sdk/2.1/api/win/license%20metadata%20property%20types#msipc_license_metadata_property_types)
* [**Preferenze di notifica**](/rights-management/sdk/2.1/api/win/constants#msipc_notification_preference)
* [**Tipo di notifica**](/rights-management/sdk/2.1/api/win/notification%20type#msipc_notification_type)
* [**IpcCreateLicenseMetadataHandle**](/rights-management/sdk/2.1/api/win/functions#msipc_ipccreatelicensemetadatahandle)
* [**IpcSetLicenseMetadataProperty**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcsetlicensemetadataproperty)
* [**IpcSerializeLicenseWithMetadata**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcserializelicensemetadata)
* [**IpcfEncryptFileWithMetadata**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcfencryptfilewithmetadata)
* [**IpcfEncryptFileStreamWithMetadata**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcfencryptfilestreamwithmetadata)
* [**IpcRegisterLicense**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcregisterlicense)
 

 


<!--HONumber=Jun16_HO1-->


