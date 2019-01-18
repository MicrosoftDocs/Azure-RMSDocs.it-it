---
title: Preparare utenti e gruppi per Azure Information Protection
description: Controllare di avere gli account utente e di gruppo necessari per iniziare a classificare, etichettare e proteggere i documenti e i messaggi di posta elettronica dell'organizzazione.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 12/06/2018
ms.topic: conceptual
ms.service: information-protection
ms.assetid: afbca2d6-32a7-4bda-8aaf-9f93f5da5abc
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: e707e84ccfafc7b3ed161d05cadac9f2314ad3ae
ms.sourcegitcommit: 9dc6da0fb7f96b37ed8eadd43bacd1c8a1a55af8
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/18/2019
ms.locfileid: "54394290"
---
# <a name="preparing-users-and-groups-for-azure-information-protection"></a>Preparazione di utenti e gruppi per Azure Information Protection

>*Si applica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

Prima di distribuire Azure Information Protection per l'organizzazione, assicurarsi che siano disponibili gli account necessari per gli utenti e i gruppi in Azure AD per il tenant dell'organizzazione.

È possibile creare gli account per utenti e gruppi in modi diversi:

- Creando gli utenti nell'interfaccia di amministrazione di Office 365 e i gruppi nell'interfaccia di amministrazione di Exchange Online.

- Creando gli utenti e i gruppi nel portale di Azure.

- Creando gli utenti e i gruppi tramite cmdlet di Azure AD PowerShell e di Exchange Online.

- Creando utenti e gruppi in Active Directory locale e sincronizzandoli in Azure AD.

- Creando utenti e gruppi in un'altra directory e sincronizzandoli in Azure AD.

Se si usano i primi tre metodi dell'elenco, gli utenti e i gruppi vengono creati automaticamente in Azure AD e i relativi account possono essere usati direttamente in Azure Information Protection. Molte reti aziendali, tuttavia, creano e gestiscono utenti e gruppi all'interno di una directory locale. Azure Information Protection non è in grado si usare direttamente questi account, che devono pertanto essere sincronizzati in AD.

## <a name="how-users-and-groups-are-used-by-azure-information-protection"></a>Uso di utenti e gruppi con Azure Information Protection

Sono possibili tre scenari di uso di utenti e gruppi con Azure Information Protection:

**Assegnazione di etichette agli utenti** al momento della configurazione dei criteri di Azure Information Protection, per consentire l'applicazione di etichette ai documenti e ai messaggi di posta elettronica. Solo gli amministratori possono selezionare questi utenti e questi gruppi:

- I criteri di Azure Information Protection predefiniti vengono assegnati automaticamente a tutti gli utenti all'interno di Azure AD del tenant. È anche possibile, tuttavia, assegnare etichette aggiuntive a utenti o gruppi specifici tramite criteri con ambito.     

**Assegnazione di diritti di utilizzo e di controlli di accesso** se per la protezione di documenti e messaggi di posta elettronica si usa il servizio Azure Rights Management. Gli amministratori e gli utenti possono selezionare questi utenti e questi gruppi:

- I diritti di utilizzo determinano se un utente può aprire un documento o un messaggio di posta elettronica e come può usarlo, ad esempio se può solo leggerlo, leggerlo e stamparlo o leggerlo e modificarlo. 

- I controlli di accesso includono una data di scadenza e specificano se per l'accesso è necessaria una connessione a Internet. 

**Configurazione del servizio Azure Rights Management** per il supporto di scenari specifici. Pertanto solo gli amministratori possono selezionare questi gruppi. Ecco alcuni esempi di elementi configurabili:

- Utenti con privilegi avanzati. I servizi o gli utenti designati possono aprire contenuto crittografato, se necessario a scopo di eDiscovery o recupero dei dati.

- Amministrazione delegata del servizio Azure Rights Management.

- Controlli di onboarding a supporto di una distribuzione a più fasi.

## <a name="azure-information-protection-requirements-for-user-accounts"></a>Requisiti di Azure Information Protection per gli account utente

Per l'assegnazione di etichette:

- Tutti gli account utente in Azure AD possono essere usati per configurare criteri con ambito che consentono di assegnare etichette aggiuntive agli utenti.

Per assegnare diritti di utilizzo e controlli di accesso e configurare il servizio Azure Rights Management:

- Per autorizzare utenti, si usano due attributi di Azure AD: **proxyAddresses** e **userPrincipalName**.

- Nell'attributo **proxyAddresses di Azure AD**, in cui vengono archiviati tutti gli indirizzi di posta elettronica di un account, è possibile inserire valori in modi diversi. Ad esempio a un utente di Office 365 che dispone di una cassetta postale di Exchange Online viene assegnato automaticamente un indirizzo di posta elettronica memorizzato in questo attributo. Se a un utente di Office 365 si assegna un indirizzo di posta elettronica alternativo, anche quest'ultimo viene salvato nell'attributo proxyAddresses. Nell'attributo è possibile archiviare anche indirizzi di posta elettronica provenienti dalla sincronizzazione con account locali. 

    Azure Information Protection può usare qualsiasi valore dell'attributo proxyAddresses di Azure AD se il dominio è stato aggiunto al tenant dell'utente ("dominio verificato"). Per altre informazioni sulla verifica di domini:

    - Per Azure AD: [Aggiungere un nome di dominio personalizzato ad Azure Active Directory](/azure/active-directory/fundamentals/add-custom-domain)

    - Per Office 365: [Aggiungere un dominio a Office 365](/office365/admin/setup/add-domain?view=o365-worldwide)

- L'attributo **userPrincipalName di Azure AD** viene usato solo se per un account nel tenant non sono presenti valori nell'attributo proxyAddresses di Azure AD, ad esempio se nel portale di Azure o per Office 365 si crea un utente senza una cassetta postale.

### <a name="assigning-usage-rights-and-access-controls-to-external-users"></a>Assegnazione di diritti di utilizzo e di controlli di accesso a utenti esterni

Oltre che per autorizzare gli utenti del tenant, Azure Information Protection usa gli attributi proxyAddresses e userPrincipalName di Azure AD allo stesso modo per autorizzare gli utenti di un altro tenant.

Altri metodi di autorizzazione:

- Azure Information Protection può autorizzare gli indirizzi di posta elettronica che non si trovano in Azure AD quando questi vengono autenticati con un account Microsoft. Non tutte le applicazioni, tuttavia, possono aprire contenuti protetti quando viene usato un account Microsoft per l'autenticazione. [Altre informazioni](./secure-collaboration-documents.md#supported-scenarios-for-opening-protected-documents)

- Quando si invia un messaggio e-mail crittografato tramite Office 365 Message Encryption con nuove funzionalità a un utente che non ha un account in Azure AD, l'autenticazione dell'utente viene eseguita tramite la federazione con un provider di identità basato su social network oppure con un passcode monouso. L'indirizzo e-mail specificato nel messaggio di posta elettronica protetto viene quindi usato per l'autorizzazione dell'utente.

## <a name="azure-information-protection-requirements-for-group-accounts"></a>Requisiti di Azure Information Protection per gli account di gruppo

Per l'assegnazione di etichette:

- Per configurare criteri con ambito che assegnano etichette aggiuntive a membri del gruppo è possibile usare qualsiasi tipo di gruppo di Azure AD che ha un indirizzo di posta elettronica con un dominio verificato per il tenant dell'utente. Un gruppo dotato di un indirizzo di posta elettronica è spesso detto "gruppo abilitato alla posta elettronica".

    È ad esempio possibile usare un gruppo di sicurezza abilitato alla posta elettronica, un gruppo di distribuzione (che può essere statico o dinamico) e un gruppo di Office 365. Non è possibile usare un gruppo di sicurezza (statico o dinamico), perché questo tipo di gruppo non ha un indirizzo di posta elettronica.

Per l'assegnazione di diritti di utilizzo e di controlli di accesso:

- È possibile usare qualsiasi tipo di gruppo in Azure AD che abbia un indirizzo di posta elettronica con un dominio verificato per il tenant dell'utente. Un gruppo dotato di un indirizzo di posta elettronica è spesso detto "gruppo abilitato alla posta elettronica". 

Per la configurazione del servizio Rights Management di Azure:

- È possibile usare qualsiasi tipo di gruppo in Azure AD che abbia un indirizzo di posta elettronica con un dominio verificato per il tenant, con un'eccezione: quando si configurano controlli di onboarding per l'uso di un gruppo, quest'ultimo deve essere un gruppo di sicurezza in Azure AD per il tenant.

- Per l'amministrazione delegata del servizio Azure Rights Management è possibile usare qualsiasi gruppo in Azure AD (con o senza un indirizzo e-mail) di un dominio verificato nel tenant.

### <a name="assigning-usage-rights-and-access-controls-to-external-groups"></a>Assegnazione di diritti di utilizzo e di controlli di accesso a gruppi esterni

Oltre che per autorizzare i gruppi del tenant, Azure Information Protection usa l'attributo proxyAddresses di Azure AD allo stesso modo per autorizzare i gruppi di un altro tenant.

## <a name="using-accounts-from-active-directory-on-premises-for-azure-information-protection"></a>Uso di account di Active Directory locale per Azure Information Protection

Se con Azure Information Protection si vogliono usare account gestiti in locale, è necessario sincronizzare questi ultimi in Azure AD. Per semplificare la distribuzione, è consigliabile usare [Azure AD Connect](/azure/active-directory/hybrid/whatis-azure-ad-connect). È tuttavia possibile usare qualsiasi metodo di sincronizzazione di directory che consenta di ottenere lo stesso risultato.

Quando si sincronizzano gli account, non è necessario sincronizzare tutti gli attributi. Per l'elenco degli attributi che devono essere sincronizzati, vedere la [sezione relativa ad Azure RMS](/azure/active-directory/connect/active-directory-aadconnectsync-attributes-synchronized#azure-rms) nella documentazione di Azure Active Directory.

Dall'elenco degli attributi per Azure Rights Management risulta che, per gli utenti, gli attributi di AD locale richiesti per la sincronizzazione sono **mail**, **proxyAddresses** e **userPrincipalName**. I valori di **mail** e **proxyAddresses** vengono sincronizzati nell'attributo proxyAddresses di Azure AD. Per altre informazioni, vedere [How the proxyAddresses attribute is populated in Azure AD](https://support.microsoft.com/help/3190357/how-the-proxyaddresses-attribute-is-populated-in-azure-ad) (Come vengono inseriti valori nell'attributo proxyAddresses di Azure AD)

## <a name="confirming-your-users-and-groups-are-prepared-for-azure-information-protection"></a>Verifica della preparazione di utenti e gruppi per Azure Information Protection

È possibile usare Azure AD PowerShell per confermare che utenti e gruppi possono essere usati con Azure Information Protection. È possibile usare PowerShell anche per confermare i valori utilizzabili per autorizzare gli utenti e i gruppi. 

Ad esempio, usando il modulo PowerShell V1 per Azure Active Directory, [MSOnline](/powershell/module/msonline/?view=azureadps-1.0), in una sessione di PowerShell, connettersi prima di tutto al servizio, specificando credenziali di amministratore globale:

    Connect-MsolService


Nota: se questo comando non funziona, è possibile eseguire `Install-Module MSOnline` per installare il modulo MSOnline.

Configurare quindi la sessione di PowerShell in modo che non consenta il troncamento dei valori:

    $Formatenumerationlimit =-1

### <a name="confirm-user-accounts-are-ready-for-azure-information-protection"></a>Confermare che gli account utente sono pronti per Azure Information Protection

Per confermare gli account utente, eseguire il comando seguente:

    Get-Msoluser | select DisplayName, UserPrincipalName, ProxyAddresses

Assicurarsi prima di tutto che siano visualizzati gli utenti che si vogliono usare con Azure Information Protection.

Controllare quindi se la colonna **ProxyAddresses** è popolata. In caso affermativo, gli indirizzi e-mail di questa colonna possono essere usati per l'autorizzazione dei rispettivi utenti per Azure Information Protection.

Se la colonna **ProxyAddresses** non è popolata, l'autorizzazione dell'utente per il servizio Azure Rights Management viene effettuata con il valore presente in **UserPrincipalName**.

Ad esempio:


|  Nome visualizzato   |     UserPrincipalName      |                            ProxyAddresses                             |
|-----------------|----------------------------|-----------------------------------------------------------------------|
| Jagannath Reddy | jagannathreddy@contoso.com |                                  {}                                   |
|    Ankur Roy    |    ankurroy@contoso.com    | {SMTP:ankur.roy@contoso.com, smtp: ankur.roy@onmicrosoft.contoso.com} |

In questo esempio:

- Per l'autorizzazione dell'account utente di Jagannath Reddy verrà usato l'indirizzo <strong>jagannathreddy@contoso.com</strong>.

- L'autorizzazione dell'account utente di Ankur Roy può essere effettuata tramite <strong>ankur.roy@contoso.com</strong> e <strong>ankur.roy@onmicrosoft.contoso.com</strong>, ma non tramite <strong>ankurroy@contoso.com</strong>.

Nella maggior parte dei casi il valore di UserPrincipalName corrisponde a uno dei valori presenti nel campo ProxyAddresses. Questa è la configurazione consigliata, ma se non è possibile modificare il nome UPN in modo che corrisponda all'indirizzo di posta elettronica, è necessario eseguire la procedura seguente:

1. Se il nome di dominio nel valore relativo al nome UPN è un dominio verificato per il tenant di Azure AD, aggiungere il nome UPN come indirizzo di posta elettronica aggiuntivo in Azure AD. In questo modo sarà possibile usare il valore relativo al nome UPN per l'autorizzazione dell'account utente per Azure Information Protection.

    Se il nome di dominio nel valore UPN non è un dominio verificato per il tenant, non può essere usato con Azure Information Protection. È tuttavia ancora possibile autorizzare l'utente come membro di un gruppo se l'indirizzo di posta elettronica del gruppo usa un nome di dominio verificato.

2. Se il nome UPN non è indirizzabile (come, ad esempio, <strong>ankurroy@contoso.local</strong>), configurare un ID di accesso alternativo per gli utenti, fornendo a questi ultimi le istruzioni necessarie per l'accesso a Office tramite questo ID. È anche necessario impostare una chiave del Registro di sistema per Office.

    Per altre informazioni, vedere [Configurazione di ID di accesso alternativo](/windows-server/identity/ad-fs/operations/configuring-alternate-login-id) e [Le applicazioni di Office richiedono periodicamente le credenziali per SharePoint Online, OneDrive e Lync Online](https://support.microsoft.com/help/2913639/office-applications-periodically-prompt-for-credentials-to-sharepoint-online,-onedrive,-and-lync-online).

> [!TIP]
> Per una gestione più semplice, ad esempio per eseguire ricerche e modifiche in blocco per l'importazione, è possibile usare il cmdlet Export-Csv per esportare i risultati in un foglio di calcolo.
>
> ad esempio `Get-MsolGroup | select DisplayName, ProxyAddresses | Export-Csv -Path UserAccounts.csv`

### <a name="confirm-group-accounts-are-ready-for-azure-information-protection"></a>Confermare che gli account di gruppo sono pronti per Azure Information Protection

Per confermare gli account di gruppo, usare il comando seguente:

    Get-MsolGroup | select DisplayName, ProxyAddresses

Assicurarsi che siano visualizzati i gruppi che si vogliono usare con Azure Information Protection. Per l'autorizzazione dei membri dei gruppi visualizzati per il servizio Azure Rights Management è possibile usare gli indirizzi di posta elettronica nella colonna **ProxyAddresses**.

Controllare quindi che i gruppi contengano gli utenti (o gli altri gruppi) che si vogliono usare per Azure Information Protection. A tale scopo è possibile usare un cmdlet di PowerShell (ad esempio, [Get-MsolGroupMember](/powershell/module/msonline/Get-MsolGroupMember?view=azureadps-1.0)) o il portale di gestione.

Per i due scenari di configurazione del servizio Azure Rights Management che usano gruppi di sicurezza, è possibile trovare l'ID oggetto e il nome visualizzato che consentono di identificare questi gruppi tramite il comando PowerShell seguente. Per trovare questi gruppi e copiare i valori relativi all'ID oggetto e al nome visualizzato, è anche possibile usare il portale di Azure:

    Get-MsolGroup | where {$_.GroupType -eq "Security"}

## <a name="considerations-for-azure-information-protection-if-email-addresses-change"></a>Considerazioni su Azure Information Protection in caso di modifica di indirizzi di posta elettronica

Se si modifica l'indirizzo di posta elettronica di un utente o di un gruppo, è consigliabile aggiungere l'indirizzo di posta elettronica precedente come secondo indirizzo di posta elettronica (detto anche indirizzo proxy, alias o indirizzo di posta elettronica alternativo) per l'utente o il gruppo. Quando si esegue questa operazione, l'indirizzo di posta elettronica precedente viene aggiunto all'attributo proxyAddresses di Azure AD. Questo tipo di amministrazione degli account garantisce la continuità aziendale per i diritti di utilizzo e per le altre configurazioni salvate quando era in uso l'indirizzo di posta elettronica precedente. 

Se non è possibile eseguire questa operazione, all'utente o al gruppo con il nuovo indirizzo di posta elettronica potrebbe essere negato l'accesso a documenti e messaggi di posta elettronica protetti in precedenza con l'indirizzo di posta elettronica precedente. In questo caso, è necessario ripetere la configurazione di protezione per salvare il nuovo indirizzo di posta elettronica. Ad esempio, se all'utente o al gruppo sono stati concessi i diritti di utilizzo nei modelli o nelle etichette, modificare i modelli o le etichette e specificare il nuovo indirizzo di posta elettronica con gli stessi diritti di utilizzo concessi all'indirizzo di posta elettronica precedente.

Si noti che è raro che per un gruppo venga modificato l'indirizzo di posta elettronica. Se si assegnano diritti di utilizzo a un gruppo anziché a utenti singoli e l'indirizzo di posta elettronica di uno o più utenti cambia, non si verificano problemi. In questo scenario, i diritti di utilizzo vengono assegnati all'indirizzo di posta elettronica del gruppi e non agli indirizzi di posta elettronica dei singoli utenti. Questo è il metodo usato dagli amministratori con maggiore frequenza, oltre che il metodo consigliato, per la configurazione dei diritti di utilizzo che proteggono documenti e messaggi di posta elettronica. In genere, tuttavia, gli utenti assegnano autorizzazioni personalizzate a utenti singoli. Poiché non è sempre possibile sapere se per concedere l'accesso è stato usato un account utente o di gruppo, il metodo più sicuro è aggiungere sempre l'indirizzo di posta elettronica precedente come secondo indirizzo di posta elettronica.

## <a name="group-membership-caching-by-azure-information-protection"></a>Memorizzazione nella cache di appartenenza a gruppi di Azure Information Protection

Per motivi di prestazioni, Azure Information Protection memorizza nella cache di appartenenza a gruppi. È quindi possibile che le modifiche apportate all'appartenenza a gruppi in Azure AD abbiano effetto tre ore dopo se tali gruppi vengono usati da Azure Information Protection. Questo lasso di tempo è soggetto a variazioni. 

Considerare questo ritardo nelle modifiche o nell'esecuzione di test, ad esempio quando vengono concessi i diritti di utilizzo, viene configurato il servizio Azure Rights Management, oppure quando vengono configurati i criteri con ambito.


## <a name="next-steps"></a>Passaggi successivi

Dopo aver confermato che gli utenti e i gruppi sono utilizzabili con Azure Information Protection e che tutto è pronto per iniziare ad applicare la protezione a documenti e messaggi di posta elettronica, controllare se è necessario attivare il servizio Rights Management. Per proteggere i documenti e i messaggi di posta elettronica dell'organizzazione, prima attivare questo servizio: 

- A partire da febbraio 2018: se la sottoscrizione che include Azure Rights Management o Azure Information Protection risale al mese di febbraio 2018 o a un mese successivo, il servizio viene attivato automaticamente. 

- Se la sottoscrizione risale a prima di febbraio 2018: è necessario attivare il servizio manualmente. 

Per altre informazioni sul controllo dello stato di attivazione, vedere [Attivazione di Azure Rights Management](./activate-service.md).

