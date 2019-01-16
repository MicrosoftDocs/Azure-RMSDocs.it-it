---
title: Come eseguire il debug dell'applicazione abilitata all'uso di diritti | Azure RMS
description: L'argomento seguente illustra come eseguire il debug dell'applicazione e usare il registro eventi di Windows.
keywords: ''
author: bryanla
ms.author: bryanla
manager: mbaldwin
ms.date: 02/23/2017
ms.topic: conceptual
ms.service: information-protection
ms.assetid: 6F6C7651-6A6E-45DD-A0C5-F036F803249B
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
ms.openlocfilehash: cb77177ecb0c92f3e991e0f6d06a55fa2c332873
ms.sourcegitcommit: bd2b31dd97c8ae08c28b0f5688517110a726e3a1
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/08/2019
ms.locfileid: "54071555"
---
# <a name="how-to-debug-a-rights-enabled-application"></a>Procedura: Eseguire il debug dell'applicazione abilitata all'uso di diritti

L'argomento seguente illustra come eseguire il debug dell'applicazione e usare il registro eventi di Windows.

## <a name="debugging-your-application"></a>Debug dell'applicazione

In Rights Management Services SDK 2.1, nella versione per gli sviluppatori del runtime, i controlli anti-debug sono disabilitati.

È possibile attivare la traccia del debug usando la chiave del Registro di sistema seguente. Per disattivare la traccia del debug, modificare il valore su 0. In questa versione non è necessaria nessun altra operazione per il debug.


```
HKEY_LOCAL_MACHINE
   SOFTWARE
      Microsoft
         MSIPC
            "Trace" = 00000001
            Data type
            dword
```

### <a name="application-logging-by-using-the-windows-event-log"></a>Registrazione dell'applicazione tramite il registro eventi di Windows

Il nome del registro eventi è "Microsoft-RMS-MSIPC/Debug". Ciò significa che in Visualizzatore eventi di Windows il registro viene visualizzato come "Registri applicazioni e servizi\\Microsoft\\RMS\\MSIPC\\Debug".

**Nota**:  il registro è abilitato per impostazione predefinita ed è impostato sul livello di dettaglio 3.

 

Per modificare le impostazioni della funzionalità di registrazione, è possibile usare l'interfaccia utente per il Visualizzatore eventi di Windows o Wevtutil, uno strumento da riga di comando di Windows.

Tramite l'interfaccia Wevtutil, è possibile controllare il livello di dettaglio del registro.

Sono attualmente supportati 3 livelli di registrazione:

-   Livello 2: Errore
-   Livello 3: Avviso
-   Livello 4: Informazioni

Ad esempio, il comando seguente abiliterà il registro eventi MSIPC e imposterà il livello di dettaglio su Informazioni.

**wevtutil sl Microsoft-RMS-MSIPC/Debug /e:true /l:4**

**Nota**:  nel menu **Visualizza** del Visualizzatore eventi di Windows selezionare **Visualizza registri analitici e di debug**  per rendere visibile il registro di debug MSIPC.
