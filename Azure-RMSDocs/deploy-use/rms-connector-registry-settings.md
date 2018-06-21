---
title: Impostazioni del Registro di sistema per il connettore di Rights Management - AIP
description: Informazioni sulle impostazioni del Registro di sistema sui server tramite il connettore RMS. Il metodo consigliato per configurare tali impostazioni è usare lo strumento di configurazione server per il connettore Microsoft RMS.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 05/16/2018
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: ed3e9a3d-0f7c-4abc-9d0b-aa3b18403d39
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 9334a781378ffdbe76dd9fe9d78f5db5913766d1
ms.sourcegitcommit: 373e05ff0c411d29cc5b61c36edaf5a203becc14
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/17/2018
ms.locfileid: "34216835"
---
# <a name="registry-setting-for-the-rights-management-connector"></a>Impostazioni del Registro di sistema per il connettore Rights Management

>*Si applica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2*


Usare le tabelle riportate nelle sezioni seguenti solo se si desidera controllare o aggiungere manualmente impostazioni del Registro di sistema sui server che eseguono Exchange, SharePoint o Windows Server. Queste impostazioni del Registro di sistema configurano i server per usare il [connettore RMS](deploy-rms-connector.md). Il metodo consigliato per configurare i server è usare lo strumento di configurazione server per il connettore Microsoft RMS.

Istruzioni per l'uso delle impostazioni:

-   *\<YourTenantURL>* corrisponde all'URL del servizio Azure Rights Management per il tenant di Azure Information Protection. Per individuare questo valore:

    1.  Eseguire il cmdlet [Get-AadrmConfiguration](http://msdn.microsoft.com/library/windowsazure/dn629410.aspx) per il servizio di Azure Rights Management. Se non è stato ancora installato il modulo Windows PowerShell per Azure RMS, vedere [Installazione di Windows PowerShell per Microsoft Azure Rights Management](install-powershell.md).

    2.  Nell'output identificare il valore **LicensingIntranetDistributionPointUrl** .

        Ad esempio: **LicensingIntranetDistributionPointUrl: https://5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com/_wmcs/licensing**

    3.  In questo valore rimuovere **/_wmcs/licensing** dalla stringa. La stringa rimanente corrisponde all'URL del servizio Azure Rights Management. Nell'esempio, l'URL del servizio Azure Rights Management è il valore seguente:

        **https://5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com**
        
        È possibile verificare di avere il valore corretto eseguendo il comando PowerShell seguente:
        
            (Get-AadrmConfiguration).LicensingIntranetDistributionPointUrl -match "https:\/\/[0-9A-Za-z\.-]*" | Out-Null; $matches[0]

-   *\<ConnectorFQDN* è il nome di bilanciamento del carico definito in DNS per il connettore. ad esempio **rmsconnector.contoso.com**.

-   Usare il prefisso HTTPS per l'URL del connettore se quest'ultimo è stato configurato per comunicare con i server locali mediante tale protocollo. Per altre informazioni, vedere la sezione [Configurazione del connettore RMS per l'uso di HTTPS](install-configure-rms-connector.md#configuring-the-rms-connector-to-use-https) nelle istruzioni principali. L'URL del servizio Azure Rights Management usa sempre il protocollo HTTPS.


## <a name="exchange-2016-or-exchange-2013-registry-settings"></a>Impostazioni del Registro di sistema per Exchange 2016 o Exchange 2013

**Percorso del Registro di sistema:** HKEY_LOCAL_MACHINE\Software\Microsoft\MSDRM\ServiceLocation\Activation

**Tipo:** Reg_SZ

**Valore:** predefinito

**Dati:** https://*\<YourTenantURL>*/_wmcs/certification

---

**Percorso del Registro di sistema:** HKEY_LOCAL_MACHINE\Software\Microsoft\MSDRM\ServiceLocation\EnterprisePublishing

**Tipo:** Reg_SZ

**Valore:** predefinito

**Data:** https://*\<YourTenantURL>*/_wmcs/Licensing

---

**Percorso del Registro di sistema:** HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ExchangeServer\v15\IRM\CertificationServerRedirection

**Tipo:** Reg_SZ

**Valore:** https://*\<YourTenantURL>*


**Dati:** uno dei seguenti, in base all'uso del protocollo HTTP o HTTPS per le comunicazioni dal server di Exchange al connettore RMS:

- http://*<\ConnectorFQDN>*

- https://*<\ConnectorFQDN>*

---

**Percorso del Registro di sistema:** HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ExchangeServer\v15\IRM\LicenseServerRedirection

**Tipo:** Reg_SZ

**Valore:** https://*<\YourTenantURL>*


**Dati:** uno dei seguenti, in base all'uso del protocollo HTTP o HTTPS per le comunicazioni dal server di Exchange al connettore RMS:

- http://*<\ConnectorFQDN>*

- https://*<\ConnectorFQDN>*


## <a name="exchange-2010-registry-settings"></a>Impostazioni del Registro di sistema per Exchange 2010

**Percorso del Registro di sistema:** HKEY_LOCAL_MACHINE\Software\Microsoft\MSDRM\ServiceLocation\Activation

**Tipo:** Reg_SZ

**Valore:** predefinito

**Dati:** https://*<\YourTenantURL>*/_wmcs/certification

---

**Percorso del Registro di sistema:** HKEY_LOCAL_MACHINE\Software\Microsoft\MSDRM\ServiceLocation\EnterprisePublishing

**Tipo:** Reg_SZ

**Valore:** predefinito

**Dati:** https://*<\YourTenantURL>*/_wmcs/Licensing

---

**Percorso del Registro di sistema:** HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ExchangeServer\v14\IRM\CertificationServerRedirection

**Tipo:** Reg_SZ

**Valore:** https://*<\YourTenantURL>*

**Dati:** uno dei seguenti, in base all'uso del protocollo HTTP o HTTPS per le comunicazioni dal server di Exchange al connettore RMS:

- http://*<\ConnectorFQDN>*

- https://*<\ConnectorFQDN>*

---

**Percorso del Registro di sistema:** HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ExchangeServer\v14\IRM\LicenseServerRedirection

**Tipo:** Reg_SZ

**Valore:** https://*<\YourTenantURL>*

**Dati:** uno dei seguenti, in base all'uso del protocollo HTTP o HTTPS per le comunicazioni dal server di Exchange al connettore RMS:

- http://*<\ConnectorFQDN>*

- https://*<\ConnectorFQDN>*


## <a name="sharepoint-2016-or-sharepoint-2013-registry-settings"></a>Impostazioni del Registro di sistema di SharePoint 2016 o SharePoint 2013

**Percorso del Registro di sistema:** HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSIPC\ServiceLocation\LicensingRedirection

**Tipo:** Reg_SZ

**Valore:** https://*<\YourTenantURL>*/_wmcs/licensing


**Dati:** uno dei seguenti, in base all'uso del protocollo HTTP o HTTPS per le comunicazioni dal server di SharePoint al connettore RMS:

- http://*<\ConnectorFQDN>*/_wmcs/licensing

- https://*<\ConnectorFQDN>*/_wmcs/licensing

---

**Percorso del Registro di sistema:** HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSIPC\ServiceLocation\EnterpriseCertification

**Tipo:** Reg_SZ

**Valore:** predefinito

**Dati:** uno dei seguenti, in base all'uso del protocollo HTTP o HTTPS per le comunicazioni dal server di SharePoint al connettore RMS:

- http://*<\ConnectorFQDN>*/_wmcs/certification

- https://*<\ConnectorFQDN>*/_wmcs/certification

---

**Percorso del Registro di sistema:** HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSIPC\ServiceLocation\EnterprisePublishing

**Tipo:** Reg_SZ

**Valore:** predefinito


**Dati:** uno dei seguenti, in base all'uso del protocollo HTTP o HTTPS per le comunicazioni dal server di SharePoint al connettore RMS:

- http://*<\ConnectorFQDN>*/_wmcs/licensing

- https://*<\ConnectorFQDN>*/_wmcs/licensing




## <a name="file-server-and-file-classification-infrastructure-registry-settings"></a>Impostazioni del Registro di sistema per i file server e la funzionalità Infrastruttura di classificazione file

**Percorso del Registro di sistema:** HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSDRM\ServiceLocation\EnterprisePublishing

**Tipo:** Reg_SZ

**Valore:** predefinito

**Dati:** http://*<\ConnectorFQDN>*/_wmcs/licensing

---

**Percorso del Registro di sistema:** HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSDRM\ServiceLocation\Activation

**Tipo:** Reg_SZ

**Valore:** predefinito

**Dati:** http://*<\ConnectorFQDN>*/_wmcs/certification


Tornare a [Distribuzione del connettore di Azure Rights Management](deploy-rms-connector.md)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]