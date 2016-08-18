---
title: Preparazione per Azure Rights Management | Azure RMS
description: 
keywords: 
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: afbca2d6-32a7-4bda-8aaf-9f93f5da5abc
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 0f355da35dff62ecee111737eb1793ae286dc93e
ms.openlocfilehash: 55f092ede1f003c700cb58359bab264772702c39


---

# Preparazione per Azure Rights Management

*Si applica a: Azure Rights Management, Office 365*

Dopo essersi iscritti per una sottoscrizione cloud e aver configurato l'organizzazione con un account per [!INCLUDE[o365_1](../includes/o365_1_md.md)] o Azure Active Directory, si è pronti per abilitare il servizio [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)].

Prima di procedere all'abilitazione del servizio, assicurarsi di soddisfare i requisiti seguenti:

-   Account e gruppi utente nel cloud creati manualmente o che sono stati creati automaticamente e sincronizzati dai Servizi di dominio Active Directory (AD DS).

    Quando si sincronizzano gli account e i gruppi locali, non è necessario sincronizzare tutti gli attributi. Per un elenco degli attributi che devono essere sincronizzati per Azure RMS, vedere la [sezione di Azure RMS](/active-directory/active-directory-aadconnectsync-attributes-synchronized#azure-rms) nella documentazione di Azure Active Directory. Per facilitare la distribuzione, è consigliabile usare [Azure AD Connect](/active-directory/active-directory-aadconnectsync-whatis) per la connessione delle directory locali ad Azure Active Directory, ma si può usare qualsiasi metodo di sincronizzazione della directory che ottenga lo stesso risultato.

-   Gruppi abilitati alla posta nel cloud da usare con Rights Management. Possono essere gruppi predefiniti o gruppi creati manualmente, che contengono utenti che useranno Rights Management.

    Se si dispone di Exchange Online, è possibile creare e utilizzare i gruppi abilitati alla posta tramite il centro di amministrazione di Exchange. Se si dispone di AD DS locale e si esegue la sincronizzazione in Azure AD, è possibile creare e utilizzare i gruppi abilitati alla posta che sono gruppi di protezione o gruppi di distribuzione.

## Abilitare Rights Management
Per impostazione predefinita, [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] è disabilitato quando ci si iscrive per l'account [!INCLUDE[o365_2](../includes/o365_2_md.md)] o Azure AD. Per abilitare [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] per l'organizzazione, è necessario attivare il servizio. Per ulteriori informazioni, vedere l'articolo relativo all'[attivazione di Azure Rights Management](../deploy-use/activate-service.md).






<!--HONumber=Jun16_HO4-->


