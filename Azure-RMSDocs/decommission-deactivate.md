---
title: Rimuovere le autorizzazioni e disattivare Azure RMS
description: Informazioni e istruzioni se si decide di non voler più usare il servizio di protezione basato sul cloud da Azure Information Protection.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/20/2018
ms.topic: conceptual
ms.service: information-protection
ms.assetid: 0b1c2064-0d01-45ae-a541-cebd7fd762ad
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 9a990e9f93c59e4ad40cea503efde70e0aed46e7
ms.sourcegitcommit: 26a2c1becdf3e3145dc1168f5ea8492f2e1ff2f3
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/07/2018
ms.locfileid: "44148087"
---
# <a name="decommissioning-and-deactivating-protection-for-azure-information-protection"></a>Rimozione delle autorizzazioni e disattivazione della protezione per Azure Information Protection

>*Si applica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](http://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

È sempre possibile controllare se l'organizzazione protegge il contenuto tramite il servizio di Azure Rights Management da Azure Information Protection. Se si decide di non usare più questa soluzione di protezione delle informazioni, si è certi che il contenuto protetto in precedenza non sia bloccato.

Se non è necessario l'accesso continuo a contenuti protetti in precedenza, disattivare il servizio e lasciare scadere la sottoscrizione di Azure Information Protection. Ad esempio, è opportuno adottare questa soluzione dopo aver completato i test di Azure Information Protection prima della distribuzione in un ambiente di produzione.

Tuttavia, se Azure Information Protection è stato implementato nell'ambiente di produzione e nei documenti e messaggi di posta elettronica protetti, assicurarsi di disporre di una copia della chiave del tenant di Azure Information Protection prima di disattivare il servizio Azure Rights Management. Assicurarsi di disporre di una copia della chiave prima della scadenza della sottoscrizione per assicurarsi che sia possibile mantenere l'accesso al contenuto protetto da Azure Rights Management dopo la disattivazione del servizio. Se si è usata la soluzione BYOK (Bring Your Own Key) con cui si genera e gestisce la propria chiave in un modulo HSM, si dispone già della chiave del tenant di Azure Information Protection. Ma se è stata gestita da Microsoft (impostazione predefinita), vedere le istruzioni per l'esportazione della chiave del tenant nell'articolo [Operazioni relative alla chiave del tenant di Azure Information Protection](operations-tenant-key.md).

> [!TIP]
> Anche dopo la scadenza della sottoscrizione, il tenant di Azure Information Protection rimane disponibile per l'utilizzo del contenuto per un periodo esteso. Tuttavia, non sarà più possibile esportare la chiave tenant.

Quando si dispone della chiave del tenant di Azure Information Protection, è possibile distribuire Rights Management in locale (AD RMS) e importare la chiave del tenant come dominio di pubblicazione trusted (TDP). Sono quindi disponibili le opzioni seguenti per la rimozione delle autorizzazioni della distribuzione di Azure Information Protection:

|Se si verifica questo...|… effettuare la seguente operazione:|
|----------------------------|--------------|
|Si vuole che tutti gli utenti continuino a usare Rights Management, ma che usino una soluzione locale anziché Azure Information Protection    →|Usare il cmdlet [Set-AadrmMigrationUrl](/powershell/module/aadrm/Set-AadrmMigrationUrl) per indirizzare gli utenti esistenti alla distribuzione locale quando utilizzano il contenuto protetto dopo questa modifica. Gli utenti utilizzeranno automaticamente l'installazione di AD RMS per utilizzare il contenuto protetto.<br /><br />Perché gli utenti possano usare il contenuto protetto prima di questa modifica, reindirizzare i client alla distribuzione locale tramite la chiave del Registro di sistema **LicensingRedirection** per Office 2016 o Office 2013. Per istruzioni, vedere la [sezione sull'individuazione dei servizi](./rms-client/client-deployment-notes.md) nelle note sulla distribuzione dei client di RMS e la chiave del Registro di sistema **LicenseServerRedirection** per Office 2010, come descritto nelle [impostazioni del Registro di Office](https://technet.microsoft.com/library/dd772637%28v=ws.10%29.aspx).|
|Si desidera interrompere completamente l'utilizzo delle tecnologie di Rights Management    →|Concedere a un amministratore designato [diritti utente con privilegi avanzati](configure-super-users.md) e installare il [client Azure Information Protection](./rms-client/client-admin-guide-install.md) per questo utente.<br /><br />L'amministratore può quindi usare il modulo di PowerShell da questo client per decrittografare i file in blocco nelle cartelle protette dal servizio Azure Rights Management. I file tornano allo stato non protetto e pertanto possono essere letti senza una tecnologia di Rights Management, come ad esempio Azure Information Protection o AD RMS. Poiché questo modulo di PowerShell può essere usato con il servizio Azure Rights Management sia da Azure Information Protection che da AD RMS, è possibile scegliere di decrittografare i file prima o dopo la disattivazione del servizio Azure Rights Management, o con una combinazione.|
|Non è possibile identificare tutti i file che erano protetti dal servizio Azure Rights Management da Azure Information Protection, oppure si desidera che tutti gli utenti siano in grado di leggere automaticamente i file protetti che sono stati saltati    →|Distribuire un’impostazione del registro su tutti i computer client usando la chiave di registro **LicensingRedirection** per Office 2016 e Office 2013, come descritto nella [sezione sull’individuazione del servizio](./rms-client/client-deployment-notes.md) nelle note sulla distribuzione dei client di RMS, e la chiave di registro **LicenseServerRedirection** per Office 2010, come descritto in [Impostazioni del registro di Office](https://technet.microsoft.com/library/dd772637%28v=ws.10%29.aspx).<br /><br />Distribuire anche un'altra impostazione del registro per impedire agli utenti di proteggere nuovi file impostando **DisableCreation** su **1**, come descritto nelle [Impostazioni del registro di Office](https://technet.microsoft.com/library/dd772637%28v=ws.10%29.aspx).|
|Si desidera un servizio di ripristino manuale controllato per tutti i file che non erano disponibili    →|Concedere [diritti di utente con privilegi avanzati](configure-super-users.md) a utenti designati in un gruppo di ripristino dei dati e installare il [client Azure Information Protection](./rms-client/client-admin-guide-install.md) per questi utenti, in modo che possano rimuovere la protezione dei file quando richiesto dagli utenti standard.<br /><br />Distribuire su tutti i computer l'impostazione del registro che impedisce agli utenti di proteggere nuovi file impostando **DisableCreation** su **1**, come descritto nelle [Impostazioni del registro di Office](https://technet.microsoft.com/library/dd772637%28v=ws.10%29.aspx).|
Per ulteriori informazioni sulle procedure in questa tabella, vedere le risorse seguenti:

- Per informazioni su AD RMS e riferimenti sulla distribuzione, vedere [Panoramica di Active Directory Rights Management Services](https://technet.microsoft.com/library/hh831364.aspx).

- Per istruzioni sull'importazione della chiave tenant di Azure Information Protection come file TPD, vedere [Aggiungere un dominio di pubblicazione trusted](https://technet.microsoft.com/library/cc771460.aspx).

- Per installare il modulo Windows PowerShell per Azure Rights Management e impostare l'URL di migrazione, vedere [Installazione del modulo PowerShell AADRM](install-powershell.md).

- Per usare PowerShell con il client Azure Information Protection, vedere [Uso di PowerShell con il client Azure Information Protection](./rms-client/client-admin-guide-powershell.md).

Quando si è pronti per disattivare il servizio Azure Rights Management dell'organizzazione, usare le istruzioni seguenti.

## <a name="deactivating-rights-management"></a>Disattivazione di Rights Management
Per disattivare Azure Rights Management, usare una delle procedure descritte di seguito.

> [!TIP]
> È anche possibile usare il cmdlet di Windows PowerShell [Disable-Aadrm](/powershell/module/aadrm/disable-aadrm) per disattivare Rights Management.

#### <a name="to-deactivate-rights-management-from-the-office-365-admin-center"></a>Per disattivare Rights Management mediante l'interfaccia di amministrazione di Office 365

1. Accedere alla [pagina Rights Management](https://account.activedirectory.windowsazure.com/RmsOnline/Manage.aspx) per gli amministratori di Office 365.
    
    Se viene chiesto di effettuare l'accesso, usare un account di amministratore globale di Office 365.    

2. Nella pagina **rights management** fare clic su **disattiva**.

3.  Quando viene chiesto **Si desidera disattivare Rights Management?** fare clic su **Disattiva**.

Verrà visualizzato il messaggio che indica che **Rights Management non è attivato** con l'opzione per l'attivazione.

#### <a name="to-deactivate-rights-management-from-the-azure-portal"></a>Per disattivare Rights Management dal portale di Azure

1. Se non è già stato fatto, aprire una nuova finestra del browser e [accedere al portale di Azure](configure-policy.md#signing-in-to-the-azure-portal). Quindi passare al pannello **Azure Information Protection**.
    
    Ad esempio, dal menu hub fare clic su **Tutti i servizi** e iniziare a digitare **Informazioni** nella casella Filtro. Selezionare **Azure Information Protection**.

2. Nel pannello iniziale di **Azure Information Protection** selezionare **Protection activation** (Attivazione protezione). 

3.  Nel pannello **Azure Information Protection - Protection activation** (Azure Information Protection - Attivazione protezione) selezionare **Disattiva**. Selezionare **Sì** per confermare la scelta.

Sulla barra delle informazioni verrà visualizzato **Disattivazione completata** mentre **Disattiva** è stato sostituito da **Attiva**. 




