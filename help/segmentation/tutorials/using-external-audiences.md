---
keywords: Experience Platform；首頁；熱門主題
solution: Experience Platform
title: 導入和使用外部受眾
description: 請按照本教程學習如何與Adobe Experience Platform一起使用外部觀眾。
exl-id: 56fc8bd3-3e62-4a09-bb9c-6caf0523f3fe
source-git-commit: 57586104f1119f5cda926faf286c1663fbb0b240
workflow-type: tm+mt
source-wordcount: '1664'
ht-degree: 0%

---

# 導入和使用外部受眾

Adobe Experience Platform支援引進外部受眾的能力，這些受眾隨後可用作新段定義的元件。 本文檔提供了設定導入和使用外部受眾的Experience Platform的教程。

## 快速入門

本教程需要對各種 [!DNL Adobe Experience Platform] 服務。 在開始本教程之前，請查看以下服務的文檔：

- [分段服務](../home.md):允許您從即時客戶配置檔案資料構建受眾段。
- [即時客戶配置檔案](../../profile/home.md):基於來自多個源的聚合資料提供統一、即時的用戶配置檔案。
- [體驗資料模型(XDM)](../../xdm/home.md):平台組織客戶體驗資料的標準化框架。 為最好地利用分段，請確保根據 [資料建模的最佳做法](../../xdm/schema/best-practices.md)。
- [資料集](../../catalog/datasets/overview.md):Experience Platform中資料持久性的儲存和管理結構。
- [流攝入](../../ingestion/streaming-ingestion/overview.md):Experience Platform如何即時接收和儲存來自客戶端和伺服器端設備的資料。

### 段資料與段元資料

在開始導入和使用外部訪問群體之前，瞭解段資料和段元資料之間的差異非常重要。

段資料是指符合段資格標準的配置檔案，因此是受眾的一部分。

段元資料是有關段本身的資訊，包括名稱、說明、表達式（如果適用）、建立日期、上次修改日期和ID。 該ID將段元資料連結到滿足段限定並且是所產生受眾的一部分的單個配置檔案。

| 段資料 | 段元資料 |
| ------------ | ---------------- |
| 符合段資格的配置檔案 | 有關段本身的資訊 |

## 為外部訪問群體建立標識命名空間

使用外部受眾的第一步是建立標識命名空間。 標識命名空間允許平台關聯段的來源。

要建立標識命名空間，請按照 [標識命名空間指南](../../identity-service/namespaces.md#manage-namespaces)。 建立標識命名空間時，將源詳細資訊添加到標識命名空間，並標籤其 [!UICONTROL 類型] 作為 **[!UICONTROL 非人員標識符]**。

![非人員標識符在「建立標識名稱空間」模式中突出顯示。](../images/tutorials/external-audiences/identity-namespace-info.png)

## 為段元資料建立架構

建立標識命名空間後，需要為要建立的段建立新架構。

要開始合成架構，請首先選擇 **[!UICONTROL 架構]** 在左導航欄上，然後是 **[!UICONTROL 建立架構]** 在「架構」工作區的右上角。 從此處，選擇 **[!UICONTROL 瀏覽]** 查看可用架構類型的完整選擇。

![「建立架構」和「瀏覽」都突出顯示。](../images/tutorials/external-audiences/create-schema-browse.png)

由於要建立段定義（即預定義類），因此請選擇 **[!UICONTROL 使用現有類]**。 現在，選擇 **[!UICONTROL 段定義]** 類，後跟 **[!UICONTROL 分配類]**。

![段定義類被加亮顯示。](../images/tutorials/external-audiences/assign-class.png)

既然您的架構已建立，則需要指定包含段ID的欄位。 此欄位應標籤為主標識並分配給您以前建立的命名空間。

![將選定欄位標籤為主標識的複選框在架構編輯器中突出顯示。](../images/tutorials/external-audiences/mark-primary-identifier.png)

標籤 `_id` 欄位作為主標識，選擇架構的標題，然後按標有的切換 **[!UICONTROL 配置檔案]**。 選擇 **[!UICONTROL 啟用]** 為 [!DNL Real-Time Customer Profile]。

![在「架構編輯器」中，突出顯示了啟用概要檔案架構的切換。](../images/tutorials/external-audiences/schema-profile.png)

現在，此架構已為配置檔案啟用，並且主標識已分配給您建立的非人員標識命名空間。 因此，這意味著使用此架構導入到平台中的段元資料將被導入到配置檔案中，而不會與其他與人員相關的配置檔案資料合併。

## 為架構建立資料集

配置架構後，您需要為段元資料建立資料集。

要建立資料集，請按照 [資料集使用手冊](../../catalog/datasets/user-guide.md#create)。 您應該 **[!UICONTROL 從架構建立資料集]** 選項，使用先前建立的架構。

![要基於資料集的架構將突出顯示。](../images/tutorials/external-audiences/select-schema.png)

建立資料集後，繼續按照 [資料集使用手冊](../../catalog/datasets/user-guide.md#enable-profile) 為Real-Time Customer Profile啟用此資料集。

![在「資料集」活動頁中，突出顯示了啟用概要檔案架構的切換。](../images/tutorials/external-audiences/dataset-profile.png)

## 設定和導入受眾資料

啟用資料集後，現在可以通過UI或使用Experience PlatformAPI將資料發送到平台。 您可以通過批處理連接或流式處理連接接收此資料。

### 使用批處理連接接收資料

要建立批處理連接，可以按照通用 [本地檔案上載UI指南](../../sources/tutorials/ui/create/local-system/local-file-upload.md)。 有關可用源的完整清單，請閱讀 [源概述](../../sources/home.md)。

### 使用流連接接收資料

要建立流連接，可以按照 [API教程](../../sources/tutorials/api/create/streaming/http.md) 或 [UI教程](../../sources/tutorials/ui/create/streaming/http.md)。

建立流連接後，您將有權訪問唯一的流終結點，您可以將資料發送到該終結點。 要瞭解如何向這些端點發送資料，請閱讀 [流記錄資料教程](../../ingestion/tutorials/streaming-record-data.md#ingest-data)。

![流連接的流終結點在源詳細資訊頁中突出顯示。](../images/tutorials/external-audiences/get-streaming-endpoint.png)

## 受眾元資料結構

建立連接後，您現在可以將資料接收到平台。

以下是外部受眾負載元資料的示例：

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
| `schemaRef` | 架構 **必須** 請參閱先前為段元資料建立的架構。 |
| `datasetId` | 資料集ID **必須** 請參考您剛剛建立的架構先前建立的資料集。 |
| `xdmEntity._id` | ID **必須** 請參閱與外部受眾使用的相同段ID。 |
| `xdmEntity.identityMap` | 此部分 **必須** 包含建立以前建立的命名空間時使用的標識標籤。 |
| `{IDENTITY_NAMESPACE}` | 這是先前建立的標識命名空間的標籤。 因此，例如，如果您將標識名稱空間稱為「externalAuviences」，則會將其用作陣列的鍵。 |
| `segmentName` | 希望將外部受眾分割的段的名稱。 |

## 使用導入的受眾構建段

一旦建立了導入的受眾，就可以將其用作分割過程的一部分。 要查找外部受眾，請轉到段生成器，然後選擇 **[!UICONTROL 觀眾]** 的 **[!UICONTROL 欄位]** 的子菜單。

![「段生成器」中的外部訪問群體選擇器將突出顯示。](../images/tutorials/external-audiences/external-audiences.png)

## 後續步驟

現在，您可以在段中使用外部訪問群體，可以使用段生成器建立段。 要瞭解如何建立段，請閱讀 [建立段的教程](./create-a-segment.md)。

## 附錄

除了使用導入的外部訪問群體元資料並使用它們建立段外，還可以將外部段成員資格導入平台。

### 設定外部段成員身份目標架構

要開始合成架構，請首先選擇 **[!UICONTROL 架構]** 在左導航欄上，然後是 **[!UICONTROL 建立架構]** 在「架構」工作區的右上角。 從此處，選擇 **[!UICONTROL XDM個人配置檔案]**。

![「XDM單個輪廓」(XDM Individual Profile)區域被加亮。](../images/tutorials/external-audiences/create-schema-profile.png)

既然已建立了架構，則需要將段成員身份欄位組添加為架構的一部分。 要執行此操作，請選擇 [!UICONTROL 段成員身份詳細資訊]，後跟 [!UICONTROL 添加欄位組]。

![「段成員身份詳細資訊」欄位組將突出顯示。](../images/tutorials/external-audiences/segment-membership-details.png)

此外，確保將架構標籤為 **[!UICONTROL 配置檔案]**。 要執行此操作，您需要將欄位標籤為主標識。

![在「架構編輯器」中，突出顯示了啟用概要檔案架構的切換。](../images/tutorials/external-audiences/external-segment-profile.png)

### 設定資料集

建立架構後，需要建立資料集。

要建立資料集，請按照 [資料集使用手冊](../../catalog/datasets/user-guide.md#create)。 您應該 **[!UICONTROL 從架構建立資料集]** 選項，使用先前建立的架構。

![將突出顯示您用於建立資料庫的架構。](../images/tutorials/external-audiences/select-schema.png)

建立資料集後，繼續按照 [資料集使用手冊](../../catalog/datasets/user-guide.md#enable-profile) 為Real-Time Customer Profile啟用此資料集。

![在建立資料集工作流中突出顯示了啟用配置檔案架構的切換。](../images/tutorials/external-audiences/dataset-profile.png)

## 設定和導入外部受眾成員身份資料

啟用資料集後，現在可以通過UI或使用Experience PlatformAPI將資料發送到平台。 您可以通過批處理連接或流式處理連接接收此資料。

### 使用批處理連接接收資料

要建立批處理連接，可以按照通用 [本地檔案上載UI指南](../../sources/tutorials/ui/create/local-system/local-file-upload.md)。 有關可用源的完整清單，請閱讀 [源概述](../../sources/home.md)。

### 使用流連接接收資料

要建立流連接，可以按照 [API教程](../../sources/tutorials/api/create/streaming/http.md) 或 [UI教程](../../sources/tutorials/ui/create/streaming/http.md)。

建立流連接後，您將有權訪問唯一的流終結點，您可以將資料發送到該終結點。 要瞭解如何向這些端點發送資料，請閱讀 [流記錄資料教程](../../ingestion/tutorials/streaming-record-data.md#ingest-data)。

![流連接的流終結點在源詳細資訊頁中突出顯示。](../images/tutorials/external-audiences/get-streaming-endpoint.png)

## 段成員結構

建立連接後，您現在可以將資料接收到平台。

以下是外部受眾成員有效負載的示例：

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
| `schemaRef` | 架構 **必須** 請參閱先前建立的段成員身份資料的架構。 |
| `datasetId` | 資料集ID **必須** 請參考您剛剛建立的成員資格架構先前建立的資料集。 |
| `xdmEntity._id` | 用於唯一標識資料集內記錄的合適ID。 |
| `{TENANT_NAME}.identities` | 此部分用於將自定義標識的欄位組與先前導入的用戶連接。 |
| `segmentMembership.{IDENTITY_NAMESPACE}` | 這是先前建立的自定義標識命名空間的標籤。 因此，例如，如果您將標識名稱空間稱為「externalAuviences」，則會將其用作陣列的鍵。 |

>[!NOTE]
>
>預設情況下，外部訪問群組成員僅保留30天。 若要將其保留超過30天，請使用 `validUntil` 的子菜單。 有關此欄位的詳細資訊，請閱讀上的指南 [段成員身份詳細資訊架構欄位組](../../xdm/field-groups/profile/segmentation.md)。