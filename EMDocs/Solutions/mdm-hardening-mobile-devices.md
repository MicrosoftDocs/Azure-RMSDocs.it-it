---
# required metadata

title: Protezione avanzata dei dispositivi mobili
description:
keywords:
author: YuriDio
manager: swadhwa
ms.date: 04/28/2016
ms.topic: article
ms.prod:
ms.service:
ms.technology:
ms.assetid: ade57c73-a8a2-497f-ad8d-5dfc3cba9e70

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: 
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Protezione avanzata dei dispositivi mobili

>[!NOTE]
>Questo argomento fa parte di una guida più ampia dedicata alle considerazioni di progettazione. Per leggere la guida dall'inizio, vedere l'[argomento principale](mdm-design-considerations-guide.md). Per scaricare una copia della versione integrale della guida, visitare la raccolta [TechNet](https://gallery.technet.microsoft.com/Mobile-Device-Management-7d401582).

Quando si crea una linea di base di configurazione per i dispositivi mobili per la protezione avanzata delle funzionalità in base alle esigenze aziendali, è necessario assicurarsi di trovare il giusto equilibrio tra usabilità e sicurezza. Un modello di protezione avanzata molto rigido può causare problemi di usabilità e accesso per i dipendenti, vanificando lo scopo di rendere gli utenti più produttivi tramite l'accesso alle risorse aziendali sui propri dispositivi. 

Tenere inoltre presente che non tutti i criteri di sicurezza sono disponibili per tutte le piattaforme per dispositivi mobili. Potrebbe essere necessario bilanciare le priorità per l'autorizzazione delle piattaforme per dispositivi mobili dell'organizzazione con i requisiti di conformità per la sicurezza per la protezione avanzata dei dispositivi.
Un possibile approccio alla protezione avanzata dei dispositivi mobili consiste nel disporre di diversi livelli di sicurezza. Le impostazioni disponibili per ogni livello possono inoltre variare a seconda della soluzione MDM. La figura che segue illustra un esempio di come è possibile impostare questo approccio a più livelli.

![Livelli di sicurezza](./media/MDM_Figure_12.png)

## Aree diverse di protezione avanzata dei dispositivi mobili

È possibile usare ogni livello per raggruppare le aree che devono essere conformi ai requisiti di sicurezza aziendali. Ad esempio, è possibile configurare Intune per distribuire [criteri di sicurezza](/intune/deployuse/manage-settings-and-features-on-your-devices-with-microsoft-intune-policies) per i dispositivi che riguardino in modo specifico la protezione avanzata delle impostazioni di sistema e l'abilitazione della crittografia. I criteri consentono anche di garantire che sono disponibili per l'installazione nei dispositivi mobili solo le [app conformi](https://technet.microsoft.com/library/dn818906.aspx), creando un elenco di accessi approvati.

Sui dispositivi BYOD che eseguono Windows 8.1 Enterprise, con AppLocker è possibile consentire o bloccare un'applicazione in base a percorso del file, hash o proprietà che vengono mantenute nei vari aggiornamenti dell'applicazione, ad esempio nome dell'autore, nome del prodotto, nome del file e versione del file. In Windows 10 è stato aggiunto un nuovo provider di servizi di configurazione AppLocker per consentire l'abilitazione delle regole di AppLocker usando un server MDM. Per altre informazioni su questa nuova funzionalità di Windows 10, vedere [CSP di AppLocker](https://msdn.microsoft.com/library/windows/hardware/dn920019(v=vs.85).aspx).

Un'altra area che deve essere controllata è l'esperienza di esplorazione degli utenti sui dispositivi mobili. Un criterio di Managed Browser include un elenco di elementi consentiti o bloccati che limita i siti Web che possono essere visitati dagli utenti del browser. Per altre informazioni su come configurare questi criteri in Intune, vedere [Gestire l'accesso a Internet usando i criteri di Managed Browser con Microsoft Intune](/intune/deployuse/manage-internet-access-using-managed-browser-policies).

In un ambiente ibrido con Configuration Manager in locale, è possibile creare una [linea di base di configurazione](https://technet.microsoft.com/library/gg712268.aspx?WT.mc_id=Blog_EntMob_Showcase_PCIT) per impostare uno stato di protezione avanzata di base per i dispositivi mobili. È possibile personalizzare la linea di base in modo da includere tutte le impostazioni necessarie e distribuirla ai dispositivi mobili. Le opzioni delle impostazioni di conformità variano in base al fornitore della piattaforma dei dispositivi mobili, pertanto per altre informazioni sulle opzioni disponibili per ogni dispositivo, vedere [Impostazioni generali per i dispositivi mobili in Configuration Manager](https://technet.microsoft.com/library/dn376523.aspx).

[MDM per Office 365](https://technet.microsoft.com/library/ms.o365.cc.devicepolicy.aspx) offre anche un set di funzionalità di supporto per la protezione avanzata dei dispositivi mobili per le categorie seguenti:

- Sicurezza
- Encryption
- Jailbroken
- Profilo e-mail gestito

Per altre informazioni sull'impostazione dei criteri di sicurezza per l'applicazione di queste opzioni, leggere l'articolo [Funzionalità di gestione dei dispositivi mobili integrate per Office 365](https://technet.microsoft.com/library/ms.o365.cc.devicepolicysupporteddevice.aspx).

La protezione avanzata della piattaforma per dispositivi mobili svolge un ruolo importante nel garantire la protezione dei dati aziendali, consentendo agli utenti di usare i dispositivi mobili senza compromettere la sicurezza. Usare la tabella riportata di seguito come riferimento per la scelta dell'opzione MDM più adatta ai requisiti aziendali di protezione avanzata dei dati.

## Intune (autonomo)

**Vantaggi**

- Consente di applicare i criteri per i dispositivi registrati: crittografia, malware, applicazioni, messaggi di posta elettronica, profilo di posta elettronica, jailbroken, sistema e sicurezza
- Supporta la distribuzione dei criteri per le principali piattaforme per dispositivi mobili, tra cui Android, iOS, Windows 10, Windows 8.x e Windows Phone

**Svantaggi**

- Non dispone dell'integrazione con la piattaforma MDM locale corrente, pertanto verrà introdotta un'interfaccia di gestione aggiuntiva da usare nell'ambito della gestione dei dispositivi mobili
- Alcuni criteri potrebbero non essere disponibili per alcune piattaforme mobili

## Gestione dei dispositivi mobili per Office 365

**Vantaggi**

- Consente di applicare i criteri per i dispositivi registrati: crittografia, applicazioni, jailbroken e sicurezza
- Supporta la distribuzione dei criteri per le principali piattaforme per dispositivi mobili, tra cui Android, iOS, Windows 10, Windows 8.x e Windows Phone

**Svantaggi**

- Non dispone dell'integrazione con la piattaforma MDM locale corrente, pertanto verrà introdotta un'interfaccia di gestione aggiuntiva da usare nell'ambito della gestione dei dispositivi mobili
- Alcuni criteri potrebbero non essere disponibili per alcune piattaforme mobili
- Non consente la stessa granularità di Intune

## Ibrida (Intune con Configuration Manager)

**Vantaggi**

- Consente di applicare i criteri per i dispositivi registrati: crittografia, malware, applicazioni, messaggi di posta elettronica, sistema, sicurezza e jailbroken
- Supporta la distribuzione dei criteri per le principali piattaforme per dispositivi mobili, tra cui Android, iOS, Windows 10, Windows 8.x e Windows Phone
- Unica console di gestione per i dispositivi mobili registrati da dispositivi locali e cloud

**Svantaggi**

- Se l'azienda attualmente non ha un'infrastruttura locale di Configuration Manager, le risorse dovranno pianificare, installare e configurare Configuration Manager prima dell'integrazione

>[!TIP] Per altre informazioni sulle impostazioni di gestione dei dispositivi mobili che è possibile configurare in un criterio di sicurezza per dispositivi mobili di Microsoft Intune, vedere [Impostazioni dei criteri di sicurezza dei dispositivi mobili in Microsoft Intune](https://technet.microsoft.com/library/dn913730.aspx). 


<!--HONumber=Apr16_HO2-->


