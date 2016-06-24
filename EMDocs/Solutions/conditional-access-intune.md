---
# required metadata

title: Usare l'accesso condizionale con Microsoft Intune
description:
keywords:
author: craigcaseyMSFT
manager: swadhwa
ms.date: 04/28/2016
ms.topic: article
ms.prod:
ms.service:
ms.technology:
ms.assetid: 28662db2-faea-425f-ada9-04cf1d976fc2

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: 
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Usare l'accesso condizionale con Microsoft Intune
Questa soluzione consente di usare l'accesso condizionale in Intune per proteggere la posta elettronica e altri servizi in base alle condizioni specificate dall'utente.

Per altre informazioni su come usare la funzionalità di accesso condizionale con Intune, vedere [Restrict access to email and O365 services with Microsoft Intune](/intune/deployuse/restrict-access-to-email-and-o365-services-with-microsoft-intune) (Limitare l'accesso alla posta elettronica e ai servizi di O365 con Microsoft Intune).

> [!TIP]
> È possibile scaricare una copia di questo argomento nella [Raccolta TechNet](https://gallery.technet.microsoft.com/protect-company-data-and-8c5e08b4).

## Prima di iniziare
È possibile controllare l'accesso a Exchange Online e a Exchange locale dalle app di posta elettronica seguenti:

-   App predefinita per Android 4.0 e versioni successive, Samsung Knox 4.0 Standard e versioni successive

-   App predefinita per iOS 7.1 e versioni successive

-   L'applicazione incorporato per Windows Phone 8.1 e versioni successive

-   La posta elettronica dell'applicazione in Windows 8.1 e versioni successiva

-   L'applicazione di Microsoft Outlook per Android e iOS (per Exchange Online solo)

Prima di iniziare a usare l'accesso condizionale, verificare che i requisiti richiesti siano soddisfatti.

## Per Exchange Online
L'accesso condizionale a Exchange Online supporta i dispositivi che eseguono:

-   Windows 8.1 e versioni successive (se registrato con Intune)

-   Windows 7.0 o versione successiva (se aggiunto a un dominio)

-   Windows Phone 8.1 e versioni successive

-   iOS 7.1 e versioni successive

-   Android 4.0 e versioni successive, Samsung Knox Standard 4.0 e versioni successive

I dispositivi devono anche essere registrati con il servizio Registrazione dispositivo Azure Active Directory.

Il servizio AAD DRS verrà attivato automaticamente per i clienti di Intune e Office 365. I clienti che hanno già distribuito il servizio di registrazione dei dispositivi di ADFS non visualizzeranno i dispositivi registrati in Active Directory locale.

-   È necessario usare una sottoscrizione a Office 365 che include Exchange Online (ad esempio E3) e gli utenti devono avere una licenza per Exchange Online.

-   L'opzione facoltativa **Microsoft Intune Service to Service Connector** connette Intune a Microsoft Exchange Online e consente di gestire le informazioni sui dispositivi tramite la console di Intune. Vedere [Gestione dei dispositivi mobili con Exchange ActiveSync e Microsoft Intune](/intune/deploy-use/mobile-device-management-with-exchange-activesync-and-microsoft-intune). Non è necessario usare il connettore per i criteri di conformità o i criteri di accesso condizionale, ma è obbligatorio eseguire i report per valutare l'impatto dell'accesso condizionale.

    Se si configura il connettore, alcuni criteri di Exchange ActiveSync di Intune potrebbero essere visualizzati nella console di Office ma non vengono impostati come criteri predefiniti e non interessano i dispositivi.

    > [!IMPORTANT]
    > Non configurare Service to Service Connector se si prevede di usare l'accesso condizionale sia per Exchange Online che per Exchange locale.

    È ora possibile scoprire come [distribuire Exchange Online con Intune](conditional-access-intune-exchange-online.md).

## Per Exchange Server locale
L'accesso condizionale a Exchange locale supporta:

-   Windows 8 e versioni successive (se registrato con Intune)

-   Windows Phone 8 e versioni successive

-   Dispositivi iOS che usano i client di posta elettronica di Exchange ActiveSync (EAS)

-   Android 4 e versioni successive

Inoltre:

-   La versione di Exchange deve essere Exchange 2010 o successiva. È supportata la configurazione del server Accesso client di Exchange Server.

    > [!TIP]
    > Se l'ambiente di Exchange si trova in una configurazione con server Accesso client, è necessario configurare Exchange Connector locale in modo che punti a uno dei server Accesso client.

-   È possibile configurare Exchange ActiveSync per l'autenticazione basata su certificati o l'immissione di credenziali utente.

-   È necessario usare **On-Premises Exchange Connector** che connette Intune a Microsoft Exchange Server locale. Ciò consente di gestire i dispositivi tramite la console di Intune. Vedere [Gestione dei dispositivi mobili con Exchange ActiveSync e Microsoft Intune](/intune/deploy-use/mobile-device-management-with-exchange-activesync-and-microsoft-intune).

  > [!IMPORTANT]
> Accertarsi di usare la versione più recente di Exchange Connector locale. Exchange Connector locale, disponibile nella console di Intune, è specifico del tenant di Intune e non può essere usato con un altro tenant. È inoltre necessario assicurarsi che Exchange Connector per il tenant sia installato in un solo computer.

  È ora possibile scoprire come [distribuire Exchange Server locale con Intune](conditional-access-intune-exchange.md).


<!--HONumber=Apr16_HO4-->


