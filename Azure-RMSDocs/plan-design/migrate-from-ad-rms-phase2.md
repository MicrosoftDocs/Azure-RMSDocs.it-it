---
# required metadata

title: Migrazione da AD RMS ad Azure Rights Management - Fase 2 | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: e3fd9bd9-3638-444a-a773-e1d5101b1793


# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---
# Fase 2 della migrazione: configurazione lato client

*Si applica a: Active Directory Rights Management Services, Azure Rights Management*

Usare le seguenti informazioni per la fase 2 della migrazione da AD RMS ad Azure Rights Management (Azure RMS). Queste procedure descrivono il passaggio 5 di [Migrazione da AD RMS ad Azure Rights Management](migrate-from-ad-rms-to-azure-rms.md).


## Passaggio 5. Riconfigurare i client per l'uso di Azure RMS
Per i client Windows:

1.  [Scaricare gli script di migrazione](http://go.microsoft.com/fwlink/?LinkId=524619):

    -   CleanUpRMS_RUN_Elevated.cmd

    -   Redirect_OnPrem.cmd

    Questi script reimpostano la configurazione nei computer Windows in modo che usino il servizio Azure RMS anziché AD RMS.

2.  Seguire le istruzioni nello script di reindirizzamento (Redirect_OnPrem.cmd) per modificare lo script in modo che faccia riferimento al nuovo tenant di Azure RMS.

3.  Nei computer Windows eseguire questi script con privilegi elevati nel contesto dell'utente.

Per i client di dispositivi mobili e i computer Mac:

-   Rimuovere i record SRV in DNS creati al momento della distribuzione dell'[estensione per dispositivi mobili di AD RMS](http://technet.microsoft.com/library/dn673574.aspx).

#### Modifiche apportate dagli script di migrazione
Questa sezione illustra le modifiche apportate dagli script di migrazione. È possibile usare queste informazioni solo a scopo di riferimento o per la risoluzione dei problemi oppure se si preferisce apportare queste modifiche manualmente.

CleanUpRMS_RUN_Elevated.cmd:

-   Eliminare il contenuto delle cartelle %userprofile%\AppData\Local\Microsoft\DRM e %userprofile%\AppData\Local\Microsoft\MSIPC, incluse eventuali sottocartelle e i file con nomi di file lunghi.

-   Eliminare il contenuto delle chiavi del Registro di sistema seguenti:

    -   HKEY_LOCAL_MACHINE\Software\Microsoft\Office\(11.0|12.0|14.0)\Common\DRM

    -   HKEY_CURRENT_USER\Software\Microsoft\Office\(11.0|12.0|14.0)\Common\DRM

    -   HKEY_LOCAL_MACHINE\Software\WoW6432Node\Microsoft\Office\(11.0|12.0|14.0)\Common\DRM

    -   HKEY_CURRENT_USER\Software\WoW6432Node\Microsoft\Office\(11.0|12.0|14.0)\Common\DRM

    -   HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSIPC\ServiceLocation

    -   HKEY_LOCAL_MACHINE\SOFTWARE\WoW6432Node\Microsoft\MSIPC\ServiceLocation

    -   HKEY_LOCAL_MACHINE\Software\Microsoft\MSDRM\ServiceLocation

-   Eliminare i valori del Registro di sistema seguenti:

    -   HKEY_CURRENT_USER\Software\Microsoft\Office\15.0\Common\DRM\DefaultServerURL

    -   HKEY_CURRENT_USER\Software\Microsoft\Office\15.0\Common\DRM\DefaultServer

Redirect_OnPrem.cmd:

-   Creare i valori del Registro di sistema seguenti per ogni URL fornito come parametro in ognuno dei percorsi seguenti:

    -   HKEY_CURRENT_USER\Software\Microsoft\Office\(11.0|12.0|14.0)\Common\DRM\LicenseServerRedirection

    -   HKEY_CURRENT_USER\Software\WoW6432Node\Microsoft\Office\(11.0|12.0|14.0)\Common\DRM\LicenseServerRedirection

    -   HKEY_LOCAL_MACHINE\Software\Microsoft\Office\(11.0|12.0|14.0)\Common\DRM\LicenseServerRedirection

    -   HKEY_LOCAL_MACHINE\Software\WoW6432Node\Microsoft\Office\(11.0|12.0|14.0)\Common\DRM\LicenseServerRedirection

    -   HKEY_CURRENT_USER\Software\Classes\Local Settings\Software\Microsoft\MSIPC\LicensingRedirection

    Ogni voce include un valore REG_SZ **https://OldRMSserverURL/_wmcs/licensing** con i dati nel formato seguente: **https://&lt;YourTenantURL&gt;/_wmcs/licensing**.

    > [!NOTE]
    > *&lt;YourTenantURL&gt;* ha il formato seguente: **{GUID}.rms.[Region].aadrm.com**.
    > 
    > Ad esempio: 5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com
    > 
    > È possibile individuare questo valore identificando il valore **RightsManagementServiceId** quando si esegue il cmdlet [Get-AadrmConfiguration](http://msdn.microsoft.com/library/windowsazure/dn629410.aspx) per Azure RMS.


## Passaggi successivi
Per continuare la migrazione, passare a [Fase 3: configurazione di servizi di supporto](migrate-from-ad-rms-phase3.md).

<!--HONumber=Apr16_HO4-->


