---
title: Concetti-archiviazione della cache
description: Questo articolo consente di comprendere i concetti relativi all'archiviazione della cache in MIP SDK.
author: tommoser
ms.service: information-protection
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.date: 07/30/2019
ms.author: tommos
ms.openlocfilehash: a72ae5169e4a7ee9a201876afbef0f5d33fc9b89
ms.sourcegitcommit: 474cd033de025bab280cb7a9721ac7ffc2d60b55
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/05/2019
ms.locfileid: "69893753"
---
# <a name="microsoft-information-protection-sdk---cache-storage"></a>Microsoft Information Protection SDK-archiviazione cache

L'SDK MIP implementa un database SQLite3 per la gestione dell'archiviazione della cache SDK. Prima della versione 1,3 di Microsoft Information Protection SDK, erano supportati solo due tipi di archiviazione dello stato della cache: su disco e in memoria. Entrambi questi tipi hanno archiviato determinati dati, in particolare le licenze per contenuto protetto e informazioni sui criteri, in testo non crittografato.

Per migliorare il comportamento di sicurezza dell'SDK, è stato aggiunto il supporto per un secondo tipo di cache su disco che usa API di crittografia specifiche della piattaforma per proteggere il database e il relativo contenuto.

Quando si carica il profilo come parte degli oggetti `FileProfileSettings`, `PolicyProfileSettings`o `ProtectionProfileSettings`, l'applicazione definisce il tipo di cache. Il tipo di cache è statico per la durata del profilo. Per passare a un tipo diverso di archiviazione della cache, è necessario eliminare il profilo esistente e crearne uno nuovo.

## <a name="cache-storage-types"></a>Tipi di archiviazione della cache

A partire dalla versione 1,3 dell'SDK MIP, sono disponibili i seguenti tipi di cache di archiviazione.

| Type            | Scopo                                                                                                                         |
| --------------- | ------------------------------------------------------------------------------------------------------------------------------- |
| InMemory        | Mantiene la cache di archiviazione in memoria nell'applicazione.                                                                       |
| OnDisk          | Archivia il database su disco nella directory fornita nell'oggetto impostazioni. Il database è archiviato in testo non crittografato.              |
| OnDiskEncrypted | Archivia il database su disco nella directory fornita nell'oggetto impostazioni. Il database viene crittografato usando le API specifiche del sistema operativo. |

Ogni **motore** generato dall'applicazione genererà una nuova chiave di crittografia.

L'archiviazione della cache viene impostata tramite uno degli oggetti impostazioni del profilo, tramite il `mip::CacheStorageType` enum.

```cpp 
FileProfile::Settings profileSettings(mMipContext,
    mip::CacheStorageType::OnDiskEncrypted, // Define the storage type to use.
    mAuthDelegate,
    std::make_shared<sample::consent::ConsentDelegateImpl>(),
    std::make_shared<FileProfileObserver>());
```

## <a name="when-to-use-each-type"></a>Quando usare ogni tipo

L'archiviazione della cache è importante per la gestione dell'accesso offline alle informazioni decrittografate in precedenza, oltre a garantire prestazioni per le operazioni di decrittografia quando i dati sono stati utilizzati in precedenza.

- **Archiviazione in memoria**: usare questo tipo di archiviazione per i processi di lunga durata, in cui non è necessario salvare le informazioni relative al criterio o alla cache delle licenze tra i riavvii del servizio.
- **Su disco**: usare questo tipo di archiviazione per le applicazioni in cui i processi possono essere arrestati e avviati di frequente, ma devono gestire i criteri, la licenza e la cache di individuazione dei servizi tra i riavvii. Questo tipo di cache di archiviazione è di testo non crittografato, quindi è più adatto per i carichi di lavoro del server in cui gli utenti non avranno accesso all'archiviazione dello stato. Ad esempio un servizio Windows o un daemon Linux in esecuzione su un server o un'applicazione SaaS in cui solo gli amministratori del servizio possono accedere ai dati di stato.
- **Su disco e crittografato**: usare questo tipo di archiviazione per le applicazioni in cui i processi possono essere arrestati e avviati di frequente, ma devono gestire i criteri, la licenza e la cache di individuazione dei servizi nei riavvii. Questa cache di archiviazione è crittografata, quindi è più adatta per le applicazioni workstation in cui un utente può esplorare e individuare il database di stato. La crittografia contribuisce a garantire che gli utenti non abbiano accesso a tramite il contenuto del criterio o il contenuto della licenza di protezione in testo normale. È importante notare che, in tutti i casi, i dati vengono crittografati con chiavi a cui l'utente potrebbe essere in grado di accedere. Un avversario esperto sarà in grado di decrittografare la cache con il minimo sforzo, ma ciò impedisce la manomissione e l'esplorazione.

## <a name="supported-platforms-for-encryption"></a>Piattaforme supportate per la crittografia

| Piattaforma          | Versione                | Note                                                                                                                               |
| ----------------- | ---------------------- | ----------------------------------------------------------------------------------------------------------------------------------- |
| Microsoft Windows | Windows 8 e versioni successive    | Windows 7 supporta solo CacheStorageType:: ondisk                                                                                    |
| macOS             | High Sierra e versioni successive  |                                                                                                                                     |
| Ubuntu Linux      | 16,04 e versioni successive        | Richiede [SecretService](https://developer.gnome.org/libsecret/unstable/SecretService.html) e il flag della funzionalità `LinuxEncryptedCache`. |
| Android           | Android 7,0 o versione successiva   |                                                                                                                                     |
| iOS               | Tutte le versioni supportate |                                                                                                                                     |

Sebbene l'SDK MIP supporti le altre distribuzioni di Linux, non è stato testato la crittografia della cache in RedHat Enterprise Linux, CentOS o Debian.

> [!NOTE]
> Il flag funzionalità per abilitare l'archiviazione della cache in Linux è impostato tramite `mip::MipContext::CreateWithCustomFeatureSettings()`

## <a name="cache-storage-database-tables"></a>Tabelle di database di archiviazione della cache

L'SDK MIP gestisce due database per la cache. Una è per le API di protezione e per la gestione dei dettagli sullo stato di protezione. L'altro riguarda le API per i criteri e la gestione dei dettagli dei criteri e delle informazioni sui servizi. Entrambi sono archiviati nel percorso definito nell'oggetto Settings, in **mip\mip.Policies.sqlite3** e **mip\mip.Protection.sqlite3**.

### <a name="protection-database"></a>Database di protezione

| Table         | Scopo                                                        | Crittografato |
| ------------- | -------------------------------------------------------------- | --------- |
| AuthInfoStore | Archivia i dettagli della richiesta di autenticazione.                       | No        |
| ConsentStore  | Archivia i risultati del consenso per ogni motore.                        | No        |
| DnsInfoStore  | Archivia i risultati della ricerca DNS per le operazioni di protezione SDK        | No        |
| EngineStore   | Archivia i dettagli del motore, l'utente associato e i dati client personalizzati | No        |
| KeyStore      | Archivia le chiavi di crittografia simmetrica per ogni motore.              | Yes       |
| LicenseStore  | Gli archivi utilizzano le informazioni sulle licenze per i dati decrittografati in precedenza.  | Yes       |
| SdInfoStore   | Archivia i risultati dell'individuazione del servizio.                              | No        |

### <a name="policy-database"></a>Database dei criteri

| Table           | Scopo                                                          | Crittografato |
| --------------- | ---------------------------------------------------------------- | --------- |
| KeyStore        | Archivia le chiavi di crittografia simmetrica per ogni motore.                | Yes       |
| Criteri        | Archivia le informazioni sui criteri etichetta per ogni utente.                   | Yes       |
| PoliciesUrl     | Archivia l'URL del servizio criteri di back-end per un utente specifico.             | No        |
| Sensibilità     | Archivia le regole di classificazione per un criterio utente specifico.          | Yes       |
| SensitivityUrls | Archivia l'URL del servizio criteri di riservatezza backend per un utente specifico. | No        |

## <a name="database-size-considerations"></a>Considerazioni sulle dimensioni del database

Le dimensioni del database dipendono da due fattori: la quantità di motori aggiunti alla cache e la quantità di licenze di protezione che sono state memorizzate nella cache. A partire da MIP SDK 1,3, non è disponibile alcun meccanismo per pulire la cache delle licenze in scadenza. È necessario che sia presente un processo esterno per rimuovere la cache se è più grande di quanto si desideri.

Il contributo più significativo alla crescita del database sarà la cache delle licenze di protezione. Se la memorizzazione nella cache delle licenze non è necessaria, poiché i round trip del servizio non influiscano sulle prestazioni dell'applicazione o se la cache può aumentare troppo, è possibile disabilitare la cache delle licenze. Questa operazione viene eseguita impostando `CanCacheLicenses` sull'oggetto `FileProfile::Settings` su false.

```cpp
FileProfile::Settings profileSettings(mMipContext,
    mip::CacheStorageType::OnDiskEncrypted,
    mAuthDelegate,
    std::make_shared<sample::consent::ConsentDelegateImpl>(),
    std::make_shared<FileProfileObserver>());

profileSettings.SetCanCacheLicenses(false);
```
