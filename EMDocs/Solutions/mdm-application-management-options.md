---
# required metadata

title: Opzioni di gestione delle applicazioni
description:
keywords:
author: robmazz
manager: swadhwa
ms.date: 04/28/2016
ms.topic: article
ms.prod:
ms.service:
ms.technology:
ms.assetid: 1f77eba2-8e27-4e08-b2f2-e71e3d776cf4

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: 
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Opzioni di gestione delle applicazioni

>[!NOTE]
>Questo argomento fa parte di una guida più ampia dedicata alle considerazioni di progettazione. Per leggere la guida dall'inizio, vedere l'[argomento principale](mdm-design-considerations-guide.md). Per scaricare una copia della versione integrale della guida, visitare la raccolta [TechNet](https://gallery.technet.microsoft.com/Mobile-Device-Management-7d401582).

I criteri di gestione delle applicazioni mobili (MAM) consentono di impedire la divulgazione dei dati dell'azienda alle app o ai servizi consumer sui dispositivi mobili. Questi criteri di solito vengono applicati solo per i dispositivi registrati in una soluzione di gestione dei dispositivi mobili. Intune ha ampliato le funzionalità MAM in modo da includere i dispositivi gestiti da altre soluzioni di gestione dei dispositivi mobili e i dispositivi che non sono registrati in alcun sistema di gestione.

Come illustrato nella figura seguente, se è già in uso una soluzione per la gestione dei dispositivi mobili (MDM), il software MAM di Intune consente di gestire e proteggere i dati delle applicazioni Office e Office 365 senza dover annullare la registrazione dei dispositivi dei dipendenti per registrarli nuovamente nella soluzione MDM di Intune in uno scenario di coesistenza o migrazione:

![Panoramica della separazione della gestione delle applicazioni per dispositivi mobili con i criteri del software MAM di Intune](./media/Intune_without_enrollment.png)

**Panoramica della separazione della gestione delle applicazioni per dispositivi mobili con i criteri del software MAM di Intune**

Le funzionalità di MAM di Intune non sostituiscono un'intera soluzione MDM. Il protocollo MDM è necessario per gli scenari di gestione completa dei dispositivi, come VPN, Wi-Fi, gestione dei certificati, distribuzione di applicazioni e configurazione delle impostazioni di sicurezza a livello di dispositivo.

Nelle distribuzioni ibride con Configuration Manager e Intune è possibile usare i criteri di gestione delle app per dispositivi mobili per proteggere le app su dispositivi non gestiti da Intune. Mediante questa nuova funzionalità, è possibile applicare criteri di gestione delle app mobili ad app che si connettono ai servizi di Office 365. Questa funzionalità non è supportata per le app che si connettono ai servizi locali di Exchange o SharePoint. Per usare questa funzionalità, è necessario usare il portale di anteprima di Azure.

In base alle risposte date alle domande del passaggio 1, l'utente dovrebbe essere in grado di determinare in che modo vuole che siano gestite le applicazioni nella soluzione di gestione dei dispositivi mobili. Gli elenchi riportati di seguito indicano i vantaggi e gli svantaggi di ogni opzione di gestione delle app.

## Intune (autonomo)

**Vantaggi**

- Supporta la gestione delle applicazioni sui dispositivi registrati in Intune, sui dispositivi registrati in altre soluzioni di gestione o sui dispositivi non registrati in alcuna soluzione di gestione
- Isola i dati aziendali dai dati personali degli utenti all'interno delle applicazioni con supporto predefinito per Intune Sono incluse le app di Office Mobile, le app di terze parti che hanno adottato l’SDK di Intune e le app line-of-business integrate in Intune
- Condivisione dei dati aziendali con funzioni Taglia/Copia/Incolla tra le app aziendali, impedita nelle app personali
- Criteri chiave di prevenzione della perdita di dati, come PIN per app, controlli salvataggio con nome e condivisione di dati gestiti tra app
- Supporto per queste funzionalità in Microsoft Word, Excel, PowerPoint, Outlook, OneNote e OneDrive for Business
- Gestione delle app per iOS acquistate attraverso il programma Volume Purchase Program di Apple per le aziende
- Supportato nei dispositivi Android e iOS

**Svantaggi**

- Non è supportato nel dispositivi Windows Phone

## Gestione dei dispositivi mobili per Office 365

- Non supportata attualmente

## Ibrida (Intune con Configuration Manager)

**Vantaggi**

- Tutti i vantaggi della versione autonoma di Intune

**Svantaggi**

- Richiede requisiti di configurazione aggiuntivi per la connessione di Intune all'infrastruttura di Configuration Manager locale
- Le organizzazioni che per il momento non hanno configurato un'infrastruttura di Configuration Manager dovranno pianificarla, installarla e configurarla prima dell'integrazione con Intune

Per informazioni dettagliate sulle opzioni di gestione delle applicazioni mobili, vedere la sezione relativa alla configurazione e alla distribuzione dei criteri di gestione delle applicazioni per dispositivi mobili per Intune e Configuration Manager nella console di Microsoft Intune. È importante controllare anche l'elenco delle applicazioni Microsoft che possono essere usate con i criteri di MAM di Intune, nonché l'elenco più ampio delle app dei partner compatibili di Intune.

<!--HONumber=Apr16_HO2-->


