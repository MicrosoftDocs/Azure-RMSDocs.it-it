---
title: Migrazione dal portale di Azure classico - Azure Information Protection
description: "Panoramica delle attività di amministrazione nel portale di Azure che venivano precedentemente eseguite nel portale di Azure classico"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/13/2018
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 57a1073c-02e0-441b-bf49-c6b72fdba24f
ms.reviewer: demizets
ms.suite: ems
ms.openlocfilehash: 5f160d766abb4a81864ac1ff466362b8ae24027d
ms.sourcegitcommit: c157636577db2e2a2ba5df81eb985800cdb82054
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/14/2018
---
# <a name="tasks-that-you-used-to-do-with-the-azure-classic-portal"></a>Attività che precedentemente venivano eseguite con il portale di Azure classico

>*Si applica a: Azure Information Protection, Office 365*

Questo articolo contiene suggerimenti per chi ha sempre usato il portale di Azure classico per la gestione del servizio Azure Rights Management e ora ha bisogno di aiuto per la transizione al portale di Azure.

Il portale di Azure classico è stato ritirato l'**8 gennaio 2018**. A partire da tale data non è più possibile gestire il servizio Azure Rights Management e i modelli personalizzati dal portale classico. Se si tenta di accedere al portale classico, viene visualizzato un collegamento che consente di passare al nuovo portale di Azure.

Per altre informazioni sul ritiro del portale classico, vedere il post del blog [Marching into the future of the Azure AD admin experience: retiring the Azure classic portal](https://cloudblogs.microsoft.com/enterprisemobility/2017/09/18/marching-into-the-future-of-the-azure-ad-admin-experience-retiring-the-azure-classic-portal/) (Verso il futuro dell'amministrazione di Azure AD: ritiro del portale di Azure classico). Per l'estensione temporanea alla data di ritiro originale, vedere [Update on retirement of Azure AD classic portal experience and migration of conditional access policies](https://cloudblogs.microsoft.com/enterprisemobility/2017/11/29/update-on-retirement-of-azure-ad-classic-portal-experience-and-migration-of-conditional-access-policies/) (Aggiornamento sul ritiro dell'esperienza del portale di Azure AD classico e sulla migrazione dei criteri di accesso condizionale).

## <a name="how-to-do-your-familiar-admin-tasks"></a>Come eseguire le attività di amministrazione più comuni

Usare le informazioni seguenti per una transizione rapida al portale aggiornato.

Per gestire i modelli, i clienti con una sottoscrizione per Office 365 US Government (Government Community Cloud) non possono attualmente usare il portale di Azure e devono usare [PowerShell](configure-templates-with-powershell.md).


|Portale di Azure classico|Come eseguire questa operazione nel portale di Azure
|-----------|--------------------|
|Accedere alle impostazioni di configurazione per la prima volta|1. [Accedere al portale di Azure](configure-policy.md#signing-in-to-the-azure-portal).<br /><br />2. Nel menu hub fare clic su **Nuovo** e quindi, nell'elenco **Marketplace**, selezionare **Sicurezza e identità**.<br /><br />3. Nell'elenco **App in primo piano** del pannello **Sicurezza e identità** selezionare **Azure Information Protection**. Quindi fare clic su **Crea** nel pannello **Azure Information Protection**.<br /><br />Questa azione consente di creare il pannello **Azure Information Protection** in modo che al successivo accesso al portale sarà possibile selezionare il servizio dall'elenco **Altri servizi** dell'hub.
|Creare un nuovo modello|Creare un'etichetta che applica la protezione e usare **Impostare le autorizzazioni** per definire le autorizzazioni, la scadenza e l'accesso offline. <br /><br />Dietro le quinte, la configurazione crea un nuovo modello predefinito accessibile dai servizi e dalle applicazioni che si integrano con i modelli di Rights Management.<br /><br />Per altre informazioni, vedere [Per creare un nuovo modello](configure-policy-templates.md#to-create-a-new-template).
|Modificare le proprietà del modello: <br /><br />- Nome e descrizione del modello<br /><br />- Diritti di utilizzo, scadenza del contenuto e impostazioni di accesso offline|Se non è già stato fatto, [convertire il modello in etichetta](configure-policy-templates.md#to-convert-templates-to-labels) e quindi eseguire le operazioni seguenti<br /><br />1. Modificare il nome e la descrizione dell'etichetta<br /><br />2. Modificare le impostazioni di protezione dell'etichetta per aggiornare le autorizzazioni, la scadenza e le impostazioni dell'accesso offline.<br /><br />Per altre informazioni, vedere [Per configurare un'etichetta per la protezione di Rights Management](configure-policy-protection.md#to-configure-a-label-for-rights-management-protection).
|Archiviare un modello|Impostare lo stato dell'etichetta su **Disabilitato**.
|Creare un modello con ambito|Creare criteri con ambito e creare un'etichetta in tale ambito che applichi la protezione. <br /><br />Per altre informazioni, vedere [Come configurare i criteri di Azure Information Protection per utenti specifici con i criteri con ambito](configure-policy-scope.md).
|Copiare un modello|Non è possibile copiare un modello nel portale di Azure. Se si vuole che due etichette abbiano le stesse impostazioni di protezione, è necessario impostare le autorizzazioni in ogni etichetta. <br /><br />Per altre informazioni, vedere [Per configurare un'etichetta per la protezione di Rights Management](configure-policy-protection.md#to-configure-a-label-for-rights-management-protection).
|Eliminare un modello|L'eliminazione di modelli può comportare che alcuni dati risultino inaccessibili, pertanto il portale di Azure non supporta questa azione. Tuttavia, è possibile eliminare l'etichetta e quindi usare il cmdlet di PowerShell [Remove-AadrmTemplate](/powershell/module/aadrm/remove-aadrmtemplate) per rimuovere il modello. <br /><br />Per altre informazioni, vedere [Come eliminare o riordinare un'etichetta per Azure Information Protection](configure-policy-delete-reorder.md).
|Supporto per più lingue|Dalla selezione di menu **GESTISCI** selezionare **Lingue** per esportare i campi personalizzabili che includono il nome e la descrizione del modello. Tradurre le stringhe e importarle nel portale. <br /><br />Per altre informazioni, vedere [Come configurare etichette e modelli per varie lingue in Azure Information Protection](configure-policy-languages.md).
|Report Web di Rights Management|Usare il cmdlet di PowerShell [Get-AadrmUsageLog](/powershell/module/aadrm/Get-AadrmUsageLog) per scaricare i log di utilizzo per il servizio Azure Rights Management. È quindi possibile usare i dati per creare report personalizzati. <br /><br />Per altre informazioni, vedere [Registrazione e analisi dell'utilizzo del servizio Azure Rights Management](log-analyze-usage.md).<br /><br />Suggerimento: cercare gli annunci nel [Enterprise Mobility and Security Blog](https://cloudblogs.microsoft.com/enterprisemobility/?product=azure-information-protection) (Blog su Enterprise Mobility + Security) per una nuova soluzione di creazione di report centralizzata per Azure Information Protection.
|Attivare e disattivare il servizio Rights Management|Dalle opzioni del menu **GESTISCI** selezionare **Impostazioni di RMS** o **Protection activation** (Attivazione protezione). L'opzione verrà rinominata.<br /><br />Per altre informazioni, vedere [Come attivare Azure Rights Management dal portale di Azure](activate-azure.md).

Prima di modificare i modelli o convertirli in etichette nel portale di Azure, vedere [Considerazioni sui modelli nel portale di Azure](configure-policy-templates.md#considerations-for-templates-in-the-azure-portal).


## <a name="what-else-has-changed"></a>Altre novità

Nuove funzionalità nel portale di Azure:

- È possibile modificare i [modelli predefiniti](configure-policy-templates.md#default-templates) che vengono creati automaticamente per l'organizzazione.

- È possibile convertire i modelli in etichette, in modo da gestire un singolo oggetto anziché gestire un modello e un'etichetta separatamente. Per le istruzioni, vedere [Per convertire i modelli in etichette](configure-policy-templates.md#to-convert-templates-to-labels).

- Supporto per altri ruoli amministrativi: mentre prima, per configurare Azure Rights Management, era necessario accedere al portale di Azure classico come amministratore globale, ora è possibile accedere al portale di Azure per configurare Azure Information Protection tramite un account con uno dei ruoli amministrativi seguenti: Amministratore globale, Amministratore della sicurezza o Amministratore di Information Protection. Per altre informazioni su ciascuno di questi ruoli, vedere la sezione [Ruoli disponibili](/azure/active-directory/active-directory-assign-admin-roles-azure-portal#available-roles) della documentazione di Azure Active Directory.

Il supporto dei cmdlet di PowerShell per creare e gestire i modelli e per attivare e disattivare il servizio rimane invariato.

## <a name="see-also"></a>Vedere anche
Per altre informazioni, vedere [Configurazione e gestione dei modelli per Azure Information Protection](../deploy-use/configure-policy-templates.md).

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
