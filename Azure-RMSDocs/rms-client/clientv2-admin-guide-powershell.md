---
title: Usare PowerShell con il client di etichettatura unificato Azure Information Protection
description: Istruzioni e informazioni per gli amministratori per la gestione del client Azure Information Protection Unified Labeling usando PowerShell.
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 06/16/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: v2client
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: a7705a284690094c3db2ac5fd3ac3e3eca1ed2e5
ms.sourcegitcommit: c133ada59dffcb9d8ee35688290d2b027bd63425
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/03/2020
ms.locfileid: "89423129"
---
# <a name="admin-guide-using-powershell-with-the-azure-information-protection-unified-client"></a>Guida dell'amministratore: uso di PowerShell con il client unificato di Azure Information Protection

>*Si applica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8, windows server 2019, windows server 2016, windows Server 2012 R2, windows Server 2012*
>
>*Se si dispone di Windows 7 o Office 2010, vedere [AIP per le versioni di Windows e Office nel supporto esteso](../known-issues.md#aip-for-windows-and-office-versions-in-extended-support).*
>
> *Istruzioni per: [Azure Information Protection client di etichetta unificata per Windows](../faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

Quando si installa il client Azure Information Protection Unified Labeling, i comandi di PowerShell vengono installati automaticamente. Ciò consente di gestire il client eseguendo i comandi che è possibile inserire negli script per l'automazione.

I cmdlet vengono installati con il modulo di PowerShell **AzureInformationProtection**, che include i cmdlet per l'assegnazione di etichette. Ad esempio:

|Cmdlet per le etichette|Esempio di utilizzo|
|----------------|---------------|
|[Get-AIPFileStatus](/powershell/module/azureinformationprotection/get-aipfilestatus)|Per una cartella condivisa, identifica tutti i file con un'etichetta specifica.|
|[Set-AIPFileClassification](/powershell/module/azureinformationprotection/set-aipfileclassification)|Per una cartella condivisa, esaminare il contenuto dei file e quindi etichettare automaticamente i file senza etichetta, in base alle condizioni specificate.|
|[Set-AIPFileLabel](/powershell/module/azureinformationprotection/set-aipfilelabel)|Per una cartella condivisa, applica un'etichetta specificata a tutti i file privi di etichetta.|
|[Set-AIPAuthentication](/powershell/module/azureinformationprotection/set-aipauthentication)|Assegna etichette ai file in modo non interattivo, ad esempio tramite uno script che viene eseguito in base a una pianificazione.|

> [!TIP]
> Per usare cmdlet con percorsi di lunghezza superiore a 260 caratteri, usare l'[impostazione di Criteri di gruppo](https://blogs.msdn.microsoft.com/jeremykuhne/2016/07/30/net-4-6-2-and-long-paths-on-windows-10/) seguente disponibile a partire da Windows 10 versione 1607:<br /> Criteri del computer **locale**  >  **Configurazione computer**  >  **Modelli amministrativi**  >  **Tutte le impostazioni**  >  **Abilita percorsi lunghi Win32** 
> 
> Per Windows Server 2016 è possibile usare la stessa impostazione di Criteri di gruppo quando si installano i modelli amministrativi più recenti (con estensione admx) per Windows 10.
>
> Per altre informazioni, vedere la sezione [Maximum Path Length Limitation](https://docs.microsoft.com/windows/desktop/FileIO/naming-a-file#maximum-path-length-limitation) (Limite massimo lunghezza del percorso) della documentazione per sviluppatori di Windows 10.

Questo modulo viene installato in **\Programmi (x86)\Microsoft Azure Information Protection** e aggiunge questa cartella alla variabile di sistema **PSModulePath**. Il file DLL per questo modulo si chiama **AIP.dll**.

> [!IMPORTANT]
> Il modulo AzureInformationProtection non supporta la configurazione delle impostazioni avanzate per le etichette o i criteri di etichetta. Per queste impostazioni, è necessario Office 365 Security & Compliance Center PowerShell. Per ulteriori informazioni, vedere [Custom Configurations for the Azure Information Protection Unified Labeling client](clientv2-admin-guide-customizations.md).

### <a name="prerequisites-for-using-the-azureinformationprotection-module"></a>Prerequisiti per l'uso del modulo AzureInformationProtection

Oltre ai prerequisiti per l'installazione del modulo AzureInformationProtection, esistono prerequisiti aggiuntivi per l'uso dei cmdlet di assegnazione di etichette per Azure Information Protection:

1. Il servizio Azure Rights Management deve essere attivato.

2. Per rimuovere la protezione dai file per altri utenti tramite il proprio account: 

    - La funzionalità relativa agli utenti con privilegi avanzati deve essere abilitata per l'organizzazione e l'account deve essere configurato come account con privilegi avanzati per Azure Rights Management.

#### <a name="prerequisite-1-the-azure-rights-management-service-must-be-activated"></a>Prerequisito 1: il servizio Azure Rights Management deve essere attivato

Se il tenant di Azure Information Protection non è attivato, vedere le istruzioni per [[attivazione del servizio di protezione da Azure Information Protection](../activate-service.md).

#### <a name="prerequisite-2-to-remove-protection-from-files-for-others-using-your-own-account"></a>Prerequisito 2: per rimuovere la protezione dai file per altri utenti tramite il proprio account

Gli scenari tipici per la rimozione della protezione dai file per altri utenti includono l'individuazione dei dati o il ripristino dei dati. Se si usano etichette per applicare la protezione, è possibile rimuovere la protezione impostando una nuova etichetta che non applica protezione oppure rimuovendo l'etichetta.

Per poter rimuovere la protezione dai file, è necessario avere diritti di utilizzo per Rights Management oppure un account utente con privilegi avanzati. Per l'individuazione dei dati o il ripristino dei dati, viene in genere usata la funzionalità per utenti con privilegi avanzati. Per abilitare questa funzionalità e configurare l'account come utente con privilegi avanzati, vedere [configurazione degli utenti con privilegi avanzati per Azure Information Protection e servizi di individuazione o ripristino dei dati](../configure-super-users.md).

## <a name="how-to-label-files-non-interactively-for-azure-information-protection"></a>Come assegnare un'etichetta ai file in modo non interattivo per Azure Information Protection

È possibile eseguire i cmdlet per l'assegnazione delle etichette in modo non interattivo tramite il cmdlet [Set-AIPAuthentication](/powershell/module/azureinformationprotection/set-aipauthentication).

Per impostazione predefinita, quando si eseguono i cmdlet per l'assegnazione di etichette, i comandi vengono eseguiti nel contesto utente personale in una sessione interattiva di PowerShell. Per eseguirli in modo automatico, utilizzare un account di Windows in grado di accedere in modo interattivo e utilizzare un account in Azure AD che verrà utilizzato per l'accesso delegato. Per semplificare l'amministrazione, usare un singolo account sincronizzato da Active Directory a Azure AD.

È anche necessario richiedere un token di accesso da Azure AD, che imposta e archivia le credenziali per l'utente delegato per l'autenticazione a Azure Information Protection.

Il computer che esegue il cmdlet AIPAuthentication Scarica i criteri di etichetta con le etichette assegnate all'account utente delegato tramite il centro di gestione delle etichette, ad esempio Office 365 Security & Compliance Center.

> [!NOTE]
> Se si usano criteri di etichetta per utenti diversi, potrebbe essere necessario creare nuovi criteri di etichetta che pubblichino tutte le etichette e pubblicare i criteri solo in questo account utente delegato.

Quando il token in Azure AD scade, è necessario eseguire nuovamente il cmdlet per acquisire un nuovo token. È possibile configurare il token di accesso in Azure AD per un anno, due anni o per non scadere mai. I parametri per set-AIPAuthentication usano i valori di un processo di registrazione delle app in Azure AD, come descritto nella sezione successiva.

Per l'account utente delegato:

- Assicurarsi di disporre di un criterio di etichetta assegnato a questo account e che il criterio includa le etichette pubblicate che si desidera utilizzare.

- Se questo account deve decrittografare il contenuto, ad esempio per riproteggere i file e controllare i file protetti da altri utenti, renderlo un [utente con privilegi](../configure-super-users.md) avanzati per Azure Information Protection e assicurarsi che la funzionalità per utenti con privilegi avanzati sia abilitata.

- Se sono stati implementati i [controlli di onboarding](../activate-service.md#configuring-onboarding-controls-for-a-phased-deployment) per una distribuzione in più fasi, assicurarsi che questo account sia incluso nei controlli di onboarding configurati.

### <a name="to-create-and-configure-the-azure-ad-applications-for-set-aipauthentication"></a>Per creare e configurare le applicazioni di Azure AD per Set-AIPAuthentication

> [!IMPORTANT]
> Queste istruzioni riguardano la versione di disponibilità generale corrente del client Unified Labeling e si applicano anche alla versione di disponibilità generale dello scanner per questo client.

Set-AIPAuthentication richiede una registrazione dell'app per i parametri *AppID* e *AppSecret* . Se è stato eseguito l'aggiornamento da una versione precedente del client e è stata creata una registrazione dell'app per i parametri *webappid* e *NativeAppId* precedenti, questi non funzioneranno con il client di etichettatura unificata. È necessario creare una nuova registrazione per l'app come segue:

1. In una nuova finestra del browser accedere al [Portale di Azure](https://portal.azure.com/).

2. Per il tenant Azure ad usato con Azure Information Protection, passare a **Azure Active Directory**  >  **Gestisci**  >  **registrazioni app**. 

3. Selezionare **+ nuova registrazione**. Nel riquadro **registra un'applicazione** specificare i valori seguenti e quindi fare clic su **registra**:

   - **Nome**: `AIP-DelegatedUser`
        
        Se preferibile, specificare un nome diverso. Deve essere univoco per ogni tenant.
    
    - **Tipi di account supportati**: **solo account in questa directory organizzativa**
    
    - **URI di reindirizzamento (facoltativo)**: **Web** e `https://localhost`

4. Nel riquadro **AIP-DelegatedUser** , copiare il valore per l' **ID applicazione (client)**. Il valore è simile all'esempio seguente: `77c3c1c3-abf9-404e-8b2b-4652836c8c66` . Questo valore viene usato per il parametro *AppID* quando si esegue il cmdlet Set-AIPAuthentication. Incollare e salvare il valore per riferimento successivo.

5. Dalla barra laterale selezionare **Gestisci**  >  **certificati & segreti**.

6. Nella sezione **segreti client** del riquadro **AIP-DelegatedUser-Certificates & Secrets** selezionare **+ nuovo segreto client**.

7. Per **Aggiungi un segreto client**, specificare quanto segue e quindi selezionare **Aggiungi**:
    
    - **Descrizione**: `Azure Information Protection unified labeling client`
    - **Scadenza**: specificare la scelta della durata (1 anno, 2 anni o nessuna scadenza)

8. Tornare al riquadro **AIP-DelegatedUser-certificates & Secrets** , nella sezione **client Secrets** , copiare la stringa per il **valore**. Questa stringa ha un aspetto simile all'esempio seguente: `OAkk+rnuYc/u+]ah2kNxVbtrDGbS47L4` . Per assicurarsi di copiare tutti i caratteri, selezionare l'icona da **copiare negli Appunti**. 
    
    È importante salvare la stringa, perché non verrà più visualizzata e non potrà essere recuperata. Come per le informazioni riservate utilizzate, archiviare il valore salvato in modo sicuro e limitarne l'accesso.

9. Dalla barra laterale selezionare **Gestisci**  >  **autorizzazioni API**.

10. Nel riquadro **autorizzazioni AIP-DelegatedUser-API** selezionare **+ Aggiungi un'autorizzazione**.

11. Nel riquadro **autorizzazioni API richiesta** , assicurarsi di essere nella scheda **Microsoft Apis** e selezionare **Azure Rights Management Services**. Quando viene richiesto il tipo di autorizzazioni richieste dall'applicazione, selezionare **Autorizzazioni applicazione**.

12. Per **autorizzazioni SELECT**, espandere **contenuto** e selezionare gli elementi seguenti:
    
    -  **Content. DelegatedReader** 
    -  **Content. DelegatedWriter**

13. Selezionare **Aggiungi autorizzazioni**.

14. Tornare al riquadro **autorizzazioni AIP-DelegatedUser-API** , selezionare **+ Aggiungi nuovamente un'autorizzazione** .

15. Nel riquadro **richieste AIP autorizzazioni** selezionare **API utilizzate dall'organizzazione**e cercare **Microsoft Information Protection Sync Service**.

16. Nel riquadro **autorizzazioni API richiesta** selezionare **Autorizzazioni applicazione**.

17. Per **autorizzazioni SELECT**, espandere **UnifiedPolicy** e selezionare le opzioni seguenti:
    
    -  **UnifiedPolicy. tenant. Read**

18. Selezionare **Aggiungi autorizzazioni**.

19. Tornare al riquadro **autorizzazioni AIP-DelegatedUser-API** , selezionare **concedi il consenso dell'amministratore \<*your tenant name*> per** e selezionare **Sì** per la richiesta di conferma.
    
    Le autorizzazioni dell'API dovrebbero essere simili alle seguenti:
    
    ![Autorizzazioni API per l'app registrata in Azure AD](../media/api-permissions-app.png)

A questo punto è stata completata la registrazione di questa app con un segreto, si è pronti per eseguire [set-AIPAuthentication](/powershell/module/azureinformationprotection/set-aipauthentication) con i parametri *AppID*e *AppSecret*. Inoltre, sarà necessario l'ID tenant. 

> [!TIP]
>È possibile copiare rapidamente l'ID tenant usando portale di Azure: **Azure Active Directory**  >  **Gestisci**  >  **Properties**  >  **ID directory**proprietà.

1. Aprire Windows PowerShell con l' **opzione Esegui come amministratore**. 

2. Nella sessione di PowerShell creare una variabile per archiviare le credenziali dell'account utente di Windows che eseguirà in modo non interattivo. Ad esempio, se è stato creato un account del servizio per lo scanner:

    ```ps
    $pscreds = Get-Credential "CONTOSO\srv-scanner"
    ```

    Viene richiesta la password di questo account.

2. Eseguire il cmdlet Set-AIPAuthentication con il parametro *OnBeHalfOf* , specificando come valore la variabile appena creata. Specificare anche i valori di registrazione dell'app, l'ID tenant e il nome dell'account utente delegato in Azure AD. Ad esempio:
    
    ```ps
    Set-AIPAuthentication -AppId "77c3c1c3-abf9-404e-8b2b-4652836c8c66" -AppSecret "OAkk+rnuYc/u+]ah2kNxVbtrDGbS47L4" -TenantId "9c11c87a-ac8b-46a3-8d5c-f4d0b72ee29a" -DelegatedUser scanner@contoso.com -OnBehalfOf $pscreds
    ```

> [!NOTE]
> Se il computer non può accedere a Internet, non è necessario creare l'app in Azure AD ed eseguire set-AIPAuthentication. Seguire invece le istruzioni per i [computer disconnessi](clientv2-admin-guide-customizations.md#support-for-disconnected-computers).  

## <a name="next-steps"></a>Passaggi successivi
Per la guida del cmdlet quando ci si trova in una sessione di PowerShell, digitare `Get-Help <cmdlet name> -online` . Ad esempio: 

```ps
Get-Help Set-AIPFileLabel -online
```

Per altre informazioni necessarie per supportare il client Azure Information Protection, vedere gli argomenti seguenti:

- [Personalizzazioni](clientv2-admin-guide-customizations.md)

- [File del client e registrazione dell'utilizzo](clientv2-admin-guide-files-and-logging.md)

- [Tipi di file supportati](clientv2-admin-guide-file-types.md)
