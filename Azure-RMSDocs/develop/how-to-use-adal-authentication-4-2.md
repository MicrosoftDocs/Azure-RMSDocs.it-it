---
title: Usare il portale di Azure per eseguire la configurazione per l&quot;autenticazione di RMS | Azure RMS
description: Descrive il processo per l&quot;autenticazione con ADAL
keywords: autenticazione, RMS, ADAL
author: bruceperlerms
ms.author: bruceper
manager: mbaldwin
ms.date: 09/25/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 2680b399-febb-4bd6-b844-ac3d1e69aca4
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 7068e0529409eb783f16bc207a17be27cd5d82a8
ms.openlocfilehash: 9a777b9a13c5ecff3083f4552a8c81f4e42c5cb2


---

# <a name="how-to-use-azure-portal-to-configure-for-rms-authentication"></a>Procedura: Usare il portale di Azure per eseguire la configurazione per l'autenticazione di RMS

Autenticazione con Azure RMS per l'app usando Azure Active Directory Authentication Library (ADAL).

Per questo approccio è necessario che l'applicazione gestisca la propria autenticazione OAuth. Con questo approccio, il client RMS eseguirà un callback definito dall'applicazione quando è necessaria l'autenticazione.

## <a name="configure-via-azure-portal"></a>Eseguire la configurazione tramite il portale di Azure
Per iniziare, eseguire la configurazione tramite il portale di Azure seguendo le istruzioni riportate in [Configurare Azure RMS per l'autenticazione ADAL](adal-auth.md). Assicurarsi di copiare e salvare i valori di *ID client* e *URI di reindirizzamento* da questo processo per usarli in seguito.

## <a name="code-sample"></a>Esempio di codice
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


## <a name="related-topics"></a>Argomenti correlati

- [MSIPCSampleApp](https://github.com/AzureAD/rms-sdk-ui-for-android/tree/master/samples/MsipcSampleApp)
- [Configurare Azure RMS per l'autenticazione ADAL](adal-auth.md)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]


<!--HONumber=Jan17_HO1-->


