---
title: Sviluppo dell'applicazione | Azure RMS
description: Istruzioni su come sviluppare un'applicazione con RMS SDK 2.1.
keywords: 
author: bruceperlerms
manager: mbaldwin
ms.date: 07/06/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 396A2C19-3A00-4E9A-9088-198A48B15289
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: cb1a4dfa4465e8f4798866c95d8965eec1b68f6b
ms.openlocfilehash: 5dcb3fe88cced7945591a08c492b32bdc8895162


---

# Sviluppo dell'applicazione

Questo argomento contiene informazioni essenziali sugli aspetti principali di un'applicazione abilitata per RMS e può essere utilizzato come base per lo sviluppo delle proprio applicazioni.

## Introduzione

Le istruzioni in questo argomento si basano sull'applicazione di esempio, IPCHelloWorld, che serve a comprendere i concetti di base e il codice di un'applicazione abilitata all'uso di diritti. È possibile scaricare l'intera applicazione di esempio IPCHellowWorld e il file [Webinar_Collateral.zip](https://connect.microsoft.com/site1170/Downloads/DownloadDetails.aspx?DownloadID=42440) da Microsoft Connect.

> [!Note] 
> Il progetto IPCHelloWorld è già configurato per Rights Management Services SDK 2.1. Per informazioni su come configurare un nuovo progetto per l'uso di RMS SDK 2.1, vedere [Configurare Visual Studio](how-to-configure-a-visual-studio-project-to-use-the-ad-rms-sdk-2-0.md).

## Caricamento di MSIPC.dll

Per poter chiamare le funzioni di RMS SDK 2.1, è prima necessario chiamare la funzione [IpcInitialize](/rights-management/sdk/2.1/api/win/functions#msipc_ipcinitialize) per caricare il file MSIPC.dll.

        C++
        hr = IpcInitialize();
        if (FAILED(hr)) {
          wprintf(L"Failed to initialize MSIPC. Are you sure the runtime is installed?\n");
          goto exit;
        }

## Enumerazione dei modelli

Un modello di RMS definisce i criteri usati per proteggere i dati, ad esempio gli utenti autorizzati ad accedere ai dati e i relativi diritti. I modelli di RMS sono installati nel server RMS.

Il frammento di codice seguente consente di enumerare i modelli di RMS disponibili dal server RMS predefinito.

      C++
      hr = IpcGetTemplateList(NULL, 0, 0, NULL, NULL, &pcTil);

      if (FAILED(hr)) {
        DisplayError(L"IpcGetTemplateList failed", hr);
        goto exit;
      }

Questa chiamata recupera i modelli di RMS installati nel server predefinito, carica i risultati nella struttura [IPC_TIL](/rights-management/sdk/2.1/api/win/functions#msipc_ipctil) indicata dalla variabile *pcTil* e quindi visualizza i modelli.

      C++
      if (0 == pcTil->cTi) {
        wprintf(L"*** No templates configured for your RMS server ***\n\n");
        wprintf(L"\\------------------------------------------------------\n\n");
        goto exit;
      }

      for (DWORD dw = 0; dw < pcTil->cTi; dw++) {
        wprintf(L"Template #%d:\n", dw);
        wprintf(L"    Name:         %s\n", pcTil->aTi[dw].wszName);
        wprintf(L"    Description:  %s\n", pcTil->aTi[dw].wszDescription);
        wprintf(L"    Issued by:    %s\n", pcTil->aTi[dw].wszIssuerDisplayName);
        wprintf(L"\n");
      }

## Serializzazione di una licenza

Per poter proteggere i dati, è prima necessario serializzare una licenza e ottenere una chiave simmetrica. La chiave simmetrica viene usata per crittografare i dati sensibili. La licenza serializzata è in genere associata ai dati crittografati e viene usata dal consumer dei dati protetti. Il consumer dovrà chiamare la funzione [IpcGetKey](/rights-management/sdk/2.1/api/win/functions#msipc_ipcgetkey) usando la licenza serializzata per ottenere la chiave simmetrica per la decrittografia del contenuto e il recupero dei criteri associati al contenuto.

Per semplicità, usare il primo modello di RMS restituito da [IpcGetTemplateList](/rights-management/sdk/2.1/api/win/functions#msipc_ipcgettemplatelist) per serializzare una licenza.

In genere, si usa una finestra di dialogo dell'interfaccia utente per consentire all'utente di selezionare il modello desiderato.

      C++
      hr = IpcSerializeLicense((LPCVOID)pcTil->aTi[0].wszID, IPC_SL_TEMPLATE_ID,
        0, NULL, &hContentKey, &pSerializedLicense);

      if (FAILED(hr)) {
        DisplayError(L"IpcSerializeLicense failed", hr);
        goto exit;
      }

Dopo questa operazione si ottengono la chiave simmetrica, *hContentKey*, e la licenza serializzata, *pSerializedLicense*, necessaria per connettersi ai dati protetti.


## Protezione dei dati

A questo punto si è pronti per crittografare i dati sensibili usando la funzione [IpcEncrypt](/rights-management/sdk/2.1/api/win/functions#msipc_ipcencrypt). In primo luogo, è necessario chiedere alla funzione **IpcEncrypt** informazioni sulle dimensioni dei dati crittografati.

      C++
      cbText = (DWORD)(sizeof(WCHAR)*(wcslen(wszText)+1));
      hr = IpcEncrypt(hContentKey, 0, TRUE, (PBYTE)wszText, cbText,
        NULL, 0, &cbEncrypted);

      if (FAILED(hr)) {
        DisplayError(L"IpcEncrypt failed", hr);
        goto exit;
      }

In questo caso wszText contiene il testo normale che deve essere protetto. La funzione [IpcEncrypt](/rights-management/sdk/2.1/api/win/functions#msipc_ipcencrypt) restituisce le dimensioni dei dati crittografati nel parametro *cbEncrypted*.

A questo punto è possibile allocare la memoria per i dati crittografati.

      C++
      pbEncrypted = (PBYTE)LocalAlloc(LPTR, cbEncrypted);

      if (NULL == pbEncrypted) {
        wprintf(L"Out of memory\n");
        goto exit;
      }

Infine, è possibile eseguire la crittografia.

      C++
      hr = IpcEncrypt(hContentKey, 0, TRUE, (PBYTE)wszText, cbText,
        pbEncrypted, cbEncrypted, &cbEncrypted);

      if (FAILED(hr)) {
        DisplayError(L"IpcEncrypt failed", hr);
        goto exit;
      }

Dopo questo passaggio sono disponibili i dati crittografati, *pbEncrypted*, e la licenza serializzata, *pSerializedLicense*, che verrà usata dai consumer per decrittografare i dati.

## Gestione degli errori

In questa applicazione di esempio viene usata la funzione *DisplayError* per gestire gli errori.

      C++
      void DisplayError(LPCWSTR wszErrorInfo, HRESULT hrError)
      {
        LPCWSTR wszErrorMessageText = NULL;

        if (SUCCEEDED(IpcGetErrorMessageText(hrError, 0, &wszErrorMessageText))) {
          wprintf(L"%s: 0x%08X (%s)\n", wszErrorInfo, hrError, wszErrorMessageText);
        }
        else {
          wprintf(L"%s: 0x%08X\n", wszErrorInfo, hrError);
        }
      }

La funzione *DisplayError* usa la funzione [IpcGetErrorMessageText](/rights-management/sdk/2.1/api/win/functions#msipc_ipcgeterrormessagetext) per ottenere il messaggio di errore dal codice errore corrispondente e visualizza il messaggio nell'output standard.

## Pulizia

Per completare la procedura, è anche necessario rilasciare tutte le risorse allocate.

      C++
      if (NULL != pbEncrypted) {
        LocalFree((HLOCAL)pbEncrypted);
      }

      if (NULL != pSerializedLicense) {
        IpcFreeMemory((LPVOID)pSerializedLicense);
      }

      if (NULL != hContentKey) {
        IpcCloseHandle((IPC_HANDLE)hContentKey);
      }

      if (NULL != pcTil) {
        IpcFreeMemory((LPVOID)pcTil);
      }

## Argomenti correlati

- [Istruzioni e informazioni per lo sviluppatore](developer-notes.md)
- [IpcEncrypt](/rights-management/sdk/2.1/api/win/functions#msipc_ipcencrypt)
- [IpcGetErrorMessageText](/rights-management/sdk/2.1/api/win/functions#msipc_ipcgeterrormessagetext)
- [IpcGetKey](/rights-management/sdk/2.1/api/win/functions#msipc_ipcgetkey)
- [IpcGetTemplateList](/rights-management/sdk/2.1/api/win/functions#msipc_ipcgettemplatelist)
- [IpcInitialize](/rights-management/sdk/2.1/api/win/functions#msipc_ipcinitialize)
- [IPC_TIL](/rights-management/sdk/2.1/api/win/functions#msipc_ipctil)
- [Webinar_Collateral.zip](https://connect.microsoft.com/site1170/Downloads/DownloadDetails.aspx?DownloadID=42440)



<!--HONumber=Jul16_HO1-->


