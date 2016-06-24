---
# required metadata

title: Sviluppare i requisiti di risposta agli eventi imprevisti
description:
keywords:
author: YuriDio
manager: swadhwa
ms.date: 04/28/2016
ms.topic: article
ms.prod:
ms.service:
ms.technology:
ms.assetid: 1072858e-dc0a-44ad-a512-d938f20310b6

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: 
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Crittografia dati

>[!NOTE]
>Questo argomento fa parte di una guida più ampia dedicata alle considerazioni di progettazione. Per leggere la guida dall'inizio, vedere l'[argomento principale](mdm-design-considerations-guide.md). Per scaricare una copia della versione integrale della guida, visitare la raccolta [TechNet](https://gallery.technet.microsoft.com/Mobile-Device-Management-7d401582).

Dopo aver risposto alle domande nell'Attività 1 riguardanti i requisiti per la crittografia dei dati inattivi e in transito, valutare le opzioni disponibili per soddisfare ogni requisito. Anche se sono inattivi, i dati possono essere crittografati in modi diversi, come illustrato nella figura che segue.

![Disco di dispositivo mobile](./media/MDM_Figure_09.png)

## Livelli diversi di crittografia

È possibile scegliere tra la crittografia completa del disco e la crittografia basata sui dati gestiti da un'app. [Configuration Manager](https://technet.microsoft.com/library/dn919655.aspx) consente di applicare i criteri che eseguono la crittografia dei file nei dispositivi mobili. Sebbene alcuni dispositivi mobili, ad esempio i dispositivi Windows 8, vengano automaticamente crittografati, altri eseguono la crittografia dei dati solo se è abilitata un'altra opzione. Ad esempio, per i dispositivi iOS, la crittografia viene eseguita automaticamente solo dopo che è stata configurata l'impostazione per richiedere l'uso di una password nei dispositivi. 

Windows 10 Mobile usa la crittografia del dispositivo, basata sulla tecnologia BitLocker, per crittografare tutta l'archiviazione interna, inclusi il sistema operativo e le partizioni di archiviazione dei dati. L'utente può attivare la crittografia del dispositivo oppure il reparto IT può attivare e applicare la crittografia per i dispositivi gestiti dall'azienda usando gli strumenti di MDM. Quando è attivata la crittografia del dispositivo, tutti i dati archiviati nel telefono vengono automaticamente crittografati. Un dispositivo Windows 10 Mobile con crittografia attivata consente di proteggere la riservatezza dei dati archiviati se il dispositivo viene smarrito o rubato. Per altre informazioni, leggere l'articolo sulla protezione di Windows 10 Mobile.

>[!TIP]Per altre informazioni sui dispositivi mobili in cui è possibile abilitare la crittografia usando Configuration Manager, vedere [Impostazioni generali per i dispositivi mobili in Configuration Manager](https://technet.microsoft.com/library/dn376523.aspx).

Per le app associate ai criteri di gestione delle applicazioni mobili di Intune, la crittografia viene fornita da Microsoft. I dati vengono crittografati in modo sincrono durante le operazioni di I/O dei file in base all'impostazione nei criteri di gestione delle applicazioni mobili. Nei dispositivi Android le app gestite usano la crittografia AES-128 in modalità Cipher Block Chaining (CBC) tramite le librerie di crittografia della piattaforma, crittografia non certificata FIPS 140-2. 

Questa opzione consente di specificare che tutti i dati associati a una particolare app verranno crittografati, inclusi i dati archiviati su supporti esterni come le schede SD. La stessa funzionalità è disponibile anche in [MDM per Office 365](https://technet.microsoft.com/library/ms.o365.cc.devicepolicysupporteddevice.aspx). 

I servizi di archiviazione cloud pubblici, ad esempio OneDrive for Business, possono anche essere integrati con la versione autonoma di Intune e con [System Center 2012 R2 Configuration Manager SP1](https://technet.microsoft.com/library/mt131422.aspx). Distribuendo l'app OneDrive for Business nel dispositivo dell'utente, tutti i documenti nell'account OneDrive for Business dell'utente verranno crittografati. 

La maggior parte delle soluzioni MDM usano SSL per proteggere i dati in transito, pertanto sarà sufficiente decidere se usare un'infrastruttura a chiave pubblica esistente per emettere certificati o se si userà l'autorità di certificazione (CA) di un fornitore di terze parti. Il vantaggio dell'uso di un'autorità di certificazione di terze parti è che gli utenti che usano il proprio dispositivo per accedere alle risorse aziendali considereranno automaticamente attendibile un'autorità di certificazione pubblica ben riconosciuta. 

## Intune (autonomo)

**Vantaggi** 

- Esegue la crittografia dei dati associati alle app controllate dai criteri di gestione di Intune

**Svantaggi** 

- Non include la crittografia nativa per l'archiviazione dei dispositivi mobili
- La mancanza dell'integrazione con la piattaforma MDM locale corrente indica che sarà disponibile un'interfaccia di gestione aggiuntiva

## MDM di Office 365

**Vantaggi**

- Esegue la crittografia dei dati in base alla funzionalità della piattaforma per dispositivi mobili

**Svantaggi**

- Se l'organizzazione attualmente non usa un'infrastruttura locale di Configuration Manager, è necessario pianificare, installare e configurare questa piattaforma prima dell'integrazione

## Ibrida (Intune con Configuration Manager)

**Vantaggi**

- Esegue la crittografia dei dati associati alle app controllate dai criteri di gestione di Intune
- Esegue la crittografia dell'archiviazione dei dispositivi mobili
- Fornisce un controllo più granulare degli elementi che possono essere crittografati nei dispositivi mobili e della modalità di esecuzione della crittografia, inclusa la selezione dell'algoritmo di crittografia

**Svantaggi**

- Se l'organizzazione attualmente non usa un'infrastruttura locale di Configuration Manager, è necessario pianificare, installare e configurare questa piattaforma prima dell'integrazione

Per altre informazioni sulla combinazione delle funzionalità di Intune e Configuration Manager per aumentare la protezione dei dati e configurare la crittografia, leggere l'articolo relativo alla [gestione della crittografia nei dispositivi mobili con Configuration Manager e Intune](http://blogs.technet.com/b/pauljones/archive/2014/08/04/managing-encryption-on-mobile-devices-with-configuration-manager-and-intune.aspx).


<!--HONumber=Apr16_HO2-->


