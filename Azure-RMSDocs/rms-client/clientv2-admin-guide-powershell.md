---
title: Usare PowerShell con il client di etichettatura unificato Azure Information Protection
description: Istruzioni e informazioni per gli amministratori per la gestione del client Azure Information Protection Unified Labeling usando PowerShell.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 01/14/2021
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: v2client
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 2a4bd98e22789e71cf090efb4c83a2a1ba000df2
ms.sourcegitcommit: f6d536b6a3b5e14e24f0b9e58d17a3136810213b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/26/2021
ms.locfileid: "98809908"
---
# <a name="admin-guide-using-powershell-with-the-azure-information-protection-unified-client"></a>Guida dell'amministratore: uso di PowerShell con il client unificato di Azure Information Protection

>***Si applica a**: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8, Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012 *
>
>*Se si dispone di Windows 7 o Office 2010, vedere [AIP e versioni legacy di Windows e Office](../known-issues.md#aip-and-legacy-windows-and-office-versions).*
>
>***Pertinente per**: [Azure Information Protection client di etichetta unificato per Windows](../faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients). Per il client classico, vedere la [Guida dell'amministratore del client classico](client-admin-guide-powershell.md). *

Quando si installa il client Azure Information Protection Unified Labeling, i comandi di PowerShell vengono installati automaticamente come parte del modulo [AzureInformationProtection](/powershell/module/azureinformationprotection) , con i cmdlet per l'assegnazione di etichette. 

Il modulo **AzureInformationProtection** consente di gestire il client eseguendo comandi per gli script di automazione.

Ad esempio:

- [Get-AIPFileStatus](/powershell/module/azureinformationprotection/get-aipfilestatus): Ottiene l'etichetta Azure Information Protection e le informazioni di protezione per un file o file specificato.
- [Set-AIPFileClassification](/powershell/module/azureinformationprotection/set-aipfileclassification): esegue l'analisi di un file per impostare automaticamente un'etichetta di Azure Information Protection per un file, in base alle condizioni configurate nei criteri.
- [Set-AIPFileLabel](/powershell/module/azureinformationprotection/set-aipfilelabel): imposta o rimuove un'etichetta Azure Information Protection per un file e imposta o rimuove la protezione in base alla configurazione dell'etichetta o alle autorizzazioni personalizzate.
- [Set-AIPAuthentication](/powershell/module/azureinformationprotection/set-aipauthentication): imposta le credenziali di autenticazione per il client di Azure Information Protection.

Il modulo **AzureInformationProtection** viene installato nella cartella **\Programmi (x86) \Microsoft Azure Information Protection** e quindi aggiunge la cartella alla variabile di sistema **PSModulePath** . Il file DLL per questo modulo si chiama **AIP.dll**.

> [!IMPORTANT]
> Il modulo **AzureInformationProtection** non supporta la configurazione delle impostazioni avanzate per le etichette o i criteri di etichetta. 
>
>Per queste impostazioni, è necessario Office 365 Security & Compliance Center PowerShell. Per ulteriori informazioni, vedere [Custom Configurations for the Azure Information Protection Unified Labeling client](clientv2-admin-guide-customizations.md).

> [!TIP]
> Per usare cmdlet con percorsi di lunghezza superiore a 260 caratteri, usare l'[impostazione di Criteri di gruppo](/archive/blogs/jeremykuhne/net-4-6-2-and-long-paths-on-windows-10) seguente disponibile a partire da Windows 10 versione 1607:<br /> Criteri del computer **locale**  >  **Configurazione computer**  >  **Modelli amministrativi**  >  **Tutte le impostazioni**  >  **Abilita percorsi lunghi Win32** 
> 
> Per Windows Server 2016 è possibile usare la stessa impostazione di Criteri di gruppo quando si installano i modelli amministrativi più recenti (con estensione admx) per Windows 10.
>
> Per altre informazioni, vedere la sezione [Maximum Path Length Limitation](/windows/desktop/FileIO/naming-a-file#maximum-path-length-limitation) (Limite massimo lunghezza del percorso) della documentazione per sviluppatori di Windows 10.

## <a name="prerequisites-for-using-the-azureinformationprotection-module"></a>Prerequisiti per l'uso del modulo AzureInformationProtection

Oltre ai prerequisiti per l'installazione del modulo **AzureInformationProtection** , esistono prerequisiti aggiuntivi per l'uso dei cmdlet di assegnazione di etichette per Azure Information Protection:

- **Il servizio Rights Management di Azure deve essere attivato**.

    Se il tenant di Azure Information Protection non è attivato, vedere le istruzioni per l' [attivazione del servizio di protezione da Azure Information Protection](../activate-service.md).

- **Per rimuovere la protezione dai file per altri utenti tramite il proprio account**:

    - La funzionalità per [utenti con privilegi avanzati](../configure-super-users.md) deve essere abilitata per l'organizzazione.
    - L'account deve essere configurato come utente con privilegi avanzati per Azure Rights Management.

    È ad esempio possibile che si desideri rimuovere la protezione per altri utenti a scopo di individuazione o ripristino dei dati. Se si usano etichette per applicare la protezione, è possibile rimuovere la protezione impostando una nuova etichetta che non applica la protezione oppure è possibile rimuovere l'etichetta.

    Per rimuovere la protezione, usare il cmdlet [set-AIPFileLabel](/powershell/module/azureinformationprotection/set-aipfilelabel) con il parametro *RemoveProtection* . Per impostazione predefinita, la funzionalità di rimozione della protezione è disabilitata e deve essere abilitata usando il cmdlet [set-LabelPolicy](/powershell/module/azureinformationprotection/set-labelpolicy) .

## <a name="rms-to-unified-labeling-cmdlet-mapping"></a>Mapping dei cmdlet da RMS a Unified Labeling

Se è stata eseguita la migrazione da Azure RMS, si noti che i cmdlet correlati a RMS sono stati deprecati per l'uso in un'etichetta unificata. 

Alcuni cmdlet legacy sono stati sostituiti con nuovi cmdlet per l'assegnazione di etichette unificata. Ad esempio, se è stato usato **New-RMSProtectionLicense** con la protezione RMS ed è stata eseguita la migrazione all'etichettatura unificata, usare invece **New-AIPCustomPermissions** .

La tabella seguente mappa i cmdlet correlati a RMS con i cmdlet aggiornati usati per l'assegnazione di etichette unificata:

|Cmdlet di RMS  |Cmdlet Unified Labeling  |
|---------|---------|
|[Get-Rmsfilestatus successivamente](/powershell/module/azureinformationprotection/get-rmsfilestatus)     |  [Get-AIPFileStatus](/powershell/module/azureinformationprotection/get-aipfilestatus)        |
|[Get-RMSServer](/powershell/module/azureinformationprotection/get-rmsserver)     |  Non pertinente per l'etichettatura unificata.      |
|[Get-RMSServerAuthentication](/powershell/module/azureinformationprotection/get-rmsserverauthentication)      |   [Set-AIPAuthentication](/powershell/module/azureinformationprotection/set-aipauthentication)       |
|[Clear-RMSAuthentication](/powershell/module/azureinformationprotection/clear-rmsauthentication)     | [Set-AIPAuthentication](/powershell/module/azureinformationprotection/set-aipauthentication)       |
|[Set-RMSServerAuthentication](/powershell/module/azureinformationprotection/set-rmsserverauthentication)     |  [Set-AIPAuthentication](/powershell/module/azureinformationprotection/set-aipauthentication)      |
|[Get-RMSTemplate](/powershell/module/azureinformationprotection/get-rmstemplate)     |       Non pertinente per l'etichettatura unificata  |
|[New-RMSProtectionLicense](/powershell/module/azureinformationprotection/new-rmsprotectionlicense)     |  [New-AIPCustomPermissions](/powershell/module/azureinformationprotection/new-aipcustompermissions)e [set-AIPFileLabel](/powershell/module/azureinformationprotection/set-aipfilelabel)con il parametro **CustomPermissions**      |
|[Proteggi-RMSFile](/powershell/module/azureinformationprotection/protect-rmsfile) |[Set-AIPFileLabel](/powershell/module/azureinformationprotection/set-aipfilelabel), con il parametro **RemoveProtection** |
| | |


## <a name="how-to-label-files-non-interactively-for-azure-information-protection"></a>Come assegnare un'etichetta ai file in modo non interattivo per Azure Information Protection

Per impostazione predefinita, quando si eseguono i cmdlet per l'assegnazione di etichette, i comandi vengono eseguiti nel contesto utente personale in una sessione interattiva di PowerShell.

Per altre informazioni, vedere:

- [Prerequisiti per l'esecuzione automatica dei cmdlet di assegnazione di etichette AIP](#prerequisites-for-running-aip-labeling-cmdlets-unattended)
- [Creare e configurare applicazioni Azure AD per set-AIPAuthentication](#create-and-configure-azure-ad-applications-for-set-aipauthentication)
- [Esecuzione del cmdlet Set-AIPAuthentication](#running-the-set-aipauthentication-cmdlet)

> [!NOTE]
> Se il computer non può accedere a Internet, non è necessario creare l'app in Azure AD ed eseguire il cmdlet **set-AIPAuthentication** . Seguire invece le istruzioni per i [computer disconnessi](clientv2-admin-guide-customizations.md#support-for-disconnected-computers).  

### <a name="prerequisites-for-running-aip-labeling-cmdlets-unattended"></a>Prerequisiti per l'esecuzione automatica dei cmdlet di assegnazione di etichette AIP

Per eseguire Azure Information Protection i cmdlet di assegnazione automatica delle etichette, usare i dettagli di accesso seguenti:

- **Un account di Windows** in grado di accedere in modo interattivo.

- **Un account Azure ad**, per l'accesso delegato. Per semplificare l'amministrazione, usare un singolo account sincronizzato da Active Directory a Azure AD.

    Per l'account utente delegato:

    |Requisito  |Dettagli  |
    |---------|---------|
    |**Criteri etichetta**     |  Assicurarsi di disporre di un criterio di etichetta assegnato a questo account e che il criterio includa le etichette pubblicate che si desidera utilizzare.   <br><br>Se si usano criteri di etichetta per utenti diversi, potrebbe essere necessario creare nuovi criteri di etichetta che pubblichino tutte le etichette e pubblicare i criteri solo in questo account utente delegato.    |
    |**Decrittografia di contenuto**     |    Se questo account deve decrittografare il contenuto, ad esempio per riproteggere i file e controllare i file protetti da altri utenti, renderlo un [utente con privilegi](../configure-super-users.md) avanzati per Azure Information Protection e assicurarsi che la funzionalità per utenti con privilegi avanzati sia abilitata.     |
    |**Controlli di onboarding**     |    Se sono stati implementati i [controlli di onboarding](../activate-service.md#configuring-onboarding-controls-for-a-phased-deployment) per una distribuzione in più fasi, assicurarsi che questo account sia incluso nei controlli di onboarding configurati.     |
    |     |         |

- **Un token di accesso Azure ad**, che imposta e archivia le credenziali per l'utente delegato per l'autenticazione a Azure Information Protection. Quando il token in Azure AD scade, è necessario eseguire nuovamente il cmdlet per acquisire un nuovo token. 

    I parametri per **set-AIPAuthentication** usano i valori di un processo di registrazione delle app in Azure ad. Per altre informazioni, vedere [creare e configurare applicazioni Azure ad per set-AIPAuthentication](#create-and-configure-azure-ad-applications-for-set-aipauthentication).

Eseguire i cmdlet di assegnazione di etichette in modo non interattivo eseguendo prima il cmdlet [set-AIPAuthentication](/powershell/module/azureinformationprotection/set-aipauthentication) .

Il computer che esegue il cmdlet **AIPAuthentication** Scarica i criteri di assegnazione delle etichette assegnati all'account utente delegato nel centro di gestione delle etichette, ad esempio il Microsoft 365 Security & Compliance Center.

### <a name="create-and-configure-azure-ad-applications-for-set-aipauthentication"></a>Creare e configurare applicazioni Azure AD per Set-AIPAuthentication

Il cmdlet **set-AIPAuthentication** richiede una registrazione dell'app per i parametri *AppID* e *AppSecret* . 

Per gli utenti che hanno eseguito di recente la migrazione dal client classico e hanno creato una registrazione dell'app per i parametri *webappid* e *NativeAppId* precedenti, è necessario creare una nuova registrazione dell'app per il client di etichettatura unificata.

**Per creare una nuova registrazione dell'app per il cmdlet Unified Labeling client Set-AIPAuthentication**:

1. In una nuova finestra del browser accedere alla [portale di Azure](https://portal.azure.com/) al tenant di Azure ad usato con Azure Information Protection.

1. Passare a **Azure Active Directory**  >  **Gestisci**  >  **registrazioni app** e selezionare **nuova registrazione**. 

1. Nel riquadro **registra un'applicazione** specificare i valori seguenti e quindi fare clic su **registra**:

    |Opzione  |Valore  |
    |---------|---------|
    |**Nome**     |  `AIP-DelegatedUser` <br>Specificare un nome diverso in base alle esigenze. Il nome deve essere univoco per ogni tenant.       |
    |**Tipi di account supportati**     |   Selezionare **Account solo in questa directory dell'organizzazione**.      |
    |**URI di reindirizzamento (facoltativo)**     |     Selezionare **Web**, quindi immettere `https://localhost` .    |
    |     |         |

1. Nel riquadro **AIP-DelegatedUser** , copiare il valore per l' **ID applicazione (client)**. 

    Il valore è simile all'esempio seguente: `77c3c1c3-abf9-404e-8b2b-4652836c8c66` . 

    Questo valore viene usato per il parametro *AppID* quando si esegue il **cmdlet Set-AIPAuthentication**. Incollare e salvare il valore per riferimento successivo.

1. Dalla barra laterale selezionare **Gestisci**  >  **certificati & segreti**.

    Quindi, nel riquadro dei segreti client **AIP-DelegatedUser-certificates &** , nella sezione **Secrets client** Selezionare **New client Secret**.

1. Per **Aggiungi un segreto client**, specificare quanto segue e quindi selezionare **Aggiungi**:

    |Campo  |Valore  |
    |---------|---------|
    |**Descrizione**     |  `Azure Information Protection unified labeling client`       |
    |**Scadenza**     |   Specificare la durata scelta (1 anno, 2 anni o nessuna scadenza)     |
    |     |         |

1. Tornare al riquadro **AIP-DelegatedUser-certificates & Secrets** , nella sezione **client Secrets** , copiare la stringa per il **valore**. 

    Questa stringa ha un aspetto simile all'esempio seguente: `OAkk+rnuYc/u+]ah2kNxVbtrDGbS47L4` . 

    Per assicurarsi di copiare tutti i caratteri, selezionare l'icona da **copiare negli Appunti**. 
    
    > [!IMPORTANT]
    > È importante salvare la stringa, perché non verrà più visualizzata e non potrà essere recuperata. Come per le informazioni riservate utilizzate, archiviare il valore salvato in modo sicuro e limitarne l'accesso.
    > 

1. Dalla barra laterale selezionare **Gestisci**  >  **autorizzazioni API**.

    Nel riquadro **autorizzazioni AIP-DelegatedUser-API** selezionare **Aggiungi un'autorizzazione**.

1. Nel riquadro **autorizzazioni API richiesta** , assicurarsi di essere nella scheda **Microsoft Apis** e selezionare **Azure Rights Management Services**. 

    Quando viene richiesto il tipo di autorizzazioni richieste dall'applicazione, selezionare **Autorizzazioni applicazione**.

1. Per **selezionare le autorizzazioni**, espandere **contenuto** e selezionare le opzioni seguenti e quindi selezionare **Aggiungi autorizzazioni**.
    
    -  **Content. DelegatedReader** 
    -  **Content. DelegatedWriter**

1. Tornare al riquadro **autorizzazioni AIP-DelegatedUser-API** e selezionare di nuovo **Aggiungi un'autorizzazione** .

    Nel riquadro **richieste AIP autorizzazioni** selezionare **API utilizzate dall'organizzazione** e cercare **Microsoft Information Protection Sync Service**.

1. Nel riquadro **autorizzazioni API richiesta** selezionare **Autorizzazioni applicazione**.
    
    Per le **autorizzazioni SELECT**, espandere **UnifiedPolicy**, selezionare **UnifiedPolicy. tenant. Read**, quindi selezionare **Aggiungi autorizzazioni**.

1. Tornare al riquadro **autorizzazioni AIP-DelegatedUser-API** , selezionare **concedi il consenso dell'amministratore \<*your tenant name*> per** e selezionare **Sì** per la richiesta di conferma.
    
    Le autorizzazioni dell'API dovrebbero avere un aspetto simile all'immagine seguente:

    :::image type="content" source="../media/api-permissions-app.png" alt-text="Autorizzazioni API per l'app registrata in Azure AD":::

A questo punto è stata completata la registrazione di questa app con un segreto, si è pronti per eseguire [set-AIPAuthentication](/powershell/module/azureinformationprotection/set-aipauthentication) con i parametri *AppID* e *AppSecret*. Inoltre, sarà necessario l'ID tenant. 

> [!TIP]
>È possibile copiare rapidamente l'ID tenant usando portale di Azure: **Azure Active Directory**  >  **Gestisci**  >    >  **ID directory** proprietà.

### <a name="running-the-set-aipauthentication-cmdlet"></a>Esecuzione del cmdlet Set-AIPAuthentication

1. Aprire Windows PowerShell con l' **opzione Esegui come amministratore**. 

1. Nella sessione di PowerShell creare una variabile per archiviare le credenziali dell'account utente di Windows che eseguirà in modo non interattivo. Ad esempio, se è stato creato un account del servizio per lo scanner:

    ```PowerShell
    $pscreds = Get-Credential "CONTOSO\srv-scanner"
    ```

    Viene richiesta la password di questo account.

1. Eseguire il cmdlet **set-AIPAuthentication** con il parametro *OnBeHalfOf* , specificando come valore la variabile creata. 

    Specificare anche i valori di registrazione dell'app, l'ID tenant e il nome dell'account utente delegato in Azure AD. Ad esempio:
    
    ```PowerShell
    Set-AIPAuthentication -AppId "77c3c1c3-abf9-404e-8b2b-4652836c8c66" -AppSecret "OAkk+rnuYc/u+]ah2kNxVbtrDGbS47L4" -TenantId "9c11c87a-ac8b-46a3-8d5c-f4d0b72ee29a" -DelegatedUser scanner@contoso.com -OnBehalfOf $pscreds
    ```
## <a name="next-steps"></a>Passaggi successivi

Per la guida del cmdlet quando ci si trova in una sessione di PowerShell, digitare `Get-Help <cmdlet name> -online` . Ad esempio: 

```PowerShell
Get-Help Set-AIPFileLabel -online
```

Per altre informazioni, vedere:

- [Personalizzazione del client con etichetta unificata](clientv2-admin-guide-customizations.md)

- [File del client e registrazione dell'utilizzo](clientv2-admin-guide-files-and-logging.md)

- [Tipi di file supportati](clientv2-admin-guide-file-types.md)