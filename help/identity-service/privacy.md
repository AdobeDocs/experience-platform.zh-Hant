---
keywords: Experience Platform；首頁；熱門主題
title: Identity Service中的隱私權請求處理
description: Adobe Experience Platform Privacy Service會根據多項隱私權法規的規定，處理客戶存取、選擇退出銷售或刪除其個人資料的請求。 本文介紹與處理Identity Service的隱私權請求相關的重要概念。
exl-id: ab84450b-1a4b-4fdd-b77d-508c86bbb073
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1005'
ht-degree: 1%

---

# 在[!DNL Identity Service]中處理隱私權請求

Adobe Experience Platform [!DNL Privacy Service]會根據一般資料保護規範(GDPR)和[!DNL California Consumer Privacy Act] (CCPA)等隱私權法規，處理客戶存取、選擇退出銷售或刪除其個人資料的請求。

本檔案說明在Adobe Experience Platform中處理[!DNL Identity Service]隱私權要求的相關基本概念。

>[!NOTE]
>
>本指南僅涵蓋如何在Experience Platform中向Identity資料存放區提出隱私權請求。 如果您也計畫提出Experience Platform資料湖或[!DNL Real-Time Customer Profile]的隱私權請求，請參閱資料湖[&#128279;](../catalog/privacy.md)中隱私權請求處理指南，以及本教學課程以外的[設定檔隱私權請求處理指南](../profile/privacy.md)。
>
>如需如何對其他Adobe Experience Cloud應用程式提出隱私權要求的步驟，請參閱[Privacy Service檔案](../privacy-service/experience-cloud-apps.md)。

## 快速入門

在閱讀本指南之前，建議您實際瞭解下列[!DNL Experience Platform]服務：

* [[!DNL Privacy Service]](../privacy-service/home.md)：管理客戶透過Adobe Experience Cloud應用程式存取、選擇退出銷售或刪除其個人資料的請求。
* [[!DNL Identity Service]](../identity-service/home.md)：透過跨裝置和系統橋接身分，解決客戶體驗資料分散所造成的根本挑戰。
* [[!DNL Real-Time Customer Profile]](home.md)：根據來自多個來源的彙總資料，提供統一的即時消費者設定檔。

## 了解身分識別命名空間 {#namespaces}

Adobe Experience Platform [!DNL Identity Service]可跨系統和裝置橋接客戶身分資料。 [!DNL Identity Service]使用&#x200B;**身分識別名稱空間**，透過將身分識別值與其來源系統建立關聯來提供身分識別值的內容。 名稱空間可代表一般概念，例如電子郵件地址（「電子郵件」），或將身分與特定應用程式相關聯，例如Adobe Advertising Cloud ID (「AdCloud」)或Adobe Target ID (「TNTID」)。

Identity Service維護全域定義（標準）和使用者定義（自訂）的身分名稱空間之存放區。 標準名稱空間適用於所有組織（例如「Email」和「ECID」），而您的組織也可以建立自訂名稱空間以滿足其特定需求。

如需[!DNL Experience Platform]中識別名稱空間的詳細資訊，請參閱[識別名稱空間概觀](../identity-service/features/namespaces.md)。

## 提交請求 {#submit}

以下各節概述如何使用[!DNL Privacy Service] API或UI為[!DNL Identity Service]提出隱私權請求。 在閱讀這些章節之前，強烈建議您檢閱[Privacy Service API](../privacy-service/api/getting-started.md)或[Privacy Service UI](../privacy-service/ui/overview.md)檔案，以取得有關如何提交隱私權工作的完整步驟，包括如何在請求裝載中正確格式化使用者資料。

### 使用 API

在API中建立工作要求時，`userIDs`內提供的任何ID都必須使用特定的`namespace`和`type`。 必須提供[!DNL Identity Service]識別的有效[身分名稱空間](#namespaces)以供`namespace`值使用，而`type`必須是`standard`或`unregistered` （分別用於標準與自訂名稱空間）。

此外，請求承載的`include`陣列必須包含請求所針對的不同資料存放區的產品值。 向[!DNL Identity]提出請求時，陣列必須包含值`Identity`。

以下請求會根據GDPR為[!DNL Identity]存放區中的單一客戶資料建立新的隱私權工作。 在`userIDs`陣列中為客戶提供了兩個身分值；一個使用標準`Email`身分名稱空間，另一個使用`ECID`名稱空間，它同時包含`include`陣列中[!DNL Identity] (`Identity`)的產品值：

>[!TIP]
>
>使用GDPR刪除身分時，您必須將身分符號指定為名稱空間，而非顯示名稱。

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
>使用GDPR刪除身分時，您必須將身分符號指定為名稱空間，而非顯示名稱。

在UI中建立工作請求時，請務必在&#x200B;**[!UICONTROL 產品]**&#x200B;下選取&#x200B;**[!UICONTROL 身分]**，以便處理儲存在[!DNL Identity Service]中之資料的工作。

![identity-gdpr](./images/identity-gdpr.png)

## 正在處理刪除請求

當[!DNL Experience Platform]收到來自[!DNL Privacy Service]的刪除請求時，[!DNL Experience Platform]會傳送確認給[!DNL Privacy Service]，確認已收到該請求且受影響的資料已標示為刪除。 個人身分的刪除是根據提供的名稱空間和/或ID值。 此外，刪除也會針對與指定組織相關聯的所有沙箱進行。

視您是否也在身分服務的隱私權要求(`identity`)中包含即時客戶設定檔(`ProfileService`)和資料湖(`aepDataLake`)作為產品而定，與身分相關的不同資料集可能會在不同時間從系統中移除：

| 包含的產品 | 效果 |
| --- | --- |
| 僅`identity` | Experience Platform一傳送確認已收到刪除請求，就會刪除提供的身分。 從該身分圖表建構的設定檔仍會保留，但不會更新為擷取新資料，因為身分關聯現在已移除。 與設定檔相關聯的資料也會保留在資料湖中。 |
| `identity` 和 `ProfileService` | Experience Platform一傳送確認已收到刪除請求，就會刪除提供的身分。 與設定檔相關聯的資料會保留在資料湖中。 |
| `identity` 和 `aepDataLake` | Experience Platform一傳送確認已收到刪除請求，就會刪除提供的身分。 從該身分圖表建構的設定檔仍會保留，但不會更新為擷取新資料，因為身分關聯現在已移除。<br><br>當Data Lake產品回應收到要求且目前正在處理時，與設定檔關聯的資料會軟刪除，因此無法由任何[!DNL Experience Platform]服務存取。 工作完成後，資料會從資料湖中完全移除。 |
| `identity`、`ProfileService`和`aepDataLake` | Experience Platform一傳送確認已收到刪除請求，就會刪除提供的身分。<br><br>當Data Lake產品回應收到要求且目前正在處理時，與設定檔關聯的資料會軟刪除，因此無法由任何[!DNL Experience Platform]服務存取。 工作完成後，資料會從資料湖中完全移除。 |

如需追蹤工作狀態的詳細資訊，請參閱[[!DNL Privacy Service] 檔案](../privacy-service/home.md#monitor)。

## 後續步驟

閱讀本檔案後，您已經瞭解在[!DNL Identity Service]中處理隱私權要求的重要概念。 如需有關處理其他[!DNL Experience Cloud]應用程式的隱私權要求的資訊，請參閱[[!DNL Privacy Service] 和 [!DNL Experience Cloud] 應用程式](../privacy-service/experience-cloud-apps.md)的檔案。
