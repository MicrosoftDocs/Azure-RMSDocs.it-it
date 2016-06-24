---
# required metadata

title: Privacy del client
description:
keywords:
author: YuriDio
manager: swadhwa
ms.date: 04/28/2016
ms.topic: article
ms.prod:
ms.service:
ms.technology:
ms.assetid: c799a6c4-fe0a-4148-8e75-29e6ffdb7e6e

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: 
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

#Privacy del client

>[!NOTE]
>Questo argomento fa parte di una guida più ampia dedicata alle considerazioni di progettazione. Per leggere la guida dall'inizio, vedere l'[argomento principale](mdm-design-considerations-guide.md). Per scaricare una copia della versione integrale della guida, visitare la raccolta [TechNet](https://gallery.technet.microsoft.com/Mobile-Device-Management-7d401582).

Quando la società implementa la gestione dei dispositivi mobili, è importante tenere presente i confini tra la privacy dell'utente e quella dell'organizzazione. Idealmente l'organizzazione dovrebbe già disporre di criteri di privacy chiari, indicanti le azioni previste da parte degli utenti sulla privacy dei dati. Poiché i dispositivi mobili potrebbero memorizzare dati aziendali e accompagneranno l'utente nei suoi spostamenti, è importante che i confini di privacy siano correttamente definiti e che gli utenti conoscano il proprio ruolo nel mantenimento della privacy dell'organizzazione.
  
Un'altra considerazione riguarda la modalità di verifica delle aspettative degli utenti quando registrano i dispositivi nella soluzione MDM dell'organizzazione. Nel [portale aziendale di Microsoft Intune](https://technet.microsoft.com/library/dn646957.aspx) è possibile personalizzare l'informativa sulla privacy dell'azienda in modo che includa un URL con la descrizione dei dati raccolti quando gli utenti usano i dispositivi gestiti.
 
È inoltre possibile pubblicare i termini e le condizioni che gli utenti visualizzeranno quando useranno per la prima volta il portale aziendale dai dispositivi, indipendentemente dal fatto che tali dispositivi siano registrati nella soluzione MDM. Gli utenti devono accettare i termini prima di poter accedere al portale aziendale. Quando si aggiornano i termini e si desidera che gli utenti visualizzino e accettino le nuove condizioni, è possibile contrassegnarle come una nuova versione, in modo che gli utenti seguano lo stesso processo di accettazione alla successiva visita del portale aziendale. 

La funzionalità per la richiesta di accettazione dei termini e delle condizioni è disponibile anche quando si usa un ambiente ibrido con Configuration Manager connesso con Intune. Configuration Manager è anche in grado di usare le impostazioni di conformità per determinare se i dispositivi sono conformi agli elementi di configurazione distribuiti usando le linee di base di configurazione. Se non sono conformi, alcune impostazioni possono essere corrette automaticamente. 

Le informazioni sulla conformità vengono inviate al server del sito dal punto di gestione e memorizzate nel database del sito. Le informazioni vengono crittografate quando i dispositivi le inviano al punto di gestione, ma non vengono memorizzate in forma crittografata nel database del sito. Le informazioni vengono conservate nel database finché non vengono eliminate nell'ambito dell'attività di manutenzione del sito *Elimina dati di gestione configurazione obsoleti* eseguita ogni 90 giorni.  È inoltre possibile configurare l'intervallo di eliminazione. Le informazioni sulla conformità non vengono inviate a Microsoft.

Poiché Intune e Office 365 sono servizi basati su cloud, gli utenti dovrebbero tenere in considerazione anche il modo in cui Microsoft gestisce la privacy dell'utente per questi servizi. È possibile aggiungere puntatori alle informazioni sulla privacy relative a questi servizi, ad esempio:

- Centro protezione di Office 365
- Centro protezione di Microsoft Intune

La privacy è importante sia per gli utenti che per l'organizzazione e la soluzione MDM in uso deve bilanciare in modo appropriato le esigenze in termini di privacy, nonché indicare agli utenti i criteri e le aspettative dell'organizzazione in termini di privacy. La tabella che segue confronta le opzioni di gestione dei requisiti relativi alla privacy in diverse soluzioni MDM per agevolare la scelta dell'opzione MDM più adatta ai requisiti della propria organizzazione in termini di privacy.

## Intune (autonomo)

**Vantaggi**

- Usa il portale aziendale di Intune per pubblicare l'informativa sulla privacy dell'organizzazione

**Svantaggi**

- Non dispone di un modello per l'informativa sulla privacy. Si presuppone che l'organizzazione disponga già di un criterio di privacy e che il portale aziendale si limiterà a pubblicare il criterio archiviato in un'altra posizione

## Office 365 con MDM

**Vantaggi**

- Nessuna funzionalità per la pubblicazione di informative sulla privacy

**Svantaggi**

- Nessuna funzionalità per la pubblicazione di informative sulla privacy

## Ibrida (Intune con Configuration Manager)

**Vantaggi**

- Usa il portale aziendale di Intune per pubblicare l'informativa sulla privacy dell'organizzazione
- Unica console di gestione per i dispositivi mobili registrati da dispositivi locali e cloud

**Svantaggi**

- Se l'organizzazione attualmente non usa un'infrastruttura locale di Configuration Manager, è necessario pianificare, installare e configurare questa piattaforma prima dell'integrazione



<!--HONumber=Apr16_HO2-->


