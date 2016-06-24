---
# required metadata

title: Considerazioni di progettazione
description:
keywords:
author: YuriDio
manager: swadhwa
ms.date: 04/28/2016
ms.topic: article
ms.prod:
ms.service:
ms.technology:
ms.assetid: 639dfd46-33ea-4cfd-918d-f3d8e57645ed

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: 
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Considerazioni di progettazione

Con un'analisi dei requisiti descritti in dettaglio nella sezione Progettazione della soluzione di infrastruttura BYOD di questo documento, è possibile selezionare i prodotti e le tecnologie appropriati per implementare i requisiti per il progetto di infrastruttura BYOD. La tabella seguente elenca i prodotti, le tecnologie e i servizi Microsoft che consentono di implementare una soluzione di infrastruttura BYOD.

I prodotti, le tecnologie e i servizi Microsoft per una soluzione di infrastruttura BYOD menzionati in questa guida sono:

## Utenti e dispositivi

- Windows Server 2012 R2
- Windows 10
- Aggiunta all'area di lavoro
- Servizio registrazione dispositivi
- Registrazione del dispositivo
- Profilo Wi-Fi
- Portale aziendale
- Protocollo HTTPS

## Protezione e accesso ai dati

- Windows Server 2012 R2
- Servizi di dominio Active Directory (AD DS)
- Active Directory di Azure (Azure AD)
- Azure Multi-Factor Authentication (Azure MFA)
- Active Directory Federation Services (ADFS)
- Controllo dinamico degli accessi
- Servizio Microsoft Rights Management
- Azure Rights Management 
- Crittografia SMB
- Single Sign-On (SSO)
- Cartelle di lavoro
- Proxy applicazione Web (WAP)

## Management

- Microsoft Intune
- Criteri di gestione dispositivi
- Infrastruttura di gestione unificata
- Cancellazione selettiva
- Distribuzione del software
- Gestione e rapporti sull'utilizzo dei punti di distribuzione
- System Center 2012 R2 Configuration Manager

## App

- Proxy applicazione Web
- VPN ad attivazione automatica
- RemoteApp
- Rapporto utilizzo copie shadow di sessione
- Riconnessione rapida
- Archiviazione di deduplicazione
- Security Development Lifecycle (SDL)
- Active Directory Federations Services (AD FS)
- Protocollo HTTPS

Le sezioni seguenti delineano il processo di progettazione ma, come indicato nella sezione Progettazione della soluzione di infrastruttura BYOD di questo documento, il processo di progettazione e di definizione dei requisiti è iterativo finché non viene completato.
Il resto della documentazione prende in esame le considerazioni di progettazione e i prodotti, le tecnologie e i servizi elencati nella tabella precedente. Quando è possibile usare più prodotti, tecnologie e servizi Microsoft per affrontare le diverse considerazioni di progettazione, ne verranno illustrati i compromessi.

Il progetto di infrastruttura per il supporto di BYOD riunisce le risposte alle domande riportate in precedenza in questo articolo, nonché le funzionalità della tecnologia e le opzioni disponibili. Il progetto illustrato in questo documento usa una tecnologia basata su Microsoft. Le considerazioni e le opzioni di progettazione possono tuttavia essere applicate a qualsiasi infrastruttura usata per adottare il modello BYOD.




<!--HONumber=Apr16_HO4-->


