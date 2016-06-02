---
# required metadata

title: Procedura&#58; Ottenere un ID applicazione di Azure | Azure RMS
description: Per la creazione di un'app abilitata per RMS con Microsoft Rights Management SDK 4.2 è necessario creare un contratto con il team di RMS.
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 0fe9dc-bc91-4018-b28d-2db293a3eaa2
# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Procedura: Ottenere un ID applicazione di Azure

Per la creazione di un'app abilitata per RMS con Microsoft Rights Management SDK 4.2 è necessario creare un contratto con il team di RMS.

## Panoramica

Per la creazione di un'app abilitata per RMS con MS RMS SDK 4.2 è necessario creare anche un contratto di utilizzo di servizi con il team di RMS. Questo contratto, noto anche come Rights Management License Agreement (RMLA), fornisce indicazioni per rispettare il contratto per la protezione del contenuto che verrà applicato per conto dell’utente e/o del proprietario del contenuto in relazione ai comportamenti (conformità alle regole di business) dell’app. Per gli autori di un'app abilitata per RMS, il contratto con il team di RMS verrà applicato in base all'esistenza di un “ID applicazione di Azure" che rappresenta il contratto e che consente all'app di connettersi al servizio di autenticazione di Azure AD.

## Elaborazione

Di seguito sono riportati i passaggi da seguire per creare un ID app e firmare il contratto di utilizzo con il team di RMS.

-   Seguire le istruzioni fornite nell'argomento [Come creare un ID app in Azure](https://msdn.microsoft.com/en-us/library/azure/dn132599.aspx) per creare l'ID app.
-   Inviare un messaggio al team di RMS comunicando l'ID app all'indirizzo <askipteam@microsoft.com> per avviare il processo RMLA.
-   Firmare il contratto RMLA e restituirlo al team di RMS.
-   Dopo la stipula del contratto RMLA, è necessario passare l’ID applicazione quando si effettua la chiamata alla libreria di autenticazione tramite il parametro *clientID*.

    Ecco come si presenta la chiamata di autenticazione nell’argomento [Esempi di codice iOS/OS X](ios-os-x-code-examples.md).


    // Retrieve token using ADAL
        [context acquireTokenWithResource:authenticationParameters.resource
                                 clientId:appClientId
                              redirectUri:redirectURI
                                   userId:authenticationParameters.userId
                          completionBlock:^(ADAuthenticationResult *result)



**Nota**  Se il team di RMS non riceve il contratto RMLA firmato entro 60 giorni, l'autenticazione dell’applicazione nel sistema di autenticazione di Azure verrà bloccata.

 

 

 


<!--HONumber=Apr16_HO4-->


