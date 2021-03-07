---
title: Attivare Azure RMS dall'interfaccia di amministrazione di Microsoft 365-AIP
description: Informazioni su come attivare il servizio Azure Rights Management dall'interfaccia di amministrazione di Microsoft 365.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 10/27/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: a2b3e1a2-59a0-4191-bf4c-4485ae7a70a9
ms.subservice: azurerms
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 24787eda3b248cab2e6cc3c055611378e39b5c3c
ms.sourcegitcommit: 74b8d03d1ede3da12842b84546417e63897778bb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/07/2021
ms.locfileid: "102414787"
---
# <a name="activate-azure-rights-management-protection-from-the-microsoft-365-admin-center"></a>Attivare la protezione di Azure Rights Management dall'interfaccia di amministrazione di Microsoft 365

>***Si applica a**: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*
>
>***Rilevante per**: [Client di etichettatura unificata e client classico di AIP](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

Questo articolo descrive in che modo gli amministratori globali con accesso al servizio Rights Management di Azure dall'interfaccia di amministrazione di Microsoft 365 possono attivare Rights Management di Azure.

## <a name="prerequisites"></a>Prerequisiti

Per attivare il servizio Azure Rights Management, è necessario un [piano Azure Information Protection Premium](https://www.microsoft.com/cloud-platform/azure-information-protection-pricing) o un [piano di Office 365 che include Rights Management](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf). Ad esempio, l'organizzazione ha un piano per Office 365 E3 o Office 365 E5. 

In caso di domande sui requisiti per la sottoscrizione o se serve assistenza per l'attivazione del servizio, [contattare il supporto tecnico Microsoft](information-support.md#to-contact-microsoft-support) o usare i canali di supporto standard.

## <a name="activating-azure-rights-management"></a>Attivazione di Azure Rights Management

1. Dopo aver verificato che l'organizzazione ha un piano che include Azure Rights Management, passare alla [pagina Rights Management](https://account.activedirectory.windowsazure.com/RmsOnline/Manage.aspx) nell'interfaccia di amministrazione di Microsoft 365.
    
    Se viene richiesto di eseguire l'accesso, usare un account che sia un amministratore globale per Microsoft 365.
    
    > [!TIP]
    > Per la guida all'interfaccia di amministrazione, vedere [Informazioni sull'interfaccia di amministrazione di Microsoft 365](/office365/admin/admin-overview/about-the-admin-center).
    
    Se si preferisce passare alla pagina **Rights Management** dall'interfaccia di amministrazione: **Impostazioni**  >  **Organigramma**  >  **Servizi** scheda > **Microsoft Azure Information Protection**  >  **Gestisci impostazioni Microsoft Azure Information Protection**

2. Nella pagina **rights management** fare clic su **Attiva**.

3. Quando viene visualizzato il messaggio **Do you want to activate Rights Management?** (Attivare Rights Management?) fare clic su **Activate** (Attiva).

Verranno quindi visualizzati il messaggio diavvenuta attivazione di Rights management e l'opzione di disattivazione.

## <a name="next-steps"></a>Passaggi successivi

Riprendere [la lettura attivando il servizio di protezione da Azure Information Protection](activate-service.md#configuring-onboarding-controls-for-a-phased-deployment).

