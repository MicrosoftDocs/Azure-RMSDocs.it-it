---
title: Migrazione da AD RMS ad Azure Information Protection - Fase 2 | Azure Information Protection
description: Fase 2 della migrazione da AD RMS ad Azure Information Protection. Viene descritto il passaggio 5 della migrazione da AD RMS ad Azure Information Protection.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 10/12/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: e3fd9bd9-3638-444a-a773-e1d5101b1793
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 9d8354f2d68f211d349226970fd2f83dd0ce810b
ms.openlocfilehash: ca8d2ccb68b96095fccf9d55b9cb9392d3a455ec


---
# <a name="migration-phase-2-clientside-configuration"></a>Fase 2 della migrazione: configurazione lato client

>*Si applica a: Active Directory Rights Management Services, Azure Information Protection, Office 365*

Usare le informazioni seguenti per la fase 2 della migrazione da AD RMS ad Azure Information Protection. Di seguito viene illustrato il passaggio 5 dell'operazione descritta in [Migrazione da AD RMS ad Azure Information Protection](migrate-from-ad-rms-to-azure-rms.md).


## <a name="step-5-reconfigure-clients-to-use-azure-information-protection"></a>Passaggio 5. Riconfigurare i client per l'uso di Azure Information Protection
Per i client Windows:

1.  [Scaricare gli script di migrazione](https://go.microsoft.com/fwlink/?LinkId=524619):

    -   CleanUpRMS_RUN_Elevated.cmd

    -   Redirect_OnPrem.cmd

    Questi script reimpostano la configurazione nei computer Windows in modo che usino il servizio Azure Information Protection anziché AD RMS.

2.  Seguire le istruzioni nello script di reindirizzamento (Redirect_OnPrem.cmd) per modificare lo script in modo che faccia riferimento al nuovo tenant di Azure Information Protection.

    > [!IMPORTANT]
    > Le istruzioni includono la sostituzione degli indirizzi di esempio **adrms** e **adrms.contoso.com** con gli indirizzi dei server AD RMS. Quando si esegue questa operazione, assicurarsi che non siano presenti spazi aggiuntivi prima o dopo gli indirizzi, che interrompono lo script di migrazione e sono molto difficili da identificare come la causa principale del problema. Alcuni strumenti di modifica aggiungono automaticamente uno spazio dopo aver incollato il testo.
    >
    > Inoltre, se i server AD RMS usano certificati del server SSL/TLS, controllare se i valori URL di gestione licenze includono il numero di porta **443** nella stringa. Ad esempio: https:// rms.treyresearch.net:443/_wmcs/licensing. Queste informazioni sono disponibili nella console di Active Directory Rights Management Services quando si fa clic sul nome del cluster e si visualizzano le informazioni **Dettagli cluster**. Se il numero di porta 443 è presente nell'URL, includere questo valore quando si modifica lo script. Ad esempio, https://rms.treyresearch.net**:443**.

3. Se gli utenti dispongono di Office 2016: gli script non sono ancora aggiornati per includere la configurazione per Office 2016, pertanto, se gli utenti dispongono di questa versione di Office, è necessario aggiornare manualmente gli script.

    - Per **CleanUpRMS.cmd**, cercare la riga `reg delete HKCU\Software\Microsoft\Office\15.0\Common\DRM /f` e immediatamente al di sotto, aggiungere la riga seguente:

            reg delete HKCU\Software\Microsoft\Office\16.0\Common\DRM /f

    - Per **Redirect_Onprem.cmd**, cercare la riga `reg add "HKEY_CURRENT_USER\Software\Microsoft\Office\15.0\Common\DRM" /t REG_SZ /v "DefaultServer" /d "%CloudRMS%" /F` e immediatamente al di sotto, aggiungere le due righe seguenti:

            reg add "HKEY_CURRENT_USER\Software\Microsoft\Office\16.0\Common\DRM" /t REG_SZ /v "DefaultServerUrl" /d "https://%CloudRMS%/_wmcs/licensing" /F 

            reg add "HKEY_CURRENT_USER\Software\Microsoft\Office\16.0\Common\DRM" /t REG_SZ /v "DefaultServer" /d "%CloudRMS%" /F

    Facoltativo: Gli script non fanno riferimento a Office 2016 nei commenti. Se si vuole aggiornare i commenti per riflettere queste aggiunte per Office 2016, apportare le modifiche seguenti a **Redirect_Onprem.cmd**:

    - Cercare `::     or MSIPC (Office 2013) with on-premises AD RMS` e sostituire con quanto segue:
    
            ::     or MSIPC (Office 2013 and 2016) with on-premises AD RMS

    - Cercare `echo Redirect SCP for Office 2013` e sostituire con quanto segue:
    
            echo Redirect SCP for Office versions based on MSIPC

    - Cercare `echo Redirect MSIPC for Office 2013` e sostituire con quanto segue:
    
            echo Redirect MSIPC for Office versions based on MSIPC

4.  Nei computer Windows:

    - Eseguire questi script con privilegi elevati nel contesto dell'utente.

    Per i client di dispositivi mobili e i computer Mac:

    -  Rimuovere i record SRV in DNS creati al momento della distribuzione dell' [estensione per dispositivo mobile di AD RMS](http://technet.microsoft.com/library/dn673574.aspx).

#### <a name="changes-made-by-the-migration-scripts"></a>Modifiche apportate dagli script di migrazione
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

-   Aggiungere i valori del Registro di sistema seguenti:

    -   HKEY_CURRENT_USER\Software\Microsoft\Office\15.0\Common\DRM\DefaultServerURL

    -   HKEY_CURRENT_USER\Software\Microsoft\Office\15.0\Common\DRM\DefaultServer

Redirect_OnPrem.cmd:

-   Creare i valori del Registro di sistema seguenti per ogni URL fornito come parametro in ognuno dei percorsi seguenti:

    -   HKEY_CURRENT_USER\Software\Microsoft\Office\(11.0|12.0|14.0)\Common\DRM\LicenseServerRedirection

    -   HKEY_CURRENT_USER\Software\WoW6432Node\Microsoft\Office\(11.0|12.0|14.0)\Common\DRM\LicenseServerRedirection

    -   HKEY_LOCAL_MACHINE\Software\Microsoft\Office\(11.0|12.0|14.0)\Common\DRM\LicenseServerRedirection

    -   HKEY_LOCAL_MACHINE\Software\WoW6432Node\Microsoft\Office\(11.0|12.0|14.0)\Common\DRM\LicenseServerRedirection

    -   HKEY_CURRENT_USER\Software\Classes\Local Settings\Software\Microsoft\MSIPC\LicensingRedirection

    Ogni voce include un valore REG_SZ **https://OldRMSserverURL/_wmcs/licensing** con i dati nel formato seguente: **https://&lt;URL del tenant&gt;/_wmcs/licensing**.

    > [!NOTE]
    > *&lt;L'URL del tenant&gt;* ha il formato seguente: **{GUID}.rms.[Region].aadrm.com**.
    > 
    > Ad esempio: 5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com
    > 
    > È possibile individuare questo valore identificando il valore **RightsManagementServiceId** quando si esegue il cmdlet [Get-AadrmConfiguration](http://msdn.microsoft.com/library/windowsazure/dn629410.aspx) per Azure RMS.


## <a name="next-steps"></a>Passaggi successivi
Per continuare la migrazione, passare a [Fase 3: configurazione di servizi di supporto](migrate-from-ad-rms-phase3.md).


<!--HONumber=Nov16_HO2-->


