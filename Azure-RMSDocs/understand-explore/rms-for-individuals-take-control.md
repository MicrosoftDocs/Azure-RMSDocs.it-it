---
title: Controllare gli account creati per RMS per utenti singoli - AIP
description: "Informazioni su come è possibile controllare gli account utente in Azure Active Directory se non si vuole convertire la sottoscrizione di RMS per utenti singoli dell&quot;organizzazione in una sottoscrizione a pagamento."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/23/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: a83880d0-f0f9-4a32-9e00-2f6635d7cc8d
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 2131f40b51f34de7637c242909f10952b1fa7d9f
ms.openlocfilehash: ff8cd150ce438a7b9ad5203dfb6d9d01c1a0d85a
ms.lasthandoff: 02/24/2017


---



# <a name="how-administrators-can-control-the-accounts-created-for-rms-for-individuals"></a>Modalità di controllo da parte degli amministratori degli account creati per RMS per utenti singoli

>*Si applica a: Azure Information Protection*


Se non si desidera convertire la sottoscrizione di RMS per utenti singoli dell'organizzazione in una sottoscrizione a pagamento, è comunque possibile controllare gli account utente nella directory di Azure creata per l'organizzazione nei modi seguenti:

-   Implementare soluzioni di integrazione delle directory per Azure Active Directory e per l'infrastruttura Servizi di dominio Active Directory. È possibile sincronizzare account e password in modo che gli utenti non debbano creare nuovi account per usare Rights Management e che i criteri associati alle password locali vengano applicati ai nuovi account utente di Azure. È inoltre possibile sincronizzare le password in modo che gli utenti non debbano ricordare una password diversa per usare Rights Management.

-   È possibile impedire agli utenti di eseguire l'iscrizione per usare Azure Rights Management con la sottoscrizione RMS per utenti singoli. Nella maggior parte dei casi, questa azione non è molto vantaggiosa perché gli utenti condivideranno file senza protezione (con potenziali rischi per la società) o useranno un altro meccanismo di protezione dei file, impedendo al personale del reparto IT di accedere ai dati. Se però si vuole impedire agli utenti di usare RMS per utenti singoli, effettuare una delle operazioni seguenti dopo aver acquisito la proprietà della directory dell'organizzazione in Azure:

    -   Impedire a tutti gli utenti di iscriversi alle sottoscrizioni self-service, incluso RMS per utenti singoli.  Attualmente, non è possibile impostare questo dal servizio; l'impostazione si applica a tutte le sottoscrizioni di Azure che utilizzano il processo self-service. A questo scopo, impostare il parametro **AllowAdHocSubscriptions** su false con il cmdlet [Set-MsolCompanySettings](http://technet.microsoft.com/library/dn194127.aspx) del modulo PowerShell per Azure Active Directory. Ad esempio: **Set-MsolCompanySettings -AllowAdHocSubscriptions $false**

    -   Impedire agli utenti di creare un nuovo account in Azure. In questo modo, solo gli utenti che dispongono già di un account in Azure potranno iscriversi alle sottoscrizioni self-service, incluso RMS per utenti singoli.  A questo scopo, impostare il parametro **AllowEmailVerifiedUsers** su false con il cmdlet [Set-MsolCompanySettings](http://technet.microsoft.com/library/dn194127.aspx) del modulo PowerShell per Azure Active Directory. Ad esempio: **Set-MsolCompanySettings -AllowEmailVerifiedUsers $false -AllowAdHocSubscriptions $true**

    -   Sincronizzare 'infrastruttura Servizi di dominio Active Directory con Azure Active Directory. In questo modo si impedisce la creazione di nuovi account quando gli utenti si iscrivono a sottoscrizioni self-service come RMS per utenti singoli ed è possibile eliminare o disabilitare account creati in precedenza nella directory di Azure.

Per controllare gli account utente nella directory di Azure o impedire agli utenti di iscriversi a RMS per utenti singoli, è necessario disporre di una sottoscrizione di Azure ed essere proprietari della directory di Azure. Se non si dispone ancora di una sottoscrizione di Azure, è possibile ottenerne una senza alcun costo aggiuntivo. Se durante il processo self-service è stata creata automaticamente una directory, acquisire la proprietà del dominio usato per crearla. Se si dispone già di una directory in Azure, ma gli utenti hanno specificato un nuovo dominio in uso nell'organizzazione, unire il dominio alla directory esistente. Per ulteriori informazioni, vedere le istruzioni in [Cos’è Self-Service Signup per Azure?](https://azure.microsoft.com/documentation/articles/active-directory-self-service-signup/)


## <a name="next-steps"></a>Passaggi successivi

Come è possibile determinare se gli utenti, anziché gli amministratori, hanno creato i propri account in Azure Active Directory per RMS per utenti singoli?  Vedere [Come determinare se gli utenti hanno effettuato l'iscrizione per RMS per utenti singoli](rms-for-individuals-identify-sign-up.md).

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
