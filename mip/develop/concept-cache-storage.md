---
title: Concetti-archiviazione della cache
description: Questo articolo consente di comprendere i concetti relativi all'archiviazione della cache in MIP SDK.
author: tommoser
ms.service: information-protection
ms.topic: conceptual
ms.date: 07/30/2019
ms.author: tommos
ms.openlocfilehash: 6e9e726c133f5796a2406a1cacb746fc561a6457
ms.sourcegitcommit: 6b159e050176a2cc1b308b1e4f19f52bb4ab1340
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/30/2020
ms.locfileid: "95567921"
---
# <a name="microsoft-information-protection-sdk---cache-storage"></a>Microsoft Information Protection SDK-archiviazione cache

L'SDK MIP implementa un database SQLite3 per la gestione dell'archiviazione della cache SDK. Prima della versione 1,3 di Microsoft Information Protection SDK, erano supportati solo due tipi di archiviazione dello stato della cache: su disco e in memoria. Entrambi questi tipi hanno archiviato determinati dati, in particolare le licenze per contenuto protetto e informazioni sui criteri, in testo non crittografato.

Per migliorare il comportamento di sicurezza dell'SDK, è stato aggiunto il supporto per un secondo tipo di cache su disco che usa API di crittografia specifiche della piattaforma per proteggere il database e il relativo contenuto.

L'applicazione definisce il tipo di cache quando si carica il profilo come parte `FileProfileSettings` degli `PolicyProfileSettings` oggetti, o `ProtectionProfileSettings` . Il tipo di cache è statico per la durata del profilo. Per passare a un tipo diverso di archiviazione della cache, è necessario eliminare il profilo esistente e crearne uno nuovo.

## <a name="cache-storage-types"></a>Tipi di archiviazione della cache

A partire dalla versione 1,3 dell'SDK MIP, sono disponibili i seguenti tipi di cache di archiviazione.

| Tipo            | Scopo                                                                                                                         |
| --------------- | ------------------------------------------------------------------------------------------------------------------------------- |
| InMemory        | Mantiene la cache di archiviazione in memoria nell'applicazione.                                                                       |
| OnDisk          | Archivia il database su disco nella directory fornita nell'oggetto impostazioni. Il database è archiviato in testo non crittografato.              |
| OnDiskEncrypted | Archivia il database su disco nella directory fornita nell'oggetto impostazioni. Il database viene crittografato usando le API specifiche del sistema operativo. |

Ogni **motore** generato dall'applicazione genererà una nuova chiave di crittografia.

L'archiviazione della cache viene impostata tramite uno degli oggetti impostazioni del profilo, tramite l' `mip::CacheStorageType` enumerazione.

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
| Ubuntu Linux      | 16,04 e versioni successive        | Richiede [SecretService](https://developer.gnome.org/libsecret/unstable/SecretService.html) e il `LinuxEncryptedCache` flag funzionalità. |
| Android           | Android 7,0 o versione successiva   |                                                                                                                                     |
| iOS               | Tutte le versioni supportate |                                                                                                                                     |

Sebbene l'SDK MIP supporti le altre distribuzioni di Linux, non è stato testato la crittografia della cache in RedHat Enterprise Linux, CentOS o Debian.

> [!NOTE]
> Il flag funzionalità per abilitare l'archiviazione della cache in Linux è impostato tramite `mip::MipContext::CreateWithCustomFeatureSettings()`

## <a name="cache-storage-database-tables"></a>Tabelle di database di archiviazione della cache

L'SDK MIP gestisce due database per la cache. Una è per le API di protezione e per la gestione dei dettagli sullo stato di protezione. L'altro riguarda le API per i criteri e la gestione dei dettagli dei criteri e delle informazioni sui servizi. Entrambi sono archiviati nel percorso definito nell'oggetto Settings, in **mip\mip.Policies.sqlite3** e **mip\mip.Protection.sqlite3**.

### <a name="protection-database"></a>Database di protezione

| Tabella         | Scopo                                                        | Crittografato |
| ------------- | -------------------------------------------------------------- | --------- |
| AuthInfoStore | Archivia i dettagli della richiesta di autenticazione.                       | No        |
| ConsentStore  | Archivia i risultati del consenso per ogni motore.                        | No        |
| DnsInfoStore  | Archivia i risultati della ricerca DNS per le operazioni di protezione SDK        | No        |
| EngineStore   | Archivia i dettagli del motore, l'utente associato e i dati client personalizzati | No        |
| KeyStore      | Archivia le chiavi di crittografia simmetrica per ogni motore.              | Sì       |
| LicenseStore  | Gli archivi utilizzano le informazioni sulle licenze per i dati decrittografati in precedenza.  | Sì       |
| SdInfoStore   | Archivia i risultati dell'individuazione del servizio.                              | No        |

### <a name="policy-database"></a>Database dei criteri

| Tabella           | Scopo                                                          | Crittografato |
| --------------- | ---------------------------------------------------------------- | --------- |
| KeyStore        | Archivia le chiavi di crittografia simmetrica per ogni motore.                | Sì       |
| Criteri        | Archivia le informazioni sui criteri etichetta per ogni utente.                   | Sì       |
| PoliciesUrl     | Archivia l'URL del servizio criteri di back-end per un utente specifico.             | No        |
| Sensibilità     | Archivia le regole di classificazione per un criterio utente specifico.          | Sì       |
| SensitivityUrls | Archivia l'URL del servizio criteri di riservatezza backend per un utente specifico. | No        |

## <a name="database-size-considerations"></a>Considerazioni sulle dimensioni del database

Le dimensioni del database dipendono da due fattori: la quantità di motori aggiunti alla cache e la quantità di licenze di protezione che sono state memorizzate nella cache. A partire da MIP SDK 1,3, non è disponibile alcun meccanismo per pulire la cache delle licenze in scadenza. È necessario che sia presente un processo esterno per rimuovere la cache se è più grande di quanto si desideri.

Il contributo più significativo alla crescita del database sarà la cache delle licenze di protezione. Se la memorizzazione nella cache delle licenze non è necessaria, poiché i round trip del servizio non influiscano sulle prestazioni dell'applicazione o se la cache può aumentare troppo, è possibile disabilitare la cache delle licenze. Questa operazione viene eseguita impostando `CanCacheLicenses` sull' `FileProfile::Settings` oggetto su false.

```cpp
FileProfile::Settings profileSettings(mMipContext,
    mip::CacheStorageType::OnDiskEncrypted,
    mAuthDelegate,
    std::make_shared<sample::consent::ConsentDelegateImpl>(),
    std::make_shared<FileProfileObserver>());

profileSettings.SetCanCacheLicenses(false);
```

### <a name="caching-api-engines"></a>Caching di motori API

In genere, in MIP SDK, viene creato un motore API per ogni utente che esegue un'operazione API e fornisce un'interfaccia per tutte le operazioni eseguite per conto di un'identità autenticata. Come illustrato in [concetti relativi ai profili e ai motori](concept-profile-engine-cpp.md), fileengine, PolicyEngine o ProtectionEngine hanno due stati `CREATED` e `LOADED` . Per poter eseguire operazioni SDK, è necessario creare e caricare un motore. Se un motore non è in uso, l'API memorizza nella cache il motore e lo mantiene nello `CREATED` stato più a lungo possibile a seconda delle risorse disponibili. La rispettiva classe del profilo dell'API fornisce anche un metodo `UnloadEngineAsync` per ottenere questo risultato in modo esplicito.

Ogni motore ha un identificatore univoco `id` che viene usato in tutte le operazioni di gestione del motore. L'applicazione client può fornire un ID in modo esplicito o l'SDK può generarne uno, se non è fornito dall'applicazione. Se viene fornito un identificatore univoco usando oggetti impostazioni motore al momento della creazione del motore e la memorizzazione nella cache è abilitata nel profilo API, come descritto in precedenza, è possibile usare gli stessi motori ogni volta che l'utente esegue un'operazione con l'SDK. Seguire i frammenti di codice per la creazione di un `[mip::FileEngine](./concept-profile-engine-file-engine-cpp.md#create-file-engine-settings)` , `[mip::PolicyEngine](./concept-profile-engine-policy-engine-cpp.md#implementation-create-policy-engine-settings)` .

Se non si specifica un ID di motore esistente, i round trip di servizio aggiuntivi potranno recuperare i criteri e le licenze che potrebbero essere già state memorizzate nella cache per il motore esistente. La memorizzazione nella cache dell'ID del motore alllows l'accesso offline all'SDK per ottenere informazioni decrittografate in precedenza e miglioramenti delle prestazioni generali.