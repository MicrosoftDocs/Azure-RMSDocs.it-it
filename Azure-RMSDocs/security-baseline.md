---
title: Baseline della sicurezza di Azure per Azure Information Protection
description: La linea di base di sicurezza Azure Information Protection fornisce indicazioni e risorse procedurali per l'implementazione delle raccomandazioni di sicurezza specificate nel benchmark di sicurezza di Azure.
author: msmbaldwin
ms.service: information-protection
ms.topic: conceptual
ms.date: 11/18/2020
ms.author: mbaldwin
ms.custom: subject-security-benchmark
ms.openlocfilehash: cddb3ad6bd23a58922a87d27dcd6a0a1e82bd312
ms.sourcegitcommit: 173f46dd5f14c27911faec737be5986a33407477
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/18/2020
ms.locfileid: "95568545"
---
# <a name="azure-security-baseline-for-azure-information-protection"></a>Baseline della sicurezza di Azure per Azure Information Protection

Questa linea di base di sicurezza applica le indicazioni della [versione 2,0 del benchmark di sicurezza di Azure](https://docs.microsoft.com/azure/security/benchmarks/overview) a Azure Information Protection. Azure Security Benchmark offre consigli sulla protezione delle soluzioni cloud in Azure. Il contenuto viene raggruppato in base ai **controlli di sicurezza** definiti dal benchmark di sicurezza di Azure e alle linee guida correlate applicabili a Azure Information Protection. I **controlli** non applicabili ai Azure Information Protection sono stati esclusi.

Per informazioni su come Azure Information Protection viene eseguito il mapping completo al benchmark di sicurezza di Azure, vedere il [file di mapping di base Azure Information Protection sicurezza completo](https://github.com/MicrosoftDocs/SecurityBenchmarks/tree/master/Azure%20Offer%20Security%20Baselines).

## <a name="network-security"></a>Sicurezza di rete

*Per altre informazioni, vedere [benchmark di sicurezza di Azure: sicurezza di rete](/azure/security/benchmarks/security-controls-v2-network-security).*

### <a name="ns-6-simplify-network-security-rules"></a>NS-6: semplificare le regole di sicurezza di rete

**Linee guida**: usare i tag del servizio di rete virtuale per definire i controlli di accesso alla rete nei gruppi di sicurezza di rete o nel firewall di Azure, configurato per le risorse Azure Information Protection. 

Quando si creano regole di sicurezza, usare i tag del servizio al posto di indirizzi IP specifici. Specificare il nome del tag di servizio, ad esempio {AzureInformationProtection}, nel campo di origine o di destinazione appropriato di una regola per consentire o negare il traffico per il servizio corrispondente.

I prefissi di indirizzo inclusi nel tag di servizio sono gestiti da Microsoft, che aggiorna automaticamente il tag in caso di modifica degli indirizzi.

- [Comprendere e usare i tag di servizio](https://docs.microsoft.com/azure/virtual-network/service-tags-overview)

- [Tag del servizio Azure Information Protection](https://docs.microsoft.com/azure/information-protection/requirements#service-tags)

**Monitoraggio del Centro sicurezza di Azure**: Non applicabile

**Responsabilità**: Customer

## <a name="identity-management"></a>Identity Management

*Per altre informazioni, vedere [benchmark di sicurezza di Azure: gestione delle identità](/azure/security/benchmarks/security-controls-v2-identity-management).*

### <a name="im-1-standardize-azure-active-directory-as-the-central-identity-and-authentication-system"></a>IM-1: standardizzare Azure Active Directory come sistema di autenticazione e identità centrale

**Linee guida**: Azure Information Protection è integrato con Azure Active Directory (Azure ad), ovvero il servizio di gestione delle identità e degli accessi predefinito di Azure. Renderla prioritaria per la sicurezza del Azure AD nella procedura di sicurezza del cloud dell'organizzazione. 

Esaminare il Punteggio sicuro di identità Azure AD per valutare la postura di sicurezza delle identità rispetto alle procedure consigliate di Microsoft. Usare il punteggio per misurare la precisione con cui la configurazione corrisponde ai consigli delle procedure consigliate e per apportare miglioramenti in termini di sicurezza.

Standardizzare Azure AD per gestire la gestione delle identità e degli accessi dell'organizzazione in:

- Microsoft Cloud risorse, ad esempio portale di Azure, archiviazione di Azure, macchine virtuali di Azure (Linux e Windows), Azure Key Vault, piattaforma distribuita come servizio (PaaS) e applicazioni SaaS (software as a Service)

- Le risorse dell'organizzazione, ad esempio le applicazioni in Azure o le risorse della rete aziendale

Azure AD supporta le identità esterne per consentire agli utenti senza account Microsoft di accedere alle applicazioni e alle risorse con gli account non Microsoft.

- [Tenancy in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/develop/single-and-multi-tenant-apps)

- [Come creare e configurare un'istanza di Azure AD](https://docs.microsoft.com/azure/active-directory/fundamentals/active-directory-access-create-new-tenant)

- [USA provider di identità esterni per l'applicazione](https://docs.microsoft.com/azure/active-directory/b2b/identity-providers)

- [Qual è il Punteggio di sicurezza identità in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/fundamentals/identity-secure-score)

**Monitoraggio del Centro sicurezza di Azure**: Non applicabile

**Responsabilità**: Customer

### <a name="im-2-manage-application-identities-securely-and-automatically"></a>IM-2: gestire le identità dell'applicazione in modo sicuro e automatico

**Linee guida**: Azure Information Protection è integrato con Azure Active Directory (Azure ad), ovvero il servizio di gestione delle identità e degli accessi di Azure. Il servizio Rights Management di Azure usa un'identità dell'applicazione Azure AD durante l'accesso alle chiavi dei clienti archiviati con scenari di Azure Key Vault per Bring Your Own Key (BYOK). L'autorizzazione del servizio Rights Management di Azure per accedere alle chiavi viene eseguita tramite la configurazione dei criteri di accesso Azure Key Vault, che possono essere eseguiti usando la portale di Azure o PowerShell.

- [Autorizzazione del servizio Azure Rights Management per BYOK](https://docs.microsoft.com/azure/information-protection/byok-price-restrictions#authorizing-the-azure-rights-management-service-to-use-your-key)

**Monitoraggio del Centro sicurezza di Azure**: Non applicabile

**Responsabilità**: Customer

### <a name="im-3-use-azure-ad-single-sign-on-sso-for-application-access"></a>IM-3: usare Azure AD Single Sign-On (SSO) per l'accesso alle applicazioni

**Linee guida**: Azure Information Protection è integrato con Azure Active Directory (Azure ad), ovvero il servizio di gestione delle identità e degli accessi predefinito di Azure. 

Azure Information Protection USA Azure AD per fornire la gestione delle identità e dell'accesso alle risorse di Azure, alle applicazioni cloud e alle applicazioni locali. Sono incluse le identità aziendali, ad esempio i dipendenti, nonché le identità esterne come partner, fornitori e fornitori. Questo consente Single Sign-On di gestire e proteggere l'accesso ai dati e alle risorse dell'organizzazione in locale e nel cloud. Connetti tutti i tuoi utenti, le tue applicazioni e i tuoi dispositivi alla Azure AD per un accesso sicuro e sicuro e una maggiore visibilità e controllo.

- [Accedere a Azure Information Protection con Azure Active Directory](https://docs.microsoft.com/azure/information-protection/requirements)

**Monitoraggio del Centro sicurezza di Azure**: Non applicabile

**Responsabilità**: Customer

### <a name="im-4-use-strong-authentication-controls-for-all-azure-active-directory-based-access"></a>IM-4: usare controlli di autenticazione avanzata per tutti gli accessi in base al Azure Active Directory

**Linee guida**: Azure Information Protection è integrato con Azure Active Directory (Azure ad), che supporta l'autenticazione avanzata tramite l'autenticazione a più fattori. Per supportare l'autenticazione e l'autorizzazione per Azure Information Protection, è necessario disporre di un Azure AD. Per usare gli account utente dalla directory locale (AD DS), è necessario anche configurare l'integrazione delle directory.

- Single Sign-on è supportato per Azure Information Protection, in modo che agli utenti non vengano richieste ripetutamente le credenziali. Se si usa la soluzione di un altro fornitore per la federazione, verificare con il fornitore come configurarla per Azure AD. WS-Trust è un requisito comune per queste soluzioni per il supporto di Single Sign-On.

- L'autenticazione a più fattori è supportata con Azure Information Protection, quando si dispone del software client richiesto e l'infrastruttura di supporto per l'autenticazione a più fattori è stata configurata correttamente.

Per altre informazioni, vedere i riferimenti seguenti:

- [Autenticazione Azure Information Protection tramite Azure Active Directory](https://docs.microsoft.com/azure/information-protection/requirements)

**Monitoraggio del Centro sicurezza di Azure**: Sì

**Responsabilità**: Customer

### <a name="im-5-monitor-and-alert-on-account-anomalies"></a>IM-5: monitoraggio e avviso per le anomalie degli account

**Linee guida**: Azure Information Protection è integrato con Azure Active Directory (Azure ad), ovvero il servizio di gestione delle identità e degli accessi predefinito di Azure. 

Informazioni aggiuntive relative a Azure AD:

- Accesso: il report di accesso fornisce informazioni sull'utilizzo delle applicazioni gestite e delle attività di accesso degli utenti.
- Log di controllo: i log consentono la tracciabilità di tutte le modifiche apportate da varie funzionalità all'interno di Azure AD. Esempi di log di controllo includono le modifiche apportate alle risorse all'interno Azure AD, ad esempio l'aggiunta o la rimozione di utenti, app, gruppi, ruoli e criteri.
- Accesso rischioso: un accesso rischioso è un indicatore di un tentativo di accesso che potrebbe essere stato eseguito da un utente che non è il legittimo proprietario di un account utente.
- Utenti contrassegnati per il rischio. Un utente rischioso è indicativo di un account utente che potrebbe essere stato compromesso.
Queste origini dati possono essere integrate con monitoraggio di Azure, Azure Sentinel o sistemi SIEM di terze parti.

Il Centro sicurezza di Azure può anche inviare avvisi su determinate attività sospette, ad esempio un numero eccessivo di tentativi di autenticazione non riusciti o account deprecati nella sottoscrizione.

Azure Advanced Threat Protection (ATP) è una soluzione di sicurezza che può usare Active Directory segnali per identificare, rilevare ed esaminare minacce avanzate, identità compromesse e azioni Insider dannose.

- [Report delle attività di controllo nell'Azure Active Directory](https://docs.microsoft.com/azure/active-directory/reports-monitoring/concept-audit-logs) 

- [Come visualizzare gli accessi a rischio per Azure AD](https://docs.microsoft.com/azure/active-directory/reports-monitoring/concept-risky-sign-ins) 

- [Come identificare gli utenti di Azure AD contrassegnati per le attività rischiose](https://docs.microsoft.com/azure/active-directory/reports-monitoring/concept-user-at-risk) 

- [Come monitorare l'identità e le attività di accesso degli utenti nel Centro sicurezza di Azure](https://docs.microsoft.com/azure/security-center/security-center-identity-access) 

- [Avvisi nel modulo di protezione dalle minacce per il Centro sicurezza di Azure](https://docs.microsoft.com//azure/security-center/alerts-reference) 

- [Come integrare i log attività di Azure in Monitoraggio di Azure](https://docs.microsoft.com/azure/active-directory/reports-monitoring/howto-integrate-activity-logs-with-log-analytics)

**Monitoraggio del Centro sicurezza di Azure**: Non applicabile

**Responsabilità**: Customer

### <a name="im-6-restrict-azure-resource-access-based-on-conditions"></a>IM-6: limitare l'accesso alle risorse di Azure in base alle condizioni

**Linee guida**: Azure Information Protection è integrato con Azure Active Directory (Azure ad), ovvero il servizio di gestione delle identità e degli accessi predefinito di Azure. In Azure AD configurare l'accesso condizionale per Azure Information Protection. Gli amministratori possono bloccare o concedere l'accesso agli utenti nel tenant, per i documenti protetti da Azure Information Protection, in base ai controlli di accesso condizionale standard.

L'autenticazione a più fattori è una delle condizioni più comunemente richieste, mentre Device-compliancy con i criteri di Intune configurati ne è un'altra. È possibile richiedere condizioni in modo che i dispositivi mobili soddisfino i requisiti di password aziendali, dispongano di una versione minima del sistema operativo e i computer connessi siano aggiunti a un dominio.

- [Criteri di accesso condizionale per Azure Information Protection](https://cloudblogs.microsoft.com/enterprisemobility/2017/10/17/conditional-access-policies-for-azure-information-protection)

**Monitoraggio del Centro sicurezza di Azure**: Non applicabile

**Responsabilità**: Customer

## <a name="privileged-access"></a>Accesso con privilegi

*Per altre informazioni, vedere [benchmark di sicurezza di Azure: accesso con privilegi](/azure/security/benchmarks/security-controls-v2-privileged-access).*

### <a name="pa-1-protect-and-limit-highly-privileged-users"></a>PA-1: proteggere e limitare gli utenti con privilegi elevati

**Linee guida**: Azure Information Protection è integrato con Azure Active Directory (Azure ad), ovvero il servizio di gestione delle identità e degli accessi predefinito di Azure. 

Azure Information Protection include un ruolo a livello di amministratore nel Azure AD. Gli utenti assegnati al ruolo amministratore hanno autorizzazioni complete nel servizio Azure Information Protection. È possibile utilizzare il ruolo amministratore per configurare le etichette per i criteri di Azure Information Protection, gestire i modelli di protezione e attivare la protezione. Tuttavia, il ruolo di amministratore non concede alcuna autorizzazione in Identity Protection Center, Privileged Identity Management, monitoraggio Microsoft 365 integrità del servizio o Office 365 Security &amp; Compliance Center.

Limitare il numero di account o ruoli con privilegi elevati e proteggere questi account a un livello elevato, in quanto gli utenti con questo privilegio possono leggere e modificare direttamente o indirettamente tutte le risorse nell'ambiente Azure. Abilitare l'accesso con privilegi JIT (just-in-Time) alle risorse di Azure e Azure AD usando Privileged Identity Management (PIM). L'accesso JIT concede le autorizzazioni temporanee per eseguire attività con privilegi solo quando gli utenti lo richiedono. PIM può inoltre generare avvisi di sicurezza in caso di attività sospette o non sicure nell'organizzazione Azure AD.

- [Ruolo amministratore Azure Information Protection](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-assign-admin-roles#azure-information-protection-administrator)

- [Autorizzazioni del ruolo amministratore in Azure AD](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-assign-admin-roles)

- [Usare gli avvisi di sicurezza di Azure Privileged Identity Management](https://docs.microsoft.com/azure/active-directory/privileged-identity-management/pim-how-to-configure-security-alerts) 

- [Protezione dell'accesso con privilegi per le distribuzioni ibride e cloud in Azure AD](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-admin-roles-secure)

**Monitoraggio del Centro sicurezza di Azure**: Non applicabile

**Responsabilità**: Customer

### <a name="pa-2-restrict-administrative-access-to-business-critical-systems"></a>PA-2: limitare l'accesso amministrativo ai sistemi aziendali critici

**Linee guida**: Azure Information Protection è integrato con Azure Active Directory (Azure ad), ovvero il servizio di gestione delle identità e degli accessi predefinito di Azure. 

Azure Information Protection include un ruolo a livello di amministratore nel Azure AD. Gli utenti assegnati al ruolo amministratore hanno autorizzazioni complete nel servizio Azure Information Protection. Il ruolo amministratore consente la configurazione delle etichette per i criteri di Azure Information Protection, la gestione dei modelli di protezione e l'attivazione della protezione. Il ruolo amministratore non concede alcuna autorizzazione in Identity Protection Center, Privileged Identity Management, monitoraggio Microsoft 365 integrità del servizio o centro conformità sicurezza di Office 365 &amp; .

- [Ruolo amministratore Azure Information Protection](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-assign-admin-roles#azure-information-protection-administrator)

- [Azioni che Azure Information Protection amministratore possono eseguire](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-assign-admin-roles#azure-information-protection-administrator-permissions)

**Monitoraggio del Centro sicurezza di Azure**: Non applicabile

**Responsabilità**: Customer

### <a name="pa-3-review-and-reconcile-user-access-regularly"></a>PA-3: rivedere e riconciliare regolarmente l'accesso utente

**Linee guida**: Azure Information Protection è integrato con Azure Active Directory (Azure ad), ovvero il servizio di gestione delle identità e degli accessi predefinito di Azure.

Usare Azure AD per gestire le risorse, verificare gli account utente e accedere regolarmente alle assegnazioni per assicurarsi che gli account e i relativi accessi siano validi. Eseguire verifiche di accesso Azure AD per verificare l'appartenenza a gruppi, l'accesso alle applicazioni aziendali e le assegnazioni di ruolo. Individuare gli account obsoleti con Azure AD Reporting. È possibile usare le funzionalità di Privileged Identity Management di Azure AD per creare il flusso di lavoro di verifica di accesso per facilitare il processo di revisione.

Inoltre, Azure Privileged Identity Management può anche essere configurato in modo da avvisare quando viene creato un numero eccessivo di account amministratore e identificare gli account amministratore non aggiornati o non configurati correttamente. Si noti che alcuni servizi di Azure supportano utenti e ruoli locali che non sono gestiti tramite Azure AD. I clienti dovranno gestire questi utenti separatamente.

- [Ruolo amministratore Azure Information Protection](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-assign-admin-roles#azure-information-protection-administrator)

- [Azioni che Azure Information Protection amministratore possono eseguire](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-assign-admin-roles#azure-information-protection-administrator-permissions)

- [Creare una verifica di accesso dei ruoli delle risorse di Azure in Privileged Identity Management (PIM)](https://docs.microsoft.com/azure/active-directory/privileged-identity-management/pim-resource-roles-start-access-review) 

- [Come usare Azure AD le verifiche di identità e accesso](https://docs.microsoft.com/azure/active-directory/governance/access-reviews-overvie)

**Monitoraggio del Centro sicurezza di Azure**: Non applicabile

**Responsabilità**: Customer

### <a name="pa-4-set-up-emergency-access-in-azure-ad"></a>PA-4: configurare l'accesso di emergenza in Azure AD

**Linee guida**: Azure Information Protection è integrato con Azure Active Directory (Azure ad) per gestire le proprie risorse. Per evitare che vengano accidentalmente bloccati dall'organizzazione Azure AD, configurare un account di accesso di emergenza per l'accesso quando non è possibile usare gli account amministrativi normali. Gli account di accesso di emergenza sono in genere con privilegi elevati e non devono essere assegnati a utenti specifici. Gli account di accesso di emergenza sono limitati a scenari di emergenza critici, in cui non è possibile usare i normali account amministrativi.

È necessario assicurarsi che le credenziali (ad esempio password, certificato o smart card) per gli account di accesso di emergenza vengano mantenute sicure e note solo a singoli utenti autorizzati a utilizzarle solo in caso di emergenza.

- [Gestire gli account di accesso di emergenza in Azure AD](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-emergency-access)

**Monitoraggio del Centro sicurezza di Azure**: Non applicabile

**Responsabilità**: Customer

### <a name="pa-5-automate-entitlement-management"></a>PA-5: automatizzare la gestione dei diritti 

**Linee guida**: Azure Information Protection è integrato con Azure Active Directory (Azure ad), il servizio di gestione delle identità e degli accessi predefinito di Azure.

Azure AD offre funzionalità di gestione dei diritti per automatizzare i flussi di lavoro delle richieste di accesso, incluse le assegnazioni di accesso, le verifiche e la scadenza. È supportata anche l'approvazione con due o più fasi.

- [Informazioni sulle verifiche di accesso Azure AD](https://docs.microsoft.com/azure/active-directory/governance/access-reviews-overview) 

- [Informazioni sulla gestione dei diritti Azure AD](https://docs.microsoft.com/azure/active-directory/governance/entitlement-management-overview)

**Monitoraggio del Centro sicurezza di Azure**: Non applicabile

**Responsabilità**: Customer

### <a name="pa-6-use-privileged-access-workstations"></a>PA-6: usare workstation con accesso con privilegi

**Linee guida**: Azure Information Protection possono essere gestite da una workstation del cliente tramite PowerShell. 

Le workstation protette e isolate sono di fondamentale importanza per la sicurezza dei ruoli sensibili, ad esempio amministratori, sviluppatori e operatori di servizi critici. 

Usare workstation utente altamente sicure e/o un bastione di Azure per le attività amministrative. Usare Azure Active Directory, Microsoft Defender Advanced Threat Protection (ATP) e/o Microsoft Intune per distribuire una workstation utente protetta e gestita per le attività amministrative. Le workstation protette possono essere gestite centralmente per applicare la configurazione protetta, tra cui l'autenticazione avanzata, le linee di base software e hardware e l'accesso logico e di rete limitato.

- [Indicazioni sull'uso di PowerShell per Azure Information Protection](https://docs.microsoft.com/azure/information-protection/rms-client/client-admin-guide-powershell)

- [Informazioni sulle workstation con accesso con privilegi](https://docs.microsoft.com/azure/active-directory/devices/concept-azure-managed-workstation) 

- [Distribuire una workstation con accesso con privilegi](https://docs.microsoft.com/azure/active-directory/devices/howto-azure-managed-workstation)

**Monitoraggio del Centro sicurezza di Azure**: Non applicabile

**Responsabilità**: Customer

### <a name="pa-7-follow-just-enough-administration-least-privilege-principle"></a>PA-7: seguire l'amministrazione sufficiente (principio dei privilegi minimi) 

**Linee guida**: Azure Information Protection è integrato con Azure Active Directory (Azure ad), ovvero il servizio di gestione delle identità e degli accessi predefinito di Azure. 

Azure Information Protection include un ruolo a livello di amministratore nel Azure AD. Gli utenti assegnati al ruolo amministratore hanno autorizzazioni complete nel servizio Azure Information Protection. È possibile utilizzare il ruolo amministratore per configurare le etichette per i criteri di Azure Information Protection, gestire i modelli di protezione e attivare la protezione. Tuttavia, il ruolo di amministratore non concede alcuna autorizzazione in Identity Protection Center, Privileged Identity Management, monitoraggio Microsoft 365 integrità del servizio o Office 365 Security &amp; Compliance Center.

Limitare il numero di account o ruoli con privilegi elevati e proteggere questi account a un livello elevato, in quanto gli utenti con questo privilegio possono leggere e modificare direttamente o indirettamente tutte le risorse nell'ambiente Azure. Abilitare l'accesso con privilegi JIT (just-in-Time) alle risorse di Azure e Azure AD usando Privileged Identity Management (PIM). L'accesso JIT concede le autorizzazioni temporanee per eseguire attività con privilegi solo quando gli utenti lo richiedono. PIM può inoltre generare avvisi di sicurezza in caso di attività sospette o non sicure nell'organizzazione Azure AD.

- [Diritti inclusi nei livelli di autorizzazione per Azure Information Protection](https://docs.microsoft.com/azure/information-protection/configure-usage-rights#rights-included-in-permissions-levels)

- [Rights Management autorità emittente e Rights Management proprietario](https://docs.microsoft.com/azure/information-protection/configure-usage-rights#rights-management-issuer-and-rights-management-owner)

- [Ruolo amministratore Azure Information Protection](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-assign-admin-roles#azure-information-protection-administrator)

- [Autorizzazioni del ruolo amministratore in Azure AD](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-assign-admin-roles)

- [Usare gli avvisi di sicurezza di Azure Privileged Identity Management](https://docs.microsoft.com/azure/active-directory/privileged-identity-management/pim-how-to-configure-security-alerts) 

- [Protezione dell'accesso con privilegi per le distribuzioni ibride e cloud in Azure AD](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-admin-roles-secure)

**Monitoraggio del Centro sicurezza di Azure**: Non applicabile

**Responsabilità**: Customer

### <a name="pa-8-choose-approval-process-for-microsoft-support"></a>PA-8: scegliere il processo di approvazione per il supporto tecnico Microsoft  

**Indicazioni**: Azure Information Protection supporta Azure Customer Lockbox per offrire ai clienti la possibilità di rivedere, approvare e rifiutare le richieste di accesso ai dati, nonché di rivedere le richieste effettuate. 

- [Panoramica dell'archivio protetto](https://docs.microsoft.com/azure/security/fundamentals/customer-lockbox-overview)

**Monitoraggio del Centro sicurezza di Azure**: Non applicabile

**Responsibilità**: Customer

## <a name="data-protection"></a>Protezione dei dati

*Per altre informazioni, vedere [benchmark di sicurezza di Azure: protezione dei dati](/azure/security/benchmarks/security-controls-v2-data-protection).*

### <a name="dp-1-discovery-classify-and-label-sensitive-data"></a>DP-1: individuazione, classificazione e assegnazione di etichette ai dati sensibili

**Linee guida**: Azure Information Protection consente di individuare, classificare ed etichettare informazioni riservate. 

Azure Information Protection è una soluzione basata sul cloud che consente alle organizzazioni di classificare e proteggere documenti e messaggi di posta elettronica mediante l'applicazione di etichette. Le etichette possono essere applicate automaticamente dagli amministratori usando regole e condizioni, manualmente dagli utenti o in modo combinato con gli amministratori che definiscono le raccomandazioni visualizzate agli utenti.

- [Panoramica di Azure Information Protection](https://docs.microsoft.com/azure/information-protection/)

- [Indicazioni su come configurare il client di etichettatura unificata](https://docs.microsoft.com/azure/information-protection/rms-client/clientv2-user-guide)

**Monitoraggio del Centro sicurezza di Azure**: Non applicabile

**Responsabilità**: Condiviso

### <a name="dp-2-protect-sensitive-data"></a>DP-2: proteggere i dati sensibili

Materiale sussidiario **: Azure Information Protection** garantisce la protezione dei dati offrendo la possibilità di etichettare informazioni riservate e garantire la protezione dei dati tramite la crittografia. La protezione viene fornita dal servizio Rights Management di Azure.

- [Azure Rights Management](https://docs.microsoft.com/azure/information-protection/what-is-azure-rms)

**Monitoraggio del Centro sicurezza di Azure**: Non applicabile

**Responsabilità**: Condiviso

### <a name="dp-3-monitor-for-unauthorized-transfer-of-sensitive-data"></a>DP-3: monitoraggio per il trasferimento non autorizzato di dati sensibili

**Linee guida**: Azure Information Protection consente di monitorare il trasferimento non autorizzato di dati sensibili tramite la funzionalità di rilevamento e revoca. Track and Revoke consente al cliente di tenere traccia del modo in cui gli utenti usano i documenti che hanno inviato e revocare l'accesso se gli utenti non sono più in grado di leggerli. 

- [Indicazioni su Track and Revoke](https://docs.microsoft.com/azure/information-protection/rms-client/client-track-revoke)

**Monitoraggio del Centro sicurezza di Azure**: Non applicabile

**Responsabilità**: Condiviso

## <a name="asset-management"></a>Asset Management (Gestione degli asset)

*Per altre informazioni, vedere [benchmark di sicurezza di Azure: gestione delle risorse](/azure/security/benchmarks/security-controls-v2-asset-management).*

### <a name="am-1-ensure-security-team-has-visibility-into-risks-for-assets"></a>AM-1: garantire ai team di sicurezza la visibilità dei rischi per gli asset

**Linee guida**: garantire ai team di sicurezza le autorizzazioni di lettura per la sicurezza nel tenant e nelle sottoscrizioni di Azure in modo che possano monitorare i rischi per la sicurezza tramite il Centro sicurezza di Azure. 

A seconda del modo in cui sono strutturate le responsabilità del team di sicurezza, il monitoraggio dei rischi per la sicurezza può essere responsabile di un team di sicurezza centrale o di un team locale. Ciò premesso, le informazioni e i rischi per la sicurezza devono sempre essere aggregati in modo centralizzato all'interno di un'organizzazione. 

Le autorizzazioni di lettura per la sicurezza possono essere applicate in modo esteso a un intero tenant (gruppo di gestione radice) o a gruppi di gestione o sottoscrizioni specifiche. 

Nota: potrebbero essere necessarie autorizzazioni aggiuntive per ottenere la visibilità dei carichi di lavoro e dei servizi. 

- [Panoramica del ruolo lettura sicurezza](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#security-reader)

- [Panoramica di Azure Gruppi di gestione](https://docs.microsoft.com/azure/governance/management-groups/overview)

**Monitoraggio del Centro sicurezza di Azure**: attualmente non disponibile

**Responsabilità**: Customer

### <a name="am-3-use-only-approved-azure-services"></a>AM-3: usare solo i servizi di Azure approvati

**Indicazioni**: Azure Information Protection non supporta le distribuzioni di Azure Resource Manager o consentire ai clienti di limitare le distribuzioni tramite le definizioni di criteri di Azure predefinite, ad esempio "Consenti risorse" o "nega risorse". Tuttavia, i clienti possono limitare l'utilizzo di Azure Information Protection tramite l'assegnazione di etichette ai criteri nel centro sicurezza e conformità. 

- [Gestire la protezione delle informazioni tramite il Centro sicurezza e conformità](https://docs.microsoft.com/microsoft-365/compliance/protect-information?view=o365-worldwide&amp;preserve-view=true)

**Monitoraggio del Centro sicurezza di Azure**: Non applicabile

**Responsabilità**: Customer

## <a name="logging-and-threat-detection"></a>Registrazione e rilevamento delle minacce

*Per altre informazioni, vedere [benchmark di sicurezza di Azure: registrazione e rilevamento delle minacce](/azure/security/benchmarks/security-controls-v2-logging-threat-protection).*

### <a name="lt-2-enable-threat-detection-for-azure-identity-and-access-management"></a>LT-2: abilitare il rilevamento delle minacce per la gestione delle identità e degli accessi di Azure

**Linee guida**: Azure Information Protection è integrato con Azure Active Directory (Azure ad), ovvero il servizio di gestione delle identità e degli accessi predefinito di Azure. 

È possibile visualizzare i log utente forniti da Azure AD con Azure AD Reporting e altre soluzioni, ad esempio monitoraggio di Azure, Azure Sentinel o altri strumenti di SIEM/monitoraggio per i casi d'uso di monitoraggio e analisi più sofisticati. 

ovvero: 

-   Report di accesso: il report di accesso fornisce informazioni sull'utilizzo delle applicazioni gestite e delle attività di accesso degli utenti.

-   Log di controllo: i log consentono la tracciabilità di tutte le modifiche apportate da varie funzionalità all'interno di Azure AD. Esempi di log di controllo includono le modifiche apportate alle risorse all'interno Azure AD, ad esempio l'aggiunta o la rimozione di utenti, app, gruppi, ruoli e criteri.

-   Accessi a rischio: un accesso rischioso è un indicatore di un tentativo di accesso che potrebbe essere stato eseguito da un utente che non è il legittimo proprietario di un account utente.

-   Utenti contrassegnati per il rischio. Un utente rischioso è indicativo di un account utente che potrebbe essere stato compromesso.

Il Centro sicurezza di Azure può anche inviare avvisi su determinate attività sospette, ad esempio un numero eccessivo di tentativi di autenticazione non riusciti e gli account deprecati nella sottoscrizione. Oltre al monitoraggio dell'igiene di base per la sicurezza, il modulo di protezione dalle minacce del Centro sicurezza può raccogliere anche avvisi di sicurezza più approfonditi dalle singole risorse di calcolo di Azure (ad esempio macchine virtuali, contenitori, servizio app), risorse di dati (ad esempio database SQL e archiviazione) e livelli di servizio di Azure. Questa funzionalità consente di visualizzare le anomalie degli account all'interno delle singole risorse.

- [Report delle attività di controllo in Azure AD](https://docs.microsoft.com/azure/active-directory/reports-monitoring/concept-audit-logs)

- [Abilitare Azure Identity Protection](https://docs.microsoft.com/azure/active-directory/identity-protection/overview-identity-protection)

- [Protezione dalle minacce nel Centro sicurezza di Azure](https://docs.microsoft.com/azure/security-center/threat-protection)

**Monitoraggio del Centro sicurezza di Azure**: Non applicabile

**Responsabilità**: Customer

### <a name="lt-4-enable-logging-for-azure-resources"></a>LT-4: abilitare la registrazione per le risorse di Azure

**Indicazioni**: Azure Information Protection fornisce la protezione dei dati per i documenti e i messaggi di posta elettronica di un'organizzazione, insieme a un log per ogni richiesta.  Queste richieste includono quando gli utenti proteggono documenti e messaggi di posta elettronica, quando utilizzano questo contenuto, le azioni eseguite dagli amministratori per questo servizio e le azioni eseguite dagli operatori Microsoft per supportare la distribuzione di Azure Information Protection.

I tipi di log prodotti da Azure Information Protection includono:

- Log di amministrazione: registra le attività amministrative per il servizio di protezione. Ad esempio, se il servizio è disattivato, quando viene abilitata la funzionalità di utente con privilegi avanzati e quando agli utenti vengono delegate autorizzazioni di amministratore per il servizio.

- Rilevamento dei documenti: consente agli utenti di rilevare e revocare i documenti rilevati con il client Azure Information Protection. Gli amministratori globali possono inoltre eseguire il rilevamento di questi documenti per conto degli utenti.

- Log eventi client-attività di utilizzo per il client di Azure Information Protection, registrato nel registro eventi di servizi e applicazioni Windows locale Azure Information Protection.

- File di log del client-risoluzione dei problemi dei log per il client di Azure Information Protection

I log di utilizzo della protezione possono essere usati per identificare ' chi ' accede ai dati protetti, da "quali" dispositivi e da "Where". I registri rivelano se le persone possono leggere correttamente il contenuto protetto, nonché identificare quali utenti hanno letto un documento importante protetto. 

- [Registrazione e analisi dell'utilizzo della protezione da Azure Information Protection](https://docs.microsoft.com/azure/information-protection/log-analyze-usage)

**Monitoraggio del Centro sicurezza di Azure**: Non applicabile

**Responsabilità**: Customer

### <a name="lt-5-centralize-security-log-management-and-analysis"></a>LT-5: centralizzare la gestione e l'analisi dei log di sicurezza

**Linee guida**: assicurarsi che il personale di supporto possa creare una panoramica completa di ciò che è accaduto durante un evento, eseguendo query e usando origini dati diverse, in quanto analizzano potenziali eventi imprevisti. 

Evitare i punti ciechi raccogliendo log diversi e inviarli a una soluzione SIEM centrale, ad esempio Azure Sentinel, per tenere traccia delle attività di un potenziale utente malintenzionato attraverso la catena di Kill. I log possono rivelare se le persone possono leggere correttamente il contenuto protetto, nonché identificare quali persone hanno letto un documento importante protetto. Assicurarsi che le informazioni e le informazioni dettagliate vengano acquisite per altri analisti e per riferimenti cronologici futuri.  

Azure Sentinel fornisce analisi approfondite dei dati in qualsiasi origine di log e un portale di gestione di case per gestire l'intero ciclo di vita degli eventi imprevisti. Le informazioni di intelligence durante un'indagine possono essere associate a un evento imprevisto a scopo di rilevamento e creazione di report. 

- [Registrazione e analisi dell'utilizzo della protezione da Azure Information Protection](https://docs.microsoft.com/azure/information-protection/log-analyze-usage)

- [Esaminare gli eventi imprevisti con Sentinel di Azure](https://docs.microsoft.com/azure/sentinel/tutorial-investigate-cases)

**Monitoraggio del Centro sicurezza di Azure**: Non applicabile

**Responsabilità**: Customer

### <a name="lt-6-configure-log-storage-retention"></a>LT-6: configurare la conservazione dell'archiviazione dei log

**Indicazioni**: Azure Information Protection fornisce la protezione dei dati per i documenti e i messaggi di posta elettronica di un'organizzazione, con un log per ogni richiesta.  Queste richieste includono quando gli utenti proteggono documenti e messaggi di posta elettronica, quando utilizzano questo contenuto, le azioni eseguite dagli amministratori per questo servizio e le azioni eseguite dagli operatori Microsoft per supportare la distribuzione di Azure Information Protection.

La quantità di dati raccolti e archiviati nell'area di lavoro Azure Information Protection e la relativa conservazione variano in modo significativo per ogni tenant, a seconda di fattori quali il numero di client Azure Information Protection e altri endpoint supportati, sia che si stiano raccogliendo i dati di individuazione degli endpoint, che siano stati distribuiti scanner, il numero di documenti protetti a cui si accede e così via.

Usare la funzionalità di utilizzo e i costi stimati del log di monitoraggio di Azure per stimare e verificare la quantità di dati archiviati e controllare anche il periodo di conservazione dei dati per l'area di lavoro Log Analytics. 

- [Registrazione e analisi dell'utilizzo della protezione da Azure Information Protection](https://docs.microsoft.com/azure/information-protection/log-analyze-usage)

- [Gestire l'utilizzo e i costi con i log di Monitoraggio di Azure](https://docs.microsoft.com/azure/azure-monitor/platform/manage-cost-storage)

**Monitoraggio del Centro sicurezza di Azure**: Non applicabile

**Responsabilità**: Customer

## <a name="incident-response"></a>Risposta agli eventi imprevisti

*Per altre informazioni, vedere [benchmark di sicurezza di Azure: risposta agli eventi imprevisti](/azure/security/benchmarks/security-controls-v2-incident-response).*

### <a name="ir-1-preparation--update-incident-response-process-for-azure"></a>IR-1: Preparazione – aggiornamento del processo di risposta agli eventi imprevisti per Azure

**Linee guida**: assicurarsi che l'organizzazione abbia processi per rispondere agli eventi imprevisti della sicurezza, abbia aggiornato questi processi per Azure e li eserciti regolarmente per garantire la conformità.

- [Implementare la sicurezza nell'ambiente aziendale](https://docs.microsoft.com/azure/cloud-adoption-framework/security/security-top-10#4-process-update-incident-response-ir-processes-for-cloud)

- [Guida di riferimento alla risposta agli eventi imprevisti](https://docs.microsoft.com/microsoft-365/downloads/IR-Reference-Guide.pdf)

**Monitoraggio del Centro sicurezza di Azure**: Non applicabile

**Responsabilità**: Customer

### <a name="ir-2-preparation--setup-incident-notification"></a>IR-2: preparazione-notifica dell'evento imprevisto di installazione

**Indicazioni**: configurare le informazioni di contatto per gli eventi imprevisti della sicurezza nel centro sicurezza di Azure. Le informazioni di contatto vengono utilizzate da Microsoft per contattare l'utente se Microsoft Security Response Center (MSRC) rileva che i dati sono stati accessibili da parte di utenti non autorizzati o non autorizzati. Sono disponibili anche opzioni per personalizzare gli avvisi e le notifiche degli eventi imprevisti in diversi servizi di Azure in base alle esigenze di risposta agli eventi imprevisti. 

- [Come impostare il contatto di sicurezza del Centro sicurezza di Azure](https://docs.microsoft.com/azure/security-center/security-center-provide-security-contact-details)

**Monitoraggio del Centro sicurezza di Azure**: Sì

**Responsabilità**: Customer

### <a name="ir-3-detection-and-analysis--create-incidents-based-on-high-quality-alerts"></a>IR-3: rilevamento e analisi: creare eventi imprevisti in base agli avvisi di alta qualità

**Linee guida**: assicurarsi di disporre di un processo per creare avvisi di alta qualità e misurare la qualità degli avvisi. Questo consente di apprendere le lezioni dagli eventi imprevisti passati e di assegnare la priorità agli avvisi per gli analisti, in modo da non sprecare tempo su falsi positivi. 

Gli avvisi di alta qualità possono essere creati in base all'esperienza degli eventi imprevisti passati, alle origini della community convalidate e agli strumenti progettati per generare e pulire gli avvisi fondendo e correlando diverse origini dei segnali. 

Il Centro sicurezza di Azure offre avvisi di alta qualità in molte risorse di Azure. È possibile usare ASC Data Connector per trasmettere gli avvisi ad Azure Sentinel. Azure Sentinel consente di creare regole di avviso avanzate per generare automaticamente eventi imprevisti per un'analisi. 

Consente di esportare gli avvisi e le raccomandazioni del Centro sicurezza di Azure usando la funzionalità di esportazione per identificare i rischi per le risorse di Azure. Esporta avvisi e consigli manualmente o in modo continuo e continuo.

- [Come configurare l'esportazione](https://docs.microsoft.com/azure/security-center/continuous-export)

- [Come trasmettere gli avvisi in Azure Sentinel](https://docs.microsoft.com/azure/sentinel/connect-azure-security-center)

**Monitoraggio del Centro sicurezza di Azure**: attualmente non disponibile

**Responsabilità**: Customer

### <a name="ir-4-detection-and-analysis--investigate-an-incident"></a>IR-4: rilevamento e analisi-esaminare un evento imprevisto

**Linee guida**: assicurarsi che gli analisti possano creare una panoramica completa di ciò che è successo eseguendo query e usando origini dati diverse durante l'analisi di potenziali eventi imprevisti. Evitare le macchie cieche raccogliendo log diversi per tenere traccia delle attività di un potenziale utente malintenzionato attraverso la catena di Kill. Inoltre, assicurarsi che le informazioni e le informazioni dettagliate vengano acquisite per altri analisti e per riferimenti cronologici futuri.  

Le origini dati per l'analisi includono le origini di registrazione centralizzate che sono già state raccolte dai servizi inclusi nell'ambito e i sistemi in esecuzione, ma possono includere anche:

- Dati di rete: usare i log di flusso dei gruppi di sicurezza di rete, Network Watcher di Azure e monitoraggio di Azure per acquisire i log del flusso di rete e altre informazioni di analisi. 

- Snapshot dei sistemi in esecuzione: 

    - Usare la funzionalità di snapshot della macchina virtuale di Azure per creare uno snapshot del disco del sistema in esecuzione. 

    - Utilizzare la funzionalità di dump della memoria nativa del sistema operativo per creare uno snapshot della memoria del sistema in esecuzione.

    - Usare la funzionalità snapshot dei servizi di Azure o la funzionalità del software per creare snapshot dei sistemi in esecuzione.

Azure Sentinel fornisce analisi approfondite dei dati in qualsiasi origine di log e un portale di gestione di case per gestire l'intero ciclo di vita degli eventi imprevisti. Le informazioni di intelligence durante un'indagine possono essere associate a un evento imprevisto a scopo di rilevamento e creazione di report. 

- [Snapshot del disco di un computer Windows](https://docs.microsoft.com/azure/virtual-machines/windows/snapshot-copy-managed-disk)

- [Snapshot del disco di un computer Linux](https://docs.microsoft.com/azure/virtual-machines/linux/snapshot-copy-managed-disk)

- [Microsoft Azure supportare le informazioni di diagnostica e la raccolta di dump della memoria](https://azure.microsoft.com/support/legal/support-diagnostic-information-collection/) 

- [Esaminare gli eventi imprevisti con Sentinel di Azure](https://docs.microsoft.com/azure/sentinel/tutorial-investigate-cases)

**Monitoraggio del Centro sicurezza di Azure**: Non applicabile

**Responsabilità**: Customer

### <a name="ir-5-detection-and-analysis--prioritize-incidents"></a>IR-5: rilevamento e analisi-assegnare priorità agli eventi imprevisti

**Linee guida**: fornire il contesto agli analisti su quali eventi imprevisti concentrarsi innanzitutto in base alla gravità dell'avviso e alla sensibilità degli asset. 

Il Centro sicurezza di Azure assegna una gravità a ogni avviso per facilitare la priorità degli avvisi che devono essere analizzati per primi. Il livello di gravità è basato sul livello di attendibilità del Centro sicurezza nell'individuazione o sull'analisi utilizzata per emettere l'avviso, oltre al livello di confidenza causato da un intento dannoso dietro l'attività che ha portato all'avviso.

Inoltre, contrassegnare le risorse usando i tag e creare un sistema di denominazione per identificare e classificare le risorse di Azure, in particolare quelle che elaborano i dati sensibili.  È responsabilità dell'utente classificare in ordine di priorità la correzione degli avvisi in base alla criticità delle risorse e dell'ambiente di Azure in cui si è verificato l'evento imprevisto.

- [Avvisi di sicurezza nel Centro sicurezza di Azure](https://docs.microsoft.com/azure/security-center/security-center-alerts-overview)

- [Usare tag per organizzare le risorse di Azure](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-using-tags)

**Monitoraggio del Centro sicurezza di Azure**: attualmente non disponibile

**Responsabilità**: Customer

### <a name="ir-6-containment-eradication-and-recovery--automate-the-incident-handling"></a>IR-6: contenimento, eliminazione e ripristino-automazione della gestione degli eventi imprevisti

**Linee guida**: automatizzare le attività ripetitive manuali per velocizzare il tempo di risposta e ridurre il carico sugli analisti. L'esecuzione delle attività manuali dura più tempo, rallentando ogni evento imprevisto e riducendo il numero di eventi imprevisti che un analista può gestire. Anche le attività manuali aumentano la fatica degli analisti, aumentando il rischio di errori umani che causano ritardi e peggiorando la capacità degli analisti di concentrarsi in modo efficace sulle attività complesse. Usare le funzionalità di automazione del flusso di lavoro nel centro sicurezza di Azure e Azure Sentinel per attivare automaticamente le azioni o eseguire un PlayBook per rispondere agli avvisi di sicurezza in ingresso. Il PlayBook esegue azioni, ad esempio l'invio di notifiche, la disabilitazione degli account e l'isolamento delle reti problematiche. 

- [Configurare l'automazione del flusso di lavoro nel centro sicurezza](https://docs.microsoft.com/azure/security-center/workflow-automation)

- [Configurare le risposte automatiche alle minacce nel centro sicurezza di Azure](https://docs.microsoft.com/azure/security-center/tutorial-security-incident#triage-security-alerts)

- [Configurare le risposte automatiche alle minacce in Azure Sentinel](https://docs.microsoft.com/azure/sentinel/tutorial-respond-threats-playbook)

**Monitoraggio del Centro sicurezza di Azure**: attualmente non disponibile

**Responsabilità**: Customer

## <a name="posture-and-vulnerability-management"></a>Gestione delle posture e delle vulnerabilità

*Per altre informazioni, vedere [benchmark di sicurezza di Azure: gestione di posture e vulnerabilità](/azure/security/benchmarks/security-controls-v2-vulnerability-management).*

### <a name="pv-1-establish-secure-configurations-for-azure-services"></a>PV-1: definire configurazioni sicure per i servizi di Azure 

**Linee guida**: Azure Information Protection possono essere configurate tramite il Centro sicurezza e conformità o PowerShell. 

All'interno del Centro sicurezza e conformità un amministratore può creare etichette di riservatezza, definire le operazioni che ciascuna etichetta può eseguire e pubblicare le etichette. 

Creare le etichette: creare e denominare le etichette di riservatezza in base alla tassonomia di classificazione dell'organizzazione per diversi livelli di sensibilità del contenuto. Usare nomi o termini comuni che hanno senso per gli utenti. Se non si dispone già di una tassonomia stabilita, prendere in considerazione l'uso di nomi di etichetta, ad esempio personale, pubblico, generale, riservato e riservatezza elevata. È quindi possibile usare le etichette secondarie per raggruppare etichette simili per categoria. Quando si crea un'etichetta, usare il testo della descrizione comando per consentire agli utenti di selezionare l'etichetta appropriata.

Definire le operazioni che ogni etichetta può eseguire: configurare le impostazioni di protezione che si desidera associare a ogni etichetta. È possibile, ad esempio, che si desideri applicare un contenuto con sensibilità inferiore (ad esempio un'etichetta "generale") per applicare solo un'intestazione o un piè di pagina, mentre un contenuto con sensibilità più elevata, ad esempio un'etichetta "riservata", deve avere una filigrana e una crittografia.

Pubblicare le etichette: una volta configurate le etichette di riservatezza, pubblicarle usando un criterio di etichetta. Decidere quali utenti e gruppi devono avere le etichette e le impostazioni dei criteri da usare. Una singola etichetta è riutilizzabile, ovvero una volta, che può essere inclusa in diversi criteri etichetta assegnati a utenti diversi. Ad esempio, è possibile pilotare le etichette di riservatezza assegnando un criterio etichetta a un numero limitato di utenti. Quando si è pronti per distribuire le etichette nell'organizzazione, è possibile creare un nuovo criterio etichetta per le etichette e questa volta specificare tutti gli utenti.

Per usare PowerShell, installare il modulo AIPService di PowerShell. In PowerShell un amministratore può eseguire queste attività insieme ad altri: 

- Eseguire la migrazione da Rights Management locali (AD RMS o Windows RMS) a Azure Information Protection
- Generare e gestire la propria chiave del tenant: scenario BYOK (Bring your own key)
- Attivare o disattivare il servizio Rights Management per l'organizzazione
- Configurare i controlli di onboarding per una distribuzione in più fasi del servizio Rights Management di Azure
- Creare e gestire modelli di Rights Management per l'organizzazione
- Gestire utenti e gruppi autorizzati ad amministrare Rights Management servizio per l'organizzazione
- Registrare e analizzare l'utilizzo per Rights Management

Per altre informazioni, vedere i riferimenti seguenti:

- [Inizia a usare le etichette di riservatezza nel centro sicurezza e conformità](https://docs.microsoft.com/microsoft-365/compliance/get-started-with-sensitivity-labels?view=o365-worldwide&amp;preserve-view=true)

- [Creazione e pubblicazione di etichette di riservatezza](https://docs.microsoft.com/microsoft-365/compliance/create-sensitivity-labels?view=o365-worldwide&amp;preserve-view=true)

- [Applicare la crittografia alle etichette di riservatezza](https://docs.microsoft.com/microsoft-365/compliance/encryption-sensitivity-labels?view=o365-worldwide&amp;preserve-view=true)

- [PowerShell per Azure Information Protection](https://docs.microsoft.com/azure/information-protection/administer-powershell)

**Monitoraggio del Centro sicurezza di Azure**: Non applicabile

**Responsabilità**: Customer

### <a name="pv-8-conduct-regular-attack-simulation"></a>PV-8: eseguire la simulazione di attacchi regolari

**Linee guida**: come richiesto, eseguire test di penetrazione o attività del Red Team sulle risorse di Azure e garantire la correzione di tutti i risultati critici della sicurezza.
Attenersi alle regole di test di penetrazione Microsoft Cloud di engagement per assicurarsi che i test di penetrazione non siano in violazione dei criteri Microsoft. Usa la strategia e l'esecuzione di Microsoft red teaming e test di penetrazione di siti Live su infrastruttura, servizi e applicazioni cloud gestite da Microsoft.

- [Test di penetrazione in Azure](https://docs.microsoft.com/azure/security/fundamentals/pen-testing)

- [Regole di coinvolgimento dei test di penetrazione](https://www.microsoft.com/msrc/pentest-rules-of-engagement?rtc=1) 

- [Microsoft Cloud Red Teaming](https://gallery.technet.microsoft.com/Cloud-Red-Teaming-b837392e)

**Monitoraggio del Centro sicurezza di Azure**: Non applicabile

**Responsabilità**: Condiviso

## <a name="backup-and-recovery"></a>Backup e ripristino

*Per altre informazioni, vedere [benchmark di sicurezza di Azure: backup e ripristino](/azure/security/benchmarks/security-controls-v2-backup-recovery).*

### <a name="br-4-mitigate-risk-of-lost-keys"></a>BR-4: ridurre il rischio di chiavi perse

**Indicazioni**: Azure Information Protection offre ai clienti la possibilità di configurare il tenant con la propria chiave tramite Bring your own key (BYOK). Le chiavi generate dal cliente devono essere archiviate in Azure Key Vault per la protezione. Azure Key Vault aiuta a evitare la perdita di chiavi tramite l'eliminazione temporanea, la separazione dei ruoli e i domini di sicurezza separati. 

- [Azure Information Protection Bring Your Own Key e integrazione con Azure Key Vault](https://docs.microsoft.com/azure/information-protection/byok-price-restrictions)
- [Abilitare l'eliminazione temporanea in Key Vault](https://docs.microsoft.com/azure/storage/blobs/storage-blob-soft-delete?tabs=azure-portal)

**Monitoraggio del Centro sicurezza di Azure**: Sì

**Responsabilità**: Customer

## <a name="governance-and-strategy"></a>Governance e strategia

*Per altre informazioni, vedere [benchmark di sicurezza di Azure: governance e strategia](/azure/security/benchmarks/security-controls-v2-governance-strategy).*

### <a name="gs-1-define-asset-management-and-data-protection-strategy"></a>GS-1: definire la strategia di gestione delle risorse e della protezione dei dati 

**Linee guida**: assicurarsi di documentare e comunicare una strategia chiara per il monitoraggio e la protezione continui dei sistemi e dei dati. Definire le priorità di individuazione, valutazione, protezione e monitoraggio dei sistemi e dei dati cruciali per l'azienda. 

Questa strategia deve includere indicazioni, criteri e standard documentati per gli elementi seguenti: 

-   Standard di classificazione dei dati in base ai rischi aziendali

-   Visibilità dell'organizzazione della sicurezza nei rischi e nell'inventario degli asset 

-   Approvazione dell'organizzazione della sicurezza dei servizi di Azure per l'uso 

-   Sicurezza degli asset attraverso il ciclo di vita

-   Strategia di controllo degli accessi obbligatoria in base alla classificazione dei dati aziendali

-   Uso delle funzionalità di protezione dei dati native e di terze parti di Azure

-   Requisiti di crittografia dei dati per i casi d'uso in transito e a riposo

-   Standard crittografici appropriati

Per altre informazioni, vedere i riferimenti seguenti:

- [Raccomandazione sull'architettura della sicurezza di Azure-archiviazione, dati e crittografia](https://docs.microsoft.com/azure/architecture/framework/security/storage-data-encryption?toc=/security/compass/toc.json&amp;bc=/security/compass/breadcrumb/toc.json)

- [Nozioni fondamentali sulla sicurezza di Azure: sicurezza, crittografia e archiviazione dei dati di Azure](https://docs.microsoft.com/azure/security/fundamentals/encryption-overview)

- [Framework di adozione cloud: procedure consigliate per la sicurezza e la crittografia dei dati di Azure](https://docs.microsoft.com/azure/security/fundamentals/data-encryption-best-practices?toc=/azure/cloud-adoption-framework/toc.json&amp;bc=/azure/cloud-adoption-framework/_bread/toc.json)

- [Benchmark di sicurezza di Azure-gestione delle risorse](https://docs.microsoft.com/azure/security/benchmarks/security-benchmark-v2-asset-management)

- [Benchmark di sicurezza di Azure-protezione dei dati](https://docs.microsoft.com/azure/security/benchmarks/security-benchmark-v2-data-protection)

**Monitoraggio del Centro sicurezza di Azure**: Non applicabile

**Responsabilità**: Customer

### <a name="gs-2-define-enterprise-segmentation-strategy"></a>GS-2: definire la strategia di segmentazione aziendale 

**Linee guida**: definire una strategia a livello aziendale per segmentare l'accesso alle risorse usando una combinazione di identità, rete, applicazione, sottoscrizione, gruppo di gestione e altri controlli.

Bilanciare accuratamente la necessità di separazione di sicurezza con la necessità di abilitare il funzionamento giornaliero dei sistemi che devono comunicare tra loro e accedere ai dati.

Assicurarsi che la strategia di segmentazione venga implementata in modo coerente tra i tipi di controllo, inclusi i modelli di sicurezza di rete, identità e accesso e i modelli di accesso e autorizzazione dell'applicazione e i controlli dei processi umani.

- [Linee guida sulla strategia di segmentazione in Azure (video)](https://docs.microsoft.com/security/compass/microsoft-security-compass-introduction#azure-components-and-reference-model-2151)

- [Linee guida sulla strategia di segmentazione in Azure (documento)](https://docs.microsoft.com/security/compass/governance#enterprise-segmentation-strategy)

- [Allinea la segmentazione della rete con la strategia di segmentazione aziendale](https://docs.microsoft.com/security/compass/network-security-containment#align-network-segmentation-with-enterprise-segmentation-strategy)

**Monitoraggio del Centro sicurezza di Azure**: Non applicabile

**Responsabilità**: Customer

### <a name="gs-3-define-security-posture-management-strategy"></a>GS-3: definire la strategia di gestione delle attitudini per la sicurezza

**Linee guida**: misurare e mitigare costantemente i rischi per le singole risorse e per l'ambiente in cui sono ospitate. Assegnare priorità ad asset di valore elevato e ad aree di attacco altamente esposte, ad esempio applicazioni pubblicate, punti di ingresso e uscita di rete, endpoint utente e amministratore e così via.

- [Benchmark di sicurezza di Azure-gestione di posture e vulnerabilità](https://docs.microsoft.com/azure/security/benchmarks/security-benchmark-v2-posture-vulnerability-management)

**Monitoraggio del Centro sicurezza di Azure**: Non applicabile

**Responsabilità**: Customer

### <a name="gs-4-align-organization-roles-responsibilities-and-accountabilities"></a>GS-4: allinea ruoli organizzazione, responsabilità e responsabilità

**Linee guida**: assicurarsi di documentare e comunicare una strategia chiara per i ruoli e le responsabilità nell'organizzazione della sicurezza. Definire le priorità per fornire una chiara responsabilità per le decisioni relative alla sicurezza, informare tutti gli utenti sul modello di responsabilità condivisa e informare i team tecnici sulla tecnologia per proteggere il cloud.

- [Procedura consigliata per la sicurezza di Azure 1 – people: educare i team al percorso di sicurezza del cloud](https://docs.microsoft.com/azure/cloud-adoption-framework/security/security-top-10#1-people-educate-teams-about-the-cloud-security-journey)

- [Procedura consigliata per la sicurezza di Azure 2-persone: istruire i team sulla tecnologia di sicurezza cloud](https://docs.microsoft.com/azure/cloud-adoption-framework/security/security-top-10#2-people-educate-teams-on-cloud-security-technology)

- [Procedura consigliata per la sicurezza di Azure 3-processo: assegnare la responsabilità per le decisioni sulla sicurezza del cloud](https://docs.microsoft.com/azure/cloud-adoption-framework/security/security-top-10#4-process-update-incident-response-ir-processes-for-cloud)

**Monitoraggio del Centro sicurezza di Azure**: Non applicabile

**Responsabilità**: Customer

### <a name="gs-5-define-network-security-strategy"></a>GS-5: definire la strategia di sicurezza di rete

**Linee guida**: definire un approccio alla sicurezza di rete di Azure come parte della strategia globale di controllo degli accessi di sicurezza dell'organizzazione.  

Questa strategia deve includere indicazioni, criteri e standard documentati per gli elementi seguenti: 

-   Gestione centralizzata della rete e responsabilità della sicurezza

-   Modello di segmentazione della rete virtuale allineato con la strategia di segmentazione aziendale

-   Strategia di monitoraggio e aggiornamento in diversi scenari di minaccia e attacco

-   Internet Edge e strategia di ingresso e uscita

-   Strategia di interconnettività locale e cloud ibrido

-   Elementi di sicurezza di rete aggiornati, ad esempio diagrammi di rete, architettura di rete di riferimento

Per altre informazioni, vedere i riferimenti seguenti:
- [Procedura consigliata per la sicurezza di Azure 11-architettura. Strategia di sicurezza unificata singola](https://docs.microsoft.com/azure/cloud-adoption-framework/security/security-top-10#11-architecture-establish-a-single-unified-security-strategy)

- [Benchmark di sicurezza di Azure-sicurezza di rete](https://docs.microsoft.com/azure/security/benchmarks/security-benchmark-v2-network-security)

- [Panoramica della sicurezza di rete di Azure](https://docs.microsoft.com/azure/security/fundamentals/network-overview)

- [Strategia di architettura di rete aziendale](https://docs.microsoft.com/azure/cloud-adoption-framework/ready/enterprise-scale/architecture)

**Monitoraggio del Centro sicurezza di Azure**: Non applicabile

**Responsabilità**: Customer

### <a name="gs-6-define-identity-and-privileged-access-strategy"></a>GS-6: definire la strategia di identità e di accesso con privilegi

**Linee guida**: definire approcci di identità e accesso con privilegi di Azure come parte della strategia globale di controllo degli accessi di sicurezza dell'organizzazione.  

Questa strategia deve includere indicazioni, criteri e standard documentati per gli elementi seguenti: 

-   Sistema di identità e autenticazione centralizzato e relativa interconnettività con altri sistemi di identità interni ed esterni

-   Metodi di autenticazione avanzata in diversi casi d'uso e condizioni

-   Protezione di utenti con privilegi elevati

-   Monitoraggio e gestione delle attività degli utenti anomalie  

-   Verifica dell'identità e dell'accesso dell'utente e processo di riconciliazione

Per altre informazioni, vedere i riferimenti seguenti:

- [Benchmark di sicurezza di Azure-gestione delle identità](https://docs.microsoft.com/azure/security/benchmarks/security-benchmark-v2-identity-management)

- [Benchmark di sicurezza di Azure-accesso con privilegi](https://docs.microsoft.com/azure/security/benchmarks/security-benchmark-v2-privileged-access)

- [Procedura consigliata per la sicurezza di Azure 11-architettura. Strategia di sicurezza unificata singola](https://docs.microsoft.com/azure/cloud-adoption-framework/security/security-top-10#11-architecture-establish-a-single-unified-security-strategy)

- [Informazioni generali sulla sicurezza della gestione delle identità di Azure](https://docs.microsoft.com/azure/security/fundamentals/identity-management-overview)

**Monitoraggio del Centro sicurezza di Azure**: Non applicabile

**Responsabilità**: Customer

### <a name="gs-7-define-logging-and-threat-response-strategy"></a>GS-7: definire la strategia di registrazione e di risposta alle minacce

**Linee guida**: definire una strategia di registrazione e risposta alle minacce per rilevare e correggere rapidamente le minacce rispettando i requisiti di conformità. Definire le priorità fornendo gli analisti con avvisi di alta qualità ed esperienze senza problemi, in modo da potersi concentrare sulle minacce anziché sull'integrazione e sui passaggi manuali. 

Questa strategia deve includere indicazioni, criteri e standard documentati per gli elementi seguenti: 

-   Il ruolo e le responsabilità dell'organizzazione per le operazioni di sicurezza (secops) 

-   Un processo di risposta agli eventi imprevisti ben definito allineato a NIST o a un altro framework di settore 

-   Acquisizione e conservazione dei log per supportare il rilevamento delle minacce, la risposta agli eventi imprevisti e le esigenze di conformità

-   Visibilità centralizzata delle informazioni sulla correlazione e sulle minacce, uso di SIEM, funzionalità native di Azure e altre origini 

-   Piano di comunicazione e notifica con i clienti, i fornitori e le parti pubbliche di interesse

-   Uso di piattaforme di terze parti e native di Azure per la gestione degli eventi imprevisti, ad esempio registrazione e rilevamento delle minacce, analisi forense e correzione e eliminazione degli attacchi

-   Processi per la gestione degli eventi imprevisti e delle attività post-evento, ad esempio le lezioni apprese e la conservazione delle prove

Per altre informazioni, vedere i riferimenti seguenti:

- [Benchmark di sicurezza di Azure: registrazione e rilevamento delle minacce](https://docs.microsoft.com/azure/security/benchmarks/security-benchmark-v2-logging-threat-detection)

- [Benchmark di sicurezza di Azure-risposta agli eventi imprevisti](https://docs.microsoft.com/azure/security/benchmarks/security-benchmark-v2-incident-response)

- [Procedura consigliata per la sicurezza di Azure 4-processo. Aggiornare i processi di risposta agli eventi imprevisti per il cloud](https://docs.microsoft.com/azure/cloud-adoption-framework/security/security-top-10#4-process-update-incident-response-ir-processes-for-cloud)

- [Guida alla decisione sul Framework di adozione di Azure, la registrazione e la creazione di report](https://docs.microsoft.com/azure/cloud-adoption-framework/decision-guides/logging-and-reporting/)

- [Scalabilità, gestione e monitoraggio di Azure Enterprise](https://docs.microsoft.com/azure/cloud-adoption-framework/ready/enterprise-scale/management-and-monitoring)

**Monitoraggio del Centro sicurezza di Azure**: Non applicabile

**Responsabilità**: Customer

## <a name="next-steps"></a>Passaggi successivi

- Vedere [Panoramica di Azure Security benchmark V2](/azure/security/benchmarks/overview)
- Altre informazioni su [Baseline di sicurezza di Azure](/azure/security/benchmarks/security-baselines-overview)
