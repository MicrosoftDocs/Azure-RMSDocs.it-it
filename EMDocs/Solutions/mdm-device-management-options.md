---
# required metadata

title: Opzioni di gestione dei dispositivi
description:
keywords:
author: robmazz
manager: swadhwa
ms.date: 04/28/2016
ms.topic: article
ms.prod:
ms.service:
ms.technology:
ms.assetid: a25f7407-92a0-4588-b5f7-a7bad9cdd070

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: 
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Opzioni di gestione dei dispositivi

>[!NOTE]
>Questo argomento fa parte di una guida più ampia dedicata alle considerazioni di progettazione. Per leggere la guida dall'inizio, vedere l'[argomento principale](mdm-design-considerations-guide.md). Per scaricare una copia della versione integrale della guida, visitare la raccolta [TechNet](https://gallery.technet.microsoft.com/Mobile-Device-Management-7d401582).

La gestione dei dispositivi mobili con Intune e Configuration Manager è incentrata sui criteri di gestione. I criteri definiscono gruppi di impostazioni per dispositivi mobili e possono essere creati da modelli o personalizzati per dispositivi, utenti o gruppi specifici. La procedura di gestione ottimale consiste nel creare i criteri di gestione prima della registrazione dei dispositivi mobili nella soluzione di gestione. Questo assicura che i dispositivi vengano immediatamente gestiti in base ai criteri e ai processi definiti nella strategia IT. Entrambe le soluzioni consentono di configurare i tipi di criteri seguenti:

- Criteri di configurazione: vengono usati per definire le impostazioni generali dell'organizzazione per ogni dispositivo mobile registrato. I criteri possono includere impostazioni relative a password, applicazioni, criteri del cloud e crittografia, ma anche **[molte altre impostazioni dei dispositivi](https://technet.microsoft.com/library/dn743712.aspx)** per diverse aree di gestione. Inoltre, i criteri di configurazione vengono applicati e configurati in modo diverso per diversi tipi di sistemi operativi mobili usando i profili di registrazione dei dispositivi.

>[!TIP]
>Quando si creano criteri diversi per tipi diversi di dispositivi, utenti o gruppi, è facile che vengano applicate allo stesso dispositivo impostazioni di criteri in conflitto. Assicurarsi di comprendere **[in che modo vengono applicate le impostazioni dei criteri in conflitto](https://technet.microsoft.com/library/dn743712.aspx)**.

- **Criteri di conformità:** i criteri di conformità applicano i requisiti dell'organizzazione per l'accesso, o la negazione dell'accesso, dei dispositivi mobili a risorse o servizi aziendali. Possono anche includere impostazioni relative a password e crittografia del dispositivo, nonché determinare se il dispositivo mobile è rooted ("jailbroken"). Come per i criteri di configurazione, le opzioni dei criteri di conformità di Intune e [Configuration Manager](https://technet.microsoft.com/library/dn376523.aspx) variano a seconda del tipo di sistema operativo del dispositivo mobile. Se si creano criteri di conformità in Configuration Manager, è importante notare che è possibile configurare una maggiore granularità nell'ambito di un processo multiparte:

 1. Creazione di [elementi di configurazione](https://technet.microsoft.com/library/gg712331.aspx?WT.mc_id=Blog_EntMob_Showcase_PCIT)
 2. Creazione di [linee di base di configurazione](https://technet.microsoft.com/library/gg712268.aspx?WT.mc_id=Blog_EntMob_Showcase_PCIT)
 3. Distribuzione delle [linee di base di configurazione](https://technet.microsoft.com/library/hh219289.aspx?WT.mc_id=Blog_EntMob_Showcase_PCIT) a raccolte di utenti o dispositivi di Configuration Manager

- **Criteri di accesso condizionale:** definiscono il modo in cui viene gestito l'accesso alla posta elettronica e possono essere usati separatamente o in combinazione con i criteri di conformità. È necessario configurare le connessioni al servizio Exchange Server o Exchange Online locale in [Intune](/Intune/deployuse/restrict-access-to-email-and-o365-services-with-microsoft-intune) o in [Configuration Manager](https://technet.microsoft.com/library/dn919655.aspx) per poter distribuire i criteri di accesso condizionale. L'accesso condizionale può anche essere configurato per servizi di Office 365 e SharePoint Online.

Le risposte alle domande nel passaggio 1 aiutano a decidere in che modo verranno registrati i dispositivi nella soluzione adottata per la gestione dei dispositivi mobili. La tabella seguente aiuta a comprendere i vantaggi e gli svantaggi di ogni scenario di gestione.

## Intune (autonomo)

**Vantaggi**

- Supporta il controllo dei criteri semplificato per la gestione di utenti e dispositivi, ora separati dalla piattaforma per dispositivi.
- Supporta le piattaforme Android, iOS, Windows 10https://technet.microsoft.com/library/mt147406.aspx, Windows 8.x e Windows Phone, nonché Exchange ActiveSync.
- Offre una console di amministrazione e gestione semplice e basata sul Web, accessibile da qualsiasi posizione
- Supporta i criteri basati su gruppo, rendendo più semplice la gestione di un numero elevato e di tipi diversi di dispositivi mobili
- Supporta caratteristiche e funzionalità avanzate di conformità dei dispositivi mobili, tra cui il rilevamento root e jailbreak dei dispositivi
- Consente la cancellazione selettiva o il ripristino completo delle impostazioni di fabbrica per tutti i dispositivi mobili
- Include un portale aziendale personalizzabile, consentendo la distribuzione sicura e gestita di applicazioni per dispositivi mobili interne e di terze parti
- Distribuisce certificati ai dispositivi mobili
- Consente alle organizzazioni di bloccare le funzioni di taglia/copia/incolla nelle applicazioni per dispositivi mobili
- Supporta l'imposizione dell'uso di browser gestiti
- Supporta l'uso dei numeri IMEI dei dispositivi per identificare e contrassegnare i dispositivi di proprietà dell'azienda in modo da separare le assegnazioni dei criteri dai dispositivi di proprietà personale

**Svantaggi**

- Requisiti e costi di licenza aggiuntivi per gli account utente che eseguono la registrazione dei dispositivi nel servizio Intune

## Gestione dei dispositivi mobili per Office 365

**Vantaggi**

- Console di amministrazione e gestione integrata basata sul Web nei tenant di Office 365
- Supporta i criteri basati su gruppo, rendendo più semplice la gestione di un numero elevato e di tipi diversi di dispositivi mobili
- Supporta caratteristiche e funzionalità avanzate di conformità dei dispositivi mobili, tra cui il rilevamento root e jailbreak dei dispositivi
- Consente la cancellazione selettiva o il ripristino completo delle impostazioni di fabbrica per tutti i dispositivi mobili

**Svantaggi**

- Non sono supportate le funzionalità avanzate di gestione dei dispositivi mobili, tra cui:
 - Provisioning e gestione di certificati, posta elettronica, VPN, profili wireless
 - Registrazione e gestione di raccolte di dispositivi
- Alcune caratteristiche e funzionalità di gestione delle applicazioni per dispositivi mobili non sono supportate:
 - Distribuzione di applicazioni line-of-business ai dispositivi mobili
 - Abilitazione dell'accesso sicuro dei dati per le applicazioni per dispositivi mobili Office
 - Estensione sicura dei dati aziendali ad app line-of-business per dispositivi mobili
 - Browser gestiti o altre applicazioni per la visualizzazione di contenuti

## Ibrida (Intune con Configuration Manager)

**Vantaggi**

- Tutti i vantaggi di Intune autonomo, oltre alle funzionalità seguenti:
 - Offre un unico riquadro di visualizzazione per la gestione aziendale, tra cui la flessibilità per l'amministrazione basata su ruoli e script (tramite PowerShell)

**Svantaggi**

- Richiede requisiti di configurazione aggiuntivi per la connessione di Intune all'infrastruttura di Configuration Manager locale
- Le organizzazioni che per il momento non hanno configurato un'infrastruttura di Configuration Manager dovranno pianificarla, installarla e configurarla prima dell'integrazione con Intune
- I profili di posta elettronica e le reti VPN per i dispositivi Android non sono attualmente supportati
- I browser gestiti non sono attualmente supportati

<!--HONumber=Apr16_HO2-->


