---
# required metadata

title: Usare l'accesso condizionale con Intune e Configuration Manager
description:
keywords:
author: craigcaseyMSFT
manager: swadhwa
ms.date: 04/28/2016
ms.topic: article
ms.prod:
ms.service:
ms.technology:
ms.assetid: e65a0662-33ff-4e8c-9305-a21e80ea0f69

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: 
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Usare l'accesso condizionale con Intune e Configuration Manager
Questo argomento presume che System Center Configuration Manager e Microsoft Exchange Server (locale, con Exchange Online o con una distribuzione ibrida di entrambi) siano già in uso all'interno dell'azienda per la gestione dell'accesso alla posta elettronica. Questa soluzione combina l'ambiente di Configuration Manager esistente con Intune per gestire in modo sicuro l'accesso alla posta elettronica in tutti i tipi di dispositivi, indipendentemente dalla loro posizione.

> [!TIP]
> È possibile scaricare una copia di questo argomento nella [Raccolta TechNet](https://gallery.technet.microsoft.com/Deploying-Enterprise-16499404).

## Prima di iniziare
Prima di iniziare a usare l'accesso condizionale, verificare che i requisiti richiesti siano soddisfatti:

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

Se l'ambiente include sia Exchange Online che Exchange locale, è possibile leggere l'articolo sulla [distribuzione di Exchange Online ed Exchange locale con Microsoft Intune e Configuration Manager](conditional-access-intune-configmgr-coexist.md).


<!--HONumber=Apr16_HO4-->


