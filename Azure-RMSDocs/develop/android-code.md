---
title: Esempi di codice Android | Azure RMS
description: In questo argomento sono presentati importanti elementi di codice per la versione Android di RMS SDK.
keywords: 
author: bruceperlerms
ms.author: bruceper
manager: mbaldwin
ms.date: 02/23/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 58CC2E50-1E4D-4621-A947-25312C3FF519
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 7068e0529409eb783f16bc207a17be27cd5d82a8
ms.openlocfilehash: 847d19feaea442da66296565f0ffb5b0663ad170
ms.lasthandoff: 01/24/2017


---

# <a name="android-code-examples"></a>Esempi di codice Android

In questo argomento sono presentati importanti elementi di codice per la versione Android di RMS SDK.

**Nota** Nel codice di esempio e nelle descrizioni che seguono, viene usato il termine MSIPC (Microsoft Information Protection and Control) per fare riferimento al processo client.


## <a name="using-the-microsoft-rights-management-sdk-42---key-scenarios"></a>Uso di Microsoft Rights Management SDK 4.2 - Scenari principali

Di seguito sono riportati esempi di codice tratti da un’applicazione di esempio di dimensioni maggiori che rappresenta scenari di sviluppo importanti per l’orientamento in questo SDK. Questi esempi illustrano l’uso del formato Microsoft Protected File definito come file protetto, l’uso di formati di file protetti personalizzati e l’uso di controlli di interfaccia utente personalizzati.



È disponibile l’applicazione di esempio *MSIPCSampleApp* da usare con questo SDK per il sistema operativo Android. Per accedere a questa applicazione di esempio, vedere [rms-sdk-ui-for-android](https://github.com/AzureAD/rms-sdk-ui-for-android) su GitHub.

### <a name="scenario-consume-an-rms-protected-file"></a>Scenario: utilizzo di un file protetto RMS

-   **Passaggio 1**: Creare un oggetto [ProtectedFileInputStream](https://msdn.microsoft.com/library/dn790851.aspx)

    **Origine**: *MsipcAuthenticationCallback.java*

    **Descrizione**: creare un'istanza dell'oggetto [ProtectedFileInputStream](https://msdn.microsoft.com/library/dn790851.aspx) tramite il relativo metodo di creazione che implementa l'autenticazione del servizio tramite [AuthenticationRequestCallback](https://msdn.microsoft.com/library/dn758250.aspx) per ottenere un token e passando all'API MSIPC un'istanza di**AuthenticationRequestCallback** come parametro *mRmsAuthCallback*. Vedere la chiamata a [ProtectedFileInputStream.create](https://msdn.microsoft.com/library/dn790851.aspx) verso la fine della sezione del codice di esempio seguente.

        public void startContentConsumptionFromPtxtFileFormat(InputStream inputStream)
        {
            CreationCallback<ProtectedFileInputStream> protectedFileInputStreamCreationCallback =
              new CreationCallback<ProtectedFileInputStream>()
            {
                @Override
                public Context getContext()
                {
                   …
               }

                @Override
                public void onCancel()
                {
                   …
                }

                @Override
                public void onFailure(ProtectionException e)
                {
                   …
                }

                @Override
                public void onSuccess(ProtectedFileInputStream protectedFileInputStream)
                {
                   …
                   …
                    byte[] dataChunk = new byte[16384];
                    try
                    {
                        while ((nRead = protectedFileInputStream.read(dataChunk, 0,
                                dataChunk.length)) != -1)
                        {
                            …
                        }
                         …
                        protectedFileInputStream.close();
                    }
                    catch (IOException e)
                    {
                      …
                    }  
              }
            };
            try
            {
               …
                ProtectedFileInputStream.create(inputStream, null, mRmsAuthCallback,
                                                PolicyAcquisitionFlags.NONE,
                                                protectedFileInputStreamCreationCallback);
            }
            catch (com.microsoft.rightsmanagement.exceptions.InvalidParameterException e)
            {
                …
            }
        }


-   **Passaggio 2**: Configurare l'autenticazione usando Active Directory Authentication Library (ADAL).

    **Origine**: *MsipcAuthenticationCallback.java*.

    **Descrizione**: in questo passaggio viene illustrato l'uso di ADAL per implementare [AuthenticationRequestCallback](https://msdn.microsoft.com/library/dn758255.aspx) con parametri di autenticazione di esempio. Per altre informazioni sull'uso di ADAL, vedere [Active Directory Authentication Library .NET](https://msdn.microsoft.com/library/jj573266.aspx).


        class MsipcAuthenticationCallback implements AuthenticationRequestCallback
        {

        …

        @Override
        public void getToken(Map<String, String> authenticationParametersMap,
                             final AuthenticationCompletionCallback authenticationCompletionCallbackToMsipc)
        {
            String authority = authenticationParametersMap.get("oauth2.authority");
            String resource = authenticationParametersMap.get("oauth2.resource");
            String userId = authenticationParametersMap.get("userId");
            final String userHint = (userId == null)? "" : userId;
            AuthenticationContext authenticationContext = App.getInstance().getAuthenticationContext();
            if (authenticationContext == null || !authenticationContext.getAuthority().equalsIgnoreCase(authority))
            {
                try
                {
                    authenticationContext = new AuthenticationContext(App.getInstance().getApplicationContext(), authority, …);
                    App.getInstance().setAuthenticationContext(authenticationContext);
                }
                catch (NoSuchAlgorithmException e)
                {
                    …
                    authenticationCompletionCallbackToMsipc.onFailure();
                }
                catch (NoSuchPaddingException e)
                {
                    …
                    authenticationCompletionCallbackToMsipc.onFailure();
                }
           }
            App.getInstance().getAuthenticationContext().acquireToken(mParentActivity, resource, mClientId, mRedirectURI, userId, mPromptBehavior,
                           "&USERNAME=" + userHint, new AuthenticationCallback<AuthenticationResult>()
                            {
                                @Override
                                public void onError(Exception exc)
                                {
                                    …
                                    if (exc instanceof AuthenticationCancelError)
                                    {
                                         …
                                        authenticationCompletionCallbackToMsipc.onCancel();
                                    }
                                    else
                                    {
                                         …
                                        authenticationCompletionCallbackToMsipc.onFailure();
                                    }
                                }

                                @Override
                                public void onSuccess(AuthenticationResult result)
                                {
                                    …
                                    if (result == null || result.getAccessToken() == null
                                            || result.getAccessToken().isEmpty())
                                    {
                                         …
                                    }
                                    else
                                    {
                                        // request is successful
                                        …
                                        authenticationCompletionCallbackToMsipc.onSuccess(result.getAccessToken());
                                    }
                                }
                            }

                            );
                      }


-   **Passaggio 3**: Verificare se esiste il diritto di **modifica** per questo utente su questo contenuto tramite il metodo [UserPolicy.accessCheck](https://msdn.microsoft.comlibrary/dn790885.aspx).

    **Origine**: *TextEditorFragment.java*


         //check if user has edit rights and apply enforcements
                if (!mUserPolicy.accessCheck(EditableDocumentRights.Edit))
                {
                    mTextEditor.setFocusableInTouchMode(false);
                    mTextEditor.setFocusable(false);
                    mTextEditor.setEnabled(false);
                    …
                }


### <a name="scenario-create-a-new-protected-file-using-a-template"></a>Scenario: creare un nuovo file protetto tramite un modello

Questo scenario inizia con il recupero di un elenco di modelli e la selezione del primo di essi per creare un criterio e procede quindi con la creazione e la scrittura di contenuto nel nuovo file protetto.

-   **Passaggio 1**: Ottenere un elenco di modelli tramite un oggetto [TemplateDescriptor](https://msdn.microsoft.com/library/dn790871.aspx).

    **Origine**: *MsipcTaskFragment.java*



    CreationCallback<List<TemplateDescriptor>> getTemplatesCreationCallback = new CreationCallback<List<TemplateDescriptor>>() { @Override public Context getContext() { …
          }

          @Override
          public void onCancel()
          {
              …
          }

          @Override
          public void onFailure(ProtectionException e)
          {
              …
          }

          @Override
          public void onSuccess(List<TemplateDescriptor> templateDescriptors)
          {
             …
          }
      }; try { …
          mIAsyncControl = TemplateDescriptor.getTemplates(emailId, mRmsAuthCallback, getTemplatesCreationCallback); } catch (com.microsoft.rightsmanagement.exceptions.InvalidParameterException e) { …
      }


-    **Passaggio 2**: Creare una classe [UserPolicy](https://msdn.microsoft.com/library/dn790887.aspx) usando il primo modello dell'elenco.

    **Origine**: *MsipcTaskFragment.java*



      CreationCallback<UserPolicy> userPolicyCreationCallback = new CreationCallback<UserPolicy>() { @Override public Context getContext() { …
          }

          @Override
          public void onCancel()
          {
              …
          }

          @Override
          public void onFailure(ProtectionException e)
          {
              …
          }

          @Override
          public void onSuccess(final UserPolicy item)
          {
              …
          }
      }; try { …
          mIAsyncControl = UserPolicy.create((TemplateDescriptor)selectedDescriptor, mEmailId, mRmsAuthCallback, UserPolicyCreationFlags.NONE, userPolicyCreationCallback); …
      } catch (InvalidParameterException e) { …
      }


-    **Passaggio 3**: Creare una classe [ProtectedFileOutputStream](https://msdn.microsoft.com/library/dn790855.aspx) e scriverci il contenuto.

    **Origine**: *MsipcTaskFragment.java*


    private void createPTxt(final byte[] contentToProtect) { …
            CreationCallback<ProtectedFileOutputStream> protectedFileOutputStreamCreationCallback = new CreationCallback<ProtectedFileOutputStream>() { @Override public Context getContext() { …
                }

                @Override
                public void onCancel()
                {
                 …
                }

                @Override
                public void onFailure(ProtectionException e)
                {
                 …
                }

                @Override
                public void onSuccess(ProtectedFileOutputStream protectedFileOutputStream)
                {
                    try
                    {
                        // write to this stream
                        protectedFileOutputStream.write(contentToProtect);
                        protectedFileOutputStream.flush();
                        protectedFileOutputStream.close();
                        …
                    }
                    catch (IOException e)
                    {
                        …
                    }
                }
            };
            try
            {
                File file = new File(filePath);
                outputStream = new FileOutputStream(file);
                mIAsyncControl = ProtectedFileOutputStream.create(outputStream, mUserPolicy, originalFileExtension,
                        protectedFileOutputStreamCreationCallback);
            }
            catch (FileNotFoundException e)
            {
                 …
            }
            catch (InvalidParameterException e)
            {
                 …
            }
        }



### <a name="scenario-open-a-custom-protected-file"></a>Scenario: aprire di un file protetto personalizzato

-   **Passaggio 1**: Creare un oggetto[UserPolicy](https://msdn.microsoft.com/library/dn790887.aspx) da *serializedContentPolicy*.

    **Origine**: *MsipcTaskFragment.java*


    CreationCallback<UserPolicy> userPolicyCreationCallbackFromSerializedContentPolicy = new CreationCallback<UserPolicy>() { @Override public void onSuccess(UserPolicy userPolicy) { …
                }

                @Override
                public void onFailure(ProtectionException e)
                {
                  …
                }

                @Override
                public void onCancel()
                {
                  …
                }

                @Override
                public Context getContext()
                {
                  …
                }
            };


    try {   ...

      // Read the serializedContentPolicyLength from the inputStream.
      long serializedContentPolicyLength = readUnsignedInt(inputStream);

      // Read the PL bytes from the input stream using the PL size.
      byte[] serializedContentPolicy = new byte[(int)serializedContentPolicyLength]; inputStream.read(serializedContentPolicy);

      ...

      UserPolicy.acquire(serializedContentPolicy, null, mRmsAuthCallback, PolicyAcquisitionFlags.NONE,           userPolicyCreationCallbackFromSerializedContentPolicy); } catch (com.microsoft.rightsmanagement.exceptions.InvalidParameterException e) {   ... } catch (IOException e) {   ... }



-    **Passaggio 2**: Creare una classe [CustomProtectedInputStream](https://msdn.microsoft.com/library/dn758271.aspx) usando la classe [UserPolicy](https://msdn.microsoft.com/library/dn790887.aspx) del **Passaggio 1**.

    **Origine**: *MsipcTaskFragment.java*



      CreationCallback<CustomProtectedInputStream> customProtectedInputStreamCreationCallback = new CreationCallback<CustomProtectedInputStream>() { @Override public Context getContext() { …
         }

         @Override
         public void onCancel()
         {
             …
         }

         @Override
         public void onFailure(ProtectionException e)
         {
             …
         }

         @Override
         public void onSuccess(CustomProtectedInputStream customProtectedInputStream)
         {
            …

             byte[] dataChunk = new byte[16384];
             try
             {
                 while ((nRead = customProtectedInputStream.read(dataChunk, 0, dataChunk.length)) != -1)
                 {
                      …
                 }
                  …
                 customProtectedInputStream.close();
             }
             catch (IOException e)
             {
                …
             }
             …
         }
     };

    try {  ...

      // Retrieve the encrypted content size.
      long encryptedContentLength = readUnsignedInt(inputStream);

      updateTaskStatus(new TaskStatus(TaskState.Starting, "Consuming content", true));

      CustomProtectedInputStream.create(userPolicy, inputStream,                                 encryptedContentLength,                                 customProtectedInputStreamCreationCallback); } catch (com.microsoft.rightsmanagement.exceptions.InvalidParameterException e) {  ... } catch (IOException e) {  ... }


-    **Passaggio 3**: Leggere il contenuto da [CustomProtectedInputStream](https://msdn.microsoft.com/library/dn758271.aspx) in *mDecryptedContent* e chiudere.

    **Origine**: *MsipcTaskFragment.java*


    @Override public void onSuccess(CustomProtectedInputStream customProtectedInputStream) {  mUserPolicy = customProtectedInputStream.getUserPolicy();  ByteArrayOutputStream buffer = new ByteArrayOutputStream();

      int nRead;                      
      byte[] dataChunk = new byte[16384];

      try  {    while ((nRead = customProtectedInputStream.read(dataChunk, 0,                                                        dataChunk.length)) != -1)    {       buffer.write(dataChunk, 0, nRead);    }

        buffer.flush();    mDecryptedContent = new String(buffer.toByteArray(), Charset.forName("UTF-8"));

        buffer.close();    customProtectedInputStream.close();  }  catch (IOException e)  {    ...  } }


### <a name="scenario-create-a-custom-protected-file-using-a-custom-ad-hoc-policy"></a>Scenario: creare un file protetto personalizzato usando un criterio personalizzato (ad-hoc)

-   **Passaggio 1**: Creare un descrittore di criteri con un indirizzo di posta elettronica fornito dall’utente.

    **Origine**: *MsipcTaskFragment.java*

    **Descrizione**: in pratica vengono creati gli oggetti [UserRights](https://msdn.microsoft.com/library/dn790911.aspx) e [PolicyDescriptor](https://msdn.microsoft.com/library/dn790843.aspx) usando gli input dell'utente dall'interfaccia del dispositivo.



      // create userRights list   UserRights userRights = new UserRights(Arrays.asList("consumer@domain.com"),     Arrays.asList( CommonRights.View, EditableDocumentRights.Print));   ArrayList<UserRights> usersRigthsList = new ArrayList<UserRights>();   usersRigthsList.add(userRights);

      // Create PolicyDescriptor using userRights list   PolicyDescriptor policyDescriptor = PolicyDescriptor.createPolicyDescriptorFromUserRights(                                                          usersRigthsList);   policyDescriptor.setOfflineCacheLifetimeInDays(10);   policyDescriptor.setContentValidUntil(new Date());



-    **Passaggio 2**: Creare una classe personalizzata [UserPolicy](https://msdn.microsoft.com/library/dn790887.aspx) dal descrittore del criterio, ovvero *selectedDescriptor*.

    **Origine**: *MsipcTaskFragment.java*


       mIAsyncControl = UserPolicy.create((PolicyDescriptor)selectedDescriptor,                                          mEmailId, mRmsAuthCallback,                                          UserPolicyCreationFlags.NONE,                                          userPolicyCreationCallback);



-   **Passaggio 3**: Creare e scrivere il contenuto per la classe [CustomProtectedOutputStream](https://msdn.microsoft.com/library/dn758274.aspx) e chiudere.

    **Origine**: *MsipcTaskFragment.java*


    File file = new File(filePath); final OutputStream outputStream = new FileOutputStream(file); CreationCallback<CustomProtectedOutputStream> customProtectedOutputStreamCreationCallback = new CreationCallback<CustomProtectedOutputStream>() { @Override public Context getContext() { …
            }

            @Override
            public void onCancel()
            {
              …
            }

            @Override
            public void onFailure(ProtectionException e)
            {
              …
            }

            @Override
            public void onSuccess(CustomProtectedOutputStream protectedOutputStream)
            {
                try
                {
                    // write serializedContentPolicy
                    byte[] serializedContentPolicy = mUserPolicy.getSerializedContentPolicy();
                    writeLongAsUnsignedIntToStream(outputStream, serializedContentPolicy.length);
                    outputStream.write(serializedContentPolicy);
                    // write encrypted content
                    if (contentToProtect != null)
                    {
                        writeLongAsUnsignedIntToStream(outputStream,
                                CustomProtectedOutputStream.getEncryptedContentLength(contentToProtect.length,
                                        protectedOutputStream.getUserPolicy()));
                        protectedOutputStream.write(contentToProtect);
                        protectedOutputStream.flush();
                        protectedOutputStream.close();
                    }
                    else
                    {
                        outputStream.flush();
                        outputStream.close();
                    }
                    …
                }
                catch (IOException e)
                {
                  …
                }
            }
        };
        try
        {
            mIAsyncControl = CustomProtectedOutputStream.create(outputStream, mUserPolicy,
                    customProtectedOutputStreamCreationCallback);
        }
        catch (InvalidParameterException e)
        {
          …
        }

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
