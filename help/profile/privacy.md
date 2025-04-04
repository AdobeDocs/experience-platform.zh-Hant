---
keywords: Experience Platform；首頁；熱門主題
solution: Experience Platform
title: 即時客戶個人檔案中的隱私權請求處理
type: Documentation
description: Adobe Experience Platform Privacy Service會根據多項隱私權法規的規定，處理客戶存取、選擇退出銷售或刪除其個人資料的請求。 本檔案說明與處理即時客戶個人檔案的隱私權請求相關的重要概念。
exl-id: fba21a2e-aaf7-4aae-bb3c-5bd024472214
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1751'
ht-degree: 1%

---

# 在[!DNL Real-Time Customer Profile]中處理隱私權請求

Adobe Experience Platform [!DNL Privacy Service]會根據一般資料保護規範(GDPR)和[!DNL California Consumer Privacy Act] (CCPA)等隱私權法規，處理客戶存取、選擇退出銷售或刪除其個人資料的請求。

本檔案說明在Adobe Experience Platform中處理[!DNL Real-Time Customer Profile]隱私權要求的相關基本概念。

>[!NOTE]
>
>本指南僅涵蓋如何在Experience Platform中向設定檔資料存放區提出隱私權請求。 如果您也打算提出Experience Platform資料湖的隱私權請求，除了本教學課程外，另請參閱資料湖](../catalog/privacy.md)中[隱私權請求處理指南。
>
>如需如何對其他Adobe Experience Cloud應用程式提出隱私權要求的步驟，請參閱[Privacy Service檔案](../privacy-service/experience-cloud-apps.md)。

>[!IMPORTANT]
>
>本指南中的隱私權要求&#x200B;**不**&#x200B;涵蓋B2B非個人實體。

## 快速入門

本指南需要您實際瞭解下列[!DNL Experience Platform]個元件：

* [[!DNL Privacy Service]](../privacy-service/home.md)：管理客戶透過Adobe Experience Cloud應用程式存取、選擇退出銷售或刪除其個人資料的請求。
* [[!DNL Identity Service]](../identity-service/home.md)：透過跨裝置和系統橋接身分，解決客戶體驗資料分散所造成的根本挑戰。
* [[!DNL Real-Time Customer Profile]](home.md)：根據來自多個來源的彙總資料，提供統一的即時消費者設定檔。

## 了解身分識別命名空間 {#namespaces}

Adobe Experience Platform [!DNL Identity Service]可跨系統和裝置橋接客戶身分資料。 [!DNL Identity Service]使用&#x200B;**身分識別名稱空間**，透過將身分識別值與其來源系統建立關聯來提供身分識別值的內容。 名稱空間可代表一般概念，例如電子郵件地址（「電子郵件」），或將身分與特定應用程式相關聯，例如Adobe Advertising Cloud ID (「AdCloud」)或Adobe Target ID (「TNTID」)。

Identity Service維護全域定義（標準）和使用者定義（自訂）的身分名稱空間之存放區。 標準名稱空間適用於所有組織（例如「Email」和「ECID」），而您的組織也可以建立自訂名稱空間以滿足其特定需求。

如需[!DNL Experience Platform]中識別名稱空間的詳細資訊，請參閱[識別名稱空間概觀](../identity-service/features/namespaces.md)。

## 提交請求 {#submit}

以下各節概述如何使用[!DNL Privacy Service] API或UI為[!DNL Real-Time Customer Profile]提出隱私權請求。 在閱讀這些章節之前，您應該檢閱或瞭解[Privacy Service API](../privacy-service/api/getting-started.md)或[Privacy Service UI](../privacy-service/ui/overview.md)檔案。 這些檔案提供如何提交隱私權工作的完整步驟，包括如何在請求裝載中正確格式化提交的使用者身分資料。

>[!IMPORTANT]
>
>Privacy Service只能使用不會執行身分拼接的合併原則來處理[!DNL Profile]資料。 如需詳細資訊，請參閱[合併原則限制](#merge-policy-limitations)的相關章節。
>
>請注意，隱私權請求是根據法規要求以非同步方式處理，完成所需時間會有所不同。 如果當要求仍在處理時，您的[!DNL Profile]資料發生變更，則無法保證這些傳入記錄也會在該要求中處理。 只有在請求隱私權工作時，儲存在Data Lake或設定檔存放區中的設定檔才會被刪除。 如果您在刪除工作期間擷取與刪除請求主題相關的設定檔資料，並不保證會刪除所有設定檔片段。
>您有責任在刪除請求時留意Experience Platform或設定檔服務中的任何傳入資料，因為這些資料將會插入記錄存放區。 您必須審慎擷取已刪除或正在刪除的資料。

### 使用 API

在API中建立工作要求時，`userIDs`內提供的任何ID都必須使用特定的`namespace`和`type`。 必須提供[!DNL Identity Service]識別的有效[身分名稱空間](#namespaces)以供`namespace`值使用，而`type`必須是`standard`或`unregistered` （分別用於標準與自訂名稱空間）。

>[!NOTE]
>
>您可能需要為每個客戶提供多個ID，具體取決於身分圖表和您的設定檔片段在Experience Platform資料集中的分配方式。 如需詳細資訊，請參閱下一節[設定檔片段](#fragments)。

此外，請求承載的`include`陣列必須包含請求所針對的不同資料存放區的產品值。 若要刪除與識別相關聯的設定檔資料，陣列必須包含值`ProfileService`。 若要刪除客戶的身分圖表關聯，陣列必須包含值`identity`。

>[!NOTE]
>
>如需在`include`陣列中使用`ProfileService`和`identity`之影響的詳細資訊，請參閱本檔案後面有關[設定檔要求與身分要求](#profile-v-identity)的章節。

以下請求會針對[!DNL Profile]存放區中的單一客戶資料建立新的隱私權工作。 在`userIDs`陣列中為客戶提供了兩個身分值；一個使用標準`Email`身分名稱空間，另一個使用自訂`Customer_ID`名稱空間。 它也會包含`include`陣列中[!DNL Profile] (`ProfileService`)的產品值：

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
>Experience Platform會處理屬於您組織的所有[沙箱](../sandboxes/home.md)的隱私權請求。 因此，請求中包含的任何`x-sandbox-name`標頭都會被系統忽略。

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

在UI中建立工作請求時，請務必在&#x200B;**[!UICONTROL 產品]**&#x200B;下選取&#x200B;**[!UICONTROL AEP Data Lake]**&#x200B;和/或&#x200B;**[!UICONTROL 設定檔]**，以便分別處理儲存在Data Lake或[!DNL Real-Time Customer Profile]中的資料工作。

![在UI中建立存取工作請求，並在[產品]下選取[設定檔]選項](./images/privacy/product-value.png)

## 隱私權請求中的設定檔片段 {#fragments}

在[!DNL Profile]資料存放區中，個別客戶的個人資料通常會由多個設定檔片段組成，這些片段會透過身分圖表與個人建立關聯。 向[!DNL Profile]存放區提出隱私權請求時，請務必注意，請求僅會在設定檔片段層級上處理，而不是在整個設定檔上處理。

例如，假設您要將客戶屬性資料儲存在三個個別的資料集中，並使用不同的識別碼將該資料與個別客戶建立關聯：

| 資料集名稱 | 主要身分識別欄位 | 已儲存的屬性 |
| --- | --- | --- |
| 資料集1 | `customer_id` | `address` |
| 資料集2 | `email_id` | `firstName`、`lastName` |
| 資料集3 | `email_id` | `mlScore` |

其中一個資料集使用`customer_id`作為其主要識別碼，而其他兩個資料集則使用`email_id`。 如果您只使用`email_id`做為使用者ID值來傳送隱私權要求（存取或刪除），則只會處理`firstName`、`lastName`和`mlScore`屬性，而`address`則不受影響。

為確保您的隱私權請求可處理所有相關客戶屬性，您必須為可能儲存這些屬性的所有適用資料集提供主要身分值（每位客戶最多九個ID）。 如需通常標籤為身分的欄位詳細資訊，請參閱結構描述組合](../xdm/schema/composition.md#identity)的[基本概念中的身分欄位相關章節。

## 正在處理刪除請求 {#delete}

當[!DNL Experience Platform]收到來自[!DNL Privacy Service]的刪除請求時，[!DNL Experience Platform]會傳送確認給[!DNL Privacy Service]，確認已收到該請求且受影響的資料已標示為刪除。 隱私權工作完成後，記錄即會被移除。

>[!IMPORTANT]
>
>隱私權刪除請求並非立即提出，而且可能會因所涉及的服務及其他影響因素（例如地理位置）而有所不同。 完成隱私權工作的時間範圍可以是15至45天，但不保證一定會完成。

視您是否也在設定檔(`ProfileService`)的隱私權要求中納入身分識別服務(`identity`)和資料湖(`aepDataLake`)作為產品而定，與設定檔相關的不同資料集，可能會在不同的時間從系統中移除：

| 包含的產品 | 效果 |
| --- | --- |
| 僅`ProfileService` | 當Experience Platform傳送確認已收到刪除請求時，會立即刪除設定檔。 不過，設定檔的身分圖表仍會保留，並且隨著擷取具有相同身分的新資料，可能會重建設定檔。 與設定檔相關聯的資料也會保留在資料湖中。 |
| `ProfileService` 和 `identity` | 當Experience Platform傳送確認已收到刪除請求時，會立即刪除設定檔及其關聯的身分圖表。 與設定檔相關聯的資料會保留在資料湖中。 |
| `ProfileService` 和 `aepDataLake` | 當Experience Platform傳送確認已收到刪除請求時，會立即刪除設定檔。 不過，設定檔的身分圖表仍會保留，並且隨著擷取具有相同身分的新資料，可能會重建設定檔。<br><br>當Data Lake產品回應收到要求且目前正在處理時，與設定檔關聯的資料會軟刪除，因此無法由任何[!DNL Experience Platform]服務存取。 工作完成後，資料會從資料湖中完全移除。 |
| `ProfileService`、`identity`和`aepDataLake` | 當Experience Platform傳送確認已收到刪除請求時，會立即刪除設定檔及其關聯的身分圖表。<br><br>當Data Lake產品回應收到要求且目前正在處理時，與設定檔關聯的資料會軟刪除，因此無法由任何[!DNL Experience Platform]服務存取。 工作完成後，資料會從資料湖中完全移除。 |

如需追蹤工作狀態的詳細資訊，請參閱[[!DNL Privacy Service] 檔案](../privacy-service/home.md#monitor)。

### 設定檔請求與身分請求 {#profile-v-identity}

如果對設定檔(`ProfileService`)而不是身分識別服務(`identity`)提出刪除請求，則產生的工作會移除為客戶（或一組客戶）收集的屬性資料，但不會移除在身分識別圖形中建立的關聯。

例如，使用客戶的`email_id`和`customer_id`的刪除請求會移除儲存在這些ID下的所有屬性資料。 不過，之後在同一`customer_id`下擷取的任何資料仍將與適當的`email_id`相關聯，因為該關聯仍然存在。

若要移除指定客戶的設定檔和所有身分關聯，請確定刪除請求中同時包含設定檔和身分識別服務作為目標產品。

### 合併原則限制 {#merge-policy-limitations}

Privacy Service只能使用不會執行身分拼接的合併原則來處理[!DNL Profile]資料。 如果您使用UI來確認您的隱私權請求是否正在處理中，請確定您使用包含&#x200B;**[!DNL None]**&#x200B;作為其[!UICONTROL ID拼接]型別的原則。 換言之，您無法使用[!UICONTROL ID拼接]設定為[!UICONTROL 私人圖表]的合併原則。

>![合併原則的ID拼接設定為None](./images/privacy/no-id-stitch.png)

## 後續步驟

閱讀本檔案後，您已經瞭解在[!DNL Experience Platform]中處理隱私權要求的重要概念。 若要加深您對如何管理身分資料和建立隱私工作的瞭解，請繼續閱讀本指南中提供的檔案。

如需處理[!DNL Profile]未使用之[!DNL Experience Platform]資源的隱私權要求的相關資訊，請參閱有關[在資料湖](../catalog/privacy.md)中處理隱私權要求的檔案。
