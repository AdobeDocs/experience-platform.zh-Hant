---
title: Salesforce Marketing Cloud Source概觀
description: 瞭解如何使用API或使用者介面將Salesforce Marketing Cloud連線至Adobe Experience Platform。
exl-id: 2177d68c-0cef-4031-a0e7-8bf22ee2e70b
last-substantial-update: 2025-05-17T00:00:00Z
source-git-commit: 0c0a58df4beae499008e52c118b40bed86ff0596
workflow-type: tm+mt
source-wordcount: '664'
ht-degree: 1%

---

# [!DNL Salesforce Marketing Cloud]

>[!WARNING]
>
>[!DNL Salesforce Marketing Cloud]來源將於2026年1月汰除。 新的來源將作為替代方案於今年晚些時候發行。 釋放新來源後，您必須在2026年1月底之前建立新的帳戶連線和資料流，以計畫移轉至新來源。

[!DNL Salesforce Marketing Cloud]可讓您從單一平台管理電子郵件、行動裝置、社群媒體和廣告的客戶參與並使其自動化。 使用Email Studio、Journey Builder和Audience Builder等工具，您可以建立針對對象量身打造的個人化行銷活動和客戶歷程。

您可以使用[!DNL Salesforce Marketing Cloud]來源來連線您的帳戶，並將您的資料帶到Adobe Experience Platform。

## 先決條件

在將[!DNL Salesforce Marketing Cloud]來源連線至Experience Platform之前，您必須確定下列&#x200B;**許可權範圍**&#x200B;已布建至您的[!DNL Salesforce Marketing Cloud]使用者端ID和使用者端密碼組合：

* `campaign_read`
* `list_and_subscribers_read`

您可以呼叫[!DNL Salesforce Marketing Cloud] API的`v2/userinfo`資源來要求範圍。 如需如何要求與比較範圍的指引，請參閱[[!DNL Salesforce Marketing Cloud] API整合許可權範圍檔案](<https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/data-access-permissions.html>)。

如需有關範圍的詳細資訊，包括其相關許可權和行為清單，請參閱此[[!DNL Salesforce Marketing Cloud] REST API檔案](<https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/rest-permissions-and-scopes.html>)。

>[!IMPORTANT]
>
>[!DNL Salesforce Marketing Cloud]來源整合目前不支援自訂物件擷取。

### IP位址允許清單

將來源連線至Experience Platform之前，您必須先將區域特定的IP位址新增至允許清單。 如需詳細資訊，請參閱[允許清單IP位址以連線至Experience Platform](../../ip-address-allow-list.md)的指南以瞭解詳細資訊。

>[!WARNING]
>
>如果您未將必要的IP位址新增至允許清單，您的[!DNL Salesforce Marketing Cloud]帳戶將不會連線至Experience Platform。

### 在Azure上驗證Experience Platform {#azure}

您必須提供下列認證的值，才能將[!DNL Salesforce Marketing Cloud]連線至[!DNL Azure]上的Experience Platform。

| 認證 | 說明 |
| --- | --- |
| Host | 應用程式的主機伺服器。 這通常是您的子網域。 **注意：**&#x200B;輸入`host`值時，您必須指定`{subdomain}.rest.marketingcloudapis.com`。 例如，如果您的主機URL是`https://acme-ab12c3d4e5fg6hijk7lmnop8qrst.auth.marketingcloudapis.com/`，則必須輸入`acme-ab12c3d4e5fg6hijk7lmnop8qrst.rest.marketingcloudapis.com/`作為主機值。 |
| 用戶端 ID | 與您的[!DNL Salesforce Marketing Cloud]應用程式關聯的使用者端識別碼。 |
| 用戶端密碼 | 與您的[!DNL Salesforce Marketing Cloud]應用程式關聯的使用者端密碼。 |
| 連線規格ID | **連線規格**&#x200B;提供資料來源的聯結器屬性。 這包含驗證規格等詳細資訊，以及建立&#x200B;**基底**&#x200B;和&#x200B;**來源**&#x200B;連線的需求。 針對[!DNL Salesforce Marketing Cloud]，連線規格ID為： `ea1c2a08-b722-11eb-8529-0242ac130003`。 **注意：**&#x200B;只有在透過API連線時才需要此認證。 |

### 在Amazon Web Services (AWS)上驗證Experience Platform {#aws}

>[!AVAILABILITY]
>
>本節適用於在Amazon Web Services (AWS)上執行的Experience Platform實作。 目前有限數量的客戶可使用在AWS上執行的Experience Platform 。 若要進一步瞭解支援的Experience Platform基礎結構，請參閱[Experience Platform多雲端總覽](../../../landing/multi-cloud.md)。

您必須提供下列認證的值，才能將[!DNL Salesforce Marketing Cloud]連線至AWS上的Experience Platform。

| 認證 | 說明 |
| --- | --- |
| 子網域 | [!DNL Salesforce Marketing Cloud]執行個體的URL的唯一部分，用來建構API端點。 |
| 用戶端 ID | 應用程式的公用識別碼，當您在[!DNL Salesforce Marketing Cloud]中建立已安裝的套件時產生 |
| 用戶端密碼 | 與您的使用者端ID相關聯的機密金鑰，也在已安裝的套件中產生。 |
| 連線規格ID | **連線規格**&#x200B;提供資料來源的聯結器屬性。 這包含驗證規格等詳細資訊，以及建立&#x200B;**基底**&#x200B;和&#x200B;**來源**&#x200B;連線的需求。 針對[!DNL Salesforce Marketing Cloud]，連線規格ID為： `ea1c2a08-b722-11eb-8529-0242ac130003`。 **注意：**&#x200B;只有在透過API連線時才需要此認證。 |

如需詳細資訊，請閱讀伺服器對伺服器整合之存取權杖的[[!DNL Salesforce] 檔案](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/access-token-s2s.html)。

## 使用API連線[!DNL Salesforce Marketing Cloud]至Experience Platform

以下檔案提供如何使用API將[!DNL Salesforce Marketing Cloud]連線至Experience Platform的資訊：

* [使用流量服務API連線 [!DNL Salesforce Marketing Cloud] 至Experience Platform](../../tutorials/api/create/marketing-automation/salesforce-marketing-cloud.md)
* [使用流量服務API探索資料表](../../tutorials/api/explore/tabular.md)
* [使用流量服務API為行銷自動化來源建立資料流](../../tutorials/api/collect/marketing-automation.md)

## 使用UI連線[!DNL Salesforce Marketing Cloud]至Experience Platform

以下檔案提供如何使用使用者介面將[!DNL Salesforce Marketing Cloud]連線至Experience Platform的相關資訊：

* [在UI中連線 [!DNL Salesforce Marketing Cloud] 至Experience Platform](../../tutorials/ui/create/marketing-automation/salesforce-marketing-cloud.md)
* [在UI中建立行銷自動化來源連線的資料流](../../tutorials/ui/dataflow/marketing-automation.md)
