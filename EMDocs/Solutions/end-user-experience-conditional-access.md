---
# required metadata

title: Esperienza utente finale di accesso condizionale
description:
keywords:
author: craigcaseyMSFT
manager: swadhwa
ms.date: 04/28/2016
ms.topic: article
ms.prod:
ms.service:
ms.technology:
ms.assetid: 3e186dd2-e17c-40d8-b160-48038b2c6593

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer:
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Esperienza utente finale di accesso condizionale
Quando l'utente prova ad accedere alla posta elettronica sul dispositivo per la prima volta o successivamente a eseguire la sincronizzazione, viene controllato lo stato della registrazione e di conformità del dispositivo. Il processo di registrazione o risoluzione dei problemi di conformità è un'esperienza interattiva. All'utente finale vengono forniti i passaggi necessari per registrare il dispositivo e renderlo conforme senza dover contattare l'help desk IT:

-   **Se il dispositivo non è registrato**, nella pagina di accesso viene visualizzato un messaggio di accesso negato e viene chiesto di eseguire la registrazione. Alla registrazione, il dispositivo viene registrato automaticamente in Azure Active Directory. Intune verifica la conformità del dispositivo e fornisce i passaggi correttivi per risolvere eventuali problemi di non conformità. Una volta che il dispositivo è conforme, Intune imposta lo stato di conformità del dispositivo con Azure Active Directory.

-   **Se il dispositivo è registrato ma non è conforme**, viene inviato al dispositivo un collegamento con i passaggi per risolvere i problemi. Quando l'utente finale corregge il problema, ad esempio relativo all'impostazione della password o alla crittografia, Intune che gestisce i criteri di conformità aggiorna lo stato di conformità del dispositivo in Azure AD.

Una volta che il dispositivo viene considerato registrato e conforme, entro pochi minuti dovrebbe essere eseguita la sincronizzazione della posta elettronica.

## Android

[Questo argomento](end-user-experience-conditional-access-android.md) descrive l'esperienza di registrazione quando un utente finale prova ad accedere alla posta elettronica nel proprio dispositivo mobile Android dopo l'abilitazione dell'accesso condizionale.

## iOS

[Questo argomento](end-user-experience-conditional-access-ios.md) descrive l'esperienza utente quando si prova ad accedere alla posta elettronica nel proprio dispositivo mobile iOS dopo l'abilitazione dell'accesso condizionale.

## Windows Phone

[Questo argomento ](end-user-experience-conditional-access-winphone.md) descrive l'esperienza utente finale quando si prova ad accedere alla posta elettronica nel proprio Windows Phone dopo l'abilitazione dell'accesso condizionale.


<!--HONumber=Apr16_HO4-->


