---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 即時客戶個人檔案中的隱私權要求處理
topic: overview
translation-type: tm+mt
source-git-commit: 066337419431db24bde0a8d0d30b85132d08f43c
workflow-type: tm+mt
source-wordcount: '1058'
ht-degree: 0%

---


# 隱私權要求處理於 [!DNL Real-time Customer Profile]

Adobe Experience Platform會 [!DNL Privacy Service] 處理客戶存取、選擇退出銷售或刪除其個人資料的要求，這些要求由隱私權法規(例如通用資料保護規則(GDPR)和(CCPA))所規 [!DNL California Consumer Privacy Act] 定。

本檔案涵蓋處理隱私權要求的相關基本概念 [!DNL Real-time Customer Profile]。

## 快速入門

建議您在閱讀本指南之前，先瞭解下 [!DNL Experience Platform] 列服務：

* [[!DNL Privacy Service]](home.md):管理客戶在Adobe Experience Cloud應用程式中存取、選擇退出銷售或刪除其個人資料的要求。
* [[!DNL Identity Service]](../identity-service/home.md):透過跨裝置和系統橋接身分，解決客戶體驗資料分散所帶來的根本挑戰。
* [[!DNL Real-time Customer Profile]](../profile/home.md):根據來自多個來源的匯整資料，提供統一、即時的消費者個人檔案。

## 瞭解身分名稱空間 {#namespaces}

Adobe Experience Platform跨 [!DNL Identity Service] 系統和裝置橋接客戶身分資料。 [!DNL Identity Service] 使用 **身分名稱空間** ，將身分值與其來源系統關聯，以提供其上下文。 命名空間可以代表一般概念，例如電子郵件地址（「電子郵件」），或將身分識別與特定應用程式(例如Adobe Advertising Cloud ID(「AdCloud」)或Adobe Target ID(「TNTID」))建立關聯。

Identity Service會維護全域定義（標準）和使用者定義（自訂）身分名稱空間的儲存。 標準名稱空間適用於所有組織（例如「電子郵件」和「ECID」），而您的組織也可以建立自訂名稱空間以符合其特定需求。

有關中身份名稱空間的詳細信 [!DNL Experience Platform]息，請參閱身份 [名稱空間概述](../identity-service/namespaces.md)。

## 提交請求 {#submit}

以下各節概述如何使用API或UI [!DNL Real-time Customer Profile] 提出 [!DNL Privacy Service] 隱私權要求。 在閱讀這些章節之前，強烈建議您檢閱 [Privacy Service API](../privacy-service/api/getting-started.md) 或 [Privacy Service UI](../privacy-service/ui/overview.md) 檔案，以取得如何提交隱私權工作的完整步驟，包括如何在請求負載中正確格式化已提交的使用者身分資料。

>[!IMPORTANT]
>
>隱私服務只能使用不執行 [!DNL Profile] 身分聯繫的合併原則處理資料。 如果您使用UI來確認是否正在處理您的隱私權要求，請確定您使用的原則是「[!DNL None]」作為 [!UICONTROL ID連結類型] 。 換言之，您無法使用將 [!UICONTROL ID接合設為] 「私用[!UICONTROL 圖形]」的合併原則。
>
>![](./images/privacy/no-id-stitch.png)
>
>此外，請務必注意，無法保證隱私權要求完成所需的時間。 如果在請求仍在處 [!DNL Profile] 理時，您的資料中發生變更，則無法保證這些記錄是否已處理。

### 使用API

在API中建立工作請求時，任何ID中提供 `userIDs` 的ID都必須使用特 `namespace` 定和 `type`。 必須為 [值提供可識別的有效](#namespaces) 身分名稱空間 [!DNL Identity Service] ，而值必須為 `namespace` 或( `type``standard``unregistered` 分別針對標準和自訂名稱空間)。

>[!NOTE]
>
>您可能需要為每個客戶提供多個ID，具體取決於身份圖表，以及您的配置檔案片段在Platform資料集中的分佈方式。 如需詳細資訊，請參 [閱下一節](#fragments) ，描述檔片段。

此外，請求 `include` 裝載的陣列必須包含請求所針對之不同資料存放區的產品值。 向請求時，陣 [!DNL Data Lake]列必須包含「ProfileService」值。

下列要求會針對商店中的單一客戶資料建立新的隱私權 [!DNL Profile] 工作。 陣列中為客戶提供了兩個身份 `userIDs` 值；一個使用標準 `Email` 識別名稱空間，另一個使用自訂名稱 `Customer_ID` 空間。 它還包括陣列中( [!DNL Profile]`ProfileService`)的產品 `include` 值：

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

在UI中建立工作請求時，請務必在 **[!UICONTROL Products下選擇]** AEP Data Lake **[!UICONTROL 和／或]** Profile **** Products下，以分別處理儲存在或 [!DNL Data Lake][!DNL Real-time Customer Profile]Products中的資料。

<img src="images/privacy/product-value.png" width="450"><br>

## 隱私權要求中的描述檔片段 {#fragments}

在資料 [!DNL Profile] 儲存中，個別客戶的個人資料通常由多個描述檔片段組成，這些片段是透過識別圖表與個人關聯。 向商店提出隱私權要 [!DNL Profile] 求時，請務必注意，請求只會在描述檔片段層級處理，而非整個描述檔。

例如，假設您將客戶屬性資料儲存在三個不同的資料集中，這些資料集使用不同的識別碼將該資料與個別客戶關聯：

| 資料集名稱 | 主要身分欄位 | 儲存的屬性 |
| --- | --- | --- |
| 資料集1 | `customer_id` | `address` |
| 資料集2 | `email_id` | `firstName`, `lastName` |
| 資料集3 | `email_id` | `mlScore` |

其中一個資料集使 `customer_id` 用其主要識別碼，而另兩個資料集則使用 `email_id`。 如果您僅使用使用者ID值來傳送隱私權要求（存取或刪除） `email_id` ，則只會處理 `firstName`、 `lastName`和 `mlScore` 屬性， `address` 而不會受到影響。

為確保您的隱私權要求能處理所有相關客戶屬性，您必須針對所有可儲存這些屬性的適用資料集提供主要識別值（每位客戶最多9個ID）。 有關通常標示為身份的欄位的 [詳細資訊，請參閱架構構成基礎中有關身份欄位的部分](../xdm/schema/composition.md#identity) 。

>[!NOTE]
>
>如果您使用不同的沙 [盒來儲存資](../sandboxes/home.md) 料 [!DNL Profile] ，則必須針對每個沙盒提出個別的隱私權要求，並在標題中指出適當的沙盒 `x-sandbox-name` 名稱。

## 刪除請求處理

當收 [!DNL Experience Platform] 到刪除請求時， [!DNL Privacy Service]會傳送確認， [!DNL Platform][!DNL Privacy Service] 確認請求已收到且受影響的資料已標示為刪除。 一旦隱私權工作完成，記 [!DNL Data Lake] 錄就 [!DNL Profile] 會從或商店中移除。 雖然刪除作業仍在處理中，但是資料是軟刪除的，因此任何服務都無法存取 [!DNL Platform] 資料。 如需追蹤工作 [[!DNL Privacy Service] 狀態的詳細資訊](../privacy-service/home.md#monitor) ，請參閱檔案。

>[!IMPORTANT]
>
>成功的刪除請求會移除客戶（或一組客戶）的收集屬性資料，但請求不會移除在識別圖中建立的關聯。
>
>例如，使用客戶的刪除請求，並移除儲 `email_id` 存在 `customer_id` 這些ID下的所有屬性資料。 但是，隨後在相同資料下提取的任何數 `customer_id` 據仍與相應資料相關聯，因 `email_id`為該關聯仍然存在。

在未來版本中， [!DNL Platform] 將在實際刪除資 [!DNL Privacy Service] 料後傳送確認給。

## 後續步驟

閱讀本檔案後，您便瞭解了處理中隱私權要求的重要概念 [!DNL Experience Platform]。 建議您繼續閱讀本指南中提供的檔案，以加深您對如何管理身分資料和建立隱私權工作的瞭解。

如需處理非使用之資源之隱 [!DNL Platform] 私權要求的詳細資 [!DNL Profile]訊，請參閱資料 [湖中隱私權要求處理的檔案](../catalog/privacy.md)。