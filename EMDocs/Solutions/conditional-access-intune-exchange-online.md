---
# required metadata

title: Usare l'accesso condizionale con Microsoft Intune ed Exchange Online
description:
keywords:
author: craigcaseyMSFT
manager: swadhwa
ms.date: 04/28/2016
ms.topic: article
ms.prod:
ms.service:
ms.technology:
ms.assetid: 8cfe421b-52c9-4d44-8df1-15c82375c335

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: 
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Distribuire Exchange Online con Intune

Ora che si sono lette con attenzione le [indicazioni sull'architettura per la protezione di documenti e messaggi di posta elettronica aziendali](architecture-guidance-for-protecting-company-email-and-documents.md) è possibile procedere alla distribuzione di una soluzione.

Per consentire a Intune di gestire i dispositivi mobili, gli utenti devono registrare i dispositivi in Intune.

## Passaggi per la distribuzione
Per distribuire la soluzione Exchange Online con Intune, seguire questi passaggi:

### Passaggio 1: Creare criteri di conformità e distribuirli agli utenti.
I criteri di conformità definiscono le regole e le impostazioni che un dispositivo deve soddisfare per essere considerato conforme ai criteri di accesso condizionale. Seguire i passaggi in [Create a device compliance policy in Microsoft Intune](/intune/deployuse/create-a-device-compliance-policy-in-microsoft-intune) (Creare criteri di conformità in Microsoft Intune) per creare e distribuire criteri di conformità.

Se si vuole avere la possibilità di rimuovere tutti i messaggi di posta elettronica aziendale da un dispositivo iOS quando non fa più parte dell'azienda, è necessario creare e distribuire un profilo di posta elettronica e quindi impostare i criteri di conformità che specificano che i profili di posta elettronica sono gestiti da Intune. È necessario distribuire il profilo di posta elettronica allo stesso set di utenti a cui sono destinati questi criteri di conformità.

![Screenshot che illustra la pagina "Regole" della Creazione guidata criteri di conformità in cui è possibile specificare che un profilo di posta elettronica deve essere gestito da Intune.](./media/ProtectEmail/Hybrid-Onprem-ExchSrvr-Wizard6.PNG)

Se si specificano questi criteri di conformità, un utente che ha già configurato il proprio account di posta elettronica dovrà rimuoverlo manualmente. Intune quindi lo aggiungerà nuovamente attraverso il processo di registrazione descritto in [Esperienza utente finale di accesso condizionale](end-user-experience-conditional-access.md).

> [!IMPORTANT]
> Se non sono stati distribuiti i criteri di conformità e abilitati i criteri di accesso condizionale di Exchange, a tutti i dispositivi di destinazione verrà consentito l’accesso.

### Passaggio 2: Valutare l'effetto dei criteri di accesso condizionale
Se è stata configurata una connessione tra Intune ed Exchange usando [Microsoft Intune Service to Service Connector](/intune/deployuse/intune-service-to-service-exchange-connector), è possibile usare i **report inventario dispositivi mobili** per identificare i client di posta EAS il cui accesso a Exchange sarà bloccato dopo la configurazione dei criteri di accesso condizionale.

Seguire le istruzioni in [Valutare l'effetto dei criteri di accesso condizionale](/intune/deployuse/restrict-access-to-exchange-online-with-microsoft-intune#configure-conditional-access) per identificare gli utenti interessati dai criteri di accesso condizionale.

### Passaggio 3: Configurare i gruppi utenti per i criteri di accesso condizionale
I criteri di accesso condizionale sono destinati a diversi gruppi di utenti in base ai tipi di criteri. Questi gruppi contengono gli utenti a cui saranno destinati i criteri o che ne saranno esenti. Quando a un utente viene destinato un criterio, ogni dispositivo in uso deve essere conforme per accedere alla posta elettronica.

Per altre informazioni, vedere [Configurare i gruppi utenti per i criteri di accesso condizionale](/intune/deployuse/restrict-access-to-exchange-online-with-microsoft-intune#configure-conditional-access).

### Passaggio 4: Configurare i criteri di accesso condizionale.
Il flusso seguente viene usato dai criteri di accesso condizionale per fare in modo che Exchange Online valuti se consentire o bloccare i dispositivi.

![Diagramma di flusso che illustra come i criteri di accesso condizionale per Exchange Online valutano se consentire o bloccare i dispositivi.](./media/ProtectEmail/conditional-access-8-1.png)

Per configurare i criteri di accesso condizionale, seguire le indicazioni in [Configurare i criteri di accesso condizionale](/intune/deployuse/restrict-access-to-exchange-online-with-microsoft-intune#configure-conditional-access).



## Reporting

### Monitorare i criteri di conformità e di accesso condizionale
Per visualizzare i dispositivi bloccati da Exchange:

Nel dashboard di Intune fare clic sul riquadro **Dispositivi bloccati da Exchange** per visualizzare il numero di dispositivi bloccati e i collegamenti ad altre informazioni.
![Screenshot che illustra il riquadro "Dispositivi bloccati da Exchange" nel dashboard di Intune](./media/ProtectEmail/intune-sa-6blocked-devices.PNG)



## Come proseguire
Dopo aver distribuito una soluzione per la protezione della posta elettronica aziendale e dei dati di questa all'interno dei dispositivi mobili, è possibile scoprire di più sull'[esperienza dell'utente finale relativa all'accesso condizionale](end-user-experience-conditional-access.md). Ciò consente di prepararsi ad affrontare i problemi che potrebbero verificarsi quando gli utenti finali registrano dispositivi specifici.


<!--HONumber=Apr16_HO4-->


