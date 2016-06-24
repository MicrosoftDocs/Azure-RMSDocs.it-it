---
# required metadata

title: Informazioni sul ciclo di vita di MDM
description:
keywords:
author: andredm7
manager: swadhwa
ms.date: 05/31/2016
ms.topic: article
ms.prod:
ms.service:
ms.technology:
ms.assetid: 901b52bf-2340-4847-aaff-c94fec9ee925

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: 
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Informazioni sul ciclo di vita di MDM

>[!NOTE]
>Questo argomento fa parte di una guida più ampia dedicata alle considerazioni di progettazione. Per leggere la guida dall'inizio, vedere l'[argomento principale](mdm-design-considerations-guide.md). Per scaricare una copia della versione integrale della guida, visitare la raccolta [TechNet](https://gallery.technet.microsoft.com/Mobile-Device-Management-7d401582).

È importante comprendere le diverse aree di gestione dei dispositivi mobili quando si progetta una soluzione di gestione dei dispositivi mobili. La figura che segue illustra le fasi generali del ciclo di vita della gestione dei dispositivi mobili. Ogni fase prevede requisiti e domande univoci da prendere in considerazione durante la pianificazione della soluzione. In questa sezione si prenderà innanzitutto in esame la fase di registrazione, mentre le fasi successive verranno illustrate in modo più approfondito in altre sezioni della guida.

![Fasi del ciclo di vita della gestione dei dispositivi mobili](./media/MDM_Figure_03.png)

**Fasi del ciclo di vita della gestione dei dispositivi mobili**

## Registrazione e configurazione dei dispositivi
Il primo passaggio nella gestione dei dispositivi mobili consiste nella registrazione e nella configurazione iniziali dei dispositivi nella soluzione di gestione dei dispositivi mobili. La semplicità e la facilità di registrazione sono i fattori chiave per il successo del ciclo di vita della gestione dei dispositivi mobili. Se la registrazione iniziale dei dispositivi risulta difficile o troppo complessa, è possibile che sia l'amministratore che gli utenti siano restii ad adottare una soluzione di gestione dei dispositivi mobili, pertanto non sarebbe possibile sfruttare le funzionalità, i vantaggi e le protezioni offerti da una soluzione di questo tipo.

La registrazione dei dispositivi mobili nelle soluzioni di gestione dei dispositivi mobili avviene solitamente in due modi:

- Registrazione gestita dall'amministratore
- Registrazione eseguita dall'utente/dal proprietario
 
La registrazione gestita dall'amministratore offre un'esperienza di registrazione gestita centralmente e in genere è incentrata sulla registrazione in blocco di più dispositivi tramite un unico account di directory. Questo è utile se è necessario registrare più dispositivi di proprietà della società in una soluzione di gestione dei dispositivi mobili.

Con la registrazione automatica, l'utente o il proprietario del dispositivo registra il dispositivo nella soluzione di gestione dei dispositivi mobili. Questo metodo è solitamente usato negli scenari BYOD (Bring Your Own Device), ma può anche essere usato negli scenari in cui la società è proprietaria del dispositivo. Questo tipo di registrazione in genere usa un modello di registrazione di tipo "push", in cui ai dispositivi viene automaticamente richiesto di registrarsi nella soluzione di gestione dei dispositivi mobili quando l'utente cerca di connettersi alla rete aziendale o a una risorsa di rete dal dispositivo. A volte, gli utenti possono scegliere di registrare i propri dispositivi prima della connessione alla rete o alle risorse di un'organizzazione.

La registrazione e la configurazione dei dispositivi mobili comprendono le operazioni seguenti:

- Distribuzione, accesso e gestione dei servizi e delle applicazioni interni ed esterni
- Imposizione delle configurazioni di sicurezza e di accesso dei dispositivi
- Protezione dei dispositivi da minacce alla sicurezza

Nella maggior parte dei casi, quando un dispositivo mobile viene registrato in una soluzione di gestione dei dispositivi mobili, al dispositivo vengono assegnati automaticamente criteri e autorizzazioni associati all'account di directory dell'utente del dispositivo e/o al gruppo a cui è associato il dispositivo stesso nei servizi directory. A seconda della soluzione di gestione dei dispositivi mobili, la maggior parte delle operazioni di configurazione e provisioning dei criteri e delle autorizzazioni del dispositivo viene eseguita prima della registrazione del dispositivo. Quindi, le impostazioni dei criteri e di conformità diventano effettive non appena i dispositivi vengono registrati, evitando discrepanze tra la registrazione e la conformità.

## Domande sulla pianificazione della registrazione e della configurazione dei dispositivi

Per pianificare la gestione del ciclo di vita della gestione dei dispositivi mobili, rispondere alle domande seguenti relative alla pianificazione di configurazione e registrazione dei dispositivi:

- La registrazione dei dispositivi mobili verrà eseguita dall'amministratore, dagli utenti o da entrambi?
- È necessario eseguire la registrazione in blocco dei dispositivi mobili?
- Qual è il numero massimo di dispositivi che è necessario registrare in blocco?
- Le piattaforme dei sistemi operativi mobili all'interno dell'organizzazione richiedono requisiti e risorse diversi per la registrazione in blocco?
- Quanti dispositivi di cui è necessario eseguire la registrazione usa solitamente ogni utente?
- La soluzione di gestione dei dispositivi mobili prevede un limite di registrazione di dispositivi per utente?
- Quali sono i requisiti (connettività, applicazione, agente di gestione, portale aziendale, supporto) per gli utenti che devono eseguire la registrazione automatica dei dispositivi?
-  Sono diversi dai requisiti per la registrazione gestita dall'amministratore?
-  Quali sono i requisiti di registrazione per ogni sistema operativo dei dispositivi che è necessario supportare?
-  I sistemi operativi dei dispositivi mobili dell'organizzazione richiedono requisiti di registrazione speciali o particolari?
-  La soluzione di gestione dei dispositivi mobili supporta sia le registrazioni tramite connessione cablata che le registrazioni in modalità wireless?
-  Quali sono i requisiti hardware (se applicabili) per supportare le registrazioni dei dispositivi?
-  Quali sono i requisiti relativi alla connettività e alla sicurezza di rete per supportare le registrazioni dei dispositivi?
-  È necessario applicare criteri di conformità specifici ai dispositivi al momento della registrazione iniziale?
-  È necessario applicare criteri di sicurezza specifici ai dispositivi al momento della registrazione iniziale?
-  È necessario poter configurare o impostare un limite di tempo massimo o minimo per il provisioning dei criteri dei dispositivi dopo la registrazione iniziale?
-  È necessario attivare automaticamente criteri di provisioning speciali in caso di errori di registrazione?

##Gestione dei dispositivi
Il modo in cui vengono gestiti i dispositivi mobili, sia dal punto di vista dell'amministratore che degli utenti, è un aspetto fondamentale di una soluzione di gestione dei dispositivi mobili.

Ad esempio, si potrebbe voler integrare la modalità di gestione dei dispositivi mobili con la modalità di gestione dei dispositivi non mobili (server, desktop, altri dispositivi di rete). A seconda dell'organizzazione, le soluzioni di gestione dei dispositivi non mobili potrebbero essere state implementate molto prima che i dispositivi mobili venissero introdotti nell'organizzazione. Questo potrebbe aver richiesto costi notevoli e investimenti a lungo termine per tali soluzioni di gestione.

Comprendere in modo approfondito la modalità in cui un'organizzazione può integrare soluzioni di gestione dei dispositivi mobili con soluzioni esistenti di gestione dei dispositivi non mobili è probabilmente una delle attività più importanti per la progettazione di una soluzione di gestione dei dispositivi mobili in grado di soddisfare le esigenze aziendali.

La gestione dei dispositivi mobili in genere abbraccia diverse aree amministrative:

- **Configurazione e sicurezza dei dispositivi:** la sicurezza dei dispositivi mobili include una vasta gamma di impostazioni che è possibile distribuire ai dispositivi gestiti dell'organizzazione. Le impostazioni possono richiedere di specificare i dettagli temporali, la scadenza e le caratteristiche necessari per l'accesso tramite passcode al dispositivo, la crittografia del dispositivo e la cancellazione di dati da dispositivi persi o rubati. Per altre informazioni sulla sicurezza e la configurazione, vedere l'argomento [Passaggio 3: Piano per la protezione dei dispositivi mobili](mdm-step-3-plan-enhancing-mobile-devices-protection.md).
- **Gestione delle applicazioni:** quest'area include la gestione di distribuzione, installazione, aggiornamento e controllo dello stato e disinstallazione delle applicazioni. È anche possibile gestire le restrizioni per alcune applicazioni non conformi, un aspetto di importanza fondamentale per una strategia globale di conformità e sicurezza. Sono anche possibili scenari di gestione delle applicazioni in cui è necessario gestire le applicazioni sui dispositivi mobili ma non è opportuno registrare i dispositivi nella piattaforma di gestione dei dispositivi mobili.
- **Accesso alle risorse aziendali:** la gestione dei dispositivi mobili può anche agevolare la gestione dell'accesso a risorse di rete locali come server di posta elettronica, reti Wi-Fi e risorse basate su VPN. Questo consente di aiutare a garantire la conformità alla sicurezza e semplifica l'accesso alle risorse della società in base ai criteri aziendali per gli utenti dei dispositivi mobili. Se l'accesso alle risorse dell'organizzazione è eccessivamente complesso o difficoltoso per gli utenti dei dispositivi mobili, possono decidere di usare risorse aziendali non approvate per archiviare dati aziendali, se questo rende il processo più semplice.
- **Inventario e creazione di report:** quando si gestiscono i dispositivi mobili, è opportuno registrare e analizzare gli eventi della piattaforma e dei dispositivi mobili per tenere traccia della conformità ai criteri di gestione dell'organizzazione. La creazione di report dettagliati può anche offrire statistiche e dati in tempo reale, per prendere decisioni migliori più velocemente in base allo stato dei dispositivi mobili e degli utenti dei dispositivi mobili. Informazioni più dettagliate sull'inventario e sulla creazione di report sono disponibili in una sezione successiva.

### Domande sulla pianificazione della gestione dei dispositivi
Per il momento, concentrarsi solo sugli aspetti amministrativi principali, in quanto si stanno ancora definendo i requisiti. È possibile perfezionare tali requisiti con l'evolversi del piano e comprendere meglio le esigenze complessive dell'organizzazione.</para><para>Rispondere alle domande seguenti relative alla pianificazione della gestione dei dispositivi:

- Sono necessari criteri di gestione specifici applicati a gruppi di utenti, gruppi di dispositivi e/o gruppi di sistemi operativi dei dispositivi?
- Sono necessari criteri di gestione specifici per diversi tipi di dispositivi? Ad esempio, criteri separati per i dispositivi di proprietà dell'utente o della società oppure dispositivi mobili e non mobili?
- Sono necessari diritti e autorizzazioni di gestione dei dispositivi separati per diversi ruoli o posizioni IT? In tal caso:
 - Quale separazione dei livelli di autorizzazione è necessaria?
 - I livelli di autorizzazione supportati dalla soluzione devono essere personalizzabili?
 - Le autorizzazioni devono essere integrate nei servizi directory dell'account esistente?
- È necessario avere la possibilità di distribuire sia manualmente che automaticamente gli agenti o il software della soluzione di gestione dei dispositivi mobili?
- È necessario avere la possibilità di gestire le applicazioni nei dispositivi mobili senza dover registrare i dispositivi in una piattaforma di gestione dei dispositivi mobili, nuova o già esistente?
- Si desidera integrare la gestione dei dispositivi mobili con una soluzione di gestione dei dispositivi non mobili esistente? In tal caso:
 - Si desidera gestire tutti i dispositivi da un portale o una console di gestione unificata?
 - Quali sono i requisiti di integrazione per la soluzione di gestione dei dispositivi non mobili esistente?
 - In che modo la soluzione di gestione dei dispositivi non mobili esistente supporta le autorizzazioni e i ruoli di gestione richiesti?
 - Esistono requisiti hardware o di rete per la connessione dei servizi di gestione tra le soluzioni di gestione dei dispositivi mobili e quelle di gestione dei dispositivi non mobili?
 - Entrambe le soluzioni sono dotate di sistemi di inventario e creazione di report separati?
- La soluzione di gestione dei dispositivi mobili dispone di un portale aziendale per consentire agli utenti di installare le proprie app?
- La soluzione di gestione dei dispositivi mobili soddisfa i requisiti di scalabilità della società?
- La soluzione di gestione dei dispositivi mobili supporta l'amministrazione remota?
- La soluzione di gestione dei dispositivi mobili supporta l'automazione?

## Gestione delle app

In alcuni casi può non essere opportuno registrare un dispositivo mobile in un sistema di gestione dei dispositivi ma è comunque necessario gestire le applicazioni sul dispositivo per impedire che i dati aziendali vengano trasferiti ad altri servizi o app consumer sul dispositivo. Questa situazione si può verificare quando i dipendenti usano i dispositivi personali per accedere alle risorse aziendali in uno scenario BYOD oppure quando si ha l'esigenza di gestire i dispositivi mobili su una piattaforma di gestione dei dispositivi e le applicazioni su un'altra piattaforma di gestione.

### Domande sulla pianificazione della gestione delle applicazioni

Per pianificare le considerazioni sulla gestione delle app, rispondere alle domande seguenti sulla pianificazione:

- I dati aziendali devono essere separati dai dati personali degli utenti nelle app dei dispositivi mobili?
- È necessario impedire che i dati vengano condivisi con operazioni Taglia/Copia/Incolla tra le app aziendali e quelle personali nei dispositivi mobili?
- È necessario impedire che le app eseguano il backup o il salvataggio dei dati in altre app o servizi?
- È necessario abilitare i criteri di prevenzione della perdita di dati per ogni app?
- È necessario limitare il contenuto Web visualizzato in un browser gestito?

##Ritiro o annullamento della registrazione del dispositivo

Quando gli utenti lasciano l'organizzazione o i dispositivi mobili vengono ritirati o sostituiti, è necessario assicurarsi che i dati aziendali non vengano persi o violati. In genere, le soluzioni di gestione dei dispositivi mobili supportano sia il ripristino del dispositivo che l'annullamento della registrazione per i dispositivi gestiti dall'IT e dall'utente. Per la maggior parte dei dispositivi mobili, l'annullamento della registrazione inizia con il ripristino del dispositivo alle impostazioni predefinite di fabbrica o con l'esecuzione di una cancellazione selettiva di tutti i dati e le applicazioni aziendali. Quindi, viene rimossa la connessione della registrazione del dispositivo alla soluzione di gestione. Tuttavia, il processo varia a seconda dei produttori di dispositivi mobili e delle piattaforme dei sistemi operativi dei dispositivi.

### Domande sul ritiro o annullamento della registrazione dei dispositivi

Rispondere alle domande seguenti relative alla pianificazione del ritiro o dell'annullamento della registrazione dei dispositivi:

- È necessario che sia l'IT che gli utenti siano in grado di annullare la registrazione dei dispositivi mobili?
- Se viene eseguita la cancellazione selettiva di un dispositivo, la registrazione del dispositivo nella soluzione di gestione dei dispositivi mobili deve essere annullata automaticamente?
- Se gli utenti dei dispositivi mobili possono annullare la registrazione dei propri dispositivi mobili, come verrà verificata la rimozione dei dati e delle applicazioni aziendali?
 - Il processo è diverso per i dispositivi sottoposti a cancellazione selettiva e i dispositivi che vengono ripristinati alle impostazioni predefinite di fabbrica?

>[!TIP]
>Assicurarsi di prendere appunti per ogni risposta e di comprendere la logica alla base della risposta. Le attività successive esamineranno le opzioni disponibili e i vantaggi e svantaggi di ogni opzione.  Rispondere a queste domande consentirà di selezionare l'opzione più adatta alle esigenze aziendali.

<!--HONumber=Jun16_HO1-->


