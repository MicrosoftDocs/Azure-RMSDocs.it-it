---
title: Sviluppo dell&quot;applicazione - AIP
description: Materiale sussidiario per un&quot;app console di base che implementa la protezione dei documenti con Azure Information Protection
keywords: 
author: bruceperlerms
ms.author: bruceper
manager: mbaldwin
ms.date: 03/13/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 396A2C19-3A00-4E9A-9088-198A48B15289
audience: developer
ms.reviewer: kartikk
ms.suite: ems
ms.openlocfilehash: 24689c3337361fb5e59420684ec8f5e9c723e448
ms.sourcegitcommit: 262f88c4f46e29f3747271276c62913b4cefe4f7
translationtype: HT
---
# <a name="developing-your-application"></a>Sviluppo dell'applicazione

In questo esempio verrà creata una semplice applicazione console che interagisce con il servizio Azure Information Protection (AIP).  Verrà usato come input il percorso di un documento da proteggere, quindi verrà applicata la protezione con criteri ad hoc o un modello di Azure. L'applicazione applicherà quindi i criteri corretti in base agli input, creando un documento con informazioni protette. Il codice di esempio che verrà usato è l'[applicazione di test Azure IP](https://github.com/Azure-Samples/Azure-Information-Protection-Samples/tree/master/AzureIP_Test) e si trova in Github.

## <a name="sample-app-prerequisites"></a>Prerequisiti dell'app di esempio
- **Sistema operativo**: Windows 10, Windows 8, Windows 7, Windows Server 2008, Windows Server 2008 R2 o Windows Server 2012
- **Linguaggio di programmazione**: C# (.NET Framework 3.0 e versioni successive)
- **Ambiente di sviluppo**: Visual Studio 2015 (e versioni successive)

## <a name="setting-up-your-azure-configuration"></a>Impostazione della configurazione di Azure

La configurazione di Azure per questa app richiede la creazione di un ID tenant, una chiave simmetrica e un ID entità applicazione.

### <a name="azure-ad-tenant-configuration"></a>Configurazione del tenant di Azure AD

Per configurare l'ambiente di Azure AD per Azure Information Protection, seguire le indicazioni fornite in [Attivazione di Azure Rights Management](https://docs.microsoft.com/en-us/information-protection/deploy-use/activate-service).

Una volta attivato il servizio saranno necessari i componenti di PowerShell per i passaggi successivi. A tale scopo, vedere [Amministrazione del servizio Azure Rights Management mediante Windows PowerShell](https://docs.microsoft.com/en-us/information-protection/deploy-use/administer-powershell).

### <a name="getting-your-tenant-id"></a>Ottenere un ID tenant

- Eseguire PowerShell come amministratore.
- Importare il modulo RMS: `Import-Module AADRM`
- Connettersi al servizio con le credenziali utente assegnate: `Connect-AadrmService –Verbose`
- Assicurarsi che RMS sia abilitato: `Enable-AADRM`
- Ottenere l'ID tenant eseguendo: `Get-AadrmConfiguration`

>Registrare il valore BPOSId (ID tenant). Sarà necessario nei passaggi successivi.

*Output di esempio*
![output del cmdlet](../media/develop/output-of-Get-AadrmConfiguration.png)

- Disconnettersi dal servizio: `Disconnect-AadrmService`

### <a name="create-a-service-principal"></a>Creare un'entità servizio
Per creare un'entità servizio, seguire questi passaggi:
> Un'entità servizio è costituita dalle credenziali configurate a livello globale per il controllo di accesso che consentono a un servizio di eseguire l'autenticazione con Microsoft Azure AD e di proteggere le informazioni tramite Microsoft Azure AD Rights Management.

- Eseguire PowerShell come amministratore.
- Importare il modulo di Microsoft Azure AD usando: `Import-Module MSOnline`
- Connettersi al servizio online con le credenziali utente assegnate: `Connect-MsolService`
- Creare una nuova entità servizio eseguendo: `New-MsolServicePrincipal`
- Specificare un nome per l'entità servizio
> Registrare la chiave simmetrica e l'ID entità applicazione per un uso futuro.

*Output di esempio*
![output del cmdlet](../media/develop/output-of-NewMsolServicePrincipal.png)

- Aggiungere l'ID entità applicazione, la chiave simmetrica e l'ID tenant al file App.config dell'applicazione.

*File App.config di esempio*
![output del cmdlet](../media/develop/example-App.config-file.png)

- I valori *ClientID* e *RedirectUri* saranno disponibile all'utente dopo la registrazione dell'applicazione in Azure. Per altre informazioni su come registrare l'applicazione in Azure e acquisire un valore *ClientID* e *RedirectUri*, vedere [Configurare Azure RMS per l'autenticazione ADAL](adal-auth.md).


## <a name="design-summary"></a>Riepilogo della progettazione
Il diagramma seguente illustra il flusso di architettura e processo per l'app creata. I passaggi vengono descritti di seguito.
![riepilogo della progettazione](../media/develop/design-summary.png)

1. L'utente inserisce l'input:
  - Il percorso del file da proteggere
  - Seleziona un modello o crea criteri ad hoc
2. L'applicazione richiede l'autenticazione con AIP.
3. AIP conferma l'autenticazione
4. L'applicazione richiede i modelli ad AIP.
5. AIP restituisce i modelli predefiniti.
6. L'applicazione trova il file specificato con il percorso specificato.
7. L'applicazione applica i criteri di protezione AIP al file.

## <a name="how-the-code-works"></a>Funzionamento del codice

Nell'esempio test di Azure IP la soluzione ha inizio con il file Iprotect.cs. Si tratta di un'applicazione console in C# e come con qualsiasi altra applicazione abilitata per AIP iniziare a caricare il file *MSIPC.dll* come illustrato nel metodo `main()`.

    //Loads MSIPC.dll
    SafeNativeMethods.IpcInitialize();
    SafeNativeMethods.IpcSetAPIMode(APIMode.Server);

Caricare i parametri necessari per connettersi ad Azure.

    //Loads credentials for the service principal from App.Config
    SymmetricKeyCredential symmetricKeyCred = new SymmetricKeyCredential();
    symmetricKeyCred.AppPrincipalId = ConfigurationManager.AppSettings["AppPrincipalId"];
    symmetricKeyCred.Base64Key = ConfigurationManager.AppSettings["Base64Key"];
    symmetricKeyCred.BposTenantId = ConfigurationManager.AppSettings["BposTenantId"];

Quando si specifica il percorso del file nell'applicazione console, l'applicazione controlla se il documento è già crittografato. Il metodo fa parte della classe **SafeFileApiNativeMethods**.

    var checkEncryptionStatus = SafeFileApiNativeMethods.IpcfIsFileEncrypted(filePath);

Se il documento non è crittografato, verrà crittografato con la selezione fornita quando richiesto.

    if (!checkEncryptionStatus.ToString().ToLower().Contains(alreadyEncrypted))
    {
      if (method == EncryptionMethod1)
      {
        //Encrypt a file via AIP template
        ProtectWithTemplate(symmetricKeyCred, filePath);

      }
      else if (method == EncryptionMethod2)
      {
        //Encrypt a file using ad-hoc policy
        ProtectWithAdHocPolicy(symmetricKeyCred, filePath);
      }

L'opzione per eseguire la protezione con il modello consente di ottenere l'elenco dei modelli dal server da cui l'utente può scegliere.
>Se i modelli non sono stati modificati, si avranno i modelli predefiniti di AIP.

     public static void ProtectWithTemplate(SymmetricKeyCredential symmetricKeyCredential, string filePath)
     {
       // Gets the available templates for this tenant             
       Collection<TemplateInfo> templates = SafeNativeMethods.IpcGetTemplateList(null, false, true,
           false, true, null, null, symmetricKeyCredential);

       //Requests tenant template to use for encryption
       Console.WriteLine("Please select the template you would like to use to encrypt the file.");

       //Outputs templates available for selection
       int counter = 0;
       for (int i = 0; i < templates.Count; i++)
       {
         counter++;
         Console.WriteLine(counter + ". " + templates.ElementAt(i).Name + "\n" +
             templates.ElementAt(i).Description);
       }

       //Parses template selection
       string input = Console.ReadLine();
       int templateSelection;
       bool parseResult = Int32.TryParse(input, out templateSelection);

       //Returns error if no template selection is entered
       if (parseResult)
       {
         //Ensures template value entered is valid
         if (0 < templateSelection && templateSelection <= counter)
         {
           templateSelection -= templateSelection;

           // Encrypts the file using the selected template             
           TemplateInfo selectedTemplateInfo = templates.ElementAt(templateSelection);

           string encryptedFilePath = SafeFileApiNativeMethods.IpcfEncryptFile(filePath,
               selectedTemplateInfo.TemplateId,
               SafeFileApiNativeMethods.EncryptFlags.IPCF_EF_FLAG_KEY_NO_PERSIST, true, false, true, null,
               symmetricKeyCredential);
          }
        }
      }

Se si selezionano i criteri ad hoc, l'utente dell'applicazione deve fornire gli indirizzi di posta elettronica degli utenti a cui concedere i diritti. In questa sezione viene creata la licenza usando il metodo **IpcCreateLicenseFromScratch()** e applicando i nuovi criteri nel modello.

    if (issuerDisplayName.Trim() != "")
    {
      // Gets the available issuers of rights policy templates.              
      // The available issuers is a list of RMS servers that this user has already contacted.
      try
      {
        Collection<TemplateIssuer> templateIssuers = SafeNativeMethods.IpcGetTemplateIssuerList(
                                                        null,
                                                        true,
                                                        false,
                                                        false, true, null, symmetricKeyCredential);

        // Creates the policy and associates the chosen user rights with it             
        SafeInformationProtectionLicenseHandle handle = SafeNativeMethods.IpcCreateLicenseFromScratch(
                                                            templateIssuers.ElementAt(0));
        SafeNativeMethods.IpcSetLicenseOwner(handle, owner);
        SafeNativeMethods.IpcSetLicenseUserRightsList(handle, userRights);
        SafeNativeMethods.IpcSetLicenseDescriptor(handle, new TemplateInfo(null, CultureInfo.CurrentCulture,
                                                                policyName,
                                                                policyDescription,
                                                                issuerDisplayName,
                                                                false));

        //Encrypts the file using the ad hoc policy             
        string encryptedFilePath = SafeFileApiNativeMethods.IpcfEncryptFile(
                                       filePath,
                                       handle,
                                       SafeFileApiNativeMethods.EncryptFlags.IPCF_EF_FLAG_KEY_NO_PERSIST,
                                       true,
                                       false,
                                       true,
                                       null,
                                       symmetricKeyCredential);
       }
    }

## <a name="user-interaction-example"></a>Esempio di interazione utente

Dopo avere eseguito tutti i passaggi di creazione ed esecuzione, gli output dell'applicazione dovrebbero essere simili ai seguenti:

1.Viene chiesto di selezionare un metodo di crittografia.
![output dell'app - passaggio 1](../media/develop/app-output-1.png)

2. Viene chiesto di specificare il percorso del file da proteggere.
![output dell'app - passaggio 2](../media/develop/app-output-2.png)

3. Viene chiesto di immettere un indirizzo di posta elettronica del proprietario della licenza (il proprietario deve avere i privilegi di amministratore globale del tenant di Azure AD).
![output dell'app - passaggio 3](../media/develop/app-output-3.png)

4. Immettere gli indirizzi di posta elettronica degli utenti con i diritti di accesso al file (separare gli indirizzi di posta elettronica con spazi).
![output dell'app - passaggio 4](../media/develop/app-output-4.png)

5. Selezionare da un elenco i diritti da assegnare agli utenti autorizzati.
![output dell'app - passaggio 5](../media/develop/app-output-5.png)

6. Immettere infine alcuni metadati dei criteri: nome dei criteri, descrizione e nome visualizzato dell'autorità di certificazione (tenant di Azure AD) ![output dell'app - passaggio 6](../media/develop/app-output-6.png)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]