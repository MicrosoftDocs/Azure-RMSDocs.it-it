---
title: Preparazione per la protezione di Azure Rights Management - AIP
description: Verificare di aver eseguito tutte le operazioni preliminari all&quot;uso del servizio Azure Rights Management, in modo da consentire all&quot;organizzazione di proteggere documenti e messaggi di posta elettronica.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 03/28/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: afbca2d6-32a7-4bda-8aaf-9f93f5da5abc
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 4b074f9a9a3d72b4d1ab5810b69e92b4792b0711
ms.sourcegitcommit: 16fec44713c7064959ebb520b9f0857744fecce9
translationtype: HT
---
# <a name="preparing-for-azure-information-protection"></a>Preparazione per Azure Information Protection

>*Si applica a: Azure Information Protection, Office 365*

Prima di distribuire Azure Information Protection per l'organizzazione, verificare la disponibilità di quanto segue:

-   Account e gruppi utente nel cloud creati manualmente o che sono stati creati automaticamente e sincronizzati dai Servizi di dominio Active Directory (AD DS).

    Quando si sincronizzano gli account e i gruppi locali, non è necessario sincronizzare tutti gli attributi. Per un elenco degli attributi che devono essere sincronizzati per il servizio Azure Rights Management usato da Azure Information Protection, vedere la sezione relativa a [Azure RMS](/active-directory/active-directory-aadconnectsync-attributes-synchronized#azure-rms) nella documentazione di Azure Active Directory. Per facilitare la distribuzione, è consigliabile usare [Azure AD Connect](/active-directory/active-directory-aadconnectsync-whatis) per la connessione delle directory locali ad Azure Active Directory, ma si può usare qualsiasi metodo di sincronizzazione della directory che ottenga lo stesso risultato.

-   Gruppi abilitati alla posta nel cloud da usare con Azure Information Protection. Possono essere gruppi predefiniti o gruppi creati manualmente, che contengono utenti che useranno documenti e messaggi di posta elettronica protetti.

    Se si dispone di Exchange Online, è possibile creare e utilizzare i gruppi abilitati alla posta tramite il centro di amministrazione di Exchange. Se si dispone di AD DS locale e si esegue la sincronizzazione in Azure AD, è possibile creare e utilizzare i gruppi abilitati alla posta che sono gruppi di protezione o gruppi di distribuzione.

### <a name="group-membership-caching"></a>Memorizzazione nella cache dell'appartenenza ai gruppi

Per motivi di prestazioni, l'appartenenza ai gruppi viene memorizzata nella cache dal servizio Azure Rights Management. Ciò significa che le modifiche all'appartenenza ai gruppi possono richiedere fino a tre ore per diventare effettive e questo periodo di tempo è soggetto a variazioni. Ricordare di scomporre questo ritardo per tutte le attività di modifica e test eseguite quando si usano gruppi nella configurazione del servizio Azure Rights Management, ad esempio quando si configurano [modelli personalizzati](../deploy-use/configure-custom-templates.md) o quando si usa un gruppo per la [funzionalità per utenti con privilegi avanzati](../deploy-use/configure-super-users.md). 

### <a name="considerations-if-email-addresses-change"></a>Considerazioni in caso di modifica degli indirizzi di posta elettronica

Quando si configurano diritti di utilizzo per utenti o gruppi e si selezionano questi ultimi in base al nome visualizzato, al momento della selezione viene salvato e usato l'indirizzo di posta elettronica dell'oggetto. Se successivamente l'indirizzo di posta elettronica viene modificato, gli utenti selezionati non verranno autorizzati.

In caso di modifica degli indirizzi di posta elettronica, è consigliabile aggiungere l'indirizzo di posta elettronica precedente come indirizzo proxy (detto anche alias o indirizzo alternativo) all'utente o al gruppo, in modo da mantenere i diritti di utilizzo assegnati in precedenza. Se non è possibile eseguire questa operazione, è necessario rimuovere l'utente o il gruppo dalla configurazione e selezionarlo nuovamente per salvare l'indirizzo di posta elettronica aggiornato da usare per il nuovo contenuto protetto.

I modelli personalizzati di Rights Management offrono un esempio di dove selezionare utenti o gruppi in base al nome visualizzato per assegnare i diritti di utilizzo. Gli utenti possono effettuare questa selezione quando configurano autorizzazioni personalizzate con il client Azure Information Protection.

## <a name="activate-the-rights-management-service-for-data-protection"></a>Attivare il servizio Rights Management per la protezione dei dati
Attivare il servizio Rights Management per abilitare questa tecnologia e iniziare a proteggere documenti e messaggi di posta elettronica. Per ulteriori informazioni, vedere l'articolo relativo all'[attivazione di Azure Rights Management](../deploy-use/activate-service.md).

[!INCLUDE[Commenting house rules](../includes/houserules.md)]


