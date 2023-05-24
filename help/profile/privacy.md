---
keywords: Experience Platform；首頁；熱門主題
solution: Experience Platform
title: 即時客戶檔案中的隱私請求處理
type: Documentation
description: Adobe Experience Platform Privacy Service處理客戶訪問、選擇退出銷售或刪除其個人資料的請求，這些資料由許多隱私法規規定。 本文檔介紹與處理即時客戶配置檔案的隱私請求相關的基本概念。
exl-id: fba21a2e-aaf7-4aae-bb3c-5bd024472214
source-git-commit: 42e59ba1c7b1980d6633ced264673afcf8d80810
workflow-type: tm+mt
source-wordcount: '1612'
ht-degree: 0%

---

# 隱私請求處理 [!DNL Real-Time Customer Profile]

Adobe Experience Platform [!DNL Privacy Service] 處理客戶訪問、選擇不銷售或刪除其個人資料的請求，如一般資料保護法規(GDPR)和 [!DNL California Consumer Privacy Act] (CCPA)。

本文檔涵蓋與處理針對 [!DNL Real-Time Customer Profile] 在Adobe Experience Platform。

>[!NOTE]
>
>本指南僅介紹如何對Experience Platform中的Profile資料儲存進行隱私請求。 如果您還計畫對平台資料湖提出隱私請求，請參閱上的指南 [資料湖中的隱私請求處理](../catalog/privacy.md) 除本教程外。
>
>有關如何對其他Adobe Experience Cloud應用程式發出隱私請求的步驟，請參閱 [Privacy Service文檔](../privacy-service/experience-cloud-apps.md)。

## 快速入門

本指南要求對以下方面有一定的認識 [!DNL Platform] 元件：

* [[!DNL Privacy Service]](../privacy-service/home.md):管理客戶跨Adobe Experience Cloud應用程式訪問、選擇退出銷售或刪除其個人資料的請求。
* [[!DNL Identity Service]](../identity-service/home.md):通過跨設備和系統橋接身份，解決客戶體驗資料碎片化帶來的根本難題。
* [[!DNL Real-Time Customer Profile]](home.md):基於來自多個源的聚合資料提供統一、即時的用戶配置檔案。

## 瞭解標識命名空間 {#namespaces}

Adobe Experience Platform [!DNL Identity Service] 跨系統和設備橋接客戶身份資料。 [!DNL Identity Service] 使用 **標識命名空間** 通過將身份值與其來源系統相關聯，提供身份值的上下文。 命名空間可以表示一個通用概念，如電子郵件地址（「電子郵件」），或將標識與特定應用程式(如Adobe Advertising CloudID(「AdCloud」)或Adobe TargetID(「TNTID」))關聯。

Identity Service維護全局定義（標準）和用戶定義（自定義）標識命名空間的儲存。 標準命名空間適用於所有組織（例如，「電子郵件」和「ECID」），而您的組織也可以建立自定義命名空間以滿足其特定需求。

有關中標識命名空間的詳細資訊 [!DNL Experience Platform]，請參見 [標識命名空間概述](../identity-service/namespaces.md)。

## 提交請求 {#submit}

以下各節概述了如何對 [!DNL Real-Time Customer Profile] 使用 [!DNL Privacy Service] API或UI。 在閱讀這些部分之前，強烈建議您查看 [Privacy ServiceAPI](../privacy-service/api/getting-started.md) 或 [Privacy ServiceUI](../privacy-service/ui/overview.md) 有關如何提交隱私作業的完整步驟的文檔，包括如何在請求負載中正確格式化已提交的用戶標識資料。

>[!IMPORTANT]
>
>Privacy Service只能處理 [!DNL Profile] 使用不執行身份縫合的合併策略的資料。 請參閱 [合併策略限制](#merge-policy-limitations) 的子菜單。
>
>請注意隱私請求完成所花的時間 **不能** 得到保證。 如果在 [!DNL Profile] 在請求仍在處理時，是否處理這些記錄也無法保證。

### 使用 API

在API中建立作業請求時，在 `userIDs` 必須使用特定 `namespace` 和 `type`。 有效 [標識命名空間](#namespaces) 確認 [!DNL Identity Service] 必須提供 `namespace` 值，而 `type` 必須為 `standard` 或 `unregistered` （分別用於標準名稱空間和自定義命名空間）。

>[!NOTE]
>
>您可能需要為每個客戶提供多個ID，具體取決於身份圖以及配置檔案片段在平台資料集中的分佈方式。 請參閱下一節 [配置檔案片段](#fragments) 的子菜單。

另外， `include` 請求負載的陣列必須包括請求所針對的不同資料儲存的產品值。 要刪除與身份關聯的配置檔案資料，陣列必須包含該值 `ProfileService`。 要刪除客戶的標識圖關聯，陣列必須包含該值 `identity`。

>[!NOTE]
>
>請參閱 [配置檔案請求和身份請求](#profile-v-identity) 以獲取有關使用 `ProfileService` 和 `identity` 在 `include` 陣列。

以下請求為中的單個客戶資料建立新的隱私作業 [!DNL Profile] 商店。 為中的客戶提供兩個標識值 `userIDs` 陣列；使用標準 `Email` 標識命名空間，而另一個使用自定義 `Customer_ID` 命名空間。 還包括產品價值 [!DNL Profile] (`ProfileService`) `include` 陣列：

**要求**

```shell
curl -X POST \
  https://platform.adobe.io/data/core/privacy/jobs \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -d '{
    "companyContexts": [
      {
        "namespace": "imsOrgID",
        "value": "{ORG_ID}"
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
    "include": ["ProfileService","identity"],
    "expandIds": false,
    "priority": "normal",
    "regulation": "ccpa"
}'
```

>[!IMPORTANT]
>
>平台處理跨所有 [沙箱](../sandboxes/home.md) 屬於您的組織。 因此， `x-sandbox-name` 系統將忽略請求中包含的標頭。

**產品響應**

對於配置檔案服務，一旦隱私作業完成，將以JSON格式返迴響應，其中包含請求的有關用戶ID的資訊。

```json
{
    "privacyResponse": {
        "jobId": "7467850f-9698-11ed-8635-355435552164",
        "response": [
            {
                "sandbox": "prod",
                "mergePolicyId": "none",
                "result": {
                    "person": {
                        "gender": "female"           
                    },
                    "personalEmail": {
                        "address": "ajones@acme.com",
                    },
                    "identityMap": {
                        "crmid": [
                            {
                                "id": "5b7db37a-bc7a-46a2-a63e-2cfe7e1cc068"
                            }
                        ]
                    }
                }
            },
            {
                "sandbox": "prod",
                "mergePolicyId": "none",
                "result": {
                    "person": {
                        "gender": "male"
                    },
                    "id": 12345678,
                    "identityMap": {
                        "crmid": [
                            {
                                "id": "e9d439f2-f5e4-4790-ad67-b13dbd89d52e"
                            }
                        ]
                    }
                }
            }
        ]
    }
}
```

### 使用UI

在UI中建立作業請求時，請確保選擇 **[!UICONTROL AEP資料湖]** 和/或 **[!UICONTROL 配置檔案]** 在 **[!UICONTROL 產品]** 以便處理儲存在資料湖或 [!DNL Real-Time Customer Profile]的下界。

![在UI中建立的訪問作業請求，在「產品」下選擇了「配置檔案」選項](./images/privacy/product-value.png)

## 隱私請求中的配置檔案片段 {#fragments}

在 [!DNL Profile] 資料儲存，個人資料通常由多個配置檔案片段組成，這些配置檔案片段通過身份圖與個人相關聯。 在向 [!DNL Profile] 儲存，必須注意的是，請求只在配置檔案片段級別處理，而不是整個配置檔案。

例如，考慮一種情況：您將客戶屬性資料儲存在三個獨立的資料集中，這些資料集使用不同的標識符將該資料與單個客戶關聯：

| 資料集名稱 | 主標識欄位 | 儲存的屬性 |
| --- | --- | --- |
| 資料集1 | `customer_id` | `address` |
| 資料集2 | `email_id` | `firstName`、`lastName` |
| 資料集3 | `email_id` | `mlScore` |

其中一個資料集使用 `customer_id` 作為主標識符，而另兩個則使用 `email_id`。 如果僅使用 `email_id` 作為用戶ID值，僅 `firstName`。 `lastName`, `mlScore` 屬性將被處理，而 `address` 不會受到影響。

要確保您的隱私請求處理所有相關的客戶屬性，您必須為所有可儲存這些屬性的適用資料集提供主要標識值（每個客戶最多可以儲存9個ID）。 請參閱中有關標識欄位的部分 [架構組合基礎](../xdm/schema/composition.md#identity) 的子菜單。

## 刪除請求處理 {#delete}

當 [!DNL Experience Platform] 從接收刪除請求 [!DNL Privacy Service]。 [!DNL Platform] 發送確認 [!DNL Privacy Service] 已接收請求並且已將受影響資料標籤為刪除。 然後，一旦隱私作業完成，就刪除記錄。

>[!IMPORTANT]
>
>隱私刪除請求不是即時的，可能會因涉及的服務和其他影響因素而有所不同。 完成隱私工作的時間可以從15天延長到45天，但並不保證。

取決於您是否還包括Identity Service(`identity`)和資料湖(`aepDataLake`)作為您對配置檔案的隱私請求中的產品(`ProfileService`)，在可能不同的時間從系統中刪除與配置檔案相關的不同資料集：

| 包括的產品 | 效果 |
| --- | --- |
| `ProfileService` 僅 | 一旦平台發送確認刪除請求，該配置檔案即會立即刪除。 然而，該輪廓的標識圖仍然存在，並且當攝取具有相同標識的新資料時，該輪廓可能被重建。 與配置檔案關聯的資料也保留在資料湖中。 |
| `ProfileService` 和 `identity` | 一旦平台發送確認刪除請求被接收，該配置檔案及其關聯的標識圖會立即被刪除。 與配置檔案關聯的資料保留在資料湖中。 |
| `ProfileService` 和 `aepDataLake` | 一旦平台發送確認刪除請求，該配置檔案即會立即刪除。 然而，該輪廓的標識圖仍然存在，並且當攝取具有相同標識的新資料時，該輪廓可能被重建。<br><br>當資料湖產品響應已接收請求並且當前正在處理時，與簡檔相關聯的資料被軟刪除，因此任何用戶都無法訪問 [!DNL Platform] 服務。 作業完成後，資料將完全從資料湖中刪除。 |
| `ProfileService`, `identity`, 和 `aepDataLake` | 一旦平台發送確認刪除請求被接收，該配置檔案及其關聯的標識圖會立即被刪除。<br><br>當資料湖產品響應已接收請求並且當前正在處理時，與簡檔相關聯的資料被軟刪除，因此任何用戶都無法訪問 [!DNL Platform] 服務。 作業完成後，資料將完全從資料湖中刪除。 |

請參閱 [[!DNL Privacy Service] 文檔](../privacy-service/home.md#monitor) 的子菜單。

### 配置檔案請求與身份請求 {#profile-v-identity}

如果對配置檔案發出刪除請求(`ProfileService`)但不是Identity Service(`identity`)，生成的作業將刪除客戶（或一組客戶）的收集屬性資料，但不會刪除在標識圖中建立的關聯。

例如，使用客戶的 `email_id` 和 `customer_id` 刪除儲存在這些ID下的所有屬性資料。 但是，隨後在同一資料下攝取的任何資料 `customer_id` 仍與相應的 `email_id`，因為關聯仍然存在。

要刪除給定客戶的配置檔案和所有身份關聯，請確保在刪除請求中同時將配置檔案和身份服務作為目標產品。

### 合併策略限制 {#merge-policy-limitations}

Privacy Service只能處理 [!DNL Profile] 使用不執行身份縫合的合併策略的資料。 如果您使用UI來確認是否正在處理您的隱私請求，請確保您使用的策略 **[!DNL None]** 作為 [!UICONTROL ID拼接] 的雙曲餘切值。 換句話說，您不能使用合併策略 [!UICONTROL ID拼接] 設定為 [!UICONTROL 專用圖]。
>![合併策略的ID拼接設定為「無」](./images/privacy/no-id-stitch.png)
>
## 後續步驟

通過閱讀本文檔，您已瞭解處理隱私請求時涉及的重要概念 [!DNL Experience Platform]。 要加深您對如何管理身份資料和建立隱私作業的理解，請繼續閱讀本指南中提供的文檔。

有關處理隱私請求的資訊 [!DNL Platform] 資源未使用 [!DNL Profile]，請參閱上的文檔 [資料湖中的隱私請求處理](../catalog/privacy.md)。
