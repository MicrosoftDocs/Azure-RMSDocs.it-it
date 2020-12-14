---
title: Domande frequenti su Azure Information Protection
description: Alcune domande frequenti su Azure Information Protection e il relativo servizio di protezione, Azure Rights Management (Azure RMS).
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 12/02/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.suite: ems
ms.custom: admin
search.appverid:
- MET150
ms.openlocfilehash: c42f2459861b7b7167469ddadd7c3ff399d47f48
ms.sourcegitcommit: 8a141858e494dd1d3e48831e6cd5a5be48ac00d2
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2020
ms.locfileid: "97381962"
---
# <a name="frequently-asked-questions-for-azure-information-protection"></a>Domande frequenti su Azure Information Protection

>***Si applica a**: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*
>
>***Pertinente per**: [AIP Unified Labeling client e client classico](#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

>[!NOTE] 
> Per offrire un'esperienza utente unificata e semplificata, **Azure Information Protection** la gestione classica di client e **etichette** nel portale di Azure verrà **deprecata** a partire dal **31 marzo 2021**. In questo intervallo di tempo tutti i clienti correnti di Azure Information Protection possono passare alla soluzione di etichettatura unificata usando la piattaforma di etichettatura unificata di Microsoft Information Protection. Altre informazioni nell'[avviso ufficiale sulla deprecazione](https://aka.ms/aipclassicsunset).

Di seguito sono riportate alcune possibili domande su Azure Information Protection o sul servizio Azure Rights Management (Azure RMS) vedere se la risposta è disponibile qui.

## <a name="whats-the-difference-between-azure-information-protection-and-microsoft-information-protection"></a>Qual è la differenza tra Azure Information Protection e Microsoft Information Protection?

A differenza di Azure Information Protection, [Microsoft Information Protection](https://www.microsoft.com/security/business/information-protection) non è una sottoscrizione o un prodotto che è possibile acquistare. Si tratta invece di un Framework per prodotti e funzionalità integrate che consentono di proteggere le informazioni riservate dell'organizzazione.

I **prodotti Microsoft Information Protection includono**:
- Azure Information Protection
- Microsoft 365 Information Protection, ad esempio Microsoft 365 DLP
- Windows Information Protection
- Microsoft Cloud App Security

Le **funzionalità di Microsoft Information Protection includono**:
- Gestione unificata delle etichette
- Esperienza di assegnazione di etichette agli utenti finali incorporata nelle app di Office
- Possibilità per Windows di comprendere le etichette unificate e applicare la protezione ai dati
- Microsoft Information Protection SDK
- Funzionalità in Adobe Acrobat Reader per visualizzare i file PDF etichettati e protetti

Per altre informazioni, vedere [funzionalità di protezione delle informazioni per proteggere i dati sensibili](https://techcommunity.microsoft.com/t5/Enterprise-Mobility-Security/Announcing-availability-of-information-protection-capabilities/ba-p/261967).

## <a name="whats-the-difference-between-labels-in-microsoft-365-and-labels-in-azure-information-protection"></a>Qual è la differenza tra le etichette nelle Microsoft 365 ed etichette Azure Information Protection?

Originariamente, Microsoft 365 aveva solo le [etichette di conservazione](https://support.office.com/article/af398293-c69d-465e-a249-d74561552d30), che consentono di classificare documenti e messaggi di posta elettronica per il controllo e la conservazione quando tale contenuto veniva archiviato in Microsoft 365 Services. 

Al contrario, Azure Information Protection le etichette, configurate nel momento in cui si usa il client AIP classico nel portale di Azure, è possibile applicare un criterio di classificazione e protezione coerente per documenti e messaggi di posta elettronica, indipendentemente dal fatto che siano archiviati in locale o nel cloud.

Microsoft 365 supporta ora le [etichette di riservatezza](/microsoft-365/compliance/sensitivity-labels) oltre alle etichette di conservazione. Le etichette di riservatezza possono essere create e configurate nei seguenti centri di amministrazione:

- Centro sicurezza e conformità di Office 365
- Centro sicurezza Microsoft 365
- Centro conformità Microsoft 365

Se nel portale di Azure sono configurate etichette AIP legacy, è consigliabile eseguirne la migrazione a etichette di riservatezza e client con etichetta unificata. Per altre informazioni, vedere [Esercitazione: Migrazione dal client classico al client di etichettatura unificata di Azure Information Protection (AIP)](tutorial-migrating-to-ul.md).

Per altre informazioni, vedere [Announcing availability of information protection capabilities to help protect your sensitive data](https://techcommunity.microsoft.com/t5/Enterprise-Mobility-Security/Announcing-availability-of-information-protection-capabilities/ba-p/261967) (Annuncio della disponibilità di funzionalità di protezione delle informazioni per proteggere i dati sensibili).

## <a name="how-can-i-determine-if-my-tenant-is-on-the-unified-labeling-platform"></a>Come è possibile determinare se il tenant si trova nella piattaforma di etichettatura unificata?

Quando il tenant si trova nella piattaforma di etichettatura unificata, supporta le etichette di riservatezza che possono essere usate dai [client e dai servizi che supportano l'assegnazione di etichette unificata](configure-policy-migrate-labels.md#clients-and-services-that-support-unified-labeling). Se è stata ottenuta la sottoscrizione per Azure Information Protection nel 2019 giugno o versione successiva, il tenant si trova automaticamente nella piattaforma di assegnazione di etichette unificata e non è necessaria alcuna azione aggiuntiva. Il tenant potrebbe anche trovarsi su questa piattaforma perché qualcuno ha eseguito la migrazione delle etichette Azure Information Protection.

Se il tenant non è presente nella piattaforma di assegnazione portale di Azure di etichette unificata, nel riquadro dei **Azure Information Protection** verrà visualizzato il banner informativo seguente:

![Banner informazioni sulla migrazione](media/migration-status-banner.png)

È anche possibile selezionare **Azure Information Protection**  >  **Gestisci**  >  **etichetta unificata** e visualizzare lo stato di **etichettatura unificata** :

|Stato |Descrizione  |
|---------|---------|
|**Attivato**     |  Il tenant si trova nella piattaforma di etichettatura unificata. <br />È possibile [creare, configurare e pubblicare etichette](/microsoft-365/compliance/create-sensitivity-labels) da Microsoft 365 Compliance Center.       |
|**Non attivato**    |  Il tenant non si trova nella piattaforma di etichettatura unificata. <br />Per istruzioni e indicazioni sulla migrazione, vedere [How to migrate Azure Information Protection labels to Unified Sensitivity labels](configure-policy-migrate-labels.md).       |
| | |

## <a name="whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients"></a>Qual è la differenza tra il Azure Information Protection i client di etichetta classica e unificata?

Il client legacy Azure Information Protection, denominato client *classico* , Scarica le etichette e le impostazioni dei criteri da Azure e consente di configurare i [criteri di AIP](overview-policy.md) dall'portale di Azure.

Il *client di etichettatura unificata* è il client più aggiornato con gli aggiornamenti più recenti e supporta la piattaforma di etichettatura unificata utilizzata da più applicazioni e servizi. Il client di etichettatura unificata Scarica le [etichette di riservatezza](/microsoft-365/compliance/sensitivity-labels) e le impostazioni dei criteri dai centri di amministrazione seguenti:

- Centro sicurezza e conformità di Office 365
- Centro sicurezza Microsoft 365
- Centro conformità Microsoft 365

Se si è un amministratore, per altre informazioni, vedere [scegliere la soluzione Windows Labeling](rms-client/use-client.md#choose-your-windows-labeling-solution).

### <a name="classic-client-deprecation"></a>Deprecazione client classica

Per offrire un'esperienza unificata e semplificata, la Azure Information Protection la gestione **classica del client** e delle **etichette** nel portale di Azure verrà **deprecata** a partire dal **31 marzo 2021**. 

Dopo la deprecazione, il client continuerà a funzionare come previsto. Tuttavia, gli amministratori non saranno in grado di aggiornare i criteri nel portale e non verranno fornite altre correzioni o modifiche per il client classico.

In questo intervallo di tempo tutti i clienti correnti di Azure Information Protection possono passare alla soluzione di etichettatura unificata usando la piattaforma di etichettatura unificata di Microsoft Information Protection. Altre informazioni nell'[avviso ufficiale sulla deprecazione](https://aka.ms/aipclassicsunset).

Se il client classico è stato distribuito, è consigliabile eseguire l'aggiornamento al client di etichettatura unificata. Per ulteriori informazioni, vedere.

- [Esercitazione: migrazione dal client classico al client Unified Labeling](tutorial-migrating-to-ul.md)
- [Come eseguire la migrazione di etichette di Azure Information Protection a etichette di riservatezza unificate](configure-policy-migrate-labels.md)
### <a name="identify-the-client-you-have-installed"></a>Identificare il client installato

Se si è un utente che desidera comprendere se è installato il client di etichettatura classica o unificata, è possibile eseguire una delle operazioni seguenti:

- Nelle app di Office, selezionare il pulsante della barra degli strumenti **sensibilità** o **Proteggi** . Il client di etichettatura unificata Mostra il pulsante **sensibilità** :::image type="icon" source="media/i-sensitivity.PNG" border="false"::: , mentre il client classico Mostra il pulsante **Proteggi** . 

- Verificare il numero di versione per l'applicazione Azure Information Protection installata.

    - Le versioni **1. x** indicano che si ha il client classico. Esempio: **1.54.59.0**
    - Le versioni **2. x** indicano che si dispone del client di etichettatura unificata. Esempio: **2.8.85.0**

    Ad esempio, nell'area **impostazioni di Windows > app e funzionalità** scorrere verso il basso fino all'applicazione **Microsoft Azure Information Protection** e verificare il numero di versione.

    :::image type="content" source="media/client-about.png" alt-text="Verificare la versione del client di Azure Information Protection":::

## <a name="when-is-the-right-time-to-migrate-my-labels"></a>Quando è il momento giusto per eseguire la migrazione delle etichette?

Si consiglia di eseguire la migrazione delle etichette di Azure Information Protection alla piattaforma di etichettatura unificata in modo da poterle usare come etichette di riservatezza con altri [client e servizi che supportano l'etichettatura unificata](configure-policy-migrate-labels.md#clients-and-services-that-support-unified-labeling).

Per ulteriori informazioni e istruzioni, vedere [How to migrate Azure Information Protection labels to Unified Sensitivity labels](configure-policy-migrate-labels.md).

## <a name="after-ive-migrated-my-labels-which-management-portal-do-i-use"></a>Dopo aver eseguito la migrazione delle etichette, qual è il portale di gestione da usare?

Dopo aver eseguito la migrazione delle etichette nella portale di Azure, continuare a gestirle in una delle posizioni seguenti, a seconda dei client installati:

|Client  |Descrizione  |
|---------|---------|
|Solo [client e servizi con etichetta unificata](configure-policy-migrate-labels.md#clients-and-services-that-support-unified-labeling)    |  Se sono stati installati solo i client con etichetta unificata, gestire le etichette in uno dei centri di amministrazione: Office 365 Security & Compliance Center, Microsoft 365 Security Center o Microsoft 365 Compliance Center. I client di etichettatura unificata scaricano le etichette e le impostazioni dei criteri da uno di questi centri di amministrazione. <br /><br />Per istruzioni, vedere [creare e configurare etichette di riservatezza e i relativi criteri](/microsoft-365/compliance/create-sensitivity-labels).     |
|Solo [client classico](./rms-client/aip-client.md)  | Se è stata eseguita la migrazione delle etichette, ma è ancora installato il client classico, continuare a usare la portale di Azure per modificare le etichette e le impostazioni dei criteri. Il client classico continua a scaricare le etichette e le impostazioni dei criteri da Azure.
|Entrambi i [client AIP classico](./rms-client/aip-client.md) e [Unified Labeling](configure-policy-migrate-labels.md#clients-and-services-that-support-unified-labeling)     | Se sono installati entrambi i client, usare il centro di amministrazione o il portale di Azure per apportare modifiche alle etichette. <br /><br />Per consentire ai client classici di selezionare le modifiche alle etichette apportate nei centri di amministrazione, tornare al portale di Azure per pubblicarle. Nel riquadro portale di Azure > **Azure Information Protection-Unified Labeling** selezionare **pubblica**.  <br /><br /> Continuare a usare il portale di Azure per il [reporting centralizzato](reports-aip.md) e lo [scanner](deploy-aip-scanner.md).     |
| | |

## <a name="do-i-need-to-re-encrypt-my-files-after-moving-to-sensitivity-labels-and-the-unified-labeling-platform"></a>È necessario crittografare nuovamente i file dopo il passaggio a etichette di riservatezza e alla piattaforma di etichettatura unificata?

No, non è necessario crittografare di nuovo i file dopo il passaggio alle etichette di riservatezza e alla piattaforma di etichettatura unificata dopo la migrazione dal client AIP classico e le etichette gestite nella portale di Azure.

Dopo la migrazione, gestire le etichette e i criteri di etichetta dall'interfaccia di amministrazione di etichette, tra cui Microsoft Security Center, Microsoft Compliance Center o Microsoft Security & Compliance Center. 

Per ulteriori informazioni, vedere informazioni [sulle etichette di riservatezza](/microsoft-365/compliance/sensitivity-labels) nella documentazione di Microsoft 365 e il Blog relativo alla [migrazione dell'etichettatura unificata](https://techcommunity.microsoft.com/t5/microsoft-security-and/understanding-unified-labeling-migration/ba-p/783185) .


## <a name="whats-the-difference-between-azure-information-protection-and-azure-rights-management"></a>Quale è la differenza tra Azure Information Protection e Azure Rights Management?

Azure Information Protection (AIP) fornisce la classificazione, l'assegnazione di etichette e la protezione per i documenti e i messaggi di posta elettronica di un'organizzazione.

Il contenuto è protetto tramite il servizio Rights Management di Azure, che è ora un componente di AIP. 

Per altre informazioni, vedere [modalità di protezione dei dati in AIP](aip-classification-and-protection.md#how-aip-protects-your-data) e informazioni su [Azure Rights Management](what-is-azure-rms.md).

## <a name="whats-the-role-of-identity-management-for-azure-information-protection"></a>Qual è il ruolo di gestione delle identità per Azure Information Protection?

Gestione identità è un componente importante di AIP, perché gli utenti devono disporre di un nome utente e una password validi per accedere al contenuto protetto.

Per altre informazioni su come Azure Information Protection consente di proteggere i dati, vedere [Il ruolo di Azure Information Protection nella protezione dei dati](/enterprise-mobility-security/solutions/azure-information-protection-securing-data). 

## <a name="what-subscription-do-i-need-for-azure-information-protection-and-what-features-are-included"></a>Quale sottoscrizione è necessaria per Azure Information Protection e quali funzionalità sono incluse?

Per ulteriori informazioni sulle sottoscrizioni AIP, vedere le informazioni sulla sottoscrizione e l'elenco delle funzionalità nella pagina dei [prezzi Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection) .

Se si dispone di una sottoscrizione di Microsoft 365 che include la protezione dei dati di Azure Rights Management, scaricare il [foglio dati di Azure Information Protection Licensing](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf) per informazioni dettagliate sull'integrazione con AIP.

Per altre domande sulle licenze, cercare le risposte nella sezione [Domande frequenti sulle licenze](https://azure.microsoft.com/pricing/details/information-protection#faq).

## <a name="do-you-need-to-be-a-global-admin-to-configure-azure-information-protection-or-can-i-delegate-to-other-administrators"></a>È necessario essere un amministratore globale per configurare Azure Information Protection oppure tale configurazione può essere delegata ad altri amministratori?

Gli amministratori globali per un tenant Microsoft 365 o Azure AD possono ovviamente eseguire tutte le attività amministrative per Azure Information Protection. 

Tuttavia, se si desidera assegnare autorizzazioni amministrative ad altri utenti, utilizzare i ruoli seguenti:

- [Amministratore Azure Information Protection](#azure-information-protection-administrator)
- [Amministratore conformità o amministratore dati di conformità](#compliance-administrator-or-compliance-data-administrator)
- [Lettore di sicurezza o Reader globale](#security-reader-or-global-reader)
- [Amministratore della sicurezza](#security-administrator)
- [Amministratore globale di Azure Rights Management e amministratore del connettore](#azure-rights-management-global-administrator-and-connector-administrator)

Inoltre, tenere presente quanto segue quando si gestiscono ruoli e attività amministrative:

|Argomento  |Dettagli  |
|---------|---------|
|**Tipi di account supportati**     | Gli account Microsoft non sono supportati per l'amministrazione delegata di Azure Information Protection, anche se questi account sono assegnati a uno dei ruoli amministrativi elencati.         |
|**Controlli di onboarding**     |Se i [controlli di onboarding](activate-service.md#configuring-onboarding-controls-for-a-phased-deployment) sono stati configurati, ciò non influisce sulla possibilità di amministrare Azure Information Protection, fatta eccezione per il connettore RMS. <br /><br />Ad esempio, se sono stati configurati controlli di onboarding in modo che la capacità di proteggere il contenuto sia limitata al gruppo *reparto it* , l'account usato per installare e configurare il connettore RMS deve essere un membro di tale gruppo.          |
|**Rimozione della protezione**     |  Gli amministratori non possono rimuovere automaticamente la protezione da documenti o messaggi di posta elettronica protetti da Azure Information Protection. <br /><br />Solo gli utenti assegnati come utenti con privilegi avanzati possono rimuovere la protezione e solo quando la funzionalità per utenti con privilegi avanzati è abilitata. <br /><br />Tutti gli utenti con autorizzazioni amministrative per Azure Information Protection possono abilitare la funzionalità per utenti con privilegi avanzati e assegnare gli utenti come utenti con privilegi avanzati, incluso il proprio account.<br /><br />Queste azioni vengono registrate in un registro amministratore. <br /><br />Per ulteriori informazioni, vedere la sezione procedure ottimali di sicurezza in [configurazione di utenti con privilegi avanzati per Azure Information Protection e servizi di individuazione o ripristino dei dati](configure-super-users.md). <br><br>**Suggerimento**: se il contenuto è archiviato in SharePoint o OneDrive, gli amministratori possono eseguire il cmdlet [Unlock-SensitivityLabelEncryptedFile](/powershell/module/sharepoint-online/unlock-sposensitivitylabelencryptedfile) per rimuovere l'etichetta di riservatezza e la crittografia. Per altre informazioni, vedere la [documentazione di Microsoft 365](/microsoft-365/compliance/sensitivity-labels-sharepoint-onedrive-files#remove-encryption-for-a-labeled-document). |
|**Migrazione all'archivio di etichette unificato**      |  Se si esegue la migrazione delle etichette di Azure Information Protection all'archivio delle etichette unificate, assicurarsi di leggere la sezione seguente dalla documentazione relativa alla migrazione delle etichette: <br />[Ruoli amministrativi che supportano la piattaforma di assegnazione di etichette unificata](configure-policy-migrate-labels.md#administrative-roles-that-support-the-unified-labeling-platform). |
| | |
### <a name="azure-information-protection-administrator"></a>Amministratore di Azure Information Protection

Questo ruolo amministratore Azure Active Directory consente a un amministratore di configurare Azure Information Protection ma non altri servizi. 

Gli amministratori con questo ruolo possono:

- Attivare e disattivare il servizio Azure Rights Management Protection
- Configurare le etichette e le impostazioni di protezione
- Configurare i criteri di Azure Information Protection
- Eseguire tutti i cmdlet di PowerShell per il [client di Azure Information Protection](./rms-client/clientv2-admin-guide-powershell.md) e dal [modulo AIPService](administer-powershell.md)
    
Per assegnare un utente a questo ruolo amministrativo, vedere [Assegnare un utente ai ruoli di amministratore in Azure Active Directory](/azure/active-directory/active-directory-users-assign-role-azure-portal).

> [!NOTE]
> Questo ruolo non supporta il rilevamento e la revoca dei documenti per gli utenti e non è supportato nel portale di Azure se il tenant si trova nella [piattaforma di etichettatura unificata](#how-can-i-determine-if-my-tenant-is-on-the-unified-labeling-platform).
    
### <a name="compliance-administrator-or-compliance-data-administrator"></a>Amministratore conformità o amministratore dati di conformità

Questi ruoli di amministratore di Azure Active Directory consentono agli amministratori di:

- Configurare Azure Information Protection, inclusa l'attivazione e la disattivazione del servizio Azure Rights Management Protection
- Configurare le etichette e le impostazioni di protezione
- Configurare i criteri di Azure Information Protection
- Eseguire tutti i cmdlet di PowerShell per il [client Azure Information Protection](./rms-client/clientv2-admin-guide-powershell.md) e dal [modulo AIPService](administer-powershell.md). 

Per assegnare un utente a questo ruolo amministrativo, vedere [Assegnare un utente ai ruoli di amministratore in Azure Active Directory](/azure/active-directory/active-directory-users-assign-role-azure-portal). 

Per visualizzare le altre autorizzazioni di un utente con questi ruoli, vedere la sezione [ruoli disponibili](/azure/active-directory/active-directory-assign-admin-roles-azure-portal#available-roles) della documentazione Azure Active Directory.

> [!NOTE]
> Questi ruoli non supportano il rilevamento e la revoca dei documenti per gli utenti.
>     
    
### <a name="security-reader-or-global-reader"></a>Lettore di sicurezza o Reader globale

Questi ruoli vengono usati solo per [Azure Information Protection analisi](reports-aip.md) e consentono agli amministratori di:

- Visualizzare la modalità di utilizzo delle etichette
- Monitorare l'accesso degli utenti ai documenti e ai messaggi di posta elettronica con etichetta
- Visualizzare le modifiche apportate alla classificazione
- Identificare i documenti che contengono informazioni riservate che devono essere protette 

Poiché questa funzionalità USA monitoraggio di Azure, è necessario disporre anche di un ruolo di supporto [RBAC](reports-aip.md#permissions-required-for-azure-information-protection-analytics).

### <a name="security-administrator"></a>Amministratore della sicurezza

Questo ruolo Azure Active Directory amministratore consente agli amministratori di configurare Azure Information Protection nel portale di Azure, oltre ad alcuni aspetti di altri servizi di Azure. 

Gli amministratori con questo ruolo non possono eseguire alcun [cmdlet di PowerShell dal modulo AIPService](administer-powershell.md)oppure rilevare e revocare i documenti per gli utenti.
    
Per assegnare un utente a questo ruolo amministrativo, vedere [Assegnare un utente ai ruoli di amministratore in Azure Active Directory](/azure/active-directory/active-directory-users-assign-role-azure-portal). 

Per conoscere le altre autorizzazioni di cui dispone un utente con questo ruolo, vedere la sezione [Ruoli disponibili](/azure/active-directory/active-directory-assign-admin-roles-azure-portal#available-roles) della documentazione di Azure Active Directory.

### <a name="azure-rights-management-global-administrator-and-connector-administrator"></a>Amministratore globale di Azure Rights Management e amministratore del connettore

Il ruolo di amministratore globale consente agli utenti di eseguire tutti i [cmdlet di PowerShell dal modulo AIPService](administer-powershell.md) senza renderli un amministratore globale per altri servizi cloud.

Il ruolo di amministratore del connettore consente agli utenti di eseguire solo il connettore Rights Management (RMS). 

Questi ruoli amministrativi non concedono le autorizzazioni alle console di gestione oppure supportano il rilevamento e la revoca dei documenti per gli utenti.
    
Per assegnare uno di questi ruoli amministrativi, usare il cmdlet di PowerShell AIPService, [Add-AipServiceRoleBasedAdministrator](/powershell/module/aipservice/add-aipservicerolebasedadministrator).

## <a name="does-azure-information-protection-support-on-premises-and-hybrid-scenarios"></a>Azure Information Protection supporta scenari locali e ibridi?

Sì. Anche se è una soluzione basata sul cloud, Azure Information Protection può classificare, etichettare e proteggere documenti e messaggi di posta elettronica archiviati in locale, oltre che nel cloud.

Se si dispone di Exchange Server, SharePoint Server e file server di Windows, utilizzare uno o entrambi i metodi seguenti:

- Distribuire il [connettore Rights Management](deploy-rms-connector.md) in modo che questi server locali possano usare il servizio Rights Management di Azure per proteggere i messaggi di posta elettronica e i documenti
- Sincronizzare e federare i controller di dominio Active Directory con Azure AD per un'esperienza di autenticazione più semplice per gli utenti. Ad esempio, usare [Azure ad Connect](/azure/active-directory/hybrid/whatis-azure-ad-connect).

Il servizio Rights Management di Azure genera e gestisce automaticamente i certificati XrML come richiesto, quindi non usa un'infrastruttura PKI locale. 

Per ulteriori informazioni sull'utilizzo dei certificati in Azure Rights Management, vedere la [procedura dettagliata relativa al funzionamento di Azure RMS: primo utilizzo, protezione del contenuto,](./how-does-it-work.md#walkthrough-of-how-azure-rms-works-first-use-content-protection-content-consumption)utilizzo del contenuto.

## <a name="what-types-of-data-can-azure-information-protection-classify-and-protect"></a>Quali tipi di dati è possibile classificare e proteggere tramite Azure Information Protection?

Azure Information Protection consente di classificare e proteggere messaggi di posta elettronica e documenti, sia in locale che nel cloud. Questi documenti includono documenti di Word, fogli di calcolo di Excel, presentazioni di PowerPoint, documenti PDF, file di testo e file di immagine. 

Per ulteriori informazioni, vedere l'elenco completo dei [tipi di file supportati](./rms-client/clientv2-admin-guide-file-types.md).

> [!NOTE]
> Azure Information Protection non è in grado di classificare e proteggere i dati strutturati, ad esempio file di database, elementi del calendario, post Yammer, contenuto Sway e notebook di OneNote.
> 

> [!TIP]
> Power BI supporta la classificazione usando le etichette di riservatezza e può applicare la protezione da tali etichette ai dati esportati nei formati di file seguenti:. pdf,. xls e. ppt. Per altre informazioni, vedere [Protezione dei dati in Power BI](/power-bi/admin/service-security-data-protection-overview).
> 
## <a name="i-see-azure-information-protection-is-listed-as-an-available-cloud-app-for-conditional-accesshow-does-this-work"></a>Azure Information Protection è elencata come un'app cloud disponibile per l'accesso condizionale, come funziona?

Sì, come offerta di anteprima, è possibile configurare l'accesso condizionale Azure AD per Azure Information Protection.

Quando un utente apre un documento protetto da Azure Information Protection, gli amministratori possono ora bloccare o concedere l'accesso agli utenti nel tenant, in base ai controlli di accesso condizionale standard. La richiesta di autenticazione a più fattori (MFA) è una delle condizioni più comunemente richieste. Un'altra è che i dispositivi siano [conformi ai criteri di Intune](/intune/protect/conditional-access-intune-common-ways-use) in modo che, ad esempio, i dispositivi mobili soddisfino i requisiti relativi alle password e possiedano una versione minima del sistema operativo e i computer siano appartenenti a un dominio.

Per altre informazioni ed esempi di procedura dettagliata, vedere il post del blog [Conditional Access policies for Azure Information Protection](https://cloudblogs.microsoft.com/enterprisemobility/2017/10/17/conditional-access-policies-for-azure-information-protection/) (Criteri di accesso condizionale per Azure Information Protection).

Altre informazioni:

|Argomento  |Dettagli  |
|---------|---------|
|**Frequenza di valutazione**    | Per i computer Windows e la versione di anteprima corrente, i criteri di accesso condizionale per Azure Information Protection vengono valutati quando [viene inizializzato l'ambiente utente](./how-does-it-work.md#initializing-the-user-environment) (questo processo è noto anche come bootstrap) e quindi ogni 30 giorni.<br /><br />Per ottimizzare la frequenza con cui i criteri di accesso condizionale vengono valutati, [configurare la durata del token](/azure/active-directory/active-directory-configurable-token-lifetimes).       |
|**Account amministratore**     |Si consiglia di non aggiungere gli account amministratore ai criteri di accesso condizionale perché questi account non saranno in grado di accedere al riquadro Azure Information Protection nel portale di Azure.         |
|**Collaborazione tra multi-factor authentication e B2B**     | Se si usa l'autenticazione a più fattori nei criteri di accesso condizionale per la collaborazione con altre organizzazioni (B2B), è necessario usare la [collaborazione B2B di Azure AD](/azure/active-directory/b2b/what-is-b2b) e creare account guest per gli utenti con cui si vuole procedere alla condivisione nell'altra organizzazione.        |
|**Richieste di condizioni per l'utilizzo**     |  Con la versione di anteprima di Azure AD dicembre 2018, è ora possibile [richiedere agli utenti di accettare le condizioni](https://techcommunity.microsoft.com/t5/Azure-Active-Directory-Identity/Updates-to-Azure-AD-Terms-of-Use-functionality-within/ba-p/294822) per l'utilizzo prima di aprire un documento protetto per la prima volta.       |
|**App cloud**     |  Se si usano numerose app cloud per l'accesso condizionale, si potrebbe riscontrare che l'app **Microsoft Azure Information Protection** non viene visualizzata nell'elenco per la selezione. <br /><br />In questo caso, usare la casella di ricerca nella parte superiore dell'elenco. Iniziare a digitare "Microsoft Azure Information Protection" per filtrare le app disponibili. Se si ha una sottoscrizione supportata, l'app **Microsoft Azure Information Protection** verrà quindi visualizzata per la selezione.        |
| | |

> [!NOTE]
> Il supporto Azure Information Protection per l'accesso condizionale è attualmente in fase di anteprima. Le [condizioni aggiuntive per l'anteprima di Azure](https://azure.microsoft.com/support/legal/preview-supplemental-terms/) includono termini legali aggiuntivi che si applicano a funzionalità di Azure in versione beta, anteprima o diversamente non ancora disponibili a livello generale. 
> 

## <a name="i-see-azure-information-protection-is-listed-as-a-security-provider-for-microsoft-graph-securityhow-does-this-work-and-what-alerts-will-i-receive"></a>Azure Information Protection è elencato come provider di sicurezza per l'API Sicurezza di Microsoft Graph: come funziona e quali avvisi verranno inviati?

Nell'ambito dell'anteprima pubblica offerta è ora possibile ricevere un avviso per le **anomalie nell'accesso ai dati di Azure Information Protection**. Questo avviso viene attivato quando si verificano tentativi insoliti di accesso ai dati protetti da Azure Information Protection, ad esempio l'accesso a un volume insolitamente elevato di dati, in orari anomali o da una posizione sconosciuta.

Tali avvisi possono essere utili per rilevare gli attacchi avanzati relativi ai dati e le minacce interne nell'ambiente. Questi avvisi usano l'apprendimento automatico per analizzare il comportamento degli utenti che accedono ai dati protetti. 

È possibile accedere agli avvisi di Azure Information Protection [tramite l'API Sicurezza di Microsoft Graph](/graph/api/resources/security-api-overview) oppure è possibile [trasmettere avvisi](/graph/security-integration) a soluzioni SIEM come Splunk e IBM Qradar tramite Monitoraggio di Azure.

Per altre informazioni sull'API Sicurezza di Microsoft Graph, vedere [Microsoft Graph Security API overview](/graph/security-concept-overview) (Panoramica dell'API Sicurezza di Microsoft Graph).

> [!NOTE]
> Il supporto Azure Information Protection per Microsoft Graph Security è attualmente in fase di anteprima. Le [condizioni aggiuntive per l'anteprima di Azure](https://azure.microsoft.com/support/legal/preview-supplemental-terms/) includono termini legali aggiuntivi che si applicano a funzionalità di Azure in versione beta, anteprima o diversamente non ancora disponibili a livello generale. 
> 

## <a name="ive-heard-a-new-release-is-going-to-be-available-soon-for-azure-information-protectionwhen-will-it-be-released"></a>Ho sentito che una nuova versione sarà presto disponibile, per Azure Information Protection, quando verrà rilasciata?

La documentazione tecnica non contiene informazioni sulle versioni future. Per questo tipo di informazioni, usare la [Roadmap di Microsoft 365](https://www.microsoft.com/microsoft-365/roadmap?&filters=Azure%20Information%20Protection%2CO365%20Information%20Protection#owRoadmapMainContent), vedere il [Blog Enterprise Mobility + Security](https://techcommunity.microsoft.com/t5/Enterprise-Mobility-Security/bg-p/enterprisemobilityandsecurity?product=azure-information-protection,azure-rights-management-services).

## <a name="is-azure-information-protection-suitable-for-my-country"></a>Azure Information Protection è disponibile in tutti i paesi?

Paesi diversi hanno normative e requisiti differenti. Per ottenere una risposta a questa domanda per l'organizzazione specifica, vedere [Idoneità per paesi diversi](./compliance.md#suitability-for-different-countries).

## <a name="how-can-azure-information-protection-help-with-gdpr"></a>In quale modo Azure Information Protection può essere utile per il Regolamento generale sulla protezione dei dati?

[!INCLUDE [gdpr-hybrid-note](includes/gdpr-hybrid-note.md)]

## <a name="where-can-i-find-supporting-information-for-azure-information-protectionsuch-as-legal-compliance-and-slas"></a>Dov'è possibile reperire le informazioni di supporto per Azure Information Protection, ad esempio le note legali, le informazioni sulla conformità e i contratti di servizio?
Vedere [Informazioni su conformità e supporto per Azure Information Protection](./compliance.md).

## <a name="how-can-i-report-a-problem-or-send-feedback-for-azure-information-protection"></a>Come è possibile segnalare un problema o inviare commenti e suggerimenti per Azure Information Protection?

Per il supporto tecnico, usare i canali di supporto standard oppure [contattare il supporto tecnico Microsoft](information-support.md#to-contact-microsoft-support).

È anche possibile rivolgersi al team di ingegneri nel [sito di Yammer per Azure Information Protection](https://www.yammer.com/askipteam/). 

## <a name="what-do-i-do-if-my-question-isnt-here"></a>Cosa fare se la domanda non è presente?

Esaminare prima di tutto le domande frequenti elencate di seguito, specifiche per la classificazione e l'assegnazione di etichette, o specifiche per la protezione dei dati. Il [servizio Azure Rights Management (Azure RMS)](what-is-azure-rms.md) fornisce la tecnologia di protezione dei dati per Azure Information Protection. Azure RMS può essere usato con la classificazione e l'assegnazione di etichette o in modo indipendente. 

- [Domande frequenti per la classificazione e l'assegnazione di etichette](faqs-infoprotect.md)

- [Domande frequenti per la protezione dati](faqs-rms.md)

- [Domande frequenti solo per il client classico](faqs-classic.md)

Se la domanda non risponde, vedere i collegamenti e le risorse elencate in [informazioni e supporto per Azure Information Protection](information-support.md).
