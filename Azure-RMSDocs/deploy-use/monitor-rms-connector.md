---
# required metadata

title: Monitorare il connettore di Azure Rights Management | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 06/09/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 8a1b3e54-f788-4f84-b9d7-5d5079e50b4e

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Monitorare il connettore di Azure Rights Management

*Si applica a: Azure Rights Management, Windows Server 2012, Windows Server 2012 R2*

Dopo aver installato e configurato il connettore RMS, è possibile usare i metodi e le informazioni seguenti per monitorare più facilmente il connettore e l'uso di Azure RMS nell'organizzazione.

## Voci del registro eventi dell'applicazione

Per registrare le voci relative agli eventi del **connettore di Microsoft RMS** viene usato il registro eventi dell'applicazione. 

Vengono ad esempio registrati eventi informativi per confermare l'avvio del servizio del connettore (ID 1000), per segnalare la connessione di un server al connettore RMS (ID 1002) e per informare che l'elenco dei singoli account autorizzati è stato scaricato nel connettore (ID 1004). 

Se il connettore non è stato configurato per l'uso di HTTPS, è possibile che venga visualizzato un avviso con ID 2002 per segnalare che un client sta usando una connessione non sicura (HTTP).

Se il connettore non riesce a connettersi a Azure RMS, molto probabilmente verrà restituito l'errore 3001. Ad esempio, questo errore potrebbe essere dovuto a un problema di DNS o alla mancanza di accesso a Internet per uno o più server che eseguono il connettore RMS. 

> [!TIP] I problemi di connessione dei server del connettore RMS ad Azure RMS sono spesso causati dalle configurazioni dei proxy Web.

Come per tutte le voci di registro eventi, analizzare il messaggio per ottenere informazioni più dettagliate.

Oltre a controllare il registro eventi quando si distribuisce il connettore per la prima volta, verificare regolarmente se sono presenti avvisi ed errori. È ad esempio possibile che il connettore funzioni inizialmente come previsto, ma che altri amministratori modifichino le configurazioni dipendenti. Ad esempio, un altro amministratore potrebbe modificare la configurazione del server proxy Web impedendo ai server del connettore RMS di accedere a Internet (errore 3001) o rimuovere un account di computer da un gruppo autorizzato per l'uso del connettore (avviso 2001).

## Contatori delle prestazioni

Quando si installa il connettore RMS, vengono creati automaticamente i contatori delle prestazioni del **connettore di Microsoft Rights Management**, che possono essere utili per monitorare le prestazioni relative all'uso di Azure RMS tramite il connettore. 

Se ad esempio si verificano regolarmente ritardi nella protezione di documenti o messaggi di posta elettronica o nell'apertura di documenti o messaggi di posta elettronica protetti, i contatori delle prestazioni possono aiutare a determinare se tali ritardi sono dovuti ai tempi di elaborazione sul connettore, ai tempi di elaborazione da Azure RMS o a ritardi sulla rete. Per identificare più facilmente il punto in cui si verifica il ritardo, cercare i contatori che includono i valori medi per **Connector Processing Time** (Tempo di elaborazione del connettore), **Service Response Time** (Tempo di risposta del servizio) e **Connector Response Time** (Tempo di risposta del connettore). Ad esempio: **Licensing Successful Batched Request Average Connector Response Time** (Tempo medio di risposta del connettore alle richieste di licenze in batch con esito positivo).

Se di recente sono stati aggiunti nuovi account di server per l'uso del connettore, è utile controllare il contatore **Time since last authorization policy update** (Tempo trascorso dall'ultimo aggiornamento di criteri di autorizzazione) per accertarsi che il connettore abbia scaricato l'elenco da quando è stato aggiornato o se è necessario attendere un po' più di tempo (fino a 15 minuti).

## RMS Analyzer

È possibile usare lo strumento Rights Management Services Analyzer per monitorare più facilmente lo stato del connettore e identificare eventuali problemi di configurazione.

Se non si è ancora scaricato questo strumento, è possibile eseguire questa operazione dall'[Area download](https://www.microsoft.com/en-us/download/details.aspx?id=46437) e quindi installare lo strumento in qualsiasi computer che dispone dell'accesso a Internet e che può connettersi al connettore RMS. Eseguire lo strumento e nella pagina iniziale** **selezionare l'opzione **Azure RMS connector** (Connettore Azure RMS).

Per altre informazioni e istruzioni, vedere **Details** (Dettagli) e **Install Instructions** (Istruzioni di installazione) nella pagina di download.

## Registrazione

La registrazione dei dati relativi all'utilizzo consente di identificare i casi in cui i messaggi di posta elettronica e i documenti vengono protetti e utilizzati. Quando questa operazione viene eseguita tramite il connettore RMS, il campo relativo all'ID utente nei log contiene il nome dell'entità servizio che viene generato automaticamente al momento dell'installazione del connettore RMS.

Per altre informazioni, vedere [Registrazione e analisi dell'utilizzo di Azure Rights Management](log-analyze-usage.md).

Se si vuole eseguire una registrazione più dettagliata a scopo di diagnosi, è possibile usare [Debugview](http://go.microsoft.com/fwlink/?LinkID=309277) da Windows Sysinternals e abilitare la traccia per il connettore RMS modificando il file web.config per il sito predefinito in IIS. A tale scopo, eseguire questa procedura:

1. Individuare il file web.config da **%programfiles%\Microsoft Rights Management connector\Web Service**.

2. Individuare la riga seguente:

        <trace enabled="false" requestLimit="10" pageOutput="false" traceMode="SortByTime" localOnly="true"/>

3. Sostituire la riga con il codice seguente:

        <trace enabled="true" requestLimit="10" pageOutput="false" traceMode="SortByTime" localOnly="true"/>

4.  Arrestare e riavviare IIS per attivare la traccia. 

5.  Una volta acquisite le tracce necessarie, ripristinare la riga nel passaggio 3, quindi arrestare e riavviare IIS.



<!--HONumber=Jun16_HO2-->


