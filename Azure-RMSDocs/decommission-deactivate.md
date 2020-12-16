---
title: Rimuovere le autorizzazioni e disattivare Azure RMS
description: Informazioni e istruzioni se si decide di non voler più usare il servizio di protezione basato sul cloud da Azure Information Protection.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 11/03/2019
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 0b1c2064-0d01-45ae-a541-cebd7fd762ad
ms.subservice: azurerms
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: b26e06a20e35bd56c44f4a44f0ffbc019a99865e
ms.sourcegitcommit: efeb486e49c3e370d7fd8244687cd3de77cd8462
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/16/2020
ms.locfileid: "97583524"
---
# <a name="decommissioning-and-deactivating-protection-for-azure-information-protection"></a>Rimozione delle autorizzazioni e disattivazione della protezione per Azure Information Protection

>***Si applica a**: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*
>
>***Pertinente per**: [AIP Unified Labeling client e client classico](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

È sempre possibile controllare se l'organizzazione protegge il contenuto tramite il servizio di Azure Rights Management da Azure Information Protection. Se si decide di non usare più questa soluzione di protezione delle informazioni, si è certi che il contenuto protetto in precedenza non sia bloccato.

Se non è necessario l'accesso continuo a contenuti protetti in precedenza, disattivare il servizio e lasciare scadere la sottoscrizione di Azure Information Protection. Ad esempio, è opportuno adottare questa soluzione dopo aver completato i test di Azure Information Protection prima della distribuzione in un ambiente di produzione.

Tuttavia, se sono state distribuite Azure Information Protection in produzione e documenti e messaggi di posta elettronica protetti, assicurarsi di disporre di una copia della chiave del tenant Azure Information Protection e del dominio di pubblicazione trusted appropriato prima di disattivare il servizio Azure Rights Management. Assicurarsi di disporre di una copia della chiave e del valore di pubblicazione trusted prima della scadenza della sottoscrizione per assicurarsi che sia possibile mantenere l'accesso al contenuto protetto da Azure Rights Management dopo la disattivazione del servizio. 

Se si è usata la soluzione BYOK (Bring Your Own Key) con cui si genera e gestisce la propria chiave in un modulo HSM, si dispone già della chiave del tenant di Azure Information Protection. Se sono state seguite le istruzioni [per prepararsi a una futura uscita dal cloud](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/How-to-prepare-an-Azure-Information-Protection-Cloud-Exit-plan/ba-p/382631), sarà disponibile anche un valore di pubblicazione trusted appropriato. Tuttavia, se la chiave del tenant è stata gestita da Microsoft (impostazione predefinita), vedere le istruzioni per l'esportazione della chiave del tenant nell'articolo [operazioni per la chiave del tenant Azure Information Protection](operations-tenant-key.md) .

> [!TIP]
> Anche dopo la scadenza della sottoscrizione, il tenant di Azure Information Protection rimane disponibile per l'utilizzo del contenuto per un periodo esteso. Tuttavia, non sarà più possibile esportare la chiave tenant.

Quando si dispone della chiave del tenant Azure Information Protection e del dominio di pubblicazione trusted, è possibile distribuire Rights Management locale (AD RMS) e importare la chiave del tenant come dominio di pubblicazione trusted. Sono quindi disponibili le opzioni seguenti per la rimozione delle autorizzazioni della distribuzione di Azure Information Protection:

|Se si verifica questo...|… effettuare la seguente operazione:|
|----------------------------|--------------|
|Si vuole che tutti gli utenti continuino a usare Rights Management, ma che usino una soluzione locale anziché Azure Information Protection    →|Reindirizzare i client alla distribuzione locale usando la chiave del registro di sistema **LicensingRedirection** per Office 2016 o Office 2013. Per istruzioni, vedere la [sezione sull'individuazione del servizio](./rms-client/client-deployment-notes.md) nelle note sulla distribuzione dei client RMS. <br><br>Per Office 2010, usare la chiave del registro di sistema **LicenseServerRedirection** per Office 2010, come descritto nelle [impostazioni del registro di Office](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd772637(v=ws.10)). Per ulteriori informazioni, vedere [AIP per le versioni di Windows e Office nel supporto esteso](known-issues.md#aip-for-windows-and-office-versions-in-extended-support).|
|Si desidera interrompere completamente l'utilizzo delle tecnologie di Rights Management    →|Concedere a un amministratore designato [diritti utente con privilegi avanzati](configure-super-users.md) e installare il [client Azure Information Protection](./rms-client/client-admin-guide-install.md) per questo utente.<br /><br />Questo amministratore può quindi usare il modulo PowerShell da questo client per decrittografare in blocco i file nelle cartelle protette da Azure Information Protection. I file tornano allo stato non protetto e pertanto possono essere letti senza una tecnologia di Rights Management, come ad esempio Azure Information Protection o AD RMS. Poiché questo modulo di PowerShell può essere utilizzato sia con Azure Information Protection che con AD RMS, è possibile scegliere di decrittografare i file prima o dopo la disattivazione del servizio di protezione da Azure Information Protection o da una combinazione.|
|Non è possibile identificare tutti i file protetti da Azure Information Protection. oppure si desidera che tutti gli utenti siano in grado di leggere automaticamente i file protetti che sono stati saltati    →|Distribuire un'impostazione del registro di sistema in tutti i computer client usando la chiave del registro di sistema **LicensingRedirection** per Office 2016 e Office 2013, come descritto nella [sezione sull'individuazione del servizio](./rms-client/client-deployment-notes.md) nelle note sulla distribuzione dei client RMS. <br><br>**Per Office 2010:** <br>-Usare la chiave del registro di sistema **LicenseServerRedirection** , come descritto in [impostazioni del registro di Office](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd772637(v=ws.10)). <br>-Distribuire un'altra impostazione del registro di sistema per impedire agli utenti di proteggere nuovi file impostando **DisableCreation** su **1**, come descritto nelle [impostazioni del registro di Office](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd772637(v=ws.10)). <br><br>Per ulteriori informazioni su AIP e Office 2010, vedere [AIP per le versioni di Windows e Office nel supporto esteso](known-issues.md#aip-for-windows-and-office-versions-in-extended-support).|
|Si desidera un servizio di ripristino manuale controllato per tutti i file che non erano disponibili    →|Concedere [diritti di utente con privilegi avanzati](configure-super-users.md) a utenti designati in un gruppo di ripristino dei dati e installare il [client Azure Information Protection](./rms-client/client-admin-guide-install.md) per questi utenti, in modo che possano rimuovere la protezione dei file quando richiesto dagli utenti standard.<br /><br />In tutti i computer, distribuire l'impostazione del registro di sistema per impedire agli utenti di proteggere nuovi file impostando **DisableCreation** su **1**, come descritto nelle [impostazioni del registro di Office](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd772637(v=ws.10)).|
| | |

Per ulteriori informazioni sulle procedure in questa tabella, vedere le risorse seguenti:

- Per informazioni sui riferimenti AD RMS e sulla distribuzione, vedere [Panoramica di Active Directory Rights Management Services](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831364(v=ws.11)).

- Per istruzioni sull'importazione della chiave tenant di Azure Information Protection come file TPD, vedere [Aggiungere un dominio di pubblicazione trusted](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc771460(v=ws.11)).

- Per usare PowerShell con il client Azure Information Protection, vedere [Uso di PowerShell con il client Azure Information Protection](./rms-client/client-admin-guide-powershell.md).

Quando si è pronti per disattivare il servizio di protezione da Azure Information Protection, utilizzare le istruzioni seguenti.

## <a name="deactivating-rights-management"></a>Disattivazione di Rights Management
Usare una delle procedure seguenti per disattivare il servizio di protezione, Azure Rights Management.

> [!TIP]
> È anche possibile usare il cmdlet di PowerShell, [Disable-AipService](/powershell/module/aipservice/disable-aipservice), per disattivare Rights Management.

#### <a name="to-deactivate-rights-management-from-the-microsoft-365-admin-center"></a>Per disattivare Rights Management dall'interfaccia di amministrazione di Microsoft 365

1. Passare alla [pagina Rights Management](https://account.activedirectory.windowsazure.com/RmsOnline/Manage.aspx) per Microsoft 365 Administrators.
    
    Se viene richiesto di eseguire l'accesso, usare un account che sia un amministratore globale per Microsoft 365.

2. Nella pagina **rights management** fare clic su **disattiva**.

3.  Quando viene chiesto se **si desidera disattivare Rights Management?** fare clic su **Disattiva**.

Verrà visualizzato il messaggio che indica che **Rights Management non è attivato** con l'opzione per l'attivazione.

#### <a name="to-deactivate-rights-management-from-the-azure-portal"></a>Per disattivare Rights Management dal portale di Azure

1. Aprire una nuova finestra del browser e accedere al [portale di Azure](configure-policy.md#signing-in-to-the-azure-portal), se questa operazione non è già stata eseguita. Quindi passare al riquadro **Azure Information Protection**.

    Ad esempio, nella casella di ricerca di risorse, servizi e documentazione: iniziare a digitare **Informazioni** e selezionare **Azure Information Protection**.

2. Nel riquadro **Azure Information Protection** iniziale selezionare **Protection Activation (attivazione protezione**). 

3.  Nel riquadro **attivazione protezione Azure Information Protection** selezionare **Disattiva**. Selezionare **Sì** per confermare la scelta.

Sulla barra delle informazioni verrà visualizzato **Disattivazione completata** mentre **Disattiva** è stato sostituito da **Attiva**.