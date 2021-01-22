---
title: Il client per Azure Information Protection-AIP
description: Microsoft Azure Information Protection offre una soluzione client-server che consente di proteggere i dati di un'organizzazione. Il client (di Azure Information Protection o di Rights Management) si integra con le applicazioni che vengono eseguite su computer e dispositivi mobili.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 01/20/2021
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.suite: ems
ms.custom: admin
search.appverid:
- MET150
ms.openlocfilehash: fcd21a58dabe65f1de88694f97dc57975bc19450
ms.sourcegitcommit: ee20112ada09165b185d9c0c9e7f1179fc39e7cf
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/21/2021
ms.locfileid: "98659069"
---
# <a name="the-client-side-of-azure-information-protection"></a>Lato client di Azure Information Protection

>***Si applica a**: Active Directory Rights Management Services, [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection),[Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8, windows server 2019, windows server 2016, Windows server 2012 R2, Windows Server 2012 *
>
>*Se si dispone di Windows 7 o Office 2010, vedere [AIP e versioni legacy di Windows e Office](../known-issues.md#aip-and-legacy-windows-and-office-versions).*
>
>***Rilevante per**: [Client di etichettatura unificata e client classico di AIP](../faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

>[!NOTE] 
> Per offrire un'esperienza per i clienti unificata e semplificata, il **client classico di Azure Information Protection** e **Gestione etichette** nel portale di Azure saranno **deprecati** a partire dal **31 marzo 2021**. In questo intervallo di tempo tutti i clienti correnti di Azure Information Protection possono passare alla soluzione di etichettatura unificata usando la piattaforma di etichettatura unificata di Microsoft Information Protection. Altre informazioni nell'[avviso ufficiale sulla deprecazione](https://aka.ms/aipclassicsunset).


Il Azure Information Protection client Unified Labeling fornisce una soluzione client-server che consente di proteggere i documenti e i messaggi di posta elettronica di un'organizzazione ed è un'alternativa alla [soluzione incorporata di assegnazione di etichette per Microsoft Office](/microsoft-365/compliance/sensitivity-labels). 

Oltre all'integrazione diretta con le applicazioni di Office, il client Unified Labeling include il supporto per Esplora file e PowerShell, in modo che sia possibile classificare e proteggere i file all'esterno di Office. I componenti aggiuntivi includono un visualizzatore per le immagini e i file PDF protetti e uno scanner per gli archivi dati locali.

Il client di etichettatura unificata deve essere installato separatamente nelle app di Office.

Il servizio risiede nel cloud o in locale:

- Il servizio cloud è **Azure Information Protection** e usa il servizio Azure Rights Management per la protezione dei dati
- Il servizio locale è **Active Directory Rights Management Services** (ad RMS)

## <a name="choose-your-windows-labeling-solution"></a>Scegliere la soluzione di etichettatura di Windows

Le etichette rendono più semplice per gli utenti l'applicazione della protezione e forniscono anche la classificazione per poter tenere traccia e gestire i dati. 

Quando si sceglie una soluzione di etichettatura di Windows, considerare le seguenti differenze di base:

- **Dove vengono scaricati le etichette e i criteri delle etichette** 

    La soluzione incorporata di assegnazione di etichette e il client AIP Unified Labeling usano uno dei seguenti centri di amministrazione: 
    
    - Centro sicurezza e conformità di Office 365 
    - Centro sicurezza Microsoft 365 
    - Centro conformità Microsoft 365
      
    Se si usa il client precedente AIP classico, i criteri etichette e etichetta vengono scaricati e gestiti nella portale di Azure. 

- **Requisiti di installazione**

    La soluzione incorporata per l'assegnazione di etichette non richiede un'installazione separata.

    Il client di assegnazione unificata di AIP e il client classico legacy richiedono entrambi un'installazione separata in Office. Scaricare e installare il client Unified Labeling dall' [area download Microsoft](https://www.microsoft.com/download/details.aspx?id=53018).  

    Se è necessario scaricare e installare il client classico legacy, contattare il supporto tecnico e aprire un ticket per accedere al file di installazione. 

Usare le sezioni seguenti per determinare il client migliore per l'organizzazione:

- [Soluzione predefinita di assegnazione di etichette per Office](#built-in-office-labeling-solution)
- [Client per l'etichettatura unificata di Azure Information Protection](#azure-information-protection-unified-labeling-client)
- [Client classico di Azure Information Protection](#azure-information-protection-classic-client)
- [Uso di più client nello stesso ambiente](#using-multiple-clients-in-the-same-environment)

Per ulteriori informazioni, vedere la pagina relativa ai [confronti dettagliati per i client e le funzionalità AIP](#detailed-comparisons-for-the-azure-information-protection-clients) [non pianificati per il client di etichettatura unificata](#features-not-planned-to-be-in-the-azure-information-protection-unified-labeling-client).

> [!NOTE]
> La versione più recente del client Unified Labeling consente di chiudere la parità nelle funzionalità con il client classico. Quando questo gap si chiude, è possibile aspettarsi che vengano aggiunte nuove funzionalità solo al client di etichettatura unificata. 
>
> Si consiglia di distribuire il client di etichettatura unificata se il set di funzionalità e le funzionalità correnti soddisfano i requisiti aziendali.
> 

### <a name="built-in-office-labeling-solution"></a>Soluzione predefinita di assegnazione di etichette per Office

La soluzione di assegnazione di etichette integrata per la Microsoft Office:

- Richiede un computer Windows con Microsoft 365 applicazioni, versione minima 1910
- Consente di condividere le etichette e le impostazioni dei criteri che possono essere usate anche da macOS, iOS e Android
- Supporta il cambio di account
- Offre prestazioni migliori nelle applicazioni di Office
- Non richiede un'installazione e una manutenzione separate
- Non disabilitabile.

Se sono necessarie funzionalità disponibili solo per i client di Azure Information Protection, ad esempio la barra Information Protection sotto la barra multifunzione, **non usare** il client di assegnazione di etichette di Office predefinito. Questa barra rende più semplice la selezione e la visibilità delle etichette.

### <a name="azure-information-protection-unified-labeling-client"></a>Client per l'etichettatura unificata di Azure Information Protection

Il client di etichettatura unificata richiede un computer Windows e consente di condividere le etichette e le impostazioni dei criteri che possono essere usate anche da macOS, iOS e Android.

**Non usare** il client di etichettatura unificata se sono state configurate etichette nel portale di Azure di cui non è ancora stata [eseguita la migrazione nell'archivio di etichette unificato](../configure-policy-migrate-labels.md).

### <a name="azure-information-protection-classic-client"></a>Client classico di Azure Information Protection

Il client classico è il client legacy di AIP, supporta funzionalità simili a quelle del client di etichettatura unificata e deve anche essere installato separatamente nelle app di Office. 

Il client classico verrà [deprecato nel 2021 marzo](https://aka.ms/aipclassicsunset).

Usare il client classico solo se non è ancora stata eseguita la migrazione a un'etichetta unificata. Per altre informazioni, vedere [Esercitazione: Migrazione dal client classico al client di etichettatura unificata di Azure Information Protection (AIP)](../tutorial-migrating-to-ul.md).

Il client classico ha impostazioni di criteri diverse per macOS, iOS e Android. Pertanto, anche se si desidera utilizzare le funzionalità aggiuntive, è necessario collaborare con un portale di gestione separato e un'esperienza utente per proteggere il contenuto tra i sistemi operativi.

Laddove possibile, è consigliabile usare il client Unified Labeling anziché il client classico.

### <a name="using-multiple-clients-in-the-same-environment"></a>Uso di più client nello stesso ambiente

È possibile utilizzare client diversi nello stesso ambiente per supportare requisiti aziendali diversi, come illustrato nel seguente esempio di distribuzione. In un ambiente client misto è consigliabile usare le etichette unificate in modo che i client condividano lo stesso set di etichette per semplificare l'amministrazione. Per impostazione predefinita, i nuovi clienti hanno etichette unificate, perché i tenant si trovano nella piattaforma di etichettatura unificata. Per ulteriori informazioni, vedere [come è possibile determinare se il tenant si trova nella piattaforma di etichettatura unificata?](../faqs.md#how-can-i-determine-if-my-tenant-is-on-the-unified-labeling-platform)

Quando si dispone di un computer Windows che esegue Microsoft 365 app con una versione minima 1910 e uno dei client di Azure Information Protection è installato, per impostazione predefinita la soluzione incorporata di assegnazione di etichette è disabilitata nelle app di Office. Tuttavia, è possibile modificare questo comportamento per usare la soluzione di assegnazione di etichette incorporata solo per le app di Office. Con questa configurazione, il client Azure Information Protection rimane disponibile per l'assegnazione di etichette in Esplora file, PowerShell e lo scanner. Per istruzioni su come disabilitare il client Azure Information Protection nelle app Microsoft 365, vedere la sezione relativa alla [soluzione di assegnazione di etichette incorporata di Office e il client di Azure Information Protection](/microsoft-365/compliance/sensitivity-labels-office-apps#office-built-in-labeling-client-and-the-azure-information-protection-client) dalla documentazione sulla conformità Microsoft 365.

##### <a name="sample-deployment-strategy"></a>Strategia di distribuzione di esempio

- Per la maggior parte degli utenti, si distribuisce il Azure Information Protection client Unified Labeling perché questo client soddisfa le esigenze aziendali per questi utenti. 
    
    Per questi utenti, la loro esperienza di etichettatura è simile in Windows, Mac, iOS e Android, perché hanno le stesse etichette pubblicate e le stesse impostazioni dei criteri. In qualità di amministratore, le etichette e le impostazioni dei criteri vengono gestite nello stesso centro di gestione.

- È anche possibile installare il client di assegnazione di etichette unificato per testare lo scanner Azure Information Protection.

- Per un subset di utenti, si distribuisce il client classico perché questi utenti richiedono etichette che applicano la protezione[HYOK](../configure-adrms-restrictions.md)(Holding your own key).
    
    Per questi utenti hanno un'esperienza di etichettatura leggermente diversa quando usano questo client. Ad esempio, viene visualizzato un pulsante **Proteggi** anziché un pulsante di **riservatezza** nelle app di Office. In qualità di amministratore, è necessario gestire le etichette per le impostazioni di HYOK e le impostazioni dei criteri in un centro di gestione diverso per le etichette e le impostazioni per le altre piattaforme client.

- Sono presenti archivi dati locali con documenti che devono essere analizzati per ottenere informazioni riservate oppure classificati e protetti. Per l'uso in produzione, si distribuisce il client di etichettatura unificata nei server per eseguire lo [scanner Azure Information Protection](../deploy-aip-scanner.md).

#### <a name="rights-management-client"></a>Client Rights Management

Il client RMS fornisce solo la protezione e viene installato automaticamente con alcune applicazioni, incluse le applicazioni di Office, l'etichetta unificata AIP e i client classici e le applicazioni abilitate per RMS da altri fornitori di software. 

È anche possibile [installare il client RMS manualmente](https://www.microsoft.com/download/details.aspx?id=38396), per supportare la [sincronizzazione dei file dalle librerie protette con IRM e OneDrive](/onedrive/deploy-on-windows)e per gli sviluppatori che desiderano integrare la protezione di Rights Management in applicazioni line-of-business.

## <a name="compare-the-labeling-solutions-for-windows-computers"></a>Confrontare le soluzioni di etichettatura per i computer Windows

Usare la tabella seguente per confrontare le funzionalità supportate dalle tre soluzioni di assegnazione di etichette per i computer Windows.

Per confrontare le funzionalità di riservatezza predefinite di Office in diverse piattaforme del sistema operativo (Windows, macOS, iOS e Android) e per il Web, vedere la documentazione relativa alla conformità del Microsoft 365, [supporto per le funzionalità di etichetta di riservatezza nelle app](/microsoft-365/compliance/sensitivity-labels-office-apps#support-for-sensitivity-label-capabilities-in-apps). Questa documentazione include anche i numeri di build di Office o le informazioni sul canale di aggiornamento di Office per le funzionalità supportate.

Per altri dettagli, vedere anche:
- [Confronti dettagliati per i client di Azure Information Protection](#detailed-comparisons-for-the-azure-information-protection-clients)
- [Funzionalità non previste nel client di Azure Information Protection Unified Labeling](#features-not-planned-to-be-in-the-azure-information-protection-unified-labeling-client)

|Funzionalità|Client classico|Client di etichetta unificato|Soluzione di assegnazione di etichette incorporata di Office|
|:------|:------------:|:---------------------:|:-----------------------------:|
|**Etichettatura manuale**| ![sì](../media/yes-icon.png)   | ![sì](../media/yes-icon.png)   |![sì](../media/yes-icon.png) |
|**Etichetta predefinita**| ![sì](../media/yes-icon.png)| ![sì](../media/yes-icon.png)| ![sì](../media/yes-icon.png)|
|**Etichettatura consigliata o automatica** <br />Per Word, Excel, PowerPoint, Outlook|![sì](../media/yes-icon.png) | ![sì](../media/yes-icon.png) | ![sì](../media/yes-icon.png) |
|**Etichettatura obbligatoria**| ![sì](../media/yes-icon.png) | ![sì](../media/yes-icon.png) |  ![no](../media/no-icon.png)|
|**Autorizzazioni definite dall'utente per un'etichetta**: <br />Non inviare i messaggi di posta elettronica| ![sì](../media/yes-icon.png) | ![sì](../media/yes-icon.png) | ![sì](../media/yes-icon.png) |
|**Autorizzazioni definite dall'utente per un'etichetta**: <br />Autorizzazioni personalizzate per Word, Excel, PowerPoint| ![sì](../media/yes-icon.png) | ![sì](../media/yes-icon.png) | ![sì](../media/yes-icon.png) |
|**Supporto multilingue per le etichette**| ![sì](../media/yes-icon.png) | ![sì](../media/yes-icon.png) |![sì](../media/yes-icon.png) |
|**Ereditarietà delle etichette dagli allegati di posta elettronica**| ![sì](../media/yes-icon.png) | ![sì](../media/yes-icon.png)  | ![no](../media/no-icon.png)|
|**Personalizzazioni che includono**:<br />- Etichetta predefinita per la posta elettronica<br />-Popup dei messaggi in Outlook <br />- Supporto S/MIME<br />- Opzione Segnala un problema| ![Sì ](../media/yes-icon.png) <sup>1</sup> | ![Sì ](../media/yes-icon.png) <sup>2</sup> |  ![no](../media/no-icon.png)|
|**Scanner per gli archivi dati locali**| ![sì](../media/yes-icon.png) |  ![sì](../media/yes-icon.png) |  ![no](../media/no-icon.png)|
|**Reporting centrale (analisi)**| ![sì](../media/yes-icon.png) | ![sì](../media/yes-icon.png) |  ![no](../media/no-icon.png)|
|**Autorizzazioni personalizzate impostate in modo indipendente da un'etichetta**| ![sì](../media/yes-icon.png) | ![Sì ](../media/yes-icon.png) <sup>3</sup>|  ![no](../media/no-icon.png)|
|**Barra di Information Protection nelle app Office**| ![sì](../media/yes-icon.png) | ![sì](../media/yes-icon.png)|  ![no](../media/no-icon.png)|
|**Contrassegni visivi come azione etichetta**<br> (intestazione, piè di pagina, filigrana)| ![sì](../media/yes-icon.png) | ![sì](../media/yes-icon.png) | ![sì](../media/yes-icon.png)|
|**Contrassegni visivi per app**| ![sì](../media/yes-icon.png) | ![sì](../media/yes-icon.png) | ![Sì ](../media/yes-icon.png) <sup>9</sup>|
|**Contrassegni visivi dinamici con variabili**| ![sì](../media/yes-icon.png) | ![sì](../media/yes-icon.png) | ![Sì ](../media/yes-icon.png) <sup>9</sup>|
|**Rimuovi contrassegno contenuto esterno nell'app**| ![sì](../media/yes-icon.png)| ![sì](../media/yes-icon.png)| ![no](../media/no-icon.png)|
|**Etichetta con Esplora file**| ![sì](../media/yes-icon.png) | ![sì](../media/yes-icon.png) |  ![no](../media/no-icon.png)|
|**Un visualizzatore per i file protetti** <br> (testo, immagini, PDF, Pfile)| ![sì](../media/yes-icon.png) | ![sì](../media/yes-icon.png) | ![no](../media/no-icon.png)|
|**Supporto di PPDF per l'applicazione di etichette**| ![sì](../media/yes-icon.png) |  ![no](../media/no-icon.png)|  ![no](../media/no-icon.png)|
|**Cmdlet per l'assegnazione di etichette di PowerShell**| ![sì](../media/yes-icon.png) | ![sì](../media/yes-icon.png)  |  ![no](../media/no-icon.png)|
|**Supporto offline per le azioni di protezione**| ![sì](../media/yes-icon.png) | ![Sì ](../media/yes-icon.png) <sup>4</sup> | ![sì](../media/yes-icon.png) |
|**Gestione manuale dei file di criteri per i computer disconnessi**| ![sì](../media/yes-icon.png) |![sì](../media/yes-icon.png)|  ![no](../media/no-icon.png)|
|**Supporto di HYOK**| ![sì](../media/yes-icon.png) |  ![no](../media/no-icon.png)|  ![no](../media/no-icon.png)|
|**Registrazione dell'utilizzo in Visualizzatore eventi**| ![sì](../media/yes-icon.png) |  ![no](../media/no-icon.png)| ![no](../media/no-icon.png)|
|**Visualizzare il pulsante Non inoltrare in Outlook**| ![sì](../media/yes-icon.png) |  ![no](../media/no-icon.png)|  ![no](../media/no-icon.png)|
|**Tenere traccia dei documenti protetti**| ![Sì ](../media/yes-icon.png) <sup>5</sup> | ![Sì ](../media/yes-icon.png) <sup>5</sup> |  ![no](../media/no-icon.png)|
|**Revocare i documenti protetti**| ![Sì ](../media/yes-icon.png) <sup>5</sup> |  ![Sì ](../media/yes-icon.png) <sup>5</sup>|  ![no](../media/no-icon.png)|
|**Modalità di sola protezione** (nessuna etichetta)| ![sì](../media/yes-icon.png) |  ![no](../media/no-icon.png)|  ![no](../media/no-icon.png)|
|**Supporto per il cambio di account**|  ![no](../media/no-icon.png)|  ![no](../media/no-icon.png)| ![sì](../media/yes-icon.png) |
|**Supporto per Servizi Desktop remoto**| ![sì](../media/yes-icon.png) | ![sì](../media/yes-icon.png) | ![sì](../media/yes-icon.png) |
|**Supporto per AD RMS**| ![sì](../media/yes-icon.png) |  ![n. ](../media/no-icon.png) <sup>6</sup> |  ![no](../media/no-icon.png)|
|**Supporto per i formati di Microsoft Office 97-2003**| ![sì](../media/yes-icon.png) | ![sì](../media/yes-icon.png) |  ![Nessun ](../media/no-icon.png) <sup>8</sup>|
|**Crittografia a chiave doppia**|  ![no](../media/no-icon.png)| ![sì](../media/yes-icon.png) |  ![no](../media/no-icon.png)|
|**Cloud della community per enti pubblici** | ![sì](../media/yes-icon.png) | ![sì](../media/yes-icon.png) | ![sì](../media/yes-icon.png)|
| | | | |

**Note a piè** di pagina:

<sup>1</sup> queste impostazioni e molte altre sono supportate come [Impostazioni client avanzate che è possibile configurare nel portale di Azure](client-admin-guide-customizations.md#how-to-configure-advanced-classic-client-configuration-settings-in-the-portal).

<sup>2</sup> queste impostazioni e molte altre sono supportate come [Impostazioni avanzate configurate con PowerShell](clientv2-admin-guide-customizations.md#configuring-advanced-settings-for-the-client-via-powershell).

<sup>3</sup> supportato da Esplora file e PowerShell. Nelle app di Office, gli utenti possono selezionare **file info**  >  **Proteggi documento**  >  **limita accesso**.

<sup>4</sup> per i comandi di Esplora file e PowerShell, l'utente deve essere connesso a Internet per proteggere i file.

<sup>5</sup> per ulteriori informazioni, vedere la guida dell'utente per l' **assegnazione di etichette unificata client**: [Guida dell'amministratore (anteprima pubblica](track-and-revoke-admin.md))  |   [(anteprima pubblica)](revoke-access-user.md). Il rilevamento è supportato solo per gli amministratori globali. **Client classico**: [](client-admin-guide-document-tracking.md)manuale  |  [dell'utente](client-track-revoke.md)della Guida dell'amministratore. Gli amministratori possono inoltre utilizzare la funzionalità di [creazione rapporti centrale](../reports-aip.md) per identificare se i documenti protetti sono accessibili dai computer Windows e se l'accesso è stato concesso o negato.

<sup>6</sup> le azioni di assegnazione di etichette e protezione non sono supportate. Tuttavia, per una distribuzione AD RMS, il visualizzatore può aprire i documenti protetti quando si usa l' [estensione Active Directory Rights Management Services Mobile Device](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn673574\(v=ws.11\)).

<sup>8</sup> mentre i client AIP supportano entrambi i formati di file Microsoft Office 97-2003, ad esempio **. doc**, nonché i formati XML Office aperti, ad esempio **. docx**, l'etichetta predefinita supporta solo formati Open XML.

<sup>9</sup> per ulteriori informazioni sul supporto per i contrassegni di contenuto dinamici e per i contrassegni di contenuto per app per la soluzione incorporata di assegnazione di etichette, vedere la [documentazione Microsoft 365](/microsoft-365/compliance/sensitivity-labels-office-apps#dynamic-markings-with-variables).

### <a name="detailed-comparisons-for-the-azure-information-protection-clients"></a>Confronti dettagliati per i client di Azure Information Protection

Quando il client di Azure Information Protection classico e il client Azure Information Protection Unified Labeling supportano entrambe la stessa funzionalità, usare gli elenchi seguenti per identificare alcune differenze funzionali tra i due client:


|Funzionalità |Client classico|Client di etichetta unificato|
|--------------|-----------------------------------|-----------------------------------------------------------|
|**Configurazione**| Opzione per installare i criteri demo locali | Nessun criterio demo locale|
|**Selezione e visualizzazione delle etichette quando vengono applicate nelle app di Office**|Dal pulsante **Proteggi** nella barra multifunzione <br /><br /> Dalla barra di Information Protection (barra orizzontale sotto la barra multifunzione)|Dal pulsante **Riservatezza** sulla barra multifunzione<br /><br /> Dalla barra di Information Protection (barra orizzontale sotto la barra multifunzione)|
|**Gestire la barra di Information Protection nelle app di Office**|**Per gli utenti**:<br />Opzione per mostrare o nascondere la barra dal pulsante **Proteggi** sulla barra multifunzione<br /><br>Quando un utente seleziona per nascondere la barra, per impostazione predefinita la barra è nascosta nell'app, ma continua a essere visualizzata automaticamente nelle app appena aperte <br /><br /> **Per gli amministratori**: <br />Impostazioni dei criteri per mostrare o nascondere automaticamente la barra quando si apre un'app e controllare se la barra rimane automaticamente nascosta per le app appena aperte dopo che un utente seleziona per nascondere la barra|**Per gli utenti**: <br />Opzione che consente di visualizzare o nascondere la barra dal pulsante **sensibilità** sulla barra multifunzione. <br><br />Quando un utente seleziona per nascondere la barra, la barra è nascosta nell'app e anche nelle app appena aperte <br /><br />**Per gli amministratori**: <br />Impostazione di PowerShell per gestire la barra |
|**Colore etichetta**| Configurare nel portale di Azure | Conservati dopo la migrazione delle etichette e configurabili con [PowerShell](clientv2-admin-guide-customizations.md#specify-a-color-for-the-label)|
|**Le etichette supportano lingue diverse**| Configurare nel portale di Azure | Configurare tramite [Office 365 Security & Compliance PowerShell](/microsoft-365/compliance/create-sensitivity-labels#additional-label-settings-with-office-365-security--compliance-center-powershell)|
|**Aggiornamento dei criteri**| -Quando si apre un'app di Office <br /> -Quando si fa clic con il pulsante destro del mouse per classificare e proteggere un file o una cartella <br />-Quando si eseguono i cmdlet di PowerShell per l'assegnazione di etichette e la protezione<br />Ogni 24 ore <br />-Per lo scanner: ogni ora e quando il servizio viene avviato e il criterio è più vecchio di un'ora| -Quando si apre un'app di Office <br />-Quando si fa clic con il pulsante destro del mouse per classificare e proteggere un file o una cartella <br />-Quando si eseguono i cmdlet di PowerShell per l'assegnazione di etichette e la protezione<br />Ogni 4 ore <br />-Per lo scanner: ogni 4 ore|
|**Formati supportati per PDF**| **Protezione**: <br /> - Standard ISO per la crittografia dei file PDF (impostazione predefinita) <br /> - Estensione ppdf <br /><br> **Consumo**: <br /> - Standard ISO per la crittografia dei file PDF <br />- Estensione ppdf<br />- Protezione IRM SharePoint| **Protezione**: <br /> - Standard ISO per la crittografia dei file PDF <br /> <br /> **Consumo**: <br /> - Standard ISO per la crittografia dei file PDF <br />- Estensione ppdf<br />- Protezione IRM SharePoint|
|**File protetti in modo generico (con estensione Pfile) aperti con il Visualizzatore**| Il file viene aperto nell'app originale, dove può essere visualizzato, modificato e salvato senza protezione | Il file viene aperto nell'app originale, dove può essere visualizzato e modificato, ma non salvato|
|**Cmdlet supportati**| -Cmdlet per l'assegnazione di etichette <br> -Cmdlet per solo la protezione | **Cmdlet per l'assegnazione di etichette**:<br /> [Set-AIPFileClassification](/powershell/module/azureinformationprotection/get-aipfileclassification) e [set-AIPFileLabel](/powershell/module/azureinformationprotection/get-aipfilelabel) non supportano il parametro **owner** <br /> È inoltre presente un singolo commento "No label to apply" per tutti gli scenari in cui non viene applicata un'etichetta <br /><br /> [Set-AIPFileClassification](/powershell/module/azureinformationprotection/get-aipfileclassification) supporta il parametro **whatIf** , in modo che possa essere eseguito in modalità di individuazione <br /><br /> [Set-AIPFileLabel](/powershell/module/azureinformationprotection/get-aipfilelabel) non supporta il parametro *EnableTracking* <br /><br /> [Get-AIPFileStatus](/powershell/module/azureinformationprotection/get-aipfilestatus) non restituisce informazioni sulle etichette da altri tenant e non Visualizza il parametro **RMSIssuedTime**<br />Inoltre, il parametro **LabelingMethod** per [Get-AIPFileStatus](/powershell/module/azureinformationprotection/get-aipfilestatus) Visualizza **Privileged** o **standard**, anziché **Manual** o **Automatic**.|
|**Richieste di giustificazione (se configurate) per azione in Office** | -Frequency: per file <br /> -Riduzione del livello di sensibilità <br /> -Rimozione di un'etichetta<br /> -Rimozione della protezione | -Frequency: per sessione <br /> -Riduzione del livello di sensibilità<br />-Rimozione di un'etichetta|
|**Rimuovi azioni etichetta applicate** | Viene chiesta conferma all'utente <br /><br />L'etichetta predefinita o un'etichetta automatica (se configurata) non viene applicata automaticamente alla prossima apertura del file da parte dell'app di Office  | All'utente non viene richiesto di confermare<br /><br /> L'etichetta predefinita o un'etichetta automatica (se configurata) viene applicata automaticamente la volta successiva che l'app di Office apre il file|
|**Etichette automatiche e consigliate** | Configurata come [condizioni per le etichette](../configure-policy-classification.md) nel portale di Azure con i tipi di informazioni predefiniti e le condizioni personalizzate che usano frasi o espressioni regolari <br /><br />Le opzioni di configurazione possibili sono: <br />- Conteggio univoco/non univoco <br /> - Conteggio minimo| Configurata nei centri di amministrazione con i tipi di informazioni riservate predefiniti e i [tipi di informazioni personalizzati](/microsoft-365/compliance/create-a-custom-sensitive-information-type)<br /><br />Le opzioni di configurazione possibili sono:  <br />- Solo conteggio univoco <br />- Conteggio minimo e massimo <br />- Supporto di AND e OR con i tipi di informazioni <br />- Dizionario di parole chiave<br />- Livello di attendibilità e prossimità dei caratteri personalizzabili|
|**Supporto degli ordini per le etichette secondarie sugli allegati** | Abilitato con un' [impostazione client avanzata](client-admin-guide-customizations.md#enable-order-support-for-sublabels-on-attachments) | Abilitata per impostazione predefinita, nessuna configurazione richiesta|
|**Modificare il comportamento di protezione predefinito per i tipi di file**| Usare le [modifiche del registro di sistema](client-admin-guide-file-types.md#changing-the-default-protection-level-of-files) per eseguire l'override delle impostazioni predefinite di protezione nativa e generica | Usare [PowerShell](clientv2-admin-guide-customizations.md#change-which-file-types-to-protect) per modificare i tipi di file da proteggere|
|**Ripetizioni automatiche** | Le ripetizioni complete vengono eseguite automaticamente ogni volta che lo scanner rileva una modifica nei criteri o nelle impostazioni di assegnazione di etichette | A partire dalla versione [2.8.85.0](unifiedlabelingclient-version-release-history.md#version-28850), gli amministratori possono scegliere di ignorare una ripetizione completa dopo avere apportato modifiche alle impostazioni del processo di analisi del contenuto o dei criteri. |
|**Individuazione di rete** |Le funzionalità di individuazione di rete non sono disponibili per lo scanner classico | Gli amministratori possono individuare ulteriori repository rischiosi analizzando un intervallo o un indirizzo IP specificato.|
| | | |

### <a name="features-not-planned-to-be-in-the-azure-information-protection-unified-labeling-client"></a>Funzionalità non previste nel client di Azure Information Protection Unified Labeling

Anche se il Azure Information Protection client di assegnazione unificata di etichette è ancora in fase di sviluppo, le seguenti funzionalità e differenze di comportamento rispetto al client classico non sono attualmente pianificate per essere disponibili nelle versioni future per il client Unified Labeling: 

- Autorizzazioni personalizzate come [opzione separata che gli utenti possono selezionare nelle app di Office: Word, Excel e PowerPoint](client-classify-protect.md#set-custom-permissions-for-a-document)

- La barra degli strumenti sensibilità non Mostra il titolo della **riservatezza** , né una descrizione comando titolo. La barra stessa viene visualizzata nel client Unified labeling.

- [Modalità di sola protezione](client-protection-only-mode.md) (nessuna etichetta) tramite i modelli

- Proteggi documento PDF come file con [estensione Ppdf (formato precedente)](client-admin-guide-customizations.md#dont-protect-pdf-files-by-using-the-iso-standard-for-pdf-encryption)

- Visualizzare il pulsante **non trasmettere** in Outlook

- Criteri demo

- Separazione dei cmdlet PowerShell per la connessione a un servizio Rights Management

- Visualizzazione dell'identità utente che ha applicato un'etichetta


### <a name="parent-labels-and-their-sublabels"></a>Etichette padre ed etichette secondarie 

Il client Azure Information Protection classico non supporta le configurazioni che specificano un'etichetta padre con etichette secondarie. Queste configurazioni includono la specifica di un'etichetta predefinita e un'etichetta per la classificazione consigliata o automatica. Quando un'etichetta ha etichette secondarie, è possibile specificare una delle etichette secondarie, ma non l'etichetta padre.

Per motivi di parità, nemmeno il client per l'etichettatura unificata di Azure Information Protection supporta l'applicazione di etichette padre con etichette secondarie, anche se è possibile selezionare queste etichette nei centri di amministrazione. In questo scenario il client di etichettatura unificata Azure Information Protection non applicherà l'etichetta padre.

## <a name="next-steps"></a>Passaggi successivi

Per installare e configurare il client di Azure Information Protection Unified Labeling, vedere:

- [Client di etichettatura unificata di Azure Information Protection: guida per gli amministratori](clientv2-admin-guide.md)
- [Guida dell'utente per l'assegnazione di etichette unificata Azure Information Protection](clientv2-user-guide.md)

Per altre informazioni sull'uso della soluzione incorporata di assegnazione di etichette per Microsoft 365 app, vedere [etichette di riservatezza nelle app di Office](/microsoft-365/compliance/sensitivity-labels-office-apps).
