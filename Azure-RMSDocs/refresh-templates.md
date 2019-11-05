---
title: Aggiornare i modelli di Azure RMS - AIP
description: Quando si usa Azure Rights Management, i modelli vengono scaricati automaticamente nei computer client, in modo che gli utenti possano selezionarli dalle rispettive applicazioni. Può tuttavia essere necessario eseguire alcuni passaggi aggiuntivi se si apportano modifiche ai modelli.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 10/09/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 8c2064f0-dd71-4ca5-9040-1740ab8876fb
ms.subservice: azurerms
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: bcd6a8cf37abc6e66fe272c7de794379efc9b49e
ms.sourcegitcommit: f5d8cf4440a35afaa1ff1a58b2a022740ed85ffd
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/04/2019
ms.locfileid: "73561353"
---
# <a name="refreshing-templates-for-users-and-services"></a>Aggiornamento di modelli per utenti e servizi

>*Si applica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

Quando si usa il servizio Rights Management di Azure da Azure Information Protection, i modelli di protezione vengono scaricati automaticamente nei computer client in modo che gli utenti possano selezionarli dalle rispettive applicazioni. Potrebbe tuttavia essere necessario effettuare alcuni passaggi aggiuntivi se si apportano modifiche ai modelli:

|Applicazione o servizio|Modalità di aggiornamento dei modelli dopo le modifiche|
|--------------------------|---------------------------------------------|
|Exchange Online<br /><br />Applicabile per regole di trasporto e Outlook Web App |Vengono aggiornati automaticamente in un'ora e non sono necessari altri passaggi.|
|Client Azure Information Protection|I modelli vengono aggiornati automaticamente ogni volta che si aggiornano i criteri di Azure Information Protection nel client:<br /><br /> - Quando viene aperta un'applicazione di Office che supporta la barra di Azure Information Protection. <br /><br /> - Quando si fa clic con il pulsante destro del mouse per classificare e proteggere un file o una cartella. <br /><br /> - Quando si eseguono i cmdlet di PowerShell per l'assegnazione di etichette e la protezione (Get-AIPFileStatus e Set-AIPFileLabel).<br /><br /> - Quando il servizio scanner di Azure Information Protection viene avviato e i criteri locali risalgono a più di un'ora prima. Il servizio scanner verifica le modifiche ogni ora e usa tali modifiche per il ciclo di analisi successivo.<br /><br /> - Ogni 24 ore.<br /><br /> Inoltre, poiché il client è strettamente integrato con Office, i modelli aggiornati per app di Office 365, Office 2019, Office 2016 o Office 2013 verranno aggiornati anche per il client Azure Information Protection.|
|Client per l'etichettatura unificata di Azure Information Protection|Aggiornamento automatico ogni 4 ore, per ogni app di Office.<br /><br /> Inoltre, poiché il client è strettamente integrato con Office, i modelli aggiornati per app di Office 365, Office 2019, Office 2016 o Office 2013 verranno aggiornati anche per il client di etichettatura unificata Azure Information Protection.|
|App di Office 365, Office 2019, Office 2016 e Office 2013|I modelli vengono aggiornati automaticamente in base a una pianificazione:<br /><br />- Per le versioni più recenti di Office: l'intervallo di aggiornamento predefinito è di 7 giorni.<br /><br />Per forzare un aggiornamento prima della pianificazione, vedere la sezione seguente, [app di office 365, office 2019, office 2016 e office 2013: come forzare un aggiornamento per i modelli](#office-365-apps-office-2019-office-2016-and-office-2013-how-to-force-a-refresh-for-templates).|
|Office 2010|I modelli vengono aggiornati automaticamente quando gli utenti si disconnettono da Windows, eseguono nuovamente l'accesso e attendono al massimo un'ora.|
|Exchange locale con il connettore di Rights Management<br /><br />Applicabile per regole di trasporto e Outlook Web App|I modelli vengono aggiornati automaticamente e non sono necessari altri passaggi. Tuttavia, Outlook Web App memorizza nella cache l'interfaccia utente per un giorno.|
|Office 2019 per Mac e Office 2016 per Mac|Aggiornamento automatico quando si apre il contenuto protetto. Per forzare un aggiornamento, vedere la sezione seguente [office 2019 per Mac e office 2016 per Mac: come forzare un aggiornamento per i modelli](#office-2019-for-mac-and-office-2016-for-mac-how-to-force-a-refresh-for-templates).|
|App RMS sharing per computer Mac|I modelli vengono aggiornati automaticamente e non sono necessari altri passaggi.|
|Le app di Office che [supportano la funzionalità Riservatezza](https://support.office.com/article/apply-sensitivity-labels-to-your-documents-and-email-within-office-2f96e7cd-d5a4-403b-8bd7-4cc636bae0f9?ad=US&ui=en-US&rs=en-US#bkmk_whereavailable)|Questi client non scaricano i modelli ma vi accedono online - non sono necessari passaggi aggiuntivi.|

Quando le applicazioni client devono scaricare i modelli (inizialmente o aggiornati per le modifiche), prepararsi ad attendere fino a 30 minuti prima che il download sia completo e che i modelli nuovi o aggiornati siano completamente operativi. Il tempo effettivo varia a seconda di fattori quali le dimensioni e la complessità della configurazione dei modelli e la connettività di rete. 

## <a name="office-365-apps-office-2019-office-2016-and-office-2013-how-to-force-a-refresh-for-templates"></a>App Office 365, Office 2019, Office 2016 e Office 2013: come forzare un aggiornamento per i modelli
Modificando il Registro di sistema nei computer che eseguono app di Office 365, Office 2019, Office 2016 oppure Office 2013 è possibile modificare la pianificazione automatica in modo che i modelli modificati vengano aggiornati nei computer più frequentemente rispetto al relativo valore predefinito. È inoltre possibile forzare un aggiornamento immediato eliminando i dati esistenti in un valore del Registro di sistema.

> [!WARNING]
> L'uso inappropriato dell'editor del Registro di sistema può causare seri problemi che potrebbero richiedere la reinstallazione del sistema operativo. Microsoft non garantisce che sia possibile risolvere i problemi derivanti da un uso non corretto dell'editor del Registro di sistema. L'uso dell'editor del Registro di sistema è di sola responsabilità dell'utente.

### <a name="to-change-the-automatic-schedule"></a>Per modificare la pianificazione automatica

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

### <a name="to-force-an-immediate-refresh"></a>Per forzare un aggiornamento immediato

1. Utilizzando un editor del Registro di sistema, eliminare i dati per il valore **LastUpdatedTime** . Ad esempio, i dati possono visualizzare **2015-04-20T15:52**; eliminare 2015-04-20T15:52 in modo che non vengano visualizzati dati. Usare le informazioni seguenti per individuare il percorso del Registro di sistema per eliminare i dati con questo valore di registro.

   **Percorso del Registro di sistema:** HKEY_CURRENT_USER\Software\Classes\Local Settings\Software\Microsoft\MSIPC\\<*MicrosoftRMS_FQDN*>\Template\\<*user_alias*>

   **Tipo:** REG_SZ

   **Valore:** LastUpdatedTime

   > [!TIP]
   > Nel percorso del Registro di sistema, <*MicrosoftRMS_FQDN*> fa riferimento all’FQDN del servizio Microsoft RMS. Se si desidera verificare questo valore:
   > 
   > Eseguire il cmdlet [Get-AipServiceConfiguration](/powershell/module/aipservice/get-aipserviceconfiguration) per Azure Information Protection. Se non è stato ancora installato il modulo AIPService di PowerShell, vedere [installazione del modulo PowerShell di AIPService](install-powershell.md).
   > 
   > Nell'output identificare il valore **LicensingIntranetDistributionPointUrl** .
   > 
   > Ad esempio: **LicensingIntranetDistributionPointUrl: https://5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com/_wmcs/licensing**
   > 
   > In questo valore rimuovere **https://** e **/_wmcs/licensing** da questa stringa. Il valore rimanente è l’FQDN del servizio Microsoft RMS. Nell'esempio, il valore dell'FQDN di Microsoft RMS è il seguente:
   > 
   > **5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com**

2. Eliminare la seguente cartella e tutti i file in essa contenuti: **%localappdata%\Microsoft\MSIPC\Templates**

3. Riavviare le applicazioni di Office e le istanze di Esplora file.

## <a name="office-2019-for-mac-and-office-2016-for-mac-how-to-force-a-refresh-for-templates"></a>Office 2019 per Mac e Office 2016 per Mac: come forzare un aggiornamento per i modelli

In queste versioni di Office per Mac, i modelli vengono aggiornati quando si apre il contenuto protetto o si protegge il contenuto usando un'etichetta di riservatezza appena configurata per applicare la crittografia. Se è necessario forzare un aggiornamento dei modelli, è possibile usare le istruzioni seguenti. Tuttavia, il comando nelle istruzioni Elimina i modelli, la cache dei token RMS nella catena di chiavi e le licenze di utilizzo locale per qualsiasi contenuto protetto aperto precedentemente. Di conseguenza, sarà necessario eseguire nuovamente l'autenticazione ed è necessario disporre di una connessione a Internet per aprire il contenuto protetto aperto precedentemente.

1. Aprire il terminale e immettere il comando seguente:
    
        defaults write ~/Library/Containers/com.microsoft.Outlook/Data/Library/Preferences/com.microsoft.Outlook ResetRMSCache 1

2. Riavviare Outlook per Mac.

3. Creare un nuovo messaggio di posta elettronica e selezionare **Crittografa**, quindi **verificare le credenziali**.


## <a name="see-also"></a>Vedere anche
[Configurazione e gestione dei modelli nei criteri di Azure Information Protection](configure-policy-templates.md)

