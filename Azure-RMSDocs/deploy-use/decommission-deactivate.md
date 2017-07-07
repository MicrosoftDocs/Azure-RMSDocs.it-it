---
title: Rimuovere le autorizzazioni e disattivare Azure RMS
description: "Informazioni e istruzioni se si decide di non voler più usare questo servizio di protezione delle informazioni da Azure Information Protection."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 05/30/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 0b1c2064-0d01-45ae-a541-cebd7fd762ad
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 6dc6a42cf6d4a5e7a2768c927a75522a265432f7
ms.sourcegitcommit: 04eb4990e2bf0004684221592cb93df35e6acebe
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/30/2017
---
# <a name="decommissioning-and-deactivating-azure-rights-management"></a>Rimozione delle autorizzazioni e disattivazione di Azure Rights Management

>*Si applica a: Azure Information Protection, Office 365*

È sempre possibile controllare se l'organizzazione protegge il contenuto tramite il servizio Azure Rights Management di Azure Information Protection e, se si decide di non usare più questa soluzione di protezione delle informazioni, si può essere certi che il contenuto protetto in precedenza non verrà bloccato. Se non è necessario l'accesso continuo a contenuti protetti in precedenza, è sufficiente disattivare il servizio e lasciare scadere la sottoscrizione di Azure Information Protection. Ad esempio, è opportuno adottare questa soluzione dopo aver completato i test di Azure Information Protection prima della distribuzione in un ambiente di produzione.

Tuttavia, se è stata eseguita la distribuzione di Azure Information Protection nell'ambiente di produzione, verificare di avere una copia della chiave del tenant di Azure Information Protection prima di disattivare il servizio Azure Rights Management e di eseguire questa operazione prima della scadenza della sottoscrizione, poiché in tal modo è possibile mantenere l'accesso al contenuto protetto da Azure Rights Management dopo la disattivazione del servizio. Se si è usata la soluzione BYOK (Bring Your Own Key) con cui si genera e gestisce la propria chiave in un modulo HSM, si dispone già della chiave del tenant di Azure Information Protection. Ma se è stata gestita da Microsoft (impostazione predefinita), vedere le istruzioni per l'esportazione della chiave del tenant nell’articolo [Operazioni relative alla chiave del tenant di Azure Rights Management](operations-tenant-key.md).

> [!TIP]
> Anche dopo la scadenza della sottoscrizione, il tenant di Azure Information Protection rimane disponibile per l'utilizzo del contenuto per un periodo esteso. Tuttavia, non sarà più possibile esportare la chiave tenant.

Quando si dispone della chiave del tenant di Azure Information Protection, è possibile distribuire Rights Management in locale (AD RMS) e importare la chiave del tenant come dominio di pubblicazione trusted (TDP). Sono quindi disponibili le opzioni seguenti per la rimozione delle autorizzazioni della distribuzione di Azure Information Protection:

|Se si verifica questo...|… effettuare la seguente operazione:|
|----------------------------|--------------|
|Si vuole che tutti gli utenti continuino a usare Rights Management, ma che usino una soluzione locale anziché Azure Information Protection    →|Usare il cmdlet [Set-AadrmMigrationUrl](/powershell/module/aadrm/Set-AadrmMigrationUrl) per indirizzare gli utenti esistenti alla distribuzione locale quando utilizzano il contenuto protetto dopo questa modifica. Gli utenti utilizzeranno automaticamente l'installazione di AD RMS per utilizzare il contenuto protetto.<br /><br />Affinché gli utenti usino il contenuto protetto prima di questa modifica, reindirizzare i client alla distribuzione locale utilizzando la chiave di registro **LicensingRedirection** per Office 2016 oppure Office 2013, come descritto nella [sezione sull’individuazione del servizio](../rms-client/client-deployment-notes.md) nelle note sulla distribuzione dei client di RMS, e la chiave di registro **License ServerRedirection** per Office 2010, come descritto in [Impostazioni del registro di Office](https://technet.microsoft.com/library/dd772637%28v=ws.10%29.aspx).|
|Si desidera interrompere completamente l'utilizzo delle tecnologie di Rights Management    →|Concedere a un amministratore designato [diritti di utente con privilegi avanzati](../deploy-use/configure-super-users.md) e assegnare a questa persona lo [Strumento di protezione di RMS](http://www.microsoft.com/en-us/download/details.aspx?id=47256).<br /><br />L'amministratore può quindi usare lo strumento per decrittografare in blocco i file nelle cartelle protette dal servizio Azure Rights Management, in modo che i file tornino allo stato non protetto e possano quindi essere letti senza una tecnologia di Rights Management, ad esempio Azure Information Protection o AD RMS. Questo strumento può essere usato con il servizio Azure Rights Management di Azure Information Protection e con AD RMS, in modo che sia possibile scegliere di decrittografare i file prima o dopo la disattivazione del servizio Azure Rights Management, o con una combinazione dei servizi.|
|Non si è in grado di identificare tutti i file che sono stati protetti dal servizio Azure Rights Management di Azure Information Protection o si vuole che tutti gli utenti siano in grado di leggere automaticamente i file protetti che non erano disponibili    →|Distribuire un’impostazione del registro su tutti i computer client usando la chiave di registro **LicensingRedirection** per Office 2016 e Office 2013, come descritto nella [sezione sull’individuazione del servizio](../rms-client/client-deployment-notes.md) nelle note sulla distribuzione dei client di RMS, e la chiave di registro **LicenseServerRedirection** per Office 2010, come descritto in [Impostazioni del registro di Office](https://technet.microsoft.com/library/dd772637%28v=ws.10%29.aspx).<br /><br />Distribuire anche un'altra impostazione del registro per impedire agli utenti di proteggere nuovi file impostando **DisableCreation** su **1**, come descritto nelle [Impostazioni del registro di Office](https://technet.microsoft.com/library/dd772637%28v=ws.10%29.aspx).|
|Si desidera un servizio di ripristino manuale controllato per tutti i file che non erano disponibili    →|Concedere [diritti di utente con privilegi avanzati](../deploy-use/configure-super-users.md) a utenti designati in un gruppo di ripristino dei dati e fornire loro lo [Strumento di protezione di RMS](http://www.microsoft.com/en-us/download/details.aspx?id=47256) , in modo che possano rimuovere la protezione dei file quando richiesto dagli utenti standard.<br /><br />Distribuire su tutti i computer l'impostazione del registro che impedisce agli utenti di proteggere nuovi file impostando **DisableCreation** su **1**, come descritto nelle [Impostazioni del registro di Office](https://technet.microsoft.com/library/dd772637%28v=ws.10%29.aspx).|
Per ulteriori informazioni sulle procedure in questa tabella, vedere le risorse seguenti:

-   Per informazioni su AD RMS e riferimenti sulla distribuzione, vedere [Panoramica di Active Directory Rights Management Services](https://technet.microsoft.com/library/hh831364.aspx).

-   Per istruzioni sull'importazione della chiave tenant di Azure Information Protection come file TPD, vedere [Aggiungere un dominio di pubblicazione trusted](https://technet.microsoft.com/library/cc771460.aspx).

-   Per installare il modulo di Windows PowerShell per Azure Rights Management e impostare l'URL di migrazione, vedere [Installazione di Windows PowerShell per Azure Rights Management](install-powershell.md).

Quando si è pronti per disattivare il servizio Azure Rights Management dell'organizzazione, usare le istruzioni seguenti.

## <a name="deactivating-rights-management"></a>Disattivazione di Rights Management
Per disattivare [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)], usare una delle procedure descritte di seguito.

> [!TIP]
> È inoltre possibile usare il cmdlet di Windows PowerShell [Disable-Aadrm](/powershell/module/aadrm/disable-aadrm) per disattivare [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)].

#### <a name="to-deactivate-rights-management-from-the-office-365-admin-center"></a>Per disattivare Rights Management mediante l'interfaccia di amministrazione di Office 365

1. Accedere alla [pagina Rights Management](https://account.activedirectory.windowsazure.com/RmsOnline/Manage.aspx) per gli amministratori di Office 365.
    
    Se viene chiesto di effettuare l'accesso, usare un account di amministratore globale di Office 365.    

2. Nella pagina **rights management** fare clic su **disattiva**.

3.  Quando viene chiesto **Si desidera disattivare Rights Management?**fare clic su **disattiva**.

Verrà visualizzato il messaggio che indica che **Rights Management non è attivato** con l'opzione per l'attivazione.

#### <a name="to-deactivate-rights-management-from-the-azure-classic-portal"></a>Per disattivare Rights Management dal portale di Azure classico

1.  Accedere al [portale di Azure classico](http://go.microsoft.com/fwlink/p/?LinkID=275081).

2.  Nel riquadro sinistro fare clic su **ACTIVE DIRECTORY**.

3.  Nella pagina **active directory** fare clic su **RIGHTS MANAGEMENT**.

4.  Verificare che il nome del tenant sia selezionato, fare clic su **DISATTIVA** e confermare l'azione.

Lo **STATO DI RIGHTS MANAGEMENT** dovrebbe ora essere **Inattivo** e l’opzione **DISATTIVA** viene sostituita da **ATTIVA**.

[!INCLUDE[Commenting house rules](../includes/houserules.md)]


