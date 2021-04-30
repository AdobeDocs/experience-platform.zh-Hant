---
keywords: Experience Platform；首頁；熱門主題
solution: Experience Platform
title: 即時客戶個人檔案中的隱私權要求處理
type: Documentation
description: Adobe Experience Platform Privacy Service公司處理客戶存取、選擇退出銷售或刪除其個人資料的要求，這些資料由許多隱私權法規所界定。 本檔案涵蓋處理即時客戶個人檔案隱私權要求的相關基本概念。
exl-id: fba21a2e-aaf7-4aae-bb3c-5bd024472214
translation-type: tm+mt
source-git-commit: 8d16a3030c663d40daed6c5105af07b2d2d5c7bf
workflow-type: tm+mt
source-wordcount: '1091'
ht-degree: 0%

---

# [!DNL Real-time Customer Profile]中的隱私權要求處理

Adobe Experience Platform[!DNL Privacy Service]處理客戶存取、選擇退出銷售或刪除其個人資料的要求，如一般資料保護規則(GDPR)和[!DNL California Consumer Privacy Act](CCPA)等隱私權法規所規定。

本檔案涵蓋處理[!DNL Real-time Customer Profile]隱私權要求的相關基本概念。

## 快速入門

建議您在閱讀本指南之前，先瞭解以下[!DNL Experience Platform]服務：

* [[!DNL Privacy Service]](../privacy-service/home.md):管理客戶在Adobe Experience Cloud應用程式中存取、選擇退出銷售或刪除其個人資料的要求。
* [[!DNL Identity Service]](../identity-service/home.md):透過跨裝置和系統橋接身分，解決客戶體驗資料分散所帶來的根本挑戰。
* [[!DNL Real-time Customer Profile]](home.md):根據來自多個來源的匯整資料，提供統一、即時的消費者個人檔案。

## 瞭解身份名稱空間{#namespaces}

Adobe Experience Platform[!DNL Identity Service]跨系統和設備橋接客戶身份資料。 [!DNL Identity Service] 使用 **身** 分名稱，將身分值與其來源系統關聯，以提供其上下文。命名空間可以代表一般概念，例如電子郵件地址（「電子郵件」），或將識別與特定應用程式(例如Adobe Advertising CloudID(「AdCloud」)或Adobe TargetID(「TNTID」))建立關聯。

Identity Service會維護全域定義（標準）和使用者定義（自訂）身分名稱空間的儲存。 標準名稱空間適用於所有組織（例如「電子郵件」和「ECID」），而您的組織也可以建立自訂名稱空間以符合其特定需求。

有關[!DNL Experience Platform]中身份名稱空間的詳細資訊，請參閱[身份名稱空間概述](../identity-service/namespaces.md)。

## 提交請求{#submit}

以下各節概述如何使用[!DNL Privacy Service] API或UI對[!DNL Real-time Customer Profile]提出隱私權要求。 在閱讀這些章節之前，強烈建議您檢閱[Privacy ServiceAPI](../privacy-service/api/getting-started.md)或[Privacy ServiceUI](../privacy-service/ui/overview.md)檔案，以取得如何提交隱私權工作的完整步驟，包括如何在請求負載中正確格式化提交的使用者身分資料。

>[!IMPORTANT]
>
>Privacy Service只能使用不執行身分拼接的合併策略處理[!DNL Profile]資料。 如果您使用UI來確認是否正在處理您的隱私權要求，請確定您使用的原則為&quot;[!DNL None]&quot;，作為其[!UICONTROL ID stitching]類型。 換言之，您無法使用將[!UICONTROL ID stitching]設為&quot;[!UICONTROL Private graph]&quot;的合併原則。
>
>![](./images/privacy/no-id-stitch.png)
>
>此外，請務必注意，無法保證隱私權要求完成所需的時間。 如果在請求仍在處理時您的[!DNL Profile]資料中發生變更，則無法保證這些記錄是否已處理。

### 使用 API

在API中建立工作請求時，`userIDs`中提供的任何ID都必須使用特定的`namespace`和`type`。 必須為`namespace`值提供由[!DNL Identity Service]識別名稱空間](#namespaces)的有效值，而`type`必須為`standard`或`unregistered`（對於標準名稱空間和自訂名稱空間分別）。[

>[!NOTE]
>
>您可能需要為每個客戶提供多個ID，具體取決於身份圖表，以及您的配置檔案片段在Platform資料集中的分佈方式。 如需詳細資訊，請參閱下一節[描述檔片段](#fragments)。

此外，請求裝載的`include`陣列必須包含請求所針對之不同資料存放區的產品值。 向[!DNL Data Lake]發出請求時，陣列必須包含值&quot;ProfileService&quot;。

以下請求會在[!DNL Profile]商店中為單一客戶的資料建立新的隱私權工作。 `userIDs`陣列中為客戶提供了兩個標識值；一個使用標準`Email`識別名稱空間，另一個使用自訂`Customer_ID`名稱空間。 它還包括`include`陣列中[!DNL Profile](`ProfileService`)的產品值：

```shell
curl -X POST \
  https://platform.adobe.io/data/core/privacy/jobs \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "companyContexts": [
      {
        "namespace": "imsOrgID",
        "value": "{IMS_ORG}"
      }
    ],
    "users": [
      {
        "key": "user12345",
        "action": ["access","delete"],
        "userIDs": [
          {
            "namespace": "Email",
            "value": "ajones@acme.com",
            "type": "standard"
          },
          {
            "namespace": "Customer_ID",
            "value": "12345678",
            "type": "unregistered"
          }
        ]
      }
    ],
    "include": ["ProfileService"],
    "expandIds": false,
    "priority": "normal",
    "analyticsDeleteMethod": "anonymize",
    "regulation": "ccpa"
}'
```

### 使用UI

在UI中建立作業請求時，請務必在&#x200B;**[!UICONTROL Products]**&#x200B;下選擇&#x200B;**[!UICONTROL AEP Data Lake]**&#x200B;和／或&#x200B;**[!UICONTROL Profile]**，以便分別處理儲存在[!DNL Data Lake]或[!DNL Real-time Customer Profile]中的資料的作業。

<img src="images/privacy/product-value.png" width="450"><br>

## 隱私權要求中的描述檔片段{#fragments}

在[!DNL Profile]資料儲存區中，個別客戶的個人資料通常會由多個描述檔片段組成，這些片段會透過識別圖表與個人關聯。 在向[!DNL Profile]商店提出隱私權要求時，請務必注意，要求僅會在描述檔片段層級處理，而非整個描述檔。

例如，假設您將客戶屬性資料儲存在三個不同的資料集中，這些資料集使用不同的識別碼將該資料與個別客戶關聯：

| 資料集名稱 | 主要身分欄位 | 儲存的屬性 |
| --- | --- | --- |
| 資料集1 | `customer_id` | `address` |
| 資料集2 | `email_id` | `firstName`, `lastName` |
| 資料集3 | `email_id` | `mlScore` |

其中一個資料集使用`customer_id`作為其主要標識符，而另兩個資料集使用`email_id`。 如果您僅使用`email_id`作為用戶ID值來傳送隱私權要求（存取或刪除），則只會處理`firstName`、`lastName`和`mlScore`屬性，而不會影響`address`。

為確保您的隱私權要求能處理所有相關客戶屬性，您必須針對所有可儲存這些屬性的適用資料集提供主要識別值（每位客戶最多9個ID）。 有關通常標籤為身份的欄位的詳細資訊，請參閱[架構構成基礎](../xdm/schema/composition.md#identity)中有關身份欄位的部分。

>[!NOTE]
>
>如果您使用不同的[沙盒](../sandboxes/home.md)來儲存[!DNL Profile]資料，您必須針對每個沙盒提出個別的隱私權要求，指出`x-sandbox-name`標題中適當的沙盒名稱。

## 刪除請求處理

當[!DNL Experience Platform]收到[!DNL Privacy Service]的刪除請求時，[!DNL Platform]會向[!DNL Privacy Service]發送確認請求已接收且受影響的資料已標籤為刪除。 一旦隱私權作業完成，記錄便會從[!DNL Data Lake]或[!DNL Profile]商店中移除。 當刪除作業仍在處理時，資料被軟刪除，因此任何[!DNL Platform]服務都無法訪問。 有關跟蹤作業狀態的詳細資訊，請參閱[[!DNL Privacy Service] 文檔](../privacy-service/home.md#monitor)。

>[!IMPORTANT]
>
>成功的刪除請求會移除客戶（或一組客戶）的收集屬性資料，但請求不會移除在識別圖中建立的關聯。
>
>例如，使用客戶的`email_id`和`customer_id`的刪除請求會刪除這些ID下儲存的所有屬性資料。 但是，隨後在相同`customer_id`下收錄的任何資料仍與相應的`email_id`相關聯，因為該關聯仍然存在。

在未來版本中，[!DNL Platform]會在實際刪除資料後傳送確認給[!DNL Privacy Service]。

## 後續步驟

閱讀本檔案後，您便瞭解處理[!DNL Experience Platform]中隱私權要求的重要概念。 建議您繼續閱讀本指南中提供的檔案，以加深您對如何管理身分資料和建立隱私權工作的瞭解。

如需處理[!DNL Platform]資源之隱私權要求的詳細資訊，請參閱資料湖](../catalog/privacy.md)中有關[隱私權要求處理的檔案。[!DNL Profile]
