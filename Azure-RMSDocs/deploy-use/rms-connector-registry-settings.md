---
title: Impostazioni del Registro di sistema per il connettore di Rights Management - AIP
description: "Informazioni sulle impostazioni del Registro di sistema sui server tramite il connettore RMS. Il metodo consigliato per configurare tali impostazioni è usare lo strumento di configurazione server per il connettore Microsoft RMS."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/23/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: ed3e9a3d-0f7c-4abc-9d0b-aa3b18403d39
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: b894be1ef3d41a9faf6c3fd3b3fd8c5b94a62517
ms.sourcegitcommit: 04eb4990e2bf0004684221592cb93df35e6acebe
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/30/2017
---
# <a name="registry-setting-for-the-rights-management-connector"></a>Impostazioni del Registro di sistema per il connettore Rights Management

>*Si applica a: Azure Information Protection, Office 365*


Usare le tabelle riportate nelle sezioni seguenti solo se si vuole controllare o aggiungere manualmente impostazioni del Registro di sistema sui server che eseguono Exchange, SharePoint o Windows Server, operazioni che consentono di configurare questi ultimi per l'uso del [connettore RMS](deploy-rms-connector.md). Il metodo consigliato per configurare i server è usare lo strumento di configurazione server per il connettore Microsoft RMS.

Istruzioni per l'uso delle impostazioni:

-   *MicrosoftRMSURL* è l'URL del servizio Microsoft RMS dell'organizzazione. Per individuare questo valore:

    1.  Eseguire il cmdlet [Get-AadrmConfiguration](http://msdn.microsoft.com/library/windowsazure/dn629410.aspx) per Azure RMS. Se non è stato ancora installato il modulo di Windows PowerShell per Azure RMS, vedere [Installazione di Windows PowerShell per Azure Rights Management](install-powershell.md).

    2.  Nell'output identificare il valore **LicensingIntranetDistributionPointUrl** .

        Ad esempio, **LicensingIntranetDistributionPointUrl   : https://5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com/_wmcs/licensing**

    3.  In questo valore rimuovere **/_wmcs/licensing** dalla stringa. La stringa rimanente è l'URL di Microsoft RMS. Nell'esempio, l'URL di Microsoft RMS è il seguente:

        **https://5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com**

-   *ConnectorFQDN* è il nome di bilanciamento del carico definito in DNS per il connettore. ad esempio **rmsconnector.contoso.com**.

-   Usare il prefisso HTTPS per l'URL del connettore se quest'ultimo è stato configurato per comunicare con i server locali mediante tale protocollo. Per altre informazioni, vedere la sezione [Configurazione del connettore RMS per l'uso di HTTPS](install-configure-rms-connector.md#configuring-the-rms-connector-to-use-https) nelle istruzioni principali. Gli URL di Microsoft RMS usano sempre HTTPS.


## <a name="exchange-2016-or-exchange-2013-registry-settings"></a>Impostazioni del Registro di sistema per Exchange 2016 o Exchange 2013

**Percorso del Registro di sistema:** HKEY_LOCAL_MACHINE\Software\Microsoft\MSDRM\ServiceLocation\Activation

**Tipo:** Reg_SZ

**Valore:** predefinito

**Dati:** https://*MicrosoftRMSURL*/_wmcs/certification

---

**Percorso del Registro di sistema:** HKEY_LOCAL_MACHINE\Software\Microsoft\MSDRM\ServiceLocation\EnterprisePublishing

**Tipo:** Reg_SZ

**Valore:** predefinito

**Dati:** https://*MicrosoftRMSURL*/_wmcs/Licensing

---

**Percorso del Registro di sistema:** HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ExchangeServer\v15\IRM\CertificationServerRedirection

**Tipo:** Reg_SZ

**Valore:** https://*MicrosoftRMSURL*


**Dati:** uno dei seguenti, in base all'uso del protocollo HTTP o HTTPS per le comunicazioni dal server di Exchange al connettore RMS:

- http://*ConnectorFQDN*

- https://*ConnectorFQDN*

---

**Percorso del Registro di sistema:** HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ExchangeServer\v15\IRM\LicenseServerRedirection

**Tipo:** Reg_SZ

**Valore:** https://*MicrosoftRMSURL*


**Dati:** uno dei seguenti, in base all'uso del protocollo HTTP o HTTPS per le comunicazioni dal server di Exchange al connettore RMS:

- http://*ConnectorFQDN*

- https://*ConnectorFQDN*


## <a name="exchange-2010-registry-settings"></a>Impostazioni del Registro di sistema per Exchange 2010

**Percorso del Registro di sistema:** HKEY_LOCAL_MACHINE\Software\Microsoft\MSDRM\ServiceLocation\Activation

**Tipo:** Reg_SZ

**Valore:** predefinito

**Dati:** https://*MicrosoftRMSURL*/_wmcs/certification

---

**Percorso del Registro di sistema:** HKEY_LOCAL_MACHINE\Software\Microsoft\MSDRM\ServiceLocation\EnterprisePublishing

**Tipo:** Reg_SZ

**Valore:** predefinito

**Dati:** https://*MicrosoftRMSURL*/_wmcs/Licensing

---

**Percorso del Registro di sistema:** HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ExchangeServer\v14\IRM\CertificationServerRedirection

**Tipo:** Reg_SZ

**Valore:** https://*MicrosoftRMSURL*

**Dati:** uno dei seguenti, in base all'uso del protocollo HTTP o HTTPS per le comunicazioni dal server di Exchange al connettore RMS:

- http://*ConnectorFQDN*

- https://*ConnectorFQDN*

---

**Percorso del Registro di sistema:** HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ExchangeServer\v14\IRM\LicenseServerRedirection

**Tipo:** Reg_SZ

**Valore:** https://*MicrosoftRMSURL*

**Dati:** uno dei seguenti, in base all'uso del protocollo HTTP o HTTPS per le comunicazioni dal server di Exchange al connettore RMS:

- http://*ConnectorFQDN*

- https://*ConnectorFQDN*


## <a name="sharepoint-2016-or-sharepoint-2013-registry-settings"></a>Impostazioni del Registro di sistema di SharePoint 2016 o SharePoint 2013

**Percorso del Registro di sistema:** HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSIPC\ServiceLocation\LicensingRedirection

**Tipo:** Reg_SZ

**Valore:** https://*MicrosoftRMSURL*/_wmcs/licensing


**Dati:** uno dei seguenti, in base all'uso del protocollo HTTP o HTTPS per le comunicazioni dal server di SharePoint al connettore RMS:

- http://*ConnectorFQDN*/_wmcs/licensing

- https://*ConnectorFQDN*/_wmcs/licensing

---

**Percorso del Registro di sistema:** HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSIPC\ServiceLocation\EnterpriseCertification

**Tipo:** Reg_SZ

**Valore:** predefinito

**Dati:** uno dei seguenti, in base all'uso del protocollo HTTP o HTTPS per le comunicazioni dal server di SharePoint al connettore RMS:

- http://*ConnectorFQDN*/_wmcs/certification

- https://*ConnectorFQDN*/_wmcs/certification

---

**Percorso del Registro di sistema:** HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSIPC\ServiceLocation\EnterprisePublishing

**Tipo:** Reg_SZ

**Valore:** predefinito


**Dati:** uno dei seguenti, in base all'uso del protocollo HTTP o HTTPS per le comunicazioni dal server di SharePoint al connettore RMS:

- http://*ConnectorFQDN*/_wmcs/licensing

- https://*ConnectorFQDN*/_wmcs/licensing




## <a name="file-server-and-file-classification-infrastructure-registry-settings"></a>Impostazioni del Registro di sistema per i file server e la funzionalità Infrastruttura di classificazione file

**Percorso del Registro di sistema:** HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSDRM\ServiceLocation\EnterprisePublishing

**Tipo:** Reg_SZ

**Valore:** predefinito

**Dati:** http://*ConnectorFQDN*/_wmcs/licensing

---

**Percorso del Registro di sistema:** HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSDRM\ServiceLocation\Activation

**Tipo:** Reg_SZ

**Valore:** predefinito

**Dati:** http://*ConnectorFQDN*/_wmcs/certification


Tornare a [Distribuzione del connettore di Azure Rights Management](deploy-rms-connector.md)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]