---
title: Aggiornare i modelli di Azure RMS - AIP
description: "Quando si usa Azure Rights Management, i modelli vengono scaricati automaticamente nei computer client, in modo che gli utenti possano selezionarli dalle rispettive applicazioni. Può tuttavia essere necessario eseguire alcuni passaggi aggiuntivi se si apportano modifiche ai modelli."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 05/30/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 8c2064f0-dd71-4ca5-9040-1740ab8876fb
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 374c807862d4922679e8622ee0d0d5a16a156bb0
ms.sourcegitcommit: 04eb4990e2bf0004684221592cb93df35e6acebe
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/30/2017
---
<a id="refreshing-templates-for-users-and-services" class="xliff"></a>

# Aggiornamento di modelli per utenti e servizi

>*Si applica a: Azure Information Protection, Office 365*

Quando si usa il servizio Azure Rights Management di Azure Information Protection, i modelli vengono scaricati automaticamente nei computer client, in modo che gli utenti possano selezionarli dalle rispettive applicazioni. Potrebbe tuttavia essere necessario effettuare alcuni passaggi aggiuntivi se si apportano modifiche ai modelli:

|Applicazione o servizio|Modalità di aggiornamento dei modelli dopo le modifiche|
|--------------------------|---------------------------------------------|
|Exchange Online<br /><br />Applicabile per regole di trasporto, regole DLP e Outlook Web App|È necessaria la configurazione manuale per aggiornare i modelli.<br /><br />Per la procedura di configurazione, vedere la sezione seguente: [Solo Exchange Online: come configurare Exchange per il download dei modelli personalizzati modificati](#exchange-online-only-how-to-configure-exchange-to-download-changed-custom-templates).|
|Client Azure Information Protection|I modelli vengono aggiornati automaticamente ogni volta che si aggiornano i criteri di Azure Information Protection nel client:<br /><br /> - Quando viene aperta un'applicazione di Office che supporta la barra di Azure Information Protection. <br /><br /> - Quando si fa clic con il pulsante destro del mouse per classificare e proteggere un file o una cartella. <br /><br /> - Quando si eseguono i cmdlet di PowerShell per l'assegnazione di etichette e la protezione (Get-AIPFileStatus e Set-AIPFileLabel).<br /><br /> - Ogni 24 ore.<br /><br /> Inoltre, poiché il client Azure Information Protection è strettamente integrato con Office, i modelli aggiornati per Office 2016 o Office 2013 verranno aggiornati anche per il client Azure Information Protection.|
|Office 2016 e Office 2013<br /><br />Applicazione RMS sharing per Windows|I modelli vengono aggiornati automaticamente in base a una pianificazione:<br /><br />- Per le versioni più recenti di Office: l'intervallo di aggiornamento predefinito è di 7 giorni.<br /><br />- Per l'applicazione RMS sharing per Windows: a partire dalla versione 1.0.1784.0 l'intervallo di aggiornamento predefinito è di 1 giorno. Le versioni precedenti prevedono un intervallo di aggiornamento predefinito di 7 giorni.<br /><br />Per anticipare l'esecuzione di un aggiornamento rispetto a questa pianificazione, vedere la sezione [Office 2016, Office 2013 e applicazione RMS sharing per Windows: come forzare un aggiornamento per un modello personalizzato modificato](#office-2016--office-2013-and-rms-sharing-application-for-windows-how-to-force-a-refresh-for-a-changed-custom-template).|
|Office 2010|I modelli vengono aggiornati automaticamente quando gli utenti si disconnettono da Windows, eseguono nuovamente l'accesso e attendono al massimo un'ora.|
|Exchange locale con il connettore di Rights Management<br /><br />Applicabile per regole di trasporto e Outlook Web App|I modelli vengono aggiornati automaticamente e non sono necessari altri passaggi. Tuttavia, Outlook Web App memorizza nella cache l'interfaccia utente per un giorno.|
|Office 2016 per Mac|I modelli vengono aggiornati automaticamente e non sono necessari altri passaggi.|
|App RMS sharing per computer Mac|I modelli vengono aggiornati automaticamente e non sono necessari altri passaggi.|

Se per le applicazioni client è necessario scaricare un modello (iniziale o aggiornato con le modifiche), prevedere un'attesa fino a 15 minuti prima che il download sia completato e che i modelli nuovi o aggiornati siano completamente funzionali. Il tempo effettivo varia a seconda di fattori quali le dimensioni e la complessità della configurazione dei modelli e la connettività di rete. 

<a id="exchange-online-only-how-to-configure-exchange-to-download-changed-custom-templates" class="xliff"></a>

## Solo Exchange Online: come configurare Exchange per il download dei modelli personalizzati modificati
Se Information Rights Management (IRM) è stato già configurato per Exchange Online, i modelli personalizzati non verranno scaricati per gli utenti finché non si apportano le modifiche illustrate di seguito mediante Windows PowerShell in Exchange Online.

> [!NOTE]
> Per altre informazioni su come usare Windows PowerShell in Exchange Online, vedere [Uso di PowerShell con Exchange Online](https://technet.microsoft.com/library/jj200677%28v=exchg.160%29.aspx).

È necessario eseguire questa procedura ogni volta che si modifica un modello.

<a id="to-update-templates-for-exchange-online" class="xliff"></a>

### Per aggiornare i modelli per Exchange Online

1.  Usando Windows PowerShell in Exchange Online, connettersi al servizio:

    1.  Fornire il nome utente di Office 365 e la password:

        ```
        $UserCredential = Get-Credential
        ```

    2.  Connettersi al servizio Exchange Online eseguendo i due comandi seguenti:

        ```
        $Session = New-PSSession -ConfigurationName Microsoft.Exchange -ConnectionUri https://outlook.office365.com/powershell-liveid/ -Credential $UserCredential -Authentication Basic -AllowRedirection
        ```

        ```
        Import-PSSession $Session
        ```

2.  Usare il cmdlet [Import-RMSTrustedPublishingDomain](http://technet.microsoft.com/library/jj200724%28v=exchg.160%29.aspx) per reimportare il dominio di pubblicazione trusted da Azure RMS:

    ```
    Import-RMSTrustedPublishingDomain -Name "<TPD name>" -RefreshTemplates -RMSOnline
    ```
    Ad esempio, se il nome del dominio di pubblicazione trusted è **RMS Online - 1** (un nome tipico per molte organizzazioni), immettere: **Import-RMSTrustedPublishingDomain -Name "RMS Online - 1" -RefreshTemplates -RMSOnline**

    > [!NOTE]
    > Per verificare il nome del dominio di pubblicazione trusted, è possibile usare il cmdlet [Get-RMSTrustedPublishingDomain](http://technet.microsoft.com/library/jj200707%28v=exchg.160%29.aspx) .

3.  Per verificare che i modelli siano stati importati correttamente, attendere alcuni minuti, quindi eseguire il cmdlet [Get-RMSTemplate](http://technet.microsoft.com/library/dd297960%28v=exchg.160%29.aspx) e impostare Type su All. Ad esempio:

    ```
    Get-RMSTemplate -TrustedPublishingDomain "RMS Online - 1" -Type All
    ```
    > [!TIP]
    > È utile conservare una copia dell'output affinché sia possibile copiare facilmente i nomi di modello o GUID se si archivia un modello in un secondo momento.

4.  Per ogni modello importato da rendere disponibile in Outlook Web App è necessario usare il cmdlet [Set-RMSTemplate](http://technet.microsoft.com/library/hh529923%28v=exchg.160%29.aspx) e impostare Type su Distributed:

    ```
    Set-RMSTemplate -Identity "<name  or GUID of the template>" -Type Distributed
    ```
    Poiché Outlook Web Access memorizza nella cache l'interfaccia utente per 24 ore, gli utenti potrebbero non vedere il nuovo modello per un intervallo di tempo che può raggiungere un giorno.

Inoltre, se si archivia un modello (personalizzato o predefinito) e si usa Exchange Online con Office 365, gli utenti continueranno a vedere i modelli archiviati se si avvalgono di Outlook Web App o di dispositivi mobili che usano il protocollo Exchange ActiveSync.

Per impedire agli utenti di visualizzare questi modelli, connettersi al servizio mediante Windows PowerShell in Exchange Online, quindi usare il cmdlet [Set-RMSTemplate](http://technet.microsoft.com/library/hh529923%28v=exchg.160%29.aspx) eseguendo il comando seguente:

```
Set-RMSTemplate -Identity "<name or GUID of the template>" -Type Archived
```

<a id="office-2016--office-2013-and-rms-sharing-application-for-windows-how-to-force-a-refresh-for-a-changed-custom-template" class="xliff"></a>

## Office 2016, Office 2013 e applicazione RMS sharing per Windows: come forzare un aggiornamento per un modello personalizzato modificato
Modificando il Registro di sistema nei computer che eseguono Office 2016, Office 2013 o l'applicazione Rights Management (RMS) sharing per Windows, è possibile modificare la pianificazione automatica in modo che i modelli modificati vengano aggiornati nei computer più frequentemente rispetto al relativo valore predefinito. È inoltre possibile forzare un aggiornamento immediato eliminando i dati esistenti in un valore del Registro di sistema.

> [!WARNING]
> L'uso inappropriato dell'editor del Registro di sistema può causare seri problemi che potrebbero richiedere la reinstallazione del sistema operativo. Microsoft non garantisce che sia possibile risolvere i problemi derivanti da un uso non corretto dell'editor del Registro di sistema. L'uso dell'editor del Registro di sistema è di sola responsabilità dell'utente.

<a id="to-change-the-automatic-schedule" class="xliff"></a>

### Per modificare la pianificazione automatica

1.  Utilizzando un editor del Registro di sistema, creare e impostare uno dei seguenti valori del Registro di sistema:

    - Per impostare una frequenza di aggiornamento in giorni (minimo di 1 giorno):  Creare un nuovo valore del Registro di sistema denominato **TemplateUpdateFrequency** e definire un valore intero per i dati, che specifica la frequenza in giorni per il download di tutte le modifiche a un modello scaricato. Usare le informazioni seguenti per individuare il percorso del Registro di sistema per creare questo nuovo valore del registro.

        **Percorso del Registro di sistema:** HKEY_CURRENT_USER\Software\Classes\Local Settings\Software\Microsoft\MSIPC

        **Tipo:** REG_DWORD

        **Valore:** TemplateUpdateFrequency

    - Per impostare una frequenza di aggiornamento in secondi (minimo di 1 secondo):  Creare un nuovo valore del Registro di sistema denominato **TemplateUpdateFrequencyInSeconds** e definire un valore intero per i dati, che specifica la frequenza in secondi per il download di tutte le modifiche a un modello scaricato. Usare le informazioni seguenti per individuare il percorso del Registro di sistema per creare questo nuovo valore del registro.

        **Percorso del Registro di sistema:** HKEY_CURRENT_USER\Software\Classes\Local Settings\Software\Microsoft\MSIPC

        **Tipo:** REG_DWORD

        **Valore:** TemplateUpdateFrequencyInSeconds

    Assicurarsi di creare e impostare uno di questi valori del Registro di sistema, non entrambi. Se sono presenti entrambi, **TemplateUpdateFrequency** viene ignorato.

2.  Se si desidera forzare un aggiornamento immediato dei modelli, passare alla procedura successiva. In caso contrario, riavviare ora le applicazioni di Office e le istanze di Esplora file.

<a id="to-force-an-immediate-refresh" class="xliff"></a>

### Per forzare un aggiornamento immediato

1.  Utilizzando un editor del Registro di sistema, eliminare i dati per il valore **LastUpdatedTime** . Ad esempio, i dati possono visualizzare **2015-04-20T15:52**; eliminare 2015-04-20T15:52 in modo che non vengano visualizzati dati. Usare le informazioni seguenti per individuare il percorso del Registro di sistema per eliminare i dati con questo valore di registro.

    **Percorso del Registro di sistema:** HKEY_CURRENT_USER\Software\Classes\Local Settings\Software\Microsoft\MSIPC\\<*MicrosoftRMS_FQDN*>\Template

    **Tipo:** REG_SZ

    **Valore:** LastUpdatedTime

    > [!TIP]
        > Nel percorso del Registro di sistema, <*MicrosoftRMS_FQDN*> fa riferimento all’FQDN del servizio Microsoft RMS. Se si desidera verificare questo valore:

    > 1.  Eseguire il cmdlet [Get-AadrmConfiguration](https://msdn.microsoft.com/library/windowsazure/dn629410.aspx) per Azure RMS. Se non è stato ancora installato il modulo di Windows PowerShell per Azure RMS, vedere [Installazione di Windows PowerShell per Azure Rights Management](install-powershell.md).
    > 2.  Nell'output identificare il valore **LicensingIntranetDistributionPointUrl** .
    > 
    >     Ad esempio: **LicensingIntranetDistributionPointUrl   : https://5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com/_wmcs/licensing**
    > 3.  In questo valore rimuovere **https://** e **/_wmcs/licensing** da questa stringa. Il valore rimanente è l’FQDN del servizio Microsoft RMS. Nell'esempio, il valore dell'FQDN di Microsoft RMS è il seguente:
    > 
    >     **5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com**

2.  Eliminare la cartella seguente e tutti i file in essa contenuti: **%localappdata%\Microsoft\MSIPC\Templates**

3.  Riavviare le applicazioni di Office e le istanze di Esplora file.


<a id="see-also" class="xliff"></a>

## Vedere anche
[Configurare modelli personalizzati per Azure Rights Management](configure-custom-templates.md)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]