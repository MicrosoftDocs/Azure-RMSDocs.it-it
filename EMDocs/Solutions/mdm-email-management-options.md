---
# required metadata

title: Opzioni di gestione della posta elettronica
description:
keywords:
author: robmazz
manager: swadhwa
ms.date: 04/28/2016
ms.topic: article
ms.prod:
ms.service:
ms.technology:
ms.assetid: 9b89da63-039f-4831-b204-28c0681478fe

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: 
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Opzioni di gestione della posta elettronica

>[!NOTE]
>Questo argomento fa parte di una guida più ampia dedicata alle considerazioni di progettazione. Per leggere la guida dall'inizio, vedere l'[argomento principale](mdm-design-considerations-guide.md). Per scaricare una copia della versione integrale della guida, visitare la raccolta [TechNet](https://gallery.technet.microsoft.com/Mobile-Device-Management-7d401582).

Il motivo principale per l'implementazione di una soluzione di gestione dei dispositivi mobili è solitamente concedere l'accesso gestito alla posta elettronica aziendale dai dispositivi mobili. Ad esempio, in MDM per Office 365 è possibile creare [criteri di sicurezza](https://technet.microsoft.com/library/ms.o365.cc.newdevicepolicy.aspx) che offrono l'accesso di base gestito alle cassette di posta elettronica ospitate in Exchange Online o l'accesso tramite app Office (in iOS e Android). Questi criteri consentono di applicare le impostazioni di conformità di base del dispositivo mobile, ad esempio richiedere password e crittografia del dispositivo prima che il dispositivo possa connettersi a una cassetta postale.

Si segue una procedura simile per configurare le opzioni di gestione della posta elettronica in Intune e nelle distribuzioni ibride con Intune e Configuration Manager. La differenza principale consiste nel fatto che è possibile implementare opzioni di gestione della posta elettronica più avanzate rispetto a MDM per Office 365. Ad esempio, usando Intune autonomo è possibile configurare l'accesso condizionale alla posta elettronica per consentire l'accesso alle cassette postali ospitate sia su Exchange Online che su Exchange in locale, nonché configurare profili di posta elettronica personalizzati. Intune consente di abilitare queste funzionalità usando criteri di configurazione e di conformità.  Anche le distribuzioni ibride con Intune e Configuration Manager supportano l'accesso condizionale alla posta elettronica, ma solo per le cassette postali ospitate in Exchange Online.

Nello scenario illustrato di seguito nella figura 6, l'utente ha registrato il dispositivo in Intune e sta ora tentando di accedere alla propria posta elettronica aziendale usando Office 365 o Exchange in locale. In base alle impostazioni definite dall'amministratore IT della società, Intune esegue un processo di verifica dei criteri. In questo scenario, l'accesso dell'utente viene concesso se il dispositivo è crittografato, se è impostato un passcode e se il dispositivo non è jailbroken o rooted. Se un utente cerca di accedere alla posta elettronica aziendale e il dispositivo non è registrato o non è conforme in base alle impostazioni definite dall'amministratore IT, l'utente riceverà un messaggio di posta elettronica che spiega perché l'accesso è stato bloccato, insieme a informazioni su come risolvere il problema. 

![Accesso condizionale](./media/MDM_Figure_06.png)

**Accesso condizionale**

Le risposte alle domande nel passaggio 1 aiutano a decidere in che modo verranno gestiti i dispositivi nella soluzione adottata per la gestione dei dispositivi mobili. Gli elenchi che seguono illustrano i vantaggi e gli svantaggi della gestione della posta elettronica per ogni soluzione MDM.

## Intune (autonomo)

**Vantaggi**

- Supporta la gestione della posta elettronica per tutti i principali sistemi operativi per dispositivi mobili (Android, iOS, Windows 10, Windows 8.x e Windows Phone)
- È in grado di sfruttare le applicazioni di posta elettronica native del dispositivo mobile grazie all'integrazione con Exchange ActiveSync
- Integrazione con Exchange Online con il connettore Service-to-Service per consentire il monitoraggio e la creazione di report per più piattaforme tra Intune e Office 365
- Supporta la configurazione di profili di posta elettronica per la gestione di impostazioni basate su Exchange ActiveSync nei dispositivi mobili
- Accesso condizionale alle risorse tramite posta elettronica

**Svantaggi**

- I profili di posta elettronica non sono supportati per i dispositivi mobili basati su Android

## Gestione dei dispositivi mobili per Office 365

**Vantaggi**

- Consente a Exchange ActiveSync di supportare password, crittografia, conformità dei dispositivi rooted
- Consente criteri di gestione dei dispositivi e richiede la registrazione dei dispositivi prima che venga concesso l'accesso ad app Office e OneDrive for Business (iOS e Android)
- Accesso condizionale alle risorse tramite posta elettronica

**Svantaggi**

- Non sono supportate alcune opzioni avanzate di gestione della posta elettronica 
- La distribuzione di profili di posta elettronica non è supportata (ad eccezione di iOS)

## Ibrida (Intune con Configuration Manager)

**Vantaggi**

- Connettore locale Intune per la connettività ibrida con Exchange Online
- Integrazione con Exchange ActiveSync (viene applicata l'impostazione dei criteri più rigida)
- Profili di posta elettronica
- Accesso condizionale per limitare l'accesso alla posta elettronica a Exchange Online
- Criteri di conformità per definire le regole e le impostazioni a cui il dispositivo deve essere conforme per consentire l'accesso ai servizi
- Criteri di accesso condizionale per ogni servizio, definizione di regole per gruppi di sicurezza, gruppi Intune o metodo di gestione dei dispositivi non registrati

**Svantaggi**

- Accesso gestito alla posta elettronica disponibile solo per le cassette postali ospitate in Exchange Online, non per quelle ospitate in Exchange in locale
- Il connettore Service-to-Service non deve essere configurato se si abilita l'accesso condizionale sia per Exchange Online che per Exchange in locale

Esaminare i dettagli sulle opzioni di gestione della configurazione della posta elettronica per dispositivi mobili prendendo in considerazione gli elementi seguenti:

- Intune: Come [abilitare i profili di posta elettronica](/Intune/deployuse/configure-access-to-corporate-email-using-email-profiles-with-microsoft-intune) e l'[accesso condizionale alla posta elettronica](/Intune/deployuse/restrict-access-to-email-and-o365-services-with-microsoft-intune)
- Configuration Manager: Abilitazione dei [profili di posta elettronica](https://technet.microsoft.com/library/dn554227.aspx) e dell'[accesso condizionale alla posta elettronica](https://technet.microsoft.com/library/dn919655.aspx)
- MDM per Office 365: [Funzionalità di gestione dei dispositivi mobili](https://technet.microsoft.com/library/ms.o365.cc.devicepolicysupporteddevice.aspx)

<!--HONumber=Apr16_HO2-->


