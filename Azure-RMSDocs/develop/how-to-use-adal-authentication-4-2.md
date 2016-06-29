---
# required metadata

title: Usare il portale di Azure per eseguire la configurazione per l'autenticazione di RMS | Azure RMS
description: Descrive il processo per l'autenticazione con ADAL
keywords: authentication, RMS, ADAL
author: bruceperlerms
manager: mbaldwin
ms.date: 06/14/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 2680b399-febb-4bd6-b844-ac3d1e69aca4

# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Procedura: Usare il portale di Azure per eseguire la configurazione per l'autenticazione di RMS

Autenticazione con Azure RMS per l'app usando Azure Active Directory Authentication Library (ADAL).

Per questo approccio è necessario che l'applicazione gestisca la propria autenticazione OAuth. Con questo approccio, il client RMS eseguirà un callback definito dall'applicazione quando è necessaria l'autenticazione.

## Eseguire la configurazione tramite il portale di Azure
Per iniziare, eseguire la configurazione tramite il portale di Azure seguendo le istruzioni riportate in [Configurare Azure RMS per l'autenticazione ADAL](adal-auth.md). Assicurarsi di copiare e salvare i valori di *ID client* e *URI di reindirizzamento* da questo processo per usarli in seguito.

## Esempio di codice
Questo è un frammento di codice tratto dall'esempio completo di codice per client di dispositivi mobili relativo all'abilitazione di Azure ADAL. Per altre informazioni, vedere l'esempio completo in [MSIPCSampleApp](https://github.com/AzureAD/rms-sdk-ui-for-android/tree/master/samples/MsipcSampleApp).

       /**
       * Instantiates a new rms authentication callback.
       *
       * @param parentActivity the parent activity
       * @throws NoSuchAlgorithmException the no such algorithm exception
       * @throws InvalidKeySpecException the invalid key spec exception
       * @throws UnsupportedEncodingException the unsupported encoding exception
       */

       public MsipcAuthenticationCallback(Activity parentActivity) throws NoSuchAlgorithmException, InvalidKeySpecException, UnsupportedEncodingException
       {
         mParentActivity = parentActivity;
         setADALKeyStore();

         /**
         * Note: Following values of are client_id and redirect_uri are for demo purpose only.
         * Your values will come from the preceeding Azure Portal process.
         */
         mClientId = "com.microsoft.rightsmanagement.sampleapp";
         mRedirectURI = mClientId + "://authorize";
       }


## Argomenti correlati

- [MSIPCSampleApp](https://github.com/AzureAD/rms-sdk-ui-for-android/tree/master/samples/MsipcSampleApp)
- [Configurare Azure RMS per l'autenticazione ADAL](adal-auth.md)


<!--HONumber=Jun16_HO2-->


