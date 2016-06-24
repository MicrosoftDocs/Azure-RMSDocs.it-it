---
# required metadata

title: Opzioni di gestione dei certificati
description:
keywords:
author: andredm7
manager: swadhwa
ms.date: 05/31/2016
ms.topic: article
ms.prod:
ms.service:
ms.technology:
ms.assetid: c3d350b5-4437-4f3d-907f-57ce6a819a74

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: 
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Opzioni di gestione dei certificati

>[!NOTE]
>Questo argomento fa parte di una guida più ampia dedicata alle considerazioni di progettazione. Per leggere la guida dall'inizio, vedere l'[argomento principale](mdm-design-considerations-guide.md). Per scaricare una copia della versione integrale della guida, visitare la raccolta [TechNet](https://gallery.technet.microsoft.com/Mobile-Device-Management-7d401582).

L'uso della gestione dei certificati digitali e dei profili dei certificati è supportato sia da [Intune](/Intune/deployuse/secure-resource-access-with-certificate-profiles) autonomo che da scenari di distribuzione [ibridi con Intune e Configuration Manager](https://technet.microsoft.com/library/dn261202.aspx). Queste funzionalità consentono di distribuire i certificati radice attendibili ai dispositivi mobili, oltre a profili basati sul protocollo SCEP (Simple Certificate Enrollment Protocol) che comunicano ai dispositivi mobili di ottenere certificati aggiuntivi da un server NDES dell'organizzazione.

Poiché il protocollo SCEP è supportato da iOS, Windows 10 e 8.1 e Windows Phone 10 e 8.1, il supporto è disponibile anche con l'app Portale aziendale di Microsoft Intune per Android. L'uso di questo protocollo di registrazione ha il vantaggio di generare la chiave privata direttamente sul dispositivo mobile. La chiave privata non viene mai generata, memorizzata nella cache o archiviata da Configuration Manager o Intune, consentendo di proteggere il dispositivo mobile.

La figura che segue illustra in che modo Intune e Configuration Manager usano NDES per eseguire in modo sicuro il provisioning dei certificati per i dispositivi mobili con SCEP:

![Provisioning sicuro dei certificati](./media/MDM_Figure_07.png)

**Provisioning sicuro dei certificati**

1. Vengono creati criteri che includono le proprietà del certificato per la registrazione SCEP sul servizio Intune.
2. Intune converte i criteri in un protocollo di gestione dei dispositivi mobili su piattaforma, ad esempio OMA-DM per Windows 10 e Windows 8.1, e li invia al dispositivo
3. Il dispositivo mobile riceve i criteri e avvia una richiesta di registrazione da NDES
4. NDES inoltra la richiesta a Configuration Manager
5. Configuration Manager confronta gli attributi della richiesta SCEP per la corrispondenza dell'autenticazione e invia una conferma a NDES.
6. NDES invia una richiesta di rilascio del certificato all'autorità di certificazione e invia il certificato al ruolo NDES.
7. Il ruolo NDES invia il certificato al dispositivo.

A seconda delle risposte alle domande nell'attività 3, si dovrebbe essere in grado di determinare in che modo si desidera gestire i certificati nella soluzione di gestione dei dispositivi mobili. MDM per Office 365 al momento non supporta la gestione dei profili dei certificati per i dispositivi mobili. 

Gli elenchi che seguono sono utili per comprendere i vantaggi e gli svantaggi della gestione dei profili dei certificati per Intune e per lo scenario di distribuzione ibrido di Intune con Configuration Manager:

## Intune (autonomo)

**Vantaggi**

- Supporta i profili dei certificati per tutti i principali sistemi operativi per dispositivi mobili (Android, iOS, Windows 10, Windows 8.x e Windows Phone)
- La piattaforma supporta il protocollo SCEP (Simple Certificate Enrollment Protocol)
- I profili dei certificati possono configurare automaticamente i dispositivi mobili in modo da poter accedere alle risorse aziendali senza dover installare manualmente i certificati o usare un processo di sicurezza non approvato
- I certificati possono essere revocati automaticamente quando il dispositivo viene ritirato dalla gestione, ne viene eseguita la cancellazione selettiva o viene bloccato dalla gerarchia di gestione

**Svantaggi**

- Per usare i profili dei certificati, è necessario che sia presente un'infrastruttura locale esistente. È necessario integrare l'infrastruttura locale seguente con Intune:
 - Un server che esegue il servizio Registrazione dispositivi di rete
 - Un'autorità di certificazione globale (enterprise)
 - Intune NDES Connector, installato nel server che esegue NDES

## Gestione dei dispositivi mobili per Office 365

- Il supporto per i profili di certificato non è previsto in MDM per Office 365.

## Ibrida (Intune con Configuration Manager)

**Vantaggi**

- Tutti i vantaggi di Intune autonomo, oltre alle funzionalità seguenti:
 - Supporta anche la gestione dei certificati per i dispositivi non mobili

**Svantaggi**

- Per usare i profili dei certificati, è necessario che sia presente un'infrastruttura locale esistente. 
- È necessario integrare l'infrastruttura locale seguente con Intune:
 - Un server che esegue il servizio Registrazione dispositivi di rete
 - Un'autorità di certificazione globale (enterprise)
 - Intune NDES Connector, installato nel server che esegue NDES

Per altre informazioni sulle opzioni di gestione dei certificati per dispositivi mobili, leggere la procedura per [abilitare i profili dei certificati](/Intune/deployuse/secure-resource-access-with-certificate-profiles) in Intune e confrontare questi requisiti e procedure con l'[abilitazione dei profili dei certificati](https://technet.microsoft.com/library/dn261202.aspx) in System Center 2012 R2 Configuration Manager.

<!--HONumber=Jun16_HO1-->


