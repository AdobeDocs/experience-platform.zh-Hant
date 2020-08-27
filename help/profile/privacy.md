---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 即時客戶個人檔案中的隱私權要求處理
topic: overview
translation-type: tm+mt
source-git-commit: 1b398e479137a12bcfc3208d37472aae3d6721e1
workflow-type: tm+mt
source-wordcount: '603'
ht-degree: 0%

---


# 隱私權要求處理於 [!DNL Real-time Customer Profile]

Adobe Experience Platform會 [!DNL Privacy Service] 處理客戶存取、選擇退出銷售或刪除其個人資料的要求，這些要求由隱私權法規(例如通用資料保護規則(GDPR)和(CCPA))所規 [!DNL California Consumer Privacy Act] 定。

本檔案涵蓋處理隱私權要求的相關基本概念 [!DNL Real-time Customer Profile]。

## 快速入門

建議您在閱讀本指南之前，先瞭解下 [!DNL Experience Platform] 列服務：

* [[!DNL隱私服務]](home.md):管理客戶在Adobe Experience Cloud應用程式中存取、選擇退出銷售或刪除其個人資料的要求。
* [[!DNL Identity Service]](../identity-service/home.md):透過跨裝置和系統橋接身分，解決客戶體驗資料分散所帶來的根本挑戰。
* [[!DNL即時客戶基本資料]](../profile/home.md):根據來自多個來源的匯整資料，提供統一、即時的消費者個人檔案。

## 瞭解身分名稱空間 {#namespaces}

Adobe Experience Platform跨 [!DNL Identity Service] 系統和裝置橋接客戶身分資料。 [!DNL Identity Service] 使用 **身分名稱空間** ，將身分值與其來源系統關聯，以提供其上下文。 命名空間可以代表一般概念，例如電子郵件地址（「電子郵件」），或將身分識別與特定應用程式(例如Adobe Advertising Cloud ID(「AdCloud」)或Adobe Target ID(「TNTID」))建立關聯。

Identity Service會維護全域定義（標準）和使用者定義（自訂）身分名稱空間的儲存。 標準名稱空間適用於所有組織（例如「電子郵件」和「ECID」），而您的組織也可以建立自訂名稱空間以符合其特定需求。

有關中身份名稱空間的詳細信 [!DNL Experience Platform]息，請參閱身份 [名稱空間概述](../identity-service/namespaces.md)。

## 提交請求 {#submit}

>[!NOTE]
>
>本節說明如何建立資料存放區的隱私權 [!DNL Profile] 要求。 強烈建議您檢閱 [Privacy Service API](../privacy-service/api/getting-started.md) 或 [Privacy Service UI](../privacy-service/ui/overview.md) 檔案，以取得如何提交隱私權工作的完整步驟，包括如何在請求負載中正確格式化已提交的使用者身分資料。

下節將說明如何對使用API或UI的 [!DNL Real-time Customer Profile] 使用者 [!DNL Data Lake] 和使用者 [!DNL Privacy Service] 提出隱私權要求。

### 使用API

在API中建立工作請求時，所 `userIDs` 提供的任何作業請求都必須使用特 `namespace` 定 `type` 的作業請求，並視其套用的資料儲存區而定。 商店的ID [!DNL Profile] 必須使用「標準」或「自訂」做為其值， `type` 而有效的識別名稱空間必須由 [「標準」或](#namespaces) 「自訂」作為 [!DNL Identity Service]`namespace` 值。


此外，請求 `include` 裝載的陣列必須包含請求所針對之不同資料存放區的產品值。 向請求時，陣 [!DNL Data Lake]列必須包含「ProfileService」值。

下列要求會使用標準的「電子郵件」身分 [!DNL Real-time Customer Profile]名稱空間，為兩者建立新的隱私權工作。 它還包括陣列中 [!DNL Profile] 的產品 `include` 值：

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

在UI中建立工作請求時，請務必在 **[!UICONTROL Products下選擇]** AEP Data Lake **[!UICONTROL 和／或]** Profile __ Products下，以分別處理儲存在或 [!DNL Data Lake][!DNL Real-time Customer Profile]Products中的資料。

<img src="images/privacy/product-value.png" width="450"><br>

## 刪除請求處理

當收 [!DNL Experience Platform] 到刪除請求時， [!DNL Privacy Service]會傳送確認， [!DNL Platform][!DNL Privacy Service] 確認請求已收到且受影響的資料已標示為刪除。 然後在七天內將記錄 [!DNL Data Lake] 從或 [!DNL Profile] 儲存中移除。 在這七天的視窗中，資料會被軟刪除，因此無法由任何服務存取 [!DNL Platform] 。

在未來版本中， [!DNL Platform] 將在實際刪除資 [!DNL Privacy Service] 料後傳送確認給。

## 後續步驟

閱讀本檔案後，您便瞭解了處理中隱私權要求的重要概念 [!DNL Experience Platform]。 建議您繼續閱讀本指南中提供的檔案，以加深您對如何管理身分資料和建立隱私權工作的瞭解。

如需處理非使用之資源之隱 [!DNL Platform] 私權要求的詳細資 [!DNL Profile]訊，請參閱資料 [湖中隱私權要求處理的檔案](../catalog/privacy.md)。