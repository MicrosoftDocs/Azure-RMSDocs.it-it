---
title: Esempi di codice iOS/OS X | Azure RMS
description: Questo argomento presenta importanti elementi di codice per la versione iOS/OS X di RMS SDK.
keywords: ''
author: msmbaldwin
ms.author: mbaldwin
manager: barbkess
ms.date: 02/23/2017
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 7E12EBF2-5A19-4A8D-AA99-531B09DA256A
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
ms.custom: dev, has-adal-ref
ms.openlocfilehash: 7ed06af67d004845de7a5a55090da9fc3b40388c
ms.sourcegitcommit: 298843953f9792c5879e199fd1695abf3d25aa70
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/08/2020
ms.locfileid: "82972000"
---
# <a name="iosos-x-code-examples"></a>Esempi di codice iOS/OS X

[!INCLUDE [deprecation notice](../includes/deprecation-warning.md)]

Questo argomento presenta importanti elementi di codice per la versione iOS/OS X di RMS SDK.

**Nota**: nel codice di esempio e nelle descrizioni che seguono, viene usato il termine MSIPC (Microsoft Information Protection and Control) per fare riferimento al processo client.



## <a name="using-the-microsoft-rights-management-sdk-42---key-scenarios"></a>Uso di Microsoft Rights Management SDK 4.2: scenari principali


Di seguito sono riportati esempi di codice **Objective C** tratti da un'applicazione di esempio di dimensioni maggiori che rappresenta scenari di sviluppo importanti per l'orientamento in questo SDK. Questi esempi illustrano l'uso del formato Microsoft Protected File definito come file protetto, l'uso di formati di file protetti personalizzati e l'uso di controlli di interfaccia utente personalizzati.

### <a name="scenario-consume-an-rms-protected-file"></a>Scenario: utilizzo di un file protetto RMS


- **Passaggio 1**: Creare un oggetto [MSProtectedData](https://msdn.microsoft.com/library/dn758348.aspx)

  **Descrizione**: creare un'istanza dell'oggetto [MSProtectedData](https://msdn.microsoft.com/library/dn758348.aspx) tramite il relativo metodo di creazione che implementa l'autenticazione del servizio tramite [MSAuthenticationCallback](https://msdn.microsoft.com/library/dn758312.aspx) per ottenere un token e passando all'API MSIPC un'istanza di **MSAuthenticationCallback** come parametro *authenticationCallback*. Vedere la chiamata a [MSProtectedData protectedDataWithProtectedFile](https://msdn.microsoft.com/library/dn758351.aspx) nella sezione di codice di esempio seguente.

        + (void)consumePtxtFile:(NSString *)path authenticationCallback:(id<MSAuthenticationCallback>)authenticationCallback
        {
            // userId can be provided as a hint for authentication
            [MSProtectedData protectedDataWithProtectedFile:path
                                                 userId:nil
                                 authenticationCallback:authenticationCallback
                                                options:Default
                                        completionBlock:^(MSProtectedData *data, NSError *error)
            {
                //Read the content from the ProtectedData, this will decrypt the data
                NSData *content = [data retrieveData];
            }];
        }

- **Passaggio 2**: Configurare l’autenticazione usando Active Directory Authentication Library (ADAL).

  **Descrizione**: in questo passaggio viene illustrato l'uso di ADAL per implementare [MSAuthenticationCallback](https://msdn.microsoft.com/library/dn758312.aspx) con parametri di autenticazione di esempio. Per altre informazioni sull'uso di ADAL, vedere Azure AD Authentication Library (ADAL).

      // AuthenticationCallback holds the necessary information to retrieve an access token.
      @interface MsipcAuthenticationCallback : NSObject<MSAuthenticationCallback>

      @end

      @implementation MsipcAuthenticationCallback

      - (void)accessTokenWithAuthenticationParameters:
             (MSAuthenticationParameters *)authenticationParameters
                                    completionBlock:
             (void(^)(NSString *accessToken, NSError *error))completionBlock
      {
          ADAuthenticationError *error;
          ADAuthenticationContext* context = [
              ADAuthenticationContext authenticationContextWithAuthority:authenticationParameters.authority
                                                                error:&error
          ];
          NSString *appClientId = @”com.microsoft.sampleapp”;
          NSURL *redirectURI = [NSURL URLWithString:@"local://authorize"];
          // Retrieve token using ADAL
          [context acquireTokenWithResource:authenticationParameters.resource
                                 clientId:appClientId
                              redirectUri:redirectURI
                                   userId:authenticationParameters.userId
                          completionBlock:^(ADAuthenticationResult *result) {
                              if (result.status != AD_SUCCEEDED)
                              {
                                  NSLog(@"Auth Failed");
                                  completionBlock(nil, result.error);
                              }
                              else
                              {
                                  completionBlock(result.accessToken, result.error);
                              }
                          }];
       }

- **Passaggio 3**: Verificare se è disponibile il diritto di modifica per questo utente su questo contenuto tramite il metodo [MSUserPolicy accessCheck](https://msdn.microsoft.com/library/dn790789.aspx) di un oggetto [MSUserPolicy](https://msdn.microsoft.com/library/dn790796.aspx).

      - (void)accessCheckWithProtectedData:(MSProtectedData *)protectedData
      {
          //check if user has edit rights and apply enforcements
          if (!protectedData.userPolicy.accessCheck(EditableDocumentRights.Edit))
          {
              // enforce on the UI
              textEditor.focusableInTouchMode = NO;
              textEditor.focusable = NO;
              textEditor.enabled = NO;
          }
      }

### <a name="scenario-create-a-new-protected-file-using-a-template"></a>Scenario: creazione di un nuovo file protetto tramite un modello

Questo scenario inizia con il recupero di un elenco di modelli, [MSTemplateDescriptor](https://msdn.microsoft.com/library/dn790785.aspx), prosegue con la selezione del primo modello per creare un criterio e termina con la creazione e la scrittura nel nuovo file protetto.

-   **Passaggio 1**: Ottenere un elenco di modelli

        + (void)templateListUsageWithAuthenticationCallback:(id<MSAuthenticationCallback>)authenticationCallback
        {
            [MSTemplateDescriptor templateListWithUserId:@"user@domain.com"
                            authenticationCallback:authenticationCallback
                                   completionBlock:^(NSArray/*MSTemplateDescriptor*/ *templates, NSError *error)
                                   {
                                     // use templates array of MSTemplateDescriptor (Note: will be nil on error)
                                   }];
        }

-   **Passaggio 2**: Creare una classe [MSUserPolicy](https://msdn.microsoft.com/library/dn790796.aspx) usando il primo modello dell'elenco.

        + (void)userPolicyCreationFromTemplateWithAuthenticationCallback:(id<MSAuthenticationCallback>)authenticationCallback
        {
            [MSUserPolicy userPolicyWithTemplateDescriptor:[templates objectAtIndex:0]
                                            userId:@"user@domain.com"
                                     signedAppData:nil
                            authenticationCallback:authenticationCallback
                                           options:None
                                   completionBlock:^(MSUserPolicy *userPolicy, NSError *error)
            {
            // use userPolicy (Note: will be nil on error)
            }];
        }

-   **Passaggio 3**: Creare una classe [MSMutableProtectedData](https://msdn.microsoft.com/library/dn758325.aspx) e scriverci contenuto.

        + (void)createPtxtWithUserPolicy:(MSUserPolicy *)userPolicy contentToProtect:(NSData *)contentToProtect
        {
            // create an MSMutableProtectedData to write content
            [contentToProtect protectedDataInFile:filePath
                        originalFileExtension:kDefaultTextFileExtension
                               withUserPolicy:userPolicy
                              completionBlock:^(MSMutableProtectedData *data, NSError *error)
            {
             // use data (Note: will be nil on error)
            }];
        }

### <a name="scenario-open-a-custom-protected-file"></a>Scenario: aprire di un file protetto personalizzato


-   **Passaggio 1**: Creare una classe [MSUserPolicy](https://msdn.microsoft.com/library/dn790796.aspx) da *serializedContentPolicy*.

        + (void)userPolicyWith:(NSData *)protectedData
        authenticationCallback:(id<MSAuthenticationCallback>)authenticationCallback
        {
            // Read header information from protectedData and extract the  PL
            /*-------------------------------------------
            | PL length | PL | ContetSizeLength |
            -------------------------------------------*/
            NSUInteger serializedPolicySize;
            NSMutableData *serializedPolicy;
            [protectedData getBytes:&serializedPolicySize length:sizeof(serializedPolicySize)];
            [protectedData getBytes:[serializedPolicy mutableBytes] length:serializedPolicySize];

            // Get the user policy , this is an async method as it hits the REST service
            // for content key and usage restrictions
            // userId provided as a hint for authentication
            [MSUserPolicy userPolicyWithSerializedPolicy:serializedPolicy
                                              userId:@"user@domain.com"
                              authenticationCallback:authenticationCallback
                                             options:Default
                                     completionBlock:^(MSUserPolicy *userPolicy,
                                                       NSError *error)
            {

            }];
         }

-   **Passaggio 2**: Creare una classe [MSCustomProtectedData](https://msdn.microsoft.com/library/dn758321.aspx) usando la classe [MSUserPolicy](https://msdn.microsoft.com/library/dn790796.aspx) del **Passaggio 1** e leggere il suo contenuto.

        + (void)customProtectedDataWith:(NSData *)protectedData
        {
            // Read header information from protectedData and extract the  protectedContentSize
            /*-------------------------------------------
            | PL length | PL | ContetSizeLength |
            -------------------------------------------*/
            NSUInteger protectedContentSize;
            [protectedData getBytes:&protectedContentSize
                         length:sizeof(protectedContentSize)];

            // Create the MSCustomProtector used for decrypting the content
            // The content start position is the header length
            [MSCustomProtectedData customProtectedDataWithPolicy:userPolicy
                                               protectedData:protectedData
                                        contentStartPosition:sizeof(NSUInteger) + serializedPolicySize
                                                 contentSize:protectedContentSize
                                             completionBlock:^(MSCustomProtectedData *customProtector,
                                                               NSError *error)
            {
             //Read the content from the custom protector, this will decrypt the data
             NSData *content = [customProtector retrieveData];
             NSLog(@"%@", content);
            }];
         }

### <a name="scenario-create-a-custom-protected-file-using-a-custom-ad-hoc-policy"></a>Scenario: creazione di un file protetto personalizzato usando un criterio personalizzato (ad-hoc)


-   **Passaggio 1**: Creare un descrittore di criteri con un indirizzo di posta elettronica fornito dall'utente.

    **Descrizione**: in pratica vengono creati gli oggetti [MSUserRights](https://msdn.microsoft.com/library/dn790811.aspx) e [MSPolicyDescriptor](https://msdn.microsoft.com/library/dn758339.aspx) usando gli input dell'utente dall'interfaccia del dispositivo.

        + (void)policyDescriptor
        {
            MSUserRights *userRights = [[MSUserRights alloc] initWithUsers:[NSArray arrayWithObjects: @"user1@domain.com", @"user2@domain.com", nil] rights:[MSEmailRights all]];

            MSPolicyDescriptor *policyDescriptor = [[MSPolicyDescriptor alloc] initWithUserRights:[NSArray arrayWithObjects:userRights, nil]];
            policyDescriptor.contentValidUntil = [[NSDate alloc] initWithTimeIntervalSinceNow:NSTimeIntervalSince1970 + 3600.0];
            policyDescriptor.offlineCacheLifetimeInDays = 10;
        }

-   **Passaggio 2**: Creare una classe personalizzata [MSUserPolicy](https://msdn.microsoft.com/library/dn790796.aspx) dal descrittore del criterio, ovvero *selectedDescriptor*.

        + (void)userPolicyWithPolicyDescriptor:(MSPolicyDescriptor *)policyDescriptor
        {
            [MSUserPolicy userPolicyWithPolicyDescriptor:policyDescriptor
                                          userId:@"user@domain.com"
                          authenticationCallback:authenticationCallback
                                         options:None
                                 completionBlock:^(MSUserPolicy *userPolicy, NSError *error)
            {
              // use userPolicy (Note: will be nil on error)
            }];
        }

-   **Passaggio 3**: Creare e scrivere il contenuto per la classe [MSMutableCustomProtectedData](https://msdn.microsoft.com/library/dn758321.aspx) e chiudere.

        + (void)mutableCustomProtectedData:(NSMutableData *)backingData policy:(MSUserPolicy *)policy contentToProtect:(NSString *)contentToProtect
        {
            //Get the serializedPolicy from a given policy
            NSData *serializedPolicy = [policy serializedPolicy];

            // Write header information to backing data including the PL
            // ------------------------------------
            // | PL length | PL | ContetSizeLength |
            // -------------------------------------
            NSUInteger serializedPolicyLength = [serializedPolicy length];
            [backingData appendData:[NSData dataWithBytes:&serializedPolicyLength length:sizeof(serializedPolicyLength)]];
            [backingData appendData:serializedPolicy];
            NSUInteger protectedContentLength = [MSCustomProtectedData getEncryptedContentLengthWithPolicy:policy contentLength:unprotectedData.length];
            [backingData appendData:[NSData dataWithBytes:&protectedContentLength length:sizeof(protectedContentLength)]];

            NSUInteger headerLength = sizeof(serializedPolicyLength) + serializedPolicyLength + sizeof(protectedContentLength);

            // Create the MSMutableCustomProtector used for encrypting content
            // The content start position is the current length of the backing data
            // The encryptedContentSize content size is 0 since there is no content yet
            [MSMutableCustomProtectedData customProtectorWithUserPolicy:policy
                                                        backingData:backingData
                                             protectedContentOffset:headerLength
                                                    completionBlock:^(MSMutableCustomProtectedData *customProtector,
                                                                      NSError *error)
            {
                //Append data to the custom protector, this will encrypt the data and write it to the backing data
                [customProtector appendData:[contentToProtect dataUsingEncoding:NSUTF8StringEncoding] error:&error];

                //close the custom protector so it will flush and finalise encryption
                [customProtector close:&error];

            }];
          }
