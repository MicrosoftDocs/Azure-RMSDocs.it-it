---
title: RMS per utenti singoli e Azure Information Protection
description: Informazioni su RMS per utenti singoli, una sottoscrizione self-service gratuita per gli utenti ai quali sono stati inviati file protetti, ma che non possono essere autenticati perché il reparto IT non gestisce per loro un account di Azure.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 11/08/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 2efcb440-fefd-45e9-872b-f471573aadf2
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: ac5b596c87649e32d27da8e2797bafe5b9745792
ms.sourcegitcommit: 8a141858e494dd1d3e48831e6cd5a5be48ac00d2
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2020
ms.locfileid: "97384792"
---
# <a name="rms-for-individuals-and-azure-information-protection"></a>RMS per utenti singoli e Azure Information Protection

>***Si applica a**: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*
>
>***Pertinente per**: [AIP Unified Labeling client e client classico](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients). *

>[!NOTE] 
> Per offrire un'esperienza utente unificata e semplificata, **Azure Information Protection** la gestione classica di client e **etichette** nel portale di Azure verrà **deprecata** a partire dal **31 marzo 2021**. In questo intervallo di tempo tutti i clienti correnti di Azure Information Protection possono passare alla soluzione di etichettatura unificata usando la piattaforma di etichettatura unificata di Microsoft Information Protection. Altre informazioni nell'[avviso ufficiale sulla deprecazione](https://aka.ms/aipclassicsunset).

RMS per utenti singoli è una sottoscrizione self-service gratuita per gli utenti che devono aprire file protetti da Azure Information Protection. Se questi utenti non possono essere autenticati da Azure Active Directory, questo servizio di iscrizione gratuito consente di creare un account in Azure Active Directory per un utente. Di conseguenza, questi utenti ora possono effettuare l'autenticazione usando l'indirizzo di posta elettronica aziendale e quindi leggere i file protetti nei computer o dispositivi mobili.

RMS per utenti singoli usa l'iscrizione self-service di Azure Active Directory. Se gli utenti hanno creato account per l'organizzazione usando questa sottoscrizione, l'amministratore dell'organizzazione può rivendicare la proprietà e [assumere il controllo dei loro account](/azure/active-directory/users-groups-roles/domains-admin-takeover#external-admin-takeover). 

Per iscriversi per ottenere l'account gratuito, gli utenti devono passare alla [pagina di Microsoft Azure Information Protection](https://aka.ms/rms-signup) e specificare il proprio indirizzo di posta elettronica aziendale. Gli utenti riceveranno un messaggio di posta elettronica di risposta da Microsoft e potranno quindi completare la procedura di iscrizione inserendo i dettagli per creare l'account. 

Dopo aver creato l'account, viene visualizzata la pagina finale con collegamenti per scaricare il client o il visualizzatore di Azure Information Protection per diversi dispositivi, con un collegamento alla guida per l'utente e un collegamento all'elenco aggiornato delle applicazioni che supportano la protezione di Rights Management in modo nativo. 

### <a name="alternatives-use-office-365-message-encryption-or-microsoft-accounts"></a>Alternative: usare la crittografia messaggi di Office 365 o gli account Microsoft

RMS per utenti singoli è un'opzione che consente di garantire che gli utenti autorizzati all'esterno dell'organizzazione possano sempre leggere i file protetti dall'organizzazione. 

Le opzioni alternative includono:

- **Inviare tramite posta elettronica i documenti usando [la crittografia messaggi di Office 365 con le nuove funzionalità](https://support.office.com/article/7ff0c040-b25c-4378-9904-b1b50210d00e).** Questa soluzione tramite posta elettronica funziona per tutti gli indirizzi di posta elettronica in tutti i dispositivi ed è il metodo consigliato per condividere in modo sicuro le informazioni e visualizzare documenti di Office in un browser insieme a utenti esterni all'organizzazione.
 
- **Usare gli account Microsoft.** Non tutte le applicazioni possono aprire il contenuto protetto quando si usa un account Microsoft per l'autenticazione. [Altre informazioni](secure-collaboration-documents.md#supported-scenarios-for-opening-protected-documents) 


## <a name="to-sign-up-for-rms-for-individuals"></a>Per iscriversi per RMS per utenti singoli

1. Su un computer Windows o Mac o un dispositivo mobile, andare alla [pagina di Microsoft Azure Information Protection](https://aka.ms/rms-signup).

2. Digitare l'indirizzo di posta elettronica usato per proteggere il documento che è necessario aprire.

3. Fare clic su **Iscrizione**.

    Microsoft usa l'indirizzo di posta elettronica dell'utente per verificare se l'organizzazione dispone già di una [sottoscrizione di Azure Information Protection Premium](https://www.microsoft.com/cloud-platform/azure-information-protection-pricing) o un [abbonamento a Office 365 che include la protezione dei dati tramite Azure Information Protection](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf). Se una di queste sottoscrizioni viene trovata, non è necessario RMS per utenti singoli. In questo caso si può accedere immediatamente e l'iscrizione self-service a RMS per utenti singoli viene annullata. Se non viene trovata nessuna di queste sottoscrizioni, si procederà al passaggio successivo.

4. Attendere un messaggio di posta elettronica di conferma proveniente da Microsoft e inviato all'indirizzo di posta indicato Verrà dal team di Microsoft 365 ( support@email.microsoftonline.com ) e il soggetto **concluderà l'iscrizione a Microsoft Azure Information Protection**.

5. Quando si riceve il messaggio di posta elettronica, fare clic su **Sì, sono io** per confermare l'indirizzo di posta elettronica e completare il processo di iscrizione.

6. A questo punto viene aperta la pagina **One last thing ...(Un'ultima operazione)** dove specificare i dettagli per l'account. Digitare il nome, il cognome, specificare e confermare una password a scelta e quindi fare clic su **Start (Avvia)**.

7. Dopo aver creato l'account, verrà visualizzata una nuova pagina di Microsoft Azure Information Protection in cui è possibile scaricare e installare il client di Azure Information Protection oppure fare clic sul collegamento alla [Guida per l'utente](./rms-client/client-user-guide.md) per le procedure per i computer Windows.

A questo punto l'account viene creato. Se viene richiesto di accedere per leggere i file protetti, immettere l'indirizzo di posta elettronica e la password usati per creare l'account per RMS per utenti singoli.

> [!IMPORTANT]
> Anche se ora si possono anche proteggere i file con questo account, non eseguire questa operazione fino a quando l'organizzazione non dispone di una [sottoscrizione di valutazione gratuita o a pagamento](https://azure.microsoft.com/pricing/details/information-protection/) per Azure Information Protection. Se si proteggono file e messaggi di posta elettronica con questa sottoscrizione gratuita e quindi l'organizzazione assume il controllo dell'account, il contenuto protetto in precedenza potrebbe diventare inaccessibile.


## <a name="next-steps"></a>Passaggi successivi
RMS per utenti singoli è un esempio di utilizzo della funzionalità di iscrizione self-service supportata da Azure Active Directory. Per ulteriori informazioni sul funzionamento di questa funzionalità, vedere [che cos'è Self-Service iscrizione per Azure Active Directory?](/azure/active-directory/users-groups-roles/directory-self-service-signup) nella documentazione di Azure Active Directory.

