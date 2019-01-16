---
title: Installazione per iOS e OS X | Azure RMS
description: Le applicazioni iOS e OS X possono usare RMS SDK 4.2 per abilitare la protezione integrata delle informazioni nella propria applicazione con AAD RM.
keywords: ''
author: bryanla
ms.author: bryanla
manager: mbaldwin
ms.date: 02/23/2017
ms.topic: conceptual
ms.service: information-protection
ms.assetid: b31e5b72-e65e-450a-b1b8-d46e81e9fb34
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
ms.openlocfilehash: 620412b55ca583d8a84cf8d167ba890cea742b7f
ms.sourcegitcommit: bd2b31dd97c8ae08c28b0f5688517110a726e3a1
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/08/2019
ms.locfileid: "54070229"
---
# <a name="ios-and-os-x-setup"></a>Installazione per iOS e OS X

Le applicazioni iOS e OS X possono usare Microsoft Rights Management SDK 4.2 per abilitare la protezione integrata delle informazioni nella propria applicazione con Azure Rights Management (Azure RMS).

Questo argomento illustra come impostare l'ambiente per la creazione di nuove applicazioni personalizzate.

**Nota**  Questo SDK non supporta l'iPod Touch.


-   [Prerequisiti](#prerequisites)
-   [Facoltativo](#optional)
-   [Configurazione dell'ambiente di sviluppo](#configuring-your-development-environment)
-   [Vedere anche](#see-also)

## <a name="prerequisites"></a>Prerequisiti

Nel sistema di sviluppo è consigliabile disporre del software seguente:

-   Per tutti i progetti di sviluppo iOS è necessario OS X.
-   Xcode versione 6.0 e successive

    Xcode è disponibile tramite il [Mac App Store](https://developer.apple.com/technologies/mac/).

-   Pacchetto MS RMS SDK 4.2 per iOS e OS X. Per altre informazioni, vedere [Introduzione](get-started.md).

    Questo SDK consente di sviluppare per iOS 7.0 e OS X 10.8 e versioni successive.

-   Libreria di autenticazione: è consigliabile usare [Azure Active Directory Authentication Library (ADAL)](https://msdn.microsoft.com/library/jj573266.aspx). Tuttavia, è possibile usare anche altre librerie di autenticazione che supportano OAuth 2.0.

    Per altre informazioni, vedere [ADAL per iOS](https://github.com/MSOpenTech/azure-activedirectory-library-for-ios) o [ADAL per OS X](https://github.com/MSOpenTech/azure-activedirectory-library-for-ios/tree/OSXUniversal)

Leggere l'argomento [Novità](release-notes.md) per informazioni sugli aggiornamenti delle API, note sulla versione e domande frequenti (FAQ).

## <a name="optional"></a>Facoltativo

La libreria dell'interfaccia utente fornisce un'interfaccia utente riutilizzabile per le operazioni di consumo e protezione per gli sviluppatori che non intendono creare un’interfaccia utente personalizzata - [Libreria dell'interfaccia utente e app di esempio per iOS](https://github.com/AzureAD/rms-sdk-ui-for-ios).

## <a name="configuring-your-development-environment"></a>Configurazione dell'ambiente di sviluppo

-   Per creare un nuovo progetto, scegliere **Nuovo** dal menu **File**, quindi fare clic su **Progetto**.
-   Selezionare **Single View Application**.

    ![Creazione di un nuovo progetto](../media/iOS-Project.png)

-   Immettere un nome e un identificatore per il nuovo progetto.

    ![Assegnare un nome al progetto](../media/iOS-project-options.png)

-   Fare clic su **Next** e selezionare il percorso per il progetto.
-   Per aggiungere il framework **MSRightsManagement** per i framework iOS, trascinare la cartella .framework dalla cartella di installazione dell’SDK alla sezione **Frameworks** del **Project Navigator**.

    ![Impostare il percorso](../media/ios-add-dependencies-01a.png)

-   Selezionare il pulsante di opzione **Create groups for any added folders** e deselezionare la casella di controllo **Copy items into destination group's folder (if needed)**.

    In questo modo si mantiene il riferimento alla cartella di installazione dell’SDK, senza doverne creare una copia.

    ![Impostare il riferimento alla cartella di installazione dell'SDK](../media/iOS-create-groups.png)

-   Per aggiungere MS RMS SDK 4.2 per il raggruppamento di risorse, trascinare il file MSRightsManagementResources.bundle dalla cartella MSRightsManagement.framework/Resources alla sezione **Frameworks** del Project Navigator.

    ![Aggiungere un'aggregazione di risorse](../media/iOS-add-resource-bundle-02a.png)

-   Come in precedenza per la copia del framework, selezionare il pulsante di opzione **Create groups for any added folders** e deselezionare la casella di controllo **Copy items into destination group’s folder (if needed)**.
-   L'SDK si basa su altri framework, tra cui: **CoreData**, **MessageUI**, **SystemConfiguration**, **Libresolv** e **Security**. Per aggiungere questi framework, passare alla sezione **Linked Frameworks and Libraries** del riquadro **Summary** di destinazione ed espandere tale sezione per aggiungerli.

    Sono necessari i framework **UIKit** e **Foundation**, in genere presenti per impostazione predefinita.

    ![Aggiungere le risorse](../media/iOS-add-libraries.png)

-   Aggiungere il flag **- ObjC** a **Other Linker Flags** in **Build Settings** di destinazione.

    ![Aggiungere le impostazioni di compilazione](../media/iOS-linker-flags.png)

-   A questo punto il **Project Navigator** dovrebbe apparire simile alla struttura ad albero seguente.

    ![Rivedere il progetto](../media/iOS-verify-setup-01a.png)

-   A questo punto si è pronti a creare le nuove app iOS/OS X personalizzate.

### <a name="see-also"></a>Vedere anche

* [Introduzione](get-started.md)

* [Novità](release-notes.md)

* [Concetti e termini per sviluppatori](core-concepts.md)

* [Informazioni di riferimento sulle API di iOS/OS X](https://msdn.microsoft.com/library/dn758306.aspx)
