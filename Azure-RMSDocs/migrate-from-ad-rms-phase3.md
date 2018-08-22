---
title: 'Eseguire la migrazione da AD RMS ad Azure Information Protection: fase 3'
description: Fase 3 della migrazione da AD RMS ad Azure Information Protection, che illustra il passaggio 7 della migrazione da AD RMS ad Azure Information Protection.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 04/11/2018
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: e3fd9bd9-3638-444a-a773-e1d5101b1793
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 07da614bf7971ee4ef89ec9ec3830be188483201
ms.sourcegitcommit: 5fdf013fe05b65517b56245e1807875d80be6e70
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2018
ms.locfileid: "39489964"
---
# <a name="migration-phase-3---client-side-configuration"></a>Fase 3 della migrazione: configurazione lato client

>*Si applica a: Active Directory Rights Management Services, [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](http://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

Usare le informazioni seguenti per la fase 3 della migrazione da AD RMS ad Azure Information Protection. Queste procedure illustrano il passaggio 7 della [Migrazione da AD RMS ad Azure Information Protection](migrate-from-ad-rms-to-azure-rms.md).

## <a name="step-7-reconfigure-windows-computers-to-use-azure-information-protection"></a>Passaggio 7. Riconfigurare i computer Windows per usare Azure Information Protection

Per i computer Windows che usano le app desktop di Office 2016 a portata di clic:

- È possibile riconfigurare questi client per l'uso di Azure Information Protection tramite il reindirizzamento DNS. Si tratta del metodo preferito per la migrazione dei client perché è il più semplice. Tuttavia, questo metodo è limitato alle app desktop di Office 2016 (o versione successiva) a portata di clic per i computer Windows.
    
    Questo metodo richiede la creazione di un nuovo record SRV e l'impostazione di un'autorizzazione Nega NTFS per gli utenti nell'endpoint di pubblicazione di AD RMS.

- Per i computer Windows che non usano Office 2016 a portata di clic:
    
    Non è possibile usare il reindirizzamento DNS ed è invece necessario apportare modifiche al Registro di sistema. Se si dispone di una combinazione di Office 2016 e altre versioni di Office, è possibile usare questo metodo per tutti i computer Windows oppure una combinazione di reindirizzamento DNS e modifica del Registro di sistema. 
    
    Per rendere più semplice apportare modifiche al Registro di sistema, è possibile modificare e distribuire script disponibili per il download. 

Per altre informazioni sulle modalità di riconfigurazione dei client Windows, vedere le sezioni seguenti.

## <a name="client-reconfiguration-by-using-dns-redirection"></a>Riconfigurazione dei client tramite il reindirizzamento DNS

Questo metodo è adatto solo per i client Windows che eseguono le app desktop di Office 2016 (o versione successiva) a portata di clic. 

1. Creare un record DNS SRV con il formato seguente:
    
    `_rmsredir._http._tcp.<AD RMS cluster>. <TTL> IN SRV <priority> <weight> <port> <your tenant URL>.`
    
    Per *\<AD RMS cluster>*, specificare il nome di dominio completo del cluster AD RMS. Ad esempio, **rmscluster.contoso.com**.
    
    In alternativa, se si dispone di un solo cluster AD RMS in tale dominio, è possibile specificare solo il nome di dominio del cluster AD RMS. In questo esempio, sarebbe **contoso.com**. Quando si specifica il nome di dominio in questo record, il reindirizzamento si applica a tutti i cluster AD RMS in tale dominio.
    
    Il numero *\<port>* viene ignorato.
    
    Per *\<your tenant URL\>*, specificare l'[URL del servizio Azure Rights Management per il tenant](migrate-from-ad-rms-phase1.md#to-identify-your-azure-rights-management-service-url).
    
    Se si usa il ruolo Server DNS in Windows Server, è possibile usare la tabella seguente come esempio per specificare le proprietà del record SRV nella console Gestore DNS.
    
    |Campo|Valore|  
    |-----------|-----------|  
    |**Dominio**|_tcp.rmscluster.contoso.com|  
    |**Servizio**|_rmsredir|  
    |**Protocollo**|_http|  
    |**Priorità**|0|  
    |**Peso**|0|  
    |**Numero porta**|80|  
    |**Host che offre questo servizio**|5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com|  

2. Impostare un'autorizzazione Nega per gli utenti di Office 2016 nell'endpoint di pubblicazione di AD RMS:

    a. In uno dei server AD RMS nel cluster avviare la console Gestione Internet Information Services (IIS).

    b. Passare a **Sito Web predefinito** > **_wmcs** > **licensing** > **licensing.asmx**

    c. Fare clic con il pulsante destro del mouse su **licensing.asmx** > **Proprietà** > **Modifica**

    d. Nella finestra di dialogo **Autorizzazioni per licensing.asmx** selezionare **Utenti** se si vuole impostare il reindirizzamento per tutti gli utenti oppure fare clic su **Aggiungi** e quindi specificare un gruppo che contiene gli utenti da reindirizzare.
    
    Anche se tutti gli utenti usano Office 2016, è preferibile specificare inizialmente un sottoinsieme di utenti per una migrazione graduale.
    
    e. Per il gruppo selezionato, selezionare **Nega** per le autorizzazioni **Lettura ed esecuzione** e **Lettura**, quindi fare clic due volte su **OK**.

    f. Per verificare che la configurazione funzioni come previsto, provare a connettersi al file licensing.asmx direttamente da un browser. Dovrebbe essere visualizzato il messaggio di errore seguente, che attiva il client che esegue Office 2016 per la ricerca del record SRV:
    
    **Error message 401.3: You do not have permissions to view this directory or page using the credentials you supplied (access denied due to Access Control Lists).** (Messaggio di errore 401.3: non si dispone delle autorizzazioni per visualizzare la directory o la pagina con le credenziali specificate (accesso negato a causa di elenchi di controllo di accesso)).


## <a name="client-reconfiguration-by-using-registry-edits"></a>Riconfigurazione di client tramite modifiche del Registro di sistema

Questo metodo è adatto per tutti i client Windows e deve essere usato se questi non eseguono Office 2016, ma una versione precedente. Questo metodo usa due script di migrazione per riconfigurare i client AD RMS:

- Migrate-Client.cmd

- Migrate-User.cmd

Lo script di configurazione client (Migrate-Client.cmd) configura le impostazioni a livello di computer nel Registro di sistema. Deve pertanto essere eseguito in un contesto di protezione che consenta di apportare modifiche di questo genere. È quindi solitamente necessario seguire questi metodi:

- Usare Criteri di gruppo per eseguire lo script come script di avvio del computer.

- Usare Criteri di gruppo Installazione software per assegnare lo script al computer.

- Usare una soluzione di distribuzione software per distribuire lo script nei computer. Usare ad esempio i [pacchetti e programmi](/sccm/apps/deploy-use/packages-and-programs) in System Center Configuration Manager. In **Modalità esecuzione** nelle proprietà del pacchetto e del programma specificare che lo script viene eseguito con autorizzazioni amministrative nel dispositivo. 

- Se l'utente dispone di privilegi di amministratore locale, usare uno script di accesso.

Lo script di configurazione utente (Migrate-User.cmd) configura le impostazioni a livello utente e pulisce l'archivio licenze client. È quindi necessario eseguire questo script nel contesto dell'utente effettivo. Ad esempio:

- Usare uno script di accesso.

- Usare Criteri di gruppo Installazione software per pubblicare lo script che l'utente deve eseguire.

- Usare una soluzione di distribuzione software per distribuire lo script agli utenti. Usare ad esempio i [pacchetti e programmi](/sccm/apps/deploy-use/packages-and-programs) in System Center Configuration Manager. In **Modalità esecuzione** nelle proprietà del pacchetto e del programma specificare che lo script viene eseguito con le autorizzazioni dell'utente. 

- Chiedere all'utente di eseguire lo script dopo aver eseguito l'accesso al computer.

I due script includono un numero di versione e non vengono rieseguiti fino a quando il numero di versione viene modificato. Ciò significa che è possibile lasciare gli script presenti fino a quando la migrazione non è stata completata. Se invece gli script vengono modificati e si vuole che i computer e gli utenti li rieseguano nei computer Windows, aggiornare la riga seguente nei due script incrementando il valore:

    SET Version=20170427

Lo script di configurazione utente è progettato per essere eseguito dopo lo script di configurazione client e usa il numero di versione specificato in questo controllo. Si interrompe se lo script di configurazione client con lo stesso numero di versione non è stato eseguito. Con questo controllo si verifica che i due script siano eseguiti nella sequenza corretta. 

Se non è possibile migrare tutti i client di Windows in una sola volta, eseguire le procedure seguenti per batch di client. Per ogni utente che ha un computer Windows per cui si vuole eseguire la migrazione in batch, aggiungere l'utente al gruppo **AIPMigrated** creato in precedenza.

### <a name="modifying-the-scripts-for-registry-edits"></a>Modificare gli script per le modifiche al Registro di sistema

1. Tornare agli script di migrazione **Migrate-Client.cmd** e **Migrate-User.cmd** che sono stati precedentemente estratti durante il download di questi script nella [fase di preparazione](migrate-from-ad-rms-phase1.md#step-2-prepare-for-client-migration).

2.  Seguire le istruzioni in **Migrate-Client.cmd** per modificare lo script in modo che contenga l'URL del servizio Azure Rights Management del tenant e i nomi server dell'URL di gestione licenze Extranet del cluster AD RMS e dell'URL di gestione licenze Intranet. A questo punto incrementare la versione dello script, come spiegato in precedenza. Per tener traccia delle versioni degli script, è consigliabile usare la data corrente nel formato seguente: AAAAMMGG
    
    > [!IMPORTANT]
    > Come in precedenza, prestare attenzione a non introdurre spazi aggiuntivi prima o dopo gli indirizzi.
    > 
    > Inoltre, se i server AD RMS usano certificati del server SSL/TLS, controllare se i valori URL di gestione licenze includono il numero di porta **443** nella stringa. Ad esempio: https://rms.treyresearch.net:443/_wmcs/licensing. È possibile accedere a queste informazioni nella console di Active Directory Rights Management Services facendo clic sul nome del cluster e visualizzando le informazioni **Dettagli cluster**. Se il numero di porta 443 è presente nell'URL, includere questo valore quando si modifica lo script. Ad esempio, https://rms.treyresearch.net:**443**. 
    
    Se è necessario recuperare l'URL del servizio Azure Rights Management per *&lt;URL tenant&gt;*, vedere nelle sezioni precedenti l'argomento [Per identificare l'URL del servizio Azure Rights Management](migrate-from-ad-rms-phase1.md#to-identify-your-azure-rights-management-service-url).

3. Seguendo le istruzioni all'inizio di questo passaggio, configurare i metodi di distribuzione script per eseguire **Migrate-Client.cmd** e **Migrate-User.cmd** nei computer client Windows che vengono usati dai membri del gruppo AIPMigrated. 

## <a name="next-steps"></a>Passaggi successivi
Per continuare la migrazione, passare a [Fase 4: configurazione di servizi di supporto](migrate-from-ad-rms-phase4.md).