---
solution: Experience Platform
title: 匯入和使用外部對象
description: 按照本教學課程瞭解如何搭配Adobe Experience Platform使用外部對象。
exl-id: 56fc8bd3-3e62-4a09-bb9c-6caf0523f3fe
hide: true
hidefromtoc: true
source-git-commit: c83070d85177c72b2e4c4ae472b89c08c20ee743
workflow-type: tm+mt
source-wordcount: '1722'
ht-degree: 0%

---

# 匯入和使用外部對象

>[!IMPORTANT]
>
>本檔案含有舊版Audiences檔案的資訊，因此已經過期。

Adobe Experience Platform支援匯入外部對象的功能，這些對象隨後可用作新對象的元件。 本檔案提供設定Experience Platform以匯入及使用外部對象的教學課程。

## 快速入門

本教學課程需要您實際瞭解各種 [!DNL Adobe Experience Platform] 與建立對象相關的服務。 在開始本教學課程之前，請先檢閱下列服務的檔案：

- [分段服務](../home.md)：可讓您從即時客戶個人檔案資料建立對象。
- [即時客戶個人檔案](../../profile/home.md)：根據來自多個來源的彙總資料，提供統一的即時消費者個人檔案。
- [體驗資料模型(XDM)](../../xdm/home.md)：Platform組織客戶體驗資料的標準化架構。 為善用分段，請確保您的資料已根據 [資料模型化的最佳實務](../../xdm/schema/best-practices.md).
- [資料集](../../catalog/datasets/overview.md)：Experience Platform中資料持續性的儲存和管理結構。
- [串流擷取](../../ingestion/streaming-ingestion/overview.md)：Experience Platform如何即時從使用者端和伺服器端裝置擷取及儲存資料。

### 受眾vs區段定義

開始匯入和使用外部對象之前，請務必瞭解對象和區段定義之間的差異。

對象是指您嘗試篩選的目標設定檔群組。 使用區段定義時，您可以建立區段定義，將您的設定檔篩選為符合區段資格標準的子集，以建立對象。

區段定義包含名稱、說明、運算式（如果適用）、建立日期、上次修改日期及ID等資訊。 ID會將區段中繼資料連結至符合區段資格的個別設定檔，並屬於產生的對象。

| 對象 | 區段定義 |
| --------- | ---------------- |
| 您嘗試尋找的設定檔群組。 使用區段定義時，這表示這會是符合區段資格的設定檔群組。 | 用來區隔您所尋找對象的規則群組。 |

## 為外部對象建立身分名稱空間

使用外部對象的第一個步驟是建立身分名稱空間。 身分名稱空間可讓Platform關聯受眾的來源。

若要建立身分名稱空間，請依照 [身分名稱空間指南](../../identity-service/namespaces.md#manage-namespaces). 建立身分名稱空間時，請將來源詳細資料新增到身分名稱空間中，並標籤其 [!UICONTROL 型別] as a **[!UICONTROL 非人員識別碼]**.

![「建立身分名稱空間」強制回應視窗中會醒目提示非人員識別碼。](../images/tutorials/external-audiences/identity-namespace-info.png)

## 為區段中繼資料建立結構

建立身分名稱空間後，您需要為要建立的區段建立新的結構描述。

若要開始構成方案，請先選取 **[!UICONTROL 方案]** ，然後按一下 **[!UICONTROL 建立結構描述]** 在「方案」工作區的右上角。 從這裡，選擇 **[!UICONTROL 瀏覽]** 以檢視可用綱要型別的完整選擇。

![建立結構描述和瀏覽都會反白顯示。](../images/tutorials/external-audiences/create-schema-browse.png)

由於您正在建立預先定義的類別區段定義，請選取 **[!UICONTROL 使用現有類別]**. 現在，選取 **[!UICONTROL 區段定義]** 類別，後面接著 **[!UICONTROL 指派類別]**.

![區段定義類別會反白顯示。](../images/tutorials/external-audiences/assign-class.png)

現在您的結構描述已建立，您將需要指定哪個欄位將包含區段ID。 此欄位應該標示為主要身分，並指派給您先前建立的名稱空間。

![用於標籤所選欄位為主要身分的核取方塊會在「架構編輯器」中反白顯示。](../images/tutorials/external-audiences/mark-primary-identifier.png)

標示 `_id` 欄位做為主要身分識別，選取結構描述的標題，然後切換標示為 **[!UICONTROL 個人資料]**. 選取 **[!UICONTROL 啟用]** 啟用以下專案的結構描述： [!DNL Real-Time Customer Profile].

![為設定檔啟用架構的切換開關會在「架構編輯器」中反白顯示。](../images/tutorials/external-audiences/schema-profile.png)

現在，此結構描述已針對設定檔啟用，主要身分識別已指派給您建立的非個人身分名稱空間。 因此，這表示使用此結構描述匯入Platform的區段中繼資料將內嵌到設定檔中，而不會與其他人員相關的設定檔資料合併。

## 為結構描述建立資料集

設定結構後，您需要為區段中繼資料建立資料集。

若要建立資料集，請依照 [資料集使用手冊](../../catalog/datasets/user-guide.md#create). 您應遵循 **[!UICONTROL 從結構描述建立資料集]** 選項，使用您先前建立的結構描述。

![您要做為資料集基礎的結構會醒目提示。](../images/tutorials/external-audiences/select-schema.png)

建立資料集後，請繼續按照 [資料集使用手冊](../../catalog/datasets/user-guide.md#enable-profile) 為即時客戶個人檔案啟用此資料集。

![為設定檔啟用架構的切換開關會在「資料集」活動頁面中反白顯示。](../images/tutorials/external-audiences/dataset-profile.png)

## 設定和匯入對象資料

在啟用資料集後，現在可以透過UI或使用Experience Platform API將資料傳送到Platform。 您可以透過批次或串流連線擷取此資料。

### 使用批次連線擷取資料

若要建立批次連線，您可以遵循一般中的指示 [本機檔案上傳UI指南](../../sources/tutorials/ui/create/local-system/local-file-upload.md). 如需可搭配內嵌資料使用的可用來源完整清單，請參閱 [來源概觀](../../sources/home.md).

### 使用串流連線擷取資料

若要建立串流連線，您可以依照 [api教學課程](../../sources/tutorials/api/create/streaming/http.md) 或 [UI教學課程](../../sources/tutorials/ui/create/streaming/http.md).

建立串流連線後，您就可以存取唯一的串流端點，將資料傳送至該端點。 若要瞭解如何傳送資料至這些端點，請閱讀 [串流記錄資料的教學課程](../../ingestion/tutorials/streaming-record-data.md#ingest-data).

![串流連線的串流端點會在來源詳細資訊頁面中強調顯示。](../images/tutorials/external-audiences/get-streaming-endpoint.png)

## 對象中繼資料結構

建立連線後，您現在可以將資料內嵌至Platform。

您可在下方看到外部對象裝載中繼資料的範例：

```json
{
    "header": {
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
            "contentType": "application/vnd.adobe.xed-full+json;version=1"
        },
        "imsOrgId": "{ORG_ID}",
        "datasetId": "{DATASET_ID}",
        "source": {
            "name": "Sample External Audience"
        }
    },
    "body": {
        "xdmMeta": {
            "schemaRef": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
                "contentType": "application/vnd.adobe.xed-full+json;version=1"
            }
        },
        "xdmEntity": {
            "_id": "{SEGMENT_ID}",
            "description": "Sample description",
            "identityMap": {
                "{IDENTITY_NAMESPACE}": [{
                    "id": "{}"
                }]
            },
            "segmentName" : "{SEGMENT_NAME}",
            "segmentStatus": "ACTIVE",
            "version": "1.0"
        }
    }
}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `schemaRef` | 結構描述 **必須** 請參閱先前建立的區段中繼資料結構。 |
| `datasetId` | 資料集ID **必須** 請參閱先前為您剛建立的結構描述建立的資料集。 |
| `xdmEntity._id` | ID **必須** 請參閱您作為外部對象使用的相同區段ID。 |
| `xdmEntity.identityMap` | 本節 **必須** 包含建立先前建立的名稱空間時使用的身分標籤。 |
| `{IDENTITY_NAMESPACE}` | 這是先前建立之身分名稱空間的標籤。 因此，舉例來說，如果您將身分名稱空間稱為「externalAudience」，系統會將其當作陣列的索引鍵。 |
| `segmentName` | 您希望外部對象分段依據的區段名稱。 |

## 使用匯入的對象建立區段

設定好匯入的對象後，就可以在細分程式中使用這些對象。 若要尋找外部對象，請前往「區段產生器」，然後選取 **[!UICONTROL 受眾]** 索引標籤中的 **[!UICONTROL 欄位]** 區段。

![區段產生器中的外部受眾選取器會醒目提示。](../images/tutorials/external-audiences/external-audiences.png)

## 後續步驟

現在，您可以在區段中使用外部對象，您可以使用區段產生器來建立區段。 若要瞭解如何建立區段，請參閱 [有關建立區段的教學課程](./create-a-segment.md).

## 附錄

除了使用匯入的外部受眾中繼資料及使用這些中繼資料建立區段外，您也可以將外部區段會籍匯入至Platform。

### 設定外部區段會籍目的地結構描述

若要開始構成方案，請先選取 **[!UICONTROL 方案]** ，然後按一下 **[!UICONTROL 建立結構描述]** 在「方案」工作區的右上角。 從這裡，選擇 **[!UICONTROL XDM個別設定檔]**.

![「XDM個別輪廓」區域會反白顯示。](../images/tutorials/external-audiences/create-schema-profile.png)

現在已建立結構描述，您將需要新增區段成員資格欄位群組作為結構描述的一部分。 要執行此操作，請選取 [!UICONTROL 區塊會籍細節]，後接 [!UICONTROL 新增欄位群組].

![「區段會籍詳細資訊」欄位群組會醒目顯示。](../images/tutorials/external-audiences/segment-membership-details.png)

此外，請確定結構已標籤為 **[!UICONTROL 個人資料]**. 為此，您需要將欄位標示為主要身分。

![為設定檔啟用架構的切換開關會在「架構編輯器」中反白顯示。](../images/tutorials/external-audiences/external-segment-profile.png)

### 設定資料集

建立結構描述後，您需要建立資料集。

若要建立資料集，請依照 [資料集使用手冊](../../catalog/datasets/user-guide.md#create). 您應遵循 **[!UICONTROL 從結構描述建立資料集]** 選項，使用您先前建立的結構描述。

![您用來建立資料庫的綱要會反白顯示。](../images/tutorials/external-audiences/select-schema.png)

建立資料集後，請繼續按照 [資料集使用手冊](../../catalog/datasets/user-guide.md#enable-profile) 為即時客戶個人檔案啟用此資料集。

![為設定檔啟用架構的切換開關會在「建立資料集」工作流程中反白顯示。](../images/tutorials/external-audiences/dataset-profile.png)

## 設定和匯入外部對象成員資格資料

在啟用資料集後，現在可以透過UI或使用Experience Platform API將資料傳送到Platform。 您可以透過批次或串流連線擷取此資料。

### 使用批次連線擷取資料

若要建立批次連線，您可以遵循一般中的指示 [本機檔案上傳UI指南](../../sources/tutorials/ui/create/local-system/local-file-upload.md). 如需可搭配內嵌資料使用的可用來源完整清單，請參閱 [來源概觀](../../sources/home.md).

### 使用串流連線擷取資料

若要建立串流連線，您可以依照 [api教學課程](../../sources/tutorials/api/create/streaming/http.md) 或 [UI教學課程](../../sources/tutorials/ui/create/streaming/http.md).

建立串流連線後，您就可以存取唯一的串流端點，將資料傳送至該端點。 若要瞭解如何傳送資料至這些端點，請閱讀 [串流記錄資料的教學課程](../../ingestion/tutorials/streaming-record-data.md#ingest-data).

![串流連線的串流端點會在來源詳細資訊頁面中強調顯示。](../images/tutorials/external-audiences/get-streaming-endpoint.png)

## 區段會籍結構

建立連線後，您現在可以將資料內嵌至Platform。

您可在下方看到外部對象成員資格裝載的範例：

```json
{
    "header": {
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
            "contentType": "application/vnd.adobe.xed-full+json;version=1"
        },
        "imsOrgId": "{ORG_ID}",
        "datasetId": "{DATASET_ID}",
        "source": {
            "name": "Sample External Audience Membership"
        }
    },
    "body": {
        "xdmMeta": {
            "schemaRef": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
                "contentType": "application/vnd.adobe.xed-full+json;version=1"
            }
        },
        "xdmEntity": {
            "_id": "{UNIQUE_ID}",
            "description": "Sample description",
            "{TENANT_NAME}": {
                "identities": {
                    "{SCHEMA_IDENTITY}": "sample-id"
                }
            },
            "personId" : "sample-name",
            "segmentMembership": {
                "{IDENTITY_NAMESPACE}": {
                    "{EXTERNAL_IDENTITY}": {
                        "status": "realized",
                        "lastQualificationTime": "2022-03-14T:00:00:00Z"
                    }
                }
            }
        }
    }
}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `schemaRef` | 結構描述 **必須** 請參閱先前建立的結構描述，以瞭解區段成員資格資料。 |
| `datasetId` | 資料集ID **必須** 請參閱先前針對您剛建立的成員資格方案建立的資料集。 |
| `xdmEntity._id` | 適合的ID，用來唯一識別資料集中的記錄。 |
| `{TENANT_NAME}.identities` | 此區段用於連線自訂身分的欄位群組與您先前匯入的使用者。 |
| `segmentMembership.{IDENTITY_NAMESPACE}` | 這是先前建立之自訂身分名稱空間的標籤。 因此，舉例來說，如果您將身分名稱空間稱為「externalAudience」，系統會將其當作陣列的索引鍵。 |

>[!NOTE]
>
>依預設，外部對象成員資格會在30天後刪除。 若要防止刪除並保留30天以上，請使用 `validUntil` 欄位擷取您的對象資料。 如需有關本欄位的詳細資訊，請閱讀以下指南： [區段會籍詳細資料結構欄位群組](../../xdm/field-groups/profile/segmentation.md).
