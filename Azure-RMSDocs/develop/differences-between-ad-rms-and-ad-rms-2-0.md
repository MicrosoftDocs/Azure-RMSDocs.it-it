---
# required metadata

title: Vantaggi di questo SDK | Azure RMS
description: Questo argomento descrive come RMS SDK 2.1 rappresenti un significativo miglioramento rispetto l'originale Active Directory Rights Management Services SDK.
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: ee4989d6-3903-4ed2-ac62-d5692e2ef494

# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

﻿
# Vantaggi di questo SDK
Questo argomento descrive come Rights Management Services SDK 2.1 rappresenti un significativo miglioramento rispetto all'originale [Active Directory Rights Management Services SDK](https://msdn.microsoft.com/library/Cc530379) in termini di sforzo necessario per creare un'applicazione abilitata per i diritti.

**Superficie dell'API**: la superficie dell'API è stata ridotta notevolmente tramite astrazione, liberando così l'utente da molti dei dettagli di implementazione back-end. Invece di una superficie API di 84 funzioni per RMS SDK, RMS SDK 2.1 include solo 20 funzioni API. La maggior parte delle applicazioni useranno solo una piccola parte di questa superficie dell'API.

**Periodo di addestramento**: con RMS SDK 2.1, sarà possibile seguire una guida dettagliata per identificare quali risorse dell'applicazione sono riservate e come proteggerle. Questo è un netto miglioramento rispetto a RMS SDK, per cui era necessario conoscere in modo approfondito certificati, formati e topologie, nonché scrivere codici complessi per il multithreading.

**Supporto di più topologie**: RMS SDK 2.1 permette di ridurre al minimo la riscrittura del codice; l'applicazione funziona con tutte le topologie e lo sviluppatore non dovrà più occuparsi della complessità della topologia. Con RMS SDK era necessario comprendere tutte le topologie supportate, quindi scrivere e testare il codice specifico per ognuna.

**A prova di futuro**: RMS SDK 2.1 permette di ridurre al minimo la riscrittura del codice di attivazione dei diritti; l'applicazione funziona in qualsiasi ambiente RMS e usufruisce automaticamente di nuove funzionalità quando vengono rilasciate le funzionalità RMS principali aggiornate. Con ASD RMS SDK era necessario aggiornare l'applicazione per usufruire esplicitamente delle nuove funzionalità.

**Nota importante**  
Tutti gli argomenti nell'originale [Active Directory Rights Management Services SDK](https://msdn.microsoft.com/library/Cc530379) in MSDN Library ora iniziano con la seguente istruzione di supporto:

La funzionalità AD RMS SDK esposta dal client in Msdrm.dll è disponibile per l'uso in Windows Server 2008, Windows Vista, Windows Server 2008 R2, Windows 7, Windows Server 2012 e Windows 8. È possibile che in versioni successive sia stata modificata o non sia più disponibile. Usare al suo posto [Active Directory Rights Management Services SDK 2.1](microsoft-information-protection-and-control-client-portal.md), che utilizza le funzionalità esposte dal client in *Msipc.dll*.

 

## Argomenti correlati ##
* [Panoramica](ad-rms-overview.md)
* [Active Directory Rights Management Services SDK](https://msdn.microsoft.com/library/Cc530379)
* [Rights Management Services SDK 2.1](microsoft-information-protection-and-control-client-portal.md)
 

 


<!--HONumber=Apr16_HO3-->


