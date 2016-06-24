---
# required metadata

title: Specificare i requisiti di privacy
description:
keywords:
author: YuriDio
manager: swadhwa
ms.date: 04/28/2016
ms.topic: article
ms.prod:
ms.service:
ms.technology:
ms.assetid: d02d3ec2-706a-4e03-977c-b7c06cbd4ebd

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: 
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Specificare i requisiti di privacy

>[!NOTE]
>Questo argomento fa parte di una guida più ampia dedicata alle considerazioni di progettazione. Per leggere la guida dall'inizio, vedere l'[argomento principale](mdm-design-considerations-guide.md). Per scaricare una copia della versione integrale della guida, visitare la raccolta [TechNet](https://gallery.technet.microsoft.com/Mobile-Device-Management-7d401582).


Nel passaggio precedente si sono definite le attività di gestione dei dispositivi, inclusa la gestione dei dispositivi e della distribuzione dei contenuti. L'obiettivo di questa attività consiste nel definire i requisiti di privacy per i contenuti aziendali presenti nel dispositivo mobile. 

>[!TIP] Per altre informazioni sulla distribuzione dei contenuti per i dispositivi mobili, leggere la soluzione Gestione semplificata per dispositivi mobili e computer in un ambiente ibrido.

I requisiti aziendali relativi a privacy e conformità variano in base al settore, alle normative applicabili e al tipo di azienda. Può essere utile, ad esempio, che la soluzione MDM consenta di eseguire inventari hardware di base, inventari software, raccolte di file e distribuzione di software su dispositivi mobili. La distribuzione di software e l'inventario hardware in genere sono supportati per impostazione predefinita. 

Tenere presente che i problemi di privacy applicabili ai computer client per l'inventario e la distribuzione di software si applicano anche ai dispositivi mobili. 

Prima di scegliere una soluzione di gestione di dispositivi mobili, considerare i propri requisiti specifici di privacy. come illustrato nell'esempio seguente:

- Privacy dei client: per consentire agli utenti di connettersi e usare le risorse aziendali con i propri dispositivi mobili, è necessario che gli utenti comprendano l'informativa sulla privacy dell'azienda e il modo in cui la stessa influisce sulla loro privacy.
    - È necessario che gli utenti leggano l'informativa sulla privacy della società e cosa dovrebbe includere?
        - In caso affermativo, la soluzione MDM prevede la possibilità di mettere a disposizione degli utenti un'informativa sulla privacy?
    - La soluzione MDM archivia nel cloud le informazioni o i dati dei dispositivi mobili degli utenti?
        - In caso affermativo, in che modo viene gestita la privacy degli utenti nel cloud? 
- Chi ha accesso ai loro dati?
- In che modo i dati vengono mantenuti privati?
- Classificazione dei dati e conformità: è importante definire cosa si intende per dati aziendali e in che modo verranno protetti. I criteri e i meccanismi per la classificazione dei dati dovrebbero essere parte del piano per garantire la privacy nell'ambito della gestione dei dispositivi mobili.
    - È possibile identificare o classificare i documenti o i dati aziendali presenti nel dispositivo mobile?
        - In caso affermativo, quali tipi di autorizzazioni o diritti relativi ai dati o ai documenti sono supportati?
    - La classificazione verrà trasmessa con i dati o i documenti, indipendentemente dal dispositivo mobile usato dall'utente?
    - Quali tipi di dati o documenti possono o non possono essere classificati?
    - I requisiti di conformità influiranno sulla scelta della piattaforma di gestione dei dispositivi mobili?
        - In caso affermativo, verificare che questi requisiti vengano specificati prima di selezionare la piattaforma di gestione dei dispositivi mobili.

Leggere l'[informativa sulla privacy di Microsoft Online Services](http://www.microsoft.com/server-cloud/products/intune-trust-center/privacy.aspx) per comprendere meglio in che modo i servizi di Microsoft Cloud, tra cui Intune, gestiscono la privacy dell'utente.

<!--HONumber=Apr16_HO2-->


