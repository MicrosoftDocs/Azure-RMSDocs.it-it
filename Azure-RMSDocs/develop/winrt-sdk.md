---
title: Installazione per Windows Store | Azure RMS
description: Le applicazioni di Windows Store possono usare Microsoft Rights Management SDK 4.2 per abilitare la protezione integrata delle informazioni nell&quot;applicazione.
keywords: 
author: bruceperlerms
manager: mbaldwin
ms.date: 09/25/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 2720aa0e-0d37-469f-be99-678bf95a9c51
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: dc452dac3a86cd9cc39127d5a29106ae87ba94be
ms.openlocfilehash: c3dfa23a4bb03aec3ad9eae835382040a5347006


---

# <a name="windows-store-setup"></a>Installazione per Windows Store

Le applicazioni Windows Store possono usare Microsoft Rights Management SDK 4.2 per abilitare la protezione integrata delle informazioni nella propria applicazione con Azure Active Directory Rights Management (AAD RM).

Questo argomento illustra come impostare l'ambiente per la creazione di nuove applicazioni personalizzate.

-   [Prerequisiti](#prerequisites)
-   [Facoltativo](#optional)
-   [Configurazione dell'ambiente di sviluppo](#configuring-your-development-environment)
-   [Vedere anche](#see-also)

## <a name="prerequisites"></a>Prerequisiti


Nel sistema di sviluppo è necessario disporre del software seguente:

-   Sistema operativo [Windows 8.1](http://windows.microsoft.com/en-US/windows-8/meet)
-   [Windows SDK per Windows 8.1](https://msdn.microsoft.com/windows/desktop/bg162891.aspx)
-   Microsoft [Visual Studio 2012](http://www.microsoft.com/visualstudio/eng/products/visual-studio-overview) o versione successiva o Visual Studio Express 2012, incluso in Windows SDK per Windows 8.0/8.1.
-   Il pacchetto di MS RMS SDK 4.2 per le applicazioni Windows Store. Per altre informazioni, vedere [Introduzione](get-started.md).
-   Libreria di autenticazione: è consigliabile usare [Azure AD Authentication Library](https://msdn.microsoft.com/en-us/library/jj573266.aspx) e altre librerie di autenticazione.

Leggere l'argomento relativo alle [novità](release-notes.md) per informazioni sugli aggiornamenti dell'API, indicazioni sul dispositivo e sull'ambiente, note sulla versione e domande frequenti (FAQ).

## <a name="optional"></a>Facoltativo

La libreria dell'interfaccia utente fornisce un'interfaccia utente riutilizzabile per le operazioni di consumo e protezione per gli sviluppatori che non vogliono creare la propria interfaccia utente personalizzata - [Libreria dell'interfaccia utente per app Windows Store](https://github.com/AzureAD/rms-sdk-ui-for-windowsstore). È inoltre possibile usare un'applicazione di esempio di app Windows Store - [Applicazione di esempio RMS per Windows Store](https://github.com/AzureADSamples/rms-samples-for-windowsstore).

## <a name="configuring-your-development-environment"></a>Configurazione dell'ambiente di sviluppo


-   Aprire Visual Studio.
-   Fare clic su **File**, **Nuovo** e quindi su **Progetto**.
-   Nella finestra di dialogo **Nuovo progetto** fare clic su **Visual C\#** e selezionare **Applicazione vuota (Windows)**, quindi fare clic su **OK**.

    ![Creare un nuovo progetto](../media/winrtsetup-newproj.png)

-   In **Esplora soluzioni** fare clic con il pulsante destro del mouse sul progetto e selezionare **Aggiungi riferimento** per aprire la finestra di dialogo **Aggiungi riferimento**.

    ![Aggiungere un riferimento](../media/winrtsetup-addref.png)

-   Nella finestra di dialogo **Aggiungi riferimento** fare clic su **Sfoglia** e selezionare il file *Microsoft.RightsManagement.dll* che si trova nella cartella in cui è stato estratto il pacchetto SDK.
-   **App gestite**: per la creazione di un'app gestita, è necessario aggiungere questo riferimento; selezionare **Windows 8.1**-&gt;**Estensioni** e selezionare la casella **Windows Visual C++ Runtime Package for Windows**

    ![Aggiungere le estensioni](../media/winrtsetup-refmngr.png)

-   **Aggiunta di funzionalità**: per usare l'SDK, l'applicazione necessita della funzionalità "Internet (client e server)". Per aggiungere questa funzionalità all'app, aprire il file *Package.appxmanifest* nel progetto e passare alla scheda **Funzionalità**.

A questo punto si è pronti per creare le nuove app Windows Store personalizzate.

### <a name="see-also"></a>Vedere anche

[Introduzione](get-started.md)

[Novità](release-notes.md)

[Concetti e termini per sviluppatori](core-concepts.md)

[Windows 8](http://windows.microsoft.com/en-US/windows-8/meet)

[Visual Studio 2012](http://www.microsoft.com/visualstudio/eng/products/visual-studio-overview)

[Informazioni di riferimento sulle API di Windows](https://msdn.microsoft.com/library/dn891914.aspx)



<!--HONumber=Nov16_HO1-->


