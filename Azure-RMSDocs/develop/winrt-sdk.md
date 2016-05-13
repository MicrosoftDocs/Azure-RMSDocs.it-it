---
# required metadata

title: Installazione per Windows Store | Azure RMS
description:
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: c2684152-7d52-4636-916d-15720f4e3346

# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

﻿
# Installazione per Windows Store

Le applicazioni Windows Store possono usare Microsoft Rights Management SDK 4.2 per abilitare la protezione integrata delle informazioni nella propria applicazione con Azure Active Directory Rights Management (AAD RM).

Questo argomento illustra come impostare l'ambiente per la creazione di nuove applicazioni personalizzate.

-   [Prerequisiti](#prerequisites)
-   [Facoltativo](#optional)
-   [Configurazione dell'ambiente di sviluppo](#configuring_your_development_environment)
-   [Vedere anche](#see_also)

## Prerequisiti


Nel sistema di sviluppo è necessario disporre del software seguente:

-   Sistema operativo [Windows 8.1](http://windows.microsoft.com/en-US/windows-8/meet)
-   [Windows SDK per Windows 8.1](https://msdn.microsoft.com/en-us/windows/desktop/bg162891.aspx)
-   Microsoft [Visual Studio 2012](http://www.microsoft.com/visualstudio/eng/products/visual-studio-overview) o versione successiva o Visual Studio Express 2012, incluso in Windows SDK per Windows 8.0/8.1.
-   Il pacchetto di MS RMS SDK 4.2 per le applicazioni Windows Store. Per altre informazioni, vedere [Introduzione](get-started.md).
-   Libreria di autenticazione: è consigliabile usare [Azure AD Authentication Library](https://msdn.microsoft.com/en-us/library/jj573266.aspx) e altre librerie di autenticazione.

Leggere l'argomento relativo alle [novità](release-notes.md) per informazioni sugli aggiornamenti dell'API, indicazioni sul dispositivo e sull'ambiente, note sulla versione e domande frequenti (FAQ).

## Facoltativo

La libreria dell'interfaccia utente fornisce un'interfaccia utente riutilizzabile per le operazioni di consumo e protezione per gli sviluppatori che non vogliono creare la propria interfaccia utente personalizzata - [Libreria dell'interfaccia utente per app Windows Store](https://github.com/AzureAD/rms-sdk-ui-for-windowsstore). È inoltre possibile usare un'applicazione di esempio di app Windows Store - [Applicazione di esempio RMS per Windows Store](https://github.com/AzureADSamples/rms-samples-for-windowsstore).

## Configurazione dell'ambiente di sviluppo


-   Aprire Visual Studio.
-   Fare clic su **File**, **Nuovo** e quindi su **Progetto**.
-   Nella finestra di dialogo **Nuovo progetto** fare clic su **Visual C\#** e selezionare **Applicazione vuota (Windows)**, quindi fare clic su **OK**.

    ![](../media/winrtsetup-newproj.png)

-   In **Esplora soluzioni** fare clic con il pulsante destro del mouse sul progetto e selezionare **Aggiungi riferimento** per aprire la finestra di dialogo **Aggiungi riferimento**.

    ![](../media/winrtsetup-addref.png)

-   Nella finestra di dialogo **Aggiungi riferimento** fare clic su **Sfoglia** e selezionare il file *Microsoft.RightsManagement.dll* che si trova nella cartella in cui è stato estratto il pacchetto SDK.
-   **App gestite**: per la creazione di un'app gestita, è necessario aggiungere questo riferimento, selezionare **Windows 8.1**-& gt;**Estensioni** e la casella per **Windows Visual C++ Runtime Package per Windows**

    ![](../media/winrtsetup-refmngr.png)

-   **Aggiunta di funzionalità**: per usare l'SDK, l'applicazione necessita della funzionalità "Internet (client e server)". Per aggiungere questa funzionalità all'app, aprire il file *Package.appxmanifest* nel progetto e passare alla scheda **Funzionalità**.

A questo punto si è pronti per creare le nuove app Windows Store personalizzate.

### Vedere anche

[Introduzione](get-started.md)

[Novità](release-notes.md)

[Concetti e termini per sviluppatori](core-concepts.md)

[Windows 8](http://windows.microsoft.com/en-US/windows-8/meet)

[Visual Studio 2012](http://www.microsoft.com/visualstudio/eng/products/visual-studio-overview)

[Informazioni di riferimento sulle API di Windows](/rights-management/sdk/4.2/api/winrt/Microsoft.RightsManagement)


<!--HONumber=Apr16_HO3-->


