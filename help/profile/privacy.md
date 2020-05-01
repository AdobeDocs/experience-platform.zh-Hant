---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 即時客戶個人檔案中的隱私權要求處理
topic: overview
translation-type: tm+mt
source-git-commit: cc296670db91640e75fd7a47b874a46eaf57ecde

---


# 即時客戶個人檔案中的隱私權要求處理

Adobe Experience Platform隱私服務會處理客戶存取、選擇退出銷售或刪除其個人資料的要求，這些資料由隱私權法規(例如通用資料保護規則(GDPR)和加州消費者隱私法(CCPA)規定。

本檔案涵蓋處理即時客戶個人檔案隱私權要求的相關基本概念。

## 快速入門

建議您在閱讀本指南之前，先瞭解下列Experience Platform服務：

* [隱私權服務](home.md): 管理客戶在Adobe Experience Cloud應用程式中存取、選擇退出銷售或刪除其個人資料的要求。
* [身分服務](../identity-service/home.md): 透過跨裝置和系統橋接身分，解決客戶體驗資料分散所帶來的根本挑戰。
* [即時客戶個人檔案](../profile/home.md): 根據來自多個來源的匯整資料，提供統一、即時的消費者個人檔案。

## 瞭解身分名稱空間 {#namespaces}

Adobe Experience Platform Identity Service可跨系統和裝置橋接客戶身分資料。 身分服務使用 **身分名稱空間** ，將身分值與其來源系統關聯，以提供其上下文。 命名空間可以代表一般概念，例如電子郵件地址（「電子郵件」），或將身分識別與特定應用程式(例如Adobe Advertising Cloud ID(「AdCloud」)或Adobe Target ID(「TNTID」))建立關聯。

Identity Service會維護全域定義（標準）和使用者定義（自訂）身分名稱空間的儲存。 標準名稱空間適用於所有組織（例如「電子郵件」和「ECID」），而您的組織也可以建立自訂名稱空間，以符合其特定需求。

如需Experience Platform中身分名稱空間的詳細資訊，請參閱身分 [名稱空間概觀](../identity-service/namespaces.md)。

## 提交請求 {#submit}

>[!NOTE] 本節說明如何建立描述檔資料存放區的隱私權要求。 強烈建議您檢閱 [Privacy Service API](../privacy-service/api/getting-started.md) 或 [Privacy Service UI](../privacy-service/ui/overview.md) 檔案，以取得如何提交隱私權工作的完整步驟，包括如何在請求負載中正確格式化已提交的使用者身分資料。

下節將說明如何使用隱私權服務API或UI，對即時客戶個人檔案和資料湖提出隱私權要求。

### 使用API

在API中建立工作請求時，所 `userIDs` 提供的任何作業請求都必須使用特 `namespace` 定 `type` 的作業請求，並視其套用的資料儲存區而定。 描述檔商店的ID必須使用「標準」或「自訂」做為其 `type` 值，而Identity Service必須識別有 [效的身分命名空間](#namespaces) ，做為其 `namespace` 值。


此外，請求 `include` 裝載的陣列必須包含請求所針對之不同資料存放區的產品值。 向Data Lake請求時，陣列必須包含值&quot;ProfileService&quot;。

下列要求會使用標準的「電子郵件」身分名稱空間，為即時客戶個人檔案建立新的隱私權工作。 它還包括陣列中Profile的產品 `include` 值：

```shell
curl -X POST \
  https://platform.adobe.io/data/core/privacy/jobs \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
            "namespace": "email_label",
            "value": "ajones@acme.com",
            "type": "unregistered"
          }
        ]
      }
    ],
    "include": ["ProfileService", "aepDataLake"],
    "expandIds": false,
    "priority": "normal",
    "analyticsDeleteMethod": "anonymize",
    "regulation": "ccpa"
}'
```

### 使用UI

在UI中建立工作請求時，請務必在 **Products下選取** AEP Data Lake **和／或** Profile __ ，以便分別處理儲存在Data Lake或Real-time Customer Profile中的資料的工作。

<img src="images/privacy/product-value.png" width="450"><br>

## 刪除請求處理

當Experience Platform收到來自隱私權服務的刪除要求時，平台會向隱私權服務傳送確認該要求已收到且受影響的資料已標示為刪除。 然後在7天內，這些記錄會從資料湖或描述檔儲存區中移除。 在該七天的時段內，資料會被軟刪除，因此無法由任何平台服務存取。

在未來版本中，平台會在實際刪除資料後傳送確認給隱私權服務。

## 後續步驟

閱讀本檔案，您就瞭解了在Experience Platform中處理隱私權要求的重要概念。 建議您繼續閱讀本指南中提供的檔案，以加深您對如何管理身分資料和建立隱私權工作的瞭解。

如需處理非設定檔使用之平台資源之隱私權要求的詳細資訊，請參閱資料 [湖中的隱私權要求處理檔案](../catalog/privacy.md)。