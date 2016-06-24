---
# required metadata

title: Sviluppare la strategia di adozione della gestione dei dispositivi mobili
description:
keywords:
author: YuriDio
manager: swadhwa
ms.date: 04/28/2016
ms.topic: article
ms.prod:
ms.service:
ms.technology:
ms.assetid: 10172816-b52d-4a55-8803-6a6805126fab

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: 
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Sviluppare la strategia di adozione della gestione dei dispositivi mobili

>[!NOTE]
>Questo argomento fa parte di una guida più ampia dedicata alle considerazioni di progettazione. Per leggere la guida dall'inizio, vedere l'[argomento principale](mdm-design-considerations-guide.md). Per scaricare una copia della versione integrale della guida, visitare la raccolta [TechNet](https://gallery.technet.microsoft.com/Mobile-Device-Management-7d401582).

In questa attività viene sviluppata la strategia di adozione della gestione dei dispositivi mobili in grado di soddisfare i requisiti aziendali identificati nelle attività 1 e 2. 

## Proprietà del dispositivo

Dopo aver esaminato la strategia e i criteri aziendali attuali di gestione dei dispositivi, è necessario avere a disposizione un elenco di scenari che l'organizzazione prevede di implementare. La sezione seguente aiuta a comprendere i vantaggi e gli svantaggi di ogni scenario:

## Il dipendente è proprietario del dispositivo (BYOD)

**Vantaggi** 

- Non è necessario acquistare i dispositivi mobili per i dipendenti della società
- In genere consente ai dipendenti di essere più produttivi, dal momento che useranno il dispositivo mobile di loro scelta
- I costi di supporto possono diminuire, poiché l'organizzazione offrirà supporto limitato per i dispositivi mobili

**Svantaggi**

- Aumentano le considerazioni sulla sicurezza per proteggere i dati aziendali che si trovano sui dispositivi personali
- Aumenta la probabilità di perdita di dati, soprattutto quando non sono stati predisposti controlli di sicurezza appropriati
- Funzionalità di gestione limitata a causa di restrizioni relative alla privacy

## Dispositivo di proprietà della società

**Vantaggi** 

- Funzionalità di gestione completa, compresa la sicurezza avanzata e i controlli di sicurezza del dispositivo
- Maggiore controllo sui dispositivi mobili
- Capacità di definire quali dispositivi mobili verranno usati dai dipendenti

**Svantaggi**

- Potenziale aumento dei costi di supporto, poiché l'organizzazione provvederà alla manutenzione dei dispositivi mobili
- Minor flessibilità per gli utenti finali, che può influire sulla produttività
- Aumento dei costi, poiché sarà necessario acquistare i dispositivi mobili

In alcuni scenari le organizzazioni adottano entrambi i modelli: BYOD e dispositivi di proprietà dell'azienda. In tal caso, la piattaforma di gestione dei dispositivi deve essere in grado di gestire più piattaforme e di integrarsi con l'attuale infrastruttura locale. Se la propria organizzazione rientra in questo scenario, verificare anche se i criteri di protezione sono in grado di coprire entrambi i modelli dal punto di vista della conformità. Si possono applicare requisiti diversi per ogni modello e la soluzione di gestione dei dispositivi mobili deve essere in grado di usare entrambi i modelli, consentendo allo stesso tempo al reparto IT di mantenere il controllo.

## Piattaforme per dispositivi mobili supportate

La decisione presa in merito alla proprietà dei dispositivi aiuta a identificare quali piattaforme per dispositivi mobili è necessario supportare. La soluzione di gestione dei dispositivi mobili scelta dovrà conformarsi a questa decisione. In uno scenario con una piattaforma unica per dispositivi mobili, la scelta della piattaforma è meno importante rispetto allo scenario con più piattaforme. Usare la sezione seguente per scegliere la soluzione di gestione dei dispositivi mobili per uno scenario con più piattaforme:

### Intune (autonomo)

**Vantaggi**

- Servizio cloud always-on che supporta le funzionalità e gli aggiornamenti più recenti per la gestione dei dispositivi mobili
- Supporta il provisioning di tutti i principali sistemi operativi per dispositivi mobili (Android, iOS, Windows 8, Windows 10 e Windows Phone)
- Consente di gestire qualsiasi dispositivo mobile da qualsiasi luogo
- Opzioni di gestione più avanzate per i dispositivi mobili
- [Gestione per applicazioni mobili](http://blogs.technet.com/b/microsoftintune/archive/2015/06/18/now-available-intune-mobile-application-management-and-conditional-access-for-outlook.aspx)

**Svantaggi**

- La mancanza di integrazione con l'attuale soluzione locale di gestione dei dispositivi introdurrà un'interfaccia di gestione aggiuntiva da usare
- I criteri creati usando la soluzione di gestione dei dispositivi mobili locale non vengono replicati nel servizio cloud

### Gestione dei dispositivi mobili per Office 365

**Vantaggi**

- Integrazione con Office 365
- Se si usa già Office 365, è possibile sfruttare facilmente le funzionalità appropriate per la gestione dei dispositivi mobili
- Se si usa già Office 365, non è necessario usare un'altra console per gestire i dispositivi mobili

**Svantaggi**

- Set di funzionalità limitato (vedere la nota che segue questa tabella) per gestire i dispositivi mobili
- La mancanza di integrazione con l'attuale soluzione locale di gestione dei dispositivi introdurrà un'interfaccia di gestione aggiuntiva da usare

### Ibrida (Intune con Configuration Manager)

**Vantaggi**

- Integrazione nativa tra Intune e Configuration Manager
- Consente di usare una console centralizzata per distribuire i criteri e gestire computer locali, server e dispositivi mobili

**Svantaggi** 

- Richiede ulteriori passaggi di configurazione per la connessione a Intune e Configuration Manager
- Se l'organizzazione attualmente non ha un'infrastruttura locale di Configuration Manager, sarà necessario pianificare, installare e configurare questa piattaforma prima dell'integrazione

Se è sufficiente gestire l'accesso alla posta elettronica di lavoro, al calendario, ai contatti e alle attività dai dispositivi mobili, leggere l'articolo relativo alle [funzionalità di gestione dei dispositivi Exchange ActiveSync disponibili in Office 365](https://technet.microsoft.com/library/dn792010.aspx#tasks).

## Requisiti delle applicazioni

In base ai requisiti definiti nell'attività 1, è possibile scegliere quale soluzione di gestione dei dispositivi mobili è più adatta all'organizzazione. Usare la tabella seguente per confrontare le opzioni di gestione dei dispositivi mobili e i vantaggi e gli svantaggi di ogni opzione:


### Intune (autonomo)

**Vantaggi**

- Consente di gestire app per dispositivi mobili durante tutto il ciclo di vita, tra cui distribuzione di app da file di installazione e archivi app, monitoraggio dettagliato dello stato delle app e rimozione di app. Per altre informazioni, leggere l'articolo relativo alla distribuzione di software ai dispositivi mobili in Microsoft Intune.
- Consente di specificare un elenco di app conformi che gli utenti possono installare e di app non conformi che gli utenti non devono installare. Per altre informazioni, leggere l'articolo relativo alla gestione dei dispositivi usando i criteri di configurazione con Microsoft Intune.
- Consente di impostare le restrizioni per le app usando criteri di gestione delle applicazioni per dispositivi mobili. Limitando operazioni come copia e incolla, backup esterno dei dati e trasferimento dei dati tra le app si aumenta la sicurezza dei dati aziendali. Per altre informazioni, leggere l'articolo relativo al controllo delle app usando i criteri di gestione delle applicazioni per dispositivi mobili con Microsoft Intune.
- Supporta diverse piattaforme per dispositivi mobili. Per altre informazioni, vedere i dispositivi mobili supportati nell'articolo relativo alle funzionalità di gestione dei dispositivi mobili in Microsoft Intune.
- Verifica delle applicazioni disponibili per gli utenti VPN. È possibile selezionare le app che si connettono automaticamente alla rete aziendale con VPN creando un elenco di app quando si configura il profilo VPN
- Supporta criteri di gestione delle applicazioni mobili (MAM) che consentono di impedire la divulgazione dei dati aziendali alle app o ai servizi consumer.
- Intune MAM consente al reparto IT di abilitare l'accesso sicuro ai dati aziendali SaaS, ad esempio Office 365, per partner, collaboratori e fornitori senza gestire i loro dispositivi.


**Svantaggi**

- Non consente l'integrazione con soluzioni locali di gestione dei dispositivi e quindi introduce un'interfaccia di gestione aggiuntiva da usare per la gestione dei dispositivi mobili se si usa una soluzione locale. 
- I criteri creati usando la piattaforma MDM locale non vengono replicati nel servizio cloud, pertanto sono necessari due set di criteri di conformità e gestione, se viene usata una soluzione MDM locale


### Gestione dei dispositivi mobili per Office 365

**Vantaggi**

- Disponibilità delle funzionalità MDM su tutte le piattaforme del sistema operativo, ad esempio i requisiti della password                                                                                                                                                                                                                                                                                                                                                           

**Svantaggi**

- Set di funzionalità limitato per il controllo delle app
- Non consente l'integrazione con soluzioni locali di gestione dei dispositivi e quindi introduce un'interfaccia di gestione aggiuntiva da usare per la gestione dei dispositivi mobili se si usa una soluzione locale.
- Non consente di distribuire app né di applicare funzioni di gestione delle applicazioni per dispositivi mobili


### Ibrida (Intune con Configuration Manager)

**Vantaggi**

- Eredita le impostazioni di controllo delle app da Intune autonomo
- Offre un'esperienza di gestione integrata, tra Intune e Configuration Manager
- Sfrutta le funzionalità di gestione delle app di Configuration Manager. Per altre informazioni, leggere l'articolo relativo alla gestione delle applicazioni in Configuration Manager.
- Sfrutta le funzionalità di gestione delle app di Configuration Manager. Per altre informazioni, leggere l'articolo relativo alla gestione delle applicazioni in Configuration Manager.
- Consente di usare un'unica console per distribuire criteri e gestire i criteri delle applicazioni per computer locali, server e dispositivi mobili
- Verifica delle applicazioni disponibili per gli utenti VPN. È possibile selezionare le app che si connettono automaticamente alla rete aziendale con VPN creando un elenco di app quando si configura il profilo VPN.

**Svantaggi**

- Richiede passaggi aggiuntivi per impostare l'integrazione
- Se l'organizzazione attualmente non usa un'infrastruttura di Configuration Manager locale, per prima cosa è necessario pianificare, installare e configurare la piattaforma di Configuration Manager
- Senza l'integrazione con Intune, Configuration Manager può offrire una soluzione limitata per la gestione dei dispositivi mobili in base alle piattaforme per dispositivi mobili supportate. Per altre informazioni, vedere l'articolo Determinare la modalità di gestione dei dispositivi mobili in Configuration Manager.


## Requisiti di rilevamento

Comprendere il comportamento degli utenti e identificarne la posizione sono fattori importanti da includere nella strategia di gestione dei dispositivi mobili. Le modalità di rilevamento dei dispositivi variano a seconda delle esigenze e dei requisiti aziendali.  Sono disponibili funzionalità di rilevamento diverse in ogni sistema operativo mobile, pertanto le piattaforme per dispositivi mobili che si sceglie di supportare avranno un impatto sulle opzioni disponibili. Ad esempio, i requisiti di conformità possono indurre a dare la priorità all'adozione di piattaforme per dispositivi mobili che consentono di tenere traccia della posizione dell'utente e di ricorrere al geofencing.

>[!TIP] I recinti virtuali consentono di monitorare la posizione geografica di un dispositivo mobile e di abilitare o disabilitare il dispositivo e le risorse di rete in base a tale posizione. Ad esempio, Windows 8.1 consente a un'app di definire un'area geografica e fa in modo che il sistema avverta l'app quando il dispositivo su cui è in esecuzione entra o esce da tale area. Per altre informazioni su questa funzionalità in Windows 8.1, leggere l'articolo [Recinti virtuali, dall'inizio alla fine (XAML)](https://msdn.microsoft.com/library/windows/apps/xaml/dn342943.aspx). 




<!--HONumber=Apr16_HO2-->


