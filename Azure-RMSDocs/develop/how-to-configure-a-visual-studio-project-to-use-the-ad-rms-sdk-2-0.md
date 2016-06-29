---
# required metadata

title: Configurare Visual Studio | Azure RMS
description: Istruzioni su come configurare un progetto di Visual Studio per l’uso di RMS SDK 2.1.
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 396A2C19-3A00-4E9A-9088-198A48B15289
# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Configurare Visual Studio

Questo argomento contiene le istruzioni su come configurare un progetto di Visual Studio per usare Rights Management Services SDK 2.1.

## Prerequisiti

-   [Installare l'SDK](install-the-rms-sdk.md)

**Istruzioni**

### Passaggio 1: Configurare un progetto di Visual Studio per usare RMS SDK 2.1

Queste istruzioni sono specifiche per Microsoft Visual Studio 2010. Se si utilizza una versione diversa di Microsoft Visual Studio, le finestre di dialogo delle impostazioni possono apparire leggermente diverse.

Queste istruzioni sono valide per la creazione di un'applicazione nativa a 32 bit.

1.  Aggiungere la directory di inclusione di RMS SDK 2.1 al progetto di Visual Studio 2010.

    In **Proprietà di configurazione** selezionare **Directory di VC++** e aggiungere la directory di inclusione di RMS SDK 2.1 **$(MSIPCSDKDIR)\\inc** nel campo **Directory di inclusione**.

    ![Campo delle directory di inclusione in Proprietà di configurazione](../media/include_directories.png)

2.  Aggiungere la directory delle librerie di RMS SDK 2.1 al progetto di Visual Studio 2010.

    In **Proprietà di configurazione** selezionare **Directory di VC + +** e aggiungere la directory delle librerie di RMS SDK 2.1 nel campo **Directory librerie** per la propria piattaforma.

    -   Per Win32 usare **$(MSIPCSDKDIR)\\lib**
    -   Per x64 usare **$(MSIPCSDKDIR)\\lib\\x64**

    ![Campo delle directory delle librerie in Proprietà di configurazione](../media/library_directories.png)

3.  Aggiungere i file di libreria di RMS SDK 2.1 come dipendenze di Visual Studio 2010.

    In **Linker** selezionare **Input** e aggiungere i file di libreria di RMS SDK 2.1 **Msipc.lib** e **Msipc\_s.lib** nel campo **Dipendenze aggiuntive**.

    ![Campo delle dipendenze di libreria in Linker](../media/additional_dependencies.png)

4.  Aggiungere la libreria di collegamento dinamico (DLL) di RMS SDK 2.1 come una DLL a caricamento ritardato.

    In **Linker** selezionare **Input** e aggiungere il file DLL di RMS SDK 2.1 **Msipc.dll** nel campo **DLL a caricamento ritardato**.

    ![Campo delle librerie a caricamento ritardato in Linker](../media/delay_loaded.png)

5.  Creare le informazioni sulla versione per il file binario risultante.

    In **Esplora soluzioni** selezionare **File di risorse** e aggiungere il nome del file binario nel campo **OriginalFileName**.

    ![Campo dei file di risorse in Esplora soluzioni](../media/original_file_name.png)

## Argomenti correlati

* [Installare l'SDK](install-the-rms-sdk.md)
 

 


<!--HONumber=Jun16_HO2-->


