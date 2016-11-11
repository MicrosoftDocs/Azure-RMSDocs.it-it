---
title: Preparazione per la protezione Azure Rights Management| Azure Information Protection
description: Verificare di aver eseguito tutte le operazioni preliminari all&quot;uso del servizio Azure Rights Management, in modo da consentire all&quot;organizzazione di proteggere documenti e messaggi di posta elettronica.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 09/25/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: afbca2d6-32a7-4bda-8aaf-9f93f5da5abc
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 9d8354f2d68f211d349226970fd2f83dd0ce810b
ms.openlocfilehash: facb9bd0d21551e9170cd9be6e9abda24766f9fd


---

# <a name="preparing-for-azure-information-protection"></a>Preparazione per Azure Information Protection

>*Si applica a: Azure Information Protection, Office 365*

Prima di distribuire Azure Information Protection per l'organizzazione, verificare la disponibilità di quanto segue:

-   Account e gruppi utente nel cloud creati manualmente o che sono stati creati automaticamente e sincronizzati dai Servizi di dominio Active Directory (AD DS).

    Quando si sincronizzano gli account e i gruppi locali, non è necessario sincronizzare tutti gli attributi. Per un elenco degli attributi che devono essere sincronizzati per il servizio Azure Rights Management usato da Azure Information Protection, vedere la sezione relativa a [Azure RMS](/active-directory/active-directory-aadconnectsync-attributes-synchronized#azure-rms) nella documentazione di Azure Active Directory. Per facilitare la distribuzione, è consigliabile usare [Azure AD Connect](/active-directory/active-directory-aadconnectsync-whatis) per la connessione delle directory locali ad Azure Active Directory, ma si può usare qualsiasi metodo di sincronizzazione della directory che ottenga lo stesso risultato.

-   Gruppi abilitati alla posta nel cloud da usare con Azure Information Protection. Possono essere gruppi predefiniti o gruppi creati manualmente, che contengono utenti che useranno documenti e messaggi di posta elettronica protetti.

    Se si dispone di Exchange Online, è possibile creare e utilizzare i gruppi abilitati alla posta tramite il centro di amministrazione di Exchange. Se si dispone di AD DS locale e si esegue la sincronizzazione in Azure AD, è possibile creare e utilizzare i gruppi abilitati alla posta che sono gruppi di protezione o gruppi di distribuzione.

## <a name="activate-the-rights-management-service-for-data-protection"></a>Attivare il servizio Rights Management per la protezione dei dati
Attivare il servizio Rights Management per abilitare questa tecnologia e iniziare a proteggere documenti e messaggi di posta elettronica. Per ulteriori informazioni, vedere l'articolo relativo all'[attivazione di Azure Rights Management](../deploy-use/activate-service.md).






<!--HONumber=Nov16_HO2-->


