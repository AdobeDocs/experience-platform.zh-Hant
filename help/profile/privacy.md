---
keywords: Experience Platform；首頁；熱門主題
solution: Experience Platform
title: 即時客戶個人檔案中的隱私權請求處理
type: Documentation
description: Adobe Experience Platform Privacy Service會根據多項隱私權法規的規定，處理客戶存取、選擇退出銷售或刪除其個人資料的請求。 本檔案說明與處理即時客戶個人檔案的隱私權請求相關的重要概念。
exl-id: fba21a2e-aaf7-4aae-bb3c-5bd024472214
source-git-commit: 6d9f8eceeb8fbe550b4e1e7e0964f2fff0cd3c70
workflow-type: tm+mt
source-wordcount: '1739'
ht-degree: 0%

---

# 隱私權請求處理於 [!DNL Real-Time Customer Profile]

Adobe Experience Platform [!DNL Privacy Service] 處理客戶存取、選擇退出銷售或刪除其個人資料的請求，這些請求由隱私權法規(例如一般資料保護規範(GDPR)和 [!DNL California Consumer Privacy Act] (CCPA)。

本檔案說明與處理隱私權請求相關的重要概念。 [!DNL Real-Time Customer Profile] 在Adobe Experience Platform中。

>[!NOTE]
>
>本指南僅涵蓋如何向Experience Platform中的設定檔資料存放區提出隱私權請求。 如果您也計畫針對Platform Data Lake提出隱私權請求，請參閱以下指南： [資料湖中的隱私權請求處理](../catalog/privacy.md) 除了本教學課程以外。
>
>如需如何對其他Adobe Experience Cloud應用程式提出隱私權要求的步驟，請參閱 [Privacy Service檔案](../privacy-service/experience-cloud-apps.md).

>[!IMPORTANT]
>
>本指南中的隱私權請求會 **非** 涵蓋B2B非個人實體。

## 快速入門

本指南需要您深入瞭解下列事項 [!DNL Platform] 元件：

* [[!DNL Privacy Service]](../privacy-service/home.md)：管理客戶在Adobe Experience Cloud應用程式中存取、選擇退出銷售或刪除其個人資料的請求。
* [[!DNL Identity Service]](../identity-service/home.md)：透過跨裝置和系統橋接身分，解決客戶體驗資料分散所造成的根本挑戰。
* [[!DNL Real-Time Customer Profile]](home.md)：根據來自多個來源的彙總資料，提供統一的即時消費者個人檔案。

## 瞭解身分名稱空間 {#namespaces}

Adobe Experience Platform [!DNL Identity Service] 跨系統和裝置橋接客戶身分資料。 [!DNL Identity Service] 使用 **身分名稱空間** 透過將身分值與其來源系統建立關聯來提供身分值的前後關聯。 名稱空間可代表一般概念，例如電子郵件地址（「電子郵件」），或將身分與特定應用程式相關聯，例如Adobe Advertising Cloud ID (「AdCloud」)或Adobe Target ID (「TNTID」)。

Identity Service維護全域定義（標準）和使用者定義（自訂）的身分名稱空間之存放區。 標準名稱空間適用於所有組織（例如「Email」和「ECID」），而您的組織也可以建立自訂名稱空間以滿足其特定需求。

如需中身分識別名稱空間的詳細資訊 [!DNL Experience Platform]，請參閱 [身分名稱空間總覽](../identity-service/namespaces.md).

## 提交請求 {#submit}

以下各節概述如何針對以下專案提出隱私權請求： [!DNL Real-Time Customer Profile] 使用 [!DNL Privacy Service] API或UI。 在閱讀這些章節之前，您應先檢閱或瞭解 [PRIVACY SERVICE API](../privacy-service/api/getting-started.md) 或 [PRIVACY SERVICEUI](../privacy-service/ui/overview.md) 檔案。 這些檔案提供如何提交隱私權工作的完整步驟，包括如何在請求裝載中正確格式化提交的使用者身分資料。

>[!IMPORTANT]
>
>Privacy Service只能處理 [!DNL Profile] 使用不執行身分拼接的合併原則的資料。 請參閱以下小節： [合併原則限制](#merge-policy-limitations) 以取得詳細資訊。
>
>請注意，隱私權請求是根據法規要求以非同步方式處理，完成所需時間會有所不同。 若您的電腦發生變更 [!DNL Profile] 當要求仍在處理時，並不保證這些傳入記錄也會在該要求中處理。 系統保證只會刪除請求隱私權工作時，Data Lake或「設定檔存放區」中保留的設定檔。 如果您在刪除工作期間擷取與刪除請求主題相關的設定檔資料，並不保證會刪除所有設定檔片段。
>您有責任在刪除請求時，留意Platform或Profile Service中的任何傳入資料，因為該資料將會插入記錄存放區。 您必須審慎擷取已刪除或正在刪除的資料。

### 使用 API

在API中建立工作請求時，在中提供的任何ID `userIDs` 必須使用特定 `namespace` 和 `type`. 有效的 [身分名稱空間](#namespaces) 辨識者 [!DNL Identity Service] 必須提供 `namespace` 值，而 `type` 必須為 `standard` 或 `unregistered` （分別針對標準和自訂名稱空間）。

>[!NOTE]
>
>您可能需要根據身分圖表以及您的設定檔片段在Platform資料集中的分配方式，為每個客戶提供多個ID。 請參閱下一節 [設定檔片段](#fragments) 以取得詳細資訊。

此外， `include` 請求承載的陣列必須包含發出請求的不同資料存放區的產品值。 若要刪除與身分相關聯的設定檔資料，陣列必須包含值 `ProfileService`. 若要刪除客戶的身分圖表關聯，陣列必須包含值 `identity`.

>[!NOTE]
>
>請參閱以下小節： [設定檔要求與身分要求](#profile-v-identity) 請參閱本檔案後續章節，以取得有關使用的影響 `ProfileService` 和 `identity` 在 `include` 陣列。

以下請求會針對中的單一客戶資料建立新的隱私權工作 [!DNL Profile] 商店。 在以下位置為客戶提供兩個身分值： `userIDs` 陣列；一個使用標準 `Email` 身分名稱空間，以及使用自訂的其他名稱空間 `Customer_ID` 名稱空間。 其中也包含下列專案的產品價值 [!DNL Profile] (`ProfileService`)中 `include` 陣列：

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
>Platform會處理所有隱私權請求 [沙箱](../sandboxes/home.md) 屬於您的組織。 因此，任何 `x-sandbox-name` 請求中包含的標頭會被系統忽略。

**產品回應**

針對設定檔服務，隱私權工作完成後，系統就會傳回JSON格式的回應，其中包含與要求的使用者ID相關的資訊。

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

在UI中建立工作請求時，請務必選取 **[!UICONTROL AEP資料湖]** 和/或 **[!UICONTROL 個人資料]** 在 **[!UICONTROL 產品]** ，以便處理儲存在data lake或中的資料工作。 [!DNL Real-Time Customer Profile]，依序輸入。

![在UI中建立存取工作請求，並在「產品」下選取「設定檔」選項](./images/privacy/product-value.png)

## 隱私權請求中的設定檔片段 {#fragments}

在 [!DNL Profile] 資料存放區中，個別客戶的個人資料通常會由多個設定檔片段組成，這些片段會透過身分圖表與個人相關聯。 向提出隱私權請求時 [!DNL Profile] 請務必注意，請求僅在設定檔片段層級上處理，而不是整個設定檔。

例如，假設您要將客戶屬性資料儲存在三個個別的資料集中，並使用不同的識別碼將該資料與個別客戶建立關聯：

| 資料集名稱 | 主要身分欄位 | 已儲存的屬性 |
| --- | --- | --- |
| 資料集1 | `customer_id` | `address` |
| 資料集2 | `email_id` | `firstName`、`lastName` |
| 資料集3 | `email_id` | `mlScore` |

其中一個資料集使用 `customer_id` 作為主要識別碼，其他兩個則使用 `email_id`. 如果您只使用傳送隱私權請求（存取或刪除） `email_id` 由於使用者ID值，因此 `firstName`， `lastName`、和 `mlScore` 將處理屬性，而 `address` 將不會受到影響。

為確保您的隱私權請求可處理所有相關客戶屬性，您必須為可能儲存這些屬性的所有適用資料集提供主要身分值（每位客戶最多九個ID）。 請參閱「 」中有關身分欄位的章節 [結構描述組合的基本面](../xdm/schema/composition.md#identity) 以取得一般標示為身分的欄位相關詳細資訊。

## 正在處理刪除請求 {#delete}

時間 [!DNL Experience Platform] 接收來自的刪除請求 [!DNL Privacy Service]， [!DNL Platform] 傳送確認給 [!DNL Privacy Service] 已收到請求，且受影響的資料已標示為刪除。 隱私權工作完成後，記錄即會被移除。

>[!IMPORTANT]
>
>隱私權刪除請求並非立即提出，而且可能會因所涉及的服務及其他影響因素（例如地理位置）而有所不同。 完成隱私權工作的時間範圍可以是15至45天，但不保證一定會完成。

視您是否同時包含Identity Service (`identity`)和資料湖(`aepDataLake`)作為設定檔隱私權請求中的產品(`ProfileService`)，則與設定檔相關的不同資料集會在不同的時間從系統中移除：

| 包含的產品 | 效果 |
| --- | --- |
| `ProfileService` 僅限 | 當Platform傳送確認已收到刪除請求時，會立即刪除設定檔。 不過，設定檔的身分圖表仍會保留，並且隨著擷取具有相同身分的新資料，可能會重建設定檔。 與設定檔相關聯的資料也會保留在資料湖中。 |
| `ProfileService` 和 `identity` | 當Platform傳送確認已收到刪除請求時，會立即刪除設定檔及其關聯的身分圖表。 與設定檔相關聯的資料會保留在資料湖中。 |
| `ProfileService` 和 `aepDataLake` | 當Platform傳送確認已收到刪除請求時，會立即刪除設定檔。 不過，設定檔的身分圖表仍會保留，並且隨著擷取具有相同身分的新資料，可能會重建設定檔。<br><br>當Data Lake產品回應收到請求且目前正在處理時，與設定檔相關聯的資料會軟刪除，因此任何人都無法存取 [!DNL Platform] 服務。 工作完成後，資料會從資料湖中完全移除。 |
| `ProfileService`, `identity`, 和 `aepDataLake` | 當Platform傳送確認已收到刪除請求時，會立即刪除設定檔及其關聯的身分圖表。<br><br>當Data Lake產品回應收到請求且目前正在處理時，與設定檔相關聯的資料會軟刪除，因此任何人都無法存取 [!DNL Platform] 服務。 工作完成後，資料會從資料湖中完全移除。 |

請參閱 [[!DNL Privacy Service] 檔案](../privacy-service/home.md#monitor) 以取得追蹤工作狀態的詳細資訊。

### 設定檔請求與身分請求 {#profile-v-identity}

如果對設定檔提出刪除請求(`ProfileService`)而非Identity Service (`identity`)，則產生的作業會移除為客戶（或一組客戶）收集的屬性資料，但不會移除在身分圖表中建立的關聯。

例如，使用客戶的刪除請求 `email_id` 和 `customer_id` 會移除儲存在這些ID下的所有屬性資料。 不過，之後會透過相同擷取的任何資料 `customer_id` 仍將與適當的 `email_id`，因為關聯仍然存在。

若要移除指定客戶的設定檔和所有身分關聯，請確定刪除請求中同時包含設定檔和身分識別服務作為目標產品。

### 合併原則限制 {#merge-policy-limitations}

Privacy Service只能處理 [!DNL Profile] 使用不執行身分拼接的合併原則的資料。 如果您使用UI來確認您的隱私權請求是否正在處理中，請確定您使用的是包含下列專案的原則 **[!DNL None]** 作為 [!UICONTROL ID拼接] 型別。 換言之，您不能在下列情況下使用合併原則： [!UICONTROL ID拼接] 設為 [!UICONTROL 私人圖表].

>![合併原則的ID拼接設為「無」](./images/privacy/no-id-stitch.png)

## 後續步驟

閱讀本檔案後，您將瞭解在中處理隱私權請求時涉及的重要概念 [!DNL Experience Platform]. 若要加深您對如何管理身分資料和建立隱私工作的瞭解，請繼續閱讀本指南中提供的檔案。

有關處理隱私權請求的資訊 [!DNL Platform] 未使用的資源 [!DNL Profile]，請參閱上的檔案 [資料湖中的隱私權請求處理](../catalog/privacy.md).
