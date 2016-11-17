---
title: Sviluppo dell&quot;applicazione | Azure RMS
description: Istruzioni su come sviluppare un&quot;applicazione con RMS SDK 2.1.
keywords: 
author: bruceperlerms
ms.author: bruceper
manager: mbaldwin
ms.date: 11/01/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 396A2C19-3A00-4E9A-9088-198A48B15289
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 4560a1cf3424ae4dddd3a0675b62e9c5e55de9fa
ms.openlocfilehash: 1f46d93a47fae3b7e7de334db73b7e7b65ea6eea


---

# <a name="developing-your-application"></a>Sviluppo dell'applicazione

Questo argomento contiene informazioni essenziali sugli aspetti principali di un'applicazione abilitata per RMS e può essere utilizzato come base per lo sviluppo delle proprio applicazioni.

## <a name="introduction"></a>Introduzione

Le istruzioni in questo argomento si basano sull'applicazione di esempio *IPCHelloWorld*, che serve a comprendere i concetti di base e il codice di un'applicazione abilitata all'uso di diritti. Il progetto *IPCHelloWorld* è già configurato per Rights Management Services SDK 2.1.

### <a name="download-sample"></a>Scaricare l'esempio
- Verificare di essere registrati nel sito Connect:
  - Per registrarsi, andare al sito [Connect](http://connect.microsoft.com)
  - Accedere con l'account Microsoft
  - Andare a [Rights Management nel sito Connect](https://connect.microsoft.com/site1170)
  - Aggiungi 
- Scaricare l'intera applicazione di esempio *IPCHellowWorld* e il file [Webinar_Collateral.zip](https://connect.microsoft.com/site1170/Downloads/DownloadDetails.aspx?DownloadID=42440)

Per informazioni su come configurare un nuovo progetto per l'uso di RMS SDK 2.1, vedere [Configurare Visual Studio](how-to-configure-a-visual-studio-project-to-use-the-ad-rms-sdk-2-0.md).



## <a name="loading-msipcdll"></a>Caricamento di MSIPC.dll

Per poter chiamare le funzioni di RMS SDK 2.1, è prima necessario chiamare la funzione [IpcInitialize](https://msdn.microsoft.com/library/jj127295.aspx) per caricare il file MSIPC.dll.

        C++
        hr = IpcInitialize();
        if (FAILED(hr)) {
          wprintf(L"Failed to initialize MSIPC. Are you sure the runtime is installed?\n");
          goto exit;
        }

## <a name="enumerating-templates"></a>Enumerazione dei modelli

Un modello di RMS definisce i criteri usati per proteggere i dati, ad esempio gli utenti autorizzati ad accedere ai dati e i relativi diritti. I modelli di RMS sono installati nel server RMS.

Il frammento di codice seguente consente di enumerare i modelli di RMS disponibili dal server RMS predefinito.

      C++
      hr = IpcGetTemplateList(NULL, 0, 0, NULL, NULL, &pcTil);

      if (FAILED(hr)) {
        DisplayError(L"IpcGetTemplateList failed", hr);
        goto exit;
      }

Questa chiamata recupera i modelli di RMS installati nel server predefinito, carica i risultati nella struttura [IPC_TIL](https://msdn.microsoft.com/library/hh535283.aspx) indicata dalla variabile *pcTil* e quindi visualizza i modelli.

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

## <a name="serializing-a-license"></a>Serializzazione di una licenza

Per poter proteggere i dati, è prima necessario serializzare una licenza e ottenere una chiave simmetrica. La chiave simmetrica viene usata per crittografare i dati sensibili. La licenza serializzata è in genere associata ai dati crittografati e viene usata dal consumer dei dati protetti. Il consumer dovrà chiamare la funzione [IpcGetKey](https://msdn.microsoft.com/library/hh535263.aspx) usando la licenza serializzata per ottenere la chiave simmetrica per la decrittografia del contenuto e il recupero dei criteri associati al contenuto.

Per semplicità, usare il primo modello di RMS restituito da [IpcGetTemplateList](https://msdn.microsoft.com/library/hh535267.aspx) per serializzare una licenza.

In genere, si usa una finestra di dialogo dell'interfaccia utente per consentire all'utente di selezionare il modello desiderato.

      C++
      hr = IpcSerializeLicense((LPCVOID)pcTil->aTi[0].wszID, IPC_SL_TEMPLATE_ID,
        0, NULL, &hContentKey, &pSerializedLicense);

      if (FAILED(hr)) {
        DisplayError(L"IpcSerializeLicense failed", hr);
        goto exit;
      }

Dopo questa operazione si ottengono la chiave simmetrica, *hContentKey*, e la licenza serializzata, *pSerializedLicense*, necessaria per connettersi ai dati protetti.


## <a name="protecting-data"></a>Protezione dei dati

A questo punto si è pronti per crittografare i dati sensibili usando la funzione [IpcEncrypt](https://msdn.microsoft.com/library/hh535259.aspx). In primo luogo, è necessario chiedere alla funzione **IpcEncrypt** informazioni sulle dimensioni dei dati crittografati.

      C++
      cbText = (DWORD)(sizeof(WCHAR)*(wcslen(wszText)+1));
      hr = IpcEncrypt(hContentKey, 0, TRUE, (PBYTE)wszText, cbText,
        NULL, 0, &cbEncrypted);

      if (FAILED(hr)) {
        DisplayError(L"IpcEncrypt failed", hr);
        goto exit;
      }

In questo caso *wszText* contiene il testo normale che deve essere protetto. La funzione [IpcEncrypt](https://msdn.microsoft.com/library/hh535259.aspx) restituisce le dimensioni dei dati crittografati nel parametro *cbEncrypted*.

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

## <a name="error-handling"></a>Gestione degli errori

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

La funzione *DisplayError* usa la funzione [IpcGetErrorMessageText](https://msdn.microsoft.com/library/hh535261.aspx) per ottenere il messaggio di errore dal codice errore corrispondente e visualizza il messaggio nell'output standard.

## <a name="cleaning-up"></a>Pulizia

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

## <a name="related-topics"></a>Argomenti correlati

- [Istruzioni e informazioni per lo sviluppatore](developer-notes.md)
- [IpcEncrypt](https://msdn.microsoft.com/library/hh535259.aspx)
- [IpcGetErrorMessageText](https://msdn.microsoft.com/library/hh535261.aspx)
- [IpcGetKey](https://msdn.microsoft.com/library/hh535263.aspx)
- [IpcGetTemplateList](https://msdn.microsoft.com/library/hh535267.aspx)
- [IpcInitialize](https://msdn.microsoft.com/library/jj127295.aspx)
- [IPC_TIL](https://msdn.microsoft.com/library/hh535283.aspx)
- [Webinar_Collateral.zip](https://connect.microsoft.com/site1170/Downloads/DownloadDetails.aspx?DownloadID=42440)



<!--HONumber=Nov16_HO1-->


