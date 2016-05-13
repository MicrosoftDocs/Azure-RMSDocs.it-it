---
# required metadata

title: Condizioni di errore comuni e relative soluzioni | Azure RMS
description: Questo argomento include i messaggi di errore più comuni che possono essere visualizzati quando si usano gli strumenti di sviluppo RMS SDK 2.1.
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: ac6453e1-e24f-480e-99bd-02ba9a49f468

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
# Condizioni di errore comuni e relative soluzioni
Questo argomento include i messaggi di errore più comuni che possono essere visualizzati quando si usano gli strumenti di sviluppo Rights Management Services SDK 2.1. Riporta inoltre un'azione consigliata per correggere l'errore, se applicabile.

**Importante**: per l'elaborazione della condizione di errore, usare sempre una chiamata a [IpcGetErrorMessageText](/rights-management/sdk/2.1/api/win/functions#msipc_ipcgeterrormessagetext) immediatamente dopo una chiamata API SDK non avvenuta correttamente per ottenere informazioni complete sulla natura dell'errore.

 

## Errore e azione ##
L'elenco seguente include alcune costanti di errori, la relativa descrizione e un'azione consigliata per risolvere la condizione di errore.

**ERRORE** - *IPCERROR_DEBUGGER_DETECTED*: RMS SDK 2.1 ha rilevato un debugger

**AZIONE**: la versione per gli sviluppatori di RMS SDK 2.1 non verifica la presenza di un debugger. Se possibile, eseguire il debug dell'applicazione usando questa versione di RMS SDK 2.1.
Se è necessario eseguire il debug della versione di produzione di RMS SDK 2.1, usare le linee guida seguenti.

Alcune funzioni di RMS SDK 2.1 sono progettate per avere esito negativo con un debugger:
- [IpcGetKey</strong>](/rights-management/sdk/2.1/api/win/functions#msipc_ipcgetkey)
- [IpcGetTemplateList](/rights-management/sdk/2.1/api/win/functions#msipc_ipcgettemplatelist)
- [IpcGetTemplateIssuerList](/rights-management/sdk/2.1/api/win/functions#msipc_ipcgettemplateissuerlist)

Per eseguire il debug del codice in seguito a queste chiamate di funzione, è necessario interrompere il processo e collegare un debugger dopo aver completato le chiamate di funzione. Per eseguire questa operazione è possibile usare un'istruzione di asserzione per interrompere l'esecuzione del debugger. La macro ASSERTE è inclusa nell'intestazione *Crtdbg. h*.
Per ulteriori informazioni su \_ASSERTE, vedere [\_ASSERT, macro \_ASSERTE](https://msdn.microsoft.com/en-us/library/ezb1wyez.aspx)

**ERRORE** - *IPCERROR_BROKEN_CERT_CHAIN*: la catena di certificati non corrisponde.

**AZIONE**: assicurarsi che la chiave di gerarchia contenga il valore corretto in base alla chiave usata per firmare il manifesto dell'applicazione AD RMS.
Queste sono le chiavi di firma e i relativi valori associati (gerarchia **DWORD**):
- ISV-1
- Produzione-0 o non presente

**ERRORE** - *IPCERROR_MACHINE_CERT_NOT_TRUSTED* : si usa un'applicazione firmata con la chiave di firma ISV che sta tentando di comunicare con un server di produzione AD RMS, o viceversa.

- Se si sta usando la versione per gli sviluppatori del server AD RMS, verificare l'effettivo uso della chiave di firma ISV per firmare l'applicazione.
- Se si sta usando la versione di produzione del server AD RMS, verificare l'effettivo uso della chiave di firma per la produzione per firmare l'applicazione.

**ERRORE** - *IPCERROR_APPLICATION_AUTH_ERROR_MANIFEST*: il manifesto dell'applicazione non è valido. Questo può verificarsi quando il file binario (applicazione) è stato ricreato e il manifesto non è stato rigenerato.

**AZIONE**: assicurarsi di rigenerare il manifesto dell'applicazione ogni volta che si ricrea l'applicazione.

## Argomenti correlati ##
* [Note per gli sviluppatori](developer-notes.md)
* [IpcGetKey](/rights-management/sdk/2.1/api/win/functions#msipc_ipcgetkey)
* [IpcGetTemplateList](/rights-management/sdk/2.1/api/win/functions#msipc_ipcgettemplatelist)
* [IpcGetTemplateIssuerList](/rights-management/sdk/2.1/api/win/functions#msipc_ipcgettemplateissuerlist)
* [\_ASSERT, macro \_ASSERTE](https://msdn.microsoft.com/en-us/library/ezb1wyez.aspx)
 

 


<!--HONumber=Apr16_HO3-->


