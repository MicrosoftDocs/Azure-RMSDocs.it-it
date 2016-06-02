---
# required metadata

title: Installazione per Android | Azure RMS
description: Le applicazioni Android possono usare SDK 4.2 Microsoft Rights Management per abilitare la protezione integrata nelle proprie applicazioni.
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 986f6932-159b-4791-bd1a-7640a83ee792
# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Installazione per Android

Le applicazioni Android possono usare SDK 4.2 Microsoft Rights Management per abilitare la protezione integrata delle informazioni nelle proprie applicazioni con Azure Active Directory Rights Management (AAD RM).

Questo argomento illustra come impostare l'ambiente per la creazione di nuove applicazioni personalizzate.

-   [Prerequisiti](#prerequisites)
-   [Facoltativo](#optional)
-   [Configurazione dell'ambiente di sviluppo](#configuring_your_development_environment_)
-   [Vedere anche](#see_also)

## Prerequisiti

Nel sistema di sviluppo si consiglia di disporre del software seguente:

-   Sistema operativo Windows o OS X per l'esecuzione dell'ambiente di sviluppo [Eclipse](http://www.oracle.com/technetwork/java/javase/downloads/jre7-downloads-1880261.html).
-   Questa guida presuppone l'uso di SDK di Eclipse a partire da Eclipse Juno 4.2 e di un'installazione predefinita.
-   Java a partire da Java 1.6.
-   [Plug-in Android Developer Tools (ADT)](http://developer.android.com/sdk/installing/index.html). NOTA: per completare l'installazione potrebbe essere richiesto di riavviare Eclipse.

     

-   Pacchetto SDK MS RMS 4.2 per Android. Per altre informazioni, vedere [Introduzione](get-started.md).

    Questo SDK consente di sviluppare per Android 4.0.3 (API livello 15) e versioni successive.

-   Libreria di autenticazione: è consigliabile usare [Azure AD Authentication Library (ADAL)](https://msdn.microsoft.com/en-us/library/jj573266.aspx). Tuttavia, è possibile usare anche altre librerie di autenticazione che supportano OAuth 2.0.

    Per altre informazioni, vedere [ADAL per Android](https://github.com/MSOpenTech/azure-activedirectory-library-for-android)

    **Nota**: se l'applicazione non usa ADAL come libreria di autenticazione OAuth 2.0, è consigliabile leggere questa guida Android [Alcune idee su SecureRandom](http://android-developers.blogspot.com/2013/08/some-securerandom-thoughts.html).

     

Leggere l'argomento [Novità](release-notes.md) per informazioni sugli aggiornamenti dell'API, note sulla versione e domande frequenti (FAQ).

## Facoltativo

La libreria dell'interfaccia utente fornisce un'interfaccia utente riusabile per le operazioni di uso e protezione per gli sviluppatori che non intendono creare la propria interfaccia utente personalizzata - [Libreria dell'interfaccia utente e app di esempio per Android](https://github.com/AzureAD/rms-sdk-ui-for-android).

## Configurazione dell'ambiente di sviluppo

**Nota**: versione di anteprima SDK MS RMS 4.2: in questa versione di anteprima, le schermate non sono state aggiornate per riflettere la modifica nel nome di pathes da com/microsoft/protection a com/microsoft/rightsmanagment. Il testo, tuttavia, è stato aggiornato.

 
-   Aprire l'ambiente di sviluppo Eclipse.
-   Per creare un nuovo progetto di applicazione Android, nel menu **File**, fare clic su **Nuovo**, fare clic su **Progetto** e quindi selezionare **Progetto di applicazione Android**.

    ![Creare una nuova applicazione Android](../media/Android-setup-01c.png)

-   Immettere il nome dell'applicazione. Il nome del progetto e il nome del pacchetto sono compilati in base al nome dell'applicazione.
-   Fare clic su **Avanti** e selezionare dove si desidera creare l'area di lavoro.

    ![Immettere il nome dell'applicazione](../media/Android-setup-02a.jpg)

-   Fare clic su **Avanti** e selezionare un'icona per l'applicazione.

    ![Selezionare un'icona per l'applicazione](../media/Android-setup-03.png)

-   Fare clic su **Avanti** e selezionare **Attività vuota** per creare l'attività.

    ![Creare l'attività](../media/Android-setup-04.png)

-   Fare clic su **Avanti** e fornire un nome per l'attività. È possibile lasciare *MainActivity* come nome predefinito con un nome di layout di *activity\_main*.

    ![Specificare un nome per l'attività](../media/Android-setup-05a.jpg)

-   Fare clic su **Fine**.

    ![Terminare la creazione](../media/Android-setup-06.jpg)

-   Il progetto è stato creato, insieme alla classe principale dell'attività *mainactivity. Java*.

**Riferimento all'SDK**

-   Passare alla cartella in cui è stato estratto *adrms\_android\_sdk.zip*. Nella cartella "SDK > com > microsoft > rightsmanagement", assicurarsi che i file *.classpath*, *.project* e *project.properties* non siano contrassegnati come di sola lettura.
-   Per fare riferimento all'SDK, è necessario importarlo nell'area di lavoro.

    In Eclipse, fare clic su **File**. Fare clic su **Importa** dal menu **File**. Nella finestra di dialogo **Importa**, selezionare **Android / Codice Android esistente nell'area di lavoro**.

    ![Importare l'SDK nell'area di lavoro](../media/Android-setup-07.png)

-   Fare clic su **Avanti**. Esplorare per selezionare la cartella in cui è stato estratto *adrms\_android\_sdk.zip*. L'SDK dovrebbe essere visualizzato nell'elenco come **com.microsoft.rightsmanagement**.

    ![Esplorare per selezionare la cartella](../media/Android-setup-08c.jpg)

-   Quando fa clic su **Fine**, il progetto dell'SDK viene visualizzato come elemento di pari livello dell'applicazione creata in precedenza.

    ![Il progetto dell'SDK viene visualizzato come elemento di pari livello dell'applicazione](../media/Android-setup-09.jpg)

-   Fare clic con il pulsante destro del mouse sull'icona del **progetto** e visualizzare le proprietà del progetto.
-   Passare alla scheda **Android**.
-   Fare clic su **Aggiungi** e quindi selezionare la libreria *com.microsoft.rightsmanagement* dall'area di lavoro.

    ![Aggiungere la libreria](../media/Android-setup-10b.jpg)

-   Fare clic su **OK**.

    Poiché MS RMS SDK 4.2 si connette con RM AAD, l'applicazione deve disporre di **INTERNET** e **ACCESS\_NETWORK\_STATE**. A tale scopo, aprire il file *Androidmanifest* nella radice del progetto.

    Per aggiungere le autorizzazioni, fare clic su **Aggiungi** e quindi selezionare **Usa autorizzazioni**.

    ![Aggiungere le autorizzazioni](../media/Android-setup-11d.jpg)

-   È possibile verificare il passaggio manifesto visualizzando il manifesto nell'editor di testo. Assicurarsi che vengano visualizzate le righe seguenti:


    <uses-sdk
         android:minSdkVersion="15"
         android:targetSdkVersion="19"/>
    <uses-permission android:name="android.permission.INTERNET"/>
    <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>
    <uses-permission/>


**Nota** SDK usa *android.support.v4*

-   A questo punto si è pronti a creare le proprie nuove app Android.

### Vedere anche

[Introduzione](get-started.md)

[Novità](release-notes.md)

[Concetti e termini per sviluppatori](core-concepts.md)

[Informazioni di riferimento sulle API di Android](android-namespaces.md)

 

 


<!--HONumber=May16_HO2-->


