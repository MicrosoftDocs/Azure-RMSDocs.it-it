---
title: Installazione per Windows Phone | Azure RMS
description: Nelle applicazioni Windows Phone è possibile usare Microsoft Rights Management SDK 4.2 per abilitare la protezione integrata delle informazioni nell'applicazione.
keywords: ''
author: bryanla
ms.author: bryanla
manager: mbaldwin
ms.date: 12/10/2018
ms.topic: conceptual
ms.service: information-protection
ms.assetid: e25a446e-b977-4736-9c65-7711171fb0e1
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
ms.openlocfilehash: 711b19631cc191f7a182602d3e05556f97072ee4
ms.sourcegitcommit: bd2b31dd97c8ae08c28b0f5688517110a726e3a1
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/08/2019
ms.locfileid: "54071715"
---
# <a name="windows-phone-setup"></a>Installazione per Windows Phone


Nelle applicazioni Windows Phone è possibile usare Microsoft Rights Management SDK 4.2 per abilitare la protezione integrata delle informazioni nella propria applicazione con Azure Active Directory Rights Management (AAD RM).

Questo argomento illustra come impostare l'ambiente per la creazione di nuove applicazioni personalizzate.

-   [Prerequisiti](#prerequisites)
-   [Configurazione dell'ambiente di sviluppo](#configuring-your-development-environment)
-   [Vedere anche](#see-also)

## <a name="prerequisites"></a>Prerequisiti


Nel sistema di sviluppo è necessario disporre del software seguente:

-   Sistema operativo [Windows 8.1](https://windows.microsoft.com/windows-8/meet).
-   [Strumenti di sviluppo (SDK) Windows Phone 8.1](https://developer.microsoft.com/windows/downloads/sdk-archive)
-   Microsoft [Visual Studio 2012](https://visualstudio.microsoft.com/vs/older-downloads/) o versione successiva o Visual Studio Express 2012, incluso in Windows Phone SDK 8.0/8.1.
-   Pacchetto MS RMS SDK 4.2 per Windows Phone. Per altre informazioni, vedere [Introduzione](get-started.md).
-   Libreria di autenticazione: è consigliabile usare [Azure AD Authentication Library](https://msdn.microsoft.com/library/jj573266.aspx) e altre librerie di autenticazione.

Leggere l'argomento relativo alle [novità](release-notes.md) per informazioni sugli aggiornamenti dell'API, indicazioni sul dispositivo e sull'ambiente, note sulla versione e domande frequenti (FAQ).

Esaminare le informazioni contenute nella guida relativa allo [sviluppo per Windows Phone](https://msdn.microsoft.com/library/windowsphone/develop/ff402535.aspx) reperibile in Windows Phone Dev Center.

## <a name="configuring-your-development-environment"></a>Configurazione dell'ambiente di sviluppo


-   Aprire *Visual Studio*.
-   Fare clic su **File**. Scegliere **Nuovo** dal menu **File**, quindi fare clic su **Progetto**.
-   Nella finestra di dialogo **Nuovo progetto** selezionare **Visual C\#**, quindi **App vuota (Windows Phone)** e fare clic su **OK**.

    ![Creare un nuovo progetto](../media/wpsetup-newproj.png)

-   In Esplora soluzioni fare clic con il pulsante destro del mouse sul progetto e selezionare **Aggiungi riferimento** per aprire la finestra di dialogo **Aggiungi riferimento**.

    ![Aggiungere un riferimento](../media/wpsetup-addref.png)

-   Nella finestra di dialogo **Aggiungi riferimento** fare clic su **Sfoglia** e selezionare il file *Microsoft.RightsManagement.dll* che si trova nella cartella in cui è stato estratto il pacchetto.
-   **App gestite**: per la creazione di un'app gestita, è necessario aggiungere questo riferimento; selezionare **Windows 8.1**-&gt;**Estensioni** e selezionare la casella **Windows Visual C++ Runtime Package for Windows**

    ![Aggiungere le estensioni](../media/wpsetup-refmngr.png)

-   **Aggiunta di funzionalità**: per usare l'SDK, l'applicazione necessita della funzionalità "Internet (client e server)". Per aggiungere questa funzionalità all'app, aprire il file *Package.appxmanifest* nel progetto e passare alla scheda **Funzionalità**.

A questo punto si è pronti per creare le nuove app Windows Phone personalizzate.

### <a name="see-also"></a>Vedere anche

[Introduzione](get-started.md)

[Novità](release-notes.md)

[Concetti base](core-concepts.md)

[Sviluppo per Windows Phone](https://msdn.microsoft.com/library/windowsphone/develop/ff402535.aspx)

[Informazioni di riferimento sulle API di Windows](https://msdn.microsoft.com/library/dn891914.aspx)

[Visual Studio 2012](https://visualstudio.microsoft.com/vs/older-downloads/)

[Windows Phone SDK](https://developer.microsoft.com/windows/downloads/sdk-archive)
