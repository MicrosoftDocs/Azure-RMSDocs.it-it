---
# required metadata

title: Autenticazione e autorizzazione
description:
keywords:
author: YuriDio
manager: swadhwa
ms.date: 04/28/2016
ms.topic: article
ms.prod:
ms.service:
ms.technology:
ms.assetid: 31b98333-5a3d-49ba-a25e-66447df68035

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: 
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Autenticazione e autorizzazione

>[!NOTE]
>Questo argomento fa parte di una guida più ampia dedicata alle considerazioni di progettazione. Per leggere la guida dall'inizio, vedere l'[argomento principale](mdm-design-considerations-guide.md). Per scaricare una copia della versione integrale della guida, visitare la raccolta [TechNet](https://gallery.technet.microsoft.com/Mobile-Device-Management-7d401582).

Per poter proteggere correttamente i dati aziendali, è necessario identificare l'identità degli utenti, quindi è possibile verificare che dispongano delle autorizzazioni di accesso alla risorsa richiesta. Le organizzazioni che hanno già servizi Active Directory locali attivi devono usarli per l'autenticazione e l'autorizzazione degli utenti mobili. Tutte le soluzioni Microsoft per la gestione dei dispositivi mobili possono usare un'infrastruttura di Active Directory esistente per eseguire questa operazione. 

Un altro aspetto da considerare per le decisioni relative all'autenticazione e all'autorizzazione riguarda la posizione in cui si troveranno i servizi di directory. La maggior parte delle organizzazioni userà servizi di Active Directory locali, ma alcune aziende potrebbero considerare la possibilità di estendere i servizi di directory locali con un servizio di directory basato su cloud come [Azure AD](http://azure.microsoft.com/documentation/articles/active-directory-whatis/). 

Configuration Manager consente di eseguire l'integrazione con [Microsoft Passport for Work](https://technet.microsoft.com/library/mt488797.aspx), un metodo di accesso alternativo che usa Active Directory o un account Azure Active Directory per sostituire una password, una smart card o una smart card virtuale su dispositivi che eseguono Windows 10. Per uno scenario ibrido, l'integrazione di entrambe le directory è una buona alternativa all'uso delle funzionalità di Azure AD, ad esempio:

- **Gestione dei gruppi in modalità self-service**: consente agli utenti di creare gruppi, richiedere l'accesso ad altri gruppi, delegare la proprietà dei gruppi in modo che altri possano approvare le richieste e gestire l'appartenenza ai gruppi.
- **Contratto di servizio Enterprise per il 99,9%**: viene garantita una disponibilità almeno del 99,9% per il servizio Azure Active Directory Premium.
- **Reimpostazione della password con writeback**: è possibile eseguire il writeback della reimpostazione della password self-service nelle directory locali.

Per altre informazioni sulle diverse opzioni e funzionalità, vedere [Azure Active Directory](https://msdn.microsoft.com/library/azure/dn532272.aspx).
La richiesta di due tipi di autenticazione (autenticazione a più fattori o MFA) è un'altra strategia da tenere in considerazione quando si pianifica una soluzione di gestione dei dispositivi mobili. Intune è in grado di [integrare i servizi di directory con l'autenticazione a più fattori](https://technet.microsoft.com/library/dn889751.aspx), aggiungendo un altro livello di sicurezza per il processo di autenticazione. 

Se l'organizzazione ha un'infrastruttura IT locale che include un dominio di Active Directory con Active Directory Federation Services (AD FS), è possibile configurare l'autenticazione a più fattori nel server federativo e abilitare l'autenticazione a più fattori per la registrazione in Intune. Se l'autenticazione a più fattori nel server federativo viene configurata ma non abilitata per la registrazione in Intune, gli utenti dovranno usare l'autenticazione a più fattori ogni volta che accedono alle risorse aziendali da qualsiasi dispositivo. 

È anche possibile usare l'autenticazione a più fattori di Azure AD per richiedere l'autenticazione a più fattori ogni volta che gli utenti accedono alle risorse aziendali, requisito che può essere abilitato a livello di singolo utente. L'autenticazione a più fattori di Azure AD è un servizio cloud che non richiede alcuna infrastruttura IT locale.

Usare la tabella che segue come riferimento per la scelta dell'opzione MDM più adatta ai requisiti aziendali di autenticazione e autorizzazione.

## Intune (autonomo)

**Vantaggi**

- Può usare servizi di directory locali come Active Directory per l'autenticazione
- Può usare servizi di directory basati su cloud come Azure AD per l'autenticazione
- Può essere integrata con l'autenticazione a più fattori

**Svantaggi**

- Il servizio cloud di Azure AD non è incluso quando si acquista una sottoscrizione di Intune

## Gestione dei dispositivi mobili per Office 365

**Vantaggi**

- Può usare directory locali come Active Directory per l'autenticazione
- Può usare directory basate su cloud come Azure AD per l'autenticazione
- Può essere integrata con l'autenticazione a più fattori
- Può sfruttare il Centro di conformità per usare il modello di autorizzazioni del controllo degli accessi in base al ruolo

**Svantaggi**

- Il servizio cloud di Azure AD non è incluso quando si acquista una sottoscrizione di Office 365

## Ibrida (Intune con Configuration Manager)

**Vantaggi**

- Può usare directory locali come Active Directory per l'autenticazione
- Può usare directory basate su cloud come Azure AD per l'autenticazione

**Svantaggi**

- Il servizio cloud di Azure AD non è incluso quando si acquista una sottoscrizione di Intune

## Enterprise Mobility Suite

**Vantaggi**

- Usa Azure AD Premium per consentire il controllo di accesso
- La licenza di Azure AD Premium è già inclusa in EMS
- Non richiede servizi di directory locali
- Può eseguire la sincronizzazione con servizi di Active Directory locali
- L'autenticazione a più fattori è disponibile in modo nativo in EMS

**Svantaggi**

- Non è disponibile per i clienti che non adottano una soluzione basata su cloud



<!--HONumber=Apr16_HO2-->


