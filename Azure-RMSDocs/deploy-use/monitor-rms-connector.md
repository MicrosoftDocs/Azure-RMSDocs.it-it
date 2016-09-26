---
title: Monitorare il connettore di Azure Rights Management | Azure RMS
description: Informazioni che consentono di monitorare il connettore e l'uso di Azure RMS da parte dell'organizzazione.
author: cabailey
manager: mbaldwin
ms.date: 08/25/2016
ms.topic: article
ms.prod: 
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 8a1b3e54-f788-4f84-b9d7-5d5079e50b4e
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: ad32910b482ca9d92b4ac8f3f123eda195db29cd
ms.openlocfilehash: 97b8107e1529271376c21837b3ac357dba9235d2


---

# Monitorare il connettore di Azure Rights Management

>*Si applica a: Azure Rights Management, Windows Server 2012, Windows Server 2012 R2*

Dopo aver installato e configurato il connettore RMS, è possibile usare i metodi e le informazioni seguenti per monitorare più facilmente il connettore e l'uso di Azure RMS nell'organizzazione.

## Voci del registro eventi dell'applicazione

Per registrare le voci relative agli eventi del **connettore di Microsoft RMS** viene usato il registro eventi dell'applicazione. 

Vengono ad esempio registrati eventi informativi per confermare l'avvio del servizio del connettore (ID 1000), per segnalare la connessione di un server al connettore RMS (ID 1002) e per informare che l'elenco dei singoli account autorizzati è stato scaricato nel connettore (ID 1004). 

Se il connettore non è stato configurato per l'uso di HTTPS, è possibile che venga visualizzato un avviso con ID 2002 per segnalare che un client sta usando una connessione non sicura (HTTP).

Se il connettore non riesce a connettersi a Azure RMS, molto probabilmente verrà restituito l'errore 3001. Ad esempio, questo errore potrebbe essere dovuto a un problema di DNS o alla mancanza di accesso a Internet per uno o più server che eseguono il connettore RMS. 

> [!TIP]
> I problemi di connessione dei server del connettore RMS ad Azure RMS sono spesso causati dalle configurazioni dei proxy Web.

Come per tutte le voci di registro eventi, analizzare il messaggio per ottenere informazioni più dettagliate.

Oltre a controllare il registro eventi quando si distribuisce il connettore per la prima volta, verificare regolarmente se sono presenti avvisi ed errori. È ad esempio possibile che il connettore funzioni inizialmente come previsto, ma che altri amministratori modifichino le configurazioni dipendenti. Ad esempio, un altro amministratore potrebbe modificare la configurazione del server proxy Web impedendo ai server del connettore RMS di accedere a Internet (errore 3001) o rimuovere un account di computer da un gruppo autorizzato per l'uso del connettore (avviso 2001).

### ID registro eventi e descrizioni

Usare le sezioni seguenti per identificare gli ID evento, le descrizioni e le informazioni aggiuntive possibili.

-----

Informazione **1000**

**Il servizio Web del connettore Microsoft RMS è stato avviato.**

L'evento viene registrato quando il connettore RMS tenta di avviarsi per la prima volta.

----

Informazione **1001**

**Il servizio Web del connettore Microsoft RMS è stato arrestato.**

L'evento viene registrato quando il connettore RMS si arresta in conseguenza di una normale operazione. Ad esempio, viene riavviato IIS o il computer è stato arrestato. 

----

Informazione **1002**

**Accesso al connettore Microsoft RMS consentito per un server autorizzato.**

Questo evento viene registrato quando un account da un server locale si connette per la prima volta al connettore RMS, dopo che l'account è stato autorizzato dall'amministratore di Azure RMS nello strumento di amministrazione del connettore RMS. Il SID, il nome dell'account e il nome del computer che esegue la connessione sono contenuti nel messaggio di evento.

----

Informazione **1003**

**Per la connessione dal client elencata di seguito è stato effettuato il passaggio da una connessione HTTP non protetta a una HTTPS protetta.**

Questo evento viene registrato quando un server locale modifica la connessione al connettore RMS da HTTP (meno sicura) a HTTPS (più sicura). Il SID, il nome dell'account e il nome del computer che esegue la connessione sono contenuti nel messaggio di evento.

----

Informazione **1004**

**L'elenco degli account autorizzati è stato aggiornato.**

Questo evento viene registrato quando il connettore RMS ha scaricato un elenco aggiornato di account (account esistenti e le eventuali modifiche) autorizzati a usare il connettore RMS. Questo elenco viene scaricato ogni 15 minuti, purché il connettore RMS riesca a comunicare con Azure RMS.

----

Avviso **2000**

**L'entità utente nel contesto HTTP risulta mancante o non valida. Verificare che l'autenticazione anonima sia disabilitata in IIS per il sito Web del connettore Microsoft RMS e che sia abilitata solo l'autenticazione di Windows.**

Questo evento viene registrato quando il connettore RMS non riesce a identificare in modo univoco l'account che sta tentando di connettersi al connettore RMS. Ciò può verificarsi quando l'autenticazione anonima non è configurata correttamente per IIS o quando l'account proviene da una foresta non attendibile.

----

Avviso **2001**

**Tentativo di accesso non autorizzato al connettore Microsoft RMS.**

Questo evento viene registrato quando un account tenta di connettersi al connettore RMS ma il tentativo ha esito negativo. Il motivo più comune è che l'account che effettua la connessione non è presente nell'elenco di account autorizzati che il connettore RMS scarica da Azure RMS. Ad esempio, l'elenco più recente non è ancora stato scaricato (l'operazione avviene ogni 15 minuti) o l'account non è presente nell'elenco. 

Un altro motivo può essere che il connettore RMS è stato installato nello stesso server che è configurato per usare il connettore. Ad esempio, si installa il connettore RMS in un server che esegue Exchange Server e si autorizza un account di Exchange a usare il connettore. Questa configurazione non è supportata perché il connettore RMS non può identificare correttamente l'account quando questo tenta di connettersi.

Il messaggio di evento contiene informazioni sull'account e sul computer che tenta di connettersi al connettore RMS:

- Se l'account che tenta di connettersi al connettore RMS è un account valido, usare lo strumento di amministrazione del connettore RMS per aggiungere l'account all'elenco di account autorizzati. Per altre informazioni su quali account devono essere autorizzati, vedere [Aggiunta di un server all'elenco dei server autorizzati](install-configure-rms-connector.md#add-a-server-to-the-list-of-allowed-servers). 

- Se l'account che tenta di connettersi al connettore RMS è dello stesso computer che esegue il server del connettore RMS, installare il connettore in un server separato. Per altre informazioni sui prerequisiti per il connettore, vedere [Prerequisiti per l'installazione del connettore RMS]( deploy-rms-connector.md#prerequisites-for-the-rms-connector).

----

Avviso **2002**

**Per la connessione dal client elencata di seguito viene utilizzata una connessione (HTTP) non protetta.**

Questo evento viene registrato quando un server locale stabilisce una connessione con esito positivo al connettore RMS, ma la connessione usa un protocollo HTTP (meno sicuro) anziché HTTPS (più sicuro). Viene registrato un evento per ogni account anziché per ogni connessione. Questo evento viene generato nuovamente se l'account passa al protocollo HTTPS ma in seguito ripristina il protocollo HTTP.

Il messaggio di evento contiene il SID dell'account, il nome dell'account e il nome del computer che esegue la connessione al connettore RMS.

Per informazioni su come configurare il connettore RMS per le connessioni HTTPS, vedere [Configurazione del connettore RMS per l'uso di HTTPS](install-configure-rms-connector.md#configuring-the-rms-connector-to-use-https).

----

Avviso **2003**

**L'elenco delle autorizzazioni è vuoto. Non sarà possibile utilizzare il servizio finché non viene popolato l'elenco di utenti e gruppi autorizzati per il connettore.**

Questo evento viene registrato quando il connettore RMS non ha un elenco di account autorizzati, quindi nessun server locale può connettersi ad esso. Il connettore RMS scarica l'elenco ogni 15 minuti da Azure RMS. 

Per specificare gli account, usare lo strumento di amministrazione del connettore RMS. Per altre informazioni, vedere [Autorizzazione dei server all'uso del connettore RMS]( install-configure-rms-connector.md#authorizing-servers-to-use-the-rms-connector). 

----

Errore **3000**

**Si è verificata un'eccezione non gestita nel connettore RMS Microsoft.**

Questo evento viene registrato ogni volta che il connettore RMS rileva un errore imprevisto, con i dettagli dell'errore nel messaggio di evento.

Una causa possibile può essere identificata dal testo **Richiesta non riuscita con risposta vuota** nel messaggio relativo all'evento. Se viene visualizzato questo testo, è possibile che sia presente un dispositivo di rete che esegue l'ispezione SSL sui pacchetti tra i server locali e il server del connettore RMS. Questa configurazione non è supportata e genererà errori di comunicazione e questo messaggio nel registro eventi.

----

Errore **3001**

**Si è verificata un'eccezione durante il download delle informazioni sulle autorizzazioni.**

Questo evento viene registrato se il connettore RMS non scarica l'elenco più recente degli account autorizzati a usare il connettore RMS, con i dettagli dell'errore nel messaggio di evento.



----

## Contatori delle prestazioni

Quando si installa il connettore RMS, vengono creati automaticamente i contatori delle prestazioni del **connettore di Microsoft Rights Management**, che possono essere utili per monitorare le prestazioni relative all'uso di Azure RMS tramite il connettore. 

Se ad esempio si verificano regolarmente ritardi nella protezione di documenti o messaggi di posta elettronica o nell'apertura di documenti o messaggi di posta elettronica protetti, i contatori delle prestazioni possono aiutare a determinare se tali ritardi sono dovuti ai tempi di elaborazione sul connettore, ai tempi di elaborazione da Azure RMS o a ritardi sulla rete. Per identificare più facilmente il punto in cui si verifica il ritardo, cercare i contatori che includono i valori medi per **Connector Processing Time** (Tempo di elaborazione del connettore), **Service Response Time** (Tempo di risposta del servizio) e **Connector Response Time** (Tempo di risposta del connettore). Ad esempio: **Licensing Successful Batched Request Average Connector Response Time** (Tempo medio di risposta del connettore alle richieste di licenze in batch con esito positivo).

Se di recente sono stati aggiunti nuovi account di server per l'uso del connettore, è utile controllare il contatore **Time since last authorization policy update** (Tempo trascorso dall'ultimo aggiornamento di criteri di autorizzazione) per accertarsi che il connettore abbia scaricato l'elenco da quando è stato aggiornato o se è necessario attendere un po' più di tempo (fino a 15 minuti).

## RMS Analyzer

È possibile usare lo strumento Rights Management Services Analyzer per monitorare più facilmente lo stato del connettore e identificare eventuali problemi di configurazione.

Se non si è ancora scaricato questo strumento, è possibile eseguire questa operazione dall'[Area download](https://www.microsoft.com/en-us/download/details.aspx?id=46437) e quindi installare lo strumento in qualsiasi computer che dispone dell'accesso a Internet e che può connettersi al connettore RMS. Eseguire lo strumento e nella pagina iniziale** **selezionare l'opzione **Azure RMS connector** (Connettore Azure RMS).

Per altre informazioni e istruzioni, vedere **Details** (Dettagli) e **Install Instructions** (Istruzioni di installazione) nella pagina di download.

## Registrazione

La registrazione dei dati relativi all'utilizzo consente di identificare i casi in cui i messaggi di posta elettronica e i documenti vengono protetti e utilizzati. Quando questa operazione viene eseguita tramite il connettore RMS, il campo relativo all'ID utente nei log contiene il nome dell'entità servizio **Aadrm_S-1-7-0** che viene generato automaticamente per il connettore RMS.

Per altre informazioni sulla registrazione dei dati sull'uso, vedere [Registrazione e analisi dell'uso di Azure Rights Management](log-analyze-usage.md).

Se si vuole eseguire una registrazione più dettagliata a scopo di diagnosi, è possibile usare [Debugview](http://go.microsoft.com/fwlink/?LinkID=309277) da Windows Sysinternals e abilitare la traccia per il connettore RMS modificando il file web.config per il sito predefinito in IIS. A tale scopo, eseguire questa procedura:

1. Individuare il file web.config da **%programfiles%\Microsoft Rights Management connector\Web Service**.

2. Individuare la riga seguente:

        <trace enabled="false" requestLimit="10" pageOutput="false" traceMode="SortByTime" localOnly="true"/>

3. Sostituire la riga con il codice seguente:

        <trace enabled="true" requestLimit="10" pageOutput="false" traceMode="SortByTime" localOnly="true"/>

4.  Arrestare e riavviare IIS per attivare la traccia. 

5.  Una volta acquisite le tracce necessarie, ripristinare la riga nel passaggio 3, quindi arrestare e riavviare IIS.




<!--HONumber=Aug16_HO4-->

