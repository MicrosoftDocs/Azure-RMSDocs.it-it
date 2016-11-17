---
title: Informazioni sulle restrizioni di utilizzo | Azure RMS
description: Tutte le applicazioni abilitate per RMS devono imporre restrizioni di utilizzo.
keywords: 
author: bruceperlerms
ms.author: bruceper
manager: mbaldwin
ms.date: 09/25/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: E388B16C-ECDA-4696-A040-D457D3C96766
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 9d8354f2d68f211d349226970fd2f83dd0ce810b
ms.openlocfilehash: cc383728d487cac45e59ef34ca43ba47c4db237b


---

# <a name="understanding-usage-restrictions"></a>Informazioni sulle restrizioni di utilizzo

Tutte le applicazioni abilitate per RMS devono imporre restrizioni di utilizzo. Una restrizione di utilizzo è una condizione risultante da un tentativo dell'utente di eseguire un'azione, ad esempio la stampa di un documento, ma i criteri RMS per tale documento non concedono autorizzazioni o diritti per eseguire l'azione (ad esempio, il diritto di stampa).

È possibile eseguire query sulle autorizzazioni di un utente per un documento tramite la funzione [IpcAccessCheck](https://msdn.microsoft.com/library/hh535253.aspx).

## <a name="understanding-usage-restrictions"></a>Informazioni sulle restrizioni di utilizzo

-   Acquisire familiarità con i diritti standard di RMS

    Per l'insieme completo dei diritti di RMS che l'applicazione può imporre, vedere [Informazioni di riferimento sulle restrizioni di utilizzo](usage-restriction-reference.md).

    Si noti che i diritti definiti dall'applicazione sono specifici della propria situazione e vanno oltre i diritti standard di RMS.

-   Identificare i punti di imposizione delle restrizione di utilizzo

    Un *punto di imposizione delle restrizioni di utilizzo* è una posizione nel flusso di controllo dell'applicazione in cui è necessario applicare una restrizione di utilizzo. L'argomento [Informazioni di riferimento sulle restrizioni di utilizzo](usage-restriction-reference.md) fornisce vari esempi di punti di imposizione comuni.

    Valutare la propria applicazione per determinare quali punti di imposizione delle restrizioni di utilizzo applicare.

    È possibile che per l'applicazione non siano necessari tutti i punti di imposizione descritti in [Informazioni di riferimento sulle restrizioni di utilizzo](usage-restriction-reference.md). Ad esempio, se l'applicazione non consente agli utenti di stampare il contenuto, non è necessario verificare il diritto **IPC\_GENERIC\_PRINT**.

-   Aggiornare il codice per eseguire un controllo di accesso per ogni punto di imposizione

    Per altre informazioni sull'imposizione di diritti specifici, vedere [Informazioni di riferimento sulle restrizioni di utilizzo](usage-restriction-reference.md).

## <a name="related-topics"></a>Argomenti correlati

* [IpcAccessCheck](https://msdn.microsoft.com/library/hh535253.aspx)
* [Informazioni di riferimento sulle restrizioni di utilizzo](usage-restriction-reference.md)
 

 



<!--HONumber=Nov16_HO2-->


