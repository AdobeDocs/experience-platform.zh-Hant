---
keywords: Experience Platform；首頁；熱門主題
title: 身份服務中的隱私請求處理
description: Adobe Experience Platform Privacy Service處理客戶訪問、選擇退出銷售或刪除其個人資料的請求，這些資料由許多隱私法規規定。 本文檔涵蓋與處理Identity Service的隱私請求相關的基本概念。
exl-id: ab84450b-1a4b-4fdd-b77d-508c86bbb073
source-git-commit: 159a46fa227207bf161100e50bc286322ba2d00b
workflow-type: tm+mt
source-wordcount: '1038'
ht-degree: 0%

---

# 隱私請求處理 [!DNL Identity Service]

Adobe Experience Platform [!DNL Privacy Service] 處理客戶訪問、選擇不銷售或刪除其個人資料的請求，如一般資料保護法規(GDPR)和 [!DNL California Consumer Privacy Act] (CCPA)。

本文檔涵蓋與處理針對 [!DNL Identity Service] 在Adobe Experience Platform。

>[!NOTE]
>
>本指南僅介紹如何對Experience Platform中的Identity資料儲存進行隱私請求。 如果您還計畫對平台資料湖或 [!DNL Real-time Customer Profile]，請參閱上的指南 [資料湖中的隱私請求處理](../catalog/privacy.md) 和指南 [配置檔案的隱私請求處理](../profile/privacy.md) 除本教程外。
>
>有關如何對其他Adobe Experience Cloud應用程式發出隱私請求的步驟，請參閱 [Privacy Service文檔](../privacy-service/experience-cloud-apps.md)。

## 快速入門

建議您對以下內容有正確理解 [!DNL Experience Platform] 服務，然後閱讀本指南。

* [[!DNL Privacy Service]](../privacy-service/home.md):管理客戶跨Adobe Experience Cloud應用程式訪問、選擇退出銷售或刪除其個人資料的請求。
* [[!DNL Identity Service]](../identity-service/home.md):通過跨設備和系統橋接身份，解決客戶體驗資料碎片化帶來的根本難題。
* [[!DNL Real-time Customer Profile]](home.md):基於來自多個源的聚合資料提供統一、即時的用戶配置檔案。

## 瞭解標識命名空間 {#namespaces}

Adobe Experience Platform [!DNL Identity Service] 跨系統和設備橋接客戶身份資料。 [!DNL Identity Service] 使用 **標識命名空間** 通過將身份值與其來源系統相關聯，提供身份值的上下文。 命名空間可以表示一個通用概念，如電子郵件地址（「電子郵件」），或將標識與特定應用程式(如Adobe Advertising CloudID(「AdCloud」)或Adobe TargetID(「TNTID」))關聯。

Identity Service維護全局定義（標準）和用戶定義（自定義）標識命名空間的儲存。 標準命名空間適用於所有組織（例如，「電子郵件」和「ECID」），而您的組織也可以建立自定義命名空間以滿足其特定需求。

有關中標識命名空間的詳細資訊 [!DNL Experience Platform]，請參見 [標識命名空間概述](../identity-service/namespaces.md)。

## 提交請求 {#submit}

以下各節概述了如何對 [!DNL Identity Service] 使用 [!DNL Privacy Service] API或UI。 在閱讀這些部分之前，強烈建議您查看 [Privacy ServiceAPI](../privacy-service/api/getting-started.md) 或 [Privacy ServiceUI](../privacy-service/ui/overview.md) 有關如何提交隱私作業的完整步驟的文檔，包括如何在請求負載中正確格式化用戶資料。

### 使用 API

在API中建立作業請求時，在 `userIDs` 必須使用特定 `namespace` 和 `type`。 有效 [標識命名空間](#namespaces) 確認 [!DNL Identity Service] 必須提供 `namespace` 值，而 `type` 必須為 `standard` 或 `unregistered` （分別用於標準名稱空間和自定義命名空間）。

另外， `include` 請求負載的陣列必須包括請求所針對的不同資料儲存的產品值。 在向 [!DNL Identity]，陣列必須包括值 `Identity`。

以下請求在GDPR下為GDPR中的單個客戶資料建立新的隱私作業 [!DNL Identity] 商店。 為中的客戶提供兩個標識值 `userIDs` 陣列；使用標準 `Email` 標識命名空間，而另一個使用 `ECID` 命名空間，還包括 [!DNL Identity] (`Identity`) `include` 陣列：

>[!TIP]
>
>使用API刪除自定義命名空間時，必須將標識符指定為命名空間，而不是顯示名稱。

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

>[!TIP]
>
>使用UI刪除自定義命名空間時，必須將標識符號指定為命名空間，而不是顯示名稱。 此外，您不能刪除非生產沙箱的UI中的自定義命名空間。

在UI中建立作業請求時，請確保選擇 **[!UICONTROL 身份]** 在 **[!UICONTROL 產品]** 以便處理儲存在 [!DNL Identity Service]。

![標識](./images/identity-gdpr.png)

## 刪除請求處理

當 [!DNL Experience Platform] 從接收刪除請求 [!DNL Privacy Service]。 [!DNL Platform] 發送確認 [!DNL Privacy Service] 已接收請求並且已將受影響資料標籤為刪除。 單個標識的刪除基於所提供的命名空間和/或ID值。 此外，刪除與給定IMS組織關聯的所有沙箱。

根據您是否還包括即時客戶配置檔案(`ProfileService`)和資料湖(`aepDataLake`)作為您的Identity Service隱私請求中的產品(`identity`)，在可能不同的時間從系統中刪除與身份相關的不同資料集：

| 包括的產品 | 效果 |
| --- | --- |
| `identity` 僅 | 一旦平台發送確認刪除請求已被接收，與提供的標識相關聯的標識圖即被立即刪除。 根據該身份圖構建的配置檔案仍然保留，但由於現在刪除了身份關聯，因此不會在接收新資料時更新。 與配置檔案關聯的資料也保留在資料湖中。 |
| `identity` 和 `ProfileService` | 一旦平台發送確認刪除請求被接收，則立即刪除標識圖及其關聯配置檔案。 與配置檔案關聯的資料保留在資料湖中。 |
| `identity` 和 `aepDataLake` | 一旦平台發送確認刪除請求已被接收，與提供的標識相關聯的標識圖即被立即刪除。 根據該身份圖構建的配置檔案仍然保留，但由於現在刪除了身份關聯，因此不會在接收新資料時更新。<br><br>當資料湖產品響應已接收請求並且當前正在處理時，與簡檔相關聯的資料被軟刪除，因此任何用戶都無法訪問 [!DNL Platform] 服務。 作業完成後，資料將完全從資料湖中刪除。 |
| `identity`, `ProfileService`, 和 `aepDataLake` | 一旦平台發送確認刪除請求被接收，則立即刪除標識圖及其關聯配置檔案。<br><br>當資料湖產品響應已接收請求並且當前正在處理時，與簡檔相關聯的資料被軟刪除，因此任何用戶都無法訪問 [!DNL Platform] 服務。 作業完成後，資料將完全從資料湖中刪除。 |

請參閱 [[!DNL Privacy Service] 文檔](../privacy-service/home.md#monitor) 的子菜單。

## 後續步驟

通過閱讀本文檔，您已瞭解處理隱私請求時涉及的重要概念 [!DNL Identity Service]。 有關處理其他隱私請求的資訊 [!DNL Experience Cloud] 應用程式，請參閱上的文檔 [[!DNL Privacy Service] and [!DNL Experience Cloud] 應用程式](../privacy-service/experience-cloud-apps.md)。
