---
keywords: Experience Platform；首頁；熱門主題
solution: Experience Platform
title: 即時客戶個人檔案中的隱私權要求處理
type: Documentation
description: Adobe Experience Platform Privacy Service會處理客戶存取、選擇退出銷售或刪除其個人資料的請求，這些資料是多項隱私權法規所規定。 本檔案涵蓋與處理即時客戶個人檔案隱私權要求相關的基本概念。
exl-id: fba21a2e-aaf7-4aae-bb3c-5bd024472214
source-git-commit: e94482532e0c5698cfe5e51ba260f89c67fa64f0
workflow-type: tm+mt
source-wordcount: '1173'
ht-degree: 0%

---

# [!DNL Real-time Customer Profile]中的隱私權要求處理

Adobe Experience Platform [!DNL Privacy Service]會處理客戶要求存取、選擇退出銷售或刪除其個人資料的請求，如一般資料保護規範(GDPR)和[!DNL California Consumer Privacy Act](CCPA)等隱私權法規所規定。

本檔案涵蓋與處理Adobe Experience Platform中[!DNL Real-time Customer Profile]隱私權要求相關的基本概念。

>[!NOTE]
>
>本指南僅說明如何針對Experience Platform中的設定檔資料存放區提出隱私權要求。 如果您也打算為Platform Data Lake提出隱私權要求，除了本教學課程外，請參閱資料湖](../catalog/privacy.md)中的[隱私權要求處理指南。
>
>如需如何為其他Adobe Experience Cloud應用程式提出隱私權要求的步驟，請參閱[Privacy Service檔案](../privacy-service/experience-cloud-apps.md)。

## 快速入門

在閱讀本指南之前，建議您對以下[!DNL Experience Platform]服務有充分的了解：

* [[!DNL Privacy Service]](../privacy-service/home.md):管理客戶在Adobe Experience Cloud應用程式中存取、選擇退出銷售或刪除其個人資料的請求。
* [[!DNL Identity Service]](../identity-service/home.md):通過跨裝置和系統橋接身分，解決客戶體驗資料分散帶來的根本難題。
* [[!DNL Real-time Customer Profile]](home.md):根據來自多個來源的匯總資料，提供統一的即時消費者設定檔。

## 了解身分識別命名空間 {#namespaces}

Adobe Experience Platform [!DNL Identity Service]橋接跨系統和裝置的客戶身分資料。 [!DNL Identity Service] 使 **用身** 分名稱名稱，將身分值與其來源系統關聯，以提供內容給身分值。命名空間可代表一般概念，例如電子郵件地址（「電子郵件」），或將身分識別與特定應用程式建立關聯，例如Adobe Advertising Cloud ID(「AdCloud」)或Adobe Target ID(「TNTID」)。

Identity Service會維護全域定義（標準）和使用者定義（自訂）身分識別命名空間的存放區。 所有組織皆可使用標準命名空間（例如「電子郵件」和「ECID」），而您的組織也可以建立自訂命名空間，以符合其特定需求。

如需[!DNL Experience Platform]中身分命名空間的詳細資訊，請參閱[身分命名空間概述](../identity-service/namespaces.md)。

## 提交請求 {#submit}

以下各節將說明如何使用[!DNL Privacy Service] API或UI，為[!DNL Real-time Customer Profile]提出隱私權要求。 閱讀這些小節之前，強烈建議您檢閱[Privacy ServiceAPI](../privacy-service/api/getting-started.md)或[Privacy ServiceUI](../privacy-service/ui/overview.md)檔案，以取得如何提交隱私權工作的完整步驟，包括如何在請求裝載中正確格式化已提交的使用者身分資料。

>[!IMPORTANT]
>
>Privacy Service只能使用不執行身分拼接的合併原則來處理[!DNL Profile]資料。 如果您使用UI來確認是否正在處理您的隱私權要求，請確定您使用的原則是「[!DNL None]」作為[!UICONTROL ID匯整]類型。 換言之，您無法使用將[!UICONTROL ID拼接]設為「[!UICONTROL 專用圖]」的合併原則。
>
>![](./images/privacy/no-id-stitch.png)
>
>同時請務必注意，無法保證隱私權要求完成所花的時間。 如果在請求仍在處理時，[!DNL Profile]資料中發生變更，則無法保證處理這些記錄。

### 使用 API

在API中建立工作請求時，`userIDs`中提供的任何ID都必須使用特定的`namespace`和`type`。 必須為`namespace`值提供由[!DNL Identity Service]識別命名空間](#namespaces)的有效[，而`type`必須為`standard`或`unregistered`（針對標準和自訂命名空間，分別）。

>[!NOTE]
>
>視身分圖表以及Platform資料集中設定檔片段的分送方式而定，您可能需要為每個客戶提供多個ID。 如需詳細資訊，請參閱下一節[設定檔片段](#fragments)。

此外，請求裝載的`include`陣列必須包含對請求進行之不同資料存放區的產品值。 向[!DNL Data Lake]提出請求時，陣列必須包含「ProfileService」值。

以下請求會為[!DNL Profile]商店中的單一客戶資料建立新的隱私權工作。 在`userIDs`陣列中為客戶提供了兩個標識值；一個使用標準`Email`身分命名空間，另一個使用自訂`Customer_ID`命名空間。 也包含`include`陣列中[!DNL Profile](`ProfileService`)的產品值：

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
    "regulation": "ccpa"
}'
```

### 使用UI

在UI中建立作業請求時，請務必在&#x200B;**[!UICONTROL Products]**&#x200B;下選取&#x200B;**[!UICONTROL AEP Data Lake]**&#x200B;和/或&#x200B;**[!UICONTROL Profile]**，以便分別處理儲存在[!DNL Data Lake]或[!DNL Real-time Customer Profile]中之資料的作業。

<img src="images/privacy/product-value.png" width="450"><br>

## 隱私權要求中的設定檔片段 {#fragments}

在[!DNL Profile]資料存放區中，個別客戶的個人資料通常由多個設定檔片段組成，這些片段透過身分圖表與人員相關聯。 向[!DNL Profile]存放區提出隱私權要求時，請務必注意，要求只會在設定檔片段層級處理，而非整個設定檔處理。

例如，假設您將客戶屬性資料儲存在三個不同的資料集中，這些資料集使用不同的識別碼將該資料與個別客戶建立關聯：

| 資料集名稱 | 主要身分欄位 | 儲存的屬性 |
| --- | --- | --- |
| 資料集1 | `customer_id` | `address` |
| 資料集2 | `email_id` | `firstName`, `lastName` |
| 資料集3 | `email_id` | `mlScore` |

其中一個資料集使用`customer_id`作為主要識別碼，另兩個資料集則使用`email_id`。 如果您只要使用`email_id`作為使用者ID值來傳送隱私權要求（存取或刪除），則只會處理`firstName`、`lastName`和`mlScore`屬性，而不會影響`address`。

為確保您的隱私權要求可處理所有相關客戶屬性，您必須為所有可儲存屬性的適用資料集提供主要身分值（每位客戶最多9個ID）。 有關通常標籤為身份的欄位的詳細資訊，請參閱[架構組合基礎](../xdm/schema/composition.md#identity)中有關標識欄位的部分。

>[!NOTE]
>
>如果您使用不同的[沙箱](../sandboxes/home.md)來儲存[!DNL Profile]資料，則必須對每個沙箱提出個別的隱私權要求，並在`x-sandbox-name`標題中指出適當的沙箱名稱。

## 刪除請求處理

當[!DNL Experience Platform]收到來自[!DNL Privacy Service]的刪除請求時， [!DNL Platform]向[!DNL Privacy Service]發送確認，確認已接收該請求，且受影響的資料已標籤為刪除。 一旦隱私權工作完成，記錄便會從[!DNL Data Lake]或[!DNL Profile]儲存中移除。 當刪除作業仍在處理時，資料會被軟刪除，因此任何[!DNL Platform]服務都無法存取。 如需追蹤工作狀態的詳細資訊，請參閱[[!DNL Privacy Service] 檔案](../privacy-service/home.md#monitor)。

>[!IMPORTANT]
>
>成功的刪除請求會移除客戶（或一組客戶）所收集的屬性資料，但請求不會移除在身分圖中建立的關聯。
>
>例如，使用客戶`email_id`和`customer_id`的刪除請求會移除儲存在這些ID下的所有屬性資料。 不過，之後在相同`customer_id`下擷取的任何資料仍會與適當的`email_id`相關聯，因為關聯仍然存在。

在未來版本中，在實際刪除資料後， [!DNL Platform]將向[!DNL Privacy Service]發送確認。

## 後續步驟

閱讀本檔案後，您便了解[!DNL Experience Platform]中處理隱私權要求的重要概念。 建議您繼續閱讀本指南中提供的檔案，以深入了解如何管理身分資料和建立隱私權工作。

如需處理[!DNL Platform]資源（[!DNL Profile]未使用）的隱私權要求的相關資訊，請參閱資料湖](../catalog/privacy.md)中的[隱私權要求處理相關檔案。
