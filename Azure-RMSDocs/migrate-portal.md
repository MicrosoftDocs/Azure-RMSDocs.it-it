---
title: Migrazione dal portale di Azure classico - Azure Information Protection
description: Panoramica delle attività di amministrazione nel portale di Azure che venivano precedentemente eseguite nel portale di Azure classico
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 03/09/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 57a1073c-02e0-441b-bf49-c6b72fdba24f
ms.reviewer: demizets
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: dceeee125fb08eae70faab5d956a3382e725b64a
ms.sourcegitcommit: b66b249ab5681d02ec3b5af0b820eda262d5976a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/10/2020
ms.locfileid: "78973186"
---
# <a name="tasks-that-you-used-to-do-with-the-azure-classic-portal"></a>Attività che precedentemente venivano eseguite con il portale di Azure classico

>*Si applica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

>[!NOTE] 
> Per offrire un'esperienza per i clienti unificata e semplificata, il **client di Azure Information Protection client (versione classica)** e la **Gestione etichette** nel portale di Azure vengono **deprecati** a partire dal **31 marzo 2021**. In questo intervallo di tempo tutti i clienti correnti di Azure Information Protection possono passare alla soluzione di etichettatura unificata usando la piattaforma di etichettatura unificata di Microsoft Information Protection. Altre informazioni nell'[avviso ufficiale sulla deprecazione](https://aka.ms/aipclassicsunset).

Questo articolo contiene suggerimenti per chi ha sempre usato il portale di Azure classico per la gestione del servizio Azure Rights Management e ora ha bisogno di aiuto per la transizione al portale di Azure.

Il portale di Azure classico è stato ritirato l'**8 gennaio 2018**. A partire da tale data non è più possibile gestire il servizio Azure Rights Management e i modelli personalizzati dal portale classico. Se si tenta di accedere al portale classico, viene visualizzato un collegamento che consente di passare al nuovo portale di Azure.

Per altre informazioni sul ritiro del portale classico, vedere il post del blog [Marching into the future of the Azure AD admin experience: retiring the Azure classic portal](https://cloudblogs.microsoft.com/enterprisemobility/2017/09/18/marching-into-the-future-of-the-azure-ad-admin-experience-retiring-the-azure-classic-portal/) (Verso il futuro dell'amministrazione di Azure AD: ritiro del portale di Azure classico). Per l'estensione temporanea alla data di ritiro originale, vedere [Update on retirement of Azure AD classic portal experience and migration of conditional access policies](https://cloudblogs.microsoft.com/enterprisemobility/2017/11/29/update-on-retirement-of-azure-ad-classic-portal-experience-and-migration-of-conditional-access-policies/) (Aggiornamento sul ritiro dell'esperienza del portale di Azure AD classico e sulla migrazione dei criteri di accesso condizionale).

## <a name="how-to-do-your-familiar-admin-tasks"></a>Come eseguire le attività di amministrazione più comuni

Usare le informazioni seguenti per una transizione rapida al portale aggiornato.

|Portale di Azure classico|Come eseguire questa operazione nel portale di Azure
|-----------|--------------------|
|Accedere alle impostazioni di configurazione per la prima volta|1. [accedere al portale di Azure](configure-policy.md#signing-in-to-the-azure-portal).<br /><br />2. seguire le istruzioni per [accedere al riquadro Azure Information Protection per la prima volta](configure-policy.md#to-access-the-azure-information-protection-pane-for-the-first-time).
|Creare un nuovo modello|Creare un'etichetta che applica la protezione e usare **Impostare le autorizzazioni** per definire le autorizzazioni, la scadenza e l'accesso offline. <br /><br />Dietro le quinte, la configurazione crea un nuovo modello predefinito accessibile dai servizi e dalle applicazioni che si integrano con i modelli di Rights Management.<br /><br />Per altre informazioni, vedere [Per creare un nuovo modello](configure-policy-templates.md#to-create-a-new-template).
|Modificare le proprietà del modello: <br /><br />- Nome e descrizione del modello<br /><br />- Diritti di utilizzo, scadenza del contenuto e impostazioni di accesso offline|Se non è già stato fatto, [convertire il modello in etichetta](configure-policy-templates.md#to-convert-templates-to-labels) e quindi eseguire le operazioni seguenti<br /><br />1. modificare il nome e la descrizione dell'etichetta<br /><br />2. modificare le impostazioni di protezione sull'etichetta per aggiornare le autorizzazioni, la scadenza e le impostazioni di accesso offline.<br /><br />Per altre informazioni, vedere [Per configurare un'etichetta per le impostazioni di protezione](configure-policy-protection.md#to-configure-a-label-for-protection-settings).
|Archiviare un modello|Impostare lo stato dell'etichetta su **Disabilitato**.
|Creare un modello con ambito|Creare criteri con ambito e creare un'etichetta in tale ambito che applichi la protezione. <br /><br />Per altre informazioni, vedere [Come configurare i criteri di Azure Information Protection per utenti specifici con i criteri con ambito](configure-policy-scope.md).
|Copiare un modello|Non è possibile copiare un modello nel portale di Azure. Se si vuole che due etichette abbiano le stesse impostazioni di protezione, è necessario impostare le autorizzazioni in ogni etichetta. <br /><br />Per altre informazioni, vedere [Per configurare un'etichetta per le impostazioni di protezione](configure-policy-protection.md#to-configure-a-label-for-protection-settings).
|Eliminare un modello|L'eliminazione di modelli può comportare che alcuni dati risultino inaccessibili, pertanto il portale di Azure non supporta questa azione. Tuttavia, è possibile eliminare l'etichetta e quindi usare il cmdlet [Remove-AipServiceTemplate](/powershell/module/aipservice/remove-aipservicetemplate) di PowerShell per rimuovere il modello. <br /><br />Per altre informazioni, vedere [Come eliminare o riordinare un'etichetta per Azure Information Protection](configure-policy-delete-reorder.md).
|Supporto per più lingue|Dalla selezione di menu **Gestisci** selezionare **Lingue** per esportare i campi personalizzabili che includono il nome e la descrizione del modello. Tradurre le stringhe e importarle nel portale. <br /><br />Per altre informazioni, vedere [Come configurare etichette e modelli per varie lingue in Azure Information Protection](configure-policy-languages.md).
|Report Web di Rights Management|[Reporting centralizzato per Azure Information Protection](reports-aip.md) è ora disponibile in anteprima.<br /><br />È anche possibile usare il cmdlet PowerShell [Get-AipServiceUsageLog](/powershell/module/aipservice/get-aipserviceuserlog) per scaricare i log di utilizzo per il servizio Azure Rights Management. È quindi possibile usare i dati per creare report personalizzati. Per ulteriori informazioni, vedere [registrazione e analisi dell'utilizzo della protezione da Azure Information Protection](log-analyze-usage.md).
|Attivare e disattivare il servizio Rights Management|Scegliere **Attivazione della protezione** dal menu **Gestisci**.<br /><br />Per ulteriori informazioni, vedere [come attivare il servizio Rights Management Protection dal portale di Azure](activate-azure.md).

Prima di modificare i modelli o convertirli in etichette nel portale di Azure, vedere [Considerazioni sui modelli nel portale di Azure](configure-policy-templates.md#considerations-for-templates-in-the-azure-portal).


## <a name="what-else-has-changed"></a>Altre novità

Nuove funzionalità nel portale di Azure:

- È possibile modificare i [modelli predefiniti](configure-policy-templates.md#default-templates) che vengono creati automaticamente per l'organizzazione.

- È possibile convertire i modelli in etichette, in modo da gestire un singolo oggetto anziché gestire un modello e un'etichetta separatamente. Per le istruzioni, vedere [Per convertire i modelli in etichette](configure-policy-templates.md#to-convert-templates-to-labels).

- Supporto per altri ruoli di amministratore: mentre era necessario accedere al portale di Azure classico come amministratore globale per configurare Rights Management di Azure, è possibile accedere al portale di Azure per gestire Azure Information Protection usando molti altri ruoli amministrativi che includono l'amministratore della **conformità** e l' **amministratore dei dati di conformità**. L'elenco completo dei ruoli supportati è incluso nella sezione [accesso alla portale di Azure](configure-policy.md#signing-in-to-the-azure-portal) .

Il supporto dei cmdlet di PowerShell per creare e gestire i modelli e per attivare e disattivare il servizio rimane invariato.

## <a name="see-also"></a>Vedere anche
Per altre informazioni, vedere [Configurazione e gestione dei modelli per Azure Information Protection](configure-policy-templates.md).

