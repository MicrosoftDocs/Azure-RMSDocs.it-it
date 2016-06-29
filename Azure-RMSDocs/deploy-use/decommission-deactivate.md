---
# required metadata

title: Rimozione delle autorizzazioni e disattivazione di Azure Rights Management | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 0b1c2064-0d01-45ae-a541-cebd7fd762ad

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Rimozione delle autorizzazioni e disattivazione di Azure Rights Management

*Si applica a: Azure Rights Management, Office 365*

È sempre possibile controllare se l'organizzazione protegge il contenuto tramite [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] (Azure RMS) e, se si decide di non usare più questa soluzione di protezione delle informazioni, si può essere certi che il contenuto protetto in precedenza non verrà bloccato. Se non è necessario l'accesso continuo a contenuti protetti precedentemente, è sufficiente disattivare il servizio e lasciare scadere la sottoscrizione di Azure Rights Management. Ad esempio, questa modalità è appropriata dopo aver completato i test di [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] prima della distribuzione in un ambiente di produzione.

Tuttavia, se è stata eseguita la distribuzione di [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] nell'ambiente di produzione, assicurarsi di disporre di una copia della chiave del tenant di Azure Rights Management prima di disattivare il servizio e di eseguire questa operazione prima della scadenza della sottoscrizione, poiché in tal modo è possibile mantenere l'accesso al contenuto protetto da Azure Rights Management dopo la disattivazione del servizio. Se si utilizza la soluzione BYOK con cui si genera e gestisce la propria chiave in un modulo HSM, si dispone già della chiave tenant di Azure Rights Management. Ma se è stata gestita da Microsoft (impostazione predefinita), vedere le istruzioni per l'esportazione della chiave del tenant nell’articolo [Operazioni relative alla chiave del tenant di Azure Rights Management](operations-tenant-key.md).

> [!TIP]
> Anche dopo la scadenza della sottoscrizione, il tenant di Azure Rights Management rimane disponibile per l'utilizzo del contenuto per un periodo esteso. Tuttavia, non sarà più possibile esportare la chiave tenant.

Quando si dispone della chiave tenant di Azure Rights Management, è possibile distribuire Rights Management in locale (AD RMS) e importare la chiave tenant come un dominio di pubblicazione trusted (TPD). Quindi sono disponibili le seguenti opzioni per la rimozione delle autorizzazioni della distribuzione di Azure Rights Management:

|Se si verifica questo...|… effettuare la seguente operazione:|
|----------------------------|--------------|
|Si desidera che tutti gli utenti continuino a utilizzare Rights Management, ma che usino una soluzione locale anziché Azure RMS    →|Usare il cmdlet [Set-AadrmMigrationUrl](https://msdn.microsoft.com/library/azure/dn629429.aspx) per indirizzare gli utenti esistenti alla distribuzione locale quando utilizzano il contenuto protetto dopo questa modifica. Gli utenti utilizzeranno automaticamente l'installazione di AD RMS per utilizzare il contenuto protetto.<br /><br />Affinché gli utenti usino il contenuto protetto prima di questa modifica, reindirizzare i client alla distribuzione locale usando la chiave di registro **LicensingRedirection** per Office 2016 o Office 2013 come descritto nella [sezione sull'individuazione del servizio](../rms-client/client-deployment-notes.md) nelle note sulla distribuzione dei client di RMS e la chiave di registro **License ServerRedirection** per Office 2010 come descritto in [Impostazioni del registro di Office](https://technet.microsoft.com/library/dd772637%28v=ws.10%29.aspx).|
|Si desidera interrompere completamente l'utilizzo delle tecnologie di Rights Management    →|Concedere a un amministratore designato [diritti di utente con privilegi avanzati](../deploy-use/configure-super-users.md) e assegnare a questa persona lo [Strumento di protezione di RMS](http://www.microsoft.com/en-us/download/details.aspx?id=47256).<br /><br />L'amministratore può quindi utilizzare lo strumento per decrittografare in blocco i file nelle cartelle protette da Azure Rights Management, in modo che i file tornino allo stato non protetto e possano quindi essere letti senza una tecnologia di Rights Management, ad esempio Azure RMS o AD RMS. Questo strumento può essere utilizzato con Azure RMS e AD RMS, pertanto è possibile scegliere di decrittografare i file prima o dopo la disattivazione di Azure RMS o una combinazione.|
|Non si è in grado di identificare tutti i file che sono stati protetti da Azure RMS o si desidera che tutti gli utenti siano in grado di leggere automaticamente i file protetti che non erano disponibili    →|Distribuire un'impostazione del registro su tutti i computer client usando la chiave di registro **LicensingRedirection** per Office 2016 e Office 2013 come descritto nella [sezione sull'individuazione del servizio](../rms-client/client-deployment-notes.md) nelle note sulla distribuzione dei client di RMS e la chiave di registro **LicenseServerRedirection** per Office 2010 come descritto in [Impostazioni del registro di Office](https://technet.microsoft.com/library/dd772637%28v=ws.10%29.aspx).<br /><br />Distribuire anche un'altra impostazione del registro per impedire agli utenti di proteggere nuovi file impostando **DisableCreation** su **1** come descritto in [Impostazioni del registro di Office](https://technet.microsoft.com/library/dd772637%28v=ws.10%29.aspx).|
|Si desidera un servizio di ripristino manuale controllato per tutti i file che non erano disponibili    →|Concedere [diritti di utente con privilegi avanzati](../deploy-use/configure-super-users.md) a utenti designati in un gruppo di ripristino dei dati e fornire loro lo [Strumento di protezione di RMS](http://www.microsoft.com/en-us/download/details.aspx?id=47256) , in modo che possano rimuovere la protezione dei file quando richiesto dagli utenti standard.<br /><br />Distribuire su tutti i computer l'impostazione del registro che impedisce agli utenti di proteggere nuovi file impostando **DisableCreation** su **1** come descritto in [Impostazioni del registro di Office](https://technet.microsoft.com/library/dd772637%28v=ws.10%29.aspx).|
Per ulteriori informazioni sulle procedure in questa tabella, vedere le risorse seguenti:

-   Per informazioni su AD RMS e riferimenti sulla distribuzione, vedere [Panoramica di Active Directory Rights Management Services](https://technet.microsoft.com/library/hh831364.aspx).

-   Per istruzioni sull'importazione della chiave tenant di Azure RMS come file TPD, vedere [Aggiungere un dominio di pubblicazione trusted](https://technet.microsoft.com/library/cc771460.aspx).

-   Per installare il modulo Windows PowerShell per Azure RMS e impostare l'URL di migrazione, vedere [Installazione di Windows PowerShell per Microsoft Azure Rights Management](install-powershell.md).

Quando si è pronti per disattivare il servizio di Azure RMS dell'organizzazione, utilizzare le istruzioni seguenti.

## Disattivazione di Rights Management
Usare una delle procedure descritte di seguito per disattivare [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)].

> [!TIP]
> È anche possibile usare il cmdlet di Windows PowerShell [Disable-Aadrm](http://msdn.microsoft.com/library/windowsazure/dn629422.aspx) per disattivare [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)].

#### Per disattivare Rights Management mediante l'interfaccia di amministrazione di Office 365

1.  [Accedere a Office 365 con l'account aziendale o dell'istituto di istruzione](https://portal.office.com/) con i privilegi di amministratore per la distribuzione di Office 365.

2.  Se l'interfaccia di amministrazione di Office 365 non viene visualizzata automaticamente, selezionare l'icona di avvio delle app in alto a sinistra e scegliere **Amministratore**. Il riquadro **Amministratore** viene visualizzato solo dagli amministratori di Office 365.

    > [!TIP]
    > Per la guida dell'interfaccia di amministrazione, vedere [Informazioni sull'interfaccia di amministrazione di Office 365 - Guida per gli amministratori](https://support.office.com/article/About-the-Office-365-admin-center-Admin-Help-58537702-d421-4d02-8141-e128e3703547).

3.  Nel riquadro sinistro fare clic su **Impostazioni servizio**.

4.  Fare clic su **Rights Management**.

5.  Nella pagina **Rights Management** fare clic su **Gestione**.

6.  Nella pagina **Rights Management** fare clic su **Disattiva**.

7.  Quando viene chiesto **Si desidera disattivare Rights Management?** fare clic su **Disattiva**.

Verrà visualizzato il messaggio che indica che **Rights Management non è attivato** con l'opzione per l'attivazione.

#### Per disattivare Rights Management dal portale di Azure classico

1.  Accedere al [portale di Azure classico](http://go.microsoft.com/fwlink/p/?LinkID=275081).

2.  Nel riquadro sinistro fare clic su **Active Directory**.

3.  Nella pagina **Active Directory** fare clic su **Rights Management**.

4.  Selezionare la directory da gestire per [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)], fare clic su **DISATTIVA** e confermare l'azione.

Lo **Stato di Rights Management** dovrebbe ora essere **Inattivo** e l'opzione **Disattiva** viene sostituita da **Attiva**.





<!--HONumber=Apr16_HO4-->


