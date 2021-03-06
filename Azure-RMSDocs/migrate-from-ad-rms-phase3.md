---
title: 'Eseguire la migrazione da AD RMS ad Azure Information Protection: fase 3'
description: Fase 3 della migrazione da AD RMS ad Azure Information Protection, che illustra il passaggio 7 della migrazione da AD RMS ad Azure Information Protection.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 11/11/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: e3fd9bd9-3638-444a-a773-e1d5101b1793
ms.subservice: migration
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: d0c643ea787d8ef9a977930aee270af5023c89a7
ms.sourcegitcommit: 8a141858e494dd1d3e48831e6cd5a5be48ac00d2
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2020
ms.locfileid: "97381528"
---
# <a name="migration-phase-3---client-side-configuration"></a>Fase 3 della migrazione: configurazione lato client

>***Si applica a**: Active Directory Rights Management Services, [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*
>
>***Pertinente per**: [AIP Unified Labeling client e client classico](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

Usare le informazioni seguenti per la fase 3 della migrazione da AD RMS ad Azure Information Protection. Queste procedure illustrano il passaggio 7 della [Migrazione da AD RMS ad Azure Information Protection](migrate-from-ad-rms-to-azure-rms.md).

## <a name="step-7-reconfigure-windows-computers-to-use-azure-information-protection"></a>Passaggio 7. Riconfigurare i computer Windows per usare Azure Information Protection

Riconfigurare i computer Windows per l'uso di Azure Information Protection usando uno dei metodi seguenti:

- **Reindirizzamento DNS**. Metodo più semplice e preferito, se supportato. 

    Supportato per i computer Windows che usano Office 2016 o versioni successive app desktop a esecuzione prolungata, tra cui:

    - App di Microsoft 365
    - Office 2019
    - Office 2016 fare clic per eseguire le applicazioni desktop

    È necessario creare un nuovo record SRV e impostare un'autorizzazione per negare NTFS per gli utenti nell'AD RMS endpoint di pubblicazione.

    Per ulteriori informazioni, vedere [riconfigurazione dei client tramite il reindirizzamento DNS](#client-reconfiguration-by-using-dns-redirection).

- **Modifiche al registro di sistema**. Pertinente per tutti gli ambienti supportati, inclusi i seguenti:

    - Computer Windows che usano Office 2016 o versioni successive, fare clic per eseguire app desktop, come elencato sopra
    - Computer Windows che usano altre app
    
    Apportare manualmente le modifiche necessarie al registro di sistema oppure modificare e distribuire gli script scaricabili per apportare le modifiche al registro di sistema.

    Per altre informazioni, vedere [riconfigurazione client usando le modifiche del registro di sistema](#client-reconfiguration-by-using-registry-edits).


> [!TIP]
> Se si dispone di una combinazione di versioni di Office che possono e non possono usare il reindirizzamento DNS, è possibile usare una combinazione di reindirizzamento DNS e modificare il registro di sistema oppure modificare il registro di sistema come metodo singolo per tutti i computer Windows.


## <a name="client-reconfiguration-by-using-dns-redirection"></a>Riconfigurazione dei client tramite il reindirizzamento DNS

Questo metodo è adatto solo per i client Windows che eseguono app desktop Microsoft 365 e Office 2016 (o versioni successive). 

1. Creare un record DNS SRV con il formato seguente:
    
    ```sh
    _rmsredir._http._tcp.<AD RMS cluster>. <TTL> IN SRV <priority> <weight> <port> <your tenant URL>.
    ```
    
    Per *\<AD RMS cluster>* , specificare il nome FQDN del cluster ad RMS. Ad esempio, **rmscluster.contoso.com**.
    
    In alternativa, se si dispone di un solo cluster AD RMS in tale dominio, è possibile specificare solo il nome di dominio del cluster AD RMS. In questo esempio, sarebbe **contoso.com**. Quando si specifica il nome di dominio in questo record, il reindirizzamento si applica a tutti i cluster AD RMS in tale dominio.
    
    Il *\<port>* numero viene ignorato.
    
    Per *\<your tenant URL\>* , specificare l' [URL del servizio Rights Management di Azure per il tenant](migrate-from-ad-rms-phase1.md#to-identify-your-azure-rights-management-service-url).
    
    Se si usa il ruolo Server DNS in Windows Server, è possibile usare la tabella seguente come esempio per specificare le proprietà del record SRV nella console Gestore DNS.
    
    |Campo|Valore|  
    |-----------|-----------|  
    |**Dominio**|_tcp.rmscluster.contoso.com|  
    |**Servizio**|_rmsredir|  
    |**Protocollo**|_http|  
    |**Priorità**|0|  
    |**Weight**|0|  
    |**Numero della porta**|80|  
    |**Host che offre questo servizio**|5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com|  
    | | |

2. Impostare un'autorizzazione Deny per l'endpoint di pubblicazione AD RMS per gli utenti che eseguono app Microsoft 365 o Office 2016 (o versione successiva):

    a. In uno dei server AD RMS nel cluster avviare la console Gestione Internet Information Services (IIS).

    b. Passare a **sito Web predefinito** ed espandere **_wmcs**.

    c. Fare clic con il pulsante destro del mouse su **Gestione licenze** e scegliere **passa a visualizzazione contenuto**.

    d. Nel riquadro dei dettagli fare clic con il pulsante destro del mouse su **License. asmx**  >  **proprietà**  >  **modifica**

    e. Nella finestra di dialogo **autorizzazioni per License. asmx** selezionare **utenti** se si desidera impostare il reindirizzamento per tutti gli utenti oppure fare clic su **Aggiungi** e quindi specificare un gruppo contenente gli utenti che si desidera reindirizzare.
    
    Anche se tutti gli utenti usano una versione di Office che supporta il reindirizzamento DNS, è preferibile specificare inizialmente un sottoinsieme di utenti per una migrazione graduale.
    
    f. Per il gruppo selezionato, selezionare **Nega** per le autorizzazioni **Lettura ed esecuzione** e **Lettura**, quindi fare clic due volte su **OK**.

    g. Per verificare che la configurazione funzioni come previsto, provare a connettersi al file licensing.asmx direttamente da un browser. Verrà visualizzato il messaggio di errore seguente, che attiva il client che esegue Microsoft 365 app o Office 2019 o Office 2016 per cercare il record SRV:
    
    **Error message 401.3: You do not have permissions to view this directory or page using the credentials you supplied (access denied due to Access Control Lists).** (Messaggio di errore 401.3: non si dispone delle autorizzazioni per visualizzare la directory o la pagina con le credenziali specificate (accesso negato a causa di elenchi di controllo di accesso)).


## <a name="client-reconfiguration-by-using-registry-edits"></a>Riconfigurazione di client tramite modifiche del Registro di sistema

Questo metodo è adatto per tutti i client Windows e deve essere usato se non eseguono app Microsoft 365 o Office 2016 (o versione successiva). Questo metodo usa due script di migrazione per riconfigurare i client AD RMS:

- Migrate-Client.cmd

- Migrate-User.cmd

Lo script di configurazione client (Migrate-Client.cmd) configura le impostazioni a livello di computer nel Registro di sistema. Deve pertanto essere eseguito in un contesto di protezione che consenta di apportare modifiche di questo genere. È quindi solitamente necessario seguire questi metodi:

- Usare Criteri di gruppo per eseguire lo script come script di avvio del computer.

- Usare Criteri di gruppo Installazione software per assegnare lo script al computer.

- Usare una soluzione di distribuzione software per distribuire lo script nei computer. Usare ad esempio i [pacchetti e programmi](/sccm/apps/deploy-use/packages-and-programs) in System Center Configuration Manager. In **Modalità esecuzione** nelle proprietà del pacchetto e del programma specificare che lo script viene eseguito con autorizzazioni amministrative nel dispositivo. 

- Se l'utente dispone di privilegi di amministratore locale, usare uno script di accesso.

Lo script di configurazione utente (Migrate-User.cmd) configura le impostazioni a livello utente e pulisce l'archivio licenze client. È quindi necessario eseguire questo script nel contesto dell'utente effettivo. ad esempio:

- Usare uno script di accesso.

- Usare Criteri di gruppo Installazione software per pubblicare lo script che l'utente deve eseguire.

- Usare una soluzione di distribuzione software per distribuire lo script agli utenti. Usare ad esempio i [pacchetti e programmi](/sccm/apps/deploy-use/packages-and-programs) in System Center Configuration Manager. In **Modalità esecuzione** nelle proprietà del pacchetto e del programma specificare che lo script viene eseguito con le autorizzazioni dell'utente. 

- Chiedere all'utente di eseguire lo script dopo aver eseguito l'accesso al computer.

I due script includono un numero di versione e non vengono rieseguiti fino a quando il numero di versione viene modificato. Ciò significa che è possibile lasciare gli script presenti fino a quando la migrazione non è stata completata. Se invece gli script vengono modificati e si vuole che i computer e gli utenti li rieseguano nei computer Windows, aggiornare la riga seguente nei due script incrementando il valore:

```sh
SET Version=20170427
```

Lo script di configurazione utente è progettato per essere eseguito dopo lo script di configurazione client e usa il numero di versione specificato in questo controllo. Si interrompe se lo script di configurazione client con lo stesso numero di versione non è stato eseguito. Con questo controllo si verifica che i due script siano eseguiti nella sequenza corretta. 

Se non è possibile migrare tutti i client di Windows in una sola volta, eseguire le procedure seguenti per batch di client. Per ogni utente che ha un computer Windows per cui si vuole eseguire la migrazione in batch, aggiungere l'utente al gruppo **AIPMigrated** creato in precedenza.

### <a name="modifying-the-scripts-for-registry-edits"></a>Modificare gli script per le modifiche al Registro di sistema

1. Tornare agli script di migrazione **Migrate-Client.cmd** e **Migrate-User.cmd** che sono stati precedentemente estratti durante il download di questi script nella [fase di preparazione](migrate-from-ad-rms-phase1.md#step-2-prepare-for-client-migration).

2. Seguire le istruzioni in **migrate-client. cmd** per modificare lo script in modo che contenga l'URL del servizio Rights Management di Azure del tenant, nonché i nomi dei server per l'URL di licenze Extranet del cluster ad RMS e l'URL delle licenze Intranet. A questo punto incrementare la versione dello script, come spiegato in precedenza. Per tenere traccia delle versioni degli script, è consigliabile usare la data odierna nel formato seguente: AAAAMMGG
    
   > [!IMPORTANT]
   > Come in precedenza, prestare attenzione a non introdurre spazi aggiuntivi prima o dopo gli indirizzi.
   > 
   > Inoltre, se i server AD RMS usano certificati del server SSL/TLS, controllare se i valori URL di gestione licenze includono il numero di porta **443** nella stringa. Ad esempio: https://rms.treyresearch.net:443/_wmcs/licensing. È possibile accedere a queste informazioni nella console di Active Directory Rights Management Services facendo clic sul nome del cluster e visualizzando le informazioni **Dettagli cluster**. Se il numero di porta 443 è presente nell'URL, includere questo valore quando si modifica lo script. Ad esempio, https://rms.treyresearch.net:<strong>443</strong>. 
    
   Se è necessario recuperare l'URL del servizio Rights Management di Azure per *&lt; YourTenantURL &gt;*, vedere di nuovo per [identificare l'URL del servizio Rights Management di Azure](migrate-from-ad-rms-phase1.md#to-identify-your-azure-rights-management-service-url).

3. Seguendo le istruzioni all'inizio di questo passaggio, configurare i metodi di distribuzione script per eseguire **Migrate-Client.cmd** e **Migrate-User.cmd** nei computer client Windows che vengono usati dai membri del gruppo AIPMigrated. 

## <a name="next-steps"></a>Passaggi successivi

Per continuare la migrazione, passare a [Fase 4: configurazione di servizi di supporto](migrate-from-ad-rms-phase4.md).
