---
# required metadata

title: Raccogliere informazioni sui requisiti di protezione dei dati
description:
keywords:
author: YuriDio
manager: swadhwa
ms.date: 04/28/2016
ms.topic: article
ms.prod:
ms.service:
ms.technology:
ms.assetid: 98f7bd00-4be7-478e-82ea-6046813f1556

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: 
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Raccogliere informazioni sui requisiti di protezione dei dati

>[!NOTE]
>Questo argomento fa parte di una guida più ampia dedicata alle considerazioni di progettazione. Per leggere la guida dall'inizio, vedere l'[argomento principale](mdm-design-considerations-guide.md). Per scaricare una copia della versione integrale della guida, visitare la raccolta [TechNet](https://gallery.technet.microsoft.com/Mobile-Device-Management-7d401582).

Per definire i requisiti di protezione dei dati dell'organizzazione per i dispositivi mobili, è utile valutare i requisiti di protezione dei dati già presenti nell'organizzazione. È probabile che la società debba ad esempio conformarsi a specifiche normative o che disponga già di una politica di protezione dei dati. 

Prendere nota innanzitutto di questi requisiti di alto livello in modo da poter porre domande più granulari che consentano di prendere decisioni di progettazione appropriate per la soluzione MDM.  Quando si definiscono questi requisiti, considerare quanto segue:

- Crittografia dei dati inattivi: come illustrato nella Figura 8, i dati aziendali verranno archiviati nel dispositivo mobile dell'utente. Stabilire se gli elementi seguenti sono importanti per la società: 
    - La soluzione MDM supporta la crittografia dell'intero disco e delle schede SD del dispositivo mobile?
        - In caso affermativo, per quali sistemi operativi?
    - La soluzione MDM supporta la crittografia dei dati dell'app?
        - In caso affermativo, per quali sistemi operativi?
        - In caso affermativo, per quali app?
- Crittografia dei dati in transito: indipendentemente dal proprietario dei dati, in un determinato momento durante la comunicazione i dati sono in transito tra il dispositivo mobile e un server aziendale (o un servizio Web). È necessario comprendere quali funzionalità sono disponibili nella soluzione MDM per la protezione dei dati in transito. Stabilire se gli elementi seguenti sono importanti per la società: 
    - La soluzione MDM supporta la crittografia dei dati in transito?
        - In caso affermativo, per quali sistemi operativi?
        - In caso affermativo, quali funzionalità sono disponibili?
    - Quali opzioni usa la soluzione MDM per proteggere i dati in transito?
- Separazione dei dati: è anche importante capire se i dati aziendali devono essere trattati in modo diverso dai dati dell'utente. Separazione o isolamento sono alcuni dei termini usati per descrivere questa funzionalità. Quando si progetta la soluzione MDM, considerare quanto segue:
    - La soluzione MDM supporta la separazione dei dati?
        - In caso affermativo, è possibile cancellare i dati aziendali, mantenendo i dati dell'utente del dispositivo mobile?
    - La funzionalità MDM di separazione dei dati garantisce che solo le app attendibili possano accedere ai dati che si trovano nel dispositivo mobile?
    - La soluzione MDM supporta la separazione dei dati in base all'identità dell'utente?
    - La soluzione MDM supporta la containerizzazione?
        - In caso affermativo, è possibile crittografare i dati che si trovano in un determinato contenitore?
- Protezione avanzata dei dispositivi mobili: l'organizzazione potrebbe usare diverse piattaforme per dispositivi mobili, quindi è necessario sapere quali funzionalità di protezione avanzata sono disponibili in ogni piattaforma per dispositivi mobili. Ogni piattaforma per dispositivi mobili può controllare e proteggere i dispositivi in modo avanzato con metodi diversi e a livelli diversi di granularità. Se un set di dispositivi mobili dispone di un set di configurazione più granulare rispetto ad altri, sarà necessario un set di opzioni comuni per la protezione avanzata dei dispositivi durante l'uso di criteri personalizzati per migliorare la sicurezza di ogni piattaforma per dispositivi mobili supportata dall'organizzazione. 

L'elenco seguente include le opzioni comuni che devono essere supportate dalla soluzione MDM per la protezione avanzata dei dispositivi mobili:

- Obbligo di una password per sbloccare i dispositivi mobili
- Obbligo di un tipo di password: numero minimo di caratteri e tipi di caratteri
- Lunghezza minima password
- Numero di errori di accesso ripetuti consentiti prima della cancellazione del dispositivo mobile
- Minuti di inattività prima dello spegnimento dello schermo del dispositivo
- Memorizzazione della cronologia delle password per impedire il riutilizzo delle password precedenti
- Scadenza password (giorni)
- Obbligo di crittografia nel dispositivo mobile
- Obbligo di crittografia nelle schede di memoria
- Restituzione inattiva senza password consentita

>[!TIP] In Windows Phone 8.1, il criterio che consente la restituzione inattiva senza password può essere configurato usando [Windows Phone 8.1 Enterprise Device Management Protocol](http://download.microsoft.com/download/C/A/0/CA091018-1A43-4063-B70B-20B9901F4D10/Windows Phone 8.1 MDM Protocol.pdf).

<!--HONumber=Apr16_HO2-->


