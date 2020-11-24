---
title: Autorizzazioni API richieste-Microsoft Information Protection SDK
description: Dettagli tecnici sulle autorizzazioni API necessarie per le operazioni di Microsoft Information Protection Software Development Kit.
author: Pathak-Aniket
ms.author: v-anikep
ms.date: 08/20/2020
ms.topic: conceptual
ms.service: information-protection
ms.openlocfilehash: ce44c0d8b65f477fdd7b08f34cfe2aacc890d259
ms.sourcegitcommit: 6b159e050176a2cc1b308b1e4f19f52bb4ab1340
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/30/2020
ms.locfileid: "95567926"
---
# <a name="api-permissions-for-the-microsoft-information-protection-sdk"></a>Autorizzazioni API per Microsoft Information Protection SDK

L'SDK MIP usa due servizi di Azure back-end per l'assegnazione di etichette e la protezione. Nel pannello autorizzazioni dell'app Azure Active Directory, questi servizi sono:

- Servizio Rights Management di Azure
- Servizio Microsoft Information Protection Sync

Quando si usa l'SDK MIP per l'assegnazione di etichette e la protezione, è necessario concedere le autorizzazioni dell'applicazione a una o più API. Diversi scenari di autenticazione delle applicazioni possono richiedere autorizzazioni di applicazione diverse. Per gli scenari di autenticazione delle applicazioni, vedere [scenari di autenticazione](/azure/active-directory/develop/authentication-flows-app-scenarios).

È necessario concedere il consenso dell'amministratore a livello di tenant per le autorizzazioni dell'applicazione in cui è richiesto il consenso dell'amministratore, come descritto nella [documentazione di AAD](/azure/active-directory/manage-apps/grant-admin-consent#grant-admin-consent-in-app-registrations).

## <a name="application-permissions"></a>Autorizzazioni applicazione

Le autorizzazioni dell'applicazione consentono a un'applicazione in Azure Active Directory di agire come entità personale, anziché per conto di un utente specifico.

| Servizio                         | Nome dell'autorizzazione           | Descrizione                                  | Il consenso dell'amministratore è obbligatorio |
| ------------------------------- | ------------------------- | -------------------------------------------- | ---------------------- |
| Servizio Rights Management di Azure | Content. superuser         | Leggi tutto il contenuto protetto per questo tenant   | Sì                    |
| Servizio Rights Management di Azure | Content. DelegatedReader   | Leggi il contenuto protetto per conto di un utente   | Sì                    |
| Servizio Rights Management di Azure | Content. DelegatedWriter   | Creare contenuto protetto per conto di un utente | Sì                    |
| Servizio Rights Management di Azure | Content. Writer            | Crea contenuto protetto                     | Sì                    |
| Servizio di sincronizzazione MIP                | UnifiedPolicy. tenant. Read | Leggere tutti i criteri unificati del tenant      | Sì                    |

### <a name="contentsuperuser"></a>Content. superuser

Questa autorizzazione è obbligatoria quando un'applicazione deve essere autorizzata a decrittografare tutto il contenuto protetto per il tenant specifico. Esempi di servizi che richiedono diritti utente con privilegi avanzati sono la prevenzione della perdita dei dati o i servizi di broker di sicurezza per l'accesso al cloud che devono essere in grado di visualizzare tutto il contenuto in testo non crittografato per prendere decisioni relative ai criteri in cui i dati possono essere o archiviati  

### <a name="contentdelegatedwriter"></a>Content. DelegatedWriter

Questa autorizzazione è obbligatoria quando un'applicazione deve essere autorizzata a crittografare il contenuto protetto da un utente specifico. Esempi di servizi che richiedono diritti di scrittura delegati sono applicazioni line-of-business che devono crittografare il contenuto in base ai criteri etichetta dell'utente per applicare etichette e crittografare il contenuto in modo nativo. Questa autorizzazione consente all'applicazione di crittografare il contenuto nel contesto dell'utente.

### <a name="contentdelegatedreader"></a>Content. DelegatedReader

Questa autorizzazione è obbligatoria quando un'applicazione deve essere autorizzata a decrittografare tutto il contenuto protetto per un utente specifico. Esempi di servizi che richiedono diritti di lettura delegati sono applicazioni line-of-business che devono decrittografare il contenuto in base ai criteri etichetta dell'utente per visualizzare il contenuto in modo nativo. Questa autorizzazione consente all'applicazione di decrittografare e leggere il contenuto nel contesto dell'utente.

### <a name="contentwriter"></a>Content. Writer

Questa autorizzazione è obbligatoria quando un'applicazione deve essere autorizzata a crittografare il contenuto. Esempi di servizi che richiedono writer sono applicazioni line-of-business che applicano etichette di classificazione ai file durante l'esportazione. Content. Writer crittografa il contenuto come identità dell'entità servizio e quindi il proprietario dei file protetti sarà l'identità dell'entità servizio.

### <a name="unifiedpolicytenantread"></a>UnifiedPolicy. tenant. Read

Questa autorizzazione è obbligatoria quando un'applicazione deve essere autorizzata a scaricare i criteri di assegnazione di etichette unificati per il tenant. Esempi di servizi che richiedono la lettura del tenant di criteri unificato sono applicazioni che richiedono l'uso delle etichette come identità dell'entità servizio.

## <a name="delegated-permissions"></a>Autorizzazioni delegate

Le autorizzazioni delegate consentono a un'applicazione in Azure Active Directory di eseguire azioni per conto di un determinato utente.

| Servizio                         | Nome dell'autorizzazione         | Descrizione                                      | Il consenso dell'amministratore è obbligatorio |
| ------------------------------- | ----------------------- | ------------------------------------------------ | ---------------------- |
| Servizio Rights Management di Azure | user_impersonation      | Creare e accedere al contenuto protetto per l'utente | No                     |
| Servizio di sincronizzazione MIP                | UnifiedPolicy. utente. Read | Leggi tutti i criteri unificati a cui un utente può accedere   | No                     |

### <a name="user_impersonation"></a>user_impersonation

Questa autorizzazione è obbligatoria quando un'applicazione deve essere consentita all'utente di Azure Rights Management Services per conto dell'utente. Esempi di servizi che richiedono diritti di User_Impersonation sono le applicazioni che devono crittografare o accedere al contenuto in base ai criteri etichetta dell'utente per applicare etichette o crittografare il contenuto in modo nativo.
  
### <a name="unifiedpolicyuserread"></a>UnifiedPolicy. utente. Read

Questa autorizzazione è obbligatoria quando un'applicazione deve essere autorizzata a leggere i criteri di etichetta unificata correlati a un utente. crittografare il contenuto protetto da un utente specifico. Esempi di servizi che richiedono diritti di scrittura delegati sono applicazioni che devono crittografare il contenuto in base ai criteri etichetta dell'utente per applicare etichette e crittografare il contenuto in modo nativo.