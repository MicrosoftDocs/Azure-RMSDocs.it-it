---
title: Modalità di sola protezione per Azure Information Protection
description: Informazioni per gli utenti che eseguono il client Azure Information Protection in modalità di sola protezione.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 1/13/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 16042717-0d7a-41f5-87e3-12826fda35df
ROBOTS: NOINDEX
ms.subservice: v1client
ms.reviewer: eymanor
ms.suite: ems
ms.custom: user
ms.openlocfilehash: af64fc43cd137bfe9f9f05c4237d4a617fd0898d
ms.sourcegitcommit: b32c16e41ba36167b5a3058b56a73183bdd4306d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/29/2020
ms.locfileid: "97807230"
---
# <a name="user-guide-protection-only-mode-for-the-azure-information-protection-client"></a>Guida dell'utente: Modalità di sola protezione per il client Azure Information Protection

>***Si applica a**: Active Directory Rights Management Services, [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8 *
>
>***Rilevante per**: [Client classico Azure Information Protection per Windows](../faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

>[!NOTE] 
> Per offrire un'esperienza per i clienti unificata e semplificata, il **client classico di Azure Information Protection** e **Gestione etichette** nel portale di Azure saranno **deprecati** a partire dal **31 marzo 2021**. In questo intervallo di tempo tutti i clienti correnti di Azure Information Protection possono passare alla soluzione di etichettatura unificata usando la piattaforma di etichettatura unificata di Microsoft Information Protection. Altre informazioni nell'[avviso ufficiale sulla deprecazione](https://aka.ms/aipclassicsunset).

Quando il client Azure Information Protection non dispone di etichette per classificare i documenti e i messaggi di posta elettronica, viene eseguito in modalità di **sola protezione**. In questa modalità, ad esempio, potrebbe essere visualizzato quanto segue quando si usa Esplora file, si fa clic con il pulsante destro del mouse e si sceglie **Classifica e proteggi**:

![Modalità di sola protezione](../media/protection-only-mode.png)

La modalità di sola protezione viene eseguita negli scenari seguenti:

- L'organizzazione non ha una sottoscrizione per Azure Information Protection che include funzionalità di classificazione e assegnazione di etichette, ma dispone di una sottoscrizione per Microsoft 365 che include la protezione dei dati tramite il servizio Rights Management di Azure. 
    
    - È possibile usare il client Azure Information Protection per proteggere i file e visualizzare i file protetti. Non è possibile classificare o etichettare documenti e messaggi di posta elettronica.

- L'organizzazione dispone di una sottoscrizione per Azure Information Protection solo per un subset di utenti:
    
    - Per questa combinazione di abbonamenti, è responsabilità dell'amministratore assicurarsi che solo il subset di utenti possa usare le funzionalità di classificazione ed etichettatura. Gli altri utenti devono eseguire il client Azure Information Protection in modalità di sola protezione. 

- L'organizzazione dispone di un abbonamento per Azure Information Protection, ma non è configurata nessuna etichetta.
    
    - Ciò può verificarsi quando tutte le etichette nei criteri globali sono disabilitate e l'account non è stato aggiunto a criteri con ambito. È possibile che il reparto IT abbia appena iniziato a distribuire Azure Information Protection, ma non abbia ancora fornito le etichette per classificare i documenti e i messaggi di posta elettronica. Nel frattempo, è possibile usare il client Azure Information Protection per proteggere i file e visualizzare i file protetti.

- L'organizzazione ha una sottoscrizione per Azure Information Protection, ma non è possibile scaricare i relativi criteri. 
    
    - Ciò può accadere a causa di un errore di configurazione o di accesso. Contattare l'help desk o l'amministratore. Nel frattempo potrebbe comunque essere possibile usare il client Azure Information Protection per proteggere i file e visualizzare i file protetti.

- L'organizzazione usa solo Active Directory Rights Management Services (AD RMS). 


## <a name="limitations-for-protection-only-mode"></a>Limitazioni per la modalità di sola protezione

- Nelle app di Office la barra di Azure Information Protection non viene visualizzata. Quando si fa clic su **Proteggi**  >  **Mostra barra**, questa opzione di menu non è disponibile.

- Quando si usa la finestra di dialogo **Classifica e proteggi - Azure Information Protection** con Esplora file, non vengono visualizzate le etichette per la classificazione. Al contrario, come illustrato nell'immagine precedente, viene visualizzata un'opzione per selezionare i modelli di Rights Management (RMS). 

## <a name="supported-tasks-for-protection-only-mode"></a>Attività supportate per la modalità di sola protezione

- Proteggere (e rimuovere la protezione) documenti e messaggi di posta elettronica dalle app di Office, usando la funzionalità Office Information Rights Management (IRM): ad esempio: fare clic su **file**  >  **informazioni**  >  **Proteggi documento**  >  **limita accesso**. Per altre informazioni, vedere [Uso della protezione delle informazioni con Office 365, Office 2019, Office 2016 o Office 2013](../help-users.md#using-information-protection-with-office365-office-2019-office-2016-or-office2013).

- Proteggere i file (e rimuovere la protezione) usando Esplora file di Windows: fare clic con il pulsante destro del mouse su uno o più file o su una cartella > **Classifica e proteggi**. Per applicare la protezione configurata dall'amministratore, nella finestra di dialogo **Classifica e proteggi - Azure Information Protection** fare clic su **Seleziona modello** e scegliere uno dei modelli disponibili.

- Visualizzare i file protetti usando il visualizzatore Azure Information Protection.

- Accedere al sito di rilevamento dei documenti dalle app di Office. È tuttavia necessario avere una sottoscrizione valida per tenere traccia dei documenti e revocarli dal sito.
  
