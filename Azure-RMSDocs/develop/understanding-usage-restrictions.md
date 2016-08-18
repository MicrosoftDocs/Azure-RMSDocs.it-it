---
title: Informazioni sulle restrizioni di utilizzo | Azure RMS
description: Tutte le applicazioni abilitate per RMS devono imporre restrizioni di utilizzo.
keywords: 
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: E388B16C-ECDA-4696-A040-D457D3C96766
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 872bb0c20db2ef8d661d321598a2b1fe61d69316
ms.openlocfilehash: 2d2cbe580349e1615371a6a76e78140f6577e890


---

# Informazioni sulle restrizioni di utilizzo

Tutte le applicazioni abilitate per RMS devono imporre restrizioni di utilizzo. Una restrizione di utilizzo è una condizione risultante da un tentativo dell'utente di eseguire un'azione, ad esempio la stampa di un documento, ma i criteri RMS per tale documento non concedono autorizzazioni o diritti per eseguire l'azione (ad esempio, il diritto di stampa).

È possibile eseguire query sulle autorizzazioni di un utente per un documento mediante la funzione [**IpcAccessCheck**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcaccesscheck).

## Informazioni sulle restrizioni di utilizzo

-   Acquisire familiarità con i diritti standard di RMS

    Per l'insieme completo dei diritti di RMS che l'applicazione può imporre, vedere [Informazioni di riferimento sulle restrizioni di utilizzo](usage-restriction-reference.md).

    Si noti che i diritti definiti dall'applicazione sono specifici della propria situazione e vanno oltre i diritti standard di RMS.

-   Identificare i punti di imposizione delle restrizione di utilizzo

    Un *punto di imposizione delle restrizioni di utilizzo* è una posizione nel flusso di controllo dell'applicazione in cui è necessario applicare una restrizione di utilizzo. L'argomento [Informazioni di riferimento sulle restrizioni di utilizzo](usage-restriction-reference.md) fornisce vari esempi di punti di imposizione comuni.

    Valutare la propria applicazione per determinare quali punti di imposizione delle restrizioni di utilizzo applicare.

    È possibile che per l'applicazione non siano necessari tutti i punti di imposizione descritti in [Informazioni di riferimento sulle restrizioni di utilizzo](usage-restriction-reference.md). Ad esempio, se l'applicazione non consente agli utenti di stampare il contenuto, non è necessario verificare il diritto **IPC\_GENERIC\_PRINT**.

-   Aggiornare il codice per eseguire un controllo di accesso per ogni punto di imposizione

    Per altre informazioni sull'imposizione di diritti specifici, vedere [Informazioni di riferimento sulle restrizioni di utilizzo](usage-restriction-reference.md).

## Argomenti correlati

* [**IpcAccessCheck**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcaccesscheck)
* [Informazioni di riferimento sulle restrizioni di utilizzo](usage-restriction-reference.md)
 

 



<!--HONumber=Jul16_HO3-->


