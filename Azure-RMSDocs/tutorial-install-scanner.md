---
title: Esercitazione - Installare lo scanner di etichettatura unificata di Azure Information Protection (AIP)
description: Installare lo scanner di etichettatura unificata di Azure Information Protection (AIP) per individuare i dati sensibili archiviati nelle condivisioni di rete locali.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 11/09/2020
ms.topic: tutorial
ms.collection: M365-security-compliance
ms.service: information-protection
ms.custom: admin
ms.subservice: aiplabels
ms.openlocfilehash: 54bb64810e2dc71f6356dfe60c0443dccfb87315
ms.sourcegitcommit: e8e4ca39278f1557e14cc8586fe357d8ebce2072
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/15/2021
ms.locfileid: "98240870"
---
# <a name="tutorial-installing-the-azure-information-protection-aip-unified-labeling-scanner"></a>Esercitazione: Installazione dello scanner di etichettatura unificata di Azure Information Protection (AIP)

>***Si applica a**: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*
>
> ***Rilevante per**: [Client di etichettatura unificata di Azure Information Protection per Windows](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

Questa esercitazione descrive come installare lo scanner locale di Azure Information Protection (AIP). Lo scanner consente agli amministratori di AIP di analizzare le reti e le condivisioni di contenuto per individuare eventuali dati sensibili e di applicare le etichette di classificazione e protezione in base ai criteri dell'organizzazione configurati.

**Tempo necessario**: è possibile completare questa esercitazione in 30 minuti.

## <a name="tutorial-prerequisites"></a>Prerequisiti per l'esercitazione

Per installare lo scanner di etichettatura unificata e completare questa esercitazione, è necessario:

|Requisito  |Descrizione  |
|---------|---------|
|**Una sottoscrizione di supporto**     |  Sarà necessaria una sottoscrizione che includa [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection/). <br /><br />In assenza di una di queste sottoscrizioni, creare un account [gratuito](https://admin.microsoft.com/Signup/Signup.aspx?OfferId=87dd2714-d452-48a0-a809-d2f58c4f68b7) per l'organizzazione.       |
|**Accesso amministrativo al portale di Azure** |Assicurarsi di poter accedere al [portale di Azure](https://portal.azure.com/) con uno degli account amministratore seguenti: <br /><br />- **Amministratore di conformità**<br />- **Amministratore dati di conformità**<br />- **Amministratore della sicurezza**<br />- **Amministratore globale** |
|**Client installato**    |   Installare il client di etichettatura unificata di AIP nel computer per accedere all'installazione dello scanner. <br /><br />Scaricare ed eseguire il file **AzInfoProtection_UL.exe** dall'[Area download Microsoft](https://www.microsoft.com/download/details.aspx?id=53018). <br /><br />Al termine dell'installazione potrebbe essere richiesto di riavviare il computer o il software di Office. Riavviare come richiesto per continuare. <br /><br />Per altre informazioni, vedere [Avvio rapido: Distribuzione del client di etichettatura unificata di Azure Information Protection (AIP)](quickstart-deploy-client.md).|
|**SQL Server**     | Per eseguire lo scanner, è necessario SQL Server installato nel computer dello scanner. <br /><br /> Per eseguire l'installazione, passare alla [pagina di download di SQL Server](https://www.microsoft.com/sql-server/sql-server-downloads) e selezionare **Scarica ora** per l'opzione di installazione desiderata. Nel programma di installazione selezionare il tipo di installazione **Basic**. <br /><br />**Nota**: si consiglia di installare SQL Server Enterprise per gli ambienti di produzione ed Express solo per gli ambienti di test.       |
|**Account di Azure Active Directory**     |  Quando si lavora in un ambiente standard e connesso al cloud, l'account del servizio del dominio che si vuole usare per lo scanner deve essere sincronizzato con [Azure Active Directory](https://azure.microsoft.com/services/active-directory/). Ciò non è necessario se si lavora offline. <br /><br />In caso di dubbi per il proprio account, contattare uno degli amministratori di sistema per verificare lo stato di sincronizzazione.   |
|**Etichette di riservatezza e criteri pubblicati** |È necessario avere creato etichette di riservatezza e aver pubblicato criteri con almeno un'etichetta nell'interfaccia di amministrazione dell'etichettatura per l'account del servizio scanner. <br /><br />Configurare le etichette di riservatezza nell'interfaccia di amministrazione dell'etichettatura, ovvero il Centro conformità di Microsoft 365, il Centro sicurezza Microsoft 365 o il Centro sicurezza e conformità di Microsoft 365. Per altre informazioni, vedere la [documentazione di Microsoft 365](/microsoft-365/compliance/create-sensitivity-labels). |
| | |

Dopo aver verificato i prerequisiti, [Configurare Azure Information Protection nel portale di Azure](#configure-azure-information-protection-in-the-azure-portal).

## <a name="configure-azure-information-protection-in-the-azure-portal"></a>Configurare Azure Information Protection nel portale di Azure

Azure Information Protection potrebbe non essere disponibile nel portale di Azure oppure la protezione potrebbe non essere attualmente attivata. 

Eseguire uno o entrambi i passaggi seguenti, se necessario:

- [Aggiungere Azure Information Protection al portale di Azure](#add-azure-information-protection-to-the-azure-portal)
- [Verificare che la protezione sia attivata](#confirm-that-protection-is-activated)

Continuare quindi con [Configurare le impostazioni dello scanner iniziali nel portale di Azure](#configure-initial-scanner-settings-in-the-azure-portal).

### <a name="add-azure-information-protection-to-the-azure-portal"></a>Aggiungere Azure Information Protection al portale di Azure

1. Accedere al [portale di Azure](https://portal.azure.com) usando un [account amministratore di supporto](#tutorial-prerequisites).

1. Selezionare **+ Crea una risorsa**. Nella casella di ricerca cercare e quindi selezionare **Azure Information Protection**. Nella pagina Azure Information Protection selezionare **Crea** e quindi di nuovo **Crea**.

    :::image type="content" source="media/gifs/quickstart-add-aip-to-portal.gif" alt-text="Aggiungere Azure Information Protection al portale di Azure":::

    > [!TIP]
    > Se è la prima volta che si esegue questo passaggio, verrà visualizzata un'icona **Aggiungi al dashboard** ![icona Aggiungi al dashboard](media/qs-tutor/pin-to-dashboard.png "Icona Aggiungi al dashboard") accanto al nome del riquadro. Selezionare l'icona di aggiunta per creare un riquadro nel dashboard in modo da poter passare direttamente a questa posizione in futuro.

Continuare con [Verificare che la protezione sia attivata](#confirm-that-protection-is-activated).

### <a name="confirm-that-protection-is-activated"></a>Verificare che la protezione sia attivata

Se Azure Information Protection è già disponibile, assicurarsi che la protezione sia attivata:

1. Nell'area Azure Information Protection, in **Gestisci** a sinistra, selezionare **Attivazione della protezione**.

1. Verificare che la protezione sia attivata per il tenant. Ad esempio:

    :::image type="content" source="media/qs-tutor/confirm-activation.PNG" alt-text="Verificare l'attivazione di AIP":::

Se la protezione non è attivata, selezionare ![Attiva AIP](media/qs-tutor/activate.png "Attiva AIP") **Attiva**. Una volta completata l'attivazione, sulla barra delle informazioni verrà visualizzato il messaggio **Activation finished successfully** (Attivazione completata).

Continuare con [Configurare le impostazioni dello scanner iniziali nel portale di Azure](#configure-initial-scanner-settings-in-the-azure-portal).

### <a name="configure-initial-scanner-settings-in-the-azure-portal"></a>Configurare le impostazioni dello scanner iniziali nel portale di Azure

Preparare le impostazioni iniziali dello scanner nel portale di Azure prima di installare lo scanner nel computer.

1. Nell'area Azure Information Protection, in **Scanner** a sinistra, selezionare :::image type="icon" source="media/i-clusters.png" border="false"::: **Cluster**.

1. Nella pagina dei cluster selezionare :::image type="icon" source="media/i-add.PNG" border="false"::: **Aggiungi** per creare un nuovo cluster per gestire lo scanner.

1. Nel riquadro **Aggiungi un nuovo cluster** visualizzato a destra, immettere un nome di cluster significativo e una descrizione facoltativa.

    > [!IMPORTANT]
    > Il nome del cluster sarà necessario durante l'installazione dello scanner.
    > 
    
    Ad esempio:

    :::image type="content" source="media/qs-tutor/qs-add-new-cluster.png" alt-text="Aggiungere un nuovo cluster per l'esercitazione":::

1. Creare un processo di analisi dei contenuti iniziale. Nel menu **Scanner** a sinistra selezionare :::image type="icon" source="media/i-content-scan-jobs.png" border="false"::: **Processi di analisi dei contenuti** e quindi selezionare :::image type="icon" source="media/i-add.PNG" border="false"::: **Aggiungi**.

1. Nel riquadro **Aggiungi un nuovo processo di analisi dei contenuti** immettere un nome significativo per il processo di analisi dei contenuti e una descrizione facoltativa.

    Scorrere quindi verso il basso nella pagina fino ad **Applicazione dei criteri** e selezionare **Disattivato**.

    Al termine, salvare le modifiche. 

    Questo processo di analisi predefinito eseguirà un'analisi per individuare tutti i tipi di informazioni sensibili noti.

1. Chiudere il riquadro dei dettagli per il processo di analisi dei contenuti e tornare alla griglia :::image type="icon" source="media/i-content-scan-jobs.png" border="false"::: **Processi di analisi dei contenuti**. 

    Nella colonna **Nome cluster** nella nuova riga visualizzata per il processo di analisi dei contenuti selezionare **+Assegna al cluster**. Selezionare quindi il cluster nel riquadro **Assegna al cluster** visualizzato a destra. 

    :::image type="content" source="media/qs-tutor/assign-cluster-all.png" alt-text="Assegna al cluster":::

A questo punto si è pronti per [Installare lo scanner di etichettatura unificata di AIP](#install-the-aip-unified-labeling-scanner).

## <a name="install-the-aip-unified-labeling-scanner"></a>Installare lo scanner di etichettatura unificata di AIP

Dopo aver [configurato le impostazioni di base dello scanner nel portale di Azure](#configure-azure-information-protection-in-the-azure-portal), installare lo scanner di etichettatura unificata nel computer client di AIP.

1. Nel computer client aprire una sessione di PowerShell con l'opzione **Esegui come amministratore**.

1. Usare il comando seguente per installare lo scanner. Nel comando specificare il percorso in cui si vuole installare lo scanner e il nome del [cluster creato nel portale di Azure](#configure-initial-scanner-settings-in-the-azure-portal).

    ```PowerShell
    Install-AIPScanner -SqlServerInstance <your SQL installation location>\SQLEXPRESS -Cluster <cluster name>
    ```
    Ad esempio:

    ```powershell
    Install-AIPScanner -SqlServerInstance localhost\SQLEXPRESS -Cluster Quickstart
    ```

    Quando PowerShell richiede le credenziali, immettere il nome utente e la password. 

    Per il campo **Nome utente** usare la sintassi seguente: `<domain\user name>`. Ad esempio: `emea\contososcanner`.

1. Tornare al portale di Azure. Nel menu **Scanner** a sinistra selezionare :::image type="icon" source="media/qs-tutor/i-nodes.png" border="false"::: **Nodi**. 

    A questo punto lo scanner dovrebbe essere aggiunto alla griglia. Ad esempio:

    :::image type="content" source="media/qs-tutor/qs-post-install-scanner.png" alt-text="Scanner appena installato visualizzato nella griglia Nodi":::

Continuare con [Ottenere un token di Azure Active Directory per lo scanner](#get-an-azure-active-directory-token-for-the-scanner) per abilitare l'esecuzione non interattiva dell'account del servizio scanner.

## <a name="get-an-azure-active-directory-token-for-the-scanner"></a>Ottenere un token di Azure Active Directory per lo scanner

Eseguire questa procedura quando si lavora in un ambiente standard connesso al cloud, per consentire allo scanner di eseguire l'autenticazione per il servizio AIP, abilitando l'esecuzione non interattiva del servizio.

Questa procedura non è necessaria se si lavora solo offline.

Per altre informazioni, vedere [Come assegnare un'etichetta ai file in modo non interattivo per Azure Information Protection](rms-client/clientv2-admin-guide-powershell.md#how-to-label-files-non-interactively-for-azure-information-protection).

**Per ottenere un token di Azure AD per lo scanner**:

1. Nel portale di Azure creare un'applicazione di Azure AD per specificare un token di accesso per l'autenticazione.

1. Nel computer dello scanner accedere con un account del servizio scanner a cui è stato concesso il diritto **Accesso locale** e avviare una sessione di PowerShell.

1. Avviare una sessione di PowerShell ed eseguire il comando seguente, usando i valori copiati dall'applicazione di Azure AD.

    ```PowerShell
    Set-AIPAuthentication -AppId <ID of the registered app> -AppSecret <client secret sting> -TenantId <your tenant ID> -DelegatedUser <Azure AD account>
    ```

    Ad esempio:

    ```PowerShell
    $pscreds = Get-Credential CONTOSO\scanner
    Set-AIPAuthentication -AppId "77c3c1c3-abf9-404e-8b2b-4652836c8c66" -AppSecret "OAkk+rnuYc/u+]ah2kNxVbtrDGbS47L4" -DelegatedUser scanner@contoso.com -TenantId "9c11c87a-ac8b-46a3-8d5c-f4d0b72ee29a" -OnBehalfOf $pscreds

    Acquired application access token on behalf of CONTOSO\scanner.
    ``` 

    > [!TIP]
    > Se non è possibile concedere il diritto di **accesso locale** per l'installazione all'account del servizio scanner, usare il parametro **OnBehalfOf** con **Set-AIPAuthentication** invece del parametro **DelegatedUser**.

Lo scanner dispone ora di un token per l'autenticazione in Azure AD. Questo token è valido per il tempo configurato in Azure Active Directory. È necessario ripetere questa procedura alla scadenza del token.

Continuare con l'[installazione del servizio di individuazione della rete facoltativo](#install-the-network-discovery-service), che consente di analizzare i repository di rete per individuare l'eventuale contenuto a rischio e quindi aggiungere tali repository a un processo di analisi dei contenuti.

## <a name="install-the-network-discovery-service"></a>Installare il servizio di individuazione della rete

A partire dalla versione [2.8.85.0](rms-client/unifiedlabelingclient-version-release-history.md#version-28850) del client di etichettatura unificata di AIP, gli amministratori possono usare lo scanner di AIP per analizzare i repository di rete e quindi aggiungere tutti i repository che risultano rischiosi a un processo di analisi dei contenuti.

I processi di analisi della rete consentono di comprendere *dove* il contenuto potrebbe essere a rischio, tentando di accedere ai repository configurati sia come amministratore che come utente pubblico.

Ad esempio, se si trova un repository con accesso pubblico sia in lettura che in scrittura, è possibile eseguire un'analisi più approfondita e verificare che in tale posizione non siano archiviati dati sensibili.

> [!NOTE]
> Questa funzionalità è attualmente disponibile in ANTEPRIMA. Le [condizioni aggiuntive per l'anteprima di Azure](https://azure.microsoft.com/support/legal/preview-supplemental-terms/) includono termini legali aggiuntivi che si applicano a funzionalità di Azure in versione beta, anteprima o diversamente non ancora disponibili a livello generale.

**Per installare il servizio di individuazione della rete**:

1. Nel computer dello scanner aprire una sessione di PowerShell come amministratore.

1. Definire le credenziali da usare con AIP per l'esecuzione del servizio di individuazione della rete, nonché per la simulazione dell'accesso come amministratore e come utente pubblico. 

    Quando viene richiesto, immettere le credenziali per ogni comando usando la sintassi seguente: `domain\user`. ad esempio `emea\msanchez`

    Eseguire: 

    **Credenziali per eseguire il servizio di individuazione della rete**:

    ``` PowerShell 
    $serviceacct= Get-Credential 
    ``` 

    **Credenziali per simulare l'accesso come amministratore**:

    ``` PowerShell 
    $shareadminacct= Get-Credential 
    ``` 

    **Credenziali per simulare l'accesso come utente pubblico**:

    ``` PowerShell  
    $publicaccount= Get-Credential 
    ``` 

1. Per installare il servizio di individuazione della rete, eseguire:

    ```PowerShell
    Install-MIPNetworkDiscovery [-ServiceUserCredentials] <PSCredential> [[-StandardDomainsUserAccount] <PSCredential>] [[-ShareAdminUserAccount] <PSCredential>] [-SqlServerInstance] <String> -Cluster <String> [-WhatIf] [-Confirm] [<CommonParameters>]

    For example:

    ```PowerShell
    Install-MIPNetworkDiscovery -SqlServerInstance SQLSERVER1\SQLEXPRESS -Cluster Quickstart -ServiceUserCredentials $serviceacct  -ShareAdminUserAccount $shareadminacct -StandardDomainsUserAccount $publicaccount
 
    ```

Il sistema visualizza un messaggio di conferma al termine dell'installazione.

## <a name="next-steps"></a>Passaggi successivi

Dopo aver installato lo scanner e il servizio di individuazione della rete, è possibile iniziare l'analisi. 

Per altre informazioni, vedere [Esercitazione: Individuazione del contenuto sensibile con lo scanner di Azure Information Protection (AIP)](tutorial-scan-networks-and-content.md).

> [!TIP]
> Se è stata installata la [versione 2.8.85.0](rms-client/unifiedlabelingclient-version-release-history.md#version-28850), è consigliabile eseguire l'analisi della rete per individuare i repository che potrebbero includere contenuto rischioso. 
>
>Per analizzare i repository rischiosi per individuare eventuali dati sensibili e quindi classificare e proteggere i dati dagli utenti esterni, aggiornare il processo di analisi dei contenuti con i dettagli dei repository trovati.
>

**Vedere anche**:

- [Informazioni sullo scanner di etichettatura unificata di Azure Information Protection](deploy-aip-scanner.md)
- [Prerequisiti per l'installazione e la distribuzione dello scanner di etichettatura unificata di Azure Information Protection](deploy-aip-scanner-prereqs.md)
- [Esercitazione: Prevenzione dell'oversharing con Azure Information Protection (AIP)](tutorial-preventing-oversharing.md)
- [Esercitazione: Migrazione dal client classico al client di etichettatura unificata di Azure Information Protection (AIP)](tutorial-migrating-to-ul.md)