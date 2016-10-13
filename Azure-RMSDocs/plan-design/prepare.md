---
title: Preparazione per la protezione Azure Rights Management| Azure Information Protection
description: Verificare di aver eseguito tutte le operazioni preliminari all'uso del servizio Azure Rights Management, in modo da consentire all'organizzazione di proteggere documenti e messaggi di posta elettronica.
author: cabailey
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
ms.sourcegitcommit: 46db6ef6f65a06c42909252cf99884cc5eaaefe4
ms.openlocfilehash: 5a3df821c70b8cd308f8fb8cc94ee0cff069a3d9


---

# Preparazione per Azure Information Protection

>*Si applica a: Azure Information Protection, Office 365*

Prima di distribuire Azure Information Protection per l'organizzazione, verificare la disponibilità di quanto segue:

-   Account e gruppi utente nel cloud creati manualmente o che sono stati creati automaticamente e sincronizzati dai Servizi di dominio Active Directory (AD DS).

    Quando si sincronizzano gli account e i gruppi locali, non è necessario sincronizzare tutti gli attributi. Per un elenco degli attributi che devono essere sincronizzati per il servizio Azure Rights Management usato da Azure Information Protection, vedere la sezione relativa a [Azure RMS](/active-directory/active-directory-aadconnectsync-attributes-synchronized#azure-rms) nella documentazione di Azure Active Directory. Per facilitare la distribuzione, è consigliabile usare [Azure AD Connect](/active-directory/active-directory-aadconnectsync-whatis) per la connessione delle directory locali ad Azure Active Directory, ma si può usare qualsiasi metodo di sincronizzazione della directory che ottenga lo stesso risultato.

-   Gruppi abilitati alla posta nel cloud da usare con Azure Information Protection. Possono essere gruppi predefiniti o gruppi creati manualmente, che contengono utenti che useranno documenti e messaggi di posta elettronica protetti.

    Se si dispone di Exchange Online, è possibile creare e utilizzare i gruppi abilitati alla posta tramite il centro di amministrazione di Exchange. Se si dispone di AD DS locale e si esegue la sincronizzazione in Azure AD, è possibile creare e utilizzare i gruppi abilitati alla posta che sono gruppi di protezione o gruppi di distribuzione.

## Attivare il servizio Rights Management per la protezione dei dati
Attivare il servizio Rights Management per abilitare questa tecnologia e iniziare a proteggere documenti e messaggi di posta elettronica. Per ulteriori informazioni, vedere l'articolo relativo all'[attivazione di Azure Rights Management](../deploy-use/activate-service.md).






<!--HONumber=Sep16_HO4-->


