---
title: Estensione per dispositivi mobili Active Directory Rights Management Services per AIP
description: Informazioni sulle estensioni per dispositivi mobili Active Directory per AIP
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 04/28/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 6dc8a5aa43b6f5d3dc53c014dd770fa87ff683a5
ms.sourcegitcommit: 8499602fba94fbfa28d7682da2027eeed6583c61
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/21/2020
ms.locfileid: "83746365"
---
# <a name="active-directory-rights-management-services-mobile-device-extension"></a>Estensione di Active Directory Rights Management Services per dispositivi mobili

 
Si applica a: Windows Server 2019, 2016, 2012 R2 e 2012

È possibile scaricare l'estensione Active Directory Rights Management Services (AD RMS) Mobile Device dall' [area download Microsoft](https://www.microsoft.com/download/details.aspx?id=43738) e installare questa estensione in una distribuzione di ad RMS esistente. In questo modo gli utenti possono proteggere e utilizzare dati sensibili quando il dispositivo supporta le più recenti app abilitate per l'API. Ad esempio, gli utenti possono eseguire le operazioni seguenti:
- Usare l'app Azure Information Protection per utilizzare file di testo protetti in formati diversi, ad esempio con estensione txt, CSV e XML.
- Usare l'app Azure Information Protection per utilizzare file di immagine protetti, inclusi i file con estensione jpg, gif e TIF.
- Usare l'app Azure Information Protection per aprire i file che sono stati protetti in modo generico (formato Pfile).
- Usare l'app Azure Information Protection per aprire un file di Office (Word, Excel, PowerPoint) che è una copia PDF (formato PDF e Ppdf).
- Usare l'app Azure Information Protection per aprire i messaggi di posta elettronica protetti (con estensione rpmsg) e i file PDF protetti in Microsoft SharePoint.
- Usare un visualizzatore PDF con supporto per AIP per la visualizzazione multipiattaforma o per aprire file PDF protetti con qualsiasi applicazione abilitata per AIP.
- Usare le app abilitate per AIP sviluppate internamente, scritte con l' [SDK MIP](https://aka.ms/mipsdkdocs).

> [!NOTE]
> È possibile scaricare l'app Azure Information Protection dalla pagina [microsoft Rights Management](https://go.microsoft.com/fwlink/?linkid=303970) del sito Web Microsoft. Per informazioni sulle altre app supportate con l'estensione per dispositivi mobili, vedere la tabella nella pagina [applicazioni](https://docs.microsoft.com/azure/information-protection/requirements-applications) da questa documentazione. Per ulteriori informazioni sui diversi tipi di file supportati da RMS, vedere la sezione tipi di file [e estensioni di file supportati](https://docs.microsoft.com/rights-management/rms-client/sharing-app-admin-guide-technical%23supported-file-types-and-file-name-extensions) nella Guida dell'amministratore dell'applicazione di condivisione Rights Management.

> [!IMPORTANT]
> Assicurarsi di leggere e configurare i prerequisiti prima di installare l'estensione per dispositivi mobili.

Per ulteriori informazioni, scaricare il white paper "Microsoft Azure Information Protection" e gli script allegati dall' [area download Microsoft](https://www.microsoft.com/download/details.aspx?id=40333).

## <a name="prerequisites-for-ad-rms-mobile-device-extension"></a>Prerequisiti per AD RMS estensione per dispositivi mobili

Prima di installare l'estensione AD RMS dispositivo mobile, verificare che siano presenti le dipendenze seguenti.


|Requisito|Ulteriori informazioni|
|---------------|------------------------|
|Una distribuzione di AD RMS esistente in Windows Server 2019, 2016, 2012 R2 o 2012, che include quanto segue:<br /><br /> -Il cluster di AD RMS deve essere accessibile da Internet. <br /><br /> -AD RMS necessario utilizzare un database completo basato su Microsoft SQL Server in un server separato e non il database interno di Windows utilizzato spesso per i test sullo stesso server. <br /><br />-L'account che verrà utilizzato per installare l'estensione per dispositivi mobili deve disporre dei diritti di amministratore di sistema per l'istanza di SQL Server utilizzata per AD RMS. <br /><br />-I server AD RMS devono essere configurati per l'uso di SSL/TLS con un certificato x. 509 valido considerato attendibile dai client dei dispositivi mobili.<br /><br /> -Se i server di AD RMS si trovano dietro un firewall o pubblicati usando un proxy inverso, oltre alla pubblicazione della cartella **/_wmcs** su Internet, è necessario pubblicare anche la cartella/problema (ad esempio: **_https: \/ \/ RMSserver.contoso.com/My**).|Per informazioni dettagliate sui prerequisiti AD RMS e le informazioni sulla distribuzione, vedere la sezione Prerequisiti di questo articolo.|
|AD FS distribuita in Windows Server:<br /><br /> -Il AD FS server farm deve essere accessibile da Internet (sono stati distribuiti i proxy server federativi). <br /><br />-L'autenticazione basata su form non è supportata. è necessario usare l'autenticazione integrata di Windows <br /><br /> **Importante**: ad FS necessario eseguire un computer diverso dal computer che esegue ad RMS e dall'estensione del dispositivo mobile.|Per la documentazione relativa AD FS, vedere la [Guida alla distribuzione di Windows server ad FS](https://docs.microsoft.com/office365/troubleshoot/active-directory/set-up-adfs-for-single-sign-on) nella libreria di Windows Server.<br /><br /> ADFS deve essere configurato per l'estensione per dispositivi mobili. Per istruzioni, vedere la sezione **Configuring ad FS for the ad RMS Mobile Device Extension** in questo argomento.|
|I dispositivi mobili devono considerare attendibili i certificati PKI nel server o nei server RMS|Quando si acquistano i certificati del server da una CA pubblica, ad esempio VeriSign o comodo, è probabile che i dispositivi mobili considerino già attendibile la CA radice per questi certificati, in modo che questi dispositivi considerino attendibili i certificati del server senza ulteriori configurazioni.<br /><br /> Tuttavia, se si usa la CA interna per distribuire i certificati server per RMS, è necessario eseguire passaggi aggiuntivi per installare il certificato CA radice nei dispositivi mobili. In caso contrario, i dispositivi mobili non saranno in grado di stabilire una connessione con il server RMS.|
|Record SRV in DNS|Creare uno o più record SRV nel dominio o nei domini aziendali:<br /><br />1: creare un record per ogni suffisso di dominio di posta elettronica che gli utenti useranno <br /><br />2: creare un record per ogni FQDN usato dai cluster RMS per proteggere il contenuto, escluso il nome del cluster <br /><br />Questi record devono essere risolvibili da qualsiasi rete utilizzata dai dispositivi mobili che si connettono, che include la Intranet se i dispositivi mobili si connettono tramite Intranet.<br /><br /> Quando gli utenti forniscono il proprio indirizzo di posta elettronica dal dispositivo mobile, il suffisso di dominio viene usato per identificare se usare un'infrastruttura AD RMS o Azure AIP. Quando il record SRV viene trovato, i client vengono reindirizzati al server AD RMS che risponde a tale URL.<br /><br /> Quando gli utenti usano contenuti protetti con un dispositivo mobile, l'applicazione client cerca in DNS un record che corrisponda al nome di dominio completo nell'URL del cluster che ha protetto il contenuto, senza il nome del cluster. Il dispositivo viene quindi indirizzato al cluster AD RMS specificato nel record DNS e acquisisce una licenza per aprire il contenuto. Nella maggior parte dei casi, il cluster RMS sarà lo stesso che ha protetto il contenuto.<br /><br /> Per informazioni su come specificare i record SRV, vedere la sezione **specifica dei record DNS SRV per l'estensione ad RMS Mobile Device** in questo argomento.|
|Client supportati che usano applicazioni sviluppate con l'SDK MIP per questa piattaforma. |Scaricare le app supportate per i dispositivi usati usando i collegamenti disponibili nella pagina di download [Microsoft Azure Information Protection](https://www.microsoft.com/download/details.aspx?id=40333) .|

### <a name="configuring-ad-fs-for-the-ad-rms-mobile-device-extension"></a>Configurare ADFS per l'estensione AD RMS per dispositivi mobili

È necessario innanzitutto configurare AD FS e quindi autorizzare l'app AIP per i dispositivi che si vuole usare.

#### <a name="step-1-to-configure-ad-fs"></a>Passaggio 1: configurare AD FS

- È possibile eseguire uno script di Windows PowerShell per configurare automaticamente ADFS in modo da supportare l'estensione AD RMS per dispositivi mobili oppure specificare manualmente le opzioni e i valori di configurazione:
    - Per configurare automaticamente AD FS per l'estensione del dispositivo mobile AD RMS, copiare e incollare il codice seguente in un file di script di Windows PowerShell, quindi eseguirlo:

```powershell
# This Script Configures the Microsoft Rights Management Mobile Device Extension and Claims used in the ADFS Server

# Check if Microsoft Rights Management Mobile Device Extension is configured on the Server
$CheckifConfigured = Get-AdfsRelyingPartyTrust -Identifier "api.rms.rest.com"
if ($CheckifConfigured)
{
Write-Host "api.rms.rest.com Identifer used for Microsoft Rights Management Mobile Device Extension is already configured on this Server"
Write-Host $CheckifConfigured
}
else
{
Write-Host "Configuring  Microsoft Rights Management Mobile Device Extension "

# TransformaRules used by Microsoft Rights Management Mobile Device Extension
# Claims: E-mail, UPN and ProxyAddresses
$TransformRules = @"
@RuleTemplate = "LdapClaims"
@RuleName = "Jwt Token"
c:[Type ==
"https://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname",
Issuer == "AD AUTHORITY"]
 => issue(store = "Active Directory", types =
("http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress",
"http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn",
"http://schemas.xmlsoap.org/claims/ProxyAddresses"), query =
";mail,userPrincipalName,proxyAddresses;{0}", param = c.Value);

@RuleTemplate = "PassThroughClaims"
@RuleName = "JWT pass through"
c:[Type == "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress"]
 => issue(claim = c);

@RuleTemplate = "PassThroughClaims"
@RuleName = "JWT pass through"
c:[Type == "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn"]
 => issue(claim = c);

@RuleTemplate = "PassThroughClaims"
@RuleName = "JWT pass through Proxy addresses"
c:[Type == "http://schemas.xmlsoap.org/claims/ProxyAddresses"]
 => issue(claim = c);
"@

# AuthorizationRules used by Microsoft Rights Management Mobile Device Extension
# Allow All users
$AuthorizationRules = @"
@RuleTemplate = "AllowAllAuthzRule"
 => issue(Type = "https://schemas.microsoft.com/authorization/claims/permit",
Value = "true");
"@

# Add a Relying Part Truest with Name -"Microsoft Rights Management Mobile Device Extension" Identifier "api.rms.rest.com"
Add-ADFSRelyingPartyTrust -Name "Microsoft Rights Management Mobile Device Extension" -Identifier "api.rms.rest.com" -IssuanceTransformRules $TransformRules -IssuanceAuthorizationRules  $AuthorizationRules

Write-Host "Microsoft Rights Management Mobile Device Extension Configured"
}
```

- Per configurare manualmente AD FS per l'estensione del dispositivo mobile AD RMS, usare le impostazioni seguenti:

|**Configuration**|**Valore**|
|-----|-----|
|**Attendibilità componente**|_api. RMS. Rest. com|
|**Regola di attestazione**|**Archivio attributi**: Active Directory <br /><br />**Indirizzi di posta elettronica**: indirizzo di posta elettronica<br /><br>**Nome-entità utente**: UPN<br /><br /> **Indirizzo proxy**: _https: \/ \/ schemas.xmlsoap.org/claims/proxyAddresses|

> [!TIP]
> Per istruzioni dettagliate per una distribuzione di esempio di AD RMS con AD FS, vedere [distribuzione di Active Directory Rights Management Services con Active Directory Federation Services](https://docs.microsoft.com/office365/troubleshoot/active-directory/set-up-adfs-for-single-sign-on).

#### <a name="step-2-authorize-apps-for-your-devices"></a>Passaggio 2: autorizzare le app per i dispositivi

1. Eseguire il comando di Windows PowerShell seguente dopo aver sostituito le variabili per aggiungere il supporto per l'app Azure Information Protection:


```powershell
Add-AdfsClient -Name "R<your application name> " -ClientId "<YOUR CLIENT ID >" -RedirectUri @("<YOUR REDIRECT URI >")
```

**Esempio di PowerShell**
```powershell
Add-AdfsClient -Name "Fabrikam application for MIP" -ClientId "96731E97-2204-4D74-BEA5-75DCA53566C3" -RedirectUri @("com.fabrikam.MIPAPP://authorize")
```

### <a name="specifying-the-dns-srv-records-for-the-ad-rms-mobile-device-extension"></a>Specificare il record DNS SRV per l'estensione AD RMS per dispositivi mobili

È necessario creare record DNS SRV per ogni dominio di posta elettronica che si vuole venga usato dagli utenti. Se tutti gli utenti usano domini figlio di un singolo dominio padre e tutti gli utenti di questo spazio dei nomi contiguo usano lo stesso cluster RMS, è possibile usare un solo record SRV nel dominio padre. RMS troverà i record DNS appropriati.
I record SRV hanno il formato seguente: _rmsdisco. _http. _tcp. \<suffissopostaelettronica>\< numeroporta>\< fqdnclusterrms>

> [!NOTE]
> Specificare 443 per il \<> NumeroPorta. Sebbene sia possibile specificare un numero di porta diverso in DNS, i dispositivi che usano l'estensione per dispositivi mobili utilizzeranno sempre 443.

Se ad esempio l'organizzazione ha utenti con gli indirizzi di posta elettronica seguenti:
  - _user@contoso.com
  - _user@sales.contoso.com
  - _user@fabrikam.comSe non sono presenti altri domini figlio per _contoso. com che usano un cluster RMS diverso da quello denominato _rmsserver. contoso. com, creare due record DNS SRV con questi valori:
- _rmsdisco. _http. _tcp. contoso. com 443 _rmsserver. contoso. com
- _rmsdisco. _http. _tcp. fabrikam. com 443 _rmsserver. contoso. com

Se si usa il ruolo server DNS in Windows Server, usare le tabelle seguenti come guida per le proprietà del record SRV nella console Gestore DNS:

|Campo|valore|
|------|------|
|Dominio|_tcp. contoso. com
|Service|_rmsdisco
|Protocollo|_http
|Priorità|0
|Peso|0
|Numero della porta|443
|Host che offre questo servizio|_rmsserver. contoso. com

|Campo|valore|
|------|------|
|Dominio|_tcp. fabrikam. com
|Service|_rmsdisco
|Protocollo|_http
|Priorità|0
|Peso|0
|Numero della porta|443
|Host che offre questo servizio|_rmsserver. contoso. com|

Oltre ai record SRV DNS per il dominio di posta elettronica, è necessario creare un altro record DNS SRV nel dominio del cluster RMS. Questo record deve specificare i nomi di dominio completi del cluster RMS che proteggono il contenuto. Ogni file protetto con RMS include un URL del cluster che lo ha protetto. I dispositivi mobili usano il record DNS SRV e il nome FQDN dell'URL specificato nel record per trovare il cluster RMS in grado di supportarli.

Ad esempio, se il cluster RMS è **_rmsserver. contoso. com**, creare un record DNS SRV con i valori seguenti: **_rmsdisco. _http. _tcp. contoso. com 443 _rmsserver. contoso. com**

Se si usa il ruolo server DNS in Windows Server, usare la tabella seguente come guida per le proprietà del record SRV nella console Gestore DNS:

|Campo|valore|
|------|------|
|Dominio|_tcp. contoso. com
|Service|_rmsdisco
|Protocollo|_http
|Priorità|0
|Peso|0
|Numero della porta|443
|Host che offre questo servizio|_rmsserver. contoso. com|

## <a name="deploying-the-ad-rms-mobile-device-extension"></a>Distribuire l'estensione AD RMS per dispositivi mobili

Prima di installare l'estensione AD RMS Mobile Device, assicurarsi che i prerequisiti della sezione precedente siano soddisfatti e che si conosca l'URL del server AD FS. Eseguire quindi le operazioni seguenti:

1. Scaricare l'estensione per dispositivi mobili AD RMS (ADRMS. MobileDeviceExtension. exe) dall'area download Microsoft.
1. Eseguire **ADRMS. MobileDeviceExtension. exe** per avviare l'installazione guidata dell'estensione per dispositivi mobili Active Directory Rights Management Services.
Quando richiesto, immettere l'URL del server ADFS configurato in precedenza.
1. Completare la procedura guidata.

Eseguire questa procedura guidata in tutti i nodi del cluster RMS.

Se si dispone di un server proxy tra il cluster AD RMS e i server AD FS, per impostazione predefinita il cluster AD RMS non sarà in grado di contattare il servizio federato. In tal caso, AD RMS non sarà in grado di verificare il token ricevuto dal client mobile e rifiuterà la richiesta. Se si dispone di un server proxy che blocca questa comunicazione, è necessario aggiornare il file Web. config dal sito Web AD RMS estensione per dispositivi mobili, in modo che AD RMS possibile ignorare il server proxy quando è necessario contattare i server AD FS.

#### <a name="updating-proxy-settings-for-the-ad-rms-mobile-device-extension"></a>Aggiornamento delle impostazioni proxy per l'estensione AD RMS dispositivo mobile

1. Aprire il file Web. config che si trova in **\Program \Programmi\active Directory Rights Management Services Mobile Device Extension\Web Service**.

1. Aggiungere il nodo seguente al file:

```powershell
   <system.net>
    <defaultProxy>
        <proxy  proxyaddress="http://<proxy server>:<port>"
                bypassonlocal="true"
        />
        <bypasslist>
            <add address="<AD FS URL>" />
        </bypasslist>
    </defaultProxy>
<system.net>
```
1. Apportare le modifiche seguenti e quindi salvare il file:
- Sostituire \< proxy-server> con il nome o l'indirizzo del server proxy.
- Sostituire \< port> con il numero di porta configurato per l'utilizzo nel server proxy.
- Sostituire \< ad FS url> con l'URL del servizio federativo. Non includere il prefisso HTTP.

    > [!NOTE]
    > Per ulteriori informazioni sull'override delle impostazioni proxy, vedere la documentazione sulla [configurazione del proxy](https://msdn.microsoft.com/library/dkwyc043(v=vs.110).aspx) .

1. Ripristinare IIS, ad esempio eseguendo **iisreset** come amministratore da un prompt dei comandi.

Ripetere questa procedura in tutti i nodi del cluster RMS.


## <a name="see-also"></a>Vedere anche

Scopri di più su Azure Information Protection, contatta con altri clienti AIP e con i responsabili dei prodotti AIP usando il [gruppo Yammer API](https://www.yammer.com/askipteam/). 

