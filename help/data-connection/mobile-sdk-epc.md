---
title: Integrare Adobe Experience Platform Mobile SDK con Commerce
description: Scopri come utilizzare l’SDK di Adobe Experience Platform Mobile con la tua vetrina commerciale headless o personalizzata.
role: Admin, Developer
feature: Personalization, Integration, Eventing
exl-id: d1340b15-e7de-42b5-ad64-d4c31f0db029
source-git-commit: 4a5877d6e1a5c7d840e36f4913306b0c440bbac5
workflow-type: tm+mt
source-wordcount: '532'
ht-degree: 0%

---

# Integrare Adobe Experience Platform Mobile SDK con Commerce

>[!IMPORTANT]
>
>L’SDK di Adobe Experience Platform Mobile per iOS supporta iOS 11 o versione successiva.

Integrazione di [SDK di Adobe Experience Platform Mobile](https://developer.adobe.com/client-sdks/home/) con l’app mobile di Commerce consente ai commercianti di inviare e-commerce  [dati evento](events.md) al bordo Experience Platform.

Quando i dati dell’evento Commerce sono disponibili al perimetro, sono accessibili ad altre applicazioni Adobe Experience Cloud. Ad esempio, puoi utilizzare i dati per creare tipi di pubblico in Real-Time CDP e quindi [utilizza tali tipi di pubblico](https://experienceleague.adobe.com/docs/commerce-admin/customers/audience-activation.html) per personalizzare la tua app mobile di Commerce.

## Configurazione

Per iniziare a utilizzare Adobe Experience Platform Mobile SDK con Commerce, installa e configura l’SDK nell’Experience Platform. Quindi, completa la configurazione in Commerce.

### Experience Platform

1. Scopri le funzionalità delle app mobili consultando il [Tutorial su Adobe Experience Cloud nelle app per dispositivi mobili](https://experienceleague.adobe.com/docs/platform-learn/implement-mobile-sdk/overview.html).

1. [Installare e configurare](https://developer.adobe.com/client-sdks/documentation/getting-started/) l’SDK in Experienci Platform.

   >[!NOTE]
   >
   >Lo schema creato e configurato nell’Experience Platform è lo stesso utilizzato nel codice dell’applicazione nell’app mobile Commerce.

### Commerce

Dopo aver completato la configurazione SDK per Experience Platform, aggiungi la configurazione SDK a Commerce.

1. Per inviare i dati dell’evento Commerce all’Experience Platform tramite l’SDK, devi fornire uno schema XDM nel codice dell’applicazione. Questo schema deve corrispondere allo schema [configurato](https://developer.adobe.com/client-sdks/home/getting-started/set-up-schemas-and-datasets/) per l’SDK nell’Experience Platform.

   L’esempio seguente mostra come tenere traccia di `web.webpagedetails.pageViews` e impostare `identityMap` utilizzando il campo e-mail.

   ```swift
   let stateName = "luma: content: ios: us: en: home"
   var xdmData: [String: Any] = [
       "eventType": "web.webpagedetails.pageViews",
       "web": [
           "webPageDetails": [
               "pageViews": [
                   "value": 1
               ],
               "name": "Home page"
           ]
       ]
   ]
   
   let experienceEvent = ExperienceEvent(xdm: xdmData)
   Edge.sendEvent(experienceEvent: experienceEvent)
   
   // Adobe Experience Platform - Update Identity
   
   let emailLabel = "mobileuser@example.com"
   
   let identityMap: IdentityMap = IdentityMap()
   identityMap.add(item: IdentityItem(id: emailLabel), withNamespace: "Email")
   Identity.updateIdentities(with: identityMap)
   ```

1. Connettersi all&#39;ambiente Commerce Cloud.

   Nelle impostazioni di build del progetto, aggiungi l’URL all’endpoint Commerce GraphQL. Ad esempio:

   - Debug: http://_debug_.commerce.cloud/graphql/
   - Versione: http://_versione_.commerce.cloud/graphql/

1. Per recuperare i dati dagli endpoint di Commerce GraphQL, genera innanzitutto i file e le directory necessari nel progetto utilizzando [Generatore di codice Apollo](https://www.apollographql.com/docs/ios/).

   1. Dalla directory del progetto, [installare](https://www.apollographql.com/docs/ios/get-started#1-install-the-apollo-frameworks) Apollo iOS.

   1. [Inizializza](https://www.apollographql.com/docs/ios/code-generation/codegen-cli/#initialize) Apollo Codegen CLI.

      Questo crea un `apollo-codegen-configuration.json` file.

   1. Genera i file e le directory GraphQL necessari nel progetto sostituendo il contenuto della `apollo-codegen-configuration.json` file con quanto segue:

      ```json
      {
      "schemaName" : "MagentoAPI",
      "input" : {
          "operationSearchPaths" : [
          "**/*.graphql"
          ],
          "schemaSearchPaths" : [
          "**/*.graphqls"
          ]
      },
      "output" : {
          "testMocks" : {
          "none" : {
          }
          },
          "schemaTypes" : {
          "path" : "../MagentoAPI",
          "moduleType" : {
              "swiftPackageManager" : {
              }
          }
          },
          "operations" : {
          "inSchemaModule" : {
          }
          }
      },
      "schemaDownloadConfiguration": {
          "downloadMethod": {
              "introspection": {
                  "endpointURL": "http://magento24.com/graphql/",
                  "httpMethod": {
                      "POST": {}
                  },
                  "includeDeprecatedInputValues": false,
                  "outputFormat": "SDL"
              }
          },
          "downloadTimeout": 60,
          "headers": [],
          "outputPath": "magento.graphqls"
      }
      }
      ```

   1. [Recupera](https://www.apollographql.com/docs/ios/code-generation/codegen-cli/#fetch-schema) lo schema Commerce GraphQL.

      Assicurati che il percorso sia `./apollo-codegen-config.json` , che contiene il riferimento allo schema Commerce GraphQL.

   1. [Genera](https://www.apollographql.com/docs/ios/code-generation/codegen-cli/#generate) il codice sorgente.

      Assicurati che il percorso sia `./apollo-codegen-config.json` , che contiene le informazioni di configurazione per generare i file e le directory necessari.

   1. All’interno del nuovo elemento creato **GraphQLGenerated** cartella, aggiungi o modifica tipi di GraphQL. Ad esempio, puoi aggiungere una `DynamicBlocks.graphql` digita con il seguente contenuto:

      ```graphql
      query dynamicBlocks($input: DynamicBlocksFilterInput){
          dynamicBlocks(input: $input)
          {
              items {
                  content {
                      html
                  }
              }
          }
      }
      ```

   Ora hai integrato l’SDK di Adobe Experience Platform Mobile con la tua app mobile Commerce. I dati dell’evento fluiscono dall’app all’edge dell’Experience Platform.

Per scoprire come recuperare i tipi di pubblico di Real-Time CDP dall’app Commerce mobile per informare le regole di prezzo del carrello e i blocchi dinamici, consulta [Audience Activation](https://experienceleague.adobe.com/docs/commerce-admin/customers/audience-activation.html).
