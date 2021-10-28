---
keywords: Experience Platform；首頁；熱門主題
title: Identity Service中的隱私權要求處理
description: Adobe Experience Platform Privacy Service會處理客戶存取、選擇退出銷售或刪除其個人資料的請求，這些資料是多項隱私權法規所規定。 本檔案涵蓋與處理Identity Service隱私權要求相關的基本概念。
source-git-commit: 49f5de6c4711120306bfc3e6759ed4e83e8a19c2
workflow-type: tm+mt
source-wordcount: '666'
ht-degree: 1%

---


# 中的隱私權要求處理 [!DNL Identity Service]

Adobe Experience Platform [!DNL Privacy Service] 處理客戶要求存取、選擇退出銷售或刪除其隱私權法規(例如一般資料保護規範(GDPR))所規定之個人資料的請求，並 [!DNL California Consumer Privacy Act] (CCPA)。

本檔案涵蓋處理隱私權要求的相關基本概念 [!DNL Identity Service] 在Adobe Experience Platform。

>[!NOTE]
>
>本指南僅說明如何針對Experience Platform中的身分資料存放區提出隱私權要求。 如果您也打算向Platform Data Lake或 [!DNL Real-time Customer Profile]，請參閱的指南 [資料湖中的隱私權要求處理](../catalog/privacy.md) 和指南 [設定檔的隱私權要求處理](../profile/privacy.md) 除了本教學課程之外。
>
>如需如何為其他Adobe Experience Cloud應用程式提出隱私權要求的步驟，請參閱 [Privacy Service檔案](../privacy-service/experience-cloud-apps.md).

## 快速入門

建議您對下列事項有切實的了解 [!DNL Experience Platform] 服務，再閱讀本指南：

* [[!DNL Privacy Service]](../privacy-service/home.md):管理客戶在Adobe Experience Cloud應用程式中存取、選擇退出銷售或刪除其個人資料的請求。
* [[!DNL Identity Service]](../identity-service/home.md):通過跨裝置和系統橋接身分，解決客戶體驗資料分散帶來的根本難題。
* [[!DNL Real-time Customer Profile]](home.md):根據來自多個來源的匯總資料，提供統一的即時消費者設定檔。

## 了解身分識別命名空間 {#namespaces}

Adobe Experience Platform [!DNL Identity Service] 橋接跨系統和裝置的客戶身分資料。 [!DNL Identity Service] uses **身分識別命名空間** 將身份值與其來源系統關聯，以提供其內容。 命名空間可代表一般概念，例如電子郵件地址（「電子郵件」），或將身分識別與特定應用程式建立關聯，例如Adobe Advertising Cloud ID(「AdCloud」)或Adobe Target ID(「TNTID」)。

Identity Service會維護全域定義（標準）和使用者定義（自訂）身分識別命名空間的存放區。 所有組織皆可使用標準命名空間（例如「電子郵件」和「ECID」），而您的組織也可以建立自訂命名空間，以符合其特定需求。

如需中身分識別命名空間的詳細資訊，請參閱 [!DNL Experience Platform]，請參閱 [身分命名空間概述](../identity-service/namespaces.md).

## 提交請求 {#submit}

以下各節將說明如何向 [!DNL Identity Service] 使用 [!DNL Privacy Service] API或UI。 閱讀這些章節之前，強烈建議您檢閱 [Privacy ServiceAPI](../privacy-service/api/getting-started.md) 或 [Privacy ServiceUI](../privacy-service/ui/overview.md) 說明檔案，以取得如何提交隱私權工作的完整步驟，包括如何在要求裝載中正確格式化使用者資料。

### 使用 API

在API中建立工作請求時， `userIDs` 必須使用特定 `namespace` 和 `type`. 有效 [身分命名空間](#namespaces) 確認 [!DNL Identity Service] 必須為 `namespace` 值，而 `type` 必須為 `standard` 或 `unregistered` （適用於標準和自訂命名空間）。

此外， `include` 要求裝載的陣列必須包含要提出要求之不同資料存放區的產品值。 向 [!DNL Identity]，陣列必須包含值 `Identity`.

下列要求會在GDPR下針對 [!DNL Identity] 儲存。 中為客戶提供兩個身分值，位於 `userIDs` 陣列；使用標準 `Email` 身分命名空間，而另一個使用 `ECID` 命名空間，也包含 [!DNL Identity] (`Identity`) `include` 陣列：

```shell
curl -X POST \
  https://platform.adobe.io/data/core/privacy/jobs \
  -H 'Authorization: Bearer <key>' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: acp_privacy_ui_gdpr' \
  -H 'x-gw-ims-org-id: sample@AdobeOrg' \
  -d '{
    "companyContexts": [
      {
        "namespace": "imsOrgID",
        "value": "sample@AdobeOrg"
      }
    ],
    "users": [
      {
        "key": "bob",
        "action": ["delete"],
        "userIDs": [
          {
            "namespace": "email",
            "value": "bob@adobe.com",
            "type": "standard"
          },
          {
            "namespace": "ECID",
            "type": "standard",
            "value":  "123451234512345123451234512345",
            "isDeletedClientSide": false
          }
        ]
      }
    ],
    "include": ["Identity"],
    "regulation": "gdpr"
}'
```

### 使用UI

在UI中建立工作請求時，請務必選取 **[!UICONTROL 身分]** 在 **[!UICONTROL 產品]** 以處理儲存於 [!DNL Identity Service].

![identity-gdpr](./images/identity-gdpr.png)

## 刪除請求處理

當 [!DNL Experience Platform] 從接收刪除請求 [!DNL Privacy Service], [!DNL Platform] 發送確認 [!DNL Privacy Service] 已收到請求，且受影響的資料已標示為刪除。 個別身分的刪除是根據提供的命名空間及/或ID值。 此外，會刪除與指定IMS組織相關聯的所有沙箱。

## 後續步驟

閱讀本檔案後，您便了解處理隱私權要求的重要概念，如 [!DNL Identity Service]. 如需處理其他隱私權要求的相關資訊， [!DNL Experience Cloud] 應用程式，請參閱 [[!DNL Privacy Service] and [!DNL Experience Cloud] 應用程式](../privacy-service/experience-cloud-apps.md).